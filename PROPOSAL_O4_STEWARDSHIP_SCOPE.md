# PROPOSAL_O4_STEWARDSHIP_SCOPE — Track B scope workshop (O4: durable stewardship & challenge routing)

> **Status: RATIFIED (Founder, 2026-07-16) — governance classification ruled T4.** Nothing below is ratified. This document
> is the Track B scope workshop for [PROGRAM_0.5](PROGRAM_0.5.md) (milestone 0.5.0), covering
> the four design-open items the kickoff assigned to it. Per the program's own instruction,
> it **opens with the governance-classification question — the 0.2.0 model bump lands
> nowhere until that ruling is made.**
>
> Obligation: **O4 — durable stewardship & challenge routing** (P5 answerability ·
> Clarification B challenge routing · Clarification C institutional continuity).
> Exit bar target: **Partial**. Plane: Governance (docs) + Control (runtime).
>
> Evidence spike: branch `feature/0.5-o4-stewardship` (worktree `ecf-wt-o4`), commit
> `64401ae` — **prototype, not merged, not ratified**; spike tests 23/23; full ECF
> regression **898 passed, 0 failed**. The live authority model (0.1.0) and every frozen
> contract are untouched.

---

## 1. GOVERNANCE CLASSIFICATION — is the 0.2.0 bump constitutional (T5) or a T-band mechanism change?

**RULED (Founder, 2026-07-16): T4 mechanism change** under the ratified model's own change process — NOT a constitutional amendment. The bump is unblocked. The question: O6 was handled as a
**T5 constitutional amendment** (founder override, [PROGRAM_0.4](PROGRAM_0.4.md)) because it
touched P7. Does binding *new* authorities (`ownership` → `stewardship_transfer`;
`accountability` → `challenge_disposition`) into the ratified model **re-touch P7** — the
constitutional amendment path, with the Root Governance Primitive at full ceremony and
Anti-Capture applied — or is it a **T-band mechanism change under the ratified model's own
change process**?

Both readings are presented at full strength. Neither is a straw man.

### 1.1 Reading A — constitutional (T5 amendment path)

1. **The 0.4 override is precedent, and its terms cover this change.** The founder's ruling
   was explicit that *both* halves of O6 — "the B1 model *and* the B2 executable rule" — were
   constitutional, "because it completes and hardens **P7 (indestructible responsibility)**,
   part of the entrenched core" ([AMENDMENT_O6](AMENDMENT_O6_RESPONSIBILITY_AUTHORITY.md)
   header; [PROGRAM_0.4](PROGRAM_0.4.md) governance override). The authority model
   (`tools/authority_rule/authority_model.py`) is the *ratified projection of Doctrine E* —
   the amendment's own words call it "the ratified role→authority table." Changing the
   content of a constitutionally-ratified table is changing what the constitution's
   projection says. If approval→approval needed T5, symmetric treatment says
   accountability→challenge_disposition does too.
2. **The new bindings define the operative meaning of constitutional clauses.** Clarification
   B says a challenge must reach "an accountable authority." *Which role that is* — deciding
   that `accountability`, not `ownership` or `approval`, answers challenges — is
   constitutional interpretation, not mechanism. Likewise, deciding who may authorize a
   stewardship transfer decides how E.2's "authority authorizing the transfer" is filled in.
   Getting either wrong mis-wires the constitution at runtime.
3. **Anti-underclassification presses upward.** PLATFORM_GOVERNANCE's safeguards:
   "**Presumption of higher tier** when two tiers are plausible" and "**effect-over-form** —
   'editorial/cleanup/temporary/operational' labels do not lower the tier." Two tiers are
   plausible here by construction (this section exists); the presumption resolves to T5.
4. **Overlay E1 arguably fires, and toward the Founder.** The vacancy mechanism routes
   challenges to the institutional fallback — the **Founder** under Genesis. The proposer's
   chain of authority ends at the same office that gains runtime disposition authority over
   challenges during any vacancy. Under E1 the beneficiary "may not be sole classifier, sole
   reviewer, or ratify alone"; during Genesis the honest mitigation is the AMENDMENT_O6 §4
   pattern — disclose, and fold into the Independent Reaffirmation Obligation — which is a
   *constitutional-amendment* pattern, suggesting the amendment path is the honest venue.
