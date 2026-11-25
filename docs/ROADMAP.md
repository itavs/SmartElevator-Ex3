# Assignment 3 - Official Work Order (12 Tasks)

## Authority and current authorization

Source: `I2SE_Exe3.docx.pdf`, page 2, ToDo; supplied and reviewed on 2026-11-25. The source is kept privately outside the published repository. `references/I2SE_Exe3.docx.pdf` is a portable local lookup convention, not a claim that the file is currently present there; no source file has been copied or moved. Page 1 defines the online allocation objective and system context.

This roadmap supersedes the former eight-stage lecture-summary plan. Tasks below are original English paraphrases preserving the official numbering, sequence and meaning. They are not quotations or a substitute for the private handout. Stage N means official Task N; source review is preparatory work, not an additional assignment task.

**Current authorization:** the owner authorized Task 2 closure after verification and staging of exactly its seven documentation files. A-01 through A-05 remain approved project conventions; A-06, physical parameters, latency and scoped exceptions remain open. Tasks 3-12, implementation, dependency installation, commits and pushes are not authorized.

**Workflow:** follow Tasks 1-12 in numerical order, with owner approval before starting each task. Work top-down through problem definition, HLD, LLD and allocation design before implementation. The official order places the testing-strategy deliverable at Task 9; routine verification of an approved earlier task does not advance or complete Task 9.

**Status:** Task 1 is complete, including publication at `https://github.com/itavs/SmartElevator-Ex3`. Local and remote `main` were verified at initial commit `786d9b5c2f4c06e476a81fd6f11b6ff93a2fed98`. Task 2 is completed within the documented scope in `docs/OPTIMIZATION_PROBLEM.md`, with its documentation prepared for staged review; Tasks 3-12 remain pending and unapproved. Reviewing the PDF and documenting requirements does not complete the problem-definition or design tasks.

## Reading the task entries

- **Official requirement (paraphrased):** an original summary of the numbered source item, without added requirements.
- **Deliverables:** our planning interpretation of the output needed to address the instruction.
- **Completion criteria:** proposed project review gates, not an official grading rubric. These remain subject to owner review and clarification.
- File names, languages, frameworks, numeric defaults and acceptance thresholds are not prescribed unless the source explicitly says so.

## Task 1 - Construct a repo

**Official requirement, paraphrased (page 2, item 1):**

Establish a repository dedicated to this assignment.

**Deliverables:** An independent local Git repository for this project, preserving the existing directory structure and documentation.

**Completion criteria (proposed project gate):** After separate authorization: the repository root resolves to this directory; existing files remain intact; repository status is inspected and reported. No commit, remote or publication is required by this local completion gate.

**Status:** Completed - public repository `https://github.com/itavs/SmartElevator-Ex3`, initial commit `786d9b5c2f4c06e476a81fd6f11b6ff93a2fed98`, local/remote `main` verified equal and working tree clean at the Task 1 handoff. Private course sources remain excluded.

## Task 2 - Define the optimization problem

**Official requirement, paraphrased (page 2, item 2):**

Formulate the optimization problem for choosing an elevator when a passenger supplies a destination-floor request.

**Deliverables:** A reviewed problem-definition document describing the allocation input/output, online information boundary, objective, scope, assumptions and unresolved constraints.

**Completion criteria (proposed project gate):** The owner can review the problem, intended metric and assumptions without implementation. Unspecified rules are identified rather than invented.

**Status:** Completed - `docs/OPTIMIZATION_PROBLEM.md` defines the objective, online boundary, inputs/outputs and approved A-01 through A-05. A-06, latency and scoped exceptions remain open. The owner authorized documentation staging only; commit approval is pending and Task 3 is not authorized.

## Task 3 - High-level design

**Official requirement, paraphrased (page 2, item 3):**

Identify the major software components at HLD level, accounting for both simulation of the chosen approach and its execution on an ESP32 microcontroller.

**Deliverables:** An HLD document describing the major components and their responsibilities, covering both PC simulation and ESP32 allocation deployment.

**Completion criteria (proposed project gate):** The owner has reviewed the component boundaries and PC/ESP32 responsibilities; unresolved transport details remain explicit. No class-level design is required here.

**Status:** Pending; requires task-specific approval.

## Task 4 - Low-level design

**Official requirement, paraphrased (page 2, item 4):**

Develop the LLD abstraction and identify the principal classes, including their public operations and associated parameters.

**Deliverables:** An LLD document describing the main classes, public methods and parameters, consistent with the reviewed HLD.

**Completion criteria (proposed project gate):** The main class contracts are reviewable and traceable to the HLD; unresolved signatures or semantics are marked. No implementation is required.

**Status:** Pending; requires task-specific approval.

## Task 5 - Design the allocation method

**Official requirement, paraphrased (page 2, item 5):**

Specify the approach that will make elevator-allocation decisions.

**Deliverables:** A documented allocation method with decision rules, required state and illustrative decision traces.

**Completion criteria (proposed project gate):** The owner can follow an allocation decision from a request and current state; tradeoffs and assumptions are explicit. No optimality claim is made without evidence.

**Status:** Pending; requires task-specific approval.

## Task 6 - Simulation parameters in JSON

**Official requirement, paraphrased (page 2, item 6):**

Enumerate the simulation settings in a JSON representation and coordinate agreement on those settings with the class.

**Deliverables:** A detailed simulation-parameter list in JSON, accompanied by evidence of class agreement or an explicitly unresolved clarification.

**Completion criteria (proposed project gate):** The JSON is syntactically valid and documents the agreed parameters. The class-agreement condition is verified or a lecturer clarification is obtained; local preference alone does not satisfy that requirement.

