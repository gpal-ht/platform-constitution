# CURRENT_PROGRAM

> **Operational control board.** Answers *"what should the engineering organization do this
> week?"* — never *"what should the platform become?"* (the Constitution answers that). This
> document is **non-constitutional**, changes frequently, and every edit to it is a **T1
> Operational** change ([PLATFORM_GOVERNANCE](PLATFORM_GOVERNANCE.md)). It **records** reality;
> it never redefines strategy, architecture, governance, or roadmap.

---

## Program Dashboard

| Field | Value |
|---|---|
| Platform Version | **1.0.0 released** (`ecf`) · EKB **0.2.1** · context_switcher 0.2.0 |
| Current Milestone | **1.0.0 — Constitutional Baseline** (CRR ratified 2026-07-18; see [CONSTITUTIONAL_READINESS_REPORT_0.9](CONSTITUTIONAL_READINESS_REPORT_0.9.md)) |
| Target Milestone | **Post-1.0 deepening** — Partial → Strong (breadth + reality-gated items); first hardening: the gate-9 drift forcing-function (fires vacuously) |
| Current Health | 🟢 **Stable** |
| Current Critical Path | Post-1.0: no existential gaps remain. Deepen the 9 Partial obligations toward Strong as real artifacts and events accrue. |
| Current Release State | Private Git releases: ECF **`v1.0.0`**, EKB `v0.2.1`; context_switcher at 0.2.0 (develop carries the EDR-0002 projection) |
| Overall Status | 🟢 **1.0 Constitutional Baseline** — 12/12 obligations ≥ Partial on real evidence, independently audited (3 Strong: O2/O5/O9), 0 contradictions blocking Strong |
| Constitutional Status | **Ratified (Genesis)** — Independent Reaffirmation Obligation **discharged** by the 0.9 independent audit (2026-07-18) |

### Constitutional document status *(recorded, not reinterpreted)*

| Document | Status |
|---|---|
| Mission · Vision · Principles | Ratified (Genesis) — Principles **0.2.0** (+ Clarification C, AMENDMENT_O6) |
| Architecture | Ratified (Genesis) — FD-2 deferred to 0.6 |
| Governance | Ratified (Genesis) — **1.1.0-genesis** (+ Doctrine E, AMENDMENT_O6) |
| Roadmap | Ratified (Genesis) |
| Capability Map | Ratified (Genesis), synced to Architecture |
| Program Execution Plan | Active |
| Glossary / Parallelization | Ratified (Genesis) portions · Draft portions — Glossary **0.3.0** (+ individual/institutional authority, AMENDMENT_O6) |
| Workstreams / Release Strategy | Draft |

---

## Current Platform State *(one page)*

| Repo (Plane) | Released | Current branch | Notes |
|---|---|---|---|
| `engineering_kb` (Knowledge) | **0.2.1** | develop | Intent model disambiguated (EKP-0001); retrieval engine drives authoritative closures |
| `ecf` (Control) | **1.0.0** | develop | Constitutional Baseline. Two workflows (WF-REASON-0001, WF-TRANSFORM-0001) driven end-to-end on real WRs; 3 canonical EDRs; cross-plane provenance; 1372 tests, 11 release gates. Bundles EKB 0.2.1 |
| `context_switcher` (Project) | 0.2.0 | feature/work-engine-project-registry (parked); develop carries WR-0001/0003/0004 + EDR-0002 projection | First consumer; WR-0001 → EDR-0002, WR-0004 → EDR-0003 |

**Architectural maturity:** three constructive Planes operational; the Control Plane now
**executes** the reasoning workflow end-to-end (not just single tasks), and the Review Plane
performs independent report validation as a workflow task.

**Current known limitations:**
- **Formal 18/18 halt run deferred** — the live run reached 16/18 (report produced + independently
  validated `passed`); the two traceability executors are fixed and unit-green but not yet
  exercised live to the formal `waiting_for_human_approval` halt.
- **RETRIEVE-0001 classification-consumption is implemented but not contract-enforced** — the
  enforcement check is deferred to 0.4 (ECD-0002).
- **Resume-cascade:** any code change invalidates a run's prior provenance (reproducibility by
  design), so resuming after an executor fix re-runs the DAG. Cheap resume (per-task env scoping)
  is a 0.4 candidate.
- Reasoning integrity (assumptions, judgment over time) is Research; Reasoning Plane is future.

---

## Current Milestone — 0.3.0 Workflow Proven ✅ SHIPPED

- **Mission:** Establish the first contract-governed path Work Request → intent → phase →
  authoritative context → bounded reasoning, with runner-owned contracts and provenance,
  halting at human approval. **Achieved.**
