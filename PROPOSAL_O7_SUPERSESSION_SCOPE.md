# PROPOSAL_O7_SUPERSESSION_SCOPE — Track A (O7) scope resolution for 0.6.0

> **Status: RATIFIED (Founder, 2026-07-16)** — including the derive-don't-rewrite
> reading (superseded record bytes never change; effective status derives from the
> store chain). Non-constitutional (T1 working
> proposal that organizes delivery of a ratified capability). This document does
> **not** ratify anything — it resolves the Track A *design-open* items from
> [PROGRAM_0.6](PROGRAM_0.6.md) as **options + one recommendation** per item,
> mirroring the 0.5 precedent ([PROPOSAL_O3_TRANSFORM_SCOPE](PROPOSAL_O3_TRANSFORM_SCOPE.md),
> ratified 2026-07-16). The founder rules; then Track A builds.
>
> Obligation: **O7 — safe supersession of canonical knowledge (P14, depends on
> O3 ✓).** P14 is inviolable throughout: *history is preserved; truth is
> revised.* Nothing proposed here rewrites, deletes, or de-cites a superseded
> record, and nothing here lets automation supersede anything (P7).

---

## 0. What is already true (findings, not proposals)

Nine facts from the real 0.5 surfaces (worktree `ecf-wt-o7`, branch
`feature/0.6-o7-supersession` @ develop `e19a2e0` = v0.5.0) anchor every
recommendation below.

1. **The store is real and has one entry.** `canonical/decisions/index.yaml`
   (schema `0.1.0`) carries exactly one entry: `EDR-0001`, keyed by
   `edr_id` and carrying `approval_id`, `acceptance_id`,
   `transformation_run_id`, `source_run_id`, `work_request_id`,
   `record_sha256`, `accepted_candidate_sha256`, `accepted_by`, `granted_at`.
   **There is no `status` field and no pointer field of any kind** — the index
   is a flat single-effective-use ledger, and both O3 docs describe it as
   write-once ("entries are never deleted", `canonical/README.md`).

2. **The index pins the promoted record's exact bytes.**
   `record_sha256: 2fb71c5…` is the digest of `EDR-0001/EDR-0001.md` *as
   promoted*. Any later mutation of that file — including a well-meaning
   front-matter status flip — breaks the ledger's own integrity pin. This
   single fact constrains Item 3 more than any preference.

3. **Byte-minimalism at promotion is the established discipline.**
   `tools/canonical_promotion/promote.py` rewrites **exactly** the defined
   front-matter status fields (`_FM_REWRITES`, each pattern must match exactly
   once or promotion refuses) and records both the accepted-candidate digest
   and the promoted digest. Consequence visible in the real record: promoted
   `EDR-0001.md` has `status: canonical` in front matter while its body still
   reads, verbatim, "Candidate EDR-0001 … This record's status is `candidate`
   … it is **not** canonical." The store already relies on *store context*,
   not on re-editing prose, to express post-promotion truth.

4. **Derived status is already the ratified corrigibility idiom.** The
   challenge system (`tools/authority_rule/challenge_records.py`,
   `load_challenge`) never rewrites `challenge.yaml`: *disposed-ness is the
   existence of the indelible sibling `disposition.yaml`* — "derived, not
   rewritten". One disposition per challenge, ever; "changing an outcome means
   a NEW challenge re-entering the cycle, the ratified
   corrigibility-by-re-entry clause."

5. **The upheld-challenge reconsideration hook exists and is enforced, but has
   never fired.** `validate_disposition_record` rejects any `upheld` /
   `upheld_with_constraints` disposition lacking
   `reconsideration: {required: true, trigger: …}` (P14 re-entry). The one
   real disposition on file (`challenges/CHG-20260716-0001/disposition.yaml`,
   against EDR-0001 itself) is `rejected`, so **no live reconsideration
   obligation exists today** — the hook is a proven contract with zero live
   instances. P2 honesty: the trigger class is real; a fired trigger is not.

6. **The promotion tool is the store's only writer and already refuses
   overwrites.** `_check_store_free` refuses when the approval was already
   used (single effective use), when the EDR identity is taken, and when
   `canonical/decisions/<EDR-ID>/` already exists — "promotion never
   overwrites the store (P14)". `mkdir(…, exist_ok=False)` makes the
   no-overwrite refusal structural, not advisory. O7 extends a refusal matrix
   that is already fail-closed; it does not invent one.

7. **Single effective use is a ledger fact, checked twice.** Entry check
   ENTRY-06 (`tools/decision_records/decision_records.py`,
   `check_single_effective_use`) and the promotion tool both reject a second
   accepted canonicalization from the same `approval_id`. APPROVAL-0001 is
   permanently consumed by EDR-0001; nothing in this proposal un-consumes it.

