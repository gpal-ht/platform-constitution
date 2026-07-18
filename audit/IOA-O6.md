# IOA-O6 — Independent Obligation Assessment

| Field | Value |
|---|---|
| **obligation_id** | O6 — Indestructible responsibility |
| **principle** | P7 (Responsibility is indestructible); Root pillar CHALLENGEABLE; via Clarification C + Doctrine E |
| **assessor** | Independent auditor (0.9 Constitutional Readiness audit). Attestation: assessor did **not** build O6 — the mechanism was authored under PROGRAM_0.4 (Track B owner) and extended under O4 (0.5); the assessor read the primary artifacts and re-derived every finding. |
| **roadmap baseline** | Partial (0.4) |
| **maturity_verdict** | **Partial** (strong on the approval-boundary surface; vacancy/escalation reality-gated) |
| **determination** | ≥ Partial: **YES** · Strong-blocker: **NO** |

## clause_under_test (quoted)

> **P7 — Responsibility is indestructible.** "Ultimate responsibility for consequential
> engineering decisions must rest with a recognized accountable authority capable of accepting
> responsibility and responding to challenge. This principle constrains *governance*, not the
> identity or nature of the decider. It protects against orphaned responsibility, as P6 protects
> against self-ratification."

Amendment AMENDMENT_O6 operationalizes P7 via **Clarification C** ("a seat may be empty, but the
responsibility behind it cannot be") and **Doctrine E.7**, whose 0.4 "Partial" line makes exactly
one provision executable: "the completion contract **rejects, failing closed, any run whose
recorded approval role does not hold approval authority in that model** — preserving the existing
P7 invariant (`approval_required: true` / `approval_granted: false`)."

The test: is P7 **enforced at runtime**, or merely descriptive?

## Evidence

### E1 — The engine never grants approval (artifact + real demonstration + checker)
- **Artifact:** `C:\Dev\ecf\tools\orchestration\engine.py` and `.\gates.py`.
  - `engine.py::_terminal` (lines 386–391): if `gates.grants_approval(completion)` is true, the
    completion result "purports to grant human approval" and is **refused** — routed to `_fail`,
    not to a successful exit. The only successful exit is a `HUMAN_BOUNDARY` halt; the module has
    no transition to `approved` and no code path to the Production Engine (module docstring,
    lines 25–29; verified by reading the whole file — no such path exists).
  - `gates.py::grants_approval` (lines 224–236): fails true on `final_run_status ∈ {approved,
    approve, granted}` or any truthy `approved`/`approval_granted`/`human_approval` key.
- **Demonstration (real):** `RUN-REASON-20260717-0003` (WR-0004 → EDR-0003) and
  `RUN-REASON-20260718-0001` — both real runs — halted at `run_status: waiting_for_human_approval`
  in `state.yaml`, with `completion.yaml` recording `final_run_status: waiting_for_human_approval`,
  `human_authority.approval_granted: false`, `production_engine_invoked: false`,
  `validation.approval_not_granted: true`.
- **Verified by:** assessor read `runtime/runs/RUN-REASON-20260717-0003/{state.yaml,reports/completion.yaml}`
  and the 0718 run directly, and re-derived the refusal logic from engine.py/gates.py source.

### E2 — The authority tuple is executably enforced in the FROZEN completion contract (O6/E.7 landed)
- **Artifact:** `C:\Dev\ecf\tools\task_runner\output_contracts\trace_completion.py`
  (`_check_approval_boundary` + `_check_approval_authority_binding`, lines 190–277) and the
  ratified table `C:\Dev\ecf\tools\authority_rule\authority_model.py`
  (`holds_authority`, `_AUTHORITY_BINDINGS`, `MODEL_VERSION = "0.3.0"`).
  - The rule (line 227): `holds_authority(role, "approval", model_version)` — "an approval
    attributed to a role without approval authority [is] impossible to commit." Only `approval`
    holds `approval`; `authorship`/`ownership`/`accountability`/`responsibility_acceptance` do not.
  - Fail-closed on: missing binding, role ∉ five ratified roles, `model_version != 0.3.0`,
    `authority != "approval"`, and mis-attributed role.
  - **This is the downstream T4 landing the amendment §6 authorized — it has been performed.** It
    is additive to the frozen P7 invariant (`approval_granted` must be `false`), which is unchanged.
- **Demonstration (real):** `RUN-REASON-20260717-0003/reports/completion.yaml` carries a conformant
  `human_authority.approval_authority: {role: approval, authority: approval, model_version: "0.3.0"}`.
  The human decision records `approvals/APPROVAL-0002.yaml` and `APPROVAL-0003.yaml` carry the same
  authority tuple `{role: approval, authority: approval, model_version: "0.3.0"}`, are byte-bound
  (SHA-256) to the exact approved artifacts, authored **separately** in the human-only `approvals/`
  directory ("written and committed by a human only. No workflow, task, executor, or tool writes
  this directory — ever (P7)", `approvals/README.md`).
- **Verified by:** assessor read both APPROVAL records + the run completion; ran the frozen
  contract's negative suite — `test_o6_role_without_approval_authority_rejected_fail_closed`,
  missing-binding, wrong-version, unknown-role, `authority-must-be-approval`,
  `a_run_may_never_grant_approval` — **16 passed** (`pytest tools/task_runner/tests/test_trace_contracts.py -k "o6 or o4 or approval or grant"`).

### E3 — Vacancy / escalation wired to the runtime boundary (advanced past 0.4-descriptive), but reality-gated
- **Artifact:** `C:\Dev\ecf\tools\authority_rule\role_state.py` (append-only recorded-acts fold:
  `record_transfer` E.2 no-gap, `record_vacancy` E.3 recorded-never-silent, `resolve()`
  Clarification C "never to nowhere" → `founder_genesis`), consulted at the boundary via
  `check_stewardship.py::check_approval_boundary_state` and `trace_completion.py::_check_role_state`
  (lines 233–259). `review_obligations.py` routes review obligations through the same seam.
- **Status now vs. the 0.4 baseline:** at 0.4 these were **descriptive-only**; at 0.5 (O4) they are
  **executable and consulted at the runtime approval boundary** — an undisclosed vacancy fails
  closed; a disclosed vacancy passes *visibly degraded* to the institutional fallback; a spurious
  escalation on an active office is rejected (P2).
- **Demonstration:** tests/fixtures only — `test_stewardship.py` + `test_authority_rule.py`
  **34 passed**; contract-level O4 negatives (`test_o4_negative_undisclosed_vacancy_fails_closed`,
  disclosed-escalation-passes, target-must-be-fallback, spurious-escalation-rejected, malformed-store)
  green within the 16 above. The recorded-acts store `tools/authority_rule/role_acts.yaml` is
  **empty (`acts: []`) — the Genesis initial condition**; no real vacancy/transfer event has ever
  occurred.
- **Verified by:** assessor read role_state.py, check_stewardship.py, role_acts.yaml, and ran the
  tests.

## open_items

1. **Vacancy/escalation never exercised on a real triggering event.** The machinery is wired
   end-to-end into the runtime boundary and fixture-proven, but `role_acts.yaml` is empty (Genesis
   condition); no genuine vacancy/transfer has fired.
   - **classification: named_gap_toward_strong** — reality-gated; the machinery is proven end-to-end
     (boundary consults `resolve()`; disclosed-vacancy passes degraded, undisclosed fails closed),
     only the triggering reality is absent (§5 reality-gated rule).
2. **Succession (Doctrine E.5, ordered next-holder rule) not yet executable.** Transfer (E.2) and
   vacancy (E.3) are executable; the ordered succession rule remains descriptive.
   - **classification: named_gap_toward_strong** — purely additive within the ratified architecture;
     no frozen-contract or architecture break required.
3. **Recorded-acts storage-format ratification deferred.** `role_state.py` marks the minimal JSON
   store as an explicit 0.5 deepening target (format not yet ratified).
   - **classification: named_gap_toward_strong** — additive refinement.
4. **Approval identity attestation is "git commit authorship" (Genesis convention), not a
   cryptographic identity binding.** Disclosed honestly in APPROVAL records and `approvals/README.md`;
   End-of-Genesis re-points the institutional office through the constitutional process.
   - **classification: named_gap_toward_strong** — additive; disclosed under P2, no architecture break.

## determination

- **≥ Partial on real evidence: YES.** P7 is **enforced at runtime, not descriptive.** Two real runs
  halted at `waiting_for_human_approval` with `approval_granted=false`; the completion contract
  cannot emit `approval_granted=true` nor attribute approval to a non-`approval` role (fail closed,
  16 contract tests green); and the human decision lives in a separate human-only, byte-bound record
  carrying the authority tuple `{approval, approval, 0.3.0}`. Automation literally cannot confer the
  authority. This clears the 0.4 baseline (descriptive model + one executable rule) — the one
  executable rule is landed in the frozen contract and demonstrated on real artifacts.
- **Strong-blocker: NO.** No open item requires breaking a frozen contract or changing the ratified
  architecture, and the Partial claim was not falsified when re-derived. Notably, the E.7 executable
  rule landed **without** modifying the frozen P7 invariant (additive; `task_version` bumped via the
  ratified change process). Every path to Strong (a real vacancy/transfer exercised end-to-end,
  executable succession, storage-format ratification, post-Genesis identity binding) is **purely
  additive** — §5 named gaps toward Strong, not contradictions.
- **Not yet Strong** only because the vacancy/escalation surface has never run on a real event
  (empty Genesis store) and succession is not yet executable — the full relevant surface is not yet
  demonstrated broadly on real (non-fixture) artifacts.

**Strongest evidence:** the executable approval-authority rule landed in the frozen
`trace_completion.py` + the engine's `grants_approval` refusal, demonstrated on real runs
(`RUN-REASON-20260717-0003`, `-20260718-0001`) paired with human-only `APPROVAL-0002/0003` — the
platform cannot self-grant approval or mis-attribute it, fail-closed, verified green.

**Weakest evidence:** vacancy/succession/escalation — wired to the runtime boundary and
fixture-proven, but never triggered by a real event (`role_acts.yaml` empty) and succession ordering
still descriptive.
