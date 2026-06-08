# RT_Safety_Manager.vi Specification

## Purpose

Evaluate all software-visible safety permissives and gate actuator commands before they reach hardware outputs.

This VI supplements hardwired safety. It does not replace E-stop circuits, relief devices, or other required independent protection.

## Runs on

- cRIO-9068 Real-Time target

## Inputs

- `Scaled_IO.ctl`
- `Raw_IO.ctl`
- Requested `Actuator_Commands.ctl`
- Current `System_State.ctl`
- `Config.ctl`
- Watchdog and HMI communication status

## Outputs

- `Safety_Status.ctl`
- Safety-gated `Actuator_Commands.ctl`
- `Fault_Status.ctl`
- Requested state override: none, fault, or emergency stop

## Core permissives

- E-stop healthy
- Door/lid closed
- Chamber pressure OK
- Oxygen level OK, if fitted
- Fan healthy / airflow proven
- Critical temperature sensors valid
- Manual key enabled for manual mode
- No critical cRIO loop fault
- No stale command timeout

## Output gating rules

### LN2 valve

LN2 output may energise only when:

- Current state is `Run_Profile`, `Hold`, or authorised `Manual_Commissioning`.
- E-stop healthy.
- Door closed.
- Pressure OK.
- Oxygen OK if fitted.
- Fan / airflow proven.
- Critical temperature sensors valid.
- No critical fault active.

Otherwise LN2 output must be false.

### Fan enable

Fan enable may energise only when:

- E-stop healthy.
- Fan command is valid.
- No fan-specific hard inhibit is active.

Fault policy should decide whether the fan remains running during controlled warmup or fault recovery.

### Heater output, if fitted

Heater output may energise only when:

- E-stop healthy.
- Temperature sensors valid.
- Overtemperature condition not active.
- State allows heating.

## Fault outputs

Faults should include:

- Code
- Severity
- Human-readable message
- Timestamp
- Latching / non-latching flag
- Reset condition

## Audit requirement

Keep the safety logic explicit. Avoid clever compressed boolean expressions that are hard to inspect during commissioning.
