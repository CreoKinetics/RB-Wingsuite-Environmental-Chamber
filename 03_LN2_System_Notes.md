# LN2 System Notes

_Last updated: 2026-06-05_

## Source

Primary source is the Statebourne Cryostor 60. Statebourne recognised the serial number, were not concerned by age, still support spares, and can perform onsite service/checks.

## Build framing

This is the intended working system, not a disposable prototype. LN2 parts should be selected as best-guess final working choices with limited iteration time.

## External valve train concept

The 'manifold' is currently a functional valve train, not necessarily a custom machined block:

```text
Cryostor liquid valve
-> Statebourne LN2 hose
-> relief valve tee
-> pressure gauge tee
-> Gems D2064-LN2-LU-C204 solenoid
-> cryogenic needle/metering valve or restrictor
-> chamber coil
-> always-open external vent
```

## Ordered/locked parts

- 3 x Gems D2064-LN2-LU-C204 D-Cryo LN2 solenoid valves ordered, £314.94 shipped from Germany.
- HEROSE USS-06002.0200.0000 relief valve selected: 1/4 in BSPT male x 3/8 in BSPT female, 1.5 barG, PN63, brass, carbon-filled PTFE, oxygen cleaned/degreased, -196 to 150 C. Confirm/procure 2 units.

## Important thread details

- Gems D2064-LN2-LU-C204: LU = 1/4-19 BSPT female.
- HEROSE 06002 quoted spec: 1/4 in BSPT male inlet, 3/8 in BSPT female outlet.
- Statebourne hose likely 1/2 in BSP ecosystem; confirm exact hose/end fittings.

## Relief logic

- RV1 protects Cryostor liquid valve to closed solenoid trapped section.
- RV2 protects downstream solenoid-to-needle/coil section if the needle valve can fully close; otherwise keep as spare.
- Dewar relief protects the dewar only, not external hose/manifold trapped volumes downstream of a closed dewar valve.

## Cooling coil direction

Prefer bending our own coil rather than buying an off-the-shelf brewing coil.

Current intended tubing target:

- 1/4 in OD soft copper or 316/316L stainless tube.
- Wall thickness: 0.028-0.035 in / approximately 0.7-0.9 mm.
- Purchase length: 10 m.
- Installed design length: approximately 6-8 m, subject to chamber fit and pressure-drop judgement.
- One continuous tube, no internal joints if possible.
- Plain tube ends into proper cryogenic-compatible compression/bulkhead fittings.
- Outlet always open to safe external vent.

Backup:

- 3/8 in OD tube if 1/4 in is too restrictive or easier to source.

Avoid for main coil:

- Long 1/8 in coil.
- Long 1/2 in coil unless justified by tests/design change.

## Solenoid electrical note

Gems valves are 24 VDC, 15 W, about 0.625 A per coil. Drive through relay/MOSFET/SSR with fuse and flyback suppression, not directly from NI output.
