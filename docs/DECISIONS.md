# Decisions, Proposals and Open Questions

## Approved owner workflow decisions

- D-01: This is an independent Assignment 3 project, separate from all other projects.
- D-02: A dedicated agent uses this project's `AGENTS.md`.
- D-03: Code, comments, documents, filenames and commit messages are English; owner communication is Hebrew.
- D-04: Follow the official tasks in numerical order with approval before each task and major decisions.
- D-05: No external repository creation, commit, push or publication without explicit authorization.
- D-06 (2026-11-25): The owner approved updating existing planning documentation to match the official PDF. That approval covered documentation alignment; subsequent Task 1 permissions are recorded in D-08 and D-09.
- D-07: Preserve the existing project structure and useful documentation; keep the approach top-down.
- D-08 (2026-11-25): The owner approved local Git setup on `main`, then one initial commit and creation/publication of the public `itavs/SmartElevator-Ex3` repository. No later assignment task is authorized.
- D-09 (2026-11-25): Reuse a consistent prior commit identity in local Git configuration only; remove personal absolute paths; preserve but ignore lecture notes; paraphrase the official task list and exclude private course sources from publication.

## Official constraints, not implementation decisions

- S-01: `I2SE_Exe3.docx.pdf` is authoritative. It was supplied and reviewed on 2026-11-25. `docs/ROADMAP.md` now follows its 12 tasks rather than the former eight-stage provisional sequence.
- S-02: Page 1 defines the online objective as total time from calling an elevator until reaching the destination.
- S-03: HLD and LLD are separate Tasks 3 and 4. ESP32 deployment must be considered in HLD.
- S-04: JSON simulation parameters agreed upon through the class are required by Task 6. Former proposal P-02 is superseded by this official requirement; the actual schema remains open.
- S-05: The time-based request list and JSON-driven auto-generator are required by Task 7.
- S-06: An allocation GUI is required by Task 8; its visual design is open.
- S-07: Task 10 requires allocation/stop output records; Task 11 requires ESP allocation execution and BLE or WiFi communication with the PC simulator. Hardware is an eventual deliverable, not merely an extension.

## Lecturer recommendations / transcript interpretations

- L-01: Separate the simulator and allocator through a clear interface.
- L-02: Begin with an understandable baseline and evaluate alternatives on the same scenarios.
- L-03: Use realistic traffic patterns; simple 2D visualization and time-speed controls may help explain results.
- L-04: Keep the project focused on a single building instance and avoid beginning with hardware integration.

These are based on summarized auto-generated transcripts, not verified verbatim lecturer clarifications. They cannot replace the official task order.

## Unapproved technical proposals

- P-01: Historical repository-name proposal resolved by D-08: `SmartElevator-Ex3`, public under `itavs`. This is an owner decision, not an official visibility requirement.
- P-02: Historical JSON proposal superseded by official requirement S-04; no schema has been selected.
- P-03: Use seeded request generation for repeatable evaluation.
- P-04: Provide CLI support for diagnosis/evaluation alongside the required GUI; no interface stack or implementation sequence is selected.
- P-05: Use a simple baseline first and optionally compare additional policies; a second policy is not an explicit ToDo requirement.
- P-06: Revisit the pre-existing module sketch during Task 3 and class contracts during Task 4. No architecture is approved by this documentation update.

## Open decisions and questions

- Q-01: Source was supplied and reviewed privately. `references/I2SE_Exe3.docx.pdf` is a portable lookup convention, not its current location. PDF publication is excluded; local lecture notes remain ignored.
- Q-02: Select implementation language, libraries, toolchain and board details at the appropriate approved tasks.
- Q-03: Task 1 local repository on `main` is constructed. The initial commit and public GitHub publication are authorized by D-08; final synchronization is verified in the handoff. Further repository actions require their own authorization.
- Q-04: Obtain deadline, grading, submission and demo expectations; the PDF does not provide them.
- Q-05: Define the problem and objective details in Task 2 after approval; later choose model fidelity and numerical values.
- Q-06: Obtain or clarify the class-agreed JSON required by Task 6.
- Q-07: Clarify Task 10 output schema and Task 11 wireless protocol/state exchange; choose BLE or WiFi without treating both as mandatory.

## Execution status

Task 1 is complete as independent repository construction on `main`; the approved initial commit and public publication are being finalized. Final verification belongs in the execution handoff. Tasks 2-12 are pending and unapproved. No application implementation, formal problem definition, approved HLD/LLD or testing strategy has been produced.
