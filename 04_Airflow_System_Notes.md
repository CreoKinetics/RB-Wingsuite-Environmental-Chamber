# Airflow System Notes

_Last updated: 2026-06-07_

## Target

Approximate current target: 120 kt TAS / 61.7 m/s through ~100 mm test section at 24 kPa absolute and -55 C.

This implies roughly:

- 0.47-0.49 m3/s actual flow
- ~1,700 m3/h
- ~1,000 CFM

Equivalent standard-density fan selection target used in fan selectors:

- ~1,745 m3/h at ~4,400-5,000 Pa static pressure
- 20 C, sea level, density about 1.2 kg/m3

Density correction basis:

- chamber density about 0.412 kg/m3
- density ratio 0.412 / 1.2 = 0.343
- 4,400 Pa at 1.2 kg/m3 is about 1.51 kPa at chamber density
- 5,062 Pa at 1.2 kg/m3 is about 1.74 kPa at chamber density

## Current direction update

Industrial blowers that meet the pressure/flow target are becoming physically large and introduce pressure-boundary, motor cooling and packaging issues. EDF options are now being treated as a serious parallel path because high-performance EDFs may provide the required 93-100 mm-class velocity in a much smaller package, at the cost of high DC power, ESC cooling, continuous-duty uncertainty, battery/power architecture and rotor-containment requirements.

## Preferred conventional technology

For industrial blower route: high-pressure centrifugal/radial blower. Avoid treating low-pressure HVAC fans, carpet dryers, axial fans, or generic extraction fans as final solutions. Regenerative/side-channel blowers have high pressure but usually too little flow for a 100 mm test section.

## EDF candidates

### DS-51-DIA HST with DSM4341-1050

Current strongest compact airflow candidate on paper.

Supplier/spec screenshot values:

- casing inside diameter: 93 mm
- jet speed: 110 m/s
- speed range: 39,500 rpm
- total weight: 640 g
- static thrust: 76 N
- input power: 6.0 kW
- overall efficiency: 70%

Performance graph / supply notes:

- The DS-51-DIA HST graph spans roughly 34.5-46 V DC, consistent with a 12S LiPo operating envelope.
- At ~46 V the graph appears to show about 140 A, giving about 6.4 kW electrical input.
- Around this point it also shows about 110 m/s exhaust speed, ~80 N thrust, ~41,000 rpm and around 68-70% total efficiency.

Interpretation:

- 110 m/s = about 214 kt TAS.
- At chamber density 0.412 kg/m3, 110 m/s gives dynamic pressure of about 2.49 kPa.
- Required 120 kt / 61.7 m/s dynamic pressure at chamber density is about 0.785 kPa.
- Using thrust / jet speed gives mass flow about 0.69 kg/s.
- At standard density this implies about 0.575 m3/s / 2,070 m3/h.
- Through a 100 mm test section this corresponds to about 73 m/s / 142 kt, assuming the volumetric flow can be realised in the duct/test section.

Status: most compelling EDF option so far. Supplier has responded positively and will consult engineering. Need confirmation on whether one DS-51-DIA HST package is viable, static/ducted rig use, continuous/semi-continuous duty, 24 kPa absolute operation, -55 C dry air/nitrogen suitability, ESC/battery/power requirements, motor cooling, telemetry/protection and rotor containment.

Commercial framing for Schubeler response: low-volume engineering/test-rig use; likely one unit initially if technically sound. Do not lead supplier toward a multi-fan solution because multiple ~GBP 2k fans plus power electronics is unlikely to be commercially attractive. Ask whether a single DS-51 is viable; if not, ask for the smallest suitable single-fan alternative.

Durability options to ask about:

- long-life/special bearings;
- low-temperature bearing lubricant;
- strengthened/abrasion-resistant blades for possible frost/ice particles, debris and test-rig durability;
- inlet ring/bellmouth for open-duct/test-bench use;
- magnet/material/adhesive/thermal-cycle limitations at -55 C.

### DS-51-DIA HST with DSM4335-950

