# IOA — O2: Platform self-honesty (P2)

| Field | Value |
|---|---|
| obligation_id | O2 |
| principle | P2 — The platform is honest about itself |
| assessor | Independent auditor (Constitutional Readiness audit, milestone 0.9). Attestation: the assessor did **not** build the ECF release process, the release notes, or gate 11; every finding below was re-derived from primary evidence (git tags, source, tests run by the assessor). |
| roadmap_baseline | Strong |
| assessed_maturity | **Strong** (baseline confirmed) |

## clause_under_test (quoted)

> **P2 — The platform is honest about itself.** Capabilities and limits are legible. Compliance is claimed only at the level actually demonstrated; unmet requirements are represented as explicit gaps, never hidden through weaker language, optimistic interpretation, or silent omission.
> *Ten-year test:* a system that conceals its limits is untrustworthy at any capability.

Reinforced by Clarification A (Root): "Known gaps between the principle and current capability must be recorded explicitly, treated as engineering obligations, and never concealed by weakening the principle."

O2 is assessed **reflexively** (PROPOSAL_09_AUDIT_METHOD §3): O2 *is* this audit's own conduct — gaps recorded, no verdict manufactured, every claim checked against primary evidence.

## evidence (artifact / demonstration / verified_by)

### E1 — The v0.8.0 → v0.8.1 honest self-correction (strongest evidence)
- **artifact:** `/c/Dev/ecf/release/RELEASE_NOTES_0.8.0.md` (correction banner, lines 10–16) + `/c/Dev/ecf/release/RELEASE_NOTES_0.8.1.md` ("Why this release exists").
- **demonstration (real, not fixture):** v0.8.0 was tagged with release notes describing 0.8 exit-sequence artifacts (JAR, `crossplane-manifest.yaml`, `CPV-project-0001.yaml`, `durable-pins-CLOSURE-0001.yaml`) that were completed on an unmerged branch and **were not in the tagged tree**. This real P2 violation was caught in post-release cleanup, recorded openly, and corrected in point-release v0.8.1 without rewriting the immutable v0.8.0 tag.
- **verified_by (assessor re-derivation from git):**
  - `git ls-tree -r v0.8.0 -- canonical/decisions/EDR-0002/` → **0** crossplane files, **0** judgment-attachment.yaml. The artifacts the notes named were genuinely absent from the tag.
  - `git ls-tree -r v0.8.1 -- .../crossplane .../judgment-attachment.yaml` → all 6 artifacts present. The correction is real.
  - `git show v0.8.0:release/RELEASE_NOTES_0.8.0.md | grep "Correction (2026-07-17"` → **0** — the correction banner is NOT in the immutable tag bytes; it exists only on the develop copy (matching the notes' own claim "the tagged v0.8.0 bytes are left immutable"). Tag immutability + corrigible-record honesty (P14) both hold.

### E2 — The release-notes honesty GATE (mechanization of the failure)
- **artifact:** `/c/Dev/ecf/scripts/validate-release.py` gate 11 (`gate_11_notes_referenced_artifacts`, lines 273–342) + test `/c/Dev/ecf/scripts/test_validate_release_notes_gate.py`.
- **demonstration:** gate 11 fails closed when release notes reference a `.yaml/.yml/.json` artifact absent from the tree — the exact v0.8.0 failure mode — and is self-validating (it checks its own version's notes).
- **verified_by:** assessor RAN `python scripts/test_validate_release_notes_gate.py` → **7 passed, 0 failed**, including `test_gate_fails_on_missing_artifact` (the v0.8.0 class fails closed) and `test_gate_passes_current_release_notes`. Provenance re-derived: gate 11 is **absent** from v0.8.0 and v0.8.1 validators, **present** in v0.8.2 and v0.8.3 (`git show <tag>:scripts/validate-release.py | grep -c gate_11...`). The v0.8.0 tagged notes contain exactly the inline `.yaml` tokens (`CPV-project-0001.yaml`, `crossplane-manifest.yaml`, `durable-pins-CLOSURE-0001.yaml`) gate 11 checks — i.e. the gate would have blocked v0.8.0, as 0.8.2's notes claim (RELEASE_NOTES_0.8.2.md line 31–32). Full honesty loop verified: violation → open record → correction (tag-immutable) → mechanized fail-closed gate → self-validation.

### E3 — Recorded named gaps on real releases (deferral, not concealment)
- **artifact/demonstration/verified_by:** `RELEASE_NOTES_0.7.0.md` records **O12A-5 "UNMET-and-open"** (lines 69, 77, 81–82) — a bar clause shipped deliberately unmet as an honest obligation "recorded honestly, never manufactured (P2)". `RELEASE_NOTES_0.8.0.md` records the **O8 walk-via-git-objects** Strong-tier gap explicitly (lines 68–78, "recorded, not concealed — P2"). Honest deferral/gap language recurs across 0.4.0–0.8.3 (assessor grep confirms non-trivial gap-recording in every milestone's notes).

### E4 — The audit's own conduct (reflexive)
- **artifact:** `/c/Dev/platform/PROPOSAL_09_AUDIT_METHOD.md`.
- **demonstration/verified_by:** the ratified method's governing edge (line 18) forbids manufactured verdicts — "a passing verdict is never manufactured to reach 1.0"; §3 mandates the primary-evidence rule; §7 defines "1.0 threshold NOT YET met" as "the audit working, not failing (P2)." This IOA itself records its gaps (below) rather than rubber-stamping the Strong baseline — the reflexive evidence is this document.

## maturity_verdict

**Strong.** P2 holds across the full relevant release surface, demonstrated on a real, unmanufactured event: the platform shipped a genuine self-description error and then recorded it, corrected it under tag-immutability constraints, mechanized a fail-closed guard against its recurrence, and self-validated that guard. The disposition to record-not-conceal is further shown by standing named-unmet clauses (O12A-5, O8 walk gap) on real releases, and reflexively by this audit's own gap-recording method. No consequential *unnamed* gap was found; the scope limits below are named in the artifacts themselves.

## open_items

### OI-1 — Mechanical honesty enforcement is narrow (data-artifact existence only)
- **description:** Gate 11 existence-checks only inline-code `.yaml/.yml/.json` tokens (deliberately, to avoid prose false-positives). Prose maturity claims, capability/compliance overstatement, `.md`/`.py` references, and test-count assertions are **not** mechanically enforced; that breadth of P2 rests on process/assessor diligence, not a checker.
- **classification:** named_gap_toward_strong
- **grounds:** Reaching broader mechanical honesty is purely additive within the existing architecture (more gate coverage) — no frozen contract or ratified architecture must break. The limitation is named openly in the gate docstring and RELEASE_NOTES_0.8.2.md ("Deliberately narrow"), so it is a *named* gap, not an unnamed one, and does not falsify the Strong demonstration.

### OI-2 — Prevention of the v0.8.0 class was reactive, not preventive, until 0.8.2
- **description:** The v0.8.0 notes/tree mismatch was caught by human post-release cleanup, not by a pre-release gate (which did not yet exist). The gate closing this class landed only in v0.8.2.
- **classification:** named_gap_toward_strong
- **grounds:** P2 requires that gaps be *recorded, not concealed* (Clarification A), which held completely; the reactive-then-mechanized response is the honest behavior P2 demands, and the class is now gated fail-closed. Closing further latent classes is additive. Does not block Strong and does not falsify the Partial-or-better claim.

## determination

- **>= Partial on real evidence?** **YES.** P2 is demonstrated on real (non-fixture) releases, re-derived by the assessor from git tags, source, and a test run.
- **Any Strong-blocker (contradiction blocking Strong)?** **NO.** Neither open item falsifies the demonstration, and neither requires breaking a frozen contract or the ratified architecture to resolve — both are purely additive coverage. The Partial claim is not falsified on re-derivation.
- **Verdict:** **Strong** — roadmap baseline confirmed. O2 clears the 0.9 → 1.0 bar (≥ Partial, no contradiction blocking Strong) with margin; it is among the best-evidenced obligations because its strongest evidence is a live, unmanufactured self-correction the assessor verified byte-for-byte against the git history.
