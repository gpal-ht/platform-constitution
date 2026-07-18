# IOA-O3 — Independent Obligation Assessment

| Field | Value |
|---|---|
| obligation_id | O3 — Canonicalization by evidence/review |
| principle | P3 (Nothing is canonical by existence) · P4 (Evidence over opinion) |
| assessor | Independent auditor (0.9 Constitutional Readiness audit). Attestation: assessor is NOT the builder of O3; verdict re-derived from primary evidence (artifacts, code, run records, recomputed digests, live tool execution). |
| roadmap_baseline | Emerging |
| claim_under_audit | Reached **Partial** at 0.5 |

## clause_under_test (quoted)

- **P3 — Nothing is canonical by existence.** "Knowledge becomes canonical only through
  evidence, review, and explicit acceptance — *including the platform's own knowledge.* The
  platform rejects documentation by accumulation, architecture by precedent, and knowledge by
  repetition."
- **P4 — Evidence over opinion.** "Challenges are settled by evidence, not by seniority,
  eloquence, or precedent."

## Evidence list

### E1 — The transformation workflow never confers canonicity (artifact)
- **artifact:** `C:\Dev\ecf\workflows\transformation\WF-TRANSFORM-0001-approved-recommendation-to-canonical-artifact.md`
  (v0.2.0, status: released). Eight deterministic tasks; `successful_exit_state: waiting_for_human_acceptance`.
- **demonstration:** Real run `RUN-TRANSFORM-20260717-0001` completion record
  (`runtime/runs/RUN-TRANSFORM-20260717-0001/reports/completion.yaml`) shows
  `final_run_status: waiting_for_human_acceptance`, `acceptance_granted: false`,
  `canonical_store_written: false`, `production_engine_invoked: false`. The run halted and wrote
  nothing to `canonical/`.
- **verified_by:** Read the workflow spec (Human Acceptance Boundary, "P7 applied twice"; Permission
  Boundaries prohibit writing `canonical/`) and re-read the actual completion.yaml of a real run.

### E2 — The human-invoked promotion refuses without BOTH human records and byte-binds artifacts (artifact + live demonstration)
- **artifact:** `C:\Dev\ecf\tools\canonical_promotion\promote.py`. `promote()` runs `verify_acceptance`
  (requires the human acceptance record — digest, attribution, run/approval binding) AND
  `_verify_approval_against_bundle` (requires the approval snapshot consumed at run entry, checks
  approving authority under the current model, and byte-binds the approved-report digest to the
  self-contained evidence-bundle copy). All checks are read-only and must pass before any write;
  `_check_store_free` enforces single-effective-use of an approval and refuses an already-taken EDR
  identity; it never overwrites the store.
- **demonstration (real, live — assessor executed the tool):**
  - TEST 1 — re-promote the already-canonicalized EDR-0003 with its genuine run + acceptance →
    `PROMOTION REFUSED — nothing was written`: "approval APPROVAL-0003 already produced canonical
    record 'EDR-0003' — single effective use (fail closed)"; "canonical identity EDR-0003 is already
    taken"; "canonical/decisions/EDR-0003/ already exists — promotion never overwrites the store
    (P14)". exit=1.
  - TEST 2 — promote with a nonexistent acceptance record → `PROMOTION REFUSED`: "acceptance record:
    record does not exist". exit=1. Confirms one human act (approval) alone cannot confer canonicity.
- **verified_by:** Read the full tool source and ran it against the live store; observed fail-closed
  refusals with nothing written.

### E3 — EDR-0002 and EDR-0003 are REAL canonical decisions produced through this path (artifact + real demonstration)
- **artifact:** `canonical/decisions/EDR-0002/`, `canonical/decisions/EDR-0003/`, and
  `canonical/decisions/index.yaml`. Two human records each:
  `approvals/APPROVAL-000{2,3}.yaml` (approval) and `approvals/ACCEPTANCE-000{2,3}.yaml` (acceptance),
  both `accepted_by: Founder (Genesis)`; evidence bundles under each `evidence/`.
