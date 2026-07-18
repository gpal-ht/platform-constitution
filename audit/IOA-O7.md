# IOA-O7 — Corrigibility: safe supersession while preserving history

| Field | Value |
|---|---|
| obligation_id | O7 |
| principle | P14 — Canonical knowledge is corrigible (*History is preserved; truth is revised.*) |
| assessor | Independent auditor (0.9 Constitutional Readiness audit). Attestation: the assessor did NOT build O7; every finding below was re-derived from primary evidence (records, code, live re-execution), not from builder claims (§2–§3 of the ratified audit method). |
| roadmap_baseline | Emerging |
| claimed | Partial (reached 0.6) |

## clause_under_test (quoted)

> **P14 — Canonical knowledge is corrigible.**
> Every canonical decision must remain replaceable by better evidence without denying its
> historical existence. *History is preserved; truth is revised.* This forecloses rewriting
> history, deleting mistakes, "latest wins," and immutable dogma in a single stroke.

Central operational rule under test: **superseded bytes are NEVER rewritten; effective status
derives from the supersession chain.**

## evidence

### E1 — The superseded record's bytes are intact and match their promotion-time pin (the P14 core)
- **artifact:** `C:\Dev\ecf\canonical\decisions\EDR-0001\EDR-0001.md` (7242 bytes) and the ledger `C:\Dev\ecf\canonical\decisions\index.yaml` (entry EDR-0001, `record_sha256: 2fb71c580633887e2aec25cd83927ef99aa15770088286dc912fc2be6392c553`).
- **demonstration (real, not fixture):** the actual first canonical supersession EDR-0001 → EDR-0002 on `better_evidence` grounds, authored by the Founder in the 0.6 exit sequence.
- **verified_by:** assessor computed `sha256(EDR-0001.md)` = `2fb71c…c553` — byte-identical to the ledger pin. Ran the tool's own invariant `promote.verify_history_intact('.', 'EDR-0001')` against the live store → `INTACT`; likewise EDR-0002 and EDR-0003. EDR-0001's directory still exists intact with its original `evidence/` and `evidence-manifest.yaml`.

### E2 — The write-once supersession marker exists and is consistent with the ledger chain
- **artifact:** `C:\Dev\ecf\canonical\decisions\EDR-0001\superseded-by.yaml` (`superseded_by: EDR-0002`, `grounds: better_evidence`, `grounds_ref: RUN-REASON-20260716-0002`, `superseding_record_sha256: 4b8f1de3…39b2d`).
- **demonstration:** written by `promote.py` with open-mode `x` (create-new), the only write the tool performs inside an existing store directory.
- **verified_by:** assessor read the marker; `decision_records.check_supersession_target` fail-closes if a marker exists without a matching index chain edge (lines 553–559) — the marker is a sibling record, not an edit of EDR-0001.

### E3 — Effective status DERIVES from the chain (not "latest wins", not stored-on-the-old-record)
- **artifact:** `index.yaml` — the *new* entry (EDR-0002) carries `supersedes: EDR-0001` and `supersession_grounds: better_evidence`; the EDR-0001 entry is unedited. `decision_records.superseding_entries()` (reverse walk, lines 516–522) derives `superseded_by` from the ledger.
- **verified_by:** assessor confirmed the chain edge lives ONLY on the new entry; EDR-0001's own entry is byte-unchanged from its original promotion. Effective "superseded" status is computed by reverse walk over `supersedes`, satisfying "effective status derives from the supersession chain."

### E4 — EDR-0001 is not deleted, rewritten, or de-cited
- **verified_by:** EDR-0001 directory present and intact (E1). EDR-0002.md still cites EDR-0001 three times, including "EDR-0001 remains intact, citable, and superseded, never rewritten (P14)" (line 47) and the supersession-intent block (line 142). The acceptance record states "EDR-0001 is not deleted, rewritten, or de-cited … its bytes unchanged, its status derived as superseded from the store chain (P14)."

