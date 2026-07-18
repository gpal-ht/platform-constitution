# PLATFORM_ARCHITECTURE

> Constitutional document. It defines the **stable architecture** of the platform — the
> enduring capabilities (Planes), their responsibilities, their contracts, and the rules
> that govern how they depend on one another. It sits between
> [PLATFORM_PRINCIPLES](PLATFORM_PRINCIPLES.md) (*what must always be true*) and
> [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md) (*what must become true next*), and was identified
> as a required document by [PROGRAM_EXECUTION_PLAN](PROGRAM_EXECUTION_PLAN.md).
>
> **This is not an implementation guide.** It names no runners, schemas, functions, or
> versions. Every section is written to pass one test: *would this still be true in ten
> years?* Where it could not be derived from the constitution or the repositories, it says
> so and defers to a **Founder Decision** rather than choosing silently.

---

## 1. Purpose

**Why this document exists.** The constitution says *what* engineering must remain
(intelligible, challengeable, reproducible) and *why*. The roadmap says *when* capabilities
mature. Neither says **what enduring capabilities exist and how they relate**. Without that,
each capability would invent its own object model, dependency direction, and ownership — the
precise fragmentation the platform exists to end. This document fixes the **architecture**:
the stable set of Planes and the contracts between them.

**Relationship to the other constitutional documents.**
- **Vision** — architecture is how "engineering as a governed system" is decomposed into
  parts that can be built, owned, and evolved.
- **Principles** — every Plane and contract traces to a principle. Architecture is the
  structural realization of the Root Principle; it is admitted under P12 (no element stands
  alone) and P13 (no structure without demonstrable value).
- **Roadmap** — the roadmap sequences the *maturation* of these Planes; it does not redefine
  them. Planes are stable; their maturity is not.
- **Governance** — changes to this document are governed by the Root Governance Primitive at
  **architecture scope** (a T4-class change; see [PLATFORM_GOVERNANCE](PLATFORM_GOVERNANCE.md)).

---

## 2. Architectural Philosophy

**Engineering is decomposed as a governed system, not as software.** The platform's parts
are not modules, services, or tools; they are **responsibilities** in a system of knowledge,
control, judgment, validation, and evidence. The decomposition is chosen so that each part
can independently satisfy some clause of the Root Principle and be independently owned,
versioned, and reviewed.

Three philosophy-level commitments govern everything below:

1. **A Plane is a responsibility, not a repository.** *(Ratified constitutional rule.)*
   Repositories are *deliverables* that realize one or more Planes. A Plane may today live
   inside a shared repository and separate later; a repository may host more than one Plane.
   The chain is strict:

   > **Repositories implement Planes; Planes implement Responsibilities.**
   > Never `Repository = Plane`.

   This separation is what lets the architecture outlive any particular code layout.
   *(Ten-year test: the responsibilities endure even if every repository is reorganized.)*
2. **Dependencies flow in one direction, through versioned interfaces, never through
   internals.** This mirrors the platform's own operating rule that a layer may depend only
   on what is upstream of it. Cycles are forbidden.
3. **No part asserts its own authority.** No Plane ratifies its own output (P6), owns its own
   accountability (P7), or asserts its own provenance/release identity (the non-recursive
   rule). Authority always comes from outside the artifact.

**Not implementation. Not AI.** This architecture would be identical if the engineers were
entirely human or entirely machine. AI is an implementation capability that executes within
these Planes; it is not a Plane, and it is not named in any responsibility.

---

## 3. Platform Context

**The platform boundary.** The platform is the governed system that turns an engineering
*intent* into trustworthy engineering *decisions and artifacts*, with durable knowledge,
provenance, and review. Inside the boundary: the Planes below. Outside the boundary:
everything that *uses* or *feeds* the platform.

**External actors.**
- **The engineer** — the primary subject; originates intent, owns decisions, accepts
  responsibility.
- **AI engineering agents** — governed participants that execute within Planes; never the
  customer, never an authority.