Supplier/spec screenshot values:

- casing inside diameter: 93 mm
- fan swept area: 51 cm2 / 0.0051 m2
- weight: 590 g
- static thrust: 41-59 N
- exhaust speed: 82-98 m/s
- RPM: 29,300-34,800 rpm
- input power: 2.4-4.1 kW
- battery: 10-12S 4500 mAh LiPo
- efficiency: 70-71%

Interpretation:

- Implied sea-level volumetric flow from thrust/exhaust speed is roughly 1,500-1,800 m3/h.
- Very close to the 100 mm target and especially close if test section is nearer 93 mm effective diameter.
- Less margin than DSM4341-1050 but lower power and less severe electrically.

Status: strong lower-power EDF candidate; ask supplier whether 950 kV or 1050 kV motor is better for static ducted chamber operation.

### DS-215-DIA HST with DSM10066-290

Supplier/spec screenshot values:

- casing inside diameter: 195 mm
- fan swept area: 215 cm2 / 0.0215 m2
- weight: 3,400 g
- static thrust: 215-250 N
- exhaust speed: 84-98 m/s
- RPM: 12,000-14,000 rpm
- input power: 9.8-15.6 kW
- recommended battery: 12-14S 20000 mAh LiPo
- efficiency: 78%

Interpretation:

- Implied sea-level volumetric flow from thrust/exhaust speed is roughly 7,650 m3/h.
- Aerodynamically more than enough, but physically/electrically much larger than required.
- Input power 10-16 kW makes power supply, heat, safety and containment significant.

Status: keep as high-power fallback or ask supplier to compare against DS-51; likely more than needed if DS-51 can operate reliably.

## YGE Aureus ESC / power notes

Recommended ESC from Schubeler for DS-51 HST: YGE Aureus 185.

Manual findings:

- Aureus 105/135/185 are 4-12S LiPo devices; Aureus 265 is up to 14S.
- The specified current is maximum continuous full-power current.
- Aureus 185/265 include temperature-controlled fan and fan cover.
- Active free-wheel allows unlimited part-load operation within current limits.
- ESC sends telemetry such as voltage, current, capacity, BEC voltage, RPM, throttle percentage, PWM, BEC temperature, warnings and errors.
- Battery-to-controller wire length must not exceed 30 cm. If longer wires are necessary, additional ultra-low-ESR capacitors are required; manual recommends YGE Cap's 9.
- Longer motor cables can be used; twist the three motor cables to reduce EMI.
- Important blocker: the manual states the ESC should only be powered by batteries and that power supplies are not allowed.

Implication:

- Do not assume a 48 V server/telecom PSU is usable with the YGE Aureus 185.
- Default supported architecture is 12S LiPo battery close to ESC with short high-current DC leads.
- Any lab DC supply, buffer battery, capacitor bank or hybrid arrangement needs Schubeler/YGE confirmation before design.
- Capacitors can suppress spikes and bus ripple but are not a substitute for a battery at ~6 kW. A 1 F capacitor at 48 V stores only ~1.15 kJ, under 0.2 s at 6.4 kW.
- A PSU in parallel with LiPo is not a simple safe solution because of charge/backfeed/current-sharing/fault-current issues; if used, it should be via a proper charger or manufacturer-approved architecture.

## Current strongest conventional fan-selector candidates

### EV-APF561

Fan selector result:

- Requested: 1,745 m3/h at 4,400 Pa static, 20 C at 0 m, density 1.2 kg/m3.
- Returned: 1,872 m3/h at 5,062 Pa static, 2900 rpm.
- Equivalent at chamber density 0.412 kg/m3: approximately 1,872 m3/h at 1.74 kPa static, assuming density scaling.
- Current status: strongest calculator-matched industrial candidate so far; supplier contact/email drafted for price, lead time, curve, drive arrangement and any larger in-stock alternative.

### EV-MPR502

Fan selector result:

