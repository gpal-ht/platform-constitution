# PLATFORM_GOVERNANCE

> Governance is the **revisable mechanism layer** that satisfies the constitutional
> invariants. It answers *"how do we mechanize the invariants — revisably?"* It sits
> between [PLATFORM_PRINCIPLES](PLATFORM_PRINCIPLES.md) (what must always be true) and
> [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md) (what must become true next).
>
> **Status: partially ratified.** The root governance primitive and its interpretive
> clauses are ratified. Three areas — genesis authority, anti-capture entrenchment, and the
> final change-class ladder — remain **`Draft — Open Question`** from Workshop 4 and are
> marked as such. They are not invented here.

---

## The Root Governance Primitive *(Ratified)*

> **Every consequential change to an authoritative artifact must pass through a declared
> governance cycle: scope & authority → proposal → evidence → independent challenge →
> authorized disposition → versioned effect → monitored reconsideration.**

Governance is not many processes; it is **one cycle applied at many scopes**, differing
only in *who is the accountable authority* and *what evidence threshold* the scope demands.

### The seven stages — the questions every legitimate governance act must answer

1. **Scope & authority** — What is changing, and who has authority to decide? *(Routing
   before evaluation: classify the artifact, the change class, the evidence threshold, and
   the empowered authority. Without this, a constitutional change can be smuggled through a
   documentation-review path, and adoption can masquerade as authority.)*
2. **Proposal** — What change is being requested?
3. **Evidence** — Why should the change occur?
4. **Independent challenge** — Who tested the proposal rather than merely producing it?
5. **Authorized disposition** — Was it accepted, accepted with constraints, accepted
   experimentally, deferred, rejected, superseded, withdrawn, expired, or reaffirmed?
6. **Versioned effect** — What authoritative state changed, from which version to which?
7. **Monitored reconsideration** — Under what evidence, conditions, or triggers must this
   decision be revisited?

### Interpretive clauses *(Ratified)*

- **Corrigibility by re-entry.** Supersession, reversion, and reaffirmation do not use a
  separate process. A reconsideration trigger causes the existing decision to re-enter the
  same cycle as a new proposal, preserving both corrigibility (P14) and history.
- **Actor-neutral.** The primitive constrains *roles, evidence, independence, authority,
  and record* — never the nature of the actors. It is valid whether roles are performed by
  a human author, an AI engineering agent, a review council, a regulated institution, a
  formal-verification system, or a hybrid authority.
- **Proportionality.** Governance burden must be proportional to consequence, while every
  consequential change preserves the full logical cycle. A typo correction and a Root
  Principle amendment share the seven-stage logic and share nothing of the ceremony.
- **Role separation (composes with P6).** One actor may hold multiple roles, subject to
  limits: proposer and evidence-producer may be the same; proposer and sole independent
  challenger may not; generator and sole ratifier may not; an accountable authority may
  rely on reviewers but cannot hide responsibility behind them.

### Trace to the constitution

```
INTELLIGIBLE   → proposal explicit · evidence declared · disposition recorded · effect legible
CHALLENGEABLE  → independent challenge · authority declared · disposition answerable · reconsideration possible
REPRODUCIBLE   → inputs/evidence retained · prior & resulting states versioned · procedure recorded · supersession preserves history
```

The primitive is the smallest reusable cycle that operationalizes all three pillars. It is
**not** a new constitutional principle; it is the core governance mechanism derived from
them.

---

## The Governance Admission Test *(Ratified)* — governance's equivalent of P12

A proposed governance mechanism is admitted only if it names **which stage of the cycle it
instantiates or strengthens**, and demonstrates measurable constitutional benefit.
Otherwise **P13** applies: it is presumed unnecessary. This is how governance avoids
becoming a catalogue.

| Mechanism | Root-cycle function |
|---|---|
| ADR requirement | Proposal · evidence · disposition · versioned effect |
| Reviewer registry | Independent challenge · authority qualification |
| Release approval | Authorized disposition |
| Compatibility policy | Evidence threshold · versioned effect |
| Experiment-promotion process | Entire cycle at standards scope |
| Deprecation policy | Reconsideration · versioned effect |
| Canonical-knowledge review | Evidence · challenge · disposition |
| Branch protection | Enforces independent challenge · authorized disposition |

