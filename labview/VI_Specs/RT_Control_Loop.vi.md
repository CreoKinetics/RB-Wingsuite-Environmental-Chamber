# RT_Control_Loop.vi Specification

## Purpose

Convert operator/profile setpoints and measured chamber values into requested actuator commands.

This VI must not write hardware outputs directly. Its outputs are requests only and must pass through `RT_Safety_Manager.vi`.

## Runs on

- cRIO-9068 Real-Time target

## Inputs

- `Scaled_IO.ctl`
- `Command_Setpoints.ctl`
- `System_State.ctl`
- `Config.ctl`
- Previous controller state / integrator values

## Outputs

- Requested `Actuator_Commands.ctl`
- Controller diagnostic values
- Control-loop fault or warning flags

## Temperature control

Suggested first implementation:

1. Apply setpoint ramp limiting.
2. Select control temperature, initially chamber air average or primary validated sensor.
3. Calculate temperature error.
4. Generate cooling demand from staged control or conservative PID.
5. Convert cooling demand to LN2 solenoid duty-cycle request or proportional demand.
6. Apply minimum on/off timing and maximum duty-cycle limits.

## LN2 control notes

- Avoid fast valve chatter.
- Use conservative duty-cycle limits during commissioning.
- Inhibit integrator wind-up when LN2 is not permitted.
- Log cooling demand even when safety gating blocks the final output.
- Keep solenoid/proportional valve driver details out of the main control logic.

## Fan control

Use abstract fan commands:

- `Fan_Enable_Request`
- `Fan_Speed_Demand_Percent`
- `Fan_Mode`

Map these to actual hardware in the I/O/output driver layer.

## State-dependent behaviour

| State | Control behaviour |
|---|---|
| `Idle_Safe` | All requests safe. |
| `Manual_Commissioning` | Requests come from manual panel but are limited. |
| `Pre_Run_Check` | Fan pre-start or readiness checks only. |
| `Run_Profile` | Automatic control active. |
| `Hold` | Automatic control active at hold setpoint. |
| `Controlled_Warmup` | LN2 request zero; airflow/heater recovery as configured. |
| `Fault` | Requests safe unless fault policy explicitly allows fan purge. |
| `Emergency_Stop` | All requests safe. |

## Diagnostics

Expose to HMI/logs:

- Active setpoint
- Ramp-limited setpoint
- Control temperature
- Temperature error
- Cooling demand percent
- LN2 duty-cycle request
- Fan demand percent
- Controller saturation flags
