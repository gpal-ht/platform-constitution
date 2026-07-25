# AMENDMENT_ECF_SCOPE_LIFECYCLE — ECF scope reconciliation (the Engineering Lifecycle as production spine; the Producer/Governor Boundary)

> **Status: RATIFIED (Founder, Genesis, 2026-07-25) — all 8 checklist items ratified.**
> Disposition **`Ratified (Genesis)`**, carrying the standing Independent Reaffirmation Obligation
> (not claimed as fully `Ratified`; not resting on the non-reusable Genesis Exception). Status ladder:
> `Draft` → `Proposed Amendment` → **`Ratified (Genesis)`** → `Ratified`. Per the
> **Deliberate-Evolution Rule** (PLATFORM_GOVERNANCE §D) this document only *proposed* the change; it
> takes effect on the Founder ratifying act recorded in §8. The §1 artifacts remain unchanged until
> the separate implementation batch — no implementation batch may change scope ahead of this amendment.
>
> **What this reconciles.** Reading of ECF's own ratified corpus (README, `FRAMEWORK_ARCHITECTURE.md`,
> `ECF_ROADMAP.md`) surfaced that **three different definitions of what ECF is** are now in force and
> have drifted apart (§4). This amendment does not invent a new direction; it makes an explicit,
> ratifiable choice among the three and draws the boundary lines the corpus currently leaves implicit.
>
> **Plane:** Governance / Framework Scope. **Empowered authority:** Founder, under the Genesis
> Authority Doctrine. **Disposition target:** `Ratified (Genesis)`, carrying the standing Independent
> Reaffirmation Obligation. Authored 2026-07-25.

---

## 0. Why this is an amendment, and what band it sits in

ECF's scope is currently stated across three documents that no single ratifying act ever reconciled:
the README's purpose, `FRAMEWORK_ARCHITECTURE.md`'s Work Request Lifecycle, and `ECF_ROADMAP.md`'s
version goals and non-goals. Each is individually ratified; **together they under-determine what ECF
produces and where its boundary lies** — exactly the kind of under-determination the O6 amendment
addressed for P7.

The change class is judged **T4 — Framework Scope / Mission**, one band below the entrenched
constitutional core (it does not alter P1–P14 or an obligation definition), but above a T3
governance-mechanism change (it fixes what the framework *is for* and *may do*, and it promotes an
existing roadmap non-goal into a standing doctrine). One clause — the **Producer/Governor Boundary**
(§5, Clause 2) — is doctrine-level and could be argued into the T5 band; the Founder makes the final
classification, and that classification is itself part of the Genesis classification debt folded into
the Reaffirmation Obligation. **Honest position (P2):** because no independent Change Classification
Authority yet exists, this amendment cannot reach full `Ratified`; it binds as `Ratified (Genesis)`.

---

## 1. Scope & authority

| Field | Value |
|---|---|
| **Artifacts to change** | `ecf/ECF_ROADMAP.md` (scope + 2.0 definition); `ecf/README.md` (Purpose — add the lifecycle framing + boundary); `PLATFORM_MISSION.md` (identity); add this doctrine to the governance record |
| **Change class (Axis 1)** | **T4 — Framework Scope / Mission** (Clause 2 is T5-adjacent; see §0) |
| **Effect overlays (Axis 2)** | **E1 fires** (Founder is both proposer and ratifier) → mitigated by the Reaffirmation Obligation. **E2 does not fire** — this *strengthens* a boundary (adds the Producer/Governor rule), it removes no safeguard. **E3 does not fire** — no legitimacy condition is weakened. |
| **Empowered authority** | Founder, under the Genesis Authority Doctrine (End-of-Genesis condition not met — no second human constitutional authority exists) |
| **Classifier** | Founder (Genesis; no independent Change Classification Authority available) |
| **Disposition target** | **`Ratified (Genesis)`**, carrying the Independent Reaffirmation Obligation. **Not** claimed as fully `Ratified`; **not** resting on the non-reusable Genesis Exception. |

---

## 2. The material this is grounded in (probed, not assumed)

Direct quotations from the ratified corpus, read 2026-07-25:

- **README — Purpose / Why ECF:** *"ECF exists to improve decision quality **before implementation
  begins**."* Objective is software that is *understandable, maintainable, testable, secure,
  accessible, explainable.* ECF standardizes *principles, workflows, activities, artifacts, review
  processes, quality gates, AI participation.*
- **`FRAMEWORK_ARCHITECTURE.md` — Work Request Lifecycle:** `Work Request → Workflow Selection →
  Engineering Activities → Canonical Artifacts → Engineering Reviews → Artifact Rendering → Quality
  Gates → Implementation → Verification → Knowledge Capture.` *"Every stage produces reusable
  engineering knowledge."* Layer-4 Activities include *Requirements Analysis, Product Design, System
  Design, Runtime Design.*
