# LabVIEW RT State Machine

This document defines the initial cRIO Real-Time state machine for the RB Wingsuite Environmental Chamber.

The state machine should run on the cRIO-9068. The host PC HMI may request transitions, but the cRIO must validate them against safety permissives.

## State list

| State | Purpose | Output policy |
|---|---|---|
| `Boot` | Start-up, initialise variables and hardware references. | All hazardous outputs safe. |
| `Self_Check` | Validate module presence, configuration, sensor plausibility, and safety inputs. | All hazardous outputs safe. |
| `Idle_Safe` | System ready, no active test. | LN2 closed; fan off or low purge if explicitly permitted. |
| `Manual_Commissioning` | Engineering manual control for wiring, sensors, fan and LN2 checks. | Safety-gated manual outputs only. |
| `Pre_Run_Check` | Confirm run permissives before automatic profile. | Prepare fan and logging; LN2 still inhibited until checks pass. |
| `Run_Profile` | Automatic test profile execution. | Normal closed-loop control with safety gating. |
| `Hold` | Maintain a target condition. | Normal closed-loop control with safety gating. |
| `Controlled_Warmup` | Recover chamber towards safe ambient condition. | LN2 closed; airflow managed; heater if fitted and permitted. |
| `Fault` | Non-emergency fault handling. | Outputs according to fault severity; hazardous outputs normally safe. |
| `Emergency_Stop` | Emergency safety state. | Hazardous outputs removed. |
| `Shutdown` | Controlled software shutdown. | Outputs parked safe; logs closed. |

## Transition rules

### `Boot` to `Self_Check`

Allowed when:

- RT application has initialised.
- Configuration file has loaded or defaults have been applied.
- I/O manager has started without fatal error.

### `Self_Check` to `Idle_Safe`

Allowed when:

- Required C Series modules are detected.
- Safety inputs are readable.
- Critical sensors are valid or explicitly bypassed for commissioning.
- Output safe state has been written and verified where possible.

### `Idle_Safe` to `Manual_Commissioning`

Allowed when:

- Manual key switch is enabled.
- E-stop is healthy.
- No critical fault is active.
- Operator has requested commissioning mode from HMI.

### `Idle_Safe` to `Pre_Run_Check`

Allowed when:

- Operator requests automatic run.
- Test profile is valid.
- Required sensors are valid.
- Safety chain is healthy.

### `Pre_Run_Check` to `Run_Profile`

Allowed when:

- Door/lid closed.
- E-stop healthy.
- Chamber pressure OK.
- Oxygen level OK if sensor fitted.
- Fan health or airflow proof OK.
- Logging started.
- cRIO has accepted current setpoint profile.

### `Run_Profile` to `Hold`

Allowed when:

- Profile requests hold segment, or chamber reaches defined tolerance band.

### `Run_Profile` or `Hold` to `Controlled_Warmup`

Allowed when:

- Profile completes.
- Operator requests normal stop.
- Non-critical condition requires controlled recovery.

### Any state to `Fault`

Required when:

- Non-emergency fault occurs.
- Sensor invalidity prevents safe automatic control.
- Host comms timeout occurs in a state where operator confirmation is required.

### Any state to `Emergency_Stop`

Required when:

- E-stop unhealthy.
- Hard safety chain reports emergency state.
- Critical pressure, oxygen, or watchdog fault requires immediate safe state.

### `Fault` to `Idle_Safe`

Allowed when:

- Fault condition has cleared.
- Operator has acknowledged the fault.
- Safety manager confirms safe permissive set.

### `Emergency_Stop` to `Self_Check`

Allowed when:

- E-stop is restored.
- Operator performs reset.
- Outputs have remained in safe state.

## Implementation notes

- Use a typedef enum for state names.
- Log every state transition with timestamp and reason.
- Reject HMI transition requests that are not valid for the current state.
- Do not allow HMI manual controls to bypass safety gating.
- Store the previous state and previous valid automatic state for recovery diagnostics.
