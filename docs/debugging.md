# Debugging

Because the framework is systemic and decoupled, debugging requires understanding how Stimuli propagate and how Reactions evaluate conditions.

This section explains how to diagnose issues efficiently.

---

## Debugging Mindset

When something does not behave as expected, always think in terms of:

Action → Stimulus → Propagation → Reaction → Conditions → Effect

A failure can occur at any step in this chain.

---

## Step-by-Step Debug Checklist

### 1. Is the Action Emitting?

Verify:

- The Action is not blocked by local flags
- The Brain does not contain blocking global flags
- The emission trigger is actually firing (input, event, physics)

If the Action is blocked, no Stimulus will propagate.

---

### 2. Is the Stimulus Propagating?

If using contact-based propagation:

The attached `PrimitiveComponent` must:

- Have collision enabled
- Have correct collision channel configuration
- Have **Generate Overlap Events** enabled (for overlaps)
- Have **Simulation Generates Hit Events** enabled (for hits)
- Block or overlap the relevant channels

If using trace-based propagation:

- Ensure collision is query-enabled
- Verify trace channel configuration
- Confirm range and shape parameters

Improper collision settings are one of the most common causes of propagation failure.

---

### 3. Is the Reaction Receiving the Stimulus?

Verify:

- Stimulus type matches the Reaction configuration
- The Behavior Component is correctly registered in the Brain
- The Reaction is not blocked by flags
- Required flags are present
- Forbidden flags are absent

---

### 4. Is Intensity Within Range?

Reactions accumulate intensity on each valid propagation.

Check:

- Minimum / Maximum values
- Inclusive vs exclusive bounds
- Whether the range is open
- Whether enough intensity has been accumulated

If intensity does not fall within the configured activation range, the Reaction will not trigger.

---

### 5. Are Meta-Property Conditions Valid?

If the Reaction depends on Meta-Properties:

- Verify current values
- Confirm threshold conditions
- Check if another system modified the property unexpectedly

---

### 6. Are Effects Executing?

If the Reaction triggers but no visible result occurs:

- Confirm Effects are correctly configured
- Verify they are not conditionally blocked
- Check if they depend on external components or states

---

## Debug Tools

### Gameplay Debugger

Use Unreal’s Gameplay Debugger to:

- Inspect active Brain flags
- Inspect Behavior local flags
- Monitor Meta-Property values
- Observe stimulus reception

---

### Visual Logger

Use Visual Logger to:

- Track propagation events
- Inspect hit/overlap events
- Analyze trace behavior
- Review activation sequences

---

### Logging

Enable plugin-specific logs (if available) to track:

- Stimulus emission
- Propagation validation
- Reaction filtering
- Intensity accumulation
- Effect execution

---

## Common Issues

- Collision misconfiguration
- Wrong stimulus type
- Intensity thresholds too strict
- Flags unintentionally blocking logic
- Meta-Property values not updated as expected

---

## Recommended Debug Strategy

When debugging:

1. Start from the Action.
2. Verify propagation.
3. Check Reaction filtering.
4. Inspect intensity accumulation.
5. Confirm Effects execution.

Always isolate one variable at a time.

Because the system is decoupled, most issues come from configuration mismatches rather than code errors.
