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
| Platform Version | **ECF `v1.0.3`** (1.0 Constitutional Baseline + post-1.0 point releases) · EKB **0.2.1** · context_switcher 0.2.0 |
| Current Milestone | **1.0.0 — Constitutional Baseline** (CRR ratified 2026-07-18; see [CONSTITUTIONAL_READINESS_REPORT_0.9](CONSTITUTIONAL_READINESS_REPORT_0.9.md)) |
| Target Milestone | **Post-1.0 deepening** (Partial → Strong) **+ lifecycle-production coverage** (toward the redefined 2.0 — [AMENDMENT_ECF_SCOPE_LIFECYCLE](AMENDMENT_ECF_SCOPE_LIFECYCLE.md)) |
| Current Health | 🟢 **Stable** |
| Current Critical Path | Post-1.0: no existential gaps remain. Deepen the 9 Partial obligations toward Strong, and grow lifecycle-stage coverage — **six producers built; five validated documents produced on WR-0004; Capability-Matrix coverage 11.9% (18/151)** — as real artifacts accrue. |
| Current Release State | Private Git releases: ECF **`v1.0.3`**, EKB `v0.2.1`; context_switcher at 0.2.0 (develop carries the five WR-0004 lifecycle runs — Requirements/Design/Plan/Learning/Validation — each halted at `waiting_for_human_approval`) |
| Overall Status | 🟢 **1.0 Constitutional Baseline** — 12/12 obligations ≥ Partial on real evidence, independently audited (3 Strong: O2/O5/O9), 0 contradictions blocking Strong |
| Constitutional Status | **Ratified (Genesis)** — Independent Reaffirmation Obligation **discharged** by the 0.9 independent audit (2026-07-18) |

> ### Status update (2026-07-27)
> Lifecycle-production progress since the 2026-07-25 note (non-constitutional; verified on
> `ecf`/`engineering_kb` `develop`):
> - **Full-lifecycle producer set built & registered** — `ecf/workflows/WORKFLOW_CATALOG.md` now
>   registers, alongside the `released` **WF-REASON-0001** and **WF-TRANSFORM-0001**, six `draft`
>   lifecycle-stage producers: **WF-REQUIREMENTS-0001**, **WF-DESIGN-0001**, **WF-PLAN-0001**,
>   **WF-VALIDATION-0001** (Test Plan), **WF-LEARNING-0001**, **WF-TECHSPEC-0001** (Technical
>   Specification). **WF-USECASE** (Use Case Model) is **not yet on `develop`**.
> - **Five real, independently validated lifecycle documents** produced end-to-end on one case
>   (**WR-0004, WinUI**), each halting non-canonical at `waiting_for_human_approval`: **FRS-0004**,
>   **SDD-0004**, **EP-0004**, **LR-0004**, **TP-0004**.
> - **Capability Matrix** roll-up (`tools/capability_matrix/`) reports **11.9% coverage (18/151)**;
>   a **Learning (stage 11)** section was added (EDL-0019).
> - **Engineering Decision Ledger** now holds **20 entries** (EDL-0001…0020).
> - **`engineering_kb`** grew to **77 decision guides across 18 disciplines** (75 Complete, 2 In
>   Progress); 6 quality attributes, 7 patterns.
> - Versions unchanged: **ECF v1.0.3**, **EKB v0.2.1**.

> ### Status update (2026-07-25)
> **The dashboard above is current; the milestone/workstream/batch sections further down remain
> the 0.3-era operational snapshot and are retained as history.** Since 1.0 shipped:
> - **ECF scope-lifecycle amendment ratified (Genesis)** — ECF is now a **full-lifecycle
>   document-production engine** under the **Producer/Governor Boundary**; **2.0 is redefined as
>   lifecycle-production coverage** ([AMENDMENT_ECF_SCOPE_LIFECYCLE](AMENDMENT_ECF_SCOPE_LIFECYCLE.md)).
> - **Engineering Design stage built** — `WF-DESIGN-0001` (System Design Document) is a real,
>   validated workflow; a live **EDR-0003** design run is in progress.
> - **Engineering Decision Ledger** live — append-only, all decision classes, **14 entries**, with
>   a hardened validator; a **Capability Matrix** coverage tracker exists.
> - **AI executor** gained bounded transient auto-retry; full suite **~1470 tests**.
> - **`engineering_kb`** grew to the **full reserved catalog** — **48 decision guides / 14
>   disciplines / 6 quality attributes / 7 patterns**, all validated.
> - **Process:** clone-per-thread parallel fan-out is the default work policy (repo `CLAUDE.md`).
> - **In progress (not yet merged):** stage workflows **WF-REQUIREMENTS** (stage 2) and
>   **WF-PLAN** (stage 6).

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
| `ecf` (Control) | **1.0.3** | develop | Constitutional Baseline + post-1.0 point releases. Full-lifecycle production engine (Producer/Governor Boundary, ratified). Two `released` workflows (WF-REASON-0001, WF-TRANSFORM-0001) plus **six `draft` lifecycle producers** (Requirements/Design/Plan/Validation/Learning/TechSpec); **five validated documents produced end-to-end on WR-0004** (FRS/SDD/EP/LR/TP-0004, each halting at `waiting_for_human_approval`). Engineering Decision Ledger (**20 entries**, hardened validator) + Capability Matrix tracker (**11.9%, 18/151**); cross-plane provenance. Bundles EKB 0.2.1 |
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
| Last state basis | **ECF v1.0.3 (1.0 Constitutional Baseline + post-1.0 point releases); EKB 0.2.1; six lifecycle producers built & registered (`draft`), five validated documents on WR-0004 (FRS/SDD/EP/LR/TP-0004); Capability Matrix 11.9% (18/151); Engineering Decision Ledger 20 entries; engineering_kb 77 guides / 18 disciplines — verified 2026-07-27** |

### Cross references
- [PROGRAM_0.4](PROGRAM_0.4.md) · [PROGRAM_EXECUTION_PLAN](PROGRAM_EXECUTION_PLAN.md) · [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md) · [PLATFORM_ARCHITECTURE](PLATFORM_ARCHITECTURE.md) · [PLATFORM_GOVERNANCE](PLATFORM_GOVERNANCE.md) · [PLATFORM_CAPABILITY_MAP](PLATFORM_CAPABILITY_MAP.md)
