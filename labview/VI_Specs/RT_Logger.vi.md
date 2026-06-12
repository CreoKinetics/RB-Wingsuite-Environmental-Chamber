# RT_Logger.vi Specification

## Purpose

Record run data, event history, state transitions, operator commands and faults from the cRIO Real-Time application.

## Runs on

- cRIO-9068 Real-Time target

## Inputs

- `Scaled_IO.ctl`
- `Raw_IO.ctl`, optional lower-rate diagnostic logging
- `System_State.ctl`
- `Safety_Status.ctl`
- Requested and final `Actuator_Commands.ctl`
- `Fault_Status.ctl`
- Operator command/event queue
- Logging configuration

## Outputs

- TDMS run file
- CSV or text event/fault log
- Logger health status
- Disk space warning

## Data files

Suggested structure on cRIO local storage:

```text
/RB_Wingsuite_Data/
    YYYY-MM-DD_Run_001.tdms
    YYYY-MM-DD_Run_001_events.csv
    YYYY-MM-DD_Run_001_config.json
```

## Required logged groups

- Temperatures
- Pressures
- Airflow / fan data
- LN2 command and permissive state
- Safety inputs and permissives
- State machine state
- Operator commands
- Faults and warnings

## Event log entries

Each event should include:

- Timestamp
- Event type
- Current state
- User/source if available
- Message
- Previous value
- New value

## Fault log entries

Each fault should include:

- Timestamp
- Fault code
- Severity
- Latching flag
- Reset condition
- Active state
- Relevant channel/tag

## Failure behaviour

If logging fails, the system should raise a fault or warning depending on test criticality. Logging failure must not prevent safety logic from executing.
