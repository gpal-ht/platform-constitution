# PROPOSAL_O6_SCOPE — Track B (O6) scope resolution for 0.4.0

> **Status: PROPOSED (draft for founder ratification).** Non-constitutional (T1 working
> proposal that organizes delivery of a ratified capability). This document does **not**
> ratify strategy — it resolves the Track B *design-open* items from
> [PROGRAM_0.4](PROGRAM_0.4.md) as **options + a recommendation**. The founder rules; then
> B1/B2 build.
>
> Obligation: **O6 — indestructible responsibility** (P7). Plane: Governance.
> Ratified exit bar: **descriptive model + one executable rule → Partial.**

---

## 0. What is already true (so we do not re-invent it)

Three facts from the repositories anchor this proposal. They are findings, not proposals.

1. **The five roles are already named and ratified** — in
   [PLATFORM_PRINCIPLES](PLATFORM_PRINCIPLES.md) P5 and
   [PLATFORM_GLOSSARY](PLATFORM_GLOSSARY.md): **authorship · approval · ownership ·
   accountability · responsibility acceptance**, described as "distinct and transferable."
   O6's B1 does not name new roles; it makes the *named* roles **complete** (transfer,
   vacancy, escalation, succession, institutional-vs-individual).

2. **The runtime already has a P7 boundary with a dedicated record.** The 0.3 orchestration
   engine (`ecf/tools/orchestration/engine.py`) drives a reasoning run to exactly one
   successful terminal state, `waiting_for_human_approval`, and **refuses** any completion
   that purports to grant approval. The completion record
   (`reports/completion.yaml`, task `TASK-TRACE-0003`) already carries a **`human_authority`**
   block, and its output contract (`ecf/tools/task_runner/output_contracts/trace_completion.py`,
   `_check_approval_boundary`) already **enforces** `approval_required: true` /
   `approval_granted: false`, executor-independently, *before commit*, **failing closed**.

3. **What the boundary does NOT yet record is *which role* holds the approval authority.**
   The contract proves *that* approval is withheld; it does not bind *who* is entitled to
   grant it. That gap is precisely the O6 executable rule (B2).

The seam for B2 therefore already exists and already fails closed. This is the single most
important scoping fact: **B2 is an extension of an existing, frozen-by-design boundary, not a
new subsystem.**

---

## Design-open item (a) — the exact authority a run must record at the boundary

**Question.** At `waiting_for_human_approval`, must the run record a bare **role identity**,
or a **role→authority binding**?

| Option | What the run records | Pros | Cons |
|---|---|---|---|
| **A1 — role identity only** | `approval_authority.role: approval` | Smallest possible field; trivially valid | The contract cannot tell whether *that* role is entitled to approve without the model; an approval attributed to a role that does **not** hold approval authority still passes. Fails the P7 test. |
| **A2 — role→authority binding, model-versioned** *(recommended)* | the role, the authority it claims (`approval`), and the **model version** it conforms to: `approval_authority: {role: approval, authority: approval, model_version: 0.1.0}` | The record is self-describing and answerable (P5/Clarification B); the contract can reject a role that does not hold approval authority; carries provenance (P8) and version (P9); no heavier than one small map | One extra field and a version pin the run must carry |
| **A3 — full role table embedded per run** | the entire role→authority matrix inline | Maximally self-contained | Duplicates the model into every run; drift risk; violates P13 (machinery beyond need) |

**Recommendation: A2.** Record the **role that holds approval authority plus the model
version the run binds to** — a role→authority binding *by reference*. This is the minimum
that makes the executable rule meaningful: the contract can reject a run whose recorded
approval role is not an approval-authorized role in that model version, and the run carries a
versioned, answerable statement of *who was entitled to cross the boundary*. A1 is rejected
because it cannot catch the exact failure P7 exists to prevent (approval attributed to a role
without approval authority). A3 is rejected under P13 (do not copy the model into every run).

**Founder ruling needed:** confirm A2, and confirm the field name/shape (`approval_authority`
with `{role, authority, model_version}`) before B2 pins a contract version.

---

## Design-open item (b) — where the executable rule lives

**Question.** Does B2 live in the existing **trace/manifest output contracts**, or in a **new
orchestration gate**?

| Option | Location | Pros | Cons |
|---|---|---|---|
| **B-i — extend the completion output contract** *(recommended for Partial)* | add the authority check to `human_authority` in `trace_completion.py` | Reuses the *exact* P7 seam; already enforced executor-independently **pre-commit**; already fails closed; adds one field + one check; no new artifact, no new tool | Couples authority-model conformance to the traceability workstream's contract; the completion contract is version-pinned, so this is a deliberate `task_version` bump |
| **B-ii — new orchestration authority gate** | a gate in `orchestration/gates.py`, checked in `_terminal()` before the halt | Keeps the completion contract about *completeness*; authority is arguably a *coordination* concern; workflow-independent | New gate = new surface; the engine deliberately "validates no task output"; the gate must read the model; larger change to a frozen coordinator |
| **B-iii — record in the run manifest + consistency rule** | `manifest.yaml` + a `RUN_MANIFEST_SCHEMA` rule | Central, machine-indexed | Manifest is runtime-owned and *mutable*; a governance assertion belongs in an immutable, task-owned record, not runtime control state (cf. WF021) |

