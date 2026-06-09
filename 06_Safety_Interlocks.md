# Safety Interlocks and Cryogenic Safety Notes

_Last updated: 2026-06-09_

This file records project-specific safety requirements and design controls for the RB Wingsuite Environmental Chamber. It is not a substitute for a formal risk assessment, COSHH assessment, supplier manuals, site safety approval, or competent-person review before operation.

## Core safety philosophy

- The cRIO/software may request operation, but must not be the only safety layer.
- Hazardous outputs must fail safe on power loss, watchdog failure, E-stop, or safety-chain trip.
- LN2 valves must be normally closed unless a specific valve is deliberately used for venting.
- Any cryogenic liquid trapped between two closed valves must have a rated thermal relief path.
- Nitrogen/LN2 discharge must not be vented into the room or into a sealed chamber volume without a defined exhaust path.
- The design should favour simple, visible, mechanically obvious protections over clever software-only logic.

## Hardwired LN2 permissive

LN2 enable should require a hardwired safety permissive chain such as:

```text
E-stop OK
+ O2 monitor OK
+ chamber closed
+ chamber pressure safe
+ vent path OK
+ airflow/fan proof if cooling requires forced flow
= LN2 enable permitted
```

Software command alone must not be sufficient to energise LN2 solenoids.

## Separate protections

- Dewar relief protects the dewar, not the external hose/manifold trapped volume.
- HEROSE 06002 or equivalent valves protect external LN2 trapped-line sections.
- Chamber overpressure relief is separate and still needs design.
- Room oxygen depletion monitoring is separate and still needs selection.
- Mechanical pressure relief must still be fitted even when electronic pressure sensing is used.

## LN2-specific hazards and mitigations

### Oxygen depletion / asphyxiation

Hazard:

- Nitrogen boil-off can displace room oxygen.
- Nitrogen is colourless, odourless and gives no reliable human warning before impairment or unconsciousness.
- A leak, vent discharge, open dewar, purge/backfill error, or coil failure can create an oxygen-deficient atmosphere.

Mitigations:

- Fit an industrial oxygen depletion monitor for the room/test area before routine LN2 operation.
- Prefer a fixed O2 monitor with audible/visual alarm; an industrial personal O2 detector is acceptable as an interim lower-cost control but not as the final fixed-room protection.
- Place the O2 sensor where depletion is credible, considering room air movement and vent locations.
- Add O2 monitor OK into the hardwired LN2 permissive chain where practical.
- Do not work alone during early LN2 commissioning.
- Keep the test area ventilated.
- Vent coil exhaust and relief outlets to a safe external location, not to the chamber or occupied room.
- Define evacuation/no-entry response for O2 alarm.

### Trapped liquid expansion / pressure rupture

Hazard:

- LN2 expands violently as it warms and boils.
- A small amount of trapped liquid between closed valves can produce destructive pressure rise.

Mitigations:

- No section that can contain liquid nitrogen may be isolated between closed valves without a rated thermal relief valve.
- Fit external trapped-line relief on the hose/valve-train section between the Cryostor outlet/manual valve and solenoid valve.
- Fit downstream trapped-line relief if the solenoid, needle valve, coil, or any downstream valve arrangement can trap liquid.
- Route relief outlets to a safe vent location where discharge cannot impinge on people, cables, plastics, insulation, or oily/organic materials.
- Do not cap or plug relief outlets.
- Use cryogenic-rated valves, fittings and hose only.
- Use mechanical supports so hose, solenoid bodies and fittings are not acting as structural supports.

### Oxygen enrichment / condensed oxygen fire risk

Hazard:

- LN2 and very cold cryogenic surfaces can condense oxygen from air in open or poorly controlled situations.
- As nitrogen preferentially boils away, remaining liquid/frost can become oxygen-enriched.
- Oxygen-enriched liquid, frost or cold surfaces can make oils, greases, solvents, hydrocarbons, cloth, foam, paper, wood, dust and other organic materials ignite or burn much more violently.

Mitigations:

