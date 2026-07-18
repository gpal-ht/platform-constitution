# PROPOSAL_O6_B1_MODEL — The Responsibility-and-Authority Model (descriptive)

> **Status: PROPOSED (draft for founder ratification).** This is the **descriptive model**
> half of the ratified O6 "Partial" bar (*descriptive model + one executable rule*). It
> completes the **five roles already ratified** in [PLATFORM_PRINCIPLES](PLATFORM_PRINCIPLES.md)
> P5 and [PLATFORM_GLOSSARY](PLATFORM_GLOSSARY.md) — it does **not** invent roles or ratify
> authority. Every clause is a proposal for the founder to accept, amend, or reject.
>
> Obligation: **O6 — indestructible responsibility (P7)**. Plane: Governance. This model is
> what 0.5's **O4** (durable stewardship / challenge routing) will operationalize.

---

## 1. Scope and non-goals

**In scope.** Make the five roles *complete* by defining, for each: **transfer, vacancy,
escalation, succession**, and the **institutional-vs-individual authority** distinction — so
that responsibility is *indestructible* (P7): it can never be orphaned, and every consequential
engineering decision has, at every moment of its life, a locatable accountable authority.

**Non-goals (P13 — not built here).** No new roles. No new governance ceremony. No runtime
routing engine (that is O4, 0.5). No change to the constitution — this document is a
governance-mechanism proposal that *derives from* P5/P7, and per the Deliberate-Evolution Rule
an implementation proposal may only *propose*, never amend, the constitution.

**Actor-neutrality (carried from P7 and the Root Governance Primitive).** Every role below
constrains a *relationship*, never the nature of the actor. A role may be held by a human, an
AI engineering agent, a council, or a regulated institution — **except** where the
constitution already restricts it (Genesis Authority Doctrine: an AI may hold *operational*
authority but never *independent constitutional* authority). This model inherits that limit
verbatim; it does not widen it.

---

## 2. The five roles (ratified names) — restated for reference

| Role | Question it answers | Ratified source |
|---|---|---|
| **Authorship** | Who *produced* the decision? | P5 |
| **Approval** | Who *authorized* it at a point in time? | P5 |
| **Ownership** | Who *currently maintains* it? | P5 |
| **Accountability** | Who must *answer* for its continued validity / initiate reconsideration? | P5 |
| **Responsibility acceptance** | Who consciously *accepts residual risk*? | P5 |

Ratified properties (P5, unchanged): the roles are **distinct**, **transferable**, and
accountability requires a *durable accountable authority*, **not** eternal attachment to the
original author. One actor MAY hold several roles, subject to the role-separation limits of the
Root Governance Primitive (proposer ≠ sole challenger; generator ≠ sole ratifier — P6).

---

## 3. Two lifetimes each role has (the completion frame)

A role is "complete" when we can answer, mechanically or by record, four questions across its
whole life:

- **Point-in-time binding** — *who holds it now?* (needed at the approval boundary — B2).
- **Transfer** — *how does it move from one holder to another without a gap?*
- **Vacancy** — *what is true when no one holds it, and what must happen?*
- **Escalation / succession** — *when a holder cannot or must not act, where does authority go?*

The rest of this document answers these for each role, then draws the institutional-vs-
individual line (§6) that makes the answers indestructible.

---

## 4. Transfer, vacancy, escalation, succession — the general model

These four are defined once as a **general mechanism**, then specialized per role in §5. All
four are instances of the ratified **Root Governance Primitive** (scope & authority → proposal
→ evidence → independent challenge → authorized disposition → versioned effect → monitored
reconsideration) applied at role scope — this document adds *no* new cycle (Governance
Admission Test).

**4.1 Transfer (a role changes holder, deliberately).**
A recorded act with: the role, the outgoing holder, the identified & **accepting** incoming
holder, the effective moment, the authority authorizing the transfer, and preserved history.
*Constraint (P7):* **no-gap** — the incoming holder is bound at the instant the outgoing holder
is released; there is never an interval with no holder. A transfer that would leave a gap is
invalid.

**4.2 Vacancy (a role has no holder — a state, not an act).**
Vacancy is **recorded, never silent** (P2). A consequential decision whose *accountability* or
*ownership* is vacant is in a **degraded** state that must (a) be visible and (b) carry an
escalation target. *Constraint (P7):* vacancy of **accountability** is never a terminal
resting state — it must resolve to a holder or escalate to the institutional authority (§6).
Authorship and approval, being *point-in-time* roles (see §5), cannot become vacant
retroactively — history is indelible (P14).

