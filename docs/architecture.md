# Architecture Overview

This section provides a high-level view of the plugin’s architecture. Understanding this is essential to grasp how systems, behaviors, and stimuli interact in a decoupled, modular way.

---

## General Architecture

The plugin is built around **Behavior Components**, which serve as containers for **Actions** and **Reactions**.

### Components Overview

- **Behavior Component**: Attached to an Actor; hosts Actions and Reactions.
- **Action**: Emits stimuli based on internal logic or game events.
- **Stimulus**: Represents information about an event in the world; purely descriptive.
- **Reaction**: Listens to stimuli and triggers Effects if conditions are met.
- **Effect**: Executes concrete changes to the actor or world state.

### Data Flow

The core data flow is always:

Action → Stimulus → Reaction → Effect

1. **Action** emits a stimulus.
2. **Stimulus** propagates through the system.
3. **Reaction** evaluates and filters stimuli.
4. **Effect** applies changes to the world or actor state.

This flow ensures that emission, listening, and execution are **clearly separated**, making systems easier to maintain and extend.

---

## Systemic Approach

The plugin is designed with a **systemic mindset**, emphasizing:

- **Logical decoupling**:  
  Actions and Reactions do not reference each other directly; all communication is via stimuli.
- **No hard-coded scripts**:  
  All gameplay interactions are configurable through Actions, Reactions, and Effects.
- **Emergent behaviors**:  
  Complex interactions can emerge from the combination of simple systems without explicit orchestration. For example, multiple actors responding to the same stimulus can create dynamic gameplay scenarios automatically.

---

## Event Lifecycle

Every interaction in the plugin follows a **clear lifecycle**:

1. **Stimulus Creation**
   - An Action emits a stimulus, providing type, parameters, and context.
2. **Propagation**
   - The stimulus is broadcasted to all relevant Reactions in the world or within scope.
3. **Interpretation by Behaviors**
   - Behavior Components evaluate incoming stimuli via their Reactions.
4. **Effect Application**
   - If conditions are satisfied, Effects are executed.
   - Effects may modify meta-properties, actor state, or trigger new stimuli, continuing the interaction chain.

---

### Summary

This architecture ensures:

- Clear separation of responsibilities
- High modularity and reusability
- Flexible, predictable, and extendable gameplay systems

By understanding this flow, designers and programmers can **create complex systems without tightly coupling components**, keeping gameplay logic clean and manageable.
