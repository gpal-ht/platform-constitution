# PROPOSAL — 0.8 Partial Exit Bar (O8 · O5 · O1, cross-plane)

> **Status: RATIFIED (Founder, 2026-07-17) — these 9 clauses are the 0.8 exit criteria.**
> The shared real anchor is a B2 projection of EDR-0002 into context_switcher discharging
> O8-3/O5-3/O1-3; cross-plane integrity essentially does not hold at v0.7.0 and the broken
> boundary is recorded honestly (Clarification A), which is precisely the deepening 0.8
> adds. This proposal turns the
> [PROGRAM_0.8](PROGRAM_0.8.md) exit criterion — the deepened obligations
> **"demonstrably hold ACROSS plane boundaries, not only within Control"** — into
> precise, evidence-checkable clauses, following the ratified 0.5/0.6/0.7 precedent
> ([PROPOSAL_07_PARTIAL_BARS](PROPOSAL_07_PARTIAL_BARS.md),
> [PROPOSAL_06_PARTIAL_BARS](PROPOSAL_06_PARTIAL_BARS.md)). Non-constitutional (T1).
> Nothing here is ratified; the founder rules. This document does not modify
> PROGRAM_0.8.md, and it does **not** pre-empt the three parallel O8 / O5 / O1 scope
> workshops: wherever a ruling from those threads could change a clause, the clause is
> written **parametrically** ("the ratified cross-plane provenance record", "the
> ratified cross-plane durability rule", "the ratified universality check", "the
> ratified projection vehicle") so that ratifying this bar constrains *what must be
> true*, not *which design gets there*.
>
> **0.8 is DEEPENING, not gap-filling.** After 0.7 every obligation is ≥ Partial; O8,
> O5, and O1 are already Strong/Partial *within a plane*. This bar asks only that each
> **crosses one real plane boundary and is demonstrated there** — measured against P2
> exactly as 0.4–0.7 were: the cross-plane guarantee is claimed only where walked, and
> any boundary that does not yet hold is recorded, not concealed (PROGRAM_0.8
> Clarification A / constitutional edge P2).

| Field | Value |
|---|---|
| Derives from | [PROGRAM_0.8](PROGRAM_0.8.md) (kicked off 2026-07-17) · [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md) 0.8.0 |
| Bar proposed | **O8 / O5 / O1 Partial-cross-plane** — deepen cross-plane provenance (P8), universal + cross-plane independent validation (P6), and judgment attachment over the projection (P1) so each **demonstrably holds across a real plane boundary** |
| The three planes | **Knowledge** `engineering_kb` (bundled EKB, pinned by digest) · **Control** `ecf` (canonical decisions, runs) · **Project** `context_switcher` (Work Requests, consumer evidence) |
| Governing edge | **P2 first.** Deepening ≠ overclaiming. A guarantee is claimed only on a boundary actually walked; a boundary that does not hold is recorded (Clarification A). Every clause is measured against honesty before completeness. |
| Real anchor | The likely real act is a **B2 projection**: a real canonical decision (`EDR-0002`) projected read-only into `context_switcher`, provenance-carrying, whose chain walks `ecf → engineering_kb → context_switcher` and digest-verifies each hop (PROGRAM_0.8 carryover B2 — "the natural real-act anchor for the 0.8 bars") |
| Precedent | PROPOSAL_07_PARTIAL_BARS (ratified 2026-07-17) — clause discipline, artifact/demonstration/checker, real-not-fixture, named real identities, bar-vs-reality tracking, honest OUT list |
| Evidence baseline probed | `ecf` worktree `chore/0.8-partial-bars` @ `c02fe64` (= v0.7.0), read-only + far planes `engineering_kb` @ `v0.2.1` and `context_switcher` @ `develop` (read-only) |
| Change class | T1 Operational (a bar refinement; the obligations and the cross-plane exit are already ruled in the roadmap and re-ruled at 0.8 kickoff) |

---

## How to read a bar (unchanged from the ratified 0.5/0.6/0.7 discipline)

A Partial bar is met only when **every clause** below has (a) a named **artifact**
that exists, (b) a named **demonstration** that was actually run, and (c) a named
**checker** who verified it. Per P2, a clause with an artifact but no demonstration,
or a demonstration nobody checked, is an **explicit gap**, never a pass. Per the
roadmap's honesty guard, 0.8 is claimed only when the bar is met, validated, and
released.

Checker vocabulary (as in 0.5–0.7): **Machine (fail-closed contract)** · **Independent
validator (O5/P6)** · **Founder** (the only checker who can mark a clause *ratified*).

One discipline carried forward from how the 0.5–0.7 bars were actually **discharged**:
the real acts were named artifacts with identities (`EDR-0002`, `APPROVAL-0002`,
`ACCEPTANCE-0002`, `RUN-REASON-20260716-0002`, `CLOSURE-0001/0002`,
`RSTATE-EDR-0002-0001`) — not assertions that "a real case was run." Every REAL clause
below discharges the same way: **by naming the identity of the real record it
produced**, and — new for 0.8 — **by naming the real cross-repo objects each hop
pins** (a commit, a blob, a content sha256 in the far plane).

**The honesty framing specific to 0.8 (read before the clauses).** This is
DEEPENING-to-Partial-cross-plane, not solving cross-plane integrity. A met bar means
**one real boundary walked and demonstrated per obligation**, wrapped in an honest
record of every boundary still not crossed (§I.5 is deliberately long, as O12's was).
A bar that read as "cross-plane integrity achieved" would itself violate P2 — the
whole milestone is measured on whether the crossings it claims were actually walked.

---

# Part I — The 0.8 cross-plane Partial bar

**Bar being refined (PROGRAM_0.8 exit criterion, restated):** the deepened O8, O5, and
O1 hold **across a real plane boundary**, not only within Control — a consequential
artifact's provenance is machine-walkable across all three repos with every hop
digest-verified (O8); a cross-plane artifact is independently validated against its
source by an actor that is not its generator (O5); and the judgment behind a decision
stays recoverable after the decision is projected into another plane (O1). The bar has
three obligation groups, each with a parametric mechanism half and a REAL-crossing half.

## I.1 The bar as enumerated clauses

### Group O8 — Cross-plane provenance (P8)

**O8-1 — A single machine-walkable cross-plane provenance record (P8).** The ratified
cross-plane provenance record (O8-workshop ruling: a materialized chain record, a
resolver that assembles the chain, or a projection-carried back-reference set —
whichever the founder ratifies) makes a consequential artifact's provenance
**traversable across all three repos from one entry point**: a canonical decision →
its Control run → its Knowledge-plane EKB pin → its Project-plane Work Request /
evidence. Each hop names the far-plane object it pins (a commit or tag, and a **content
digest**), so the chain is walkable *without opening every repo by hand and guessing*.
This clause exists because today the chain is **scattered across three records that do
not reference each other** — `EDR-0002/evidence-manifest.yaml` names the source run and
`WR-0001` but not the EKB; `release/release-manifest.json` pins the EKB but names no
decision; `information_closures/CLOSURE-*.yaml` cite `context_switcher` dossiers but
bind to neither (see §I.6). No entry point walks all three.

**O8-2 — Every cross-plane citation is digest-bound and durable — the FD-2 rule
generalized across planes (P8).** The ratified cross-plane durability rule extends the
0.7 FD-2 permanence rule (`tools/reproducibility/durability.py`, today scoped to
`MORTAL_ROOTS = ("runtime/",)` **inside `ecf`**) to **every cross-repo citation**: a
permanent Control record may cite a Project-plane or Knowledge-plane path **only when it
is digest-bound** — a pinned content `sha256` (and, where line-endings diverge, a
declared normalization such as the `LF-stable` note) — so a later reader can prove the
cited bytes regardless of where the far branch has moved. A **bare** cross-plane
citation (a branch-and-path with no content digest) is **rejected by contract**, the
same fail-closed shape `durability.py` already applies within `ecf`. This closes the
open gap: the closure evidence schema is today exactly `{ref, note}`
(`tools/assumption_registry/closures.py`, `_EVIDENCE_ENTRY_FIELDS`) — **no `sha256`
field, no verification of cited cross-repo bytes**.

**O8-3 — One REAL decision's provenance walks all three repos and every hop
digest-verifies.** The chain is walked end-to-end for a **real** canonical decision (the
natural target is `EDR-0002`): from the Control decision, to its Control run
(`RUN-REASON-20260716-0002` / `RUN-TRANSFORM-20260716-0003`), to the Knowledge-plane EKB
pin (`engineering_kb` `v0.2.1` @ `26750dca…`, the release-manifest pin), to the
Project-plane origin (`context_switcher` `WR-0001` and the closure dossiers), and **each
hop's pinned digest re-verifies against the far-plane bytes**. The discharged clause
names the identities and the pinned far-plane objects (commit, tag, blob, sha256).
Fixtures prove the negatives; they never discharge this clause.

### Group O5 — Universal + cross-plane independent validation (P6)

**O5-1 — Generation ≠ validation made a universal, checkable invariant (P6).** The
ratified universality check turns separation-of-generation-from-validation from a
**per-workflow convention** into a **platform invariant every workflow must satisfy** —
a validator gate that is *checkable*, so a workflow that lets its generator ratify its
own output is rejected structurally, not merely by convention. Today the property is
real but **local**: `WF-REASON`'s `VALIDATE-0001` + the C13 gate
(`tools/review_gate/gate.py` — "consumes a verdict derived from bound outputs only …
never reads generation internals … no dependency on the task runner or any executor")
and `WF-TRANSFORM`'s `VALIDATE-0002` each enforce it inside their own workflow; nothing
enforces it *as an invariant across all workflows*.

**O5-2 — A cross-plane artifact is independently validated against its source by a
non-generator (P6).** When a Control artifact **projects into the Project plane** (the
B2 projection) or **consumes Knowledge-plane content**, the ratified cross-plane
validation requires the projection/consumption to be independently validated **against
its source**, by an actor that is **not its generator**, across the boundary. The
validator checks fidelity to source (the projection's digests match the Control record;
the consumed EKB content matches the pinned bytes) without being the party that produced
the projection — the C13 "verdict over bound outputs only" discipline, applied across a
plane boundary for the first time.

**O5-3 — One REAL cross-plane validation by a non-generator.** The projection (or
consumption) of §O8-3's real decision is **actually validated across the boundary** by
an actor distinct from its generator, producing a real recorded validation verdict whose
identity the discharged clause names. The negative is the sharp edge: a cross-plane
artifact whose generator **is** its validator (generator == validator across the
boundary) is **rejected** — the P6 failure mode the bar must foreclose. Fixtures prove
the negative; the real clause names the real verdict and the two distinct actors.

### Group O1 — Judgment attachment over the projection (P1)

**O1-1 — The judgment-link survives projection and supersession (P1).** A decision
projected into another plane carries a **recoverable back-reference to its Control-plane
judgment and its Knowledge-plane basis** — not merely its conclusion. The ratified
projection vehicle records, on the projected artifact, the links by which a reader
reaches the Control run/judgment and the EKB pin the judgment rested on, and these links
**survive supersession** (a projection of a superseded decision resolves forward through
the O7 chain to the live judgment, reusing `resolve.py`'s chain, never surfacing only
the stale conclusion). Designed **records-only** — it stores links, it does not depend on
O12's research-grade reasoning migration (the O1/O12 seam; PROGRAM_0.8 Workshop O1
design-open 3).

**O1-2 — Recoverable, not archaeological, across the boundary (the Vision scene,
cross-plane; P1).** From a **Project-plane projection** of a canonical decision, a reader
can recover the Control-plane judgment and the Knowledge-plane basis **without
reconstruction** — following the recorded links, not re-deriving them by hand across
three repos. A projection that carries a conclusion the reader must reverse-engineer back
to its judgment fails this clause: the judgment must be *reachable*, the cross-plane form
of the archaeology-to-engineering line the North Star draws.

**O1-3 — One REAL projection carries a recoverable judgment across the plane boundary.**
A **real** canonical decision (`EDR-0002`) is projected read-only into `context_switcher`
via the ratified vehicle, provenance-carrying (digest back-references to the Control
source; **never a second source of truth** — PROGRAM_0.8 B2), and from that real
projection an independent reader **recovers the Control judgment and the Knowledge
basis** — the honest `RSTATE-EDR-0002-0001` reproducibility state included (its judgment
recovers *as* `irreproducible: model_never_recorded`, which is the honest recoverable
answer, not a miss). The discharged clause names the real projection artifact's identity
and the links it carries. Fixtures prove the negatives; they never discharge this clause.

## I.2 Artifact · demonstration · checker, per clause

| Clause | Artifact that proves it | Demonstration that verifies it | Who checks |
|---|---|---|---|
| O8-1 | The ratified cross-plane provenance record + its walk surface over `canonical/decisions/`, `release/release-manifest.json`, and the Project-plane origin | A single walk from `EDR-0002` reaches the Control run, the EKB pin, and the Project WR/evidence, each hop naming its far-plane object; **negative: a chain with a hop that names no far-plane pin (a dangling cross-plane edge) is rejected (P8)** | Machine (walk contract) + independent validator (the chain assembles from digest-bound records, not hand-authored prose) |
| O8-2 | The ratified cross-plane durability rule (the generalized `durability.py`) + the closure/citation schema carrying a `sha256` field | Positive: a cross-plane citation with a pinned content sha256 admits and re-verifies. **Negatives: (i) a bare branch-and-path citation with no digest is rejected; (ii) a pinned digest that fails to re-hash against the far-plane bytes is rejected (P8)** | Machine (fail-closed contract + digest check) + independent validator (the rule is on an enforced path, not decorative) |
| O8-3 | The real walked chain over `EDR-0002` binding: run IDs, the `engineering_kb v0.2.1 @ 26750dca` pin, and `context_switcher WR-0001` / dossier objects, each with a pinned digest | The end-to-end walk on the real store; each hop's digest re-verifies against the real far-plane bytes (e.g. the ADR-0005 blob `e1797fe` → sha256 `a861cb72…`, re-verified); identities named | Machine (contracts) + Founder (confirms the decision is real) + independent validator (walks all three repos, each hop verifies) |
| O5-1 | The ratified universality check (the platform-wide validator-gate invariant) + its enforced invocation path | Positive: each released workflow satisfies the invariant. **Negative: a workflow whose generator ratifies its own output — or that lacks a validate gate — is rejected structurally (P6), not by convention** | Machine (invariant contract) + independent validator (the gate is enforced across workflows, the ratified O4-2/C13 discipline) |
| O5-2 | The ratified cross-plane validation contract (projection/consumption validated against source by a non-generator) | Positive: a projection/consumption is validated against its pinned source by an actor ≠ its generator. **Negative: a validation whose validator == the projection's generator is rejected (P6)** | Machine (fail-closed contract) + independent validator (validator identity ≠ generator identity) |
| O5-3 | The real cross-plane validation verdict over §O8-3's real projection, naming the two distinct actors | The live validation: the real projection is checked against its Control source by a non-generator; identities named; **negative (fixture): a self-validated cross-plane artifact is rejected** | Machine (contract) + Founder (confirms the validation was real) + independent validator (generation ≠ validation across the boundary) |
| O1-1 | The ratified projection vehicle carrying judgment-link + EKB-basis back-references, chain-resolving | The projected artifact's links resolve to the Control judgment and the EKB pin; **negative: a projection of a superseded decision that surfaces only the stale conclusion (does not resolve forward through the O7 chain) is rejected (P1/P14)** | Machine (link-resolution contract) + independent validator (links resolve, chain-forward holds) |
| O1-2 | The recovery walk from the Project-plane projection back to Control judgment + Knowledge basis | A reader recovers the judgment and basis by following links, no reconstruction; **negative: a projection carrying only a conclusion with no recoverable judgment-link fails** | Independent validator (performs the recovery without opening the generator's internals) + Machine (links present and typed) |
| O1-3 | The real read-only projection of `EDR-0002` in `context_switcher` + the back-reference links it carries (incl. `RSTATE-EDR-0002-0001`) | The real projection exists, is read-only (not a second source of truth), and a reader recovers the Control judgment + EKB basis from it; identities named | Machine (contract) + Founder (confirms the real decision + read-only standing) + independent validator (recovery succeeds cross-plane) |

## I.3 REAL-not-fixture requirements (the 0.5–0.7 discipline, applied cross-plane)

Fixtures are **required** — they are the only honest way to prove the negatives (O8-2's
bare-citation rejection and digest-mismatch rejection, O5's self-validation rejection,
O1's conclusion-only rejection). But **fixtures prove negatives only; they never
discharge the REAL clauses (O8-3, O5-3, O1-3).** The demonstration crosses **real** plane
boundaries:

1. **The provenance walks REAL repos.** The chain is walked over the real `EDR-0002` and
   re-verifies against the **real bytes in the real far planes**: `engineering_kb` at the
   real `v0.2.1` @ `26750dca…` pin, and `context_switcher`'s real objects (e.g. the
   ADR-0005 blob `e1797fe` re-hashing to the cited `a861cb72…`, verified during probing).
   A walk over fixture repos discharges nothing here.
2. **The cross-plane validation is by a REAL non-generator.** The real projection of
   `EDR-0002` is validated against its Control source by an actor that is **not** the
   party that produced the projection — a real recorded verdict with two named, distinct
   identities, not a self-check dressed as independent.
3. **The projection is a REAL read-only artifact in the REAL consumer repo.** The
   judgment-recoverable projection lives in `context_switcher` (which today holds **zero**
   projected `ecf` canonical decisions — verified), carries digest back-references to the
   Control source, and is **never a second source of truth**. A projection into a fixture
   consumer, however complete, discharges nothing.

Each REAL clause is discharged the 0.6/0.7 way: **by naming the identity of the real
record it produced** *and* the real far-plane objects each hop pins.

## I.4 Boundary cases — what explicitly does NOT count (sharp, P2-forward)

1. **A cross-repo citation with no content digest fails P8 (O8-2).** *This is the
   sharpest edge, and it is not hypothetical.* `CLOSURE-0001` cites
   `context_switcher: docs/evidence/MISS-0001-change-driver-analysis.md (develop @
   defa16f)` with **no content sha256**. At the pinned commit the dossier exists; at the
   **current `develop` HEAD the entire `docs/evidence/` directory is gone** — the cited
   path has moved out from under the citation, and with no digest the reader cannot even
   prove what the bytes were. A cross-plane citation that is not digest-bound is a promise
   the platform cannot keep across the boundary: it fails, exactly as a bare `runtime/`
   pointer failed FD-2 — one plane out.
2. **A mortal cited path across planes fails, and the 0.7 rule does not yet reach it
   (O8-2).** `durability.py`'s `MORTAL_ROOTS = ("runtime/",)` knows only `ecf`'s mortal
   root; a cross-repo path is **neither** mortal-by-that-rule **nor** tracked-in-`ecf`, so
   it is *ungoverned* today. A permanent Control record citing a far-plane path that only
   the far repo's mutable branch resolves — with no pinned digest and no durable copy — is
   the cross-plane form of the dangling-evidence exposure FD-2 named. The named cross-plane
   inputs must be digest-durable, or the citation is not honest about its own
   recoverability.
3. **A cross-plane artifact validated by its own generator fails P6 (O5-2/O5-3).** A B2
   projection that is "validated" by the same actor that produced it is **self-ratification
   across a boundary** — precisely the P6 failure, and *worse* than the within-Control case
   because the boundary crossing lends it false independence. The validator's identity must
   differ from the generator's, or the cross-plane validation is a costume.
4. **A projection carrying only a conclusion (not a recoverable judgment-link) fails P1
   (O1-1/O1-2).** A Project-plane copy of a decision's *answer* with no reachable link back
   to the Control judgment and the Knowledge basis is archaeology waiting to happen — the
   reader must reconstruct the judgment across three repos. Recoverable-not-archaeological
   means the judgment is *reachable by link*; a conclusion-only projection is a fact
   stripped of its reasoning, which P1 forbids (judgment precedes artifact).
5. **Claiming a cross-plane guarantee on a boundary NOT actually walked is THE P2
   violation (all groups).** This is the milestone's defining edge. Asserting "O8 holds
   across planes" while only the Control↔Knowledge hop was walked and Control→Project was
   not, or marking O5 "universal" while only two workflows were checked, is exactly the
   overclaim P2 and PROGRAM_0.8's constitutional edge forbid. A boundary that does not yet
   hold is **recorded** (Clarification A), never papered over by a guarantee that reads
   wider than the walk. Deepening ≠ overclaiming.
6. **A within-Control demonstration does not discharge a cross-plane clause.** Walking the
   provenance chain inside `ecf` only, validating a projection with a Control-plane actor
   that is actually the generator's proxy, or "projecting" a decision into another `ecf`
   directory satisfies nothing in O8-3/O5-3/O1-3 — the bar's word is *across a plane
   boundary*, and the real clauses name real far-plane objects.
7. **A projection that becomes a second source of truth fails (O1-3/P7).** If the
   `context_switcher` projection can be edited into disagreement with the Control source,
   or confers standing (approval/acceptance) across the boundary, it has stopped being a
   read-only provenance-carrying projection and become a rival canon — the P7 edge
   (cross-plane projection is read-only and human-gated where it confers standing; no
   automation grants standing across a boundary).
8. **A fixture cross-plane act discharges nothing real.** Walking a fixture chain,
   validating a fixture projection, or recovering judgment from a fixture consumer proves
   the contracts (and is required for the negatives). The real clauses name real identities
   and real far-plane objects in the real stores.

## I.5 Partial vs Strong — deliberately OUT of the Partial bar (P13)

0.8 is **DEEPENING to Partial-cross-plane**, not solving cross-plane integrity. The OUT
list is long **and that is honest** — it is the P2-required record of the ceiling, not an
apology. One real boundary walked per obligation is the bar; everything below is Strong.

- **Full bidirectional cross-plane sync.** The bar projects Control → Project **read-only,
  one direction**. A projection the consumer can write back, a two-way reconciliation
  loop, or Project-plane changes flowing back into Control is deepening (and P7-constrained
  regardless — no automation grants standing across a boundary).
- **Automated cross-repo provenance repair.** When a far-plane citation's bytes move or a
  digest fails to re-verify, the bar **detects and reports** it (fail-closed); a mechanism
  that *re-pins*, *re-copies*, or *heals* the cross-plane reference automatically is
  deepening.
- **Cross-REASONING provenance (O8's eventual reach).** The bar walks a decision's
  provenance across the three repos; walking the *reasoning* — every intermediate inference
  and its cross-plane inputs — across planes is O8's Strong horizon, explicitly out.
- **Real-time / live projection.** The bar requires a projection that exists and carries
  provenance at a point in time. A projection that tracks the Control source continuously,
  a refresh daemon, or guaranteed projection-staleness bounds is deepening (as 0.6/0.7 kept
  evaluation-on-invocation, not daemons).
- **Universal validation beyond the two released workflows' real check.** O5-1 makes the
  invariant *checkable and enforced*; retrofitting and re-validating every historical run
  and every future workflow against it is deepening — the bar requires the invariant plus
  **one** real cross-plane validation, not a platform-wide backfill.
- **General EKB canonicalization and general far-plane permanence (B1).** The bar makes
  digest-durable exactly the cross-plane citations a walked chain depends on. A general
  permanence regime for all of `engineering_kb` / `context_switcher` history (B1
  canonicalization) remains deferred and non-gating (PROGRAM_0.8: B1 deferred).
- **Cross-plane invalidation / supersession propagation.** Making `context_switcher` *act
  on* a Control-plane supersession or an invalidation (the 0.7 propagation reaching the
  consumer) is deepening — the projection carries provenance and judgment-links; it does
  not push state changes across the boundary.
- **Multi-consumer projection.** One real projection into `context_switcher` is the bar.
  Projecting into every consumer, or a general projection framework across arbitrary
  Project-plane repos, is Strong.

## I.6 Bar-vs-reality baseline (what holds across planes at v0.7.0 = `c02fe64` vs what 0.8 must add)

| Clause | Holds across planes today (probed evidence) | 0.8 must add |
|---|---|---|
| O8-1 | **No single walkable cross-plane record.** The chain exists but is **scattered and mutually unlinked**: `canonical/decisions/EDR-0002/evidence-manifest.yaml` names `source_run_id: RUN-REASON-20260716-0002` and `work_request_id: WR-0001` but **never the EKB**; `release/release-manifest.json` pins the EKB (`engineering_kb 0.2.1`, `source_commit 26750dca`, `source_tag v0.2.1`) but names **no decision**; `information_closures/CLOSURE-0001/0002` cite `context_switcher` dossiers but bind to neither. `EDR-0002.md` carries **no EKB reference at all**. No entry point walks all three repos | The ratified cross-plane provenance record + a walk surface that assembles the chain from one entry point, each hop digest-named |
| O8-2 | **Cross-plane citations are NOT digest-bound by contract.** `closures.py` evidence schema is exactly `_EVIDENCE_ENTRY_FIELDS = {"ref", "note"}` — **no `sha256` field**, and the checker verifies only that `ref` is non-empty; it never fingerprints the cited cross-repo bytes. Reality shows the split: `CLOSURE-0002`'s ADR-0005 citation **is** genuinely digest-bound (`git blob e1797fe; sha256 a861cb72…; LF-stable`, re-verified during probing) — but by **human discipline in a free-text note**, not an enforced field; `CLOSURE-0001`'s four citations and four of `CLOSURE-0002`'s five carry **only a branch-and-commit ref, no content digest**. `durability.py`'s `MORTAL_ROOTS` is `("runtime/",)` — it does **not reach cross-repo paths** at all | The ratified cross-plane durability rule (FD-2 generalized): a `sha256`-bound, verified citation field, fail-closed on bare cross-plane refs; `durability.py` extended past `ecf`'s mortal root |
| O8-3 | **Partly walkable, not end-to-end verified.** The Knowledge hop is strong (EKB commit+tag pin, immutable, verifiable); one Project hop is provably digest-bound (ADR-0005). But the walk is not assembled from one record, and most Project-plane hops are unprovable — and one is **already broken**: `CLOSURE-0001`'s MISS-0001 dossier path is gone at `context_switcher` `develop` HEAD, recoverable only from an un-gc'd historical commit, with no digest to fall back on | The real end-to-end walk over `EDR-0002` where **every** hop digest-verifies against real far-plane bytes; identities + pins named |
| O5-1 | **Generation ≠ validation is real but LOCAL, not a universal invariant.** `tools/review_gate/gate.py` enforces P6 rigorously *within a workflow* (verdict over bound outputs only; never reads executor internals; no task-runner dependency), via `VALIDATE-0001`/C13 (`WF-REASON`) and `VALIDATE-0002` (`WF-TRANSFORM`). But it is a **per-workflow convention**: nothing enforces separation as an invariant *every* workflow must satisfy | The ratified universality check — a platform-wide validator-gate invariant, checkable, rejecting a workflow that self-ratifies |
| O5-2 | **No cross-plane validation exists.** Independent validation is entirely within-Control; **no** Control→Project projection or Knowledge-plane consumption is validated against its source by a non-generator across the boundary (there is no projection to validate — see O1 row) | The ratified cross-plane validation contract: projection/consumption checked against pinned source by an actor ≠ its generator |
| O5-3 | Nothing across the boundary. The within-Control machinery is proven and reusable, but no cross-plane verdict has ever been recorded | One real cross-plane validation verdict, two distinct named actors; the self-validation negative |
| O1-1 | **Judgment attaches within Control; nothing carries it across a boundary.** Judgment is recorded as run outputs, the EDR, `RSTATE-EDR-0002-0001` (honest `irreproducible: model_never_recorded`), and the supersession chain — all inside `ecf`. No projected artifact carries a judgment-link or EKB-basis back-reference across a plane boundary | The ratified projection vehicle carrying chain-resolving judgment-link + EKB-basis back-references |
| O1-2 | **Recoverable within Control only.** A reader inside `ecf` can recover judgment from the records; from the Project plane there is nothing to recover *from* — no projection exists | The cross-plane recovery: judgment + basis reachable by link from a Project-plane projection, no reconstruction |
| O1-3 | **Zero projected decisions in the consumer.** `context_switcher` holds **no** projected `ecf` canonical decisions (verified: no reference to `EDR-*` or `canonical/decisions` anywhere in the repo). Control→Project projection does not exist | The one real read-only, provenance-carrying, judgment-recoverable projection of `EDR-0002` in `context_switcher` |

---

# Part II — Cross-consistency check (the 0.8 bar vs PROGRAM_0.8's constitutional edges and the ratified 0.5/0.6/0.7 bars)

1. **P2 is honored first, and made testable.** PROGRAM_0.8's edge — "a cross-plane
   guarantee is claimed only where demonstrated; a boundary that does not yet hold is
   recorded, not concealed (Clarification A)" — maps clause-for-clause: guarantee-only-where-walked
   → boundary I.4-5 (the defining P2 edge) + the REAL clauses' named far-plane objects;
   honest ceiling recorded → the long §I.5 and the "already broken" O8-3 baseline row. The
   bar adds the *checkable form* of P2 (each hop verifies against real bytes, or the clause
   is an explicit gap), not a reinterpretation. **Consistent** — and structured so
   "declaring it built" is impossible: the OUT list and the recorded broken boundary
   (`CLOSURE-0001`'s dead dossier path) are load-bearing, not decorative.
2. **P8 is the substrate, made cross-plane.** "Every cross-plane hop is digest-bound; no
   permanent record cites a mortal path" → O8-2 (the generalized FD-2 rule) + boundaries
   I.4-1/I.4-2. The 0.7 FD-2 rule is **inherited and widened**, not weakened:
   `durability.py`'s within-`ecf` fail-closed shape is the exact template O8-2 extends past
   the `runtime/` root to the far planes. **Consistent.**
3. **P6 is honored on the validation half.** "No artifact is validated by its own
   generator, across a plane boundary either" → O5-1 (universal invariant) + O5-2/O5-3
   (cross-plane validation by a non-generator) + boundary I.4-3. The C13 "verdict over
   bound outputs only" discipline (`gate.py`) is reused across the boundary, not relaxed.
   **Consistent.**
4. **P7 is honored on the projection half.** "Cross-plane projection is read-only and
   human-gated where it confers standing; no automation grants approval/acceptance across a
   boundary" → O1-3 (read-only, never a second source of truth) + boundary I.4-7. The
   projection carries provenance; it never pushes standing or state changes across the
   boundary — the 0.6/0.7 line (an invalidation may *trigger*, never *execute*) inherited in
   cross-plane form. **Consistent.**
5. **P1 is honored and made cross-plane.** "Engineering judgment precedes engineering
   artifacts" → O1-1/O1-2: the projected artifact is never primary; the judgment-link back
   to Control and the EKB basis travel with it, recoverable not archaeological. The O1/O12
   seam is respected — O1's cross-plane attachment is **records-only** and does not depend on
   O12's research-grade migration (PROGRAM_0.8 Workshop O1 design-open 3). **Consistent.**
6. **The ratified 0.5/0.6/0.7 bars are not contradicted; they are extended.** O7's narrow
   canonical store, its bidirectional walkable chain, and digest-stability survive untouched
   — O1-1 *reuses* `resolve.py`'s chain to resolve a projection of a superseded decision
   forward to the live judgment, never around it. O12's honest `RSTATE-EDR-0002-0001` is
   carried *into* the projection as the recoverable judgment (O1-3), not re-opened. The FD-2
   durability rule (0.7) is generalized, not weakened (O8-2). The closure records and the EKB
   pin (0.6/0.7 cross-plane artifacts) are the exact material the walk assembles. **Consistent.**
7. **Tension 1 (flagged, honesty-guarding) — one cross-plane boundary is already demonstrably
   broken, and the bar must not conceal it.** `CLOSURE-0001`'s MISS-0001 dossier citation is a
   live counter-example: bare (no digest) and dangling (path gone at `develop` HEAD). The bar
   is written so this does not silently pass — O8-2 rejects the bare citation by contract, and
   O8-3 requires *every* hop to verify. But it also means the real O8-3 walk may need the
   citation **re-pinned durably first** (a digest-bound copy, the ADR-0005 pattern) before the
   chain verifies end-to-end. This is a real sequencing cost, and the honest reading is that
   *today the Control→Project provenance does **not** hold across this boundary* — recorded
   here (Clarification A), not concealed. Flagged so it is ruled, not stumbled into.
8. **Tension 2 (flagged, design-constraining) — the walk must reconcile divergent far-repo
   line-endings and moving branches (the recurring CRLF/digest tension).** `CLOSURE-0002`'s
   ADR-0005 citation already shows the resolution shape — `LF-stable` plus a pinned blob
   `sha256` makes the bytes provable regardless of the far branch's CRLF state or where
   `develop` moves. O8-2 is written to require *that property* (a normalized, digest-bound
   pin) without dictating the mechanism, but the O8 workshop must **rule how divergent
   line-ending / commit states across planes are reconciled** (PROGRAM_0.8 Workshop O8
   design-open 3), or the walk will intermittently fail on a byte-difference that is not a
   content change. A sequencing cost, resolvable; flagged so the bar does not silently depend
   on an unruled normalization.
9. **Tension 3 (flagged, honestly bounding) — this is DEEPENING, and the bar says so.** Unlike
   the gap-filling of 0.4–0.7, every obligation here is already ≥ Partial within a plane; the
   honestly minimal bar — one real boundary walked per obligation — sits beside a deliberately
   long §I.5. A reader who mistakes the met bar for "cross-plane integrity achieved" has
   misread it against P2; the metadata, the governing-edge row, the OUT list, and the recorded
   broken boundary exist to foreclose that misreading. **Honestly achievable as deepening
   work, and honestly bounded** — which is the whole point of ruling the bar minimal.

---

## Metadata

| Field | Value |
|---|---|
| Status | **RATIFIED (Founder, 2026-07-17)** — the 9-clause 0.8 exit criteria; real anchor = B2 projection of EDR-0002 across all three repos |
| Owner Role | Program Steward (WS-0) |
| Change class | T1 Operational (a bar refinement; the obligations and the cross-plane exit are ruled in the roadmap and re-ruled at 0.8 kickoff) |
| Derives from | [PROGRAM_0.8](PROGRAM_0.8.md) · [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md) 0.8.0 · [PLATFORM_PRINCIPLES](PLATFORM_PRINCIPLES.md) (Root lifetime clause + Clarification A, P1, P2, P6, P7, P8, P9, P13, P14) |
| Evidence probed | `ecf` worktree `chore/0.8-partial-bars` @ `c02fe64` (v0.7.0), read-only: `information_closures/{CLOSURE-0001,CLOSURE-0002,README}.yaml/md`, `canonical/decisions/EDR-0002/{EDR-0002.md, evidence-manifest.yaml, reproducibility-state.yaml, evidence/}`, `challenges/CHG-20260716-0001/{durable-evidence/, durable-evidence-manifest.yaml}`, `release/release-manifest.json`, `tools/reproducibility/durability.py`, `tools/assumption_registry/closures.py`, `tools/review_gate/gate.py`, `tools/reasoning_propagation/propagate.py` · far planes read-only: `engineering_kb` @ `v0.2.1`/`26750dca` (EKB pin verified), `context_switcher` @ `develop` `221a59e` (WR-0001/dossiers; ADR-0005 blob `e1797fe` → sha256 `a861cb72…` verified; `CLOSURE-0001` MISS-0001 dossier path confirmed gone at HEAD, present at pinned `defa16f`) |
| Cross references | [PROPOSAL_07_PARTIAL_BARS](PROPOSAL_07_PARTIAL_BARS.md) (bar precedent, ratified) · [PROPOSAL_06_PARTIAL_BARS](PROPOSAL_06_PARTIAL_BARS.md) · [PROPOSAL_05_PARTIAL_BARS](PROPOSAL_05_PARTIAL_BARS.md) (exit discipline) · [PLATFORM_ARCHITECTURE](PLATFORM_ARCHITECTURE.md) (the three planes; FD-2, parametric) |
