# Core Concepts

This framework is built around a small set of fundamental concepts. Understanding these concepts is essential before creating gameplay systems with the plugin, as they define how information is emitted, propagated, and interpreted across the game world.

Gameplay logic is expressed through **data-driven interactions** between emitters and listeners, rather than through direct actor-to-actor communication.

---

## Systemic Design

The plugin follows a **systemic, event-driven design**.

A system is defined by:

- What information it emits (**stimuli**)
- What information it listens to (**reactions**)
- How it affects the game world (**effects**)

Systems remain decoupled from each other. They do not reference specific actors directly, but instead operate on shared signals and state, making behaviors easier to extend, combine, and maintain.

---

## Stimulus

A **Stimulus** is a piece of information emitted into the world.

It represents **something that happened**, without implying any outcome or response.

### Examples

- A sound emission
- A damage event
- A state change
- An interaction attempt
- A zone entry

A stimulus can contain:

- A type or identifier
- Parameters (value, intensity, radius, etc.)
- Contextual data (source, location, instigator)

Stimuli are purely descriptive. They do not contain logic and do not directly trigger effects.

---

## Behavior Component

A **Behavior Component** is a container component attached to an Actor.

It does not define logic by itself. Instead, it acts as a host for:

- **Actions** (stimulus emitters)
- **Reactions** (stimulus listeners)

The Behavior Component provides the execution context and lifecycle for actions and reactions, allowing them to coexist and interact without tight coupling.

---

## Action

An **Action** defines the emission of a stimulus.

Actions are responsible for:

- Deciding **when** a stimulus should be emitted
- Defining **which stimulus** is emitted
- Providing the stimulus parameters and context

Actions represent the **emitter side** of the system.

### Examples

- Emitting a _Noise_ stimulus when firing a weapon
- Emitting an _Interact_ stimulus when a button is pressed
- Emitting a _StateChanged_ stimulus when a meta-property is modified

Actions do not listen to stimuli and do not apply effects directly.

---

## Reaction

A **Reaction** defines how an actor listens to and responds to incoming stimuli.

Reactions are responsible for:

- Filtering stimuli by type and conditions
- Evaluating contextual data
- Triggering one or more effects

Reactions represent the **listener side** of the system.

Multiple reactions can listen to the same stimulus, and a single reaction can trigger multiple effects.

---

## Effect

An **Effect** represents a concrete modification to the game world or to an actor’s state.

### Examples

- Applying damage
- Modifying a meta-property
- Triggering an animation or sound
- Applying a force or impulse

Effects are:

- Stateless
- Reusable
- Executed as a result of a reaction

Effects may optionally emit new stimuli, enabling chained or systemic interactions.

---

## Meta-Properties

**Meta-properties** are abstract data values associated with actors or systems.

They can represent:

- States (alerted, powered, disabled)
- Quantities (heat, stress, energy)
- Flags or contextual markers

Meta-properties can be:

- Read by actions and reactions
- Modified by effects
- Used as conditions for stimulus emission or reaction filtering

They provide a shared state layer between otherwise independent systems.

---

## Conceptual Flow

At a high level, interactions follow this flow:

**Action → Stimulus → Reaction → Effect**

This strict separation between emission, listening, and execution ensures:

- Clear responsibilities
- High modularity
- Predictable yet flexible system behavior
