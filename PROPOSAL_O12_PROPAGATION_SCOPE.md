# PROPOSAL_O12_PROPAGATION_SCOPE — Track A (O12) scope workshop: dependency & invalidation propagation

> **Status: RATIFIED (Founder, 2026-07-17).** Non-constitutional (T1 working
> proposal that organizes delivery of a ratified obligation). This document resolves the
> **Track A** design-open items from [PROGRAM_0.7](PROGRAM_0.7.md) as **2–3 options + one
> recommendation** per item, mirroring the ratified 0.6 precedents
> ([PROPOSAL_O7_SUPERSESSION_SCOPE](PROPOSAL_O7_SUPERSESSION_SCOPE.md),
> [PROPOSAL_O11_ASSUMPTIONS_SCOPE](PROPOSAL_O11_ASSUMPTIONS_SCOPE.md), both ratified
> 2026-07-16). The founder rules; then Track A builds. **No build precedes the ruling.**
>
> Obligation: **O12 — lifetime reproducibility of judgment** (P-Root, *"throughout their
> lifetime"*; depends on O11 ✓ / O7 ✓). Track A is the **concrete half**: the dependency
> graph and the live invalidation-propagation path. The governing tension is stated up
> front and honored throughout: **O12 is Research-stability; declaring it built would
> violate P2.** This proposal claims only a *demonstrated partial mechanism* — real
> invalidation propagated end-to-end — and names its ceiling explicitly (Clarification A).
>
> Constitutional edges honored throughout: **P7** (propagation raises *candidates*; never
> supersedes, never re-judges), **P8** (every dependency edge is *derived* from
> digest-bound evidence, never hand-maintained), **P14** (superseded bytes and chain
> intact), **P2** (no mechanism claims more than it demonstrates; the honest gaps are
> named, not concealed). Plane: Reasoning (PLATFORM_ARCHITECTURE §4.6), records-only.
>
> Evidence baseline: worktree `ecf-wt-o12a` (branch `feature/0.7-o12-propagation`) off
> `develop` @ `16ee325` (= v0.6.0). Every finding below is **probed from the real 0.6
> store**, not assumed. No spike code was written — this workshop is design-only.

---

## 0. The real material this design is grounded in (probed, not assumed)

Ten facts from the real v0.6.0 surfaces anchor every recommendation below.

1. **The seam is built and has never fired.** `tools/authority_rule/review_obligations.py`
   already validates the `invalidated` review outcome and **requires** a closed
   `supersession_candidate` block `{decision_ref, assumption_ref, obligation_ref,
   reason: assumption_invalidated}`. But every review on file
   (`assumptions/ASM-0001/obligations/OBL-20260716-0001/review.yaml` and `.../OBL-...-0002`)
   carries `outcome: reaffirmed`. **The `invalidated` arm has zero live instances.** This
   arm is O12 Track A's spine: it is where propagation must begin, and today it goes
   nowhere by construction (the O11 README states the seam "is consumed by no one").

2. **The store has a real, walkable supersession chain.** `canonical/decisions/index.yaml`
   (schema `0.2.0`) carries `EDR-0001` (superseded) and `EDR-0002` (current), linked by
   `EDR-0002.supersedes: EDR-0001`, grounds `better_evidence`; the write-once sibling
   `canonical/decisions/EDR-0001/superseded-by.yaml` mirrors the edge. `tools/canonical_resolution/resolve.py`
   answers `status | chain | current | list-current`, **derives** currency (an EDR is
   current iff nothing supersedes it), and **refuses (never guesses)** on a dangling,
   cyclic, forked, or marker-disagreeing store. This resolver is the exact idiom Item 2's
   dependency resolver must copy.

3. **The registry's two assumptions both bind only to the *superseded* decision.**
   `assumptions/ASM-0001` and `ASM-0002` each carry `provenance.decision_ref: EDR-0001`
   and were harvested from `RUN-REASON-WR0001-V040-0002`. **`EDR-0002` — the current
   decision — has zero harvested assumptions.** This single fact is the crux of the whole
   milestone: as the store stands, an invalidation can only ever reach a *superseded*
   record — which is archaeology, not the Vision workflow (§5).

4. **The dependency edge is genuinely derivable from digest-bound evidence — verified.**
   `ASM-0001.provenance.source_sha256 = e894a84e6c631f7b7928b1ca582d8276d1e0914d8b128fa0b69631caadd1053f`
   is **byte-identical** to the `approved-report` entry's `sha256` in
   `canonical/decisions/EDR-0001/evidence-manifest.yaml`, which in turn re-verifies against
   the report bytes on disk (probed live). So the edge *ASM-X → EDR-Y* is computable as:
   *ASM-X's `provenance.source_sha256` equals a `sha256` bound in EDR-Y's evidence
   manifest.* No hand-maintained pointer is needed — the `decision_ref` scalar is a
   convenience the derivation can *cross-check*, never trust (P8).

5. **"The same assumption over time" is byte-different across the supersession.**
   EDR-0001's `ASSUME-0001` reads *"The **two** open upstream blockers are resolvable…"*;
   EDR-0002's `ASSUME-0001` reads *"The **open upstream blocker MISS-0001** is
   resolvable… — **producing a dependency/coupling map** —…"* (singular; `MISS-0002` was
   demoted from blocker to confidence-reducer on the re-run). Different bytes → different
   `source_sha256` → the verbatim/digest harvest discipline **cannot** assign them one
   identity without lying about provenance (P8) or making a *semantic* sameness judgment
   (a human act, P7/P1). This drives Item 1.

6. **Harvest is scoped to canonical decisions' digest-bound evidence, and is verbatim.**
   `tools/assumption_registry/harvest.py` copies each assumption out of the digest-verified
   `approved-report`, refuses on digest mismatch, on out-of-scope sources, on transcription
   drift, and on a re-registered `(run, task, local-id)` triple. It is the promotion-tool
   idiom (deterministic, stdlib-only, fail-closed, never touches `runtime/`).

