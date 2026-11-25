# Task 2 - Elevator Allocation Optimization Problem

## 1. Status, scope and evidence

**Status:** Task 2 completed within the documented initial problem-definition scope, following owner-authorized closure and final documentation verification. A-01 through A-05 are approved initial project conventions. A-06, physical parameters, latency and exceptional behavior remain open. Closure does not authorize Task 3. The seven Task 2 documents may be staged for review; commit and push require separate approval. This document does not define HLD, LLD, an allocation strategy, application code or a testing strategy.

**Primary source:** the privately supplied `I2SE_Exe3.docx.pdf`, re-read on 2026-11-25. References below identify its pages and numbered tasks. This specification uses original wording and does not reproduce private lecture notes. See `../references/README.md` for source handling.

Evidence labels:

- **Official:** directly supported by the PDF.
- **Interpretation:** a mathematical expression or consequence of the objective, not additional handout wording.
- **Lecture-derived:** secondary guidance from summarized automatic transcripts, not independently verified clarification.
- **Approved project convention:** an explicit owner decision for the initial model, separate from official PDF requirements (A-01 through A-05, approved 2026-11-25).
- **Proposed:** a remaining modeling assumption awaiting approval or clarification; A-06 remains proposed.
- **Open:** an unspecified detail to resolve before the relevant later work.

| Source | Confirmed basis |
|---|---|
| Page 1, problem statement | Given a building and elevator fleet, allocate online and improve aggregate time from a call until the passenger reaches the destination. |
| Page 1, destination-dispatch context | The passenger's destination is known when requesting service. |
| Page 2, Task 2 | Define the allocation optimization problem for a destination-floor request. |
| Page 2, Task 7 | Request fields are time, src and target. This informs the input definition; no generator is designed here. |
| Page 2, Task 8 | The later simulation evaluates the allocation method against total waiting time. |
| Page 2, Task 10 | Later output includes allocation information and elevator-identified stop records. No serialization is selected here. |

The GUI, JSON, ESP32 and BLE/WiFi requirements remain unchanged in the roadmap. No language, class structure, wireless protocol, optimization technique or numerical simulator default is selected here.

## 2. Formal problem statement and notation

**Interpretation:** Allocate every arriving valid serviceable request to an elevator using only information available at that decision. Subject to agreed physical and service constraints, seek to minimize the sum of passenger call-to-destination durations, including effects on passengers already waiting or riding.

**Core versus model choices:** the official core is destination-based online allocation and the call-to-destination objective. The notation below defines a family of evaluation problems parameterized by initial conditions and service semantics. Individual ordinary passengers, no transfers, assignments fixed during normal operation, the destination measurement event and stable equal-time exposure are now approved project conventions A-01 through A-05. They are not extra official PDF requirements. Results are comparable only under the same declared choices. The physical model, exceptional handling and latency remain open for later approved work; Task 2 completes the problem definition within those explicitly documented limits.

| Symbol | Meaning and evidence |
|---|---|
| $F$ | Building floor identifiers: notation for the official building context. |
| $E$ | Elevator identifiers: notation for the given fleet. |
| $\theta$ | Given building/fleet parameters: proposed abstraction, with values left open for Task 6. |
| $S_0$ | Initial system state: elevator positions, loads, operational state and existing service commitments where modeled. |
| $\sigma$ | Agreed service semantics: motion, stop execution, boarding/alighting, information release, event ordering and measurement conventions. Not a design of those rules. |
| $r_i=(t_i,s_i,d_i)$ | Request time, source and destination: official fields expressed in our notation. |
| $a_i$ | Elevator allocated to request occurrence $i$. |
| $\ell_i,\tau_i$ | Release to the allocator and allocation-decision times; notation, not added mandatory request fields. |
| $b_i$ | Boarding-start event when the passenger begins consuming onboard capacity under the proposed counting convention. |
| $c_i$ | Destination-completion time: official event concept; the doors-sufficiently-open measurement boundary is approved project convention A-04. |
| $u_i$ | Physical exit-completion event, when the passenger ceases consuming onboard capacity. Distinct from $c_i$. |
| $\mathcal R$ | Fixed finite indexed input list of all $n$ request occurrences; known to evaluation, not revealed in advance to the allocator. |
| $V$ | Fixed set of valid request indices established by policy-independent input rules. All valid occurrences remain included, even if service is impossible or unfinished. |

