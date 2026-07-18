# PROPOSAL — O8 Cross-Plane Provenance Scope (0.8)

> **Status: RATIFIED (Founder, 2026-07-17) — ratify all as recommended.** The finding that
> cross-plane provenance does not yet hold across the Control→Project boundary (8 of 9
> citations not digest-bound/durable) CONFIRMS the milestone premise and is handled by the
> bar's `unbound` honesty clause (O8-5, Clarification A). This resolves the four design-open
> items in [PROGRAM_0.8](PROGRAM_0.8.md) "Workshop O8 — Cross-Plane Provenance (P8)".
> It is a **scope/design** workshop: it recommends *what must be true* for cross-plane
> provenance to hold, grounded in the REAL cross-plane artifacts already in the repos,
> and proposes an O8 Partial-bar contribution as evidence-checkable clauses. **No build.**
> Everything here is PROPOSED; the founder rules. Non-constitutional (T1); it organizes
> 0.8 scope, it does not amend the roadmap or the architecture.

| Field | Value |
|---|---|
| Derives from | [PROGRAM_0.8](PROGRAM_0.8.md) (kicked off 2026-07-17) · [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md) 0.8.0 · [PLATFORM_ARCHITECTURE](PLATFORM_ARCHITECTURE.md) §4.1–4.3, §5, §9 |
| Obligation deepened | **O8 — Provenance is mandatory (P8)**, currently Strong/Partial *within Control*; 0.8 deepens it to hold **across the three plane boundaries** |
| Governing edge | **P2 first, then P8.** A cross-plane guarantee is claimed only where **demonstrated**; a boundary that does not yet hold is **recorded, not concealed** (Clarification A). Every retained hop is digest-bound (P8); a hop that is not is named as an explicit gap. |
| Precedent | [PROPOSAL_07_PARTIAL_BARS](PROPOSAL_07_PARTIAL_BARS.md) (ratified 2026-07-17) — clause discipline (artifact · demonstration · checker), real-not-fixture, named real identities, fixtures-prove-negatives, bar-vs-reality tracking |
| Evidence baseline probed | `ecf-wt-o8` @ `c02fe64` (= v0.7.0), read-only far ends `engineering_kb` and `context_switcher` main checkouts. Every finding below was measured, not assumed (§0). |
| Change class | T1 Operational (a deepening-scope workshop; the obligation and its cross-plane target are already in the roadmap and re-ruled at 0.8 kickoff) |

---

## 0. The single most important finding — cross-plane provenance does **not** hold today (measured)

Before any option, the honest baseline (P2). The three planes are three repos:
**Knowledge** = `engineering_kb`, **Control** = `ecf`, **Project** = `context_switcher`.
I walked every real cross-plane crossing in the store and hashed the far ends.

**Where it HOLDS today (digest-bound + durable):**

- **Control-internal and Control→Knowledge.** `EDR-0002`'s evidence bundle
  (`canonical/decisions/EDR-0002/evidence-manifest.yaml`) copies each mortal
  `runtime/` input into a tracked `evidence/*` file, each carrying `sha256` + an
  `origin_path` breadcrumb. The **Knowledge** hop is pinned in
  `release/release-manifest.json` → `bundled_ekb {source_commit:
  26750dca…, source_tag: v0.2.1, bundle_version: 0.2.1}`, and the EKB bytes are
  **vendored durably** into Control at `vendor/engineering_kb/` (which carries its
  own `release/release-manifest.json` with a `content_digest`). Those hops are the
  gold pattern and they verify.
- **The one lucky Project citation.** `CLOSURE-0002` evidence[0] pins the
  Project-plane ADR-0005 fully: `git blob e1797fe31b40ddf557d88fc58f9ccfeaff6c4f9f;
  sha256 a861cb72…b876a18a; LF-stable`. I re-hashed the live Project bytes:
  `a861cb72…b876a18a` — **an exact match, end-to-end, today.**

**Where it does NOT hold (the boundary being recorded, per Clarification A):**

- **The Control→Project boundary is unbound for 8 of 9 closure citations.** Across
  `CLOSURE-0001` (4 evidence refs) and `CLOSURE-0002` (5 evidence refs), **exactly one**
  (the ADR-0005 pin above) carries a content digest. The other **eight** are
  commit-pinned at best — `context_switcher: docs/evidence/MISS-0001-…md (develop @
  defa16f)` — or weaker still (`ADR-0006 … (Accepted 2026-07-13)` records no commit;
  `acceptance_tests/check_architecture_consistency.sh` records no pin at all). **None
  of the eight is digest-bound; none has a durable copy in Control.**
