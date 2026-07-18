# PROPOSAL — 0.5 Partial Exit Bars (O3 · O4)

> **Status: RATIFIED (Founder, 2026-07-16).** Non-constitutional (T1). This
> proposal turns the two *proposed* bars recorded in [PROGRAM_0.5](PROGRAM_0.5.md)
> (Track A design-open item 4; Track B design-open item 4) into precise,
> evidence-checkable exit criteria, following the 0.4 precedent
> ([PROGRAM_0.4](PROGRAM_0.4.md): "O10 Partial = Specified + minimal enforcement";
> "O6 Partial = descriptive model + one executable rule"). Nothing here is ratified;
> the founder rules at the scope workshops. This document does not modify
> PROGRAM_0.5.md.

| Field | Value |
|---|---|
| Derives from | [PROGRAM_0.5](PROGRAM_0.5.md) (kicked off 2026-07-16) · [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md) 0.5.0 |
| Bars proposed | **O3 Partial** (Track A) · **O4 Partial** (Track B) |
| Precedent | PROGRAM_0.4 exit bars + its "0.4 exit-bar status" bar-vs-reality tracking |
| Evidence baseline probed | `ecf` @ `9a96563` (branch `chore/0.5-partial-bars` worktree) + real run `RUN-REASON-WR0001-V040-0002` (main checkout, read-only) |
| Change class | T1 Operational (a bar refinement; obligations and milestone exit are already ratified in the roadmap) |

---

## How to read a bar (the 0.4 discipline, made explicit)

A Partial bar is met only when **every clause** below has (a) a named **artifact** that
exists, (b) a named **demonstration** that was actually run, and (c) a named **checker**
who verified it. Per P2 (honesty guard), a clause with an artifact but no demonstration,
or a demonstration nobody checked, is an **explicit gap**, never a pass. Per the
roadmap's honesty guard, 0.5 is claimed only when both bars are met, validated, and
released.

Checker vocabulary used below:

- **Machine (fail-closed contract)** — an output contract / validator in `ecf` that
  rejects the nonconformant case; the negative test is part of the demonstration.
- **Independent validator (O5/P6)** — an actor (human or machine) other than the
  generator of the artifact being checked.
- **Founder** — ratification under Genesis; the only checker who can mark a clause
  *ratified* rather than *proposed/demonstrated*.

---

# Part I — O3 Partial bar (Track A: `WF-TRANSFORM-0001`)

**Proposed bar (PROGRAM_0.5, restated):** specification released **+ one real approved
recommendation transformed** into a canonical artifact with evidence/review/acceptance
recorded.

## I.1 The bar as enumerated clauses

**O3-1 — Specification released.** `WF-TRANSFORM-0001` (*Approved Recommendation →
Canonical Artifact*) has a complete specification under the frozen workflow-execution
discipline and has traversed the catalog status ladder to **`released`**
(`planned → draft → review → approved → released`), including a defined
acceptance-test file.

**O3-2 — Entry gate = a recorded human approval, verified fail-closed.** The workflow's
entry state is a **recorded human approval** of an Engineering Recommendation, authored
by a human outside any automated run (P7). TRANSFORM verifies the approval record
against the halted reasoning run it approves — binding at minimum `run_id` and the O6
`approval_authority` role — and **rejects** a missing, malformed, unbound, or
mis-attributed approval before executing anything.

**O3-3 — Narrow canonical-artifact definition ratified.** The first canonicalization
target (artifact type + where canonical artifacts live) is defined **narrowly**, ruled
at the scope workshop, and explicitly does **not** depend on O10's full model contract
(founder ruling 1, PROGRAM_0.5).

**O3-4 — One real transformation executed.** One **real** approved recommendation — an
approval authored against a genuine halted `WF-REASON-0001` run (the standing candidate
is `RUN-REASON-WR0001-V040-0002`, the formal 18/18 halt) — is transformed into a
canonical artifact by an authoritative run of the released workflow.

