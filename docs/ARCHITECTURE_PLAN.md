# Architecture Sketch — Proposal Only

No architecture has been approved or implemented. This is a pre-existing proposal preserved during documentation alignment, not execution of Task 3 or Task 4. Revisit it only after those tasks are approved.

## Official constraints for the later design review

- Task 3 requires HLD covering both simulation and ESP32 deployment; Task 4 separately requires classes, public methods and parameters.
- Task 6 requires class-agreed JSON simulation parameters; Task 7 requires a time-based request list and JSON-driven auto-generator.
- Task 8 requires an allocation GUI. Its design is open, but the GUI itself is not optional.
- Task 10 requires allocation output plus a record for each stop with elevator ID.
- Task 11 requires actual allocation execution on an ESP microcontroller communicating with the PC simulator by BLE or WiFi. Task 3 names ESP32.
- The official objective is call-to-destination time. Numeric parameters, component contracts, protocol, transport choice and toolchain remain open.

The module list below is a proposal, not an official module list or an approved implementation decision. It does not prescribe the execution order; follow `docs/ROADMAP.md`.

## Proposed modules

1. **Domain model:** Building, ElevatorConfiguration, ElevatorState, PassengerRequest, AllocationDecision.
2. **Configuration:** Validated building/elevator and timing parameters (JSON required by Task 6; schema and values open).
3. **Scenario generator:** Seeded request streams with configurable demand patterns.
4. **Simulation engine:** Virtual clock, elevator travel/door states, passengers, events and metrics.
5. **Allocator interface:** Receives current state plus a request; returns an eligible elevator assignment.
6. **Strategies:** Simple baseline first, alternatives later.
7. **Evaluation:** Same fixed scenarios per strategy, aggregate performance and reliability metrics.
8. **Presentation:** Required allocation GUI; optional CLI support and proposed 2D live/accelerated visualization. Visual design remains open.

## Core constraint

Lecturer recommendation and project direction: isolate the allocation strategy from simulator/graphics internals through an explicit interface. Review this boundary during Task 3 to support the required ESP deployment. No interface has been designed or approved. The wireless adapter, message schema and state exchange still need design at the appropriate approved task.

## Design questions

- Are floors contiguous or an explicit set (e.g., -2, -1, 0, 1...)?
- Is allocation immutable once made? What happens to broken elevators?
- What elevator scheduling and boarding semantics best reflect the task?
- Which metrics should supplement aggregate request-to-arrival time (e.g., max latency or fairness)?
- Which GUI design, language and framework should be chosen? The GUI is required; its design is open, and the language/framework are unspecified.
- Which ESP32 board/toolchain and BLE or WiFi protocol will support the required PC-to-ESP integration?
- How will Task 10 allocation and stop records be represented?
