# PROGRAM_EXECUTION_PLAN

> **Operational bridge:** Vision → Principles → Roadmap → **Execution.**
> Non-constitutional and revisable. This document optimizes for **capability growth**, not
> implementation throughput. The primary planning unit is the **workstream**; the
> implementation batch is the smallest unit.
>
> **Authority order:** the Constitution wins. Where this plan and any constitutional
> document disagree, [PLATFORM_PRINCIPLES](PLATFORM_PRINCIPLES.md) and the ratified
> [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md) govern. This plan never amends them; it schedules
> against them.

---

## 1. Program Overview

**Purpose.** Translate the ratified constitution into an executable, dependency-aware
program that grows platform capability from the released **0.2.0** baseline to the
**1.0 Constitutional Baseline**, with the immediate objective of reaching **0.3.0**.

**Scope.** All three platform repositories (`engineering_kb`, `ecf`, `context_switcher`)
and the platform governance home (`C:\Dev\platform`). Planning only — no code, tests, repo
changes, commits, pushes, or releases.

**Relationship to the Constitution.**
- Every milestone's **exit criteria are constitutional obligations** (see
  [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md)), not feature lists.
- Every batch must trace to a principle and an obligation (see §10 Program Rules).
- 1.0 is defined constitutionally: *every obligation ≥ Partial, no contradiction blocking
  Strong.*

---

## 2. Current Platform State

| Dimension | State |
|---|---|
| Current release | **0.2.0** (coordinated private Git release; non-recursive manifest, exact upstream pins) |
| Current milestone | **0.3.0-dev** — *not* "at 0.3" until the substrate executes and the milestone contract is met (O2/P2) |
| Current maturity | Obligations O2, O5, O8, O9 **Strong**; O1 **Partial**; O3, O4, O6, O7, O10, O11, O12 **Emerging** |
| Architectural strengths | Layered ECF (principles→standards→workflows→roles→runtime); complete runtime schemas (intent, phase, run manifest, run state, task provenance, execution trace); provenance-first design; independent validation via review packs; coordinated reproducible releases |
| Runtime tooling present | `task_runner` (single-task execution + Claude executor + output contracts), `workflow_planner`, `workflow_validator`, `run_initializer`, `runtime_state/transaction`, `artifact_fingerprint` |
| Key gap to 0.3 | **No orchestration engine** drives the full 18-task DAG of `WF-REASON-0001`; it is specification-complete but not automatically executable |
| Constitutional open questions | **OQ-001** judgment integrity (0.7 target); **OQ-GOV-001/002/003** genesis authority, anti-capture, change-class ladder (Workshop 4 — founder rulings); ~~OQ-ARCH-001~~ **resolved** (accountability is a governance concern, not a Plane — PLATFORM_ARCHITECTURE FD-3); **roadmap-view divergence** (§3 note) |

---

## 3. Platform Milestones

> **Reconciliation note (founder ruling requested).** The ratified roadmap sequences
> milestones by **constitutional obligation**; the execution labels below (Workflow Proven,
> Review Plane, …) come from the program batches and sequence by **plane delivery**. These
> two sequencings **materially diverge from 0.4 onward.** Per "Constitution wins," the
> **exit criteria below are the ratified obligations**; the plane label is an execution
> overlay. Making the plane-delivery sequence *authoritative* would be a change to the
> ratified roadmap (a T4/T5 governance act) — flagged in §Known Risks and
> §Recommended Governance Improvements. 0.3 is identical in both framings.

| Ver | Execution label | Ratified obligation focus | Goal | Exit criteria (constitutional) |
|---|---|---|---|---|
| **0.3** | Workflow Proven | Controlled Reasoning Workflow substrate | `WF-REASON-0001` executes end-to-end, halting at human approval, with auditable provenance | 18-task DAG runs via an orchestration engine; every task emits admissible provenance; a real Work Request produces a validated Recommendation Report + run record; independent review passes |
| **0.4** | *(Review Plane)* | **O10** authoritative-model contract · **O6** responsibility-and-authority model | Put the two foundational contracts in place that later capabilities reference | O10 and O6 each reach **Partial** (versioned-stable model contract; five-role responsibility model) |
| **0.5** | *(Artifact synchronization)* | **O3** canonicalization · **O4** stewardship | Knowledge becomes canonical by evidence; accountability becomes durable | O3 and O4 each reach **Partial** |
| **0.6** | *(Operational Evidence)* | **O7** corrigibility · **O11** assumption lifecycle | Safe supersession; open the first-class assumption lifecycle | O7 and O11 each reach **Partial** |
| **0.7** | *(Knowledge Expansion)* | **O12** lifetime reasoning integrity | Move the weakest obligation from unaddressed to demonstrated | O12 reaches **Partial**; OQ-001 has a demonstrated partial mechanism |
| **0.8** | *(Multiple Consumers)* | Deepen **O8, O5, O1** across planes | Cross-plane integrity; additional consumers exercise the substrate | Deepened obligations hold *across* plane boundaries |
| **0.9** | Release Automation | Constitutional Readiness | Verify, with evidence, every obligation meets the 1.0 threshold | Independent evidence-backed audit; release automation; no blocking contradiction |
| **1.0** | AI Engineering Platform | Constitutional Baseline | The constitutional definition of 1.0 is met | Every obligation ≥ Partial, no contradiction blocking Strong |