- **Exit criteria — status:**
  - ✅ 18-task DAG runs via an orchestration engine.
  - ✅ Every task emits admissible provenance (all gates provenance-verified).
  - ✅ A real `context_switcher` Work Request produces a **validated** Engineering Recommendation
    Report (independent verdict: `passed`).
  - ✅ Independent review passes.
  - ⚠️ Complete run record halting at `waiting_for_human_approval` — substantively proven to 16/18;
    all 18 executors code-complete and unit-green; **formal 18/18 halt run deferred**.
- **Evidence (WR-0001):** recommendation `gather_additional_evidence` — the retrieval chain caught
  that ADR-0005 was absent from the permitted sources and carried the finding forward (T4 rule) to
  govern the recommendation. Report + validation committed with provenance.
- **Release:** ECF `v0.3.0` tagged and merged to `develop`; all release gates pass in-place.

---

## Critical Path

**0.3 is shipped.** The forward path is 0.4 planning.

```
0.3.0 — Workflow Proven  ✅ SHIPPED
    ↓
0.4 planning
    ├─ formal 18/18 live halt run (close the last exit-criterion gap)
    ├─ ECD-0002: RETRIEVE-0001 contract enforces classification consumption
    ├─ resume-cascade: per-task provenance/env scoping for cheap resume-after-fix
    └─ (roadmap-defined 0.4 scope)
```

---

## Workstreams *(ratified model; owner = role, not person)*

| WS | Mission | Current capability | State | Blocked? | Depends on | Parallel? | Owner Role |
|---|---|---|---|---|---|---|---|
| **WS-0** Program Management | Keep the program coherent | This board + dependency graph | 🟢 Active | No | — | Always | Program Steward |
| **WS-1** Reasoning Substrate | 18 reasoning tasks runnable | **All 18 executors shipped** | 🟢 Done (0.3) | No | — | — | Reasoning Task Engineer |
| **WS-5** Workflow Runtime | Orchestration engine + run lifecycle | **Engine drives DAG to halt; --live + recovery** | 🟢 Done (0.3) | No | — | — | Runtime Architect |
| **WS-6** Review Plane | Independent validation | **VALIDATE-0001 executor shipped; verdict recorded** | 🟢 Done (0.3) | No | — | — | Review Engineer |
| **WS-9** Release Engineering | ECF 0.3 release | **v0.3.0 tagged + merged** | 🟢 Done (0.3) | No | — | — | Release Engineer |
| **WS-10** Consumers | Real Work Request end-to-end | **WR-0001 driven to validated recommendation** | 🟢 Substantially done | No | formal 18/18 run | Join | Consumer/Adoption Engineer |
| WS-2/3/4/7/8 | 0.4+ foundations & later | — | ⚪ Deferred | — | 0.4 | — | (deferred) |

---

## Current Batches *(status only — no backlog, no wish list)*

| Batch | State |
|---|---|
| 0.2.0 coordinated release | ✅ Completed |
| Constitution + Architecture + Governance | ✅ Completed |
| Execution Contract Freeze | ✅ Completed |
| Per-task output-contract registry (T3) + strict validation | ✅ Completed |
| Orchestration engine (C11) + walking skeleton | ✅ Completed |
| EKB 0.2.1 — EKP-0001 intent-model disambiguation | ✅ Completed |
| All 18 task executors (classify/retrieve/analysis/decision/production/validation/trace) | ✅ Completed |
| Executor fan-out (AN / DP / VT) + WS-0 registry integration | ✅ Completed |
| Full-DAG live run on WR-0001 → validated report | ✅ Completed (16/18; formal halt deferred) |
| **ECF 0.3.0 release (tag + develop merge)** | ✅ Completed |
| Formal 18/18 halt run | 🔵 Deferred → 0.4 |
| ECD-0002 contract enforcement | 🔵 Deferred → 0.4 |
| Resume-cascade (per-task env scoping) | 🔵 Candidate → 0.4 |

---

## Governance

- **Constitutional status:** Ratified (Genesis) across the constitutional set.
- **Genesis status:** founder-only phase active; unilateral founder ratification still in
  effect; ends automatically at the substantive-independence trigger.
- **Recent ratifications (2026-07-15):** **T4** — WF-REASON-0001 Steps 17/18 carried-forward-blocker
  rule (workflow `draft` → `released`). **ECD-0002** enforcement explicitly deferred to 0.4.
  **T5 — AMENDMENT_O6 (O6 / P7) Ratified (Genesis)**, all 8 checklist items: PLATFORM_PRINCIPLES
  Clarification C (→ 0.2.0), PLATFORM_GOVERNANCE Doctrine E (→ 1.1.0-genesis), PLATFORM_GLOSSARY
  two terms (→ 0.3.0); folded into the Independent Reaffirmation Obligation.
- **0.4 obligation status:** **O10 — Partial (done, merged).** **O6 — descriptive model RATIFIED**
  (constitutional amendment) **+ B2 executable rule authorized & merged as a standalone module**
  (`ecf` `tools/authority_rule/`, merge `22c3fa7`; rule 6/6; regression 774/0). The rule is
  **inert until wired**: the `trace_completion.py` **T4 wiring is the one remaining step** before
  O6's executable half is live at runtime. **O6 is not yet fully "Partial-live"** until that lands;
  no frozen 0.3 contract was modified.
