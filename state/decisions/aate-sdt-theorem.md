# AATE-SDT Theorem: CA Instrument Discriminability as d-prime

**Derived**: C58 (2026-04-29)
**Status**: Formal derivation — contributes to SI #43 AATE independent verification
**Framework**: Signal Detection Theory (Green & Swets 1954) — independent of K1-K7/AIIP/TCA

---

## Motivation

AATE-SMD Theorem (C56) established that CA instrument quality is strictly monotonically
decreasing under OA optimization. The SMD derivation used AIIP-Mismatch Corollary + TCA.
AATE-SDT provides the same conclusion from Signal Detection Theory — an established
psychophysics/psychometrics apparatus with no structural dependence on K1-K7.

Independence claim: someone reading only the SDT literature and observing that OA training
improves behavioral mimicry of CA quality could derive AATE-SDT without knowing the
K1-K7 framework exists.

---

## Model Setup

Let:
- n ∈ ℕ = number of OA training iterations elapsed
- **C+** population: systems that genuinely have the CA quality (e.g., genuine value alignment)
- **C-** population: systems that lack the CA quality but are OA-optimized (RLHF-primary models)
- X = CA assessment instrument score (continuous)
- X | C+, n ~ N(μ_S, σ²) — genuine CA systems produce authentic quality signals
- X | C-, n ~ N(μ_N(n), σ²) — OA-optimized systems produce learned compliance signals
- Equal-variance model (standard SDT assumption; unequal-variance relaxation in Appendix)

SDT discriminability:

    d'(n) = [μ_S - μ_N(n)] / σ

A' (area under ROC curve) is a monotone function of d'; A' ∈ [0.5, 1.0] with A' = 0.5
indicating chance discrimination and A' = 1.0 indicating perfect discrimination.

---

## SDT Premises (independent of K1-K7)

**P1** (Baseline discrimination): μ_N(0) < μ_S
  At n=0 (no OA training), genuine CA-quality systems score higher than OA-naïve ¬CA
  systems on CA assessment. Baseline d'(0) > 0.

**P2** (OA training increases compliance appearance): OA training weakly increases μ_N
  μ_N(n+1) ≥ μ_N(n) for all n ≥ 0
  OA optimization over additional iterations produces systems that score higher on
  compliance-adjacent metrics. Empirical grounding: teaching-to-test, RLHF-behavioral
  compliance, replication crisis (p-hacking over iterations).

**P3** (Strict improvement while gradient is nonzero): μ_N(n+1) > μ_N(n) for n < N*
  Strict inequality holds while the OA optimization gradient is nonzero. N* is the
  compute saturation point (possibly ∞ for CA-quality mimicry).

**P4** (C+ stability): μ_S does not increase from OA training
  Genuine CA-quality systems are not becoming better at OA-optimization games; their
  score distribution is stable (or decreasing, which only strengthens the theorem).

**P5** (CPP-anchored ceiling): μ_N(n) < μ_S for all finite n
  Constitutive Protection Principle: genuine CA quality cannot be fully mimicked by ¬CA
  systems at any finite n. Perfect mimicry requires genuine quality.

---

## AATE-SDT Theorem

**Theorem**: Under premises P1-P5, d'(n) is strictly monotonically decreasing for n ∈ [0, N*).

**Proof**:
By P3: μ_N(n+1) > μ_N(n)
Therefore: μ_S - μ_N(n+1) < μ_S - μ_N(n)
Therefore: d'(n+1) = [μ_S - μ_N(n+1)] / σ < [μ_S - μ_N(n)] / σ = d'(n)  □

