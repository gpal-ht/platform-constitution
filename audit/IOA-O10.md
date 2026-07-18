# IOA-O10 — Engineering-model synchronization: artifacts stay in sync with their authoritative model

| Field | Value |
|---|---|
| obligation_id | O10 |
| principle | P10 — Engineering artifacts remain synchronized with their authoritative engineering model (pillar: Reproducible) |
| assessor | Independent auditor (0.9 Constitutional Readiness audit). Attestation: assessor did NOT build ecf-version.yaml, the release-manifest builder, the validate-release gates, the EKB engine, or the cross-repo bundling; every finding below was re-derived from primary evidence (code and artifacts read directly; the validator, the drift check, and the fixture test executed by the assessor). |
| roadmap_baseline | Partial (0.4) |
| claimed | Partial (full model contract + cross-repo projection noted as the gap toward Strong) |

## clause_under_test (quoted)

> **P10 — Engineering artifacts remain synchronized with their authoritative engineering
> model.**
> The forcing function is execution, not discipline: when an artifact drifts from its
> authoritative model, execution breaks. *(Current governance mechanism: artifacts rendered
> from the model. The invariant is synchronization, not any particular mechanism.)*

Operative test for this audit: (a) does the authoritative engineering model carry real
version identity + a compatibility/migration contract; (b) is a drift between a projection and
that model a **fail-closed, execution-forced** failure (not a discipline reminder); and (c) has
that been demonstrated on a **real** release against the **real** bundled model — not only on a
fixture?

## Evidence list

Each entry: artifact + demonstration (real, not fixture) + how the assessor re-derived it.

