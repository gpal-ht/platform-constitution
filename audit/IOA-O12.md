# IOA-O12 — Independent Obligation Assessment

| Field | Value |
|---|---|
| obligation_id | **O12** — Lifetime reproducibility of engineering judgment (the *"throughout their lifetime"* clause; Open Question OQ-001) |
| principle | **P-Root** (REPRODUCIBLE pillar) + Clarification A (aspirational invariant; known gaps recorded, never concealed); served by P8, P9, P7, P14, P2 |
| assessor | Independent auditor (0.9 Constitutional Readiness audit). **assessor ≠ builder**: I did not design or implement the reasoning-model attestation, the reproducibility-state contract, the assumption-dependency resolver, or the propagator. Every finding below was re-derived by reading primary evidence and running the tools against the **real** store. |
| roadmap baseline | Emerging (PLATFORM_ROADMAP 0.7.0 row) → claimed **Partial** at 0.7 (honestly, under the O12A-5 honesty rule) |

## clause_under_test (quoted)

Root Principle, PLATFORM_PRINCIPLES.md:

> "Engineering decisions must remain intelligible, challengeable, and **reproducible throughout their lifetime.**"

Reproducible pillar: *"the decision can be reconstructed and its basis re-evaluated."*
Clarification A: *"The Root Principle is an invariant design standard, not a claim that the platform presently satisfies it in full. Known gaps … must be recorded explicitly, treated as engineering obligations, and never concealed by weakening the principle."*

This is the platform's self-identified principal gap (OQ-001 / "throughout their lifetime").

## evidence

### E1 — Reasoning-model attestation, per run (real)
- **artifact:** `/c/Dev/ecf/runtime/runs/*/reasoning-model.yaml` (e.g. `RUN-REASON-20260718-0001/reasoning-model.yaml`).
- **demonstration (real):** Every run from 0.7 onward carries an attestation. All five I read record `model.model_id: unrecorded`, `declared_by.source: none`, `verification: declared_not_api_verified`. Runs predating 0.7 (`RUN-AN`, `RUN-REASON-20260716-0001`) carry **no** attestation file at all.
- **verified_by:** I read the raw files and surveyed every `reasoning-model.yaml` in `runtime/runs/`. The attestation records the model honestly as `unrecorded` — a confession, never a guessed identity. **Honest-but-thin:** the machinery to attest exists and fires on every run, but no real run has yet recorded a *resolved* model (the executor declares `source: none`). Recording a real id is additive (executor-supplied), not an architecture change.

### E2 — Degraded/irreproducible reproducibility-state on a REAL decision (real; strongest evidence)
- **artifact:** `/c/Dev/ecf/canonical/decisions/EDR-0002/reproducibility-state.yaml` (RSTATE-EDR-0002-0001) + validator `/c/Dev/ecf/tools/reproducibility/reproducibility_state.py`.
- **demonstration (real):** The record states `state: irreproducible`, `irreproducible_reason: model_never_recorded` — a genuine confession that the pre-instrumentation run `RUN-REASON-20260716-0002` that produced EDR-0002 never recorded its model. It is digest-bound: `decision_record_sha256 = 4b8f1de3…39b2d`.
- **verified_by:** I recomputed the SHA-256 of `EDR-0002/EDR-0002.md` → `4b8f1de3…39b2d`, byte-identical to the recorded `decision_record_sha256` (the state binds to the exact decision bytes, P8). I ran the validator against the real record with `repo_root='.'`: it returns **empty reasons** (valid). I then forged the same record to `state: fully_reproducible` and re-validated: it **refuses** on all three gates — the model identity does not resolve (`model_id: unrecorded` maps to empty), `model_availability` is not `available`, and there is no durable `model_independent_input`. The closed field set additionally makes `reproduced`/`identical`/`partially_reproducible` **unrepresentable**. So `fully_reproducible` is genuinely unreachable unless model resolves **and** is recorded-available **and** inputs are durable — exactly as claimed. This is a real, honest, checkable state on a real decision.

