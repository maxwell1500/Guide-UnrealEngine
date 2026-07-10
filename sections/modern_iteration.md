## Modern Actor Iteration

Iterating over actors in a world is a common task. UE5 introduced several modern approaches that are safer and more efficient than the old `ForEachActor` loop.

### TActorRange (UE5.1+)

The recommended way to iterate actors in UE5.1+ is `TActorRange`. It's a range-based for loop that works with any actor class:

```cpp
// Iterate all actors of a specific class
for (AMyActor* Actor : TActorRange<AMyActor>(GetWorld()))
{
    // Do something with Actor
}

// Filter by a specific actor instance
for (AMyActor* Actor : TActorRange<AMyActor>(GetWorld(), MySpecificActor))
{
    // Only matches MySpecificActor
}

// Iterate all actors in a level
for (AActor* Actor : TActorRange<AActor>(GetWorld()))
{
    // Do something with any actor
}
```

You can also filter by component:

```cpp
// Iterate all actors that have a specific component type
for (AActor* Actor : TActorRange<AActor>(GetWorld(), FActorPredicateIncludeComponents<USceneComponent>{}))
{
    // Only actors with USceneComponent
}
```

### TObjectIterator

For iterating **all** objects of any class (not just actors), use `TObjectIterator`:

```cpp
// Iterate all UStaticMesh objects in the engine
for (UStaticMesh* Mesh : TObjectIterator<UStaticMesh>())
{
    UE_LOG(LogTemp, Log, TEXT("Found mesh: %s"), *Mesh->GetName());
}

// Skip pending kill objects (objects marked for deletion)
for (UStaticMesh* Mesh : TObjectIterator<UStaticMesh>(EObjectIteration::SkipPendingKill))
{
    // Safe — won't return objects being garbage collected
}

// Skip objects that are being loaded from disk
for (UStaticMesh* Mesh : TObjectIterator<UStaticMesh>(EObjectIteration::SkipLoadingObjects))
{
    // Only fully loaded objects
}
```

### Old-style ForEachActor (legacy)

The old `TActorIterator` and `UGameplayStatics::GetAllActorsOfClass` still work but are less flexible:

```cpp
// Legacy — still works but TActorRange is preferred
TActorIterator<AMyActor> It(GetWorld());
while (It++)
{
    AMyActor* Actor = *It;
}

// Even older — spawns a TArray, uses more memory
TArray<AMyActor*> Actors;
UGameplayStatics::GetAllActorsOfClass(GetWorld(), AMyActor::StaticClass(), Actors);
```

### Best Practices

- **Use `TActorRange`** for actor iteration — it's clean, efficient, and supports filtering.
- **Always check `IsValid()`** when iterating actors that might be destroyed during the loop.
- **Avoid `GetAllActorsOfClass`** in performance-critical code — it allocates a TArray every time.
- **Use `TObjectIterator`** for engine-wide searches (all meshes, all materials, etc.).
- **Skip pending kill objects** with `EObjectIteration::SkipPendingKill` to avoid crashes.
