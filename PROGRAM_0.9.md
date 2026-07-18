# PROGRAM 0.9 — Constitutional Readiness

> Organizes delivery of the [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md) 0.9.0 milestone. It
> **organizes** that ratified scope; it does not amend it. Non-constitutional (T1).

| Field | Value |
|---|---|
| Milestone | **0.9.0 — Constitutional Readiness** |
| Goal (ratified) | Verify, **with evidence**, that every obligation meets the 1.0 threshold. |
| Capabilities (ratified) | Evidence-backed constitutional audit; resolution of any blocking architectural contradiction. |
| Exit criteria (ratified) | An **independent, evidence-backed report** shows every obligation ≥ Partial with **no contradiction blocking Strong**. *(O2 does not begin here — it runs continuously from 0.3; 0.9 is the formal assessment.)* |
| Gates | **1.0.0 — Constitutional Baseline** (the constitutional definition of 1.0: every obligation ≥ Partial, no known architectural contradiction preventing Strong). |
| Status | **Audit complete, CRR proposed 2026-07-18.** All four lanes done: 0.9-A method RATIFIED → twelve independent assessments written ([audit/](audit/)) → contradiction-resolution lane **empty** (no Strong-blocker) → synthesis = [CONSTITUTIONAL_READINESS_REPORT_0.9](CONSTITUTIONAL_READINESS_REPORT_0.9.md). Determination: **1.0 threshold MET** (12/12 ≥ Partial, 0 blockers) — **awaiting Founder ratification**, the act that gates 1.0. |

## The inflection (read first)

**0.9 is not a build. It is an audit.** Every prior milestone (0.4–0.8) *added* capability to
move an obligation up the maturity scale. 0.9 adds nothing to the maturity of the twelve
obligations — after 0.7 they are all already **≥ Partial**, and 0.8 deepened O8/O5/O1 across
plane boundaries. 0.9's deliverable is **a verdict, backed by evidence**: an independent report
that certifies the 1.0 threshold is met, and resolves anything that genuinely blocks it.

This is **O2's (platform self-honesty, P2) formal assessment** — the one milestone whose whole
product is the truth about the platform, produced to the same standard the platform demands of
any engineering claim: evidence-bound, independently validated, with every gap recorded rather
than concealed. If the audit finds an obligation that is *not* honestly ≥ Partial, or a
contradiction that *does* block Strong, then 0.9's exit is not met and 1.0 waits — that outcome
is a success of the audit, not a failure of it (P2).

Two things make this milestone's integrity load-bearing:
1. **Independence is the whole point.** The exit criterion says *independent*. An audit written
   by the same author who built the obligation, asserting the obligation passes, is exactly the
   generation==validation collapse the platform forbids (P6/O5). The independence model is the
   first ruling below.
2. **The constitution was ratified under Genesis** (Founder alone), with an *Independent
   Reaffirmation Obligation* still recorded as outstanding (CURRENT_PROGRAM). A
   constitutional-readiness audit is where that independence obligation comes due.

## The audit surface — the twelve obligations and where each reached Partial+

The baseline maturity table (roadmap, assessed at 0.2.0) plus what each milestone delivered:

| # | Obligation (principle) | Reached ≥ Partial | Primary evidence to audit |
|---|---|---|---|
| O1 | Intelligibility — recoverable judgment (P1) | 0.8 (JAR/JAL) | Judgment Attachment Record + Link; `recover_judgment` walk-back (Partial) |
| O2 | Platform self-honesty (P2) | continuous | This audit is its formal assessment; every release's honest deferrals |
| O3 | Canonicalization by evidence/review (P3,P4) | 0.5 (WF-TRANSFORM-0001) | Transform workflow + promotion tool; EDR-0002/0003 canonical |
| O4 | Answerability (P5) | 0.5 (stewardship runtime) | Authority model 0.3.0; stewardship + challenge routing |
| O5 | Independent validation (P6) | Strong (baseline) → 0.8 universal | WF022 universality invariant; CPV cross-plane record |
| O6 | Indestructible responsibility (P7) | 0.4 | Authority model; vacancy/succession/escalation runtime |
| O7 | Corrigibility (P14) | 0.6 (supersession) | Supersession vehicle; EDR-0001→0002 superseded, bytes intact |
| O8 | Provenance (P8) | Strong → 0.8 cross-plane | Cross-plane manifest + walker; two-tier durability; `sha256_normalized` |
| O9 | Versioned knowledge (P9) | Strong (baseline) | EKB versioning; model→projection drift gate (O10 release gate) |
| O10 | Model synchronization (P10) | 0.4 | Model contract; drift check; cross-repo projection |
| O11 | First-class assumptions (P11) | 0.6 | Assumption registry + evaluators + review triggers; read-only gate (0.8.3) |
| O12 | Lifetime reproducibility (P… "throughout their lifetime") | 0.7 (Partial, honest) | Model attestation; degraded-reproducibility schema; invalidation propagation |

## The hardest calls — honest open items the audit must classify