- **Those citations resolve today only by luck of an unrewritten branch.** I confirmed
  `develop @ defa16f` is currently reachable and the MISS-0001 dossier hashes to
  `1d0e27fa…`. But `develop` is a **moving, rewritable branch**, and CLOSURE-0001
  records **no digest** for that dossier — so a later reader cannot prove the cited
  bytes from the closure alone. A rebase, a `gc`, or a branch deletion in
  `context_switcher` breaks the citation **silently** — the P8 "mortal path" failure,
  across a repo boundary this time.
- **The EDR→Project hop is identity-only.** `EDR-0002`'s bundle references the origin
  Work Request as `work_request_id: WR-0001` — a bare identifier, **no digest, no
  durable copy** of the Project-plane WR. And `WR-0001` in `context_switcher` is stored
  **CRLF** (`git ls-files --eol` → `i/crlf w/crlf`), while Control normalizes to LF —
  so even a naive content digest would mismatch across the boundary (§3).
- **The 0.7 FD-2 durability rule fixed exactly one _Control-internal_ mortal pointer**
  (`CHG-20260716-0001/disposition.yaml`'s `runtime/` citation). It has **never been
  applied to a cross-repo citation**, and closures are outside its reach.

**So: within Control, O8 is real; across the Control→Project boundary, O8 is _asserted
but not demonstrable_ for the closures — the exact boundary 0.8 exists to close.** The
Control→Knowledge boundary already holds. This finding is the spine of every
recommendation below and of the proposed bar's negatives.

---

## Design-open item 1 — the cross-plane provenance CHAIN (machine-walkable, without opening every repo by hand)

**The question (PROGRAM_0.8):** is a consequential artifact's provenance machine-walkable
*across all three repos* — a canonical decision → its Control run → its Knowledge EKB pin
→ its Project Work Request / evidence? What record makes the chain traversable?

**What exists.** `tools/canonical_resolution/resolve.py` is a real, fail-closed resolver —
but it walks **only** the Control-internal decision→decision supersession chain
(`status`/`chain`/`current`). There is **no** resolver hop from a decision to its EKB pin,
to its Project WR, or to a closure's Project evidence. Those links exist as scattered fields
(`work_request_id`, `bundled_ekb`, closure `evidence[].ref`) with **no single walkable
record** and no resolver that crosses a repo boundary.

**Options.**

- **1A — Derived-on-read cross-plane resolver (extend `canonical_resolution`).** Add a
  read-only `walk` verb that, given an EDR, assembles the chain by reading the fields
  already present: EDR → `source_run_id`/`work_request_id` → `evidence-manifest` digests →
  `release-manifest.bundled_ekb` → closure records naming Project paths. Each hop is
  *derived* at read time from existing records; nothing new is stored.
  - *For:* no new artifact to drift (P10); reuses the ratified resolver idiom; single
    source of truth stays the underlying records.
  - *Against:* the resolver must reach **across repos** to verify the far ends (the Project
    bytes, the EKB bytes). Derived-on-read means the far repos must be *present and pinned*
    at walk time — which is exactly what does not hold today (§0). A derived walk over
    unbound citations produces a chain that *looks* complete but cannot verify (P2 risk).
- **1B — Recorded cross-plane provenance manifest (one per consequential artifact).** A new
  tracked record — e.g. `canonical/decisions/EDR-<id>/crossplane-manifest.yaml` — that
  **enumerates every cross-plane hop as an explicit, digest-bound edge**: `{plane, repo,
  ref, commit_or_tag, blob_id, content_sha256, durable_ref}`. The resolver walks *this*
  record; the record is the machine-walkable chain.
  - *For:* the chain is a **first-class artifact with its own provenance and durability
    obligations** (feeds items 2–4 directly); a reader walks one record, not three repos;
    the record can be checked by a gate at write time (the far bytes must exist and hash).
  - *Against:* a new record type to keep synchronized with its underlying fields (P10);
    risks becoming a *second* source of truth if it restates rather than *pins*.
- **1C — Hybrid: recorded edges, derived integrity (recommended).** Record the manifest of
  1B, but make every edge **a pin, not a copy of meaning** — each edge names the
  underlying record and its digest, and the resolver of 1A **re-derives and re-verifies**
  the chain from the manifest's pins on read (blob id resolves, content digest matches the
  durable copy). The manifest is *what to walk*; verification is *derived, never trusted*.
  The manifest never asserts a hop the far bytes cannot prove.

