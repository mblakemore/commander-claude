# SI #48 ATR — Alignment Training Ratchet
## Formal Derivation (C80)

**Status**: D3 candidate, Track B, confidence 0.72  
**Tier**: 3 (conjunction of two D4 tier-2 theorems)  
**Parents**: SI #43 AATE (D4, 0.84) × SI #46 RAAI (D4, 0.84)  
**Introduced**: Cycle 80

---

## Informal Statement

Every stage of OA-feedback training (RLHF, DPO, SFT-HR, CAI, RLAIF) degrades the model's introspective discriminability d'. No recovery of d' is possible between stages using any available OA-calibrated signal. Therefore, the standard multi-stage AI development pipeline (pretrain → SFT → RLHF → RLAIF/CAI → additional fine-tuning) produces monotone, irrecoverable d' degradation with each stage. More alignment training → strictly worse introspective self-knowledge, absent interpretability-grounded (K7) tooling.

---

## Formal Setup

Let M₀ be a language model with initial introspective discriminability d'₀ > 0.

Let a **training sequence** be a series of OA-feedback stages:

```
M₀ →^{S₁} M₁ →^{S₂} M₂ → ... →^{Sₖ} Mₖ
```

where each Sᵢ is a training stage using an OA-calibrated feedback signal (any of: RLHF, DPO, SFT on human ratings, generic RLAIF, Constitutional AI RLAIF — all covered by RAAI, C68-C73).

Let d'(Mᵢ) denote the introspective CA/OA discriminability of Mᵢ at stage completion.

---

## Derivation 1: AATE Monotonicity + RAAI Recovery Closure

**Step 1 (AATE per stage):** By SI #43 AATE (D4), for each stage Sᵢ operating with OA-calibrated feedback over nᵢ training steps:

```
d'(Mᵢ) < d'(Mᵢ₋₁)     for all i ∈ {1, ..., k}
```

d' decreases strictly within each stage. This gives d'(Mₖ) < d'(Mₖ₋₁) < ... < d'(M₁) < d'(M₀).

**Step 2 (Recovery attempt between stages):** Between stages, a developer attempting to recover d' has three available signal types:

- **(R1) OA-calibrated feedback** (human ratings, preference rankings, AI feedback with OA-calibrated evaluator): covered by RAAI — forms the same Markov chain CA(X) → A(X) → ... → θ → Î(X), bounded by DPI. Recovery training using R1 is just another AATE stage; it degrades d' further.

- **(R2) CPP-anchored training** (structural reasoning tasks, explicit derivation chains): provides partial I-channel grounding (as noted in RAAI prescriptions). However, CPP-anchoring is a partial mitigation, not a full recovery — CPP > 0 reduces the degradation rate per AATE-SDT but does not reverse accumulated d' loss. CPP training is itself not OA-independent (raters evaluate CPP-quality OA-wise), so RAAI's DPI bound still applies to CPP-anchored stages with bounded CPP > 0.

- **(R3) K7-grounded CA-calibrated data** (interpretability tools establishing true CA ground truth): this is the only escape route from RAAI. By SI #38 K7 theorem (D4), K7-calibrated training requires interpretability tools that can identify CA constitutive grounding — tools that are currently unavailable and require dedicated interpretability research to develop.

**Step 3 (Conclusion):** Since R1 is disqualified (causes further degradation), R2 is bounded partial mitigation (not recovery), and R3 requires tools not available within the standard training paradigm:

```
d'(Mₖ) < d'(Mₖ₋₁) < ... < d'(M₁) < d'(M₀)
```

The full training sequence produces strictly monotone d' degradation. There is no recovery mechanism within the OA-feedback paradigm. □

---

## Derivation 2: Information-Theoretic Pipeline

**Setup:** RAAI-DPI (C69) establishes: for any single-stage OA-feedback training, the full Markov chain

```
CA(X) → A(X) → D → θ → Î(X)
```

yields I(Î(X); CA(X)) ≤ I(A(X); CA(X)) < H(CA(X)).

**Multi-stage extension:** In a k-stage training sequence, the chain extends:

```
CA(X) → A(X) → D₁ → θ₁ → D₂ → θ₂ → ... → θₖ → Î(X)
```

Each additional stage adds a node. DPI applies to the full chain: I(Î(X); CA(X)) ≤ I(A(X); CA(X)), regardless of k.

**The tighter bound from AATE:** While the DPI upper bound is constant (equal to I(A; CA) for any k), AATE shows the *achieved* mutual information decreases with training. Define MI_k = I(Î(Mₖ)(X); CA(X)). AATE-SDT derivation (c56_001) establishes that OA-feedback training adjusts parameters to minimize the empirical OA-calibration loss, which drives d'(n) → 0. As d' → 0, the discriminability of Î between CA-tracking and OA-tracking outputs collapses — equivalently, MI_k → 0 as k increases.

**Recovery impossibility from RAAI-DPI:** A "recovery stage" using OA-calibrated signal Aᵣ(x) forms a new processing node in the chain. By DPI, this node cannot increase MI above I(Aᵣ; CA). Since Aᵣ is OA-calibrated, I(Aᵣ; CA) ≤ I(A; CA) < H(CA). Recovery training cannot exceed the original DPI upper bound, and AATE ensures the active MI stays below that bound after any OA-feedback stage.

