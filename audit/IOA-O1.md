# IOA-O1 — Intelligibility: decisions carry recoverable judgment

| Field | Value |
|---|---|
| obligation_id | O1 |
| principle | P1 — Engineering judgment precedes engineering artifacts (pillar: INTELLIGIBLE; Root: "the decision can be understood") |
| assessor | independent 0.9 audit — did not build this |
| roadmap baseline | 0.2.0 Partial; claimed deepened at 0.8 via JAR/JAL |
| maturity_verdict | **Partial** |
| determination | ≥ Partial? **YES** · any Strong-blocker? **NO** |

## clause_under_test (quoted)

P1, PLATFORM_PRINCIPLES.md: "**Engineering judgment precedes engineering artifacts.** The
artifact is never primary; the judgment that produced it is. Reasoning, proofs, simulations,
symbolic planning, and model checking are all forms of judgment, and none may be skipped on the
way to an artifact." Serving the Root pillar INTELLIGIBLE: "the decision can be understood." O1
restates this as: a canonical decision must carry its producing judgment in a form a reader can
recover.

## evidence

Each entry is artifact + demonstration + checker (independently re-derived from primary bytes).

### E1 — The JAR is digest-bound to the REAL decision EDR-0002 and to its judgment

- **artifact**: `C:\Dev\ecf\canonical\decisions\EDR-0002\judgment-attachment.yaml`
  (`judgment_attachment_record` JAR-EDR-0002-0001), file digest
  `sha256 ab0f471920883aeb290098e2905a3b3962938d52fc8bd40a04305cb3fb052790`. It pins
  `decision_record_sha256 = 4b8f1de3addda22498c9af30a6821bc6c05edbc0a5e2dd484610ebd701439b2d`
  and nine `carried_judgment` elements (engineering-forces, decision-options,
  engineering-alternatives, engineering-trade-offs, engineering-risks, engineering-confidence,
  engineering-recommendation, missing-information, trace) each with its own sha256, plus 14
  anchored task_outputs, 18 provenance records, and an EKB pin (engineering_kb 0.2.1,
  `282a0a28…`).
