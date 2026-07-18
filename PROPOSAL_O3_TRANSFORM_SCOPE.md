# PROPOSAL_O3_TRANSFORM_SCOPE — Track A (O3) scope resolution for 0.5.0

> **Status: RATIFIED (Founder, 2026-07-16).** Non-constitutional (T1 working
> proposal that organizes delivery of a ratified capability). This document does **not**
> ratify anything — it resolves the Track A *design-open* items from
> [PROGRAM_0.5](PROGRAM_0.5.md) as **options + a recommendation** per item, mirroring the
> 0.4 scope-workshop precedent ([PROPOSAL_O6_SCOPE](PROPOSAL_O6_SCOPE.md),
> [PROPOSAL_O10_SCOPE](PROPOSAL_O10_SCOPE.md)). The founder rules; then Track A builds.
>
> Obligation: **O3 — canonicalization by evidence/review (P3, P4).** Vehicle (founder
> ruling, 2026-07-16 kickoff): **`WF-TRANSFORM-0001`** — *Approved Recommendation →
> Canonical Artifact*, beginning exactly where `WF-REASON-0001`'s proven
> `waiting_for_human_approval` halt ends. Canonical-artifact definition scoped
> **narrowly**; not gated on O10's full model contract.

---

## 0. What is already true (findings, not proposals)

Six facts from the repositories anchor every recommendation below.

1. **The halt is real and its shape is known.** A real reasoning run exists at
   `ecf/runtime/runs/RUN-REASON-WR0001-V040-0002/` — 18/18 tasks completed, final state
   `waiting_for_human_approval`. Its `reports/completion.yaml` records the P7 boundary
   (`approval_required: true`, `approval_granted: false`) **plus** the O6 binding
   `approval_authority: {role: approval, authority: approval, model_version: "0.1.0"}`,
   enforced fail-closed by `tools/task_runner/output_contracts/trace_completion.py`
   (reusing the ratified role→authority table in `tools/authority_rule/`).

2. **The artifact model already carries the canonical seam.** The recommendation report
   (`reports/engineering-recommendation-report.md`, contract
   `artifacts/ENGINEERING_RECOMMENDATION_REPORT_CONTRACT.md`) declares in front matter:
   `generated: true`, **`canonical: false`**, `approval_status: pending_human_approval`.
   The framework has always said this artifact is *not yet canonical* — O3 is the missing
   mechanism that can ever truthfully flip that state, and P3 says only evidence + review
   + explicit acceptance may do it.

3. **`runtime/` is gitignored** (`ecf/.gitignore`: `runtime/`). Run outputs — including the
   report a human approves — are **not version-controlled**. Anything canonical, and any
   evidence that must outlive the run directory, must live in a **git-tracked** path or it
   violates P9 (versioned knowledge) and P8 (provenance) the day the run directory is
   cleaned. This single fact constrains items 1–3 below more than any preference.

4. **Digest-binding is already the native idiom.** Every task has a provenance record
   (`provenance/<TASK_ID>.yaml`) with SHA-256 fingerprints of inputs and output (e.g. the
   report's digest `e894a84…` in `TASK-PRODUCE-0001.yaml`), and `tools/artifact_fingerprint/`
   exists. Binding a human approval to *exact bytes* requires no new machinery.

5. **Independent validation and the gate seam exist (O5).** The generation/validation split
   is proven (`TASK-PRODUCE-0001` vs `TASK-VALIDATE-0001`), and `tools/review_gate/` (C13,
   frozen) interprets verdicts with a review-pack extension seam that may only make the
   gate **stricter**. `GateResult.grants_approval` is structurally `False`.

6. **Authority model 0.1.0 binds only `approval → approval`.** In
   `tools/authority_rule/authority_model.py`, ownership and accountability hold **no**
   authorities at 0.1.0. Any reviewer/acceptance role binding this proposal enforces must
   therefore work at 0.1.0 and merely *get stronger* if Track B's 0.2.0 lands (coordination
   point, not a dependency).

