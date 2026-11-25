# Decisions, Proposals and Open Questions

## Approved owner workflow decisions

- D-01: This is an independent Assignment 3 project, separate from all other projects.
- D-02: A dedicated agent uses this project's `AGENTS.md`.
- D-03: Code, comments, documents, filenames and commit messages are English; owner communication is Hebrew.
- D-04: Follow the official tasks in numerical order with approval before each task and major decisions.
- D-05: No external repository creation, commit, push or publication without explicit authorization.
- D-06 (2026-11-25): The owner approved updating existing planning documentation to match the official PDF. That approval covered documentation alignment; subsequent Task 1 permissions are recorded in D-08 and D-09.
- D-07: Preserve the existing project structure and useful documentation; keep the approach top-down.
- D-08 (2026-11-25): The owner approved local Git setup on `main`, then one initial commit and creation/publication of the public `itavs/SmartElevator-Ex3` repository. This historical authorization did not cover later tasks; Task 2 documentation was subsequently authorized in D-10.
- D-09 (2026-11-25): Reuse a consistent prior commit identity in local Git configuration only; remove personal absolute paths; preserve but ignore lecture notes; paraphrase the official task list and exclude private course sources from publication.

- D-10 (2026-11-25): The owner authorized Task 2 specification documentation and necessary consistency updates. No staging, commit, push, HLD, LLD, allocation-strategy design, implementation or dependencies are authorized. This historical approval did not approve model assumptions; A-01 through A-05 were subsequently approved in D-11.

- D-11 (2026-11-25): The owner approved A-01 through A-05 as initial project conventions and authorized minimal documentation consistency updates and closure validation. A-06, physical parameters, latency and exceptional failure/recovery behavior remain open. At that stage Task 2 still required final approval and staging was not authorized; the subsequent closure/staging authorization is recorded in D-12.

- D-12 (2026-11-25): The owner authorized final Task 2 closure subject to verification, recording Task 2 as completed and staging exactly its seven documentation files. Approved A-01 through A-05 and all remaining open questions are preserved. Commit, push and Task 3 remain unauthorized. Final validation and staged-diff results are reported in the closure handoff.

## Approved initial modeling conventions

Approval source: explicit owner instruction on 2026-11-25. These are project decisions, not official PDF requirements. The same table appears in `OPTIMIZATION_PROBLEM.md`.

| ID | Status | Convention and limits |
|---|---|---|
| A-01 | Approved project decision | Each ordinary request represents one passenger with different source and destination floors. The passenger stays in the same elevator; intermediate stops are allowed. Same-floor and invalid requests require explicit handling rules and must not be silently discarded. |
| A-02 | Approved project decision | Each ordinary serviceable request receives one elevator assignment, fixed during normal operation. Exceptional failure/recovery behavior remains unresolved. Zero communication, release or decision latency is not approved by A-02. |
| A-03 | Approved project decision | Use an unweighted sum over a fixed, policy-independent evaluation cohort. Continue service after the last request arrival. Report incomplete requests explicitly; never omit them to improve the score. |
| A-04 | Approved project decision | Measured completion occurs at the destination when doors are sufficiently open for alighting. Release physical capacity only when the passenger finishes exiting. Boarding-start details and physical durations remain open. |
| A-05 | Approved project decision | Expose identical-timestamp requests in stable input order. Earlier processed requests may be visible to later decisions; unreleased requests remain hidden. Exposure order does not determine service order. |
| A-06 | Open proposal, not approved | Capacity, movement, availability, service ranges, boarding details, physical parameters, units, telemetry and fidelity remain for later approved work. |

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
- Q-03: Task 1 local repository on `main` is constructed. Public publication is complete at `https://github.com/itavs/SmartElevator-Ex3`; local/remote `main` were verified at initial commit `786d9b5c2f4c06e476a81fd6f11b6ff93a2fed98`. Further repository actions require their own authorization.
- Q-04: Obtain deadline, grading, submission and demo expectations; the PDF does not provide them.
- Q-05: A-01 through A-05 are approved in `OPTIMIZATION_PROBLEM.md`. A-06, physical values, latency, same-floor/invalid handling, cancellation and exceptional failure/recovery remain open. No numerical physical model or allocation method is chosen.
- Q-06: Obtain or clarify the class-agreed JSON required by Task 6.
- Q-07: Clarify Task 10 output schema and Task 11 wireless protocol/state exchange; choose BLE or WiFi without treating both as mandatory.

## Execution status

Task 1 is complete including public publication and synchronization verification. Task 2 is completed within its documented problem-definition scope and remains uncommitted. Staging of its seven documentation files is authorized for final review; committing and pushing require separate approval. A-01 through A-05 are approved project conventions; A-06, latency and scoped exceptions remain open. Tasks 3-12 are pending and unapproved. No application implementation, approved HLD/LLD, allocation method or testing strategy has been produced.