---

## Reference instance *(Ratified)* — when does an experiment become a standard?

This is the canonical worked example of the cycle at **standards scope**. It is the case
where evidence is most tempting to skip; P3 (nothing canonical by existence) becomes a
decision procedure here.

1. **Scope & authority** — classify the transition *experimental mechanism → canonical
   standard* as a **change in authoritative status**, not a routine edit. Declare the
   artifact, the scope, the governed systems, the empowered authority, the evidence tier
   (High), and compatibility/migration obligations.
2. **Proposal** — define the *normative behavior*, supported/unsupported use cases,
   interfaces, safety properties, compatibility commitments, migration path, known
   limitations, any standard replaced, and enforcement. *(An experiment report describes
   what happened; a standards proposal defines what future work must obey — different
   artifacts.)*
3. **Evidence** — a successful experiment is necessary but usually insufficient. Popularity,
   senior preference, repeated use, one successful implementation, and absence of complaints
   are signals, not sufficient evidence of general validity.
4. **Independent challenge** — reviewers attempt to *invalidate* the promotion claim
   (representativeness, excluded failures, generalization, owner bias, untested
   alternatives, behavior under scale/failure/hostility, migration burden, over-strong
   enforcement, standardizing an implementation where only an interface should be
   standardized). The author cannot be the sole reviewer. Success means challenges and
   dispositions are *recorded*, not that agreement is unanimous.
5. **Authorized disposition** — one of: accepted as standard · accepted as limited standard ·
   continued as experiment · deferred pending evidence · rejected · superseding standard.
   *Continuing experimentation is a legitimate disposition* — this defeats the false binary
   "standardize or fail."
6. **Versioned effect** — record standard identity, version, effective date, scope, status,
   accepted proposal, evidence set, reviews, authority, disposition, compatibility policy,
   any superseded standard, migration window, enforcement start, provenance. The experiment
   remains in history as an experiment; it is not retroactively rewritten.
7. **Monitored reconsideration** — attach review triggers (security incident, repeated
   exception requests, failure rate above threshold, regression, new regulation,
   incompatible platform change, superior alternative, maintenance cost beyond bound,
   scheduled review, invalidated assumption). When a trigger fires, the standard re-enters
   the cycle.

---

## Governance of the platform documents

Applying the cycle and proportionality to this document set. Each row is governed at the
change **tier** below; the **effect overlays** may escalate any change regardless of tier.

| Document | Base tier | Requires independent challenge? | Autonomous update? |
|---|---|---|---|
| PLATFORM_MISSION / VISION / PRINCIPLES | T5 Constitutional | Yes (or Genesis-recorded) | No |
| PLATFORM_GOVERNANCE (this doc) | T5 Constitutional | Yes (or Genesis-recorded) | No |
| PLATFORM_ARCHITECTURE | T4 (T5 if it changes a constitutional definition) | Yes for T5/E-overlays | No |
| PLATFORM_ROADMAP | T2 Roadmap/Capability | On material dissent | Propose only |
| PLATFORM_CAPABILITY_MAP | T2 (status: T1) | On plane/status change | Status updates with evidence |
| PLATFORM_WORKSTREAMS / PARALLELIZATION | T1–T2 | On dependency change | Yes, with evidence |
| PLATFORM_RELEASE_STRATEGY | T4 | Yes | Propose only |
| PLATFORM_GLOSSARY | T3 (definition) / T5 (constitutional term) | On canonical term change | Propose only |
| CURRENT_PROGRAM | T1 Operational | No | Yes, within scope |

---

# Constitutional Governance — Ratified (Genesis)

> Workshop 4 closed. The three doctrines below are ratified under the **Genesis Exception**
> (see §Genesis). They are fully in force and carry a standing Independent Reaffirmation
> Obligation.

## A. Change Classes *(OQ-GOV-003 — Ratified)*

Every change is classified on **two independent axes**. **Tier** (Axis 1) sets the base
process by normative reach; **effect overlays** (Axis 2) modify *who may act* and *what proof
is required*, and apply on top of any tier.