Index $i$ distinguishes occurrences, including identical request triples. It is notation, not a fourth mandatory request field. Floors need not start at zero or be contiguous; geometry and service ranges remain open.

The decision variable is elevator assignment. Completion times depend on assignments, the fixed input, initial state $S_0$, configuration $\theta$ and service semantics $\sigma$. Identical assignments alone need not yield identical times if those conditions differ. Existing passengers in $S_0$ must either be represented in the fixed evaluation cohort with their original request times or explicitly treated as fixed background load under the same rule for every policy. No policy may decide which existing passengers count.

Stop order and motion rules affect the outcome but are not designed here. If routing is later part of the allocation policy's control, that control must be stated explicitly; otherwise external service rules are held fixed. This document chooses neither design. Randomized policies or environments additionally require a declared random realization or reporting convention; no probability law is assumed here.

## 3. Request input and allocation output

### Request input

**Official (Task 7):**

| Field | Meaning | Unspecified details |
|---|---|---|
| `time` | Service-request creation time $t_i$. | Units, precision, clock origin and ordering. |
| `src` | Passenger's source floor $s_i$. | Valid identifiers, access and elevator service ranges. |
| `target` | Destination floor $d_i$, known at allocation. | Explicit same-floor/invalid-destination handling remains open; transfers are excluded for ordinary requests by approved A-01. |

Configuration and observed elevator state are decision context, not extra mandatory request fields. The official triple contains no passenger count, weight, priority or cancellation field.

**Approved project convention A-01:** each ordinary request represents one passenger with valid, different source and destination floors, $s_i,d_i\in F$ and $s_i\ne d_i$. This is the initial project domain, not an official PDF restriction. Same-floor and invalid requests require explicit handling rules and must not be silently discarded. Group requests are outside this initial ordinary-request model; any later extension requires review.

Here **direct trip means remaining in the same elevator from source to destination, without transfers**. Intermediate stops to serve other passengers remain allowed and their delay contributes to the duration. It does not mean express, nonstop or exclusive service.

### Allocation output

**Interpretation:** for a valid serviceable request, the allocation identifies an elevator and associates it with that request occurrence:

$$
a_i\in E.
$$

For example, occurrence 4 with `(time=12, src=0, target=6)` is allocated to elevator B. This is semantic notation, not an API or output-file schema.

Under **approved A-01 and A-02** for ordinary serviceable requests, assignment indicators can express the same decision:

$$
x_{ie}=\begin{cases}1,&a_i=e,\\0,&\text{otherwise},\end{cases}
\qquad \sum_{e\in E}x_{ie}=1.
$$

**Approved project convention A-02:** each ordinary serviceable request receives one elevator assignment, fixed during normal operation. Exactly-one allocation above applies to that case. Exceptional failure and recovery behavior, cancellation and deferral rules remain unresolved. A-02 neither imposes an immediate decision nor approves zero communication, release or decision latency. The PDF does not prescribe these project conventions.

If no elevator can serve the trip, no feasible assignment in $E$ may exist. Deferral, rejection, reporting and recovery must be clarified; do not invent an elevator ID or silently drop the request. Pickup/completion times and stops are service outcomes, not guarantees obtained simply by selecting an elevator.

### Event chronology and simultaneous requests

Creation $t_i$ is when the passenger makes the request and always starts the official duration. Release $\ell_i$ is when that occurrence becomes visible to the allocator. Decision $\tau_i$ is when an actual elevator assignment is made, not merely when a request is queued. Service events include boarding $b_i$, destination completion $c_i$ and physical exit $u_i$. For an ordinarily completed trip under the initial model and declared event semantics,

$$
t_i\le\ell_i\le\tau_i\le b_i\le c_i\le u_i.
$$