Also on record: ECF's transformation vocabulary already exists
(`transformations/TRANSFORMATION_SPECIFICATION.md`, `knowledge/KNOWLEDGE_TRANSFORMATION_MODEL.md`
— transformations consume canonical artifacts, apply standards, produce canonical artifacts,
and are "not complete until the required reviews have been performed"), and the catalog
already lists WF-TRANSFORM-0001 as `planned` (`workflows/WORKFLOW_CATALOG.md`).

---

## Item 1 — The first canonicalization target

**Question.** Which artifact type does WF-TRANSFORM-0001 produce first, and where do
canonical artifacts live — consumer repo or Control-Plane outputs?

**Grounding in what WR-0001 would actually produce.** The real halted run's approved
recommendation is **`gather_additional_evidence`** (selected option OPT-0005; two open
blockers MISS-0001/MISS-0002 disclosed; no structural alternative selected). An approved
WR-0001 therefore canonicalizes a **disposition of an engineering question** — *"do not
commit to the subsystem boundary; close MISS-0001/MISS-0002 first"* — not an architecture
decision. That is still a genuine, consequential, challengeable engineering decision
(P5/P14: it has an accountable disposition and it is revisable by better evidence), and it
is exactly what the evidence supports. Anything grander would over-claim.

### 1a — Artifact type

| Option | What becomes canonical | Pros | Cons |
|---|---|---|---|
| **T1 — Canonical Engineering Decision Record (EDR)** *(recommended)* | A new, narrowly-specified artifact type: the human-ratified disposition of one engineering question, carrying the approved recommendation, the approval, and the evidence chain | Truthful for *any* recommendation outcome (including `gather_additional_evidence`); narrow contract ownable by ECF `artifacts/`; does not wait on O10's full model contract (per the kickoff ruling); ADR-compatible later | One new (small) artifact specification to write |
| **T2 — Consumer-repo ADR** | An ADR written into `context_switcher/decisions/` | Knowledge lands where it is used | **Over-claims for this run** — no structural decision was made, and MISS-0002 (*authoritative confirmation of the canonical subsystem model, ADR-0005*) is itself an open blocker, so an ADR would rest on unconfirmed foundations; consumer owns its ADR format; forces cross-repo write machinery into the Partial bar |
| **T3 — Promote the report in place** (flip `canonical: false → true`) | The run's own report file | Zero new artifacts | Mutates an immutable, provenance-tracked run output (violates the run-record discipline and P14's history preservation); lives in unversioned `runtime/` (finding 3); "canonical by flag-flip" is a hair away from the canonical-by-existence failure P3 forbids |

**Recommendation: T1.** Specify a **Canonical Engineering Decision Record** contract
(`artifacts/CANONICAL_DECISION_RECORD_CONTRACT.md`, or EDR for short): identity
(`EDR-<NNNN>`), the engineering question, the ratified disposition and its statement,
decisive forces/trade-offs/risks by ID, unresolved items carried forward, full provenance
(work request → run → approval), status vocabulary (`canonical | superseded | retired` —
corrigible per P14, never deleted), and the evidence/review/acceptance records of Item 3.
This is the "narrow canonical-artifact definition" the founder scoped: one type, one
contract, no dependency on O10's full model semantics.

### 1b — Where canonical artifacts live

| Option | Location | Pros | Cons |
|---|---|---|---|
| **L1 — Control-Plane canonical store** *(recommended)* | git-tracked `ecf/canonical/decisions/EDR-<NNNN>/` (new root; **not** under `runtime/`) | Versioned (P9) and durable — survives run-directory cleanup (finding 3); inside the repo the workflow machinery already governs; the O10 precedent is exactly this shape (*"internal pair first; cross-repo projection is the deepening target"* — ratified in PROGRAM_0.4) | Consumer-project knowledge temporarily lives in the Control Plane; needs a one-line placement rule so `canonical/` is never writable by a *running* workflow (see Appendix, prohibitions) |
| **L2 — Consumer repo now** | `context_switcher/decisions/` | Where the knowledge belongs long-term | Requires cross-repo authorization and commit-pin machinery in the very first slice; the run permission boundary ("no sibling-repo access") would need an exception; disproportionate to the Partial bar (P13) |
| **L3 — Control-Plane run outputs** | under `runtime/runs/<RUN_ID>/` | No new root | **Rejected outright**: `runtime/` is gitignored — a canonical artifact that is not version-controlled contradicts P9/P8 and finding 3 |