*(The plane labels 0.4–0.8 in parentheses are the batch's proposed overlay; their exit
criteria are shown as the ratified obligations they must satisfy. See
[PLATFORM_CAPABILITY_MAP](PLATFORM_CAPABILITY_MAP.md) for the plane-delivery lens.)*

---

## 4. Workstreams

**Partition change (explained before changing, per instruction).** The earlier
[PLATFORM_WORKSTREAMS](PLATFORM_WORKSTREAMS.md) used WS-1…WS-8 + cross-cutting WS-C1/C2,
scoped to the whole road to 1.0. This plan adopts the **richer WS-0…WS-10 partition** below
because it (a) adds a permanent **program-management** workstream (WS-0), (b) separates
**workflow runtime** (the orchestration engine) from **reasoning content** (the tasks),
which is the actual parallelization seam for 0.3, and (c) names **consumers** and **release
engineering** as first-class. This supersedes the earlier numbering *for execution
planning*; reconciling `PLATFORM_WORKSTREAMS.md` to match is a recommended governance
action (§Recommended Governance Improvements). Mapping is given per row.

| WS | Name | Mission | Maps to earlier | Primary obligations |
|---|---|---|---|---|
| **WS-0** | Program Management | Keep the program coherent: CURRENT_PROGRAM, dependency graph, capability map, risk register, synchronization. No implementation. | *(new)* | O2 (program self-honesty) |
| **WS-1** | Reasoning Substrate | The 18 reasoning **tasks** (classify→retrieve→analyze→decide→produce→validate→trace) as runnable task specs. | old WS-1 | O1, O5, O8 |
| **WS-2** | Engineering Model Contracts | The authoritative engineering-model contract (versioned-stable). | old WS-2 | O10 |
| **WS-3** | Responsibility Model | Five-role responsibility-and-authority model. | old WS-3 | O6 |
| **WS-4** | Knowledge Plane | Canonicalization, corrigibility, versioned knowledge lifecycle. | old WS-4/WS-6 | O3, O7, O9 |
| **WS-5** | Workflow Runtime | The **orchestration engine** + run lifecycle + provenance emission (drives WS-1 tasks). | *(split from old WS-1)* | O1, O6(halt), O8 |
| **WS-6** | Review Plane | Independent validation universalized (review packs, reviewer registry). | old (Review) | O5, O6 |
| **WS-7** | Artifact Synchronization *(Control responsibility, not a Plane — FD-1)* | Artifacts (projections) synchronized with the authoritative model. | *(Control responsibility)* | O10 |
| **WS-8** | Operational Evidence | Operational reality feeds evidence back to challenge assumptions/decisions. | *(new)* | O11, O12 |
| **WS-9** | Release Engineering | Coordinated reproducible releases; release automation. | old (Release) | O8 |
| **WS-10** | Consumers | Real projects exercise the substrate (starting with `context_switcher`). | *(new)* | O1, O5 |

For 0.3, the active workstreams are **WS-0, WS-1, WS-5, WS-6 (validation), WS-9 (release),
WS-10 (consumer proof)**. WS-2/3/4/7/8 are **deferred** (§Known Risks, §Deferred is implicit
in milestone sequencing).

---

## 5. Capability Map

Status ∈ {Implemented, In Progress, Planned, Research}. Owner `TBD (Founder)` where not yet
assigned — not invented. Full plane view: [PLATFORM_CAPABILITY_MAP](PLATFORM_CAPABILITY_MAP.md).

### 0.3 capabilities (detailed)

