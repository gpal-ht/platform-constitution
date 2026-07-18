# IOA-O4 — Independent Obligation Assessment

| Field | Value |
|---|---|
| obligation_id | O4 — Answerability (durable, transferable stewardship & challenge routing) |
| principle | P5 (Answerability) · Root Clarification B (challengeability requires answerability) · Clarification C (institutional continuity of responsibility) |
| assessor | Independent auditor (0.9 Constitutional Readiness audit). Attestation: assessor is NOT the builder of O4; verdict re-derived from primary evidence — module source, the frozen completion contract, the real challenge/disposition/approval records, and live re-execution of the checkers by the assessor. |
| roadmap_baseline | Emerging (`PLATFORM_ROADMAP.md` line 50) |
| claim_under_audit | Reached **Partial** at 0.5 (durable, transferable stewardship across the lifecycle) |

## clause_under_test (quoted)

- **P5 — Answerability.** "Every consequential engineering decision must have a durable
  accountable authority, an escalation path, and a recorded disposition. The five roles below are
  distinct and transferable." The five roles: "**authorship** … **approval** … **ownership** …
  **accountability** (who must answer for its continued validity or initiate reconsideration) ·
  **responsibility acceptance** …". "Accountability requires *durable accountable authority*, not
  eternal attachment to the original author. The role is transferable while the historical chain is
  preserved."
- **Clarification B — Challengeability requires answerability.** "A challenge that reaches no
  accountable recipient is not a challenge. Every consequential decision must have a durable path by
  which a challenge reaches an accountable authority and receives a recorded disposition."
- **Clarification C — Institutional continuity of responsibility.** The accountable authority "is an
  **office**, not merely an individual holder … the **institutional** authority behind the office
  persists across holders and is **never vacant by construction** … it rests with the institution's
  standing accountable authority (under the current constitutional order, the **Founder** …)."

## Evidence list

### E1 — The role→authority model is executable and version-pinned (artifact)
- **artifact:** `C:\Dev\ecf\tools\authority_rule\authority_model.py` — authority **model 0.3.0**
  (`MODEL_VERSION = "0.3.0"`). Five ratified roles (closed set). `_AUTHORITY_BINDINGS` binds
  `ownership → stewardship_transfer`, `accountability → {challenge_disposition, assumption_review}`,
  `approval → approval`. `holds_authority()` **fails closed** on any other model version or unknown
  role. `ESCALATION_TARGETS = {role → founder_genesis}` (E.4 named targets; the token names an
  office, not a person).
- **demonstration:** assessor executed `holds_authority` — `accountability` holds
  `challenge_disposition` at 0.3.0 (True) and does NOT at 0.2.0 (False, strict pin).
- **verified_by:** read the module; re-ran the predicate. This is a live table consulted by rules, not
  a descriptive doc.

### E2 — Stewardship state is a fold over an append-only recorded-acts ledger, wired into the LIVE frozen contract (artifact + live execution)
- **artifact:** `role_state.py` (`StewardshipLedger`: `record_transfer` E.2 no-gap, `record_vacancy`
  E.3 recorded-never-silent, `resolve()` Clarification C never-to-nowhere, `load_ledger`/`replay_acts`
  fail-closed on malformed history) and `check_stewardship.py` (`route_challenge`, `record_disposition`,
  `check_approval_boundary_state`). **Crucially, these are consulted at runtime:** the frozen completion
  contract `tools/task_runner/output_contracts/trace_completion.py` imports
  `check_approval_boundary_state` and `load_ledger` (lines 58–59) and calls them in `_check_role_state`
  (lines 233–259), invoked from `_check_approval_boundary` on every reasoning-run completion.
- **demonstration (real, live — assessor executed the contract against a REAL run):** on the real
  completion record `runtime/runs/RUN-REASON-20260718-0001/reports/completion.yaml` (dated 2026-07-18),
  the live contract's `_check_approval_authority_binding` and `_check_role_state` both returned **no
  reasons** — the run passes the O4 boundary, its `approval_authority` tuple bound to model 0.3.0
  (role=approval, authority=approval), office active, no spurious escalation. Assessor then exercised
  all four vacancy paths on a ledger: active+conformant → pass; active+spurious-escalation → REJECT
  (P2); vacant+silent → REJECT (E.3 fail closed); vacant+disclosed-escalation → pass, visibly degraded.
- **verified_by:** read the frozen contract wiring; ran the live checks on a genuine completion record
  and on a `record_vacancy`-mutated ledger.

### E3 — A REAL challenge was routed to the accountable office and received a recorded evidence-bearing disposition (real, not fixture)
- **artifact:** `C:\Dev\ecf\challenges\CHG-20260716-0001\{challenge.yaml, disposition.yaml}` — the
  platform's one real challenge, bound to a **genuine canonical artifact** (`challenges.kind: artifact`,
  `ref: canonical/decisions/EDR-0001`). Routing (router-written): `accountable_role: accountability`,
  `authority: challenge_disposition`, `effective_recipient: accountability`, `degraded: false`,
  `model_version: "0.2.0"`. Disposition: `rejected`, four evidence refs (EDR-0001 front matter, the
  transformation candidate report, APPROVAL-0001, ACCEPTANCE-0001), a reasoned rationale, recipient =
  the routed accountable recipient.
- **demonstration (real):** the Founder (Genesis) contested whether canonicalizing a
  gather-more-evidence disposition overstates EDR-0001's standing; the challenge reached the
  accountable office and was disposed `rejected` on evidence (P4) — Clarification B end-to-end on a real
  platform decision, not a fixture.
