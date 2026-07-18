# PROPOSAL — A1: Authoritative Engineering-Model Contract (DRAFT)

> **Status: PROPOSED (draft for founder ratification).** This is the draft of deliverable **A1**
> from [PROGRAM_0.4](PROGRAM_0.4.md) Track A. It specifies the contract for the **authoritative
> engineering model**. It is not ratified and carries no force until the founder accepts it.
> On ratification the normative body is destined for `engineering_kb/foundations/` (see
> [PROPOSAL_O10_SCOPE](PROPOSAL_O10_SCOPE.md) design-open (c)). Traces to **P10 / O10**.

**Subject of the contract (per scope proposal, PROPOSED):** the **EKB knowledge model** — the graph
of Knowledge Objects defined in `engineering_kb`, made executable by `engine/ekb.py`. The contract is
written to survive a future transition to ADR-0001's Engineering Intermediate Representation (EIR),
which is named as the deferred convergence target, not the current subject.

**What "authoritative" means here.** The model is the single source of truth; every `generated/`
artifact is a **projection** of it and has no independent authority (FD-1: artifacts are projections
of engineering state). When a projection disagrees with the model, the **model wins** and the
projection is stale by definition.

---

## The six required elements

### 1. Version

- **Model-instance identity:** each Knowledge Object carries `version:` (semver) in its front matter,
  per `knowledge_model/KNOWLEDGE_OBJECT_STANDARD.md`. Major = breaking conceptual change; minor =
  meaningful content expansion; patch = correction/editorial.
- **Model-standard version:** the contract itself and the executable validation semantics are versioned.
  The engine already stamps `GENERATOR_VERSION` (currently `0.2.0`) into every generated report; the
  repo carries a top-level `VERSION` (currently `0.2.1`).
- **PROPOSED rule:** the authoritative model has **two** version axes — *per-object* (semver in
  front matter) and *model-standard* (the contract + `GENERATOR_VERSION`). A projection must record
  both the objects it drew from and the generator version that produced it, so drift is attributable.
- *Open choice for founder:* keep two separate axes (recommended — they change for different reasons),
  or fold object versions into a single model-wide version (simpler, but loses per-object granularity).

### 2. Compatibility rules

- **Backward-compatible (minor/patch):** content expansion, editorial fixes, adding a new object, or
  adding an *optional* relationship edge. Existing projections remain valid **iff** their declared
  closure still equals the recomputed closure.
- **Breaking (major):** removing/renaming an object ID, changing an object `type`, removing a
  relationship that alters a retrieval closure, or changing a canonical `type`-string (as in
  MIGRATION-0002, which was explicitly *not* backward-compatible at the type-string level).
- **PROPOSED rule:** *identity-affecting or closure-affecting* changes are breaking and require a
  migration (element 3); everything else is non-breaking. The drift check (A2) is the mechanical
  arbiter of "closure-affecting."
- *Open choice for founder:* do we treat adding an optional back-edge as always non-breaking, or as
  breaking when it changes a closure? (Recommendation: judge by closure effect, not edge category.)

### 3. Migration policy

- **Precedent exists and works:** `migrations/MIGRATION-000X-*.md` already record breaking changes with
  a *supersedes* banner, an old-vs-new representation table, validation behavior, compatibility
  expectations, and downstream (ECF bundle) impact. MIGRATION-0002 is a complete worked example.
- **PROPOSED rule:** every breaking change (element 2) ships with a `migrations/MIGRATION-NNNN-*.md`
  that (a) preserves history (never rewrites it — **P14 corrigibility**), (b) states old→new, (c)
  states validation behavior after migration, and (d) lists downstream consumers to refresh. The
  engine enforces the *result* (e.g., legacy `type` tokens are rejected), not the prose.