8. **WF-TRANSFORM-0001's supersession reservation is about *runs*, not
   records.** The released workflow's states include `superseded` ("a newer
   run replaces this run") and its closing section says "Supersession records
   the superseding Run ID; the superseded run is retained for audit." The
   catalog ladder likewise defines a `superseded` **workflow** status
   ("retained for audit, not selected for new runs"). The EDR contract
   reserves the **record**-level vocabulary — `canonical | superseded |
   retired` — and explicitly defers mechanics to 0.6/O7. O7's job is to give
   the record-level word the same discipline the run-level word already has:
   *the superseding thing records what it replaces; the replaced thing is
   retained, unmodified, for audit.*

9. **The named first target is real but expensive.** EDR-0001 canonicalizes
   `gather_additional_evidence`: "close MISS-0001 and MISS-0002 and re-run the
   subsystem decision against a completed evidence base." The bundled report
   defines both blockers precisely — MISS-0001: *evidence that repository
   responsibilities have independent change-drivers*; MISS-0002:
   *authoritative confirmation of the canonical subsystem model (ADR-0005)* —
   both `open`, both consumer-repo (`context_switcher`) evidence work. The
   superseding decision requires a **fresh 18-task WF-REASON-0001 run**, a new
   approval, a new transformation run, and a new acceptance before any
   supersession can be real. (Closed schemas note: both human-record shapes
   and the challenge/disposition shapes are **closed field sets** that reject
   stray keys — every field added below is a schema bump, never a silent
   widening.)

---

## Item 1 — The supersession vehicle

**Question.** Extend WF-TRANSFORM-0001, a distinct workflow, or promotion-tool
store semantics — and where "current vs superseded" lives in the index.

### 1a — The vehicle

| Option | Shape | Pros | Cons |
|---|---|---|---|
| **V1 — WF-TRANSFORM-0001 extended (0.2.0, additive) + promotion-tool supersede mode** *(recommended)* | The superseding EDR is produced by the same released transformation workflow (a new approval of a new reasoning run, exactly as EDR-0001 was); the workflow additionally **carries a supersession intent through the chain** (approval → candidate front matter → validation → acceptance); supersession itself is executed as **store semantics of the human-invoked promotion step** | The superseding record needs the full P3 triple anyway — that IS WF-TRANSFORM-0001; the candidate *states what it replaces*, so the independent validator (P6) can check the claim and the accepting human reads it (P2); the store's only writer stays the only writer (finding 6); minimal delta (front-matter fields + one promotion mode) | Workflow version bump (0.1.0 → 0.2.0) with a compatibility note; the intent must be equality-checked at every hop (the entry-check idiom, already proven) |
| V2 — Distinct workflow WF-SUPERSEDE-0001 | A new transformation-family workflow dedicated to supersession | Clean conceptual separation | Duplicates the eight-task pipeline to add, in substance, three front-matter fields and one promotion mode — the textbook P13 failure; two workflows to keep synchronized; the catalog gains a workflow whose removal would not reduce quality |
| V3 — Promotion-tool semantics only (workflow untouched) | The workflow knows nothing of supersession; the acceptance record alone names the target; the tool writes the chain | Smallest possible code delta; zero workflow changes | The candidate never states what it replaces, so the independent validator cannot check the supersession claim (P6 gap) and the accepted bytes are silent about the record's most consequential effect (P2 gap); the intent appears for the first time in the second human act, weakening "P7 twice" to "P7 once, plus a flag" |

**Recommendation: V1.** The superseding transformation run is an ordinary
WF-TRANSFORM-0001 run whose approval carries a supersession intent; the
candidate renders it; the validator checks it; the acceptance confirms it; the
promotion tool executes it. No task is added; the eight-task graph, entry gate,
and halt at `waiting_for_human_acceptance` are unchanged. Supersession is a
**promotion-time store act**, exactly as canonicalization already is.

### 1b — Where "current vs superseded" lives (the index's real shape constrains this)

| Option | Mechanism | Pros | Cons |
|---|---|---|---|
| X1 — Mutate the superseded entry | Add `status: superseded` / `superseded_by:` to the *existing* EDR-0001 index entry at supersession | One place to look | **Violates the write-once ledger discipline** (finding 1: entries are never deleted — or edited; the ledger is the single-effective-use proof and must stay append-only); invites the exact "latest wins" mutation habit P14 forecloses |
| **X2 — Chain field on the NEW entry; current-ness derived** *(recommended)* | The superseding entry (schema `0.2.0`) carries `supersedes: EDR-0001` (+ `supersession_grounds`). `superseded_by` is **derived** by reverse walk; **current** is derived: *an EDR is current iff no entry's `supersedes` names it* | Append-only preserved — old entries are byte-identical after supersession; both directions machine-walkable from one index scan (P8); mirrors the ratified derived-status idiom (finding 4: disposed-ness is the existence of the sibling record) | Consumers must resolve through the index (or the resolver tool, Appendix) rather than trusting a record's own front matter — addressed by the marker below and Item 3 |
| X3 — Separate supersessions ledger (`canonical/decisions/supersessions.yaml`) | A second file listing supersession edges | Index untouched entirely | A second source of truth beside the ledger that already records every promotion; two files to keep atomic; P13 |

