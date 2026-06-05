# RB Wingsuite Environmental Chamber

Shared working project repository for the RB Wingsuite / CreoKinetics environmental chamber build.

This repository is the live project source of truth for:

- parts selection and purchasing status;
- LN2 source, valve-train and cooling-coil design;
- airflow/blower selection;
- cRIO I/O and feedback architecture;
- safety interlocks and hazards;
- supplier RFQs and decision history.

## Current design intent

This is the intended working build, not a disposable prototype. The first assembled implementation should use robust, conservative, serviceable choices with limited iteration time. Backup paths are kept only where a subsystem fails major tests.

## Key files

| File | Purpose |
|---|---|
| `00_Project_Summary.md` | Project baseline, target condition, critical paths |
| `01_Parts_Register.csv` | Live parts/purchasing register |
| `02_Project_Todo.md` | Current open tasks |
| `03_LN2_System_Notes.md` | LN2 source, valve train, relief, tubing and coil notes |
| `04_Airflow_System_Notes.md` | Blower/fan selection and airflow notes |
| `05_IO_Schedule.csv` | cRIO I/O schedule and feedback signals |
| `06_Safety_Interlocks.md` | Safety interlocks and hazard controls |
| `07_Supplier_RFQs.md` | Supplier email/RFQ snippets |
| `08_Decision_Log.md` | Dated decision history |
| `supplier_emails/` | Supplier-specific notes and follow-ups |

## Workflow

Use Markdown and CSV files as the live records. Excel/PDF outputs can be generated as snapshots later, but should not be treated as the master records.