**O3-5 — Evidence, review, and explicit acceptance recorded as first-class run
outputs (P3).** The transformation run records: (a) the **evidence set** supporting
canonicalization, (b) an **independent review** whose validator is separate from the
generator (O5 discipline), and (c) an **explicit acceptance** record. A canonical
artifact missing any of the three is the P3 failure mode ("canonical by existence"),
not a pass.

**O3-6 — Provenance end-to-end (P8).** The canonical artifact is traceable through an
unbroken chain: Work Request → reasoning run → recommendation report → human approval
record → transformation run → evidence/review/acceptance → canonical artifact, at the
same standard as `WF-REASON-0001` (immutable final manifest, trace, completion record).

## I.2 Artifact · demonstration · checker, per clause

| Clause | Artifact that proves it | Demonstration that verifies it | Who checks |
|---|---|---|---|
| O3-1 | `workflows/transformation/WF-TRANSFORM-0001-*.md` + its `acceptance_tests/` file + `workflows/WORKFLOW_CATALOG.md` entry showing `status: released` | Structural validation against `WORKFLOW_EXECUTION_SPECIFICATION.md` (all tasks resolve, versions pinned, DAG acyclic, run root canonical); acceptance tests pass; catalog status transitions recorded | Machine (structural validation) + Founder (release of the spec) |
| O3-2 | The approval-record schema + the entry-gate contract module (task-runner output contract or entry validator) | Positive: a conformant approval admits the run. **Negative: the run is rejected on (i) no approval record, (ii) `run_id` mismatch, (iii) a role that does not hold `approval` authority in the pinned model version** — mirroring `trace_completion.py`'s fail-closed pattern | Machine (fail-closed contract); negative tests reviewed by an independent validator |
| O3-3 | A ratified scope-workshop ruling (target type, canonical home — consumer repo vs Control-Plane outputs) recorded in the Track-A scope document | Inspection: the definition names one artifact type and its location, and cites no O10 full-contract element (no migration policy / identity semantics dependency) | Founder (ruling) + Program Steward (traceability check) |
| O3-4 | The transformation run directory under `runtime/runs/<RUN_ID>/` + the produced canonical artifact at its ratified home | A live authoritative run of the `released` workflow, consuming the real approval; the run reaches its successful exit state | Machine (workflow contracts) + Founder (confirms the input approval was real, not synthetic) |
| O3-5 | Three first-class run outputs: evidence-set record, review record, acceptance record (schemas ruled at the workshop) | The run's completion contract **rejects** a transformation whose evidence, review, or acceptance output is absent or empty (negative test); the review record's validator identity differs from the generator identity (O5 check) | Machine (fail-closed contract) + independent validator (the reviewer itself, by construction) |
| O3-6 | `reports/final-manifest.yaml`, `reports/trace.md`, completion record of the transformation run; the canonical artifact carries a provenance reference back to the approval record and reasoning `run_id` | Walk the chain from canonical artifact back to WR-0001 with no gap; the immutable final manifest (not the mutable runtime manifest) is the terminal evidence, per the WF021 discipline already enforced in `trace_completion.py` | Machine (manifest/trace contracts) + independent validator (chain walk) |

## I.3 Boundary cases — what explicitly does NOT count

1. **A synthetic or fixture approval does not count as "one real approved
   recommendation" (O3-4).** An approval record fabricated for testing, an approval of
   a fixture run, or an approval authored by an automated executor fails the clause.
   The consumed approval must be a human-authored acceptance of a genuine
   recommendation from a real halted reasoning run. (Fixture approvals are still
   *required* — as negative/positive test inputs for O3-2 — they just don't satisfy
   O3-4.)
2. **A canonical artifact without a recorded explicit acceptance is the P3 failure
   mode, not a pass (O3-5).** Likewise an artifact whose "evidence" is the artifact's
   own existence, or whose "review" was performed by its generator (P6 violation).