5. **AMENDMENT_O6 §7 planned this moment as a reconsideration trigger.** "O4 (0.5) trigger.
   When O4 operationalizes vacancy/succession/escalation routing, **E.7's
   descriptive/executable line is revisited**." Under the ratified interpretive clauses,
   reconsideration means the decision **re-enters the same cycle** — and Doctrine E's cycle
   is T5.

### 1.2 Reading B — T-band mechanism change (T4, under the ratified model's own change process)

1. **The Change-Class Doctrine classifies by normative reach, and the reach here is a
   schema.** No constitutional text changes: PRINCIPLES, GOVERNANCE, and GLOSSARY are
   untouched; no principle, clarification, doctrine, or term is added, weakened, or
   reinterpreted. What changes is a versioned role→authority table and the contracts that
   consult it. The **T4 band exists for exactly this**: "canonical standards,
   **schemas/contracts**, … **ownership rules**, compatibility" — with its own heavy process
   (ADR + independent technical review + migration/compat analysis + accountable
   architectural approval).
2. **Doctrine E already decided the constitutional content; O4 only mechanizes it.** The new
   bindings are *projections of ratified text*, not new decisions: E.2 already says a
   transfer is "a recorded act … the authority authorizing the transfer" (→
   `stewardship_transfer` held by the continuous maintainer role, `ownership`); Clarification
   B + E.4 already say a challenge reaches *the accountable authority* — and P5's ratified
   role list *defines* `accountability` as "who must answer for its continued validity or
   initiate reconsideration" (→ `challenge_disposition`). The constitution answered *who*;
   0.2.0 writes that answer into the table. A projection that merely transcribes ratified
   semantics does not re-open them.
3. **The ratified amendment itself pre-authorized this work — twice, at the T-band.**
   (a) E.4, verbatim: "Escalation *routing at runtime* is **deferred to O4 (0.5)**; this
   doctrine only names the targets **so O4 can route them**." (b) E.7: transfer, vacancy,
   escalation, succession "are **operationalized by O4 (0.5)**." (c) The controlling
   precedent for *how* pre-authorized runtime work lands is ratification item 8: the B2 rule
   landed in `trace_completion.py` as "**a T4 contract change**," performed downstream and
   founder-reviewed — the constitution amends once; the mechanisms it authorizes land at T4
   under that authorization (exactly how the 0.4.0 workflow migration record reads:
   "Authorized by AMENDMENT_O6 ratification item 8 … T4 landing"). E.7's "for 0.4.0, exactly
   one provision is enforced" is *time-scoped by its own words* — enforcing more at 0.5
   **fulfills** the doctrine; it does not amend it.
4. **The 0.4 override's stated reason no longer holds.** AMENDMENT_O6 §0 justified T5 because
   "**P7 is presently under-determined**" — the constitution did not yet say what prevents
   orphaning. The amendment *fixed that*. O4 operates inside a now-determined P7; the
   condition that forced 0.4 upward is spent. Precedent transfers with its rationale, not
   past it.
5. **Overlays, honestly examined, do not escalate.** **E2** does not fire: the change is
   oversight-*strengthening* (it adds fail-closed enforcement of vacancy visibility and
   challenge disposition; removes nothing). **E3** does not fire (no legitimacy condition
   weakened; independent challenge is *implemented*, not abolished). **E1** (Founder-as-
   fallback) adds **no authority beyond what Clarification C already grants
   constitutionally** — the fallback routing is the ratified text executing; the conflict was
   disclosed and mitigated in AMENDMENT_O6 §4 and is carried in the standing Reaffirmation
   Obligation. Re-litigating it at T5 each time the ratified fallback is *mechanized* makes
   the amendment ceremony a toll on implementing the constitution.
6. **Proportionality (P13) is itself a ratified interpretive clause.** "Governance burden
   must be proportional to consequence." If every additive projection of ratified doctrine
   re-enters T5, amendment becomes the default change process and the T-ladder below it is
   dead letter — precisely the bureaucratic accretion P13 exists to forbid.

### 1.3 Recommendation *(one line, then the caveats)*

**Recommend Reading B: classify the 0.2.0 bump as a T4 Standard/Architecture change executed
under the ratified model's own change process, pre-authorized by Doctrine E (E.4/E.7) —
with E1 disclosed and carried exactly as in AMENDMENT_O6 §4 — and record the classification
act itself as challengeable. RULED T4 (Founder, 2026-07-16) — until this ruling, the 0.2.0 bump landed nowhere
(not on develop, not in any release) until ruled.**

