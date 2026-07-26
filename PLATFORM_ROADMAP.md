# PLATFORM_ROADMAP

> **This document is explicitly non-constitutional.** It answers *"what must become true
> next?"* — not *"what must always be true?"* (see [PLATFORM_PRINCIPLES](PLATFORM_PRINCIPLES.md)).
> It may change freely as the platform matures, **without reopening constitutional
> debate.** Every roadmap item traces to a constitutional obligation; an item that serves
> no obligation is scope creep (P13).

---

## The roadmap's spine

**Constitutional obligation → Current capability → Gap → Planned milestones.**

The roadmap is organized along three orthogonal dimensions:

1. **Constitutional obligations (Why)** — the rows; derived from the ratified principles;
   change rarely.
2. **Platform capabilities / Planes (What)** — long-lived architectural capabilities that
   satisfy obligations. See [PLATFORM_CAPABILITY_MAP](PLATFORM_CAPABILITY_MAP.md).
3. **Deliverables (How)** — what is actually built (repositories, engines, schemas). See
   [PLATFORM_WORKSTREAMS](PLATFORM_WORKSTREAMS.md).

`Obligation → Capability → Deliverable → Task` gives end-to-end traceability from
constitution to commit.

---

## What 1.0 means

**1.0 is defined constitutionally, not by feature completeness:**

> Every constitutional obligation is implemented to at least **Partial** maturity, with no
> known architectural contradiction preventing advancement to **Strong**.

After 1.0, the roadmap deepens maturity; it no longer fills existential gaps.

---

## Constitutional obligations and current maturity

Maturity scale: **None · Emerging · Partial · Strong.** Baseline established by inspection
of the platform repositories at released version **0.2.0**.

| # | Obligation (principle) | Maturity | Gap |
|---|---|---|---|
| O1 | Intelligibility — decisions carry recoverable judgment (P1) | Partial | Recoverable judgment exists only for parts of the lifecycle |
| O2 | Platform self-honesty (P2) | Strong | Automated evidence-backed compliance reporting |
| O3 | Canonicalization by evidence/review (P3, P4) | Emerging | Complete evidence-driven canonicalization workflow |
| O4 | Answerability (P5) | Emerging | Durable, transferable stewardship across the lifecycle |
| O5 | Independent validation (P6) | Strong | Extend separation-of-generation-and-validation to every workflow |
| O6 | Indestructible responsibility (P7) | **Partial** *(0.4.0)* | Vacancy/succession/escalation are descriptive-only; runtime enforcement is O4's 0.5 job |
| O7 | Corrigibility (P14) | Emerging | Safe supersession while preserving history |
| O8 | Provenance (P8) | Strong | Cross-plane (and eventually cross-reasoning) provenance |
| O9 | Versioned knowledge (P9) | Strong | Automated lifecycle governance |
| O10 | Engineering-model synchronization (P10) | **Partial** *(0.4.0)* | Full model contract (version/compatibility/migration/identity); cross-repo projection |
| O11 | First-class assumptions (P11) | Emerging | Executable assumptions with review triggers |
| O12 | Lifetime reproducibility — the "throughout their lifetime" clause | Emerging | Long-term preservation of engineering judgment (Open Question 001) |

**The road to 1.0 is now five obligations** — the Emerging set: **O3, O4, O7, O11, O12.**
(O6 and O10 reached Partial at 0.4.0.) Everything else is deepening.

> **Status update (2026-07-25).** The milestone line below has been **completed through 1.0**:
> the **1.0 Constitutional Baseline** shipped and was independently audited — **12/12 obligations
> ≥ Partial, 3 Strong (O2, O5, O9), 0 contradictions blocking Strong** (see
> [CONSTITUTIONAL_READINESS_REPORT_0.9](CONSTITUTIONAL_READINESS_REPORT_0.9.md)). The maturity
> snapshot above is the **0.2.0 baseline** and is retained as history; the current per-obligation
> position is the 1.0 audited set. Post-1.0 work is *deepening* (Partial → Strong), organized by
> [POST_1.0_DEEPENING_ROADMAP](POST_1.0_DEEPENING_ROADMAP.md), not new milestones.

---

## Current position

| | |
|---|---|
| Released baseline | **1.0.0 Constitutional Baseline** *(ECF v1.0.0; advanced to **v1.0.3**). EKB v0.2.1; context_switcher 0.2.0* |
| Current development line | **Post-1.0 deepening** — continuous/opportunistic (see [POST_1.0_DEEPENING_ROADMAP](POST_1.0_DEEPENING_ROADMAP.md)) |
| Next milestone | **None on the constitutional line** — 1.0 is the constitutional baseline; deepening ships as point releases (v1.0.1 … v1.0.3) as done |
| Scope note *(2026-07-25)* | ECF scope-lifecycle amendment ratified: ECF is a full-lifecycle production engine; **2.0** is redefined as lifecycle-production coverage ([AMENDMENT_ECF_SCOPE_LIFECYCLE](AMENDMENT_ECF_SCOPE_LIFECYCLE.md)) |
| Progress note *(2026-07-27)* | Toward the redefined 2.0: **6 lifecycle-stage producers built & registered** (`draft`) in ECF; **five validated documents produced end-to-end on WR-0004** (FRS/SDD/EP/LR/TP-0004, each halting at `waiting_for_human_approval`). Capability-Matrix coverage **11.9% (18/151)**; Engineering Decision Ledger **20 entries**; `engineering_kb` **77 guides / 18 disciplines**. ECF v1.0.3 / EKB v0.2.1 unchanged |

