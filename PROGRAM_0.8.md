# PROGRAM 0.8 — Cross-Plane Integrity

> Organizes delivery of the [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md) 0.8.0 milestone. It
> **organizes** that scope; it does not amend it. Non-constitutional (T1).

| Field | Value |
|---|---|
| Milestone | **0.8.0 — Cross-Plane Integrity** |
| Obligations | Deepen **O8** cross-plane provenance (P8) · **O5** universal independent validation (P6) · **O1** judgment attachment over time (P1) — all currently **Strong/Partial** *within* a plane |
| Exit criteria | the deepened obligations **demonstrably hold ACROSS plane boundaries**, not only within Control |
| Status | **Kicked off 2026-07-17.** Founder ruled: **proceed with 0.8 as roadmapped.** Structure + carryovers taken at the recommended defaults (below) pending any redirection — no build before the design-open items are ruled. |

## The inflection (read first)

**After 0.7, every one of the 12 constitutional obligations is ≥ Partial.** The seven that
were Emerging (O3, O4, O6, O7, O10, O11, O12) all reached Partial across 0.4–0.7. On the
maturity axis, the ratified 1.0 threshold — *"every obligation ≥ Partial, no known
architectural contradiction preventing Strong"* — is technically met **today**.

So 0.8 and 0.9 are no longer filling existential gaps. **0.8 deepens** three obligations so
they hold across plane boundaries; **0.9** is the formal evidence-backed audit that
certifies the 1.0 threshold. This is depth-and-verification work, a different shape from the
gap-filling of 0.4–0.7 — and it is measured the same way against P2: demonstrate the
cross-plane guarantee for real, record any boundary that does not yet hold.

## The three planes (the boundaries 0.8 must cross)

- **Knowledge Plane** — `engineering_kb` (the bundled EKB, pinned in Control by digest).
- **Control Plane** — `ecf` (workflows, canonical decisions, the reasoning/transformation runs).
- **Project Plane** — `context_switcher` (the consumer repo; Work Requests originate here,
  and consumer evidence — e.g. the MISS-closure dossiers — lives here).

The 0.6/0.7 work already crossed these boundaries in anger: closures cite Project-plane
dossiers; the EDR bundle pins Knowledge-plane EKB; the FD-2 mortality issue was a
cross-plane provenance leak. 0.8 makes those crossings *first-class and demonstrable*.

## Founder kickoff rulings (2026-07-17)

1. **Proceed with 0.8 as roadmapped** (sequencing ruled) — deepen O8/O5/O1 cross-plane,
   then 0.9 readiness, then 1.0.
2. *(Recommended default, pending redirection)* **Three focused workshops** — one per
   obligation (O8, O5, O1) + a bars proposal, all under the single "demonstrably holds
   across planes" exit criterion; parallel, own worktrees.
3. *(Recommended default, pending redirection)* **Carryovers folded in** because they ARE
   cross-plane: **B2** consumer-repo projection (Control→Project provenance made concrete),
   **cross-repo evidence permanence** (generalize the 0.7 FD-2 durability rule to all
   cross-repo citations), and the **engine-hardening** debt (H1/H2/H3) as the background
   lane. **B1** EKB canonicalization remains deferred, non-gating.

## Scope ratifications (2026-07-17 — "ratify all as recommended")

All four proposals **RATIFIED (Founder)**: [PROPOSAL_O8_CROSSPLANE_PROVENANCE_SCOPE](PROPOSAL_O8_CROSSPLANE_PROVENANCE_SCOPE.md) ·
[PROPOSAL_O5_UNIVERSAL_VALIDATION_SCOPE](PROPOSAL_O5_UNIVERSAL_VALIDATION_SCOPE.md) ·
[PROPOSAL_O1_JUDGMENT_ATTACHMENT_SCOPE](PROPOSAL_O1_JUDGMENT_ATTACHMENT_SCOPE.md) ·
[PROPOSAL_08_PARTIAL_BARS](PROPOSAL_08_PARTIAL_BARS.md) (the 9-clause exit criteria).

No frozen contract re-opened (no T4): O8's `fingerprint.py` `sha256_normalized` is additive
(raw hasher untouched); O5's universality check is a new validator rule (WF022); O1's
JAR/JAL and O5's CPV are new record types.

**The four workshops converged on one blunt, honest finding: cross-plane integrity
essentially does not hold across the Control→Project boundary at v0.7.0** — which is exactly
the deepening 0.8 exists to add, recorded per Clarification A rather than concealed:
- **O8:** of 9 Project-plane citations in the CLOSURE records, exactly ONE is digest-bound;
  the rest are commit-pinned at best and one is already demonstrably broken (its cited path
  is gone at `context_switcher` develop HEAD). The 0.7 FD-2 durability rule never reached
  across a repo boundary. → generalized durability + a machine-walkable cross-plane manifest.