- **Reviewers / accountable authorities** — individuals, councils, or institutions that
  challenge and dispose (may be human, machine, or hybrid — P5/P7).
- **Consuming projects** — concrete engineering efforts that adopt the platform.
- **Operational reality** — the running world that later contradicts or confirms assumptions.

**Repositories (deliverables, not Planes).**
- `engineering_kb` — realizes the **Knowledge Plane**.
- `ecf` — realizes the **Control Plane**, and today also hosts the **Review** responsibility
  and the runtime that will host the future **Reasoning Plane**.
- `context_switcher` — realizes the **Project Plane**; the platform's first consumer.
- `C:\Dev\platform` — the constitutional/governance home; not a repository, not a Plane.

**Future consumers.** Additional projects (each a Project-Plane instance) adopt the platform
at milestone 0.8 ("Multiple Consumers"). The architecture must support N consumers without
change to the upstream Planes — a constraint on the Project Plane's interface, below.

---

## 4. Planes

> Each Plane is defined by: **Mission · Responsibilities · Owns · Never owns · Primary
> artifacts · Primary outputs · Dependencies · Interfaces · Success criteria.** Every Plane
> is then **challenged**: does it belong, and would it still belong in ten years?

**The Plane taxonomy *(FD-5, Ratified)*.** Every part is either constructive or cross-cutting:
- **Constructive Planes** — produce engineering: **Knowledge, Control, Project.**
- **Cross-cutting Planes** — operate *across* constructive Planes: **Review, Release,** and
  (future) **Reasoning.**
- **Cross-cutting *concerns* that are not Planes** — enforced by every Plane but owning no
  execution responsibility of their own: **Governance / Accountability** (and, by the same
  test, security, observability, performance). They *influence* every Plane; they *are* not
  one.
- **Not Planes *(Ratified)*:** **Artifact** — an output category (FD-1); **Accountability** —
  a governance model (FD-3); **Operational Evidence** — a cross-cutting concern (FD-2,
  **Ruled 2026-07-16, Reading B**: evidence permanence is a named **Control-owned
  obligation**; consumption belongs to Reasoning under FD-4; re-open trigger — evidence
  from outside the platform boundary arrives, or ≥2 independent producers/consumers
  exist. Decision record: `FD2_DECISION_MEMO`).

### 4.1 Knowledge Plane *(constructive)*

- **Mission:** Hold the canonical, technology-neutral body of engineering knowledge — what
  "good" means — for humans and machines.
- **Responsibilities:** Define quality; version knowledge; model knowledge (objects, graph,
  retrieval); provide decision guides.
- **Owns:** Knowledge objects, decision guides, disciplines/patterns/practices/quality
  attributes, the knowledge model.
- **Never owns:** Project-specific decisions; engineering *process* (that is Control);
  runtime execution; the authority to approve a decision.
- **Primary artifacts:** Canonical knowledge objects; decision guides.
- **Primary outputs:** Retrieved, versioned engineering context.
- **Dependencies:** None upstream (it is the source).
- **Interfaces:** A versioned **knowledge-retrieval interface** (identity + version of every
  object returned).
- **Success criteria:** Any consumer can retrieve versioned knowledge and reconstruct which
  knowledge informed a decision (P8, P9).
- **Challenge:** Distinct beyond doubt — it is the only Plane whose content is
  technology-neutral and project-independent. *Ten-year: yes.*

### 4.2 Control Plane *(constructive)*

- **Mission:** Govern the engineering *process* — turn intent into a validated engineering
  result through defined workflows, tasks, and runtime execution, using Knowledge.
- **Responsibilities:** Classify intent/phase; retrieve context; define and execute
  workflows and tasks; enforce inter-step validation; produce provenance and run records;
  halt at human approval.
- **Owns:** Workflows, tasks, runtime execution contracts, run state, run manifests, task
  provenance, orchestration.
- **Never owns:** The definition of quality (Knowledge); the accepted decision and its
  residual risk (the accountable authority, via Project); its own validation verdict
  (Review, P6); its own release identity (Release).
