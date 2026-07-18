# PLATFORM_PRINCIPLES

> Constitutional document. It answers one question: **what must always be true?**
> Every principle here has survived the ten-year test — *"would you still believe this
> in ten years, even if the technology is unrecognizable?"* A statement that fails that
> test is a preference, not a principle, and does not belong here.

---

## Preamble — how to read this document

**The constitution governs engineering *responsibility*, not engineering *capability*.
It constrains how engineering judgment is exercised, challenged, and accounted for, but
does not constitutionalize assumptions about who or what may possess that judgment.**

This is the interpretive key. Wherever a principle appears to speak about people or
machines, read it as speaking about *roles and relationships*. The constitution
constrains institutions; it does not forecast cognition.

---

## The Root Principle

> **Engineering decisions must remain intelligible, challengeable, and reproducible
> throughout their lifetime.**

Everything else in this document descends from that sentence. If every other principle
were lost, the platform could be reconstructed from this one.

### The three pillars

- **Intelligible** — the decision can be understood.
- **Challengeable** — the decision can be questioned, contested, and reconsidered.
- **Reproducible** — the decision can be reconstructed and its basis re-evaluated.

### Constitutional clarifications

- **Clarification A — Aspirational invariant.** The Root Principle is an invariant design
  *standard*, not a claim that the platform presently satisfies it in full. Known gaps
  between the principle and current capability must be recorded explicitly, treated as
  engineering obligations, and never concealed by weakening the principle. (See
  [PLATFORM_VISION](PLATFORM_VISION.md) Open Question 001 for the principal current gap.)
- **Clarification B — Challengeability requires answerability.** A challenge that reaches
  no accountable recipient is not a challenge. Every consequential decision must have a
  durable path by which a challenge reaches an accountable authority and receives a
  recorded disposition.
- **Clarification C — Institutional continuity of responsibility.** The accountable authority
  required by P5 and P7 is an **office**, not merely an individual holder. Individual holders
  are corrigible, revocable, and finite, and a role may fall vacant; the **institutional**
  authority behind the office persists across holders and is **never vacant by
  construction**. When no individual holds an accountable role, the responsibility does not
  evaporate — it rests with the institution's standing accountable authority (under the
  current constitutional order, the **Founder** under the Genesis Authority Doctrine, until
  End-of-Genesis introduces additional constitutional authority). This is the construction
  that makes responsibility **indestructible** (P7): a seat may be empty, but the
  responsibility behind it cannot be. The completion of the five accountability roles
  (transfer, vacancy, escalation, succession) that this clause presumes is specified in
  [PLATFORM_GOVERNANCE](PLATFORM_GOVERNANCE.md) **Doctrine E**.

---

## The Principles

Each principle is traced to the pillar of the Root it serves. **No principle stands
alone** (P12): a candidate that cannot be traced to the Root is not constitutional.

### Under INTELLIGIBLE

**P1 — Engineering judgment precedes engineering artifacts.**
The artifact is never primary; the judgment that produced it is. Reasoning, proofs,
simulations, symbolic planning, and model checking are all forms of judgment, and none
may be skipped on the way to an artifact.
*Ten-year test:* "reason" is one manifestation; "judgment precedes artifact" outlives any
particular method.

**P2 — The platform is honest about itself.**
Capabilities and limits are legible. Compliance is claimed only at the level actually
demonstrated; unmet requirements are represented as explicit gaps, never hidden through
weaker language, optimistic interpretation, or silent omission.
*Ten-year test:* a system that conceals its limits is untrustworthy at any capability.

### Under CHALLENGEABLE

**P3 — Nothing is canonical by existence.**
Knowledge becomes canonical only through evidence, review, and explicit acceptance —
*including the platform's own knowledge.* The platform rejects documentation by
accumulation, architecture by precedent, and knowledge by repetition.
*Ten-year test:* authority-by-existence is a permanent failure mode.

**P4 — Evidence over opinion.**
Challenges are settled by evidence, not by seniority, eloquence, or precedent.
*Ten-year test:* timeless.

**P5 — Answerability.**
Every consequential engineering decision must have a durable accountable authority, an
escalation path, and a recorded disposition. The five roles below are distinct and
transferable.
*Ten-year test:* mechanism-agnostic — the authority may be an individual, a rotating
stewardship role, a council, or a regulated institution.

> **The five roles of accountability** (distinct, and often held by different actors):
> **authorship** (who produced the decision) · **approval** (who authorized it at a point
> in time) · **ownership** (who currently maintains it) · **accountability** (who must
> answer for its continued validity or initiate reconsideration) · **responsibility
> acceptance** (who consciously accepts residual risk). Accountability requires *durable
> accountable authority*, not eternal attachment to the original author. The role is
> transferable while the historical chain is preserved.

**P6 — Validation is independent of generation.**
The actor that produces a decision cannot be the sole actor that ratifies it — regardless
of whether that actor is human or machine.
*Ten-year test:* separation of production from verification is a durable engineering
invariant.

**P7 — Responsibility is indestructible.**
Ultimate responsibility for consequential engineering decisions must rest with a
recognized accountable authority capable of accepting responsibility and responding to
challenge. This principle constrains *governance*, not the identity or nature of the
decider. It protects against orphaned responsibility, as P6 protects against
self-ratification.
*Ten-year test:* responsibility cannot evaporate, even in a world where the decider is
non-human.