**Recommendation: X2**, plus one **directory-local marker** for legibility
(P2): at supersede-promotion the tool also writes
`canonical/decisions/EDR-0001/superseded-by.yaml` — a new, write-once sibling
file (never a modification of `EDR-0001.md` or its evidence) recording
`{superseded_by, supersedes_entry, acceptance_id, approval_id, grounds,
granted_at, superseding_record_sha256}`. This is the challenge system's
sibling-record pattern applied to the store: the superseded directory *gains*
its status change as a new indelible record; nothing in it is edited. The
index remains authoritative; the marker is a projection written in the same
tool invocation.

---

## Item 2 — The supersession triggers

**Question.** Better evidence, an upheld challenge's reconsideration
obligation, an invalidated assumption (Track B seam) — what may initiate
supersession, and how is the seam designed without depending on Track B?

**Non-negotiable framing (P7).** A trigger never supersedes. A trigger — of
any class — creates at most a **recorded obligation to reconsider**; humans
decide whether reconsideration culminates in a superseding decision, and only
the two-human-record chain of Item 4 can execute it. (Constitutional edge, and
P2: a "trigger" with no evaluator wired must not be recorded as executable.)

| Option | Trigger classes admitted at 0.6 | Pros | Cons |
|---|---|---|---|
| G1 — Better evidence only | P14's own words, nothing else | Smallest | Ignores the reconsideration hook 0.5 already built and enforced (finding 5) — the one trigger class with live machinery would be the one excluded; the Track B seam the kickoff ruling *requires* would go undesigned |
| **G2 — Three grounds, one interface** *(recommended)* | `better_evidence` \| `upheld_challenge_reconsideration` \| `invalidated_assumption`, each a **typed grounds entry** on the supersession intent, each requiring a resolvable reference | All three charter classes admitted with honest asymmetry (below); one closed vocabulary, fail-closed on anything else; the Track B seam is an ID-string interface, not a dependency | The `invalidated_assumption` class ships as interface-only at 0.6 Partial (evaluator is Track B's O11; propagation is O12/0.7) — must be stated as an explicit gap, not implied capability |
| G3 — Free-text grounds | Human writes why | Zero schema | Unfalsifiable grounds — P4 (evidence over opinion) and the OUTPUT-DISCIPLINE lesson both argue for closed vocabularies; a machine cannot refuse a missing reference it cannot recognize |

**Recommendation: G2.** The supersession intent (Item 4) carries:

```yaml
supersedes:
  edr_id: EDR-0001
  grounds: better_evidence            # closed: better_evidence |
                                      #   upheld_challenge_reconsideration |
                                      #   invalidated_assumption
  grounds_ref: RUN-REASON-<...>       # typed by grounds (fail closed):
                                      #   better_evidence          → the new source run ID
                                      #   upheld_challenge_…       → CHG-<date>-<seq> whose
                                      #                              disposition is upheld*
                                      #   invalidated_assumption   → ASSUME-<...> reference
```

Fail-closed reference checks per class: `better_evidence` — the ref **is** the
superseding chain's own source run (verified anyway by the entry gate);
`upheld_challenge_reconsideration` — the referenced challenge exists, targets
the superseded EDR, and its disposition is `upheld`/`upheld_with_constraints`
with the mandatory `reconsideration` block (finding 5's contract is the
verifier — nothing new to build there); `invalidated_assumption` — at 0.6 the
ref is a recorded assumption identifier **and the check is existence-only**;
what fires it is Track B's business. **The seam is the record shape, not Track
B's machinery**: whatever O11 ratifies for assumption identity, this field
consumes an ID string, reconciled at integration per the founder's kickoff
ruling 1. No Track A deliverable waits on Track B.

Honest asymmetry to record in the proposal itself (P2): at 0.6 Partial,
`better_evidence` will have a real instance (Item 5),
`upheld_challenge_reconsideration` has a proven contract and no live instance,
and `invalidated_assumption` is interface-only. The bar (Part: Partial bar)
demands reality only of the first.

---

## Item 3 — History semantics

**Question.** Superseded records intact and citable; the chain machine-walkable
(P8); what "current" means for consumers.

### 3a — What happens to the superseded record's bytes

| Option | Mechanism | Pros | Cons |
|---|---|---|---|
| H1 — Controlled front-matter flip | Mirror promotion: rewrite `status: canonical → superseded` in `EDR-0001.md`, exactly-once patterns, record pre/post digests in the ledger | The record's own front matter stays truthful; promotion precedent exists (finding 3) | **Breaks the ledger's standing digest pin** (finding 2: `record_sha256` pins the promoted bytes; a flip forces a mutable-digest discipline onto a store whose whole value is byte-stability); every past citation that pinned the digest goes stale; the promotion-flip precedent is candidate→canonical (pre-store), not a mutation of a record *already in the store* — extending it crosses the line P14 draws |
| **H2 — Bytes immutable; status derived; sibling marker** *(recommended)* | `EDR-0001.md` and its evidence bundle are **never touched again after promotion**. Effective status is derived from the index chain (Item 1b/X2); the write-once `superseded-by.yaml` sibling gives directory-local legibility | "Intact and citable" is *literal*: post-supersession, `sha256(EDR-0001.md) == index.record_sha256` is a machine-checkable invariant (bar clause O7-6); existing citations — including CHG-20260716-0001's evidence refs into EDR-0001 — never dangle; the derived-status idiom is already ratified (finding 4); the real promoted record already demonstrates that front matter is status-at-promotion, not live status (finding 3) | The front-matter `status: canonical` of a superseded record becomes historically true rather than currently true — requires one honest contract clarification (below), ruled by the founder |
| H3 — Move superseded records to an archive path | `canonical/superseded/EDR-0001/` | "Current" is a directory listing | **Rejected outright**: de-citing by relocation — every existing reference (`canonical/decisions/EDR-0001/…`, in the disposition record, in platform docs) breaks; P14 says superseded is never deleted *or rewritten*, and a moved path is a rewritten address |

**Recommendation: H2**, with one contract clarification for the founder to
ratify: `CANONICAL_DECISION_RECORD_CONTRACT.md` 0.2.0 states that front-matter
`status:` records **status-as-promoted** and that a record's **effective**
status is `superseded` iff the store chain says so (index `supersedes` edge +
sibling marker), `retired` likewise (retirement mechanics stay out of 0.6
scope), else `canonical`. This is a clarification of what 0.5 already built —
the promoted record's body/front-matter divergence (finding 3) shows the store
was never designed for prose re-editing — not a weakening of the vocabulary.

### 3b — The chain, and what "current" means

- **Chain (P8, machine-walkable both ways).** `supersedes` lives on the
  superseding index entry and in the superseding record's front matter;
  `superseded_by` is derived (reverse index walk) and materialized in the
  sibling marker. Chains may be arbitrary length (EDR-0001 ← EDR-0002 ←
  EDR-0007…); each hop carries grounds + both human-record IDs.
- **Chain integrity rules (fail closed, enforced by the promotion tool and the
  resolver):** no self-supersession; the target must exist in the index; **only
  a current record may be superseded** (no forks: superseding an
  already-superseded record is refused — reconsidering a settled question means
  superseding the *head* of its chain); a dangling or cyclic `supersedes`
  reference makes the resolver refuse, never guess.
- **"Current", defined for consumers:** *an EDR is current iff it appears in
  the index and no index entry's `supersedes` names it.* Consumers (including
  the B2 consumer-repo projection) must resolve currency through the store —
  never through a record's own front matter. A superseded record remains
  **citable forever**: existing citations stand as recorded (P14/P9 — history
  is history); *new* citations of a superseded record are legitimate for
  provenance and audit but must be knowing — the resolver returns
  `{status: superseded, superseded_by: …, grounds: …}` so no consumer can
  read a superseded record as current by accident (P2).
