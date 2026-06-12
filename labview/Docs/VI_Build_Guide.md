# LabVIEW VI Build Guide

This guide gives the recommended build order for creating the native LabVIEW 2019 VIs from the text specifications in this folder.

## 1. Create the LabVIEW project

1. Open LabVIEW 2019.
2. Create a new project named `RB_Wingsuite_Environmental_Chamber.lvproj`.
3. Add the cRIO-9068 as a Real-Time target.
4. Add the detected C Series modules under the cRIO chassis.
5. Use Scan Interface for normal analogue and digital I/O unless a specific module or timing requirement requires FPGA.

## 2. Create typedefs first

Create strict typedefs before writing logic:

- `System_State.ctl` - enum matching `State_Machine.md`.
- `Raw_IO.ctl` - unscaled channel values and raw booleans.
- `Scaled_IO.ctl` - engineering-unit values and validity flags.
- `Command_Setpoints.ctl` - operator and profile setpoints.
- `Actuator_Commands.ctl` - requested actuator outputs before safety gating.
- `Safety_Status.ctl` - permissives and trip states.
- `Fault_Status.ctl` - active fault code, severity, and message.
- `Config.ctl` - limits, scaling coefficients, logging settings, and mode options.

## 3. Build `RT_IO_Manager.vi`

Purpose:

- Read all C Series inputs.
- Apply scaling.
- Detect invalid channels.
- Publish `Raw_IO` and `Scaled_IO` clusters.
- Write final safety-gated outputs.

Initial implementation may use simulated I/O values to allow development without hardware.

## 4. Build `RT_Safety_Manager.vi`

Purpose:

- Evaluate E-stop, door, pressure, fan, oxygen, sensor validity, watchdog and manual key states.
- Generate `Safety_Status`.
- Gate all actuator commands.
- Generate fault codes for unsafe conditions.

This VI should be simple, explicit, and easy to audit.

## 5. Build `RT_Main.vi`

Purpose:

- Own the main state machine.
- Start and coordinate all loops.
- Apply state transition rules.
- Handle shutdown.

Use a queued message handler or equivalent architecture. Keep hardware-specific I/O out of the state machine.

## 6. Build `RT_Control_Loop.vi`

Purpose:

- Convert setpoints and measured values into actuator requests.
- Implement temperature ramping, cooling demand, fan demand and optional heater demand.
- Never directly write outputs.

Outputs from this VI must pass through `RT_Safety_Manager.vi` before reaching hardware.

## 7. Build `RT_Logger.vi`

Purpose:

- Log scaled values, state, commands, final outputs, safety status and faults.
- Use TDMS for run data.
- Use CSV or text for event/fault logs.

Files should be bounded and periodically copied to the host PC.

## 8. Build `HMI_Main.vi`

Purpose:

- Display chamber status.
- Allow start/stop and setpoint/profile requests.
- Show safety permissives and active faults.
- Provide manual commissioning panel when authorised.

The HMI should send requests, not direct output commands.

## 9. Commissioning order

1. Verify cRIO target, modules and deployment.
2. Confirm every input changes correctly in raw I/O view.
3. Confirm scaling and range checks.
4. Confirm all outputs are de-energised by default.
5. Test E-stop and hardwired safety chain.
6. Test door, pressure, oxygen and fan permissives.
7. Test stack light / indicator outputs.
8. Test fan enable and speed command without LN2.
9. Test LN2 solenoid command with supply isolated or safely vented.
10. Perform low-duty LN2 commissioning only after permissives and logging are proven.

## 10. Coding conventions

- Use typedef clusters for all cross-VI data.
- Use explicit fault codes rather than free text only.
- Centralise scaling in one VI or library.
- Centralise output safety gating in one VI.
- Log all operator commands and rejected commands.
- Use descriptive tag names matching `IO_Map.csv`.
- Avoid hidden local variables for safety-related data.
- Prefer clear block diagrams over compact clever code.