**4.3 Escalation (a challenge or decision must reach a higher authority).**
Every role has a **named escalation target** — the authority a challenge reaches when the
current holder is absent, conflicted, or unresponsive (Clarification B: a challenge that
reaches no accountable recipient is not a challenge). Escalation **routing** at runtime is O4
(0.5); B1 only *names the targets* so O4 can route them.

**4.4 Succession (continuity of a role across holders over time).**
The ordered rule for *who becomes the next holder* when the current one departs — planned
(transfer, §4.1) or unplanned (vacancy, §4.2). *Constraint:* a successor **receives the
office, not freedom from its constraints** (inherited verbatim from the Genesis Succession
doctrine). Succession preserves the historical chain; it never rewrites who held the role
before (P8, P14).

---

## 5. The completion, role by role *(PROPOSED)*

### 5.1 Authorship — *point-in-time, historical*
- **Binding:** fixed at production; recorded in provenance (P8). **Immutable** — authorship is
  history.
- **Transfer:** authorship does **not** transfer (you cannot become the past author). What
  transfers is *ownership/accountability* of what was authored.
- **Vacancy:** impossible retroactively; an *unknown* author is a provenance defect (P8), not a
  vacancy.
- **Escalation/succession:** n/a (historical). Challenges about an authored decision escalate
  via its **accountability** holder.

### 5.2 Approval — *point-in-time, authority-bearing (the B2 role)*
- **Binding:** at the approval boundary, exactly one **approval authority** is in force and is
  **recorded** (this is what B2 makes executable: the run records *which role holds approval
  authority* and the model version it binds to).
- **Transfer:** approval authority may be *delegated* only when explicit and bounded
  (inherited from the Delegation doctrine: recorded granted authority, scope, duration/trigger,
  permitted/forbidden decisions, accountable owner, revocation). *Authority may be delegated;
  accountability must remain identifiable.*
- **Vacancy:** if no role holds approval authority, the boundary **cannot be crossed** — the
  run stays at `waiting_for_human_approval` and **fails closed** (this is the natural, but for
  Partial *not-yet-built*, extension of B2; see SCOPE item (c)).
- **Escalation/succession:** a withheld or unavailable approver escalates to the **institutional
  approval authority** (§6). Individual approvers may change; the *institutional* authority to
  approve is continuous.

### 5.3 Ownership — *continuous, present-tense*
- **Binding:** exactly one current owner maintains the decision now.
- **Transfer:** the paradigm transfer (§4.1), no-gap.
- **Vacancy:** an *ownerless* consequential decision is a degraded state; it must be visible and
  escalate to accountability, then to the institution.
- **Escalation/succession:** owner → **accountability** holder → institutional owner.

### 5.4 Accountability — *continuous, the indestructible core of P7*
- **Binding:** every consequential decision has, at all times, one accountable authority "capable
  of accepting responsibility and responding to challenge" (P7).
- **Transfer:** no-gap transfer; the durable role explicitly *may* leave the original author
  (P5) — accountability is *durable*, not *eternal to the author*.
- **Vacancy:** **the one vacancy the model forbids as a resting state.** Vacant accountability
  must immediately escalate to the **institutional accountable authority** (§6) — this is
  exactly the "orphaned responsibility" P7 exists to prevent.
- **Escalation/succession:** individual holder → institutional accountable authority, which is
  **never vacant by construction** (§6). This is what makes responsibility *indestructible*.

### 5.5 Responsibility acceptance — *point-in-time, risk-bearing*
- **Binding:** whoever consciously accepts residual risk records that acceptance (P8).
- **Transfer:** a *new* acceptance by a new holder supersedes the prior one (P14: history
  preserved); the earlier acceptance remains in the record.
- **Vacancy:** unaccepted residual risk is a **blocking** state — a decision may not be treated
  as approved while its residual risk is accepted by no one.
- **Escalation/succession:** escalates to the **accountability** holder, then the institution.

---

## 6. Institutional vs individual authority *(PROPOSED — the load-bearing distinction)*

> **Individual authority** is held by a specific actor at a specific time and *can* become
> vacant. **Institutional authority** is the office/role itself, which persists across holders
> and is **never vacant by construction** — when no individual holds it, it rests with the
> institution's standing accountable authority (ultimately, under the current constitutional
> order, the **Founder** under the Genesis Authority Doctrine, until End-of-Genesis introduces
> additional constitutional authority).

