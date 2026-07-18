# PLATFORM_GLOSSARY

> Canonical definitions for the platform. Every repository and every future document must
> use these terms with these meanings. **No duplicate definitions** — if a term is defined
> here, other documents reference it rather than redefining it.
>
> Terms drawn from ratified workshop outputs are marked *Ratified*. Terms drawn from the
> current repositories, describing existing mechanisms, are marked *Descriptive (0.2.0)* —
> they record present practice and are subject to normal governance. Where a term names a
> not-yet-ratified structure, it is marked *Draft*.

---

## Constitutional terms

**Unverifiable engineering** *(Ratified)* — Engineering output that may be correct but
cannot be trusted, because its knowledge, reasoning, decisions, or evidence cannot be
understood, challenged, or reproduced. The condition the platform exists to end.

**Engineering control plane** *(Ratified)* — The system that lets humans and machines
engineer from shared knowledge, defined workflows, traceable evidence, explicit authority,
independent review, and durable artifacts. (Distinct from the "Control Plane" repository
role; see below.)

**Governed engineering** *(Ratified)* — The platform's identity: engineering treated as a
governed system of knowledge, reasoning, evidence, review, decision, execution, and
learning — not as a sequence of prompts, documents, or code changes.

**The Root Principle** *(Ratified)* — *Engineering decisions must remain intelligible,
challengeable, and reproducible throughout their lifetime.* See
[PLATFORM_PRINCIPLES](PLATFORM_PRINCIPLES.md).

**Intelligible / Challengeable / Reproducible** *(Ratified)* — The three pillars of the
Root Principle. Intelligible: can be understood. Challengeable: can be questioned,
contested, reconsidered. Reproducible: can be reconstructed and re-evaluated.

**Aspirational invariant** *(Ratified)* — A standard the platform is designed and measured
against, which it does not yet fully satisfy. Gaps are recorded as obligations, never used
to weaken the standard. (Root Principle Clarification A.)

**Answerability** *(Ratified)* — The requirement that a challenge reach an accountable
authority and receive a recorded disposition. Challengeability is not real without it.
(Clarification B; principle P5.)

**The five roles of accountability** *(Ratified)* — **Authorship** (produced the decision),
**approval** (authorized it at a point in time), **ownership** (currently maintains it),
**accountability** (must answer for continued validity), **responsibility acceptance**
(consciously accepts residual risk). Distinct and transferable.

**Individual authority** *(Ratified)* — authority held by a specific actor at a specific time;
it can become vacant when the actor departs, is revoked, or cannot act.

**Institutional authority** *(Ratified)* — the standing authority of an office/role itself,
which persists across individual holders and is never vacant by construction; under the current
constitutional order it rests ultimately with the Founder (Genesis) when no individual holds it.
(Constitutional basis: PLATFORM_PRINCIPLES Clarification C; PLATFORM_GOVERNANCE Doctrine E.6.)

**Corrigibility** *(Ratified)* — The property that canonical knowledge can be superseded by
better evidence without denying its historical existence. *History is preserved; truth is
revised.* (Principle P14.)

**Forcing function (execution, not discipline)** *(Ratified)* — The property that engineering
artifacts stay current because they participate in execution: if they drift from their
authoritative model, execution breaks. (Principle P10.)

**First-class assumption** *(Ratified)* — An assumption recorded as an artifact with
identity, confidence, evidence, and a review trigger, so that reality can challenge it.
(Principle P11.)

**Engineer's future self** *(Ratified)* — The platform's truest beneficiary: the person who
must understand, reproduce, and trust a decision months or years after it was made.

## Governance terms

**Root Governance Primitive** *(Ratified)* — The single governance cycle: *scope & authority
→ proposal → evidence → independent challenge → authorized disposition → versioned effect →
monitored reconsideration.* See [PLATFORM_GOVERNANCE](PLATFORM_GOVERNANCE.md).

**Authorized disposition** *(Ratified)* — The recorded outcome of a governance act by an
accountable authority: accepted, accepted with constraints, accepted experimentally,
deferred, rejected, superseded, withdrawn, expired, or reaffirmed.

**Monitored reconsideration** *(Ratified)* — The standing final stage of the cycle: recorded
conditions and triggers under which a decision must re-enter the cycle. The operational
form of corrigibility.

**Governance admission test** *(Ratified)* — A proposed mechanism is admitted only if it
names which cycle stage it instantiates or strengthens and shows measurable constitutional
benefit; otherwise P13 presumes it unnecessary.

**Change class / tier** *(Draft)* — The category of an authoritative change, used at Stage 1
to route evidence threshold and authority. Draft ladder T0–T5 in
[PLATFORM_GOVERNANCE](PLATFORM_GOVERNANCE.md).

**Canonical** *(Ratified)* — Having achieved authoritative status through evidence, review,
and explicit acceptance. Nothing is canonical merely by existing (P3).

## Platform structure terms

**Plane** *(Ratified)* — A long-lived architectural **responsibility** of the platform with
distinct responsibility, explicit interfaces, and an independent lifecycle. **A Plane is a
responsibility, not a repository** (Repositories implement Planes; Planes implement
Responsibilities). Planes are **constructive** or **cross-cutting**. Authoritative source:
[PLATFORM_ARCHITECTURE](PLATFORM_ARCHITECTURE.md) §4.