| Capability | Status | WS | Repo | Dependencies | Target |
|---|---|---|---|---|---|
| Single-task execution (`task_runner`) | Implemented | WS-1 | ecf | — | 0.2 |
| Intent/phase classification runners (CLASSIFY-0001/0002) | Implemented | WS-1 | ecf | task contract | 0.3 |
| Workflow planner / validator | Implemented | WS-5 | ecf | — | 0.2 |
| Run initializer / run-state transactions | Implemented | WS-5 | ecf | — | 0.2 |
| Artifact fingerprint / provenance digest | Implemented | WS-1/5 | ecf | — | 0.2 |
| **Task output-contract + execution-trace freeze** | **Planned (gate)** | WS-1/5 | ecf | — | 0.3 |
| Retrieval runners (RETRIEVE-0001/0002) | In Progress | WS-1 | ecf(+ekb) | contract freeze | 0.3 |
| Analysis runners (ANALYZE-0001…0007) | Planned | WS-1 | ecf | contract freeze | 0.3 |
| Decision/Production runners (DECIDE-0001/2, PRODUCE-0001) | Planned | WS-1 | ecf | contract freeze | 0.3 |
| Validation runner (VALIDATE-0001) + enforcement | Planned | WS-6/5 | ecf | contract freeze | 0.3 |
| Traceability runners (TRACE-0001/2/3) | Planned | WS-1 | ecf | contract freeze | 0.3 |
| **Orchestration engine** (drive DAG, halt at approval) | **Planned (spine)** | WS-5 | ecf | contract freeze | 0.3 |
| End-to-end run on real Work Request | Planned | WS-10 | ecf+cs | engine + all tasks | 0.3 |
| Provenance admissibility (continuous) | In Progress | WS-1/5 | all | provenance schema | continuous |
| Compliance evidence (continuous) | In Progress | WS-0 | all | — | continuous |

### Post-0.3 capabilities (summary)

| Capability | Status | WS | Target |
|---|---|---|---|
| Authoritative engineering-model contract (O10) | Planned | WS-2 | 0.4 |
| Responsibility-and-authority model (O6) | Planned | WS-3 | 0.4 |
| Evidence-based canonicalization (O3) | Planned | WS-4 | 0.5 |
| Durable stewardship (O4) | Planned | WS-6 | 0.5 |
| Safe supersession (O7) | Planned | WS-4 | 0.6 |
| First-class assumptions (O11) | Planned | WS-8 | 0.6 |
| Lifetime reasoning integrity (O12) | Research | WS-8 | 0.7 |
| Release automation (O8 deepen) | Planned | WS-9 | 0.9 |

---

## 6. Critical Path to v0.3.0

**Freeze contract → Orchestration engine → integrate 18 tasks → end-to-end run → 0.3 release.**

```
[WS-1/5] Freeze task output-contract + execution-trace + provenance write-points
        │  (gate — nothing else may stabilize before this is accepted)
        ▼
[WS-5] Orchestration engine skeleton (drives stubbed DAG to waiting_for_human_approval)
        │
        ├───────── parallel width: 16 task runners (WS-1) build off the frozen contract ─────────┐
        ▼                                                                                          │
[WS-5] Integrate real tasks into the engine  ◄─────────────────────────────────────────────────── ┘
        ▼
[WS-10] End-to-end reasoning run on a real context_switcher Work Request (join)
        ▼
[WS-9] Coordinated 0.3.0 release (once exit gate passes)
```

**What cannot be parallelized, and why:**
1. **Contract freeze** — a single shared interface. Building 16 task runners against an
   unfrozen contract guarantees 16× rework (R-Arch). It is the gate.
2. **Orchestration engine** — one coherent execution semantics (DAG ordering, inter-task
   validation, provenance write-points, halt boundary, stale/rerun handling). Split across
   sessions it forks the runtime. **One owner.**
3. **End-to-end run** — an inherent join: needs the engine *and* all 18 tasks. Cannot begin
   until the parallel width closes.

Program wall-clock ≈ `contract + engine + e2e`. The 16 task runners are **width, not
length** — they leave the critical path entirely if ≥3 sessions run them.

---

## 7. Parallelization Matrix

> Optimized for **capability independence**, not repository boundaries. Color: 🟢 may
> proceed independently now · 🟡 concurrent only via interface-first design, stabilize after
> a named contract · 🔴 must not start production before a prerequisite is accepted (research
> may overlap).

