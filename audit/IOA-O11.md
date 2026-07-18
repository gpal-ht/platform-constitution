# IOA-O11 — First-class assumptions: executable assumptions with review triggers

| Field | Value |
|---|---|
| obligation_id | O11 |
| principle | P11 — Assumptions are first-class, executable artifacts (pillar: Reproducible) |
| assessor | Independent auditor (0.9 Constitutional Readiness audit). Attestation: assessor did NOT build the assumption registry, the evaluators, the release gate, or the dependency resolver; every finding below was re-derived from primary evidence (code read directly; tools executed by the assessor). |
| roadmap_baseline | Emerging |
| claimed | Partial (reached at 0.6) |

## clause_under_test (quoted)

> **P11 — Assumptions are first-class, executable artifacts.**
> Decisions declare their assumptions with confidence, evidence, and review triggers, so
> that reality can challenge them. The reasoning need not be executable; the assumptions
> that support it can be.

Operative test for this audit: are review triggers **executable** — evaluated
deterministically against recorded inputs (closure records, file digests, dates) — rather than
descriptive prose; and has that machinery been demonstrated on **real** registered assumptions
in a **real** release path (the forcing function), not on fixtures?

## Evidence list

Each entry: artifact + demonstration (real, not fixture) + how the assessor re-derived it.

1. **Executable evaluators (the "executable" clause).**
   - artifact: `C:\Dev\ecf\tools\assumption_registry\evaluators.py` — three registered, deterministic, stdlib-only trigger classes: `evidence_arrival_v1` (fires on a schema-valid human-authored closure record binding the subject `{run_id,item_id}`), `dependency_change_v1` (fires when the current streamed SHA-256 of the subject path differs from the declared baseline; absence fails toward firing), `time_based_v1` (fires when recorded `as_of` is past `review_by`). `REGISTERED_IMPLS` is a closed table; `evaluate_trigger` fails closed to `defective_input` on an unregistered class/impl. Driver: `evaluate.py`.
   - demonstration: triggers are evaluated against **recorded inputs only** (closure records, file digests, the recorded `--as-of` date) — not prose. Confirmed in code (`evaluate.py:248-319`) and in the real evaluation records below.
   - verified_by: read both files in full; each evaluator returns a closed `{outcome, observed, fired_because}` dict computed purely from recorded artifacts. No interpretation, no scoring — the machine detects the record/digest/date, never judges evidence (P7/P4 preserved).

2. **Real registered assumptions (the "first-class" clause).**
   - artifact: `C:\Dev\ecf\assumptions\index.yaml` + `ASM-0001..ASM-0004\assumption.yaml`. Real assumptions harvested from real canonical decisions EDR-0001 (ASM-0001/0002) and EDR-0002 (ASM-0003/0004), each carrying statement, evidence_strength, digest-bound provenance (`source_sha256`), declaring actor, and executable `review_triggers` wired to `evaluate.py` impls. ASM-0003/0004 declare `supersedes_assumption` ASM-0001/0002.
   - demonstration: these are genuine harvested assumptions from approved recommendation reports, not test fixtures (real EDR provenance digests, real decision refs).
   - verified_by: read the index and every ASM record; cross-checked provenance digests against the dependency resolver (evidence 5).

3. **Real firing → routed → reviewed (the forcing function, end-to-end).**
   - artifact: `assumptions\evaluations\EVAL-20260716T162710Z.yaml`; `ASM-0001\obligations\OBL-20260716-0001\{obligation,review}.yaml` (and OBL-0002).
   - demonstration (REAL, not fixture): on 2026-07-16 both `evidence_arrival` triggers TRG-0001/TRG-0002 **fired** on real closure records `CLOSURE-0001`/`CLOSURE-0002`, each producing a routed obligation (`effective_recipient: accountability`, `degraded: false`), which was then **reviewed** — outcome `reaffirmed`, with digest-bound evidence and a rationale proceeding on `better_evidence` grounds (O7). A prior evaluation (`EVAL-20260716T142834Z`, same triggers) recorded `not_fired` before the closures arrived — so the state transition from not-fired → fired → obliged → reviewed is present in the record trail. This is reality challenging a declared assumption, exactly what P11 requires.
   - verified_by: read both EVAL records, the obligation, and the review; the fired evaluation's `obligation_id` matches the persisted obligation, whose `fired_because` matches the fired trigger's `fired_because` (the idempotence cause-key).