Any release, communication or decision delay is included in $c_i-t_i$; the clock does not restart at release or assignment. A deferred request has no actual $a_i$ or $\tau_i$ yet and remains in the evaluation set. Invalid inputs and same-floor special cases must not be forced into this ordinary-trip chronology without an agreed rule.

**Unapproved latency option, independent of A-02:** $\ell_i=\tau_i=t_i$, with equal-time decisions ordered logically. This is a possible simulation convention, not an official latency requirement. Nonzero latency is an alternative requiring agreement.

Equal creation timestamps do not determine release order, decision order or service order. Under approved A-05, identical-timestamp requests are exposed in stable input order; earlier processed occurrences may be visible to later decisions, while unreleased occurrences remain hidden. Batch exposure is not the selected initial convention and would require a separate change approval, even though an actually released batch can be causal. The exposure rule is fixed independently of the policy and does not impose first-come-first-served routing. Ordering simultaneous door, exit, boarding and motion events belongs to $\sigma$ and remains open.

## 4. Online information boundary

**Official:** allocation is online. **Interpretation:** a decision can use information released by its decision event and the current request, but cannot use unreleased requests or future outcomes.

Let $\mathcal I_i$ denote information released and observable by decision event $\tau_i$, including its logical position among equal-time events. Write a causal policy abstractly as

$$
a_i=\pi(\mathcal I_i).
$$

This is an information restriction, not an algorithm, class or interface design.

**Proposed observable context, to review later:**

- Current request, clock and known building/fleet configuration.
- Observed elevator positions, direction/motion, doors, load and operational state, where exposed by the model.
- Requests exposed under the agreed release convention, earlier allocations, passenger progress and established service commitments.
- Past observations available before the decision.

The PDF specifies no exact telemetry schema, update frequency or synchronization rules. These are candidate state concepts, not approved interfaces or an obligation to implement all physical sensors.

**Disallowed under the online interpretation:**

- Reading future rows in a prerecorded scenario or future generator output.
- Recovering the actual unreleased sequence from a request-generator seed/internal state.
- Treating a future failure or an actual future pickup/completion time as already observed.

The simulator may hold a complete evaluation scenario without exposing future demand to the allocator. Estimates based on known state differ from actual future outcomes. Forecasts learned only from past data may be causal, but support for them is open; no forecasting method or demand distribution is assumed.

Under approved project convention A-05, equal-time requests are exposed in stable input order. This is a project decision, not an official PDF requirement. A possible causal batch model is outside the selected initial convention. With fixed policy random choices, identical observable histories through a decision must produce the same allocation even when the unreleased suffixes differ. This non-anticipation condition concerns released information, not creation timestamps alone.

The PDF gives no numerical real-time response deadline. Causality does not imply zero computation/communication delay; the magnitude and modeled treatment of latency remain open. If a nonzero delay is represented on the simulation clock, it is included in call-to-destination duration; the clock is never reset at decision time.

## 5. Mathematical objective

### Individual duration

**Official:** waiting time extends from the call until destination arrival. **Interpretation:**

$$
w_i=c_i-t_i\ge0.
$$

Using pickup notation,

$$
w_i=(b_i-t_i)+(c_i-b_i).
$$

This includes the pre-pickup interval and the interval from pickup to destination completion, including intermediate stops and applicable door/boarding time. The event conventions must avoid gaps and double counting. Optimizing pickup delay alone would not express the specified objective.

### Fixed evaluation cohort and request status

**Approved A-03 and its evaluation formalization:** fix the entire indexed input $\mathcal R$ before comparing policies. Apply the same declared input-validity rules independently of policy decisions to establish $V$. In the ordinary valid-input case, $V=\{1,\ldots,n\}$. Invalid rows remain visible in the input-validation report; any evaluation on a filtered valid subset must disclose that preprocessing and use exactly the same subset for every policy. It is not a successful evaluation of all original rows.