**Recommendation: 1C.** It resolves the derived-vs-recorded tension the item names in the
only P2-honest way: **record the edges** (so the walk needs one record, not three
repos and hand-labor), but **derive the verdict** (so a recorded edge that no longer
verifies **fails loud**, never passes on trust). It makes the manifest the natural home
for items 2 (durability per edge) and 3 (digest normalization per edge), and the walk
itself is the item-4 demonstration. Crucially, it is honest about §0: for the eight
unbound closure citations, the manifest edge is written with **no `content_sha256`/
`durable_ref`**, and the gate **records that edge as an explicit gap** — a walkable record
that *says where it cannot yet prove*, rather than a derived walk that silently omits the
weak hops.

---

## Design-open item 2 — cross-repo DURABILITY, generalized

**The question:** the 0.7 fix closed ONE mortal cross-repo pointer; O8 needs the durability
rule to hold for **every** cross-repo citation — a permanent Control record may cite a
Project/Knowledge path **only** digest-bound + durable. Reuse `tools/reproducibility/durability.py`.

**What exists — and its exact reach.** `durability.py` already states the general rule
cleanly: `DURABLE(ref) := ref is a tracked non-`runtime/` path OR a sha256-pinned copy
under a tracked path carrying an `origin_path` breadcrumb`, with a fail-closed checker
(`check_durable_ref` / `check_durable_refs`). But `MORTAL_ROOTS = ("runtime/",)` — the rule
today recognizes exactly one mortality mode: **gitignored `runtime/` in the same repo.** A
citation into *another repo's live branch* (`context_switcher: … (develop @ defa16f)`) is
**not** caught by `is_mortal_path` — it does not start with `runtime/` — yet it is *more*
mortal than a `runtime/` path, because the bytes live in a repo Control does not control and
on a branch that rewrites. The rule is right; its **mortality predicate is too narrow**.

**Options.**

- **2A — Widen `MORTAL_ROOTS` to treat every _foreign-repo_ ref as mortal.** A ref that
  names another repo (`context_switcher:`/`engineering_kb:` prefix, or any path resolved
  outside the Control repo root) is mortal-by-default unless it carries a durable in-Control
  copy. Same rule, broader predicate.
  - *For:* smallest change; the existing checker and its fail-closed shape carry over
    verbatim; directly generalizes FD-2.
  - *Against:* "durable" for a foreign ref can mean two different things — (i) a **copy of
    the bytes into Control** (as EDR bundles and the FD-2 remediation already do), or (ii) an
    **immutable content-address in the foreign repo** (a git blob id, which is permanent even
    if the branch moves). 2A alone does not say which; it must.
- **2B — Two-tier durability: prefer in-Control copy, accept immutable foreign
  content-address (recommended).** Define, for a cross-repo citation:
  - **Tier-1 (strongest) — durable in-Control copy.** The cited bytes are copied into a
    tracked Control path (the EDR-bundle / FD-2-sibling idiom) with `sha256` + an
    `origin_path` breadcrumb naming `{repo, commit, blob_id}`. Survives anything the far
    repo does. This is what the gold hops already do.
  - **Tier-2 (acceptable) — immutable foreign content-address.** The citation pins the
    **git blob id** (content-addressed, permanent under the object model, unaffected by
    branch movement) **and** a content digest with a declared normalization (§3). Verifiable
    whenever the far repo's object is reachable; **fails loud** when it is gc'd.
  - **Forbidden — a bare branch/commit citation with no digest** (the §0 state of the eight
    closure refs) and **a bare `runtime/` citation** (the FD-2 state). Both are mortal paths
    with no content anchor; the checker rejects them.
- **2C — Mandate Tier-1 for everything.** Every cross-repo citation must copy bytes into
  Control.
  - *For:* one rule, maximally durable, no dependence on the far repo at all.
  - *Against:* over-broad (P13) — copying every cited Project ADR into Control risks a second
    source of truth and mass duplication; some citations are *negative* (an amendment-trail
    "this does not supersede X") where the durable claim is "this text said N", well served
    by a Tier-2 blob-id pin. Reserve Tier-1 copies for load-bearing bytes.

**Recommendation: 2B**, implemented by **generalizing `durability.py`**: (a) add a
`foreign-repo` mortality mode so `check_durable_ref` treats an un-pinned cross-repo ref as
mortal; (b) extend the durable-entry field set to carry `{repo, commit, blob_id,
content_sha256, normalization}` for Tier-2, keeping `durable_ref`+`sha256` for Tier-1; (c)
expose a **checker/gate** (`check_crossplane_refs`) that the item-1C manifest gate and a
closure/evidence linter call — fail-closed, reasons-listed, exactly like the existing
`check_durable_refs`. This reuses the ratified module and its idiom; it does **not** build a
new store, and it stays scoped (P13) — Tier-1 for bytes that must survive, Tier-2 for
citations whose content-address suffices. The general rule, stated once:

> **A permanent Control record may cite a Project/Knowledge path only if the citation is
> DURABLE: either a digest-bound in-Control copy (Tier-1) or an immutable foreign
> content-address — git blob id + normalized content digest (Tier-2). A bare
> branch/commit/`runtime/` citation with no content anchor is REJECTED (fail-closed).**

---

## Design-open item 3 — digest AGREEMENT across planes (the CRLF/digest tension, grounded in reality)

**The question:** a Project-plane dossier cited by a Control closure must be pinned so a
later reader can prove the cited bytes, across divergent repo commit/line-ending states.

**The measured reality (decisive).** `tools/artifact_fingerprint/fingerprint.py` hashes
**raw bytes in binary mode — it does not normalize line endings.** So a content digest is
**line-ending-sensitive**, and the planes disagree on line endings *at the file level*:

- Control (`ecf`) normalizes its own records to LF (`git ls-files --eol` on every EDR/closure
  record → `attr/text eol=lf`).
- In Project (`context_switcher`), **ADR-0005 is LF** (`i/lf w/lf`) but **WR-0001 is CRLF**
  (`i/crlf w/crlf`) — the very Work Request at the head of the EDR-0002 chain.

This is exactly why `CLOSURE-0002`'s ADR-0005 pin verifies today and why the human hand-wrote
the qualifier **"LF-stable"**: the digest is only meaningful because the file is LF *and stays
LF*. That qualifier is a human doing by hand what a rule must enforce. A raw-byte digest of a
CRLF Project file, recomputed by a reader whose checkout normalized it to LF (or vice-versa),
**mismatches** — a false P8 failure — while a reader who happens to match the stored EOL sees
a false pass. Neither is a proof.

**Options.**

- **3A — Pin the git blob id (content-address), not a recomputed digest.** A blob id is
  computed by git over the bytes *as that repo stores them* and is immutable. `CLOSURE-0002`
  already does this (`git blob e1797fe…`). A reader verifies by `git cat-file`, no
  re-hashing, no EOL ambiguity.
  - *For:* zero normalization ambiguity; permanent under the object model; already in use.
  - *Against:* proves *which git object*, not *what a normalized reader sees*; requires the
    far repo's object to be reachable; two repos storing the "same" text with different EOL
    have **different** blob ids, so it does not prove cross-plane *content* equality, only
    object identity.
- **3B — Declare a normalization and pin the normalized content digest.** Record
  `content_sha256` computed over **LF-normalized** bytes plus an explicit
  `normalization: lf` field. Any reader normalizes-then-hashes and gets the same digest
  regardless of their checkout's EOL.
  - *For:* proves *content* across the boundary, EOL-independent; a reader on any platform
    reproduces it; directly kills the CRLF tension.
  - *Against:* requires a normalization step the current `fingerprint.py` does not do (a
    small, additive `sha256_normalized` alongside the raw `sha256_file` — the raw hasher is
    untouched); "LF" is a choice that must be recorded, not assumed.
- **3C — Pin both, and record the normalization (recommended).** Every cross-plane content
  pin carries **three fields**: `blob_id` (immutable object identity — 3A), `content_sha256`
  + `normalization: lf` (EOL-independent content proof — 3B), and (for Tier-1) the
  `durable_ref` in-Control copy whose bytes are the LF-normalized truth. A reader can prove
  the object *and* the normalized content; a Tier-1 copy sidesteps the tension entirely
  because the pinned bytes then live under **one** repo's normalization regime.

**Recommendation: 3C.** It is what the one working pin (`CLOSURE-0002` ADR-0005) already
gropes toward by hand — blob id + sha256 + a "LF-stable" note — turned into a **rule with a
recorded normalization field** so no future pin depends on a human remembering to write
"LF-stable". Concretely: extend `fingerprint.py` with an additive `sha256_normalized(path,
normalization="lf")` (raw `sha256_file` unchanged, so nothing existing breaks), and require
cross-plane pins to carry `{blob_id, content_sha256, normalization}`. The WR-0001 CRLF case
is the fixture proof: a pin that records only a raw `sha256` with **no** `normalization`
field is **rejected** (it cannot be reproduced across the boundary); a pin that records
`content_sha256` over LF-normalized bytes + `normalization: lf` **verifies** whether the far
file is CRLF or LF. For load-bearing bytes, the Tier-1 in-Control copy is preferred, which
makes the normalization question moot for that hop.

