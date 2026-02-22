# FAQ

## General

### Do I need both a Brain Component and a Behavior Component?

Yes.

Any Actor that owns one or more Behavior Components must also have a single Brain Component.

- An Actor can have multiple Behavior Components.
- An Actor must have only one Brain Component.

The Brain acts as a registry and holds global flags shared across all Behavior Components.

---

### Can I use the Meta-Property system without Actions and Reactions?

Yes.

The Meta-Property system is fully independent and can be used as a lightweight state container.

However, it becomes significantly more powerful when combined with Reactions and Effects, as it enables decoupled systemic interactions.

---

### If I have a question, how can I get support?

You can find all the information in the dedicated page :

[Support](support.md){ .md-button .md-button--primary }

---

## Architecture

### Why separate Brain and Behavior?

The separation ensures:

- Localized logic per PrimitiveComponent (Behavior)
- Centralized Actor-level state (Brain)
- Clean decoupling between physical interaction zones and global logic

This prevents tight coupling and keeps systems scalable.

---

### Can an Actor have multiple Behavior Components?

Yes.

For example:

- One Behavior on the body (damage reception)
- One on a weapon (noise emission)
- One on a sensor collider (detection zone)

Each handles its own localized logic while sharing global state through the Brain.

---

## Actions

### Can an Action emit multiple Stimuli?

An Action defines the emission of a specific Stimulus type per configuration.  
Multiple Actions can coexist on the same Behavior Component.

---

### What happens if activation flags block an Action?

The Stimulus will not propagate.

Actions can be conditionally blocked based on:

- Local flags
- Brain global flags

---

## Reactions

### How does intensity accumulation work?

Each time a valid Stimulus propagation is received:

- The Reaction accumulates intensity.
- The accumulated value is compared against its configured activation range.

Activation ranges can be:

- Min/Max inclusive
- Min/Max exclusive
- Open (no threshold requirement)

The Reaction activates only when the accumulated intensity satisfies the configured range.

---

### Can a Reaction modify states?

Yes.

When triggered, a Reaction can:

- Add or remove local Behavior flags
- Add or remove global Brain flags

This enables cascading systemic behaviors.

---

### Can multiple Reactions respond to the same Stimulus?

Yes.

Stimuli are broadcasted.  
Any Reaction configured to listen to that Stimulus type can respond independently.

---

## Meta-Properties

### When should I use a Meta-Property instead of a flag?

Use:

- **Flags** for binary state logic (e.g., Alerted, Disabled).
- **Meta-Properties** for quantitative or shared state values (e.g., Heat, Stress, Energy, Open state driven by multiple systems).

Meta-Properties are ideal when multiple systems may influence the same value.

---

## Technical

### Can I use Blueprint only?

Yes.

The framework is fully available in both **C++ and Blueprint**.

You can:

- Create custom Effects entirely in Blueprint
- Define and manipulate Meta-Properties in Blueprint
- Configure Brain and Behavior Components without writing C++

C++ is only required if you want to extend the framework at a deeper architectural level or implement highly optimized custom logic.

The plugin is designed to be accessible to designers while remaining extensible for programmers.

---

### Does the plugin support replication?

No, replication is not currently supported.

Replicating fully systemic interactions is a complex challenge, especially when dealing with decoupled stimuli propagation, state accumulation, and chained reactions.

While replication support was initially planned for release, it requires careful architectural considerations to ensure determinism, consistency, and performance in networked environments.

Replication support is part of a future roadmap but is not available at this time.

---

## Debugging

### How do I verify if a Stimulus is propagating?

Use:

- Gameplay Debugger integration
- Visual Logger
- Logs

Check:

- If the Action is blocked by flags
- If propagation mode (Hit, Overlap, Trace) is correctly configured
- If Reactions are filtered by incorrect conditions

---

### Why is my Reaction not triggering?

Common causes:

- Stimulus type mismatch
- Intensity not within activation range
- Required flags missing
- Blocking flags active
- The attached `PrimitiveComponent` does not have proper collision settings

If the Reaction depends on contact-based propagation (Hit or Overlap) or trace-based detection, the `PrimitiveComponent` hosting the Behavior Component must:

- Have collision enabled
- Have the correct collision channels configured
- Have **Generate Overlap Events** enabled (for overlap-based propagation)
- Have **Simulation Generates Hit Events** enabled (for hit-based propagation)
- Block or overlap the appropriate channels
- Be query-enabled for trace-based detection

Always verify both local Behavior flags and Brain global flags, as well as the collision configuration of the attached PrimitiveComponent.

## Design Philosophy

### Is this replacing Unreal’s native systems?

No.

The plugin acts as a systemic logic layer on top of Unreal Engine.  
It integrates naturally with Actors, Components, physics events, and Blueprint workflows.