**P14 — Canonical knowledge is corrigible.**
Every canonical decision must remain replaceable by better evidence without denying its
historical existence. *History is preserved; truth is revised.* This forecloses rewriting
history, deleting mistakes, "latest wins," and immutable dogma in a single stroke.
*Ten-year test:* the ability to be corrected by evidence is what separates knowledge from
dogma, in any era.

### Under REPRODUCIBLE

**P8 — Provenance is mandatory.**
Every consequential artifact can be traced to the inputs, knowledge, and process that
produced it.
*Ten-year test:* reconstruction is impossible without an unbroken chain.

**P9 — Knowledge is versioned.**
Engineering knowledge has identity, history, and lifecycle — never an ambient "current
truth."
*Ten-year test:* reproducibility over time is impossible without versioned knowledge.

**P10 — Engineering artifacts remain synchronized with their authoritative engineering
model.**
The forcing function is execution, not discipline: when an artifact drifts from its
authoritative model, execution breaks. *(Current governance mechanism: artifacts rendered
from the model. The invariant is synchronization, not any particular mechanism.)*
*Ten-year test:* the anti-drift invariant is independent of how synchronization is
achieved.

**P11 — Assumptions are first-class, executable artifacts.**
Decisions declare their assumptions with confidence, evidence, and review triggers, so
that reality can challenge them. The reasoning need not be executable; the assumptions
that support it can be.
*Ten-year test:* this is the bridge toward the long-term integrity of judgment (Open
Question 001).

### META — principles that govern the constitution itself

**P12 — No principle stands alone.**
Every principle must trace to the Root. A candidate that cannot is not constitutional and
belongs in governance, architecture, tooling, or the roadmap. This is the **admission
test** for future principles.
*Ten-year test:* it keeps the constitution from bloating into a catalogue.

**P13 — Governance is presumed unnecessary until justified.**
Every governance mechanism starts guilty and must prove it improves engineering quality,
traceability, reproducibility, or safety. If removing a mechanism would not measurably
reduce one of those, the mechanism should not exist.
*Ten-year test:* the permanent defense against bureaucratic accretion.

---

## Principle index

| # | Principle | Pillar |
|---|---|---|
| P1 | Engineering judgment precedes engineering artifacts | Intelligible |
| P2 | The platform is honest about itself | Intelligible |
| P3 | Nothing is canonical by existence | Challengeable |
| P4 | Evidence over opinion | Challengeable |
| P5 | Answerability — durable accountable authority | Challengeable |
| P6 | Validation is independent of generation | Challengeable |
| P7 | Responsibility is indestructible | Challengeable |
| P14 | Canonical knowledge is corrigible | Challengeable |
| P8 | Provenance is mandatory | Reproducible |
| P9 | Knowledge is versioned | Reproducible |
| P10 | Artifacts synchronized with the authoritative model | Reproducible |
| P11 | Assumptions are first-class, executable artifacts | Reproducible |
| P12 | No principle stands alone | Meta |
| P13 | Governance is presumed unnecessary until justified | Meta |

> Numbering note: P14 (corrigibility) was admitted during Workshop 2 after P1–P13 and is
> grouped under CHALLENGEABLE by meaning rather than by number. Numbers are stable
> identifiers, not an ordering.

---

## Metadata

| Field | Value |
|---|---|
| Owner | Founder |
| Status | Ratified (Genesis) |
| Document Version | 0.2.0 |
| Applies To | AI Engineering Platform (all repositories) |
| Review Cadence | Annual |

### Decision history
- **0.2.0** — Amended by AMENDMENT_O6 (T5, Ratified Genesis 2026-07-15) — Clarification C
  (institutional continuity of responsibility). Completes the five accountability roles (P5)
  and constitutionalizes institutional continuity of responsibility (P7); Ratified (Genesis),
  folded into the Independent Reaffirmation Obligation. Prior text preserved; nothing rewritten.
- **0.1.0** — Root Principle established as a triad + two clarifications. P1–P14 ratified,
  each traced to a pillar and each passing the ten-year test.
- **Accountability ruling** — Accountability was considered as a fourth pillar and
  rejected. It is a first-order *descendant of challengeability* (P5, P7): a challenge with
  no answerable recipient is not a challenge.
- **P7 ruling** — Originally "ultimate authority rests with an accountable human." Rewritten
  to be responsibility-centric, not human-centric, because constitutionalizing human
  authority embeds a prediction about intelligence. This ruling amended
  [PLATFORM_VISION](PLATFORM_VISION.md) non-goal #2.
- **P1 broadening** — Originally "Reason before generation"; broadened to "Engineering
  judgment precedes engineering artifacts."
- **P14 addition** — Corrigibility added to prevent history-rewriting and "latest wins."
- **P13 wording** — Tightened from "Governance bears the burden of proof" to "Governance
  is presumed unnecessary until justified."

### Open questions
- See [PLATFORM_VISION](PLATFORM_VISION.md) Open Question 001, which is the principal known
  gap against Clarification A and the "throughout their lifetime" clause of the Root.

### Cross references
- [PLATFORM_MISSION](PLATFORM_MISSION.md) · [PLATFORM_VISION](PLATFORM_VISION.md) · [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md) · [PLATFORM_GOVERNANCE](PLATFORM_GOVERNANCE.md) · [PLATFORM_GLOSSARY](PLATFORM_GLOSSARY.md)