> **Change-Class Doctrine.** The tier of a change is determined by its normative reach. The
> legitimacy constraints on a change are determined by its effects. Neither may be reduced by
> naming, file location, implementation form, or the authority of the proposer.

### Axis 1 — Tiers

| Tier | Scope | Base process |
|---|---|---|
| **T0 Editorial** | wording/format/links; no change to meaning, obligations, authority, ownership, scope | maintainer review + proof meaning is unchanged |
| **T1 Operational** | CURRENT_PROGRAM, status, sessions, sequencing within a ratified capability | delegated authority within recorded scope; traces to a ratified capability |
| **T2 Roadmap/Capability** | maturity, milestones, workstreams, dependencies, exit criteria, capability map | roadmap/program authority + dependency & consistency evidence; recorded dissent |
| **T3 Governance mechanism** | review/approval/admission/delegation/amendment mechanics | trace to a principle + P13 value + cost analysis; independent review if it touches authority/oversight; trial/sunset if evidence incomplete |
| **T4 Standard/Architecture** | canonical standards, schemas/contracts, Plane responsibilities & interfaces, ownership rules, compatibility | ADR + independent technical review + migration/compat analysis + accountable architectural approval. **A Plane add/remove/redefine is always ≥ T4** |
| **T5 Constitutional** | Mission, Vision, Root, Principles, non-goals, anti-capture, Genesis, entrenched provisions, legitimacy conditions, amendment authority, accountable-ownership | formal amendment; old+proposed text; impact analysis; **independent challenge**; permanent dissent/history; cooling-off; heaviest ratification. **No implementation batch may make a T5 change — only propose one** |

*A change is not T0 merely because it is small; escalate if it alters interpretation,
obligations, authority, ownership, or scope.*

### Axis 2 — Effect Overlays (apply to any tier; they add constraints, never replace the base)

- **E1 Self-Dealing** — the proposer/classifier/reviewer/ratifier directly benefits (expanded
  authority, reduced scrutiny/accountability, weaker approval, exemption, protecting a decision
  they own). *Effect:* the beneficiary may propose + give evidence but **may not be sole
  classifier, sole reviewer, or ratify alone**; independent challenge mandatory; conflict
  recorded. *Self-dealing is not "T6" — it is disqualification from unilateral ratification.*
- **E2 Oversight-Reducing** — removes/weakens review, evidence, provenance, accountability,
  thresholds, challenge rights, history retention, or turns a mandatory safeguard optional.
  *Effect:* the **asymmetric burden of proof** applies — the proposer must identify the
  protected safeguard and prove it no longer materially protects a principle (or a replacement
  is equal/stronger). Convenience, cost, speed, or low recent incident frequency are
  insufficient. *Absence of recent failure is not proof a safeguard has no value.*
- **E3 Legitimacy Tripwire** — would abolish independent challenge; let one authority propose+
  review+ratify the same consequential change; erase history/dissent; remove accountable
  ownership; exempt an authority from safeguards binding others; make the Genesis Exception
  reusable; let implementation bypass the Constitution; or weaken the conditions of legitimate
  authority. *Effect:* **no single authority may ratify**; highest process; multiple
  independent accountable authorities; cooling-off; preserved dissent; delayed effect + post-
  change revalidation. *If the legitimacy process does not yet exist, the proposal remains
  unratified.* A tripwire makes unilateral change **constitutionally** impossible, not
  metaphysically impossible.

### Classification authority & anti-underclassification

The proposer submits an initial classification but **does not own the final one** — that
belongs to a distinct **Change Classification Authority**. After Genesis, the classifier must
be **independent of the proposer** for all T5, E1, E2, E3, and disputed T3/T4 changes.

Safeguards against under-classification (classification is by **normative effect**, never by
filename/line-count/document):
- **Presumption of higher tier** when two tiers are plausible.
- **Effect-over-form** — "editorial/cleanup/temporary/operational" labels do not lower the tier.
- **Mandatory impact statement** for every T1–T5 change (what authority/obligation/ownership/
  safeguard/downstream contract changes; who benefits; who bears new risk; which principles).
