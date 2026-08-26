# Understanding Data Flows with Flowcharts

A **flowchart** is a diagram that visually represents the steps of a process using shapes and arrows, showing the sequence of actions, decisions, and outcomes from start to end.

- **Oval/rounded rectangle (Terminator)** — start/end points of a process
- **Arrow (Flow line)** — shows direction/sequence between shapes
- **Rectangle (Process)** — a step, action, or task
- **Trapezoid (Manual operation)** — a step done manually, not by a system
- **Parallelogram (Input/Output)** — data entering or leaving the process
- **Diamond/Rhombus (Decision)** — a yes/no or branching point
- **Cylinder (Database)** — represents data storage
- **Asymmetric/flag (Storage)** — represents a document or report generated in the process, Document shape with wavy bottom
- **Hexagon (Preparation)** — a setup or initialization step before the main process begins
- **Double-struck Rectangle (Subroutine)** — a step that's actually a separate, defined process elsewhere
- **Circle (Connector, Goto)** — links one part of the flowchart to another, often across pages

#### Shapes

```sh
Oval(start/end)
Hexagon{{setup}}
Rectangle[step]
Trapezoid[/Manuel step\]
Parallelogram[/input/output/]
Diamond_Rhombus{decision}
Flag>storage]
Cylinder[(database)]
DoubleStruck_Rectangle[[subroutine]]
Circle((goto))
```

## Mermaid Flowchart

> PROMPT: generate mermaid syntax ONLY. use all flow chart shapes. represent cbt exam web app data flow

```mermaid
flowchart TD
    Start([Student starts exam])
    Login[/Enter login credentials/]
    Auth{Valid credentials?}
    AuthFail[\Show error message\]
    LoadExam[[Load exam questions]]
    DB[(Exam database)]
    Manual[\Invigilator verifies ID/]
    Prep{{Initialize timer and settings}}
    Answer[Student answers question]
    NextQ{More questions?}
    Submit[Submit exam]
    Grade[[Auto-grade responses]]
    Report>Generate result document]
    Sync((Sync to server))
    End([Exam session ends])

    Start --> Manual
    Manual --> Login
    Login --> Auth
    Auth -- No --> AuthFail
    AuthFail --> Login
    Auth -- Yes --> Prep
    Prep --> DB
    DB --> LoadExam
    LoadExam --> Answer
    Answer --> NextQ
    NextQ -- Yes --> Answer
    NextQ -- No --> Submit
    Submit --> Grade
    Grade --> DB
    Grade --> Report
    Report --> Sync
    Sync --> End
```
