# PLATFORM_WORKSTREAMS

> The units of work that advance the constitutional obligations toward the 1.0 baseline.
> Non-constitutional and revisable. Each workstream traces to one or more obligations in
> [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md); a workstream that serves no obligation is scope
> creep (P13).
>
> **Status: Draft.** *Owner*, *Candidate Claude session*, and *Suggested cadence* fields are
> planning placeholders. They are **not invented** — where a value is not yet decided it is
> marked `TBD (Founder)`. Milestone targets follow the ratified obligation-based roadmap.

---

## WS-1 — Reasoning Workflow Substrate

- **Mission:** Establish the contract-governed path Work Request → intent → phase →
  authoritative context → bounded reasoning, with runner-owned contracts and provenance.
- **Obligations:** O1, O5, O8 (substrate for O11/O12).
- **Repositories:** `ecf` (primary), `engineering_kb` (context), `context_switcher` (consumer).
- **Dependencies:** none blocking; builds on 0.2.0 runtime schemas.
- **Parallelizable?** Foundational for the Reasoning Plane; runs largely first.
- **Owner:** TBD (Founder).
- **Target milestone:** 0.3.
- **Candidate Claude session:** "0.3 reasoning substrate — Work Request execution."
- **Suggested cadence:** TBD (Founder).
- **Blocks:** WS-5 (assumptions) depends on the substrate; WS-2 model contract informs it.

## WS-2 — Authoritative Engineering-Model Contract

- **Mission:** Define the authoritative engineering model as a *versioned, stable* contract
  (version, compatibility rules, migration policy, identity semantics, validation boundary,
  change process) — stable, **not frozen**.
- **Obligations:** O10.
- **Repositories:** `ecf` (primary), `engineering_kb` (identity alignment).
- **Dependencies:** consumes discovery feedback from WS-4 and WS-5 (interface-first).
- **Parallelizable?** Interface discovery may overlap consumers; *implementation
  stabilization must precede dependent stabilization*.
- **Owner:** TBD (Founder).
- **Target milestone:** 0.4.
- **Candidate Claude session:** "0.4 authoritative-model contract."
- **Suggested cadence:** TBD (Founder).
- **Blocks:** WS-4 (canonicalization), WS-5 (assumptions), WS-6 (corrigibility) may not
  *stabilize* against an unversioned model contract.

## WS-3 — Responsibility & Authority Model

- **Mission:** Define the five roles + transfer, vacancy, escalation, succession, and
  institutional-vs-individual authority.
- **Obligations:** O6 (foundation for O4).
- **Repositories:** platform governance (`C:\Dev\platform`), enforced by all repos.
- **Dependencies:** none blocking; ratified principle P7.
- **Parallelizable?** Runs in parallel with WS-2 (different concern); a thin *provisional*
  manual stewardship may be used meanwhile, explicitly marked provisional.
- **Owner:** TBD (Founder).
- **Target milestone:** 0.4.
- **Candidate Claude session:** "0.4 responsibility-and-authority model."
- **Suggested cadence:** TBD (Founder).
- **Blocks:** WS-7 (stewardship automation) may not stabilize before this is accepted.

## WS-4 — Evidence-Based Canonicalization

- **Mission:** Implement the workflow by which knowledge becomes canonical through evidence,
  review, and explicit acceptance.
- **Obligations:** O3 (P3, P4).
- **Repositories:** `engineering_kb` (primary), `ecf` (review packs).
- **Dependencies:** WS-2 model contract (for stabilization); reuses Review Plane.
- **Parallelizable?** Yes, across a narrow versioned interface with WS-7; discovery may
  precede WS-2 acceptance.
- **Owner:** TBD (Founder).
- **Target milestone:** 0.5.
- **Candidate Claude session:** "0.5 canonicalization workflow."
- **Suggested cadence:** TBD (Founder).
- **Blocks:** WS-6 (supersession) may not stabilize before canonicalization semantics are
  accepted.

## WS-7 — Durable Stewardship & Challenge Routing

- **Mission:** Operationalize answerability — route challenges to accountable authorities,
  handle vacancy and succession, record dispositions.
- **Obligations:** O4 (operationalizes O6).
- **Repositories:** platform governance + `ecf` runtime.
- **Dependencies:** WS-3 responsibility model (must be accepted first).
- **Parallelizable?** Yes with WS-4, across a small versioned authority interface; neither
  embeds the other's internal model.
- **Owner:** TBD (Founder).
- **Target milestone:** 0.5.
- **Candidate Claude session:** "0.5 stewardship & challenge routing."
- **Suggested cadence:** TBD (Founder).
- **Blocks:** —

