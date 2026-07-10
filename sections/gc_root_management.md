## Garbage Collection & Root Management

UE's garbage collector automatically cleans up `UObject` instances that are no longer referenced. Understanding how GC works is essential for preventing memory leaks and dangling references.

### How GC Works

The UE garbage collector:
1. **Marks** all objects reachable from root objects (world, game instance, etc.)
2. **Sweeps** unmarked objects — destroys them and cleans up references
3. Runs periodically during gameplay (controlled by console variables)

Objects that are "rooted" will never be garbage collected. This is intentional — you need to keep important objects alive.

### AddToRoot / RemoveFromRoot

The simplest way to prevent GC:

```cpp
// Keep this object alive forever
MyObject->AddToRoot();

// Later, allow it to be garbage collected
MyObject->RemoveFromRoot();
```

This is simple but blunt — the object will **never** be collected, even if nothing references it. Use sparingly.

### FGCRootTracker (UE5+)

The modern approach uses `FGCRootTracker` for scoped root management:

```cpp
#include "Misc/RootSet.h"

void MyActor::KeepObjectAlive()
{
    // Create a tracked root — object stays alive while this scope is active
    FGCRootTracker::AddRoot(MyObject);
    
    // ... do work ...
    
    // Object can be collected again when this function returns
    FGCRootTracker::RemoveRoot(MyObject);
}
```

For scoped management, use RAII:

```cpp
#include "Misc/RootSet.h"

struct FScopedRoot
{
    UObject* Object;
    FScopedRoot(UObject* Obj) : Object(Obj) { FGCRootTracker::AddRoot(Object); }
    ~FScopedRoot() { FGCRootTracker::RemoveRoot(Object); }
};

void MyActor::TemporarilyKeepAlive()
{
    FScopedRoot Root(MyObject);
    
    // MyObject is rooted here — won't be GC'd
    
    // Do async work, callbacks, etc.
    
    // MyObject can be collected when this scope exits
}
```

### UObject::AddToRoot() vs FGCRootTracker

| Approach | Lifetime | Use Case |
|----------|----------|----------|
| `AddToRoot()` | Forever (until `RemoveFromRoot()`) | Singletons, global managers |
| `FGCRootTracker` | Scoped (manual or RAII) | Temporary roots, async callbacks |
| `UPROPERTY()` | Automatic (tracked by GC) | Normal references |

### Checking Object Validity

Always check if an object is valid before using it:

```cpp
// Check if object is still alive (not pending kill)
if (MyObject && !MyObject->IsPendingKill())
{
    // Safe to use
}

// For UObject pointers, the pointer itself may be non-null but the object could be pending kill
if (IsValid(MyObject))
{
    // UE's IsValid macro checks both non-null and not pending kill
}
```

### Common GC Pitfalls

**1. Static UObject pointers**

Static variables are not tracked by GC:

```cpp
// BAD — static UObject pointer, GC won't track it
static UMyObject* GlobalObject;

// GOOD — use AddToRoot or a subsystem
UPROPERTY()
UMyObject* GlobalObject; // In a persistent class like UGameInstance
```

**2. Raw C++ pointers to UObject**

Raw pointers don't prevent GC:

```cpp
// BAD — MyObject can be GC'd while this pointer is dangling
UMyObject* MyObject = NewObject<UMyObject>();
SomeStruct.RawPtr = &MyObject;

// GOOD — use TWeakObjectPtr or UPROPERTY()
TWeakObjectPtr<UMyObject> WeakRef(MyObject);
```

**3. Delegates keeping references**

Dynamic delegates bound with `BindDynamic` or `AddDynamic` keep weak references, so they won't prevent GC. But raw pointer bindings (`BindRaw`) can cause dangling references:

```cpp
// BAD — if Target is GC'd, delegate fires a dangling pointer
MyDelegate.BindRaw(Target, &TargetClass::MyFunction);

// GOOD — UObject delegates use weak references
MyDelegate.AddUObject(Target, &TargetClass::MyFunction);
```

### GC Tuning

You can adjust GC behavior with console variables:

```ini
[Core]
; Number of frames between GC passes (default: 1)
r.GC.MaxFPS=30

; Enable/disable GC during gameplay
gc.FlushStreamingOnGC=1

; Debug: print objects being collected
gc.Debug=1
```

### Best Practices

- **Use `UPROPERTY()`** for references that should keep objects alive — GC tracks them automatically.
- **Use `TWeakObjectPtr`** for references that shouldn't prevent GC.
- **Use `FGCRootTracker`** for temporary roots (async callbacks, scoped operations).
- **Avoid `AddToRoot()`** unless you truly need an object to live forever.
- **Always check `IsValid()`** before using objects that might be collected.
- **Never store raw C++ pointers to `UObject`** without a corresponding `UPROPERTY()` or weak reference.