| Workstream / capability | Parallel? | Depends on | Produces | Consumes | Repo | Suggested session | Sync frequency |
|---|---|---|---|---|---|---|---|
| WS-0 Program Management | 🟢 always | — | CURRENT_PROGRAM, dep graph, risk register | all statuses | platform | *(founder/PM)* | continuous |
| **Contract freeze** (WS-1/5) | 🔴 first | — | task output-contract, exec-trace, provenance write-points | task specs | ecf | Session A (then hands off) | one-time gate |
| WS-5 Orchestration engine | 🟡 single owner | contract freeze | DAG runner, run manifest/state, halt | task runners, planner | ecf | **Session A** | daily during integration |
| WS-1 Retrieval (RETRIEVE-0001/2) | 🟢 after gate | contract freeze | context, knowledge package | EKB retrieval model | ecf+ekb | **Session B** | weekly |
| WS-1 Analysis (ANALYZE-0001…0007) | 🟢 after gate | contract freeze | forces/options/alternatives/tradeoffs/risks/gaps | retrieval outputs | ecf | **Session C** | weekly |
| WS-1 Decision/Production (DECIDE, PRODUCE) | 🟢 after gate | contract freeze | confidence, recommendation, report | analysis outputs | ecf | **Session D** | weekly |
| WS-6 Validation (VALIDATE-0001) + enforcement | 🟡 after gate | contract freeze, engine hooks | report validation, stale/rerun | all task outputs | ecf | **Session D/E** | weekly |
| WS-1 Traceability (TRACE-0001/2/3) | 🟢 after gate | contract freeze | reasoning trace, manifest, finalize | run record | ecf | **Session E** | weekly |
| Provenance admissibility (WS-1/5) | 🟡 continuous | provenance schema | admissibility checks | all runs | all | **Session E** | on contract change |
| WS-10 End-to-end run | 🔴 join | engine + all tasks | validated run record | everything | ecf+cs | *(join session)* | at gate |
| WS-9 Release 0.3 | 🔴 after e2e | run record, review | coordinated 0.3 tag | all | all | *(release session)* | at release |
| WS-2/3/4/7/8 (post-0.3) | 🔴 deferred | 0.3 proven | — | — | — | — | — |

---

## 8. Program Synchronization — WS-0 (permanent)

A standing, non-implementation workstream that keeps the program coherent as up to five
sessions run in parallel.

**Responsibilities:**
- Maintain **CURRENT_PROGRAM.md** (live weekly operational state — §9).
- Maintain the **dependency graph** and **capability map** as batches land.
- Maintain the **risk register** (§Known Risks) and drive mitigations.
- Run **weekly synchronization**: reconcile branch state, surface merge contention, confirm
  the contract has not silently drifted, re-ground obligation maturity from evidence (O2).
- **Cross-workstream coordination**: enforce that the contract freeze precedes fan-out, and
  that the orchestration engine has a single owner.
- **Governance interface**: carry OQ-GOV rulings and roadmap-reconciliation decisions to the
  founder; never resolve them by program formatting.

WS-0 owns no code and ships no capability; it exists so the other workstreams remain
independently reviewable and honestly reported.

---

## 9. CURRENT_PROGRAM specification

A **live, non-constitutional** operational document (changes weekly; owned by WS-0). It is
*not* created by this batch — this is its specification and a ready-to-instantiate snapshot.

**Required sections:**
- **Current milestone** — e.g., "0.3.0-dev — Workflow Proven."
- **Current workstreams** — which of WS-0…WS-10 are active this week.
- **Current blockers** — with owner and the capability they block.
- **Current Claude sessions** — session ↔ workstream ↔ branch.
- **Current critical path** — the live shortest chain and where it stands.
- **Recently completed** — batches accepted since last sync, with evidence links.
- **Next architectural review** — date/trigger (e.g., before O10 contract at 0.4).
- **Upcoming release** — target version + gate status.

**Seed snapshot (copy into `CURRENT_PROGRAM.md` when WS-0 stands up):**
```
Current milestone:     0.3.0-dev (Workflow Proven)
Active workstreams:    WS-0, WS-1, WS-5, WS-6
Current blockers:      Contract freeze (Batch 2) gates all task-runner stabilization
Claude sessions:       A=orchestration+contract, B=retrieval, C=analysis, D=decide/produce/validate, E=trace/provenance
Critical path:         contract freeze → engine skeleton → task integration → e2e run → 0.3 release
Recently completed:    TASK-CLASSIFY-0002 (phase) merged to develop; RETRIEVE-0001 in design
Next architectural review: before 0.4 (O10 authoritative-model contract)
Upcoming release:      0.3.0 (coordinated, non-recursive manifest)
```

