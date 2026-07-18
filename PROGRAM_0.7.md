# PROGRAM 0.7 — Lifetime Reasoning Integrity

> Organizes delivery of the [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md) 0.7.0 milestone. It
> **organizes** that scope; it does not amend it. Non-constitutional (T1).

| Field | Value |
|---|---|
| Milestone | **0.7.0 — Lifetime Reasoning Integrity** |
| Obligation | **O12** lifetime reproducibility of judgment (P-Root "throughout their lifetime"; depends on O11 ✓) — the platform's **weakest** obligation, Research → **Partial** |
| Exit criteria | O12 reaches **Partial**; **Open Question 001** has a *demonstrated* partial mechanism |
| North star | The Vision success scene: *a standing decision can be revisited as an **engineering workflow** when an assumption is contradicted — not an archaeological exercise* |
| Status | **Scope RATIFIED 2026-07-17.** Both track scopes + the 8+6 Partial bars ratified as recommended; model recording = **Option B** (run-level attestation, no frozen-contract touch); the O12A-5 real-invalidation clause is under the **honesty rule** (pursue a genuine invalidation; record UNMET-and-open if a human review honestly rules it `revised`; never manufacture one — P2). **Tracks A and B authorized to build.** Engine-hardening rides the background lane. |

## The governing tension (read first)

O12 is **Research**-stability. The ratified architecture says plainly: *"declaring it built
would violate P2."* The single most consequential act of this milestone is therefore
setting a Partial bar that is **honestly minimal** — a real, demonstrated mechanism, never
a claim to have solved lifetime reproducibility. Clarification A governs: known gaps
between the Root Principle and current capability are recorded as obligations, **never
concealed by weakening the principle**. Every 0.7 deliverable is measured against P2 first.

## What already exists (0.6 did most of the plumbing)

- **Assumption registry** (`assumptions/`, `ASM-<NNNN>`) with digest-bound provenance to the
  emitting run; **review obligations** whose `invalidated` outcome already carries a
  `supersession_candidate` block (the Track-A seam, built but never fired).
- **O7 supersession** chain, exercised for real (EDR-0001 → EDR-0002, bytes intact,
  chain-walkable).
- The `information_closures/` registry and the deterministic evaluator (O11).

O11 **explicitly deferred full invalidation propagation to O12**. So much of 0.7 is *wiring
existing pieces into a live propagation path* — plus the genuinely research-grade honesty
layer (reasoning migration across models; degraded-reproducibility states).

## Founder kickoff rulings (2026-07-17)

1. **Two parallel tracks** — Track A = dependency graph + invalidation propagation
   (concrete; builds O11→O7); Track B = reasoning migration + degraded-reproducibility
   states (the OQ-001 research core). Each: scope workshop → founder ratification → build,
   in its own worktree (the proven 0.4–0.6 pattern).
2. **O12 Partial bar = real invalidation propagated end-to-end** (ruled up front, refined
   by the Bars workshop): **(a)** one REAL assumption *invalidated* (not reaffirmed) →
   propagation surfaces **every** dependent canonical decision → a **supersession-candidate
   raised on EDR-0002 as a routed workflow** (the Vision scene); **(b)** one REAL run
   carries a recorded **degraded-reproducibility state** naming its reasoning model
   (`claude-opus-4-8`) and what a future re-evaluation would need. Honest about the ceiling.
3. **Carryover lane = engine hardening only.** Evidence-permanence (FD-2's Control-owned
   obligation) was NOT taken as a separate carryover — it is **folded into Track B's
   scope**, because a degraded-reproducibility state is meaningless if the evidence it
   points to lives in mortal `runtime/`. B1 (EKB canonicalization) and B2 (projection)
   remain deferred, non-gating.

## Scope ratifications (2026-07-17)

Proposal docs — all **RATIFIED (Founder)**: [PROPOSAL_O12_PROPAGATION_SCOPE](PROPOSAL_O12_PROPAGATION_SCOPE.md) ·
[PROPOSAL_O12_MIGRATION_SCOPE](PROPOSAL_O12_MIGRATION_SCOPE.md) ·
[PROPOSAL_07_PARTIAL_BARS](PROPOSAL_07_PARTIAL_BARS.md) (the exit criteria).

Ratified as recommended, with three rulings:
- **Model recording = Option B** — a runner-written run-level `reasoning-model.yaml`
  attestation from executor-declared config; the frozen per-task provenance contract is
  NOT re-opened (per-task binding would have been a T4 amendment). Declared-not-API-verified
  is the honest ceiling. (Baseline confirmed by both threads: the reasoning model is
  recorded **nowhere** today — provenance names only `executor: claude-code`.)