- Requested: 1,745 m3/h at 4,400 Pa static, 20 C at 0 m, density 1.2 kg/m3.
- Returned: 1,746 m3/h at 4,407 Pa static, 2900 rpm.
- Equivalent at chamber density 0.412 kg/m3: approximately 1,746 m3/h at 1.51 kPa static.
- Current status: serious candidate but less margin than EV-APF561; may be attractive if cheaper/smaller/more available.

### EV-APF range chart note

Screenshot of APF range curve shows EV-APF561A/B at the lower end of the range and larger EV-APF632/711/802/901 families above it. Our 100 mm target point is approximately 1,745 m3/h / 1,027 CFM and 4,400 Pa / 17.7 inWG at catalogue density. EV-APF561 appears to cover this region, with the selector returning a slightly higher operating point. Larger APF models may give more margin but will increase motor power, size and cost.

## Kongskilde TRL conveying blower route

Kongskilde FRL/FEA/TRL data sheet reviewed. TRL blowers are proven conveying blowers for air supply/conveying/ventilation where high pressure is required. They are centrifugal blowers and not intended for corrosive gases; catalogue maximum air temperature is 70 C.

Best candidates:

- TRL 75: 5.5 kW, direct drive, 2900 rpm, 96 kg with motor. Interesting performance/size but direct-drive motor issue remains.
- TRL 100: 7.5 kW, V-belt drive, motor 2900 rpm, rotor 3650 rpm, 129 kg with motor. Current preferred Kongskilde model to ask about due to belt drive and pressure capability.
- TRL 150: 11 kW, V-belt drive, rotor 4200 rpm, 157 kg with motor. Stronger pressure margin but larger/more power.

Status: supplier contact form/email drafted asking which of TRL 75/100/150 can provide approximately 1,745 m3/h at 4,400 Pa static at standard density; also asking static-pressure data, -55 C suitability, bare-shaft/motorless options, stock/lead time and cost.

## Airflow pressure-boundary architecture

As fan size increases, a fully internal fan becomes less practical. Current preferred conventional blower architecture to investigate is:

```text
freezer/chamber pressure volume
-> short vacuum-rated duct
-> external sealed blower/plenum box
-> short vacuum-rated return duct
-> chamber/test section
```

The fan/blower impeller and scroll should be inside the low-pressure recirculation boundary, but the motor should preferably remain outside the pressure/cold boundary where possible.

Belt drive or remote shaft drive is a serious option because it allows:

- blower/impeller inside an external sealed low-pressure plenum;
- motor outside at ambient pressure and temperature;
- easier motor cooling;
- easier VFD/motor selection;
- reduced risk from TEFC motor cooling at 24 kPa absolute;
- reduced heat rejection into the cold/low-pressure airflow loop.

Key risks to resolve for remote/belt drive:

- shaft penetration through pressure boundary;
- rotating shaft seal leakage and wear;
- bearing support/alignment;
- belt slip/tension/guarding;
- belt material and pulley suitability if any belt section is cold or low pressure;
- ensuring the sealed plenum can withstand approximately 77 kPa external differential pressure without deformation.

Avoid relying on a standard industrial fan casing to hold vacuum unless the manufacturer explicitly confirms it. A purpose-built sealed blower box/plenum may be safer and more controllable.

For EDF route, likely architecture is different:

```text
EDF in sealed recirculating duct/plenum
-> short diffuser/settling section if needed
-> 93-100 mm test section/nozzle
-> return duct/plenum
```

ESC and power electronics should preferably remain outside cold/low-pressure boundary, with sealed motor phase/power/control feedthroughs.

## ACI VBW9 used candidate

ACI VBW9-00114, with CMG SLA-90L-2 motor plate:

- 220-240 V delta, 50 Hz, 2.2 kW, 2830 rpm
- 380-415 V star, 50 Hz, 2.2 kW, 2830 rpm
- 440-480 V star, 60 Hz, 2.5 kW, 3395 rpm
- bearing 6205-2RS-C3

This is VFD-friendly if run from a suitable 230 V single-phase input to 230 V three-phase output VFD, motor linked delta.

