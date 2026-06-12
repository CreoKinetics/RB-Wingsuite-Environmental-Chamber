# LabVIEW Starter Pack

This folder defines the proposed LabVIEW 2019 implementation structure for the RB Wingsuite Environmental Chamber using a cRIO-9068 controller.

The files in this folder are intentionally text-based so they can be reviewed in GitHub. Native `.vi` files should be created in the LabVIEW 2019 IDE from these specifications rather than generated externally.

## Target

- LabVIEW version: 2019
- Controller: NI cRIO-9068
- Recommended execution model: LabVIEW Real-Time on cRIO as system authority
- Recommended I/O mode: Scan Engine / Scan Interface for ordinary I/O
- FPGA use: only where timing, pulse generation/counting, module support, or watchdog behaviour requires it

## Design principles

1. The cRIO owns all real control and safety permissive decisions.
2. The PC HMI sends setpoints and commands but never directly drives outputs.
3. All actuator outputs pass through the safety manager before reaching hardware.
4. LN2 valves fail closed on power loss, software fault, or critical permissive loss.
5. I/O mapping, scaling, safety logic, and VI interfaces remain version-controlled.
6. Manual commissioning mode must remain safety-gated and fully logged.

## Suggested LabVIEW project layout

```text
RB_Wingsuite_Environmental_Chamber.lvproj

/Host_PC
    HMI_Main.vi
    Trend_Viewer.vi
    Recipe_Editor.vi
    Manual_Commissioning_Panel.vi

/cRIO-9068 RT Target
    RT_Main.vi
    RT_System_Init.vi
    RT_IO_Manager.vi
    RT_Safety_Manager.vi
    RT_Control_Loop.vi
    RT_Logger.vi
    RT_Comms_To_Host.vi
    RT_Fault_Manager.vi

/Shared
    /TypeDefs
    /Scaling
    /Fault_Codes
    /State_Machine
```

## Files in this starter pack

- `Docs/IO_Map.csv` - initial channel map template.
- `Docs/Safety_Matrix.csv` - safety permissive and trip matrix.
- `Docs/State_Machine.md` - operating states and transition logic.
- `Docs/VI_Build_Guide.md` - practical build order in LabVIEW.
- `VI_Specs/*.vi.md` - implementation specs for the main VIs.

## First implementation target

Build enough to support safe manual commissioning first:

1. cRIO boots to safe state.
2. Inputs are visible, scaled, and range-checked.
3. Safety permissives are evaluated.
4. Manual fan and LN2 commands are possible only when permissives allow.
5. All command, state, and fault events are logged.

Automatic profiles should be added after basic I/O, interlocks, and manual commissioning are proven.
