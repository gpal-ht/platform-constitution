# IOA-O5 — Independent Obligation Assessment

| Field | Value |
|---|---|
| obligation_id | O5 — Independent validation: separation of generation and validation |
| principle | P6 (Validation is independent of generation) — under CHALLENGEABLE |
| assessor | Independent auditor (0.9 Constitutional Readiness audit). Attestation: the assessor did NOT build WF022, the CPV contract, or the reasoning/transformation workflows; every finding below was re-derived from primary evidence (code run, records re-hashed) rather than from builder release notes. |
| roadmap baseline | Strong (deepened at 0.8 to universal + cross-plane) |

## clause_under_test (quoted)

> **P6 — Validation is independent of generation.**
> The actor that produces a decision cannot be the sole actor that ratifies it — regardless
> of whether that actor is human or machine.
> *Ten-year test:* separation of production from verification is a durable engineering invariant.

Audit-method binding (PROPOSAL_09 §3, primary-evidence rule): the assessor "reads the artifacts,
code, tests, and run records directly and re-derives the verdict … does not accept 'the release
notes say it passes' as evidence — that is precisely the generation==validation collapse the
platform forbids (P6)." O5 is therefore also the principle the audit method itself invokes.

## evidence

### E1 — WF022 universal independent-validation invariant (fail-closed)
- **artifact:** `C:\Dev\ecf\tools\workflow_validator\validate_workflow.py` (check `WF022`,
  lines 923–989; helpers `parse_validates` 209–230, `parse_consequential` 233–247,
  `_consequential_producers` 903–920); tests
  `C:\Dev\ecf\tools\workflow_validator\tests\test_validate_workflow.py` (class
  `TestWF022IndependentValidation`, 95–137); negative fixtures
  `C:\Dev\ecf\acceptance_tests\fixtures\workflows\wf022_no_validate_task.md`,
  `...\wf022_self_validation.md`.
- **demonstration (real + fail-closed):** the invariant is category-independent: for every
  consequential producer (bound output under `reports/` that is not a trace/manifest/completion
  leaf, or a task named in an explicit `consequential:` block) it requires a distinct validation
  task V that (a) is not the producer, (b) depends transitively on the producer, (c) binds a
  C13-routed verdict envelope (leaf contains `validation`), and (d) names the producer in the
  machine-readable `validates:` block. Demonstrated passing on BOTH released workflows —
  `WF-REASON-0001` (`validates: TASK-VALIDATE-0001 -> TASK-PRODUCE-0001`) and `WF-TRANSFORM-0001`
  (`validates: TASK-VALIDATE-0002 -> TASK-CANON-0001`).
- **verified_by:** I ran the validator directly against both negative fixtures (not just the
  test wrapper). `wf022_no_validate_task.md` → `Result: INVALID`, `[FAIL] WF022 … consequential
  producer TASK-PRODUCE-0001 … declares no validation task`. `wf022_self_validation.md` →
  `Result: INVALID`, `[FAIL] WF022 … TASK-PRODUCE-0001 validates its own output (generator ==
  validator)`. I also ran `TestWF022IndependentValidation` (6 tests) → all pass. Fail-closed
  confirmed: a workflow producing a consequential artifact with no independent validate task, and
  a workflow whose producer validates itself, are BOTH rejected.

### E2 — Cross-Plane Validation record CPV-project-0001 (structural actor distinctness on real bytes)
- **artifact:** record `C:\Dev\ecf\canonical\decisions\EDR-0002\crossplane\CPV-project-0001.yaml`;
  contract `C:\Dev\ecf\tools\crossplane_validation\cpv_record.py`
  (`check_actor_distinctness` 228–285) and `...\validate_cpv.py`
  (`validate_cpv_record` 95–162, mechanical digest re-derivation `_rederive` 71–92,
  `gate_standing` 181–202); tests `...\tests\test_crossplane_validation.py`.
- **demonstration (real, not fixture):** the record binds a control-plane source
  (`EDR-0002.md`) to its project-plane projection (`projection-EDR-0002-cs.md`) by sha256,
  naming `generator_actor` = `ecf-control-plane-projection-generator` (`control:generator`) and
  `validator_actor` = `Founder (Genesis)` (`project:reviewer`), fidelity `faithful`.
- **verified_by:** I ran `validate_cpv_record(...)` against the real record with base_dir at the
  repo root. Result: `valid=True`, `fidelity=faithful`, generator/validator actor ids distinct,
  both digests **re-derived from the bytes on disk** to `4b8f1de3addda224…` (I independently
  re-hashed both files — they match the pinned digests), `gate_standing` →
  `standing_eligible=True`, `grants_acceptance=False` (structurally, `init=False`). I confirmed
  `generator == validator` is **unrepresentable as a pass by construction**: `check_actor_distinctness`
  rejects, fail-closed, (a) equal `actor_id`, (b) equal `plane_role`, (c) a validator whose
  function is not `reviewer`, and (d) a validator sitting in the source plane's generating role;
  `confers_standing: true` is likewise unrepresentable (shape check). All 24 crossplane tests pass,
  including the six actor-distinctness rejections and the colluding-`faithful`-over-mismatched-bytes
  rejection.

