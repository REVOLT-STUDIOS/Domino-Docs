# Reaction Effects

A **Reaction Effect** represents a concrete modification to the game world or to an Actor’s state.

It is the execution layer of the system.

---

## Examples

- Applying damage
- Modifying a Meta-Property
- Triggering an animation or sound
- Applying a force or impulse

Effects are:

- Stateless
- Reusable
- Executed as a result of a Reaction

Effects may optionally emit new Stimuli, enabling chained or systemic interactions.

---

## Creating Custom Effects

You can create your own Reaction Effects in **Blueprint** or **C++**.

The base class is: `UDominoReactionEffect`

It derives from `UGameplayTask`, allowing time-based execution, ticking, delays, and duration control.

---

## Creating an Effect in Blueprint

1. Create a new Blueprint class.
2. Inherit from `DominoReactionEffect`.
3. Override the desired Blueprint events:
   - `CanApplyEffect`
   - `StartEffect`
   - `TickEffect`
   - `FinishEffect`

Blueprint-only effects are fully supported and do not require C++.

---

## Creating an Effect in C++

To create a custom effect in C++:

```cpp
UCLASS()
class YOURPROJECT_API UMyCustomEffect : public UDominoReactionEffect
{
    GENERATED_BODY()

protected:

    virtual void StartEffect_Implementation() override;
    virtual void TickEffect_Implementation(float DeltaTime) override;
    virtual void FinishEffect_Implementation(bool bWasCancelled) override;
};
```

You can override:

- CanApplyEffect_Implementation()
- StartEffect_Implementation()
- TickEffect_Implementation()
- FinishEffect_Implementation()

## Core Effect Parameters

Each effect automatically receives contextual data:
Stimulus Context

- Stimulus → The GameplayTag of the triggering stimulus
- Intensity → The accumulated intensity value
- SelfActor → The owning Actor
- Hit → Associated HitResult (if applicable)

These values are BlueprintReadOnly and can be used inside your logic.
Timing Control

Effects support built-in timing parameters:

- StartDelay → Delay before StartEffect is called
- Duration → Duration before automatic finish (0 = instant)
- bUseTick → Enables ticking via TickEffect

This allows you to implement:

- Timed buffs
- Progressive damage
- Charging effects
- Temporary states

## Effect Execution Flow

When triggered, an Effect follows this lifecycle:

    CanApplyEffect()
    → Validates whether the effect should execute

    StartEffect()
    → Called after StartDelay

    TickEffect() (if bUseTick is true)
    → Called every frame during Duration

    FinishEffect()
    → Called when duration ends or effect is cancelled

**Important:**

`FinishEffect()` must be called manually in your implementation.
If it is not called, the underlying `UGameplayTask` will never complete, which means:

- The Reaction that triggered the effect will remain active
- Any subsequent effects or state changes may not execute
- Delays, duration timers, or ticked effects may not stop

Always ensure that FinishEffect() is invoked at the end of your effect logic, whether the effect finishes naturally or is cancelled.
