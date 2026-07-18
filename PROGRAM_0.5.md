# PROGRAM 0.5 — Canonicalization & Stewardship

> **Milestone working plan.** Non-constitutional (T1). Derives entirely from the ratified
> [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md) 0.5.0 milestone — it **organizes** delivery of that
> milestone; it does not redefine it (K5). Every deliverable traces to a constitutional
> obligation (P13: no obligation, no item).

| Field | Value |
|---|---|
| Milestone | **0.5.0 — Canonicalization & Stewardship** |
| Obligations | **O3** (P3 nothing-canonical-by-existence · P4 evidence over opinion) · **O4** (P5 answerability · Clarification B challenge routing · Clarification C institutional continuity) |
| Roadmap exit | O3 and O4 each reach **Partial** |
| Structure | **Two parallel tracks** + a background lane (carryover; does **not** gate the exit) |
| Baseline | ECF **v0.4.0** released (formal 18/18 halt proven; O6 authority model 0.1.0 live at the completion boundary; O10 drift release gate) |
| Status | **EXIT SEQUENCE COMPLETE — 2026-07-16.** Both tracks built, merged, reconciled (1021 tests green). All ratified bar clauses discharged, including the real acts: WF-TRANSFORM-0001 `released`; **APPROVAL-0001** (Founder) → authoritative transformation run `RUN-TRANSFORM-20260716-0002` halted at `waiting_for_human_acceptance` → **ACCEPTANCE-0001** (Founder) → **EDR-0001 promoted to the canonical store**; real challenge **CHG-20260716-0001** routed live to the accountability office and **disposed (rejected) with evidence**. Two T4 landings en route (C5 env-scope; C3 declared human-boundary exits). Carryovers H1–H3 landed. Remaining: release ceremony (version bump, notes, tag) on founder call. |

---

## Founder decisions (2026-07-16 kickoff)

1. **O3 vehicle → `WF-TRANSFORM-0001`** (*Approved Recommendation → Canonical Artifact*): build
   the post-approval canonicalization workflow that begins exactly where the proven
   `waiting_for_human_approval` halt ends. The "canonical artifact" definition is scoped
   **narrowly** for 0.5 — it does **not** wait on O10's full model contract.
2. **O4 → minimal authority-model bump to 0.2.0.** Bind the stewardship-relevant authorities
   (direction: `ownership` → stewardship transfer; `accountability` → challenge disposition)
   with an **explicit version bump + compatibility note**. The version-evolution discipline
   doubles as the **first exercise of O10's compatibility semantics**.
3. **Two tracks + background lane** — Track A = O3, Track B = O4; mirrors the 0.4 structure.
4. **Background lane carries all three 0.4 carryovers** (below). Background work never gates
   the O3/O4 exit.

### Scope ratifications (2026-07-16, post scope-workshop — "ratify all with T4 ruling")

Proposal docs: [PROPOSAL_O3_TRANSFORM_SCOPE](PROPOSAL_O3_TRANSFORM_SCOPE.md) ·
[PROPOSAL_O4_STEWARDSHIP_SCOPE](PROPOSAL_O4_STEWARDSHIP_SCOPE.md) ·
[PROPOSAL_05_PARTIAL_BARS](PROPOSAL_05_PARTIAL_BARS.md) — all **RATIFIED (Founder)**.

**Track A — O3 (ratified as recommended):**
- First canonicalization target: the narrow **Canonical Engineering Decision Record (EDR)** in a
  git-tracked Control-Plane store (`ecf/canonical/decisions/`); consumer-repo projection is the
  deepening step (O10 internal-first precedent). `runtime/` stays unversioned; canonical
  artifacts never live there.
- Approval record: human-authored `ecf/approvals/APPROVAL-<NNNN>.yaml` binding `run_id` + SHA-256
  of the approved bytes + the O6 `{role, authority, model_version}` tuple; six fail-closed entry
  checks; the halted run's `approval_granted: false` is never mutated.
- Evidence bundle as first-class run outputs; authority bindings enforce against model 0.1.0
  today and strengthen under 0.2.0 — **no dependency on Track B**.
- **P7 applied twice:** exit is `waiting_for_human_acceptance`; a second human act + a
  human-invoked deterministic promotion step writes the canonical store — the workflow never does.
- Known caveat (accepted): WR-0001's live recommendation is `gather_additional_evidence`, so the
  first real EDR canonicalizes a disposition record unless MISS-0001/0002 close and a fresh
  reasoning run is driven.