- **`ECF_ROADMAP.md` — Version 0.1 Explicit Non-Goals:** *AI orchestration; Automation; CLI tooling;
  **Code generation**; IDE integration.* Roadmap philosophy: *"Framework before tooling — Tools
  implement ECF."*
- **`ECF_ROADMAP.md` — Version 1.0 "Stable Framework":** deliverables are *Stable specifications,
  standards, workflows, templates; Adoption guide; Migration guide; Reference implementations; Sample
  projects; Adoption playbook.*

Two structural facts follow directly and are load-bearing below: (a) ECF's lifecycle **begins at the
Work Request**, not at product ideation; (b) ECF's lifecycle already separates **Canonical Artifacts**
from **Artifact Rendering** — the authoritative artifact is distinct from the rendered document.

---

## 3. The three divergences between the Lifecycle model and the ratified corpus

The proposed Engineering Lifecycle (IDEA → Product Discovery → Product Requirements → Engineering
Discovery → Engineering Analysis → Engineering Design → Implementation Planning → Implementation →
Validation → Release → Operations → Learning) aligns with ECF's documented Work Request Lifecycle
through the **engineering core** — Discovery, Analysis, Design, Planning, Reviews, Quality Gates,
Knowledge Capture are ECF's own model nearly verbatim. It diverges at exactly three points:

- **D1 — Product front-end (IDEA, Product Discovery, Product Requirements/business goals).** ECF's
  lifecycle starts at the Work Request; product strategy and business goals are upstream. *In-scope
  today:* Requirements Analysis and Product **Design** (Layer 4). *Out of scope today:* product
  **discovery**, business strategy, "Business Review."
- **D2 — Implementation.** Present in ECF's lifecycle as a governed/verified stage — but **Code
  generation is a ratified non-goal**, and the value claim is *"before implementation begins."* ECF
  **verifies** implementation against approved artifacts; it does not **author** code.