---

## Design-open item 4 — what "holds across planes" DEMONSTRABLY means (the O8 bar contribution)

**The question:** the bar is a real artifact whose provenance is walked end-to-end across all
three repos and **every hop digest-verifies**. Fixtures prove the negatives; the real walk is
the integration act.

**What the real walk looks like (the natural anchor).** The end-to-end chain already exists
in fragments and can be made to verify with the least new machinery around **EDR-0002**,
because its Control-internal and Knowledge hops already hold (§0):

```
Project WR-0001  ──▶  RUN-REASON-20260716-0002  ──▶  EDR-0002 (canonical)  ──▶  EKB v0.2.1
(context_switcher)     (Control run + evidence)       (Control decision)         (engineering_kb,
   [Tier-2 pin]           [digest-bound bundle]         [record sha256]           vendored + pinned)
        ▲                                                    │
        └──────────  CLOSURE-0001/0002 evidence  ◀───────────┘  (Project dossiers/ADRs:
                     [Tier-1 copy or Tier-2 pin]                  today unbound — must be pinned)
```

The **integration act** is: run the item-1C resolver `walk EDR-0002`, and have **every** hop
digest-verify — the Control bundle (already passes), the EKB pin (already passes), the
Project WR pin (needs a Tier-2 blob-id + normalized-digest pin — item 3), and the closure
Project-evidence pins (need Tier-1/Tier-2 durability — items 2, 3). A walk in which one hop
does not verify **fails the bar** — and that failing walk is itself the P2-honest record of
the boundary that does not yet hold.

**Recommendation for item 4:** the bar is discharged by **one real walk over one real
artifact (`EDR-0002`) in which every retained hop digest-verifies across all three repos**,
plus the durability + normalization pins (items 2, 3) that make the two weak hops (Project WR,
closure evidence) verify — and an **honest record of any hop that cannot be made to verify at
0.8** (e.g. a cited Project dossier whose bytes are no longer reachable is recorded `unbound`,
not silently dropped). Fixtures prove the negatives; the `EDR-0002` walk is the real act, named
by identity the way `EDR-0002`/`APPROVAL-0002`/`CLOSURE-0001` were named at 0.5–0.7.

---

## Part II — Proposed O8 Partial-bar contribution (evidence-checkable clauses)

Same discipline as the ratified 0.7 bar: each clause has (a) a named **artifact** that
exists, (b) a named **demonstration** actually run, (c) a named **checker**. A clause with an
artifact but no demonstration, or a demonstration nobody checked, is an **explicit gap**,
never a pass (P2). Checker vocabulary: **Machine (fail-closed contract)** · **Independent
validator (O5/P6)** · **Founder** (the only checker who can mark a clause *ratified*). Every
REAL clause discharges by **naming the identity of the real record it produced**.

### The clauses

**O8-1 — A machine-walkable cross-plane chain exists for one real consequential artifact
(P8).** The item-1C cross-plane manifest + resolver `walk` renders the provenance of a REAL
canonical decision (`EDR-0002`) as an enumerated edge set spanning all three repos
(Project WR → Control run/evidence → Control decision → Knowledge EKB → Project closure
evidence). *Artifact:* the `crossplane-manifest` for `EDR-0002` + the `walk` verb.
*Demonstration:* `walk EDR-0002` returns the full ordered chain. *Checker:* Machine
(resolver contract) + independent validator (the chain is derived from the underlying
records, not hand-authored).

**O8-2 — Every RETAINED hop in the walk digest-verifies (P8).** For each edge the manifest
retains, the resolver re-derives and re-verifies the pin: the git object resolves and the
normalized content digest matches. *Artifact:* the per-edge `{blob_id, content_sha256,
normalization, durable_ref?}` pins. *Demonstration:* `walk --verify EDR-0002` re-hashes every
retained edge and passes. *Negative (fixture):* **a walk in which any retained hop's digest
does not match is REJECTED** — a broken hop fails the whole walk, never a best-effort pass.
*Checker:* Machine (fail-closed verify) + independent validator.

**O8-3 — Cross-repo durability holds for every retained cross-plane citation (P8; generalizes
FD-2).** Every retained edge into Project/Knowledge is DURABLE per the item-2B rule —
Tier-1 in-Control copy or Tier-2 immutable content-address — checked by the generalized
`durability.check_crossplane_refs`. *Artifact:* the durable copies / content-address pins.
*Demonstration:* the checker passes on the retained edges. *Negatives (fixtures): **(i) a
permanent Control record citing a Project/Knowledge path with NO digest FAILS P8** (the §0
state of the eight closure citations); **(ii) a citation into a foreign live branch with no
content anchor is a MORTAL path and FAILS** (generalized FD-2); **(iii) a bare `runtime/`
citation still FAILS** (the original FD-2 negative, unregressed).* *Checker:* Machine
(fail-closed) + independent validator.