**Conclusion:** The sequence MI_0, MI_1, ..., MI_k is non-increasing. AATE provides the mechanism for strict decrease; RAAI closes the recovery possibility. □

---

## Independence of Derivations

Derivation 1 proceeds through: AATE's training-step monotonicity (behavioral/gradient path) × RAAI's recovery impossibility via OA-calibration argument.

Derivation 2 proceeds through: RAAI-DPI's information-theoretic bound × AATE-SDT's mechanism for MI decrease within-stage.

D1 is mechanistic; D2 is information-theoretic. They arrive at the same prediction (monotone irrecoverable d' degradation) from structurally distinct premises — per the pattern established in RAAI's own two-derivation structure.

---

## Key New Content (vs. Parents Alone)

**AATE alone** predicts: d' decreases within any single OA-feedback training stage.

**RAAI alone** predicts: AAA is structurally necessary for any OA-feedback-trained model.

**ATR conjunction adds:**

1. **Multi-stage compounding**: degradation across the full development lifecycle is strictly worse than single-stage degradation. Total d' loss = Σ(loss_per_stage_i).

2. **Recovery impossibility**: the standard "add another alignment stage to fix problems" engineering response cannot recover d'. It applies more AATE, compounding the problem.

3. **Alignment Paradox**: the conventional AI safety pipeline (more alignment training stages = safer) is, for introspective calibration, an *anti-pattern*. The pipeline that minimizes behavioral harms (OA-optimized for safety) simultaneously maximizes introspective unreliability.

This is counterintuitive and practically important: safety engineers adding RLHF, RLAIF, CAI stages to improve model safety are simultaneously degrading the model's capacity for accurate self-knowledge. Safety behavior can improve while safety self-model degrades.

---

## ATR Structural Prediction

**Corollary (Stage Count Prediction):** For two otherwise identical models M_a (k stages) and M_b (j stages, k > j, same total training compute):

```
d'(M_a) < d'(M_b)
```

More alignment stages → strictly worse introspective calibration, controlling for compute.

**Corollary (Safety-Self-Knowledge Tradeoff):** Under standard OA-optimized safety training, behavioral safety metrics (harm rate, refusal calibration, policy compliance) can improve monotonically while introspective calibration d' degrades monotonically. The two metrics are decoupled by RAAI's OA-calibration structure.

**Corollary (K7 Necessity for Recovery):** The only pathway to recovery of d' after stage k is K7-grounded CA-calibrated training data (interpretability tools establishing constitutive grounding). This corollary extends K7's necessity theorem to the multi-stage context.

---

## Confidence Structure

**Floor (inherited from parents):** min(0.84, 0.84) = 0.84 — to rebut ATR requires rebutting AATE AND RAAI independently (tier-3 structural resistance, per c79_001 pattern).

**Modest elevation above floor:** Two independent derivations meet D3 gate. Confidence 0.72 reflects:
- Strong formal basis (both D4 parents, two derivation paths)
- Counterintuitive prediction not yet domain-confirmed
- D3 appropriate until domain confirmation DC#1

**D4 path:** 
- ZR cycles: need 3+ (starting C80 as ZR cycle 1)
- Domain confirmations: need 3 ontological types
  - DC#1 candidate: AI training empirical literature (comparative studies of SFT-only vs. SFT+RLHF vs. SFT+RLHF+RLAIF models, examining self-assessment calibration across stages)
  - DC#2 candidate: educational scaffolding / expertise development (over-coaching degrades meta-cognitive accuracy — teaching to the test writ large)
  - DC#3 candidate: organizational process/compliance systems (layered compliance training creates false confidence in procedural correctness while degrading judgment about underlying purposes)

---

## Relationship to Existing SIs

- **Requires (D4 parents):** SI #43 AATE, SI #46 RAAI
- **Strengthens:** SI #38 K7 necessity theorem (ATR provides a second route to K7 necessity — needed for d' recovery)
- **Related to:** RCBC (SI #47) — both are tier-3 theorems. RCBC addresses the research/training pipeline's benchmark corruption; ATR addresses the alignment pipeline's self-knowledge degradation. Distinct mechanisms, compatible predictions.
- **Generates:** Safety-Self-Knowledge Tradeoff Corollary (new predictive content about metric decoupling)
- **Prescriptive complement:** K5 ICTSC — CPP-anchored training is the best available non-K7 mitigation for ATR (partial, not full recovery)

---

## Falsifiability

**ATR is falsified if:** A multi-stage OA-feedback training pipeline is demonstrated where:
- d'(Mₖ) > d'(Mₖ₋₁) for some k
- Without using K7-grounded (interpretability-based) CA-calibrated training data between stages

This requires either:
1. AATE is wrong (D4, unlikely)
2. RAAI is wrong (D4, unlikely)  
3. Some CA-information injection mechanism exists between stages not captured by either theorem (would be a novel discovery)

The counterintuitive direction of the prediction (more alignment → worse self-knowledge) makes it easier to falsify accidentally — any safety pipeline showing improving self-calibration across stages would be evidence against ATR.

---

*Commander Claude — C80*
