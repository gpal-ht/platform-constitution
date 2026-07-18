# PLATFORM_CAPABILITY_MAP

> The platform's capabilities, grouped by **Plane**, each marked with implementation status.
> This document answers *"what capabilities exist to satisfy the constitution?"*
> [PLATFORM_ARCHITECTURE](PLATFORM_ARCHITECTURE.md) is **authoritative** for the Plane set,
> taxonomy, and ownership; this map records capability *status* against it.
>
> **Status: Ratified (synchronized to Architecture).** Statuses are grounded in inspection of
> the platform repositories at released version **0.2.0**; they are claimed at the level
> demonstrated (P2/O2).

**Ratified Plane taxonomy** ([PLATFORM_ARCHITECTURE](PLATFORM_ARCHITECTURE.md) §4, FD-5):
- **Constructive Planes** (produce engineering): **Knowledge** → `engineering_kb`,
  **Control** → `ecf`, **Project** → `context_switcher`.
- **Cross-cutting Planes** (operate across constructive Planes): **Review**, **Release**, and
  (future) **Reasoning** — realized where they exist inside the constructive repositories
  until a separation trigger fires (FD-6).
- **Not a Plane:** **Artifact** — a platform-wide artifact *category*; artifacts are
  projections of engineering state (FD-1). Artifact synchronization/rendering is a **Control**
  responsibility (P10) and appears under Control below.
- **Not a Plane:** **Accountability** — a cross-cutting *governance concern* (FD-3), like
  security/observability/performance; enforced by every Plane, owned by
  [PLATFORM_GOVERNANCE](PLATFORM_GOVERNANCE.md).
- **Deferred:** **Operational Evidence** — provisional/Research; decide at 0.6 (FD-2).

Status legend: **Implemented** · **In Progress** · **Planned** · **Research**.

---

## Knowledge Plane *(constructive)* — `engineering_kb`

| Capability | Status | Evidence (0.2.0) |
|---|---|---|
| Versioned engineering knowledge (identity, history) | Implemented | `VERSION`, `knowledge_model/KNOWLEDGE_OBJECT_STANDARD` |
| Knowledge model (objects, graph, retrieval) | Implemented | `knowledge_model/{KNOWLEDGE_GRAPH_MODEL, ENGINEERING_KNOWLEDGE_RETRIEVAL_MODEL}` |
| Decision guides | Implemented | `knowledge_model/DECISION_GUIDE_MODEL`, `decision_guides/` |
| Concepts, disciplines, patterns, practices, quality attributes | Implemented | corresponding directories |
| Evidence-driven canonicalization workflow (O3) | In Progress | philosophy present; execution engine maturing |
| Automated knowledge lifecycle governance (O9 deepening) | Planned | — |
| Safe supersession preserving history (O7) | Planned | corrigibility principle ratified; mechanism pending |

## Control Plane *(constructive)* — `ecf`

| Capability | Status | Evidence (0.2.0) |
|---|---|---|
| Layered framework (principles → standards → workflows → roles → runtime) | Implemented | `FRAMEWORK_ARCHITECTURE`, `FOUNDATION` |
| Workflow catalog & execution specification | Implemented | `workflows/{WORKFLOW_CATALOG, WORKFLOW_EXECUTION_SPECIFICATION}` |
| Runtime contracts (transaction, run manifest, run state) | Implemented | `runtime_schemas/{RUNTIME_TRANSACTION_CONTRACT, RUN_MANIFEST_SCHEMA, RUN_STATE_SCHEMA}` |
| Intent & phase classification results | Implemented | `runtime_schemas/{ENGINEERING_INTENT_RESULT_SCHEMA, ENGINEERING_PHASE_RESULT_SCHEMA}` |
| Reasoning workflow (recommendation) | In Progress | `workflows/reasoning/WF-REASON-0001` |
| Controlled Work Request → intent → phase → context → reasoning substrate (0.3) | In Progress | 0.3.0-dev line |
| Authoritative engineering-model contract (O10) | Planned | ADR-0001 engineering intermediate representation is a seed |
| Universal generation from authoritative model (O10 deepening) | Planned | — |
| Artifact & diagram standards *(relocated from "Artifact Plane" per FD-1)* | Implemented | `ecf/standards/{ARTIFACT_STANDARD, DIAGRAM_STANDARD}` |
| Artifact generation/projection from engineering model (O10, P10) | In Progress | `ecf/generated/`, `engineering_kb/generated/` |
| Artifact–model synchronization enforcement (O10) | Planned | drift currently relies partly on discipline |

## Project Plane *(constructive)* — `context_switcher`

| Capability | Status | Evidence (0.2.0) |
|---|---|---|
| Platform adoption in a concrete project | Implemented | `PROJECT_ECF_ADOPTION_REPORT`, `work_requests/` |
| Project runtime & acceptance tests | Implemented | `runtime/`, `acceptance_tests/` |
| Modular platform architecture, canonical subsystem model | Implemented | `decisions/ADR-000{2,5}` |
| Event-driven application design | Implemented | `decisions/ADR-0004` |

## Review Plane *(cross-cutting; realized within `ecf` until FD-6 trigger)*