Caveats recorded for the ruling:

- The **presumption-of-higher-tier** safeguard (Reading A, point 3) is real ratified text and
  the strongest single argument against this recommendation. The response is that the
  presumption applies when two tiers are *plausible on the merits*; §1.2 argues T5 is not, once
  E.4/E.7's explicit pre-authorization is read. The founder is the Change Classification
  Authority under Genesis and owns that judgment.
- **If the founder rules Reading A**, scope does not change — the same §2–§4 content is
  carried by an `AMENDMENT_O4_*` document through the seven-stage cycle at T5 (old/new text,
  impact analysis, disposition `Ratified (Genesis)`, folded into the Reaffirmation
  Obligation), and the runtime landing remains a downstream T4 step on the AMENDMENT_O6
  item-8 pattern. Cost: one amendment document and its ceremony; benefit: symmetric precedent
  with 0.4.
- **Either way**, the §7-trigger note (Reading A, point 5) should be honored cheaply: when
  0.2.0 lands, Doctrine E's E.7 paragraph gains a Decision-history annotation in
  PLATFORM_GOVERNANCE recording that the O4 trigger fired and *which* provisions are now
  machine-checked. Recording a fired trigger in Decision history preserves the
  reconsideration record; whether that annotation is T0 (records a fact, changes no meaning)
  or must ride an amendment is part of the same ruling.

---

## 2. Authority model 0.2.0 — DRAFT deltas + compatibility note (first exercise of O10 semantics)

### 2.1 Exact proposed deltas (`tools/authority_rule/authority_model.py`)

```python
MODEL_VERSION = "0.2.0"                                        # was "0.1.0"

_AUTHORITY_BINDINGS = {
    "authorship": frozenset(),                                 # unchanged
    "approval": frozenset({"approval"}),                       # unchanged (0.1.0)
    "ownership": frozenset({"stewardship_transfer"}),          # NEW at 0.2.0
    "accountability": frozenset({"challenge_disposition"}),    # NEW at 0.2.0
    "responsibility_acceptance": frozenset(),                  # unchanged
}
```

Plus (from §4): `_ROLE_STATE` is superseded by the recorded-acts ledger, and the module gains
`ESCALATION_TARGETS` (E.4 named targets: every role → `founder_genesis` under Genesis) and
`resolve()` (Clarification C: never resolves to nowhere). `ROLES` is **unchanged** — no sixth
role; stewardship is an *authority held by* `ownership`, not a role (P5's five-role set is
ratified and closed at this tier).

Semantics of the two new authorities:

| Authority | Held by | Grants exactly | Constitutional source |
|---|---|---|---|
| `stewardship_transfer` | `ownership` | being the *authorizing authority* of a recorded transfer act (E.2) for continuous roles; never self-transfer without the no-gap conditions | E.2; P5 ("who currently maintains it") |
| `challenge_disposition` | `accountability` | being the *accountable recipient* who records a challenge's disposition (by evidence, P4) | Clarification B; E.4; P5 ("who must answer for its continued validity") |

### 2.2 Compatibility note *(the version-evolution discipline the kickoff asked to double as O10's first exercise)*

**What a 0.1.0 consumer may assume** (and 0.2.0 preserves): the five ratified roles, exactly;
`approval` holds `approval` and no other role does; `holds_authority()` fails closed on any
model version other than the one the module implements; unknown roles hold nothing.

**What changes at 0.2.0:** two roles that held *no* authorities now hold one each. **Additive
only** — no binding is removed or moved; the approval boundary's behavior for conformant
runs is bit-identical. Hence a **minor** bump (0.1.0 → 0.2.0), consistent with the semver
discipline the runtime schemas already use.

**Migration semantics — strict pinning, lockstep landing, history untouched:**

- **Pinning stays strict** (a run binds exactly one `model_version`; the checker rejects all
  others). We considered a compatible-versions set (`{"0.1.0","0.2.0"}`) and **recommend
  against it for 0.5**: the fail-closed single-version pin is the simplest possible
  compatibility contract, and the entire migration surface is inside one repo (below), so a
  window buys nothing and weakens the pin.
- **The live consumer moves in lockstep by construction.** `trace_completion.py` (contract)
  imports `MODEL_VERSION` dynamically and the executor emits it dynamically — both follow the
  model in the same commit. The bump therefore lands as **one atomic change** in `ecf`:
  model 0.2.0 + the §4 runtime checks + the migration surface below.