**Honesty guard (O2/P2):** a version is claimed only when its milestone contract is met,
validated, and released. 1.0 was claimed on that basis (independently audited); post-1.0
point releases are claimed the same way. Obligations reach **Strong** only on real evidence —
the platform does not manufacture triggering events (P2).

---

## Milestone line (ratified — obligation-based)

Each milestone states **goals, capabilities, and exit criteria** — not feature lists.

### 0.2.0 — Released framework baseline *(shipped)*
- **Goal:** operational three-plane foundation.
- **Capabilities:** governed knowledge (Knowledge Plane), controlled execution (Control
  Plane), project adoption (Project Plane), coordinated release engineering.
- **Exit criteria:** met — coordinated private release of `engineering_kb`, `ecf`,
  `context_switcher` at 0.2.0. See [PLATFORM_RELEASE_STRATEGY](PLATFORM_RELEASE_STRATEGY.md).

### 0.3.0 — Controlled Reasoning Workflow substrate
- **Goal:** establish the first contract-governed path from Work Request through intent
  classification, phase classification, authoritative context retrieval, and bounded
  downstream reasoning, with runner-owned contracts and provenance.
- **Capabilities:** reasoning-workflow substrate (this does **not** bring O11/O12 to
  Partial — it creates the execution substrate later obligations build on).
- **Exit criteria:** a Work Request executes end-to-end through the governed workflow with
  recorded provenance and independent validation.

### 0.4.0 — Authoritative Model & Responsibility Foundations
- **Goal:** put the two foundational contracts in place that later capabilities reference.
- **Capabilities:** **O10** authoritative engineering-model contract (versioned and stable
  — *not* frozen: explicit version, compatibility rules, migration policy, identity
  semantics, validation boundary, change process); **O6** responsibility-and-authority
  model (all five roles + transfer, vacancy, escalation, succession, institutional vs
  individual authority).
- **Exit criteria:** O10 and O6 each reach **Partial**.

### 0.5.0 — Canonicalization & Stewardship
- **Goal:** make knowledge canonical by evidence, and accountability durable.
- **Capabilities:** **O3** evidence-based canonicalization; **O4** durable stewardship and
  challenge routing (operationalizes O6).
- **Exit criteria:** O3 and O4 each reach **Partial**.

### 0.6.0 — Corrigibility & Assumption Lifecycle
- **Goal:** allow canonical knowledge to be superseded safely, and open the first-class
  assumption lifecycle. *(The Reasoning Plane is already open; what opens here is the
  assumption lifecycle, not reasoning itself.)*
- **Capabilities:** **O7** safe supersession (depends on O3); **O11** executable
  assumptions with review triggers (depends on O10).
- **Exit criteria:** O7 and O11 each reach **Partial**.

### 0.7.0 — Lifetime Reasoning Integrity
- **Goal:** move the platform's weakest obligation from unaddressed to demonstrated.
- **Capabilities:** **O12** lifetime reproducibility of judgment (depends on O11) —
  assumption identity, dependency propagation, invalidation, degraded-reproducibility
  states, reasoning migration across tools and models.
- **Exit criteria:** O12 reaches **Partial**; Open Question 001 has a demonstrated partial
  mechanism.

### 0.8.0 — Cross-Plane Integrity
- **Goal:** deepen the already-strong obligations across plane boundaries.
- **Capabilities:** deepen O8 (cross-plane provenance), O5 (universal independent
  validation), O1 (judgment attachment over time).
- **Exit criteria:** the deepened obligations demonstrably hold *across* planes, not only
  within them.

### 0.9.0 — Constitutional Readiness
- **Goal:** verify, with evidence, that every obligation meets the 1.0 threshold.
- **Capabilities:** evidence-backed constitutional audit; resolution of any blocking
  architectural contradiction.
- **Exit criteria:** an independent, evidence-backed report shows every obligation ≥
  Partial with no contradiction blocking Strong. *(O2 does not begin here — it runs
  continuously from 0.3 onward; 0.9 is the formal assessment.)*

### 1.0.0 — Constitutional Baseline
- **Goal:** the constitutional definition of 1.0 is met.
- **Exit criteria:** every obligation ≥ Partial, no known architectural contradiction
  preventing Strong.

---

## Parallelization