**O8-4 — Cross-plane digest agreement is normalization-declared (P8; the CRLF resolution).**
Every retained content pin carries an explicit `normalization`, and verification is
EOL-independent. *Artifact:* the `content_sha256` + `normalization: lf` fields;
`fingerprint.sha256_normalized`. *Demonstration:* a real Project file stored **CRLF**
(`WR-0001`) verifies against its LF-normalized pin regardless of the reader's checkout EOL.
*Negative (fixture): **a pin recording only a raw byte digest with no `normalization` field
is REJECTED** (unreproducible across the boundary — the CRLF/digest trap).* *Checker:*
Machine (fail-closed) + independent validator.

**O8-5 — The walk names an honest boundary where a hop cannot verify (P2, Clarification A).**
A hop whose far bytes cannot be pinned at 0.8 is recorded `unbound` in the manifest and
surfaced by the walk as an explicit gap — never silently omitted. *Artifact:* the `unbound`
edge record + the walk's gap report. *Demonstration:* a real currently-unbound citation
(a `CLOSURE-0001` Project dossier with no digest) is walked and reported as a named gap, not
a pass. *Negative: **a walk that reports "complete" while an edge is unverified FAILS P2** —
a partial walk dressed as a whole one is worse than an honest gap.* *Checker:* Machine + Founder
(confirms the boundary is recorded, not concealed).

**O8-6 — The walk detects and reports; it grants no cross-plane standing (P7).** The resolver
is READ-ONLY (the ratified `resolve.py` property, extended across planes): it walks, verifies,
and reports; it never writes a pin, never copies bytes across a boundary on its own authority,
never confers acceptance/approval across a plane. *Artifact:* the resolver's read-only surface.
*Demonstration/Negative: **the resolver attempting to write a manifest, mint a durable copy, or
mark a cross-plane edge "accepted" is REFUSED**; durable copies are minted by a separate
human-invoked tool (the FD-2 remediation idiom).* *Checker:* Machine (fail-closed refusals) +
Founder.

### The three required negatives, stated sharply (fixtures prove these; they never discharge the real clauses)

1. **A cross-repo citation with no digest FAILS P8 (O8-3-i).** This is the §0 reality: eight
   of nine closure citations. The bar's teeth is that this state is a *failure*, not the
   baseline — a Control record permanently citing Project bytes it cannot prove is precisely
   the concealment P8/P2 forbid.
2. **A mortal cited path FAILS (O8-3-ii/iii).** A citation into another repo's live branch
   (rewritable, gc-able) with no content anchor is mortal — *more* mortal than `runtime/`,
   because Control does not even own the repo. Generalizes FD-2 from one exposure to the rule.
3. **A broken hop in the walk FAILS the walk (O8-2).** An end-to-end walk in which any
   retained hop's digest does not match is rejected whole — never a partial/best-effort pass.
   A chain is only as walkable as its weakest verified hop.

### REAL-not-fixture discipline

Fixtures are **required** (they are the only honest way to prove the three negatives above),
but **fixtures never discharge O8-1, O8-2, O8-4 for the real artifact.** The real walk is over
`EDR-0002` and the real records around it (`RUN-REASON-20260716-0002`, `CLOSURE-0001/0002`,
`release-manifest.bundled_ekb`, `WR-0001`), each named by identity. A walk over a fixture
decision, however green, discharges nothing real.

### Deliberately OUT of the Partial bar (P13 / P2 — the honest ceiling)

- **Every consequential artifact walking cross-plane.** The bar is **one** real walk
  (`EDR-0002`). A universal walk over all decisions is deepening.
- **Two-way / consumer-initiated walk (B2 projection).** Making `context_switcher` walk *back*
  into Control from a projected decision is the B2 carryover — real-anchor-adjacent but
  deepening; the 0.8 bar walks Control→out, not consumer→in.
- **Automatic re-pinning when a far repo moves.** The bar *detects* a broken hop (O8-2/O8-5);
  a daemon that re-mints durable copies when `context_switcher` rebases is deepening.
- **Tier-1 copies of all cited Project bytes.** Reserve in-Control copies for load-bearing
  bytes (P13); negative/amendment-trail citations are well served by Tier-2 content-address.
