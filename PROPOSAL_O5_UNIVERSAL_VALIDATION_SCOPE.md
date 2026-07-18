# PROPOSAL — O5 Universal Independent Validation Scope (P6, cross-plane)

> **Status: RATIFIED (Founder, 2026-07-17) — ratify all as recommended.** The finding that
> generation and semantic validation share an ACTOR within a run (P6 holds today via
> MECHANICAL independence — output contracts + the C13 gate — not a distinct actor) is
> recorded honestly (bar clause O5-3, not concealed); distinct-actor independence is
> required across plane boundaries. Non-constitutional (T1). Workshop
> output for [PROGRAM_0.8](PROGRAM_0.8.md) Workshop O5 ("Universal Independent
> Validation, P6 — make generation≠validation a checkable platform invariant that holds
> ACROSS plane boundaries"). It resolves the three design-open items in the O5 charter
> with options, trade-offs, real evidence, and one recommendation each, and proposes an
> O5 contribution to the 0.8 Partial bar. **It designs; it does not build** (PROGRAM_0.8
> immediate-next-step: workshop before build). Everything here is PROPOSED; the founder
> rules. Where a clause could bind differently depending on whether B2 lands in 0.8, the
> clause is written **parametrically** ("the ratified cross-plane act", "the ratified
> projection vehicle") so ratifying it constrains *what must be true*, not *which design
> gets there*.

| Field | Value |
|---|---|
| Derives from | [PROGRAM_0.8](PROGRAM_0.8.md) Workshop O5 · [PLATFORM_PRINCIPLES](PLATFORM_PRINCIPLES.md) P6 (verbatim), P2, P7, P8 · [PLATFORM_ARCHITECTURE](PLATFORM_ARCHITECTURE.md) §2.3, §4.4 (Review Plane), §5 (cross-plane contracts) |
| Governing principle | **P6 — "The actor that produces a decision cannot be the sole actor that ratifies it — regardless of whether that actor is human or machine."** Read across a plane boundary too (PROGRAM_0.8 constitutional edge P6). |
| Precedent | [PROPOSAL_06_PARTIAL_BARS](PROPOSAL_06_PARTIAL_BARS.md) / [PROPOSAL_07_PARTIAL_BARS](PROPOSAL_07_PARTIAL_BARS.md) (ratified) — clause discipline, artifact/demonstration/checker, real-not-fixture, named identities, bar-vs-reality tracking, honesty-first (P2) |
| Evidence baseline probed | `ecf` worktree `feature/0.8-o5-validation` @ `c02fe64` (= v0.7.0), read-only study; `context_switcher` main checkout (read-only) |
| Change class | T1 Operational (a scope workshop + a proposed bar contribution; the obligation and milestone exit are already ratified in the roadmap). A workflow-validator invariant that touches the P6 boundary is a T4 landing when built — flagged, not pre-authorized here. |

---

## How to read this proposal (the ratified 0.5/0.6/0.7 discipline)

A design-open item is *resolved* only when it names the **real surface** it was decided
against (a file, a check, a record that exists at `c02fe64`), the **options** weighed, and
**one recommendation** with its trade-off stated. A proposed bar clause is met only when it
has (a) a named **artifact** that exists, (b) a named **demonstration** actually run, and
(c) a named **checker**. Per P2, a clause with an artifact but no demonstration is an
**explicit gap**, never a pass. Checker vocabulary (unchanged): **Machine (fail-closed
contract)** · **Independent validator (O5/P6)** · **Founder** (the only checker who marks a
clause *ratified*).

---

# Part 0 — The key finding (read before the items)

**Is generation≠validation actually enforced as an invariant today, or only
conventionally? — It is enforced *per-workflow and mechanically*, NOT as a universal
invariant, and NOT by an independent *actor*.** Three facts, each grounded in code at
`c02fe64`:

1. **Structural separation is real but not universally checked.** Each released workflow
   *does* separate validation into a distinct task that depends on the generator:
   `WF-REASON-0001` Step 15 `TASK-VALIDATE-0001` (depends on `TASK-PRODUCE-0001` + all
   reasoning tasks) and `WF-TRANSFORM-0001` Step 5 `TASK-VALIDATE-0002` (depends on
   `TASK-CANON-0001`). But the **workflow-validator (`tools/workflow_validator/validate_workflow.py`,
   checks WF001–WF021) has no check that requires an independent validate task**. The
   closest, **WF015**, requires a validation *binding*
   (`recommendation-report-validation.yaml`) — but it **self-skips for any workflow whose
   `successful_exit_state` is not `waiting_for_human_approval`** (line 680: *"Not a
   reasoning-terminal workflow; terminal-artifact check skipped"*). So WF015 enforces
   validation for `WF-REASON` **by hard-coded reasoning-terminal artifact list**, and
   enforces **nothing** for `WF-TRANSFORM` — whose `TASK-VALIDATE-0002` is guaranteed only
   by spec prose (*"validator is not the drafting actor (O5/P6, structural)"*, Step 5) and
   by its own output contract. **A new workflow authored with no validate task would pass
   WF001–WF021.** Generation≠validation is therefore a **per-workflow convention**, not a
   platform invariant.

2. **The independence that *does* bind is mechanical, not actor-based.** What actually
   stops an executor from waving its own broken output through is the **output contract**,
   which re-derives ground truth executor-independently and fails closed:
   - `output_contracts/validate_report.py` re-runs the report contract against the report
     on disk (*"an executor could wave a broken report through the approval gate simply by
     asserting `result: passed`"*) and **rejects a PASS verdict over a non-conformant
     report** — the *unsafe direction*. It deliberately *allows* a FAIL verdict over a
     clean report (the safe direction).
   - `output_contracts/verify_source_run.py` re-verifies every provenance digest from disk
     — *"the executor cannot invent an intact chain"* — literally executor-independent.
   - The **C13 review gate** (`tools/review_gate/gate.py`) is *"pure and read-only… never
     reads generation internals — no prompts, no executor transcripts, no chain-of-thought"*
     and **fails closed** (*"the absence of a 'no' is never a 'yes'"*). This is P6
     independence-of-*inputs*: the verdict is derived from bound outputs only.

3. **The validating ACTOR is the same as the generating actor.** `TaskRunner.__init__`
   (`tools/task_runner/runner.py:86`) binds **one** `executor` for the whole run; every
   task — generation *and* validation — executes on `self.executor`. The
   `reasoning_attestation` module records *"one model per run in the observed pipeline"*
   (write-once run-level `reasoning-model.yaml`). **So the same model that writes the
   recommendation also writes its validation verdict.** The mechanical contract catches the
   *unsafe-direction* claim; **semantic** validation (an unsupported prose fact, an
   assumption dressed as evidence — the very cases `validate_report.py` says *"no mechanical
   check can see"*) is produced by the generator's own actor.

**The honest one-line answer (P2):** *within a plane, generation≠validation is enforced as
a per-workflow convention plus a fail-closed mechanical contract on the unsafe direction —
not as a universal validator invariant, and not by an independent actor. Across a plane
boundary, it is not enforced at all: no cross-plane validation record exists.* The three
items below close exactly those three gaps.

---

# Part I — The three design-open items resolved

## Item 1 — UNIVERSAL: invariant or convention? Make it checkable.

**The question (charter):** is separation-of-generation-and-validation a platform invariant
every workflow must satisfy (a workflow-validator check, WF0xx), or only a per-workflow
convention today? Probe: would a new workflow without a validate step be rejected?

**Probe result:** No. As Part 0 shows, WF015 is reasoning-terminal-only and no other WFxxx
requires a validate task. A `category: transformation` or a future `category: *` workflow
with generation tasks and no validation task passes the validator. Convention, not
invariant.

**Options.**

- **1A — Leave as convention; rely on review at authoring time.** Each new workflow spec is
  human-reviewed and *ought* to include a validate task. **Trade-off:** this is precisely
  the *"0.4-style discipline, not enforcement"* line the ratified O4/O11 bars drew
  (PROPOSAL_06 II.3-4). P6 is constitutional; a constitutional invariant guarded only by
  reviewer diligence is a P13/P2 weakness — the platform would *claim* universal
  independent validation while enforcing it for one workflow category. Rejected.

- **1B — Generalize WF015's hard-coded list per category.** Extend the terminal-artifact
  table with a transformation branch, a future-category branch, etc. **Trade-off:** it
  scales by enumeration — every new category needs a new hard-coded branch, and a category
  nobody added a branch for silently enforces nothing. It also conflates *"has the right
  terminal artifacts"* with *"has an independent validation step,"* which are different
  invariants. Partial; rejected as the primary mechanism.

- **1C — A single category-independent invariant check (recommended).** Add **WF022 —
  independent-validation invariant**: a workflow that produces any *consequential artifact*
  (defined structurally: a bound output under `reports/` that is the workflow's terminal
  deliverable, or any output the workflow declares `consequential: true`) must declare a
  **validation task** V such that (a) V is **distinct** from every task that produces a
  consequential artifact; (b) V **depends on** (directly or transitively, via the existing
  `depends_on` DAG the validator already parses) each consequential producer it validates;
  (c) V **binds a verdict output** that is routed through the frozen C13 gate; and (d) V
  declares, in a machine-readable `validates:` block, which producer task(s) it ratifies.
  The check reuses machinery the validator already has — `parse_binding_table`,
  `parse_depends_on`, the acyclicity/ordering checks (WF008/WF012). **A workflow with no
  such V fails WF022, in every category.**

**Recommendation: 1C.** It lifts generation≠validation from convention to a **checkable
structural invariant** applied uniformly, closes the "new workflow without a validate step"
hole the probe found, and is a small, mechanical addition to an existing read-only
validator. Trade-off honestly stated: **WF022 checks structural separation (distinct task +
dependency + C13-routed verdict), not actor independence** — that is Item 3's boundary and
Part 0 fact 3's honest ceiling. Structural universality is the achievable 0.8 step; actor
independence within a single-executor run is deepening (§ OUT list).

## Item 2 — CROSS-PLANE: is a projection/consumption independently validated against its source?

**The question (charter):** when a Control artifact projects into Project (B2) or consumes
Knowledge-plane content, is that projection/consumption independently validated against its
SOURCE by an actor that is not its generator? Define the cross-plane validation record + who
validates.

**Probe result:** No such validation exists. Evidence at `c02fe64`:
- **Knowledge consumption.** `TASK-RETRIEVE-0002` consumes the bundled EKB and emits the
  knowledge package; the EKB is **pinned by digest** (WF-REASON Environment Dependencies;
  `check_bundle_integrity.sh` in `context_switcher` re-checks bundle SHAs). But a **digest
  pin is a provenance fact (P8), not a validation verdict (P6)** — it proves *which bytes*,
  not that the consumption is *faithful to the source and ratified by a non-generator*.
- **Project projection (B2).** Does not exist. The consumer's `acceptance_tests/`
  (`check_consumer_integration.sh`, `check_bundle_integrity.sh`) validate that the bundle
  is intact and the integration *runs* — a Project-plane self-check of wiring, **not** an
  independent validation of a projected Control decision against its Control source.
  `canonical/decisions/EDR-0002/` is never seen by `context_switcher`.
- **No record type.** A repo-wide probe for `cross_plane` / `projection_validation` /
  `source_plane` finds no cross-plane validation record anywhere in `tools/`.

So the P6 guarantee stops at the plane boundary. This is exactly the 0.8 exit gap
("demonstrably hold ACROSS plane boundaries").

**Options.**

- **2A — Rely on the source-plane verdict; the projection inherits it.** If EDR-0002 was
  independently validated inside Control, a faithful copy is "already validated."
  **Trade-off:** a *copy* is a new artifact with a new failure mode — the projection can
  diverge, be stale, or be partial, and the source verdict says nothing about the copy's
  fidelity. Inheriting a verdict across a boundary is the self-ratification-by-proxy the
  architecture forbids (§5: *"A Plane boundary crossed without a versioned interface +
  provenance is an architectural violation"*). Rejected.

- **2B — Digest pin only (status quo).** Bind the projection to the source by SHA and
  declare done. **Trade-off:** P8, not P6. It proves the bytes match *at pin time* but
  names no independent actor that *ratified* the crossing; a corrupted-but-consistent
  projection (same bytes, wrong artifact selected) passes. Necessary but insufficient.

- **2C — A cross-plane validation (CPV) record, validated by a non-generator in the
  consuming plane (recommended).** Define a first-class **CPV record** emitted whenever a
  Control artifact projects into another plane or consumes another plane's content. It binds:
  - `source_ref` + `source_digest` — the pinned source-plane bytes (the Control canonical
    record, or the EKB object) — reusing the digest-durability rule
    (`tools/reproducibility/durability.py`: a permanent record's live reference must be a
    tracked or digest-bound path, never a bare mortal `runtime/` cite — O8/P8);
  - `projection_ref` + `projection_digest` — the consuming-plane bytes;
  - `generator_actor` — who produced/projected the crossing;
  - `validator_actor` — who ratified it (Item 3 makes this ≠ generator, fail-closed);
  - a **fidelity verdict** (`faithful | divergent | stale`) over a mechanical
    re-derivation: the CPV contract **recomputes** `projection_digest` from the
    consuming-plane bytes and **re-resolves** `source_digest`, refusing a `faithful` verdict
    the bytes do not support — mirroring `verify_source_run.py`'s executor-independent
    re-derivation.
  **Who validates:** the **Review responsibility of the consuming plane** (Review is the
  cross-cutting Plane whose *reason to exist* is validation independent of generation,
  §4.4), acting as an actor that is **neither the projector nor the source-plane
  generator**. Consistent with **P7** (PROGRAM_0.8 edge): the projection is **read-only and
  confers no standing** in the consuming plane until an affirmative CPV verdict gates it;
  no automation grants acceptance across the boundary.

**Recommendation: 2C, layered on 2B.** The digest pin (2B) is retained as the P8 substrate;
the CPV record adds the P6 layer the boundary is missing — an independent actor ratifying
the crossing against source. The natural real anchor is **B2**: a projection of `EDR-0002`
into `context_switcher` carries a CPV validated by a Project-plane reviewer against the
Control source. If B2 does not land in 0.8, the **EKB-consumption** crossing (the knowledge
package validated against the pinned EKB object by a non-`RETRIEVE-0002` actor) is the
fallback anchor. **Trade-off / honesty (P2):** a full Review Plane does not exist as a
separate authority at `c02fe64` (FD-6: Review ships inside `ecf` until a trigger fires), so
the "consuming-plane reviewer" is, in 0.8, a **distinct recorded actor discharging the
Review responsibility**, not a separate repository. That is disclosed, not concealed — the
same honest ceiling FD-6 already sets.

## Item 3 — THE BOUNDARY CASE: make generator == validator unrepresentable across the boundary

**The question (charter):** a self-validated cross-plane artifact (generator == validator
across the boundary) is the P6 failure mode; the bar must reject it. Show how the
schema/gate makes it unrepresentable.

**The failure mode, concretely.** A Control actor projects `EDR-0002` into the Project plane
and *also* authors its CPV record with `validator_actor` = itself (or another actor holding
the *same* generating role). The bytes match; the record says `faithful`; nothing else
notices. This is P6 violated across a boundary: the producer is the sole ratifier.

**How the schema/gate forecloses it (recommended design).** The CPV record is a
**closed-field, fail-closed** record in the house style (the discipline proven by
`review_obligations.py` and `validate_report.py` — unknown fields rejected, required fields
absent → reject). Three interlocking guards make the self-validated crossing
**unrepresentable**:

1. **Distinct required actor fields.** `generator_actor` and `validator_actor` are **both
   required, closed** sub-records (each `{actor_id, plane_role}`). A CPV missing either is
   rejected (like a verdict missing `overall` — `gate.py` BLOCKs).

2. **Fail-closed non-identity check.** The CPV contract rejects, fail-closed, any record
   where `validator_actor.actor_id == generator_actor.actor_id` **or**
   `validator_actor.plane_role == generator_actor.plane_role` **or**
   `validator_actor` sits in the **source plane's** generating role. The gate that consumes
   the CPV verdict (a cross-plane sibling of C13) **BLOCKs** on a self-identity exactly as
   `gate.py` BLOCKs on an open blocker — *"the absence of a 'no' is never a 'yes'."* The
   dishonest value is not "discouraged"; it is **unrepresentable** — a CPV that names one
   actor as both cannot serialize to a valid record.

3. **Mechanical re-derivation defeats a colluding `faithful`.** Even a *distinct* validator
   cannot rubber-stamp: the contract recomputes `projection_digest` and re-resolves
   `source_digest`, so a `faithful` verdict over bytes that do not match is rejected — the
   `validate_report.py` asymmetry carried across the boundary (claiming faithful on a
   divergent projection → REJECTED; claiming divergent on a faithful one → allowed, safe
   direction).

**Recommendation:** adopt guards 1–3 as the CPV schema's fail-closed core. This makes the
P6 cross-plane failure mode *structurally impossible to record as a pass*, the same way
`review_obligations.py` makes `fully_reproducible`-with-no-model unrepresentable (the O12
precedent, PROPOSAL_07 O12-6). **Trade-off:** guard 2 enforces *role/identity* distinctness,
which is only as strong as the actor-identity the record carries; where a single human or a
single model legitimately holds two roles, the record must name the *distinct role under
which it validated*, and P7's institutional-continuity clause (Clarification C) supplies the
never-empty validating office. Disclosed as the residual seam, not hidden.

---

# Part II — PROPOSED O5 contribution to the 0.8 Partial bar

**What the O5 half of the 0.8 "demonstrably holds across planes" bar asserts:**
generation≠validation is a **universal, checkable** invariant within every workflow, **and**
it holds **across a plane boundary** for one real crossing, with the self-validated crossing
provably rejected. Written parametrically over the vehicles Items 1–3 recommend; the founder
rules the vehicles.

## II.1 The bar as enumerated clauses

**O5-1 — Universality is a released validator check (Item 1).** The
generation≠validation invariant is a **category-independent** workflow-validator check (the
ratified WF022 vehicle) at authoritative status. It requires, for every workflow producing a
consequential artifact, a validation task distinct from every consequential producer,
depending on it, binding a C13-routed verdict, and declaring `validates:`. **Negative
(fixture): a workflow spec stripped of its validate task — or one whose "validator" is the
producer itself — is REJECTED by the validator.** Both released workflows (`WF-REASON-0001`,
`WF-TRANSFORM-0001`) pass it unchanged.

**O5-2 — Within-plane independence holds mechanically, verdict gated by C13 (real, exists
today).** For each released workflow, the validate task's verdict is interpreted by the
frozen C13 gate reading **bound outputs only** (no generation internals), and the output
contract **re-derives ground truth and rejects the unsafe direction**. **Negative: a verdict
claiming `passed` over a non-conformant artifact is rejected (`validate_report.py` /
`validate_canonical_candidate.py`); a gate handed generation internals has no code path to
read them (`gate.py`).** Discharged by naming the real verdict identities
(`recommendation-report-validation.yaml` in a real reasoning run; the
`canonical-candidate-validation.yaml` of a real transform run).

**O5-3 — Actor-sharing is recorded, not concealed (P2 honesty ceiling).** Where, in a
single-executor run, the generating and validating tasks share one actor
(`runner.py` binds one `self.executor`; `reasoning-model.yaml` records one model per run),
that fact is **recorded** and the independence relied upon (mechanical re-derivation +
C13, scoped to the unsafe/structural direction) is **disclosed with its scope**. **Negative:
a claim of *actor-independent* validation for a single-executor run is rejected as
overclaim (P2).** True independent-actor validation (a distinct model/human ratifying) is
named as **deepening, explicitly OUT** (§II.4).

**O5-4 — One real cross-plane crossing carries a CPV validated by a non-generator (Item 2).**
The ratified cross-plane act (B2 projection of a canonical decision into `context_switcher`,
or the fallback EKB-consumption crossing) carries a real **CPV record** binding
`source_ref`+`source_digest` ↔ `projection_ref`+`projection_digest`, with a **fidelity
verdict** independently validated by a named actor discharging the **consuming plane's
Review responsibility** — an actor that is **not** the projector and **not** the source-plane
generator. The projection **confers no standing** in the consuming plane until the CPV
verdict gates it (P7). The discharged clause **names the identities**: the CPV record, the
source digest, the projection digest, the validator actor. **Negative: a projection with no
CPV record, or a CPV whose recomputed digests do not match its claim, confers nothing / is
rejected.**

**O5-5 — The self-validated crossing is unrepresentable (Item 3 — the P6 failure mode).**
The CPV schema requires distinct `generator_actor` and `validator_actor` and **rejects,
fail-closed**, any record whose validator equals the generator by `actor_id`, by
`plane_role`, or by source-plane generating role. **Negative pair: (i) a CPV naming one
actor as both generator and validator cannot serialize to a valid record (unrepresentable);
(ii) a distinct validator asserting `faithful` over bytes that do not match is rejected by
mechanical re-derivation.** A cross-plane projection validated by its own generator **fails
P6**, and the bar demonstrates the refusal on a fixture.

**O5-6 — REAL, not fixture (the 0.5–0.7 discipline).** Fixtures prove the negatives
(O5-1's stripped workflow, O5-5's self-identity refusal); **fixtures never discharge O5-4.**
The cross-plane clause is discharged only by a real CPV record on a real crossing, named by
identity. **Honesty rule (Clarification A, carried from PROPOSAL_07's O12A-5): if B2 does not
land in 0.8 and the EKB-consumption fallback is not stood up honestly, O5-4/O5-6 are recorded
UNMET-and-open and the O5 half ships at whatever is demonstrable — a cross-plane guarantee is
never manufactured to pass the bar (P2). Reality outranks the plan.**

## II.2 Artifact · demonstration · checker, per clause

| Clause | Artifact that proves it | Demonstration | Who checks |
|---|---|---|---|
| O5-1 | The ratified WF022 check + both released workflows passing it | Run the validator over both workflows (pass); over a fixture workflow with the validate task removed (**reject**) | Machine (validator) + Founder (ratifies the invariant + WF022) |
| O5-2 | Real `recommendation-report-validation.yaml` + `canonical-candidate-validation.yaml`; `gate.py` | Verdicts interpreted by C13; **negative**: PASS-over-broken rejected by the output contract | Machine (fail-closed contract + C13) + Independent validator |
| O5-3 | The run's `reasoning-model.yaml` + the disclosure that generation/validation shared it | Read the attestation; confirm the scope-of-independence disclosure; **negative**: an actor-independence claim over a one-executor run is refused | Machine (attestation) + Independent validator (P2 review) |
| O5-4 | The real CPV record + source/projection digests + the named non-generator validator | Walk source → projection; re-derive both digests; confirm the validator ≠ generator and discharges Review; the projection gates on the verdict | Machine (CPV contract) + consuming-plane reviewer + Founder (confirms the crossing is real) |
| O5-5 | The CPV schema + its fail-closed non-identity check | **Negatives**: self-identity CPV unrepresentable; distinct-validator `faithful`-over-mismatch rejected | Machine (fail-closed contract) + Independent validator |
| O5-6 | The real CPV identities (or the honest UNMET-and-open record) | The live crossing, identities named; or the recorded gap (Clarification A) | Founder (real vs synthetic) + Independent validator |

## II.3 Boundary cases — what explicitly does NOT count

1. **A digest pin is not a validation (O5-4).** A projection bound to its source by SHA with
   no CPV verdict satisfies P8, not P6. The independent verdict is the obligation; the pin is
   its substrate.
2. **The source-plane verdict does not travel (O5-4/O5-5).** "EDR-0002 was validated in
   Control, so its projection is validated" is verdict-inheritance-by-proxy — the copy is a
   new artifact with its own fidelity failure mode. The consuming plane validates the
   *crossing*, not the origin.
3. **A distinct validator who rubber-stamps still fails (O5-5).** Actor-distinctness alone is
   not sufficient; the mechanical re-derivation must independently support `faithful`. A
   `faithful` verdict over divergent bytes is rejected regardless of who signed it.
4. **A consuming-plane self-check is not cross-plane validation (O5-4).** `context_switcher`'s
   `acceptance_tests/` prove the bundle is intact and the integration runs (Project-plane
   wiring); they do not validate a projected Control decision against its Control source by a
   non-generator.
5. **WF022 passing is not O5-4 passing (O5-1 vs O5-4).** Universal *within-plane* structural
   separation (O5-1) and *cross-plane* independent validation (O5-4) are different guarantees;
   meeting one does not discharge the other.
6. **A fixture crossing discharges nothing real (O5-6).** A CPV over a test projection proves
   the contract's negatives only. The real clause names a real crossing.
7. **Actor-independent validation is not claimed where a single executor ran both (O5-3).**
   Recording "independently validated" for a one-model run, without the actor-sharing
   disclosure, is the P2 concealment the bar forbids.

## II.4 Partial vs deepening — deliberately OUT (P13)

- **True independent-*actor* validation within a single run.** Assigning a *distinct* model
  or human to the validate task (so generation and validation never share an actor even
  inside one run) is the strongest reading of P6 and is **deepening** — at 0.8 the invariant
  is structural (distinct task, C13-gated verdict, mechanical re-derivation) with the
  actor-sharing honestly recorded (O5-3). Named OUT so the met bar is not misread as
  "machine self-ratification solved."
- **A separated Review Plane repository/authority.** FD-6 keeps Review inside `ecf` until a
  trigger fires; the consuming-plane reviewer in O5-4 is a distinct recorded actor
  discharging the Review responsibility, not a new repo. Separation is deepening.
- **CPV for every cross-plane hop.** The bar demonstrates one real crossing. A CPV regime
  over *all* Knowledge consumptions and *all* projections (N consumers) is deepening.
- **Automated fidelity re-validation on drift.** The CPV is validated at crossing time;
  a daemon that re-validates when the source supersedes (the O1/O12 seam) is deepening and
  P7-constrained regardless.
- **Cross-plane supersession/propagation of a failed CPV.** A `divergent` verdict raises an
  obligation; propagating it into a supersession is the O7/O12 machinery, out of O5's scope.

## II.5 Bar-vs-reality baseline (v0.7.0 = `c02fe64`)

| Clause | Exists today (probed) | 0.8 must add |
|---|---|---|
| O5-1 | WF001–WF021; **no** universal validate-task check. WF015 is reasoning-terminal-only (self-skips otherwise); WF-TRANSFORM's validate task is spec-convention | The category-independent WF022 invariant + `validates:` block |
| O5-2 | **Live.** `validate_report.py` / `validate_canonical_candidate.py` re-derive and reject the unsafe direction; `verify_source_run.py` re-verifies digests; `gate.py` (C13) reads bound outputs only, fail-closed | Nothing structural — this clause is discharged by naming real verdicts; carried forward as the evidence base |
| O5-3 | `runner.py` binds one executor per run; `reasoning-model.yaml` records one model per run — generation and validation share the actor. No disclosure of that scope exists as a first-class statement | The recorded scope-of-independence disclosure + the P2 overclaim negative |
| O5-4 | **Nothing cross-plane.** EKB pinned by digest (P8); `durability.py` guards permanence (O8/FD-2); no CPV record type; B2 does not exist; consumer `acceptance_tests/` are Project-plane self-checks | The CPV record + a real crossing validated by a non-generator |
| O5-5 | The fail-closed closed-field idiom exists (`review_obligations.py`, `validate_report.py`) to build on; no actor-distinctness check exists | The CPV schema's distinct-actor requirement + fail-closed non-identity check |
| O5-6 | The candidate real anchors exist: `canonical/decisions/EDR-0002/` (projectable), the EKB pin (consumable). Neither has ever crossed a plane under validation | One real CPV, identities named — or the honest UNMET-and-open record |

---

# Part III — Spec appendix (proposed vehicles; the founder rules the design)

### A. WF022 — independent-validation invariant (workflow-validator check)

- **Inputs (already parsed by the validator):** the binding table, the `depends_on` DAG, the
  step list.
- **New machine-readable spec element:** a `validates:` block per validation task, e.g.
  ```yaml
  validates:
    TASK-VALIDATE-0001:
      - TASK-PRODUCE-0001
  ```
- **Consequential-artifact rule (structural, no new vocabulary needed for the two released
  workflows):** the workflow's terminal deliverable under `reports/` (for WF-REASON:
  `engineering-recommendation-report.md`; for WF-TRANSFORM:
  `candidate-canonical-artifact.md`), plus any output flagged `consequential: true`.
- **Check (fail-closed):** for each consequential producer P, there exists a validation task
  V with (a) V ≠ P; (b) P ∈ transitive `depends_on*(V)`; (c) V's bound output is C13-routed
  (a verdict envelope with an `overall` block — the shape `gate.py` consumes); (d) P ∈
  `validates[V]`. Missing any ⇒ **WF022 FAIL**. Reuses WF008/WF012 graph machinery.

### B. Cross-plane validation (CPV) record — closed-field, fail-closed

```yaml
schema_version: 0.1.0
record_type: cross_plane_validation
record_id: CPV-<consuming-plane>-<seq>
crossing_kind: projection | consumption          # Control→Project, or *→consume(Knowledge)
source:
  plane: control | knowledge
  ref: canonical/decisions/EDR-0002/EDR-0002.md   # tracked or digest-bound (durability.py)
  digest_sha256: <64-hex>
projection:
  plane: project | control
  ref: <consuming-plane path>
  digest_sha256: <64-hex>
generator_actor:      { actor_id: <id>, plane_role: <role> }   # who projected/consumed
validator_actor:      { actor_id: <id>, plane_role: <role> }   # who ratified (Review resp.)
fidelity:
  result: faithful | divergent | stale
  rederived_source_digest: <64-hex>       # recomputed by the contract, not trusted
  rederived_projection_digest: <64-hex>
confers_standing: false                   # P7: no standing until the gate passes
recorded_at: <iso8601>
```

- **Fail-closed contract (mirrors `verify_source_run.py` + `validate_report.py`):**
  recompute both digests from bytes on disk; reject `faithful` unless
  `rederived_* == digest_sha256` for both. Reject the record if `validator_actor.actor_id ==
  generator_actor.actor_id`, or `validator_actor.plane_role == generator_actor.plane_role`,
  or `validator_actor` holds the source plane's generating role. Unknown fields rejected;
  required fields absent ⇒ reject.
- **Cross-plane gate (a sibling of C13):** consumes the CPV verdict, reads bound record only
  (never generation internals), fails closed; `confers_standing` flips to `true` only on an
  affirmative, coherent, non-self-validated verdict — and standing that confers acceptance
  remains **human-gated** (P7).

### C. Actor-scope disclosure (O5-3)

A one-line first-class statement bound to a run/crossing declaring the **scope** of the
independence claimed: `independence: mechanical_and_structural` (single-executor run,
unsafe-direction + C13) vs `independence: actor_distinct` (a distinct validator actor). The
validator/CPV contract rejects `actor_distinct` unless generator and validator actor ids
actually differ. This is the P2 guard against overclaim.

---

# Part IV — Cross-consistency check

1. **P6 honored and made checkable, within and across planes.** Within: O5-1 (universal
   structural check) + O5-2 (mechanical re-derivation + C13). Across: O5-4 (CPV by a
   non-generator) + O5-5 (self-validation unrepresentable). The proposal adds the *checkable
   form* of P6, not a reinterpretation. **Consistent.**
2. **P2 honored first.** O5-3 records actor-sharing rather than claiming actor independence;
   §II.4 names the deepening OUT; O5-6 carries PROPOSAL_07's honesty rule (UNMET-and-open
   over manufacture). **Consistent** — the met bar cannot be misread as "machine
   self-ratification solved."
3. **P7 honored across the boundary.** O5-4's projection confers no standing until gated;
   the cross-plane gate never grants acceptance (PROGRAM_0.8 edge P7: *"no automation grants
   approval/acceptance across a boundary"*). Reuses the C13 *"a gate never approves"*
   discipline. **Consistent.**
4. **P8 reused, not weakened.** The CPV's `source`/`projection` digest binding rides
   `durability.py`'s fail-closed permanence rule (a live cross-plane reference is tracked or
   digest-bound, never a bare mortal `runtime/` cite). O5 depends on O8's substrate; it does
   not duplicate it. **Consistent** (O8 seam is records-only, per charter).
5. **The ratified 0.5–0.7 bars are not contradicted.** C13 stays frozen and only-stricter;
   the output contracts are reused verbatim; the CPV fail-closed idiom is the
   `review_obligations.py` / `validate_report.py` pattern carried across the boundary. WF022
   is additive to WF001–WF021. **Consistent.**
6. **Tension 1 (flagged) — the cross-plane real act depends on B2, which does not exist at
   `c02fe64`.** O5-4/O5-6 name B2 as the primary anchor and the EKB-consumption crossing as
   the fallback, and carry the Clarification-A honesty rule so the exit does not silently
   block: if neither real crossing is stood up honestly in 0.8, the cross-plane half is
   recorded UNMET-and-open, and the *within-plane universality* half (O5-1/O5-2/O5-3) can
   still ship. Flagged so the founder rules the anchor, not stumbles into it. This is the O5
   analogue of PROPOSAL_07 tension 1.
7. **Tension 2 (flagged, design-constraining) — actor identity is only as strong as what the
   record names.** O5-5 guard 2 enforces role/identity distinctness; where one human or one
   model legitimately holds two roles, the record must name the distinct validating role, and
   P7 Clarification C supplies the never-empty validating office. The vehicle must rule the
   actor-identity model explicitly or the check enforces a distinctness the records cannot
   express. A sequencing cost, resolvable; flagged.
8. **Tension 3 (flagged, honesty-guarding) — within-plane "independence" is mechanical, and
   the bar says so.** O5-2's mechanical contract catches the unsafe direction; the *semantic*
   validation in a single-executor run is same-actor (Part 0 fact 3). The bar does not claim
   actor independence for those runs (O5-3), and names actor-distinct validation OUT. A reader
   who mistakes the met O5 bar for "machine cannot self-ratify, ever" has misread it against
   P2 — §II.4 and O5-3 exist to foreclose that.

---

## Metadata

| Field | Value |
|---|---|
| Status | **RATIFIED (Founder, 2026-07-17)** — O5 authorized to build; within-plane independence = mechanical (actor-sharing recorded per O5-3); cross-plane = distinct-actor |
| Owner Role | Program Steward (WS-0) / Workshop O5 |
| Change class | T1 Operational (the workshop + bar contribution); the WF022 landing and the cross-plane gate are **T4 when built** (they touch the P6 boundary) — flagged, not pre-authorized |
| Recommendations (one line each) | **Item 1 (UNIVERSAL):** lift generation≠validation to a category-independent workflow-validator invariant (WF022) — distinct validate task, depends on the generator, C13-routed verdict, `validates:` block; a workflow without it fails, in every category. · **Item 2 (CROSS-PLANE):** add a cross-plane validation (CPV) record binding source↔projection by digest, validated by a non-generator actor discharging the *consuming* plane's Review responsibility; the projection confers no standing until the CPV gate passes (P7). · **Item 3 (BOUNDARY):** make generator==validator unrepresentable — CPV requires distinct `generator_actor`/`validator_actor`, fail-closed on actor/role identity, plus mechanical digest re-derivation so a colluding `faithful` is rejected. |
| Key finding | Generation≠validation is enforced **per-workflow (convention) + mechanically (fail-closed output contract on the unsafe direction) + gated by C13** — **NOT** as a universal validator invariant (WF015 is reasoning-terminal-only; a new workflow with no validate task passes WF001–WF021) and **NOT** by an independent actor (`runner.py` binds one executor per run; `reasoning-model.yaml` records one model per run, so generation and validation share the actor). **Across a plane boundary it is not enforced at all** — no cross-plane validation record exists; the EKB is pinned by digest (P8), which is not validation (P6). |
| Evidence probed | `ecf` @ `c02fe64` (read-only): `tools/workflow_validator/validate_workflow.py` (WF001–WF021; WF015 self-skip line 680), `tools/review_gate/gate.py` (C13, fail-closed, bound-outputs-only), `tools/task_runner/output_contracts/{validate_report.py, validate_canonical_candidate.py, verify_source_run.py}`, `tools/task_runner/{runner.py (one executor per run, l.86), reasoning_attestation.py (one model per run), executor.py}`, `workflows/reasoning/WF-REASON-0001-*` (Step 15), `workflows/transformation/WF-TRANSFORM-0001-*` (Step 5, CHK-C7), `canonical/decisions/EDR-0002/reproducibility-state.yaml`, `tools/reproducibility/durability.py` · `context_switcher` (read-only): `acceptance_tests/{check_consumer_integration.sh, check_bundle_integrity.sh}` |
| Cross references | [PROGRAM_0.8](PROGRAM_0.8.md) Workshop O5 · [PLATFORM_PRINCIPLES](PLATFORM_PRINCIPLES.md) (P6, P2, P7, P8, Clarification A/C) · [PLATFORM_ARCHITECTURE](PLATFORM_ARCHITECTURE.md) §4.4 Review Plane, §5, FD-6 · [PROPOSAL_06_PARTIAL_BARS](PROPOSAL_06_PARTIAL_BARS.md) · [PROPOSAL_07_PARTIAL_BARS](PROPOSAL_07_PARTIAL_BARS.md) (bar precedent) · O8 seam: [PROPOSAL_O12_MIGRATION_SCOPE] `durability.py` (records-only) |