- **verified_by:** assessor re-ran the live mechanism. (a) `validate_routed_challenge` on the real
  record → no reasons; recipient == routed effective_recipient. (b) Re-routing the real challenge's
  filed fields through the current `route_challenge` on a fresh Genesis ledger reproduced the recorded
  routing — `effective_recipient: accountability`, `degraded: false` — differing only by stamping model
  0.3.0. (c) `validate_disposition_record` under 0.3.0 fails **only** on the model-version pin
  (`'0.2.0' != '0.3.0'`), never on the merits — the historical record stands as recorded (P14/P9),
  corroborated by the passing suite `tests/test_historical_records_stand.py`.

### E4 — Real approval-authority tuples are bound in real records across the lifecycle (real, not fixture)
- **artifact:** `approvals/APPROVAL-0002.yaml` carries `authority: {role: approval, authority: approval,
  model_version: "0.3.0"}` on a real human decision (supersedes EDR-0001, better_evidence). Real
  completion records `runtime/runs/RUN-REASON-2026071*/reports/completion.yaml` carry the same
  `approval_authority` tuple consumed by the frozen contract.
- **demonstration/verified_by:** read the records; confirmed (E2) the live contract accepts the real
  0.3.0 binding and fail-closes an unauthorized or mis-versioned one via `holds_authority`.

## maturity_verdict

**Partial** (met on real, non-fixture evidence; no architectural contradiction preventing Strong).

Rationale against the §4 rubric: the mechanism is implemented (E1/E2) AND demonstrated at least once on
a real, non-fixture artifact — a real challenge routed to an accountable recipient with a recorded
evidence-bearing disposition (E3), and real approval-authority tuples enforced at the live boundary
(E2/E4). The roadmap's concern that "vacancy/succession/escalation are descriptive-only" (its O6 row,
line 52) is **resolved for the runtime-enforcement half**: the recorded-acts ledger is now *consulted*
by the frozen completion contract, and vacancy disclosure / escalation-to-institutional-fallback is
fail-closed enforced (assessor re-derived all four boundary paths). Answerability holds by construction
against Clarification C: `resolve()` never returns nowhere; a vacant office escalates, visibly degraded,
to `founder_genesis`. Every gap to Strong is named below and each is additive within the ratified
architecture. This satisfies the per-obligation 1.0 bar.

## open_items

1. **description:** Vacancy, transfer, and escalation have **never been triggered by a real event** —
   `tools/authority_rule/role_acts.yaml` is empty (`acts: []`, the Genesis initial condition). The
   degraded-routing and vacancy-disclosure paths are proven only on synthetic ledgers (tests + the
   assessor's live `record_vacancy` exercise), not on a recorded real vacancy/transfer.
   - **classification:** named_gap_toward_strong
   - **grounds:** Reality-gated. The machinery is proven end-to-end (assessor drove all four boundary
     outcomes and the E.2 no-gap transfer rule); only a genuine triggering act is absent. §5 treats a
     reality-gated item with fixture-proven-but-here-live machinery as a named gap, not a blocker.

2. **description:** Answerability breadth is modest — exactly **one** real challenge (against one
   canonical decision), a single accountable office, and a single actor identity ("Founder (Genesis)",
   who both filed and disposed CHG-20260716-0001 under the Genesis single-office condition). Strong
   ("full relevant surface … every decision … demonstrated broadly") wants many decisions carrying
   challenge/stewardship records and, post-End-of-Genesis, a disposer distinct from the challenger.
   - **classification:** named_gap_toward_strong
   - **grounds:** Purely additive coverage through the unchanged path; the same-actor file/dispose is
     the disclosed Genesis institutional-continuity condition (Clarification C; carried in the standing
     Reaffirmation Obligation), not a P5 defect — P5 requires a challenge *reach an accountable
     recipient and receive a recorded disposition*, which it did. No contract or architecture change is
     required to add breadth.

3. **description:** Succession *ordering* (E.5's ordered next-holder rule), escalation beyond one hop,
   challenge SLAs/timeouts, multi-holder offices, and ratification of the persistent `role_acts.yaml`
   storage format are not implemented — explicitly scoped out of Partial by
   `PROPOSAL_O4_STEWARDSHIP_SCOPE` §5.
   - **classification:** named_gap_toward_strong
   - **grounds:** Named as deepening targets by the ratified scope (P2 honesty), each additive within
     the existing five-role / single-version-pin / institutional-fallback architecture. Succession as
     *reseat* (transfer from a vacant office to an accepting incoming holder) IS implemented and
     test-proven; only ordered-succession is deferred.

## determination

- **≥ Partial?** YES — implemented and demonstrated on real (non-fixture) artifacts: a real challenge
  routed to the accountable office with a recorded evidence-bearing disposition (E3), real
  approval-authority tuples enforced at the live frozen boundary (E2/E4). Stewardship + challenge
  routing is EXECUTABLE and runtime-enforced, not descriptive — re-derived by the assessor running the
  checkers.
- **Any Strong-blocker?** NO — no open item requires breaking a frozen contract or changing the
  ratified architecture, and the Partial claim was not falsified on re-derivation (the real challenge
  re-routes correctly under the live 0.3.0 mechanism; the 0.2.0 record's strict-pin refusal is
  by-design history, failing only on the version pin, never on the merits). All three open items are
  additive / reality-gated named gaps toward Strong.