- Do not use open LN2 baths, trays or catch-pans for normal operation.
- Do not allow LN2 to drip into or soak porous/organic materials such as foam, cloth, wood, cardboard, insulation, cable bundles, oil-contaminated surfaces, rags or absorbent mats.
- Keep the LN2 path closed from Cryostor to internal coil, then always-open to the external vent.
- Do not vent LN2 or cold nitrogen into the chamber or room except during deliberately controlled commissioning with an approved temporary procedure.
- Keep oils, greases, solvents and hydrocarbons away from LN2 components and cold discharge paths.
- Use oxygen-clean/degreased cryogenic components where oxygen enrichment is credible, especially relief valves and cold valve-train parts.
- Select non-combustible drip shields/guards where shielding is needed; avoid absorbent insulation around possible leak points.
- If unexplained pale-blue liquid, unusual frosty liquid accumulation, or oxygen-enrichment suspicion occurs, stop work, remove ignition sources, isolate LN2 if safe, ventilate and allow the area to warm/evaporate without contact.
- Do not strike, scrape or mechanically disturb suspected oxygen-enriched frozen/soaked material.

### Frostbite / cold burn / brittle fracture

Hazard:

- LN2 and cold metal surfaces can cause severe cold burns.
- Many plastics, rubbers and adhesives become brittle at cryogenic temperatures.

Mitigations:

- Wear cryogenic gloves, face protection and suitable clothing during fill, connection, venting and commissioning.
- Do not touch uninsulated cold metalwork.
- Use guards or labels on exposed cold components.
- Use materials compatible with cryogenic service near the LN2 path.
- Keep non-rated flexible tubing, cable insulation, plastics and adhesives away from possible LN2 spray or relief discharge.

### Chamber pressure / vacuum / backfill hazards

Hazard:

- The chamber operates below atmospheric pressure and may be backfilled or purged.
- Incorrect valve sequencing can overpressure or underpressure parts of the chamber, ducting or sensor lines.

Mitigations:

- Fit chamber absolute pressure measurement.
- Add independent chamber overpressure protection separate from software.
- Use defined purge/backfill procedures and restrictor/needle valve where needed.
- Do not rely on the APTech or other purge regulator as the only overpressure protection.
- Rate or test ducts, windows, covers and ports for the differential pressure they will see.
- Verify pressure sensor scaling before automated operation.

### Fan / EDF hazards

Hazard:

- EDF operation involves high rotational speed, high electrical power and possible blade failure.
- Cold operation may affect bearings, grease, blades, adhesives and motor materials.

Mitigations:

- Use mechanical containment around the EDF/fan path.
- Include fan enable in safety gating where fan operation is required for safe cooling.
- Prove airflow before allowing LN2 injection where practical.
- Follow supplier bearing warmup advice: run around 10000 rpm / quarter maximum speed before cold high-speed operation.
- Avoid starting from stationary at the lowest chamber temperature where possible.
- Use guarded electrical terminals, fused DC supply/battery wiring and an emergency isolation method.
- Follow ESC manufacturer/supplier guidance on battery, DC supply, capacitor, pre-charge and cable length.

## Chamber risk cases

- LN2 coil leak into sealed chamber.
- Relief valve discharge into unsafe area.
- LN2 leak onto absorbent/organic material leading to oxygen-enriched contamination.
- Purge/backfill overpressure.
- Vacuum pump/vent/purge valve operator error.
- Blower/EDF/VFD fault or unexpected run state.
- Relay stuck on/off or solenoid coil open circuit.
- Sensor scaling error causing unsafe automatic control.
- Loss of HMI/comms while cRIO continues operation.

## Feedback philosophy

For each safety-relevant actuator, log both:

- commanded_state
- feedback_state

Use relay auxiliary contacts, VFD/ESC run/fault outputs, pressure/flow confirmation, and/or current sensing to detect mismatch.

## Gems solenoid electrical safety

Each Gems solenoid is 24 VDC, 15 W, about 0.625 A. Use:

- per-channel fuse or electronic protection;
- flyback suppression;
- interposing relay/MOSFET/SSR rated for DC inductive load;
- relay auxiliary or current feedback where possible.

## Minimum pre-run checks

Before LN2-enabled operation:

- E-stop tested.
- LN2 solenoid de-energised safe state verified.
- Vent path confirmed open.
- Relief valves installed and not capped.
- Chamber pressure sensor scaling checked at atmosphere.
- Pitot/airflow DP sensor zero checked.
- O2 monitor active and alarm response understood.
- Fan/airflow proof checked if required for cooling.
- No open absorbent/organic materials under possible LN2 discharge paths.
- Operators briefed on stop/evacuation response.
