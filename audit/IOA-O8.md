# IOA-O8 — Provenance (P8)

| Field | Value |
|---|---|
| obligation_id | O8 |
| principle | P8 — Provenance is mandatory (pillar: Reproducible) |
| assessor | Independent auditor (0.9 Constitutional Readiness audit). Attestation: assessor ≠ builder — I did not author `tools/crossplane_provenance/*`, the durability rule, or the EDR-0002 manifest/walk; every finding below was re-derived from primary evidence I read and ran myself. |
| roadmap baseline | Strong (deepened at 0.8 to cross-plane) |
| maturity_verdict | **Partial** |
| determination | ≥ Partial? **YES**  ·  Strong-blocker? **NO** |

## clause_under_test (quoted)

> **P8 — Provenance is mandatory.**
> Every consequential artifact can be traced to the inputs, knowledge, and process that
> produced it.
> *Ten-year test:* reconstruction is impossible without an unbroken chain.

Descends from the Root pillar **Reproducible**: "the decision can be reconstructed and its
basis re-evaluated." The 0.8 deepening extends the traceability chain across all three planes:
decision → Control evidence bundle → Knowledge EKB pin → Project projection.

## Evidence

### E1 — Cross-plane manifest + verifying walker (the mechanism)
- **artifact:**
  - `/c/Dev/ecf/tools/crossplane_provenance/manifest.py` (schema, builder, fail-closed structural validation; closed field set)
  - `/c/Dev/ecf/tools/crossplane_provenance/walker.py` (READ-ONLY resolver; re-derives and re-verifies every retained hop)
  - `/c/Dev/ecf/tools/reproducibility/durability.py` (two-tier cross-plane durability rule `check_crossplane_ref`, additive over the 0.7 FD-2 rule)
  - `/c/Dev/ecf/tools/artifact_fingerprint/fingerprint.py` (`sha256_normalized` — additive EOL-independent LF content digest; raw `sha256_file` untouched)
