# PLATFORM_RELEASE_STRATEGY

> How the platform's repositories are released together so that a release remains
> **reproducible** (P8, P9) and its identity remains **intelligible** (P1) and
> **challengeable** (P3). Non-constitutional; a governance mechanism under the Root
> Governance Primitive (authorized disposition + versioned effect).
>
> **Status: Draft (Descriptive).** This document records the *current* coordinated-release
> practice observed at version 0.2.0. It was not produced in a workshop; changes follow the
> governance cycle. Full release automation is a **Planned** capability (roadmap 0.9).

---

## The platform is released as a coordinated set

The platform comprises three coordinated repositories, released together:

| Plane | Repository | Package |
|---|---|---|
| Knowledge Plane | `engineering_kb` | `@gpal-ht/engineering-kb` |
| Control Plane | `ecf` | `@gpal-ht/ecf` |
| Project Plane | `context_switcher` | `@gpal-ht/context-switcher` |

**Dependency chain (exact pins):**

```
context_switcher  pins  ecf  (exact commit)
        ecf       pins  engineering_kb  (exact commit)
context_switcher's nested engineering_kb  ==  ecf's bundled engineering_kb   (identity match required)
```

At 0.2.0 these were **private Git releases**: tagged commits with exact upstream pins. No
`npm publish`; no GitHub Releases. That posture is the current default and is itself subject
to governance if it changes.

---

## Release-manifest identity model *(Critical Release-Manifest Rule)*

- **Non-recursive manifest.** A committed manifest **never asserts its own containing
  commit** — doing so would create a self-reference loop. Release-content identity is a
  **content digest / exact upstream pins**.
- **`git_commit` is best-effort provenance**, excluded from equality and drift checks. The
  authoritative tag→commit binding is the release attestation (e.g. `git rev-list -n1
  v0.2.0` in the containing repository), not a field the manifest asserts about itself.
- **Identity match across nesting.** The bundled and nested copies of a lower plane must
  resolve to the *same* content identity (e.g. Context Switcher's nested EKB must equal ECF's
  bundled EKB).

> **Operational note (known environment gotcha):** after a checkout, a `content_digest`
> validation step can fail on line-ending normalization (CRLF/LF) even when the content is
> byte-for-byte identical to the tag. Treat a digest mismatch as a *line-ending* suspect
> before treating it as a *content* change. This is a validation-environment concern, not a
> release-integrity failure.

---

## What a coordinated release must guarantee

Derived from the constitution; enforced by the Release Plane.

1. **Reproducibility (P8, P9):** every released component is a versioned, tagged commit with
   exact upstream pins, so the exact set can be reconstructed.
2. **Provenance admissibility (P8):** a release is inadmissible if pins are missing,
   identities fail to match across nesting, or content digests are inconsistent (line-ending
   caveat above).
3. **Self-honesty (P2):** the release result states exactly what was and was **not** done
   (e.g. "npm not published, GitHub Releases not created, no history rewriting after tags").
4. **Independent validation (P6):** release validation is separate from release production;
   validation does not execute live generation workflows.
5. **Corrigibility (P14):** a superseding release replaces a prior one with migration
   obligations while the prior release remains in history — it is never rewritten.

---

## Backward compatibility

Consistent with the framework's own roadmap philosophy (validate before expanding; maintain
backward compatibility; breaking changes rare and documented):

- Consumers depend on a **declared version** of an upstream contract, not on an eternally
  frozen schema (see O10 — *versioned and stable, not frozen*).
- Contract changes to cross-cutting semantics (provenance identity/digest, validation,
  compatibility) require compatibility + migration review and coordinated versioning across
  planes (see [PLATFORM_PARALLELIZATION](PLATFORM_PARALLELIZATION.md) rule 4).

---

## Governance of releases

A release is an instance of the Root Governance Primitive at **release scope**:

| Cycle stage | Release form |
|---|---|
| Scope & authority | which components, which versions, which authority approves |
| Proposal | the intended coordinated version set + pins |
| Evidence | validation results, digest/identity checks, "what was NOT done" statement |
| Independent challenge | release validation independent of production (P6) |
| Authorized disposition | release approved / deferred / rejected |
| Versioned effect | tags, pins, manifest, attestation |
| Monitored reconsideration | supersession / hotfix triggers |

Whether a document change requires **release synchronization** is specified in
[PLATFORM_GOVERNANCE](PLATFORM_GOVERNANCE.md); constitutional documents in `C:\Dev\platform`
govern all repositories but are **not** part of a repository release.

---

## Metadata

| Field | Value |
|---|---|
| Owner | Founder |
| Status | **Draft (Descriptive — current practice at 0.2.0)** |
| Document Version | 0.1.0 |
| Applies To | `engineering_kb`, `ecf`, `context_switcher` |
| Review Cadence | Quarterly, or on any change to the release model |

### Decision history
- **0.1.0** — Documented from the observed coordinated release at 0.2.0
  (`context_switcher/PLATFORM_RELEASE_0.2.0.md`): private Git releases, non-recursive
  manifest, content-digest identity, exact upstream pins. Not workshopped; recorded
  descriptively.

### Open questions
- **Release automation** (roadmap 0.9) — releases are currently validated manually.
- **Publication posture** — whether/when to move beyond private Git releases (npm, GitHub
  Releases) is an open governance decision, not assumed here.

### Cross references
- [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md) · [PLATFORM_GOVERNANCE](PLATFORM_GOVERNANCE.md) · [PLATFORM_PARALLELIZATION](PLATFORM_PARALLELIZATION.md) · [PLATFORM_CAPABILITY_MAP](PLATFORM_CAPABILITY_MAP.md)
