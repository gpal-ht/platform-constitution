# PROPOSAL — 0.9 Audit Method & Rubric (Workshop 0.9-A)

> **Status: RATIFIED (Founder, 2026-07-18) — this is the fixed 0.9 audit standard.** The
> evidence discipline (§2), independence rules (§3), maturity rubric (§4), blocker-vs-gap test
> (§5), and IOA/CRR record shapes (§6–§7) govern the twelve assessments and the synthesis; the
> real-not-fixture rule for Partial is kept strict as recommended. This is the serialized
> meta-decision of [PROGRAM_0.9](PROGRAM_0.9.md): it
> fixes *how* the Constitutional Readiness audit judges every obligation, **before** any
> obligation is judged, so the twelve assessments and the synthesis are measured against one
> stated standard rather than an assessor's discretion. Non-constitutional (T1). It does not
> amend the roadmap or the constitution; it operationalizes the ratified 0.9 exit criterion.

| Field | Value |
|---|---|
| Derives from | [PROGRAM_0.9](PROGRAM_0.9.md) (kicked off + ruled 2026-07-18) · [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md) 0.9.0 |
| Governs | The four-lane audit: this rubric → 12 independent per-obligation assessments → conditional contradiction-resolution → synthesis (the Constitutional Readiness Report) |
| Ratified inputs | Independent-assessor model (assessor ≠ builder; Founder ratifies) · four-lane structure · named-gap-toward-Strong permitted at 1.0 (Founder, 2026-07-18) |
| Governing edge | **P2 first.** The audit's product is the *truth* about the platform. A verdict is claimed only where primary evidence is read and re-derived; a gap is recorded, never concealed; a passing verdict is never manufactured to reach 1.0. |
| Change class | T1 Operational (an audit-method refinement; the obligations, the 1.0 definition, and the independent-audit exit are already ruled in the roadmap and re-ruled at 0.9 kickoff) |
| Precedent | The ratified 0.5–0.8 bar discipline (artifact + demonstration + checker; real-not-fixture; honesty before completeness) — reused here and turned reflexively on the platform itself |

---

## 1. What the audit produces

- **One Independent Obligation Assessment (IOA) per obligation** (O1…O12) — an evidence-bound
  record, authored by an assessor that did not build that obligation, carrying a maturity
  verdict and an open-item classification (§4–§6).
- **One Constitutional Readiness Report (CRR)** — the synthesis over all twelve IOAs, stating
  the 1.0 determination (met / not-yet, with the honest reason). The CRR is the 0.9 exit
  artifact; the accountability office (Founder) ratifies it.

Both reuse the platform's existing independent-validation record shape where it fits (a
generator/validator separation, digest-bound citations) rather than inventing new machinery —
0.9 stays an audit, not a build.

## 2. Admissible evidence (the discipline, reused from 0.5–0.8)

An obligation's maturity claim stands on three things, each **named and checkable**:

1. **Artifact** — a thing that exists at a path, cited by content digest where the plane
   supports it (canonical records, released source + its tests, workflow validators, release
   manifests, run records). A claim with no artifact is Emerging at best.
2. **Demonstration** — a named run that actually happened, on the right kind of input.
   - **Real, not fixture:** a demonstration on a genuine artifact (a real WR, a real EDR, a real
     cross-repo projection) is required for **Partial**. Tests and fixtures prove the mechanism
     is *built* (they support Emerging and buttress Strong-breadth), but by themselves they do
     not lift an obligation to Partial — the ratified 0.5–0.8 rule, applied unchanged.
3. **Checker** — the **independent assessor** who verified (1) and (2) by reading the **primary
   evidence** and re-deriving the finding. A builder's release-note claim is a *pointer to
   check*, never the evidence itself.

Evidence that fails any of the three is recorded as such; the obligation does not borrow
maturity it cannot show.

## 3. Independence (operational)

- **Structural separation.** The assessor of obligation O is not the author/builder of O's
  mechanism. Independence is a property of *who assesses*, not of how careful they are.
- **Primary-evidence rule.** The assessor reads the artifacts, code, tests, and run records
  directly and re-derives the verdict. It does not accept "the release notes say it passes" as
  evidence — that is precisely the generation==validation collapse the platform forbids (P6).
- **Ratification.** The Founder, as accountability office, ratifies the synthesized CRR (and may
  reject or return any IOA). This is where the constitution's outstanding **Independent
  Reaffirmation Obligation** is discharged: the readiness claim is reaffirmed by an assessment
  independent of the Genesis builder-of-record.
- **O2 is assessed reflexively.** O2 (platform self-honesty, P2) is not audited by a separate
  mechanism — it *is* this audit. Its evidence is the audit's own conduct: gaps recorded, no
  verdict manufactured, every claim checked against primary evidence. If the audit itself cuts a
  corner, O2 fails by that fact.