- **Primary artifacts:** Workflow and task specifications; run records.
- **Primary outputs:** Validated engineering results (e.g., a recommendation) halted at the
  approval boundary; provenance.
- **Dependencies:** Knowledge (via the retrieval interface).
- **Interfaces:** A versioned **workflow/execution interface** (Work Request in →
  validated-result-at-approval out) and a **provenance interface**.
- **Success criteria:** A workflow executes end-to-end, reproducibly, with admissible
  provenance, never ratifying itself and never approving on a human's behalf.
- **Challenge:** Distinct. Note a *sub-boundary* — workflow **definition/planning** vs
  workflow **runtime** — is a capability split (WS-5), **not** a Plane split; both are Control
  responsibilities. *Ten-year: yes.*

### 4.3 Project Plane *(constructive)*

- **Mission:** Adopt the platform within a concrete engineering effort — the boundary where
  governed engineering meets a real codebase.
- **Responsibilities:** Originate Work Requests; carry project-specific decisions and ADRs;
  hold the accepted decision and its accountable owner; consume Control's results.
- **Owns:** Work Requests; project ADRs; project-specific canonical artifacts; the *acceptance*
  of a recommendation.
- **Never owns:** General knowledge (Knowledge); process definitions (Control); the review
  verdict (Review).
- **Primary artifacts:** Work Requests; project decisions/ADRs.
- **Primary outputs:** Accepted engineering decisions; adoption evidence.
- **Dependencies:** Control (workflow/execution interface).
- **Interfaces:** A versioned **consumer interface** (submit Work Request, receive
  validated result, record acceptance) — designed so that **N consumers** attach without
  changing upstream Planes.
- **Success criteria:** A project can run governed engineering end-to-end and later
  reconstruct why each decision was made (the Vision success scene).
- **Challenge:** Distinct — it is the only Plane that is project-specific and instance-plural.
  *Ten-year: yes.*

### 4.4 Review Plane *(cross-cutting)*

- **Mission:** Provide **validation independent of generation** across all constructive
  Planes (P6).
- **Responsibilities:** Evaluate artifacts and decisions; produce review packs and verdicts;
  qualify reviewers; route challenges to disposition (with Governance).
- **Owns:** Review packs, verdicts, reviewer qualification.
- **Never owns:** The artifacts it reviews; their generation; the authority to *produce* what
  it validates.