- **D3 — Operations.** ECF's documented lifecycle **ends at Knowledge Capture**. There is no
  Operations/runtime-telemetry stage. Incident reports, reliability metrics, and customer feedback are
  external real-world signal, not ECF-produced artifacts. (One exploratory "Operational Evidence
  plane" memo exists; it is not part of the ratified core lifecycle.)

---

## 4. The reconception being ratified (name it, don't smuggle it)

Three definitions of ECF are currently in force:

1. **Specification framework** (`ECF_ROADMAP` 1.0 "Stable Framework"): a reusable set of specs,
   standards, templates, and reference implementations that *other teams adopt.*
2. **Constitutional governance baseline** (the 1.0 actually shipped): the 12 obligations at ≥ Partial,
   self-consistent and independently audited.
3. **Full-lifecycle document-production engine** (the direction of this amendment): ECF itself
   *produces* the engineering documents across the lifecycle, gated by reviews, traced to canonical
   sources.

These are different products. This amendment **elects definition 3 as ECF's forward identity**, while
preserving definition 2 as the meaning of the shipped 1.0 tag (unchanged, per Founder direction) and
retaining definition 1's assets (specs/standards/templates) as the *contracts* the production engine
renders against. **This is a reconception, not a restatement** — which is precisely why it must be an
explicit, ratified amendment rather than an assumption baked into a roadmap edit.

---

## 5. The amended scope — clauses

**Clause 1 — The Engineering Lifecycle is ECF's production spine.** ECF organizes all document
production as a review-gated lifecycle whose engineering core is: *Engineering Discovery → Engineering
Analysis → Engineering Design → Implementation Planning → (Implementation) → Validation → Release →
(Operations) → Learning.* Each stage produces canonical artifacts; each transition is guarded by
named reviews and quality gates; every stage feeds the one Engineering Decision Ledger. Stages are
**states in the Ledger, not stations on a one-way conveyor** — a failed downstream review fires a
review-trigger that reopens the relevant upstream decision (reusing supersession + assumption-review
machinery already built).

**Clause 2 — The Producer/Governor Boundary (standing doctrine).** For every lifecycle stage, ECF's
role is exactly one of:
- **Produce** — ECF authors the artifact from canonical sources: *Engineering Discovery, Engineering
  Analysis, Engineering Design, Implementation Planning, Validation reporting, Release documentation,
  Learning.*
- **Govern, not author** — ECF orchestrates, reviews, gates, and attaches provenance, but does **not**
  author the artifact, which originates outside ECF: **Implementation** (source code, tests — authored
  by human/AI executors; *Code generation remains a non-goal, here promoted from roadmap non-goal to
  standing doctrine*) and **Operations** (incident/telemetry/feedback — real-world signal, ingested
  not generated).

No stage may claim "ECF produces X" where ECF only governs X. Counting a governed-not-authored artifact
as produced capability is prohibited (this is the specific error that inflated the 1.0 label).

**Clause 3 — The product front-end is out of scope.** IDEA, Product Discovery, business strategy, and
"Business Review" belong to the consumer/product plane, not ECF. ECF's intake remains the **Work
Request**. Requirements Analysis and Product Design remain in scope (Layer 4); product *discovery* does
not. ECF *consumes* product inputs; it does not *produce* them.

**Clause 4 — Canonical-vs-Rendered rule (affirmed, not new).** ECF's existing *Canonical Artifacts →
Artifact Rendering* separation is the authoritative model: a small set of **canonical** artifacts hold
truth; every other document is a **rendering** (projection) of them. **Zero parallel sources of
truth**; no rendered document is ever hand-edited. A document type counts as delivered only when it is
either canonical or a live projection of a canonical source.

**Clause 5 — Version semantics.** The shipped **1.0 stays** as the Constitutional Baseline (unchanged).
**2.0 is redefined** as *lifecycle-production coverage*: every document type in the ratified taxonomy is
either produced (Clause 2 "produce" stages) or governed end-to-end (Clause 2 "govern" stages), with
100% derivation integrity (Clause 4) and the reliability floor met. Progress is measured as delivered
capability, never as governance-machinery completeness.

---

## 6. What explicitly does NOT change (P2 — reduces no safeguard)

- **No obligation (O1–O12) or principle (P1–P14) is altered.** This is scope/mission, not the core.
- **The "Code generation" non-goal is preserved** — in fact strengthened into Clause 2's doctrine.
- **The Work Request intake is preserved.** ECF does not become a product-management tool.
- **The Deliberate-Evolution Rule is honored:** this document proposes; only Founder ratification (§8)
  binds it.
- **No safeguard is removed;** Clauses 2 and 4 *add* boundaries. Per the Anti-Capture reading this is
  oversight-strengthening, so E2 does not fire.

---

## 7. Effect overlays, risks, and the honest caveat

- **E1 (Founder is proposer and ratifier).** Mitigated only by the standing Reaffirmation Obligation;
  under Genesis this remains single-actor. Recorded, not resolved.
- **Scope-expansion risk — re-committing the over-build.** Electing the production-engine identity
  authorizes a large build. The guard is Clause 5's capability metric + the roadmap's **real-case
  rule** (a type counts only when a genuine document has flowed through it): the amendment expands the
  *target*, not permission to build machinery ahead of content.
- **Boundary-erosion risk.** Over time there will be pressure to let ECF "just generate the code" or
  "just track the incidents." Clause 2 is the fixed line; moving it is itself a future amendment, never
  a batch decision.

---

## 8. Disposition & ratification checklist

Ratification is the Founder marking each item. **All 8 ratified by the Founder (Genesis) on 2026-07-25.**

- [x] **C1** — The Engineering Lifecycle is adopted as ECF's production spine (stages as states, not a conveyor).
- [x] **C2** — The Producer/Governor Boundary is adopted as standing doctrine (produce vs govern-not-author; Implementation and Operations are govern-not-author; Code generation remains prohibited).
- [x] **C3** — The product front-end (ideation/business strategy) is confirmed out of scope; intake remains the Work Request.
- [x] **C4** — The Canonical-vs-Rendered rule is affirmed (zero parallel sources of truth).
- [x] **C5** — 1.0 stays as the Constitutional Baseline; 2.0 is redefined as lifecycle-production coverage.
- [x] **C6** — Artifacts in §1 are updated to reflect C1–C5.
- [x] **C7** — Change class accepted as **T4** (with C2 noted as T5-adjacent), disposition **`Ratified (Genesis)`**.
- [x] **C8** — This amendment is folded into the one outstanding Independent Reaffirmation cycle.

**Disposition recorded (2026-07-25).** Status has advanced `Draft → Proposed Amendment → Ratified
(Genesis)`. The formal Engineering Decision Ledger entry (`decision_class: governance`) is **deferred
to the EDR→Ledger generalization (roadmap Phase 0)**, where this amendment is a designated backfill
entry; until then, **this ratified document plus its git-commit attestation is the decision record**
(Genesis attestation model). The §1 artifacts (`ECF_ROADMAP`, README, `PLATFORM_MISSION`) remain
**unedited** and are changed only in a separate implementation batch, which may not itself change
scope (Deliberate-Evolution Rule).

---

## Metadata

| Field | Value |
|---|---|
| Derives from | README Purpose; `FRAMEWORK_ARCHITECTURE.md` (Work Request Lifecycle, Layer 4); `ECF_ROADMAP.md` (non-goals, 1.0/2.0); Deliberate-Evolution Rule; Genesis Authority Doctrine; the ratified document taxonomy + capability roadmap |
| Change class | T4 — Framework Scope / Mission (C2 T5-adjacent) |
| Disposition target | `Ratified (Genesis)` + Independent Reaffirmation Obligation |
| Review triggers | End-of-Genesis (independent reaffirmation); first pressure to move the Producer/Governor Boundary; first 2.0 coverage report |
| Authored | 2026-07-25, Founder (Genesis) |
| Ratified | 2026-07-25, Founder (Genesis) — `Ratified (Genesis)`, all 8 checklist items; Ledger backfill pending Phase 0 |