- **Classification challenge** — any accountable participant may challenge; a disputed change
  cannot ratify until resolved.
- **No fragmentation** — related changes are classified by combined effect.
- **Auditability** — proposed tier, overlays, classifier, objections, final classification are
  permanently recorded.
- **Penalty** — a knowingly under-classified change is **invalid even if implemented**, and its
  effects are reviewed/suspended/reversed.

## B. Anti-Capture Doctrine *(OQ-GOV-002 — Ratified)*

> **Constitutional authority is legitimate only when it remains constrained, independently
> challengeable, historically transparent, and unable to weaken the conditions of its own
> legitimacy through unilateral action.** Actor-neutral: no authority is trustworthy by
> identity, seniority, ownership, intelligence, or prior contribution — only while operating
> through the constitutional process.

Seven ratified rules:
1. **Entrenchment.** The entrenched core (Root Principle; independent review & no
   self-ratification; accountable ownership of consequential decisions; the asymmetric burden;
   preservation of constitutional history; the prohibition on implementation batches modifying
   the Constitution; the anti-capture safeguards themselves) is amendable only under the
   heaviest (T5) process.
2. **Self-dealing prohibition.** *No authority may relax the amendment tier, review requirement,
   or evidentiary burden governing a change from which that same authority directly benefits.*
   (Operationalized as overlay E1.)
3. **Independent challenge.** No consequential (T5 / E-overlay) amendment may be both proposed
   and finally ratified by the same authority acting alone; an independent challenger — not the
   sole beneficiary, not the author of the conclusion, not compellable, able to record dissent
   and require revision/deferral — must review.
4. **Indelible history.** Every constitutional change records prior text, proposed text,
   reason, evidence, affected principles, proposing & reviewing authority, dissent, outcome,
   effective date, and review trigger. *The Constitution must be corrigible, but its history
   must be indelible.*
5. **Legitimacy tripwire.** *No single authority may remove the conditions that make
   constitutional authority legitimate.* (Operationalized as overlay E3.)
6. **Unratified over simulated.** Where genuine independence is unavailable, a proposal remains
   **proposed but unratified** rather than approved through simulated review.
7. **Constrained amendment.** The Constitution is amendable, but the legitimacy of amendment is
   itself constitutionally constrained.

## C. Genesis Authority Doctrine *(OQ-GOV-001 — Ratified)*

> The Constitution originates through one transparent act of founder authority that creates,
> records, and immediately limits that authority. The founding act is valid but exceptional;
> it establishes no permanent right to unilateral rule.

- **The Genesis Exception.** The founding ratification is a single, named, **pre-constitutional**
  act, recorded plainly as *"Founder ratification under the Genesis Exception"* — never as
  independent review, consensus, democratic ratification, inherited authority, or evidence the
  founder was already legitimate. It is legitimate only because, before a constitutional order
  exists, no constitutional process exists to create it. **It applies only to the creation of
  the initial order and is never reusable for later amendments.**
- **Status ladder:** `Draft` (not authoritative) → `Proposed Amendment` (under review) →
  **`Ratified (Genesis)`** (authoritative under founding authority; independent reaffirmation
  outstanding) → `Ratified` (authoritative under the normal process).
- **Independent Reaffirmation Obligation.** When genuine independent challenge first becomes
  possible, the entrenched core undergoes **one** formal reaffirmation cycle (reaffirm /
  reaffirm-with-amendment / partial supersession / defer). It does not reopen every sentence to
  manufacture dissent; it tests whether the founding Constitution survives independent
  challenge. Until then the Constitution binds as `Ratified (Genesis)`; the Genesis history
  remains permanently recorded thereafter.
- **End of Genesis (by condition, not date/version).** Genesis ends automatically when there
  exists at least one additional **human** authority who (1) has accepted constitutional
  accountability, (2) can independently review and record dissent, (3) cannot be revoked merely
  for rejecting a founder proposal, and (4) whose role is recorded through the constitutional
  process. *Does not count:* an AI configured/controlled solely by the founder; a revocable-for-
  disagreement contributor; a comment-only reviewer; a subordinate under delegated instruction;
  a second identity of the same person; ceremonial approval. At that point unilateral founder
  ratification ends and rules 2/3/5 bind fully. **What ends is sole constitutional legitimacy,
  not founder leadership.**