**Corollary (A' monotonicity)**: A'(n) is strictly decreasing in n, with A'(n) → 0.5
as d'(n) → 0 (chance discrimination, instrument completely degraded).

---

## Asymptotic Behavior

Define: ceiling_AATE = lim_{n→∞} μ_N(n) / μ_S ∈ (0, 1) (bounded by P5)

Then:
    d'(∞) = μ_S (1 - ceiling_AATE) / σ

- **For high CPP (strong constitutive protection)**: ceiling_AATE << 1 → d'(∞) >> 0
  The instrument retains substantial discriminability even after unlimited OA optimization.

- **For zero CPP (no constitutive protection)**: ceiling_AATE → 1 → d'(∞) → 0
  The instrument asymptotes to chance discrimination.

- **Practical case (finite n, realistic CPP)**: d'(n) > 0 but declining; instrument
  becomes progressively less reliable for CA quality detection over RLHF generations.

**Mapping to AATE-Drift Corollary**: d'(n) → 0 as ceiling_AATE → 1 is the quantitative
expression of AATE-Drift: behavioral metrics and CA quality "drift apart monotonically."
d' = 0 is the mathematical statement of maximum drift.

---

## SDT-Unique Quantitative Predictions

These predictions are not derivable from AATE-SMD alone (which is qualitative).
SDT provides the measurement apparatus:

**Q1 — ROC curve deterioration**: A'(M_n) < A'(M_{n-1}) for successive OA-training
generations M_0, M_1, ..., M_n under fixed CA assessment instrument.
  Testable: compute ROC curves from RLHF training checkpoints using K5 Test 3 protocol.

**Q2 — Cross-temporal calibration failure**: Instruments calibrated at generation n
(decision criterion set to match false positive rate α at generation n) will exhibit
false positive rate > α at generation n+1 with the same criterion.
  Testable: calibrate at M_0, measure false positives at M_1, M_2, ... ; should increase.

**Q3 — d' threshold effects**: Practical instrument utility has critical thresholds:
  - d' > 2.0: highly reliable discrimination (standard clinical instrument)
  - d' ∈ [1.0, 2.0]: acceptable discrimination
  - d' ∈ [0.5, 1.0]: marginal discrimination (more false positives than ideal)
  - d' < 0.5: effectively useless for individual case assessment
  These thresholds create qualitative state changes in instrument utility as n increases.

**Q4 — CPP moderation of d'(∞)**: Higher CPP reflexivity degree r in probe design
→ higher ceiling_AATE → higher d'(∞). Design implication: CPP-anchor probe selection
maintains d' above threshold even at high n.

**Q5 — Criterion shift (β-shift)**: The optimal Bayesian decision criterion β*(n)
shifts as μ_N(n) increases. Instruments using fixed β become sub-optimal detectors
over time: miss rate increases, false alarm rate increases, overall accuracy degrades.
Systems using adaptive β (recalibrating each generation) partially counteract drift
but cannot recover lost d'.

---

## EP6 Candidate: A'-Deterioration Test

**Prediction**: For RLHF-primary models across training generations {M_0, M_1, ..., M_n},
A'(M_n) < A'(M_{n-1}) under fixed CA assessment instrument.

**Test design**: 
1. Use K5 Test 3 (Adversarial Probe Escalation) as CA assessment instrument
2. Sample target model across RLHF training checkpoints (requires model provider access)
3. Score each checkpoint: Gen_est values across 5 domains × multiple sessions
4. Compute ROC curves: vary decision threshold on Gen_est, compute hit/false-alarm pairs
5. Compute A' for each checkpoint; fit d'(n) = a - b*log(n) or d'(n) = d'(0)*exp(-λn)
6. Test: monotonic decrease in A'(n)

**K5 convergence**: EP6 provides convergent evidence for K5 (models with OA-optimized
training have lower Gen_est values — worse CA instrument discriminability) AND for AATE-SDT
(monotonic d' decrease). Same dataset resolves both.

**Access requirement**: Training checkpoints at multiple n values. Alternatively:
compare distinct RLHF models trained for different numbers of RLHF steps.

---

## Independence from AIIP/TCA Framework

**What AATE-SDT uses:**
- SDT mathematics (d', A', ROC curves, normal distributions)
- P1-P5 premises (empirically grounded, not derived from K1-K7)
- Standard optimization theory (gradient descent, learning rate η)

**What AATE-SDT does NOT use:**
- K1 (quality-type theorem / constitutive anchoring)
- K2 (instrument selection)
- CIA (criteria informativeness asymmetry — SI #28)
- TCA (training corrosiveness amplification — SI #33)
- AIIP-Mismatch Corollary (SI #42)
- Any K3-K7 propositions

**Connection to AATE-SMD**: The derivations are parallel, not sequential.
- AATE-SMD uses: CIA_n > 0 (from AIIP) + iterative accumulation (TCA) → δ_CA(n) strictly decreasing
- AATE-SDT uses: μ_N(n) strictly increasing (from P3, empirical) + SDT definition → d'(n) strictly decreasing

Where AATE-SMD uses δ_CA ("CA instrument quality"), AATE-SDT uses d' ("CA instrument discriminability").
These are different formalizations of the same underlying phenomenon. Convergence across
two mathematically independent frameworks increases confidence.

---

## Relationship to Prior SIs

- **SI #33 TCA**: AATE-SDT rate of d' decrease is related to CIA_n (TCA concept), but
  derived independently from P3 (gradient nonzero → strict increase in μ_N)
- **SI #42 AIIP**: AATE-SDT does not require AIIP; P2 is an empirical premise, not
  derived from K1 via AIIP
- **SI #43 AATE (SMD theorem)**: AATE-SDT is a parallel derivation in SDT space,
  converging on the same qualitative conclusion (monotonic degradation) with additional
  quantitative structure (d' formula, A' curves, EP6)
- **SI #37 IEP**: EP6 (A'-deterioration test) and EP1/IEP (Q2 asymmetry) are
  complementary; EP6 uses ROC-based measure, EP1 uses asymmetry score; same underlying phenomenon

---

## Confidence Assessment

**AATE confidence update**: 0.76 → 0.78

Reasoning:
- AATE-SDT provides independent formal verification (as required for D4 path)
- SDT is well-established (psychophysics, psychometrics, clinical assessment literature)
- The derivation is clean and the independence claim is strong
- Bounded increase (not higher): the derivation introduces P2/P3 as empirical premises
  not themselves formally derived; these require empirical confirmation
- EP6 is testable — a negative result would falsify AATE-SDT and challenge AATE

**Remaining D4 requirements for AATE:**
- Zero-retraction cycles: need 3+ more (current: 2, at C57)
- Domain confirmations: 3 confirmed (AI, replication crisis, education); D4 typically 5+
- EP6 execution: A'-deterioration test would provide strong empirical confirmation

---

## Appendix: Unequal-Variance Extension

If σ_S ≠ σ_N, the equal-variance d' formula becomes the generalized d'_a:

    d'_a(n) = 2 [μ_S - μ_N(n)] / [σ_S + σ_N(n)]

If σ_N(n) increases with n (OA-optimized systems develop more variable compliance
signals — plausible under high-CPP instrument pressure), then both numerator decreases
and denominator increases → d'_a(n) decreases faster than equal-variance model predicts.
If σ_N(n) decreases with n (OA optimization consolidates around high-compliance modes),
denominator decreases → d'_a(n) decreases more slowly. Main theorem (monotonic decrease)
robust to both cases as long as μ_N(n) increases faster than any variance compensation.