**Track B — O4 (ratified as recommended; governance RULED T4):**
- **Governance classification RULED: T4 mechanism change** under the ratified authority model's
  own change process — not a constitutional amendment. (The T5 reading was presented at full
  strength and declined; Doctrine E.4/E.7 pre-authorized O4's runtime operationalization, and the
  0.4 override's rationale is spent.) The 0.2.0 bump is unblocked.
- Authority model **0.2.0**: `ownership → {stewardship_transfer}`, `accountability →
  {challenge_disposition}`; additive minor bump; strict single-version pinning; lockstep landing
  with `TASK-TRACE-0003` 0.4.0 → 0.5.0 + workflow bump; historical 0.1.0 runs stand.
- Challenge/disposition schemas as proposed (`effective_recipient` never empty; disposition
  requires non-empty evidence; one disposition ever — reconsideration is a new challenge).
- Runtime: `_ROLE_STATE` becomes a fold over append-only recorded acts; gap-leaving transfers
  invalid *and unrecorded*; silent vacancy fails closed, disclosed escalation passes visibly
  degraded. Spike (23/23; full regression 898/0 in-worktree) is the starting point.

**Exit bars (ratified):** the 6+6 clauses of PROPOSAL_05_PARTIAL_BARS are the 0.5 exit criteria,
including the negative tests (rejected tampered/mis-attributed approvals; vacancy must *change
contract behavior*), the "real, not fixture" requirements, and "ratified means live at the
boundary."

---

## Track A — O3: evidence-based canonicalization (`WF-TRANSFORM-0001`)

**Obligation.** P3: knowledge becomes canonical only through **evidence, review, and explicit
acceptance** — never by existence, accumulation, or repetition. P4: challenges settle by evidence.

**In scope (direction set at kickoff):**
- Specify `WF-TRANSFORM-0001` under the frozen workflow-execution discipline: entry state is a
  **recorded human approval** of an Engineering Recommendation (the reasoning workflow's halt is
  upstream and unchanged — P7 preserved: the reasoning run never approves; TRANSFORM **consumes**
  an approval a human authored).
- A **narrow canonical-artifact definition** for the first target (scope-workshop item), with
  evidence, review, and explicit acceptance recorded as first-class run outputs.
- Independent validation separated from generation (O5 discipline carries over).
- Provenance end-to-end, as in `WF-REASON-0001`.

**Design-open (scope workshop before build):**
- The **first canonicalization target** (which artifact type; where canonical artifacts live —
  consumer repo vs Control-Plane outputs).
- The **approval record**: schema, where the human writes it, and how TRANSFORM verifies it
  against the halted run (binding to `run_id` + the O6 `approval_authority` role).
- The **evidence set** required for acceptance, and who reviews (role bindings — coordinate
  with Track B).
- The **O3 Partial bar** (proposed, to be ratified at the workshop): specification released
  **+ one real approved recommendation transformed** into a canonical artifact with
  evidence/review/acceptance recorded.

## Track B — O4: durable stewardship & challenge routing

**Obligation.** P5: every consequential decision has a durable accountable authority, an
escalation path, and a recorded disposition. Clarification B: a challenge must **reach** an
accountable recipient and **receive a recorded disposition**. Clarification C: the authority is
an **office, never vacant by construction** — vacancy falls back to the institution's standing
authority (Founder under Genesis).

**In scope (direction set at kickoff):**
- **Authority model 0.2.0**: bind stewardship-relevant authorities to `ownership` /
  `accountability`; explicit `MODEL_VERSION` bump with a compatibility note (first exercise of
  O10 compatibility semantics). Existing 0.1.0 bindings unchanged (`approval` → approval).
- **Runtime role-state seam made real** (0.4's declared handoff: vacancy / transfer /
  escalation were descriptive-only for O6 Partial — "O4's runtime job at 0.5"). Start from the
  unmerged `ecf-wt-o6` prototype (6/6 tests).
- **Challenge routing**: a challenge artifact reaches the accountable office and receives a
  recorded disposition; vacancy routes to the institutional fallback, never to nowhere.

**Design-open (scope workshop before build):**
- The **challenge artifact** (schema, where it lives, how it binds to the decision it challenges).
- The **disposition record** (schema; disposition by evidence per P4).
- **Governance classification of the model bump**: O6 was handled as a constitutional amendment
  because it touched P7. Does binding *new* authorities re-touch P7 (constitutional), or is it
  a T-band mechanism change under the already-ratified model's change process? **Founder ruling
  required before the bump lands.**
- The **O4 Partial bar** (proposed, to be ratified at the workshop): model 0.2.0 ratified
  **+ vacancy fallback enforced at runtime + one challenge routed to a recorded disposition**.

## Background lane (carryover — never gates the exit)

| Item | Traces to | Note |
|---|---|---|
| **H1 — O10 full-model-contract slice** | O10 | Version/compatibility/migration semantics; feeds Track B's 0.2.0 bump discipline. |
| **H2 — Resume-cascade env scoping** | O8/DX | Per-task environment fingerprints so an executor fix doesn't cascade a full DAG re-run. |
| **H3 — EKB decision-guide authoring** | O9/O3 | Begin authoring the 7 unauthored architecture guides (ECF now refuses to offer them — EKB-RD-0001); grows retrieval coverage. |

---

## Constitutional edges this program must respect

- **P7 is not re-opened by Track A.** `WF-REASON-0001` still halts at
  `waiting_for_human_approval`; `WF-TRANSFORM-0001` runs **only** on a recorded human approval.
  The recommend/approve boundary moves for no one.
- **P3's explicit-acceptance gate is the point of Track A** — a transformation without recorded
  evidence, review, and acceptance is exactly the "canonical by existence" failure mode.
- **Anti-Capture / asymmetric burden** applies to any Track B change ruled constitutional.

## Immediate next step

A **scope workshop per track** (the design-open items above) before any build — mirroring 0.4.
Track B's workshop must open with the governance-classification ruling.
