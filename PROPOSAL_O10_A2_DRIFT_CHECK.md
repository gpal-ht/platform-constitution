# PROPOSAL — A2: Mechanical Model↔Projection Drift Check (DESIGN)

> **Status: PROPOSED (draft for founder ratification).** Design for deliverable **A2** from
> [PROGRAM_0.4](PROGRAM_0.4.md) Track A: *one* mechanical check that a projection is consistent with
> its authoritative model, so drift is **detected, not left to discipline** (P10: the forcing
> function is execution, not discipline). Traces to **P10 / O10**.

## The core finding: the check already exists

`engine/ekb.py` already ships the drift check as command **`packages`**
(`check_generated_packages`). A2 is therefore **not "build a checker"** — it is *specify, ratify as
the O10 drift gate, and make it non-optional for the one covered pair.*

**Covered pair (per [PROPOSAL_O10_SCOPE](PROPOSAL_O10_SCOPE.md), PROPOSED):**
authoritative model = EKB knowledge graph; projection =
`engineering_kb/generated/packages/EKP-ARCH-0001-subsystem-decision.md`.

---

## What it compares

For each generated projection in `generated/packages/`:

1. Read the projection's front matter: `primary_object` (or `generated_from`) and the declared
   `retrieved_objects` list.
2. Recompute the **live retrieval closure** from the authoritative graph:
   `retrieve(g, primary)` → the set of object IDs the model *currently* yields.
3. **Compare** declared closure vs live closure. Any set difference ⇒ `STALE — declared closure … !=
   current closure …`.
4. **Secondary drift signal:** scan the projection text for **legacy type tokens** (e.g. a
   pre-migration `engineering_decision`); presence ⇒ the projection was produced before a model
   migration ⇒ stale.
5. **Missing-metadata guard:** a projection that lacks `primary_object`/`retrieved_objects` cannot be
   verified ⇒ reported as a problem (not silently passed).

This is a **structural identity** comparison (does the projection's declared closure still equal the
model's closure?), which is exactly the P10 synchronization invariant at the projection's own
granularity. It deliberately does **not** diff prose bodies — that would be brittle and is not what
"synchronized" means here.

## How it fails closed

- `cmd_packages` returns **non-zero** whenever any projection is stale, invalid, or unverifiable, and
  prints each offender. Zero exit only when *every* projection matches the current graph.
- Unverifiable (missing metadata) is treated as a **failure**, not a pass — the check cannot be
  satisfied by omitting the fields it inspects. This is the "fail closed" property.
- The model side is recomputed from source every run, so the check cannot be fooled by a stale
  cached closure.

## Where it lives

- **Detection logic:** `engineering_kb/engine/ekb.py` (`check_generated_packages`, `cmd_packages`).
  No new location needed; keep the check co-located with the model and its validation boundary
  (A1 element 5).
- **Enforcement point (the "minimal enforcement" decision — founder picks ONE for Partial):**
  - **Option E1 — pre-release gate.** Add `ekb.py packages` (and `validate`) to
    `engineering_kb/scripts/validate-release.py` so a release cannot be cut with a stale projection.
    *Pro:* ties enforcement to the moment artifacts are published; matches the Release Plane. *Con:*
    drift can sit un-flagged between releases.
  - **Option E2 — required CI step.** A CI job runs `python engine/ekb.py packages` on every change
    to `engineering_kb`; red build blocks merge. *Pro:* catches drift at commit time. *Con:* needs CI
    wiring; depends on the repo's CI setup.
  - **Recommendation:** **E1 for Partial** (smallest, self-contained, no external CI dependency, and
    release is the point where an out-of-sync projection would actually mislead a consumer), with E2
    named as the deepening step. Either one satisfies "minimal enforcement"; the requirement is only
    that the check stop being purely manual.

## Implementation plan (specify + wire; minimal new code)

1. **Specify** (this doc + A1): declare `ekb.py packages` the O10 drift gate for the covered pair.
2. **Confirm green baseline** (done): `python engine/ekb.py packages` → *"all generated packages match
   the current graph"*; `python engine/test_engine.py` → **40 passed, 0 failed**.
3. **Wire enforcement** (founder picks E1 or E2). For E1: add a `packages`+`validate` call to
   `scripts/validate-release.py` with a non-zero exit on failure. ~10–20 lines, no new mechanism.
4. **Document** the gate in `engine/README.md` and the ratified A1 contract.
5. **No second checker.** Building a parallel drift checker is rejected (P13): it would not measurably
   improve traceability over the tested one that exists.

*All build steps land in `engineering_kb` via an isolated worktree (`feature/0.4-o10-drift`), staged
by explicit path, never merged to `develop` by Track A — the founder ratifies first.*

---

## A3 — Evidence (already present)

The pass + negative tests the exit bar asks for **already exist and pass** in
`engineering_kb/engine/test_engine.py`:

| Requirement | Existing test | Behavior |
|---|---|---|
| Check runs **green** on a real pair | `test_current_package_passes` | live closure == declared ⇒ `[]` (no problems) |
| **Deliberate drift is rejected** | `test_stale_package_detected_by_closure_mismatch` | declared `["DG-ARCH-0001","CON-ARCH-0001"]` != live 8-object closure ⇒ `STALE … closure` |
| Migration-drift rejected (bonus) | `test_stale_package_detected_by_legacy_token` | legacy `engineering_decision` token ⇒ flagged stale |
| End-to-end command | `python engine/ekb.py packages` | exit 0 today; would exit non-zero on any injected drift |

**Recommendation for A3:** *cite this evidence* rather than author redundant tests. If the founder
wants A3 to be visibly O10-labeled, add one thin test named for the obligation
(`test_o10_drift_gate_rejects_stale_projection`) that simply asserts the same behavior — optional,
cosmetic, not load-bearing.

### Optional prototype
A prototype is **not required** — the mechanism and both tests already exist and are green. If the
founder wants a fresh demonstration, Track A can, in the `feature/0.4-o10-drift` worktree, add the E1
wiring plus the optional O10-named test and show: (a) release-validate green on the current pair, then
(b) release-validate **red** after injecting a one-object closure change. No new detection logic.

---

## Scope guard (what A2 is NOT for Partial)
- **Not** the cross-repo `ecf` projection (`P-ecf`) — that needs commit-pin resolution and write
  access to `ecf` (forbidden now); it is the named deepening target.
- **Not** prose/body diffing — synchronization is defined at closure granularity, not text.
- **Not** a new checker — the existing `packages` command is the check.

## Founder rulings needed
1. Ratify `ekb.py packages` as the O10 drift gate for the covered pair? (Y/N)
2. Enforcement point: **E1** (release gate) or **E2** (CI step) for Partial? (pick one)
3. A3: cite existing tests, or also add the optional O10-named test? (cite / add)
4. Do you want the optional worktree prototype demonstration, or is citing the green suite enough?

## Metadata
| Field | Value |
|---|---|
| Owner (draft) | Track A owner (O10) |
| Status | **PROPOSED** — design of A2, awaiting ratification |
| Detection logic | `engineering_kb/engine/ekb.py` (`check_generated_packages`) — exists, tested |
| Evidence (A3) | `engineering_kb/engine/test_engine.py` (3 tests, green) — exists |
| Change class | T1 Operational |
| Cross references | [PROPOSAL_O10_SCOPE](PROPOSAL_O10_SCOPE.md) · [PROPOSAL_O10_A1_CONTRACT](PROPOSAL_O10_A1_CONTRACT.md) |