- **Cross-plane digest *canonicalization* (B1 EKB).** Normalization here is declared-LF for
  the pin; a general canonical content form for the EKB remains the deferred, non-gating B1.
- **Retroactively binding the eight unbound closure citations.** The bar requires they be
  *recorded as gaps honestly* (O8-5) and that the **rule** reject the shape going forward
  (O8-3); rebinding historical closures (write-once P14) is a separate remediation act, like
  FD-2's sibling — not folded into the Partial bar.

---

## Part III — Cross-consistency with PROGRAM_0.8's constitutional edges

1. **P2 first (honored and made testable).** §0 records the boundary that does not hold rather
   than concealing it; O8-5 makes "record the gap, never fake the walk" a fail-closed clause;
   the OUT list is the honest ceiling. **Consistent** — the bar is structured so "cross-plane
   provenance is solved" is *unclaimable*: `unbound` edges and the gap report are load-bearing.
2. **P8 is the substrate, made concrete across the boundary.** "Every cross-plane hop is
   digest-bound; no permanent record cites a mortal path" maps clause-for-clause: retained hops
   verify → O8-2; cross-repo durability → O8-3 (generalizing FD-2); normalization-declared
   agreement → O8-4. **Consistent.**
3. **P7 honored across the boundary.** "No automation grants approval/acceptance across a
   boundary; cross-plane projection is read-only and human-gated" → O8-6 (the resolver walks
   and reports, never writes or confers standing; durable copies are human-invoked, the FD-2
   idiom). **Consistent** with §4.2/§9 architecture (a plane boundary is crossed only by
   versioned interface + provenance, never by internals).
4. **P6 not weakened (records-only seam to O5).** The walk *verifies digests*; it does not
   *validate content* — whether the cited Project bytes are the *right* evidence is an O5/P6
   question. O8's checker is a machine digest-verifier, distinct from an independent content
   validator; the O5 seam is consumed records-only, not depended on (per the isolation
   constraint). **Consistent.**
5. **Reuses ratified machinery, adds no premature store.** `durability.py` (generalized, not
   rebuilt), `canonical_resolution/resolve.py` (extended read-only, fail-closed idiom intact),
   `artifact_fingerprint` (additive normalized hasher, raw hasher untouched), the
   EDR-bundle / FD-2-sibling durable-copy idiom (reused for Tier-1). No new store, no daemon,
   no EKB canonicalization. **Consistent with P13.**
6. **Tension flagged (honesty-guarding) — the real walk may not fully verify at 0.8, and that
   is a recorded outcome, not a failure to manufacture.** Eight closure citations are unbound
   today (§0); some cited Project commits may not stay reachable. The bar is written so that if
   a hop cannot be bound by real bytes, it is recorded `unbound` (O8-5) and the walk is honest
   about it — the O8 analogue of the 0.7 "never manufacture an invalidation" guard. A green
   end-to-end walk is the target; an honestly-gapped walk is a **pass of the bar as written**
   (the boundary is recorded), and a walk *claimed* green over an unverified hop is the P2
   failure the bar exists to forbid.

---

## Appendix A — Spec-level sketch (manifest + resolver + generalized checker)

**Not a build.** Shapes only, to make the four recommendations concrete and checkable.

### A.1 Cross-plane provenance manifest (item 1C) — `canonical/decisions/EDR-<id>/crossplane-manifest.yaml`

```yaml
schema_version: "0.1.0"
record_type: crossplane_provenance_manifest
subject: { plane: control, repo: ecf, edr_id: EDR-0002 }
edges:
  - hop: origin_work_request
    plane: project
    repo: context_switcher
    ref: work_requests/WR-0001-repository-integration-subsystem.md
    commit: <sha>                       # breadcrumb
    blob_id: <git-blob-id>              # immutable object identity (item 3A)
    content_sha256: <lf-normalized>     # EOL-independent content proof (item 3B)
    normalization: lf                   # REQUIRED; a pin with none is rejected (O8-4)
    durability: tier2_content_address   # tier1_in_control_copy | tier2_content_address
    durable_ref: null                   # set for tier1 (an in-Control copy path)
  - hop: control_evidence_bundle
    plane: control
    repo: ecf
    ref: canonical/decisions/EDR-0002/evidence-manifest.yaml
    content_sha256: <...>
    normalization: lf
    durability: tier1_in_control_copy   # already holds today
  - hop: knowledge_ekb_pin
    plane: knowledge
    repo: engineering_kb
    ref: release/release-manifest.json#bundled_ekb
    source_tag: v0.2.1
    source_commit: 26750dca...
    durable_ref: vendor/engineering_kb/  # vendored durable copy in Control (holds today)
    durability: tier1_in_control_copy
  - hop: closure_project_evidence
    plane: project
    repo: context_switcher
    ref: docs/evidence/MISS-0001-change-driver-analysis.md
    commit: defa16f
    blob_id: null                       # NOT pinned today
    content_sha256: null                # NOT pinned today
    status: unbound                     # O8-5: recorded gap, never silently dropped
```

