# HMI_Main.vi Specification

## Purpose

Primary PC operator interface for monitoring, command requests, commissioning controls, trend display and fault acknowledgement.

The HMI must not directly drive cRIO hardware outputs. It sends requests to the cRIO, and the cRIO validates them.

## Runs on

- Windows host PC with LabVIEW 2019 runtime or development environment

## Inputs

- cRIO status stream
- Operator interactions
- Profile/configuration files

## Outputs

- Command requests to cRIO
- Setpoint/profile requests
- Fault acknowledgement requests
- Manual commissioning requests

## Main screens

1. Overview
2. Temperatures
3. LN2 System
4. Airflow System
5. Safety Inputs
6. Raw I/O
7. Manual Commissioning
8. Fault History
9. Run Profile
10. Logs / Export

## Overview screen

Show:

- Current state
- Chamber temperature summary
- Active setpoint
- LN2 permitted / inhibited
- Fan status
- Safety permissive summary
- Active fault banner
- Start, stop and acknowledge controls

## Manual commissioning screen

Manual controls require:

- cRIO in `Manual_Commissioning` state.
- Manual key switch enabled.
- E-stop healthy.
- Relevant permissives healthy.

Manual controls should include timeouts and conservative limits.

## Fault presentation

Faults should show:

- Severity
- Fault code
- Description
- First timestamp
- Current active/cleared state
- Required reset condition

## Command handling

All operator commands should include:

- Timestamp
- Command type
- Requested value
- Optional user/comment

The cRIO should return accepted/rejected status with reason.

## HMI disconnect behaviour

The cRIO remains the authority. If the HMI disconnects, the cRIO continues safety logic and either maintains the current safe automatic state or transitions according to the configured fault policy.