Each of these was **recorded, not concealed** (P2) in a prior release. The audit's job is to
classify each one under the ratified 1.0 test — is it *a contradiction blocking Strong* (which
blocks 1.0), or *a recorded Partial-with-named-gap* (which the 1.0 bar explicitly permits)? A
named path toward Strong is allowed at 1.0; an architectural contradiction preventing Strong is
not.

- **O12A-5 — one REAL assumption invalidation propagated end-to-end** ships **UNMET-and-open**
  (0.7, Clarification A): the machinery is fixture-proven, but reality has not yet produced a
  genuine invalidation to propagate. Reality-gated, not architecturally blocked.
- **Cross-model re-run execution** (O12) — specified, not demonstrated (the OQ-001 research
  ceiling). Does "reproducibility throughout their lifetime" require a demonstrated cross-model
  re-run for Partial, or is the honest degraded-state schema sufficient?
- **O8 walk-via-git-objects** — the cross-plane walker resolves working-tree bytes, so a walk
  against a consumer checkout on another branch reports the Project hop `unbound`; the durable
  pin itself holds. Named as a **Strong-tier refinement** (P13), deferred beyond 0.8's Partial
  bar.
- **Now resolved (should be confirmed closed by the audit):** the engine-reliability backlog
  (H1 failure-detail, H2 retry/lockstep, H3 O11 read-only gate) — shipped in **0.8.3**, so it is
  no longer an open item; the audit should verify it as closed rather than deferred.
- **Stale operational record:** CURRENT_PROGRAM's dashboard still reads "0.3.0 released / 0.4-dev
  next." That is an operational-board (T1) staleness, not a constitutional gap — but the audit
  needs a truthful current-state baseline, so refreshing it is a 0.9 housekeeping input.

## Proposed structure *(recommended defaults — pending founder ruling)*

Because 0.9 is an audit, the lanes are **assessment lanes**, not build tracks:

1. **Workshop 0.9-A — Audit method & rubric.** Define, before any obligation is judged: what
   counts as admissible **evidence** per obligation; the operational meaning of **independent**;
   the **maturity rubric** (None/Emerging/Partial/Strong bound to the constitutional clauses);
   and the **blocker-vs-gap test** that classifies each open item. This is the meta-decision the
   rest depends on — it is serialized before the audit.
2. **The audit — twelve independent per-obligation assessments.** Each obligation is assessed
   against its constitutional clause and the **real artifacts** (not claims), by an assessor
   **independent of the builder**, producing an evidence-bound maturity verdict + a gap
   classification. Parallelizable (the twelve are independent); each cites digest-bound evidence.
3. **Contradiction-resolution lane** *(conditional)* — engaged only if the audit finds a real
   contradiction blocking Strong. This is the only place 0.9 may do "build" work; if nothing
   blocks, this lane is empty and recorded so.
4. **Synthesis — the Constitutional Readiness Report.** One independent, evidence-backed report
   over all twelve: the 0.9 exit artifact. It states the 1.0 determination (met / not-yet, with
   the honest reason) for the Founder to ratify.

## Founder rulings needed to proceed

The kickoff cannot run the audit until these are ruled:

1. **Independence model.** How is the auditor made independent of the builder? (See the question
   below — this is the load-bearing decision.)
2. **Structure.** Adopt the four-lane shape above, or a leaner one?
3. **Open-item disposition rule.** Confirm the test: a *named path toward Strong* is permitted at
   1.0; only an *architectural contradiction preventing Strong* blocks it. (This governs O12A-5,
   cross-model re-run, and walk-via-git-objects.)

## Founder kickoff rulings (2026-07-18)

1. **Independence model — independent assessor, Founder ratifies.** Each obligation is audited
   by an assessor that did **not** build it, producing evidence-bound verdicts that cite
   digest-bound artifacts; the accountability office (Founder) ratifies. Reuses the platform's
   existing independent-validation record types rather than building new machinery. This
   satisfies P6 (independence from generation) and discharges the constitution's outstanding
   Independent Reaffirmation Obligation. *(0.9 stays an audit, not a build.)*
2. **Structure — the four lanes as proposed.** Workshop 0.9-A (method + rubric, serialized) →
   twelve independent per-obligation assessments (parallel) → contradiction-resolution lane
   (conditional, only if a real blocker is found) → synthesis into the Constitutional Readiness
   Report.
3. **Open-item disposition — a named path toward Strong is permitted at 1.0.** Per the ratified
   1.0 definition, only an *architectural contradiction preventing Strong* blocks 1.0; a
   recorded, honest named-gap does not. O12A-5, cross-model re-run, and walk-via-git-objects are
   therefore treated as Partial-with-named-gaps **subject to the audit confirming** each is
   genuinely non-architectural (the audit may still reclassify one as a blocker on the evidence).

## Governance

- **T1** — this document organizes ratified scope; it does not amend the roadmap or constitution.
- Milestone exit is a founder-visible integration step; the Constitutional Readiness Report is
  ratified by the accountability office (Founder) before 1.0 is claimed.
- Knowledge Plane remains pinned at **EKB 0.2.1** unless the audit finds cause to move it.
