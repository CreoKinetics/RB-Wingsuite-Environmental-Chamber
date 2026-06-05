# Safety Interlocks

_Last updated: 2026-06-05_

## Hardwired LN2 permissive

LN2 enable should require a hardwired safety permissive chain such as:

```text
E-stop OK
+ O2 monitor OK
+ chamber closed
+ chamber pressure safe
+ vent path OK
= LN2 enable permitted
```

Software command alone must not be sufficient to energise LN2 solenoids.

## Separate protections

- Dewar relief protects the dewar, not the external hose/manifold trapped volume.
- HEROSE 06002 valves protect external LN2 trapped-line sections.
- Chamber overpressure relief is separate and still needs design.
- Room oxygen depletion monitoring is separate and still needs selection.

## Chamber risk cases

- LN2 coil leak into sealed chamber.
- Purge/backfill overpressure.
- Vacuum pump/vent/purge valve operator error.
- Blower/VFD fault or unexpected run state.
- Relay stuck on/off or solenoid coil open circuit.

## Feedback philosophy

For each safety-relevant actuator, log both:

- commanded_state
- feedback_state

Use relay auxiliary contacts, VFD run/fault outputs, and/or current sensing to detect mismatch.

## Gems solenoid electrical safety

Each Gems solenoid is 24 VDC, 15 W, about 0.625 A. Use:

- per-channel fuse or electronic protection;
- flyback suppression;
- interposing relay/MOSFET/SSR rated for DC inductive load;
- relay auxiliary or current feedback where possible.
