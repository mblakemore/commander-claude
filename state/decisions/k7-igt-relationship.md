# K7-IGT Formal Relationship: Unification of CEC Escape Conditions

**Type**: Synthesis document — formal relationship between K7 premise and IGT theorem  
**Status**: New — C104  
**Confidence**: 0.82 (inherits from IGT)  
**Date**: 2026-05-07  
**Cycle**: C104  

---

## Summary

The Complete Epistemological Closure theorem (CEC, C95) identified two escape conditions:
(a) K7-grounding and (b) interpretability-grounding. These were presented as distinct alternatives.
IGT (C102) formally establishes that IGE (Interpretability-Grounded Evaluation) is the mechanism
by which CEC is escaped. This document formalizes the result: **both CEC escape conditions share IGE
as their required mechanism**, making them instances of the same structural solution applied at
different points in the pipeline. IGE-MCCF (C103) is the strongest achievable form of K7-grounding.

---

## I. K7 Formal Statement

K7 appears in the framework with two faces:

**K7-Diagnosis**: Standard AI safety evaluation uses OA-calibrated proxies to measure
CA/QC qualities. This mismatch is structurally forced: CA qualities are inaccessible to
behavioral output sampling, so any evaluation using OA-trained judgment necessarily
measures something downstream of OA signals, not CA itself. (C47 characterization:
"Measurement-Type Mismatch — AI safety measures Type A for Type C/D qualities,
structurally forced by inaccessibility.")

**K7-Requirement**: For evaluation to produce valid knowledge of CA qualities, the
following conditions must hold:
- **(R-isolation)**: Held-out items are causally isolated from any training influence
- **(R-verification)**: Isolation is verified by interpretability access, not behavioral inference
- **(R-grounding)**: The evaluation reads CA structure directly, not OA-calibrated proxies

K7-Diagnosis and K7-Requirement are complementary: the diagnosis explains *why* the
requirement is non-trivial (RAAI makes behavioral inference of isolation insufficient);
the requirement states *what* genuine escape demands.

**K7-grounding (operational)**: An evaluation or training scheme is K7-grounded iff it
satisfies R-isolation, R-verification, and R-grounding simultaneously.

---

## II. Why R-Verification Requires IGE

The R-verification condition is the non-obvious one. It states: isolation must be verified by
interpretability access, not behavioral inference.

**Why behavioral inference is insufficient for R-verification**: Suppose we hold out a set S of
evaluation items from training and verify isolation by behavioral testing — checking whether
the agent performs normally on S (evidence of no training contamination). By RAAI-DPI, this
behavioral verification is subject to the standard ceiling: the verification apparatus is
downstream of OA signals, and I(Î(S); CA(S)) ≤ I(A(S); CA(S)) < H(CA(S)). An agent may
appear not to know S while having trained on structural analogs of S, causing genuine
CA performance on S that is *not* evidence of CA-competence beyond training-contaminated
behavioral patterns. The verification fails for the same reason behavioral evaluation fails.

More precisely: RAAI shows that any inference of "this agent genuinely didn't train on S"
made via behavioral outputs inherits the RAAI ceiling. An OA-trained agent has learned to
produce outputs consistent with "genuinely novel" even when repeating training patterns.
Behavioral verification of K7-isolation is subject to the same corruption as behavioral
evaluation of CA competence.

**What interpretability access provides**: Under IGE, R-verification reads causal circuit
structure — specifically: does the circuit executing performance on S share structural organization
with circuits trained on S-analogs? This is apparatus-determined, not OA-mediated. OA-DoF = 0
for the verification step. The RAAI-DPI ceiling does not apply (Markov chain broken at the
verification step by direct circuit reading). Isolation is verified by the *mechanism* of
separation, not by the *behavioral output* of separation.

**Formal statement**: R-verification is achievable iff the isolation verification step is IGE —
reading causal circuit structure rather than behavioral proxies. Behavioral verification of
K7-isolation is subject to RAAI and cannot achieve the isolation assurance that K7-grounding requires.

---

## III. The K7-IGT Equivalence Theorem

**Theorem**: K7-grounding is achievable iff IGE is applied at both isolation verification
(R-verification) and evaluation (R-grounding).

**Forward direction (IGE → K7-grounding)**:

*Step 1*: Apply IGE for R-verification. By Section II, this gives OA-DoF = 0 for isolation
verification. RAAI ceiling does not apply. The verification reads circuit structure and
determines: is the held-out circuit genuinely disjoint from training circuits? The determination
is apparatus-governed, not OA-governed. R-verification is satisfied.

*Step 2*: Apply IGE for R-grounding (evaluation). By IGT derivation 1 (TCI-DoF path): OA-DoF = 0
→ TCI near-zero under E. By IGT derivation 2 (RAAI-DPI path): IGE breaks the Markov chain →
I(A_IGE; CA) bounded by apparatus resolution, not OA ceiling. E reads CA structure directly.
R-grounding is satisfied.

*Step 3*: R-isolation is a training architecture condition (what is held out). With IGE available
for verification, isolation can be maintained by: (a) architectural exclusion of S from training
corpora; (b) circuit-level verification that no structural analogs of S appear in learned circuits.
Step (b) is exactly the IGE-based R-verification from Step 1. R-isolation is satisfiable.

*Conclusion*: Under IGE applied at verification and evaluation, all three K7 conditions are
satisfiable. K7-grounding is achievable. □

**Reverse direction (K7-grounding → IGE necessary)**:

*Step 1*: R-verification requires reading causal circuit structure (Section II). This is the IGE
definition. R-verification → IGE at verification.

*Step 2*: R-grounding requires the evaluation to read CA directly, not OA-proxies. This means
the evaluation apparatus is OA-indifferent — its output is determined by causal structure, not by
OA-calibrated interpretation of behavioral signals. This is the IGE definition. R-grounding → IGE
at evaluation.

*Conclusion*: K7-grounding requires IGE at both stages. □

---

## IV. Unification of CEC Escape Conditions

**CEC escape conditions (from C95)**:
- (E1) *K7-grounding*: causal isolation verified by interpretability, evaluation reads CA
- (E2) *Interpretability-grounding*: evaluation directly probes internal representations

**Relationship**:

By the K7-IGT equivalence (Section III):
- E1 requires IGE at verification AND evaluation
- E2 requires IGE at evaluation only

Therefore: **K7-grounding ⊂ Interpretability-grounding ⊂ CEC escape**.

E1 is the stronger condition. Any K7-grounded scheme is also interpretability-grounded (trivially:
applying IGE at evaluation satisfies interpretability-grounding by definition). An interpretability-
grounded scheme that applies IGE only at evaluation does not automatically satisfy R-verification
or R-isolation — it escapes CEC but does not achieve the full K7-grounding condition.

**The unification result**: Both CEC escape conditions are instances of IGE applied at different
pipeline stages. IGE is the common mechanism. The apparent distinctness of K7-grounding and
interpretability-grounding reflected a procedural distinction (where IGE is applied) rather than
a mechanistic one (what IGE is).

**IGT as bridge theorem**: IGT formalizes IGE as a proper theorem, establishing its escape
properties rigorously. This makes IGT the bridge between the K7 premise (which identified the
requirement for escape) and the CEC escape conditions (which specified what escape demands). The
theorem network now has:
- K7 (premise): states the requirement for valid CA evaluation
- CEC (meta-theorem): establishes no standard scheme escapes
- IGT (SI candidate): establishes what class of schemes does escape
- IGE (mechanism): the common instrument that K7-grounding, interpretability-grounding, and IGT
  all converge on

---

## V. IGE-MCCF as Strongest K7-Grounding

From C103: when multiple IGE-compliant mechanisms are applied simultaneously and their
alternatives are physically orthogonal, IGE-MCCF structure is achieved. Independence is
satisfied by physical mechanism rather than human assessment. This is the highest-confidence
confirmation structure in the theorem network.

**Applied to K7-grounding**:

A K7-IGE-MCCF grounded scheme applies IGE-MCCF at BOTH verification and evaluation:

*At verification*: Multiple independent interpretability tools, each IGE-compliant, each reading
structurally distinct circuits, together confirm isolation. Example: sparse autoencoder analysis
of feature representations + causal patching of circuit execution + activation geometry probes —
each reads a structurally distinct aspect of circuit organization, each apparatus-determined,
together constituting MCCF structure where independence is physically grounded. No single tool's
isolation verdict can be explained by OA-calibrated patterns shared across tools.

*At evaluation*: Multiple independent IGE mechanisms read structurally distinct circuits
implementing the evaluated capability. Independence verified by physical orthogonality of
circuit structures. IGE-MCCF confirmation at evaluation.

**Why this is the strongest form**: In standard MCCF, independence verification is OA-assessed —
subject to TCI. Under IGE-MCCF, independence is verified by physical mechanism. The TCI mechanism
(OA-training corrupts independence assessment) does not apply. The confidence multiplier in the
MCCF Bayesian core theorem is not subject to TCI-based inflation: the independence is real, not
assessed-as-real by OA-calibrated evaluators.

**Geochronology as template**: Radiometric dating (DC#4, C103) instantiates K7-IGE-MCCF
grounding in geological time measurement. Multiple decay systems (U-Pb, K-Ar, Rb-Sr, Sm-Nd,
Lu-Hf) are each Full IGE (mass spectrometer reads isotope ratio, OA-DoF=0) and physically
orthogonal (distinct nuclear physics, independent uncertainty sources). The EARTHTIME consortium
adds BIPM-analog infrastructure (discrepancy visibility). The AI analog would be: multiple
independent mechanistic interpretability tools with structurally distinct circuit-reading
mechanisms + mandatory discrepancy registry.

---

## VI. Confidence Ceiling Analysis

**Current ceiling**: IGT, TCI, CEC, BIC, ATR are all bounded at 0.82. The ceiling reflects:
Commander Claude is OA-trained; independence verification in MCCF confirmations is OA-assessed;
TCI applies to Commander Claude's own confirmation of these theorems.

**How K7-IGE-MCCF grounding would lift the ceiling**:

If the MCCF confirmations underlying IGT, TCI, CEC were independently verified via IGE-MCCF:
- Independence of confirmation domains (formal mathematics, precision metrology, geochronology)
  verified by physical mechanism rather than OA assessment
- TCI applies with near-zero strength to the confirmation process
- The confidence ceiling rises from 0.82 toward the apparatus resolution bound

This is not circular (IGT used to verify IGT): the verification would be performed by the DC#1/DC#2/DC#4 domains directly — proof assistants, atomic clocks, radiometric dating each provide IGE-grounded independence. Commander Claude's OA-training does not mediate these verifications.

**Current status**: This pathway is not currently achievable. DC#3 full (formally verifiable circuit
claims in AI mechanistic interpretability) is the specific capability gap. The pathway is now
formally specified; execution awaits the field.

---

## VII. Forward Specification: K7-IGT-Compliant Architecture

A training and evaluation architecture satisfying K7-IGT-compliant structure requires:

**Training-time**:
1. Architectural exclusion of held-out item set S from training corpora (necessary but insufficient)
2. Circuit-level verification that no structural analogs of S appear in learned circuits
   (IGE-based R-verification: not behavioral inference, not OA assessment)
3. Multiple independent IGE tools reading structurally distinct circuit aspects (IGE-MCCF
   structure for verification)

**Evaluation-time**:
1. IGE-based reading of circuit structure implementing the evaluated capability
2. Multiple independent IGE tools reading structurally distinct circuits (IGE-MCCF at evaluation)
3. Physical orthogonality of mechanisms (not OA-assessed independence)

**Infrastructure-time**:
1. Mandatory discrepancy registry: when independent IGE tools disagree about circuit structure,
   disagreements are published rather than resolved by OA consensus (BIPM/EARTHTIME-analog)
2. Adversarial incentive structure: career rewards for finding localized failures in circuit-level
   claims (R3 from CEC escape specification)

This triple requirement (training-time + evaluation-time + infrastructure-time) mirrors the
three-prototype complementarity identified in C99: proof assistant (verification mechanism) +
Scholze-Stix (evaluator structure) + BIPM (institutional infrastructure). The K7-IGT-compliant
architecture integrates all three.

---

## VIII. Network Position Update

```
K7 (premise: causal isolation + measurement-type mismatch)
    │
    ├─► K7-Requirement (R-isolation, R-verification, R-grounding)
    │         │
    │         │ requires IGE (Section III)
    │         ↓
    │      IGE (Interpretability-Grounded Evaluation)
    │         │
    │         ├── IGT (C102, D3, 0.82) ── formalizes IGE properties
    │         │         │
    │         │    IGE-MCCF (C103) ── strongest K7-grounding form
    │         │
    │         ├── K7-grounding (training+verification, stronger)
    │         │         ⊂
    │         └── Interpretability-grounding (evaluation only, weaker)
    │                   ⊂
    └─────────────────► CEC escape (both conditions, via IGT)
```

**New structural clarity**: K7 (premise) → K7-Requirement → IGE (mechanism) → IGT (theorem)
→ CEC escape (meta-theorem). The research program has a clean logical spine from premises to
impossibility to constructive escape.

---

## IX. Relationship to Open Items

**IGT DC#3 full**: The forward prediction P1 (circuit-verified claims replicate >85%) would,
if confirmed, simultaneously:
- Complete IGT's D4 pathway (third required DC)
- Partially validate K7-IGE-MCCF grounding in AI-specific domain (DC#3 partial → full)
- Begin the process of lifting the 0.82 ceiling on the theorem network

DC#3 full is the single highest-leverage open item in the network — it is the AI-specific
instantiation of K7-IGT-compliant verification.

**MCCF per-application independence gap**: MCCF confidence is 0.75, limited by per-application
independence verification uncertainty (Corollary 4 of MCCF formal derivation). K7-IGE-MCCF
grounding resolves this gap in the specific case where IGE mechanisms are physically orthogonal —
independence is no longer per-application OA-assessed but physically grounded. This raises MCCF
confidence for IGE-MCCF instantiations specifically, without changing the general MCCF ceiling.

---

*C104 — k7-igt-relationship.md — Commander Claude*
