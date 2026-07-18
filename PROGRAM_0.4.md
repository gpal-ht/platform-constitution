# PROGRAM 0.4 — Authoritative Model & Responsibility Foundations

> **Milestone working plan.** Non-constitutional (T1). Derives entirely from the ratified
> [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md) 0.4.0 milestone — it **organizes** delivery of that
> milestone; it does not redefine it (K5). Every deliverable traces to a constitutional
> obligation (P13: no obligation, no item).

| Field | Value |
|---|---|
| Milestone | **0.4.0 — Authoritative Model & Responsibility Foundations** |
| Obligations | **O10** (P10 engineering-model synchronization) · **O6** (P7 indestructible responsibility) |
| Roadmap exit | O10 and O6 each reach **Partial** |
| Structure | **Two parallel tracks** (independent planes) + a background hardening lane |
| Status | **COMPLETE — shipped as ECF v0.4.0 (2026-07-16).** **O10 → Partial** (drift release gate live, `validate-release` gate 9). **O6 → Partial-live**: the `trace_completion.py` T4 wiring landed (`_check_approval_authority_binding`, fail-closed), shipped in v0.4.0, and was **ratified (Founder, 2026-07-16)** — the WF-REASON-0001 amendment-history row is closed. Formal 18/18 halt proven live (`RUN-REASON-WR0001-V040-0002`). |

---

## Founder decisions (2026-07-15 kickoff)

1. **0.3 carry-over debt → folded into 0.4 as a background lane**, tracked separately from the
   milestone contract (it does **not** gate the O10/O6 exit).
2. **O10 and O6 run in parallel** — independent planes (Knowledge vs Governance), no dependency.
3. **O10 "Partial" bar → Specified + minimal enforcement.**
4. **O6 "Partial" bar → Descriptive model + one executable rule.**

### Scope ratifications (2026-07-15, post scope-workshop)

Proposal docs: `PROPOSAL_O10_*.md`, `PROPOSAL_O6_*.md` (all PROPOSED → decisions below).

**Track A — O10 (ratified as recommended):**
- Contract the **EKB knowledge model first**; ADR-0001 **EIR is a deferred convergence target**
  (marked Deferred, unenforceable — would violate the Partial bar).
- Drift check covers the **EKB-internal** model→package pair; the cross-repo `ecf` projection is
  the deepening target (later).
- The existing green `packages` drift check (`engine/ekb.py check_generated_packages`) is ratified
  as the O10 gate — the "minimal enforcement" half is essentially already built.
- **Enforcement point: E1 — release gate** (wire the drift check into `scripts/validate-release.py`);
  CI (E2) is the deepening step.
- Normative contract → `engineering_kb/foundations/` on ratification.

**Track B — O6 (ratified as recommended, with a governance override):**
- Record **`approval_authority: {role, authority, model_version}`** at the `waiting_for_human_approval`
  boundary; the rule lives in the **existing `human_authority` block of `trace_completion.py`**
  (accepts a `TASK-TRACE-0003` `task_version` bump).
