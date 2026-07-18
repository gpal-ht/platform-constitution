# PROPOSAL_O6_B2_RULE — One executable authority rule (design + prototype evidence)

> **Status: PROPOSED (draft for founder ratification).** This is the **executable rule**
> half of the ratified O6 "Partial" bar. It couples the descriptive model
> ([PROPOSAL_O6_B1_MODEL](PROPOSAL_O6_B1_MODEL.md)) to the 0.3 runtime by making **one** thing
> machine-checkable and **fail-closed**. Scope choices below assume the SCOPE recommendations
> (A2 · B-i · c-1); if the founder rules differently, this design adjusts.
>
> Obligation: **O6 / P7**. Serves: the "indestructible responsibility" boundary the 0.3
> engine already halts at.

---

## 1. The rule, in one sentence

> **A reasoning run may rest at `waiting_for_human_approval` only if it records a role that
> holds *approval authority* in the referenced authority-model version; a run that records a
> role without approval authority (or records no binding) is rejected, failing closed.**

This is the smallest coupling that satisfies P7 at runtime: it makes an approval **attributable
to a role that is not entitled to approve** impossible to commit — the exact "orphaned /
mis-attributed responsibility" failure P7 exists to prevent.

---

## 2. Where it attaches (the existing seam)

The 0.3 runtime already stops at the P7 boundary and already carries a dedicated record:

- Engine: `ecf/tools/orchestration/engine.py` drives to exactly one success state,
  `waiting_for_human_approval`, and refuses any completion that *grants* approval.
- Record: `reports/completion.yaml` (task `TASK-TRACE-0003`) already has a **`human_authority`**
  block.
- Enforcement: `ecf/tools/task_runner/output_contracts/trace_completion.py`
  (`_check_approval_boundary`) already validates, executor-independently and **before commit**,
  that `approval_required: true` and `approval_granted: false`, **failing closed**.

B2 adds **one field** to `human_authority` and **one check** to that function. It introduces no
new artifact, no new tool, and no new gate (SCOPE option B-i).

---

## 3. What the run records (SCOPE option A2)

Extend the `human_authority` block of `completion.yaml` with a role→authority binding:

```yaml
human_authority:
  approval_required: true          # unchanged (frozen P7 invariant)
  approval_granted: false          # unchanged (frozen P7 invariant)
  approval_authority:              # NEW (B2)
    role: approval                 # one of the five ratified roles (P5)
    authority: approval            # the authority being claimed at this boundary
    model_version: 0.1.0           # the authority-model version this run conforms to
```

- `role` — which of the five ratified roles holds approval authority for this run.
- `authority` — the authority claimed at this boundary (`approval`).
- `model_version` — ties the individual binding back to the **institutional** authority behind
  it (B1 §6) and makes the check version-aware (P9). Recording bare identity (SCOPE option A1)
  is rejected because the contract could not then tell whether the role is entitled to approve.

This is additive to the completion contract's **closed** top-level field set (the new key is
*inside* the already-allowed `human_authority` map, so the closed-set check is unaffected).

---

## 4. What the contract checks (fail closed)

Added to `_check_approval_boundary` (or its B2 successor). Pseudocode mirrors the prototype:

```
binding = human_authority.approval_authority
reject if binding missing/not-an-object            # fail closed
reject if role not in the five ratified roles
reject if model_version != the model version the contract implements   # fail closed
reject if authority != "approval"
reject if NOT model.holds_authority(role, "approval", model_version)   # THE RULE
```

Every branch **fails closed**: absent, unknown, wrong-version, or mismatched authority never
commits. This matches the idiom the frozen contract already uses (an absent or unrecognized
verdict is `unknown`, which never continues the run).

**Model source.** The contract needs the model's role→authority table. For Partial it is a
**small, versioned, in-repo table** (the projection of B1 §5–6), pinned by `model_version`.
This keeps B2 self-contained and avoids a cross-repo read for the exit bar; a later milestone
(O4, 0.5) may relocate the table to a canonical governance projection.

