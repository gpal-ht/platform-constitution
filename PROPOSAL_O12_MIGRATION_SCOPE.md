# PROPOSAL — O12 Track B: Reasoning Migration & Degraded-Reproducibility States

> **Status: RATIFIED (Founder, 2026-07-17) — model recording via run-level attestation
> (Option B, no frozen-contract touch).** This is the Track B scope-workshop
> deliverable required by [PROGRAM_0.7](PROGRAM_0.7.md) ("Track B workshop → founder
> ratification → build"). It **decides nothing**; it resolves the five Track B
> design-open items into options + trade-offs + a single recommendation each, grounded
> in a read-only probe of the real surfaces, and proposes an O12 Track-B Partial-bar
> contribution with evidence-checkable clauses and negatives. No build. The Founder rules.

| Field | Value |
|---|---|
| Milestone | 0.7.0 — Lifetime Reasoning Integrity (O12 → **Partial**) |
| Track | **B** — reasoning migration + degraded-reproducibility states (the OQ-001 research core) |
| Charter | [PROGRAM_0.7](PROGRAM_0.7.md) Track B (five design-open items) + folded-in FD-2 permanence obligation |
| Worktree | `C:\Dev\ecf-wt-o12b` @ `feature/0.7-o12-migration` (off `develop` @ `16ee325` = v0.6.0) |
| Evidence base | Read-only probe of real run `RUN-REASON-20260716-0002`, its executor and provenance, `canonical/decisions/EDR-0002/`, `challenges/CHG-20260716-0001/`, `assumptions/ASM-*`, `tools/task_runner/`, `tools/workflow_planner/env_scope.py` |
| Governing edge | **P2** — no mechanism may claim reproducibility it does not deliver; `irreproducible` and `degraded` are honest, first-class outcomes (Clarification A) |
| Precedents | PROPOSAL_05/06_PARTIAL_BARS (clause discipline, negatives, real-not-fixture); PROPOSAL_O7/O11 (record-type scoping); FD2_DECISION_MEMO (the named exposure) |
| Author | Track B scope-workshop thread (one of three 0.7 background threads; strict isolation) |
| Date | 2026-07-17 |

---

## 0. Framing — what Track B is, and its three hard boundaries

O12 is the platform's **weakest** obligation and its only Research-stability one. The
ratified architecture (§4.6) says plainly of the Reasoning Plane: *"declaring it built
would violate P2."* Track B therefore does **not** attempt to solve lifetime
reproducibility of judgment. It builds the **honest substrate** underneath it: a run
records **which model produced its judgment**; a decision carries a **first-class,
fail-closed reproducibility state** that can never over-claim; and the model-independent
inputs a future re-evaluation needs are made **durable** so the state means something.

Three boundaries constrain every recommendation below:

1. **Records-only seam with Track A.** Track A (dependency graph + invalidation
   propagation) is an **interface**, not a dependency. Track B defines record *types* and
   the fields Track A will read/write; it takes **no dependency on Track A's output** and
   ships independently. Where a field belongs to invalidation (e.g. "this state was
   marked stale by a propagated invalidation"), Track B reserves the field and leaves it
   `null` — it does not implement the propagation.
2. **O12-scoped permanence, not a runtime-permanence project.** Design-open #4 folds in
   FD-2's Control-owned permanence obligation, but **only to the exact extent O12 needs**:
   every *permanent record a reproducibility-state points to* must be durable. It is
   explicitly **not** general `runtime/` versioning; EKB canonicalization (B1) and
   projection (B2) stay deferred and non-gating, per the PROGRAM_0.7 carryover ruling.
3. **Everything PROPOSED; humans decide (P7).** No mechanism here invalidates,
   supersedes, re-judges, or accepts a migration. Machines evaluate and record; the
   accountable office disposes.

---

## 1. Design-open #1 — Model identity in provenance

### 1.1 Probe result: **NO — the reasoning model is not recorded anywhere today.**

Confirmed against the real run behind EDR-0002 (`RUN-REASON-20260716-0002`) and the code:

- **Per-task provenance** (`runtime/runs/RUN-REASON-20260716-0002/provenance/TASK-*.yaml`)
  records, as its only executor fact, `executor:\n  id: claude-code`. That is the
  **executor host id**, not the model. The reasoning model (`claude-opus-4-8`) appears in
  **no** field of any of the 18 provenance files.
- **The runner writes that line, and only that line.**
  `tools/task_runner/runner.py` → `_build_provenance()` emits
  `["executor:", f"  id: {getattr(self.executor, 'id', 'fixture')}", ...]`. The executor
  object's `id` is the class constant `ClaudeCodeExecutor.id = "claude-code"`
  (`tools/task_runner/executors/claude_code.py`). Provenance is **runner-owned** —
  the executor "NEVER writes the final runtime output, generates provenance, …"
  (module docstring). So the model can only enter provenance via the runner.
- **The invocation command is not persisted either.** The executor runs `self.command`
  + `self.fixed_args` through a subprocess and captures stdout; even if a `--model` flag
  lived in `fixed_args`, nothing writes it to a durable record — the diagnostics that *do*
  carry `duration`/`exit` are explicitly "no secrets" and are not committed to provenance.
- **The env-scope fingerprint deliberately excludes the model.**
  `tools/workflow_planner/env_scope.py` fingerprints **code** — runner/planner/validator,
  the executor *modules*, task specs, bundled EKB — by content hash. Its integrity
  argument enumerates the behavior surface as "run inputs + task/workflow text + EKB +
  runtime + executor/contract module closure." The **external model is never
  fingerprinted** (it is not a repo file; static import analysis cannot see it). This is
  correct for its purpose (resume-cascade scoping) but means the H2 machinery gives O12
  **zero** coverage of model identity.
- **Manifest, `run-record.json`, and the EDR-0002 evidence bundle** are all silent on the
  model. `manifest.yaml` records `executor: {type: none, has_run: false}` (the fixture
  planning header); `run-record.json` records task/gate outcomes; the EDR bundle carries
  the *report* and governance records but no model attestation.

**Consequence for O12:** reproducibility-over-time is impossible without this (P8/P9).
Today **no decision can honestly claim `fully_reproducible`**, because the identity of the
judge is unrecorded. Closing this is the precondition for everything in §2–§5.

### 1.2 Options

| Option | What it is | Cost / risk |
|---|---|---|
| **A — Amend the per-task provenance contract** | Add an additive `reasoning_model:` block (id, version, provider, recorded_by) under the existing `executor:` key of every AI task's `provenance/TASK-*.yaml`; bump `schema_version`. | Re-opens the **frozen** provenance contract (`schema_version: 1`) → **T4 amendment** (the same discipline H2's `env_scope` fields went through — see runner.py "C5 T4 amendment" note). Heavy: touches every task record; model is a **run-level** fact recorded 18× per run. |
| **B — Run-level model attestation (sidecar record)** | The **runner** writes one new run-level record, `reasoning-model.yaml`, at run start/first AI task: `{model_id, model_version, provider, executor_id, declared_by, recorded_at, applies_to: <run_id>}`. Provenance contract **untouched**. The model becomes a first-class, digest-bindable artifact the EDR bundle can carry. | New record type (small). Binds at run granularity, which matches reality (one model per run in the observed pipeline). Needs the runner to *know* the model — see §1.4. |
| **C — Executor self-reports the model into its output/diagnostics** | The executor declares the model in the JSON envelope or diagnostics; runner lifts it. | **Rejected.** Violates the runner-owns-provenance boundary and P6 (generation attesting its own provenance). A model that names itself is not independently recorded. |

### 1.3 Recommendation

**Adopt B (run-level attestation), and flag A as a founder call, not a default.**

- **B is the minimal honest capture.** A model is a per-run fact; recording it once, by
  the runner, as a digest-bindable sidecar (that the EDR evidence bundle then carries,
  §4) captures P8/P9 identity **without re-opening the frozen per-task provenance
  contract carelessly**. It is the same shape as the assumption/challenge records O11/O7
  added: a new record type, not a mutation of an existing frozen one.
- **A is a T4 amendment — flag it, don't smuggle it.** If the Founder wants the model
  bound at *task* granularity (defensible: different tasks could one day use different
  models), that is a deliberate T4 amendment of the provenance contract, reviewed as
  such — **not** something this workshop should slip in under "additive field." Track B
  recommends **B now**; **A only on an explicit founder ruling** that per-task binding is
  required. **The provenance contract must not be re-opened without a recorded T4
  decision** (this is the discipline flag the charter asks for).

### 1.4 The one real dependency this creates

The runner can only attest a model it is *told*. Today the executor invokes an opaque
`command`; the model is a property of that command's environment, not of ECF config. So B
requires the **executor to declare its model identity to the runner as configuration**
(an executor capability field, e.g. `ClaudeCodeExecutor(model_id=…, model_version=…)`
supplied at construction from run config), which the runner records verbatim. This keeps
the executor from *writing* provenance (it only *declares* a config value the runner
commits) and keeps the attestation honest: an executor with **no declared model** yields
**no attestation**, and §5's fail-closed rule then forbids any affirmative reproducibility
claim for that run. (Whether the declared value can be *verified* against the real API
model is out of scope and OUT of Partial — see §6.)

---

## 2. Design-open #2 — Degraded-reproducibility state vocabulary

### 2.1 The record type

A **first-class, per-decision `reproducibility-state` record**, keyed to a canonical
decision (EDR). It answers one question honestly: *can this decision's judgment be
reproduced today, and if not, what would a re-evaluation need?* It is **fail-closed** and
its state field is a **closed enum of exactly three values**:

| State | Meaning | Preconditions the validator enforces |
|---|---|---|
| `fully_reproducible` | The judging model is still available **and** every model-independent input is durable. | (i) a resolvable `reasoning-model` attestation (§1); (ii) the model is marked **available** by a recorded availability assertion; (iii) **all** cited inputs are durable (§4). Missing any ⇒ **not representable** (§5). |
| `degraded` | The model is **gone or unavailable**, but the recorded inputs + a substitute model would let a human re-evaluate. Names the original model and **what a re-evaluation needs**. | (i) a resolvable original-model identity; (ii) all model-independent inputs durable; (iii) a populated `reevaluation_requirements` block. |
| `irreproducible` | The decision cannot be reproduced or re-evaluated — the model identity was never captured, or required inputs are not durable and cannot be recovered. **First-class, non-shameful (P2).** | Requires an **explicit recorded reason** (enum, §2.2). Never a silent default. |

There is **no fourth "mostly reproducible" value** — that is the P2 point (§5). Anything
short of the `fully_reproducible` preconditions collapses to `degraded` or
`irreproducible`, both of which are honest.

### 2.2 The closed schema (summary; full draft in Appendix B)

```
reproducibility-state:
  schema_version: "0.1.0"
  record_id:            RSTATE-<EDR>-<seq>
  decision_ref:         EDR-0002            # the canonical decision this state describes
  decision_record_sha256: <digest of EDR-0002.md at state time>
  state:                fully_reproducible | degraded | irreproducible   # CLOSED enum
  reasoning_model:                          # resolved from the §1 attestation; REQUIRED unless state=irreproducible w/ reason=model_never_recorded
    model_id:           claude-opus-4-8
    model_version:      <declared>
    attestation_ref:    <path to reasoning-model.yaml> + sha256
  model_availability:   available | unavailable | unknown   # CLOSED enum; recorded assertion, never inferred
  model_independent_inputs:                 # each MUST be durable (§4) or the record fails closed
    - name: approved-report
      durable_ref: canonical/decisions/EDR-0002/evidence/engineering-recommendation-report.md
      sha256: 40db94c5…b54eaf
    - name: assumptions
      durable_ref: assumptions/ASM-0001/assumption.yaml
      sha256: <…>
  reevaluation_requirements:                # REQUIRED iff state=degraded; forbidden iff fully_reproducible
    substitute_model_needed: true
    inputs_needed: [approved-report, assumptions, decision-options]
    note: "Re-evaluate OPT-0003 disposition under a substitute model against the bound inputs."
  irreproducible_reason:                    # REQUIRED iff state=irreproducible; CLOSED enum
    model_never_recorded | input_not_durable | input_lost | model_and_substitute_unavailable
  invalidation_ref:     null                # Track A seam — reserved, records-only, left null by Track B
  recorded_by:          { actor, recorded_at }
```

### 2.3 Fail-closed semantics

The validator **refuses to write** a record that: omits a required cross-field block,
carries an out-of-enum value, claims a state whose preconditions are unmet, or cites a
non-durable input. There is no "best effort" write. A run that cannot substantiate any
affirmative state produces, at most, `irreproducible` with an explicit reason — never a
silent or optimistic value. This is the P2 edge implemented as a contract (§5).

### 2.4 Recommendation

Adopt the three-value closed enum and the fail-closed cross-field contract above. Bind
each `reproducibility-state` to its EDR by the decision's record digest so the state is
falsifiable against the exact bytes it describes (P8), and reserve `invalidation_ref` for
Track A without implementing it (records-only seam).

---

## 3. Design-open #3 — What reasoning migration means

### 3.1 The honest definition

The assumptions and evidence a decision rests on are **model-independent recorded
artifacts** (already digest-bound: ASM-0001 pins `source_sha256` into a canonical
evidence copy; the EDR-0002 bundle pins the report). The **judgment** — the disposition
`gather_additional_evidence`, the selection of `OPT-0003` — was **model-dependent**: it
was produced by `claude-opus-4-8` reading those inputs.

**Migration is therefore NOT re-running to get identical bytes.** It is:

> Re-evaluating a **standing decision** under a **different model** against the **same
> recorded, digest-bound inputs**, and **recording the comparison** between the original
> judgment and the substitute model's judgment — then routing that comparison to the
> accountable office as a candidate, never auto-accepting it (P7).

A migration record **must never claim byte-identical reproduction**; the schema makes that
claim unrepresentable (there is no "reproduced: true / identical" field — only a
comparison outcome).

### 3.2 The migration record (summary; full draft in Appendix C)

```
reasoning-migration:
  schema_version: "0.1.0"
  record_id:            MIG-<EDR>-<seq>
  decision_ref:         EDR-0002
  original:
    model: { model_id, model_version, attestation_ref + sha256 }
    judgment_digest:    <sha256 of the original approved report / recommendation>
  substitute:
    model: { model_id, model_version }
    reevaluation_run_ref: <run_id + durable output ref + sha256>   # may be null if specified-not-run (§6)
  inputs_reused:                              # the SAME digest-bound inputs both models saw
    - { name, durable_ref, sha256 }
  comparison:
    outcome:            concordant | divergent | inconclusive   # CLOSED enum — never "identical"
    summary:            "<what differs / agrees, by recorded ID>"
  disposition:                                # P7 — a human decides what the comparison means
    routed_to:          accountability
    human_decision:     pending | accept_migration | reject | supersede_candidate
  recorded_by:          { actor, recorded_at }
```

### 3.3 Recommendation

Specify the migration record type as above. **Whether an actual cross-model re-run is
executed within 0.7 is a specified-not-demonstrated mechanism** — recommend it, but leave
it to the bar ruling (see §6). The schema is written so a migration can be **fully
specified** (original judgment digest + reused input digests + the substitute model named)
**without** a re-run having occurred (`substitute.reevaluation_run_ref: null`,
`comparison.outcome: inconclusive`), which is itself an honest state. The comparison enum
deliberately omits any "identical/reproduced" value so P2 is enforced structurally.

---

## 4. Design-open #4 — Evidence permanence (folded-in FD-2 obligation)

### 4.1 The exact live exposure (grounded in the real store)

A degraded/reproducible state is meaningless if what it points to dies. The FD-2 memo
names the exposure precisely; the probe confirms its **exact shape today**:

- **The live dangling pointer (the FD-2-named exposure).**
  `challenges/CHG-20260716-0001/disposition.yaml` is a **versioned, permanent** governance
  record. Its `evidence[1].ref` is
  `runtime/runs/RUN-TRANSFORM-20260716-0002/reports/candidate-canonical-artifact.md` — a
  path under `runtime/`, which is **gitignored** (mortal). Critically, that evidence entry
  carries **no `sha256` and no digest-bound copy** — it is a **bare pointer into a mortal
  path**. The moment that checkout is cleaned (`git clean`), a ratified disposition's
  evidence chain dangles. This is a live P8 exposure **today**, exactly as FD-2 §2 item 1
  states.
- **What is NOT exposed (and why the distinction matters for scope).** The EDR-0002
  evidence bundle (`canonical/decisions/EDR-0002/evidence-manifest.yaml`) also *mentions*
  `runtime/runs/RUN-REASON-20260716-0002/...` — but only as `origin_path`
  **back-references**, alongside a **digest-bound byte copy** under
  `canonical/decisions/EDR-0002/evidence/*` with a pinned `sha256`. Those are durable
  (the `origin_path` is a provenance breadcrumb, not a live dependency). Likewise
  `assumptions/ASM-0001` pins `source_sha256` into a canonical evidence copy — durable.
  **So the O12 permanence hole is narrow and specific: it is bare mortal pointers with no
  digest-bound copy** (the disposition), plus (from §1) the fact that the **model identity
  itself has no durable home at all**.

### 4.2 What O12 needs — and only that

Two closable gaps, scoped to exactly what a reproducibility-state requires:

1. **Every permanent record a reproducibility-state (or migration record) points to must
   be durable** — meaning either *versioned* (tracked git path) or *digest-bound* (a
   sha256-pinned copy under a tracked path with an `origin_path` back-reference). A
   **bare mortal pointer fails closed.** Concretely this obliges the challenge-disposition
   pattern (and any O12 record) to carry a digest-bound copy of anything it cites from
   `runtime/`, exactly as the EDR promotion tool already does for the report. This closes
   the FD-2-named exposure **using the mechanism that already exists** (`canonical_*`
   digest-bound copy), not a new store.
2. **The `reasoning-model` attestation (§1) must be carried into the decision's durable
   bundle**, so the identity of the judge survives with the decision. The EDR evidence
   bundle is the natural home; promotion carries `reasoning-model.yaml` as one more
   digest-bound evidence item.

**Explicitly OUT of O12 scope** (deferred, non-gating, per PROGRAM_0.7): general
`runtime/` versioning; a new Operational-Evidence store; EKB canonicalization (B1);
projection (B2); external-boundary evidence capture (FD-2 re-open trigger territory). O12
does **not** make `runtime/` permanent — it makes *the specific things a reproducibility
state depends on* permanent, and it makes *citing a mortal path without a durable copy*
an error.

### 4.3 Recommendation

Adopt the **durability rule** as a fail-closed contract on O12 record types (and,
recommended, extend the same rule to the challenge-disposition writer to close the exact
FD-2 exposure): **a permanent O12 record may cite a `runtime/` path only when a
digest-bound durable copy accompanies it; a bare mortal citation is rejected.** Reuse the
existing `canonical_promotion` digest-bound-copy mechanism; introduce **no** new store.
This is the Control-owned permanence obligation FD-2 created, discharged at exactly O12's
scope.

---

## 5. Design-open #5 — P2 honesty enforced in the schema

The constitutional edge of 0.7: **a state that claims reproducibility it cannot deliver
must be *unrepresentable*, and `irreproducible` must be a first-class, non-shameful
outcome.** The schema enforces this four ways — none of them relying on the author's good
intentions:

1. **Closed enum, no optimistic middle.** `state ∈ {fully_reproducible, degraded,
   irreproducible}` only. There is no `partially_reproducible`, no `likely`, no boolean
   `reproducible: true`. The vocabulary itself cannot express an over-claim.
2. **`fully_reproducible` is gated by cross-field preconditions, checked by the
   validator, fail-closed.** It is writable **only if** (a) a `reasoning-model`
   attestation resolves (§1), (b) `model_availability: available` is a *recorded*
   assertion (never inferred from silence), and (c) **every** `model_independent_inputs`
   entry is durable (§4). Fail any ⇒ the validator **refuses** `fully_reproducible`; the
   honest record is `degraded` or `irreproducible`. The claim is literally unrepresentable
   without its evidence.
3. **`irreproducible` is first-class and carries no penalty.** It is a valid terminal
   value requiring only an **explicit recorded reason** (closed enum). It has no "failure"
   flag, no remediation-required field — it is an honest recorded outcome, exactly as the
   Vision frames OQ-001 as "not an embarrassment." What is **forbidden** is reaching it
   *silently*: absence of a model attestation does not auto-stamp `irreproducible`; it
   requires `irreproducible_reason: model_never_recorded` to be written and reviewed.
4. **No "identical/reproduced" field anywhere.** Migration records (§3) compare with a
   closed `{concordant, divergent, inconclusive}` enum. The system **cannot** claim
   byte-identical reproduction of a model-dependent judgment because no field exists to
   carry that claim.

**Net:** the only way to *record* `fully_reproducible` is to *have* the model identity and
durable inputs. The only way to record `irreproducible` is to *state why*. P2 stops being
a review-time judgment call and becomes a contract the writer cannot evade.

---

## 6. PROPOSED — O12 Track-B Partial-bar contribution

> These clauses turn PROGRAM_0.7 founder bar **2(b)** — *"one REAL run carries a recorded
> degraded-reproducibility state naming its reasoning model (`claude-opus-4-8`) and what a
> future re-evaluation would need"* — into evidence-checkable exit criteria with
> negatives. They compose with the Track A clauses (bar 2a) and the Partial-bars thread,
> which owns the final ratified wording. Written parametric where a founder ruling could
> change them. **Fixtures prove the negatives; they never discharge a REAL clause.**

### 6.1 The clauses

**O12B-1 — Model identity is recorded for a REAL run.** The real run behind a standing
decision (`RUN-REASON-20260716-0002` → EDR-0002) carries a durable, resolvable
`reasoning-model` attestation naming `claude-opus-4-8` (§1, Option B), captured by the
runner from executor-declared config, and carried into the decision's durable bundle (§4).

**O12B-2 — A REAL decision carries a recorded reproducibility state.** EDR-0002 has a
`reproducibility-state` record (§2) whose `state` is substantiated by its cross-field
preconditions, bound to the EDR by record digest. Given the model is presently available,
the honest real value is `degraded` **or** `fully_reproducible` per §5's gate — and the
record **names what a re-evaluation would need** (`reevaluation_requirements`), satisfying
bar 2(b) verbatim.

**O12B-3 — The reasoning-migration record type is specified and schema-valid.** The
migration record (§3) exists as a validated type: a decision's original judgment digest +
reused input digests + a substitute model can be recorded, with a `{concordant, divergent,
inconclusive}` comparison and a **human** disposition (P7). *(Executing a real cross-model
re-run is OUT of Partial — see §6.3.)*

**O12B-4 — The folded-in FD-2 exposure is closed under the durability rule.** No permanent
O12 record cites a mortal `runtime/` path without a digest-bound durable copy; the durable
copy of anything a reproducibility state depends on is present and digest-verifiable (§4).
*(Recommended, and checkable: the specific `challenges/CHG-20260716-0001/disposition.yaml`
bare-pointer exposure is remediated by the same rule.)*

**O12B-5 — Fail-closed negatives demonstrated (fixtures).** The three contract negatives
below reject, fail-closed.

**O12B-6 — Independent verification.** An independent validator (O5/P6) confirms the real
state record's preconditions actually resolve against the real store (model attestation
resolves; every cited input digest verifies) — not merely that a record was written.