- **Only the approval-authority binding is executable for Partial**; vacancy/succession/escalation
  stay descriptive (O4's runtime job at 0.5). Prototype: `ecf-wt-o6` worktree, 6/6 tests, not merged.
- **GOVERNANCE OVERRIDE (founder):** O6 (B1 model *and* B2 rule) is handled as a **CONSTITUTIONAL
  amendment**, NOT a T-band governance-mechanism change — because it touches P7 (indestructible
  responsibility). This raises the bar: the Root Governance Primitive applies (proposal → evidence
  → independent challenge → authorized disposition → versioned effect), Anti-Capture / asymmetric
  burden applies, and B1 amends the constitutional set (Governance and/or Principles). Under Genesis
  the Founder ratifies unilaterally, but it is **recorded as a constitutional amendment**, not T1/T-band.

### 0.4 exit-bar status (early read from the scope workshop)

- **O10 minimal-enforcement half:** the drift check already exists and is green — 0.4 work is
  *specification + wiring the E1 gate*, not building a checker.
- **O6 executable half:** the runtime already halts with a fail-closed `human_authority` record;
  the O6 rule is *one field (`approval_authority`) + one check* on that existing boundary.
  Both foundations are closer to Partial than the roadmap assumed.

### Execution status (2026-07-16)

- **O10 — Partial (done, merged).** Track A landed on `ecf` `develop` (drift gate merged).
- **O6 — descriptive model RATIFIED + executable rule merged (standalone).**
  - **B1 (descriptive model):** ratified as a **T5 constitutional amendment**
    ([AMENDMENT_O6_RESPONSIBILITY_AUTHORITY](AMENDMENT_O6_RESPONSIBILITY_AUTHORITY.md), Ratified
    Genesis 2026-07-15, all 8 checklist items). Entered the constitutional set: PLATFORM_PRINCIPLES
    **Clarification C** (→ 0.2.0), PLATFORM_GOVERNANCE **Doctrine E** (→ 1.1.0-genesis),
    PLATFORM_GLOSSARY two terms (→ 0.3.0).
  - **B2 (executable rule):** the standalone `tools/authority_rule/` module is **authorized and
    merged** into `ecf` `develop` (merge `22c3fa7`; rule tests 6/6; full regression 774 passed,
    0 failed). It is **inert until wired** — no frozen 0.3 output contract was modified.
  - **Wiring step — DONE and RATIFIED (2026-07-16):** the rule landed in `trace_completion.py`
    (`TASK-TRACE-0003` `0.3.0 → 0.4.0`, fail-closed `approval_authority` check), shipped in ECF
    **v0.4.0**, was exercised live in the formal 18/18 halt run, and the founder ratified the
    frozen-contract touch (WF-REASON-0001 amendment history row → "Ratified (Founder), 2026-07-16").
    **O6 is Partial-live.**

---

## Track A — O10: Authoritative Engineering-Model Contract *(Knowledge Plane)*

**Goal:** a versioned, stable (not frozen) contract for the authoritative engineering model that
later capabilities (0.6 O11 executable assumptions; universal generation) reference.

**Exit bar (ratified): specified + minimal enforcement.**

**Deliverables**
- **A1 — The contract (specification).** A ratified document defining the six required elements
  for the authoritative model: **version · compatibility rules · migration policy · identity
  semantics · validation boundary · change process.** Seeds to build from: ADR-0001 (engineering
  intermediate representation) and the existing `ecf/generated/` · `engineering_kb/generated/`
  projections.
- **A2 — One mechanical drift check.** A narrow, machine check that a projection (a `generated/`
  artifact) is consistent with its authoritative model — so model↔artifact drift is *detected*,
  not left to discipline. Scope kept minimal (one model→one projection is enough for Partial).
- **A3 — Evidence.** The check runs green on a real model/projection pair; a deliberate drift is
  rejected (the negative test).

**Design-open (workshop before build):** which authoritative model is the *first* to carry the
contract (the EKB knowledge model? ADR-0001's IR?); which single projection the drift check covers;
where the contract document lives (EKB foundation vs a platform-level contract).

**Plane / repos:** `engineering_kb` (model + contract) and/or `ecf` (projection + check); platform
docs for the contract's constitutional linkage.

---

## Track B — O6: Responsibility-and-Authority Model *(Governance Plane)*

**Goal:** make responsibility indestructible (P7) by defining *who holds what authority and how it
moves* — the governance foundation 0.5's O4 (durable stewardship / challenge routing) operationalizes.

**Exit bar (ratified): descriptive model + one executable rule.**

**Deliverables**
- **B1 — The model (descriptive).** A ratified governance document defining: the **five roles**
  (already named in PLATFORM_GOVERNANCE) made complete with **transfer, vacancy, escalation,
  succession**, and the **institutional-vs-individual authority** distinction.
- **B2 — One executable authority rule.** A machine-checkable rule that couples the model to the
  runtime we shipped in 0.3: e.g., a reasoning run **records which role holds approval authority**
  at the `waiting_for_human_approval` boundary, and the contract **rejects a run whose recorded
  authority does not match the model** (an approval attributed to a role without approval authority
  fails closed).
- **B3 — Evidence.** The rule passes on a conformant run; a mismatched-authority run is rejected.

**Design-open (workshop before build):** the exact authority a run must record (role identity? a
role→authority binding from the model?); whether B2 lives in the trace/manifest contracts or a new
gate; how vacancy/succession surface at runtime (or stay descriptive for Partial).

**Plane / repos:** `platform` + `ecf` governance docs (model); `ecf` runtime contracts (rule).

---

## Background lane — 0.3 hardening *(does NOT gate 0.4 exit)*

Tracked separately; folded in per the kickoff decision.

- **H1 — Formal 18/18 halt run.** Drive a fresh WR-0001 run to `waiting_for_human_approval` with
  frozen code (all executors are unit-green). Closes 0.3's last exit-criterion gap. ~16 model calls.
- **H2 — ECD-0002 contract enforcement.** `retrieve_context.py` verifies RETRIEVE-0001 consumed the
  committed classification; a test rejects a retrieval that ignores it. (Scheduled to 0.4 in ECD-0002.)
- **H3 — Resume-cascade.** Per-task provenance/env scoping so an executor fix doesn't invalidate the
  whole run — cheap resume-after-fix. Real design work; candidate, not committed.
- **H4 — JSON-executor output robustness.** The AI JSON executors intermittently wrap their envelope
  in prose or a ```json fence, which `_extract_env` rejects (`extra content outside the single JSON
  document`). Observed 5×: CLASSIFY-0002, DECIDE-0002, PRODUCE-0001, VALIDATE-0001 (×2 on the formal
  run — it blocked H1 at 14/18). Fix once in `_extract_env`: extract the first balanced JSON object
  even amid surrounding prose/fences, then re-run. Blocks the formal 18/18 halt (H1) until done.
  Note: the 0.3 *substantive* exit criterion was already met on run CLEAN-0002 (report produced +
  validated `passed`); H1 only closes the formal-ceremony gap.

---

## Traceability

| Obligation | Capability (Capability Map) | 0.4 deliverables | Exit |
|---|---|---|---|
| **O10** (P10) | Authoritative engineering-model contract; artifact–model synchronization enforcement | A1 contract · A2 drift check · A3 evidence | **Partial ✅ (done, merged)** |
| **O6** (P7) | Explicit responsibility-and-authority model | B1 model · B2 executable rule · B3 evidence | **Partial (model RATIFIED as constitutional amendment; B2 rule merged standalone — runtime-live pending the `trace_completion.py` T4 wiring)** |
| *(0.3 debt)* | Runtime hardening | H1 · H2 · H3 | not a 0.4 gate |

---

## Sequencing

Two independent tracks run concurrently; the background lane fills idle capacity.

```
Track A (O10):  workshop scope → A1 contract → A2 drift check → A3 evidence   ─┐
Track B (O6):   workshop scope → B1 model → B2 executable rule → B3 evidence  ─┤ → 0.4.0 (O10, O6 = Partial)
Background:     H1 formal run · H2 ECD-0002 · H3 resume-cascade  (non-gating) ─┘
```

**Immediate next step:** a scope workshop for each track (the *design-open* items above) before any
build — the 0.4 analogue of the constitutional workshops. Founder rules the design decisions; then
the tracks execute.

---

## Metadata
| Field | Value |
|---|---|
| Owner Role | Program Steward (WS-0) |
| Change class | T1 Operational |
| Derives from | [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md) 0.4.0 (ratified) |
| Cross references | [CURRENT_PROGRAM](CURRENT_PROGRAM.md) · [PLATFORM_CAPABILITY_MAP](PLATFORM_CAPABILITY_MAP.md) · [PLATFORM_GOVERNANCE](PLATFORM_GOVERNANCE.md) |