- **demonstration (real, not fixture):** Two genuinely distinct engineering decisions on different
  Work Requests —
  - EDR-0002 = WR-0001 "Should Repository Integration become a first-class subsystem?",
    disposition `gather_additional_evidence`, promoted in **supersede mode** over EDR-0001 on
    `better_evidence` grounds (the platform's first real supersession of canonical knowledge);
  - EDR-0003 = WR-0004 desktop UI framework, disposition `proceed_with_conditions` (adopt WinUI 3
    behind a bounded Experience subsystem), a **fresh** canonical decision resolving a novel
    question in the affirmative.
  Each approval statement records that the source recommendation was independently validated
  (verdict: passed) before the human decided.
- **verified_by (recomputed digests — byte-binding is real, not merely claimed):**
  - `sha256(canonical/decisions/EDR-0002/EDR-0002.md)` = `4b8f1de3…39b2d` = index `record_sha256`. ✓
  - `sha256(canonical/decisions/EDR-0003/EDR-0003.md)` = `7ed86998…2c8e` = index `record_sha256`. ✓
  - `sha256(EDR-0002/evidence/engineering-recommendation-report.md)` = `40db94c5…4eaf` = the digest
    the human byte-approved in APPROVAL-0002 (`approved_artifacts[0].sha256`). ✓
  - `sha256(EDR-0003/evidence/engineering-recommendation-report.md)` = `5843798d…44c8` = the digest
    the human byte-approved in APPROVAL-0003. ✓
  The stored canonical bytes equal the ledger pin, and the promoted record carries the exact bytes
  the human approved — the review/evidence chain is cryptographically closed.

## maturity_verdict

**Partial** (met on real, non-fixture evidence; approaches Strong).

Rationale against §4 rubric: the mechanism is implemented AND demonstrated on real artifacts
(EDR-0002 supersession, EDR-0003 fresh — plus EDR-0001), not fixtures; every gap to Strong is named
below; and no architectural contradiction prevents Strong. This satisfies the per-obligation 1.0 bar.
The path is the *only* way `canonical/` can be written: the workflow is structurally prohibited from
writing it and halts at `waiting_for_human_acceptance`, and `promote.py` is the sole writer and
fail-closes without both human records plus digest-verified byte-binding. P3 ("nothing canonical by
existence") is enforced by construction — canonicity is conferred by two distinct human acts +
independent validation + digest binding, never by an artifact's mere presence. P4 ("evidence over
opinion") is embodied in the digest-binding and re-verification: the record that stands is the one
the evidence proves, not the one asserted.

## open_items

1. **description:** Demonstrated breadth is modest — 3 real canonical decisions, a single canonical
   store (ECF), and a single approver identity ("Founder (Genesis)", Genesis-condition attestation).
   Strong ("full relevant surface … demonstrated broadly") wants more decisions and, in time, a
   distinct approval authority once End-of-Genesis introduces additional constitutional authority.
   - **classification:** named_gap_toward_strong
   - **grounds:** Purely additive within the ratified architecture — more decisions through the same
     unchanged path. The Partial claim already stands on real evidence; no contract or architecture
     change is required to add coverage.

2. **description:** The refusal matrix (rejected/malformed/tampered/mis-attributed acceptance;
   digest-mismatched bundle; already-consumed approval) is proven by the tool's code, its fixtures,
   and the assessor's live synthetic refusal tests — but a *production* refusal driven by a genuine
   rejected human acceptance has not yet occurred (reality-gated).
   - **classification:** named_gap_toward_strong
   - **grounds:** The machinery is proven end-to-end (the assessor executed the tool and observed
     fail-closed refusals with nothing written); only a real triggering event is absent. Under §5
     this is a named gap, not a blocker.

## determination

- **≥ Partial?** YES — implemented and demonstrated on real (non-fixture) artifacts EDR-0002 and
  EDR-0003; two-human-act gate confirmed live and fail-closed by direct tool execution; byte-binding
  re-derived from recomputed digests.
- **Any Strong-blocker?** NO — no open item requires breaking a frozen contract or changing the
  ratified architecture, and the Partial claim was not falsified on re-derivation (it was confirmed).
  Both open items are additive/reality-gated named gaps toward Strong.