| Status | Meaning | Evaluation treatment |
|---|---|---|
| Invalid input | A row violates agreed syntax/domain rules, such as an unknown floor. Same-floor handling is not yet agreed. | Report explicitly before comparison; do not call it a completed trip or let a policy classify a difficult valid request as invalid. |
| Infeasible service | A valid trip has no feasible service under the declared fleet/model conditions, such as no elevator covering both endpoints in a no-transfer model. | Keep it in $V$, report the reason and do not issue a complete finite total for that cohort. No actual elevator output exists unless feasibility changes. |
| Temporary unavailability | No immediate service is possible, but service may become feasible later, such as after unloading or a modeled recovery. | Keep the request in $V$; delay continues to count from $t_i$. It is not automatically permanently infeasible. |
| Unfinished request | A valid request lacks an observed completion by observation cutoff $T$. | Keep it in $V$, report status; unfinished alone does not prove infeasibility. It may reflect waiting, a finite cutoff or policy-caused starvation. |

These classifications can overlap in time: a temporarily unavailable request may be unfinished at $T$. They distinguish input validity, physical feasibility and observed progress, rather than imposing a single exclusive lifecycle enumeration. A feasibility claim requires a reason under fixed conditions; the policy's failure to serve is not that reason by itself.

Rejection, deferral, failure to assign, cancellation or silent omission does not remove a valid occurrence from $V$ under approved A-03. Cancellation semantics and any permitted cohort adjustment require a separate declared rule fixed across policies. No such adjustment is selected here. There is no policy-dependent acceptance filter in the objective.

### Evaluation cost versus policy selection

**Interpretation of page 1 and Task 8:** for an already defined causal policy $\pi$, fixed $(\mathcal R,S_0,\theta,\sigma)$, and finite completion of every $i\in V$, evaluate

$$
c_i^{\pi}=c_i(\pi;\mathcal R,S_0,\theta,\sigma),
\qquad
J_V(\pi;\mathcal R,S_0,\theta,\sigma)
=\sum_{i\in V}\bigl(c_i^{\pi}-t_i\bigr).
$$

The full input is an argument to the evaluator, not to each online decision. Values are realized outcomes under the policy and fixed service conditions; predictions are not substituted for measured completions. For randomized behavior, these expressions are conditional on the declared random realization; any statistical aggregation needs a separately agreed convention.

**Optimization aim:** choose/design an admissible causal allocation policy that reduces this total on the declared evaluation conditions, without granting its selection/tuning or live decisions knowledge of unreleased evaluation demand. One may compare realized costs of already defined policies after a scenario finishes, but must not present a winner selected using that scenario's future as an online decision or an unbiased held-out selection result.

There is deliberately no per-scenario $\min_{\pi}$ asserted as an online-achievable optimum. Minimizing over policies separately for each fully known scenario can produce an oracle hindsight benchmark, even when each chosen policy's runtime actions are causal. A policy-selection rule would need a declared criterion across scenarios or an explicitly agreed information/training protocol; the PDF supplies neither, and Task 2 does not invent one. The goal of reducing total duration remains official; universal online optimality is not claimed.

**Approved project convention A-03:** use an unweighted sum over a fixed, policy-independent evaluation cohort, with one passenger per ordinary request under A-01. With $m=|V|>0$ and a complete run, mean duration $\bar w=J_V/m$ ranks policies identically on that same cohort. Sum and mean need not rank different-size cohorts identically. If $V$ is empty, its mathematical sum is zero and its mean is undefined. An empty valid cohort resulting from invalid input does not convert invalid rows into successful completions.

No probability distribution, weights, competitive-ratio guarantee, fairness bound or optimality threshold is specified by the PDF. An expected-cost objective would need an agreed demand model and is not added as a requirement.

The goal covers all passengers: a new allocation can delay previous requests. Minimizing the new passenger's duration alone can therefore disagree with minimizing the aggregate. How to predict and improve these effects belongs to Task 5.

### Completion and unfinished requests

**Approved project convention A-04, measurement event:** $c_i$ is when the elevator is stopped at the destination and its doors are open enough for that passenger to alight. Merely passing the destination or stopping with doors closed does not satisfy A-04. Physical exit finishes at $u_i\ge c_i$; a passenger can have completed the measured trip but still consume capacity while exiting. Measurement through finished alighting is not the selected convention and would require an approved change. The doors-open boundary is an owner-approved interpretation, not a claim that the PDF specifies the exact event.