- *Open choice for founder:* should a migration be **blocking** (release cannot proceed until named
  downstream bundles are refreshed) or **advisory** (as today — "action required before next
  cross-repo experiment")? Recommendation: advisory for Partial, blocking is a deepening step.

### 4. Identity semantics

- **Stable IDs:** every object has a stable ID (`<TYPE>-<DOMAIN>-<NUMBER>`) that **does not change**
  when files are renamed or moved; the file name is not the identity. ID prefix must match type
  (`DG/CON/PAT/QA/EX/REF`) — enforced by `validate_object`.
- **PROPOSED rule:** identity = the front-matter `id`. Renames/moves preserve identity; an ID may be
  *retired via migration* but never silently reused for a different object. Projections reference
  objects by ID, never by path.
- *Open choice for founder:* do retired IDs become permanently reserved (recommended — prevents
  identity collisions across history), or may they be reused after a deprecation window?

### 5. Validation boundary

- **The boundary is `engine/ekb.py`.** It is the single executable authority that decides whether a
  model instance is well-formed and whether a projection is synchronized. Specifically:
  `validate` (per-object metadata + relationship policy REL001–REL007), `integrity` (types, orphans,
  cycles), `retrieve` + sufficiency gate, and `packages` (projection ↔ model drift).
- **PROPOSED rule:** "valid" and "synchronized" mean *exactly what the engine computes* — no
  document, reviewer, or projection may assert validity the engine does not confirm (P6: validation
  independent of generation; the engine is not the generator of the knowledge). "File exists" is
  explicitly **not** sufficiency.
- *Open choice for founder:* is the engine the **sole** validation boundary, or one of several
  (e.g., a future reviewer sign-off layered on top)? Recommendation: sole *mechanical* boundary for
  Partial; human review is governance, layered later.

### 6. Change process

- **PROPOSED flow:** (1) propose change → (2) if breaking, author a migration → (3) update the model
  objects/standard → (4) update `engine/ekb.py` semantics if the rule is mechanical → (5) update tests
  → (6) run `validate`/`integrity`/`packages` green → (7) regenerate affected projections (never
  hand-edit them) → (8) record in the migration's decision history. This mirrors exactly what
  MIGRATION-0002's "Affected Files" table already did.
- **PROPOSED rule:** projections are **regenerated, never hand-edited**; a hand-edit that diverges
  from the closure is caught as drift by A2. Canonical model changes go through review (P3: nothing
  canonical by existence).
- *Open choice for founder:* who ratifies a model change for Partial — the model owner (`owner:
  engineering_kb`) alone, or a second independent reviewer (P6)? Recommendation: second reviewer for
  *breaking* changes only, self-review acceptable for patch, for Partial.

---

## What is already true vs what ratification adds

| Element | Already present in EKB | What A1 ratification adds |
|---|---|---|
| Version | per-object semver; `GENERATOR_VERSION`; `VERSION` | names the two axes as contract; requires projections to record both |
| Compatibility | implicit in migrations | explicit breaking/non-breaking rule keyed to closure effect |
| Migration policy | MIGRATION-000X precedent | makes the migration template a required, named obligation |
| Identity | stable IDs, prefix rule enforced | retired-ID reservation rule; "reference by ID only" |
| Validation boundary | `engine/ekb.py` | declares the engine the *sole mechanical authority* |
| Change process | MIGRATION-0002 worked example | codifies the 8-step flow; "regenerate never hand-edit" |

**Net:** A1 is mostly *consolidation and ratification* of practice that already exists, plus a few new
rules (closure-keyed compatibility, retired-ID reservation, projections-record-both-versions). This is
consistent with the Partial bar and with P13 (no new governance beyond what earns its place).

---

## Open questions carried to the founder
1. Two version axes vs one? (Recommendation: two.)
2. Migration blocking vs advisory for Partial? (Recommendation: advisory.)
3. Retired IDs permanently reserved? (Recommendation: yes.)
4. Engine as sole mechanical validation boundary for Partial? (Recommendation: yes.)
5. Second-reviewer requirement scope? (Recommendation: breaking changes only.)

## Metadata
| Field | Value |
|---|---|
| Owner (draft) | Track A owner (O10) |
| Status | **PROPOSED** — draft of A1, awaiting ratification |
| Destined home (on ratification) | `engineering_kb/foundations/AUTHORITATIVE_MODEL_CONTRACT.md` |
| Change class | T1 Operational (the model change process it defines may gate T-classes later) |
| Cross references | [PROPOSAL_O10_SCOPE](PROPOSAL_O10_SCOPE.md) · [PROPOSAL_O10_A2_DRIFT_CHECK](PROPOSAL_O10_A2_DRIFT_CHECK.md) · `engineering_kb/knowledge_model/KNOWLEDGE_OBJECT_STANDARD.md` · `engineering_kb/foundations/KNOWLEDGE_RELATIONSHIP_MODEL.md` |