---

## 10. Program Rules

Every implementation batch must answer all five, or it should not exist:
1. **Which workstream?** (WS-0…WS-10)
2. **Which capability?** (one, exactly)
3. **Which milestone?** (its target version + exit criterion it advances)
4. **Which principle?** (the constitutional obligation it serves)
5. **Which exit criterion?** (the measurable evidence it produces)

A batch that advances more than one capability is split. A batch that traces to no principle
is scope creep (P13) and is rejected.

---

## 11. Suggested Parallel Claude Sessions (five, by workstream)

Assigned by **capability independence**, never by repository — all five touch `ecf`, so a
repo-based split would serialize them.

| Session | Workstream focus | Why independent |
|---|---|---|
| **A — Runtime Spine** | Contract freeze → Orchestration engine (WS-1 gate, WS-5) | Single owner of shared execution semantics; must not be split |
| **B — Retrieval** | RETRIEVE-0001/0002 (WS-1) | Unique output paths; only consumes EKB retrieval model |
| **C — Analysis** | ANALYZE-0001…0007 (WS-1) | Seven independent tasks; heaviest — split into C1/C2 if a 6th session opens |
| **D — Decision & Report** | DECIDE-0001/2, PRODUCE-0001, VALIDATE-0001 (WS-1/6) | Consumes analysis outputs via bound paths, not shared state |
| **E — Trace & Provenance** | TRACE-0001/2/3 + provenance admissibility (WS-1/5) | Run-record tail; independent output paths |

**Sequencing:** Session A runs the **contract-freeze gate first and alone**; B–E begin once
the contract is accepted. A then owns engine integration while B–E fill task width. A **join
session** (any) runs the end-to-end proof.

**Session hygiene:** every session branches from `develop`, never `release/*`; one feature
branch per task (matching the existing `feature/task-*` convention) to keep five sessions
from colliding.

---

## 12. Next Ten Batches

Each advances exactly one capability, has acceptance criteria, produces measurable evidence,
names dependencies, and states parallel safety. All serve **0.3 (Workflow Proven)** plus WS-0
standup. *(No prompts — capability scope only.)*

| # | Batch | WS | Advances | Acceptance / evidence | Depends on | Parallel safety |
|---|---|---|---|---|---|---|
| 1 | Stand up Program Management | WS-0 | Live program coherence | CURRENT_PROGRAM instantiated; dep graph + risk register live | — | 🟢 independent (non-code) |
| 2 | **Freeze execution contract** | WS-1/5 | Task output-contract + exec-trace + provenance write-points | Contract versioned & accepted; CLASSIFY-0001/2 conform; write-ownership pinned | — | 🔴 gate — run first, alone |
| 3 | Orchestration engine skeleton | WS-5 | DAG execution to halt boundary (stubbed tasks) | Planned DAG runs node-by-node; writes run manifest/state; halts at `waiting_for_human_approval`; never invokes Production Engine | 2 | 🟡 single owner |
| 4 | Retrieval runners | WS-1 | RETRIEVE-0001/0002 | Context + knowledge-package tasks emit bound outputs + provenance | 2 | 🟢 parallel |
| 5 | Analysis runners I | WS-1 | ANALYZE-0001…0003 | Reasoning-context, forces, options produced; provenance per task | 2 | 🟢 parallel |
| 6 | Analysis runners II | WS-1 | ANALYZE-0004…0007 | Alternatives, trade-offs, risks, missing-info produced | 2 | 🟢 parallel |
| 7 | Decision & production runners | WS-1 | DECIDE-0001/2, PRODUCE-0001 | Confidence + recommendation + report produced | 2, (5/6 for real inputs) | 🟢 parallel |
| 8 | Validation + enforcement | WS-6/5 | VALIDATE-0001 + inter-task validation | Report validated; invalid inputs yield `stale`/`rerun_required` | 2, 3 | 🟡 concurrent w/ engine |
| 9 | Traceability + provenance admissibility | WS-1/5 | TRACE-0001/2/3 + admissibility rejection | Reasoning trace/manifest/finalize; runs with missing/mismatched provenance rejected (line-ending false-positives excluded) | 2, 3 | 🟢 parallel |
| 10 | End-to-end consumer proof | WS-10 | Real Work Request run (0.3 exit gate) | `context_switcher` Work Request → validated Recommendation Report + complete auditable run halting at approval; independent review pack passes | 3, 4–9 | 🔴 join |

---

## Known Risks

