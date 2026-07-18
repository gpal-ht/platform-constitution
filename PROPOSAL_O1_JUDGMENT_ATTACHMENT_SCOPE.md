# PROPOSAL — 0.8 Workshop O1: Judgment Attachment Over Time (P1)

> **Status: RATIFIED (Founder, 2026-07-17) — ratify all as recommended.** The finding that
> EDR-0002's full judgment is recoverable today only from MORTAL runtime/ (the durable
> bundle carries the conclusion + narrative, but the structured elements, trace, and 18
> provenance records are mortal and un-digest-anchored) is the honest gap this milestone
> closes (JAR/JAL); recorded per Clarification A. This resolves the three design-open
> items of [PROGRAM_0.8](PROGRAM_0.8.md) Workshop O1 (judgment attachment over time)
> and proposes O1's contribution to the 0.8 "demonstrably holds ACROSS planes" Partial
> bar. It is a **scope** document: options, trade-offs, real evidence, one recommendation
> per item, plus bar clauses and a spec appendix. **NO build.** Everything here is
> PROPOSED; the founder rules. Non-constitutional (T1).
>
> **The governing edge is P1 read together with P2.** P1: *"Engineering judgment precedes
> engineering artifacts. The artifact is never primary; the judgment that produced it
> is."* O1 asks whether that judgment stays **recoverable** as its decision moves across
> planes and through its lifecycle. P2 forces the honest answer where it does not yet:
> **the full judgment behind the platform's current canonical decision is recoverable
> today only from mortal `runtime/`, and is not even digest-anchored in the durable
> record.** That exposure — not a claim of completion — is what this workshop is about.

| Field | Value |
|---|---|
| Derives from | [PROGRAM_0.8](PROGRAM_0.8.md) Workshop O1 · [PLATFORM_PRINCIPLES](PLATFORM_PRINCIPLES.md) P1 (+ Root "throughout their lifetime", Clarification A, P2, P8, P14) · [PLATFORM_VISION](PLATFORM_VISION.md) Open Question 001 / success scene · [PLATFORM_ARCHITECTURE](PLATFORM_ARCHITECTURE.md) §4.1–4.3, §4.6 |
| Obligation | **O1 — Judgment Attachment Over Time (P1)**, currently Strong/Partial *within* Control; 0.8 deepens it to hold **across plane boundaries** |
| The 0.8 inflection | O1 is DEEPENING, not gap-filling. Measured against P2: demonstrate the cross-plane guarantee for real, or record honestly the boundary that does not yet hold |
| Evidence baseline probed | `ecf-wt-o1` @ `c02fe64` (= v0.7.0), read-only for runtime: `canonical/decisions/{EDR-0001,EDR-0002}/`, `assumptions/{index.yaml,ASM-0001..0004}`, `tools/canonical_resolution/resolve.py` · `ecf` main checkout (READ-ONLY): `runtime/runs/RUN-REASON-20260716-0002/` (18-task reasoning, mortal) · `context_switcher` (READ-ONLY): `decisions/ADR-000{1..8}` |
| Change class | T1 Operational (a workshop scope + bar contribution; the obligation and its Partial target are already roadmapped and re-affirmed at 0.8 kickoff) |
| Seam discipline | Records-only interfaces to O8 (cross-plane provenance) and O12 (reproducibility). O1 depends on **neither** thread's build (§3, §II) |

---

## How to read this document

Three design-open items, each with **Options → Trade-offs → Real evidence → one
Recommendation**. Then Part I: O1's Partial-bar contribution as enumerated, evidence-checkable
clauses with sharp negatives (the 0.5/0.6/0.7 discipline — a clause passes only with a named
**artifact**, a named **demonstration**, and a named **checker**; an artifact with no
demonstration is an explicit gap, never a pass). Then Part II: cross-consistency. Then the
spec appendix (the proposed records).

Two terms, fixed up front:

- **The conclusion** — *what* was decided: the disposition, the selected option, the
  recommendation statement. This is durable today.