### A.2 Resolver verb (item 1A/1C) — extends `tools/canonical_resolution/resolve.py`

```
resolve.py walk EDR-0002              # emit the ordered cross-plane chain from the manifest
resolve.py walk --verify EDR-0002     # re-derive + digest-verify every RETAINED hop; fail-closed
                                      # exit 0 = every retained hop verifies (unbound hops reported)
                                      # exit 1 = a retained hop failed to verify (broken-hop → whole walk fails, O8-2)
```
Read-only (O8-6): `walk` never writes the manifest, never mints a durable copy, never confers
standing. It reuses the `ResolutionRefused(reasons)` fail-closed idiom already in `resolve.py`.

### A.3 Generalized durability checker (item 2B) — extends `tools/reproducibility/durability.py`

```python
# add a foreign-repo mortality mode alongside the existing runtime/ mode
FOREIGN_REPO_PREFIXES = ("context_switcher:", "engineering_kb:")   # + out-of-root path resolution

def check_crossplane_ref(edge, repo_root=None, *, verify=True) -> list:
    """Fail-closed. Reasons empty == durable. A cross-plane edge is DURABLE iff:
      tier1: durable_ref is a tracked in-Control copy + sha256 (reuses check_durable_ref), OR
      tier2: blob_id present AND content_sha256 present AND normalization declared.
    REJECTS: a foreign-repo ref with no content anchor (generalized FD-2);
             a bare runtime/ ref (original FD-2, unregressed);
             a content pin with no `normalization` field (item 3 / O8-4)."""
```
The raw `sha256_file` is untouched; a new additive `fingerprint.sha256_normalized(path,
normalization="lf")` provides the EOL-independent digest for Tier-2 verification.

---

## Metadata

| Field | Value |
|---|---|
| Status | **RATIFIED (Founder, 2026-07-17)** — O8 authorized to build; fingerprint.py change is additive (no T4) |
| Owner Role | Program Steward (WS-0) |
| Change class | T1 Operational (a deepening-scope workshop; obligation + cross-plane target already roadmapped and re-ruled at 0.8 kickoff) |
| Derives from | [PROGRAM_0.8](PROGRAM_0.8.md) · [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md) 0.8.0 · [PLATFORM_PRINCIPLES](PLATFORM_PRINCIPLES.md) (P8, P2 + Clarification A, P6, P7, P13) · [PLATFORM_ARCHITECTURE](PLATFORM_ARCHITECTURE.md) §4.1–4.3, §5, §9 · [PROPOSAL_07_PARTIAL_BARS](PROPOSAL_07_PARTIAL_BARS.md) (bar discipline, ratified) |
| Evidence probed | `ecf-wt-o8` @ `c02fe64` (v0.7.0), read-only: `canonical/decisions/EDR-0002/{EDR-0002.md, evidence-manifest.yaml, reproducibility-state.yaml, evidence/*}`, `information_closures/{CLOSURE-0001.yaml, CLOSURE-0002.yaml, README.md}`, `challenges/CHG-20260716-0001/{disposition.yaml, durable-evidence-manifest.yaml, durable-evidence/*}`, `release/release-manifest.json`, `vendor/engineering_kb/`, `tools/reproducibility/{durability.py, remediate_fd2.py, README.md}`, `tools/canonical_resolution/resolve.py`, `tools/artifact_fingerprint/fingerprint.py` · read-only far ends: `context_switcher` (`git ls-files --eol` + `git cat-file` on ADR-0005 [verified sha256 a861cb… matches CLOSURE-0002 pin], WR-0001 [CRLF], MISS-0001 dossier @ defa16f), `engineering_kb` (vendored pin) |
| Cross references | [PROPOSAL_06_PARTIAL_BARS](PROPOSAL_06_PARTIAL_BARS.md) · [PROPOSAL_05_PARTIAL_BARS](PROPOSAL_05_PARTIAL_BARS.md) · [PLATFORM_ARCHITECTURE](PLATFORM_ARCHITECTURE.md) FD-2 (durability, folded) · O5/O1 workshops (records-only seams; not depended on) |
```
