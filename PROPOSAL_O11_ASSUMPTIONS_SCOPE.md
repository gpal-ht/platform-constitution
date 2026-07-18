# PROPOSAL_O11_ASSUMPTIONS_SCOPE — Track B scope workshop (O11: first-class executable assumptions with review triggers)

> **Status: RATIFIED (Founder, 2026-07-16)** — including the authority-model bump
> 0.2.0 → 0.3.0 (`accountability → assumption_review`), **ruled T4** under the O4
> precedent. This document
> is the Track B scope workshop for [PROGRAM_0.6](PROGRAM_0.6.md) (milestone 0.6.0),
> resolving the five design-open items the kickoff assigned to it. **No build precedes the
> ruling.**
>
> Obligation: **O11 — first-class executable assumptions with review triggers** (P11,
> verbatim: *"Decisions declare their assumptions with confidence, evidence, and review
> triggers, so that reality can challenge them. The reasoning need not be executable; the
> assumptions that support it can be."*). Constitutional edges honored throughout: **P2**
> (a trigger that cannot fire is never recorded as executable), **P7** (machines detect
> and oblige; humans review and decide), **P13** (every mechanism below must earn its
> place). Exit bar target: **Partial**. Plane: Control (runtime + registries) +
> Governance (this proposal).
>
> Evidence baseline: worktree `ecf-wt-o11` (branch `feature/0.6-o11-assumptions`) off
> `develop` @ `e19a2e0` (= v0.5.0); read-only probes of the real reasoning run
> `runtime/runs/RUN-REASON-WR0001-V040-0002` in the main checkout. **No spike code was
> written** — this workshop is design-only, grounded in probed 0.5 artifacts.

---

## 0. The real material this design is grounded in (probed, not assumed)

1. **Assumptions already exist — but only as run-local prose with colliding identities.**
   The one real reasoning run carries `ASSUME-*` records in two sequences that collide:
   - The **analysis register**: `engineering-reasoning-context.yaml` emits `ASSUME-0001`
     ("ADR-0005's six-subsystem model is authoritative even though ADR-0005 is not among
     the permitted sources") and `ASSUME-0002` (question framing);
     `engineering-risks.yaml`'s `assumptions_register` carries both forward verbatim and
     adds `ASSUME-0003` ("repository responsibilities… still change for the same reasons
     as other external-system connections").
   - The **recommendation envelope**: `engineering-recommendation.yaml` starts a *fresh*
     sequence under the *same IDs* — its `ASSUME-0001` is "The two open upstream blockers
     are resolvable through a **bounded** evidence-gathering effort rather than requiring
     an indefinite investigation" (`evidence_strength: weak`); its `ASSUME-0002` is "The
     boundary described by the forces and axes will remain **stable enough** that
     gathered evidence can be evaluated against the same subsystem question without
     re-scoping it" (`evidence_strength: weak`).

   Same IDs, different statements, one run. A trigger cannot bind to "`ASSUME-0001`"
   without qualifying which sequence it means — naive harvesting destroys identity.
   This single fact drives most of §1.

2. **The envelope shape is closed and minimal.** The recommendation contract
   (`tools/task_runner/output_contracts/decide_recommendation.py`) admits exactly
   `{id, statement, evidence_strength}` per assumption (strength ∈ strong|moderate|weak),
   enforces "an assumption is not evidence" (an assumption ID cited as a decisive force /
   trade-off / risk is rejected), and admits nothing else — no confidence field, no
   trigger field. P11's triad (confidence, evidence, review triggers) is therefore
   **two-thirds absent** from the recorded shape today.

3. **The trigger material is live.** `MISS-0001` / `MISS-0002` are open blockers in the
   run's immutable Missing Information Assessment; `EDR-0001` (the canonical store's
   first and only record) carries them forward explicitly ("open at approval time") and
   its own disposition — `gather_additional_evidence` — *is* the instruction to close
   them and re-run. "Evidence arrives that closes MISS-0002" is a genuine, standing
   evidence-arrival trigger, and the re-run it obliges is the exact re-entry Track A
   flagged as O7's natural first supersession target.

4. **The routing machinery exists and is proven live.** O4 landed
   `tools/authority_rule/{role_state.py, check_stewardship.py, challenge_records.py}`:
   one `StewardshipLedger.resolve()` seam ("one seam, two consumers" — the approval
   boundary and challenge routing), a router-written routing block whose
   `effective_recipient` is **never empty** (Clarification C), evidence-based
   dispositions (P4), write-once records (P14), and a real exercised instance
   (`challenges/CHG-20260716-0001/` filed against `EDR-0001` and disposed `rejected`
   with four evidence refs).

5. **The evaluation idioms available are exactly two** — fail-closed output contracts at
   run boundaries, and human-invoked deterministic stdlib-only tools
   (`tools/canonical_promotion/promote.py` is the exemplar: refuses unless every
   human-authored record exists, verifies, and byte-binds; same inputs → same bytes).
   There is no daemon, scheduler, or long-running process anywhere in `ecf`, and
   `tools/artifact_fingerprint` already provides streamed SHA-256 fingerprinting.
   Digest-binding is the established dependency discipline (EDR-0001's five-item
   evidence manifest).

6. **Time-based review has demonstrated need, not hypothetical need.** The run's own
   risk analysis names the failure mode: `MISS-0007` — "Without a concrete, monitorable
   signal set and named ownership, the deferral alternative cannot be operated and
   **risks silently becoming permanent**" (RISK-0005, silent deferral). And the
   recommendation's `ASSUME-0001` is intrinsically time-shaped: "bounded
   evidence-gathering effort" is falsified by nothing *arriving* — only by time passing
   without arrival.

---

## 1. Item 1 — the assumption record: shape, identity, location, extraction path

### 1.1 Options

**1A — Run-bound only.** Assumptions stay where they are (inside recommendation
envelopes under `runtime/runs/`); triggers reference `(run_id, task, local id)`.

- *For:* zero new stores (P13's preferred answer); the envelope is already
  contract-enforced; provenance is trivially perfect because the record never moves.
- *Against, decisive:* `runtime/` is unversioned and mortal — the 0.5
  run-evidence-permanence deferral says exactly this — so the platform's *first-class
  executable* artifacts would live in its most disposable directory, while the canonical
  decision resting on them (`EDR-0001`) lives in the permanent store. IDs collide across
  tasks (§0.1). And an immutable run output cannot carry a *declared* trigger at all
  without mutating history (P14 violation) — the trigger would have to live somewhere
  else anyway, at which point 1A has quietly become 1C with worse identity.

**1B — Repo-level registry, fresh declaration.** A human authors new assumption records
into a registry, writing statements afresh.

- *For:* the declaration is a deliberate human act (P1); the registry shape is free of
  envelope legacy.
- *Against, decisive:* re-typing severs provenance to the emitting run (P8) and invites
  silent divergence between what the run recorded and what the registry claims —
  precisely the drift class P10 exists to kill. It also re-exercises judgment already
  exercised and validated inside the run (the contract proved the assumptions distinct
  from evidence; a fresh copy re-opens that).

**1C — Repo-level registry populated by deterministic harvest, with human-authored
triggers at registration.** A human-invoked, deterministic registrar tool copies the
assumption **verbatim** out of a digest-verified source, assigns a platform-wide
identity, and binds provenance; the *review triggers* are the human-authored part of the
same registration record.

- *For:* verbatim + digest-bound = provenance preserved to the byte (P8), exactly the
  evidence-bundle discipline EDR-0001 already uses; platform-wide IDs fix the collision;
  the registry lives in git (durable, versioned — P9); the human act is spent where
  judgment is actually new (declaring what would make reality challenge the assumption),
  not where it is mere transcription (P1/P13 both satisfied).
- *Against:* one new registry root and one new tool — cost acknowledged, and bounded by
  the harvest-scope rule below.

### 1.2 Recommendation (Item 1)

**Recommend 1C.** Specifically:

- **Location:** a repo-root registry `assumptions/` in `ecf` — sibling of `approvals/`
  and `challenges/`, the established 0.5 pattern for repo-level record roots.
  Deliberately **not** under `canonical/`: the canonical store's definition was ruled
  narrow in 0.5 and PROGRAM_0.6's background lane forbids silently widening it.
  Layout:

  ```text
  assumptions/
    index.yaml                    # write-once append ledger (canonical-store idiom)
    ASM-<NNNN>/
      assumption.yaml             # the record (schema: Appendix A)
      obligations/                # fired-trigger obligations land here (§3)
        OBL-<YYYYMMDD>-<NNNN>/{obligation.yaml, review.yaml}
  ```

- **Identity:** `ASM-<NNNN>`, platform-wide, assigned by the registrar against the
  write-once index (single-effective-use idiom from `canonical/decisions/index.yaml`).
  The harvested source identity `(source_run_id, source_task_id, source_local_id)` is
  carried as provenance, never as identity.

- **Shape (Appendix A):** harvested core — `statement` (verbatim), `evidence_strength`
  (verbatim; carried as the recorded confidence surrogate at Partial — a richer
  per-assumption confidence model is a named deepening, see §6) — plus a `provenance`
  block binding the emitting run, task, local ID, and the SHA-256 of the digest-verified
  source bytes, plus zero or more human-authored `review_triggers` (§2), plus
  `declared_by` (the registering human). The registrar **refuses** if the statement does
  not match the digest-verified source bytes verbatim.

- **Extraction path and harvest scope at Partial:** harvest **from the digest-bound
  evidence of canonical decision records** — i.e., the assumptions carried by the
  approved report inside `canonical/decisions/EDR-*/evidence/`. Rationale: P11 says
  *decisions* declare their assumptions; the decision's assumptions are the ones in the
  recommendation the human approved. For 0.6 that means exactly two real entries:
  EDR-0001's `ASSUME-0001` and `ASSUME-0002` (recommendation sequence). The analysis
  register's assumptions (context/risks sequence) remain run evidence — explicitly
  un-harvested, reported as a gap, not silently promoted (P2, P3: registration is an
  explicit act, never accumulation).

- **What `MISS-*` records are, and are not:** they are **not** assumptions and are not
  harvested into this registry — they are open-information records with their own
  lifecycle, and duplicating them would create a second source of truth. They are
  **trigger subjects** (§2.2): the most real material O11 has.

---

## 2. Item 2 — review-trigger classes and their machine evaluation

### 2.1 The evaluation model (what evaluates, when, against what — common to all classes)

**What evaluates:** one deterministic, stdlib-only, read-only-inputs tool —
`tools/assumption_registry/evaluate.py` (companion to the registrar; promotion-tool
idiom). It loads every registry entry, evaluates every declared trigger through a
**registered per-class evaluator** (§5 makes this binding fail-closed), and:

- writes one **evaluation record** `assumptions/evaluations/EVAL-<UTC-timestamp>.yaml`
  enumerating every trigger evaluated, its inputs as observed, and its outcome
  (`not_fired | fired | already_obliged | defective_input`), and
- for each *newly* fired trigger, writes one **obligation record** (§3) and routes it
  (§4) — atomically with the evaluation record: an evaluator that reports `fired`
  without persisting the obligation exits nonzero (the O11-3 negative, §6).

**When it runs:** human- or CI-invoked, at named checkpoints — at minimum, **as a
mandatory step of the release gate** (the forcing function: no release ships without
every declared trigger having been evaluated; execution forces synchronization, the P10
idiom). No daemon and no scheduler at Partial — scheduled evaluation is a **named
deferral** (§6), and the honesty cost of its absence is mitigated because every
evaluation record is dated and the release gate makes staleness visible, never silent.

**Idempotency:** one *open* obligation per (assumption, trigger). A trigger that stays
fired across evaluations records `already_obliged`, never a duplicate (write-once
discipline; the challenge registry's "file a NEW challenge instead" idiom).

### 2.2 The three classes, exactly

| | **evidence-arrival** | **dependency-change** | **time-based** |
|---|---|---|---|
| **Subject (declared)** | one open-information item: `{run_id, item_id}` (e.g. `MISS-0002` of the real run) | one repo artifact: `{path, baseline_sha256}` (e.g. `canonical/decisions/EDR-0001/EDR-0001.md`, or `decisions/ADR-0005` once it exists) | one date: `{review_by: YYYY-MM-DD}` |
| **What makes it fire** | a schema-valid, human-authored **closure record** exists in `information_closures/` binding exactly that `{run_id, item_id}` with non-empty evidence (Appendix C). Evidence arrival is itself a recorded act — the machine detects the record, it never judges the evidence (P7, P4) | current SHA-256 of `path` ≠ `baseline_sha256`, or the file is absent. Streamed SHA-256 via the existing `tools/artifact_fingerprint` (reuse, not reinvention) | `--as-of` date (recorded in the evaluation record; defaults to invocation UTC date) > `review_by`. Determinism preserved because the clock reading is an explicit, recorded input |
| **Inputs read** | the `information_closures/` registry + the immutable source MISS record (to verify the subject exists) | the subject file's bytes | the evaluation timestamp |
| **Fail-closed behavior** | a malformed closure record does **not** fire the trigger and is reported `defective_input` in the evaluation record — garbage neither fires nor hides | an unreadable subject fires (absence is a change) | an unparseable date is impossible by construction — rejected at declaration (§5) |
| **Real first instance** | ASM harvested from rec-`ASSUME-0001` → closure of `MISS-0001` and `MISS-0002` | ASM from rec-`ASSUME-0002` ("boundary… without re-scoping") → digest of `EDR-0001.md`; also the Track A seam surface (§4.4) | ASM from rec-`ASSUME-0001` ("**bounded** effort") → a founder-set review-by date; the direct answer to RISK-0005's silent-permanence failure |

The closure registry (`information_closures/CLOSURE-<NNNN>.yaml`, Appendix C) is the one
genuinely new record type this class needs: MISS items live inside immutable run outputs
and cannot be flipped to `closed` without rewriting history (P14), so closure is a new
human-authored record referencing the item it closes — the same "answer by sibling
record, never by mutation" idiom as challenge dispositions.

### 2.3 In the bar vs named deferrals (P13)

**IN the Partial bar: all three classes** — each machine-evaluated with a positive and a
negative fixture, and **one real firing** end-to-end (§6, O11-5). All three earn their
place on probed evidence, not symmetry: evidence-arrival is the live MISS-0001/0002
re-entry; dependency-change is the digest discipline the store already runs on;
time-based answers a failure mode the run's own risk analysis recorded (RISK-0005).
Each evaluator is a few dozen lines over existing idioms — the marginal governance cost
is near zero, the schema cost of *excluding* one (a class named by the program but not
representable) would itself be a P2 problem.

**Named deferrals (recorded so their absence is a gap, not an omission):**

- **Operational-evidence triggers** (telemetry, production signals, external feeds).
  Deliberately absent until the **FD-2 ruling** lands: at Partial every trigger consumes
  *recorded repo artifacts* (closure records, digests, dates) — a fact this workshop
  hands the FD-2 memo as evidence (it cuts toward reading (b), operational evidence as a
  cross-cutting concern; the deferred class is exactly where a distinct Plane would earn
  admission).
- **Scheduled/daemon evaluation.** Evaluation stays human/CI-invoked at named
  checkpoints; the release gate is the floor.
- **Trigger expressions** (boolean combinations, thresholds over evidence strength).
  One trigger = one subject = one firing rule at Partial.
- **Cross-repo subjects.** Everything binds inside `ecf`.

---

## 3. Item 3 — what "executable" means at Partial: the review-obligation record

**The scope sentence, stated plainly: a machine-evaluated trigger produces a recorded,
routed review obligation — and nothing more.** The obligation *obliges a human review*;
it never invalidates the assumption, never marks the decision stale, never re-runs
reasoning, never touches the canonical store. **Full invalidation propagation across
reasoning is O12 (0.7) and is explicitly OUT of this bar (P13)** — recorded here so its
absence is a named gap, not a silent omission (P2).

The obligation record (`assumptions/ASM-*/obligations/OBL-*/obligation.yaml`, Appendix
B) carries, in closed fields:

- **identity + bindings:** `obligation_id` (`OBL-<YYYYMMDD>-<NNNN>`), `assumption_ref`
  (ASM id + the registry record's SHA-256 at firing time), `trigger_ref` (the trigger's
  id and class), `evaluation_id` (the evaluation record that fired it) — the unbroken
  chain (P8).
- **`fired_because`:** the machine-observed facts, verbatim — the closure record path
  and digest, or `{baseline_sha256, observed_sha256}`, or `{review_by, as_of}`. The
  obligation states *what was observed*, never an interpretation (P2).
- **`routing`:** written by the router, never by the evaluator's caller (§4).
- **status by sibling:** `open` until a human-authored `review.yaml` (Appendix B2)
  exists — evidence-based, indelible, one per obligation ever; a later change of mind
  re-enters as a new obligation or a challenge. Review outcomes:
  `reaffirmed | revised | invalidated` (+ evidence, non-empty — P4; + authority binding
  — §4). An `invalidated` outcome additionally emits the Track A seam record (§4.4).

P7 discipline, stated for the record: the machine's whole authority here is *detect and
oblige* — exactly parallel to 0.3's `waiting_for_human_approval` halt. A fired trigger
is a halt in the assumption's lifecycle; a human answers it.

---

## 4. Item 4 — routing: O4 challenge machinery vs a distinct review-obligation channel

### 4.1 Option R1 — a fired trigger files a challenge (full reuse)

The evaluator authors a `CHG-*` record against the decision; routing, disposition,
indelibility all come for free, already live and exercised.

- *For:* zero new routing surface; Clarification B guarantees inherited wholesale; P11's
  own words are "so that reality can challenge them" — the challenge registry is where
  challenges live.
- *Against, decisive:* (a) a challenge has a *challenger* who states falsifiable
  *grounds* — making the evaluator a challenger puts an automated actor in an
  adversarial human role and stretches P4's "ANY actor may challenge" past its intent;
  (b) challenge dispositions (`upheld | rejected | …`) misfit a review whose normal
  outcome is "reaffirmed — evidence arrived and still supports it"; (c) a routine
  time-based review consuming the adversarial instrument means every calendar tick
  inflates the challenge registry — vocabulary overload is how record types rot (P13);
  (d) a challenge binds to the *decision*, but the obligation binds to the *assumption*
  — the decision may survive a revised assumption.

### 4.2 Option R2 — a distinct review-obligation channel on the same resolution seam

A new record type (§3) routed by the **same** `StewardshipLedger.resolve()` seam and the
**same** router-written routing-block shape (`accountable_role`, `authority`,
`model_version`, `holder_state`, `effective_recipient` — never empty, `degraded`,
`escalation_target` when degraded), with the same disposition discipline (evidence
non-empty; recipient must equal `routing.effective_recipient` and hold the required
authority in the pinned model; write-once).

- *For:* "one seam, two consumers" was O4's own design sentence — this makes it three,
  which is reuse of the *mechanism* without overloading the *instrument*. Vacancy
  behaves identically at all boundaries by construction. The record vocabulary fits the
  act (review, not contest). The adversarial path stays available downstream: a review
  that finds the assumption `invalidated` obliges reconsideration — and *that* re-entry
  uses the challenge/supersession machinery, which is where it belongs.
- *Against:* one new record type + one authority question (below).

### 4.3 Recommendation (Item 4)

**Recommend R2 — a distinct review-obligation channel routed through the O4 `resolve()`
seam**, with the routing-block schema reused verbatim and the disposition discipline
mirrored.

**The authority question, presented honestly.** Who may author `review.yaml`? Two
readings:

- *(i) Reuse `challenge_disposition`.* No model change; but it stretches a ratified
  binding whose name and grant are challenge-specific — the kind of optimistic
  interpretation P2 forbids.
- *(ii) Additive minor bump — authority model 0.2.0 → 0.3.0: `accountability` →
  + `assumption_review`.* P5's ratified definition of `accountability` — "who must
  answer for its **continued validity** or initiate reconsideration" — is *literally the
  assumption-review job description*; the bump writes that ratified answer into the
  table, exactly the "projection of ratified text" reasoning the founder accepted in
  ruling O4's bump **T4** (PROPOSAL_O4 §1, ruled 2026-07-16). Additive-only, minor,
  strict single-version pin, lockstep landing, compatibility note — the 0.5 ceremony
  re-run with fresh precedent.

**Recommend (ii).** Cost: one small, pattern-proven model change riding the T4 process.
Benefit: the table stays honest about what each authority grants. If the founder prefers
(i), §3/§6 are unchanged — only the pinned authority token differs.

### 4.4 The Track A seam — designed as an interface, no dependency

When a review records `outcome: invalidated`, the review record **must** carry a closed
`supersession_candidate` block: `{decision_ref (e.g. EDR-0001), assumption_ref,
obligation_ref, reason: assumption_invalidated}` (Appendix B2). That record is the whole
seam: a durable, digest-addressable fact Track A's supersession triggers **may** consume
as "an invalidated assumption is a natural supersession trigger" (PROGRAM_0.6 kickoff
ruling 1). Track B neither calls Track A code nor blocks on its design; reconciliation
happens at integration, on records. Conversely, dependency-change triggers give Track A
a free consumer surface: supersession of a canonical record changes its bytes/index,
which fires any assumption depending on it — again through records only.

---

## 5. Item 5 — the P2 edge, honored in the schema itself

**The rule: a trigger that cannot actually fire must not be representable as
"executable."** Enforced at **declaration time**, fail-closed, in the registrar — not by
convention, and not discovered later at evaluation time:

1. **Closed class enum.** `class ∈ {evidence_arrival, dependency_change, time_based}`.
   An unknown class is rejected — there is no "other/free-text" arm to hide an
   aspirational trigger in.
2. **Mandatory evaluator binding that must resolve.** Every trigger carries
   `evaluator: {tool: "tools/assumption_registry/evaluate.py", impl: <registered id>}`;
   the registrar refuses any declaration whose `impl` is not in the evaluator's
   registered-implementation table for that class. A trigger with no wired evaluator
   **cannot be written** (the exact P2 edge PROGRAM_0.6 names: "no evaluator wired →
   must not be recorded as executable").
3. **Subject resolution at declaration.** evidence_arrival: the referenced
   `{run_id, item_id}` must exist in the (immutable) source Missing Information
   Assessment; dependency_change: `path` must exist and `baseline_sha256` must equal its
   current bytes *at declaration* (you cannot declare a baseline you did not take);
   time_based: `review_by` must parse and lie in the future at declaration.
4. **Executability is derived, never asserted.** There is **no** author-settable
   `executable:` field anywhere in the schema. An assumption's executable status is
   computed: ≥ 1 declared trigger, all valid under rules 1–3. A registered assumption
   with `review_triggers: []` is legal but is reported by every evaluation record under
   `gaps: assumptions_without_triggers` — an explicit Clarification-A-style gap, visible
   at every release gate, never a silent pass and never a hidden lie.
5. **The negative is in the bar** (O11-2, §6): the registrar demonstrably rejects a
   declaration with an unknown class, an unregistered evaluator impl, an unresolvable
   subject, or a stale baseline.

---

## 6. The proposed O11 Partial bar

Read per the ratified 0.5 discipline (PROPOSAL_05_PARTIAL_BARS): every clause needs a
named artifact, a named demonstration actually run, and a named checker; anything less
is an explicit gap, never a pass.

### 6.1 Clauses

**O11-1 — Assumption registry live with provenance-preserving harvest.** `assumptions/`
registry + write-once index + registrar tool exist; the two real assumptions carried by
EDR-0001's digest-bound approved report are registered as `ASM-0001`/`ASM-0002` with
verbatim statements, carried `evidence_strength`, and provenance (run, task, local id,
source SHA-256). *Negative:* the registrar rejects a statement that does not match the
digest-verified source bytes, and rejects a source outside the harvest scope.

**O11-2 — Unevaluatable trigger rejected at declaration (the P2 edge).** All three
trigger classes declarable per Appendix A; the registrar **rejects**, fail-closed:
unknown class · unregistered `evaluator.impl` · nonexistent evidence-arrival subject ·
dependency baseline that does not match current bytes · unparseable/past `review_by`.
Executability is derived (no assertable field); trigger-less assumptions appear in the
evaluation record's gap list.

**O11-3 — A fired trigger produces a recorded obligation — or the evaluation fails.**
The evaluator, run at a named checkpoint, writes the evaluation record and, for each
newly fired trigger, the obligation record with machine-observed `fired_because`.
*Negative:* a firing that cannot persist its obligation makes the evaluator exit
nonzero — **a fired trigger without a recorded obligation is a failure**, never a log
line. *Negative:* a still-open obligation is never duplicated (`already_obliged`).

**O11-4 — Every obligation is routed; an unrouted obligation fails Clarification B.**
The routing block is written by the router via `StewardshipLedger.resolve()`;
`effective_recipient` is never empty; with the accountable office recorded vacant, the
obligation routes visibly degraded to `founder_genesis`. *Negative:* an obligation
record lacking a routing block, or whose recipient is empty, is rejected by the record
validator — a review obligation that reaches no accountable recipient is not an
obligation (Clarification B, applied to O11's channel).

**O11-5 — One REAL fired trigger, end-to-end.** One trigger declared on a real
registered assumption fires on real inputs — the standing candidates: **evidence
arrives that closes MISS-0002** (a real closure record with real evidence), or the
founder-set **bounded-effort review date on ASM-0001 passes** — producing a routed
obligation and a human-authored, evidence-bearing review record whose author holds the
§4.3 authority in the pinned model (fail-closed check). A fixture firing proves the
mechanism; it does not satisfy this clause (the 0.5 "real, not fixture" rule).

**O11-6 — Honesty and compatibility.** Un-harvested run assumptions and trigger-less
registered assumptions are enumerated as explicit gaps in every evaluation record; the
model bump (if §4.3(ii) is ruled) lands additively with a compatibility note and full
regression green; **no clause claims propagation** — O12's boundary is stated in the
registry README verbatim.

### 6.2 Artifact · demonstration · checker

| Clause | Artifact | Demonstration | Checker |
|---|---|---|---|
| O11-1 | `assumptions/{index.yaml, ASM-0001/, ASM-0002/}` + registrar | registrar run against EDR-0001's evidence bundle; byte-mismatch fixture rejected | Machine (registrar, fail-closed) + independent validator (digest walk) |
| O11-2 | trigger schema + registrar validation + negative tests | five rejection fixtures (§6.1) each rejected with reasons | Machine + independent validator (reviews the negatives are on the enforced path) |
| O11-3 | `assumptions/evaluations/EVAL-*.yaml` + `OBL-*/obligation.yaml` | evaluator run: fixture positive fires and persists; persistence-failure fixture exits nonzero; re-run yields `already_obliged` | Machine (evaluator exit code + record cross-check) |
| O11-4 | routing block in each obligation | active-office routing + vacant-office degraded routing (against the recorded ledger, not a stub); unrouted-obligation fixture rejected | Machine (record validator) + Founder (fallback attribution truthful) |
| O11-5 | the real closure record (or dated firing) + `OBL-*` + `review.yaml` | the live end-to-end chain, walked | Machine (contracts) + Founder (confirms the firing input was real) |
| O11-6 | evaluation-record gap lists + compat note + regression run | inspection + full suite green | Machine (regression) + Program Steward (note review) |

### 6.3 Explicitly OUT of the Partial bar (P13 — named deferrals)

- **Invalidation propagation across reasoning** — what an invalidated assumption does to
  the decisions and artifacts downstream. **O12, milestone 0.7.** Out, verbatim, per the
  program. The Partial boundary is: obligation recorded, routed, humanly reviewed;
  the seam record (§4.4) is emitted and consumed by no one in 0.6 Track B.
- **Operational-evidence trigger class** — awaits the FD-2 ruling (§2.3).
- **Scheduled/daemon evaluation** — evaluation is invoked, at minimum at the release
  gate.
- **Harvest beyond canonical decisions' assumptions** — the analysis register's
  sequence (context/risks) stays run evidence (reported as gaps).
- **Per-assumption confidence model richer than the carried `evidence_strength`.**
- **Review SLAs / obligation aging policy; trigger expressions; cross-repo subjects;
  MISS-record lifecycle management** (closure records reference, never manage, the
  source items).

---

## Appendix A — `assumptions/ASM-<NNNN>/assumption.yaml` (draft)

```yaml
schema_version: "0.1.0"
assumption_id: ASM-0001                    # platform-wide; write-once index entry
statement: >                               # VERBATIM from the digest-verified source
  The two open upstream blockers are resolvable through a bounded
  evidence-gathering effort rather than requiring an indefinite investigation.
evidence_strength: weak                    # carried verbatim (strong|moderate|weak)
provenance:                                # P8 — binds the emitting run to the byte
  source_run_id: RUN-REASON-WR0001-V040-0002
  source_task_id: TASK-DECIDE-0002
  source_local_id: ASSUME-0001             # the run-local, colliding id — provenance only
  source_path: canonical/decisions/EDR-0001/evidence/engineering-recommendation-report.md
  source_sha256: e894a84e6c631f7b7928b1ca582d8276d1e0914d8b128fa0b69631caadd1053f
  decision_ref: EDR-0001                   # the decision that declares this assumption (P11)
declared_by: {actor: "Founder (Genesis)", recorded_at: "2026-07-..."}
review_triggers:                           # human-authored at registration; may be []
  - trigger_id: TRG-0001                   # unique within the assumption
    class: evidence_arrival                # CLOSED enum (§5.1)
    subject: {run_id: RUN-REASON-WR0001-V040-0002, item_id: MISS-0002}
    evaluator: {tool: tools/assumption_registry/evaluate.py,
                impl: evidence_arrival_v1} # MUST resolve at declaration (§5.2)
  - trigger_id: TRG-0002
    class: time_based
    subject: {review_by: "2026-10-16"}     # future at declaration (§5.3)
    evaluator: {tool: tools/assumption_registry/evaluate.py, impl: time_based_v1}
# no `executable:` field exists — executability is derived, never asserted (§5.4)
```

Dependency-change subject shape:
`subject: {path: canonical/decisions/EDR-0001/EDR-0001.md, baseline_sha256: 2fb71c58…}`
(baseline must match current bytes at declaration).

## Appendix B — `OBL-*/obligation.yaml` (draft)

```yaml
schema_version: "0.1.0"
obligation_id: OBL-20261016-0001
assumption_ref: {assumption_id: ASM-0001, record_sha256: "<registry bytes at firing>"}
trigger_ref: {trigger_id: TRG-0002, class: time_based}
evaluation_id: EVAL-20261016T090000Z
fired_because:                             # machine-observed facts, verbatim (P2)
  review_by: "2026-10-16"
  as_of: "2026-10-16"
routing:                                   # WRITTEN BY THE ROUTER (O4 shape, verbatim)
  accountable_role: accountability
  authority: assumption_review             # or challenge_disposition, per §4.3 ruling
  model_version: "0.3.0"                   # strict pin
  holder_state: active | vacant
  effective_recipient: accountability | founder_genesis   # NEVER empty
  degraded: false
status: open | reviewed                    # derived from the sibling review.yaml
```

## Appendix B2 — `OBL-*/review.yaml` (draft; write-once, one per obligation ever)

```yaml
schema_version: "0.1.0"
obligation_id: OBL-20261016-0001
outcome: reaffirmed | revised | invalidated
reviewed_by: {actor: "...", role: accountability,
              authority: assumption_review, model_version: "0.3.0"}
              # must equal routing.effective_recipient; fail-closed authority check
evidence: [ ... ]                          # NON-EMPTY (P4)
rationale: "..."
revised_to: {assumption_id: ASM-000X}      # REQUIRED iff outcome: revised (new record;
                                           # the old one is never rewritten — P14)
supersession_candidate:                    # REQUIRED iff outcome: invalidated — the
  decision_ref: EDR-0001                   # Track A seam record (§4.4); consumed by
  assumption_ref: ASM-0001                 # no one in 0.6 Track B
  obligation_ref: OBL-20261016-0001
  reason: assumption_invalidated
recorded_at: "2026-10-16"
```

## Appendix C — `information_closures/CLOSURE-<NNNN>.yaml` (draft)

```yaml
schema_version: "0.1.0"
closure_id: CLOSURE-0001
closes: {run_id: RUN-REASON-WR0001-V040-0002, item_id: MISS-0002}
evidence: [ {ref: "decisions/ADR-0005-...", note: "the canonical subsystem model,
             now among permitted sources"} ]   # NON-EMPTY (P4)
recorded_by: {actor: "..."}
recorded_at: "..."
# Write-once; references the immutable MISS item, never mutates it (P14).
```

## Appendix D — evaluation record `assumptions/evaluations/EVAL-<ts>.yaml` (sketch)

Closed fields: `evaluation_id`, `as_of`, `invoked_by`, per-trigger results
(`not_fired | fired | already_obliged | defective_input`, with observed inputs),
`obligations_written: [...]`, and `gaps: {assumptions_without_triggers: [...],
unharvested_sources: [...]}` (§5.4, O11-6).

---

## The five recommendations, one line each

1. **Record:** repo-root `assumptions/` registry (`ASM-<NNNN>`, write-once index),
   populated by deterministic **harvest** — verbatim, digest-bound to the emitting run —
   from canonical decisions' evidence, with triggers human-authored at registration.
2. **Triggers:** all three classes (evidence-arrival via human-authored closure records;
   dependency-change via SHA-256 vs declared baseline; time-based via recorded `as_of`
   vs `review_by`) evaluated by one deterministic, invoked tool, mandatory at the
   release gate; operational-evidence class deferred to the FD-2 ruling.
3. **Executable at Partial:** fired trigger → write-once, machine-fact-bearing
   **obligation record** halting for human review — reaffirm / revise / invalidate;
   invalidation propagation is O12 (0.7), OUT.
4. **Routing:** a **distinct review-obligation channel** on the O4 `resolve()` seam
   (routing block reused verbatim, never-empty recipient, evidence-based indelible
   review), with an additive T4 model bump `accountability → assumption_review`
   (0.3.0); challenges stay the adversarial instrument downstream of invalidation.
5. **P2 edge:** closed class enum + mandatory evaluator binding that must resolve +
   subject resolution at declaration + **derived, never assertable** executability —
   an unevaluatable trigger cannot be written, and trigger-less assumptions are
   standing visible gaps.

---

## Metadata

| Field | Value |
|---|---|
| Status | **RATIFIED (Founder, 2026-07-16)** — Track B authorized to build; model bump ruled T4 |
| Change class (this document) | T1 operational (a scope-workshop proposal); the model bump it proposes classifies T4 on the PROPOSAL_O4 §1 precedent (founder confirms) |
| Owner (proposing) | Track B owner (O11) |
| Evidence | Worktree `ecf-wt-o11` @ `e19a2e0` (v0.5.0, design-only — no spike code); read-only probes: `runtime/runs/RUN-REASON-WR0001-V040-0002/task_outputs/{engineering-recommendation, missing-information, engineering-reasoning-context, engineering-risks}.yaml` · `canonical/decisions/EDR-0001/` · `challenges/CHG-20260716-0001/` · `tools/authority_rule/{authority_model, role_state, check_stewardship, challenge_records}.py` · `tools/{canonical_promotion, artifact_fingerprint}` |
| Derives from | P11 (verbatim) · P2 · P4 · P7 · P8 · P13 · P14 · Clarifications B/C · [PROGRAM_0.6](PROGRAM_0.6.md) Track B design-open items 1–5 + kickoff ruling 1 (the A/B seam) |
| Cross references | [PROPOSAL_O4_STEWARDSHIP_SCOPE](PROPOSAL_O4_STEWARDSHIP_SCOPE.md) (routing machinery + T4 precedent) · [PROPOSAL_05_PARTIAL_BARS](PROPOSAL_05_PARTIAL_BARS.md) (bar discipline) · [PROGRAM_0.5](PROGRAM_0.5.md) · [PLATFORM_PRINCIPLES](PLATFORM_PRINCIPLES.md) · FD-2 workshop thread (operational-evidence deferral is its input) |