- **The judgment** (P1's primary object) — *why*, in full: the structured decision elements
  (forces, options, alternatives, trade-offs, risks, confidence), the reasoning trace, and
  the per-task provenance chain that produced them. **This is the artifact P1 protects.** The
  central finding below is that the judgment, in full, is **not** durable today.

---

## The key finding (read before the options)

**Is the full judgment behind `EDR-0002` recoverable from durable records today, or only
from mortal `runtime/`?**

**Only the conclusion and a legible narrative *summary* of the judgment are durably
recoverable. The full judgment is recoverable only from mortal `runtime/`, and the durable
record does not even digest-anchor it.** Concretely, from the probed evidence:

- **The current canonical decision** is `EDR-0002` (supersedes `EDR-0001` on
  `better_evidence`; `canonical/decisions/index.yaml`, `record_sha256:
  4b8f1de3…`). Its source judgment is reasoning run `RUN-REASON-20260716-0002`.
- **The full judgment lives in mortal `runtime/`:**
  `C:\Dev\ecf\runtime\runs\RUN-REASON-20260716-0002\` holds the 18-task reasoning — the
  structured decision elements (`task_outputs/engineering-forces.yaml`,
  `decision-options.yaml`, `engineering-alternatives.yaml`, `engineering-trade-offs.yaml`,
  `engineering-risks.yaml`, `engineering-confidence.yaml`, `engineering-recommendation.yaml`,
  `missing-information.yaml`), the reasoning trace (`reports/trace.md`), and the 18
  `provenance/TASK-*.yaml` records. This tree is **unversioned, mortal `runtime/`** —
  outside any durable store.
- **The durable `EDR-0002` bundle carries six items only**
  (`canonical/decisions/EDR-0002/evidence/`, digest-bound by `evidence-manifest.yaml`): the
  **recommendation report**, its validation, `completion.yaml`, `final-manifest.yaml`, the
  approval record, the acceptance record. The report is a rich *rendering* — it embeds a
  narrative reasoning trace, the two declared assumptions, and per-dimension confidence,
  enough to answer the Vision's four questions **at the conclusion level.** But by its own
  words it *"performs no independent reasoning; it presents what the run's reasoning and
  decision tasks already produced."* It is a **projection** of the mortal structured
  artifacts, and it references decisive elements by ID whose substance is mortal (e.g.
  `FORCE-0003`/`FORCE-0004` appear in the durable report only as *"a characterizing force"*;
  `AXIS-0003`/`AXIS-0004` only as *"a trade-off axis"* — their real definitions are in
  `runtime/…/engineering-forces.yaml`).
- **The mortal judgment is not even digest-anchored durably.** The bundled
  `final-manifest.yaml` lists every task-output *path* but carries **zero `sha256`** over
  them (verified: `grep -c sha256` = 0). So a copy of a mortal `task_output` recovered later
  could **not be proven** to be the one that produced `EDR-0002`. The durable record neither
  **carries** the full judgment nor **anchors** it.

This is the honest P1×P2 gap O1 exists to close. It is adjacent to — but distinct from — the
0.7/O12 finding on the same decision: `canonical/decisions/EDR-0002/reproducibility-state.yaml`
records `state: irreproducible`, `irreproducible_reason: model_never_recorded`. O12 says the
judgment cannot be **re-run** (the model is gone). O1 says something sharper and independently
true: the judgment cannot be **fully recovered as records** either. **A decision can be both
irreproducible AND attached** — and making it attached is O1's job, achievable regardless of
O12 (§3).

---

## Design-open item 1 — ATTACHMENT across the lifecycle

**Where does the judgment-link live so it survives projection (into Project) AND supersession
(`EDR-0001`→`EDR-0002`)? Is the durable EDR bundle enough to recover the judgment — or is the
judgment mortal in `runtime/` (the honest gap)? Define the attachment record.**

### Options

- **1-A — Status quo: the report-in-bundle *is* the judgment of record.** The durable EDR
  bundle (report + validation + manifests + approval/acceptance) stands as "the judgment."
- **1-B — Anchor-only: add a durable digest manifest over the full mortal run**, but leave the
  reasoning bytes in `runtime/`. A recovered mortal artifact becomes *verifiable*, but the
  bytes remain mortal.
- **1-C — Judgment Attachment Record (JAR): a first-class, per-decision durable record** that
  (i) **carries** the model-independent structured reasoning the conclusion references (the
  decision elements, the trace), and (ii) **digest-anchors** the full source run (every
  `task_output`, `trace.md`, every `provenance/TASK-*`), and (iii) holds the **attachment
  link** that travels across supersession and projection. Co-located with the EDR bundle;
  a compact back-reference sits in the EDR front matter.

### Trade-offs

| Option | Recovers full judgment from durable records? | Survives supersession? | Survives projection? | Cost / risk |
|---|---|---|---|---|
| 1-A | **No** — conclusion + summary only; decisive elements resolve into mortal `runtime/` | Chain survives (P14) but points at the same thin bundle | The projection can cite the EDR, but there is no full judgment to reach | Zero build; **fails P1 at depth** and **fails durability** — the status quo *is* the gap |
| 1-B | Verifiable-if-found, but bytes still mortal | Anchor travels; bytes do not | Link reaches an anchor, not the judgment | Cheap; still leaves the judgment mortal → **fails the durability negative** |
| 1-C | **Yes** — carried + anchored, digest-verifiable | **Yes** — JAR is part of the never-rewritten superseded bundle; successor JAR carries `supersedes_judgment` | **Yes** — projection carries the JAR digest as its link (item 2) | Bundle grows; one promotion-time **harvest** step from run → durable JAR; the honest engineering cost |

### Real evidence

The platform **already has a working precedent for 1-C's attachment style**, in the
assumption store. When `EDR-0001` was superseded by `EDR-0002`, the assumptions migrated:
`ASM-0001`/`ASM-0002` (superseded) recorded provenance as `source_run_id:
RUN-REASON-WR0001-V040-0002` — a **mortal run** citation. Their successors `ASM-0003`/`ASM-0004`
record `provenance.source_path:
canonical/decisions/EDR-0002/evidence/engineering-recommendation-report.md` with
`source_sha256: 40db94c5…` — a **durable, digest-bound bundle** citation, and each carries
`supersedes_assumption: ASM-000{1,2}` (`assumptions/index.yaml`, `assumptions/ASM-0003/assumption.yaml`).
That is exactly the shape a JAR needs: a durable digest-bound source pointer + a
`supersedes_*` link that survives the chain. **The mechanism exists at the assumption grain;
O1 lifts it to the whole judgment.** The one thing the assumption records did *not* do —
carry/anchor the full structured reasoning, only the single statement — is precisely what the
JAR adds.

The supersession chain itself is already machine-walkable and digest-bound
(`EDR-0001/superseded-by.yaml` → `superseding_record_sha256: 4b8f1de3…`; resolved by
`tools/canonical_resolution/resolve.py`), so a JAR's `supersedes_judgment` pointer rides an
existing, proven rail rather than inventing one.

### Recommendation

**Adopt 1-C — the Judgment Attachment Record (JAR).** The judgment-link lives **in the JAR**
(a durable, digest-bound record co-located with the EDR bundle), never in mortal `runtime/`
and never only in the EDR front matter. The JAR **carries** the model-independent structured
reasoning the conclusion references and **digest-anchors** the full source run. It **survives
supersession** because it is part of the superseded bundle whose bytes are never rewritten
(P14) *and* the successor JAR carries `supersedes_judgment` (the `ASM-0003` precedent, lifted).
It **survives projection** via item 2. **1-B is retained as the mandatory floor** (anchoring
is non-negotiable even where carrying is deferred), and **1-A is rejected**: it *is* the gap,
and named as such is a P2 violation to leave standing while claiming O1 holds. Answering the
design-open question directly: **the durable EDR bundle is NOT enough today** — it recovers the
conclusion, not the judgment — and the JAR is the record that makes it enough.

---

## Design-open item 2 — RECOVERABLE, not archaeological (the Vision scene, cross-plane)

**From a Project-plane projection of a canonical decision, can a reader recover the
Control-plane judgment and the Knowledge-plane basis without reconstruction? What makes it a
workflow, not an excavation?**

### Options

- **2-A — Projection carries the conclusion only** (`edr_id` + disposition). The reader sees
  *what* was decided and must go excavate Control by hand for *why*.
- **2-B — Projection carries a Judgment Attachment Link (JAL):** a durable, digest-bound
  back-reference block that names the EDR record, the JAR, the source run, and the Knowledge
  pin, plus a resolve instruction. One follow, each hop digest-verifies.
- **2-C — Project plane holds a full durable copy of the judgment** (not a link, a replica).

### Trade-offs

| Option | Reader recovers *why* + Knowledge basis? | Workflow or excavation? | P7 / single-source-of-truth |
|---|---|---|---|
| 2-A | No — must hand-reconstruct from Control runtime | **Excavation** — the exact failure the Vision scene names | Safe but useless for recovery |
| 2-B | **Yes** — EDR (why, verbatim) → JAR (full reasoning, digest-verified) → EKB pin (Knowledge basis) | **Workflow** — one resolve call, no reconstruction | Read-only back-reference; Control stays the single source of truth (P7, architecture §4.3) |
| 2-C | Yes, but creates a second source of truth | Workflow, but forbidden | **Violates** "never a second source of truth" (B2 rule) and drifts |

### Real evidence

**No projection of `EDR-0002` exists in the Project plane today.** `context_switcher/decisions/`
holds `ADR-0001…ADR-0008` — the project's *own* decisions. The subsystem question `EDR-0002`
answers is the same one the project's `ADR-0005-canonical-subsystem-model.md` lives in, yet
**no ADR carries a back-reference to `EDR-0002`'s Control judgment** (only `ADR-0006` mentions
Control/EDR in passing, in a release context). Every `context_switcher` reference to
`RUN-REASON`/`canonical/decisions` sits inside its *own* mortal `runtime/runs/` or in
`vendor/ecf/` docs. So the cross-plane recovery scene is, honestly, **un-instantiated**: a
Project-plane reader at the subsystem boundary today has **no link at all** back to the Control
judgment or the Knowledge basis. This is the natural real anchor for the 0.8 bar (the B2
projection), and per P2 it must be stated as a **design target, not a demonstrated
capability**.

### Recommendation

**Adopt 2-B — the Judgment Attachment Link (JAL), carried by the B2 projection.** A
Project-plane projection of a canonical decision carries a durable, digest-bound JAL:
`{edr_id, edr_record_sha256, jar_id, jar_sha256, source_run_id, knowledge_pin (ekb_version +
digest), resolve}`. What makes it a **workflow, not an excavation** is that recovery is a
single **resolve call** — extend `tools/canonical_resolution/resolve.py` semantics so that,
given a projection, it returns the recoverable judgment chain (EDR record → JAR full reasoning,
each hop digest-verified → EKB pin) with **no hand-reconstruction of Control `runtime/`**. The
link is **read-only** and confers no standing (P7); Control remains the single source of truth
(2-C rejected). The bar's teeth (item's negative): **a projection carrying only its conclusion,
with no recoverable judgment-link, fails P1** — it re-creates the archaeology the Vision scene
exists to abolish.

---

## Design-open item 3 — The O12 seam (records-only, not a dependency)

**O1 (judgment stays *attached*) and O12 (judgment stays *reproducible*) are adjacent. Design
O1's cross-plane attachment as records-only, NOT a dependency on O12's research-grade
migration. Where is the clean line?**

### The distinction, made concrete on the same decision

`EDR-0002` is the ideal illustration because **both obligations touch it and they diverge**:

- **O12 (reproducibility)** asks: *can this judgment be re-run / re-evaluated?* For `EDR-0002`
  the answer is **no** — `reproducibility-state.yaml` records `irreproducible`,
  `model_never_recorded` (the pre-0.7 run never attested its reasoning model). Re-execution is
  impossible; that is O12's honest ceiling (ratified in PROPOSAL_07 as `O12B-2 SATISFIED` by
  the honest `irreproducible` state).
- **O1 (attachment)** asks: *can this judgment be recovered as durable, verifiable records,
  and reached by a link that survives projection + supersession?* That answer **can be yes**
  — the structured reasoning, the trace, and the provenance can be carried + digest-anchored
  in a JAR and reached by a JAL, **whether or not the model that produced them still exists.**

**Attachment ≠ reproducibility.** A decision that can never be re-run can still have its
judgment fully attached and cross-plane-recoverable. This is the clean line.

### Where the line is drawn (the records-only rule)

- **O1 owns:** durability, digest-anchoring, and reachability of the judgment **records** —
  the JAR (carry + anchor) and the JAL (cross-plane link). O1 obligates that the bytes exist,
  are verifiable, and are reachable by a link that survives the lifecycle.
- **O12 owns:** whether those records can be **re-executed / re-evaluated** — model recording,
  model availability, substitute-model migration, the `reproducibility-state` vocabulary.
- **The seam is a records-only cross-reference, one direction only.** The JAR **MAY** name the
  `reproducibility-state` record (so a reader sees both facts in one place) but **MUST NOT**
  require it, MUST NOT require a recorded/available model, and MUST NOT require
  `state: fully_reproducible`. **A JAR over an `irreproducible` decision is fully valid.** O1
  never consumes O12's migration machinery; it does not wait on it; it does not break if O12
  never advances past Partial.

### Recommendation

**O1's attachment is records-only and O12-independent.** The JAR carries and anchors bytes and
holds a link; it never obligates model recording, model availability, or re-execution. The
`reproducibility-state.yaml` stays O12's artifact; the JAR cross-references it as one optional,
non-load-bearing field. The bar enforces this directly (clause O1-7 + its negative): **an
attachment mechanism that only functions when the decision is reproducible has coupled O1 to
O12 and fails the seam.** This also keeps O1 clear of the O8/O5 threads: the JAL reuses O8's
digest-binding *discipline* (records-only) but declares no dependency on O8's cross-plane chain
build, and nothing in O1 asks a generator to validate its own output (P6/O5 untouched).

---

# Part I — O1's contribution to the 0.8 Partial bar

**The bar being contributed to** (PROGRAM_0.8 exit criterion): the deepened obligation
**demonstrably holds ACROSS plane boundaries**, with any boundary that does not yet hold
**recorded, not concealed** (P2 / Clarification A). O1's contribution: *the judgment behind a
canonical decision stays recoverable — as durable, digest-verifiable records reachable by a
link — as the decision is superseded and as it is projected into the Project plane.*

A clause passes only with a named **artifact** (exists), a named **demonstration** (was run),
and a named **checker** (verified it). Checker vocabulary (as ratified at 0.6/0.7):
**Machine (fail-closed contract)** · **Independent validator (O5/P6)** · **Founder** (the only
checker who marks a clause *ratified*). Per P2, an artifact with no demonstration is an explicit
gap, never a pass. Where a downstream ruling could change a clause, it is written
**parametrically** ("the ratified JAR", "the ratified JAL") so ratifying the bar constrains
*what must be true*, not *which design gets there*.

## I.1 The clauses

**O1-1 — A durable Judgment Attachment Record (JAR) exists for the current canonical
decision (P1/P8).** The ratified JAR is a first-class, digest-bound record co-located with the
EDR bundle (`canonical/decisions/EDR-*/`), with a compact back-reference in the EDR front
matter. *Negative:* a decision whose only durable judgment artifact is the recommendation
report — the status quo — does not satisfy O1-1; the report is the conclusion's rendering, not
the attachment record.

**O1-2 — The JAR digest-anchors the FULL judgment (P8).** The JAR carries a manifest of
`sha256` over **every** reasoning `task_output`, the reasoning `trace`, and **every**
`provenance/TASK-*` record of the source run — so a later reader can prove any recovered
reasoning artifact is the one that produced the decision. *Negative (the real exposure):* a
JAR that anchors only the report and manifests — leaving the decisive elements
(`engineering-forces.yaml`, `engineering-risks.yaml`, …) un-anchored, as `EDR-0002`'s bundled
`final-manifest.yaml` does today (zero `sha256` over task outputs) — fails O1-2.

**O1-3 — The JAR durably CARRIES the model-independent structured reasoning the conclusion
references (P1 durability).** The decision elements the report cites by ID (forces, options,
alternatives, trade-offs, risks, confidence, and the trace) are carried into the durable JAR,
not left resolvable only into mortal `runtime/`. *Negative (charter-required):* **a judgment
recoverable only from mortal `runtime/` fails durability** — a decision whose `FORCE`/`OPT`/
`RISK`/`AXIS` substance resolves only to `runtime/…/task_outputs/*.yaml` (exactly `EDR-0002`
today) fails O1-3.

**O1-4 — The attachment link survives SUPERSESSION (P14).** Across `EDR-0001`→`EDR-0002`, the
superseded JAR's bytes stand intact and citable (never rewritten), and the successor JAR
carries `supersedes_judgment` so `resolve.py` walks the judgment chain in both directions —
the `ASM-0003 → supersedes_assumption: ASM-0001` precedent, lifted to the whole judgment.
*Negative (charter-required):* **an attachment link that does not survive supersession fails**
— a successor whose JAR orphans or overwrites the predecessor's judgment, or a link that
resolves only to the superseded record and stops (the stale-back-pointer trap: `ASM-0001`
recorded `decision_ref: EDR-0001`, now superseded), fails O1-4.

**O1-5 — The attachment link survives PROJECTION into the Project plane (P1 cross-plane).** A
B2 projection of the canonical decision carries a durable, digest-bound Judgment Attachment
Link (JAL) back to the EDR record, the JAR, and the Knowledge pin. *Negative
(charter-required):* **a projected decision that carries only its conclusion, not a recoverable
judgment-link, fails P1** — it makes the judgment primary in name while stranding it in another
repo, the archaeology the Vision scene forbids.

**O1-6 — RECOVERABLE, not archaeological: one resolve workflow, no reconstruction (Vision
scene).** From the Project-plane projection, a single resolve call returns the judgment chain —
EDR record (why, verbatim) → JAR (full reasoning, each hop digest-verified) → EKB pin
(Knowledge basis) — with no hand-reconstruction of Control `runtime/`. *Negative:* a recovery
that requires opening Control by hand, or that reaches an anchor but not the reasoning bytes,
fails O1-6 (it is excavation, not workflow).

**O1-7 — The O12 seam is records-only; the JAR is valid over an irreproducible decision.** The
JAR functions with no dependency on a recorded/available reasoning model or on
`reproducibility-state = fully_reproducible`; it may cross-reference the `reproducibility-state`
record but never requires it. *Negative:* an attachment mechanism that only functions when the
decision is reproducible has coupled O1 to O12's research-grade migration and fails the seam —
demonstrated concretely by `EDR-0002`, which is `irreproducible` yet **must** be attachable.

**O1-8 — The honest gap is NAMED, not concealed (P2 / Clarification A).** Until the JAR/JAL
exist for `EDR-0002`, O1-across-planes is recorded **UNMET-and-open**: the full judgment behind
the current canonical decision is recoverable today only from mortal `runtime/` and is not
digest-anchored durably. Naming the exposure is a pass of O1-8; concealing it by pointing at
the rich report as if it were the full judgment is the P2 violation O1-8 forbids.

## I.2 Artifact · demonstration · checker, per clause

| Clause | Artifact that proves it | Demonstration | Who checks |
|---|---|---|---|
| O1-1 | The ratified JAR for the current decision, co-located under `canonical/decisions/EDR-0002/` | The JAR exists, is digest-bound, and is referenced from the EDR front matter; **negative: the report-only bundle is rejected as the JAR** | Machine (schema) + Founder (ratifies the record shape) |
| O1-2 | The JAR's `anchored_judgment` manifest (`sha256` over every task_output, trace, provenance record) | Anchor-verify: each named mortal artifact re-hashes to its recorded digest; **negative: an unanchored task_output (today's `final-manifest.yaml`, 0 `sha256`) is rejected** | Machine (digest contract) + independent validator |
| O1-3 | The JAR's carried structured reasoning (the decision elements + trace, durable copies) | Recover a decisive element (`FORCE-0002`, `RISK-0002`) in full from the durable JAR alone — no `runtime/` access; **negative: an element resolvable only into mortal `runtime/` fails** | Machine + independent validator (recovery from durable store only) |
| O1-4 | The successor JAR's `supersedes_judgment` + the intact superseded JAR bytes | `resolve.py` walks `EDR-0002` JAR → `EDR-0001` JAR both directions; superseded bytes re-hash intact; **negative: an orphaning/overwriting successor, or a stop-at-superseded link, fails** | Machine (chain contract) + Founder (P14 confirmation) |
| O1-5 | The JAL block on a B2 projection in `context_switcher` | The projection carries `{edr_id, edr_record_sha256, jar_id, jar_sha256, source_run_id, knowledge_pin}`, each digest-resolving to Control/Knowledge; **negative: a conclusion-only projection fails P1** | Machine (link contract) + independent validator (cross-repo digests) |
| O1-6 | The extended resolve workflow output over the projection | One resolve call returns EDR → JAR reasoning (digest-verified) → EKB pin, no reconstruction; **negative: recovery needing hand-excavation of Control `runtime/` fails** | Machine (resolve contract) + independent validator (walks the full chain) |
| O1-7 | The JAR validating over `EDR-0002` (whose `reproducibility-state` = `irreproducible`) | The JAR is well-formed and complete with no recorded model and `state: irreproducible`; **negative: a JAR that requires `fully_reproducible` or a recorded model fails the seam** | Machine (fail-closed contract) + Founder (seam ruling) |
| O1-8 | This proposal's key-finding section + the recorded UNMET-and-open status | The gap is stated with the real identities (`EDR-0002`, `RUN-REASON-20260716-0002`, the mortal task_outputs); **negative: any claim that the report is the full judgment fails P2** | Founder (honesty ruling) |

## I.3 REAL-not-fixture (the 0.5/0.6/0.7 discipline, applied to O1)

Fixtures are **required** to prove the negatives (an unanchored task_output rejected; a
conclusion-only projection rejected; a stop-at-superseded link rejected; a JAR demanding
`fully_reproducible` rejected). But **fixtures prove negatives only; they never discharge the
REAL clauses.** Each REAL clause discharges the 0.6/0.7 way — **by naming the identity of the
real record it produced:**

1. **The JAR is over the REAL current decision** `EDR-0002`, anchoring the REAL source run
   `RUN-REASON-20260716-0002`'s actual task_outputs/trace/provenance — not a fixture run.
2. **The supersession survival is over the REAL chain** `EDR-0001`→`EDR-0002` (the
   `ASM-0003 supersedes ASM-0001` precedent is real), named by identity.
3. **The projection carrying the JAL is a REAL B2 projection** into `context_switcher`,
   digest-back-referencing the real Control records — not a fixture ADR.
4. **The seam is demonstrated on the REAL `irreproducible` decision** `EDR-0002` — a JAR that
   works there proves O1-7 against reality, not a contrived reproducible fixture.

## I.4 Deliberately OUT of the O1 Partial bar (P13 — honest ceiling)

- **Re-execution or migration of the judgment.** O1 makes the judgment *recoverable as
  records*; making it *re-runnable under a substitute model* is O12, and is out.
- **The general cross-plane provenance chain (all three repos, every hop).** O1 carries the
  judgment-link on the B2 projection; the full O8 machine-walkable chain is O8's, and out.
- **Universal projection.** One real B2 projection carrying a JAL is the bar; projecting every
  canonical decision, or into N consumers, is deepening.
- **Automated projection or automated recovery-standing.** Projection is read-only and
  human-gated where it confers standing (P7); an automated projector that grants acceptance
  across the boundary is out and forbidden.
- **Retro-attaching the entire history of `runtime/`.** O1 attaches the judgment behind
  *canonical decisions*; a general permanence regime for all runs is out (and is the FD-2/B1
  deferral).
- **Carrying knowledge bytes.** The JAL pins the EKB by digest (identity + version); durably
  replicating Knowledge content into the projection is out (Knowledge stays the source).

## I.5 Bar-vs-reality baseline (what exists at v0.7.0 vs what O1 must add)

| Clause | Exists today (probed) | O1 must add |
|---|---|---|
| O1-1 | No JAR. The durable judgment artifact is the recommendation report in the EDR bundle | The ratified per-decision JAR, co-located, digest-bound |
| O1-2 | **No durable anchor of the full judgment.** Bundled `final-manifest.yaml` lists task-output paths with **0** `sha256`; the 18 `provenance/TASK-*` and `trace.md` are not in the bundle | The JAR anchor manifest (sha256 over every task_output, trace, provenance record) |
| O1-3 | **Full structured reasoning is mortal.** Forces/options/risks/axes/confidence live only in `runtime/…/task_outputs/`; the report renders a summary + placeholder-describes some elements | The JAR carrying durable copies of the decision elements + trace |
| O1-4 | **Chain walkable; judgment not attached to it.** `resolve.py` + `superseded-by.yaml` walk decision→decision; `ASM-0003` shows the durable-source + `supersedes_*` pattern at assumption grain | `supersedes_judgment` on the JAR; the judgment chain resolvable both directions |
| O1-5 | **No projection exists.** `context_switcher/decisions/` (`ADR-0001..0008`) carries no back-reference to `EDR-0002` | The JAL block on a real B2 projection |
| O1-6 | `resolve.py` resolves the canonical chain within Control; no cross-plane judgment-recovery workflow | The extended resolve workflow: projection → EDR → JAR → EKB pin, digest-verified |
| O1-7 | `reproducibility-state.yaml` = `irreproducible`/`model_never_recorded` exists (O12's); nothing attaches the judgment independent of it | The JAR proven valid over the irreproducible decision; the records-only cross-reference |
| O1-8 | The gap is real and, until now, unrecorded as an O1 obligation | This proposal names it UNMET-and-open (P2) |

---

# Part II — Cross-consistency check

1. **P1 is honored and made testable.** "The judgment that produced the artifact is primary
   and must stay recoverable" → O1-1/O1-2/O1-3 (durable, anchored, carried) + O1-5/O1-6
   (recoverable across the boundary). The bar adds the *checkable form* of P1, not a
   reinterpretation. **Consistent.**
2. **P2 is honored first.** The central finding is a gap, stated with real identities; O1-8
   makes "recorded, not concealed" a clause; §I.4 is a deliberate OUT list. The bar cannot be
   misread as "judgment attachment solved" — the honest ceiling is load-bearing. **Consistent.**
3. **P8 is the substrate.** Every attachment is digest-bound (JAR anchor, JAL back-references);
   no permanent record cites a mortal path un-anchored (the exact 0.7 FD-2 durability rule,
   here applied to the judgment). **Consistent** — and the JAR *closes* the un-anchored-mortal
   exposure this workshop found, rather than repeating it.
4. **P14 is depended upon, not weakened.** Supersession keeps the superseded JAR's bytes and
   chain intact (`EDR-0001` stands, `superseded-by.yaml` + ledger cross-checked by
   `resolve.py`); the successor adds `supersedes_judgment`. History preserved; truth revised.
   **Consistent.**
5. **P7 is honored across the boundary.** The JAL is read-only and confers no standing;
   projection is human-gated; no automation grants acceptance across the plane boundary
   (PROGRAM_0.8 P7 edge). **Consistent.**
6. **The O12 seam is clean and records-only (design-open 3).** O1 succeeds on a decision O12
   honestly rules `irreproducible`; the JAR never consumes O12's migration machinery.
   Adjacent, not dependent. **Consistent.**
7. **The O8/O5 seams are records-only.** O1 reuses O8's digest-binding discipline without
   depending on O8's cross-plane-chain build, and introduces no self-validation (P6/O5
   untouched). No dependency on either parallel thread. **Consistent.**
8. **Tension (flagged, honesty-guarding) — the real cross-plane demonstration depends on a
   real B2 projection that does not exist yet.** O1-5/O1-6 discharge only once a real
   projection into `context_switcher` carries a JAL. Per P2 this is a **design target**; if
   the 0.8 schedule cannot produce a real B2 projection, O1-5/O1-6 are recorded
   UNMET-and-open (Clarification A) and O1 ships its within-Control clauses (O1-1..O1-4, O1-7,
   O1-8) — never a manufactured projection to pass the bar. Flagged so it is ruled, not
   stumbled into.

---

# Appendix A — Proposed records (spec, PROPOSED)

> Illustrative shapes, not a build. Field names are parametric; ratifying the bar constrains
> what must be true, not the exact keys.

### A.1 Judgment Attachment Record (JAR) — `canonical/decisions/EDR-XXXX/judgment-attachment.yaml`

```yaml
schema_version: "0.1.0"
record_type: judgment_attachment_record
record_id: JAR-EDR-0002-0001
decision_ref: EDR-0002
decision_record_sha256: 4b8f1de3addda22498c9af30a6821bc6c05edbc0a5e2dd484610ebd701439b2d
source_run_id: RUN-REASON-20260716-0002        # the mortal reasoning run

# (1) CARRIED — durable copies of the model-independent structured reasoning
carried_judgment:
  - name: engineering-forces
    path: judgment/engineering-forces.yaml       # durable copy, co-located
    origin_path: runtime/runs/RUN-REASON-20260716-0002/task_outputs/engineering-forces.yaml
    sha256: <digest>
  # … decision-options, engineering-alternatives, engineering-trade-offs,
  #     engineering-risks, engineering-confidence, engineering-recommendation,
  #     missing-information, reports/trace.md

# (2) ANCHORED — digest manifest over the FULL judgment (carried or not),
#     so any recovered mortal artifact is provable
anchored_judgment:
  task_outputs:
    - {path: task_outputs/engineering-forces.yaml, sha256: <digest>}
    # … every task_output
  trace: {path: reports/trace.md, sha256: <digest>}
  provenance:
    - {path: provenance/TASK-ANALYZE-0002.yaml, sha256: <digest>}
    # … all 18 provenance records

# (3) LIFECYCLE links
supersedes_judgment: JAR-EDR-0001-0001           # survives supersession (P14)
knowledge_pin: {ekb_version: "0.2.1", digest: <ekb-digest>}   # Knowledge basis

# (4) O12 seam — records-only cross-reference, NON-load-bearing
reproducibility_state_ref: RSTATE-EDR-0002-0001  # may be `irreproducible`; JAR valid regardless

recorded_by: {actor: "<promotion actor>", recorded_at: "<date>"}
```

### A.2 Judgment Attachment Link (JAL) — block carried by a B2 projection in `context_switcher`

```yaml
schema_version: "0.1.0"
record_type: judgment_attachment_link
projected_decision_ref: EDR-0002
control_repo_pin: {ref: "<tag/commit>", edr_record_sha256: 4b8f1de3…}
jar_ref: {jar_id: JAR-EDR-0002-0001, jar_sha256: <digest>}
source_run_id: RUN-REASON-20260716-0002
knowledge_pin: {ekb_version: "0.2.1", digest: <ekb-digest>}
resolve: "tools/canonical_resolution/resolve.py --recover-judgment EDR-0002"
standing: read_only            # confers no acceptance/approval (P7)
```

---

## Metadata

| Field | Value |
|---|---|
| Status | **RATIFIED (Founder, 2026-07-17)** — O1 authorized to build; JAR digest-anchors the full judgment, JAL carries it across projection; O12-independent |
| Owner Role | Program Steward (WS-0) |
| Change class | T1 Operational |
| Derives from | [PROGRAM_0.8](PROGRAM_0.8.md) Workshop O1 · [PLATFORM_PRINCIPLES](PLATFORM_PRINCIPLES.md) (Root "throughout their lifetime", Clarification A, P1, P2, P8, P14) · [PLATFORM_VISION](PLATFORM_VISION.md) Open Question 001 / success scene · [PLATFORM_ARCHITECTURE](PLATFORM_ARCHITECTURE.md) §4.1–4.3, §4.6 |
| Evidence probed | `ecf-wt-o1` @ `c02fe64` (v0.7.0): `canonical/decisions/{index.yaml, EDR-0001/superseded-by.yaml, EDR-0002/{EDR-0002.md, evidence-manifest.yaml, reproducibility-state.yaml, evidence/*}}`, `assumptions/{index.yaml, ASM-0003/assumption.yaml}`, `tools/canonical_resolution/resolve.py` · `ecf` main (READ-ONLY): `runtime/runs/RUN-REASON-20260716-0002/{task_outputs/*, provenance/TASK-*.yaml (18), reports/{trace.md, engineering-recommendation-report.md, final-manifest.yaml}}` · `context_switcher` (READ-ONLY): `decisions/ADR-000{1..8}` |
| Cross references | [PROPOSAL_07_PARTIAL_BARS](PROPOSAL_07_PARTIAL_BARS.md) (O12 seam, bar discipline) · [PROPOSAL_06_PARTIAL_BARS](PROPOSAL_06_PARTIAL_BARS.md) (bar precedent) · O8/O5 0.8 workshops (records-only seams) |
| Constitutional edges | P1 (judgment primary, recoverable) · P2 (the mortal-judgment gap named, not concealed) · P8 (every attachment digest-bound) · P14 (supersession preserves the superseded JAR) · P7 (projection read-only, human-gated) |

> **The one-line finding, for the founder:** the full judgment behind `EDR-0002` is recoverable
> today **only from mortal `runtime/`** — the durable bundle carries the conclusion and a
> narrative summary but neither **carries** nor even **digest-anchors** the structured reasoning,
> the trace, or the 18-task provenance. The JAR closes that; the JAL carries it across the
> Project boundary; both are records-only and succeed even though the decision is
> `irreproducible`.