### 6.2 The three required negatives (fixtures only)

| # | Negative | Enforced by |
|---|---|---|
| **NEG-1** | A `reproducibility-state` for a run with **no recorded reasoning model** cannot claim **any affirmative** state: `fully_reproducible` and `degraded` both assert a named model and are **rejected**; `irreproducible` is admissible **only** with `irreproducible_reason: model_never_recorded` explicitly recorded — never as a silent default. | §5.2 / §5.3 cross-field contract, fail-closed |
| **NEG-2** | A permanent O12 record (state or migration) that **cites a mortal `runtime/` path with no digest-bound durable copy** is **rejected** (closes the FD-2 dangling exposure). | §4 durability rule, fail-closed |
| **NEG-3** | A record asserting **`fully_reproducible` while the model id is unrecorded**, or while any cited model-independent input is **not durable**, is **rejected** — the assertion is unrepresentable. | §5.2 precondition gate, fail-closed |

These are proved on **fixtures**. Per the ratified clause discipline (PROPOSAL_05/06), a
fixture store — however complete — satisfies **only** the negative/positive contract
tests; the REAL clauses (O12B-1, O12B-2) name **real identities in the real store**
(`RUN-REASON-20260716-0002`, `claude-opus-4-8`, `EDR-0002`).

### 6.3 Deliberately OUT of the Partial bar (P13 / P2)