**Approved A-04 exit boundary; proposed boarding-start convention:** capacity is released only at physical exit completion $u_i$. Counting capacity from boarding start $b_i$, hence using $[b_i,u_i)$, remains a proposed physical-model detail under open A-06. The chronology and examples use that candidate start event explicitly; it is not promoted to an approved physical parameter by A-04. The count must not end at $c_i$ solely because the measurement clock has stopped. For example, doors open at 22 and exit finishes at 24: the metric can complete at 22 while the passenger still occupies capacity until 24. If timed boarding/alighting is modeled differently, resolve the open boarding/occupancy details explicitly rather than silently redefining $c_i$.

At cutoff $T$, let $C(T)\subseteq V$ contain only observed metric completions, and $U(T)=V\setminus C(T)$. If $U(T)\ne\varnothing$, the observed completed-only subtotal is not $J_V$. No complete finite score is reported until every cohort member has a finite observed completion. Report proven infeasible service separately from an incomplete observation or policy-caused non-completion. Do not label them all infeasible or silently assign zero duration.

**Approved A-03 continuation:** continue service after the last request arrival for the fixed cohort. A finite observation cutoff can be used for reporting, but does not imply a completed run. Metric completion does not authorize erasing remaining physical exit events or releasing capacity early. Permanent non-completion, infinite-duration treatment, cancellation, timeouts and numerical penalties remain open. No invented finite penalty is used to rank an incomplete run against a complete run.

The fixed cohort, continuation and explicit non-completion reporting are approved A-03. Detailed validity rules, failure handling, penalties and timeouts remain open; they are not official requirements invented here.

## 6. Relevant constraints and evidence

The physical details below remain proposed/open under A-06; ordinary-request lifecycle and scoring conventions are approved A-01 through A-05 where identified. These project decisions are distinct from official requirements or their mathematical interpretation. None selects an allocation strategy or numerical default.

| Constraint | Formal/model condition | Evidence and open details |
|---|---|---|
| Domain and eligibility | $s_i,d_i\in F$. If per-elevator service sets $F_e$ are modeled, the assigned elevator must serve the trip's endpoints under the agreed rules. | Building/fleet/request concepts are official; ranges remain proposed; the ordinary no-transfer restriction is approved A-01. |
| Capacity | For a passenger-count model, $0\le L_e(t)\le K_e$: onboard load never exceeds capacity. | Lecture-derived/proposed. Weight-sensor context does not specify capacity units or limits. No $K_e$ value is chosen. |
| Movement | Each elevator has one physical position at a time and respects agreed floor/travel constraints; boarding/alighting requires stopping at the relevant floor under agreed door rules. | Proposed physical feasibility. Floor heights, speeds, acceleration, reversal and door times are open. |
| Availability | Assignments and service respect observed operational status; a busy operational elevator may accept feasible future service. | Lecture-derived/proposed. Faults, maintenance and recovery rules are unspecified; busy is not synonymous with ineligible. |
| Service chronology | For an ordinarily completed trip, $t_i\le\ell_i\le\tau_i\le b_i\le c_i\le u_i$; boarding at $s_i$ precedes destination completion and physical exit at $d_i$. | Chronology interpretation with A-04 completion/exit boundary; boarding-start details, latency and invalid/same-floor handling remain open. |
| Request lifecycle | Under approved A-01/A-02 in normal operation, each valid serviceable request has one allocation, one pickup and one completion. | Approved ordinary lifecycle. Identical triples can be different passengers; exceptional recovery, cancellation and any group extension remain open. |
| Online decision | $a_i$ uses only $\mathcal I_i$, hiding future requests. | Online allocation is official; equal-time exposure is approved A-05; detailed telemetry remains open. |
| Complete evaluation | A complete finite score covers every fixed $i\in V$; no policy-dependent acceptance or serviceability filter removes requests. | Approved A-03 scoring boundary. Invalid input, infeasible service, temporary unavailability and unfinished requests remain separately reported; detailed responses are open. |

A full elevator is not automatically an invalid allocation: it may unload before pickup. Capacity applies at boarding and during the trip, not merely as a free-seat check at request creation. No reservation/prediction rule is chosen here.