**Status:** Pending; requires task-specific approval.

## Task 7 - Time-based requests and auto-generator

**Official requirement, paraphrased (page 2, item 7):**

Describe requests as a chronological list containing time, src and target, and define an automatic request generator driven by the simulation JSON.

**Deliverables:** A time-based request-list definition using time, src and target, and an auto-generator that accepts the simulation JSON.

**Completion criteria (proposed project gate):** The generator accepts the agreed JSON and produces requests in the defined format. Checks against the agreed configuration and actual execution results are recorded.

**Status:** Pending; requires task-specific approval.

## Task 8 - Complete simulation and allocation GUI

**Official requirement, paraphrased (page 2, item 8):**

Build the full building-and-elevator simulation using timestamped passenger requests. Use it to evaluate the allocation approach against total call-to-destination time, and provide a graphical allocation interface with a freely chosen visual design.

**Deliverables:** A complete building/elevator simulation accepting time-based requests, evaluating the allocation method against total request-to-destination time, with an allocation GUI.

**Completion criteria (proposed project gate):** A documented scenario runs through the simulation and GUI; allocation behavior and total request-to-destination measurements are demonstrated. Any limitations are reported. This evidence does not mark Task 9 complete.

**Status:** Pending; requires task-specific approval.

## Task 9 - Testing strategy

**Official requirement, paraphrased (page 2, item 9):**

Document how the system will be tested.

**Deliverables:** A documented testing strategy describing what will be checked, how it will be checked and how evidence will be recorded.

**Completion criteria (proposed project gate):** The owner has reviewed coverage, test inputs, expected outcomes and the evidence/reporting approach. The PDF specifies no particular framework or coverage threshold.

**Status:** Pending; requires task-specific approval.

## Task 10 - Simulator output format

**Official requirement, paraphrased (page 2, item 10):**

Extend the request-list output structure with allocation information, and emit a separate entry for every elevator stop that identifies the elevator.

**Deliverables:** Simulator output using the request-list format with allocation information, plus a line for every stop including the elevator ID.

**Completion criteria (proposed project gate):** A sample output is checked for allocation data and every simulated stop with elevator ID. Any schema ambiguity is clarified or explicitly approved before implementation.

**Status:** Pending; requires task-specific approval.

## Task 11 - ESP32 implementation and BLE/WiFi integration

**Official requirement, paraphrased (page 2, item 11):**

Run the allocation approach on an ESP device and link it wirelessly to the PC simulation using either BLE or WiFi. The PC must transmit an origin-and-destination request to that device.

**Deliverables:** The allocation method running on an ESP microcontroller (ESP32 is specified in Task 3), connected to the PC simulator using BLE or WiFi.

**Completion criteria (proposed project gate):** An end-to-end run demonstrates the allocation method executing on the ESP and a source-destination request sent by the PC over the selected wireless link; observed communication and allocation behavior are recorded.

**Status:** Pending; requires task-specific approval.

## Task 12 - Results and conclusion

**Official requirement, paraphrased (page 2, item 12):**

Finish the assignment with a brief written account of the results.

**Deliverables:** A short written description of results, including the observed outcomes and relevant limitations.

**Completion criteria (proposed project gate):** The written summary reports actual results and limitations and checks the deliverables against Tasks 1-11. Unknown submission rules are flagged, not asserted.

**Status:** Pending; requires task-specific approval.

## Mapping from the superseded lecture-summary roadmap

This table preserves useful context without retaining the former execution order.

| Former stage | Official tasks | Change required by the handout |
|---|---|---|
| 0 - Source/setup | Preparatory review | Source has now been reviewed; it is not an official numbered task. |
| 1 - Repository, scope and specification | 1, then 2 | Repository work is separate from problem definition. |
| 2 - Formal problem | 2 | Retain problem-model questions for Task 2; do not execute them during Task 1. |
| 3 - HLD and LLD | 3, then 4 | Separate the two design deliverables; include ESP32 deployment in HLD. |
| 4 - Minimal simulation | 8 | Do not begin simulation ahead of official Tasks 5-7. |
| 5 - Baseline and checks | 5, 8, 9 | Separate allocation design, implementation and testing strategy. A baseline is a lecture recommendation. |
| 6 - Scenarios, logs and evaluation | 6, 7, 8, 10 | Define JSON and requests before the simulation; explicitly address output records. |
| 7 - Alternative strategy | Optional recommendation | The official ToDo does not explicitly require a second strategy. |
| 8 - Visualization and handoff | 8, 11, 12 | GUI and ESP implementation are required; hardware is not merely a possible extension. |

## Requirement boundaries and open questions

- JSON configuration and class agreement are explicit in Task 6; parameter names and values are not supplied.
- Time-based requests and their JSON-driven auto-generator are explicit in Task 7.
- An allocation GUI is required in Task 8; its design is open. A 2D view and speed controls are lecture recommendations, not mandated designs.
- ESP32 is named in Task 3; Task 11 requires an ESP allocation implementation and BLE or WiFi communication. The protocol and board details are open.
- Page 1 defines waiting time as the interval from the call to arrival at the destination. Task 2 defines the unweighted fixed-cohort sum under approved project convention A-03; exceptional edge-case handling and physical parameters remain open.
- The page-1 discussion of sensors and AI provides context; it does not establish an explicit obligation to implement all sensors or machine learning.
- Language, deadline, grading rubric, submission format and demonstration format are not specified. The Guidelines heading on page 2 is empty.

## End-of-task report

For each separately approved task, report the source instruction, files changed, decisions/proposals, checks actually run and their results, remaining questions and the next approval gate. Never claim an unexecuted test or later task is complete.