## 4. The maturity rubric (bound to the constitutional clauses)

The scale is the roadmap's: **None · Emerging · Partial · Strong.** Operationalized so two
assessors reading the same evidence reach the same level:

| Level | Test (met only if ALL hold) |
|---|---|
| **None** | The obligation's mechanism does not exist in the platform. |
| **Emerging** | The mechanism is specified or partially implemented, and/or exercised only on fixtures/tests — never on a real artifact. |
| **Partial** | The mechanism is implemented **and demonstrated at least once on a real (non-fixture) artifact** (§2); **every** gap to Strong is named honestly; and **no architectural contradiction prevents Strong** (§5). *This is the per-obligation 1.0 bar.* |
| **Strong** | Partial, **and** the mechanism holds across the obligation's full relevant surface as its clause requires (every workflow / every plane / every decision), demonstrated broadly, with no consequential unnamed gap. |

The 1.0 threshold (ratified) = **every obligation ≥ Partial, and no known architectural
contradiction preventing Strong.** The audit therefore establishes, per obligation: (a) is it
≥ Partial on real evidence? and (b) is there any contradiction that would prevent it *ever*
reaching Strong within the ratified architecture?

## 5. The blocker-vs-gap test (the decision procedure)

Every open item recorded against an obligation is classified by this test — applied to
evidence, not to hope:

**An open item is a CONTRADICTION BLOCKING STRONG (blocks 1.0) iff either:**
- (a) reaching Strong would require **breaking a frozen contract or changing the ratified
  architecture** — not merely adding coverage within it; or
- (b) it **falsifies the Partial claim itself** — the "real demonstration" does not actually
  hold when the assessor re-derives it.

**An open item is a NAMED GAP TOWARD STRONG (permitted at 1.0) iff all hold:**
- the Partial claim stands on real evidence; and
- reaching Strong is **purely additive within the existing architecture** (more coverage, a
  deferred refinement); and
- where the item is **reality-gated** (awaiting a genuine triggering event — e.g. a real
  assumption invalidation), the **machinery is proven end-to-end** and only the triggering
  reality is absent.

Applied to the three known open items (the audit may still reclassify on evidence):
- **O12A-5** (one real invalidation propagated) — reality-gated; machinery fixture-proven →
  *named gap*, provided the assessor confirms the propagation machinery actually runs.
- **Cross-model re-run** (O12) — additive (a second model run against durable inputs); the
  honest degraded-reproducibility schema already stands → *named gap*, unless the assessor
  finds the "throughout their lifetime" clause is architecturally unsatisfiable as built.
- **O8 walk-via-git-objects** — additive refinement (resolve via git objects, not working-tree
  bytes); the durable pin holds today → *named gap* (P13).

## 6. The Independent Obligation Assessment (IOA) record — fields

Each obligation's assessment records, at minimum:

```
obligation_id            # O1..O12
principle                # the constitutional principle it serves
assessor                 # who; and the attestation that assessor != builder
clause_under_test        # the constitutional clause, quoted
evidence:                # >=1 entry; each is artifact + demonstration + checker
  - artifact             #   path (+ content digest where supported)
    demonstration        #   the real run/case that was exercised (real, not fixture)
    verified_by          #   how the assessor re-derived it from primary evidence
maturity_verdict         # None | Emerging | Partial | Strong (§4)
open_items:              # each classified by §5
  - description
    classification       # contradiction_blocking_strong | named_gap_toward_strong
    grounds              # the evidence for the classification
determination           # >= Partial? yes/no ; any Strong-blocker? yes/no
```

## 7. Synthesis → the 1.0 determination

The CRR aggregates the twelve IOAs and states exactly one of:
- **1.0 threshold MET** — every obligation ≥ Partial on real evidence, and every open item is a
  named gap toward Strong (no contradiction blocking Strong). 1.0 may be claimed on the
  Founder's ratification.
- **1.0 threshold NOT YET met** — at least one obligation is below Partial, or at least one open
  item is a contradiction blocking Strong. The CRR names it precisely; the conditional
  contradiction-resolution lane engages (the only place 0.9 builds), or 1.0 waits. **This
  outcome is the audit working, not failing** (P2).

The CRR carries no verdict the twelve IOAs do not support; the synthesis may not upgrade an
obligation its own assessment left short.

## 8. What this proposal asks the founder to ratify

The **evidence discipline (§2)**, the **independence rules (§3)**, the **maturity rubric (§4)**,
the **blocker-vs-gap test (§5)**, and the **IOA/CRR record shapes (§6–§7)** — as the fixed
standard the twelve assessments and the synthesis are measured against. Wherever the audit later
finds these need a refinement, that is a T1 change ruled openly, not an assessor's silent
discretion.