- **O5 (worth the founder's eye):** generation and *semantic* validation share an ACTOR
  within a run — the same model that writes a recommendation writes its own validation
  verdict. P6 holds today only via MECHANICAL independence (output contracts + the C13 gate
  re-derive ground truth; the non-model contract is the independent ratifier), NOT a distinct
  actor. Ratified reading: within-plane = mechanical independence with actor-sharing
  **recorded honestly** (bar O5-3); **cross-plane = distinct-actor required**. Universality
  becomes a checkable invariant (WF022) — today a new workflow with no validate task passes
  the validator.
- **O1:** EDR-0002's full judgment is recoverable today only from MORTAL `runtime/` — the
  durable bundle carries the conclusion + narrative, but the structured elements, trace, and
  18 provenance records are mortal and un-digest-anchored (`final-manifest.yaml` lists paths
  with zero sha256). → the Judgment Attachment Record (JAR) digest-anchors the full judgment;
  the JAL carries it across projection; O12-independent (valid over an `irreproducible` decision).

**Shared real anchor:** a **B2 projection of EDR-0002 into `context_switcher`** discharges
O8-3 / O5-3 / O1-3 at once — the first exit act that spans all three repos. It does not exist
at v0.7.0 (`context_switcher` holds zero projected canonical decisions), so it is built in
0.8; any boundary that still cannot be walked is recorded UNMET-and-open (P2).

## Exit sequence — outcomes (2026-07-17)

The first exit sequence to span all three repos (Knowledge / Control / Project). Every
real-act clause discharged against real bytes; **nothing manufactured**, one honest
Strong-vs-Partial refinement recorded (P2).

- **Act 1 — O1 (Control):** `JAR-EDR-0002-0001` digest-anchors EDR-0002's full mortal
  judgment (14 task-outputs, 18 provenance records, trace) and carries its 9 structured-
  reasoning elements durably. The judgment, previously recoverable only from mortal
  `runtime/`, now recovers from the durable store alone (verified). Valid over the
  `irreproducible` decision (attachment ≠ reproducibility). **O1-1..O1-7 discharged.**
- **Act 2 — O8 durability (Control):** `durable-pins-CLOSURE-0001.yaml` — a P14-safe
  sibling to write-once CLOSURE-0001 — durably re-pins all 4 cross-repo citations Tier-2
  (immutable git `blob_id` + LF-normalized content digest, resolved from the real consumer
  repo). All 5 file-pins verify; none unbound. Generalizes the 0.7 one-exposure fix.
- **Act 3 — B2 projection (Project):** EDR-0002 projected read-only into
  `context_switcher` (`engineering/canonical-decisions/EDR-0002/`) with a walk-back JAL;
  `recover_judgment` walked from the Project projection back through the real Control bytes
  to the JAR and EKB pin — **recovered: true**. Confers no standing (P7). **O1-cross-plane
  discharged.**
- **Act 4 — O5 CPV (P6):** a real cross-plane validation — generator = `control:generator`,
  validator = **Founder (Genesis) / project:reviewer** (distinct by id AND role), verdict
  `faithful`, `confers_standing: false`. `validate_cpv` re-derived both digests from the
  real cs projection bytes (`4b8f1de3…`); generator==validator is structurally impossible.
  **O5-3/O5-4 discharged with a genuinely distinct human validator.**
- **Act 5 — O8 walk:** EDR-0002's cross-plane manifest walked end-to-end —
  decision → Control evidence bundle → Knowledge EKB pin → Project projection — **3/3 hops
  digest-verified, 0 unbound, 0 broken, status `verified`.** **O8-3 discharged.**

**Honest Strong-vs-Partial refinement (recorded, not concealed — P2).** The Tier-2 projection
pin is genuinely durable — the projection blob `bf58ebde…` lives in the consumer repo's
object store, branch-independent, and its normalized digest equals EDR-0002's exactly. But
the *walker* resolves **working-tree bytes**, so a walk pointed at a consumer checkout on a
different branch reports the Project hop `unbound` (observed: the walk verified 3/3 against
the projection checkout; `gapped` against the consumer main checkout on its feature branch).
Cross-plane provenance HOLDS (the durable pin is immutable and content-verified); making
walk-verification resolve via git objects rather than working-tree files, so it holds
regardless of consumer branch state, is a **Strong-tier refinement** deferred beyond 0.8's
Partial bar (P13). O8 reaches Partial-cross-plane for real; this is the named gap to Strong.

**Net: all three obligations' cross-plane real clauses discharged against real bytes.** Full
regression at the merged tip: **1365 passed, 0 failed** (19 packages). Merged: ecf develop
(exit records) + context_switcher develop (the projection). The first canonical decision to
cross into the Project plane.

## Workshop O8 — Cross-Plane Provenance (P8)

**In place:** within-Control provenance (per-task records, env-scope fingerprints, the
canonical store chain); the EKB pinned by digest; the 0.7 durability rule (scoped to one
exposure); reasoning-model attestation.

**Design-open (workshop before build):**
1. **The cross-plane chain** — is a consequential artifact's provenance machine-walkable
   *across all three repos* (a canonical decision → its Control run → its Knowledge EKB pin
   → its Project Work Request/evidence)? What record makes the chain traversable without
   opening every repo by hand?
2. **Cross-repo durability, generalized** — the 0.7 fix closed ONE mortal cross-repo
   pointer; O8 needs the durability rule to hold for EVERY cross-repo citation (a
   permanent Control record may cite a Project/Knowledge path only digest-bound + durable).
3. **Digest agreement across planes** — a Project-plane dossier cited by a Control closure
   must be pinned so a later reader can prove the cited bytes; how divergent repo line-ending
   / commit states are reconciled (the recurring CRLF/digest tension).
4. **What "holds across planes" demonstrably means** — the bar: a real artifact whose
   provenance is walked end-to-end across all three repos and every hop digest-verifies.

## Workshop O5 — Universal Independent Validation (P6)

**In place:** generation≠validation within each released workflow (WF-REASON's
VALIDATE-0001 + C13 gate; WF-TRANSFORM's VALIDATE-0002).

**Design-open (workshop before build):**
1. **Universal** — is separation-of-generation-and-validation a *platform invariant* every
   workflow must satisfy (a validator gate), or only a per-workflow convention today? Make
   it checkable.
2. **Cross-plane validation** — when a Control artifact projects into the Project plane (B2)
   or consumes Knowledge-plane content, is the projection/consumption independently
   validated against its source, by an actor that is not its generator?
3. **The boundary case** — a self-validated cross-plane artifact (generator == validator
   across the boundary) is the P6 failure mode; the bar must reject it.

## Workshop O1 — Judgment Attachment Over Time (P1)

**In place:** judgment recorded as run outputs, canonical EDRs, assumptions; O12's
reproducibility-state and model attestation; the supersession chain.

**Design-open (workshop before build):**
1. **Attachment across the lifecycle** — the judgment behind a decision must stay
   recoverable as the decision moves across planes (projected into Project, superseded,
   re-evaluated). Where does the judgment-link live so it survives projection and
   supersession?
2. **Recoverable, not archaeological** (the Vision scene, cross-plane) — from a Project-plane
   projection of a canonical decision, can a reader recover the Control-plane judgment and
   the Knowledge-plane basis without reconstruction?
3. **The O12 seam** — O1 (judgment stays attached) and O12 (judgment stays reproducible) are
   adjacent; design O1's cross-plane attachment as records-only, not a dependency on O12's
   research-grade migration.

## Carryover / background lane (non-gating)

- **B2 — Consumer-repo projection** (arguably core, not carryover): project
  `canonical/decisions/` into `context_switcher` read-only, provenance-carrying (digest
  back-references to the Control source; never a second source of truth). This is O8/O1
  cross-plane provenance made concrete and is the natural real-act anchor for the 0.8 bars.
- **Cross-repo evidence permanence** — generalize the FD-2 durability rule (0.7 scoped it to
  one exposure) to every cross-repo citation. Directly O8.
- **Engine hardening (H1/H2/H3)** — executor-failure-detail in the run record;
  `--retry-failed`/state-manifest lockstep; O11 gate read-only. 3×-deferred; a deepening
  milestone is the right home for cross-cutting quality debt.

## Constitutional edges

- **P2** — a cross-plane guarantee is claimed only where demonstrated; a boundary that does
  not yet hold is recorded, not concealed (Clarification A). Deepening ≠ overclaiming.
- **P8** — every cross-plane hop is digest-bound; no permanent record cites a mortal path.
- **P6** — no artifact is validated by its own generator, across a plane boundary either.
- **P7** — cross-plane projection is read-only and human-gated where it confers standing;
  no automation grants approval/acceptance across a boundary.

## Immediate next step

Background threads, own worktrees, everything returned **PROPOSED** for founder
ratification (the established pattern): O8 workshop · O5 workshop · O1 workshop · Partial-bars
proposal (the cross-plane "demonstrably holds" criterion as evidence-checkable clauses, with
the real anchor likely being a B2 projection whose provenance walks all three repos).

| Field | Value |
|---|---|
| Owner | Founder |
| Status | Kicked off; workshops pending launch |
| Created | 2026-07-17 (post v0.7.0) |
| Cross references | [PROGRAM_0.7](PROGRAM_0.7.md) · [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md) · [PLATFORM_ARCHITECTURE](PLATFORM_ARCHITECTURE.md) (the planes) · [PLATFORM_PRINCIPLES](PLATFORM_PRINCIPLES.md) (P1, P6, P8, P2) |
