# Decision Log

_Last updated: 2026-06-05_

## 2026-06-05

- Project file workflow moved to GitHub as live source of truth; markdown/CSV records preferred over Excel for live editing.
- Build framing updated: treat current environmental chamber as intended working system, not disposable prototype.
- LN2 source path: proceed with Statebourne Cryostor 60; Statebourne recognises serial number and supports service/spares.
- LN2 solenoid: ordered 3 x Gems Sensors D2064-LN2-LU-C204 D-Cryo valves from Germany, £314.94 shipped.
- LN2 thermal relief: selected HEROSE USS-06002.0200.0000, 1.5 barG, BSPT, oxygen-cleaned, cryogenic; quantity 2 recommended.
- LN2 valve train: no custom manifold block required initially; build as short supported cryogenic valve train using tees/adapters/fittings.
- LN2 coil: prefer bending own continuous coil; target 1/4 in OD soft copper or 316/316L stainless, 0.7-0.9 mm wall, 10 m purchased, 6-8 m installed design length.
- Airflow technology: high-pressure centrifugal/radial blower is preferred; regenerative blowers are pressure-rich but too low-flow for 100 mm test section.
- ACI VBW9-00114 remains best used centrifugal candidate; motor plate is favourable for 230 V delta VFD operation.
- LMB aerospace fans: technically interesting but cost/availability-gated; Hyperfan 160 insufficient pressure; 2 x MX150-01 may work only if losses are close to 1 kPa.
- Control architecture: use cRIO outputs through interposing relays/contactors/SSR/MOSFET drivers; use feedback inputs for command/actual mismatch detection; LN2 enable requires hardwired permissive chain.