### E3 — Invalidation-propagation substrate, run against the REAL store (real, for the graph half)
- **artifact:** `/c/Dev/ecf/tools/assumption_dependency/resolve.py` (derived-on-read dependency graph) + real records `assumptions/ASM-0001..0004`, `canonical/decisions/EDR-0001..0002`.
- **demonstration (real):** I ran the resolver against the real store (no fixtures):
  - `rests-on EDR-0002` → `[ASM-0003, ASM-0004]` (derived purely from digest matches against EDR-0002's `approved-report` manifest entry).
  - `dependents ASM-0003` → `[{EDR-0002, current}]`; `dependents ASM-0001` → `[{EDR-0001, superseded}]`.
  - `current-dependents ASM-0003` → `[EDR-0002]`; and critically `current-dependents ASM-0001` → `[EDR-0002]` **via the real human-authored lineage edge** `ASM-0003.supersedes_assumption: ASM-0001`. An invalidation of the superseded-bound predecessor honestly reaches the *current* decision because a human drew the lineage edge — the "workflow, not archaeology" property, on real data.
- **verified_by:** I executed each query myself and cross-read the underlying real records (`assumptions/index.yaml`, `ASM-0003/assumption.yaml`). The graph is derived from bound digests and refuses (never guesses) on scalar/digest disagreement (I read the refusal paths and the 10 passing tests). This is a genuine end-to-end run of the graph substrate on real, non-fixture artifacts reaching a current decision.

### E4 — Propagator (invalidation → routed candidate): built, wired, fixture-proven only
- **artifact:** `/c/Dev/ecf/tools/reasoning_propagation/propagate.py` + `tools/reasoning_propagation/tests/test_propagate.py`.
- **demonstration (fixtures):** `propagate.py` imports the **real** `assumption_dependency.resolve` and the real `review_obligations`/`StewardshipLedger` routing seam; its full suite passes (71 tests across propagate + reproducibility). But it has **never fired on real data**: `find` shows **zero** `CAND-*` or `PROP-*` records anywhere in the real store (only fixture tempdirs).
- **verified_by:** I confirmed the tool exists, read its wiring (it genuinely calls `current_dependents`, not a re-implementation), ran the suite, and searched the real store for any produced candidate/propagation record — none exist. The final leg (a real `invalidated` review → propagate → `candidate.yaml` on EDR-0002) is fixture-proven, not reality-demonstrated.

## maturity_verdict

**Partial** (honestly earned, at the floor).

O12's mechanism is implemented and **demonstrated on real, non-fixture artifacts** on two independent axes: (a) the reproducibility-state contract produced a true, digest-bound, validator-enforced honest answer about a real decision (E2), and (b) the dependency-graph substrate runs end-to-end on the real store and reaches a *current* decision via a real lineage edge (E3). Every gap to Strong is named (below). No architectural contradiction prevents Strong. This is a genuine Partial — but it is carried by an honest *failure* state and a read-only graph substrate; the headline capabilities (a real invalidation propagated to a workflow candidate; a cross-model re-run) are not yet demonstrated on reality. That is the correct picture of the platform's weakest obligation, and it is recorded, not concealed (P2).

## open_items

### OI-1 — O12A-5: one REAL assumption invalidation propagated end-to-end
- **status:** shipped **UNMET-and-open** (PROPOSAL_07_PARTIAL_BARS exit ruling: the accountability office honestly ruled ASM-0003 `revised`, not `invalidated`; no obligation has fired on it — its trigger binds the still-open coupling map). Never manufactured (P2).
- **classification:** **named_gap_toward_strong.**
- **grounds:** Reality-gated. The audit method (§5) pre-classifies this a named gap *"provided the assessor confirms the propagation machinery actually runs."* I confirmed the machinery runs: the graph half runs **end-to-end on real data** reaching EDR-0002 (E3), and the propagator is built, correctly wired to the real resolver, and passes its suite (E4). Only the triggering reality is absent — no assumption has been honestly ruled `invalidated`. Reaching Strong here is purely additive (a genuine contradiction, ruled by a human) within the existing architecture; no frozen contract or architecture must break. **Honesty note:** the propagator's *own* final leg is fixture-proven, not real-proven — so this axis, taken alone, would be Emerging; O12 is lifted to Partial by E2/E3, not by E4.

### OI-2 — Cross-model re-run execution (OQ-001 research ceiling)
- **status:** specified, not demonstrated. No run has yet recorded a resolved model (all `unrecorded`, E1); no substitute-model re-run has been executed against durable inputs.
- **classification:** **named_gap_toward_strong.**
- **grounds:** Additive and architecturally satisfiable as built. The reproducibility-state schema can already *represent* a `degraded` state (resolvable original model + durable inputs + a populated `reevaluation_requirements` block that a substitute-model re-run consumes) and gates `fully_reproducible` on the same preconditions — I verified the gate refuses over-claims (E2). Nothing about "throughout their lifetime" is unrepresentable or requires a contract break; it requires (i) an executor that declares its model (additive to the attestation E1) and (ii) an actual cross-model re-run demonstration. This is the OQ-001 research ceiling named honestly, not a contradiction.

## determination

- **≥ Partial on real evidence?** **YES.** Two independent real-artifact demonstrations (E2 the honest irreproducible state on EDR-0002, digest-bound and validator-enforced; E3 the dependency graph run end-to-end on the real store reaching a current decision via a real lineage edge). The Partial claim is not falsified when re-derived — it holds.
- **Any Strong-blocker (contradiction blocking Strong)?** **NO.** Both open items are additive within the ratified, records-only architecture. `fully_reproducible`/`degraded` are representable and gated; the propagator is built and wired to the real graph; recording a real model is executor-additive. Reaching Strong needs more real coverage (a genuine invalidation; a cross-model re-run; model-recording executors), none of which requires breaking a frozen contract or the architecture.
- **Honesty verdict on Partial:** **Partial is genuinely earned — and no more.** The risk that it is "specification dressed as capability" is real for the *propagation* axis (E4) and the *cross-model* axis (OI-2), both of which are fixture/spec only. But O12 does not rest its Partial on those: it rests on E2 and E3, which are real, non-fixture, independently re-derived demonstrations of working machinery producing true, checkable answers about real decisions. The undemonstrated pieces are recorded UNMET-and-open (O12A-5) and research-ceiling (OQ-001), exactly as P2/Clarification A require. Partial holds honestly; the verdict deliberately does not inflate to Strong.
