# IOA-O9 — Versioned knowledge (P9)

| Field | Value |
|---|---|
| obligation_id | O9 |
| principle | P9 — Knowledge is versioned |
| assessor | Independent auditor (0.9 Constitutional Readiness audit). Attestation: assessor did not build the EKB versioning, the Control bundle pin, or the release-validation gates; every finding below was re-derived from primary evidence (files, git objects, and live tool runs) by the assessor. |
| roadmap_baseline | Strong |
| maturity_verdict | **Strong** |
| determination | ≥ Partial: **yes** · Strong-blocker: **no** |

## clause_under_test (quoted)

> **P9 — Knowledge is versioned.**
> Engineering knowledge has identity, history, and lifecycle — never an ambient "current truth."
> *Ten-year test:* reproducibility over time is impossible without versioned knowledge.

Read from `/c/Dev/platform/PLATFORM_PRINCIPLES.md` (lines 138–141), document version 0.2.0, Status Ratified (Genesis).

## Evidence

### E1 — The Knowledge plane (EKB) is versioned and released with a manifest (real artifact)
- **artifact:** `/c/Dev/engineering_kb/VERSION` = `0.2.1`; `/c/Dev/engineering_kb/package.json` version `0.2.1`; `/c/Dev/engineering_kb/release/release-manifest.json` (schema_version 1.0.0, package_version 0.2.1, `content_digest: sha256:282a0a28…daac427`, content_file_count 46, `compatibility.canonical_decision_guide_type: decision_guide`, `consumer_pins: [package_version, git_commit, knowledge_object_schema_version, package_contract_version]`).
- **demonstration (real, not fixture):** Git tags `v0.2.0` and `v0.2.1` both resolve — `git rev-list -n1 v0.2.1` = `26750dca949041f24b155a40d9aee87c1d8bd420`, `v0.2.0` = `ce160741…`. Release notes exist for both (`RELEASE_NOTES_0.2.0.md`, `RELEASE_NOTES_0.2.1.md`), alongside `VERSIONING_POLICY.md`, `RELEASE_PROCESS.md`, `RELEASE_CHECKLIST.md`. Identity (name+version+digest), history (two tags + notes + decision history), and lifecycle (versioning policy, release process, release_status field) are all present on the real repository.
- **verified_by:** assessor read the files directly and resolved the tags against the real `/c/Dev/engineering_kb` git repo (HEAD `7a98226`, past v0.2.1).

### E2 — The bundled EKB is pinned in Control by exact version + commit + ontology (real artifact)
- **artifact:** `/c/Dev/ecf/vendor/engineering_kb/VERSION` (pin file: `version: 0.2.1`, `source_commit: 26750dca949041f24b155a40d9aee87c1d8bd420`, `source_tag: v0.2.1`, `status: released`); `/c/Dev/ecf/release/release-manifest.json` `bundled_ekb` block (bundle_version 0.2.1, manifest_package_version 0.2.1, source_commit 26750dc…, source_tag v0.2.1, `ontology: decision_guide`, package_contract_version 1.0); `/c/Dev/ecf/vendor/BUNDLE_RULES.md` (read-only bundle rule).
- **demonstration (real, not fixture):** The pinned `source_commit` `26750dc…` is exactly the commit of tag `v0.2.1` in the source repo (re-derived above) — the bundle is pinned to the released tag, not to "latest." The vendored `release/release-manifest.json` is byte-identical to the manifest at `git show v0.2.1:release/release-manifest.json` (both carry `git_commit 1e5ab30…`, `content_digest sha256:282a0a28…`), confirming the bundle faithfully reproduces the tagged release. This is the direct constitutional counter to "ambient current truth": Control consumes an immutable, commit-pinned version.
- **verified_by:** assessor read the pin and both manifests and compared the vendored manifest against the tag's manifest via git.

### E3 — Release-validation pin-integrity gates run and pass on the real release (real demonstration)
- **artifact:** `/c/Dev/ecf/scripts/validate-release.py` gates 4b (content_digest recompute) and 5 (bundled-EKB pin: version 0.2.1, 40-hex commit, ontology decision_guide, bundle==manifest version agreement).
- **demonstration (real, not fixture):** `python scripts/validate-release.py` on the real ecf release (package 0.8.3, `release_status: released`) — assessor ran it; gate 4b `PASS content_digest matches canonical content`, gate 5 all four checks `PASS` (version 0.2.1 / source_commit 26750dc… 40-hex / ontology decision_guide / bundle==manifest versions agree). The pin's shape and internal consistency are gate-enforced on the actual shipped manifest.
- **verified_by:** assessor executed the validator and read its output.