### E3 — Independent report validation in real reasoning runs (WR-0001 / WR-0004)
- **artifact:** `C:\Dev\ecf\canonical\decisions\EDR-0002\evidence\recommendation-report-validation.yaml`
  (run `RUN-REASON-20260716-0002`, WR-0001, report ERR-0001) and
  `C:\Dev\ecf\canonical\decisions\EDR-0003\evidence\recommendation-report-validation.yaml`
  (run `RUN-REASON-20260717-0003`, WR-0004, report ERR-0004); real run output
  `C:\Dev\ecf\runtime\runs\RUN-REASON-20260716-0002\task_outputs\recommendation-report-validation.yaml`.
- **demonstration (real, not fixture):** each validation record is emitted by
  `TASK-VALIDATE-0001`, validating a report produced by a distinct task (`TASK-PRODUCE-0001`),
  running 11 closed-field checks (contract completeness, provenance, evidence-vs-assumptions,
  approval-claims, no-unsupported-facts, …), `overall.result=passed`, `report_modified=false`.
- **verified_by:** I diffed the EDR-0002 evidence copy against the actual runtime run output
  (`RUN-REASON-20260716-0002/task_outputs/...`) — content-identical, so the canonical evidence is
  a faithful copy of a real run, not a hand-authored fixture. The validator task
  (`TASK-VALIDATE-0001`) is structurally distinct from the producer (`TASK-PRODUCE-0001`); the
  `validates:` block and transitive-dependency closure (I confirmed `TASK-PRODUCE-0001 ∈
  closure[TASK-VALIDATE-0001]`) tie them. Two independent real runs, not one.

## maturity_verdict

**Strong** — with one named gap toward its fullest expression (E-gap-1 below).

Grounds: the mechanism is (i) **universal** — WF022 lifts generation≠validation from per-workflow
convention to a category-independent, fail-closed platform invariant, demonstrated rejecting both a
no-validate-task and a self-validating-producer workflow, and passing on every released workflow;
(ii) **cross-plane** — the CPV contract makes generator==validator structurally unrepresentable as a
pass and mechanically re-derives digests, demonstrated on a real EDR-0002 projection with a
genuinely distinct human validator (Founder as `project:reviewer`); and (iii) **demonstrated on real
artifacts**, not fixtures — the CPV over real projection bytes and two real reasoning-run report
validations (WR-0001, WR-0004). No unnamed consequential gap; every gap below is named.

## open_items

**E-gap-1 — Actor independence within a single-executor reasoning run.**
- description: On the reasoning plane, WF022 and the report-validation records enforce and
  demonstrate separation of the validating **task** from the generating **task**, but within a
  single-executor run the same machine actor executes both `TASK-PRODUCE-0001` and
  `TASK-VALIDATE-0001`. WF022's own docstring records this honestly (O5-3): it "checks the
  separation of the validating task from the generating task, not actor independence … explicitly
  OUT of the 0.8 bar." Genuine, distinct-**actor** independence is demonstrated only on the
  cross-plane CPV path (Founder), not yet within reasoning runs.
- classification: **named_gap_toward_strong**
- grounds: The Partial/Strong claim stands on real evidence (re-derived, not asserted). Reaching
  full per-actor independence on the reasoning plane is **purely additive within the ratified
  architecture** — the architecture already supports and demonstrates a distinct validating actor
  (the CPV path proves distinct actors are representable and gate-enforced); no frozen contract or
  architecture break is required, only extending the distinct-actor discipline into the
  single-executor reasoning run. It is honestly named in-code as O5-3, satisfying P2.

**E-gap-2 — CPV projection is byte-identical to its source (verbatim projection).**
- description: `projection-EDR-0002-cs.md` (8436 bytes) is byte-identical to `EDR-0002.md`
  (8436 bytes; both sha256 `4b8f1de3…`). The `faithful` fidelity verdict is therefore satisfied
  over a verbatim copy; the cross-plane demonstration exercises the independence/gate machinery on
  a degenerate (identity) projection rather than a transformed one.
- classification: **named_gap_toward_strong**
- grounds: Does not falsify any claim — the digest re-derivation, actor-distinctness, and standing
  gate all genuinely executed and passed, and generator/validator independence is orthogonal to how
  much the projection transforms the source. Broadening to a non-trivial (transformed) projection is
  additive coverage within the existing contract.

## determination

- **≥ Partial on real evidence:** **YES.** The CPV over real EDR-0002 projection bytes and the two
  real reasoning-run report validations (WR-0001, WR-0004) are genuine artifacts re-derived by the
  assessor, not fixtures; the mechanism is built and demonstrated; all gaps are named; no
  architectural contradiction was found.
- **Any Strong-blocker:** **NO.** The Partial claim is not falsified (I re-derived every element).
  Reaching the fullest Strong (per-actor independence inside single-executor reasoning runs) is
  additive within the ratified architecture — no frozen-contract or architecture break is required,
  and the CPV path already demonstrates distinct actors are supported and gated. Both open items are
  named gaps toward Strong, not contradictions blocking Strong.
- **Verdict:** **Strong**; O5 clears the 1.0 bar (≥ Partial, no Strong-blocker).