**Recommendation: L1, with L2 named as the deepening step** (a *projection* of the
canonical store into the consumer repo, following O10's model→projection discipline, once
cross-repo pin machinery exists). The `ecf/canonical/` root is written **only** by the
post-acceptance promotion step (see Item 3 and the Appendix) — never by a running
workflow — so the store cannot accumulate anything that lacks the P3 triple.

---

## Item 2 — The approval record

**Question.** Schema, where the human writes it, and how WF-TRANSFORM-0001 verifies it
against the halted run.

**Non-negotiable framing (P7).** The reasoning run records `approval_granted: false`
forever — that record is *never* mutated. The approval is a **new, human-authored
artifact** that *references* the halted run. WF-TRANSFORM-0001 **consumes and verifies**
it; nothing in the workflow can create, amend, or infer one. The absence of a "no" is
never a "yes".

### 2a — Where the human writes it

| Option | Location | Pros | Cons |
|---|---|---|---|
| **W1 — inside the halted run directory** | `runtime/runs/<RUN_ID>/approval/…` | Adjacent to what it approves | Writes into a completed run's tree (blurs the audit boundary even if additive); unversioned (finding 3); the run root is runtime-owned — a *human* artifact does not belong under a machine-owned root |
| **W2 — git-tracked approvals root** *(recommended)* | `ecf/approvals/APPROVAL-<NNNN>.yaml`, authored and **committed by the human** | Durable + versioned (P9); the git commit (author, timestamp, history) is the identity attestation for Partial — no signature machinery needed under Genesis; cleanly outside both the run tree and the canonical store | One new top-level directory; identity is only as strong as commit authorship (accepted for Genesis; noted as a deepening item) |
| **W3 — consumer repo** | `context_switcher/…` | Near the requester | Same cross-repo cost as L2, for no Partial benefit |

**Recommendation: W2.**

### 2b — Schema (proposed `APPROVAL_RECORD` 0.1.0, human-authored YAML)

```yaml
schema_version: "0.1.0"
approval_id: APPROVAL-0001
run_id: RUN-REASON-WR0001-V040-0002          # the halted run this approval answers
work_request_id: WR-0001
workflow_id: WF-REASON-0001                   # + workflow_version, for pin verification
decision: approved                            # approved | rejected | approved_with_constraints
constraints: []                               # required non-empty iff approved_with_constraints
approved_artifacts:                           # the human approves EXACT BYTES, not a path
  - path: reports/engineering-recommendation-report.md
    sha256: e894a84e6c631f7b7928b1ca582d8276d1e0914d8b128fa0b69631caadd1053f
  - path: reports/final-manifest.yaml
    sha256: <digest>
  - path: reports/completion.yaml
    sha256: <digest>
authority:                                    # must equal the run's recorded binding
  role: approval
  authority: approval
  model_version: "0.1.0"
approved_by: founder                          # holder identity; attested by git authorship
granted_at: "2026-07-16"
statement: >-
  Free-text human rationale — why this recommendation is approved.
```

A `rejected` record is equally first-class (P4/P5: a recorded disposition either way);
WF-TRANSFORM-0001 simply refuses to run on it.

### 2c — How WF-TRANSFORM-0001 verifies it (entry gate; deterministic; fail closed)

1. **Run integrity** — `run_id` resolves to a real run; `reports/completion.yaml` parses;
   `final_run_status: waiting_for_human_approval`; `approval_required: true`;
   `approval_granted: false`. (The source run never claims approval — P7 intact.)
