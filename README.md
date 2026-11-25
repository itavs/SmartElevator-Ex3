# SmartElevator-Ex3

Assignment 3 - Introduction to Software Engineering (OOP/OOD)

## Goal and official deliverables

Design an end-to-end online destination-based smart-elevator allocation system for a building with a set of elevators. The official objective is to minimize overall waiting time, explicitly defined as the time from calling an elevator to reaching the destination.

The official deliverables cover a repository, problem definition, HLD, LLD, allocation-method design, class-agreed simulation parameters in JSON, time-based requests and a JSON-driven auto-generator, a complete simulation with an allocation GUI, a testing strategy, allocation/stop output records, an ESP allocation implementation communicating with the PC simulator via BLE or WiFi, and a short results summary. ESP32 is named in the HLD instruction.

## Status and approval boundary

The official two-page `I2SE_Exe3.docx.pdf` was supplied and reviewed on 2026-11-25. The source is kept privately outside this published project. `references/I2SE_Exe3.docx.pdf` is a portable local lookup convention only; no PDF has been copied there or tracked.

Task 1 is complete as repository construction: an independent local Git repository on `main` has been verified. The owner has approved publication cleanup, one initial commit and a public GitHub repository named `itavs/SmartElevator-Ex3`; final commit/push verification is reported in the Task 1 handoff. There is no application implementation, algorithm, test suite or GUI. Tasks 2-12 remain pending and require separate approval.

## Sources and evidence labels

1. **Official requirement:** the assignment PDF, page 1 context/objective and page 2 numbered ToDo.
2. **Verified lecturer clarification:** record its date and source; surface any conflict with the handout for review.
3. **Lecturer recommendation / transcript interpretation:** lecture summaries based on auto-generated transcripts; not verbatim verified instructions.
4. **Project decision / proposal:** owner-approved workflow choices or explicitly unapproved technical proposals.
5. **Open question:** a detail not resolved by the available sources.

Do not treat a recommendation, proposal or unspecified default as an official requirement.

## Project documents

- `AGENTS.md` - scope, authority, permissions and work-order instructions.
- `docs/ROADMAP.md` - original English summaries of official Tasks 1-12 in their exact order, planning deliverables, proposed completion gates and mapping from the old roadmap.
- `docs/REQUIREMENTS_DRAFT.md` - source-indexed requirement inventory and open questions; not a completed Task 2 specification.
- `docs/LECTURE_NOTES.md` - optional local-only lecture summaries, retained on the owner's machine and excluded from Git; unavailable in a public clone.
- `docs/ARCHITECTURE_PLAN.md` - pre-existing, unapproved architecture sketch; not completed HLD or LLD.
- `docs/DECISIONS.md` - approved workflow choices, official constraints, technical proposals and open decisions.
- `agent/FIRST_MESSAGE.md` - read-only onboarding for a new agent.
- `references/README.md` - source location and reference-handling guidance.

## Working conventions

- Documentation, code, comments, filenames and commit messages are English; communication with the owner is Hebrew.
- Keep this project independent of other assignments and preserve existing useful work.
- Follow official Tasks 1-12 in order. Obtain owner approval before starting each task.
- Use a top-down approach: problem definition, HLD, LLD and allocation design precede implementation.
- Git initialization, external repository creation, commits, pushes, dependency installation and hardware connection require explicit authorization for the action.
- Repository visibility is public by owner decision. Implementation language, framework and wireless transport remain undecided.

## Next task - approval required

Task 2 is to define the optimization problem. It has not started. Request owner approval before drafting its model, scope or acceptance examples. Do not infer that permission to create or publish the repository authorizes later assignment work.

## Public repository contents

The public repository contains nine documentation/configuration files. The ten-file local inventory also includes `docs/LECTURE_NOTES.md`, which remains ignored. The assignment PDF, raw transcripts, course reference files, personal filesystem paths and credentials are excluded. Public task descriptions are original paraphrases rather than copied handout text.
