# Actions / Reactions

## Action

An **Action** defines the emission of a Stimulus and how it propagates through the world.

It represents the **emitter side** of the system.

An Action is responsible for:

- Defining **which Stimulus** is emitted
- Defining **how the Stimulus propagates**
- Providing contextual data (source, instigator, location)
- Defining propagation parameters (range, shape, contact rules, intensity)
- Validating activation conditions before emission

---

### Propagation Modes

An Action does not simply emit a signal globally.  
It defines how the Stimulus is transmitted.

Propagation can occur through:

**Direct contact**

- Physical hit
- Overlap events

**Area-based range**

- Radius-based propagation
- Shape-based volumes

This allows Actions to represent physical, spatial, or abstract emissions.

---

### Intensity & Parameters

An Action can define:

- Stimulus intensity
- Radius or range
- Shape configuration
- Custom parameters relevant to the Stimulus type

Intensity can later influence the activation of a Reaction.

---

### Activation Conditions

Actions may include activation constraints.

For example, emission can be blocked if:

- The owning Actor has specific flags active or inactive
- The Brain contains restrictive global flags

This ensures that emission logic remains controlled and context-aware.

---

### Important

Actions:

- Do not listen to Stimuli
- Do not apply Effects directly
- Only define emission and propagation rules

They are responsible for broadcasting structured information into the system — nothing more.

---

## Reaction

A **Reaction** defines how an Actor listens to, filters, and interprets incoming Stimuli.

It represents the **listener side** of the system.

A Reaction does not directly execute gameplay logic by itself — it evaluates conditions and, if valid, triggers one or more Effects.

---

### Stimulus Filtering

Reactions are responsible for:

- Filtering by **Stimulus type**
- Validating contextual data (source, instigator, location)
- Checking local component flags
- Checking global Brain flags
- Evaluating Meta-Property conditions

A Reaction can be blocked if specific required flags are missing, or if forbidden flags are present.

This ensures precise and context-aware activation.

---

### Intensity Accumulation

Stimuli can carry an **intensity value**.

Each time a valid propagation is received, the Reaction:

- Accumulates the received intensity
- Compares the accumulated value against its activation range

Activation ranges can be configured as:

- **Minimum / Maximum**
- Inclusive or exclusive bounds
- **Open range** (no min or max requirement)

The Reaction activates only when the accumulated intensity falls within the defined range.

This allows behaviors such as:

- Gradual alertness increase
- Threshold-based activation
- Progressive environmental responses

---

### State Modification

When activated, a Reaction can:

- Add or remove **local states** on its Behavior Component
- Add or remove **global states** on the Brain Component

This allows a Reaction to:

- Modify Actor-level logic
- Influence other Behavior Components indirectly
- Trigger cascading systemic responses

State changes may themselves be interpreted by other Reactions.

---

### Effect Triggering

Once all conditions are satisfied, the Reaction triggers one or more Effects.

Multiple Reactions can listen to the same Stimulus.  
A single Reaction can trigger multiple Effects.

---

### Important

Reactions:

- Do not emit Stimuli directly (unless via Effects)
- Do not contain hard-coded actor references
- Operate strictly through filtering, accumulation, and condition evaluation

They interpret information — they do not own the logic of execution.