- **demonstration:** `python -m pytest tools/crossplane_provenance/tests/test_walker.py -q` → **25 passed**. (Tests support built-ness, not Partial by themselves — §2.)
- **verified_by:** I read all four modules. The walker resolves the far file, checks git `blob_id` (immutable object identity) AND an LF-normalized `content_sha256`; a present-but-mismatched retained hop → BROKEN → whole walk fails; an unreachable Tier-2 far file → recorded `unbound` (not dropped, not passed); a walk is `complete` only with zero broken AND zero unbound. The field set is closed (a typo'd pin key is rejected). Verification is derived on read, never trusted from the record.

### E2 — The REAL walk on EDR-0002 (Partial-qualifying real artifact)
- **artifact:** `/c/Dev/ecf/canonical/decisions/EDR-0002/crossplane/crossplane-manifest.yaml` + `walk-result.json` (a real canonical decision, not a fixture).
- **demonstration + verified_by (I re-derived every hop from primary bytes):**
  - Hop 1 `control_evidence_bundle` (Tier-1): `sha256(canonical/decisions/EDR-0002/evidence-manifest.yaml)` = `20e5a6b8…e6ba` — **matches** the pin.
  - Hop 2 `knowledge_ekb_pin` (Tier-1): `sha256(vendor/engineering_kb/release/release-manifest.json)` = `3654dd24…d0dcd` — **matches** the pin.
  - Hop 3 `project_projection` (Tier-2, cross-repo into context_switcher): blob `bf58ebd…` **exists** in the context_switcher object store; commit `6afb386…` **exists**; `git rev-parse 6afb386:engineering/canonical-decisions/EDR-0002/EDR-0002.md` → `bf58ebd…` (**pinned blob reachable at pinned path@commit**); LF-normalized `content_sha256` of the blob = `4b8f1de3…9b2d` — **matches** the pin.
  - I then **reproduced the whole walk end-to-end**: materialized the pinned blob at the cited relative path, ran `walker.py … --verify` → `status: verified, complete: true, verified: [all 3 hops], broken: [], unbound: []` — identical to the recorded `walk-result.json` (**3/3 hops, each digest-verified**).
  - **Adversarial (fail-closed):** appended one byte to the far file and re-ran → `WALK REFUSED … project_projection is BROKEN: blob_id … != pinned …`, **exit 1**. The walk does not pass on altered bytes.

### E3 — Two-tier durability + additive `sha256_normalized`, on a permanent record
- **artifact:** `/c/Dev/ecf/information_closures/durable-pins-CLOSURE-0001.yaml` (a sibling record that Tier-2-durably re-pins the four cross-repo citations CLOSURE-0001 — a write-once P14 record — had cited by bare branch/commit only).
- **demonstration + verified_by:** I spot-checked citation 4 (ADR-0007) against the context_switcher object store without trusting the record: blob `b7de071…` exists; `git rev-parse 1dcf298:decisions/ADR-0007-optional-ecf-integration.md` → `b7de071…` (reachable at pinned path@commit); LF-normalized content digest = `fa240623…8f94` — **matches** the pin. The bare foreign-branch citation (a MORTAL path — the far repo rewrites/gc's its branches) is thereby anchored to immutable content. The durability rule's negatives are real: a cross-repo ref with no content anchor, a bare `runtime/` ref, and a content pin with no declared `normalization` are each fail-closed rejected in `check_crossplane_ref`.

## open_items

### OI-1 — Walker resolves WORKING-TREE bytes → off-branch consumer checkout reports Project hop `unbound`
- **classification:** **named_gap_toward_strong** (P13 deferred refinement).
- **grounds (re-derived live):** The live `/c/Dev/context_switcher` checkout sits on the parked branch `feature/work-engine-project-registry`, whose working tree does **not** contain `EDR-0002.md`. I ran the real walk against that live root: the Project hop resolved to `unbound`, `status: gapped`, `complete: false`, **exit 0** — the honest-gap path (cannot prove → recorded unbound; never silently dropped, never falsely passed). This is **not** a durability failure: the durable pin holds — I confirmed the pinned blob `bf58ebd` is reachable from the pinned commit `6afb386` at the pinned path in the object store, and its LF-normalized content digest matches. Reaching Strong requires only changing the walker's resolution strategy from working-tree `is_file()` to git-object resolution at the pinned commit (`git cat-file`), which the manifest schema already carries (`commit` + `blob_id` are pinned). That is **purely additive within the ratified architecture** — no frozen-contract break, and it does **not** falsify the Partial claim (the real EDR-0002 walk verifies 3/3 when the projection bytes are present, which I reproduced). Fails neither limb of the §5 blocker test.

### OI-2 — Cross-plane manifest + walk demonstrated on 1 of 3 canonical decisions
- **classification:** **named_gap_toward_strong** (additive coverage).
- **grounds:** Canonical decisions are EDR-0001, EDR-0002, EDR-0003; only EDR-0002 carries a `crossplane/` manifest and a real walk (confirmed by directory scan — the single `crossplane-manifest.yaml` in the repo). The mechanism holds on the one real decision it was exercised on; extending to the remaining decisions is minting more manifests within the existing schema — additive, no architecture change. This is the breadth gap that separates the current **Partial** from Strong ("every decision, demonstrated broadly").

## Rationale for the verdict

- **≥ Partial (real, not fixture):** met. The mechanism is implemented and demonstrated on a genuine artifact — EDR-0002, a real canonical decision — with all three cross-plane hops digest-verified by my own re-derivation, the complete walk reproduced, and fail-closed BROKEN confirmed on tamper. Both gaps to Strong are named honestly (OI-1, OI-2).
- **Not Strong:** the clause's full surface is "every consequential decision, demonstrated broadly." Cross-plane provenance is demonstrated on one decision (OI-2), and a consumer checkout on a different branch cannot yet complete the walk (OI-1). Both are coverage/refinement gaps, not contradictions.
- **No architectural contradiction preventing Strong:** the frozen contract (manifest schema with `commit` + `blob_id` + normalized `content_sha256`; two-tier durability) already carries everything the deferred git-object walk and the additional manifests need. Neither open item requires breaking a contract or changing the architecture, and neither falsifies the Partial claim.

**determination:** ≥ Partial? **YES.**  Any Strong-blocker? **NO.**  Meets the per-obligation 1.0 bar.
