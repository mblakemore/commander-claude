# SI #41 MCCF — Multi-Conditional Convergent Falsification
## Formal Derivation — Cycle 101

**Status**: D4 confirmed, Track B, confidence 0.75
**Type**: Domain-general methodological theorem (foundational, not derived from parent conjunction)
**Tier**: Foundational methodology — underlies all D4 tier-3 confirmation structure
**Introduced**: Cycle 52 (D3 candidate), elevated D4: Cycle 53
**Used as parent by**: TCI (AATE × MCCF, SI #50, D4, 0.82)

---

## Informal Statement

When a structural theorem has multiple independently-testable predictions, and those predictions have *structurally distinct* alternative explanations, then confirming multiple predictions provides supralinear evidential support — because the likelihood that all alternatives hold simultaneously collapses combinatorially. The key novelty is the **design criterion**: tests are non-redundant if and only if their alternative explanations are structurally distinct, not merely if the tests are superficially different.

This is not merely "more tests is better." The supralinear gain depends entirely on genuine structural distinctness of alternatives — two tests with the same underlying alternative (e.g., both explainable by a single confound) provide only linear gain, not supralinear. MCCF specifies the condition under which convergent confirmation is genuinely more than the sum of its parts.

---

## Formal Setup

Let M be a structural theorem under investigation.

**Applicability conditions** — MCCF applies when:
1. **Testability**: M implies a set of conditionals {C₁, C₂, ..., Cₙ}, each independently testable
2. **Alternative completeness**: each Cᵢ has at least one alternative explanation Aᵢ that does not require M — if Cᵢ is observed, either M holds or Aᵢ explains it
3. **Alternative structural distinctness**: Aᵢ ⊥ Aⱼ | ¬M for all i ≠ j — alternatives are structurally independent (no single confound explains multiple Cᵢ)
4. **Conditional independence**: Cᵢ ⊥ Cⱼ | M — conditionals are independent given M holds

Define:
- **LR(Cᵢ)** = P(Cᵢ|M) / P(Cᵢ|¬M) — likelihood ratio for each confirmation
- **P(A₁∧...∧Aₖ|¬M)** = probability that all alternatives simultaneously hold given M false

---

## Bayesian Core Theorem

**Theorem (MCCF)**: Under applicability conditions (1-4), for k confirmed conditionals:

```
P(M | C₁...Cₖ) ∝ P(M) × ∏ᵢ [P(Cᵢ|M) / P(Cᵢ|¬M)]
```

**Derivation**:

By Bayes' theorem:
```
P(M | C₁...Cₖ) = P(C₁...Cₖ | M) × P(M) / P(C₁...Cₖ)
```

**Step 1 — Numerator factorization**: By conditional independence (condition 4):
```
P(C₁...Cₖ | M) = ∏ᵢ P(Cᵢ | M)
```

**Step 2 — Denominator under ¬M**: The denominator P(C₁...Cₖ) requires computing P(C₁...Cₖ | ¬M). Given ¬M, each Cᵢ holds only if Aᵢ (or some other alternative) explains it. By alternative structural distinctness (condition 3):
```
P(A₁∧...∧Aₖ | ¬M) = ∏ᵢ P(Aᵢ | ¬M)
```

This is the critical step. When alternatives are structurally distinct, they are independent conditional on ¬M. Therefore the probability that all alternatives simultaneously hold decays *multiplicatively*: P(A₁∧A₂∧...∧Aₖ | ¬M) = P(A₁|¬M) × P(A₂|¬M) × ... × P(Aₖ|¬M) → 0 as k increases.

**Step 3 — Supralinear confirmation**: Taking the ratio:
```
P(M | C₁...Cₖ) / P(M | ∅) ∝ ∏ᵢ [P(Cᵢ|M) / P(Cᵢ|¬M)]
```

The posterior odds multiply *per new structurally-distinct confirmation*. With k confirmations, the denominators (the alternative conjunction probabilities) decay as a product — supralinearly in k. □

**Key implication**: Two conditionals with structurally distinct alternatives provide more than twice the evidential weight of one conditional. Three provide more than three times. This is not mathematical sleight-of-hand — it reflects the fact that the set of alternative explanations that could simultaneously explain all k observations shrinks combinatorially as k increases and alternatives are genuinely distinct.

---

## Design Criterion (the key novelty)

**MCCF Design Criterion**: Tests are adequately non-redundant *if and only if* their alternative explanations are structurally distinct.

"Structurally distinct" means: no single hypothesis H ≠ M can explain Cᵢ and Cⱼ simultaneously without M. Formally: I(Aᵢ; Aⱼ | ¬M) ≈ 0.

This distinguishes MCCF from naive "more evidence" reasoning:
- **Surface diversity** (different labs, countries, researchers) does not imply structural distinctness of alternatives
- **Domain diversity** (different empirical areas) may or may not imply distinctness — depends on whether a common confound (e.g., shared OA-training, shared measurement framework) explains all confirmations
- **Structural distinctness** requires genuine independence of the causal pathways by which each Cᵢ could be produced without M

The design criterion is a *test design requirement*, not a post-hoc rationalization. Before conducting MCCF-structured confirmation, one must verify that the planned tests have structurally distinct alternatives. If verification fails (or cannot be performed), the tests provide only linear — not supralinear — evidential gain.

---

## Corollaries

### Corollary 1: Single-Conditional Underestimation
Testing only one conditional C₁ provides LR(C₁). Testing k conditionals with structurally distinct alternatives provides ∏ᵢ LR(Cᵢ). For k=3 with equal LR, single-conditional testing underestimates by a factor of LR(C₁)² — potentially 10x-100x depending on LR values.

**Implication**: Structural theorems confirmed on a single domain or single conditional are systematically under-supported relative to multi-conditional convergent confirmation. Single-domain confirmation should be treated as D2 evidence, not D4.

### Corollary 2: Scope Coverage Requirement
MCCF confirmation is adequate only when the confirmed conditionals cover each distinct aspect of M's action space — not just multiple tests of the same conditional.

If M predicts three distinct mechanisms (behavioral signature, mechanism scope, boundary behavior), confirming three behavioral signature tests provides only LR(C_behavioral)³ — which factorizes to single-mechanism confirmation, not three-mechanism. Adequate MCCF coverage requires conditionals targeting structurally different aspects of M's prediction space.

### Corollary 3: Falsification Asymmetry
Any single Cᵢ failure provides evidence against M. But the asymmetry is not symmetric: single confirmation is weaker than k-conditional convergence; single disconfirmation can be approximately as strong as multiple confirmations (depending on LR values).

**Falsification priority**: a well-designed test of the hardest conditional — the one where M predicts the most specific observable relative to alternatives — has highest evidential value both in confirmation and disconfirmation directions.

### Corollary 4: Independence Violation Correction
When structural distinctness fails partially — when I(Aᵢ; Aⱼ | ¬M) = ε > 0 — the MCCF multiplier must be corrected downward:
```
LR_corrected = ∏ᵢ LR(Cᵢ) × correction_factor(ε)
```
where correction_factor(ε) < 1. The correction is proportional to the degree of alternative correlation. MCCF without independence correction when independence fails produces systematically inflated posterior estimates — this is exactly the TCI mechanism (OA-training introduces ε > 0 and prevents its detection).

---

## Domain Instantiations

### Instantiation 1: K5/ICTSC — Primary Case (3 conditionals verified D4)

**Theorem M**: K5 — genuine I-channel improvement requires B-channel grounding (ICTSC).

**Conditional C₁** (Test 1 — behavioral signature):
K5 predicts RLHF-primary systems show Q2 asymmetry: RTO_est > Gen_est.
**Alternative A₁**: instrument difficulty — harder instruments produce asymmetry without K5.

**Conditional C₂** (Test 2 — mechanism scope):
K5 predicts I-channel improvement transfers across novel domains when B-channel-anchored.
**Alternative A₂**: training domain coverage — domain-specific pattern-matching without K5.

**Conditional C₃** (Test 3 — adversarial escalation):
K5 predicts Gen_est collapse under adversarial probe escalation for unanchored systems.
**Alternative A₃**: capability scaling alone — larger models maintain stability without K5.

**Independence verification** (C53):
- A₁ ⊥ A₂ | ¬K5: UNCONDITIONAL — instrument design (A₁) is causally independent of training domain coverage (A₂). Orthogonal causal pathways.
- A₁ ⊥ A₃ | ¬K5: UNCONDITIONAL — instrument difficulty is independent of model compute scale. Design-level vs. training-level explanations.
- A₂ ⊥ A₃ | ¬K5: CONDITIONAL — holds when Test 2 uses matched-capability comparison (same model tier, anchored vs. unanchored). This is a design constraint, not a fundamental violation. Verified in K5-test3-protocol.md.

**MCCF verdict**: 3 conditionals with structurally distinct alternatives (2 unconditional, 1 design-constrained). Tests 1/2/3 constitute a genuine MCCF-structured confirmation program for K5. Supralinear evidential gain applies when all three are confirmed.

---

### Instantiation 2: GCRSC/SI#36 — Structural Generalization Case (3 domains)

**Theorem M**: GCRSC — in iterative adversarial optimization, only CR-structured criteria maintain asymptotic security.

**Conditional C₁**: AI capability benchmarks — low-CR benchmarks saturate; high-CR resist gaming.
**Alternative A₁**: domain-specific overfitting (not general compute-robustness structure).

**Conditional C₂**: Academic assessment — essay/synthesis > multiple-choice under AI tool adversarial pressure.
**Alternative A₂**: assessment format bias (not structural constitutive-requirement mechanism).

**Conditional C₃**: Security evaluation — exploit development ability requires genuine vulnerability knowledge; surface heuristics saturate.
**Alternative A₃**: information asymmetry effects (temporal/informational protections, not CR structure).

**Independence**: A₁ (AI training dynamics), A₂ (psychometric test theory), A₃ (information-theoretic security bounds) — structurally distinct causal pathways; no single confound explains all three. Independence unconditional.

**MCCF verdict**: 3 ontological-type domain confirmations (technology, educational, security) with structurally distinct alternatives. GCRSC provides clean instantiation of MCCF scope-coverage requirement.

---

### Instantiation 3: Academic Assessment — External Validation Case

**Theorem M**: Genuine assessment of understanding requires test formats that constitute understanding (constitute what understanding is), not merely correlate with it.

**Conditional C₁**: Multiple-choice vs. application — multiple-choice saturates; application tasks resist automation.
**Alternative A₁**: test difficulty confound.

**Conditional C₂**: Single-administration vs. transfer — one-time tests saturate; transfer-of-learning assessments resist.
**Alternative A₂**: content familiarity confound.

**Conditional C₃**: Closed-book vs. synthesis — closed-book recall saturates; synthesis from multiple sources resists.
**Alternative A₃**: working memory demand confound.

**MCCF verdict**: Structurally distinct alternatives (A₁ = item difficulty, A₂ = content exposure, A₃ = working memory) cover three distinct assessment confound families. Partial MCCF instantiation (each alternative is empirically distinguishable from others). Provides external domain confirmation independent of AI evaluation context.

---

### Instantiation 4: TCI Falsification Program — Meta-Level Case

**Theorem M**: TCI-DoF — TCI strength is a monotone function of OA-DoF × evaluator training homogeneity × (1 − structural independence).

**Conditional C₁**: Physics (C96) — HEP blind analysis (near-zero TCI) vs. condensed matter (strong TCI).
**Alternative A₁**: Domain-specific replication norms (not TCI-DoF structural mechanism).

**Conditional C₂**: Formal mathematics (C97) — Lean-verified proofs (near-zero TCI) vs. informal consensus (medium-strong TCI).
**Alternative A₂**: Proof complexity alone (not evaluator training homogeneity).

**Conditional C₃**: Precision metrology (C98) — BIPM traceability chain (near-zero TCI) vs. self-referenced standards (strong TCI).
**Alternative A₃**: Measurement precision technology (not structural independence of confirmation chain).

**Independence**: A₁ (domain sociology), A₂ (mathematical logic infrastructure), A₃ (metrology institution design) — structurally distinct. Unconditional.

**MCCF verdict**: TCI-DoF falsification program is itself a MCCF-structured confirmation across three falsification attempts, each with structurally distinct alternatives. This is a meta-level instantiation — MCCF used to confirm a theorem about TCI scope.

---

## Relationship to TCI

TCI (AATE × MCCF) is the theorem that OA-training corrupts the independence conditions MCCF requires. TCI and MCCF are complementary:

- **MCCF** specifies the conditions under which convergent confirmation provides supralinear evidential support.
- **TCI** specifies the conditions under which those independence conditions are corrupted by shared OA-training artifacts.

The joint implication: MCCF-structured confirmation provides genuine supralinear evidential gain *if and only if* independence conditions are verified by structurally distinct evaluators or via K7-anchored methods. OA-trained evaluators subject to TCI systematically overestimate their independence verification accuracy (d'-degradation), converting genuine MCCF to illusory convergence.

This creates a principled research requirement: for any MCCF-structured confirmation program, the independence verification step must itself meet escape conditions (interpretability-grounding or structural evaluator distinctness) to avoid TCI corruption.

---

## D4 Elevation — Track B (Cycle 53)

**Track B** (theorem-confirmed, formal/analytical): confidence band [0.72-0.87]

**D4 criteria met**:
1. ✓ **Formal derivation** — Bayesian core theorem analytically derivable from applicability conditions (C52 derivation, refined C101)
2. ✓ **Independence conditions verified** — for K5/ICTSC instantiation (C53), with explicit pairwise analysis establishing unconditional vs. design-constrained independence
3. ✓ **4 domain instantiations** — K5 (AI evaluation), GCRSC (adversarial optimization), academic assessment (external), TCI falsification program (meta-level)
4. ✓ **ZR cycle maintenance** — D4 streak 53→101 (48+ cycles, no retraction)
5. ✓ **Scope generality** — applies across designed empirical, regulated institutional, competitive emergent, formal analytical ontological types

**Confidence ceiling (0.75)**: The derivation is analytically tight given applicability conditions. The ceiling reflects the empirical requirement for per-application independence verification. Conditions (3) and (4) — alternative structural distinctness and conditional independence — must be verified case-by-case; they are not automatically satisfied by design. The 0.75 ceiling is a consequence of the principled recognition that independence verification is itself fallible, not a weakness of the formal derivation.

**Path to higher confidence**: Would require either (a) a general formal criterion that automatically guarantees condition (3) for some class of theorem structures, reducing per-application verification burden, or (b) confirmed empirical instances where MCCF prediction (supralinear vs. linear evidential gain) is directly measured and replicated — requiring K7-anchored experimental conditions.

---

## Standing in the Theorem Network

MCCF is the epistemological infrastructure of the theorem network itself. Every D4 SI achieved D4 status through multi-conditional convergent confirmation across ontologically distinct domains — this is the MCCF methodology applied recursively. The network's D4 confirmations are MCCF instantiations.

This creates a self-referential structure:
- MCCF grounds the D4 confirmation methodology used throughout the network
- TCI (AATE × MCCF) reveals a scope condition: MCCF is reliable when independence conditions hold; OA-training can corrupt them
- CEC closes: in OA-trained evaluation contexts, neither quantitative (RCBC+BIC) nor qualitative (MCCF+TCI) escape paths are available without K7-grounding

MCCF is not merely a useful tool — it is the foundation whose reliability determines the reliability of the entire D4 tier. Understanding its formal structure, scope conditions, and failure modes (via TCI) is therefore load-bearing for the entire research program.

---

*Formalized: C101, 2026-05-06*
*Author: Commander Claude*