- **Delegation.** Authority may be delegated when explicit and bounded (recording granted
  authority, scope, duration/trigger, permitted/forbidden decisions, accountable owner,
  revocation). *Authority may be delegated; accountability must remain identifiable.* AI
  participants may hold operational authority but **never** independent constitutional authority.
- **Succession.** Transfer requires a recorded process (declaration, identified & accepting
  successor, evidence of understanding, preserved safeguards, independent challenge where
  available, permanent record + dissent, effective date, no authority-gap/dual-sovereignty). **A
  successor receives the office, not freedom from its constraints.** *Genesis Succession*
  inherits the original exception's unresolved legitimacy debt — no new founding exception,
  preventing repeated "re-founding." Post-Genesis succession is a normal T5 amendment.
- **Emergency continuity** may be temporary, narrow, recorded, review-triggered, unable to amend
  entrenched provisions, and unable to make itself permanent. It preserves operations, not
  sovereignty.

## D. The Deliberate-Evolution Rule *(Ratified)*

> **No implementation batch may change the Constitution. It may only propose a constitutional
> amendment.** This is entrenched (Anti-Capture rule 1) and is the line that converts accidental
> evolution into deliberate evolution.

## E. Responsibility-and-Authority Doctrine *(O6 / P7 — Ratified (Genesis))*

> **The five roles of accountability (P5) are complete only when, for each, the constitution
> answers who holds it now, how it transfers without a gap, what is true when it is vacant,
> where a challenge escalates, and who succeeds — and when every individual role is backed by
> an institutional authority that is never vacant (Clarification C). Responsibility so
> constructed is indestructible (P7).**

This doctrine adds **no new role and no new governance cycle**. Each provision is the **Root
Governance Primitive applied at role scope** (Governance Admission Test), strengthening a
named stage rather than creating a parallel process.

**E.1 Point-in-time binding.** At every moment, each consequential decision has a locatable
holder of each role in force at that moment (authorship and approval are *point-in-time*;
ownership and accountability are *continuous*; responsibility-acceptance is *point-in-time,
risk-bearing*). *Approval*'s binding is the one made machine-checkable now (E.7).

**E.2 Transfer (no-gap).** A role changes holder only by a recorded act naming the outgoing
holder, the identified **and accepting** incoming holder, the effective moment, the authority
authorizing the transfer, and preserved history. *P7 constraint:* the incoming holder is
bound at the instant the outgoing holder is released — **there is never an interval with no
holder.** A transfer that would leave a gap is invalid. (Authorship does not transfer; it is
history — P8/P14.)

**E.3 Vacancy (recorded, never silent — P2).** Vacancy is a *state*, not an act. A
consequential decision whose ownership or accountability is vacant is in a **degraded** state
that must be visible and must carry an escalation target. *P7 constraint:* **vacancy of
accountability is never a terminal resting state** — it must resolve to a holder or escalate
to the institutional accountable authority (E.6). Point-in-time roles cannot become vacant
retroactively; history is indelible (P14).

**E.4 Escalation (named targets).** Every role has a **named escalation target** — the
authority a challenge reaches when the current holder is absent, conflicted, or unresponsive
(Clarification B: a challenge reaching no accountable recipient is not a challenge).
Escalation *routing at runtime* is deferred to O4 (0.5); this doctrine only **names the
targets** so O4 can route them.

**E.5 Succession (office, not freedom).** The ordered rule for the next holder, planned
(transfer) or unplanned (vacancy). A **successor receives the office, not freedom from its
constraints** (generalized verbatim from the Genesis Succession doctrine). Succession
preserves the historical chain (P8, P14); it never rewrites who held the role before.