- **Known hardcoded `"0.1.0"` surfaces that must migrate in the same change** (found by
  audit of the worktree): `tasks/traceability/TASK-TRACE-0003-finalize-reasoning-run.md`
  (two YAML examples), `tools/task_runner/tests/test_trace_contracts.py` (binding-shape
  assertion), `tools/task_runner/tests/test_trace_executors.py` (executor-emission
  assertion), `tools/authority_rule/tests/test_authority_rule.py` (fixture). Per the
  established 0.4 pattern this rides a `TASK-TRACE-0003` `task_version` bump
  (`0.4.0 → 0.5.0`) and a `WF-REASON-0001` workflow bump with a migration table — the same
  ceremony the v0.3.0→v0.4.0 O6 landing used.
- **Historical runs are history (P14/P9):** runs that recorded `model_version: "0.1.0"`
  remain valid *as recorded* and are never rewritten; new runs record `"0.2.0"`. Replaying an
  old run under the new contract is a version error **by design** — that is the pin working,
  not a defect.
- **O10 mapping**, element by element: **version** = `MODEL_VERSION`, semver, minor-for-
  additive; **compatibility rules** = the consumer-assumption list above; **migration
  policy** = lockstep atomic landing + enumerated hardcoded surfaces + history untouched;
  **identity semantics** = the model is identified by (module path, `MODEL_VERSION`);
  **validation boundary** = `holds_authority()`/`resolve()` fail-closed; **change process** =
  whatever §1's ruling selects. This table is offered to the H1 background lane as the first
  concrete instance of the full model contract.

---

## 3. Challenge artifact + disposition record (proposed schemas)

Design intent: **Clarification B end-to-end** — a challenge *reaches* an accountable
recipient and *receives* a recorded disposition; **Clarification C** — vacancy routes to the
institutional fallback, never to nowhere; **P4** — disposition by evidence; **P14** — the
record is indelible.

### 3.1 Challenge artifact (`challenge.yaml`)

```yaml
schema_version: "0.1.0"           # challenge-record schema (not the authority model's)
challenge_id: CHG-20260716-0001   # CHG-<date>-<seq>, unique platform-wide
challenges:                       # binds to EXACTLY ONE identified target (P8)
  kind: run | decision | artifact
  ref: RUN-REASON-20260715-0001   # run_id | decision id (ADR/disposition ref) | artifact path
  target_version: "0.4.0"         # optional; pins the challenged state (P9)
challenger: {actor: "...", role: authorship}   # ANY actor may challenge (P4 is not gated on rank)
grounds: >                        # what is contested, falsifiably stated
  ...
evidence: [ ... ]                 # refs; may be empty at filing — disposition may not be
routing:                          # WRITTEN BY THE ROUTER, not the challenger
  accountable_role: accountability
  authority: challenge_disposition
  model_version: "0.2.0"
  holder_state: active | vacant
  effective_recipient: accountability | founder_genesis   # NEVER empty (Clarification C)
  degraded: false                 # true iff routed via the institutional fallback
status: open | disposed
```

### 3.2 Disposition record (`disposition.yaml`, sibling of the challenge)

```yaml
schema_version: "0.1.0"
challenge_id: CHG-20260716-0001
disposition: upheld | upheld_with_constraints | rejected | deferred | withdrawn
disposed_by:
  recipient: accountability | founder_genesis   # must equal routing.effective_recipient
  authority: challenge_disposition
  model_version: "0.2.0"
evidence: [ ... ]                 # NON-EMPTY — settled by evidence, not opinion (P4)
rationale: "..."
reconsideration:                  # stage 7; REQUIRED when upheld*
  required: true
  trigger: "..."                  # what the upheld challenge obliges (re-entry, P14)
recorded_at: "2026-07-16T..."
```

Rules the schemas encode (all fail-closed, all demonstrated in the spike):

- **Reach**: a challenge that cannot name its target, or names no grounds, is rejected at
  filing — it never enters "routed to nobody" limbo. Routing resolves the accountable office
  through the *recorded role state* (§4); vacancy yields `effective_recipient:
  founder_genesis` with `degraded: true` — visible, never silent (E.3).
- **Disposition**: only the routed `effective_recipient` may dispose; an active recipient
  must hold `challenge_disposition` in the pinned model; evidence must be non-empty; the
  vocabulary is the challenge-scope projection of the Root Primitive's stage-5 set.
