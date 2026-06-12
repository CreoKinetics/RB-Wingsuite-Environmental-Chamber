# RT_IO_Manager.vi Specification

## Purpose

Single owner of C Series I/O access. Reads raw inputs, applies scaling and validation, and writes final safety-gated outputs.

No other VI should directly write actuator outputs.

## Runs on

- cRIO-9068 Real-Time target

## Inputs

- Module references or Scan Engine variables
- Output command cluster after safety gating
- Configuration/scaling cluster
- Simulation mode flag

## Outputs

- `Raw_IO.ctl`
- `Scaled_IO.ctl`
- I/O fault flags
- Output write status

## Responsibilities

### Input acquisition

- Read all analogue inputs.
- Read all digital inputs.
- Timestamp acquisition cycles.
- Preserve raw values for diagnostics.

### Scaling

- Thermocouple to degC.
- Voltage/current to engineering units.
- Boolean input normalisation so `True` means healthy where appropriate.

### Validation

- Detect open thermocouples.
- Detect out-of-range analogue values.
- Detect stale values.
- Flag missing or failed module reads.

### Output write

- Write only safety-gated final outputs.
- Apply default safe values on I/O manager error.
- Never use HMI direct commands.

## Suggested update rates

- Analogue and digital read: 10-50 Hz.
- Output write: 10-50 Hz or on command change.

## Simulation mode

Provide simulated values for software development without hardware. Simulation mode must be clearly indicated on the HMI and in logs.

## Notes

Keep all tag names aligned with `Docs/IO_Map.csv`.