VBW9 curve found. At the project flow of approximately 1,745 m3/h / 1,027 CFM, the VBW9 curve shows roughly 4.4-4.6 inWG static pressure at catalogue density, equivalent to about 1.1 kPa at 1.2 kg/m3. Corrected to chamber density 0.412 kg/m3, this is only about 0.38 kPa for one fan. Two identical VBW9 units in series would be roughly 8.8-9.2 inWG / 2.2-2.3 kPa catalogue static, or about 0.75-0.79 kPa at chamber density before additional series/duct losses.

Conclusion: one VBW9 is too weak for the full 100 mm / 120 kt target. Two VBW9 in series may be useful for bench testing or reduced-diameter/lower-loss operation, but are likely still short of the desired 1.5 kPa class chamber-density pressure margin. Do not buy as primary solution unless very cheap and useful for test/fallback.

## Other rejected or marginal options

- Teqnivent U/AP402: curve suggests only about 1.4-1.6 kPa catalogue static at 1,700 m3/h, about 0.5 kPa at chamber density; too small for full 100 mm target.
- Soler & Palau CBT-N: direct-driven extraction fan range; largest CBT-130N is 1.1 kW / 1,910 m3/h max, low pressure near target flow; reject for main blower.
- U/ARP 251-252: about 140 mmH2O / 1.37 kPa at target flow; too low.
- Colasit CMVeco250/250-225: broad centrifugal family but curves shown only around 2.2-2.6 kPa max catalogue pressure; likely too low for full 100 mm target. Plastic cold suitability also uncertain.
- Large axial/AHU/biomass/extraction fans: high volume but wrong pressure class.
- FPZ regenerative/side-channel blower: high pressure but too low flow for 100 mm section. Example FPZ SCL e08-MS-7.5-3 is 5.5 kW and 110 inH2O pressure but only 331 CFM at 50 Hz, giving only about 40 kt through 100 mm, though viable for small 50 mm jet/test section.

## LMB aerospace fan route

Treat as technically interesting but cost/availability-gated.

LMB feedback:

- Hyperfan 160 can generate 476 l/s but only about 510 Pa at density 0.412 kg/m3; not enough pressure.
- MX150-01 example points per fan appear to be:
  - 200 l/s at 1360 Pa at 0.412 kg/m3
  - 270 l/s at 1020 Pa at 0.412 kg/m3
- Two MX150-01 fans may meet the flow target if arranged appropriately and if system pressure loss is around ~1 kPa.
- If system pressure loss is 2-3 kPa, two MX150-01 fans likely do not meet requirement.

Need before further design time:

- budgetary price per fan and for two-fan arrangement;
- lead time;
- required electrical supply/controller;
- whether two-fan arrangement is standard/off-the-shelf;
- -55 C and 24 kPa absolute suitability;
- whether a final solution within two weeks is practical.

## Design lever

Consider interchangeable nozzle/test-section inserts. Reducing from 100 mm to 70-80 mm dramatically reduces required flow.

A 93 mm effective EDF/test-section diameter is now plausible because the DS-51 casing ID is 93 mm and the required flow for 120 kt through 93 mm is about 0.419 m3/s / 1,510 m3/h.

## Search target

For industrial fan route, search for blowers with roughly:

- 1,700-2,000 m3/h at 4,000-5,000 Pa catalogue static pressure at density 1.2 kg/m3;
- 4-7.5 kW motor likely, depending family/efficiency;
- ~2800-3000 rpm or higher impeller speed via belt;
- usable VFD control;
- preferably belt-drive or remote-drive option so motor can remain outside pressure/cold boundary.

For EDF route, ask for:

- static ducted performance, thrust/flow/pressure data;
- continuous/semi-continuous duty ratings at 50/75/100% power;
- low-pressure 24 kPa absolute suitability;
- -55 C dry air/nitrogen suitability;
- ESC, battery/power, telemetry and cooling requirements;
- rotor containment/safety recommendations for fixed test rig.