- **demonstration (real, not fixture)**: EDR-0002 is a real canonical decision ("Should
  Repository Integration become a first-class subsystem within Context Switcher?"). I re-hashed
  the real bytes.
- **verified_by**: `sha256sum EDR-0002.md` → `4b8f1de3…b2d`, byte-identical to the JAR's
  `decision_record_sha256`. All nine `judgment/*.yaml|.md` files re-hash to exactly the digests
  the JAR carries (engineering-forces `598767cd…`, decision-options `185b1454…`, alternatives
  `455569…`, trade-offs `4a71a7…`, risks `7588f4…`, confidence `1736b9…`, recommendation
  `7829d9…`, missing-information `f71b9d…`, trace `e9ae16…` — every one matched). The JAR file
  itself re-hashes to `ab0f4719…790`, matching the JAL back-reference.

### E2 — The judgment subdir holds genuinely recoverable reasoning (not a stub)

- **artifact**: `C:\Dev\ecf\canonical\decisions\EDR-0002\judgment\` — forces, options,
  alternatives, trade-offs, risks, recommendation, confidence, missing-information, trace.md.
- **demonstration (real)**: `resolve.py element EDR-0002 engineering-recommendation` recovered
  the full element from the durable JAR copy alone (no runtime/ access) — real content: task
  `TASK-DECIDE-0002`, run `RUN-REASON-20260716-0002`, recommendation outcome
  `gather_additional_evidence`, selected option `OPT-0003`.
- **verified_by**: ran the tool against `--repo-root /c/Dev/ecf`; it re-hashes the copy before
  returning and returned real decision content.

### E3 — Cross-plane recovery: a Project-plane reader recovers the Control judgment (recovered=true)

- **artifact**: real committed projection in the Project plane —
  `context_switcher` branch `develop`,
  `engineering/canonical-decisions/EDR-0002/projection-jal.yaml`
  (`judgment_attachment_link`), alongside a byte-identical `EDR-0002.md` projection
  (`sha256 4b8f1de3…b2d`, identical to the Control source) and a README stating the projection
  is read-only and confers no standing. Introduced by commit `6afb386` (merge `22cb36b`), which
  is an ancestor of `develop`.
- **demonstration (real, not fixture)**: extracted the real committed JAL
  (`git show develop:…/projection-jal.yaml`) and ran
  `python -m tools.judgment_attachment.resolve --repo-root /c/Dev/ecf recover <jal>`. Result:
  `recovered: true`, walking `EDR-0002 → JAR-EDR-0002-0001 → source run
  RUN-REASON-20260716-0002 (9 carried elements) → EKB pin 0.2.1 (282a0a28)`, exit 0. It also
  surfaces the O12 seam honestly (`reproducibility_state_ref: RSTATE-EDR-0002-0001`,
  `reconstruction_required: false`) — recovery of judgment is delivered independently of
  reproducibility, consistent with O1 being O12-independent.
- **verified_by**: I re-derived every hop the tool checks — projected `EDR-0002.md` digest,
  JAR digest, carried-element digests, and JAL↔JAR `knowledge_pin` identity — all match. The
  JAL is the only thing the Project plane carries; the judgment itself stays governed in
  Control (P7 standing preserved).

### E4 — The mechanism is fail-closed, not a rubber stamp

- **demonstration (real)**: flipping a single hex character in the real JAL's
  `edr_record_sha256` produced `RECOVERY REFUSED: EDR hop … re-hashes to …b2d, JAL pins …b2e
  (fail closed)`, exit 1. `verify_carried`, `_jar_intact_digest`, and the JAL shape gate
  (conclusion-only projections refuse, O1-5) enforce the same discipline in code
  (`resolve.py`).
- **checker (mechanism health)**: `tools/judgment_attachment/tests/` — 36 passed. (Tests
  buttress Emerging/Strong-breadth; the Partial lift rests on E1–E3, which are real artifacts.)

## open_items

1. **description**: Judgment attachment is demonstrated on 1 of 3 real canonical decisions.
   EDR-0002 carries a JAR; EDR-0001 (superseded) and EDR-0003 (current) carry none.
   - **classification**: named_gap_toward_strong
   - **grounds**: Purely additive within the ratified architecture — attach JARs to the other
     real EDRs; no frozen contract or architecture changes. The `jar_chain` walk already
     records a missing JAR as an honest `jar: null` gap ("recorded, not guessed") rather than
     breaking, so the mechanism tolerates incremental coverage. Strong requires "every
     decision"; today's real surface coverage is partial.

2. **description**: The JAR supersession chain (`supersedes_judgment` edge / O1-4 negatives) is
   proven only on fixtures — no real dual-JAR supersession exists, so `jar_chain EDR-0002`
   traverses just one real JAR.
   - **classification**: named_gap_toward_strong
   - **grounds**: Additive and reality-gated on a second real JAR entering a supersession
     chain; the enforcement code and its tests exist and pass, and the single-JAR real walk
     succeeds. No architectural obstacle; reaching Strong needs a second real JAR, not a
     contract break.

3. **description**: The live projection JAL is on `context_switcher` `develop`; the currently
   checked-out branch (`feature/work-engine-project-registry`, parked) does not carry it.
   - **classification**: named_gap_toward_strong
   - **grounds**: Observability/branch-hygiene only — `develop` (mainline) carries the real
     artifact and the merge is in `develop` ancestry. Not a falsification of the Partial claim
     and not architectural.

## Strong-blocker analysis (§5)

No open item is a contradiction blocking Strong. (a) Reaching Strong is additive (more real
JARs, a real supersession chain) — no frozen-contract or ratified-architecture break is
required; the projection-as-byte-copy + JAL-back-reference design and the fail-closed
Control-side verifier hold as-is. (b) The Partial claim is not falsified on re-derivation: I
independently re-hashed every digest and re-ran `recover_judgment` to `recovered=true` on the
real EDR-0002 projection JAL, and confirmed fail-closed refusal on tamper. O1 being
O12-independent, the possible irreproducibility of EDR-0002 does not impair judgment recovery.

## determination

≥ Partial on real evidence: **YES**. Any contradiction blocking Strong: **NO**. O1 meets the
per-obligation 1.0 bar.