2. **Identity chain** — `work_request_id`, `workflow_id`/version in the approval match the
   run's completion and final manifest.
3. **Authority binding (O6 reuse)** — the approval's `authority` tuple **equals** the run's
   recorded `approval_authority` binding, **and** `holds_authority(role, "approval",
   model_version)` is true against `tools/authority_rule/`. A role without approval
   authority, a wrong model version, or a mismatch with what the run declared → reject.
4. **Byte binding** — every `approved_artifacts.sha256` matches the current bytes on disk
   (via `artifact_fingerprint`). The human approved *exactly* what the run produced; any
   post-halt tamper or swap → reject.
5. **Decision** — `decision: approved` (or `approved_with_constraints`, whose constraints
   are carried forward as open findings visible at the acceptance gate); `rejected` or
   absent → the workflow does not start.
6. **Single effective use** — the canonical store's index records which `approval_id`
   produced which EDR; a second *accepted* canonicalization from the same approval is
   rejected (re-runs after a failed/blocked attempt are fine).

Any check failing → the run terminates `failed` with the reason recorded. There is no
degraded path.

---

## Item 3 — The evidence set for acceptance, and who reviews

**Question.** What evidence must exist for acceptance (P3: evidence, review, explicit
acceptance), and what are the reviewer role bindings?

### 3a — The evidence set

Finding 3 controls this: because `runtime/` is unversioned, *digest pointers alone will
dangle* once a run directory is cleaned. The canonical artifact must **carry** the
evidence it cites.

| Option | Evidence shape | Pros | Cons |
|---|---|---|---|
| E1 — pointers only | `run_id` + digests | Tiny | Dangles when the run dir is cleaned; the canonical artifact stops being auditable — fails P8 the moment evidence dies |
| E2 — copy all 18 outputs | full run snapshot | Complete | Bulk duplication of intermediate reasoning; P13 |
| **E3 — evidence bundle** *(recommended)* | The EDR ships as a directory: copies of the **load-bearing** artifacts + an `evidence-manifest.yaml` binding every copy to its origin by SHA-256 | Self-contained and durable (survives run cleanup); minimal (four small files); digests still tie the bundle back to the original run for as long as it exists | Copies must be digest-verified at assembly and at acceptance (the workflow does both) |

**Recommended bundle** — `ecf/canonical/decisions/EDR-0001/`:

```text
EDR-0001.md                    # the canonical decision record (Item 1)
evidence/
  engineering-recommendation-report.md   # what was approved (copy, digest-bound)
  recommendation-report-validation.yaml  # the independent verdict (O5, from the run)
  completion.yaml                        # the halt + authority binding (P7/O6)
  final-manifest.yaml                    # the immutable run snapshot (provenance chain)
  approval-record.yaml                   # copy of the human approval (Item 2)
  acceptance-record.yaml                 # the human acceptance (below)
evidence-manifest.yaml         # origin path + sha256 for every copy; run/workflow/task pins
```

Evidence, review, and acceptance are thereby **first-class run outputs** (the bundle is
assembled and validated *inside* the transformation run, then promoted), exactly as the
kickoff directed.

### 3b — Review and explicit acceptance (the P3 triple, and who does what)

The three legs are distinct and none substitutes for another:

- **Evidence** — the bundle above (machine-assembled, digest-verified, deterministic).
- **Review** — **independent validation separated from generation (O5/P6)**: the task that
  drafts the candidate EDR is never the task that validates it. The validator checks the
  candidate against its contract *and* against the evidence manifest (every claim in the
  EDR resolves to bundled evidence), and its verdict is interpreted through the frozen
  `review_gate` (C13) — which can only be made stricter, never weaker.
- **Explicit acceptance** — **a second human act.** This is the pivotal design point:

> **P7 applied twice.** If the automated transformation run could *end* with a canonical
> artifact, automation would be granting canonical status — the exact failure P3 exists
> to prevent, one boundary later than P7 usually bites. Therefore WF-TRANSFORM-0001's
> successful exit state is **`waiting_for_human_acceptance`**, structurally parallel to
> `waiting_for_human_approval`: the run produces a *candidate* EDR + evidence + review
> verdict, records `acceptance_granted: false` with an `acceptance_authority` binding in
> its completion contract (fail closed, mirroring `trace_completion.py`), and halts.
> Canonical status is conferred only by a **human-authored acceptance record**
> (schema mirrors the approval record: run_id of the *transformation* run, digest of the
> candidate EDR and evidence manifest, authority tuple, statement), after which a
> **deterministic promotion step, invoked by a human**, copies the bundle into
> `ecf/canonical/` and updates the store index. The workflow never writes `canonical/`.

**Reviewer role bindings (coordination with Track B — designed to degrade).** All review
and acceptance records carry O6-style tuples `{role, authority, model_version}`:

- **At authority model 0.1.0 (today, no Track B dependency):** only `approval → approval`
  is bound, so the *enforceable* binding for acceptance is the `approval` role — under
  Genesis the same institutional authority (Founder) that approved the recommendation
  accepts the canonical artifact, and the independent-review leg is satisfied structurally
  (separate validator task + gate), with the reviewer identity recorded **descriptively**.
- **If Track B lands 0.2.0** (`ownership` → stewardship transfer, `accountability` →
  challenge disposition, per the kickoff ruling): the acceptance record's `model_version`
  bumps and reviewer/steward bindings become machine-checkable with **no schema change** —
  the tuples are already there. Enforcement always fails closed against whichever model
  version the record cites (unknown version ⇒ reject), so nothing here waits on 0.2.0 and
  nothing breaks when it arrives.

---

## Item 4 — The O3 Partial bar

**Proposed at kickoff:** *"specification released + one real approved recommendation
transformed into a canonical artifact with evidence/review/acceptance recorded."*

**Recommendation: CONFIRM, with three tightenings** (all evidence-shaped, none scope-creep):

1. **"Specification released"** means WF-TRANSFORM-0001 reaches `released` in
   `WORKFLOW_CATALOG.md` under the frozen workflow-execution discipline — pinned task
   versions, unique output bindings, explicit DAG, acceptance-test file — plus the two new
   small contracts it rests on (`APPROVAL_RECORD`, `CANONICAL_DECISION_RECORD`).
2. **"One real approved recommendation transformed"** means end-to-end on real artifacts:
   the founder authors a real approval record for `RUN-REASON-WR0001-V040-0002`'s report,
   the workflow runs to `waiting_for_human_acceptance`, the founder authors a real
   acceptance record, and `EDR-0001` lands in the canonical store with the full bundle.
   (Note honestly: for WR-0001 that canonicalizes a `gather_additional_evidence`
   disposition — see Item 1 grounding — which is a legitimate first canonical artifact.)
3. **Add the negative test** (the 0.4 B3 precedent — P4, evidence over opinion): a
   demonstrated fail-closed rejection of at least (a) a missing/absent approval record,
   and (b) a digest-mismatched (tampered) or authority-mismatched approval. Canonicalization
   that cannot be shown to *refuse* is not P3's gate.

The bar deliberately does **not** require: consumer-repo projection (deepening, Item 1b),
supersession mechanics beyond the status vocabulary (0.6 O7 owns safe supersession),
signature-grade identity (Genesis: git authorship), or authority model 0.2.0 (Track B,
degradation designed in).

---

## Appendix — Spec-level skeleton of WF-TRANSFORM-0001 *(SPEC-LEVEL ONLY — nothing here is built)*