- **O12A-5 honesty rule** — pursue a genuine invalidation of `ASM-0003` on CLOSURE-0001's
  recorded independent-drivers contradiction of its "same reasons" premise; **if a human
  review honestly rules it `revised`/`reaffirmed`, record O12A-5 UNMET-and-open**
  (Clarification A) and ship 0.7 Partial with that gap visible. The machinery still ships
  proven-by-fixture. **An invalidation is never manufactured to pass a bar (P2).**
- **Harvest-format fix** — the O11 harvest regex cannot parse EDR-0002's report (format
  drift); harvesting EDR-0002's assumptions is the precondition for all propagation. The
  fix folds into Track A build scope (a defect fix, not a governance item).

Design decisions ratified: assumption identity = distinct ASM per decision + human-authored
lineage chain; dependency graph = derived-on-read (no stored index, P8); propagation =
deterministic, reaches every dependent, fails closed on a miss, raises candidates via O7's
`invalidated_assumption` grounds class, never supersedes (P7); degraded-state = closed enum
`{fully_reproducible, degraded, irreproducible}` with no optimistic middle; migration
comparison = `{concordant, divergent, inconclusive}`, never "identical"; cross-model re-run
= specified-not-demonstrated (OUT of Partial); FD-2 durability rule scoped to the one real
exposure (`CHG-20260716-0001/disposition.yaml`'s bare mortal pointer).

## Exit sequence — outcomes (2026-07-17)

The 0.7 exit sequence, executed with the Founder making each human act. **Both real-act
clauses resolved honestly, and neither was manufactured** — the milestone's whole point.

**O12B — the platform's first reproducibility record is a confession.** The schema would
not permit a lie: `degraded` requires a reasoning-model identity that resolves, and
`RUN-REASON-20260716-0002` (behind EDR-0002) never recorded its model — runs before 0.7
did not attest it, and there is no honest retroactive attestation source. So the only state
the machinery accepts is **`irreproducible: model_never_recorded`**, recorded at
`canonical/decisions/EDR-0002/reproducibility-state.yaml` (digest-bound to EDR-0002).
**Founder ruling:** this honest record SATISFIES bar clause O12B-2 — the clause's intent
was a real, honest reproducibility-state on a real decision; the honest value for a
pre-instrumentation run is `irreproducible`, and that is a pass, not a miss. The clause
wording "degraded" is read as "the honest reproducibility-state." The `degraded` machinery
is proven by fixture; runs from 0.7 onward attest their model (the runner now writes
`reasoning-model.yaml`) and will honestly earn `degraded`/`fully_reproducible`.

**O12A — the real invalidation honestly does not exist yet; O12A-5 UNMET-and-open.** The
propagatable assumption `ASM-0003` ("the coupling map is obtainable by bounded effort",
weak) was reviewed by the accountability office (Founder) against `CLOSURE-0001` ("no
implementation code exists; untestable pre-implementation"). **Founder ruling: `revised`,
not `invalidated`** — the evidence weakens but does not falsify the assumption. Mechanically
this is doubly honest: `ASM-0003`'s own evidence-arrival trigger is bound to EDR-0002's
still-OPEN MISS-0001 (the coupling map, ungathered), so **no obligation has fired** — there
is nothing to hang an invalidation on, and manufacturing a trigger firing would be a fixture
in costume (P2). Per the ratified honesty rule, **bar clause O12A-5 is recorded
UNMET-and-open** (Clarification A): the invalidation→propagation machinery is proven by
fixture (the once-dead `supersession_candidate` seam now fires end-to-end in tests), and the
real invalidation awaits real triggering evidence that does not yet exist. 0.7 ships Partial
with this gap **visible, not concealed** — exactly the outcome a Research→Partial obligation
should be able to reach.

This is O12 at Partial the only way P2 permits: the machinery demonstrated, the reasoning
model now recorded going forward, the FD-2 permanence exposure closed — and the platform
recording, in its own store, both that it cannot reproduce its past reasoning and that its
first real invalidation has not honestly arrived.

## Track A — Dependency & Invalidation Propagation

**Design-open (workshop before build):**
1. **Assumption identity across time** — an assumption's stable identity as decisions are
   superseded (EDR-0001 and EDR-0002 rest on overlapping assumptions; is "the same
   assumption" one identity across the supersession, or re-harvested per decision?). The
   identity model is the spine everything else hangs on.
2. **The dependency graph** — machine-walkable edges *assumption → canonical decision(s)
   that rest on it*, derived from the digest-bound evidence bundles (never hand-maintained,
   P8). "What depends on ASM-X?" must be a machine-answerable query, like O7's chain.
3. **Invalidation propagation** — when a review outcome is `invalidated`, the existing
   `supersession_candidate` block must actually **reach every dependent decision** and be
   routed as an obligation (O4 seam) — not logged. P7: propagation raises *candidates for
   human supersession*; it never supersedes.
4. **As a workflow, not archaeology** — the output is a routed, actionable obligation on
   each dependent decision (the Vision scene), with the invalidation evidence bound in.
5. **First real target** — which real assumption to invalidate. EDR-0002's disposition
   still rests on live assumptions (it deferred pending the coupling map); a genuinely
   contradicted one is the honest trigger. Fixtures prove negatives, never the real clause.

## Track B — Reasoning Migration & Degraded Reproducibility

**Design-open (workshop before build):**
1. **Model identity in provenance** — is the reasoning model (`claude-opus-4-8`) recorded
   in the run's provenance today? Reproducibility-over-time is impossible without it (P8/P9).
2. **Degraded-reproducibility state vocabulary** — a recorded state per decision:
   *fully-reproducible* (the model is still available), *degraded* (model gone; re-evaluation
   needs the recorded assumptions + evidence + a substitute model), *irreproducible*. A
   first-class record type, fail-closed and honest (P2).
3. **What reasoning migration means** — the assumptions and evidence are model-independent
   recorded artifacts; the *judgment* was model-dependent. Migration = re-evaluating a
   standing decision under a different model against the same recorded inputs, and recording
   the comparison — not claiming byte-identical reproduction.
4. **Evidence permanence (folded-in FD-2 obligation)** — a degraded-reproducibility state
   is only meaningful if what it points to survives. Track B closes the live dangling-
   evidence exposure (permanent records citing mortal `runtime/` paths) by making a
   decision's model-independent inputs (assumptions, evidence bundle) durable. This is the
   Control-owned permanence obligation FD-2 created, scoped to exactly what O12 needs.
5. **P2 honesty in the schema** — a state that claims reproducibility it cannot deliver must
   be unrepresentable; "irreproducible" is a first-class, non-shameful recorded outcome.

## Carryover lane (non-gating) — Engine hardening

The three engine-ergonomics defects the 0.5/0.6 real runs surfaced (each has a documented
ops workaround; the proper fix belongs in the engine):
- **H1** — surface **executor-level failure detail** in the run record (three diagnostics
  this cycle needed the probe because the engine summary swallowed it).
- **H2** — fix **`--retry-failed`** (no-op on an already-reset task) and the **state/manifest
  lockstep** divergence on the frontier-failure path (both now handled by `reopen_run.py`).
- **H3** — make the **O11 release gate (gate 10) read-only** (or commit-its-evidence
  cleanly) instead of writing eval records into a tracked dir on every validation run.

## Constitutional edges

- **P2 (honesty) is THE edge of 0.7** — no mechanism may claim reproducibility it does not
  deliver; `irreproducible` and `degraded` are honest, first-class outcomes. Clarification A.
- **P7** — invalidation propagation raises *candidates*; humans decide every supersession
  and every migration acceptance. No automation invalidates, supersedes, or re-judges.
- **P8/P9** — provenance and versioned knowledge are the substrate of reproducibility;
  the reasoning model's identity is part of provenance.
- **P14** — a superseded-via-invalidation decision keeps its bytes and chain intact.

## Immediate next step

Background threads, own worktrees, everything returned **PROPOSED** for founder
ratification (the established pattern): Track A workshop · Track B workshop · Partial-bars
proposal (turning the ruled bar into evidence-checkable clauses with negatives and the
Partial-vs-Strong line). Engine-hardening rides as the background lane once builds start.

| Field | Value |
|---|---|
| Owner | Founder |
| Status | Kicked off; workshops pending launch |
| Created | 2026-07-17 (post v0.6.0) |
| Cross references | [PROGRAM_0.6](PROGRAM_0.6.md) · [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md) · [PLATFORM_PRINCIPLES](PLATFORM_PRINCIPLES.md) (Root, P2, P7, P8, P9) · [PLATFORM_ARCHITECTURE](PLATFORM_ARCHITECTURE.md) §4.6 Reasoning Plane · [PLATFORM_VISION](PLATFORM_VISION.md) Open Question 001 |