The dependency ordering and concurrency rules for these milestones live in
[PLATFORM_PARALLELIZATION](PLATFORM_PARALLELIZATION.md). In brief: **serialize accepted
contracts before dependent stabilization; parallelize across narrow versioned interfaces;
cross-cutting capabilities advance continuously.**

---

## Metadata

| Field | Value |
|---|---|
| Owner | Founder |
| Status | Ratified (Genesis) |
| Document Version | 0.1.0 |
| Applies To | AI Engineering Platform (all repositories) |
| Review Cadence | Quarterly |

### Decision history
- **0.1.0** — Milestone line ratified in Workshop 3, organized by constitutional obligation.
- **1.0 definition** — Defined constitutionally (every obligation ≥ Partial) rather than by
  feature completeness.
- **O10 de-implemented** — Reworded from "rendered artifacts" (a mechanism) to
  "engineering-model synchronization" (the invariant).
- **Current-position ruling** — Released at 0.2.0; on the 0.3.0-dev line; not to be called
  "at 0.3" until the 0.3 milestone contract is met and released.
- **Roadmap-view reconciliation** — The Platform Constitution Establishment Batch proposed
  an alternative, *plane-delivery-based* milestone naming (0.4 Review Plane, 0.5 Artifact
  Plane, 0.6 Operational Evidence, …). Per the batch's own instruction to treat approved
  workshop outputs as the source of truth, the ratified **obligation-based** sequence above
  is authoritative here; the plane-delivery view is recorded as a complementary lens in
  [PLATFORM_CAPABILITY_MAP](PLATFORM_CAPABILITY_MAP.md). *(Founder recommendation accepted.)*
- **0.3.0 / 0.4.0 released; position advanced (2026-07-16)** — 0.3.0 (Workflow Proven) and
  0.4.0 (Authoritative Model & Responsibility Foundations) met their milestone contracts and
  shipped (`ecf` v0.3.0 / v0.4.0). O6 and O10 recorded at **Partial**; the Emerging set is now
  O3, O4, O7, O11, O12. 0.5 kicked off — founder rulings recorded in
  [PROGRAM_0.5](PROGRAM_0.5.md).
- **1.0 shipped; post-1.0 deepening; scope reconceived (status update 2026-07-25)** —
  Non-constitutional status reconciliation (the milestone line itself is unchanged). The
  **1.0 Constitutional Baseline** shipped and was independently audited (12/12 ≥ Partial; 3
  Strong: O2/O5/O9); ECF has advanced to **v1.0.3** on point releases. Post-1.0 direction is
  continuous deepening ([POST_1.0_DEEPENING_ROADMAP](POST_1.0_DEEPENING_ROADMAP.md)). The
  **ECF scope-lifecycle amendment** is ratified (Genesis): ECF is a full-lifecycle production
  engine (Producer/Governor Boundary), **2.0 redefined as lifecycle-production coverage**
  ([AMENDMENT_ECF_SCOPE_LIFECYCLE](AMENDMENT_ECF_SCOPE_LIFECYCLE.md)). Current-position snapshot
  updated accordingly.

- **Lifecycle-production progress (status update 2026-07-27)** — Non-constitutional status
  reconciliation (milestone line unchanged). Toward the redefined 2.0 (lifecycle-production
  coverage): ECF now has **six lifecycle-stage producers built and registered** as `draft`
  workflows (WF-REQUIREMENTS/DESIGN/PLAN/VALIDATION/LEARNING/TECHSPEC-0001), and **five real,
  independently validated lifecycle documents produced end-to-end on WR-0004** (FRS-0004, SDD-0004,
  EP-0004, LR-0004, TP-0004), each halting non-canonical at `waiting_for_human_approval`.
  Capability-Matrix coverage stands at **11.9% (18/151)** with a Learning stage-11 section; the
  Engineering Decision Ledger holds **20 entries**; `engineering_kb` reached **77 decision guides
  across 18 disciplines**. WF-USECASE is not yet on `develop`.

### Open questions
- **Open Question 001** — long-term integrity of engineering judgment; targeted by 0.7.
- **Plane taxonomy — RATIFIED** in [PLATFORM_ARCHITECTURE](PLATFORM_ARCHITECTURE.md)
  (constructive/cross-cutting; Accountability is a governance concern, not a Plane). The one
  remaining architectural item is **FD-2** (Operational Evidence as a distinct Plane),
  deferred to 0.6.

### Cross references
- [PLATFORM_ARCHITECTURE](PLATFORM_ARCHITECTURE.md) · [PLATFORM_PRINCIPLES](PLATFORM_PRINCIPLES.md) · [PLATFORM_CAPABILITY_MAP](PLATFORM_CAPABILITY_MAP.md) · [PLATFORM_WORKSTREAMS](PLATFORM_WORKSTREAMS.md) · [PLATFORM_PARALLELIZATION](PLATFORM_PARALLELIZATION.md) · [PLATFORM_RELEASE_STRATEGY](PLATFORM_RELEASE_STRATEGY.md)
