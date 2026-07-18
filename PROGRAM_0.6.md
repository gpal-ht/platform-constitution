# PROGRAM 0.6 — Corrigibility & Assumption Lifecycle

> Organizes delivery of the [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md) 0.6.0 milestone. It
> **organizes** that scope; it does not amend it. Non-constitutional (T1).

| Field | Value |
|---|---|
| Milestone | **0.6.0 — Corrigibility & Assumption Lifecycle** |
| Obligations | **O7** safe supersession (P14, depends on O3 ✓) · **O11** executable assumptions with review triggers (P11, depends on O10 ✓) |
| Exit criteria | O7 and O11 each reach **Partial** (bars to be ratified — see Bars thread) |
| Also in scope | **FD-2 ruling** — Operational Evidence as a distinct Plane (deferred to 0.6 by the ratified architecture; ruled here) |
| Status | **Scope RATIFIED 2026-07-16 ("Reading B, ratify all as recommended, dedicated background thread").** FD-2 RULED Reading B and landed in PLATFORM_ARCHITECTURE; both track scopes and the 6+6 Partial bars ratified (derive-don't-rewrite ratified; authority-model 0.2.0→0.3.0 bump ruled T4). **Tracks A and B authorized to build.** MISS-closure evidence assigned to a dedicated background thread in context_switcher. |

## Founder kickoff rulings (2026-07-16)

1. **Parallel A/B tracks** — Track A = O7 supersession; Track B = O11 assumptions; each
   runs scope workshop → founder ratification → build, in its own worktree (the proven
   0.5 pattern). One declared seam: an invalidated assumption is a natural supersession
   trigger — reconciled at integration, not by coupling the tracks.
2. **FD-2 is workshopped and RULED in 0.6** — a focused architecture thread produces the
   decision memo (both readings, at full strength), grounded in how O11's triggers
   actually consume operational evidence and in the 0.5 run-evidence-permanence deferral.
   The Founder rules during 0.6; the roadmap's promise is kept.
3. **Background lane** (never gates the exit): **B1** EKB draft-guide canonicalization —
   DG-ARCH-0002/0003 through a real evidence/review/acceptance path; **B2** consumer-repo
   projection of canonical decisions into `context_switcher` (O10 internal-first
   deepening). Identity-attestation hardening and role-acts ratification deferred (not
   selected).

## Scope ratifications (2026-07-16)

Proposal docs — all **RATIFIED (Founder)**: [PROPOSAL_O7_SUPERSESSION_SCOPE](PROPOSAL_O7_SUPERSESSION_SCOPE.md) ·
[PROPOSAL_O11_ASSUMPTIONS_SCOPE](PROPOSAL_O11_ASSUMPTIONS_SCOPE.md) ·
[PROPOSAL_06_PARTIAL_BARS](PROPOSAL_06_PARTIAL_BARS.md) (the exit criteria) ·
[FD2_DECISION_MEMO](FD2_DECISION_MEMO.md) (**RULED Reading B**, landed in PLATFORM_ARCHITECTURE).

Key embedded rulings:
- **Derive-don't-rewrite (P14):** superseded record bytes never change; effective status
  derives from the store chain (`supersedes` on the new index entry; write-once sibling
  marker). Three threads converged on this independently; ratified as the reading of the
  0.5 EDR contract text.
- **Authority model 0.2.0 → 0.3.0 (`accountability → assumption_review`) ruled T4** under
  the O4 precedent; lands lockstep with Track B's build.
- **Bar reconciliation:** PROPOSAL_06_PARTIAL_BARS' 6+6 clauses are THE exit criteria;
  Track A's O7-7 (trigger-seam-at-interface) is build scope, not a bar clause.
- **MISS-closure:** closure is a human-accepted record in Track B's `information_closures/`
  registry; the REAL consumer-repo evidence for MISS-0001/0002 is gathered by a dedicated
  background thread in `context_switcher` (PROPOSED dossier + draft closure records; the
  founder's acceptance is the human act). FD-2's permanence obligation governs where the
  evidence lives durably.

## Track A — O7 Safe Supersession (P14)

**In place from 0.5:** the canonical store with write-once index and its first record
(`EDR-0001`); `superseded` in every status ladder (C1/C3/workflow catalog); WF-TRANSFORM's
reservation that *supersession records the superseding Run ID*; the upheld-challenge →
mandatory reconsideration hook (P14 re-entry) in the disposition contract.

**Design-open (workshop before build):**
1. The supersession **vehicle** — extend WF-TRANSFORM-0001 (a superseding transformation
   run consuming a new approval), a distinct workflow, or the promotion tool's store
   semantics; where the "current vs superseded" pointer lives in the index.
2. The supersession **triggers** — better evidence (P14's own words), an upheld
   challenge's reconsideration obligation, an invalidated assumption (seam with Track B).
3. **History semantics** — superseded records remain intact and citable; nothing is
   rewritten; the chain (superseded_by / supersedes) is machine-walkable (P8).
4. **Authority** — supersession is human-decided end-to-end (P7 twice, as in O3): what
   records, what roles, what fail-closed checks.
5. Natural first target (flagged, not decided): `EDR-0001` itself, superseded by the
   re-run subsystem decision once MISS-0001/0002 close — the exact re-entry its own
   statement anticipates.

## Track B — O11 Executable Assumptions (P11)

**In place from 0.5:** reasoning runs already emit `ASSUME-*` records with
`evidence_strength` inside the recommendation envelope; `MISS-*` open-information records
with status; EDR-0001 carries them in its digest-bound evidence.

**Design-open (workshop before build):**
1. The **assumption record** — shape, identity, where it lives (run-bound vs repo-level
   registry), and the extraction path from existing run envelopes vs fresh declaration.
2. **Review-trigger classes** — evidence-arrival, dependency-change, time-based — and
   their machine evaluation: what checks them, when, against what.
3. What **"executable" means at Partial** — a machine-evaluated trigger produces a
   recorded, routed review obligation. Full invalidation propagation across reasoning is
   O12 (0.7), explicitly out of the Partial bar (P13).
4. **Routing** — a fired trigger routes like a challenge (O4 machinery: accountable
   office, never-empty recipient, evidence-based disposition)?
5. P11's boundary, verbatim: the reasoning need not be executable; the **assumptions**
   must be.

## FD-2 Workshop — Operational Evidence Plane

Deliverable: a decision memo presenting both readings at full strength — (a) Operational
Evidence becomes a distinct constructive Plane; (b) it remains a cross-cutting concern of
existing Planes — with evidence from Track B's trigger design (what actually consumes
operational signals), the 0.5 run-evidence-permanence deferral (`runtime/` mortality vs
digest-bound canonical evidence), and the capability map. **Founder rules; the ruling
lands in PLATFORM_ARCHITECTURE with the FD-2 marker resolved.**

## Background lane (non-gating)

- **B1 — EKB draft-guide canonicalization.** DG-ARCH-0002/0003 (authored `draft` in 0.5)
  through a REAL evidence/review/acceptance path. Honest scoping question inside the
  lane: WF-TRANSFORM canonicalizes approved *recommendations*; EKB guides are a different
  artifact class — either extend the transform surface or exercise the EKB's own release
  discipline with equivalent evidence/review/acceptance records. No silent widening of
  the canonical store's definition (ruled narrow in 0.5).
- **B2 — Consumer-repo projection.** Project `canonical/decisions/` into
  `context_switcher` read-only, provenance-carrying (digest back-references, never a
  second source of truth). Makes EDR-0001 visible where the work happens.

## Constitutional edges

- **P14:** superseded is never deleted, never rewritten; "latest wins" is
  unconstitutional; every supersession preserves the full chain.
- **P7:** no automation supersedes canonical knowledge, fires-and-decides a review, or
  accepts a superseding record — humans decide at every boundary, machines verify and
  refuse.
- **P11:** assumptions are the executable artifact; reasoning is not required to be.
- **P2:** a trigger that cannot actually fire (no evaluator wired) must not be recorded
  as "executable" — descriptive honesty over aspiration.

## Immediate next step

Four background threads, own worktrees, everything returned **PROPOSED** for founder
ratification (the 0.5 pattern): Track A workshop · Track B workshop · FD-2 memo ·
Partial-bars proposal (evidence-checkable clauses, negative cases, Partial-vs-Strong
line, bar-vs-reality baseline).

| Field | Value |
|---|---|
| Owner | Founder |
| Status | Kicked off; workshops pending launch |
| Created | 2026-07-16 (post v0.5.0) |
| Cross references | [PROGRAM_0.5](PROGRAM_0.5.md) · [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md) · [PLATFORM_ARCHITECTURE](PLATFORM_ARCHITECTURE.md) (FD-2) · [PLATFORM_PRINCIPLES](PLATFORM_PRINCIPLES.md) (P7, P11, P13, P14) |
