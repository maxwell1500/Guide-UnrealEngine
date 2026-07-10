## Enhanced Input System

The Enhanced Input system replaced the legacy input system (Action/Axis mappings) starting in UE4.27 and is the default in UE5. It provides a more flexible, asset-based approach to handling player input with support for runtime remapping, contextual inputs, and complex trigger chains.

### Core Concepts

Enhanced Input has four main building blocks:

1. **Input Actions** — Data assets representing what the player can do (e.g., "Jump", "Fire Weapon"). Each action has a value type: `bool`, `float` (Axis1D), `FVector2D` (Axis2D), or `FVector` (Axis3D).

2. **Input Mapping Contexts** — Collections of Input Actions mapped to specific triggers (keys, gamepad buttons, etc.). Contexts can be added/removed at runtime for different states (walking, driving, menu).

3. **Input Triggers** — Rules that determine when an action fires (press, release, hold, double-tap, chord).

4. **Input Modifiers** — Pre-processors that alter raw input values (dead zones, axis inversion, smoothing).

### Creating Input Assets

In the Content Browser, create:
- **Input Action** — defines what the player does
- **Input Mapping Context** — maps keys/buttons to actions

### Binding in C++

```cpp
#include "InputAction.h"
#include "InputMappingContext.h"
#include "EnhancedInputSubsystems.h"
#include "EnhancedInputComponent.h"

// In your header:
UPROPERTY(EditAnywhere, Category = "Input")
UInputAction* JumpAction;

UPROPERTY(EditAnywhere, Category = "Input")
UInputAction* MoveAction;

UPROPERTY(EditAnywhere, Category = "Input")
UInputMappingContext* DefaultMappingContext;

// In your .cpp:
void AMyCharacter::SetupPlayerInputComponent(UInputComponent* PlayerInputComponent)
{
    Super::SetupPlayerInputComponent(PlayerInputComponent);

    // Cast to Enhanced Input Component
    UEnhancedInputComponent* EnhancedInput = Cast<UEnhancedInputComponent>(PlayerInputComponent);
    if (EnhancedInput && JumpAction)
    {
        // Bind to the "Triggered" event (action completed)
        EnhancedInput->BindAction(JumpAction, ETriggerEvent::Triggered, this, &AMyCharacter::OnJump);
        
        // Bind to Start/Completed events for continuous movement
        EnhancedInput->BindAction(MoveAction, ETriggerEvent::Started, this, &AMyCharacter::OnMoveStarted);
        EnhancedInput->BindAction(MoveAction, ETriggerEvent::Completed, this, &AMyCharacter::OnMoveCompleted);
    }
}

void AMyCharacter::OnJump()
{
    Jump();
}

void AMyCharacter::OnMoveStarted(const FInputActionInstance& Instance)
{
    // Get the float or vector value from the action
    FVector2D MovementValue = Instance.Value.Get<FVector2D>();
    AddMovementInput(MovementValue.Rotate(0.f, GetControlRotation().Yaw).GetSafeNormal());
}

void AMyCharacter::OnMoveCompleted(const FInputActionInstance& Instance)
{
    // Player released the input
}
```

### Adding Mapping Context at Runtime

```cpp
void AMyCharacter::BeginPlay()
{
    Super::BeginPlay();

    if (APlayerController* PC = Cast<APlayerController>(GetController()))
    {
        if (UEnhancedInputLocalPlayerSubsystem* Subsystem = ULocalPlayer::GetSubsystem<UEnhancedInputLocalPlayerSubsystem>(PC->GetLocalPlayer()))
        {
            // Add mapping context with priority (higher = more important)
            Subsystem->AddMappingContext(DefaultMappingContext, 0);
        }
    }
}

// Remove when needed (e.g., entering a vehicle)
void AMyCharacter::EnterVehicle()
{
    if (APlayerController* PC = Cast<APlayerController>(GetController()))
    {
        if (UEnhancedInputLocalPlayerSubsystem* Subsystem = ULocalPlayer::GetSubsystem<UEnhancedInputLocalPlayerSubsystem>(PC->GetLocalPlayer()))
        {
            // Remove walking context, add vehicle context
            Subsystem->RemoveMappingContext(DefaultMappingContext);
            Subsystem->AddMappingContext(VehicleMappingContext, 0);
        }
    }
}
```

### Trigger States

Enhanced Input actions have four trigger states you can bind to:

| State | When it fires |
|-------|---------------|
| `Started` | Input began (e.g., key pressed down) |
| `Ongoing` | Input is being held/processed (fires every tick while active) |
| `Triggered` | Input completed all trigger conditions (e.g., press-and-release) |
| `Completed` | Input finished (e.g., key released) |
| `Canceled` | Input was interrupted before completing |

### Custom Input Modifiers

Create a custom modifier by subclassing `UInputModifier`:

```cpp
UCLASS(NotBlueprintable, MinimalAPI)
class UMyInputModifierDeadZone : public UInputModifier
{
    GENERATED_BODY()

protected:
    virtual FInputActionValue ModifyRaw_Implementation(
        const UEnhancedPlayerInput* PlayerInput,
        FInputActionValue CurrentValue,
        float DeltaTime) override
    {
        // Apply dead zone to a 2D axis value
        FVector2D Value = CurrentValue.Get<FVector2D>();
        float DeadZoneRadius = 0.2f;
        
        if (Value.Size() < DeadZoneRadius)
        {
            return FInputActionValue(FVector2D::ZeroVector);
        }
        
        return CurrentValue;
    }

    UPROPERTY(EditAnywhere, Category = "Settings")
    float DeadZoneRadius = 0.2f;
};
```

### Debug Commands

Useful console commands for debugging input:

- `showdebug enhancedinput` — Shows all active input action mappings
- `showdebug devices` — Shows connected input devices
- `Input.+key Gamepad_Left2D X=0.7 Y=0.5` — Inject input (simulate gamepad)
- `Input.-key Gamepad_Left2D` — Stop injecting input

### Best Practices

- **Use Input Actions for what the player does**, not what they press. "Jump" is an action; "Spacebar" is a binding.
- **Use Mapping Contexts to manage input states** — walking, driving, menu, paused. Add/remove them at runtime.
- **Bind to specific trigger events** (`Started`, `Triggered`, `Completed`) instead of polling in Tick.
- **Use priority** when adding multiple mapping contexts — higher priority contexts win when actions conflict.
- **Use soft references** (`TSoftObjectPtr<UInputAction>`) for input assets to avoid loading them on startup.
- **Create custom modifiers** for platform-specific behavior (dead zones, axis inversion, sensitivity curves).
