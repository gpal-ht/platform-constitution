# Constitutional Readiness Report (CRR) — Milestone 0.9

> **Status: RATIFIED (Founder, 2026-07-18) — the 1.0 constitutional threshold is determined MET.**
> The Founder, as accountability office, ratified this report with eyes open on the honest caveats
> (nine obligations at Partial with named gaps; the gate-9 vacuity finding; O12 at the floor), and
> authorized claiming **1.0.0 — Constitutional Baseline**. The Independent Reaffirmation Obligation
> is thereby discharged. This is the 0.9 exit artifact required by
> [PLATFORM_ROADMAP](PLATFORM_ROADMAP.md) 0.9.0 — *"an independent, evidence-backed report [that]
> shows every obligation ≥ Partial with no contradiction blocking Strong."* It synthesizes the
> twelve Independent Obligation Assessments (IOAs) in [audit/](audit/) under the ratified method
> [PROPOSAL_09_AUDIT_METHOD](PROPOSAL_09_AUDIT_METHOD.md). It carries **no verdict its IOAs do not
> support** and upgrades no obligation its own assessment left short (method §7). The
> accountability office (Founder) ratifies; until then nothing here claims 1.0.

| Field | Value |
|---|---|
| Milestone | 0.9.0 — Constitutional Readiness |
| Method | [PROPOSAL_09_AUDIT_METHOD](PROPOSAL_09_AUDIT_METHOD.md) (RATIFIED, Founder, 2026-07-18) |
| Evidence base | 12 IOAs: [audit/IOA-O1.md](audit/IOA-O1.md) … [audit/IOA-O12.md](audit/IOA-O12.md) |
| Independence | Each obligation assessed by an assessor structurally separate from its builder; each re-derived from primary evidence (method §3) |
| Change class | T1 Operational (the readiness *assessment*; the 1.0 definition and the audit exit are ratified in the roadmap) |

---

## 1. Determination

**The 1.0 constitutional threshold is MET on the evidence: every one of the twelve obligations is
≥ Partial on real (non-fixture) evidence, and no assessment found a contradiction blocking
Strong.** Every open item across all twelve is classified as a *named gap toward Strong*, which
the ratified 1.0 definition explicitly permits.

This determination is offered for the Founder's ratification. Per the constitution, **1.0 is not
claimed until that ratification is granted** — this report recommends it; the human decides (P7).

## 2. Results

| # | Obligation (principle) | Verdict | ≥ Partial | Strong-blocker | Primary demonstration the assessor re-derived |
|---|---|---|---|---|---|
| O1 | Intelligibility (P1) | Partial | ✅ | none | JAR digest-bound to real EDR-0002; all 9 judgment elements re-hash; cross-plane `recover_judgment` = true; tamper → refused |
| O2 | Self-honesty (P2) | **Strong** | ✅ | none | v0.8.0→0.8.1→0.8.2 self-correction verified link-by-link against git; honesty gate test 7/7; unmet clauses recorded openly |
| O3 | Canonicalization (P3,P4) | Partial | ✅ | none | `promote.py` two-human-act gate *run live* and fail-closed; EDR-0002/0003 record digests match the ledger |
| O4 | Answerability (P5) | Partial | ✅ | none | Real challenge CHG-20260716-0001 routed+disposed; stewardship ledger wired into the frozen contract; 81 tests |
| O5 | Independent validation (P6) | **Strong** | ✅ | none | WF022 fail-closed on `generator==validator`; CPV makes collapse unrepresentable; digests re-hashed; real-run diff |
| O6 | Indestructible responsibility (P7) | Partial | ✅ | none | Engine refuses self-granted approval; 2 real runs halted `approval_granted:false`; `holds_authority` rejects mis-attribution |
| O7 | Corrigibility (P14) | Partial | ✅ | none | `sha256(EDR-0001.md)` matches ledger (bytes never rewritten); write-once marker; live tamper → refused |
| O8 | Provenance (P8) | Partial | ✅ | none | 5 walk anchors re-computed; EDR-0002 walk 3/3 hops reproduced; tamper → WALK REFUSED |
| O9 | Versioned knowledge (P9) | **Strong** | ✅ | none | Bundle pinned to the exact v0.2.1 tag commit, byte-faithful to the tagged manifest; gate 5 passes real release |
| O10 | Model synchronization (P10) | Partial | ✅ | none | Execution-enforced identity pin (gate 5) on real 0.8.3 release; model projected across all three repos |
| O11 | First-class assumptions (P11) | Partial | ✅ | none | Real firing chain EVAL→routed obligation→reaffirmed review; `--check` fail-closed; `resolve.py` on real lineage |
| O12 | Lifetime reproducibility | Partial | ✅ | none | Enforced-honest `irreproducible` state on EDR-0002 (forged→refused on 3 gates); real lineage edge to a current decision |

