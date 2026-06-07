# Project Todo

_Last updated: 2026-06-07_

## Immediate

- Confirm/order 2 x HEROSE USS-06002.0200.0000 relief valves at 1.5 barG; quoted spec is 1/4 in BSPT male x 3/8 in BSPT female, 6 mm orifice, PN63, oxygen-cleaned, -196 to 150 C.
- Await HEROSE quote for cryogenic needle/metering valve, manual shutoff, gauge, tees/adapters/reducers, and 3/8 in relief outlet fittings.
- Await Statebourne service/accessory quote for Cryostor 60: onsite service/check, hose 3701004/3701006, outlet adapters, hose relief advice, phase separator, spares, PPE/O2 alarm options and manual/schematic.
- Track delivery of 3 x Gems D2064-LN2-LU-C204 solenoid valves and bench-test on arrival: coil continuity, actuation at 24 VDC, visual port/thread condition, and leak/function check when safe.
- Reply to Schubeler/EDF supplier with bounded question: assess whether one DS-51-DIA HST package is viable; if not, recommend smallest suitable single-fan alternative. Include 24 kPa/-55 C duty, 93-100 mm test section, single-fan commercial constraint, long-life bearing, low-temperature lubricant, strengthened blade, inlet ring and YGE battery-supply questions.
- Check YGE/Schubeler position on lab DC supply. YGE Aureus manual states ESC should only be powered by batteries and power supplies are not allowed; ask whether any approved lab rig supply arrangement exists.
- Add NI 9219 to cRIO module inventory and update I/O allocation once sensor list stabilises.
- Await/seek LMB budgetary cost, lead time, electrical/control details and two-week feasibility for MX150-01 fan route.
- Contact EV/APF or Fans & Blowers supplier about EV-APF561 and EV-MPR502: price, lead time, full curve, motor/drive arrangement, and any larger suitable in-stock option.
- Contact Kongskilde about TRL 75 / TRL 100 / TRL 150 suitability, stock/lead time, cost, static pressure at 1,700-1,800 m3/h, cold suitability and motorless/belt-drive options.

## Next

- Confirm Statebourne hose length and fittings, preferably 1.2-1.5 m; avoid >2 m unless necessary.
- Draft the actual external LN2 valve train once all thread details are known. Treat 'manifold' as a short supported valve train from tees/adapters/fittings unless a supplier recommends a block.
- Add cooling-coil tubing purchase once source/spec is selected: 1/4 in OD copper or 316/316L stainless, 0.7-0.9 mm wall, 10 m.
- Select oxygen depletion monitoring strategy.
- Decide whether to buy one ACI VBW9 as cheap fallback/test blower only; one unit is too weak for full 100 mm / 120 kt target, two in series still marginal.
- Develop chamber purge/vent/overpressure protection layout.
- Develop EDF electrical/safety concept if supplier response is favourable: battery and ESC mounting, LiPo storage and charging, fusing, sealed feedthroughs, interlocks, telemetry, rotor containment and emergency shutdown.
- Develop conventional blower pressure-boundary concept if EV-APF/Kongskilde route is chosen: sealed plenum, duct penetrations, motor placement, belt/shaft seal if applicable, plenum structural check for chamber differential pressure.

## Ongoing rules

- Treat this as the intended working build, not a disposable prototype.
- Any section that can trap liquid nitrogen between closed valves needs thermal relief or must be redesigned so it cannot trap liquid.
- LN2/nitrogen from the coil must exhaust externally, not into the chamber/freezer atmosphere.
- Software command alone must not be sufficient to energise LN2; use hardwired safety permissive.
- For airflow, distinguish actual chamber-density volumetric flow from standard-density fan selection pressure; current standard-density target is about 1,745 m3/h at 4,400-5,000 Pa static.
