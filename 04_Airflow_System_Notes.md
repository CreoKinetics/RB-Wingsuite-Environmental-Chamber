# Airflow System Notes

_Last updated: 2026-06-05_

## Target

Approximate current target: 120 kt TAS / 61.7 m/s through ~100 mm test section at 24 kPa absolute and -55 C.

This implies roughly:

- 0.47-0.49 m3/s actual flow
- ~1,700 m3/h
- ~1,000 CFM

## Preferred technology

Target high-pressure centrifugal/radial blower. Avoid treating low-pressure HVAC fans, carpet dryers, or leaf blowers as final solutions. Regenerative/side-channel blowers have high pressure but usually too little flow for a 100 mm test section.

## Current strongest selector candidates

### EV-APF561

Fan selector result:

- Requested: 1,745 m3/h at 4,400 Pa static, 20 C at 0 m, density 1.2 kg/m3.
- Returned: 1,872 m3/h at 5,062 Pa static, 2900 rpm.
- Equivalent at chamber density 0.412 kg/m3: approximately 1,872 m3/h at 1.74 kPa static, assuming density scaling.
- Current status: strongest calculator-matched industrial candidate so far; confirm curve, drive arrangement, motor power/voltage, price and lead time.

### EV-MPR502

Fan selector result:

- Requested: 1,745 m3/h at 4,400 Pa static, 20 C at 0 m, density 1.2 kg/m3.
- Returned: 1,746 m3/h at 4,407 Pa static, 2900 rpm.
- Equivalent at chamber density 0.412 kg/m3: approximately 1,746 m3/h at 1.51 kPa static.
- Current status: serious candidate but less margin than EV-APF561; may be attractive if cheaper/smaller/more available.

### EV-APF range chart note

Screenshot of APF range curve shows EV-APF561A/B at the lower end of the range and larger EV-APF632/711/802/901 families above it. Our 100 mm target point is approximately 1,745 m3/h / 1,027 CFM and 4,400 Pa / 17.7 inWG at catalogue density. EV-APF561 appears to cover this region, with the selector returning a slightly higher operating point. Larger APF models may give more margin but will increase motor power, size and cost.

## Airflow pressure-boundary architecture

As fan size increases, a fully internal fan becomes less practical. Current preferred architecture to investigate is:

```text
freezer/chamber pressure volume
-> short vacuum-rated duct
-> external sealed blower/plenum box
-> short vacuum-rated return duct
-> chamber/test section
```

The fan/blower impeller and scroll should be inside the low-pressure recirculation boundary, but the motor should preferably remain outside the pressure/cold boundary where possible.

Belt drive or remote shaft drive is now a serious option because it allows:

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

## Current best used candidate

ACI VBW9-00114, with CMG SLA-90L-2 motor plate:

- 220-240 V delta, 50 Hz, 2.2 kW, 2830 rpm
- 380-415 V star, 50 Hz, 2.2 kW, 2830 rpm
- 440-480 V star, 60 Hz, 2.5 kW, 3395 rpm
- bearing 6205-2RS-C3

This is VFD-friendly if run from a suitable 230 V single-phase input to 230 V three-phase output VFD, motor linked delta. Two identical VBW9 units in series remain an interesting low-cost pressure-increase experiment, but curve is unknown.

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

## Search target

Search for industrial centrifugal/radial blowers with roughly:

- 1,700-2,000 m3/h at 4,000-5,000 Pa catalogue static pressure at density 1.2 kg/m3;
- 4-5.5 kW motor likely, depending family/efficiency;
- ~2800-3000 rpm;
- usable VFD control;
- preferably belt-drive or remote-drive option so motor can remain outside pressure/cold boundary.