---

## 5. Prototype evidence (deliverable B3)

A **standalone, non-frozen** prototype lives in the isolated worktree
`C:\Dev\ecf-wt-o6` (branch `feature/0.4-o6-authority`, **not merged to develop**). It does not
modify any frozen 0.3 contract; it demonstrates the added field + check end to end.

| File | Role |
|---|---|
| `tools/authority_rule/authority_model.py` | the model (role→authority table, `MODEL_VERSION`, `holds_authority`), + a `role_is_active` forward seam (unused for Partial) |
| `tools/authority_rule/check_authority.py` | the one executable rule (`check_approval_authority`), fail-closed |
| `tools/authority_rule/tests/test_authority_rule.py` | evidence: conformant-pass + mismatch-reject + fail-closed edges |

**Result (observed):**

```
PASS test_conformant_run_passes            # approval bound to `approval` role -> passes
PASS test_mismatch_authority_is_rejected   # approval bound to `authorship` -> rejected, fail closed
PASS test_missing_binding_fails_closed
PASS test_unknown_model_version_fails_closed
PASS test_unknown_role_fails_closed
PASS test_granted_approval_still_rejected  # frozen P7 invariant preserved
6/6 passed
```

The two required B3 scenarios — **conformant run passes**, **mismatched-authority run is
rejected** — both hold, plus three fail-closed edges and preservation of the existing P7
invariant.

---

## 6. Path to land it in the real contract (post-ratification, not done here)

1. Bump `TASK-TRACE-0003` and `trace_completion.py` `task_version` (a deliberate contract
   change — the frozen 0.3 surface is versioned, not immutable).
2. Add the in-repo versioned role→authority table (projection of B1 §5–6).
3. Add the `approval_authority` binding to the task's output example + `ALLOWED` shape, and the
   check to `_check_approval_boundary`.
4. Update the WS-E completion fixtures to carry a conformant binding; add a mismatch fixture as
   a negative acceptance test (mirrors the prototype tests).
5. Because the check runs in the runner *before commit*, executor-independently, a
   mismatched-authority run **cannot be committed** — the same guarantee the prototype shows.

This is a **T-band contract change** (touches the P7 authority boundary → independent review
applies); it is *proposed* here, not performed.

---

## 7. Why this passes the Governance Admission Test (P13)

Removing this rule would let a run record an approval attributable to a role with **no**
approval authority and still commit — a measurable loss of traceability and answerability
(P5/P7). The rule therefore *earns* its existence: it strengthens the *scope & authority* and
*authorized disposition* stages of the Root Governance Primitive at the one boundary where the
platform hands off from reasoning to human decision. It adds one field and one fail-closed
check — proportional to consequence.

---

## 8. Founder rulings this deliverable depends on
1. Adopt **A2** field shape (§3) — else the check in §4 changes.
2. Adopt **B-i** home + accept the `TASK-TRACE-0003` `task_version` bump (§6).
3. Confirm the model table lives **in-repo, versioned** for Partial (§4), relocation deferred to
   O4/0.5.
4. Confirm B2 lands as a **T-band contract change with independent review** (§6), not editorial.

---

## Metadata
| Field | Value |
|---|---|
| Status | **PROPOSED** — executable rule for O6 Partial; prototype green |
| Owner (proposing) | Track B owner (O6) |
| Prototype | `C:\Dev\ecf-wt-o6` · branch `feature/0.4-o6-authority` (not merged) |
| Serves | O6 / P7; couples B1 model to the 0.3 `waiting_for_human_approval` boundary |
| Cross references | [PROPOSAL_O6_SCOPE](PROPOSAL_O6_SCOPE.md) · [PROPOSAL_O6_B1_MODEL](PROPOSAL_O6_B1_MODEL.md) · `ecf/tools/task_runner/output_contracts/trace_completion.py` · `ecf/tools/orchestration/engine.py` |