**Knowledge Plane** *(constructive)* — The responsibility of governed, versioned engineering
knowledge. Current deliverable: `engineering_kb`.

**Control Plane** *(constructive)* — The responsibility of controlled, contract-governed
engineering execution — including artifact synchronization/rendering from the authoritative
model (P10). Current deliverable: `ecf` (Engineering Control Framework).

**Project Plane** *(constructive)* — The responsibility of adopting the platform within a
concrete project. Current deliverable: `context_switcher`.

**Review Plane** *(cross-cutting)* — The responsibility of independent validation of
engineering work (e.g., ECF review packs); realized within `ecf` until the FD-6 separation
trigger.

**Artifact** *(not a Plane — FD-1)* — A platform-wide artifact **category**. Artifacts
(diagrams, ADRs, reports, schemas, manifests) are **projections of engineering state, not
independent responsibilities**. Their synchronization/rendering is a Control responsibility.

**Release Plane** *(cross-cutting)* — The responsibility of coordinated, reproducible release
engineering across repositories. See [PLATFORM_RELEASE_STRATEGY](PLATFORM_RELEASE_STRATEGY.md).

**Operational Evidence** *(provisional — Research; FD-2)* — The capability by which
operational reality feeds evidence back to challenge assumptions and decisions. Whether it is
a distinct Plane is deferred to 0.6.

**Accountability** *(not a Plane — FD-3)* — A cross-cutting **governance concern** (the five
roles, answerability), enforced by every Plane like security/observability/performance. Owned
by [PLATFORM_GOVERNANCE](PLATFORM_GOVERNANCE.md), not a Plane.

**Reasoning Plane** *(future, cross-cutting)* — The responsibility by which engineering
judgment itself becomes versioned, challengeable, and evidence-linked over time. Addresses
Open Question 001. The substrate is emerging (0.3); the assumption lifecycle opens at 0.6.

**Constitutional obligation (O1–O12)** *(Ratified)* — A requirement derived from a principle,
used as a roadmap row and a maturity-tracking unit. See
[PLATFORM_ROADMAP](PLATFORM_ROADMAP.md).

**Maturity (None / Emerging / Partial / Strong)** *(Ratified)* — The scale for how fully an
obligation is implemented. 1.0 requires every obligation ≥ Partial.

**Workstream** *(Draft)* — A coherent unit of work advancing one or more obligations. See
[PLATFORM_WORKSTREAMS](PLATFORM_WORKSTREAMS.md).

## Repository / runtime terms *(Descriptive 0.2.0)*

**ECF (Engineering Control Framework)** — The Control-Plane framework (`ecf`) defining
principles, standards, workflows, roles, and runtime contracts for governed execution.

**EKB (Engineering Knowledge Base)** — The Knowledge-Plane repository (`engineering_kb`):
knowledge model, concepts, disciplines, patterns, practices, standards.

**Work Request** — The entry unit of an engineering workflow; the thing that enters intent
and phase classification.

**Runtime transaction contract / Run manifest / Task provenance** — ECF runtime schemas that
make execution reproducible and provenance-bearing (`ecf/runtime_schemas`).

**Non-recursive manifest** — The release rule that a committed manifest never asserts its own
containing commit; release-content identity is a content digest / exact upstream pins, with
`git_commit` treated as best-effort provenance excluded from equality/drift checks. See
[PLATFORM_RELEASE_STRATEGY](PLATFORM_RELEASE_STRATEGY.md).

---

## Metadata

| Field | Value |
|---|---|
| Owner | Founder |
| Status | Ratified (Genesis) (constitutional terms) · Descriptive/Draft (structure & repository terms) |
| Document Version | 0.3.0 |
| Applies To | AI Engineering Platform (all repositories) |
| Review Cadence | Annual (constitutional terms); on definition change (others) |

### Decision history
- **0.3.0** — Amended by AMENDMENT_O6 (T5, Ratified Genesis 2026-07-15): added two constitutional
  terms — *individual authority* and *institutional authority* (basis: PLATFORM_PRINCIPLES
  Clarification C; PLATFORM_GOVERNANCE Doctrine E.6). Ratified (Genesis), folded into the
  Independent Reaffirmation Obligation.
- **0.1.0** — Constitutional and governance terms captured from ratified Workshops 1–4.
  Structure and repository terms captured descriptively from platform repositories at 0.2.0.
- **0.2.0 — Constitutional Consistency Pass.** Synchronized structure terms to ratified
  [PLATFORM_ARCHITECTURE](PLATFORM_ARCHITECTURE.md): Plane defined as a responsibility (not a
  repository); constructive/cross-cutting labels applied (FD-5); "Artifact Plane" → "Artifact"
  category (FD-1); added "Accountability" as a governance concern (FD-3); "Operational
  Evidence" marked provisional (FD-2).

### Open questions
- **FD-2** — whether Operational Evidence is a distinct Plane; deferred to 0.6.

### Cross references
- [PLATFORM_ARCHITECTURE](PLATFORM_ARCHITECTURE.md) · [PLATFORM_PRINCIPLES](PLATFORM_PRINCIPLES.md) · [PLATFORM_GOVERNANCE](PLATFORM_GOVERNANCE.md) · [PLATFORM_CAPABILITY_MAP](PLATFORM_CAPABILITY_MAP.md) · [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md)