- **Indelible**: one disposition per challenge, ever. A second disposition attempt is
  rejected; changing an outcome means a **new challenge** re-entering the cycle
  (corrigibility by re-entry — the ratified interpretive clause, verbatim).
- **Where they live** (proposed): run-bound challenges under
  `runs/<run_id>/challenges/CHG-*/{challenge.yaml,disposition.yaml}` in the run store;
  non-run targets (artifacts, standing decisions) under a repo-level `challenges/` registry
  in `ecf`. Both write-once. The disposition is a first-class run output the same way the
  0.3 approval halt is — recorded, not conversational.

---

## 4. Vacancy / transfer / escalation — the runtime design (making `_ROLE_STATE` real)

0.4 shipped `_ROLE_STATE = {r: "active" for r in ROLES}` and `role_is_active()` as a
declared-but-unconsulted seam. 0.5 makes the seam **derive from recorded acts and be
consulted at the boundaries**, building directly on the `feature/0.4-o6-authority` prototype
(whose model/check split and fail-closed idiom this design keeps; that branch's content is
already on `develop` as the merged standalone module).

### 4.1 State machine (per role)

```
            record_transfer (E.2: outgoing + ACCEPTING incoming + authorizing authority
                             + effective moment; a gap-leaving transfer is INVALID
                             and is NOT recorded)
   ┌──────────────────────────────────────────────────────────────┐
   ▼                                                              │
 ACTIVE(holder) ── record_vacancy (E.3: reason + recorder + escalation target;
   ▲                               never silent) ──► VACANT(degraded,
   │                                                  escalates → founder_genesis)
   └── record_transfer seating an accepting incoming holder ◄─────┘
        (vacancy→active REQUIRES acceptance; there is no silent re-seat)
```

- **State is derived, never asserted**: the only writes are append-only recorded acts
  (transfer / vacancy); current state is a fold over history (P8: the chain is unbroken;
  P14: acts are never deleted). Genesis initial condition: every office's holder is the
  standing institutional authority (`founder_genesis`) until a recorded act seats another.
- **Who may transfer**: the act must name its authorizing authority. In model 0.2.0 that is
  the holder of `stewardship_transfer` (= `ownership`), with the institutional authority
  (Founder under Genesis) always able to authorize as backstop — this is Delegation/E.6
  executing, not a new power. Self-benefiting transfers remain subject to overlay E1 at the
  governance layer (the runtime records; the classification challenge is a human act).
- **Persistence** (production form, post-ruling): an append-only
  `tools/authority_rule/role_acts.yaml` (or `governance/role_acts.yaml`) in `ecf`, loaded at
  check time; the spike models it as the in-memory `StewardshipLedger` so the semantics are
  test-proven before a storage format is ratified.

### 4.2 What a vacancy does at the approval boundary

The 0.4 rule (`_check_approval_authority_binding` in
`ecf/tools/task_runner/output_contracts/trace_completion.py`) keeps working unchanged for an
**active** office. The 0.5 extension consults the ledger:

- **Active office + conformant binding** → pass (0.4 behavior, bit-identical).
- **Active office + a binding that *claims* escalation** → **reject** (P2: the record must be
  honest about role state; a spurious degradation claim is a lie in the provenance).
- **Vacant office + silent binding** → **reject, fail closed** (E.3: vacancy is recorded,
  never silent — the run may not pretend the office is staffed).
- **Vacant office + disclosed escalation** (`escalation: {target: founder_genesis, reason:
  vacancy}`) → **pass, visibly degraded**: the run still halts at
  `waiting_for_human_approval` (P7 untouched — nothing auto-approves, ever); what changes is
  *who the halt is answerable to*, which now escalates to the institutional fallback instead
  of dangling. Never to nowhere; never silently.
- The same `resolve()` primitive drives challenge routing (§3), so vacancy behaves
  identically at both boundaries — one seam, two consumers.

### 4.3 Escalation (E.4 named targets, routed)

`ESCALATION_TARGETS = {role: founder_genesis for role in ROLES}` under Genesis — the model
*routes* the targets Doctrine E *named*, exactly the division of labor E.4 prescribed. The
token names an **office, not a person** (actor-neutral); End-of-Genesis re-points it through
the constitutional process, not through code.

### 4.4 Spike status (evidence, not a landing)