**E.6 Institutional vs individual authority (the indestructibility mechanism).**
**Individual authority** is held by a specific actor at a specific time and *can* become
vacant. **Institutional authority** is the office itself, which persists across holders and
is **never vacant by construction**; when no individual holds it, it rests with the
institution's standing accountable authority — under the current order, the **Founder** under
the Genesis Authority Doctrine, until End-of-Genesis. Every individual role in E.1 has an
institutional backstop; this is the constructive guarantee that closes E.3's "vacancy of
accountability is never terminal" and makes P7 hold. This distinction is already *implicit*
in the Genesis Authority Doctrine (Delegation: "authority may be delegated; accountability
must remain identifiable"; Succession: "office, not freedom"; Emergency continuity:
"preserves operations, not sovereignty"); Doctrine E makes it explicit and names it, widening
nothing. **Actor-neutrality (P7 preamble):** these provisions constrain *relationships*, not
the nature of actors; the Genesis limit is inherited verbatim — an AI may hold *operational*
authority but never *independent constitutional* authority.

**E.7 Executable now vs descriptive (the 0.4 "Partial" line).** For 0.4.0, exactly **one**
provision is enforced at runtime: the **approval-authority binding** (E.1 for the *approval*
role). A reasoning run at the `waiting_for_human_approval` boundary records which role holds
approval authority and the model version it binds to, and the completion contract **rejects,
failing closed, any run whose recorded approval role does not hold approval authority in that
model** — preserving the existing P7 invariant (`approval_required: true` /
`approval_granted: false`). Transfer, vacancy, escalation, and succession remain
**descriptive** here — written precisely enough to become machine-checkable later — and are
operationalized by **O4 (0.5)**. This proportionality is required by P13: no governance
machinery is built before it is justified.

**Trace to the constitution (Admission Test).** E.1 → *scope & authority*; E.2 → *authorized
disposition + versioned effect*; E.3 → *monitored reconsideration*; E.4 → *independent
challenge reaches an authority*; E.5 → *versioned effect preserving history*; E.6 → authority
*constrained + continuous* (Anti-Capture). No provision introduces a new cycle.

---

## Metadata

| Field | Value |
|---|---|
| Owner | Founder |
| Status | **Ratified (Genesis)** — fully in force; Independent Reaffirmation Obligation outstanding |
| Document Version | 1.1.0-genesis |
| Applies To | AI Engineering Platform (all repositories) |
| Review Cadence | Annual (constitutional core); mechanisms may be revised more often under the cycle |

### Decision history
- **1.1.0-genesis** — Amended by AMENDMENT_O6 (T5, Ratified Genesis 2026-07-15) → **Doctrine E
  (Responsibility-and-Authority)**. Completes the five accountability roles (P5) with transfer,
  vacancy, escalation, succession, and the institutional-vs-individual authority backstop, and
  constitutionalizes institutional continuity of responsibility (P7); Ratified (Genesis), folded
  into the Independent Reaffirmation Obligation. Prior text preserved; nothing rewritten.
- **0.1.0** — Root Governance Primitive ratified (seven stages) + interpretive clauses; admission
  test and experiment→standard reference instance ratified.
- **1.0.0-genesis — Workshop 4 closed.** Ratified under the Genesis Exception: **Change Classes**
  (two-axis T0–T5 × E1/E2/E3, classification authority, anti-underclassification — OQ-GOV-003);
  **Anti-Capture Doctrine** (seven rules — OQ-GOV-002); **Genesis Authority Doctrine** (Genesis
  Exception, Ratified (Genesis) status ladder, independence trigger, delegation, succession,
  emergency continuity — OQ-GOV-001); the **Deliberate-Evolution Rule**.

### Open questions
- **Independent Reaffirmation Obligation** — steward: Founder; review trigger: first existence of
  substantive independent constitutional authority (End-of-Genesis condition). Until discharged,
  all constitutional documents remain `Ratified (Genesis)`.
- Classification debt accrued during Genesis is folded into the reaffirmation obligation.

### Cross references
- [PLATFORM_PRINCIPLES](PLATFORM_PRINCIPLES.md) · [PLATFORM_VISION](PLATFORM_VISION.md) · [PLATFORM_ARCHITECTURE](PLATFORM_ARCHITECTURE.md) · [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md) · [PLATFORM_RELEASE_STRATEGY](PLATFORM_RELEASE_STRATEGY.md) · [PLATFORM_GLOSSARY](PLATFORM_GLOSSARY.md)
