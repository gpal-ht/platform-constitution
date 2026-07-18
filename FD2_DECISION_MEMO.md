# FD-2 DECISION MEMO — Operational Evidence: distinct Plane, or cross-cutting concern?

> **Status: RULED (Founder, 2026-07-16) — READING B.** Operational Evidence is NOT a
> distinct Plane at 0.6: evidence permanence is a named Control-owned obligation now;
> consumption transfers to Reasoning under FD-4; re-open trigger recorded
> (external-boundary evidence arrives, or ≥2 independent producers/consumers). The
> ruling is landed in PLATFORM_ARCHITECTURE (FD-2 resolved).
> This is the FD-2 workshop deliverable required by [PROGRAM_0.6](PROGRAM_0.6.md)
> ("FD-2 Workshop") and promised by the ratified architecture
> ([PLATFORM_ARCHITECTURE](PLATFORM_ARCHITECTURE.md) §4.7, §10: "decide at 0.6").
> Both readings are presented at full strength (per the Founder's kickoff ruling #2).
> The Founder rules; the ruling lands in PLATFORM_ARCHITECTURE by the Founder's hand
> (or by scribe at the Founder's explicit instruction) — see §7.

| Field | Value |
|---|---|
| Decision | FD-2 — Operational Evidence: distinct Plane or input half of Reasoning? |
| Deferred by | PLATFORM_ARCHITECTURE 0.1.0 ratification ("⏳ DEFER — decide at 0.6") |
| Evidence base | Read-only probe of `ecf` @ `e19a2e0` (v0.5.0 merged to develop) and live `runtime/runs/` |
| Author | FD-2 workshop thread (0.6 background thread; one of four) |
| Date | 2026-07-16 |

---

## 1. The question, precisely

The ratified taxonomy (FD-5) admits exactly three kinds of part:

1. **Constructive Planes** — produce engineering; sit in the one-directional chain
   `Knowledge → Control → Project`.
2. **Cross-cutting Planes** — operate *across* constructive Planes via their published
   outputs (Review, Release, future Reasoning).
3. **Cross-cutting concerns that are not Planes** — enforced by every Plane, owning no
   execution responsibility of their own (Governance/Accountability, security,
   observability, performance).

Under that taxonomy, ruling that Operational Evidence **is a distinct constructive
Plane** would mean all of the following become true:

- **Mission** — capture operational reality (run outcomes, arriving external signals,
  MISS-closures) and hold it as durable, identity-bearing evidence that can contradict
  standing assumptions and decisions.
- **Boundary** — it *produces* evidence artifacts as engineering outputs (constructive),
  not merely *operates across* other Planes' outputs; it would take a position in the
  dependency chain from which Reasoning (and Review, and supersession) draw fuel.
- **Artifacts it would own** — the evidence store and its index; evidence identity
  (stable IDs + digests); evidence provenance and arrival records. Concretely, today's
  ownership table rows **Runtime State** and **Run Manifest** (currently: *Control*,
  §6 of the architecture) would transfer to it, plus a new row for durable evidence
  records.
- **Contracts** — a versioned **evidence interface**: evidence in (with identity,
  provenance, timestamp) → durable, citable evidence out; consumed by Reasoning (O11
  triggers), Review (challenge/disposition citations), and the supersession machinery
  (O7 "better evidence").

Ruling that it **remains a cross-cutting concern** would mean: evidence capture and
permanence are *obligations enforced within existing Planes* — Control owns run
evidence and its store semantics (it already owns run state, run manifests, task
provenance per §4.2); Reasoning (future) owns evidence-driven challenge, per §4.6
("Dependencies: Operational Evidence (fuel)") and the §4.7 provisional note that it
"may be the input half of the Reasoning Plane." No new Plane, no ownership transfer,
FD-2 marker resolved as ❌ (with or without a re-open trigger — §6).

Two precedents bound the ruling:

- **Accountability (FD-3, ❌ Ratified):** "no distinct state of its own; it annotates
  every artifact… enforced by every Plane" → governance concern, not a Plane.
  Operational Evidence is *not* identical to that case — it demonstrably **has** state
  of its own (§4 below). The FD-3 test that transfers is narrower: *does the candidate
  own an execution responsibility no existing Plane can own?*
- **Artifact (FD-1, ❌ Ratified):** "projections of engineering state, not independent
  responsibilities… a catch-all that violates single-ownership by trying to own
  everyone's outputs." This is the sharpest knife against Reading A: evidence records
  are, today, *outputs of other Planes' activities*.

---

## 2. READING A — Operational Evidence as a distinct Plane (at full strength)

**The strongest form of the argument is not "evidence exists" — it is "no Plane is
actually exercising ownership of evidence permanence, and the platform is already
paying for that."** Three concrete exhibits from the probe:

1. **A permanent governance record already cites mortal evidence.** The disposition of
   the platform's first real challenge —
   `ecf/challenges/CHG-20260716-0001/disposition.yaml` (versioned, permanent) — cites
   as evidence `runtime/runs/RUN-TRANSFORM-20260716-0002/reports/candidate-canonical-artifact.md`,
   which is **gitignored** (`runtime/` in `ecf/.gitignore`; confirmed with
   `git check-ignore`). The moment that checkout is cleaned, a ratified disposition's
   evidence chain dangles. This is not hypothetical risk; it is a live P8 exposure
   *today*, produced by the current arrangement in which Control "owns" run state but
   deliberately does not persist it.
2. **The 0.5 release recorded the gap as a deferral, not a solved problem.**
   `ecf/release/RELEASE_NOTES_0.5.0.md` (Known deferrals): "**Run-evidence
   permanence** — `runtime/` remains unversioned; canonical artifacts carry
   digest-bound evidence copies, but general run evidence is mortal (0.6 candidate)."
   A Plane whose single mission is evidence permanence would make that deferral
   structurally impossible to repeat.
3. **The next milestone's centerpiece consumes evidence that has nowhere to land.**
   Track B's O11 triggers (evidence-arrival class) fire when evidence *arrives* — but
   arrival of what, where? MISS-0001/0002 (the blockers whose closure Track A names as
   the natural first supersession trigger for EDR-0001) exist only inside a mortal run
   (`runtime/runs/RUN-REASON-WR0001-V040-0002/task_outputs/missing-information.yaml`,
   `status: open`) and inside EDR-0001's frozen digest-bound copy. There is **no
   artifact type in the ownership table** in which "MISS-0001 is now closed, here is
   the evidence, here is who supplied it" can be durably recorded. The closing of a
   MISS *is* operational evidence arriving, and today it has no home.

**What a Plane would make possible:**

- A single owned **evidence store** with write-once semantics (the pattern already
  proven by `canonical/decisions/index.yaml`), giving challenges, dispositions,
  supersessions, and triggers one citable place — ending per-consumer ad-hoc copying
  (today there are already *two* such ad-hoc mechanisms: `canonical/*/evidence/`
  digest-bound copies and the hand-promoted `ecf/evidence/WS-E-traceability/`).
- A versioned **evidence contract** (identity, digest, provenance, arrival time,
  freshness) that O11 trigger evaluation can consume without coupling to Control's run
  internals — protecting the P6-style independence of the future Reasoning Plane from
  the Plane that generated the evidence.
- A clean seat for **external** operational reality: the architecture's own external
  actor list includes "Operational reality — the running world that later contradicts
  or confirms assumptions." When consuming projects (0.8, Multiple Consumers) emit
  operational signals, Control — whose mission is the engineering *process* — is a
  strange owner for sensing the *outside world*.

**What it costs now:** a T4 architecture amendment; ownership-table transfers (Runtime
State, Run Manifest — currently Control's, ratified) that reopen Control's §4.2
definition; a Plane whose capability-map rows would today read almost entirely
**Research** (only "run state capture" is Implemented); and contradiction of the
architecture's own stabilizing rule — "adding or redefining a Plane requires a
compelling reason grounded in operational evidence."

---

## 3. READING B — cross-cutting concern (at full strength)

**The strongest form: every exhibit in Reading A is an argument for a *store and a
contract*, not for a *Plane* — and the ratified precedents show the difference.**

1. **The FD-1 test cuts directly.** Every operational-evidence artifact that exists
   today (§4) is a **projection or output of an existing Plane's activity**: run
   records are written by Control's runtime; evidence copies are written by Control's
   promotion tool; challenge evidence lists are written by governance acts;
   validation verdicts are written by Review's gates. An Operational Evidence Plane
   would own *everyone's outputs* — exactly the "catch-all that violates
   single-ownership" reasoning by which Artifact was ruled out. FD-1 even assigned the
   analogous cross-plane mechanism (artifact synchronization/rendering, P10) to
   **Control as a responsibility**, not to a new Plane. Evidence permanence is the same
   shape: a store-semantics responsibility, assignable to Control today.
2. **The Accountability precedent, correctly transferred.** Accountability was ruled
   out not merely because it lacked state, but because it owned **no execution
   responsibility that existing Planes couldn't enforce**. The same holds here:
   Control already *owns* "run state, run manifests, task provenance" (§4.2, ratified)
   — the permanence defect is Control under-implementing an ownership it already has,
   which is a **maturity gap** (roadmap material, O2/P2 honest-gap handling), not a
   missing responsibility (architecture material). You do not create a new Plane
   because an existing Plane has a known deferral open against it.
3. **Single-producer, single-consumer reality.** The FD-2 deferral rationale was
   "insufficient evidence (one consumer, one live workflow, one experiment)." The 0.5
   probe shows growth in *volume*, not in *kind*: 13 runs under `ecf/runtime/runs/`,
   all from the **same one workflow family** (WF-REASON + its WF-TRANSFORM
   promotions); **one** canonical record (EDR-0001); **one** challenge
   (CHG-20260716-0001). The first genuine machine consumer — O11 trigger evaluation —
   is being *designed this milestone* and does not exist yet. Ruling a Plane into
   existence for a consumer that is still a workshop deliverable is architecture ahead
   of evidence — precisely what the stabilizing rule forbids. Compare FD-6: Review, a
   *ratified* Plane with implemented capabilities, still doesn't get its own
   repository until **two independent consumers** exist. Operational Evidence has one
   pending consumer and would get a whole Plane.
4. **External-reality evidence count: zero.** The provisional mission ("capture
   operational reality") describes sensing the running world. Not one artifact of that
   kind exists on the platform today — no telemetry, no consuming-project operational
   signal, no deployed-system feedback. A Plane chartered now would be chartered
   almost entirely on aspiration (P2), and the taxonomy placement itself would be
   awkward: a *constructive* Plane must produce engineering in the
   Knowledge→Control→Project chain; evidence capture is closer to the cross-cutting
   family — meaning even Reading A, examined closely, dissolves into "a future
   cross-cutting Plane," which is what §4.6/§4.7 already say about Reasoning and its
   input half.
5. **The architecture already reserves the seat.** §4.6 makes Reasoning depend on
   "Operational Evidence (fuel)"; §4.7 records that the responsibility "may be the
   input half of the Reasoning Plane"; FD-4 already established the transfer pattern
   (Control produces → ownership transfers to Reasoning when it exists). Reading B
   is not "evidence doesn't matter" — it is "the evidence responsibility matures
   inside Control now and rides the already-ratified FD-4 transfer when Reasoning
   stands up."

**What it costs:** the permanence gap must be closed *without* a Plane forcing it —
i.e., by obligation pressure (an O11 Partial bar cannot honestly claim
"evidence-arrival triggers are executable" while evidence has no durable place to
arrive — P2 would forbid the claim). And the dangling-disposition exposure (§2 item 1)
must be owned by someone *named*, or Reading B repeats the exact failure it excuses.

---

## 4. The evidence inventory — what exists TODAY (P2: claimed at the level demonstrated)

Permanence classes: **mortal** = gitignored (`runtime/` per `ecf/.gitignore`), dies
with the checkout; **digest-bound** = sha256-pinned copy under a tracked path with
`origin_path` back-reference; **versioned** = tracked in git, release-pinned.

| # | Artifact | Where (today) | Written by | Read by | Permanence |
|---|---|---|---|---|---|
| 1 | Run records (13 runs: 11 reasoning, 2 transformation) — `manifest.yaml`, `state.yaml`, `run-record.json`, `task_outputs/`, `reports/`, `transactions/`, `staging/`, `drive.log` | `C:\Dev\ecf\runtime\runs\RUN-*` | Control runtime (`task_runner`: deterministic + AI executors) | Review gates; WF-TRANSFORM promotion; humans | **Mortal** |
| 2 | Per-task provenance (18/run; sha256 of every input/output, `ecf_commit`, executor id, timestamp) | `runtime/runs/*/provenance/TASK-*.yaml` | Control runtime | Gates, manifest generation | **Mortal** |
| 3 | Run manifests & completion (`final-manifest.yaml`, `completion.yaml`, `trace.md`) | `runtime/runs/*/reports/` | Control runtime (TASK-TRACE-000x) | Promotion tool, humans | **Mortal** |
| 4 | ASSUME-* records with `evidence_strength` (weak/moderate) | `runtime/runs/*/task_outputs/engineering-reasoning-context.yaml`, `engineering-recommendation.yaml` | AI executors (ANALYZE/DECIDE) | DECIDE tasks; Track B's raw material | **Mortal**, except digest-bound copies inside #6 |
| 5 | MISS-* open-information records (`status: open`; MISS-0001/0002 are the blockers gating EDR-0001's anticipated supersession) | `runtime/runs/RUN-REASON-WR0001-V040-0002/task_outputs/missing-information.yaml` | AI executor (TASK-ANALYZE-0007) | DECIDE tasks; humans; Track A's trigger | **Mortal**; frozen digest-bound snapshot inside #6. **No artifact type exists in which a MISS-closure can be durably recorded.** |
| 6 | Digest-bound evidence copies (6 items: approved report, validation verdict, completion, final manifest, approval, acceptance) + `evidence-manifest.yaml` with per-item sha256 and `origin_path` into mortal runtime paths | `ecf/canonical/decisions/EDR-0001/evidence/` | Control's promotion tool (`tools/canonical_promotion`, deterministic, human-invoked) | Anyone consuming EDR-0001; challenge disposition | **Digest-bound (permanent)** |
| 7 | Canonical write-once index | `ecf/canonical/decisions/index.yaml` | Promotion tool | Consumers; future supersession pointer home | **Versioned** |
| 8 | Challenge + disposition evidence lists (the platform's first real challenge) | `ecf/challenges/CHG-20260716-0001/{challenge,disposition}.yaml` | Humans via O4 routing machinery | Governance; P14 re-entry hook | **Versioned** — but disposition evidence ref #2 points at a **mortal** path (live dangling-evidence exposure) |
| 9 | Approval / acceptance records | `ecf/approvals/{APPROVAL-0001,ACCEPTANCE-0001}.yaml` | Humans (Founder, Genesis) | Promotion tool; disposition | **Versioned** |
| 10 | Hand-promoted workstream evidence (completion, gate decision, provenance, trace) | `ecf/evidence/WS-E-traceability/` | Humans (manual copy from a run) | Release validation | **Versioned** — the ad-hoc precursor of a store |
| 11 | Validation verdicts (`recommendation-report-validation.yaml`, `gate-decision.json`) | `runtime/runs/*/task_outputs/`; copies in #6/#10 | Review gates | Promotion tool | **Mortal**, except copies |
| 12 | External operational reality (deployed-system telemetry, consuming-project signals) | — | — | — | **Does not exist. Count: zero.** |

Honest summary (P2): the platform has **plenty of process evidence and zero world
evidence**. Everything in rows 1–11 is produced *by the platform about its own runs
and governance acts*; permanence, where it exists, is achieved by two ad-hoc copy
mechanisms (#6, #10), both Control-operated. The provisional mission's distinctive
content — reality contradicting assumptions — has no instances yet.

## 5. Decision criteria the Founder can rule on

1. **The contract test.** Does O11 trigger evaluation need an evidence contract
   (identity, durable storage, provenance, freshness/arrival time) that **no existing
   Plane can own**? — Probe answer: no. Control already owns run state, manifests, and
   task provenance (§4.2, ratified) and operates both existing permanence mechanisms;
   the evidence-arrival contract is a versioned Control interface extension, with the
   FD-4 transfer to Reasoning already ratified for exactly this family of artifacts.
2. **The store test.** Does evidence permanence require a store that no Plane owns? —
   Probe answer: the store is *missing*, not *unownable*. The write-once pattern
   exists (`canonical/decisions/index.yaml`); the 0.5 deferral names the gap; FD-1
   precedent assigns cross-plane mechanisms of this shape to Control as a
   responsibility. A gap in an owned responsibility is roadmap material, not a Plane.
3. **The real-artifacts test (P2/P13 scope-creep guard).** Would a Plane created now
   own real artifacts it *brings*, or only artifacts it *takes* from Control's ratified
   ownership plus aspirational rows? — Probe answer: it would take rows 1–3 and 6–7
   from Control and bring only Research-status aspirations (row 12 is empty). The
   capability map would show a Plane that is one Implemented row (run-state capture,
   already Control's) and the rest Research.
4. **The consumer test (FD-6 symmetry).** How many independent producers and consumers
   of operational evidence exist? — One producer (the WF-REASON/WF-TRANSFORM family);
   consumers today are Control's own promotion tool and one governance disposition;
   the first genuine machine consumer (O11 trigger evaluation) is a 0.6 workshop
   deliverable, not yet built. Review — a ratified Plane — was denied a repository on
   a two-independent-consumers trigger; Operational Evidence does not currently meet a
   weaker bar than that.
5. **The external-sensing test (the honest future trigger).** Does evidence exist that
   originates *outside* the platform boundary (operational reality of consuming
   projects, deployed systems)? — No; count zero. This is the one criterion whose
   flip would genuinely change the answer, because sensing the outside world is the
   single responsibility in the provisional mission that Control's process-governance
   charter fits poorly.

## 6. Recommendation (PROPOSED)

**Rule Reading B: Operational Evidence is not a distinct Plane at 0.6 — it remains a
cross-cutting concern realized as (a) a Control-owned evidence-permanence
responsibility now and (b) the designated input half of the Reasoning Plane under the
already-ratified FD-4 transfer — with an explicit, FD-6-style re-open trigger:**

> FD-2 re-opens when **either** (i) operational evidence originating outside the
> platform boundary (consuming-project or deployed-system signals) must be captured
> and no existing Plane's charter fits, **or** (ii) two or more independent evidence
> producers/consumers exist beyond the Control-internal pipeline. This is a trigger,
> not a version milestone.

All five criteria in §5 currently point the same direction; the deferral rationale
("one consumer, one live workflow") has changed in volume but not in kind; and the
stabilizing rule sets the bar at "compelling reason grounded in operational evidence,"
which an inventory whose distinctive class (row 12) is empty cannot clear.

Paired with the ruling (proposed, non-gating for either track): the run-evidence
permanence deferral and the dangling-disposition exposure (§2 item 1, §4 row 8) should
be **named as Control-owned obligations** — Track B's O11 Partial bar already cannot
honestly claim executable evidence-arrival triggers without a durable place for
evidence to arrive (P2), so the store gets forced into existence by obligation
pressure rather than by Plane creation. That is P13 working as designed.

**The strongest counter-argument, stated fairly:** ownership on paper is not ownership
in fact. Control has "owned" run evidence through two releases while gitignoring it,
and the platform's first permanent disposition already cites a path that a `git clean`
would erase. Reading B trusts the same owner that produced the exposure to close it,
with only obligation pressure as the forcing function; a Plane would make the
permanence mission *structurally* un-deferrable, and FD-2 was deferred precisely so
that 0.6 — the milestone where evidence starts doing work (triggers, supersession) —
could decide with the consumer in view. If the Founder judges that a twice-deferred
gap plus a live P8 exposure is itself the "compelling operational evidence" the
stabilizing rule demands, Reading A is the honest ruling. The response embedded in
Reading B: the exposure argues for a *store with an owner*, and both candidate
mechanisms that exist today are already Control's; creating a Plane to force an owner
to do its job substitutes structure for accountability — the exact trade P13 exists
to refuse.

**What the ruling changes either way (both minimal for the 0.6 tracks — stated per
charter):**

- **If B (recommended):** PLATFORM_ARCHITECTURE — §4.7 is replaced by an entry in
  §4.8 (challenged out) recording FD-2 ❌ with the re-open trigger; §4 taxonomy bullet
  "Deferred" becomes "Not a Plane (trigger-based re-open)"; §8 stability row moves
  "Operational Evidence (provisional, FD-2)" out of Research-as-Plane into Control's
  evolving responsibilities; §10 FD-2 marked resolved. PLATFORM_CAPABILITY_MAP — the
  "Operational Evidence (provisional)" section retitles to a concern grouped under
  Control (permanence/store) and Reasoning (consumption), mirroring the FD-1
  relocation precedent. PLATFORM_ROADMAP — open-questions note updated (FD-2
  resolved). **0.6 scope impact: none.** Track A is untouched; Track B defines its
  evidence-arrival contract as a Control interface, which is what it would have built
  anyway.
- **If A:** PLATFORM_ARCHITECTURE — §4.7 expands to a full Plane definition
  (mission/owns/never-owns/interfaces/success criteria); ownership-table transfers of
  Runtime State and Run Manifest from Control reopen §4.2 (T4); dependency rules §5/§9
  gain the evidence interface; §8 keeps the Plane at Research (P2). CAPABILITY_MAP
  gains a Plane section that is one Implemented row plus Research rows. **0.6 scope
  impact: still minimal** — nothing O11 builds this milestone differs in code; only
  the interface's declared owner changes. The cost is architectural (ownership churn
  in ratified text), not schedule.

## 7. Reserved to the Founder

This memo decides nothing. The FD-2 ruling is made by the **Founder**; it lands in
[PLATFORM_ARCHITECTURE](PLATFORM_ARCHITECTURE.md) — resolving the §4.7 provisional
entry, the §10 FD-2 marker, and the taxonomy bullet — **by the Founder's hand, or by
scribe acting at the Founder's explicit instruction**. No text in PLATFORM_ARCHITECTURE,
PLATFORM_CAPABILITY_MAP, or PLATFORM_ROADMAP is modified by this thread. Until that
ruling is recorded, Operational Evidence remains exactly what the ratified
architecture says it is: provisional, Research, deferred.

### Cross references
- [PLATFORM_ARCHITECTURE](PLATFORM_ARCHITECTURE.md) §4.2, §4.6–4.8, §6, §8, §10 ·
  [PLATFORM_CAPABILITY_MAP](PLATFORM_CAPABILITY_MAP.md) ·
  [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md) ·
  [PLATFORM_PRINCIPLES](PLATFORM_PRINCIPLES.md) (P2, P8, P11, P13) ·
  [PROGRAM_0.6](PROGRAM_0.6.md) (FD-2 Workshop charter)
- Probe evidence: `ecf` worktree @ `e19a2e0` (`chore/0.6-fd2-probe`);
  `ecf/release/RELEASE_NOTES_0.5.0.md` (Known deferrals);
  `ecf/canonical/decisions/EDR-0001/` ; `ecf/challenges/CHG-20260716-0001/` ;
  `ecf/approvals/` ; `ecf/evidence/WS-E-traceability/` ;
  `C:\Dev\ecf\runtime\runs\` (read-only; 13 runs).