- **Nothing is de-cited.** The superseded record keeps its evidence bundle,
  its ledger entry, its digests, and its place in every chain that ever cited
  it. The superseding record must cite its predecessor (the `supersedes`
  front-matter field is contract-required in a superseding candidate), so the
  chain is walkable from either end starting at either record.

---

## Item 4 — Authority: the full human chain (P7 twice, as O3 did)

**Question.** What records, what fail-closed checks, and what the superseding
chain consumes given the old approval is spent.

### 4a — The records

| Option | Human records for one supersession | Pros | Cons |
|---|---|---|---|
| A1 — A third record type (SUPERSESSION-NNNN) | New approval + new acceptance + a dedicated human supersession record | Maximum explicitness | A third human signature for one decision fails P13 unless it adds a check the other two cannot carry — and it cannot: the acceptance already byte-binds the candidate that names the target, and the approval already ratifies the superseding judgment. Three records also blur *which* act conferred the supersession (P5 wants the roles distinct, not multiplied) |
| **A2 — The existing two human acts, each extended to name the supersession** *(recommended)* | `APPROVAL_RECORD` 0.2.0: optional `supersedes` block (Item 2 shape) — required when the approved recommendation replaces a canonical decision. `ACCEPTANCE_RECORD` 0.2.0: the same block, **required in supersede mode**, equality-checked against the approval's and the candidate's | Exactly O3's construction, extended: two human acts, both *knowingly* naming what is replaced; the intent flows approval → candidate front matter → validation → acceptance → promotion with field-equality checks at every hop (the proven entry-check idiom); closed schemas mean the new blocks are honest version bumps (finding 9), never silent widening | Both record schemas bump to 0.2.0 — needs a compatibility note (the third exercise of O10's semantics): APPROVAL-0001/ACCEPTANCE-0001 at 0.1.0 remain valid **as recorded** (P14/P9), exactly as the authority-model 0.1.0→0.2.0 note ruled for runs |
| A3 — Acceptance-only supersession | Approval unchanged; the acceptance alone names the target | One schema bump | The first human act would ratify a superseding judgment without stating it supersedes — "P7 twice" degrades to once-and-a-half; the validator could not check the candidate's supersession claim against anything human-authored upstream |

