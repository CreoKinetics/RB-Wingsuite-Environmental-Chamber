# Project Todo

_Last updated: 2026-06-05_

## Immediate

- Confirm/order 2 x HEROSE USS-06002.0200.0000 relief valves at 1.5 barG.
- Await HEROSE quote for cryogenic needle/metering valve, manual shutoff, gauge, tees/adapters, and relief outlet fittings.
- Await Statebourne service/accessory quote for Cryostor 60.
- Track delivery of 3 x Gems D2064-LN2-LU-C204 solenoid valves and bench-test on arrival.
- Await/seek LMB budgetary cost, lead time, electrical/control details and two-week feasibility for MX150-01 fan route.
- Contact EV/APF or Fans & Blowers supplier about EV-APF561 and EV-MPR502: price, lead time, full curve, motor/drive arrangement, and any larger suitable in-stock option.
- Contact Kongskilde about TRL 75 / TRL 100 / TRL 150 suitability, stock/lead time, cost, static pressure at 1,700-1,800 m3/h, cold suitability and motorless/belt-drive options.
- Contact Schubeler/EDF supplier about DS-51-DIA HST with DSM4341-1050 and DSM4335-950, plus DS-215 fallback: continuous duty, 24 kPa operation, -55 C suitability, ESC/power supply, telemetry and containment.

## Next

- Confirm Statebourne hose length and fittings, preferably 1.2-1.5 m.
- Draft the actual external LN2 valve train once all thread details are known.
- Add cooling-coil tubing purchase once source/spec is selected: 1/4 in OD copper or 316/316L stainless, 0.7-0.9 mm wall, 10 m.
- Select oxygen depletion monitoring strategy.
- Decide whether to keep ACI VBW9 pair as cheap fallback only; curve shows it is likely too weak for main full-target airflow.
- Develop chamber purge/vent/overpressure protection layout.
- Develop EDF electrical/safety concept if supplier response is favourable: DC supply or battery, ESC mounting, sealed feedthroughs, interlocks, temperature telemetry, rotor containment and emergency shutdown.
- Develop conventional blower pressure-boundary concept if EV-APF/Kongskilde route is chosen: sealed plenum, duct penetrations, motor placement, belt/shaft seal if applicable, plenum structural design for ~77 kPa differential.

## Ongoing rules

- Treat this as the intended working build, not a disposable prototype.
- Any section that can trap liquid nitrogen between closed valves needs thermal relief or must be redesigned so it cannot trap liquid.
- LN2/nitrogen from the coil must exhaust externally, not into the chamber/freezer atmosphere.
- Software command alone must not be sufficient to energise LN2; use hardwired safety permissive.
- For airflow, distinguish actual chamber-density volumetric flow from standard-density fan selection pressure; current standard-density target is about 1,745 m3/h at 4,400-5,000 Pa static.