Under approved A-01/A-04 and the still-proposed boarding-start count convention, $L_e(t)$ counts passengers on elevator $e$ whose physical occupancy interval $[b_i,u_i)$ contains $t$, including background passengers from $S_0$. Use actual physical exit, not the metric completion $c_i$, to release capacity. A modeled shared-time exit/boarding event must preserve $L_e(t)\le K_e$ under its declared ordering. Group sizes, weights and detailed transition semantics remain open.

## 7. Simple illustrative examples

All values below are invented for explanation. They are not simulator parameters, measured results, predictions, policy rules or optimality evidence. Seconds are illustrative units. The outcome tables stipulate feasibility and do not prescribe how outcomes are obtained. The approved initial conventions apply where relevant; physical numbers and zero-duration events remain example-only assumptions.

### A. Later pickup, earlier destination

Request: `(time=10, src=0, target=5)`.

| Hypothetical allocation | Pickup $b_i$ | Destination $c_i$ | Pickup delay | Duration $c_i-t_i$ |
|---|---:|---:|---:|---:|
| A | 14 | 45 | 4 | 35 |
| B | 18 | 38 | 8 | 28 |

B reduces this passenger's duration by 7 seconds despite a later pickup. This alone does not establish a smaller fleet-wide total; other passengers may be affected.

### B. Individual benefit versus total benefit

Assume one existing and one new passenger, with the following feasible outcomes and no other differences:

| Allocation of new request | Existing passenger's full duration | New passenger's full duration | $J_V$ |
|---|---:|---:|---:|
| A | 100 | 30 | 130 |
| B | 70 | 40 | 110 |

B reduces the aggregate by 20 seconds even though the new passenger takes 10 seconds longer. Each existing passenger's clock starts at the original request, not when the new request arrives.

### C. Eligibility before optimization

Request: `(time=20, src=2, target=8)`. Under a toy service-range model and approved no-transfer convention A-01, A serves floors 0-5 and B serves 0-10. A cannot serve this trip. B is eligible if its other constraints permit service. Busy B may still serve later; if B is out of service and no other elevator can serve, the handling rule is unresolved rather than a successful allocation.

### D. Future demand is hidden

At time 0, `(0, 0, 5)` is released. A stored scenario also contains `(30, 8, 0)`. The first decision cannot read the second row. Replacing that future row must not change the first decision's available information. For a randomized policy, hold its own random state fixed when checking this information restriction; do not expose a generator seed that reveals demand.

### E. Manual revalidation of the 11 review scenarios

The following checks use stipulated event traces and conditional toy models, not an implemented algorithm. They validate the definitions, not optimality or an approved physical configuration. Travel rates and zero-duration door/exit events below apply only to the explicitly stated examples. For these toy traces only, release and decision use a stipulated zero-delay abstraction unless stated otherwise. This is not an approved project latency convention and is not inferred from A-02.

