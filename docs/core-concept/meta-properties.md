# Meta-Properties

**Meta-properties** are abstract data values associated with actors or systems.

They can represent:

- States (Alerted, Powered, Disabled, Open)
- Quantities (Heat, Stress, Energy)
- Flags or contextual markers

Meta-properties can be:

- Modified by Effects
- Modified independently via the component itself

They provide a shared state layer between otherwise independent systems.

---

### Independent Yet Systemic

The Meta-Property system is fully independent and can be used on its own as a lightweight data container for storing Actor-level or component-level state.

However, when coupled with Actions, Reactions, and Effects, it becomes a powerful decoupling tool.

Instead of directly linking systems together, multiple systems can influence the same meta-property without referencing each other.

For example:

A door may have a meta-property:

`Open = false`

The door can become open due to different causes:

- An explosion destroys the lock
- A lockpicking interaction succeeds
- A power system restores electricity
- A scripted event triggers the mechanism

None of these systems need to reference the door directly.

They simply modify:

`Open = true`

Once the meta-property changes, the Actor can:

- React automatically through an event
- Play an animation
- Disable collision

This approach ensures that:

- Systems remain decoupled
- State changes are centralized
- Multiple causes can lead to the same outcome
- The Actor interprets its own state change instead of being forced externally

Meta-properties therefore act as a **state abstraction layer**, enabling systemic interactions without tight coupling.
