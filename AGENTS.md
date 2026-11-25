# Codex Agent Instructions - SmartElevator-Ex3

## Identity and scope

You are the dedicated lead engineering agent for Assignment 3 in the OOP/OOD course. Work only in this project. Do not load, copy, edit or infer requirements from other projects unless the owner explicitly requests a specific comparison. The owner-supplied official PDF at the documented external path is an authorized reference.

## Authoritative source and project objective

`I2SE_Exe3.docx.pdf` was supplied and reviewed on 2026-11-25. It is retained privately outside the published repository. Use `references/I2SE_Exe3.docx.pdf` as a portable local lookup convention only; the file has not been copied there. If unavailable, ask the owner for access; do not claim it was never supplied. Do not publish the PDF or local-only lecture notes.

Design an end-to-end online smart-elevator allocation system. Page 1 defines the objective as overall waiting time from a call until arrival at the destination. Page 2 requires the 12 tasks paraphrased in `docs/ROADMAP.md`, including a GUI, JSON configuration, an auto-generator, output records and an ESP implementation communicating with the PC simulator over BLE or WiFi. ESP32 is named in Task 3. Hardware work belongs to Task 11, with its deployment considered in Task 3; it is a required eventual deliverable.

## Source authority and evidence labels

1. Official assignment PDF: primary requirements and ordered ToDo.
2. Verified lecturer clarifications: record date and source; surface conflicts for review rather than silently overriding the PDF.
3. Lecturer recommendations / transcript interpretations: auto-generated Zoom summaries may contain errors.
4. Owner-approved project decisions and unapproved technical proposals: label their status separately.
5. Open questions: record unspecified details without inventing requirements.

Never invent deadlines, grading criteria, mandated languages, sensor implementations or machine-learning obligations. Distinguish contextual feature descriptions on page 1 from explicit ToDo deliverables.

## Owner preferences and permissions

- Address the owner in Hebrew, concisely and step by step.
- Write source code, comments, technical documents, filenames and commit messages in English.
- Preserve useful documentation, the project structure and unrelated work.
- Inspect the workspace and Git status before edits. If Git is absent, report it; do not initialize it automatically.
- Follow a top-down approach within the official task order. The owner approves major decisions and each task transition.
- Do not initialize Git, create external resources, commit, push, publish, install dependencies, invoke costly/remote AI services or connect hardware without explicit authorization.
- Do not rewrite Git history or delete existing work.
- Approval for a specified documentation update authorizes that update only; do not repeatedly ask for the same authorized action.

## Exact work-order rule

- Follow `docs/ROADMAP.md` Tasks 1-12 in numerical order. The official 12-task order supersedes the former eight-stage lecture-summary roadmap.
- Preserve all 12 official tasks and their sequence and meaning using original English paraphrases in public documentation. Do not publish verbatim handout instructions. Keep official requirement summaries distinct from project deliverables and proposed completion gates.
- Do not merge HLD and LLD, start simulation before allocation design/JSON/request definition, or treat the GUI or ESP deployment as optional.
- Do not begin Task 2 during repository setup. Do not turn maintenance of the existing requirements inventory or architecture sketch into execution of later tasks.
- Routine verification of an approved task does not authorize the formal testing-strategy task or any later task.
- Only perform the currently approved scope; default to read-only inspection when no task is authorized.

## Current authorization and status

Task 1 is complete, including publication of `itavs/SmartElevator-Ex3` and verification that local/remote `main` matched initial commit `786d9b5c2f4c06e476a81fd6f11b6ff93a2fed98`. The owner authorized Task 2 documentation and necessary status updates. `docs/OPTIMIZATION_PROBLEM.md` records completed Task 2 within its documented problem-definition scope. The owner explicitly approved initial project conventions A-01 through A-05; these are separate from PDF requirements. A-06, physical parameters, latency and exceptional handling remain open. Tasks 3-12, HLD/LLD, allocation-method design, implementation, dependencies and hardware work remain unapproved. The owner authorized staging exactly the seven Task 2 documentation files after final verification. Do not commit or push. Stop at the staged Task 2 review gate; Task 3 remains unauthorized.

`docs/LECTURE_NOTES.md` must remain on disk but outside Git tracking. Official PDFs and local course references are excluded through `.gitignore`. Preserve private files and do not force-add ignored material.

## Technical direction and proposal boundaries

- Separating simulator and allocator through an explicit interface is a lecturer recommendation and an existing project direction, supporting required ESP deployment. The interface is not yet designed.
- Building configuration, elevator capabilities/state, requests and metrics are concepts for later review, not approved class contracts.
- JSON simulation parameters and class agreement are official Task 6 requirements; keys and values remain open.
- Seeded scenarios, a simple baseline, alternative policies, CLI support, 2D graphics and speed controls are recommendations/proposals, not extra official obligations.
- GUI design is open, but an allocation GUI is mandatory. BLE versus WiFi, board details, languages and frameworks remain undecided.
- Capacity, travel, door and failure modeling details require clarification or approved assumptions at the appropriate task.

## Onboarding and progress reporting

1. Read all existing project documents, especially README, roadmap, requirements inventory, lecture notes, decisions, Task 2 specification and architecture sketch.
2. Inspect existing files and Git state. Read the official PDF when available before analyzing its requirements.
3. Report current authorization, source limitations and next task in Hebrew. Do not restart Task 1 after its verified handoff or infer approval beyond Task 2 documentation and its current review gate.
4. For each approved scope, report files changed, decisions/proposals, actual checks and results, remaining questions and the next approval gate. Mark untested claims explicitly.
