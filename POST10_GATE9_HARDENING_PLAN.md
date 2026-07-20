# Post-1.0 Deepening Plan — O10 Gate-9 (drift forcing-function) Hardening

> **Status: EXECUTED (Founder ruling 2026-07-18: Phases 1+2, Option A; re-vendor deferred).**
> Shipped in **ECF v1.0.1**: Phase 1 (gate 9 checks a real, version-controlled reference
> projection of the bundled graph — no more vacuous pass) and Phase 2 (the cross-plane
> consumer-projection drift verifier, which surfaces context_switcher's real staleness). Two of
> the four O10 named-gaps toward Strong are closed; the consumer re-vendor is a deferred,
> separately-tracked consumer decision. See the "Execution record" at the end.
>
> Post-1.0 deepening, not a 1.0 gate: 1.0 is already ratified and does not depend on gate 9 (O10
> rests on the identity pin, gate 5). This was the top hardening item the 0.9 Constitutional
> Readiness audit surfaced — the sharpest single step of O10 from **Partial → Strong**.
> Non-constitutional (T1). Continues the thread of [PROPOSAL_O10_A2_DRIFT_CHECK](PROPOSAL_O10_A2_DRIFT_CHECK.md).

| Field | Value |
|---|---|
| Obligation | O10 — engineering-model synchronization (P10) |
| Derives from | [CONSTITUTIONAL_READINESS_REPORT_0.9](CONSTITUTIONAL_READINESS_REPORT_0.9.md) §5 + [audit/IOA-O10](audit/IOA-O10.md) open items 1 & 2 |
| Independent corroboration | Two assessors (O9, O10) converged on the finding without seeing each other's work |
| Change class | T1 Operational (additive; no frozen contract or ratified architecture change) |

## The problem (precisely)

`validate-release.py` **gate 9** shells `ekb.py packages` → `check_generated_packages`, which
compares each generated package's declared `retrieved_objects` closure against the live
`retrieve()` closure of the bundled graph, failing closed on a stale/legacy package. The
mechanism is real and fail-closed — **but it checks an empty set on every real release.**
Generated packages live under `generated/`, which is git-ignored in the vendored EKB and in the
manifest builder's `EXCLUDE_PARTS`, so **no projection is ever bundled**. `ekb.py packages` hits
its `if not GENERATED_PACKAGES_DIR.exists(): return 0` branch — "No generated packages
directory; nothing to check." — and gate 9 "passes" vacuously. Its fail-closed behavior is
proven **only by a fixture** that injects a stale package into the gitignored directory.

**Consequence:** the P10 drift forcing-function — whose whole job is "when an artifact drifts
from its model, execution breaks" — is a structural no-op on the real artifact. Real
synchronization *is* enforced (the gate-5 identity pin, which the audit watched pass on 0.8.3),
so this is a **named gap toward Strong**, not a 1.0 blocker — but it is a genuine weakness.

## Two facts that make this small

1. **The projection surface is one guide.** The bundled graph has a single decision guide
   (`DG-ARCH-0001`), so the canonical projection set gate 9 should check is essentially **one
   EKP**. This is not a fleet of generated artifacts — it is one file.
2. **A real drift already exists to catch.** The one real projection that does exist — the
   consumer EKP at `context_switcher/runtime/work_requests/WR-0001/engineering-knowledge-
   package.md` (`generated_from: DG-ARCH-0001`) — declares a **stale `ekb_version: v0.1-local`**
   and is checked by no gate. The hardening has a real target on day one, not a hypothetical.

## Options

| | Approach | Makes gate fire on real content | Cost / caveat |
|---|---|---|---|
| **A** | **Bundle the canonical EKP + check it.** Render the `DG-ARCH-0001` EKP from the bundled graph, commit it as a first-class canonical projection (un-ignore one path, e.g. `canonical_packages/`), digest-pin it in the release manifest; gate 9 runs the existing `check_generated_packages` on it. | ✅ Yes — one real shipped projection, digest-pinned | Commits one generated artifact. The drift-in-git risk it introduces is *exactly what the gate guards* — acceptable, and the tension is resolved by declaring this one projection **canonical**, not transient. |
| **B** | **Regenerate-and-verify (no commit).** At build time render the canonical EKP(s) from the graph and pin `{package_id: content_digest}` in the manifest; gate 9 **regenerates** from the bundled graph into a temp dir, runs `check_generated_packages`, and verifies each digest matches its pin. | ✅ Yes — and nothing generated is committed | Needs a **generator** in the vendored engine: today `ekb.py` only *checks* packages (no `cmd_generate`); generation lives in ecf's RETRIEVE-0002 executor. Porting a small `retrieve+render` generator is the extra work. Purest, most pin-by-digest-consistent. |
| **C** | **Consumer-projection drift gate.** Re-derive the consumer EKP's declared closure against the pinned graph and assert its declared `ekb_version` matches the pinned EKB; fix the stale `v0.1-local`. | ✅ Yes — catches the **real** existing drift | Cross-plane (O8+O10); the consumer EKP lives in gitignored `runtime/`, so this is a consumer-repo / cross-plane check, not an ecf-release gate. |

## Recommended path (phased)

- **Phase 1 — make the release gate real (Option A).** Given the one-guide surface, commit the
  single canonical `DG-ARCH-0001` EKP as a first-class projection, digest-pin it in the manifest,
  and point gate 9 at it. Update the fixture test to *also* prove fail-closed on (i) a real
  regenerated-vs-graph mismatch and (ii) a digest mismatch — so the forcing-function's
  fail-closed path is proven on real bundled content, not only an injected fixture.
  **Exit:** gate 9 checks ≥1 real projection on a real ECF release (never the empty set), and
  fails closed on a real drift.
- **Phase 2 — catch the real drift that exists (Option C).** Add the cross-plane consumer-EKP
  drift check and fix the stale `ekb_version: v0.1-local`. **Exit:** the real consumer projection
  is drift-verified against the pinned graph; the known staleness is closed.
- **Phase 3 — toward Strong (the remaining O10 named gaps).** (a) Regenerate-don't-commit
  (Option B) once a generator is warranted; (b) a declared **compatibility range** instead of the
  exact `0.2.1` pin (IOA-O10 item 3); (c) a **real migration** invalidating a real projection,
  end-to-end (IOA-O10 item 4). These lift O10 from Partial toward Strong.

## Honest constraints (P2)

- **Not urgent.** 1.0 stands without this; sequence it as ordinary deepening.
- **It may surface real drift.** Making the gate real could fail on the existing `v0.1-local`
  staleness — that is the gate *working*, and Phase 2 fixes the root cause.
- **A commits a generated artifact.** That is a deliberate trade (one canonical, gate-guarded,
  digest-pinned file) chosen because the surface is a single guide; Phase 3(a) removes it if the
  no-commit purity is later preferred.

## What this asks the founder to decide

1. **Adopt Phase 1 = Option A** (bundle-and-check the one canonical EKP) as the core, or hold for
   Option B (regenerate-don't-commit) from the start despite the generator work?
2. **Sequence** — Phase 1 alone now, or Phases 1+2 together (the consumer drift is where a real
   defect already lives)?

## Execution record (2026-07-18)

**Founder ruling:** Phases 1+2 together, Option A; build the drift verifier and **defer** the
context_switcher re-vendor. **Shipped in ECF v1.0.1.**

- **Phase 1 (done).** `scripts/build-reference-projection.py` renders ECF's canonical reference
  projection of the bundled graph to `release/reference-projections/` (one EKP per decision
  guide — currently `EKP-REF-DG-ARCH-0001`, closure of 8 objects), version-controlled and
  content-digested. Gate 9 (`scripts/check-reference-projections.py`, reusing the vendored
  engine's `check_generated_packages`) now **fails closed**: exit 2 = nothing to check (the
  vacuous pass removed), exit 1 = closure drift or legacy token. Gate-9 test rewritten: 5 cases.
- **Phase 2 (done).** `scripts/check-consumer-projection.py` re-derives a consumer EKP's closure
  against its pinned graph and reports CLOSURE-DRIFT (exit 1) / VERSION-LAG · PIN-SKEW (exit 3) /
  OK. Run against real `context_switcher` it surfaces the audit's finding: EKP built at EKB
  `v0.1-local`, consumer now pins `0.2.0`, released is `0.2.1` (exit 3). Test: 5 cases.
- **Deferred (tracked).** The context_switcher re-adoption (re-vendor ECF 1.0 / EKB 0.2.1,
  regenerate its projections, reconcile inconsistent pins) — a parked-repo decision, not gate
  work. The verifier reports OK once done.
- **Result:** closes O10 audit open items 1 (gate-9 vacuity) and 2 (consumer projection
  un-checked). Remaining toward Strong: item 3 (compatibility *range* vs exact pin) and item 4
  (a real migration demonstrated end-to-end). 1372 tests pass; all 11 release gates pass.
