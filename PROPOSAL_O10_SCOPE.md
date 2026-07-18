# PROPOSAL — O10 Scope (Track A, 0.4.0)

> **Status: PROPOSED (draft for founder ratification).** Track A owner recommendation.
> Nothing here is settled. Every design choice is presented as options + a recommendation.
> The founder rules; then Track A builds. Non-constitutional (T1); derives from
> [PROGRAM_0.4](PROGRAM_0.4.md) Track A and the ratified [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md)
> 0.4.0 milestone (O10 → Partial). Traces to **P10** (artifacts stay synchronized with their
> authoritative engineering model).

| Field | Value |
|---|---|
| Obligation | **O10** — engineering-model synchronization (P10), Knowledge Plane |
| Exit bar (ratified) | **Partial = specified + minimal enforcement** |
| Deliverables | **A1** contract · **A2** one drift check · **A3** evidence |
| This document | Resolves the three *design-open* items with options + a recommendation |

---

## Headline finding (P2 honesty — read this first)

The mechanical half of O10 Partial **already exists and is green** in `engineering_kb`:

- `engine/ekb.py` command **`packages`** (`check_generated_packages`) compares a generated
  projection's declared `retrieved_objects` against the **live retrieval closure** recomputed
  from the authoritative graph, and **fails closed** on any mismatch.
- Tests already cover both directions: `test_current_package_passes` (green pass) and
  `test_stale_package_detected_by_closure_mismatch` + `test_stale_package_detected_by_legacy_token`
  (drift rejected). Full suite: **40 passed, 0 failed**; `python engine/ekb.py packages` →
  *"all generated packages match the current graph."*

So the **real O10 gap is not "build a drift check."** It is two things:

1. **No ratified specification (A1).** No document names the authoritative model or fixes the six
   required elements (version · compatibility · migration · identity · validation boundary · change
   process). The contract lives implicitly in code, the standards, and the migration notes — never
   ratified as *the* O10 contract.
2. **The existing check is optional.** It runs when someone types `ekb.py packages`. "Minimal
   enforcement" for Partial means **choosing an enforcement point that makes it non-optional** for
   the one covered pair — not writing new detection logic.

This reframes Track A from "implement" to **"specify + ratify + wire the existing mechanism."**
That is cheaper and more honest than it looked at kickoff, and it is exactly the "specified +
minimal enforcement" bar.

---

## Design-open (a) — which authoritative model carries the contract FIRST?

| | Option A1 — **EKB knowledge model** | Option A2 — ADR-0001 EIR/IR |
|---|---|---|
| What it is | The graph of Markdown Knowledge Objects in `engineering_kb`, made executable by `engine/ekb.py` | An *Engineering Intermediate Representation* proposed as a future canonical model |
| Status today | **Implemented**; validated, retrievable, projected, tested | **Deferred** (ADR-0001 status: *Deferred*); no schema, no code, no instance |
| Six elements present? | 5 of 6 de facto (identity, versioning, validation boundary, change process via migrations, compatibility in practice); needs consolidation | 0 of 6 — nothing to specify against yet |
| Enforceable now? | Yes — the `packages` check already runs against it | No — cannot enforce synchronization of a model that does not exist |

**Recommendation: Option A1 — the EKB knowledge model carries the contract first.**
Rationale: the exit bar requires *enforcement*, and you can only enforce a model that exists (P2:
claim only what is demonstrated). ADR-0001's EIR is explicitly a future-major-version direction; its
own review triggers ("three substantial projects", "recurring consistency problems") have not fired.
Draft A1 so the EIR is named as the **future convergence target** the contract is forward-compatible
with — i.e., the contract is written to *survive* the EKB→EIR transition, not to block it.

*Founder ruling needed:* accept EKB-model-first, with EIR recorded as the deferred convergence target?

---

## Design-open (b) — which single model→projection pair does the drift check cover?

There are currently **two** projections of the same authoritative closure (DG-ARCH-0001):

- **P-int** — `engineering_kb/generated/packages/EKP-ARCH-0001-subsystem-decision.md`
  (EKB-internal; front-matter `generated_from` + `retrieved_objects`).
- **P-ecf** — `ecf/generated/packages/EKP-ARCH-0001-should-i-introduce-another-subsystem.md`
  (cross-repo; `primary_object` + `retrieved_objects`, plus a source pin to EKB commit `89556c02`).

| | Option B1 — **EKB graph → P-int** | Option B2 — EKB graph → P-ecf (cross-repo) |
|---|---|---|
| Repos touched | `engineering_kb` only | `engineering_kb` **and** `ecf` |
| Mechanism | `ekb.py packages` — **already works, already tested** | Needs commit-pin resolution: check must load the *pinned* EKB commit, not HEAD |
| Isolation fit | Clean — no shared-repo collision | **Blocked now** — another thread is driving a live run on `ecf/develop`; charter forbids touching `ecf` |
| P10 fidelity | Same-plane synchronization (sufficient for Partial) | The "true" cross-plane P10 concern (Control artifact ← Knowledge model) |

