## Async Loading & Asset Streaming

Loading assets synchronously blocks the game thread. UE provides several systems for loading assets asynchronously to keep the game running smoothly.

### FStreamableManager

The `FStreamableManager` is the modern way to load assets asynchronously in UE5:

```cpp
#include "Engine/StreamableManager.h"

// Get the streamable manager from the world
FStreamableManager& StreamableManager = UGameplayStatics::GetStreamableManager();

// Async load a single asset
FSoftObjectPath AssetPath(TEXT("/Game/MyAssets/MyMesh.MyMesh"));
StreamableManager.RequestAsyncLoad(
    AssetPath,
    FStreamableDelegate::CreateLambda([this]()
    {
        // Called when loading is complete
        UE_LOG(LogTemp, Log, TEXT("Asset loaded!"));
    })
);

// Get the loaded object (call after RequestAsyncLoad completes)
UStaticMesh* Mesh = Cast<UStaticMesh>(AssetPath.ResolveObject());
```

### FStreamableHandle

For more control, use `FStreamableHandle`:

```cpp
// Request async load and keep a handle
FStreamableHandle* Handle = StreamableManager.RequestAsyncLoad(
    AssetPath,
    FStreamableDelegate::CreateWeakLambda(this, [this]()
    {
        // Loading complete — do something
    }),
    FStreamableManager::DefaultAsyncLoadPriority
);

// Check progress
float Progress = Handle->GetProgress(); // 0.0 to 1.0

// Cancel the load if needed
Handle->CancelHandle();

// Force synchronous wait (blocks until loaded)
Handle->WaitForCompletion();
```

### LoadObject (synchronous, but simple)

For quick loads where blocking is acceptable:

```cpp
// Synchronous load — blocks until complete
UStaticMesh* Mesh = LoadObject<UStaticMesh>(nullptr, TEXT("/Game/MyAssets/MyMesh.MyMesh"));

// Check if load succeeded
if (Mesh && !Mesh->IsPendingInitialization())
{
    // Safe to use
}
```

### Soft Object References + Async Loading

Soft references pair naturally with async loading:

```cpp
UPROPERTY()
TSoftObjectPtr<UStaticMesh> SoftMesh;

// In a function:
void MyActor::LoadMeshAsync()
{
    FStreamableManager& Streamable = UGameplayStatics::GetStreamableManager();
    
    Streamable.RequestAsyncLoad(
        SoftMesh.ToSoftObjectPath(),
        FStreamableDelegate::CreateWeakLambda(this, [this]()
        {
            // Mesh is now loaded — get the hard reference
            UStaticMesh* LoadedMesh = SoftMesh.Get();
            if (LoadedMesh)
            {
                // Use it
            }
        })
    );
}

// Or load synchronously when you need it immediately:
UStaticMesh* MyActor::GetLoadedMesh()
{
    if (SoftMesh.IsNull()) return nullptr;
    
    FStreamableManager& Streamable = UGameplayStatics::GetStreamableManager();
    return Cast<UStaticMesh>(Streamable.LoadSynchronous(SoftMesh.ToSoftObjectPath()));
}
```

### Loading Levels

For streaming levels asynchronously:

```cpp
// Async load a level
UGameplayStatics::LoadStreamLevel(GetWorld(), TEXT("Level_MyLevel"), false, true);

// The level is now loading in the background. Check progress:
UWorld* LoadedWorld = UGameplayStatics::GetLoadedStreamLevel(GetWorld(), TEXT("Level_MyLevel"));
if (LoadedWorld)
{
    // Level is ready — transition to it
    UGameplayStatics::OpenLevel(GetWorld(), TEXT("Level_MyLevel"));
}
```

### Best Practices

- **Use `FStreamableManager`** for asset loading — it handles reference counting and can load multiple assets in parallel.
- **Use soft references** (`TSoftObjectPtr`) to store asset paths without loading them immediately.
- **Always check if the loaded object is valid** before using it — async loads can fail.
- **Don't block the game thread** for large assets — use `RequestAsyncLoad` with callbacks.
- **Use `LoadSynchronous`** only when you need an asset immediately and can afford to wait.
- **Unload unused assets** by letting soft references go out of scope or calling `StreamableManager.Unload()`.
