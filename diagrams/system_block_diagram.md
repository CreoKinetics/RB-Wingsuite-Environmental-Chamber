# Environmental Chamber System Block Diagram

_Last updated: 2026-06-07_

## Purpose

High-level system block diagram for the RB Wingsuite environmental chamber build. This diagram captures major subsystems and interfaces rather than detailed fittings, wiring or fabrication geometry.

## Overall architecture

```mermaid
flowchart TB
    subgraph LN2["LN2 Cooling System"]
        CRYO[Statebourne Cryostor 60\nself-pressurising LN2 source]
        HOSE[Statebourne LN2 hose\n1.2-1.5 m target]
        VT[External LN2 valve train\nRV-101 + PI-101 + SV-101 + MV-101]
        COIL[Internal sealed LN2 cooling coil\nHX-101]
        LVENT[Always-open LN2/N2 vent\nto safe external discharge]
        CRYO --> HOSE --> VT --> COIL --> LVENT
    end

    subgraph CHAMBER["Environmental Chamber / Pressure Volume"]
        TS[Test section / camera volume\n~93-100 mm airflow path target]
        COIL_IN[Cooling coil inside airflow path]
        PITOT[Pitot/static pickup]
        CAM[Camera / test article]
        TEMP[Temperature sensors]
        COIL_IN --> TS
        CAM --- TS
        PITOT --- TS
        TEMP --- TS
    end

    subgraph AIR["Airflow System"]
        EDF[Schubeler EDF candidate\nDS-51-DIA HST]
        ESC[YGE Aureus 185 ESC\npreferred outside cold/low-pressure boundary]
        BAT[12S LiPo battery system\nor approved supplier-supported alternative]
        DUCT[Recirculating duct / nozzle / diffuser]
        EDF --> DUCT --> TS --> DUCT
        BAT --> ESC --> EDF
    end

    subgraph VAC["Vacuum / Purge / Vent System"]
        VPUMP[Vacuum pump]
        VISOL[Vacuum isolation valve]
        PURGE[Dry N2 purge/backfill source\nTBD: separate cylinder or Cryostor gas side]
        PINLET[Purge inlet valve / restrictor]
        CVENT[Controlled chamber vent valve]
        PRVCH[Independent chamber overpressure relief\nTBD]
        VPUMP --> VISOL --> CHAMBER
        PURGE --> PINLET --> CHAMBER
        CHAMBER --> CVENT --> SAFEVENT[Safe vent / extraction]
        CHAMBER --> PRVCH --> SAFEVENT
    end

    subgraph CONTROL["Control / DAQ"]
        CRIO[NI cRIO-9068]
        AI[Analogue input modules\nNI 9239 / 9203 / 9211 / 9219]
        DI[Digital input module\nNI 9421]
        DO[Digital output / relay modules\nNI 9475 / NI 9481]
        HMI[LabVIEW HMI / logging]
        CRIO --> AI
        CRIO --> DI
        CRIO --> DO
        CRIO --> HMI
    end

    subgraph SAFETY["Safety / Interlocks"]
        ESTOP[E-stop chain]
        O2[Oxygen depletion monitor]
        DOOR[Door/lid closed switch]
        PERM[Hardwired LN2 permissive chain]
        ALARM[Beacon / buzzer]
        ESTOP --> PERM
        O2 --> PERM
        DOOR --> PERM
        PERM --> DO
        DO --> ALARM
    end

    COIL -. physically inside .-> COIL_IN
    PITOT --> AI
    TEMP --> AI
    VT --> AI
    VT --> DO
    VPUMP --> DO
    VISOL --> DO
    PINLET --> DO
    CVENT --> DO
    ESC --> AI
    ESC --> DI
    DO --> ESC
    SAFETY --> CONTROL
```

## Major subsystem notes

### LN2 cooling system

- Primary LN2 source path is Statebourne Cryostor 60, pending service/check and hose confirmation.
- External LN2 valve train is not a custom manifold block initially; it is a supported assembly of cryogenic fittings, tees, reliefs, gauge, solenoid and metering valve.
- LN2 must remain inside sealed tubing/coil and exhaust to a safe external vent.
- LN2 must not be intentionally vented into the chamber/freezer atmosphere.

### Airflow system

Two parallel routes remain open:

1. Schubeler EDF route, currently strongest compact candidate.
2. Conventional high-pressure centrifugal/radial blower route, likely requiring an external sealed plenum or remote/belt-drive architecture.

For the EDF route:

- Fan/motor may need to sit inside the low-pressure recirculating airflow if Schubeler confirms suitability.
- ESC and batteries/power electronics should remain outside cold/low-pressure volume where possible.
- YGE Aureus manual currently indicates battery-only operation, not direct PSU operation.
- Rotor containment and overspeed/telemetry shutdown remain important design items.

### Vacuum / purge / chamber protection

- Chamber pressure target is approximately 24 kPa absolute.
- Purge/backfill system is still TBD.
- Use dry nitrogen purge/backfill if practical to reduce frost/moisture.
- Chamber overpressure protection is separate from LN2 line thermal relief.
- If LN2 coil failure can dump nitrogen into chamber, chamber relief/vent sizing must account for that credible fault.

### Control and safety

- NI cRIO-9068 is the main controller.
- NI 9239 handles key 0-10 V signals such as Keller absolute pressure and Dwyer Pitot differential pressure.
- NI 9211 handles thermocouples; NI 9219 now available as a universal spare/development input module.
- Digital outputs must drive interposing relays/contactors/drivers only, not high-power coils/loads directly.
- LN2 enable must require a hardwired safety permissive chain, not software command alone.

## Boundary assumptions

| Boundary | Current intent |
|---|---|
| LN2 pressure boundary | Cryostor + hose + external valve train + sealed coil + external vent |
| Chamber pressure boundary | Vacuum chamber/freezer pressure volume plus any sealed duct/plenum extensions |
| Cold boundary | Chamber/freezer interior and cold recirculating airflow path |
| Power electronics boundary | Prefer outside cold/low-pressure volume |
| Safety boundary | E-stop/O2/door/permissive chain independent of software |

## Open diagram actions

- Add exact Statebourne hose/outlet fitting after quote.
- Add exact HEROSE metering valve/manual valve/gauge/fittings after quote.
- Add final airflow route once Schubeler/industrial blower decision is made.
- Add chamber purge/vent/overpressure relief once chamber port layout is developed.
- Create separate wiring/interlock diagram once final actuators and sensors are selected.