**Recommendation: Option B1 for Partial; name B2 as the deepening target (0.6 O10 deepening).**
B1 is self-contained, already enforced-capable, and respects isolation. B2 is the architecturally
"real" P10 case but requires cross-repo commit-pin machinery and write access to `ecf` — out of
scope now and explicitly forbidden by the current isolation constraints. Record B2 as the first
deepening step so we are honest that Partial covers the internal pair only.

*Founder ruling needed:* accept the EKB-internal pair as the single covered pair for Partial?

---

## Design-open (c) — where does the contract document live?

| | Option C1 — EKB foundation | Option C2 — platform-level | Option C3 — **split (recommended)** |
|---|---|---|---|
| Location | `engineering_kb/foundations/AUTHORITATIVE_MODEL_CONTRACT.md` | a `platform/` contract doc | Normative contract as an EKB foundation; constitutional linkage at platform level |
| Pro | Versioned with the model it governs | Carries the P10/O10 constitutional linkage | Each concern lives where it belongs; contract versions with the model, linkage with the constitution |
| Con | A shared repo; constitutional linkage is awkward here | Drifts from the model it governs | Two docs to keep in step (one cross-reference) |

**Recommendation: Option C3 (split).** On ratification: the **normative contract** lands as an
EKB foundation doc (versioned alongside the model, enforced by `ekb.py`); a short **linkage note**
in [PLATFORM_CAPABILITY_MAP](PLATFORM_CAPABILITY_MAP.md) / [PLATFORM_PRINCIPLES](PLATFORM_PRINCIPLES.md)
records the O10/P10 tie. **Until ratified**, the A1 draft lives here at platform as
[PROPOSAL_O10_A1_CONTRACT](PROPOSAL_O10_A1_CONTRACT.md) — I do not create standing files in the shared
`engineering_kb` main checkout (isolation), and I do not ratify (role constraint).

*Founder ruling needed:* accept the split, with the normative contract destined for
`engineering_kb/foundations/` on ratification?

---

## Recommended scope for O10 Partial (summary)

1. **Model:** EKB knowledge model carries the contract first; EIR is the deferred convergence target.
2. **Pair:** EKB graph → EKB-internal generated package (`generated/packages/EKP-ARCH-0001`).
3. **Contract home:** split — normative doc → `engineering_kb/foundations/` on ratification; draft
   at platform now; constitutional linkage recorded at platform.
4. **Enforcement (the "minimal enforcement" half):** ratify the *existing* `ekb.py packages` check as
   the O10 drift gate for the covered pair, and make it non-optional at one point (see
   [PROPOSAL_O10_A2_DRIFT_CHECK](PROPOSAL_O10_A2_DRIFT_CHECK.md) for the two enforcement-point options).
5. **Evidence (A3):** already present — `test_current_package_passes` (pass) +
   `test_stale_package_detected_by_closure_mismatch` (drift rejected); cite, do not rebuild.

### Alternatives weighed (for the record)
- *Contract the EIR first* — rejected: cannot enforce a non-existent model; violates the Partial bar.
- *Cover the cross-repo ecf pair* — deferred: forbidden by isolation now; needs commit-pin machinery.
- *Write a brand-new drift checker* — rejected: duplicates a tested, green mechanism (P13: governance
  must justify itself; a second checker would not measurably improve traceability).

---

## Exact founder rulings still needed before build

1. **(a)** EKB-model-first, EIR as deferred convergence target? (Y/N)
2. **(b)** EKB-internal pair as the single covered pair for Partial? (Y/N)
3. **(c)** Split contract home, normative doc → `engineering_kb/foundations/` on ratification? (Y/N)
4. **Enforcement point:** which makes the check non-optional for Partial —
   (i) an EKB pre-release gate in `scripts/validate-release.py`, or
   (ii) a required CI step running `ekb.py packages`? (see A2 doc). Pick one for Partial.
5. **Scope confirmation:** is "ratify + wire the existing check" acceptable as the enforcement half,
   or does the founder want net-new enforcement mechanism (not recommended)?

---

## Metadata
| Field | Value |
|---|---|
| Owner (draft) | Track A owner (O10) |
| Status | **PROPOSED** — awaiting founder ratification |
| Change class | T1 Operational |
| Derives from | [PROGRAM_0.4](PROGRAM_0.4.md) Track A · [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md) 0.4.0 |
| Cross references | [PROPOSAL_O10_A1_CONTRACT](PROPOSAL_O10_A1_CONTRACT.md) · [PROPOSAL_O10_A2_DRIFT_CHECK](PROPOSAL_O10_A2_DRIFT_CHECK.md) · [PLATFORM_CAPABILITY_MAP](PLATFORM_CAPABILITY_MAP.md) · [PLATFORM_PRINCIPLES](PLATFORM_PRINCIPLES.md) |
