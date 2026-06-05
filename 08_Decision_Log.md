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
- Airflow initial technology: high-pressure centrifugal/radial blower preferred over generic extraction, axial, carpet dryer, leaf blower and regenerative blower options.
- Standard-density airflow selection basis established: approximately 1,745 m3/h at 4,400-5,000 Pa static at 1.2 kg/m3, corresponding to roughly 1.5-1.7 kPa at chamber density of 0.412 kg/m3.
- EV-APF561 fan selector result recorded: 1,872 m3/h at 5,062 Pa static, 2900 rpm, approximately 1.74 kPa equivalent at chamber density. Current best conventional fan-selector candidate; supplier contact drafted for price, lead time, curve, drive arrangement and larger stock alternative.
- EV-MPR502 fan selector result recorded: 1,746 m3/h at 4,407 Pa static, 2900 rpm, approximately 1.51 kPa equivalent at chamber density. Serious conventional candidate with less margin than EV-APF561.
- Kongskilde TRL range reviewed. TRL 100 is preferred Kongskilde enquiry target due to V-belt drive, 7.5 kW motor and high-pressure conveying-blower duty; TRL 75 and TRL 150 also to be asked about.
- ACI VBW9-00114 curve found. One VBW9 is too weak for full 100 mm / 120 kt target; two in series likely only about 0.75-0.79 kPa chamber-density equivalent at target flow. Demoted to test/fallback only.
- LMB aerospace fans: technically interesting but cost/availability-gated; Hyperfan 160 insufficient pressure; 2 x MX150-01 may work only if losses are close to 1 kPa.
- Pressure-boundary airflow architecture identified for conventional large blowers: external sealed blower/plenum box, with motor preferably outside pressure/cold boundary via belt or remote drive where practical.
- EDF route promoted to serious parallel path because industrial blowers meeting the duty are large and complex. DS-51-DIA HST with DSM4341-1050 is current strongest compact EDF candidate on paper: 93 mm ID, 110 m/s jet speed, 76 N thrust, 6 kW input, about 2.49 kPa dynamic pressure at chamber density and implied flow around 2,070 m3/h at standard density. Must confirm continuous duty, 24 kPa operation, -55 C suitability, ESC/power supply, telemetry and rotor containment.
- DS-51-DIA HST with DSM4335-950 remains strong lower-power EDF option: 93 mm ID, 41-59 N thrust, 82-98 m/s exhaust speed, 2.4-4.1 kW input, implied flow roughly 1,500-1,800 m3/h. Ask supplier to compare against 1050 kV version.
- DS-215-DIA HST with DSM10066-290 recorded as high-power EDF fallback: 195 mm ID, 215-250 N thrust, 84-98 m/s exhaust, 9.8-15.6 kW input; aerodynamically more than enough but likely physically/electrically larger than necessary.
- VasyFan VF-120-06 recorded as promising 120 mm EDF option: TPPOWER 5670 600 kV, 14S, 9.1 kgf thrust, 121 A, 6.267 kW. Similar power class to DS-51 1050 kV but larger fan diameter and more thrust/flow margin.
- Battery-run concept noted: Tattu Pro 14S 22 Ah 53.2 V pack has about 1.17 kWh nominal energy. At 6.267 kW VF-120-06 full-power draw, ideal runtime is about 11.2 minutes and practical full-power runtime likely 8-10 minutes. A 20 minute full-power run would require about 2.09 kWh before reserve, so likely two such packs or a higher-capacity/parallel battery arrangement.
- EDF operational concept noted: low-speed running during cold soak may help keep motor/bearings warmer and verify system health before ramping to full power, but this needs supplier confirmation because low throttle may not adequately warm bearings and may still add heat to the chamber. Main-test duration must be matched to battery capacity and motor/ESC continuous-duty limits.
- Control architecture: use cRIO outputs through interposing relays/contactors/SSR/MOSFET drivers; use feedback inputs for command/actual mismatch detection; LN2 enable requires hardwired safety permissive chain.