| # | Scenario and fixed conditions | Manual result and interpretation |
|---|---|---|
| 1 | One ordinary trip: $t=10,b=14,c=24$, physical exit $u\ge24$. | $w=24-10=14=(14-10)+(24-14)=4+10$. Valid chronology; capacity lasts until $u$, not automatically 24. |
| 2 | Same fixed request and background conditions; A: $b=14,c=45$, B: $b=18,c=38$, $t=10$. | Durations 35 and 28, so B improves this passenger by 7 despite a later pickup. Other passengers are needed for an aggregate conclusion. |
| 3 | Same elevator throughout: request at 0, boarding at 2, travel 4 seconds, intermediate stop 3 seconds, then travel 4 seconds to metric completion. | $c=2+4+3+4=13$, $w=13$. A direct/no-transfer trip allows the intermediate stop and counts its delay. |
| 4 | Fixed two-passenger cohort, including the existing passenger's original clock. A durations: 100 and 30; B: 70 and 40. | $J_V(A)=130$, $J_V(B)=110$. B lowers the sum by 20 while increasing the new passenger's duration by 10. |
| 5 | Two requests at time 0, both from floor 0 to floors 1 and 3. One elevator initially at 0, capacity 1, one second/floor, zero boarding/door/exit durations. | Short trip first: completions 1 and 5, total 6. Long trip first: completions 3 and 7, total 10. Both are feasible service orders; neither follows automatically from input/decision order. A-05 selects stable sequential exposure; it still does not choose either service order. |
| 6 | Two distinct occurrences of `(0,0,1)`; one elevator at 0, capacity 1, one second/floor, zero door/boarding/exit times. | Completions 1 and 3 yield total 4. Deduplicating the occurrences would incorrectly yield 1 and change the fixed cohort. |
| 7 | Request at 0; elevator is initially full. Previous passenger physically exits by 5; new passenger boards at 6 and completes at 12. | $w=12$. Initial full load does not imply permanent infeasibility. Capacity is feasible if the previous occupancy ends before new boarding. |
| 8 | Request at 10; elevator stops at destination at 20, doors allow alighting at 22, physical exit finishes at 24. | Under approved A-04, $c=22,u=24,w=12$. Scores 10 (stop-based) or 14 (exit-based) describe alternative conventions, not this one. Capacity remains occupied until 24. |
| 9 | Valid target 8, but no elevator can serve above floor 5 under the no-transfer model. | Request stays in $V$, but there is no feasible assignment or complete finite $J_V$. Separately, an unknown floor outside $F$ is invalid input, not the same physical-feasibility case. |
| 10 | Empty input, then separately a same-floor occurrence `(5,2,2)`. | Empty valid cohort: sum 0, mean undefined. Same-floor handling remains conditional: a no-op convention, if later approved, could give $c=t=5,w=0$; declaring it invalid requires explicit validation/reporting. It is never silently counted as success. |
| 11 | Two scenarios have identical released histories through the first decision and different unreleased time-30 rows. Fix $S_0,\theta,\sigma$, the same preselected policy and its random choices. | The first allocation must match. Different future suffixes cannot affect that decision; this is a causal consistency check, not a claim that a particular elevator choice is optimal. |

Two additional boundary checks follow from the same definitions. With creation 10, release 12, decision 13, boarding 14, completion 24 and exit 25, the duration remains 14, not 12 or 11. If a fixed two-request cohort has only one observed completion by $T$, then $|U(T)|=1$: the completed subtotal is not a complete cohort score even if the policy rejected or omitted the other request.

## 8. Approved initial conventions and open modeling questions

**Approval source:** explicit owner instruction on 2026-11-25. A-01 through A-05 are initial project decisions, not official PDF requirements. Task 2 closure does not approve A-06 or authorize later tasks. The same convention table is recorded in `DECISIONS.md`.

| ID | Status | Convention and limits |
|---|---|---|
| A-01 | Approved project decision | Each ordinary request represents one passenger with different source and destination floors. The passenger stays in the same elevator; intermediate stops are allowed. Same-floor and invalid requests require explicit handling rules and must not be silently discarded. |
| A-02 | Approved project decision | Each ordinary serviceable request receives one elevator assignment, fixed during normal operation. Exceptional failure/recovery behavior remains unresolved. Zero communication, release or decision latency is not approved by A-02. |
| A-03 | Approved project decision | Use an unweighted sum over a fixed, policy-independent evaluation cohort. Continue service after the last request arrival. Report incomplete requests explicitly; never omit them to improve the score. |
| A-04 | Approved project decision | Measured completion occurs at the destination when doors are sufficiently open for alighting. Release physical capacity only when the passenger finishes exiting. Boarding-start details and physical durations remain open. |
| A-05 | Approved project decision | Expose identical-timestamp requests in stable input order. Earlier processed requests may be visible to later decisions; unreleased requests remain hidden. Exposure order does not determine service order. |
| A-06 | Open proposal, not approved | Capacity, movement, availability, service ranges, boarding details, physical parameters, units, telemetry and fidelity remain for later approved work. |

The core objective and information restriction remain official requirements or their mathematical interpretation. A-01 through A-05 select initial project semantics within that core. Physical details under A-06, latency, and exceptional behavior remain unresolved. Zero-delay toy traces are examples only. No route insertion, service-order algorithm, numerical defaults or class/interface design is approved.

