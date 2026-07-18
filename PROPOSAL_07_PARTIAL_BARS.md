# PROPOSAL — 0.7 Partial Exit Bar (O12)

> **Status: RATIFIED (Founder, 2026-07-17) — these clauses are the 0.7 exit criteria.**
> The real-invalidation clause (O12A-5) is governed by the honesty rule: pursue a genuine
> invalidation; if a human review honestly rules the candidate `revised`/`reaffirmed`, the
> clause is recorded UNMET-and-open (Clarification A) and 0.7 still ships Partial — an
> invalidation is NEVER manufactured to pass the bar (P2). This proposal turns the
> [PROGRAM_0.7](PROGRAM_0.7.md) exit criterion ("O12 reaches **Partial**; Open
> Question 001 has a *demonstrated* partial mechanism") into precise,
> evidence-checkable clauses, following the ratified 0.6 precedent
> ([PROPOSAL_06_PARTIAL_BARS](PROPOSAL_06_PARTIAL_BARS.md)). Non-constitutional (T1).
> **It does not re-open the ruled bar.** PROGRAM_0.7 kickoff ruling 2 already fixed
> what O12-Partial *is* — (a) a real invalidation propagated end-to-end to a routed
> supersession-candidate on the dependent decision, and (b) a real run carrying a
> recorded degraded-reproducibility state naming its reasoning model. This document
> only makes that ruling *checkable*. It does not modify PROGRAM_0.7.md, and it does
> **not** pre-empt the parallel Track A / Track B scope workshops: wherever a ruling
> from those threads could change a clause, the clause is written **parametrically**
> ("the ratified propagation record", "the ratified degraded-state schema", "the
> ratified dependency-derivation") so that ratifying this bar constrains *what must
> be true*, not *which design gets there*.

| Field | Value |
|---|---|
| Derives from | [PROGRAM_0.7](PROGRAM_0.7.md) (kicked off 2026-07-17) · [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md) 0.7.0 |
| Bar proposed | **O12 Partial** — lifetime reproducibility of judgment (the platform's **weakest** obligation, Research → Partial; depends on O11 ✓) |
| Governing edge | **P2 first.** The ratified architecture states plainly that *"declaring it built would violate P2."* Every clause is measured against honesty before completeness. |
| Precedent | PROPOSAL_06_PARTIAL_BARS (ratified 2026-07-16) — clause discipline, artifact/demonstration/checker, real-not-fixture, named real identities, bar-vs-reality tracking |
| Evidence baseline probed | `ecf` @ `16ee325` (= v0.6.0; branch `chore/0.7-partial-bars`, read-only worktree) + the real run `RUN-REASON-20260716-0002` (`ecf` main checkout, read-only) |
| Change class | T1 Operational (a bar refinement; the obligation and the Partial target are already ratified in the roadmap and re-ruled at 0.7 kickoff) |

---

## How to read a bar (unchanged from the ratified 0.5/0.6 discipline)

A Partial bar is met only when **every clause** below has (a) a named **artifact**
that exists, (b) a named **demonstration** that was actually run, and (c) a named
**checker** who verified it. Per P2, a clause with an artifact but no demonstration,
or a demonstration nobody checked, is an **explicit gap**, never a pass. Per the
roadmap's honesty guard, 0.7 is claimed only when the bar is met, validated, and
released.

Checker vocabulary (as in 0.6): **Machine (fail-closed contract)** · **Independent
validator (O5/P6)** · **Founder** (the only checker who can mark a clause
*ratified*).

One discipline carried forward from how the 0.5/0.6 bars were actually
**discharged**: the real acts were named artifacts with identities (`EDR-0002`,
`APPROVAL-0002`, `ACCEPTANCE-0002`, `RUN-REASON-20260716-0002`, `CLOSURE-0001`,
`OBL-20260716-0001`) — not assertions that "a real case was run." Every REAL clause
below must discharge the same way: by naming the identity of the real record it
produced.

**The honesty framing specific to O12 (read before the clauses).** O12 is a
**Research-stability** obligation. A Partial bar here is not "lifetime reproducibility
solved at reduced scope"; it is **one real, demonstrated mechanism** on each of the
two ruled halves, wrapped in an honest declaration of everything still open (§I.5 is
deliberately long). A bar that read as a completeness claim would itself violate P2.

---

# Part I — The O12 Partial bar

**Bar being refined (PROGRAM_0.7 kickoff ruling 2, restated):** a standing decision
can be revisited as an **engineering workflow** when an assumption is contradicted —
not an archaeological exercise (the Vision scene) — **and** the platform records,
honestly, the degree to which each decision's *judgment* can be reproduced over time,
naming the reasoning model it depended on. The bar has two ruled halves:

- **Group A — real invalidation, propagated (the concrete Track-A half).** One REAL
  registered assumption *invalidated* → propagation surfaces **every** dependent
  canonical decision → a **supersession-candidate raised on the current dependent
  decision (`EDR-0002`) as a routed workflow**.
- **Group B — real degraded-reproducibility (the OQ-001 research half).** One REAL
  run carries a recorded **degraded-reproducibility state** naming its reasoning
  model (`claude-opus-4-8`) and what a future re-evaluation would need — honest about
  the ceiling, with the model-independent inputs it points to made durable.

## I.1 The bar as enumerated clauses

### Group A — real invalidation propagated end-to-end

**O12-1 — A machine-derivable dependency graph: assumption → every *current*
dependent decision (P8).** The ratified dependency-derivation (Track-A workshop
ruling: a derived edge set, a materialized record, or a resolver query — whichever
the founder ratifies) answers **"what current canonical decision depends on
`ASM-X`?"** as a machine query, exactly as `resolve.py` answers "what superseded
`EDR-X`?". The edges are **derived from the digest-bound evidence bundles, never
hand-maintained** (P8), and they **resolve through the supersession chain**: an
assumption recorded against a *superseded* decision whose live successor re-rests on
it resolves to the **successor**. This clause exists because the baseline back-pointer
is stale by construction — `ASM-0001`/`ASM-0002` both record `decision_ref: EDR-0001`,
which `resolve.py` now reports `superseded_by: EDR-0002` (see §I.6). A graph that
returned `EDR-0001` would surface history, not the live dependency.

**O12-2 — A REAL assumption *invalidated* fires the ratified propagation trigger
(P4).** The `invalidated` review outcome — already schema-live and fail-closed in
`tools/authority_rule/review_obligations.py` (it *requires* the closed
`supersession_candidate` block on that outcome) — is recorded against a **real
registered assumption on real, contradicting evidence**, producing a real review
record whose identity the discharged clause names. The invalidation is settled by
evidence (P4), not manufactured to pass this bar (§I.3, §II tension 1).

**O12-3 — Propagation surfaces *every* dependent current decision as a routed
supersession-candidate workflow (the Vision scene; P8/O4).** From the `invalidated`
review's `supersession_candidate` seam, the ratified propagation record reaches
**each** decision the dependency graph (O12-1) names as currently dependent — at the
real target, `EDR-0002` — and is **routed as an actionable obligation** on that
decision (the O4 `StewardshipLedger.resolve()` seam, never-empty recipient), with the
invalidation evidence bound in. It is a **routed workflow, not a log line**: the
output is an obligation a human can act on, the archaeology-to-engineering transition
the North Star names. Completeness is the clause's teeth — a propagation that reaches
*some* dependents is a P8-derivability failure (§I.4-1), not a partial pass.

**O12-4 — Propagation raises a candidate; it never executes a supersession (P7).**
The whole authority of the propagation path is **detect, surface, and route**. It
raises a *supersession-candidate obligation*; a human decides every supersession, and
the existing O7 supersession machinery (fresh approval + acceptance + human-invoked
write, ratified at 0.6) performs any actual supersession. Nothing in the propagation
path auto-invalidates a decision, auto-supersedes a record, or auto-re-judges. This is
the O11/O7 seam consumed for the first time — and consumed *as a candidate*.

### Group B — real degraded-reproducibility state

**O12-5 — The reasoning model is recorded in the run's provenance (P8/P9).** The
identity of the reasoning model that produced the judgment (`claude-opus-4-8`) is a
recorded provenance fact of the run, distinct from the **executor** (`executor.id:
claude-code` — the harness, which is all provenance records today; see §I.6). Whether
ratified as a new provenance field, a run-manifest entry, or a decision-bound
attestation, the property is fixed: **reproducibility-over-time is impossible without
naming what did the reasoning** (P8/P9), and a decision whose reasoning model is
unrecorded cannot honestly claim `fully_reproducible` (O12-6, §I.4-2).

**O12-6 — The ratified degraded-reproducibility state schema — fail-closed and honest
(P2).** A first-class, per-decision recorded state over the ratified vocabulary
(`fully_reproducible` — the reasoning model is still available; `degraded` — the model
is gone, re-evaluation needs the recorded assumptions + evidence bundle + a substitute
model; `irreproducible`) that **names the reasoning model** and, for `degraded`,
**what a future re-evaluation would need**. The schema is **honest by construction**:
a state that claims reproducibility it cannot deliver — e.g. `fully_reproducible` with
no recorded model — is **unrepresentable** (the closed-field, fail-closed discipline
of `review_obligations.py`), and `irreproducible` is a first-class, non-shameful
outcome. This is the clause that carries "declaring it built would violate P2."

**O12-7 — One REAL run carries a recorded degraded state naming its model and its
re-evaluation needs.** The state is recorded against a **real run** — the natural
target is `RUN-REASON-20260716-0002`, the source run of the current decision
`EDR-0002` — naming `claude-opus-4-8` and the **model-independent recorded inputs** a
substitute-model re-evaluation would consume (the assumption records, the digest-bound
evidence bundle). The discharged clause names the real state record's identity.
Fixtures prove the negatives; they never discharge this clause (§I.3).

**O12-8 — What the degraded state points to survives (evidence permanence; folded
FD-2, P8/P9).** A degraded-reproducibility state is meaningless if the inputs it names
live only in mortal `runtime/`. Per PROGRAM_0.7 kickoff ruling 3 (FD-2's
Control-owned permanence obligation, folded into Track B scoped to exactly what O12
needs), the decision's **model-independent inputs** the state points to — its
assumption records and its evidence bundle — are **durable** (the digest-bound
`canonical/decisions/EDR-*/evidence/` pattern already proven at 0.5/0.6), not a
permanent record citing a mortal `runtime/` path. The state's references resolve, and
keep resolving after the emitting run is gone.

## I.2 Artifact · demonstration · checker, per clause

| Clause | Artifact that proves it | Demonstration that verifies it | Who checks |
|---|---|---|---|
| O12-1 | The ratified dependency-derivation + its query surface over `assumptions/` and `canonical/decisions/` | Query "what depends on `ASM-0001`?" returns `EDR-0002` (the current dependent), resolved through the chain; **negative: an edge that resolves only to the superseded `EDR-0001` and stops is rejected — the graph must reach the live successor (P8)** | Machine (derivation contract) + independent validator (edges are derived from evidence bundles, not hand-authored) |
| O12-2 | The real `invalidated` review record under `assumptions/ASM-*/obligations/OBL-*/review.yaml` with its non-empty evidence and closed `supersession_candidate` block | The live fire on real contradicting evidence; **negative (already live): an `invalidated` review missing the `supersession_candidate` block is rejected; an unchanged-evidence evaluation fires nothing** | Machine (fail-closed contract) + Founder (confirms the contradiction is real, not staged) |
| O12-3 | The ratified propagation record(s) — one routed obligation per current dependent decision, evidence-bound, on the O4 seam | A propagation walk: the `supersession_candidate` reaches every decision O12-1 names as dependent, each as a routed obligation; **negative: a dependent decision that receives no obligation fails the completeness check** | Machine (propagation + routing contract) + independent validator (walks assumption → graph → every routed obligation) |
| O12-4 | The propagation path's refusal surface + the (separate, human-driven) O7 supersession act if one follows | **Negative pair: (i) the propagation path attempting to write `superseded` status, or admit a superseding record, is refused; (ii) no supersession exists in the store that lacks the 0.6-ratified fresh human approval + acceptance.** Positive: propagation ends at a routed *candidate* | Machine (fail-closed refusals) + Founder (the supersession decision, if taken, is the Founder's own) |
| O12-5 | The reasoning-model field on the run's provenance (or ratified equivalent) carrying `claude-opus-4-8` | A provenance read returns the reasoning model distinct from `executor.id`; **negative: a decision claiming `fully_reproducible` (O12-6) whose run has no recorded reasoning model is rejected** | Machine (provenance schema) + independent validator (model ≠ executor) |
| O12-6 | The ratified degraded-state schema (closed field set, fail-closed) | Schema validation: `fully_reproducible` without a recorded model is **unrepresentable**; `irreproducible` is a legal first-class value; **negative: a state asserting reproducibility above what its recorded inputs support is rejected (P2)** | Machine (fail-closed contract) + Founder (vocabulary ratification) |
| O12-7 | The real degraded-state record bound to `RUN-REASON-20260716-0002` / `EDR-0002`, naming `claude-opus-4-8` + the re-evaluation inputs | The real record exists, names the model, and names the recorded assumptions + evidence bundle a substitute-model re-run would consume; identities named | Machine (contract) + Founder (confirms the run is real) + independent validator (the named inputs resolve) |
| O12-8 | The durable (digest-bound) copies of the degraded state's referenced inputs under a permanent home | The state's references are re-resolved after the emitting `runtime/` run is treated as gone; **negative: a state whose only reference is a mortal `runtime/` path is rejected (P8)** | Machine (reference-permanence check) + independent validator (durability, not a live-`runtime/` citation) |

## I.3 REAL-not-fixture requirements (the 0.5/0.6 discipline, applied to O12)

Fixtures are **required** — they are the only honest way to prove the negatives
(O12-2's missing-`supersession_candidate` rejection, O12-6's unrepresentable
`fully_reproducible`, O12-1's stop-at-superseded rejection, O12-8's mortal-path
rejection). But **fixtures prove negatives only; they never discharge the REAL
clauses (O12-2, O12-3, O12-5, O12-7).** Specifically:

1. **The invalidation is of a REAL registered assumption.** `ASM-0001` / `ASM-0002`
   are real records in `assumptions/index.yaml`, digest-bound to their emitting run.
   The `invalidated` outcome must be recorded against a real one on real contradicting
   evidence — not a fixture assumption in a test store. (Reality's honest candidate is
   discussed in §II tension 1: `EDR-0002` still *rests on a live assumption* — the
   coupling-map deferral, `MISS-0001` still open — so a genuine contradiction is
   possible without manufacture.)
2. **Propagation surfaces the REAL dependent `EDR-0002`.** The routed
   supersession-candidate must land on the real current decision in
   `canonical/decisions/`, named by identity — not on a fixture decision, and not on
   the superseded `EDR-0001`.
3. **The degraded state is on a REAL run naming the REAL model.** The state is
   recorded against `RUN-REASON-20260716-0002` (the real source run of `EDR-0002`) and
   names `claude-opus-4-8` — the actual reasoning model — not a placeholder string.
   A degraded state over a fixture run, however complete, discharges nothing here.

Each REAL clause is discharged the 0.6 way: **by naming the identity of the real
record it produced** (the review record, the propagation obligation(s), the
provenance field, the degraded-state record).

## I.4 Boundary cases — what explicitly does NOT count (sharp, P2-forward)

1. **A propagation that silently misses a dependent decision fails P8-derivability
   (O12-3).** Surfacing *some* dependents while missing others is worse than the
   baseline: it manufactures false confidence that the impact of an invalidation has
   been fully seen. If the dependency graph (O12-1) names a current dependent and no
   obligation reaches it, the bar fails — a partial propagation is not a Partial pass.
2. **A degraded state that claims `fully_reproducible` while the model id is
   unrecorded is *the* P2 violation, not a pass (O12-5/O12-6).** This is the sharpest
   edge of the whole milestone. Reproducibility-over-time requires naming what did the
   reasoning; a record that asserts full reproducibility over a run whose reasoning
   model is absent is precisely the concealment P2 forbids. The honest value for such
   a run is `degraded` (or `irreproducible`), and the schema must make the dishonest
   value **unrepresentable**, not merely discouraged.
3. **Automation that *performs* a supersession (rather than raising a candidate) fails
   P7 (O12-4).** An invalidated assumption may *trigger* a supersession obligation; it
   may never *execute* one. A propagation path that flips a decision to `superseded`,
   admits a superseding record, downgrades a decision's status, or re-runs the
   reasoning has crossed from *detect-and-oblige* into deciding — the line
   `review_obligations.py` draws in its own docstring, extended to the decision.
4. **A migration/degraded record claiming byte-identical reproduction across models is
   dishonest by construction and fails (O12-6).** The judgment was model-dependent;
   the assumptions and evidence are the model-independent artifacts. Any record
   asserting that a different model reproduced the *judgment* byte-for-byte is a
   category error wearing a proof's costume — reasoning migration means re-evaluating
   against the same recorded inputs and **recording the comparison**, never claiming
   identity. The schema must reject the byte-identical-across-models claim.
5. **A manufactured invalidation does not discharge O12-2 (P2).** A challenge filed in
   order to be upheld, or an assumption declared in order to be invalidated on
   command, is a fixture wearing a costume — the same honesty guard the 0.6 bars drew
   (PROPOSAL_06 tension 3). The two real obligations that have fired to date
   (`OBL-20260716-0001/0002`) were both **`reaffirmed`**, honestly — the evidence
   *proved* the assumption. The real invalidation must be an evidence-settled
   contradiction, or it is not real.
6. **A fixture propagation or fixture degraded state discharges nothing real.**
   Firing an `invalidated` review against a test assumption, or writing a degraded
   state over a test run, satisfies the contract negatives/positives only (and is
   required for them). The real clauses name real identities in the real stores.
7. **A dependency edge that stops at the superseded record fails O12-1.** An edge
   `ASM-0001 → EDR-0001` that does not resolve forward to the live `EDR-0002` surfaces
   history as if it were the live dependency — the stale-back-pointer trap the baseline
   sets (§I.6). The graph must resolve through the supersession chain or it is wrong.
8. **A degraded state pointing only into mortal `runtime/` fails O12-8.** A permanent
   record whose re-evaluation inputs resolve only to an unversioned `runtime/` path is
   a promise the platform cannot keep — the dangling-evidence exposure FD-2 named. The
   named inputs must be durable, or the state is not honest about its own
   reproducibility.

## I.5 Partial vs Strong — deliberately OUT of the Partial bar (P13)

O12 is a **Research → Partial** obligation. The OUT list is long **and that is
honest** — it is the P2-required record of the ceiling, not an apology.

- **Full automatic multi-hop invalidation cascades.** The bar propagates one
  invalidation to its *direct* current dependents. Transitive cascades — an
  invalidation that surfaces a supersession, whose acceptance invalidates a further
  assumption, and so on, automatically — are deepening (and P7-constrained regardless:
  every hop still raises a candidate a human decides).
- **Actually executing a cross-model re-run.** Migration may be
  **specified-not-demonstrated**: the degraded state records *what* a substitute-model
  re-evaluation would need (O12-6/O12-7). Actually running `EDR-0002`'s reasoning under
  a different model and recording the comparison is deepening — Partial requires the
  honest *state*, not the re-run.
- **General runtime-evidence permanence beyond a decision's own inputs.** O12-8 makes
  durable exactly what a degraded state points to (the decision's assumptions and
  evidence bundle). A general permanence regime for all of `runtime/` (FD-2's B1 EKB
  canonicalization, B2 projection) remains deferred and non-gating (kickoff ruling 3).
- **Propagation across the consumer-repo boundary.** The bar lives inside `ecf`.
  Making `context_switcher` (or any consumer) see an invalidation or a
  degraded-reproducibility state is deepening.
- **Automated confidence recalculation or re-judgment.** Machines evaluate *trigger
  conditions* and *route*; judging what an invalidation does to a decision's
  confidence, or what a substitute model's re-evaluation *means*, remains with the
  human reviewer (P7).
- **Daemon / scheduled evaluation.** As at 0.6, evaluation-on-invocation suffices;
  guaranteed evaluation latency, cron wiring, and background sweepers that *propose*
  invalidations are deepening.
- **A general reasoning-migration framework.** One real degraded state on one real run
  is the bar. A migration engine, a substitute-model registry, or cross-model
  equivalence scoring is Strong, not Partial.
- **Retirement / irreproducible-by-loss mechanics beyond the recorded state.** The bar
  requires that `irreproducible` be *representable and honest*; a lifecycle for acting
  on irreproducible decisions (retire, re-derive, escalate) is deepening.

## I.6 Bar-vs-reality baseline (what exists at v0.6.0 = `16ee325` vs what 0.7 must add)

| Clause | Exists today (probed evidence) | 0.7 must add |
|---|---|---|
| O12-1 | **No dependency graph.** `resolve.py` walks the *decision→decision* supersession chain (`status`/`chain`/`current`, fail-closed on forks/cycles/dangling), but there is **no assumption→decision derivation**. The only back-pointer is `provenance.decision_ref` on each assumption — and it is **stale by construction**: `ASM-0001`/`ASM-0002` both record `decision_ref: EDR-0001`, which `resolve.py` reports `superseded_by: EDR-0002`. `EDR-0002` re-rests on the same bounded-resolvability premise but **no assumption is harvested against it** (the index holds only the two `EDR-0001` rows) | The ratified derivation answering "what *current* decision depends on `ASM-X`?", resolving through the chain; and the ruling on assumption identity across supersession (one identity vs re-harvest per decision) |
| O12-2 | **The invalidation path is built but has never fired.** `tools/authority_rule/review_obligations.py` is fully live: `invalidated` *requires* the closed `supersession_candidate {decision_ref, assumption_ref, obligation_ref, reason}` block, fail-closed. But **both** real obligations that have fired (`OBL-20260716-0001`, `-0002` under `ASM-0001`) are **`reaffirmed`** — the evidence (`CLOSURE-0001/0002`) *proved* the assumption. No real `invalidated` review exists | One real `invalidated` review on real contradicting evidence (honest trigger discussed in §II tension 1) |
| O12-3 | **No propagation consumer.** The `supersession_candidate` seam is a durable record the docstring says Track A "**may** consume" — and it is "consumed by no one in 0.6." No routing of a candidate onto a dependent decision exists | The ratified propagation record + routing of a candidate onto every current dependent, on the O4 seam, as a workflow |
| O12-4 | **The P7 discipline is live for reviews; untested for propagation.** `review_obligations.py` "detects and obliges" and never auto-decides; O7's `promote.py`/supersession requires fresh human approval + acceptance (ratified 0.6, exercised for real: `EDR-0002` supersedes `EDR-0001` via `APPROVAL-0002`/`ACCEPTANCE-0002`, `better_evidence`) | The refusal surface proving the *propagation path* raises a candidate and never executes a supersession |
| O12-5 | **The reasoning model is NOT recorded.** Every provenance record in `RUN-REASON-20260716-0002/provenance/` carries only `executor: {id: claude-code}` (the harness) + `generated_at`. The single `model_version: 0.3.0` anywhere in the run (`reports/completion.yaml`) is the **authority model**, not the reasoning LLM. `claude-opus-4-8` appears **nowhere** in the run | The reasoning-model provenance field (model ≠ executor), carrying `claude-opus-4-8` |
| O12-6 | **No degraded-reproducibility vocabulary exists** anywhere in the repo — no `reproducibility_state`, `degraded`, `irreproducible`, or `reasoning_model` field in any schema. The fail-closed closed-field-set idiom to build it on is proven (`review_obligations.py`, `resolve.py`) | The ratified degraded-state schema — fail-closed, honest-by-construction, `irreproducible` first-class |
| O12-7 | Nothing. The real target run exists and is well-formed (`RUN-REASON-20260716-0002` → `EDR-0002`, current), but carries no reproducibility state and does not name its reasoning model | The one real degraded-state record on the real run, naming the model + re-evaluation inputs |
| O12-8 | **Partial durability already exists; the gap is the pointer.** `EDR-0002`'s evidence bundle is digest-bound under `canonical/decisions/EDR-0002/evidence/` (the durable pattern), and `ASM-*` records carry `record_sha256`. But a degraded state does not exist yet to point at them, and the run's own `runtime/` inputs remain mortal | The state's references bound to the durable inputs (not mortal `runtime/`), and the check that they keep resolving |

---

# Part II — Cross-consistency check (the O12 bar vs PROGRAM_0.7's constitutional edges and the ratified 0.6 bars)

1. **P2 is honored first, and made testable.** "No mechanism may claim reproducibility
   it does not deliver; `irreproducible` and `degraded` are honest, first-class
   outcomes" maps clause-for-clause: unrepresentable-false-reproducibility →
   O12-6 + boundary I.4-2/I.4-4; model recorded or no `fully_reproducible` claim →
   O12-5; honest ceiling recorded → the long §I.5. The bar adds the *checkable form*
   of P2 (a fail-closed schema), not a reinterpretation. **Consistent** — and the bar
   is deliberately structured so that "declaring it built" is impossible: the OUT list
   and `irreproducible` are load-bearing, not decorative.
2. **P7 is honored on the propagation half.** "Invalidation propagation raises
   *candidates*; humans decide every supersession and every migration acceptance" →
   O12-4 (propagation raises, never executes) + boundary I.4-3. The O11/O7 seam is
   consumed for the first time, and consumed *as a candidate* — the 0.6 boundary
   (PROPOSAL_06 I.3-3: "an invalidated assumption may *trigger* a supersession
   obligation; it may never *execute* one") is inherited verbatim. **Consistent.**
3. **P8/P9 are the substrate, made concrete.** "The reasoning model's identity is part
   of provenance" → O12-5; "versioned knowledge is the substrate of reproducibility" →
   O12-8 durable inputs; "what depends on `ASM-X` must be machine-answerable, derived,
   never hand-maintained" (Track A design-open 2) → O12-1. **Consistent.**
4. **P14 is not contradicted; it is depended upon.** Propagation surfaces a
   supersession *candidate*; if a human accepts it, the 0.6-ratified O7 machinery keeps
   the superseded record's bytes and chain intact (`EDR-0001` stands, `superseded-by`
   marker + ledger cross-checked by `resolve.py`). The bar reuses that machinery; it
   does not weaken it. **Consistent.**
5. **The ratified 0.6 bars are not contradicted.** O11's boundary that "a fired trigger
   produces a *review obligation* and nothing more; full invalidation propagation is
   O12" (PROPOSAL_06 II.4) is exactly the seam this bar now consumes — 0.7 picks up
   precisely where 0.6 declared the line. O7's narrow canonical-store definition, its
   fresh-human-acts requirement, and its digest-stability survive untouched (O12-4
   routes *to* that machinery, never around it). The O4 routing properties
   (never-empty recipient, visible degradation) are reused, not weakened (O12-3).
   **Consistent.**
6. **Tension 1 (flagged, honesty-guarding) — the ruled real invalidation cannot be
   manufactured, and reality has so far *reaffirmed*.** Kickoff ruling 2(a) requires a
   REAL invalidated assumption. But an invalidation filed *in order to* discharge the
   bar is a fixture in costume (P2; boundary I.4-5), and the only two real obligations
   that have fired were both `reaffirmed` — honestly, because the evidence proved the
   assumption. The bar is therefore written to require an **evidence-settled**
   contradiction, and reality supplies an honest candidate **without manufacture**:
   `EDR-0002` is `gather_additional_evidence` and still **rests on a live assumption** —
   the dependency/coupling map (`MISS-0001`) is still open, and the bounded-resolvability
   premise (`ASM-0001`) is exactly the kind a coupling map could contradict. *If* that
   evidence arrives and contradicts the premise, the invalidation is genuine; *if it
   reaffirms*, reality outranks the plan and the bar waits for an honest trigger rather
   than staging one. This is the O12 analogue of PROPOSAL_06 tension 3, and it is the
   single most likely place the 0.7 schedule blocks on reality — flagged so it is ruled,
   not stumbled into.
7. **Tension 2 (flagged, design-constraining) — the assumption's recorded dependent is
   the *superseded* decision.** `ASM-0001`/`ASM-0002` record `decision_ref: EDR-0001`,
   but `EDR-0001` is superseded by `EDR-0002`, and no assumption is harvested against
   `EDR-0002`. O12-1 is written to require resolution *through* the chain (and
   boundary I.4-7 rejects an edge that stops at the superseded record), but the Track-A
   workshop must **rule assumption identity across supersession** (one identity carried
   forward vs re-harvest per decision — Track A design-open 1) or the build will either
   surface the wrong (superseded) decision or miss the live one. A sequencing cost,
   resolvable; flagged so the bar does not silently depend on an unruled identity model.
8. **Tension 3 (flagged, honestly bounding) — this is Research reaching Partial, and
   the bar says so.** Unlike O7/O11 (Foundational/near-complete obligations reaching
   Partial with short OUT lists), O12 is the platform's *weakest* obligation. The
   honestly minimal bar — one real propagation, one real degraded state — sits beside a
   deliberately long §I.5. A reader who mistakes the met bar for "lifetime
   reproducibility achieved" has misread it against P2; the metadata, the governing-edge
   row, and §I.5 exist to foreclose that misreading. **Honestly achievable, and
   honestly bounded** — which is the whole point of ruling the bar minimal.

---

## Metadata

| Field | Value |
|---|---|
| Status | **RATIFIED (Founder, 2026-07-17)** — the 0.7 exit criteria; O12A-5 under the honesty rule |

> **Exit-sequence outcomes (Founder, 2026-07-17):** **O12B-2 SATISFIED** by the honest
> `irreproducible: model_never_recorded` state on EDR-0002 (degraded was unreachable —
> the run never recorded its model; the honest value is a pass, not a miss). **O12A-5
> UNMET-and-open** (Clarification A): the accountability office ruled ASM-0003 `revised`
> not `invalidated`, and no obligation has fired on it (its trigger binds the still-open
> coupling map) — the propagation machinery is fixture-proven; the real invalidation
> awaits real evidence. Never manufactured (P2).

| Owner Role | Program Steward (WS-0) |
| Change class | T1 Operational |
| Derives from | [PROGRAM_0.7](PROGRAM_0.7.md) · [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md) 0.7.0 · [PLATFORM_PRINCIPLES](PLATFORM_PRINCIPLES.md) (Root lifetime clause + Clarification A, P2, P7, P8, P9, P13, P14) · [PLATFORM_VISION](PLATFORM_VISION.md) Open Question 001 |
| Evidence probed | `ecf` worktree `chore/0.7-partial-bars` @ `16ee325` (v0.6.0), read-only: `assumptions/{index.yaml, README.md, ASM-0001/, ASM-0002/, evaluations/}`, `assumptions/ASM-0001/obligations/OBL-20260716-000{1,2}/{obligation,review}.yaml`, `canonical/decisions/{index.yaml, EDR-0001/, EDR-0002/}`, `tools/authority_rule/review_obligations.py`, `tools/canonical_resolution/resolve.py`, `tools/assumption_registry/` · `ecf` main checkout, read-only: `runtime/runs/RUN-REASON-20260716-0002/provenance/*.yaml` (18 task records, all `executor.id: claude-code`), `reports/completion.yaml` |
| Cross references | [PROPOSAL_06_PARTIAL_BARS](PROPOSAL_06_PARTIAL_BARS.md) (bar precedent, ratified) · [PROPOSAL_05_PARTIAL_BARS](PROPOSAL_05_PARTIAL_BARS.md) (exit discipline) · [PLATFORM_ARCHITECTURE](PLATFORM_ARCHITECTURE.md) §4.6 Reasoning Plane, FD-2 (parametric) |