- **Outstanding open questions:** FD-2 Operational Evidence (decide 0.6) · Open Question 001
  judgment integrity (0.7) · **K5 resolved** (below).
- **Independent Reaffirmation Obligation:** outstanding; steward: Founder; trigger: first
  substantive independent constitutional authority. All constitutional docs remain `Ratified
  (Genesis)` until discharged.

---

## Current Risks *(real, not theoretical)*

| # | Risk | Likelihood | Impact | Mitigation | Owner Role |
|---|---|---|---|---|---|
| R1 | ~~Task output-contract churns after runners start~~ | — | — | **Retired** — contract frozen; all 18 executors shipped against it | Runtime Architect |
| R2 | ~~Orchestration engine under-scoped~~ | — | — | **Retired** — engine drives the full DAG to the halt boundary | Runtime Architect |
| R4 | ECF release:validate 4b (content_digest) fails after checkout on CRLF/LF | High | Low | **Known/accepted** — content byte-identical to tag; validates in-place; normalize in a future release | Release Engineer |
| R5 | Resume after an executor fix re-runs the whole DAG (provenance staleness) | High | Med | Freeze code for a run; scope env fingerprint per-task in 0.4 | Runtime Architect |
| R6 | AI executors slip the recommend/approve (P7) boundary in prose | Med | High | Machine-authoritative approval boundary + explicit forbidden-verb prompts; contracts fail closed | Reasoning Task Engineer |

---

## Upcoming Reviews

| Review | Cadence / Trigger |
|---|---|
| Program Sync | **Weekly** (WS-0) |
| Architecture Review | Trigger: before 0.4 (O10 authoritative-model contract) |
| Milestone Review | **0.3 exit — held** (this refresh) |
| Release Review | 0.4 (next coordinated release) |

*(Governance Review is annual / on-amendment — not imminent.)*

---

## Program Health

| Dimension | Status |
|---|---|
| Constitution | 🟢 |
| Architecture | 🟢 |
| Governance | 🟢 |
| Execution Contract | 🟢 Frozen + enforced |
| Runtime (Control) | 🟢 Executes the workflow end-to-end |
| Knowledge | 🟢 (EKB 0.2.1) |
| Review Plane | 🟢 Operational (report validation) |
| Reasoning Plane | ⚪ Research |
| **Overall** | 🟢 **0.3 Workflow Proven** |

---

## K5 Resolution *(recorded permanently)*

> **Capability milestones are normative. Architectural planes are descriptive. Workstreams are
> operational. These are three independent dimensions.**
>
> The ratified obligation-based milestones in [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md) are the
> single normative sequence. Plane-delivery is a descriptive lens; workstreams are the
> operational unit. **No operational planning may redefine constitutional milestones.**

This resolves the roadmap-view divergence (Program Plan K5). *(Follow-up: flip Program Plan K5
to "resolved" as a T2 edit; not done here to keep this board within its non-constitutional
scope.)*

---

## Integration Gates

### Strict-Validation Exit Gate — ✅ SATISFIED

All 18 task validators registered; strict unknown-task rejection is the default; the generic-pass
path survives only as an explicit test-only escape hatch the runner never takes; two tests prove
no workflow task can commit without a registered validator. Owner: WS-0. Closed.

### Executor Fan-Out Integration — ✅ SATISFIED

All 18 task **executors** implemented behind one explicit handler registry
(`tools/task_runner/executors/registry.py`), dispatched by two hosts (`ClaudeCodeExecutor`,
`DeterministicExecutor`). Fan-out (Analysis / Decision-Production / Validation-Trace) integrated;
registry reconciled by WS-0. Full regression **774 tests green**. Owner: WS-0. Closed.

---

## Metadata

| Field | Value |
|---|---|
| Owner Role | Program Steward (WS-0) |
| Status | **Operational (Living)** — non-constitutional; every edit is a T1 change |
| Change class | T1 Operational |
| Applies To | AI Engineering Platform (all repositories) |
| Update Cadence | Weekly (Program Sync), or on any state change |
| Last state basis | **ECF 0.3.0 released (2026-07-15); EKB 0.2.1; WF-REASON-0001 proven end-to-end on WR-0001** |

### Cross references
- [PROGRAM_0.4](PROGRAM_0.4.md) · [PROGRAM_EXECUTION_PLAN](PROGRAM_EXECUTION_PLAN.md) · [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md) · [PLATFORM_ARCHITECTURE](PLATFORM_ARCHITECTURE.md) · [PLATFORM_GOVERNANCE](PLATFORM_GOVERNANCE.md) · [PLATFORM_CAPABILITY_MAP](PLATFORM_CAPABILITY_MAP.md)