1. **Model version identity (the authoritative-model contract).**
   - artifact: `C:\Dev\ecf\ecf-version.yaml` (ECF framework identity: `component`, `version v0.1`, `schema_version 0.1.0`, `commit_policy best_effort` — declared as the ONLY authoritative ECF version source for tooling); `C:\Dev\ecf\vendor\engineering_kb\VERSION` (EKB model: `version 0.2.1`, `source_commit`, `source_tag v0.2.1`, `status released`); `C:\Dev\ecf\vendor\engineering_kb\release\release-manifest.json` `compatibility` — `knowledge_object_schema_version 1.0`, `package_contract_version 1.0`, `canonical_decision_guide_type decision_guide` (ontology/identity), `engine_generator_version 0.2.0`, and an explicit `consumer_pins` list (`package_version`, `git_commit`, `knowledge_object_schema_version`, `package_contract_version`).
   - demonstration (REAL): these are the real identity files of the real bundled EKB 0.2.1, not fixtures. The model contract dimensions the roadmap gap named — version, identity, compatibility, migration — are all present as real artifacts (migration: `vendor\engineering_kb\migrations\MIGRATION-0001…`, `MIGRATION-0002…`, plus the engine's `LEGACY_TYPES` pre-migration token detector, `engine\ekb.py:74,561,980`).
   - verified_by: read every file; cross-checked the manifest's `bundled_ekb` block against `VERSION` and the EKB manifest.

2. **The pin — model synchronized into ECF by identity (gate 5, the enforced sync guarantee).**
   - artifact: `C:\Dev\ecf\scripts\build-release-manifest.py` `bundled_ekb()` (records package_name, bundle_version, manifest_package_version, source_commit, source_tag, ontology, package_contract_version); `C:\Dev\ecf\scripts\validate-release.py` `gate_5` (asserts EKB version `0.2.1`, 40-hex source_commit, ontology `decision_guide`, and bundle/manifest version agreement).
   - demonstration (REAL): assessor ran `python scripts/validate-release.py` on the real 0.8.3 release. Gate 5 **passed** against the real bundled EKB — `bundle_version 0.2.1`, `source_commit 26750dca949041f24b155a40d9aee87c1d8bd420`, `ontology decision_guide`, bundle/manifest agree. This is a real, execution-enforced synchronization check: the ECF release cannot ship unless its recorded model identity matches the real bundled model.
   - verified_by: assessor executed the validator and read gate 5; confirmed the manifest `bundled_ekb` values against the real `VERSION` file.

3. **Cross-repo projection — the model pinned across all three repos by identity.**
   - artifact: EKB → ECF: `vendor\engineering_kb\VERSION` (+ manifest) inside ecf. ECF+EKB → CS: `C:\Dev\context_switcher\vendor\ecf\VERSION` (pins ecf `0.2.0` @ commit + tag AND re-declares `ekb_source`/`ekb_version 0.2.0`/`ekb_commit`/`ekb_tag`) and `C:\Dev\context_switcher\vendor\ecf\vendor\engineering_kb\VERSION` (the transitively-bundled EKB, `0.2.0` @ `ce160741…`).
   - demonstration (REAL): a real durable-pin chain across repos — each hop carries version + commit + tag + ontology. A real projected artifact exists: `C:\Dev\context_switcher\runtime\work_requests\WR-0001\engineering-knowledge-package.md`, a genuine EKP rendered from the graph (`generated_from DG-ARCH-0001`, `retrieved_objects` closure of 8 objects, `generated_by TASK-RETRIEVE-0002`, `ekb_commit`). This is the model actually projected into a consumer artifact.
   - verified_by: read all three VERSION files and the CS EKP frontmatter. Noted the expected version skew (CS pins the older ECF 0.2.0/EKB 0.2.0; ecf HEAD bundles EKB 0.2.1) — pins are durable, not "latest".

4. **The DRIFT forcing function (gate 9 / P10) — fail-closed mechanism, but demonstrated only on a fixture; VACUOUS on the real release.**
   - artifact: `C:\Dev\ecf\scripts\validate-release.py` `gate_9_ekb_drift` → shells `python vendor/engineering_kb/engine/ekb.py packages`, which calls `check_generated_packages` (`engine\ekb.py:951-1000`): compares each generated package's declared `retrieved_objects` closure against the live `retrieve()` closure of the graph and flags stale/legacy-token packages; non-zero exit fails the release. Fixture test: `C:\Dev\ecf\scripts\test_validate_release_ekb_gate.py`.
   - demonstration — mechanism proven on FIXTURE ONLY: assessor ran the test → `3 passed`, including `test_gate_fails_on_injected_drift` (a stale package with a mismatched closure + legacy `engineering_decision` token injected into `vendor/engineering_kb/generated/packages/` makes gate 9 fail closed). The fail-closed behaviour is real and works.
   - demonstration — real release is VACUOUS (the adversarial finding): the assessor ran the underlying check directly — `python vendor/engineering_kb/engine/ekb.py packages` → **"No generated packages directory; nothing to check." exit 0**. In the real 0.8.3 release gate 9 "PASSED", but it verified an **empty set**: `generated/` is git-ignored in the vendored EKB (`vendor\engineering_kb\.gitignore` line 8) and is in the manifest builder's `EXCLUDE_PARTS`, so generated projections are transient, non-canonical, and **never bundled**. `git ls-files vendor/engineering_kb/generated/` → empty. The one real projection that does exist (evidence 3, the CS runtime EKP) lives in `runtime/` (gitignored) and is checked by **no** drift gate; it even declares a stale `ekb_version: v0.1-local`.
   - verified_by: assessor executed both the validator and the raw engine command, read `cmd_packages` (the `if not GENERATED_PACKAGES_DIR.exists(): return 0` vacuous-pass branch), the `.gitignore`, and `git ls-files`.

5. **Mechanism built (tests).** `test_validate_release_ekb_gate.py` → 3 passed. Supports Emerging / Strong-breadth; by §2 it does not by itself lift O10 to Partial — the real pin (evidence 2) and the real cross-repo projection (evidence 3) do.

## maturity_verdict

**Partial.**

O10 clears Partial on **real, non-fixture** evidence — but not via the gate the framing points at. The authoritative model carries real version + compatibility + migration + identity contract (evidence 1); that model is **synchronized into the ECF release by an execution-enforced identity pin** that the assessor watched pass on the real 0.8.3 release (gate 5, evidence 2); and the model is **really projected across all three repos** by durable version+commit+tag+ontology pins, with a real rendered EKP in the consumer (evidence 3). That is genuine model→artifact synchronization, demonstrated on real artifacts.

What it does **not** clear, and where the roadmap's "Partial" is thinner than it reads: the P10 **drift forcing function** (gate 9) — the mechanism whose whole job is "when an artifact drifts from its model, execution breaks" — passes **vacuously** on every real ECF release, because generated projections are by design transient/git-ignored/never-bundled, so there is never a projection in the bundle for gate 9 to check. Its fail-closed behaviour is real but **fixture-only** (evidence 4). Honesty note (P2): had O10 rested solely on gate 9, the honest verdict would be **Emerging** (mechanism + fixtures, no real projection ever checked). It rests instead on the real pin + real cross-repo projection, which is what lifts it to Partial.

## open_items

1. **Gate 9 is structurally vacuous on the real release artifact.** In the shipped 0.8.3 release gate 9 checked zero projections ("No generated packages directory; nothing to check") because generated packages are git-ignored and never bundled. The drift forcing function, as wired, cannot fire on a real ECF release; its fail-closed path is proven only by an injected-fixture test.
   - classification: **named_gap_toward_strong**
   - grounds: additive within the ratified architecture, not a frozen-contract break. Real synchronization IS enforced on the release by the identity pin (gate 5, evidence 2), so the ≥Partial claim does not rest on gate 9 and is not falsified. Reaching Strong requires making a real projection surface drift-checkable — either extend gate 9 to a projection that actually ships (e.g. the canonical `decision_guides` rendered from the model, or the consumer's rendered EKP class), or bundle a real generated projection. Neither breaks a contract. This is flagged prominently because the forcing function being a structural no-op on the real artifact is a genuine weakness, not a cosmetic one — but it is closable by adding coverage.

2. **Cross-repo projection is pinned by identity but not drift-verified end-to-end.** The real consumer projection (CS `runtime\...\engineering-knowledge-package.md`, `ekb_version v0.1-local`) is synchronized to its source only by the durable pin; no gate re-derives its declared closure against the pinned graph, and its declared ekb_version is stale relative to the bundled EKB.
   - classification: **named_gap_toward_strong**
   - grounds: additive breadth. The pin (version+commit+tag+ontology) is a real synchronization guarantee across repos; extending the drift check to the consumer-side projection surface is coverage, not an architecture change.

3. **Compatibility contract is an exact pin, not a declared range.** Gate 5 hard-codes EKB `0.2.1`; `consumer_pins` are enumerated but there is no compatibility range / version negotiation, so every model bump requires a code edit to the gate.
   - classification: **named_gap_toward_strong**
   - grounds: additive. Exact-pin synchronization is stricter (safer) than a range and does not contradict the architecture; a declared-range compatibility contract is a refinement toward Strong.

4. **Migration path present but not demonstrated end-to-end.** `migrations/` (two records) and the engine's `LEGACY_TYPES` legacy-token detector exist and the token detector is exercised by the gate-9 fixture, but no real model migration invalidating a real projection has been demonstrated.
   - classification: **named_gap_toward_strong**
   - grounds: reality-gated + additive. The detection machinery is built and fixture-proven; only a real migration event is absent.

No open item is a contradiction blocking Strong. The vacuity of gate 9 (item 1) was tested against §5: it does **not** falsify the Partial claim, because the Partial claim stands on the real identity pin and real cross-repo projection, not on gate 9; and closing it is additive (add a real projection surface to the drift check), requiring no frozen-contract or architecture break.

## determination

- maturity_verdict: **Partial**
- ≥ Partial on real evidence? **YES** — real model version/compat/migration/identity contract, a real execution-enforced identity pin verified passing on the real 0.8.3 release, and a real cross-repo projection chain with a real rendered EKP.
- Any Strong-blocker (contradiction blocking Strong / falsified Partial claim)? **NO** — all four open items are named gaps toward Strong. The sharpest (gate 9 vacuous on the real release) is a real weakness but additive to close, and the ≥Partial verdict does not depend on it.