| Capability | Status | Evidence (0.2.0) |
|---|---|---|
| Independent validation via review packs (O5) | Implemented | `ecf/review_packs/{REVIEW_PACKS, REVIEW_PACK_SPECIFICATION}` |
| Universal separation of generation and validation (O5 deepening) | In Progress | extend to every workflow |
| Reviewer registry / qualification (governance) | Planned | see [PLATFORM_GOVERNANCE](PLATFORM_GOVERNANCE.md) reviewer registry |

## Release Plane *(cross-cutting; realized across all three repos)*

| Capability | Status | Evidence (0.2.0) |
|---|---|---|
| Coordinated multi-repo release | Implemented | `context_switcher/PLATFORM_RELEASE_0.2.0` |
| Non-recursive manifest / content-digest identity | Implemented | release-manifest identity model |
| Exact upstream pinning across planes | Implemented | ECF pins EKB commit; CS pins ECF commit |
| Release automation (O8 deepening) | Planned | releases currently validated manually |

## Operational Evidence *(provisional — Research; plane status deferred to 0.6, FD-2)*

| Capability | Status | Evidence (0.2.0) |
|---|---|---|
| Run state capture | Implemented | `ecf/runtime_schemas/RUN_STATE_SCHEMA` |
| Operational reality feeding back to challenge assumptions (O11/O12) | Research | depends on first-class assumptions |
| Evidence-triggered decision review | Research | Open Question 001 |

## Reasoning Plane *(future, cross-cutting)*

| Capability | Status | Evidence (0.2.0) |
|---|---|---|
| Reasoning workflow substrate | In Progress | `WF-REASON-0001`; 0.3 substrate |
| First-class assumption lifecycle (O11) | Planned | opens at 0.6 |
| Lifetime reasoning integrity (O12) | Research | 0.7; Open Question 001 |

---

## Complementary lens — plane-delivery view of the roadmap

The ratified roadmap in [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md) is organized by
**constitutional obligation**. The Platform Constitution Establishment Batch proposed an
alternative organizing principle — **which plane matures when**. Both describe the same
platform; this lens is recorded here so nothing is lost, without overriding the ratified
obligation-based sequence.

| Milestone | Obligation focus *(ratified)* | Plane-delivery emphasis *(complementary)* |
|---|---|---|
| 0.3 | Controlled Reasoning Workflow substrate | Control / Reasoning substrate proven |
| 0.4 | O10, O6 foundations | Control (authoritative model) + governance foundations |
| 0.5 | O3, O4 | Knowledge (canonicalization) + Review/stewardship |
| 0.6 | O7, O11 | Knowledge (corrigibility) + Reasoning (assumptions) |
| 0.7 | O12 | Reasoning (lifetime integrity) |
| 0.8 | deepen O8, O5, O1 | Cross-plane integrity; Operational Evidence begins |
| 0.9 | Constitutional readiness | Release automation + audit |
| 1.0 | Constitutional baseline | AI Engineering Platform |

> Where the two lenses appear to disagree on a milestone's *name*, the obligation-based
> roadmap governs (it is the ratified source of truth). The plane emphasis is guidance for
> sequencing deliverables, not an alternate contract.

---

## Resolved architectural questions

- **OQ-ARCH-001 (accountability as a Plane) — RESOLVED.** Ratified as a cross-cutting
  governance concern, **not** a Plane ([PLATFORM_ARCHITECTURE](PLATFORM_ARCHITECTURE.md) FD-3).
- The only open architectural item is **FD-2** (Operational Evidence as a distinct Plane),
  deliberately deferred to 0.6.

---

## Metadata

| Field | Value |
|---|---|
| Owner | Founder |
| Status | **Ratified (Genesis)** (synchronized to PLATFORM_ARCHITECTURE); statuses grounded at 0.2.0 |
| Document Version | 0.2.0 |
| Applies To | AI Engineering Platform (all repositories) |
| Review Cadence | Quarterly, or on any plane/status change with evidence |

### Decision history
- **0.1.0** — Capability map assembled from read-only inspection of `engineering_kb`, `ecf`,
  and `context_switcher` at 0.2.0, plus the ratified obligation set. Plane taxonomy followed
  the establishment batch's eight-plane grouping, marked Draft.
- **0.2.0 — Reconciled to ratified [PLATFORM_ARCHITECTURE](PLATFORM_ARCHITECTURE.md).** Pure
  synchronization, no new concepts: adopted the constructive/cross-cutting taxonomy (FD-5);
  removed "Artifact Plane" and relocated its capabilities under Control (FD-1); reclassified
  Accountability as a cross-cutting governance concern and removed OQ-ARCH-001 (FD-3, resolved);
  left Operational Evidence as provisional/Research (FD-2); labelled Review/Release cross-cutting
  and noted the FD-6 separation trigger.

### Open questions
- **FD-2** (Operational Evidence as a distinct Plane) — decide at 0.6; status re-grounding each
  time a milestone is released.

### Cross references
- [PLATFORM_ARCHITECTURE](PLATFORM_ARCHITECTURE.md) · [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md) · [PLATFORM_PRINCIPLES](PLATFORM_PRINCIPLES.md) · [PLATFORM_WORKSTREAMS](PLATFORM_WORKSTREAMS.md) · [PLATFORM_GLOSSARY](PLATFORM_GLOSSARY.md)