| Field | Value |
|---|---|
| Workflow ID | WF-TRANSFORM-0001 |
| Name | Approved Recommendation to Canonical Artifact |
| Category | transformation |
| Entry state | `approval_recorded` — a verified human approval record exists referencing a run halted at `waiting_for_human_approval` |
| Successful exit state | **`waiting_for_human_acceptance`** — never `canonical`; canonical status is a post-run human act (P3/P7) |
| Run ID | `RUN-TRANSFORM-<YYYYMMDD>-<SEQUENCE>` under `runtime/runs/<RUN_ID>/` |
| Task count | **8** |

### Sketched task list (one-line purposes)

| # | Task (new) | Purpose | Nature |
|---|---|---|---|
| 1 | TASK-VERIFY-0001 — verify-approval-binding | Item 2c checks 1–6: approval record vs halted run (identity, authority via `tools/authority_rule/`, digests, decision, single-use) | deterministic |
| 2 | TASK-VERIFY-0002 — verify-source-run-integrity | Re-verify the source run's provenance chain (per-task SHA-256, pins) so canonicalization never builds on a corrupted run | deterministic |
| 3 | TASK-ASSEMBLE-0001 — assemble-evidence-bundle | Copy the load-bearing artifacts (Item 3a) into the run and emit `evidence-manifest.yaml` binding every copy to its origin digest | deterministic |
| 4 | TASK-CANON-0001 — draft-canonical-decision-record | Render the candidate EDR from the approved report + approval record; **no new engineering reasoning** — the judgment already exists upstream (P1); every claim must cite bundled evidence | rendering under contract |
| 5 | TASK-VALIDATE-0002 — validate-canonical-candidate | Independent validation of the candidate against the EDR contract and the evidence manifest (O5/P6 — never the drafting actor); verdict interpreted via frozen `review_gate` (C13) | independent validator |
| 6 | TASK-TRACE-0004 — generate-transformation-trace | Auditable trace of the transformation run (`reports/trace.md`), per the execution-trace contract | deterministic |
| 7 | TASK-TRACE-0005 — generate-transformation-manifest | Immutable snapshot `reports/final-manifest.yaml` (mirrors TASK-TRACE-0002 discipline; WF021 applies) | deterministic |
| 8 | TASK-TRACE-0006 — finalize-transformation-run | Completion contract mirroring `trace_completion.py`: exactly one final status; `acceptance_required: true`, `acceptance_granted: false`, `acceptance_authority: {role, authority, model_version}` fail-closed; `canonical_store_written: false` enforced | deterministic, fail closed |

### Output bindings sketch

```text
task_outputs/approval-verification.yaml       (1)
task_outputs/source-run-integrity.yaml        (2)
task_outputs/evidence-manifest.yaml           (3)   + evidence copies under task_outputs/evidence/
reports/candidate-canonical-artifact.md       (4)   ← the candidate EDR (still non-canonical)
task_outputs/canonical-candidate-validation.yaml (5)
reports/trace.md                              (6)
reports/final-manifest.yaml                   (7)
reports/completion.yaml                       (8)
```

All bindings under `task_outputs/` or `reports/` only — the existing runner write
boundary is unchanged and **not** widened.

### States

```text
approval_recorded → verifying_approval → verifying_source → assembling_evidence
  → drafting_candidate → validating_candidate → finalizing_trace
  → waiting_for_human_acceptance
any active state → blocked | failed | cancelled | superseded
```

### Failure / halt semantics

- **Verification failure (tasks 1–2) → `failed`, not resumable-in-run.** An invalid
  approval cannot be repaired by resuming; a *new* human approval means a *new* run.
- **Candidate validation failure (task 5) → `blocked`** — the candidate may be
  regenerated (mirrors the Step-15 `blocked`-for-regeneration semantics of WF-REASON-0001).
- **Fail closed everywhere**: missing output, digest mismatch, unknown authority-model
  version, or a completion that claims acceptance → the run never reaches the exit state.
- **Independent validation (O5)** sits at task 5 + the C13 gate; review-pack hooks may
  only tighten it.

### Prohibitions (P7, restated for the transformation family)