**Recommendation: A2.**

### 4b — What the superseding chain consumes

The old approval (APPROVAL-0001) is **spent forever** — single effective use
is a permanent ledger fact (finding 7), and supersession does not un-consume,
re-open, or invalidate it: it remains the standing authority *for the
historical record*, which is precisely what P14 preserves. The superseding
chain consumes:

1. **Its own fresh approval** — a new human approval of the new reasoning
   run's recommendation, carrying the `supersedes` intent; it enters the
   ledger with its own single-effective-use entry, subject to ENTRY-06
   unchanged.
2. **Its own fresh acceptance** — the second human act, byte-binding the
   superseding candidate that names the target.
3. **The reconsideration obligation, when one exists** — if the grounds are
   `upheld_challenge_reconsideration` (or, post-Track-B,
   `invalidated_assumption`), the supersession **discharges** the referenced
   obligation: the supersession records which obligation it answers
   (`grounds_ref`), and the obligation is thereby closed *by reference* — the
   challenge/disposition records themselves are never touched (they are
   write-once; finding 4). At 0.6 Partial the discharge is recorded, not
   ledger-enforced (no obligation registry exists yet — Track B/O11
   territory; stated as an explicit seam, P2).

Symmetry worth stating for the founder: canonicalization consumes one approval
per record; supersession consumes one *new* approval per superseding record
**plus, at most once, one reconsideration obligation**. Nothing human-authored
is ever consumed twice, and nothing consumed is ever handed back.

### 4c — The fail-closed refusal matrix (supersede mode; extends finding 6's)

Promotion in supersede mode refuses (exit 1, nothing written) when — in
addition to every existing refusal (both human records verified, digests,
authority tuples under the current model, store-free identity, single
effective use):

1. the target `edr_id` is absent from the index or its directory is missing;
2. the target is **not current** (already superseded — no forks) or equals
   the new record (self-supersession);
3. the `supersedes` blocks of approval, candidate front matter, and acceptance
   are not field-identical (identity-chain idiom);
4. `grounds` is outside the closed vocabulary, or `grounds_ref` is missing or
   fails its class check (Item 2);
5. the superseded record's bytes would change: the tool never opens the target
   record or its evidence for writing, and it **verifies before and after**
   that `sha256(target EDR .md) == the target's ledger `record_sha256`` —
   a tamper discovered at supersession time refuses the supersession;
6. the sibling marker already exists (write-once), or the index entry it
   would append already exists.

And the standing prohibitions extend verbatim: the workflow never writes
`canonical/` in any mode; no automation authors, amends, or infers an
approval, an acceptance, or a supersession intent; the absence of a "no" is
never a "yes".

---

## Item 5 — The first real target, evaluated honestly