### E4 — The model↔projection drift gate (gate 9) runs, reuses the EKB engine's own checker, and fails closed
- **artifact:** `validate-release.py::gate_9_ekb_drift` (invokes `python vendor/engineering_kb/engine/ekb.py packages`, which calls `check_generated_packages` in `/c/Dev/engineering_kb/engine/ekb.py:951`); test `/c/Dev/ecf/scripts/test_validate_release_ekb_gate.py`.
- **demonstration:** Gate 9 runs in the real release validation and reports `PASS 9 bundled EKB model->projection in sync (no drift)`. Fail-closed behaviour is proven end-to-end: `python scripts/test_validate_release_ekb_gate.py` → 3/3 pass, including `test_gate_fails_on_injected_drift` (a stale generated package with a mismatched closure + a legacy type token is injected into `vendor/engineering_kb/generated/packages/` and gate 9 raises `9 EKB drift`), and `test_gate_recovers_after_cleanup`.
- **verified_by:** assessor ran both the validator and the gate test, and read `check_generated_packages`. **Caveat re-derived by assessor (see Open Item O9-a):** the real vendored EKB ships *no* `generated/packages/` directory (`package.json` `files` excludes `generated/`), so on the real bundle `ekb.py packages` returns "No generated packages directory; nothing to check" (exit 0). The real-release gate-9 PASS is therefore *vacuous* — the drift-catching behaviour is demonstrated only against an injected fixture, not against a real drifting projection in the shipped bundle.

## open_items

### O9-a — Gate 9's real-release pass is vacuous (no shipped projections to check)
- **classification:** named_gap_toward_strong
- **grounds:** The bundled EKB intentionally ships no generated projections (`package.json` `files` list omits `generated/`), so gate 9 has nothing to compare in the real release and passes trivially. The fail-closed machinery is proven end-to-end via `test_gate_fails_on_injected_drift`, so only a real drifting artifact is absent — reality-gated, machinery proven. This is O10-adjacent integrity, not the core O9 versioning claim (which stands on E1–E3). Additive within the architecture (ship or reference real projections and the gate exercises them). No frozen-contract or architecture break required.

### O9-b — No gate cross-verifies vendored bytes against the pinned commit's content digest
- **classification:** named_gap_toward_strong
- **grounds:** Gate 5 checks the pin fields' shape and mutual consistency but does not recompute the vendored EKB's `content_digest` (`282a0a28…`) against the bundle bytes or the pinned commit. The pin's provenance-to-content binding is asserted (manifest) but not re-derived by a Control-side gate. Purely additive integrity coverage; the durable version+commit+tag pin holds today (E2). No contradiction.

### O9-c — EKB's own release-manifest records release_status "draft" / git_tag null at the tagged release
- **classification:** named_gap_toward_strong
- **grounds:** `release/release-manifest.json` at tag `v0.2.1` still reads `release_status: "draft"` and `git_tag: null`, while the Control pin and the git tag treat v0.2.1 as released. The authoritative lifecycle marker (the git tag `v0.2.1`) exists and resolves, so version identity/history is intact; the manifest's status field simply lags the tag. Mild P2 tension, additive fix (stamp released status/tag into the manifest post-tag). Not a contradiction — the tag, not the field, is the lifecycle authority.

## determination

- **≥ Partial on real evidence?** Yes. The EKB is a real, versioned, released artifact with identity, history, and lifecycle (E1); Control consumes it pinned by exact version + commit + ontology, faithful to the tag (E2); and pin-integrity + content-digest gates pass on the real ecf release (E3). This is demonstrated on genuine artifacts, not fixtures.
- **Strong verdict:** The full P9 surface — identity, history, lifecycle, and the anti-"ambient current truth" invariant — is demonstrated broadly on real artifacts, with the exact-commit pin gate-enforced in a real release and a fail-closed drift gate wired into the pipeline. Every gap found is named.
- **Any Strong-blocker?** No. All three open items are named gaps toward Strong: each is purely additive within the ratified architecture (more integrity coverage, a manifest-field refresh, a real projection for the drift gate to bite on), none requires breaking a frozen contract or changing the architecture, and none falsifies the Partial claim — the pin, the tags, and the digest all re-derive cleanly. Applying §5(a)/(b): neither branch is met.