4. **The O11 RELEASE gate (gate 10) — read-only, fails closed.**
   - artifact: `C:\Dev\ecf\scripts\validate-release.py` `gate_10_assumption_triggers` (called from `main`, line 364). Since 0.8.3 (H3) it invokes `evaluate.py --repo-root . --invoked-by release_gate --check`.
   - demonstration: assessor ran `evaluate.py ... --check` at as-of 2026-07-18: `evaluated 7 trigger(s) across 4 assumption(s); 0 would newly fire; nothing written`, exit 0, and `git status assumptions/` was **clean** afterward — the gate wrote no EVAL record and no obligation. The would-fire fail-closed path returns `EXIT_UNPERSISTED_FIRING` (exit 3) so a release cannot proceed while a trigger would newly fire without a persisted+routed obligation (`evaluate.py:325-335`; covered by `test_evaluate.py:349 test_check_fails_closed_on_a_would_fire_trigger`).
   - verified_by: assessor executed the gate command directly and inspected the working tree; read the `check_only` branch and its test.

5. **Invalidation / dependency (supersession via O7 grounds).**
   - artifact: `C:\Dev\ecf\tools\assumption_dependency\resolve.py` — read-only; derives ASM→EDR edges purely from digest matches (`source_sha256` == EDR approved-report digest), re-verifies every manifest, and REFUSES (writes nothing) on any scalar-vs-digest disagreement, lineage fork/cycle, or unverifiable manifest.
   - demonstration (REAL): assessor ran `dependents ASM-0001` → `EDR-0001 (superseded)`; `current-dependents ASM-0001` → `EDR-0002` (reached by closing over the human-authored lineage ASM-0001→ASM-0003). Real supersession chain on real assumptions.
   - verified_by: assessor executed both subcommands; exit 0, output consistent with the index's `supersedes_assumption` edges.

6. **Mechanism built (tests).** `python -m pytest` — registry tests 63 passed, dependency tests 10 passed (73 total). Supports Emerging/Strong-breadth; does not by itself lift to Partial (§2) — the real demonstrations above do.

## maturity_verdict

**Partial.**

The mechanism is implemented AND demonstrated on real, non-fixture artifacts: real assumptions harvested from real EDRs; a real `evidence_arrival` trigger that fired on real closure records, wrote a routed obligation, and received a recorded reaffirmation review; a release gate the assessor ran that evaluates every declared trigger and fails closed; and a supersession/dependency resolver the assessor ran on the real lineage. Every gap to Strong is named below and each is purely additive within the ratified architecture. No architectural contradiction prevents Strong.

Emerging-vs-Partial subtlety (noted honestly): the roadmap baseline was Emerging, and much of the surface is exercised only through evaluation records that read `not_fired`. What lifts O11 above Emerging is evidence 3 — a genuine firing on a real artifact producing a real reviewed obligation. Without that single real firing, the honest verdict would be Emerging (mechanism + fixtures only). It exists, so Partial holds.

## open_items

1. **Harvest scope is deliberately partial.** Only decision-report assumptions are registered; the analysis-register assumption sequences (`engineering-reasoning-context.yaml`, `engineering-risks.yaml`) are explicitly un-harvested per ratified PROPOSAL_O11 §1.2 and are surfaced in every EVAL record's `gaps.unharvested_sources`.
   - classification: **named_gap_toward_strong**
   - grounds: additive (harvest more sources within the same registrar); the gap is recorded openly in the tool's own output (P2 honored), not concealed. No contract break needed to close it.

2. **Only two of three trigger classes have fired on real events.** `evidence_arrival` fired for real (evidence 3); `dependency_change` and `time_based` have only recorded `not_fired` on real inputs (real digests/dates) — no real firing yet. A fourth, operational-evidence class is a named deferral awaiting the FD-2 ruling (`evaluators.py` docstring).
   - classification: **named_gap_toward_strong**
   - grounds: reality-gated — the machinery is proven end-to-end (a real firing routed and reviewed); only the triggering reality (a real dependency change / a passed review date) is absent for the other two classes. Reaching Strong is additive.

3. **Single-plane surface.** The registry, evaluators, gate, and resolver live in the Control plane (ecf) where canonical decisions live; engineering_kb and context_switcher carry no registry.
   - classification: **named_gap_toward_strong**
   - grounds: additive breadth. The clause is satisfied where consequential decisions are recorded (ecf); extending the mechanism to other planes is coverage, not a contradiction.

No open item is a contradiction blocking Strong. The Partial claim was re-derived, not accepted: the real firing, the routed/reviewed obligations, the read-only gate, and the supersession resolution were all reproduced by the assessor. The 0.8.3 read-only-gate change does not weaken the forcing function — `--check` fails closed (exit 3) on a would-fire trigger, so a release still cannot proceed past an un-obliged firing; it merely stops the gate from mutating the store.

## determination

- maturity_verdict: **Partial**
- ≥ Partial on real evidence? **YES**
- Any Strong-blocker (contradiction blocking Strong / falsified Partial claim)? **NO** — all three open items are named gaps toward Strong; the Partial claim was independently re-derived and holds.