| # | Category | Risk | L | I | Mitigation |
|---|---|---|---|---|---|
| K1 | Architectural | Contract churns after task runners start → 16× rework | Med | High | Batch 2 gate; version the contract (stable, not frozen) |
| K2 | Technical | Orchestration engine under-scoped (DAG/validation/halt semantics) | Med | High | Batch 3 skeleton reaches halt boundary early against stubs, then integrate |
| K3 | Operational | 5 sessions collide on shared ecf files | Med | Med | Branch-per-task off develop; unique output paths; contract shrinks shared surface |
| K4 | Release | 0.3 provenance validation fails on CRLF/LF digest mismatch though content identical | High | Med | Normalize line endings in digest step; treat mismatch as line-ending suspect before content |
| K5 | Governance | **Roadmap-view divergence** (plane labels vs ratified obligations) left unresolved | Med | Med | Founder ruling; until then, ratified obligations govern exit criteria (§3) |
| K6 | Governance | Acting before OQ-GOV rulings | Low | Low | 0.3 halts at human approval (P7 by design); minimal governance surface |
| K7 | Review | Weak independent validation → unverifiable substrate | Low | High | Every batch independently reviewed via review packs (P6); generator ≠ sole ratifier |
| K8 | Knowledge | RETRIEVE tasks blocked on EKB retrieval-model gaps | Low | Med | Validate against EKB retrieval model early (Batch 4) |

---

## Recommended Governance Improvements

1. **Resolve the roadmap-view divergence (K5).** Decide whether the plane-delivery sequence
   (Review→Artifact→Operational Evidence→Knowledge→Consumers) becomes authoritative or
   remains a lens. This is a change to a ratified document — run it through the governance
   cycle at roadmap/architecture scope. Until ruled, obligations govern.
2. **Reconcile `PLATFORM_WORKSTREAMS.md` to the WS-0…WS-10 partition** (§4) so the execution
   plan and the constitutional workstream doc use one numbering.
3. **Close Workshop 4** — rule on OQ-GOV-001 (genesis authority), OQ-GOV-002 (anti-capture),
   OQ-GOV-003 (change-class ladder T0–T5). Until then, `PLATFORM_GOVERNANCE.md` remains
   Partially Ratified and batch routing (§10) rests on a Draft ladder.
4. ~~**Commission `PLATFORM_ARCHITECTURE.md`**~~ **DONE** — [PLATFORM_ARCHITECTURE](PLATFORM_ARCHITECTURE.md)
   is ratified; it owns the Plane taxonomy and resolved the accountability-as-Plane question
   (FD-3). §4/§5 no longer carry Draft architecture.

---

## Metadata

| Field | Value |
|---|---|
| Owner | Founder (program), WS-0 (maintenance) |
| Status | Active — Draft where dependent on unresolved governance (K5, Recommendations) |
| Document Version | 0.1.0 |
| Applies To | AI Engineering Platform (all repositories) |
| Review Cadence | Weekly (via CURRENT_PROGRAM); plan re-baselined per milestone |
| Supersedes | The previous (v1) execution guide/report |

### Decision history
- **0.1.0** — Established as the constitution-driven v2 execution plan. Milestone exit
  criteria anchored to ratified obligations; plane labels carried as overlay. Adopted the
  WS-0…WS-10 partition (rationale §4). Critical path to 0.3 grounded in repository inspection
  (18-task DAG, existing `task_runner`/planner/validator tooling, missing orchestration
  engine, 0.2.0 baseline).

### Open questions
- K5 roadmap-view divergence · OQ-GOV-001/002/003 · FD-2 (Operational Evidence) · owners
  `TBD (Founder)` across sessions. *(OQ-ARCH-001 resolved by PLATFORM_ARCHITECTURE FD-3.)*

### Cross references
- [PLATFORM_MISSION](PLATFORM_MISSION.md) · [PLATFORM_VISION](PLATFORM_VISION.md) · [PLATFORM_PRINCIPLES](PLATFORM_PRINCIPLES.md) · [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md) · [PLATFORM_GOVERNANCE](PLATFORM_GOVERNANCE.md) · [PLATFORM_CAPABILITY_MAP](PLATFORM_CAPABILITY_MAP.md) · [PLATFORM_WORKSTREAMS](PLATFORM_WORKSTREAMS.md) · [PLATFORM_PARALLELIZATION](PLATFORM_PARALLELIZATION.md) · [PLATFORM_RELEASE_STRATEGY](PLATFORM_RELEASE_STRATEGY.md)