Why this is the mechanism that makes P7 hold:

- Individuals are corrigible and mortal; **offices are continuous.** P7 requires responsibility
  to be *indestructible*, which is impossible if it attaches only to individuals. The office
  absorbs vacancy: an individual seat may be empty, but the *institutional* accountability
  behind it is not.
- **Every individual role in §5 has an institutional backstop.** When an individual holder is
  vacant, conflicted, or unresponsive, the role does not evaporate — it **rests with the
  institution** until re-bound. This is the constructive guarantee that closes §4.2's "vacancy
  of accountability is never terminal."
- This distinction is **already implicit** in the constitution: Delegation ("authority may be
  delegated; *accountability must remain identifiable*"), Succession ("a successor receives the
  office, not freedom from its constraints"), and Emergency continuity ("preserves operations,
  not sovereignty") all separate the *office* from the *holder*. B1 makes that separation
  explicit and names it, without amending anything.

**Recorded at runtime (B2):** the approval-authority binding records an **individual/role
holder** *and* the **model version** — the model version is what ties the individual binding
back to the institutional authority that stands behind it. That is why SCOPE item (a)
recommends recording the model version, not bare identity.

---

## 7. Trace to the constitution (Governance Admission Test)

| B1 clause | Root-cycle function it instantiates | Principle served |
|---|---|---|
| Point-in-time binding (§5.2) | *scope & authority* recorded | P5, P7 |
| Transfer no-gap (§4.1) | *authorized disposition* + *versioned effect* | P7, P8 |
| Vacancy recorded, non-terminal (§4.2, §5.4) | *monitored reconsideration* | P2, P7 |
| Escalation targets (§4.3) | *independent challenge* reaches an authority | P5, Clarification B |
| Succession preserves chain (§4.4) | *versioned effect* preserving history | P8, P14 |
| Institutional backstop (§6) | authority is *constrained + continuous* | P7, Anti-Capture |

No clause introduces a new cycle; each strengthens a named stage — so the model passes the
Admission Test rather than becoming a catalogue.

---

## 8. What is executable now vs descriptive (the Partial line)

- **Executable now (B2):** §5.2 point-in-time approval-authority **binding** — the run records
  which role holds approval authority + model version; the contract rejects a mismatch, failing
  closed.
- **Descriptive now (this document):** transfer, vacancy, escalation, succession for all roles,
  and the institutional backstop — written **precisely enough to become machine-checkable
  later** (the A2 record already carries the role + model version a future vacancy/succession
  check would need). Operationalizing them is **O4 (0.5)**.

---

## 9. Open questions for the founder
1. **Institutional authority identity (§6).** Confirm that, under the current order, the
   standing institutional accountable authority is the **Founder** (Genesis), and that
   End-of-Genesis is the trigger that introduces an additional institutional authority. B1
   assumes this rather than deciding it.
2. **Responsibility acceptance as a blocking state (§5.5).** Confirm that unaccepted residual
   risk should *block* readiness. (Alternative: record it as a non-blocking finding for
   Partial.)
3. **Delegation depth (§5.2).** For Partial, is delegated approval authority in-scope to
   *record*, or explicitly deferred to O4? (Recommendation: record the field shape, do not
   enforce delegation chains yet.)
4. **Ratification class.** Confirm B1 is ratified as a **governance-mechanism** document (T3
   band per PLATFORM_GOVERNANCE — it touches authority, so independent review applies), not as a
   constitutional change.

---

## Metadata
| Field | Value |
|---|---|
| Status | **PROPOSED** — descriptive model for O6 Partial |
| Owner (proposing) | Track B owner (O6) |
| Ratifies into | Governance-mechanism layer ([PLATFORM_GOVERNANCE](PLATFORM_GOVERNANCE.md)) |
| Serves | O6 / P7; operationalized later by O4 (0.5) |
| Derives from | P5 (five roles), P7 (indestructible responsibility), Root Governance Primitive, Genesis Authority Doctrine (delegation/succession/continuity) |
| Cross references | [PROPOSAL_O6_SCOPE](PROPOSAL_O6_SCOPE.md) · [PROPOSAL_O6_B2_RULE](PROPOSAL_O6_B2_RULE.md) · [PLATFORM_PRINCIPLES](PLATFORM_PRINCIPLES.md) · [PLATFORM_GLOSSARY](PLATFORM_GLOSSARY.md) |
