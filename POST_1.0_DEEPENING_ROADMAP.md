# Post-1.0 Deepening Roadmap — Partial → Strong

> **Status: KICKOFF (proposed 2026-07-18) — the founder rules.** Organizes the platform's
> post-1.0 direction: taking the nine Partial obligations toward **Strong**, from the named gaps
> the 0.9 Constitutional Readiness audit recorded. Not existential work — 1.0 is met and stands.
> Non-constitutional (T1); it organizes the ratified roadmap's own post-1.0 clause ("after 1.0
> the roadmap deepens maturity; it no longer fills existential gaps"), and does **not** amend the
> constitution or the 1.0 definition.

| Field | Value |
|---|---|
| Derives from | [CONSTITUTIONAL_READINESS_REPORT_0.9](CONSTITUTIONAL_READINESS_REPORT_0.9.md) §4 (open-items register) + the twelve [audit/](audit/) IOAs |
| Baseline | 1.0 Constitutional Baseline: 12/12 obligations ≥ Partial · 3 Strong (O2, O5, O9) · 0 contradictions blocking Strong |
| Already shipped | **O10 gate-9 hardening** (ECF v1.0.1) — closed O10 audit items 1 & 2. The first deepening increment; the template for the rest. |
| Change class | T1 Operational (deepening within the ratified "deepen maturity" intent) |

**Founder rulings (2026-07-18):** (1) **Continuous / opportunistic** program — Lane A refinement
builds ship as point releases when done; Lanes B/C accrue with reality and usage; **no formal
post-1.0 milestones, no roadmap amendment.** (2) **Kick off Lane A item 1 — O8 walk-via-git-
objects** as the next increment. The recommended Lane A order (O8 → O11 → O10 → O5 → O12 → O2)
stands, opportunistically.

## The inflection — post-1.0 deepening is a different shape

The 0.4–0.9 milestones were **existential builds**: an obligation went from absent to Partial by
building a mechanism and demonstrating it once on a real artifact. Every remaining gap toward
Strong is one of three kinds, and only one is a "build":

1. **Breadth-through-use** — the mechanism is Partial because it's been exercised on *one* real
   anchor (largely EDR-0002); Strong wants the full surface. This closes **by using the platform
   on more real engineering questions**, not by new code. (O1, O3, O7, O8, O12.)
2. **Reality-gated** — the machinery is built and fixture-proven end-to-end; only a real
   triggering *event* is absent (a real assumption invalidation, a vacancy/succession, a
   migration, a fork). This closes by **instrumenting to catch the event when it occurs**, then
   waiting. (O12A-5, O4/O6 vacancy·succession·escalation, O7 fork-safety, O10 migration, O11
   trigger classes.)
3. **Named refinements** — discrete engineering that closes a specific gap without a
   frozen-contract or architecture break. These are the actual **build** backlog. (O8
   walk-via-git-objects, O5 multi-actor validation + non-identity CPV, O10 compatibility range,
   O11 harvest breadth, O12 model-resolving executor / cross-model re-run, O2 honesty-gate scope.)

Consequences worth stating plainly (P2): **there is no forcing deadline** — deepening is
continuous, driven by usage and opportunity, not a milestone clock; and **some obligations reach
Strong only when reality cooperates** (a real invalidation, a real vacancy), which the platform
cannot manufacture without violating P2.

## Per-obligation: what Strong needs (from the IOAs)

| # | Obligation | At 1.0 | The gap to Strong | Kind |
|---|---|---|---|---|
| O1 | Intelligibility | Partial | JAR/recovery on more than one real decision + a real supersession-chain JAR | breadth |
| O3 | Canonicalization | Partial | Broader canonical surface (more decisions/approvers) + a real *rejected* acceptance exercised | breadth |
| O4 | Answerability | Partial | Vacancy/transfer/escalation fired on a **real** event; succession *ordering* executable | reality-gated + refinement |
| O6 | Indestructible responsibility | Partial | Same real vacancy/succession event; recorded-acts storage format ratified | reality-gated + refinement |
| O7 | Corrigibility | Partial | More real supersessions; fork/multi-head safety on a real chain; wire the `invalidated_assumption` grounds class | breadth + reality-gated + refinement |
| O8 | Provenance | Partial | **walk-via-git-objects** (resolve pins via git objects, not working-tree bytes); manifests for more decisions | refinement + breadth |
| O10 | Model synchronization | Partial | Compatibility **range** vs exact pin; a real migration invalidating a real projection | refinement + reality-gated *(gate-9 done)* |
| O11 | First-class assumptions | Partial | Harvest the analysis-register sequences; two more trigger classes fired on real events; multi-plane | refinement + reality-gated |
| O12 | Lifetime reproducibility | Partial | A **model-resolving executor** (a run earns `degraded`/`fully_reproducible`); one real invalidation propagated (O12A-5); cross-model re-run | refinement + reality-gated |
| O2 | Self-honesty | **Strong** | (refinement) broaden the honesty gate beyond inline `.yaml/.json` tokens | refinement |
| O5 | Independent validation | **Strong** | (refinement) multi-actor validation (distinct executor for produce vs validate); a non-identity CPV projection | refinement |

## Proposed structure — three lanes, one continuous program

- **Lane A — Refinement builds (the backlog you sequence).** Discrete, gate-9-shaped tasks. A
  recommended value/feasibility order: **O8 walk-via-git-objects** (small, high-value cross-plane;
  the pins already carry `commit`+`blob_id`) → **O11 harvest breadth** → **O10 compatibility
  range** → **O5 multi-actor validation** → **O12 model-resolving executor** (unlocks cross-model
  re-run) → **O2 honesty-gate scope**. Each ships as a small point release, like v1.0.1.
- **Lane B — Reality-gated instrumentation (build the catcher, then wait).** For each event class
  (invalidation, vacancy/succession, migration, fork, un-fired trigger), ensure the machinery
  *records the obligation the moment the event happens*, and record honestly that it awaits a real
  event. No manufacturing (P2).
- **Lane C — Breadth-through-use (drive real questions).** Every additional real Work Request
  driven end-to-end accrues breadth for O1/O3/O7/O8/O12 at once. The cadence here is *use*, not
  build; the WR-0003/WR-0004-style runs are the vehicle.

## Governance note (one decision to make explicit)

The ratified [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md) milestone line ends at 1.0. This document
organizes deepening as a **T1 program** within the roadmap's own "deepen maturity" clause — it
does not add a post-1.0 milestone to the constitution. If you want a *formal* post-1.0 milestone
line (e.g. 1.1, 1.2 tied to specific obligations reaching Strong), that is a **roadmap
amendment** and should be ruled as such.

## Founder rulings needed

1. **Cadence** — run deepening as a **continuous, opportunistic program** (Lane A ships point
   releases as done; B/C accrue as reality and usage allow), or define **formal post-1.0
   milestones** (1.1, 1.2 …) with obligation targets (a roadmap amendment)?
2. **Lane A order** — adopt the recommended sequence (O8 → O11 → O10 → O5 → O12 → O2), or
   reprioritize?
3. **Scope now** — kick off **Lane A item 1 (O8 walk-via-git-objects)** as the next increment, or
   hold the roadmap as a plan and pick the first item later?