### E5 — promote.py SUPERSEDE MODE re-verifies target bytes BEFORE and AFTER, and refuses on tamper
- **artifact:** `C:\Dev\ecf\tools\canonical_promotion\promote.py` — `verify_history_intact` called PRE-write (lines 326–327, "pre-supersession invariant") and POST-write (lines 498–504); tamper raises fail-closed.
- **demonstration (live, adversarial):** assessor copied the store to an isolated scratch dir, appended one byte to `EDR-0001.md`, and re-ran `verify_history_intact` → refused: `EDR-0001 bytes on disk (0d033efe…) != the ledger's promotion-time record_sha256 (2fb71c…c553) — history is not intact (fail closed)`. Real store never touched.
- **verified_by:** direct code read + live tamper re-derivation. Mode is activated solely by the acceptance record carrying a `supersedes` block (line 369), never a flag; equality of the `supersedes` block across approval/candidate/acceptance is enforced by `verify_acceptance`.

### E6 — The supersession vehicle (WF-TRANSFORM-0001 0.2.0) carries the intent end-to-end
- **artifact:** `C:\Dev\ecf\workflows\transformation\WF-TRANSFORM-0001-approved-recommendation-to-canonical-artifact.md` (version 0.2.0). The `supersedes` intent flows approval → candidate render → validation → acceptance; the workflow halts at `waiting_for_human_acceptance` having written nothing; only the human-invoked promote executes the store act (lines 24–26, 299, 520–524).
- **demonstration:** real acceptance record `ACCEPTANCE-0002` (`workflow_id: WF-TRANSFORM-0001`, `workflow_version: 0.2.0`, `decision: accepted`, `supersedes: {EDR-0001, better_evidence, RUN-REASON-20260716-0002}`), authored on Founder instruction "Accept and supersede-promote".
- **verified_by:** assessor read the workflow and both human records; store `evidence-manifest.yaml` records `promotion.tool: tools/canonical_promotion`, `human_invoked: true`, and the `supersedes` block.

### E7 — Mechanism is test-proven (buttresses breadth)
- **verified_by:** ran `python -m pytest tests/test_promote.py -q` → **26 passed**. Tests exercise refusal paths (tamper, already-superseded/no-forks, self-supersession, missing marker, grounds vocabulary).

## maturity_verdict

**Partial.** The mechanism is implemented AND demonstrated on a genuine, non-fixture artifact — the platform's first real canonical supersession (EDR-0001 → EDR-0002, `better_evidence`), authored by the Founder. The central P14 rule holds on re-derivation: superseded bytes are byte-identical to their promotion-time pin (E1), status derives from the chain (E3), the record is not deleted/rewritten/de-cited (E4), and the tool fail-closes on tamper (E5, live). Every gap to Strong is named below and is purely additive within the ratified architecture; no architectural contradiction prevents Strong. The Partial claim is confirmed, not merely accepted.

## open_items

1. **description:** Real demonstration is n=1 — a single supersession (EDR-0001 → EDR-0002). Strong requires the mechanism to hold across the full decision surface, demonstrated broadly.
   **classification:** named_gap_toward_strong
   **grounds:** Additive coverage within the existing architecture; the machinery is proven end-to-end (live invariant + 26 tests). No contract or architecture change is required to add further supersessions.

2. **description:** The `invalidated_assumption` grounds class is INTERFACE-ONLY at 0.6 (Track B seam; `decision_records.check_supersession_grounds` documents it as an explicit O7-7/P2 gap). Only `better_evidence` was exercised on a real artifact.
   **classification:** named_gap_toward_strong
   **grounds:** The gap is honestly self-declared in code (P2/O2), not concealed. Wiring the remaining grounds class is additive; the demonstrated grounds path is fully implemented and fail-closed. Reaching Strong-breadth here adds coverage, it does not break a frozen contract.

3. **description:** Fork/multi-head safety (refusing supersession of an already-superseded record) and the pre/post invariant are proven by refusal logic and fixtures, but not demonstrated on a real multi-supersession chain.
   **classification:** named_gap_toward_strong
   **grounds:** Reality-gated on a second real supersession; the machinery (`superseding_entries` reverse walk, `check_supersession_target` no-forks refusal) is fixture-proven and the no-forks rule is enforced. Purely additive.

## determination

- **>= Partial on real evidence?** YES — confirmed by independent re-derivation (E1–E7), not by builder claim.
- **Any contradiction blocking Strong?** NO. Neither §5(a) (Strong needs no frozen-contract/architecture break — it needs more real supersessions and the remaining grounds classes wired, both additive) nor §5(b) (the Partial claim was re-derived and holds — bytes intact, chain-derived status, tamper-refused live) applies. All three open items are named gaps toward Strong.
- **1.0 bar (>= Partial, no Strong-blocker):** MET for O7.