| Item | Value |
|---|---|
| Branch / worktree | `feature/0.5-o4-stewardship` · `C:\Dev\ecf-wt-o4` — **not merged; never pushed** |
| Spike commit | `64401ae` — `tools/authority_rule/{stewardship_model.py, check_stewardship.py, tests/test_stewardship_draft.py}`, all headed **PROTOTYPE ONLY — NOT MERGED, NOT RATIFIED** |
| Live 0.1.0 model / frozen contracts | **untouched** (a spike test asserts `authority_model.MODEL_VERSION == "0.1.0"` still) |
| Spike tests | **23/23 pass** — 0.2.0 deltas additive; version-pin fail-closed; transfer no-gap (gap-leaving transfer invalid *and unrecorded*); vacancy recorded/degraded/never-nowhere; boundary rejects undisclosed vacancy and spurious escalation; challenge routes to `accountability`, falls back to `founder_genesis` when vacant; disposition requires evidence + correct recipient; second disposition rejected (indelible); unrouted challenge cannot be disposed |
| Full ECF regression | **898 passed, 0 failed** (`python .claude/scripts/run_tests.py`, 9 packages) |

---

## 5. The O4 Partial bar — confirm, with three refinements

The kickoff's proposed bar: *"model 0.2.0 ratified + vacancy fallback enforced at runtime +
one challenge routed to a recorded disposition."* **Confirmed**, refined for testability:

1. **"Model 0.2.0 ratified"** means: disposed through **whichever change process §1's ruling
   selects** (T4 under the model's own process, or T5 amendment), landed atomically with the
   §2.2 migration surface (task/workflow version bumps included), and **live at the
   completion boundary** — not merely merged. (0.4's lesson: "merged standalone but inert"
   left O6 not-Partial-live for a stretch; the bar should say *live* so 0.5 cannot re-create
   that gap.)
2. **"Vacancy fallback enforced at runtime"** means, concretely: with a role recorded vacant,
   the completion contract **rejects an undisclosed-vacancy run** (negative fixture) and
   **accepts a disclosed-escalation run** (positive fixture), and challenge routing resolves
   `effective_recipient: founder_genesis` with `degraded: true` — all against the *recorded*
   role-state store, not an in-test stub.
3. **"One challenge routed to a recorded disposition"** means **one real challenge**: bound
   to an actual run or artifact of the platform (e.g., an assumption in the 0.3/0.4 reasoning
   runs, or — coordinating with Track A — the first canonicalized artifact), reaching the
   accountable office, and receiving an evidence-bearing disposition record that persists in
   the run store / registry. A synthetic fixture proves the mechanism (spike already does);
   the bar's exercise must be real, mirroring O3's "one real approved recommendation
   transformed."

Explicitly **out of scope for Partial** (deepening targets, recorded so their absence is a
gap and not an omission — P2): succession *ordering* rules beyond transfer/vacancy (E.5's
ordered next-holder rule); escalation beyond one hop; challenge SLAs/timeouts;
multi-holder offices; the persistent `role_acts.yaml` storage format ratification if the
founder prefers to hold it for independent review.

---

## Metadata

| Field | Value |
|---|---|
| Status | **RATIFIED (Founder, 2026-07-16)** — §1 ruled **T4**; §2–§5 ratified as scoped; Track B authorized to build |
| Change class (this document) | T1 operational (a scope-workshop proposal); the *changes it proposes* classify per §1's ruling |
| Owner (proposing) | Track B owner (O4) |
| Evidence | Spike `ecf-wt-o4` / `feature/0.5-o4-stewardship` @ `64401ae` — 23/23 spike tests; 898/0 full regression; live model + frozen contracts untouched |
| Derives from | P4 · P5 · Clarifications B, C · Doctrine E (E.2–E.4, E.6, E.7) · Root Governance Primitive · Anti-Capture · Genesis Authority Doctrine · [PROGRAM_0.5](PROGRAM_0.5.md) Track B kickoff rulings |
| Cross references | [AMENDMENT_O6_RESPONSIBILITY_AUTHORITY](AMENDMENT_O6_RESPONSIBILITY_AUTHORITY.md) · [PROGRAM_0.4](PROGRAM_0.4.md) · [PLATFORM_GOVERNANCE](PLATFORM_GOVERNANCE.md) · [PLATFORM_PRINCIPLES](PLATFORM_PRINCIPLES.md) · [PLATFORM_GLOSSARY](PLATFORM_GLOSSARY.md) |
