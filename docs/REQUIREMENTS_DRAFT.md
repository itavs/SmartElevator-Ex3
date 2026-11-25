# Requirements Inventory - Official Source Reviewed

## Status and purpose

This is a source-alignment inventory, not an approved SRS. Task 1 publication is complete. Task 2 documentation was authorized; the dedicated Task 2 problem definition in `OPTIMIZATION_PROBLEM.md` is completed within its documented scope, with A-01 through A-05 approved as project conventions and A-06, physical parameters, latency and scoped exceptions still open. This inventory remains a traceability summary. Do not choose numerical parameters, design interfaces or implement anything here.

Primary source: `I2SE_Exe3.docx.pdf`, supplied and reviewed on 2026-11-25; private source handling is described in `references/README.md`. Original English task summaries in official sequence are in `docs/ROADMAP.md`. No course source is reproduced here.

## Official requirements

| ID | Requirement inventory | Source |
|---|---|---|
| O-01 | Construct a repository. | Page 2, Task 1 |
| O-02 | Define the elevator-allocation optimization problem for a destination-floor request. | Page 2, Task 2 |
| O-03 | Define major software components for simulation and deployment on ESP32. | Page 2, Task 3 |
| O-04 | Define detailed abstractions, main classes, public methods and parameters. | Page 2, Task 4 |
| O-05 | Design the allocation method. | Page 2, Task 5 |
| O-06 | Define all simulation parameters in JSON, agreed upon through the class. | Page 2, Task 6 |
| O-07 | Define time-based requests using time, src and target, and an auto-generator taking the simulation JSON as input. | Page 2, Task 7 |
| O-08 | Implement a complete building/elevator simulation with time-based requests; test the allocation objective and provide an allocation GUI whose design is open. | Page 2, Task 8 |
| O-09 | Define a testing strategy. | Page 2, Task 9 |
| O-10 | Produce request-format output with allocation information and a line for each stop including elevator ID. | Page 2, Task 10 |
| O-11 | Implement allocation on an ESP microcontroller connected to the PC simulator by BLE or WiFi; the PC sends a source-destination request to the ESP. | Page 2, Task 11; ESP32 named in Task 3 |
| O-12 | Write a short description of the results to conclude the assignment. | Page 2, Task 12 |
| O-13 | Allocate online and minimize overall waiting time, defined from calling an elevator to reaching the destination. | Page 1, Problem statement |

Page 1 describes destination dispatch, sensors/monitoring and AI/traffic algorithms. The description is relevant context; the available text does not explicitly require every listed sensor or a machine-learning implementation.

## Lecturer recommendations and transcript interpretations

The previous R-01 through R-11 inventory was provisional. Its useful content is retained below with corrected evidence status; O-IDs above are the current official traceability identifiers.

| Previous ID | Retained understanding | Current evidence classification |
|---|---|---|
| R-01 | A configurable building and elevator fleet. | Official building/fleet simulation; configurability details from lectures and Task 6 parameter work. |
| R-02 | Requests contain creation time, origin and destination. | Official Task 7: time, src, target. |
| R-03 | Online decisions use currently available information rather than future requests. | Official online objective; information boundary is defined in completed Task 2; exact telemetry remains open. |
| R-04 | Model boarding, alighting, travel and door behavior. | Lecture interpretation; exact fidelity and values unresolved. |
| R-05 | Generate realistic traffic patterns and variable demand. | Generator officially required; traffic-pattern details are lecture recommendations. |
| R-06 | Aggregate request-to-destination time. | Official objective; the unweighted fixed-cohort sum is approved project convention A-03; exceptional edge-case handling remains open. |
| R-07 | Separate simulator and allocation policy through an interface. | Lecturer emphasis and project direction supporting official ESP deployment; interface not designed. |
| R-08 | Produce HLD and LLD. | Official Tasks 3 and 4, separately and in that order. |
| R-09 | Compare a baseline with alternative policies. | Lecturer recommendation; a second policy is not explicitly required by the official ToDo. |
| R-10 | Use 2D visualization and optional speed controls. | GUI officially required; 2D and speed controls remain recommendations. |
| R-11 | Consider portability early; defer physical hardware work. | Official ESP32 consideration in Task 3 and mandatory ESP implementation in Task 11. |

Lecture-derived scope guidance: evaluate one building at a time; do not optimize elevator procurement or coordinate buildings; avoid starting with hardware or complex 3D. These are not additional verbatim handout requirements.

## Project decisions and proposals

Approved workflow choices: English project artifacts, Hebrew owner communication, independent project scope, task-by-task approval, public repository visibility and Task 2 documentation. Task 1 is complete; Task 2 is completed within its documented scope and its seven documents are authorized for staging review; commit approval is pending; A-01 through A-05 are approved project conventions and A-06 remains open. Tasks 3-12 are unapproved.

Unapproved implementation proposals: seeded scenarios, a simple baseline first, optional comparison policies, CLI support alongside the required GUI, and any specific module/class structure. See `docs/DECISIONS.md`. JSON itself is official, not a proposal.

## Open questions requiring clarification or later approved work

- Is the class-agreed simulation JSON already available? What keys, units and parameters have been agreed?
- What are the intended capacity, service-range, travel, acceleration, doors, boarding and failure rules?
- A-03 approves the unweighted fixed-cohort objective and explicit reporting of incomplete requests in `OPTIMIZATION_PROBLEM.md`. Numerical penalties, timeouts and exceptional handling remain open.
- What exact schema represents allocations and stop records in Task 10?
- Which ESP32 board, language/toolchain and BLE or WiFi protocol should be used? What messages/state exchanges beyond the specified source-destination request are needed?
- Are additional manual-input modes required beyond the request list and auto-generator?
- What are the deadline, grading rubric, submission channel and demonstration format? Repository visibility has been approved as public.

The PDF specifies no mandated implementation language, numerical defaults, particular testing framework or coverage threshold. Its Guidelines heading is empty. Resolve these questions only within the relevant approved task; do not invent answers.
