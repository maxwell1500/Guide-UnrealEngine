## PCG (Procedural Content Generation) Framework

The PCG Framework is UE5's built-in system for procedural generation. It uses a node-based graph editor to define rules for spawning, filtering, and attributing content across levels and worlds.

### Core Concepts

PCG works with three main components:

1. **PCG Graph** — A node-based definition of procedural rules (where to spawn, what to spawn, how to filter).
2. **PCG Component** — An actor component that executes a PCG graph at runtime or in the editor.
3. **PCG Data** — The data structures that flow through the graph (spawned actors, points, attributes).

### Creating a PCG Graph

In the Content Browser:
1. Right-click → **PCG** → **PCG Graph**
2. Open the graph in the PCG Graph Editor
3. Add nodes for:
   - **Data Source** — where to generate points (grid, scatter, along spline, etc.)
   - **Filter** — remove or keep certain points (by distance, by tag, by attribute)
   - **Spawner** — spawn actors at the remaining points
   - **Attribution** — assign properties to generated points (scale, rotation, material variant)

### Using PCG in C++

```cpp
#include "PCGComponent.h"
#include "PCGGraph.h"

// In your header:
UPROPERTY(EditAnywhere, Category = "PCG")
TSoftObjectPtr<UPCGGraph> PCGGraphAsset;

// In your .cpp:
void AMyPCGActor::BeginPlay()
{
    Super::BeginPlay();

    if (UPCGComponent* PCGComponent = FindComponentByClass<UPCGComponent>())
    {
        // Set the graph to execute
        if (!PCGGraphAsset.IsNull())
        {
            UPGC* Graph = Cast<UPGC>(PCGGraphAsset.LoadSynchronous());
            if (Graph)
            {
                PCGComponent->SetGraph(Graph);
            }
        }

        // Execute the graph
        PCGComponent->Execute();
    }
}
```

### PCG Component Setup

Add a `UPCGComponent` to any actor:

```cpp
// Add this to your actor's BeginPlay or constructor
UPCGComponent* PCG = CreateDefaultSubobject<UPCGComponent>(TEXT("PCG"));
PCG->SetupAttachment(RootComponent);
```

### Runtime Graph Modification

You can modify PCG graphs at runtime for dynamic generation:

```cpp
void AMyPCGActor::RegenerateAtLocation(FVector NewLocation)
{
    if (UPCGComponent* PCGComponent = FindComponentByClass<UPCGComponent>())
    {
        // Modify graph parameters before re-executing
        if (UPCGContext* Context = PCGComponent->GetCurrentContext())
        {
            // Update spawn location or other parameters
            Context->SetInputValue(TEXT("SpawnLocation"), NewLocation);
        }

        // Re-execute the graph
        PCGComponent->Execute();
    }
}
```

### PCG Data Attributes

PCG graphs pass data through **contexts** — collections of named values. Common attributes:

| Attribute | Type | Description |
|-----------|------|-------------|
| `Location` | `FVector` | Spawn position |
| `Rotation` | `FRotator` | Spawn rotation |
| `Scale` | `float` | Spawn scale multiplier |
| `Tags` | `FPCGTag` | Tags for filtering and grouping |
| `Color` | `FLinearColor` | Per-instance color |

### Best Practices

- **Use PCG for world-scale generation** — terrain features, vegetation, buildings, props. Not for gameplay logic.
- **Run PCG in the editor** for level design, then bake results into the level for runtime.
- **Use runtime PCG** for dynamic worlds (roguelike levels, terrain deformation).
- **Cache loaded graphs** — don't call `LoadSynchronous()` every frame.
- **Use tags** (`FPCGTag`) to group and filter generated content efficiently.
- **Profile PCG execution** — complex graphs with many nodes can be slow. Use the PCG Editor's profiling tools.
