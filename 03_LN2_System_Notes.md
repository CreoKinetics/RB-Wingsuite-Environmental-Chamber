# LN2 System Notes

_Last updated: 2026-06-10_

## Source

Primary source is the Statebourne Cryostor 60. Statebourne recognised the serial number, were not concerned by age, still support spares, and can perform onsite service/checks.

Manual now available: Statebourne Cryostor Series User Manual, covering Cryostor 30/60/90/120/180/240. Local uploaded filename: `Statbourne_Liquid-Nitrogen-Storage_Cryostor_manual.pdf`.

## Build framing

This is the intended working system, not a disposable prototype. LN2 parts should be selected as best-guess final working choices with limited iteration time.

## Cryostor manual-derived data

### Vessel design and service

- Cryostor series are stainless steel, self-pressurising cryogenic dewars for liquefied gases at low pressures up to 3 bar.
- Approved service from manual: liquid nitrogen and argon only. Do not use for other unapproved media.
- Inner vessel protection uses a primary spring-loaded relief valve and a secondary rupture device. Manual states relief valves may be set up to 3 barG, with 1.5 barG more usual; the secondary device is listed as 4 barG.
- Standard 1.5 bar and 3 bar relief configurations have threaded outlets so reliefs can be piped away when the dewar is used in a confined space.
- Vacuum/interspace protection is by the evacuation port / outer jacket relief cover.

### Cryostor 60 fitting and spare-part references

Manual replacement-parts table for Cryostor 60 lists:

- 1901053: 4 bar secondary relief device, 1/4 in NPTM x 1/4 in NPTF.
- 1801102: 1.5 bar / 22 psi relief valve, 1/4 in NPTM x 3/8 in NPTF.
- 1801275: 3 bar relief valve, 1/4 in NPTM x 3/8 in NPTF.
- 1801255: 1.5 bar BOC-only relief valve, 1/4 in NPTM x 3/8 in BSPP female.
- 2001091: 0-60 psi pressure gauge, 63 mm, 1/4 in NPTM.
- 2101105: pressure regulator, 1-50 psi, set at 15 psi, 1/4 in BSPTF x 1/4 in BSPTF.
- 1701085: valve repair kit.
- 2201013: evacuation port cover.
- 3101100: 3 in swivel castor, quantity 4 for Cryostor 60.
- 3803001: operational valve sequence label.
- 9702018: contents indicator with probe for Cryostor 60.

### Valve and connection identification

Manual schematic identifies:

1. Liquid fill / decant valve, 1/2 in BSPP female fitting.
2. Trycock vent valve, 1/2 in BSPP female fitting.
3. Liquid fill / decant valve, 1/2 in BSPP female fitting.
4. Pressure raise valve.
5. Pressure regulator.
6. Pressure gauge.
7. Secondary relief device.
8. Relief valve.
9. Pump-down / evacuation port.

Connection/adaptor notes from manual:

- Liquid fill/decant outlet fitting on Cryostor: 1/2 in BSPP female.
- Hose needs 1/2 in BSPT male fitting.
- Statebourne 1401335: 1/2 in BSPT male to 1/2 in BSPP male adapter.
- Statebourne 1201382: BSPM 1/2 in to CGA295 male connector.
- Statebourne 3701106: 1/2 in BSPM to CGA295F, 2 m flexible hose.
- Statebourne 1201239: 3/4 male fitting / 1/2 in to 3/4 in adapter.

### Pressure building and liquid withdrawal

- Cryostor has integral pressure-building vaporiser.
- Pressure regulator factory set at 15 psig / approximately 1 barG.
- Regulator adjustment range stated as 2-20 psig / 0.1-1.4 barG.
- Never set regulator pressure above the relief-valve setting; manual notes this may cause excessive boil-off and relief-valve wear.
- To withdraw liquid or gas, first pressurise the dewar.
- For liquid withdrawal, manual states 10 psig / 0.7 barG is enough for most operations.
- Cryostor pressure must be above process pressure to prevent reverse flow.
- Never leave the dewar unattended while transferring liquid.

### Valve sequence label / operating modes

Manual and vessel label agree on these modes:

| Mode | Liquid fill/decant A | Liquid fill/decant B | Trycock vent | Pressure raising |
|---|---:|---:|---:|---:|
| Filling | Open | Closed | Open | Closed |
| Dispensing | Open or B open | Open or A open | Closed | Open |
| Pressure raising | Closed | Closed | Closed | Open |
| Gas withdrawal | Closed | Closed | Open | Open |
| Liquid storage, 24 h or less | Closed | Closed | Closed | Closed |
| Liquid storage, longer periods | Closed | Closed | Open | Closed |

For the chamber rig, normal liquid supply to the external valve train should be treated as dispensing:

```text
selected liquid fill / decant valve OPEN
trycock vent CLOSED
pressure raising OPEN
```

### Filling notes

- Start with all valves closed, then open trycock/vent.
- Connect supply hose to one liquid fill/decant valve.
- Manual explicitly requires an in-line relief valve at one end between hose end and valve to relieve possible trapped gas/liquid between two closed valves.
- Fill only to trycock level. Trycock is set at 95% gross vessel volume.
- Overfilling is hazardous and can cause uncontrolled liquid blow-off when pressure rises because liquid warms and expands.
- Never leave the dewar unattended while filling.

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
- Statebourne hose likely 1/2 in BSP ecosystem; Cryostor manual says liquid fill/decant outlets are 1/2 in BSPP female and hose needs 1/2 in BSPT male.

## Relief logic

- RV1 protects Cryostor liquid valve to closed solenoid trapped section.
- RV2 protects downstream solenoid-to-needle/coil section if the needle valve can fully close; otherwise keep as spare.
- Dewar relief protects the dewar only, not external hose/manifold trapped volumes downstream of a closed dewar valve.
- Manual explicitly calls for an in-line relief valve on transfer hose connections where gas/liquid can be trapped between two closed valves.

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

## Maintenance and siting points from Cryostor manual

- Keep external surfaces clean and free from oil and grease.
- Servicing should only be carried out by competent personnel.
- Check relief valves for satisfactory operation annually and replace if necessary.
- UK use should be inspected to a schedule compatible with Pressure Systems Safety Regulations 2000.
- Manual minimum periodic inspection/maintenance includes visual inspection, leak testing at MAWP or main relief valve limit, functional testing of valves, relief devices and contents indicator.
- Suggested interval between inspection/tests should not exceed three years.
- Written Scheme of Examination section includes yearly checks and 5-yearly checks.
- 5-yearly checks listed: pressure gauge accuracy against calibrated unit; replace pressure regulator; replace relief valve; replace secondary relief device.
- For indoor siting, manual states building should be non-combustible, adequately vented, ideally used exclusively for gas storage, and all relief devices should be vented externally.