- **Primary artifacts:** Review packs; recorded verdicts and challenge dispositions.
- **Primary outputs:** Independent validation results.
- **Dependencies:** The *outputs* of the Planes it reviews — **never their generation
  internals** (this independence is the Plane's reason to exist).
- **Interfaces:** A versioned **review interface** (artifact/decision in → verdict +
  recorded challenges out).
- **Success criteria:** No consequential artifact becomes canonical or released without an
  independent verdict; the reviewer is never the sole generator.
- **Challenge:** ECF today realizes review as an internal *layer* (Layer 6: "reviews do not
  create artifacts; they validate them"). Because independence is **constitutional (P6)**, it
  is a genuine Plane by responsibility even while it ships inside the Control repository. It
  may separate into its own deliverable/authority later. *Ten-year: yes — independence is
  timeless.*

### 4.5 Release Plane *(cross-cutting)*

- **Mission:** Guarantee the **reproducible identity and integrity** of what is released
  across all Planes.
- **Responsibilities:** Coordinate multi-repository releases; enforce content-digest identity
  and exact upstream pins; enforce the **non-recursive manifest** rule; record release
  provenance and attestations.
- **Owns:** Release manifests, tags/pins, release attestations.
- **Never owns:** The content it packages; its *own* containing-commit identity (non-recursive
  rule); the decision to change what is released (Governance authorizes; Release effects).
- **Primary artifacts:** Release manifests and attestations.
- **Primary outputs:** Reproducible, verifiable releases.
- **Dependencies:** Versioned outputs of every constructive Plane.
- **Interfaces:** A versioned **release interface** (pinned component set in → attested
  coordinated release out).
- **Success criteria:** Any release can be reconstructed and verified; no manifest asserts its
  own identity; digest checks are content-true (line-ending–robust).
- **Challenge:** Cross-cutting but coherent — release *integrity* is a single ownable
  responsibility with genuine architectural invariants. *Ten-year: yes.*

### 4.6 Reasoning Plane *(future, cross-cutting)*

- **Mission:** Make **engineering judgment itself** versioned, challengeable, and
  evidence-linked over time (addresses Open Question 001).
- **Responsibilities:** First-class assumptions with review triggers; decision-review and
  supersession lifecycles; reasoning migration across tools and models.
- **Owns:** Assumption artifacts; decision-review records; reasoning lifecycle state.
- **Never owns:** The engineering *facts* (Knowledge/Control); the accountable *acceptance*
  (Project/authority).
- **Primary artifacts:** First-class assumptions; decision-review and supersession records.
- **Primary outputs:** Evidence-driven challenges to standing decisions.
- **Dependencies:** Operational Evidence (fuel); the decisions it re-examines.
- **Interfaces:** A versioned **assumption/challenge interface**.
- **Success criteria:** A standing decision can be revisited as an *engineering workflow* when
  an assumption is contradicted — not an archaeological exercise (the Vision success scene).
- **Challenge:** Recognized in the constitution (Open Question 001). Correctly **future** and
  **Research** stability — declaring it built would violate P2. *Ten-year: yes.*

### 4.7 Operational Evidence — *not a Plane (Founder Decision FD-2, Ruled 2026-07-16)*

- **Ruling (Reading B):** Operational Evidence is a **cross-cutting concern**, not a
  distinct constructive Plane. Every artifact of it that exists today is an output of an
  existing Plane's activity; the distinctive class — evidence from outside the platform
  boundary — has count zero at ruling time (P2).
- **What the ruling obliges NOW:** evidence **permanence** is a named Control-owned
  obligation (a permanent record may never cite only a mortal path — the dangling-evidence
  exposure found at ruling time must be closed); evidence **consumption** (review
  triggers, O11) belongs to the Reasoning Plane under FD-4.
- **Re-open trigger (recorded):** external-boundary operational evidence arrives, or ≥2
  independent producers/consumers of operational evidence exist. Either re-opens FD-2 as
  a fresh founder decision; nothing re-opens silently.
- Decision record: `FD2_DECISION_MEMO` (both readings preserved at full strength).

### 4.8 Challenged out — recommended **not** Planes

- **Artifact — *not* a Plane (FD-1, Ratified).**

  > **Artifacts are projections of engineering state, not independent engineering
  > responsibilities.**

  ECF Layer 5 treats "canonical artifact" as an **output type with a single canonical
  representation**, produced by whichever activity owns it. Diagrams, ADRs, reports, schemas,
  and release manifests are all *projections* generated by other responsibilities; none is a
  responsibility in itself. A separate "Artifact Plane" would be a catch-all that violates
  single-ownership by trying to own everyone's outputs. "Canonical artifact" is therefore a
  **platform-wide artifact category** (see §6), and *artifact synchronization/rendering from
  the authoritative model* (P10) is a **Control responsibility**, not a Plane.
- **Accountability — *not* a Plane (FD-3, Ratified; resolves OQ-ARCH-001).** Accountability has
  no distinct state of its own; it *annotates every artifact* with ownership and authority and
  is enforced by every Plane. It is a **cross-cutting governance model** (the five roles,
  answerability), defined in [PLATFORM_GOVERNANCE](PLATFORM_GOVERNANCE.md) and enforced by each
  Plane's ownership rules — **exactly like security, observability, and performance: it
  influences every Plane, but it is not one.**

---

## 5. Cross-Plane Contracts

**The constructive chain and the cross-cutting Planes:**

```
Knowledge ──▶ Control ──▶ Project
                 ▲            │
                 │            ▼
             (validates)  (originates intent / accepts decisions)
Review  ── validates outputs of all constructive Planes (never their internals)
Release ── packages versioned outputs of all constructive Planes (asserts none of its own identity)
Operational Evidence ─▶ Reasoning ─▶ (challenges standing decisions across Planes)   [future]
```

**Allowed interactions.**
- A constructive Plane may consume the **versioned interface output** of the Plane
  immediately upstream (Control←Knowledge; Project←Control).
- Cross-cutting Planes (Review, Release) may consume the **published outputs** of any Plane.
- Reasoning (future) may consume Operational Evidence and the decision records it re-examines.

**Forbidden interactions.**
- Reaching into another Plane's **internals** instead of its versioned interface.
- **Review depending on generation internals** (destroys P6 independence).
- **Any Plane ratifying its own output** (P6) or **asserting its own provenance/release
  identity** (non-recursive rule).
- **Cycles** of any kind (e.g., Knowledge depending on Control).
- Knowledge holding **project-specific** content; Project redefining **general** knowledge.

**Ownership rules.** Exactly one Plane owns each artifact type (§6). Producing an artifact
does not grant ownership of the *authority* over it — generation, validation, and acceptance
are always separable (P6, P7).

**Versioning rules.** Every cross-Plane interface is **versioned and stable, not frozen**
(explicit version, compatibility rules, migration policy). Consumers depend on a *declared
version*. Cross-cutting contract changes (provenance identity, validation, release identity)
require coordinated compatibility/migration review.

**Traceability rules.** Every cross-Plane artifact carries **provenance** (P8): the inputs,
knowledge versions, and process that produced it, sufficient to reconstruct it. Provenance is
**admissibility-enforcing** — an artifact with missing/inconsistent provenance is inadmissible.

---

## 6. Ownership Model

**Every artifact type has exactly one owning Plane.** (P5/P7: an owner is an accountable
*authority*, distinct from author/approver; ownership is transferable while history is
preserved.) Lifecycles follow the governance cycle
([PLATFORM_GOVERNANCE](PLATFORM_GOVERNANCE.md)).

| Artifact type | Owning Plane | Lifecycle | Primary repository | Review authority |
|---|---|---|---|---|
| Knowledge Object | Knowledge | candidate → canonical → superseded (corrigible, P14) | `engineering_kb` | Review Plane (knowledge review) |
| Decision Guide | Knowledge | draft → canonical → superseded | `engineering_kb` | Review Plane |
| Workflow | Control | draft → active → deprecated | `ecf` | Review Plane |
| Task | Control | draft → active → deprecated | `ecf` | Review Plane |
| Runtime State | Control | per-run, immutable once written | `ecf` | n/a (system) |
| Run Manifest | Control | per-run attestation | `ecf` | Review Plane (validation) |
| Reasoning (run/trace) | Control now → **Reasoning Plane** when it exists (FD-4) | per-run | `ecf` | Review Plane |
| Recommendation | Control (produces) → Project (accepts) | proposed → waiting_for_approval → accepted/rejected | `ecf` → `context_switcher` | Review Plane; accountable authority |
| ADR | The Plane making the decision (platform ADRs → Governance) | proposed → accepted → superseded | repo of the decision | Review Plane |
| Diagram | Producing Plane (rendered from its model) — pending FD-1 | generated → validated → regenerated | producing repo | Review Plane |
| Release Manifest | Release | proposed → attested → superseded | all (coordinated) | Review Plane; release authority |
| Experiment | Governance (author until promoted) | experimental → promoted/continued/rejected | originating repo | Review Plane; standards authority |
| Capability | Program Management (WS-0) | planned → in-progress → implemented | `platform` | Program/architecture authority |
| Workstream | Program Management (WS-0) | proposed → active → closed | `platform` | Program authority |
| Platform Principle | Constitution (constitutional authority) | ratified → amended (heaviest tier) | `platform` | Constitutional authority |
| Open Question | Governance (accountable steward) | open → owned → resolved | `platform` | Governance authority |

*(Entries with FD references are provisional pending the Founder Decisions in §10.)*

---

## 7. Architectural Layers

The platform separates five layers by **volatility** — the rate at which each is allowed to
change. Conflating them is what lets short-lived decisions corrupt long-lived ones.

```
Constitution   — what must always be true            (Mission, Vision, Principles, Governance root)   — changes rarely, heaviest tier
      ▼
Architecture   — the stable Planes and contracts      (this document)                                  — changes deliberately (T4)
      ▼
Capability     — what capabilities exist & their maturity (Capability Map, Roadmap)                     — evolves per milestone (T1)
      ▼
Implementation — the code, schemas, runners that realize capabilities (repositories)                    — changes frequently (T0–T2)
      ▼
Operation      — runs, evidence, releases in the world (run records, releases, operational evidence)    — changes continuously
```

**Why the separation.** Each layer may depend downward on stability, never upward on
volatility: implementation may assume architecture is stable; architecture must not bend to an
implementation convenience. This is the same three-layer insight from the constitution
(Constitution / Governance / Roadmap) extended with **Architecture** between Principles and
Roadmap, and **Operation** below Implementation — the two layers the Program Plan showed were
missing. *(Ten-year test: the layer names may endure even as their contents are wholly
replaced.)*

---

## 8. Stability Model

Every architectural element is classified by how much it is allowed to change.

| Stability | Meaning | Elements |
|---|---|---|
| **Constitutional** | Changeable only under the heaviest governance tier | The constructive-Plane set (Knowledge, Control, Project); one-directional acyclic dependency; Review independence (P6); non-recursive release identity; single-owner-per-artifact |
| **Stable** | Deliberate T4 change | Control's workflow/task/runtime contract *shape*; Knowledge object model; Review and Release as cross-cutting Planes; the volatility-layer model |
| **Evolving** | Expected to change per milestone | Cross-Plane interface *versions*; the authoritative engineering-model contract (O10); orchestration capability boundary |
| **Experimental** | Under active trial | First-class assumption lifecycle (O11); durable stewardship (O4) |
| **Research** | Not yet demonstrable | Reasoning Plane; Operational Evidence *(provisional, FD-2)*; lifetime judgment integrity (O12 / Open Question 001) |

---

## 9. Dependency Rules

- **Who may depend on whom.** Constructive chain only, upstream, via versioned interfaces:
  `Control → Knowledge`, `Project → Control`. Cross-cutting Planes (Review, Release) depend on
  *published outputs* of any Plane. Reasoning (future) depends on Operational Evidence and
  decision records.
- **What is forbidden.** Cycles; internal (non-interface) coupling; Review depending on
  generation internals; self-ratification; self-asserted provenance/release identity; Knowledge
  holding project specifics.
- **What crosses repositories.** Only versioned interface outputs and provenance — never
  internals. Cross-repository dependencies are **exact-pinned** at release
  ([PLATFORM_RELEASE_STRATEGY](PLATFORM_RELEASE_STRATEGY.md)).
- **What crosses Planes.** Only the published artifacts and interfaces named in §5, each
  carrying provenance. A Plane boundary crossed without a versioned interface + provenance is
  an architectural violation.

---

## 10. Founder Decisions (Ratified) & Open Architectural Questions

> All six decisions below were ruled by the Founder. Five are ratified; FD-2 is a deliberate
> deferral. From this point, adding or redefining a Plane requires a compelling reason
> grounded in **operational evidence** — the architecture is treated as stabilizing.

- **FD-1 — Is "Artifact" a Plane? — ❌ NO (Ratified).** Artifacts are projections of
  engineering state, not responsibilities. "Canonical artifact" is a platform-wide category;
  synchronization/rendering from the authoritative model is a Control responsibility (P10).
- **FD-2 — Operational Evidence: distinct Plane or input half of Reasoning? — ⏳ DEFER
  (Ratified deferral).** Insufficient evidence (one consumer, one live workflow, one
  experiment). Remains **Research/provisional**; **decide at 0.6** as O11/O12 mature. No
  premature optimization.
- **FD-3 — Is "Accountability" a Plane? (OQ-ARCH-001) — ❌ NO (Ratified).** A cross-cutting
  governance model enforced by every Plane, like security/observability/performance.
  OQ-ARCH-001 is hereby resolved.
- **FD-4 — Interim ownership of Reasoning artifacts — ✅ ACCEPT (Ratified).** Until the
  Reasoning Plane exists: **Control produces → Project accepts**; ownership **transfers to the
  Reasoning Plane** when it is established. Explicit transition, no premature Plane, no fake
  ownership.
- **FD-5 — Constructive / cross-cutting taxonomy — ✅ YES (Ratified).** Adopted platform-wide;
  it explains dependencies, ownership, and evolution in one stroke.
- **FD-6 — Does Review get its own repository/authority? — ❌ NOT YET (Ratified, trigger-based).**
  Review remains inside `ecf` **until an architectural trigger fires: two independent
  consumers, or organizational independence, requires separation.** This is a *trigger*, not a
  version milestone.

**Remaining open questions** (carried, not blocking): FD-2 (Operational Evidence, at 0.6);
Open Question 001 (judgment integrity); OQ-GOV-001/002/003 (governance); the roadmap-view
divergence in [PROGRAM_EXECUTION_PLAN](PROGRAM_EXECUTION_PLAN.md) K5.

**Related open questions carried from other documents:** Open Question 001 (judgment
integrity); OQ-GOV-001/002/003 (genesis authority, anti-capture, change-class ladder); the
roadmap-view divergence (plane-delivery vs obligation sequencing) recorded in
[PROGRAM_EXECUTION_PLAN](PROGRAM_EXECUTION_PLAN.md) K5.

---

## Metadata

| Field | Value |
|---|---|
| Owner | Founder |
| Status | **Ratified (Genesis)** (FD-1, FD-3, FD-4, FD-5, FD-6 ratified; FD-2 deliberately deferred to 0.6) |
| Document Version | 0.1.0 |
| Applies To | AI Engineering Platform (all repositories) |
| Review Cadence | Annual (constitutional); architecture changes are T4 governance acts |

### Decision history
- **0.1.0** — Architecture derived from the constitution and from read-only inspection of
  `engineering_kb`, `ecf`, `context_switcher` (ECF's six-layer framework model; EKB's
  knowledge/technology-neutral charter; ECF review/artifact layer distinction). Established
  "a Plane is a responsibility, not a repository" and the constructive/cross-cutting taxonomy.
  Challenged the suggested eight Planes: kept Knowledge/Control/Project (constructive),
  Review/Release (cross-cutting), Reasoning (future); recommended Artifact and Accountability
  are **not** Planes; marked Operational Evidence provisional. Uncertainties recorded as
  FD-1…FD-6 rather than chosen.
- **0.1.0 ratification** — Founder ruled all six FDs. FD-1 ❌, FD-2 ⏳ (defer to 0.6), FD-3 ❌
  (OQ-ARCH-001 resolved), FD-4 ✅, FD-5 ✅, FD-6 ❌ trigger-based. Elevated "A Plane is a
  responsibility, not a repository" to a ratified constitutional rule (Repositories → Planes →
  Responsibilities) and added "Artifacts are projections of engineering state, not independent
  engineering responsibilities." Architecture declared stabilizing: new/redefined Planes now
  require operational-evidence justification.

### Open questions
- FD-2 (Operational Evidence — decide at 0.6). OQ-ARCH-001 **resolved** (FD-3).

### Cross references
- [PLATFORM_MISSION](PLATFORM_MISSION.md) · [PLATFORM_VISION](PLATFORM_VISION.md) · [PLATFORM_PRINCIPLES](PLATFORM_PRINCIPLES.md) · [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md) · [PLATFORM_GOVERNANCE](PLATFORM_GOVERNANCE.md) · [PLATFORM_CAPABILITY_MAP](PLATFORM_CAPABILITY_MAP.md) · [PLATFORM_WORKSTREAMS](PLATFORM_WORKSTREAMS.md) · [PROGRAM_EXECUTION_PLAN](PROGRAM_EXECUTION_PLAN.md)