3. **A demonstration run of a `draft`/`review` workflow does not count (O3-1/O3-4).**
   The catalog is explicit: only a `released` workflow may be selected for an
   authoritative run. A transformation executed while the spec sits below `released`
   is a non-authoritative validation run — useful, but not the bar.
4. **An approval that merely exists near the run does not count (O3-2).** If TRANSFORM
   does not *verify* the approval against the halted run (run_id + authority binding),
   the entry gate is discipline, not enforcement — the same distinction 0.4 drew for
   O10 ("detected, not left to discipline").
5. **Specification completeness without a runner does not count as O3-4.**
   `WF-REASON-0001` history is the precedent: spec-complete and runtime-live are
   tracked independently; the bar requires the live run.

## I.4 Partial vs Strong — deliberately OUT of the Partial bar (P13)

- **More than one canonicalization target / artifact type.** One narrow type is the
  bar; a general canonicalization taxonomy is deepening.
- **The O10 full model contract for canonical artifacts** (identity semantics,
  migration policy, cross-repo projection). Explicitly severed by founder ruling 1.
- **Supersession of canonical artifacts (P14/O7).** Corrigibility of what 0.5
  canonicalizes is the 0.6 milestone, not this bar.
- **Automated evidence sufficiency judgment.** For Partial, the contract checks that
  evidence/review/acceptance records *exist and are well-formed*; judging evidence
  *quality* remains with the human reviewer. Encoding sufficiency rules is deepening.
- **Batch/repeatable canonicalization throughput.** One real transformation is the
  bar; operationalizing a pipeline is deepening.

## I.5 Bar-vs-reality baseline (what exists today at `9a96563` vs what 0.5 must add)

| Clause | Exists today (probed evidence) | 0.5 must add |
|---|---|---|
| O3-1 | `WF-TRANSFORM-0001` is listed in `workflows/WORKFLOW_CATALOG.md` as **`planned`** only ("not yet specified … must not be referenced by the Orchestration Engine until `released`") | The entire specification + acceptance tests + ladder traversal to `released` |
| O3-2 | **No approval record exists anywhere.** The real run's `reports/completion.yaml` records `approval_granted: false`, `next_action: request_human_approval` — the halt is proven; the approval it awaits has never been authored. The O6 binding pattern to imitate is live in `trace_completion.py::_check_approval_authority_binding` (fail-closed, model-version-pinned) | The approval-record schema, where the human writes it, and the fail-closed entry gate that verifies it |
| O3-3 | Nothing — first canonicalization target is a design-open workshop item | The founder ruling |
| O3-4 | The consumable upstream input **exists and is real**: `runtime/runs/RUN-REASON-WR0001-V040-0002/` — 18/18 tasks completed, `final_run_status: waiting_for_human_approval`, validated report + trace + immutable final manifest | The human approval of it, then the transformation run |
| O3-5 | Nothing for transformation. The *pattern* exists: `WF-REASON-0001` separates validation from generation (O5) and its contracts fail closed | Evidence/review/acceptance as first-class outputs of the new workflow + their contract |
| O3-6 | Provenance discipline is live for reasoning runs (provenance/, trace, immutable final manifest, WF021 rule in `trace_completion.py`) | Extending the unbroken chain across the approval record into the transformation run |

---

# Part II — O4 Partial bar (Track B: stewardship & challenge routing)

**Proposed bar (PROGRAM_0.5, restated):** authority model 0.2.0 ratified **+ vacancy
fallback enforced at runtime + one challenge routed to a recorded disposition**.

## II.1 The bar as enumerated clauses