The workflow must never: **write to `canonical/`** (promotion is a post-acceptance human
step), **grant or imply acceptance**, mutate the source reasoning run or the approval
record, create consumer-repo artifacts, or start a further downstream transformation.
The recommend/approve boundary moved for no one; this workflow adds a
**produce-candidate/accept** boundary with the same discipline.

---

## Risks and coordination points found while grounding this proposal

1. **The first canonical artifact will be a disposition, not a structural decision.**
   WR-0001's real recommendation is `gather_additional_evidence`. Approving it is
   honest and exercises the full P3 triple — but if the founder wants the *first* EDR to
   record a structural decision, the two blockers (MISS-0001/MISS-0002) must be closed and
   a fresh reasoning run driven first (schedule risk to 0.5).
2. **Evidence permanence gap (platform-level).** `runtime/` being unversioned means *all*
   run evidence is currently mortal. The bundle design (Item 3a) protects canonical
   artifacts; the general gap is worth recording under Clarification A honesty
   (candidate background/0.6 item, not Track A scope).
3. **Identity attestation is git authorship only** for approval/acceptance records —
   adequate under Genesis (single founder), flagged as a deepening item for
   post-Genesis governance.
4. **Track B coordination is one-way by design**: O6-style `{role, authority,
   model_version}` tuples appear in approval and acceptance records now, enforce against
   0.1.0 today, and become richer if/when 0.2.0 lands. No Track A deliverable waits on
   Track B.
5. **Worktree hygiene note**: `ecf-wt-o3` currently shows unrelated modified files under
   `research/` (parallel-session shared-state artifact). Track A work must stage explicit
   paths only; those files were left untouched by this workshop.

## Exact founder rulings needed before build

1. **(Item 1)** Adopt **T1** (Canonical Engineering Decision Record) + **L1**
   (`ecf/canonical/decisions/`, workflow-unwritable), with the consumer-repo projection
   named as the deepening step.
2. **(Item 2)** Adopt **W2** (`ecf/approvals/`, human-committed) and the
   `APPROVAL_RECORD` 0.1.0 shape, including digest-binding and the O6 authority-tuple
   equality check.
3. **(Item 3)** Adopt **E3** (evidence bundle) and the **two-human-acts** construction —
   exit state `waiting_for_human_acceptance`, acceptance as a new human-authored record,
   deterministic human-invoked promotion; reviewer bindings recorded as versioned tuples
   degrading cleanly to model 0.1.0.
4. **(Item 4)** Ratify the Partial bar as confirmed **with the negative-test addition**.
5. **(Appendix)** Confirm the 8-task skeleton (entry `approval_recorded`, exit
   `waiting_for_human_acceptance`) as the build target, and the new task-family names
   (`TASK-VERIFY-*`, `TASK-CANON-*`, `TASK-TRACE-0004..6`).

---

## Metadata

| Field | Value |
|---|---|
| Owner (proposing) | Track A owner (O3) |
| Status | **RATIFIED (Founder, 2026-07-16)** — Track A authorized to build |
| Change class | T1 working proposal (K5: organizes the ratified 0.5.0 milestone) |
| Derives from | [PROGRAM_0.5](PROGRAM_0.5.md) Track A · [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md) 0.5.0 |
| Serves | O3 / P3 (nothing canonical by existence) · P4 (evidence over opinion) |
| Evidence base | `ecf-wt-o3` @ develop 9a96563 (branch `feature/0.5-o3-transform`) · run `RUN-REASON-WR0001-V040-0002` (read-only) |
| Cross references | [PROPOSAL_O6_SCOPE](PROPOSAL_O6_SCOPE.md) · [PROPOSAL_O10_SCOPE](PROPOSAL_O10_SCOPE.md) · [AMENDMENT_O6_RESPONSIBILITY_AUTHORITY](AMENDMENT_O6_RESPONSIBILITY_AUTHORITY.md) · [PLATFORM_PRINCIPLES](PLATFORM_PRINCIPLES.md) |
