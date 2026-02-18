# Core Concepts

This framework is built around a small set of fundamental concepts. Understanding these concepts is essential before creating gameplay systems with the plugin, as they define how information is emitted, propagated, and interpreted across the game world.

Gameplay logic is expressed through **data-driven interactions** between emitters and listeners, rather than through direct actor-to-actor communication.

---

## Systemic Design

The plugin follows a **systemic, event-driven design**.

A system is defined by:

- What information it emits (**actions**)
- What information it listens to (**reactions**)
- How it affects the game world (**effects**)

Systems remain decoupled from each other. They do not reference specific actors directly, but instead operate on shared signals and state, making behaviors easier to extend, combine, and maintain.

---

## Stimulus

A **Stimulus** is a piece of information emitted into the world.

It represents **something that happened**, without implying any outcome or response, it is represented as a `Gameplay Tag` in Unreal Engine.

!!! info "Example"

    - A sound emission
    - A damage event
    - A state change
    - An interaction attempt

    Stimuli are purely descriptive. They do not contain logic and do not directly trigger effects.

---

## Conceptual Flow

At a high level, interactions follow this flow:

**Action → Stimulus → Reaction → Effect**

This strict separation between emission, listening, and execution ensures:

- Clear responsibilities
- High modularity
- Predictable yet flexible system behavior