**O4-1 — Authority model 0.2.0 ratified.** The model binds the stewardship-relevant
authorities — `ownership` → stewardship transfer; `accountability` → challenge
disposition — with an explicit `MODEL_VERSION` bump to `0.2.0` and a **compatibility
note** (the first exercise of O10's compatibility semantics). Existing 0.1.0 bindings
(`approval` → approval) are unchanged. **Precondition:** the founder's
governance-classification ruling (constitutional amendment vs T-band change) lands
*before* the bump — the Track-B workshop opens with it.

**O4-2 — Runtime role-state seam made real.** Role/holder state (active · vacant ·
superseded) becomes **runtime data consulted by an enforced check**, not the
descriptive module constant it is today. The seam 0.4 declared ("O4's runtime job at
0.5") is closed: at least one contract path calls the role-state check and fails
closed on it.

**O4-3 — Vacancy fallback enforced at runtime (Clarification C).** When the
accountable office is vacant, responsibility routes **mechanically** to the
institution's standing authority (Founder under Genesis) — never to nowhere. A record
attributing an action to a vacant office without the fallback binding is **rejected**
by contract, and the fallback routing itself is recorded (who actually held the
responsibility, and why).

**O4-4 — One challenge routed to the accountable office (Clarification B, first
half).** A challenge artifact — bound to the consequential decision it challenges —
demonstrably **reaches** the office holding `accountability` authority in model 0.2.0
(or its Clarification-C fallback).

**O4-5 — The challenge receives a recorded disposition (Clarification B, second
half).** The disposition record exists, is settled **by evidence** (P4), is authored by
the role holding `accountability` authority in model 0.2.0 (verified against the model,
fail closed), and is durably bound to both the challenge and the challenged decision.

**O4-6 — Compatibility preserved.** Runs and records conformant to model 0.1.0
semantics remain valid where the compatibility note says they do; specifically, the
released 0.4 evidence (the real run's `approval_authority` binding at `0.1.0`) is not
retroactively invalidated. The version-evolution discipline is documented well enough
to serve as O10's first compatibility exercise.

## II.2 Artifact · demonstration · checker, per clause

| Clause | Artifact that proves it | Demonstration that verifies it | Who checks |
|---|---|---|---|
| O4-1 | Updated `tools/authority_rule/authority_model.py` (`MODEL_VERSION = "0.2.0"`; `ownership`/`accountability` bindings non-empty) + the ratified model document + the compatibility note + the recorded governance-classification ruling | Model tests: 0.2.0 bindings hold; a record pinning an unknown version fails closed (the existing `holds_authority` fail-closed behavior, re-proven at 0.2.0) | Founder (ratification, after the classification ruling) + Machine (model tests) |
| O4-2 | The role-state store (runtime data, schema ruled at workshop) + the contract module that consults it (successor of the `_ROLE_STATE` / `role_is_active` seam) | Positive: an active-holder record passes. Negative: the check actually fires — flipping a role to `vacant` changes contract behavior (proves it is consulted, not decorative) | Machine (fail-closed contract) + independent validator (reviews that the check is on an enforced path) |
| O4-3 | The fallback-routing record (vacant office → institutional standing authority) + the rejecting contract | Negative pair: (i) an action attributed to a vacant office **with no fallback binding** is rejected; (ii) the same action with the recorded Founder-fallback binding passes, and the routing record shows who held the responsibility | Machine (fail-closed contract) + Founder (confirms the fallback attribution is truthful) |
| O4-4 | The challenge artifact (schema, location, binding to the challenged decision — workshop items) + a routing/receipt record showing it reached the accountable office | A live routing of one real challenge: artifact created, receipt recorded; a challenge addressed to a role without `accountability` authority is rejected or re-routed (negative test) | Machine (routing contract) + the accountable office (acknowledges receipt) |
| O4-5 | The disposition record: evidence cited, disposition stated, author's role + `model_version: 0.2.0` binding | Contract verifies fail-closed that the disposition's author holds `accountability` in 0.2.0 and that the record binds challenge ↔ decision ↔ disposition; a disposition without cited evidence is rejected (P4 check) | Machine (fail-closed contract) + independent validator (evidence citation is real, not decorative) |
| O4-6 | The compatibility note + regression evidence | Full regression suite green (0.4 precedent: 774 passed); the archived 0.1.0-bound run record (`RUN-REASON-WR0001-V040-0002/reports/completion.yaml`) still validates under whatever the note says applies to historical records | Machine (regression) + Program Steward (note review) |

## II.3 Boundary cases — what explicitly does NOT count

1. **A challenge routed but without a recorded disposition fails Clarification B
   (O4-5).** Reaching an inbox is half the obligation; "a challenge that reaches no
   accountable recipient is not a challenge," and one that reaches a recipient who
   never records a disposition is answered by silence — the same failure. Equally: a
   disposition recorded by a role that does not hold `accountability` authority in
   0.2.0 fails, exactly as a mis-attributed approval fails the O6 rule today.
2. **A vacancy handled by convention rather than enforced fallback fails
   Clarification C (O4-2/O4-3).** "The Founder just answers when nobody else does" is
   the descriptive status quo — 0.4 already has that on paper. The bar is the
   *mechanical* route: the contract must reject the no-fallback case. If flipping a
   role to `vacant` changes nothing at runtime, the seam is still descriptive and the
   clause is unmet.
3. **A synthetic challenge against a fixture decision does not count for O4-4/O4-5.**
   The routed challenge must target a real consequential decision (a natural first
   candidate: a challenge against the 0.5 canonical artifact or the pending WR-0001
   approval — coordinating with Track A per the workshop's role-binding item).
   Fixture challenges remain necessary as contract test inputs; they do not satisfy
   the "one challenge routed" clause.
4. **Bumping `MODEL_VERSION` without the compatibility note fails O4-1/O4-6.** The
   bump was explicitly ruled to double as O10's first compatibility exercise; a bare
   constant change discharges neither.
5. **A disposition "by decision" without cited evidence fails O4-5.** P4: challenges
   settle by evidence, not by the authority of the disposer — even when the disposer
   is the correctly-bound accountable office.

## II.4 Partial vs Strong — deliberately OUT of the Partial bar (P13)

- **Stewardship transfer executed end-to-end.** 0.2.0 *binds* `ownership` →
  stewardship transfer (the model half); demonstrating a live transfer with historical
  chain preservation is deepening. Only vacancy-fallback enforcement is the runtime
  clause for Partial.
- **Succession and escalation enforcement.** Doctrine E describes them; Partial
  enforces vacancy fallback only. Escalation-path enforcement is deepening.
- **General challenge intake** (arbitrary challengers, arbitrary decisions,
  SLAs/timelines on dispositions). One challenge, one office, one disposition is the
  bar.
- **The O10 full model contract** for the authority model itself (migration tooling,
  identity semantics). The 0.2.0 note exercises compatibility semantics only.
- **Cross-repo / cross-plane routing.** The bar lives inside `ecf` + platform
  governance records; routing across repositories is deepening.

## II.5 Bar-vs-reality baseline (what exists today at `9a96563` vs what 0.5 must add)

| Clause | Exists today (probed evidence) | 0.5 must add |
|---|---|---|
| O4-1 | `authority_model.py` at `MODEL_VERSION = "0.1.0"`; `ownership` and `accountability` are **empty frozensets** — the model literally cannot express challenge-disposition authority today. Version pinning + fail-closed unknown-version behavior already proven (rule tests 6/6) | The 0.2.0 bindings, the bump, the compatibility note, the classification ruling |
| O4-2 | The seam exists **descriptively**: `_ROLE_STATE = {r: "active" for r in ROLES}` is a hard-coded module constant; `role_is_active()` is defined but consulted by **nothing** (its own docstring: "The Partial rule does not consult this; a 0.5/O4 vacancy check would") | Role state as runtime data + an enforced consulting check |
| O4-3 | Clarification C is ratified text (PLATFORM_PRINCIPLES 0.2.0, AMENDMENT_O6); zero runtime mechanism | The fallback routing record + the rejecting contract + the negative test |
| O4-4 | **No challenge artifact, schema, or routing mechanism exists anywhere in `ecf`** (repo-wide probe found the term only in unrelated KB/task/defect prose) | Everything: schema, location, decision binding, routing, receipt |
| O4-5 | Nothing. The nearest pattern is the fail-closed authority binding now **live** in `trace_completion.py::_check_approval_authority_binding` (note: PROGRAM_0.4 recorded this wiring as "remaining"; commit `9a96563` shows it landed and its ratification recorded — the O6 executable half is runtime-live, a *stronger* baseline than the program doc states) | The disposition record + its fail-closed authority/evidence contract |
| O4-6 | The real archived evidence to protect: `RUN-REASON-WR0001-V040-0002/reports/completion.yaml` carries `approval_authority: {role: approval, authority: approval, model_version: "0.1.0"}` | The note's ruling on historical records + regression proof |

---

# Part III — Cross-consistency check (both bars vs PROGRAM_0.5 constitutional edges)

1. **P7 is not re-opened — no automation approves.** Nothing in either bar grants,
   automates, or simulates approval. O3-2 makes the *human-authored* approval the
   workflow's entry precondition; the reasoning halt (`waiting_for_human_approval`)
   is upstream and untouched — the frozen invariant (`approval_granted: false` inside
   reasoning runs) is not relaxed by any clause. TRANSFORM **consumes** an approval a
   human wrote; it never produces one. O4's disposition authority (O4-5) is likewise
   a *recording-and-verification* rule about who answered a challenge — it moves the
   recommend/approve boundary for no one. **Consistent.**
2. **P3's explicit-acceptance gate is the point, not a side effect.** O3-5 makes
   evidence/review/acceptance contract-enforced run outputs; boundary case I.3-2 names
   the canonical-by-existence failure explicitly. **Consistent** with PROGRAM_0.5's
   second constitutional edge.
3. **Achievable without O10's full contract (founder ruling 1).** O3-3 severs the
   canonical-artifact definition from O10 by construction (and the checker verifies no
   full-contract element is cited). O4-1/O4-6 use only O10's *compatibility semantics*
   — deliberately, as the ruled "first exercise" — and depend on no migration/identity
   machinery. Neither bar blocks on background-lane H1. **Consistent.**
4. **Anti-Capture / asymmetric burden.** O4-1's precondition (classification ruling
   before the bump) preserves the possibility that Track B is ruled constitutional; if
   so, the amendment discipline applies to the model change without altering these
   clauses — the clauses state *what must be true*, not the change class that gets it
   ratified. **Consistent.**
5. **One noted tension (flagged, not resolved here):** the catalog rule "only a
   `released` workflow runs authoritatively" means O3-4's real transformation cannot
   precede O3-1's release — the clauses are strictly ordered, unlike 0.4's tracks
   where the enforcement half pre-existed the specification. The schedule must absorb
   a full ladder traversal before the single demonstrating run. This is a sequencing
   cost, not a contradiction.

---

## Metadata

| Field | Value |
|---|---|
| Status | **RATIFIED (Founder, 2026-07-16)** — these bars are the 0.5 exit criteria |
| Owner Role | Program Steward (WS-0) |
| Change class | T1 Operational |
| Derives from | [PROGRAM_0.5](PROGRAM_0.5.md) · [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md) 0.5.0 · [PLATFORM_PRINCIPLES](PLATFORM_PRINCIPLES.md) (P2, P3, P4, P5, P6, P7, P8, P13, Clarifications B/C) |
| Evidence probed | `ecf` worktree `chore/0.5-partial-bars` @ `9a96563`: `workflows/WORKFLOW_CATALOG.md`, `tools/authority_rule/{authority_model.py, check_authority.py, tests/}`, `tools/task_runner/output_contracts/trace_completion.py` · main checkout (read-only): `runtime/runs/RUN-REASON-WR0001-V040-0002/reports/{completion.yaml, final-manifest.yaml, trace.md, engineering-recommendation-report.md}` |
| Cross references | [PROGRAM_0.4](PROGRAM_0.4.md) (bar precedent) · [AMENDMENT_O6_RESPONSIBILITY_AUTHORITY](AMENDMENT_O6_RESPONSIBILITY_AUTHORITY.md) |
