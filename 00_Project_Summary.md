# RB Wingsuite Environmental Chamber - Project Summary

_Last updated: 2026-06-05_

## Target condition

- Equivalent altitude: ~35,000 ft
- Chamber pressure: ~24 kPa absolute
- Temperature: -55 C target
- Airspeed: 120 kt TAS / 61.7 m/s
- Nominal test-section diameter: ~100 mm, with interchangeable smaller inserts under consideration
- Approximate flow basis: ~100 mm test section requires ~0.47-0.49 m3/s actual flow (~1,700 m3/h / ~1,000 CFM)

## Build framing

This is the intended working system, not a disposable prototype. Use robust, conservative, serviceable choices. Avoid options that depend on multiple redesign cycles unless a subsystem fails major tests.

## Core architecture

- Vestfrost VT147 ULT freezer as cold box.
- LN2 cooling via sealed internal heat-exchanger coil; LN2/nitrogen exhausted externally, not injected into chamber.
- Chamber pressure measured by Keller 23SY absolute transmitter.
- Airspeed measured by custom Pitot/static pickup and Dwyer MS-311 differential transmitter.
- cRIO-9068 control/DAQ with NI 9211, 9203, 9239, 9475, 9481, 9421 modules.

## Current critical paths

1. Cryostor 60 service/check and Statebourne hose/adapters.
2. HEROSE relief valves and downstream needle/metering valve/fittings.
3. External LN2 valve train layout.
4. Oxygen safety monitor.
5. Airflow blower selection and VFD.
6. Chamber overpressure/purge/vacuum protection.

## Current selected/ordered highlights

- 3 x Gems D2064-LN2-LU-C204 D-Cryo LN2 solenoid valves ordered, £314.94 shipped from Germany.
- HEROSE USS-06002.0200.0000 relief valve selected, 1.5 barG, 1/4 in BSPT male inlet x 3/8 in BSPT female outlet; confirm/procure 2 units.
- Statebourne Cryostor 60 selected as LN2 source path; Statebourne recognises serial number and can support/service.
- ACI VBW9-00114 is current best used centrifugal blower candidate; LMB MX150-01 route is cost/availability gated.
