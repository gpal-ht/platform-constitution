# PROPOSAL — 0.6 Partial Exit Bars (O7 · O11)

> **Status: RATIFIED (Founder, 2026-07-16)** — these 6+6 clauses are the 0.6 exit
> criteria; parametric clauses now bind to the ratified Track A/B scopes and the
> FD-2 Reading-B ruling. Non-constitutional (T1). This
> proposal turns the [PROGRAM_0.6](PROGRAM_0.6.md) exit criteria ("O7 and O11 each reach
> **Partial** — bars to be ratified") into precise, evidence-checkable exit criteria,
> following the ratified 0.5 precedent
> ([PROPOSAL_05_PARTIAL_BARS](PROPOSAL_05_PARTIAL_BARS.md)). Nothing here is ratified;
> the founder rules. This document does not modify PROGRAM_0.6.md, and it does **not**
> pre-empt the parallel Track A / Track B scope workshops or the FD-2 memo: wherever a
> ruling from those threads could change a clause, the clause is written
> **parametrically** ("the ratified vehicle", "the ratified trigger classes", "the
> ratified routing") so that ratifying this bar constrains *what must be true*, not
> *which design gets there*.

| Field | Value |
|---|---|
| Derives from | [PROGRAM_0.6](PROGRAM_0.6.md) (kicked off 2026-07-16) · [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md) 0.6.0 |
| Bars proposed | **O7 Partial** (Track A — safe supersession, P14) · **O11 Partial** (Track B — executable assumptions, P11) |
| Precedent | PROPOSAL_05_PARTIAL_BARS (ratified 2026-07-16) — clause discipline, negative cases, real-not-fixture, bar-vs-reality tracking |
| Evidence baseline probed | `ecf` @ `e19a2e0` (= v0.5.0; branch `chore/0.6-partial-bars` worktree) + real runs `RUN-REASON-WR0001-V040-0002` and the 0.5 exit chain (main checkout, read-only) |
| Change class | T1 Operational (a bar refinement; obligations and milestone exit are already ratified in the roadmap) |

---

## How to read a bar (unchanged from the ratified 0.5 discipline)

A Partial bar is met only when **every clause** below has (a) a named **artifact** that
exists, (b) a named **demonstration** that was actually run, and (c) a named **checker**
who verified it. Per P2, a clause with an artifact but no demonstration, or a
demonstration nobody checked, is an **explicit gap**, never a pass. Per the roadmap's
honesty guard, 0.6 is claimed only when both bars are met, validated, and released.

Checker vocabulary (as in 0.5): **Machine (fail-closed contract)** · **Independent
validator (O5/P6)** · **Founder** (the only checker who can mark a clause *ratified*).

One discipline carried forward from how the 0.5 bars were actually **discharged**
(PROGRAM_0.5 exit, 2026-07-16): the real acts were named artifacts with identities
(`APPROVAL-0001`, `RUN-TRANSFORM-20260716-0002`, `ACCEPTANCE-0001`, `EDR-0001`,
`CHG-20260716-0001`) — not assertions that "a real case was run." Every REAL clause
below must discharge the same way: by naming the identity of the real record it
produced.

---

# Part I — O7 Partial bar (Track A: safe supersession, P14)

**Bar being refined (PROGRAM_0.6, restated):** canonical knowledge can be superseded
safely — replaced by better evidence without denying its historical existence — with
the full chain preserved and every boundary human-decided.

## I.1 The bar as enumerated clauses

**O7-1 — Supersession vehicle ratified and released.** The ratified vehicle (Track-A
workshop ruling: extension of `WF-TRANSFORM-0001`, a distinct workflow, or extended
promotion-tool store semantics — whichever the founder ratifies) is specified under the
frozen workflow-execution discipline (or, if a tool-side vehicle, under an equivalent
documented contract) and reaches its authoritative status before the demonstrating
act. The ruling also fixes **where the current-vs-superseded pointer lives** in
`canonical/decisions/index.yaml` (or a ratified successor structure).

**O7-2 — History semantics enforced: intact, citable, digest-stable.** After a
supersession: (a) the superseded record's **originally promoted bytes remain
byte-identical** — the `record_sha256` pinned at its promotion still verifies against
the stored record content; (b) the record remains **resolvable at its original
identity** and citable; (c) it remains **indexed** — supersession never de-lists;
(d) its *effective* status (`superseded`) is representable **without rewriting the
record's content** — by an appended supersession record, a sidecar, or derived status
(the pattern already proven by `challenge_records.load_challenge`, which derives
`disposed` from the existence of the sibling disposition record and never rewrites
`challenge.yaml`).

**O7-3 — The chain is machine-walkable (P8/P14).** The superseding and superseded
records are linked by explicit, machine-readable `supersedes` / `superseded_by`
references, and a checker can walk the chain **in both directions** — from the current
record back to the original and from the original forward to what replaced it — with
no gap. The supersession record itself binds: the two record identities, the two
record digests, the superseding transformation/promotion run ID (honoring the standing
WF-TRANSFORM reservation that *supersession records the superseding Run ID*), and the
trigger under O7-4.

**O7-4 — Trigger recorded and evidence-bound (P4).** Every supersession record names
which of the **ratified trigger classes** (Track-A ruling over: better evidence ·
upheld-challenge reconsideration obligation · invalidated assumption, the declared
Track-B seam) produced it, and binds the trigger's evidence (for better evidence: the
new evidence artifacts; for an upheld challenge: the disposition record carrying
`reconsideration.required: true`; for the seam: the ratified Track-B obligation
record). A supersession with no recorded trigger, or a trigger with no bound evidence,
is rejected.

**O7-5 — Human authority end-to-end (P7 applied twice, the 0.5 pattern).** The
superseding record enters the canonical store only through **recorded human acts**: a
human approval consumed by the superseding run and a human acceptance answering it,
each verified fail-closed (authority tuple against the current model, byte-binding,
single effective use), with the store write performed by a **human-invoked
deterministic step**. No automation supersedes, fires-and-decides, or accepts. The
superseding record itself meets the **full O3 canonical standard** (evidence, review,
explicit acceptance) — supersession is not a cheaper door into the store.

**O7-6 — One REAL canonical record superseded, chain walkable.** One **real** record
in `canonical/decisions/` (at baseline the only candidate is `EDR-0001`) is superseded
by a real superseding record produced from a genuine run with genuine human acts, and
the discharged clause names the identities: the superseding EDR, its approval and
acceptance records, its run ID, and the supersession record. After the act, an
independent validator walks the real chain both directions and verifies O7-2 (a)–(d)
hold on the real store — not on a fixture. Fixtures are still required (as the
negative/positive contract inputs for O7-2/3/4/5) but **fixtures prove negatives; they
never discharge this clause**.

## I.2 Artifact · demonstration · checker, per clause

| Clause | Artifact that proves it | Demonstration that verifies it | Who checks |
|---|---|---|---|
| O7-1 | The ratified Track-A scope ruling + the vehicle's specification/contract at its authoritative status + the ruled index pointer location | Structural validation of the vehicle (as `WF-TRANSFORM-0001` was validated for O3-1, or the documented-contract equivalent for a tool vehicle); the pointer semantics are inspectable in the store schema | Founder (ratification of vehicle + pointer ruling) + Machine (structural validation) |
| O7-2 | The post-supersession store: superseded record directory + its unchanged `record_sha256` + the appended/sidecar/derived status mechanism | Digest re-verification of the superseded record against its promotion-time `record_sha256`; resolution of the record at its original identity; **negative tests: the contract rejects (i) content rewrite of a superseded record, (ii) deletion of its directory, (iii) removal of its index entry** | Machine (fail-closed contract + digest check) + independent validator (reviews the negatives are on an enforced path) |
| O7-3 | The supersession record (schema ruled at the workshop) carrying `supersedes`/`superseded_by`, both digests, run ID, trigger | A machine chain-walk in both directions with no gap; **negative: a superseding record without the chain reference is rejected ("latest wins" refused by contract)** | Machine (chain-walk contract) + independent validator (walks the real chain, O7-6) |
| O7-4 | The trigger field + bound trigger evidence inside the supersession record | Positive: each ratified trigger class admits with its evidence bound. **Negative: a supersession with no trigger, or trigger evidence that fails its digest/reference check, is rejected (P4)** | Machine (fail-closed contract) + Founder (confirms the real act's trigger is truthful) |
| O7-5 | The superseding approval + acceptance records; the human-invoked promotion/supersession step's refusal list (the `promote.py` discipline extended) | **Negative pair: (i) a supersession attempt with no human approval/acceptance records is refused, nothing written; (ii) an automation-authored approval is refused (mirrors the ratified O3-2 negatives).** Positive: the two real human acts admit the act | Machine (fail-closed refusals) + Founder (the human acts are the Founder's own, as in 0.5) |
| O7-6 | The real superseding EDR + its APPROVAL-*/ACCEPTANCE-* records + its RUN-* + the supersession record binding it to the real superseded record | The live act on the real store; then the independent bidirectional chain-walk and digest re-verification of the superseded record | Machine (contracts) + independent validator (chain-walk) + Founder (confirms the input was real, not synthetic) |

## I.3 Boundary cases — what explicitly does NOT count

1. **A superseded record that is deleted, rewritten, or de-indexed fails P14 even if
   a perfectly good new record exists.** The new record's existence is not the
   obligation; the old record's preserved existence is. *History is preserved; truth
   is revised* — a store where only the revision survives has revised history, not
   truth.
2. **"Latest wins" without a walkable chain fails (O7-3).** A newer EDR answering the
   same engineering question, sitting beside the old one with no machine-readable
   `supersedes`/`superseded_by` binding, is exactly the failure P14 names. Two
   contradictory canonical records with no recorded relationship is *worse* than the
   baseline, not progress past it.
3. **Supersession by automation fails P7 (O7-5).** A workflow, evaluator, or tool that
   writes `superseded` status — or admits a superseding record — without both recorded
   human acts fails, even when the trigger is legitimate. This explicitly covers the
   Track-B seam: an invalidated assumption may *trigger* a supersession obligation; it
   may never *execute* one.
4. **An in-place status flip that breaks digest verifiability fails O7-2.** If marking
   `EDR-0001` superseded rewrites `EDR-0001.md`'s bytes such that the promotion-time
   `record_sha256` no longer verifies, the record has been rewritten in the P14 sense
   regardless of how small the edit is. (This is a live design constraint, not a
   hypothetical — see the baseline table and Part III tension 2.)
5. **A run marked `superseded` is not canonical supersession.** The workflow catalog
   and both released workflow specs already use `superseded` as a **run/spec status**
   ("a newer run replaces this run"). Marking runs or workflow specs superseded — a
   capability that exists today — discharges nothing in this bar, which is about
   **canonical knowledge** records.
6. **A superseding record that skips the O3 standard fails P3 (O7-5).** Supersession
   must not become the cheap path into the store: a superseding record without its own
   evidence/review/explicit-acceptance chain is "canonical by supersession" — the same
   failure mode as canonical-by-existence.
7. **Re-using a spent approval fails single effective use (O7-5).** The 0.5 store is a
   single-effective-use ledger (`promote.py` refuses an approval that already produced
   a canonical record); the superseding record requires its **own** fresh human
   approval and acceptance. `APPROVAL-0001` is spent.
8. **A fixture supersession does not discharge O7-6.** Superseding a fixture record in
   a test store, however complete the chain, satisfies the contract clauses' negative
   and positive tests only. The real clause names real identities in the real store.

## I.4 Partial vs Strong — deliberately OUT of the Partial bar (P13)

- **Full invalidation propagation (O12).** When a superseded record's conclusions were
  consumed downstream, propagating invalidation across dependent reasoning is the 0.7
  milestone, explicitly not this bar.
- **Multi-hop supersession chains under contention.** One real hop
  (record → superseding record) is the bar. Chains of three or more, concurrent
  competing superseders of the same record, and branch/merge semantics of the chain
  are deepening.
- **Automated supersession-candidate detection.** A sweeper that watches evidence and
  *proposes* supersessions is deepening (and is P7-constrained regardless).
- **Supersession of other artifact classes.** The bar covers the ratified narrow
  canonical store (`canonical/decisions/`). EKB guides (background lane B1), workflow
  specs, and the authority model have their own lifecycles; widening is deepening —
  and the 0.5 ruling that the store's definition is narrow stands.
- **Consumer-repo projection of supersession status** (background lane B2's concern).
  The bar lives inside `ecf`; making `context_switcher` see superseded status is
  deepening.
- **Retirement (`retired`) mechanics.** The EDR contract's vocabulary includes
  `retired`; 0.6 exercises `superseded` only. Retirement-without-replacement is
  deepening.

## I.5 Bar-vs-reality baseline (what exists at v0.5.0 = `e19a2e0` vs what 0.6 must add)

| Clause | Exists today (probed evidence) | 0.6 must add |
|---|---|---|
| O7-1 | No vehicle. `promote.py` is append-only by design: it refuses when "the target EDR identity is already taken" and comments "promotion never overwrites the store (P14)"; the index (`canonical/decisions/index.yaml`, schema 0.1.0) is a single-effective-use ledger whose entries carry **no status field and no chain pointers** | The ratified vehicle + the current-vs-superseded pointer ruling + spec/contract at authoritative status |
| O7-2 | The store holds exactly one record: `EDR-0001` (`record_sha256: 2fb71c58…c553`), digest-pinned at promotion. The *vocabulary* exists on paper: `CANONICAL_DECISION_RECORD_CONTRACT.md` declares post-promotion status `canonical \| superseded \| retired` and itself defers "supersession *mechanics* beyond this vocabulary" to 0.6/O7. The derive-don't-rewrite pattern is proven in `challenge_records.py` (`status: disposed` derived from the sibling record, "derived, not rewritten") | The status mechanism that preserves byte-identity + the three fail-closed negatives (rewrite/delete/de-index rejected) |
| O7-3 | `supersedes`/`superseded_by` exist **nowhere** in the store or index. The only reservation is prose in both released workflow specs: "Supersession records the superseding Run ID; the superseded run is retained for audit" — about **runs**, not canonical records | The supersession-record schema, the chain fields, and the bidirectional machine walk |
| O7-4 | Trigger classes exist as raw material only: the upheld-challenge hook is **live in code** (`challenge_records.validate_disposition_record`: an upheld disposition *requires* `reconsideration {required: true, trigger}` — "re-entry, P14") but has **never fired in reality** — the only real disposition, `CHG-20260716-0001`, is `rejected`. The Track-B seam is a declared kickoff ruling, not a mechanism | The ratified trigger classes + the evidence-binding contract |
| O7-5 | The P7-twice pattern is fully live for *first* promotion: `promote.py` "REFUSES unless BOTH human-authored records exist, verify, and byte-bind"; six fail-closed entry checks at approval; acceptance verification; human-invoked deterministic write | Extending the same discipline to the superseding act (fresh approval + acceptance + refusal list) |
| O7-6 | The real target exists: `EDR-0001` is canonical, promoted 2026-07-16 from `RUN-TRANSFORM-20260716-0002`, with its evidence bundle digest-bound. Its own text anticipates re-entry ("close the open blockers … and re-run the subsystem decision"). But `MISS-0001`/`MISS-0002` are both `status: open` (run's `missing-information.yaml`) and **no mechanism exists to close a MISS record** — statuses live only inside the completed run's output in unversioned `runtime/` (see Part III tension 1) | The real superseding chain: whatever real path closes the evidence gap (or another ratified real trigger), a fresh reasoning/transformation chain, and the supersession act |

---

# Part II — O11 Partial bar (Track B: executable assumptions with review triggers, P11)

**Bar being refined (PROGRAM_0.6, restated):** assumptions become first-class,
executable artifacts — declared with confidence, evidence, and review triggers, so
that reality can challenge them. At Partial, "executable" means (PROGRAM_0.6 Track-B
item 3, verbatim direction): *a machine-evaluated trigger produces a recorded, routed
review obligation.*

## II.1 The bar as enumerated clauses

**O11-1 — The assumption record ratified: identity, home, and the P11 triple.** The
Track-B ruling fixes the record's shape, its **platform-unique identity**, and where
it lives (run-bound vs repo-level registry). Whatever is ruled, each record carries
P11's declared triple — a **confidence/evidence-strength** statement, **references to
its evidence**, and **at least one review trigger** — plus **provenance to its
emitting run and task output** (P8). Identity must resolve the baseline collision:
`ASSUME-*` IDs today are task-scoped, and the same ID denotes different assumptions
inside one real run (see II.5).

**O11-2 — Ratified trigger classes, each with a wired evaluator (P2).** For each
trigger class the workshop ratifies (over the design-open menu: evidence-arrival ·
dependency-change · time-based), there is a **machine evaluator that actually runs** —
invocable, tested, and consulted on an enforced path. A trigger class may be ratified
*without* an evaluator only if the records claiming it are marked **non-executable**
(an explicit gap, P2) — a declared trigger with no evaluator recorded as "executable"
fails the clause.

**O11-3 — A firing produces a durable, recorded review obligation.** When an evaluator
determines a trigger's condition holds, it writes a **review-obligation record**
(schema ruled at the workshop) durably bound to: the assumption's identity, the
trigger class, and the **triggering evidence** (what arrived/changed, digest- or
reference-bound). The obligation is a record, not a log line: write-once, dated,
resolvable.

**O11-4 — The obligation is routed to a never-empty accountable recipient
(Clarifications B/C).** The obligation reaches an accountable office via the
**ratified routing** (Track-B design-open 4: whether it rides the O4 challenge
machinery — `route_challenge` over the stewardship ledger — or a parallel mechanism;
either way the ratified properties hold): `effective_recipient` never empty, vacancy
falls back **visibly degraded** to the institutional fallback, and the routing block
is written by the router, never by the evaluator choosing its own reviewer. The
machine **fires and routes; a human reviews and decides** — the evaluator never
disposes the review it created (P7: no automation "fires-and-decides").

**O11-5 — One REAL assumption's trigger actually fires.** One **real** assumption —
extracted with provenance from the real run envelope
(`RUN-REASON-WR0001-V040-0002`'s `ASSUME-0001`/`ASSUME-0002`, both
`evidence_strength: weak` and both keyed to the open blockers MISS-0001/0002) or
freshly declared against a real canonical decision (EDR-0001 is the natural host),
per the ratified extraction path — has its trigger **actually fire on real
evidence**, producing a real recorded, routed review obligation whose identities the
discharged clause names (assumption ID, obligation record, effective recipient).
Fixtures prove the negatives; they never discharge this clause.

**O11-6 — Fail-closed negatives demonstrated.** The contracts reject: a malformed
assumption record (closed field set, the record convention); an "executable" claim
with no wired evaluator (O11-2's negative); an obligation record with an empty or
router-bypassing recipient (O11-4's negative); and a second obligation for the same
(assumption, trigger-event) pair if the ratified semantics are once-per-event
(idempotence per the ruled semantics — no silent duplicate storms). And the negative
of firing itself: an evaluator run against **unchanged** evidence fires nothing —
no false positives manufactured to pass O11-5.

## II.2 Artifact · demonstration · checker, per clause

| Clause | Artifact that proves it | Demonstration that verifies it | Who checks |
|---|---|---|---|
| O11-1 | The ratified assumption-record schema + the registry/home + at least the real extracted/declared records carrying the P11 triple + provenance fields | Schema validation (closed field set, fail-closed); a record missing confidence, evidence refs, a trigger, or run provenance is rejected; identity-uniqueness check across the registry | Founder (shape/home ratification) + Machine (schema contract) |
| O11-2 | The evaluator module(s) per ratified trigger class + their tests + the enforced invocation path | Positive: the evaluator runs and evaluates a known condition. **Negative: a record claiming an unratified/unwired trigger class as executable is rejected (P2)** | Machine (contract + tests) + independent validator (reviews the evaluator is on an enforced path, not decorative — the ratified O4-2 discipline) |
| O11-3 | The review-obligation record schema + a written obligation bound to assumption + trigger + evidence | Positive: a firing writes the obligation with all bindings. **Negative: an obligation not bound to an identified assumption or lacking the triggering evidence reference is rejected (P8)** | Machine (fail-closed contract) + independent validator (bindings resolve) |
| O11-4 | The routing block on the obligation record (recipient, model version, degraded flag) per the ratified routing | Positive: an obligation routes to the accountable office. **Negatives: (i) empty recipient rejected (Clarification B/C); (ii) evaluator-chosen recipient rejected (router-written fields only); (iii) vacancy case routes degraded to the institutional fallback, disclosed** — the proven `route_challenge` semantics, reused or mirrored | Machine (routing contract) + the accountable office (acknowledges receipt) |
| O11-5 | The real assumption record(s) with provenance to `RUN-REASON-WR0001-V040-0002` (or the real fresh declaration) + the real fired obligation + its routing record | The live fire: real evidence arrives/changes, the evaluator is invoked, the obligation exists and reached its recipient; identities named | Machine (contracts) + Founder (confirms the evidence event was real, not staged) + independent validator (walks assumption → trigger → obligation → recipient) |
| O11-6 | The negative-test suite over all four rejection families + the no-false-positive run | Each negative rejects fail-closed; the unchanged-evidence evaluator run produces zero obligations | Machine (fail-closed contracts) + independent validator (negative coverage review) |

## II.3 Boundary cases — what explicitly does NOT count

1. **A trigger with no wired evaluator recorded as "executable" fails P2 (O11-2).**
   Writing `review_trigger: on-evidence-arrival` into a YAML file is a *description*;
   P11's word is *executable*. If no machine can evaluate the condition, the record
   must say so (explicit gap) — descriptive honesty over aspiration, per
   PROGRAM_0.6's own constitutional edge.
2. **A fired trigger without a routed recipient fails Clarification B (O11-4).** An
   obligation written to disk that reaches no accountable office is the review-side
   twin of "a challenge that reaches no accountable recipient is not a challenge."
   Logging is not routing; a dashboard nobody is accountable for is not a recipient.
3. **Bulk-harvesting old `ASSUME-*` rows without provenance to their emitting run
   fails P8 (O11-1).** This is not hypothetical: in the one real run, `ASSUME-0001`
   in `engineering-reasoning-context.yaml` ("ADR-0005 is authoritative", moderate) and
   `ASSUME-0001` in `engineering-recommendation.yaml` ("blockers are resolvable
   bounded-effort", weak) are **different assumptions under the same ID** — and
   `MISS-0002`'s prose cites "ASSUME-0001" ambiguously across that collision. A
   registry built by grepping IDs out of run envelopes without binding each record to
   its emitting run *and task output* imports that ambiguity as corrupted provenance.
4. **A human noticing and filing a review is not a machine-evaluated trigger
   (O11-2/O11-3).** Humans may always initiate review (that path exists since 0.5 as
   a challenge); the bar is that the *machine* evaluates the trigger condition. A
   process document saying "re-check assumptions when evidence arrives" is 0.4-style
   discipline, not enforcement — the same line the ratified O4-2 drew.
5. **An evaluator that fires and also disposes fails P7 (O11-4).** Auto-revalidating
   the assumption, auto-downgrading its confidence *as a decision*, or auto-closing
   the review it opened crosses "no automation fires-and-decides a review." The
   evaluator's writes end at the routed obligation.
6. **A fixture assumption's fire does not discharge O11-5.** A test assumption with a
   test trigger fired by a test event proves the contracts (and is required for
   O11-6); the real clause requires a real assumption, a real evidence event, and a
   real obligation with named identities.
7. **Making the reasoning executable is neither required nor a substitute (P11,
   verbatim boundary).** Executable *reasoning* — re-running the recommendation
   pipeline — does not satisfy any clause here, and no clause may be read to demand
   it. The assumptions are the executable artifact; the reasoning is not required to
   be.

## II.4 Partial vs Strong — deliberately OUT of the Partial bar (P13)

- **Full invalidation propagation (O12, 0.7).** A fired trigger produces a *review
  obligation*; it does not invalidate the assumption, the decision that rests on it,
  or downstream reasoning. Dependency graphs, invalidation states, and
  degraded-reproducibility semantics are the next milestone, explicitly out
  (PROGRAM_0.6 Track-B item 3 says exactly this).
- **Time-based trigger scheduling infrastructure.** If the time-based class is
  ratified, Partial requires at most evaluation-on-invocation (the check runs when
  called and fires if the deadline passed). Daemons, cron wiring, and guaranteed
  evaluation latency are deepening. *(If the workshop ratifies only
  evidence-arrival/dependency-change, this row is moot — the bar does not force the
  time class in.)*
- **Retroactive harvest of all historical runs.** The bar requires the real records
  it names; a complete backfill of every `ASSUME-*` ever emitted (with the P8 rigor
  exclusion II.3-3 demands) is deepening.
- **Review-disposition machinery beyond routing.** The obligation must *reach* an
  accountable recipient; SLAs, disposition schemas for the review itself, and
  escalation-on-silence are deepening (the review's outcome, if it invalidates the
  assumption, re-enters as the Track-A seam — reconciled at integration per the
  kickoff ruling, not barred here).
- **Cross-repo assumption visibility** (`context_switcher` projection). Inside `ecf`
  is the bar.
- **Automated confidence recalculation.** Machines evaluate *trigger conditions*;
  judging what new evidence does to confidence remains with the human reviewer.

## II.5 Bar-vs-reality baseline (what exists at v0.5.0 = `e19a2e0` vs what 0.6 must add)

| Clause | Exists today (probed evidence) | 0.6 must add |
|---|---|---|
| O11-1 | Assumptions exist **only inside run envelopes**: `engineering-recommendation.yaml` carries `ASSUME-0001`/`ASSUME-0002` with exactly `{id, statement, evidence_strength}` — no confidence beyond that one field, **no evidence references, no review triggers, no registry, no platform identity**. IDs are task-scoped and collide within the single real run (II.3-3). The material sits in unversioned, mortal `runtime/` — durable only where EDR-0001's digest-bound evidence bundle copied it | The record schema, unique identity, ratified home, the P11 triple, and the provenance-carrying extraction (or fresh-declaration) path |
| O11-2 | **No trigger evaluator exists anywhere.** A repo-wide probe finds "trigger" in exactly one mechanism: `challenge_records.py`'s `reconsideration.trigger` field on upheld dispositions — a recorded *obligation string*, evaluated by nothing | Every ratified class's evaluator, tests, and enforced invocation path |
| O11-3 | No obligation record or schema. The nearest durable-record patterns to imitate are proven: write-once challenge/disposition records with closed field sets, JSON-envelope convention | The obligation schema + write-once persistence + bindings |
| O11-4 | The routing machinery O11 could reuse is **live and tested**: `route_challenge` over `role_state.StewardshipLedger` — `effective_recipient` never empty (`accountability` or `founder_genesis`), vacancy passes visibly degraded with disclosed escalation, spurious escalation claims rejected (P2), router-written fields enforced. Authority model at `MODEL_VERSION = "0.2.0"` | The ratified routing ruling (reuse vs mirror) + the obligation-side recipient/authority contract |
| O11-5 | The real raw material exists and is well-chosen by reality itself: `ASSUME-0001`/`0002` (both `weak`) are premised on exactly the evidence gaps `MISS-0001`/`MISS-0002` (both `open`, classification `blocker`) — an evidence-arrival trigger keyed to their closure is the natural real fire, and it is the same event PROGRAM_0.6 flags as O7's natural first target (the declared seam, from the other side). **But no MISS lifecycle exists** — see Part III tension 1 | The real record(s), the real trigger wiring, and the real evidence event that fires it |
| O11-6 | Nothing assumption-specific; the fail-closed negative-test discipline is the house style (promotion refusal list; challenge/disposition rejection suites) | The four rejection families + the no-false-positive demonstration |

---

# Part III — Cross-consistency check (both bars vs PROGRAM_0.6's constitutional edges and the ratified 0.5 bars)

1. **P14 edge honored, and made testable.** "Superseded is never deleted, never
   rewritten; 'latest wins' is unconstitutional; every supersession preserves the full
   chain" maps clause-for-clause: never deleted/de-indexed → O7-2(b)(c) + boundary
   I.3-1; never rewritten → O7-2(a) digest-stability + I.3-4; latest-wins → O7-3 +
   I.3-2; full chain → O7-3 bidirectional walk. **Consistent** — the bar adds the
   *checkable form* of the edge (digest re-verification), not a reinterpretation.
2. **P7 edge honored on both tracks.** "No automation supersedes canonical knowledge,
   fires-and-decides a review, or accepts a superseding record" → O7-5 (human acts
   twice, human-invoked write, refusal list) and O11-4/II.3-5 (evaluator fires and
   routes; never disposes). The seam is stated in both directions: an invalidated
   assumption may trigger, never execute, a supersession (I.3-3). **Consistent.**
3. **P11/P2 edges are the point of the O11 clauses.** P11's verbatim boundary is
   boundary case II.3-7; P2's "a trigger that cannot actually fire must not be
   recorded as executable" is O11-2 and II.3-1 word-for-word. **Consistent.**
4. **The ratified 0.5 bars are not contradicted.** Single effective use survives
   (I.3-7: the superseding record needs fresh human acts; `APPROVAL-0001` stays
   spent). One-disposition-ever survives (reconsideration re-enters as a *new*
   challenge — `challenge_records` already enforces this; O7-4 consumes the
   reconsideration obligation, it never reopens the disposition). The narrow
   canonical-store definition survives (I.4: no widening of artifact classes). The
   O4 routing properties are reused, not weakened (O11-4 requires the same
   never-empty/degraded-disclosure semantics whichever routing is ratified).
   **Consistent.**
5. **Tension 1 (flagged, not resolved here) — the charter's natural first target
   rests on a lifecycle that does not exist.** PROGRAM_0.6 names `EDR-0001`
   "superseded by the re-run subsystem decision **once MISS-0001/0002 close**" — and
   O11-5's natural real fire is the same closure event. But at v0.5.0, MISS statuses
   live *only* inside the completed run's `missing-information.yaml` in unversioned
   `runtime/` (copied read-only into EDR-0001's evidence bundle); **no mechanism,
   registry, or record type can close a MISS item**, and no 0.6 track owns creating
   one. The bars above are written so this does not silently block the exit: O7-6
   admits *any* ratified real trigger, and O11-5's evidence-arrival fire needs a real
   evidence event, not specifically a MISS-status flip. But if the founder wants the
   charter's named target discharged as written, **some track must be assigned the
   MISS-closure mechanism** (or the closure must be ruled to be itself an
   evidence-arrival record rather than a status mutation of an immutable run output —
   which would also respect the 0.5 run-evidence-permanence deferral that FD-2 is
   weighing).
6. **Tension 2 (flagged, design-constraining) — the EDR contract's status vocabulary
   collides with the digest-pinned store.** `CANONICAL_DECISION_RECORD_CONTRACT.md`
   says the record's post-promotion status *becomes* `superseded`, and status today
   lives in the record's front matter; but the write-once index pins
   `record_sha256` over those exact bytes, and `promote.py` never rewrites the store.
   An in-place front-matter flip would break digest verification (I.3-4). The
   derive-don't-rewrite pattern (`load_challenge`: "derived, not rewritten") shows the
   constitutionally clean resolution, and O7-2(d) is written to require *that
   property* without dictating the mechanism — but the Track-A workshop must rule the
   mechanism explicitly, or the contract's own words will steer the build into the
   P14 violation the bar rejects. A sequencing cost, resolvable; flagged so it is
   ruled, not stumbled into.
7. **Tension 3 (flagged, honesty-guarding) — the P14 re-entry hook has never fired in
   reality.** The upheld-challenge → mandatory-reconsideration mechanism is live in
   code, but the only real disposition (`CHG-20260716-0001`) is `rejected`; no real
   reconsideration obligation exists, and one cannot be manufactured honestly (P2) —
   a challenge filed in order to be upheld is a fixture wearing a costume. The bars
   therefore do **not** require the upheld-challenge trigger class for the real acts
   (O7-6/O11-5): it is exercised by fixture negatives/positives under O7-4, and the
   real supersession may ride better-evidence (or the seam). If a genuine upheld
   challenge arrives during 0.6, it may of course serve — reality outranks the plan.
8. **Ordering note (the 0.5 pattern repeats).** As in the ratified 0.5 bars, the real
   acts are strictly ordered behind the vehicles: O7-6 cannot precede O7-1's release
   (only authoritative vehicles act on the real store), and O11-5 cannot precede
   O11-1/O11-2. The schedule absorbs a spec/ladder traversal before each single
   demonstrating act. A sequencing cost, not a contradiction.

---

## Metadata

| Field | Value |
|---|---|
| Status | **RATIFIED (Founder, 2026-07-16)** — the 0.6 exit criteria |
| Owner Role | Program Steward (WS-0) |
| Change class | T1 Operational |
| Derives from | [PROGRAM_0.6](PROGRAM_0.6.md) · [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md) 0.6.0 · [PLATFORM_PRINCIPLES](PLATFORM_PRINCIPLES.md) (P2, P3, P4, P7, P8, P11, P13, P14, Clarifications B/C) |
| Evidence probed | `ecf` worktree `chore/0.6-partial-bars` @ `e19a2e0` (v0.5.0): `canonical/decisions/{index.yaml, EDR-0001/}`, `artifacts/CANONICAL_DECISION_RECORD_CONTRACT.md`, `tools/canonical_promotion/promote.py`, `tools/authority_rule/{challenge_records.py, check_stewardship.py, authority_model.py}`, `challenges/CHG-20260716-0001/{challenge.yaml, disposition.yaml}`, `approvals/`, `workflows/{WORKFLOW_CATALOG.md, WORKFLOW_EXECUTION_SPECIFICATION.md, transformation/WF-TRANSFORM-0001-*.md}` · main checkout (read-only): `runtime/runs/RUN-REASON-WR0001-V040-0002/task_outputs/{engineering-recommendation.yaml, engineering-reasoning-context.yaml, missing-information.yaml}` |
| Cross references | [PROPOSAL_05_PARTIAL_BARS](PROPOSAL_05_PARTIAL_BARS.md) (bar precedent, ratified) · [PROGRAM_0.5](PROGRAM_0.5.md) (exit discipline) · [PLATFORM_ARCHITECTURE](PLATFORM_ARCHITECTURE.md) (FD-2, parametric) |