**Recommendation: B-i for Partial, with B-ii recorded as the likely 0.5 home.** The completion
contract is already the structural P7 boundary, already runs for every executor before commit,
and already fails closed — so B-i is the smallest change that satisfies "one executable rule."
B-ii is the cleaner long-term architecture *if* authority conformance should be a
workflow-independent coordination gate (a natural question for 0.5 O4 "challenge routing"),
and is recorded here so the founder can choose the trajectory now rather than be surprised
later. B-iii is rejected: an authority assertion must not live in mutable runtime control
state.

**Founder ruling needed:** confirm B-i as the Partial home, and acknowledge the `task_version`
bump to `TASK-TRACE-0003` / its contract. Optionally signal whether B-ii is the intended 0.5
destination so B1's descriptive model is written toward it.

---

## Design-open item (c) — vacancy / succession / escalation: runtime vs descriptive

**Question.** For Partial, which parts of the completed model are **executable** at runtime,
and which stay **descriptive**?

**Recommendation.** For **Partial**, exactly **one** thing is executable: the
**approval-authority binding** (B2). **Vacancy, succession, escalation, and transfer remain
descriptive** in B1. Rationale: the exit bar is "descriptive model + *one* executable rule";
P13 forbids building governance machinery before it is justified; and 0.5's O4 (durable
stewardship / challenge routing) is the ratified milestone that *operationalizes* O6 — so
runtime succession/escalation is that milestone's work, not this one.

**One forward seam, recommended but not built now.** Because A2 makes the run record the
**model version** and the **role**, a *future* check can reject a run whose recorded approval
role is marked **vacant** or **superseded** in that model version — with no change to what the
run records. B1 should therefore define vacancy/succession/escalation *precisely enough to be
machine-checkable later*, while B2 checks only the binding today. This keeps Partial minimal
and 0.5 cheap.

Options weighed:
- *(c-1)* keep all four descriptive, build only the binding check — **recommended**.
- *(c-2)* also make **vacancy** executable now (reject a run binding approval to a vacant
  role). Deferred: adds a model-state read and a second rule; beyond the "one rule" bar; P13.
- *(c-3)* make escalation executable now. Rejected: escalation routing is O4 (0.5) by the
  ratified roadmap.

**Founder ruling needed:** confirm c-1 (only the binding is executable for Partial;
vacancy/succession/escalation described so as to be checkable later).

---

## Recommended scope (one paragraph)

Deliver **B1** as a PROPOSED governance document that completes the five ratified roles with
transfer, vacancy, escalation, succession, and the institutional-vs-individual distinction —
written precisely enough that vacancy/succession become machine-checkable *later*. Deliver
**B2** as **one** executable rule at the existing P7 boundary: the reasoning-run completion
record gains an `approval_authority` binding (**role + claimed authority + model version**,
option A2), and the completion output contract (**option B-i**) rejects, failing closed, any
run whose recorded approval role does not hold approval authority in the referenced model
version. Everything else about vacancy/succession/escalation stays **descriptive** for Partial
(**option c-1**). Evidence (**B3**): the rule passes on a conformant run and rejects a
mismatched-authority run — demonstrated by the prototype in `ecf-wt-o6`.

## Alternatives explicitly weighed and set aside
- Recording bare role identity (A1) — cannot catch the P7 failure mode.
- A new orchestration gate now (B-ii) — cleaner but larger; better fitted to 0.5 O4.
- Making vacancy/escalation executable now (c-2/c-3) — exceeds the one-rule bar; P13.

## Exact founder rulings still needed before build
1. **(a)** Adopt **A2** and confirm the `approval_authority: {role, authority, model_version}`
   shape.
2. **(b)** Adopt **B-i** as the Partial home; accept the `TASK-TRACE-0003` contract
   `task_version` bump; optionally confirm **B-ii** as the 0.5 destination.
3. **(c)** Adopt **c-1**: only the approval-authority binding is executable for Partial.
4. **Ownership:** confirm the Governance Plane owner (Program Steward WS-0 per PROGRAM_0.4)
   ratifies B1 as a T-class governance document, and who is the accountable authority for the
   authority *model* itself (institutional authority — see B1 §6).

---

## Metadata
| Field | Value |
|---|---|
| Owner (proposing) | Track B owner (O6) |
| Change class | T1 working proposal → B1 ratification is a governance-doc change (see B1) |
| Derives from | [PROGRAM_0.4](PROGRAM_0.4.md) Track B; [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md) 0.4.0 |
| Serves | O6 / P7 (indestructible responsibility) |
| Cross references | [PROPOSAL_O6_B1_MODEL](PROPOSAL_O6_B1_MODEL.md) · [PROPOSAL_O6_B2_RULE](PROPOSAL_O6_B2_RULE.md) · [PLATFORM_GOVERNANCE](PLATFORM_GOVERNANCE.md) · [PLATFORM_PRINCIPLES](PLATFORM_PRINCIPLES.md) |