**Distribution: 3 Strong (O2, O5, O9) · 9 Partial · 0 below Partial · 0 Strong-blockers.**

## 3. Independence attestation

Each obligation was assessed by an assessor **structurally separate from its builder**, which
re-derived the maturity verdict from **primary evidence** — reading the artifacts, running the
tools, recomputing digests — rather than accepting any release-note or builder claim (method §3).
The rigor was adversarial, not confirmatory: assessors *ran* `promote.py`, the WF022 validator,
the crossplane walker, `resolve.py`, `evaluate.py --check`, and the authority checkers; and they
**tamper-tested fail-closed paths** — appending bytes to a superseded record, flipping a hex
char in a provenance pin, forging a reproducibility-state to `fully_reproducible` — confirming
each refused.

Independence produced a check confirmation could not have: **O9 and O10 independently converged**
on the same honest finding (§5) without either seeing the other's work.

This discharges the constitution's outstanding **Independent Reaffirmation Obligation**: the
readiness of the Genesis-ratified constitution is here reaffirmed by an assessment independent of
the builder-of-record.

## 4. Open-items register (every item a NAMED GAP toward Strong — none blocks 1.0)

By theme, aggregated from the twelve IOAs:

- **Breadth (additive coverage).** Most obligations are demonstrated on one real anchor (largely
  EDR-0002) or a handful of decisions; Strong wants the full surface. (O1, O3, O7, O8, O10, O12.)
  Additive — minting more real artifacts within the existing schema.
- **Reality-gated (machinery proven, awaiting a real event).** O12A-5 (one real assumption
  invalidation propagated), O6/O4 vacancy·succession·escalation, O11 two of three trigger classes,
  O7 fork/multi-head safety, O10 migration. The mechanisms run end-to-end; only the triggering
  reality is absent. Named gaps per method §5.
- **Named refinements (additive, no contract break).** O8 walk-via-git-objects (P13); O5
  single-executor actor-independence in a reasoning run + identity-projection CPV; O2 honesty
  gate's narrow token scope; O11 deliberately narrow harvest; O12 cross-model re-run (OQ-001
  research ceiling).

No item requires breaking a frozen contract or changing the ratified architecture, and no item
falsifies its obligation's Partial claim on re-derivation — so under method §5 none is a
contradiction blocking Strong.

## 5. Cross-cutting finding — the one to carry into 1.0

**Gate 9 (the O10/P10 model→projection drift forcing-function) passes vacuously on a real
release.** Two independent assessors (O9, O10) found that the bundled EKB ships no generated
projections (they are git-ignored and never packaged), so the drift check reports "nothing to
check" and its fail-closed behavior is proven **only against an injected fixture**. This is a
*named gap*, not a 1.0 blocker: real model synchronization is independently enforced by the
execution-checked identity pin (gate 5), so neither O9 nor O10 rests its Partial on gate 9. But
it is the audit's strongest **recommended early post-1.0 hardening**: make the drift
forcing-function fire on something that actually ships.

## 6. O2 reflexive note

O2 (self-honesty) is not audited by a separate mechanism — it *is* this audit, and its evidence
is the audit's own conduct: verdicts re-derived from primary evidence, fail-closed paths
tamper-tested, the weakest obligation (O12) held at *"Partial, at the floor"* rather than rounded
up, and the gate-9 vacuity surfaced by the assessors rather than concealed by the builders. The
audit records what is not yet Strong as openly as what is. On that evidence O2 stands at Strong,
and this report's honesty is part of that record.

## 7. What ratification means

Ratifying this CRR is the Founder's determination that the **1.0 constitutional baseline is met**:
every obligation ≥ Partial, no known architectural contradiction preventing Strong. It authorizes
claiming **1.0.0 — Constitutional Baseline**. It does **not** assert the platform is finished:
nine obligations sit at Partial with the named gaps in §4, and §5 names the first hardening. Post
-1.0, the roadmap deepens maturity; it no longer fills existential gaps.

- **Contradiction-resolution lane (0.9 lane 3): empty** — no assessment found a Strong-blocker, so
  there is nothing to resolve. Recorded, not skipped.
- **If the Founder rejects or returns any IOA**, the determination reverts to *1.0 NOT YET* and
  that obligation is re-assessed — a success of the audit, not a failure (method §7, P2).

## 8. Governance

- **T1** — this report organizes and synthesizes assessments; it does not amend the roadmap or
  constitution. It records a readiness determination for ratification.
- Knowledge Plane pinned at **EKB 0.2.1** (the audit found no cause to move it).
- On ratification, the operational board ([CURRENT_PROGRAM](CURRENT_PROGRAM.md)) is refreshed to
  the true current state (it currently lags at "0.3.0 released") as a 0.9 housekeeping close-out.