7. **The genuine contradiction material is already recorded — outside the harvested set.**
   `information_closures/CLOSURE-0001.yaml` (which closed the first run's MISS-0001)
   records, verbatim, that the cohesion signal is *"untestable pre-implementation"* and
   that the analysis register's `ASSUME-0003` (*"repository responsibilities… change for
   the same reasons as other external-system connections"*) is *"unsupported by any
   observed change."* That is a real, digest-bound refutation of a real assumption — but
   `ASSUME-0003` lives in the analysis register, which O11 **explicitly left un-harvested**
   as a named gap. The honest first-target discussion (§5) turns on this.

8. **O7 already built the consuming grounds class — as interface-only.** The supersession
   vehicle admits `supersession_grounds: invalidated_assumption` (closed vocabulary,
   PROPOSAL_O7 Item 2/G2), ratified but shipped **interface-only** at 0.6 (the evaluator
   was Track B's; propagation was deferred to O12 verbatim). **O12 Track A is the first
   real consumer of that grounds class.** No new supersession vehicle is needed — O12 wires
   the existing one to a derived, propagated candidate.

9. **The routing seam is proven and reusable a fourth time.** `review_obligations.py`
   routes on `StewardshipLedger.resolve()` ("one seam, three consumers" — approval,
   challenge, review-obligation), never yields an empty recipient (Clarification B/C), and
   degrades visibly to `founder_genesis` on vacancy. A candidate-on-a-decision is the
   fourth consumer, and it must inherit these properties unchanged.

10. **A concrete harvestability blocker exists for the current decision.** The O11 harvest
    regex expects `- **ASSUME-0001** (evidence_strength: weak): <statement>` (EDR-0001's
    rendering). EDR-0002's report renders `- **ASSUME-0001** — <statement>
    *(evidence_strength: weak)*` — a different assumptions-block format the regex does not
    match. **EDR-0002's assumptions therefore cannot be harvested by the tool as it
    stands** (probed: the regex finds zero matches in EDR-0002's report). This is the
    long pole under §5 and is flagged as a blocker.

---

## 1. Item 1 — assumption identity across time

**Question.** Is "the same assumption" one identity across a supersession (EDR-0001 and
EDR-0002 rest on overlapping assumptions), or re-harvested per decision? The identity
model is the spine everything else hangs on.

### 1.1 Options

**1A — One durable identity, re-bound across decisions.** `ASM-0001` is "the bounded-effort
assumption" as a concept; on supersession its `decision_ref`/provenance is extended (or a
new provenance entry appended) to also point at `EDR-0002`. One record, many decisions.

- *For:* matches the intuition that EDR-0001 and EDR-0002 "share" the bounded-effort
  assumption; a single query subject.
- *Against, decisive:* (a) the two statements are **byte-different** (§0.5) — one identity
  would have to hold two different verbatim texts, or silently pick one, destroying the
  provenance-to-the-byte discipline harvest is built on (P8); (b) re-binding *mutates* a
  write-once record (P14 violation — the registry index is an append-only ledger); (c)
  asserting the two are "the same" is a **semantic judgment** the machine is not permitted
  to make (P7/P1). 1A buys a convenient subject by lying about identity.

**1B — Distinct identity per decision, re-harvested; continuity is a derived *lineage
chain*** *(recommended)*. Each decision harvests its **own** assumptions to their own
`ASM-<NNNN>` identities, digest-bound to that decision's report. "The same assumption over
time" is expressed as an explicit, human-authored **lineage edge** between two distinct
records — reusing the primitive O11 already built: the `review.yaml` `revised_to:
{assumption_id: ASM-<NNNN>}` field. A lineage chain of `ASM` records mirrors the `EDR`
supersession chain: append-only, walkable, never a shared mutable identity.

- *For:* verbatim/digest provenance stays literal (P8); the append-only ledger is never
  mutated (P14); "sameness" is a *recorded human act* (a review outcome `revised` pointing
  `revised_to` the successor), not a machine inference (P7); it is **structurally identical
  to the ratified O7 supersession chain**, so `canonical_resolution`'s walk/refuse idiom
  transfers directly to an assumption-lineage resolver; and it composes with Item 2 — each
  `ASM` binds to exactly one report, so edges never smear across the supersession.
- *Against:* "what is the current form of this assumption?" requires a lineage walk, not a
  field read (addressed by the resolver, §2/Appendix); and today the lineage is **latent** —
  no `revised_to` links `ASM-0001` to any EDR-0002 assumption, because EDR-0002's
  assumptions were never harvested (§0.3, §0.10).

**1C — Content-hash identity (dedupe by statement).** Identity = hash of the normalized
statement; identical statements collapse to one `ASM`.

- *For:* automatic dedupe; byte-difference *creates* new identity for free.
- *Against, decisive:* it makes *near*-identical restatements (the EDR-0001→EDR-0002 case,
  which differs by a few words) **distinct** and *exact* restatements collapse — precisely
  the wrong grouping for "same assumption, revised." Normalization is itself an unbounded
  judgment surface (whitespace? synonyms? the "two blockers"→"MISS-0001" narrowing?). It
  smuggles the semantic call of 1A into a hash function and hides it (P2).

### 1.2 Recommendation (Item 1)

**Recommend 1B — distinct identity per decision; continuity as a derived lineage chain.**

- **Identity rule:** one `ASM-<NNNN>` per `(decision, declared assumption)`, harvested
  verbatim and digest-bound as O11 already does. Supersession of a decision **never**
  re-binds or mutates its assumptions; the successor decision harvests its own.
- **Lineage primitive (reuse, not invention):** the human-authored lineage edge is the O11
  `review.yaml` `revised_to` field, generalized so a *review of the predecessor
  assumption* can point at the *successor decision's freshly harvested assumption*. A new
  optional `supersedes_assumption: ASM-<NNNN>` field on the harvested successor record
  makes the edge walkable from the new end too (the O7 chain shape, applied to
  assumptions). Both ends are **human-declared**; neither is machine-inferred.
- **Resolution:** an assumption-lineage resolver (Appendix) walks the chain both directions
  and, like `canonical_resolution`, **refuses on a dangling/cyclic/forked lineage** rather
  than guessing. "Current form of ASM-0001" = walk forward to the head of its lineage.
- **Grounding:** this is the only model consistent with all four edges at once — the
  byte-difference (§0.5) forbids 1A/1C's merge; the append-only ledger forbids 1A's
  mutation; P7 forbids the machine declaring sameness; and P9 (*knowledge is versioned,
  never an ambient current truth*) is exactly "an assumption has identity, history, and
  lifecycle." The EDR chain already demonstrates the pattern works.

---

## 2. Item 2 — the dependency graph (machine-walkable, derived, never hand-maintained)

**Question.** Machine-walkable edges *assumption → dependent canonical decision(s)*,
DERIVED from digest-bound evidence bundles (P8). Define "what depends on ASM-X?" as a
resolver like `tools/canonical_resolution`. Where do the edges live — derived-on-read, or a
recorded index?

### 2.1 The derivation, stated precisely (probed, §0.4)

An edge *ASM-X → EDR-Y* exists **iff** `ASM-X.provenance.source_sha256` equals a `sha256`
bound in `EDR-Y/evidence-manifest.yaml` (the `approved-report` entry — the digest-verified
artifact the assumption was harvested from). This is a pure function of two digest-bound
facts already in the store; no edge is authored. The verification is live: `ASM-0001` and
`ASM-0002` both resolve to `EDR-0001` and to **nothing else** (their `source_sha256`
appears in no other manifest), which is correct — `EDR-0002` re-derived its own assumptions
and does not cite EDR-0001's report.

### 2.2 Options for where the edges live

**2A — Derived-on-read, recomputed every query** *(recommended)*. No stored edge set. A
read-only resolver scans the registry and the canonical manifests and computes the edge set
on each invocation, exactly as `canonical_resolution` recomputes currency from the ledger
on each call.

- *For:* the edge set **cannot drift** from the evidence (P8/P10 — there is no second copy
  to fall out of sync); it is impossible to hand-edit an edge into existence; it mirrors the
  ratified resolver idiom the store already trusts; the store is tiny and the scan is
  cheap. The `decision_ref`/`source_path` scalars in the registry become *cross-checks*: the
  resolver **refuses** if a scalar disagrees with the digest derivation (fail-closed, the
  `canonical_resolution` marker-vs-ledger idiom).
- *Against:* recomputation cost grows with store size (irrelevant at Partial; a named
  deepening if it ever matters).

**2B — A recorded, materialized edge index** (`assumptions/dependency-index.yaml`). The edge
set is written to a file and updated when assumptions/decisions land.

- *For:* O(1) lookup; a single artifact to inspect.
- *Against, decisive:* it is a **second source of truth** that must be kept atomic with the
  registry and the store — the exact hand-maintained edge P8 and the charter forbid ("never
  hand-maintained"). It can encode an edge no evidence supports, and nothing structurally
  stops it. This is the trap PROPOSAL_O7 rejected for the supersession index (X3) and O11
  rejected for closures.

**2C — Hybrid: derive-on-read, but *cache* with a digest guard.** Compute on read; persist a
cache keyed by the inputs' digests; recompute if the guard mismatches.

- *For:* speed with a correctness guard.
- *Against:* the cache is pure optimization with a real invalidation-bug surface, for zero
  benefit at Partial (P13 — a mechanism that must prove it earns its place cannot, here).

### 2.3 Recommendation (Item 2)

**Recommend 2A — derived-on-read, no stored edge set.** A new read-only resolver
`tools/assumption_dependency/resolve.py` (sibling of `canonical_resolution`, same house
style) exposes:

- `dependents(ASM-X)` → the EDRs whose manifests bind `ASM-X`'s `source_sha256`, each
  tagged `current | superseded` by delegating to `canonical_resolution.status` — so a query
  distinguishes *live* dependents from *historical* ones (this is what turns propagation
  into workflow, not archaeology, §3/§4).
- `rests_on(EDR-Y)` → the `ASM` records whose `source_sha256` is bound in EDR-Y's manifest.
- `current_dependents(ASM-X)` → `dependents` filtered to `status == current`, optionally
  **closed over the lineage chain** (Item 1): if `ASM-X` has a lineage successor bound to a
  current EDR, that EDR is a current dependent of the lineage.

**Fail-closed, never guess** (the ratified resolver contract): the resolver refuses on a
`decision_ref` scalar that disagrees with the digest derivation, on a manifest that does not
re-verify against its report bytes, and on a lineage edge that dangles or cycles. It writes
nothing, ever.

**Honest finding this surfaces immediately:** run today, `current_dependents(ASM-0001)` = **∅**
— ASM-0001 binds only EDR-0001, which is superseded. The graph is correct and the answer is
honest: *no current decision rests on ASM-0001*. Making a current decision depend on a
harvested assumption is the §5 precondition.

---

## 3. Item 3 — invalidation propagation (the seam fires, at last)

**Question.** When a review outcome is `invalidated`, how does the existing
`supersession_candidate` block reach **every** dependent decision and get routed as an
obligation (reuse the O4 `resolve()` seam / `review_obligations`)? P7: it raises
*candidates*; it never supersedes.

### 3.1 The gap in the built seam

`review_obligations.py` already produces, on `outcome: invalidated`, a
`supersession_candidate` with a **single scalar** `decision_ref` (today hand-set to the
assumption's own `provenance.decision_ref`). Two problems for O12: (a) a single scalar
reaches **one** decision — it cannot reach *every* dependent (the completeness requirement);
and (b) a hand-set scalar **is** the hand-maintained edge P8 forbids. Propagation must
replace the scalar's *authority* with the derived graph.

### 3.2 Options

**3A — Widen the scalar to a hand-authored list.** The reviewer writes `decision_refs: [...]`.

- *Against, decisive:* asks a human to enumerate the dependent set by hand — the P8
  violation, now with a completeness failure mode baked in (a missed dependent is a silent
  correctness hole). Rejected.

**3B — A deterministic propagation tool derives the dependent set and routes one candidate
per current dependent** *(recommended)*. On a persisted `invalidated` review, a
human-invoked, stdlib-only propagator:
1. reads the review's `supersession_candidate` and its bound `assumption_ref`;
2. calls `assumption_dependency.current_dependents(ASM-X)` (Item 2, lineage-closed) to
   derive the **full** set of current dependent decisions;
3. **cross-checks** the reviewer-recorded `decision_ref` is *within* the derived set
   (refuse if the human named a decision the evidence does not support — P4/P8);
4. writes, for **each** derived current dependent, one routed **supersession-candidate
   record** under that decision (Item 4), routed via `StewardshipLedger.resolve()` with the
   never-empty recipient (§0.9);
5. writes an atomic **propagation record** enumerating the assumption, the derived set, and
   every candidate written — and **exits nonzero if any derived dependent did not receive a
   candidate** (completeness is fail-closed, the O11-3 "a firing that cannot persist its
   obligation is a FAILURE, never a log line" idiom, applied to propagation).

- *For:* completeness is *derived and enforced*, not trusted; the edge authority is the
  digest graph (P8); routing reuses the proven seam (§0.9); P7 is structural — the outputs
  are *candidates on decisions*, nothing is superseded; it composes with the lineage model
  (an invalidation of ASM-0001 reaches EDR-0002 **iff** a human drew the lineage edge, which
  is the honest answer).
- *Against:* one new tool + one new record type (bounded; both are thin over existing
  idioms).

**3C — Fold propagation into the supersession/promotion tool.** Make `promote.py` compute
candidates when it sees an invalidated review.

- *Against:* overloads the store's sole *writer* with a *reasoning-plane* read/derive
  concern, and couples candidate-raising to a supersede act that P7 says must stay a
  separate human decision. Rejected (separation of raising from executing).

### 3.3 Recommendation (Item 3)

**Recommend 3B.** The propagator is the missing wire between the built-but-unfired seam and
the store. It **derives, routes, and enforces completeness**; it **never** supersedes,
re-judges, or mutates any EDR, index entry, or assumption (P7/P14). The reviewer's
`supersession_candidate.decision_ref` is retained as a *cross-checked* human declaration,
not the propagation authority — reconciling the built seam with the derived graph without a
schema break to `review_obligations.py`.

---

## 4. Item 4 — a workflow, not archaeology (the record(s))

**Question.** The output is a routed, actionable obligation on each dependent decision (the
Vision scene), with the invalidation evidence bound in. Specify the record(s).

### 4.1 The output record — a supersession-candidate obligation *on the decision*

The Vision scene (PLATFORM_ARCHITECTURE §4.6) is: *a standing decision can be revisited as an
engineering workflow when an assumption is contradicted — not an archaeological exercise.*
"Not archaeology" has a precise, checkable meaning here: the output is not a log entry a
human must go digging for, but a **routed, evidence-bound, human-answerable record sitting on
the decision itself**, discharged through the machinery O7 already built.

**Record: `canonical/decisions/EDR-<NNNN>/candidates/CAND-<YYYYMMDD>-<NNNN>/candidate.yaml`**
— a write-once sibling *in the dependent decision's directory* (the O7 `superseded-by.yaml`
sibling idiom: the directory *gains* an indelible record; nothing in it is edited — P14).
Closed field set:

- `candidate_id` (`CAND-<YYYYMMDD>-<NNNN>`), `decision_ref` (the EDR it sits on);
- `assumption_ref: {assumption_id, record_sha256}` — the invalidated assumption, pinned;
- `obligation_ref`, `review_ref: {path, sha256}` — the O11 obligation and the indelible
  `review.yaml` that produced the `invalidated` outcome, digest-bound (P8);
- `invalidation_evidence: [...]` — **non-empty** (P4), carried verbatim from the review's
  `evidence` (e.g. the closure record or contradicting dossier that refuted the assumption);
- `derived_via: {tool, source_sha256, manifest_sha256}` — the digest facts that made this an
  edge, so the candidate is self-certifying that it was derived, not asserted (P8);
- `routing` — written by the router via `resolve()`, never-empty recipient, `degraded`
  disclosed (§0.9; the O11 routing block, verbatim);
- `status: open | dispositioned` — **derived** from the existence of a sibling disposition,
  never rewritten.

**Disposition (the workflow's terminus, human-decided).** A candidate is answered by a
sibling `disposition.yaml` (one per candidate, ever — the challenge/O7 idiom) recording one
of: `superseded_via: {edr_id}` (a real superseding EDR was promoted with
`supersession_grounds: invalidated_assumption` and `grounds_ref` = this candidate — the O7
class §0.8 gets its first real consumer), `revised`, or `no_change` (with evidence and
rationale — a reaffirmation is a legitimate, recorded outcome). **P7:** the disposition is a
human act; the propagator never writes it.

### 4.2 The propagation record (the audit spine)

`assumptions/ASM-<NNNN>/propagations/PROP-<YYYYMMDD>-<NNNN>.yaml` — one per propagation
invocation, enumerating: the invalidated `assumption_ref`, the `review_ref`, the **full
derived dependent set** (each EDR with its `current|superseded` status), the candidates
written (paths + digests), and a `complete: true` assertion the tool only emits when every
current dependent received a candidate. This is the machine-checkable proof of the O12A-2
completeness clause (§bar), and the record a checker walks to verify no dependent was missed.

### 4.3 Why this is workflow, not archaeology (checkable)

Archaeology = a human must reconstruct, from scattered immutable history, which standing
decisions an invalidated assumption touched. Workflow = the touched **current** decisions
each carry, at their own identity, a routed obligation with the refuting evidence bound in
and a one-step human disposition path into the ratified supersession machinery. The
difference is the `candidate.yaml` on `EDR-0002` (current) — routed, evidence-bound,
answerable — versus a line in a log. The bar's O12A-4/O12A-5 clauses make exactly this
difference the pass condition.

---

## 5. Item 5 — the first real target, evaluated honestly

**The charter's flag.** EDR-0002 is current and still rests on live assumptions; a genuinely
contradicted one is the honest trigger. *Fixtures prove negatives, never the real clause.*

### 5.1 What the real store actually offers (the honest picture)

Three hard facts constrain the honest target:

- **(a)** The two harvested assumptions (`ASM-0001/0002`) bind only `EDR-0001` (**superseded**).
  Invalidating either raises a candidate on a superseded record — **archaeology, not the
  Vision scene**, which the ruled bar (PROGRAM_0.7 ruling 2a) requires to land *on EDR-0002*.
- **(b)** `EDR-0002` (current) has **no harvested assumptions** (§0.3), and cannot be
  harvested by the tool as it stands — the report-format drift blocker (§0.10). So *no
  current decision has any assumption edge at all today.*
- **(c)** The one **recorded, digest-bound refutation** in the corpus (CLOSURE-0001: the
  cohesion clause is *"untestable pre-implementation"*; `ASSUME-0003`'s "same reasons" clause
  *"unsupported by any observed change"*, §0.7) refutes an **analysis-register** assumption
  (`ASSUME-0003`) that O11 left **un-harvested**, and which the re-run (EDR-0002) already
  **dropped** — better evidence retired it implicitly.

The honest conclusion: **there is no already-harvested, already-contradicted assumption
bound to a current decision.** Manufacturing one (harvesting an assumption *in order to*
invalidate it, or inventing a contradiction) is the P3/P2 failure the O7 bar named ("a
fixture supersession is the P3 failure mode wearing O7's clothes"). The real target must be
*built up to*, honestly, in this order.

### 5.2 Options

**5A — Invalidate `ASM-0002` (bound to superseded EDR-0001) on the re-scoping evidence.**
EDR-0002's own bytes record that the re-run **re-scoped** (blocker set changed from two to
one; MISS-0001 redefined from "change-driver evidence" to "full coupling map") — arguably
contradicting ASM-0002's "*without re-scoping it*." The candidate lands on EDR-0001.

- *For:* uses only already-harvested material; a real contradiction with real bytes.
- *Against, decisive:* the dependent is **superseded** → fails the ruled Vision-scene bar
  (candidate must reach EDR-0002). Proves the mechanism, not the milestone. Useful only as a
  fixture-adjacent rehearsal, not the real clause.

**5B — Harvest EDR-0002's assumptions, then invalidate the honestly-contradicted one**
*(recommended)*. Precondition work first, then the real fire:
1. **Fix the harvest-format blocker (§0.10):** reconcile the report assumptions-block
   rendering (freeze the recommendation-report contract's format, or widen the harvest regex
   to accept both renderings). This is a small, honest engine fix; without it EDR-0002's
   assumptions are unreachable.
2. **Harvest EDR-0002's two assumptions** → new identities (e.g. `ASM-0003` from EDR-0002
   `ASSUME-0001`, `ASM-0004` from `ASSUME-0002`), digest-bound to EDR-0002's manifest
   (`source_sha256` = EDR-0002's `approved-report` sha), so `rests_on(EDR-0002)` and thus
   `current_dependents` become non-empty and **derivable** (P8).
3. **Draw the lineage edges** (Item 1): human-author `revised_to`/`supersedes_assumption`
   linking `ASM-0001→ASM-0003` and `ASM-0002→ASM-0004`, recording the "same assumption,
   revised on better evidence" continuity as an explicit act.
4. **Designate `ASM-0003`** (EDR-0002 `ASSUME-0001`: *"MISS-0001 [the coupling map] is
   resolvable through a bounded evidence-gathering effort rather than requiring an indefinite
   investigation"*) **as the first real target.** Its honest, recorded contradiction: the
   change-driver dossier that fed the very run (CLOSURE-0001) records that the
   coupling/cohesion signal MISS-0001 depends on is *"untestable pre-implementation"* — i.e.
   the map is **not** obtainable by bounded pre-implementation evidence-gathering, which is
   what the assumption asserts. This is a genuine tension a human reviewer can rule
   `invalidated` (or `revised`) on real evidence — P7 keeps the ruling human.
5. **Fire it:** a trigger on `ASM-0003` produces a routed obligation; the reviewer records
   `outcome: invalidated` with CLOSURE-0001 (and the coupling-map's non-arrival) as evidence,
   emitting the `supersession_candidate`; the propagator (§3) derives
   `current_dependents(ASM-0003) = {EDR-0002}` and raises a routed `candidate.yaml` **on
   EDR-0002** — the Vision scene, discharged.

- *For:* the **only** path that lands the candidate on a *current* decision honestly; every
  step is real work on real artifacts; it exercises the full stack (lineage, derived graph,
  propagation, candidate-on-decision, O7's `invalidated_assumption` grounds class as first
  consumer). What invalidating takes and what surfaces is stated exactly.
- *Against:* the long pole — the format fix + harvest + lineage + a defensible invalidation
  ruling all precede the single demonstrating propagation; and the "untestable
  pre-implementation" contradiction is **arguable**, not slam-dunk (a reviewer could
  honestly rule `revised`). If ruled `revised`, the real-fire clause is not discharged by
  *this* assumption and another must be found — reality outranks the plan.

**5C — Reduced bar: mechanics + negatives real; the one real propagation deferred/recorded
unmet.** Build the graph, propagator, candidate records, and all negatives against fixtures;
if no assumption is honestly ruled `invalidated` at exit, mark the real-fire clause
**explicitly unmet** (the O7-3/F2 precedent) rather than firing a fixture as if real.

- *For:* decouples the mechanism from the honesty of a specific contradiction ruling.
- *Against:* an O12 "Partial" with zero real propagations is specification, not capability —
  the line 0.5/0.6 refused to blur. Acceptable only as the founder's explicit fallback, with
  the gap recorded (P2/Clarification A), never a fixture passing as real.

### 5.3 Recommendation (Item 5)

**Recommend 5B**, with the sequencing stated plainly as the milestone's schedule risk: the
**harvest-format fix (§0.10) is on the critical path** — EDR-0002's assumptions are
unreachable without it, and every downstream step depends on them. If, at the invalidation
review, the founder/reviewer honestly rules `ASM-0003` `revised` rather than `invalidated`,
fall back to **5C** and record clause **O12A-5 unmet** — a recorded gap, not a redefinition,
and never a fixture firing dressed as the real clause (*fixtures prove negatives, never the
real clause*).

---

## 6. The proposed O12 Track-A Partial bar (PROPOSED, for the Bars thread)

Read per the ratified bar discipline: every clause needs a named **artifact**, a named
**demonstration** actually run, and a named **checker**; anything less is an explicit gap,
never a pass. Real clauses discharge by naming the identity of the real record produced.

### 6.1 Clauses

**O12A-1 — The dependency graph is derived, never hand-maintained (P8).** A read-only
resolver (`tools/assumption_dependency/resolve.py`) answers `dependents(ASM-X)`,
`rests_on(EDR-Y)`, and `current_dependents(ASM-X)` by matching assumption
`provenance.source_sha256` against canonical evidence-manifest digests, delegating currency
to `canonical_resolution`. *Negative:* an edge asserted by a `decision_ref`/`source_path`
scalar that is **not** backed by a digest match makes the resolver **refuse** (never guess) —
*a dependency edge not derivable from bound evidence fails.* *Checker: Machine (fail-closed
resolver) + independent validator (digest walk).*

**O12A-2 — Invalidation propagation reaches every dependent (completeness, fail-closed).** On
a persisted `invalidated` review, the propagator derives the **full** current-dependent set
from the graph and writes one routed candidate per dependent, plus a propagation record
asserting completeness. *Negative:* a propagation that routes to fewer than the derived set
(**misses a dependent**) exits nonzero and writes nothing final; a human-supplied
`decision_ref` outside the derived set is refused. *Checker: Machine (completeness cross-check
against the graph) + independent validator.*

**O12A-3 — Propagation raises candidates; it never supersedes (P7).** Every output is a
write-once `candidate.yaml` *on* a dependent decision; the propagator touches no `EDR-*.md`,
no `index.yaml` chain edge, no `superseded-by.yaml`, and no assumption record. *Negative:*
any path that writes a `supersedes` edge, a supersession marker, or an index mutation as a
*consequence of an invalidation* (i.e. without the two O7 human records) **fails** — *automation
that supersedes fails P7.* *Checker: Machine (write-surface audit) + independent validator +
Founder.*

**O12A-4 — The candidate is a workflow, not a log: routed, actionable, evidence-bound.** Each
`candidate.yaml` carries the invalidation evidence digest-bound (`review_ref`+sha,
`assumption_ref`+sha, non-empty `invalidation_evidence`, `derived_via` digests), a never-empty
`routing` block via `resolve()`, and a human disposition path into O7's `invalidated_assumption`
grounds. *Negative:* a candidate lacking bound evidence, or with an empty recipient, is
rejected (Clarification B). *Checker: Machine (fail-closed contract) + the accountable office
(acknowledges receipt).*

**O12A-5 — One REAL invalidation propagated end-to-end (the Vision scene).** One real
registered assumption **bound to a current decision** is reviewed `invalidated` on real
recorded evidence → propagation surfaces every dependent current decision → a routed
`candidate.yaml` is raised **on EDR-0002**. The discharged clause names the identities: the
assumption ID, the `review.yaml`, the propagation record, and the `CAND-*` on EDR-0002. A
fixture firing proves the mechanism; it **never** discharges this clause. *If no assumption is
honestly ruled `invalidated` at exit, this clause is recorded UNMET (P2), never fixture-passed.*
*Checker: Machine (contracts) + Founder (confirms the contradiction and the review are real) +
independent validator (walks assumption → review → propagation → candidate-on-EDR-0002).*

**O12A-6 — Identity/lineage is honest, human-declared, and derived-walkable.** Assumptions are
re-harvested per decision (distinct identity, digest-bound); continuity across a supersession
is an explicit human-authored lineage edge (`revised_to` / `supersedes_assumption`), walked by
the resolver like the EDR chain. *Negative:* a lineage edge that merges two distinct-byte
assumptions into one identity, that mutates a write-once record, or that is machine-inferred
rather than human-declared, **fails** (P7/P8/P14). *Checker: Machine (lineage validator,
fail-closed) + Founder (the lineage act is a human act).*

**Clause count: 6.**

### 6.2 Explicitly OUT of the Partial bar (P13 — named deferrals)

- **Reasoning migration / degraded-reproducibility states** — Track B (O12's research half);
  this proposal designs its side as **records-only** and depends on no Track B output (the
  seam is an interface, per the kickoff ruling).
- **Automated supersession-candidate *detection*** (a sweeper proposing candidates) — remains
  P7-constrained and is deepening; O12A raises candidates only from a *human-reviewed*
  invalidation.
- **Multi-hop / concurrent / branching propagation under contention** — one real hop is the
  bar; competing superseders and merge semantics are deepening (mirrors the O7 deferral).
- **Cross-repo dependents** (`context_switcher` projection) — inside `ecf` is the bar.
- **Transitive propagation across the lineage of *superseded* dependents** — candidates route
  to **current** dependents only (workflow, not archaeology); a superseded dependent's edge is
  recorded for audit, never routed.
- **Retirement-driven invalidation and non-assumption dependency classes** — the bar covers
  assumption→canonical-decision edges only.

---

## 7. The five recommendations, one line each

1. **Identity:** distinct `ASM` identity per decision, re-harvested verbatim/digest-bound;
   "same assumption over time" is an explicit **human-authored lineage chain** (`revised_to` /
   `supersedes_assumption`), walked like the EDR chain — never one shared mutable identity
   (byte-difference §0.5 + append-only ledger + P7 forbid a merge).
2. **Dependency graph:** **derived-on-read**, no stored edge set — a resolver matches
   `ASM.provenance.source_sha256` against canonical evidence-manifest digests (verified live),
   tags each dependent `current|superseded` via `canonical_resolution`, and **refuses** on any
   scalar that disagrees with the digest derivation (P8; hand-maintained edges rejected).
3. **Propagation:** a deterministic propagator derives the **full** current-dependent set,
   routes one candidate per dependent via the proven `resolve()` seam, cross-checks the
   reviewer's `decision_ref` against the derived set, and **fails closed if any dependent is
   missed** — replacing the built seam's single hand-set scalar; it never supersedes (P7).
4. **Workflow record:** a write-once, routed, evidence-bound **`candidate.yaml` on each current
   dependent decision** (the O7 sibling idiom), disposed by a human via O7's
   `invalidated_assumption` grounds class (its first real consumer) — plus a completeness-proving
   propagation record; candidates on *current* decisions, never a log.
5. **First real target:** **harvest EDR-0002's assumptions first** (after fixing the report-format
   harvest blocker §0.10), draw the lineage edges, then invalidate `ASM-0003` (EDR-0002's
   bounded-coupling-map assumption) on the recorded *"untestable pre-implementation"* refutation
   (CLOSURE-0001) → candidate raised on **EDR-0002** (the Vision scene); if honestly ruled
   `revised`, record clause O12A-5 unmet (5C) rather than fire a fixture as real.

---

## Appendix — spec-level deltas + resolver sketch *(SPEC-LEVEL ONLY — nothing here is built)*

### A. New read-only resolver `tools/assumption_dependency/resolve.py`

```text
# Derived-on-read; standard library; writes nothing, ever. Refuses (never guesses)
# on any inconsistency — the canonical_resolution contract, applied to edges.

def edge_exists(asm, edr_manifest) -> bool:
    # THE derivation (probed real, §0.4): the assumption's harvested source digest
    # is bound as evidence in the decision's manifest.
    return asm["provenance"]["source_sha256"] in {
        e["sha256"] for e in edr_manifest["evidence"]}

def rests_on(repo, edr_id):        # {ASM ids whose source_sha256 ∈ EDR-Y manifest}
def dependents(repo, asm_id):      # [{edr_id, status}] status via canonical_resolution
def current_dependents(repo, asm_id, close_lineage=True):
    # dependents filtered status=='current', optionally closed over the ASM lineage:
    # if asm_id has a human-declared successor bound to a current EDR, include that EDR.

# Fail-closed refusals (raise ResolutionRefused, exit 1):
#   - ASM.provenance.decision_ref disagrees with the digest-derived edge set
#   - an EDR manifest does not re-verify against its report bytes
#   - a lineage edge dangles / cycles / forks (two successors of one assumption)
```

### B. Registry / record deltas (all additive; closed field sets → honest version bumps)

- **`assumptions/ASM-<NNNN>/assumption.yaml` 0.1.0 → 0.2.0** — optional
  `supersedes_assumption: ASM-<NNNN>` (the harvested successor names its lineage predecessor;
  the walkable "new end" of Item 1's chain). Existing 0.1.0 records valid as recorded (P14).
- **`review.yaml`** — no schema change; the existing `revised_to` field is the lineage "old
  end." The `supersession_candidate.decision_ref` remains, re-read by O12 as a *cross-checked*
  human declaration, not the propagation authority (§3.3) — no break to `review_obligations.py`.

### C. New records (write-once; challenge/O7 sibling idiom)

```yaml
# canonical/decisions/EDR-<NNNN>/candidates/CAND-<YYYYMMDD>-<NNNN>/candidate.yaml
schema_version: "0.1.0"
candidate_id: CAND-20261016-0001
decision_ref: EDR-0002                      # a CURRENT dependent (workflow, not archaeology)
assumption_ref: {assumption_id: ASM-0003, record_sha256: "<registry bytes>"}
obligation_ref: OBL-<YYYYMMDD>-<NNNN>
review_ref: {path: "assumptions/ASM-0003/obligations/OBL-.../review.yaml", sha256: "<...>"}
invalidation_evidence:                       # NON-EMPTY (P4), carried from the review
  - {ref: "information_closures/CLOSURE-0001.yaml",
     note: "cohesion signal untestable pre-implementation — bounded-effort clause refuted"}
derived_via:                                 # self-certifying that the edge was DERIVED (P8)
  tool: tools/assumption_dependency/resolve.py
  source_sha256: "<ASM-0003 provenance.source_sha256>"
  manifest_sha256: "<EDR-0002 approved-report sha it matched>"
routing:                                     # ROUTER-written via resolve() (O11 shape, verbatim)
  accountable_role: accountability
  authority: assumption_review               # or a new candidate-review grant, founder's call
  model_version: "0.3.0"
  holder_state: active | vacant
  effective_recipient: accountability | founder_genesis   # NEVER empty (Clarification B/C)
  degraded: false
status: open | dispositioned                 # DERIVED from the sibling disposition

# .../CAND-*/disposition.yaml  (human act; one per candidate ever — P7/P14)
outcome: superseded_via | revised | no_change
superseded_via: {edr_id: EDR-0003}           # iff a real EDR-0003 was promoted with
                                             #   supersession_grounds: invalidated_assumption,
                                             #   grounds_ref: CAND-20261016-0001 (O7's first
                                             #   real consumer of that grounds class, §0.8)
evidence: [ ... ]                            # NON-EMPTY (P4)
```

```yaml
# assumptions/ASM-<NNNN>/propagations/PROP-<YYYYMMDD>-<NNNN>.yaml  (the completeness proof)
schema_version: "0.1.0"
assumption_ref: {assumption_id: ASM-0003, record_sha256: "<...>"}
review_ref: {path: "...", sha256: "<...>"}
derived_dependents:                          # the FULL graph answer, each tagged
  - {edr_id: EDR-0002, status: current}
  - {edr_id: EDR-0001, status: superseded}   # recorded for audit; NOT routed (current-only)
candidates_written:
  - {edr_id: EDR-0002, candidate_id: CAND-20261016-0001, path: "...", sha256: "<...>"}
complete: true                               # emitted ONLY if every current dependent got a
                                             #   candidate; else the tool exits nonzero (O12A-2)
```

### D. New tool `tools/reasoning_propagation/propagate.py` (deterministic, human-invoked)

Reads a persisted `invalidated` review + the derived graph; writes the `CAND-*` records and
the `PROP-*` record atomically; **never** writes into `canonical/decisions/EDR-*.md`, the
index, or any assumption record. Refusal matrix (fail closed, nothing written): review not
`invalidated` or unreadable; `supersession_candidate.decision_ref` outside the derived set;
any derived current dependent that cannot receive a candidate (completeness); a target
candidate id already exists (write-once); routing yields an empty recipient. Exit codes
mirror the house style: `0` propagated · `1` refused (reasons on stderr) · `2` usage/config.

---

## Risks and blockers found while grounding this proposal

1. **Are the edges truly derivable from bound evidence? — YES, verified; but the live
   current decision has none.** `ASM-0001.provenance.source_sha256` is byte-identical to
   EDR-0001's `approved-report` manifest digest, which re-verifies against the report bytes
   (probed). The derivation is real and hand-pointer-free. **However**, `current_dependents`
   of both harvested assumptions is **empty** — they bind only the superseded EDR-0001, and
   **EDR-0002 has no harvested assumptions.** Propagation to a current decision is therefore
   *impossible today* until §5's precondition work lands. This is the central structural
   finding and the milestone's real content.

2. **BLOCKER — the harvest tool cannot read EDR-0002's assumptions (report-format drift).**
   The O11 harvest regex expects `- **ASSUME-0001** (evidence_strength: weak): <stmt>`
   (EDR-0001's rendering); EDR-0002's report renders `- **ASSUME-0001** — <stmt>
   *(evidence_strength: weak)*` and matches **zero** assumptions (probed). Harvesting
   EDR-0002's assumptions — the precondition for any current-decision edge — requires either
   freezing the recommendation-report assumptions-block format in its contract or widening the
   harvest regex to accept both renderings. On the milestone's critical path; must be ruled.

3. **The one recorded contradiction is arguable, not slam-dunk (P2 honesty).** The
   *"untestable pre-implementation"* refutation (CLOSURE-0001) supports an `invalidated`
   ruling on `ASM-0003`, but a reviewer could honestly rule `revised`. P7 keeps the ruling
   human; §5.3 provides the 5C fallback (record O12A-5 unmet) so the bar cannot be forced by a
   fixture. The genuinely *un-arguable* refutation in the corpus (`ASSUME-0003`, "same
   reasons") targets an **un-harvested, already-dropped** analysis-register assumption — a
   named gap, not a live target.

4. **Routing authority for a candidate-on-a-decision needs a founder call.** The candidate
   reuses the `resolve()` seam, but "who reviews a supersession candidate raised on a
   decision" may be `assumption_review` (reuse) or a new grant. Additive T4-style bump if the
   founder prefers the honest token; the §4 records are unchanged either way. Flagged, not
   assumed.

5. **Lineage edges are latent and must be human-authored.** Item 1's continuity depends on a
   human drawing `ASM-0001→ASM-0003` etc.; the machine must never infer it (P7). Until drawn,
   `current_dependents` does not close over the lineage, and an invalidation of `ASM-0001`
   honestly reaches no current decision — the correct, honest answer, not a bug.

6. **Worktree hygiene.** `ecf-wt-o12a` carries CRLF churn under `research/`, `review_packs/`,
   `roles/`, `standards/`, `vendor/`, `transformations/`, `tasks/classification/` (shared
   parallel-session artifacts). This workshop staged nothing; any Track A build must stage
   explicit paths only and never `git add -A`.

---

## Metadata

| Field | Value |
|---|---|
| Owner (proposing) | Track A owner (O12 — dependency & invalidation propagation) |
| Status | **RATIFIED (Founder, 2026-07-17)** — Track A authorized to build; harvest-format fix folded into build |
| Change class | T1 working proposal (organizes the ratified 0.7.0 milestone); the routing-authority token (risk 4), if the founder prefers a new grant, classifies T4 on the O4/O11 precedent |
| Derives from | [PROGRAM_0.7](PROGRAM_0.7.md) Track A design-open items 1–5 + kickoff ruling 2(a) · P-Root ("throughout their lifetime") + Clarification A · P2 · P7 · P8 · P9 · P14 · P11 |
| Evidence base | `ecf-wt-o12a` @ develop `16ee325` (= v0.6.0, design-only — no spike code): `assumptions/{index.yaml, ASM-0001/, ASM-0002/, README.md}` · `assumptions/ASM-0001/obligations/OBL-20260716-000{1,2}/{obligation,review}.yaml` · `assumptions/evaluations/` · `canonical/decisions/{index.yaml, EDR-0001/, EDR-0002/}` (records, `evidence-manifest.yaml`, `superseded-by.yaml`, `evidence/engineering-recommendation-report.md`) · `information_closures/CLOSURE-000{1,2}.yaml` · `tools/assumption_registry/{harvest.py, records.py, evaluate.py, closures.py}` · `tools/authority_rule/review_obligations.py` · `tools/canonical_resolution/resolve.py` · `tools/canonical_promotion/promote.py`; live digest probe confirming `ASM-0001.source_sha256 == EDR-0001 approved-report manifest sha` |
| Serves | O12 / P-Root ("throughout their lifetime") · P8 (derived, never hand-maintained edges) · P7 (raises candidates, never supersedes) · P14 (bytes + chain intact) · P2 (honest ceiling, named gaps) |
| Cross references | [PROPOSAL_O7_SUPERSESSION_SCOPE](PROPOSAL_O7_SUPERSESSION_SCOPE.md) (supersession vehicle + `invalidated_assumption` grounds class) · [PROPOSAL_O11_ASSUMPTIONS_SCOPE](PROPOSAL_O11_ASSUMPTIONS_SCOPE.md) (§4.4 seam · harvest · routing) · [PROPOSAL_06_PARTIAL_BARS](PROPOSAL_06_PARTIAL_BARS.md) (bar discipline · O12 deferral I.4) · [PLATFORM_PRINCIPLES](PLATFORM_PRINCIPLES.md) · [PLATFORM_ARCHITECTURE](PLATFORM_ARCHITECTURE.md) §4.6 |