**The charter's flag:** EDR-0001, superseded by the re-run subsystem decision
once MISS-0001/0002 close — the exact re-entry its own statement anticipates
("close MISS-0001 and MISS-0002 and re-run the subsystem decision against a
completed evidence base").

**What closing them actually takes (finding 9):**

- **MISS-0001** — *evidence that repository responsibilities have independent
  change-drivers*: real analytical work in `context_switcher` (change-history
  / responsibility analysis of the repository-integration surface), producing
  citable evidence artifacts. Days, not hours; the work is engineering, not
  ceremony.
- **MISS-0002** — *authoritative confirmation of the canonical subsystem model
  (ADR-0005)*: a consumer-repo governance act confirming (or amending) the
  subsystem model the question is asked against. This is a human decision in
  the consumer repo, not a Control-Plane artifact.
- **Then the full 0.5 chain, again, end-to-end:** a fresh 18-task
  WF-REASON-0001 run on the completed evidence base → a new human approval
  (carrying the `supersedes` intent) → a WF-TRANSFORM-0001 (0.2.0) run →
  independent validation → a new human acceptance → supersede-promotion →
  EDR-0002 current, EDR-0001 superseded with the chain intact.

**Can a Partial-bar-worthy supersession be real without it?** The honest
answer is **no** — and the 0.5 bar discipline already settles why. The store
contains exactly one canonical record; there is no other real supersession
target, and the ratified boundary-case rule ("a synthetic or fixture approval
does not count as one real approved recommendation") transfers directly: **a
fixture supersession — superseding a record nobody canonicalized for real, on
evidence nobody gathered — is the P3 failure mode wearing O7's clothes.**
Worse, superseding EDR-0001 *without* closing MISS-0001/0002 would
canonicalize a "better evidence" claim with no better evidence — a P4 and P2
violation the bar's own negative tests should refuse.

| Option | Pros | Cons |
|---|---|---|
| **F1 — EDR-0001 → EDR-0002 via the real re-run; MISS closure inside 0.6 Track A scope** *(recommended)* | The one honest target; exercises every mechanism this proposal designs (better-evidence grounds, chain, two extended human records, supersede-promotion); the re-run is exactly what the canonical decision itself ordered — 0.6 executes the platform's first canonical decision, which is the best possible evidence the store means something | The long pole of 0.6: consumer-repo evidence work + a governance confirmation + two full runs precede the single demonstrating supersession (the same strictly-ordered sequencing cost the 0.5 bars absorbed for release-before-run) |
| F2 — Reduced bar: mechanics + fail-closed negatives real; the one real supersession explicitly deferred | Decouples O7's machinery from consumer-repo schedule risk | An O7 "Partial" with zero real supersessions is specification, not capability — the exact "spec-complete vs runtime-live" line 0.4/0.5 refused to blur; if ruled anyway, P2/Clarification A demands the gap be recorded as an explicit unmet clause, never a pass |
| F3 — Manufacture a second canonical record in 0.6 just to supersede it | A real store entry as target | The record would exist *in order to be superseded* — canonicalization as test fixture; violates the spirit of finding 6's ledger and the "real, not synthetic" boundary case; P13 |

**Recommendation: F1**, with the sequencing stated plainly in the program:
MISS-0001/0002 closure and the WF-REASON re-run are **on Track A's critical
path**, and the founder should treat them as the milestone's schedule risk
(they are consumer-repo work the Control Plane cannot do to itself). If the
founder rules F2 instead, the bar below marks clause O7-3 explicitly unmet at
exit — a recorded gap, not a redefinition.

---

## The proposed O7 Partial bar (for the Bars thread; PROPOSED, not ratified)

Following the ratified bar discipline: every clause needs a named artifact, a
named demonstration actually run, and a named checker; a clause missing any of
the three is an explicit gap, never a pass.

**O7-1 — Supersession semantics specified and released.** The four contract
deltas exist and traverse to authoritative status: `APPROVAL_RECORD` 0.2.0 and
`ACCEPTANCE_RECORD` 0.2.0 (the `supersedes` block, closed grounds vocabulary),
`CANONICAL_DECISION_RECORD_CONTRACT` 0.2.0 (superseding-candidate front
matter; the status-as-promoted clarification), canonical-store index schema
0.2.0 (the `supersedes` chain field, append-only), and WF-TRANSFORM-0001
0.2.0 (additive; intent carried through candidate and validation) with a
compatibility note protecting every 0.1.0 record as recorded.
*Checker: Machine (structural validation) + Founder (release).*

**O7-2 — "Current" is machine-answerable.** A deterministic resolver (tool
function over the store alone) answers, for any EDR: current | superseded (by
whom, on what grounds) — walking the chain both directions.
*Negative: the resolver refuses (never guesses) on a dangling or cyclic
`supersedes` reference.* *Checker: Machine + independent validator.*

**O7-3 — One real supersession executed.** EDR-0001 is superseded by a real
EDR-0002 produced from the genuine re-run chain (MISS-0001/0002 closed → fresh
WF-REASON run → new approval with intent → transformation run → new acceptance
→ supersede-promotion). A fixture supersession does not count (0.5 boundary
case, transferred). *Checker: Machine (all contracts) + Founder (confirms the
evidence closure and both human records are real).*

**O7-4 — Silent overwrite impossible (negative).** Demonstrated refusals:
(a) promoting over an existing EDR identity/directory; (b) supersede mode
attempting any write into the superseded record's directory other than the
write-once sibling marker; (c) a second supersession of an already-superseded
record (no forks). Nothing written on any refusal.
*Checker: Machine (fail-closed tool) + independent validator (reviews the
refusal paths are on the only write path).*

**O7-5 — Supersession without both human records refused (negative).**
Demonstrated refusals: missing/malformed/`rejected` new approval; acceptance
absent or lacking the `supersedes` block in supersede mode; intent-block
mismatch across approval/candidate/acceptance; grounds outside the closed
vocabulary or with an unresolvable `grounds_ref`; an upheld-challenge ground
whose referenced disposition is not upheld. *Checker: Machine + independent
validator.*

**O7-6 — History intact after supersession.** Post-O7-3, machine-verified:
`sha256(EDR-0001.md)` equals its pre-supersession ledger `record_sha256`; the
evidence bundle re-verifies digest-by-digest; the EDR-0001 index entry is
byte-identical; CHG-20260716-0001's citations into EDR-0001 still resolve; the
chain walks EDR-0002 → EDR-0001 and back. *Checker: Machine (digest walk) +
independent validator (chain walk).*

**O7-7 — The trigger seam is real at interface level.** The grounds vocabulary
and typed `grounds_ref` checks exist and fail closed; the
upheld-challenge class is demonstrated against the live disposition contract
(a fixture upheld disposition exercising `{required: true, trigger}` →
accepted as grounds; a rejected disposition → refused as grounds); the
`invalidated_assumption` class is recorded as **interface-only** pending Track
B — an explicit gap statement, not a capability claim (P2).
*Checker: Machine + Program Steward (seam/gap statement review).*

**Clause count: 7.**

**Deliberately OUT of the Partial bar (P13):** retirement mechanics (the third
vocabulary word); multi-record batch supersession; an obligation registry that
ledger-enforces reconsideration discharge (Track B integration);
consumer-repo projection of chain status (B2 lane); assumption-trigger
evaluation (O11) and invalidation propagation (O12, 0.7); any editing of
superseded prose, ever.

---

## Appendix — spec-level deltas *(SPEC-LEVEL ONLY — nothing here is built)*

### Store / index delta

```yaml
# canonical/decisions/index.yaml — schema 0.2.0 (append-only, unchanged rule)
# Existing entries: byte-identical, never edited (write-once ledger).
# A SUPERSEDING entry adds two fields:
entries:
  - edr_id: EDR-0002
    # ... all existing 0.1.0 fields (approval_id, acceptance_id, run ids,
    #     record_sha256, accepted_candidate_sha256, accepted_by, granted_at) ...
    supersedes: EDR-0001                 # NEW — the chain edge (absent = not a supersession)
    supersession_grounds: better_evidence  # NEW — closed vocabulary (Item 2)
```

```yaml
# canonical/decisions/EDR-0001/superseded-by.yaml — NEW write-once sibling
# (the directory gains a record; nothing in it is edited — challenge idiom)
schema_version: "0.1.0"
edr_id: EDR-0001
superseded_by: EDR-0002
grounds: better_evidence
grounds_ref: RUN-REASON-<...>
approval_id: APPROVAL-<NNNN>            # the SUPERSEDING chain's records
acceptance_id: ACCEPTANCE-<NNNN>
superseding_record_sha256: <digest of EDR-0002.md as promoted>
granted_at: "<date>"
```

Derived (never stored on old entries): `superseded_by` via reverse index walk;
`current(edr) := edr in index and no entry.supersedes == edr`.

### Record-contract deltas

- `APPROVAL_RECORD` 0.2.0 — optional `supersedes: {edr_id, grounds,
  grounds_ref}`; closed set extended by exactly one key; 0.1.0 records valid
  as recorded (compatibility note).
- `ACCEPTANCE_RECORD` 0.2.0 — same block, required iff the run's candidate
  declares supersession; equality with approval + candidate enforced.
- `CANONICAL_DECISION_RECORD_CONTRACT` 0.2.0 — superseding-candidate front
  matter adds `supersedes: EDR-<NNNN>`, `supersession_grounds`,
  `supersession_grounds_ref`; new grounding rule: the superseded EDR must be
  current at draft time and its identity must match the approval's intent;
  status-as-promoted clarification (Item 3a).

### Workflow / tool delta

- **WF-TRANSFORM-0001 → 0.2.0 (additive).** Entry gate gains check
  ENTRY-07-supersession-intent (target exists, is current, intent well-formed
  — only when the approval carries the block); TASK-CANON renders the chain
  fields; TASK-VALIDATE verifies candidate-vs-approval intent equality and
  target currency; completion carries `supersession_declared: true|false`.
  No new tasks; graph, states, halt unchanged.
- **tools/canonical_promotion → supersede mode.** Activated solely by the
  records (an acceptance with a `supersedes` block), never by a flag alone;
  executes Item 4c's refusal matrix; on success writes, atomically-in-order:
  the new `EDR-<NNNN>/` (as today) → the sibling `superseded-by.yaml` → the
  index append with chain fields. Pre- and post-verifies the superseded
  record's digests (O7-6's invariant).
- **tools/canonical_resolution (new, tiny).** The Item 3b resolver:
  `current(edr)`, `chain(edr)`, `status(edr)` — read-only, standard library,
  consumed by contracts, the B2 projection later, and humans.

---

## Exact founder rulings needed before build

1. **(Item 1)** Adopt **V1** (WF-TRANSFORM-0001 0.2.0 additive +
   promotion-tool supersede mode; no new workflow) and **X2** (chain field on
   the new index entry, append-only; current-ness derived; write-once sibling
   marker in the superseded directory).
2. **(Item 2)** Adopt **G2**: the three-grounds closed vocabulary with typed,
   fail-closed references; `invalidated_assumption` explicitly interface-only
   at 0.6 (Track B seam = an ID string, reconciled at integration).
3. **(Item 3)** Adopt **H2**: superseded bytes immutable forever, effective
   status derived from the store, and ratify the status-as-promoted
   clarification to the EDR contract; adopt the "current" definition and the
   knowing-citation rule.
4. **(Item 4)** Adopt **A2**: the two human acts, both extended (schemas
   0.2.0) to name the supersession, equality-enforced end-to-end; confirm the
   consumption semantics (old approval stays spent; the superseding chain
   consumes its own fresh pair, plus at most one reconsideration obligation by
   reference).
5. **(Item 5)** Adopt **F1**: EDR-0001 → EDR-0002 through the real re-run, with
   MISS-0001/0002 closure on Track A's critical path — or rule F2 and accept a
   recorded unmet clause O7-3 at exit (P2; no third option).
6. **(Bar)** Forward the 7-clause O7 Partial bar to the Bars thread as
   proposed here.

---

## Risks and coordination points found while grounding this proposal

1. **The critical path runs through the consumer repo.** MISS-0001 (evidence
   work) and MISS-0002 (ADR-0005 confirmation) live in `context_switcher`, not
   `ecf`; the Control Plane cannot close them from inside. This is 0.6's
   principal schedule risk — the same shape as O3's risk 1, now binding
   instead of avoidable.
2. **Three closed schemas bump at once** (approval, acceptance, EDR contract)
   plus the index schema — `tools/decision_records/decision_records.py` is
   consumed by both the entry gate and the promotion tool, so the regression
   surface is the whole O3 chain. The 0.5 authority-model note is the
   template: additive-only, strict pinning, historical records valid as
   recorded; regression must re-prove the existing negative tests.
3. **The status-as-promoted clarification needs an explicit ruling**, because
   the 0.5 contract text ("status vocabulary after promotion: canonical |
   superseded | retired") can be read as promising an in-record flip. H2
   resolves the tension in favor of byte-stability with the ledger digest as
   the deciding evidence, but that reading is the founder's to ratify, not
   Track A's to assume.
4. **Track B seam is one-way by design** (kickoff ruling 1): the
   `invalidated_assumption` grounds class consumes an assumption ID string
   and nothing else. If O11 ratifies a different identity shape, the
   reconciliation happens at integration; no O7 deliverable waits.
5. **Reconsideration-obligation discharge is recorded, not enforced, at 0.6**
   — there is no obligation registry to enforce against (the only live
   disposition is `rejected`). Stated as an explicit gap in O7-7; building the
   registry belongs with Track B's routing machinery, not here.
6. **Worktree hygiene note:** `ecf-wt-o7` shows unrelated modified files
   (CRLF churn under `review_packs/`, `roles/`, `standards/`, `vendor/`,
   `transformations/`, `tasks/classification/`, and others) — parallel-session
   shared-state artifacts. This workshop staged nothing; Track A build work
   must stage explicit paths only.

---

## Metadata

| Field | Value |
|---|---|
| Owner (proposing) | Track A owner (O7) |
| Status | **RATIFIED (Founder, 2026-07-16)** — Track A authorized to build; the ratified exit bar is PROPOSAL_06_PARTIAL_BARS (O7-7's seam requirement is absorbed into build scope) |
| Change class | T1 working proposal (organizes the ratified 0.6.0 milestone) |
| Derives from | [PROGRAM_0.6](PROGRAM_0.6.md) Track A · [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md) 0.6.0 |
| Serves | O7 / P14 (canonical knowledge is corrigible) · P7 (no automation supersedes) · P8 (machine-walkable chain) · P2 (honest gaps) |
| Evidence base | `ecf-wt-o7` @ develop `e19a2e0` (= v0.5.0, branch `feature/0.6-o7-supersession`): `canonical/decisions/{index.yaml, EDR-0001/}` · `approvals/{APPROVAL-0001, ACCEPTANCE-0001}.yaml` · `challenges/CHG-20260716-0001/` · `tools/canonical_promotion/promote.py` · `tools/decision_records/decision_records.py` · `tools/authority_rule/{authority_model.py, challenge_records.py, check_stewardship.py}` · `workflows/transformation/WF-TRANSFORM-0001-*.md` · `artifacts/CANONICAL_DECISION_RECORD_CONTRACT.md` |
| Cross references | [PROPOSAL_O3_TRANSFORM_SCOPE](PROPOSAL_O3_TRANSFORM_SCOPE.md) · [PROPOSAL_05_PARTIAL_BARS](PROPOSAL_05_PARTIAL_BARS.md) · [PLATFORM_PRINCIPLES](PLATFORM_PRINCIPLES.md) (P2, P7, P8, P13, P14) |
