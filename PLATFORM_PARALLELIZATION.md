# PLATFORM_PARALLELIZATION

> How workstreams may run concurrently without producing incompatible foundations.
> Non-constitutional. The doctrine is ratified (Workshop 3); the per-workstream matrix is
> Draft and tracks the current plan in [PLATFORM_WORKSTREAMS](PLATFORM_WORKSTREAMS.md).

---

## Parallelization doctrine *(Ratified)*

The words *never* and *always* are too absolute for real dependencies. The doctrine
distinguishes **learning** from **stabilization**:

1. **Serialize accepted contracts before dependent stabilization.** A consumer may be
   researched or prototyped concurrently, but it cannot be declared *stable* before the
   versioned contract it depends upon is accepted.
2. **Parallelize workstreams across narrow interfaces.** Different planes may advance
   concurrently when they exchange only explicit, versioned identities and operations —
   never shared internal state.
3. **Cross-cutting capabilities advance continuously.** Provenance, validation, and
   self-honesty accompany every milestone; they are never postponed to a cleanup phase.
4. **Cross-cutting contract changes are coordinated.** Because provenance, identity,
   validation, and compliance semantics affect many planes, their *contracts* cannot change
   independently without compatibility and migration review.
5. **Research may precede dependency completion.** A later capability may explore
   requirements early — especially where it may reveal missing foundation requirements —
   while implementation acceptance still respects the dependency order.

---

## Status legend

- 🟢 **Green** — may proceed independently now.
- 🟡 **Yellow** — may proceed concurrently *only* through interface-first design; may not
  *stabilize* before a named contract is accepted.
- 🔴 **Red** — must not start production implementation until a named prerequisite is
  accepted (research/discovery may still overlap).

The per-workstream questions: *Can run independently? · Requires bundle refresh? · Requires
constitutional approval? · Requires repository synchronization? · Requires release
synchronization?*

---

## Parallelization matrix *(Draft)*

| Workstream | Independent? | Bundle refresh? | Constitutional approval? | Repo sync? | Release sync? | Status |
|---|---|---|---|---|---|---|
| **WS-1** Reasoning substrate | Yes (foundational) | No | No | ECF↔EKB context | No | 🟢 |
| **WS-2** Model contract | Interface-first | No | No | ECF↔EKB identity | No | 🟡 *(consumers may discover; stabilize before WS-4/5/6)* |
| **WS-3** Responsibility model | Yes | No | Uses ratified P7 | No | No | 🟢 |
| **WS-4** Canonicalization | Concurrent w/ WS-7 | No | No | EKB↔ECF review | No | 🟡 *(stabilize after WS-2)* |
| **WS-7** Stewardship | Concurrent w/ WS-4 | No | No | governance↔ECF | No | 🔴 *(after WS-3 accepted)* |
| **WS-6** Supersession | Requirements only | No | No | EKB | No | 🔴 *(after WS-4 accepted)* |
| **WS-5** Assumptions | Research early | No | No | ECF↔EKB | No | 🔴 *(stabilize after WS-2; needs WS-1)* |
| **WS-8** Lifetime integrity | Research early | No | Touches Open Q 001 | ECF↔EKB | No | 🔴 *(after WS-5)* |
| **WS-C1** Provenance | Continuous | On identity/digest change | No | **All** | On contract change | 🟡 *(contract changes coordinated)* |
| **WS-C2** Self-honesty | Continuous | No | Gates may block claims | All | Gates releases | 🟡 *(reporting cannot ratify itself — P6)* |

---

## Concurrency guidance derived from the doctrine

**Safe to run in parallel now (interface-first):**
- WS-1 (substrate) ∥ WS-2 (model contract) ∥ WS-3 (responsibility) — three different
  concerns; WS-2 takes discovery feedback from later consumers.
- WS-4 (canonicalization) ∥ WS-7 (stewardship) — different planes, small versioned authority
  interface; neither embeds the other's internals.
- WS-C1 (provenance) and WS-C2 (self-honesty) ∥ everything — continuously.

**Must serialize before stabilization (Red until prerequisite accepted):**
- WS-2 model contract **before** WS-4 / WS-5 / WS-6 stabilize (everything attaches to the
  authoritative model).
- WS-4 canonicalization **before** WS-6 supersession (you cannot define *replacing* canonical
  knowledge before *what canonical means* is settled).
- WS-3 responsibility model **before** WS-7 stewardship automation.
- WS-5 assumptions **before** WS-8 lifetime integrity (O12 is built out of the assumption
  artifact).

**Coordinated-change caution (Yellow, cross-cutting):**
- Changes to **provenance identity / digest semantics** and to **compliance/validation
  contracts** ripple across all planes — they require compatibility + migration review and
  may require a coordinated bundle/release refresh (see
  [PLATFORM_RELEASE_STRATEGY](PLATFORM_RELEASE_STRATEGY.md)).

---

## Metadata

| Field | Value |
|---|---|
| Owner | Founder |
| Status | Ratified (Genesis) (doctrine) · **Draft** (matrix) |
| Document Version | 0.1.0 |
| Applies To | AI Engineering Platform (all repositories) |
| Review Cadence | Quarterly, or whenever a workstream's dependencies change |

### Decision history
- **0.1.0** — Five-rule doctrine ratified in Workshop 3, replacing an earlier never/always
  formulation. Matrix derived from the Workshop 3 dependency graph and the Draft workstreams.

### Open questions
- Matrix statuses depend on workstream owners and acceptance events, which are `TBD (Founder)`
  in [PLATFORM_WORKSTREAMS](PLATFORM_WORKSTREAMS.md).

### Cross references
- [PLATFORM_WORKSTREAMS](PLATFORM_WORKSTREAMS.md) · [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md) · [PLATFORM_RELEASE_STRATEGY](PLATFORM_RELEASE_STRATEGY.md)