## 9. Open questions and resolution points

| ID | Question | Needed before |
|---|---|---|
| Q-01 | Ordinary requests are one-passenger, same-elevator trips with fixed normal-operation assignments under A-01/A-02. What explicit same-floor, invalid-input, priority, cancellation and exceptional recovery rules are needed? | These exceptions remain scoped as unresolved; detailed handling requires later approved work. Group/transfer extensions are outside the initial model. |
| Q-02 | Which detailed validity rules establish $V$, and what responses are required for invalid, infeasible or temporarily unavailable requests? | A-03 fixes cohort independence and explicit non-completion reporting. Detailed validation, response and recovery behavior remain unresolved; no silent success or removal is allowed. |
| Q-03 | Which telemetry and service commitments are observable, and how fresh/consistent are they? | Task 3 boundaries and Task 4 contracts; no schema chosen here. |
| Q-04 | A-05 fixes stable equal-time exposure. What release/communication/decision latency, clock units/origin and physical equal-time ordering should be modeled? | Latency remains explicitly unapproved and separate from A-02; detailed values and physical ordering can wait for later approved tasks. |
| Q-05 | A-03/A-04 settle the total-duration metric and separate completion/exit boundaries. What boarding-start, door-opening and exit-duration parameters implement them? | Physical parameters remain open under A-06; the approved measurement boundary is not reopened by their absence. |
| Q-06 | What capacity, floor/range, movement, acceleration, door and boarding parameters apply? | Task 6 class agreement and Task 8 implementation. |
| Q-07 | Are faults/maintenance required, and how do pending passengers recover? | Relevant design review and implementation. |
| Q-08 | Is the class-agreed simulation JSON available? | Task 6; no schema invented in Task 2. |
| Q-09 | Beyond A-03 explicit non-completion reporting and the complete-score domain in Section 5, are numerical penalties, fairness bounds or timeouts required? | Penalty models and thresholds remain open for clarification; none is invented, and no incomplete run is reported as a successful complete finite score. |
| Q-10 | Are causal statistical forecasts allowed or expected? | Task 5, if a forecasting method is later proposed. |
| Q-11 | Which output schema and PC/ESP state exchanges are expected? | Tasks 10-11, with deployment considered in Task 3. |
| Q-12 | What deadline, grading, submission and demo rules apply? | Planning/final handoff; absent from the supplied PDF. |
| Q-13 | Which $S_0$, background-passenger cohort convention and $\sigma$ will define a comparison, and who controls routing? | Task 2 makes these dependencies explicit; later approved design resolves control boundaries and detailed values. |
| Q-14 | Which cross-scenario selection/tuning and randomized reporting protocol, if any, will be used? | Later allocation/evaluation work; not required to define cost for an already fixed policy. No online optimum or probability law is assumed. |

## 10. Completion scope and verification limits

The completed Task 2 problem definition provides input/output semantics, the online boundary, mathematical goal, source labels, constraints, examples and open questions. A-01 through A-05 are now explicitly approved project decisions. A-06, latency and scoped exceptions remain open; later stages must not treat them as approved rules or attribute project decisions to the PDF.

This is a problem specification. It contains no policy selection, prediction method, routing design, pseudocode, class/interface design or optimization solver. Tasks 3-5 remain unstarted.

All seven correction findings are addressed: evaluation versus policy selection (Section 5), fixed cohort/status distinctions (Section 5), initial state/service dependencies (Section 2), direct trips with stops (Section 3), metric versus physical capacity events (Sections 5-6), creation/release/decision/service and simultaneous events (Sections 3-4), and core versus unapproved assumptions (Sections 2 and 8-9). The 11 review scenarios are revalidated manually in Section 7.

Task 2 is completed for its documented scope under the owner's closure authorization. A-01 through A-05 remain approved project conventions; A-06, latency and exceptional behavior remain open. Final documentation, conceptual-scenario and staging verification results are reported in the closure handoff. No simulator or allocation method exists to execute; these checks are not software-test results or the formal Task 9 testing strategy. Only the seven Task 2 documentation files may be staged. No commit, push or Task 3 work is authorized.