## WS-6 — Corrigibility & Supersession

- **Mission:** Safe supersession of canonical knowledge while preserving history.
- **Obligations:** O7 (P14).
- **Repositories:** `engineering_kb` (primary).
- **Dependencies:** WS-4 canonicalization (accepted lifecycle first).
- **Parallelizable?** Requirements exploration may parallel WS-4; production implementation
  follows accepted canonicalization.
- **Owner:** TBD (Founder).
- **Target milestone:** 0.6.
- **Candidate Claude session:** "0.6 supersession lifecycle."
- **Suggested cadence:** TBD (Founder).
- **Blocks:** —

## WS-5 — First-Class Assumption Lifecycle

- **Mission:** Assumptions as executable artifacts with identity, confidence, evidence, and
  review triggers.
- **Obligations:** O11 (bridge to O12).
- **Repositories:** `ecf` (runtime), `engineering_kb` (assumption knowledge).
- **Dependencies:** WS-2 model contract; WS-1 substrate.
- **Parallelizable?** Research may precede WS-2; stabilization follows the model contract.
- **Owner:** TBD (Founder).
- **Target milestone:** 0.6.
- **Candidate Claude session:** "0.6 assumption lifecycle."
- **Suggested cadence:** TBD (Founder).
- **Blocks:** WS-8 (lifetime integrity) is built on the assumption artifact.

## WS-8 — Lifetime Reasoning Integrity

- **Mission:** Long-term preservation and reconstructability of engineering judgment;
  dependency propagation, invalidation, degraded-reproducibility states, reasoning migration.
- **Obligations:** O12 (Open Question 001).
- **Repositories:** `ecf` + `engineering_kb` (Reasoning Plane).
- **Dependencies:** WS-5 first-class assumptions.
- **Parallelizable?** Research may begin early and may place requirements on WS-5;
  implementation follows.
- **Owner:** TBD (Founder).
- **Target milestone:** 0.7.
- **Candidate Claude session:** "0.7 lifetime reasoning integrity."
- **Suggested cadence:** TBD (Founder).
- **Blocks:** —

## WS-C1 — Provenance (cross-cutting)

- **Mission:** Continuous provenance capture accompanying every capability; admissibility
  enforcement (reject artifacts with missing/inconsistent provenance).
- **Obligations:** O8 (deepen to cross-plane).
- **Repositories:** all three.
- **Parallelizable?** Advances continuously; *contract changes to identity/digest semantics
  require coordinated versioning* across planes.
- **Owner:** TBD (Founder). **Target milestone:** continuous; deepen at 0.8.
- **Suggested cadence:** every milestone.

## WS-C2 — Self-Honesty & Compliance Evidence (cross-cutting)

- **Mission:** Continuous, evidence-backed compliance capture; independent governance gates
  that block unsupported maturity/release claims. The reporting mechanism cannot ratify
  itself (P6).
- **Obligations:** O2.
- **Repositories:** all three + platform governance.
- **Parallelizable?** Runs continuously from 0.3; formal readiness assessment at 0.9.
- **Owner:** TBD (Founder). **Target milestone:** continuous; formal audit at 0.9.
- **Suggested cadence:** every milestone.

---

## Dependency summary

```
WS-1 substrate ──▶ WS-5 assumptions ──▶ WS-8 lifetime integrity
WS-2 model contract ──▶ WS-4, WS-5, WS-6 (stabilization)
WS-3 responsibility ──▶ WS-7 stewardship
WS-4 canonicalization ──▶ WS-6 supersession
WS-C1 provenance, WS-C2 self-honesty ── continuous across all
```

Detailed concurrency status (Green/Yellow/Red) is in
[PLATFORM_PARALLELIZATION](PLATFORM_PARALLELIZATION.md).

---

## Metadata

| Field | Value |
|---|---|
| Owner | Founder |
| Status | **Draft** (owners, sessions, cadences are `TBD (Founder)`) |
| Document Version | 0.1.0 |
| Applies To | AI Engineering Platform (all repositories) |
| Review Cadence | Quarterly |

### Decision history
- **0.1.0** — Workstreams derived from the ratified obligation set and the Workshop 3
  dependency graph. Planning fields left `TBD (Founder)` rather than invented.

### Open questions
- Owners, candidate sessions, and cadences require founder assignment.

### Cross references
- [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md) · [PLATFORM_PARALLELIZATION](PLATFORM_PARALLELIZATION.md) · [PLATFORM_CAPABILITY_MAP](PLATFORM_CAPABILITY_MAP.md)