| Item | Why OUT | Disposition |
|---|---|---|
| **Executing a real cross-model re-run** (running EDR-0002's inputs through a substitute model and recording a real `comparison`) | A genuine research mechanism; valuable but not required to demonstrate *honest state-keeping*. The migration record type can be Partial-complete as **specified-not-demonstrated**. | **Recommend**; let the bar ruling decide whether one real re-run is in-scope for 0.7. |
| **Verifying the declared model against the live API** (that `claude-opus-4-8` really produced the bytes) | Requires trusting/querying an external boundary; the attestation is a *recorded declaration*, honest at that level (P2). | Deferred; note the honest ceiling in the record. |
| **Automated model-availability probing / a model registry** | `model_availability` is a *recorded assertion* in 0.7, not a live probe. | Deferred; `unknown` is a valid value. |
| **Live invalidation propagation** (marking a state stale when a dependency is invalidated) | Track A's obligation; Track B only reserves `invalidation_ref` (records-only seam). | Track A. |
| **General `runtime/` permanence / new evidence store / EKB canonicalization (B1) / projection (B2)** | Beyond exactly what O12 needs (§4.2); PROGRAM_0.7 carryover ruling keeps them deferred, non-gating. | Deferred. |

### 6.4 Partial vs the honest ceiling (Strong)

**Partial (this bar):** the substrate is honest — the judge is *identified*, the decision
*declares* whether it can be reproduced and what a re-evaluation needs, over-claiming is
*unrepresentable*, and the evidence a state depends on is *durable*. **Strong (explicitly
not 0.7):** re-evaluation is routinely *executed* across models, comparisons *demonstrated*
at scale, and availability *actively verified*. Declaring Strong now would violate P2 — the
architecture's own words for O12. This bar is the honestly-minimal, demonstrated mechanism
the milestone asks for, and nothing more.

---

## 7. Exists-today vs. must-add (probed)

| Capability | Exists today (probed) | 0.7 Track B must add |
|---|---|---|
| Reasoning model in provenance | **Nothing.** `executor: {id: claude-code}` only; env_scope fingerprints code, "never the model" | Runner-written `reasoning-model.yaml` attestation from executor-declared config (§1 Option B) |
| Reproducibility state per decision | **Nothing.** EDRs carry disposition + evidence, no reproducibility state | `reproducibility-state` record type, closed 3-value enum, fail-closed (§2) |
| Reasoning migration record | **Nothing** | `reasoning-migration` record type, `{concordant,divergent,inconclusive}`, human disposition (§3) |
| Model-independent input durability | **Partial.** EDR bundle + ASM digest-bound (durable); **but** `disposition.yaml` cites a **bare mortal** `runtime/` path (no sha256, no copy) — live FD-2 exposure | Durability rule (fail-closed) on O12 records + carry model attestation into the bundle; remediate the disposition bare pointer (§4) |
| P2 over-claim prevention | **Nothing** (no state vocabulary exists to over-claim yet) | Closed enum + precondition-gated `fully_reproducible` + no "identical" field (§5) |
| Invalidation → state staleness | **Nothing** (Track A) | Reserve `invalidation_ref` only; **records-only seam**, no implementation |

---

## Appendix A — `reasoning-model.yaml` (run-level attestation, §1 Option B)

```yaml
# runtime/runs/<RUN>/reasoning-model.yaml  (runner-written; carried into the EDR bundle at promotion)
schema_version: "0.1.0"
record_type: reasoning_model_attestation
run_id: RUN-REASON-20260716-0002
applies_to: all_ai_tasks            # run-level; a T4 provenance amendment (Option A) would bind per-task instead
model:
  model_id: claude-opus-4-8         # declared by the executor as config; NOT self-reported in output (P6)
  model_version: "<declared>"       # provider-declared version string, verbatim
  provider: anthropic
executor_id: claude-code            # the host that carried the model (matches provenance executor.id)
declared_by:
  source: executor_config           # runner records the declared value verbatim; executor never writes this file
  recorded_by: task_runner
recorded_at: "<UTC>"
# Honest ceiling (P2): this is a recorded DECLARATION of model identity, not an API-verified attestation.
```

## Appendix B — `reproducibility-state` (§2, §5)

```yaml
schema_version: "0.1.0"
record_type: reproducibility_state
record_id: RSTATE-EDR-0002-0001
decision_ref: EDR-0002
decision_record_sha256: 4b8f1de3addda22498c9af30a6821bc6c05edbc0a5e2dd484610ebd701439b2d
state: degraded                      # CLOSED: fully_reproducible | degraded | irreproducible
reasoning_model:                     # REQUIRED unless state=irreproducible AND reason=model_never_recorded
  model_id: claude-opus-4-8
  model_version: "<declared>"
  attestation_ref: canonical/decisions/EDR-0002/evidence/reasoning-model.yaml
  attestation_sha256: "<…>"
model_availability: unknown          # CLOSED: available | unavailable | unknown  (recorded, never inferred)
model_independent_inputs:            # each MUST be durable (versioned or digest-bound) or the record fails closed
  - name: approved-report
    durable_ref: canonical/decisions/EDR-0002/evidence/engineering-recommendation-report.md
    sha256: 40db94c5aac0091a002412cd192b7b04e10cd26c020fda59d9adc746b3b54eaf
  - name: assumptions
    durable_ref: assumptions/ASM-0001/assumption.yaml
    sha256: "<…>"
reevaluation_requirements:           # REQUIRED iff state=degraded; FORBIDDEN iff state=fully_reproducible
  substitute_model_needed: true
  inputs_needed: [approved-report, assumptions, decision-options]
  note: "Re-evaluate the OPT-0003 gather_additional_evidence disposition under a substitute model against the bound inputs."
irreproducible_reason: null          # REQUIRED iff state=irreproducible; CLOSED:
                                     #   model_never_recorded | input_not_durable | input_lost | model_and_substitute_unavailable
invalidation_ref: null               # Track A seam — reserved, records-only, left null by Track B
recorded_by: { actor: "<office>", recorded_at: "<UTC>" }
```

**Validator (fail-closed) obligations:** reject if — `state` out of enum; `state:
fully_reproducible` with any unmet precondition (no resolvable attestation, availability ≠
`available`, or any non-durable input); `state: degraded` with empty
`reevaluation_requirements` or unresolvable model; `state: irreproducible` with no
`irreproducible_reason`; any `model_independent_inputs` entry whose `durable_ref` is a
mortal path lacking a digest-bound copy (§4); `decision_record_sha256` not matching the
cited EDR bytes.

## Appendix C — `reasoning-migration` (§3)

```yaml
schema_version: "0.1.0"
record_type: reasoning_migration
record_id: MIG-EDR-0002-0001
decision_ref: EDR-0002
original:
  model: { model_id: claude-opus-4-8, model_version: "<declared>",
           attestation_ref: canonical/decisions/EDR-0002/evidence/reasoning-model.yaml, attestation_sha256: "<…>" }
  judgment_digest: 40db94c5aac0091a002412cd192b7b04e10cd26c020fda59d9adc746b3b54eaf   # the original approved judgment's bytes
substitute:
  model: { model_id: "<substitute>", model_version: "<…>" }
  reevaluation_run_ref: null          # null = specified-not-run (an honest state; §6.3)
  reevaluation_output_sha256: null
inputs_reused:                        # the SAME digest-bound inputs the original judgment saw
  - { name: approved-report, durable_ref: canonical/decisions/EDR-0002/evidence/engineering-recommendation-report.md, sha256: 40db94c5…b54eaf }
  - { name: assumptions,    durable_ref: assumptions/ASM-0001/assumption.yaml, sha256: "<…>" }
comparison:
  outcome: inconclusive               # CLOSED: concordant | divergent | inconclusive — NEVER "identical/reproduced"
  summary: "Specified only; no substitute re-run executed (OUT of Partial)."
disposition:                          # P7 — a human decides; no automation accepts a migration
  routed_to: accountability
  human_decision: pending             # CLOSED: pending | accept_migration | reject | supersede_candidate
recorded_by: { actor: "<office>", recorded_at: "<UTC>" }
```

## Appendix D — The durability rule (§4, folded-in FD-2 obligation)

```
DURABLE(ref) :=  ref is a versioned tracked git path
             OR  ref is digest-bound: a sha256-pinned copy under a tracked path,
                 carrying an origin_path back-reference (the existing canonical_promotion pattern)

RULE (fail-closed): a permanent O12 record (reproducibility-state, reasoning-migration)
  may cite a runtime/ (mortal, gitignored) path ONLY when a DURABLE copy accompanies it
  with a verifiable sha256. A bare mortal citation is REJECTED.

SCOPE: exactly the inputs a reproducibility-state / migration record depends on, plus the
  reasoning-model attestation carried into the decision bundle. NOT general runtime/
  permanence, NOT a new store, NOT EKB canonicalization (B1) or projection (B2).

RECOMMENDED EXTENSION (closes the exact FD-2-named exposure): apply the same rule to the
  challenge-disposition writer, so challenges/CHG-20260716-0001/disposition.yaml's
  evidence[1] bare pointer into runtime/runs/RUN-TRANSFORM-20260716-0002/... gains a
  digest-bound copy or is refused.
```

---

## 8. Risks, blockers, and open questions for the Founder

1. **T4 discipline (§1).** Recommendation B avoids re-opening the frozen provenance
   contract. If the Founder wants per-task model binding (Option A), that is a **T4
   amendment** and must be ruled as one — **flagged, not smuggled**. *Blocker only if the
   Founder requires per-task binding.*
2. **Executor must declare its model (§1.4).** B depends on the executor exposing
   `model_id`/`model_version` as config the runner records. Today the executor invokes an
   opaque command; wiring a declared model is a small, real change — but it is the one new
   coupling this scope introduces. *Risk: a declared model that isn't API-verified — noted
   as the honest ceiling; verification is OUT of Partial.*
3. **P2 tension is the entire point (§5).** The strongest failure mode is a future
   contributor adding an optimistic value (`partially_reproducible`, `reproduced: true`)
   "for convenience." The closed enum + precondition gate is the defense; **the founder
   ruling should lock the enum closed** so it cannot be widened without constitutional
   review.
4. **Real state value for EDR-0002.** With `claude-opus-4-8` presently available, the
   honest real state is `fully_reproducible` *iff* §5's preconditions all resolve
   (attestation present, availability recorded `available`, inputs durable) — otherwise
   `degraded`. Bar 2(b) literally asks for a **degraded** state naming the model. Two
   honest readings: (a) record `degraded` because availability cannot be *verified* (only
   asserted), satisfying 2(b) as written; (b) record `fully_reproducible` and demonstrate
   the *degraded path* on a fixture where the model is marked unavailable. **Recommend (a)
   for the REAL clause** (it is the more honest posture and matches the bar's wording),
   with (b)'s fixture proving the machinery — *founder to confirm which the real clause
   requires.*
5. **Track A seam is records-only (§0, §2).** `invalidation_ref` is reserved and left
   null. If Track A's identity model (their design-open #1) changes what a state must
   reference, only the reserved field's *shape* changes — no Track B mechanism depends on
   Track A shipping. *Low risk by construction.*
6. **Scope creep into a permanence project (§4).** The durability rule must stay scoped to
   "what a reproducibility state points to." The explicit OUT list (§6.3, Appendix D)
   guards this; the FD-2 memo's own boundary (no new Plane, no new store) is the anchor.

---

### Cross references
- [PROGRAM_0.7](PROGRAM_0.7.md) (Track B charter, founder bar 2b) ·
  [PLATFORM_PRINCIPLES](PLATFORM_PRINCIPLES.md) (Root "throughout their lifetime",
  Clarification A, P2, P7, P8, P9) · [PLATFORM_VISION](PLATFORM_VISION.md) Open Question 001 ·
  [PLATFORM_ARCHITECTURE](PLATFORM_ARCHITECTURE.md) §4.6 Reasoning Plane, §4.7 FD-2 ruling ·
  [FD2_DECISION_MEMO](FD2_DECISION_MEMO.md) (the named dangling-evidence exposure) ·
  [PROPOSAL_06_PARTIAL_BARS](PROPOSAL_06_PARTIAL_BARS.md) (clause discipline, negatives)
- Probe evidence (read-only): `RUN-REASON-20260716-0002/provenance/TASK-*.yaml`,
  `.../manifest.yaml`, `.../run-record.json`; `tools/task_runner/runner.py`
  (`_build_provenance`); `tools/task_runner/executors/claude_code.py`;
  `tools/workflow_planner/env_scope.py`; `canonical/decisions/EDR-0002/` (record +
  evidence-manifest); `challenges/CHG-20260716-0001/disposition.yaml`;
  `assumptions/ASM-0001/assumption.yaml`.

---

| Field | Value |
|---|---|
| Owner | Founder (rules); Track B thread (drafts) |
| Status | **RATIFIED (Founder, 2026-07-17)** — Track B authorized to build; model recording = Option B (run-level attestation) |
| Created | 2026-07-17 (post v0.6.0) |
