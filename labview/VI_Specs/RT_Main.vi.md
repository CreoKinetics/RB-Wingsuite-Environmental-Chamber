# RT_Main.vi Specification

## Purpose

Top-level Real-Time application VI for the cRIO-9068. Owns application start-up, loop launch, state machine execution, fault handling and controlled shutdown.

## Runs on

- cRIO-9068 Real-Time target

## Inputs

- Configuration file path or default config cluster
- HMI command queue or network stream
- Stop request

## Outputs

- System state
- Fault status
- HMI status stream
- Log events

## Internal loops

Suggested parallel loops:

1. State machine loop, 10 Hz.
2. I/O acquisition loop, 10-50 Hz.
3. Safety loop, 20-50 Hz.
4. Control loop, 5-20 Hz.
5. Logging loop, 1-10 Hz.
6. HMI communication loop, 2-10 Hz.

## State machine

Use `System_State.ctl` with states defined in `Docs/State_Machine.md`.

The state machine should:

- Enforce valid transitions only.
- Log every transition.
- Reject unsafe HMI requests.
- Enter `Fault` or `Emergency_Stop` when commanded by the safety manager.

## Safe start behaviour

On start-up:

1. Initialise all command clusters to safe defaults.
2. Write safe output states before accepting HMI commands.
3. Start logging and fault manager.
4. Enter `Self_Check`.

## Error handling

- Any unrecoverable loop error should request `Fault` or `Emergency_Stop` depending severity.
- Loss of HMI comms must not stop the cRIO from maintaining safety.
- Shutdown should close logs and write final safe outputs.
