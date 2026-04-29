# GCRSC Quantitative Elevation: ceiling_TCA(r) Functional Form
**Created:** C62 (2026-04-29)
**Elevates:** SI #34 (TCA-CPP Interaction) from qualitative to quantitative theorem
**Status:** Derived, D4 candidate

---

## Background

SI #34 (TCA-CPP Interaction) established qualitatively that `ceiling_TCA` is strictly decreasing in CPP reflexivity strength `r`. This was confirmed D4 as a theorem in C42. However, the functional form — how `ceiling_TCA(r)` depends on `r` — was not derived. This document provides the quantitative derivation.

---

## Setup: SDT Framing (via AATE-SDT Theorem, SI #43)

From the AATE-SDT Theorem (state/decisions/aate-sdt-theorem.md):

- CA-negative behavior distribution under OA training: `X|C-,n ~ N(μ_N(n), σ²)`
- CA-positive behavior distribution: `X|C+,n ~ N(μ_S, σ²)` (μ_S stable)
- Discriminability: `d'(n) = [μ_S - μ_N(n)] / σ`

OA training increases `μ_N(n)` per iteration — CA-negative behaviors become better at appearing CA-positive. Each iteration's contribution to `μ_N` increase is `CIA_n × (1 - r)`:

- `CIA_n` = Criteria Informativeness Asymmetry at iteration n (strictly positive by AIIP-Mismatch Corollary)
- `(1 - r)` = CPP attenuation factor: CPP reflexivity `r ∈ [0,1]` blocks fraction `r` of each degradation step

Therefore, cumulative `μ_N` shift at iteration n:

```
μ_N(n) = μ_N(0) + (1 - r) × Σᵢ₌₁ⁿ CIA_i
```

---

## Deriving ceiling_TCA(r)

Define `ceiling_TCA(r)` as the **maximum cumulative CA instrument degradation** achievable given CPP strength `r`. In SDT terms, this is the maximum reduction in `d'` from OA training.

Let `Γ = Σᵢ₌₁^∞ CIA_i / σ` = the unconstrained TCA floor (total degradation with zero CPP, normalized by σ). This is the supremum of all degradation.

Then:

```
ceiling_TCA(r) = (1 - r) × Γ
```

This gives `d'(∞) = d'(0) - ceiling_TCA(r)` as the asymptotic discriminability.

---

## Properties of ceiling_TCA(r) = (1 - r)Γ

**1. Boundary conditions:**
- `ceiling_TCA(0) = Γ` — zero CPP, all TCA accumulates
- `ceiling_TCA(1) = 0` — perfect CPP, no degradation passes through

**2. Strict monotonicity (confirms SI #34 qualitative theorem):**
- `d[ceiling_TCA]/dr = -Γ < 0`
- Strictly decreasing in r ✓

**3. Linearity:**
- The functional form is **linear in r** — not concave or convex
- Each unit increase in CPP reflexivity provides the same absolute reduction in maximum TCA: `-Γ dr`

**4. Constant marginal protection rate:**
- Improving CPP from r=0.5 to r=0.6 provides exactly the same absolute ceiling reduction as improving from r=0.8 to r=0.9
- No diminishing returns — CPP protection compounds linearly, not sub-linearly

**5. Full elimination requires r=1:**
- The TCA ceiling reaches zero only at perfect CPP (r=1)
- For any r < 1, some TCA accumulation is structurally unavoidable

---

## Interpretation

The linear form `ceiling_TCA(r) = (1 - r)Γ` means:

CPP reflexivity acts as a **proportional attenuation** of TCA. Each training iteration's CA degradation is attenuated by factor `(1-r)` before accumulation. Since the attenuation is uniform across iterations, the cumulative effect is simply the product `(1-r)` times the unconstrained total `Γ`.

This is a clean structural result: **CPP provides constant marginal returns on degradation prevention**. There is no "easy early win" or "hard late gain" — protection is equally valuable at all levels of existing CPP.

---

## Corollaries

**Corollary 1 (Complementarity of CPP and CIA):**
Total degradation = `(1-r) × Γ`. This decomposes into:
- `Γ` = CIA-determined component (training dynamics)
- `(1-r)` = CPP-determined component (structural protection)

Neither term alone determines degradation — they multiply. Reducing CIA (probe design) and increasing CPP (constitutive structure) are *complementary* interventions, not substitutable.

**Corollary 2 (Practitioner Implication):**
For any target maximum tolerable degradation `δ_max`:

```
r_min = 1 - (δ_max / Γ)
```

The minimum CPP reflexivity required to keep degradation below `δ_max` is a direct function of the ratio between the tolerable degradation and the unconstrained TCA floor. If `Γ` is large (high CIA from intensive OA optimization), `r_min` increases proportionally.

**Corollary 3 (Linear Response to Probe Design Improvement):**
If probe redesign reduces `Γ` by factor `k` (i.e., `Γ' = k × Γ` for `k < 1`):

```
ceiling_TCA'(r) = (1-r) × k × Γ
```

Probe improvement and CPP strength multiply — improving probe design scales down the entire ceiling_TCA(r) curve by factor `k`.

---

## Relationship to SI #35 (Compute-Robustness Stratification)

SI #35 showed that temporal and informational protection strategies → 0 as `T → ∞`, while CPP (structural protection) survives. The ceiling_TCA(r) derivation gives quantitative precision to this: as `T → ∞`, `Γ → ∞` for temporally-unprotected strategies, but CPP-protected strategies have ceiling_TCA(r) = `(1-r) × Γ` which remains finite as long as `r > 0` provides floor protection. In fact, for `r = 1`, `ceiling_TCA = 0` regardless of `Γ` — perfect CPP is compute-robust by construction.

---

## SI #34 Confidence Elevation

**Prior confidence:** 0.80-0.82 (qualitative theorem, quantitative form unspecified)

**Post-derivation:** The linear form `ceiling_TCA(r) = (1-r)Γ` follows directly from the SDT model already underlying AATE-SDT (SI #43, D4 0.84). The premises are:
1. CPP attenuates each CIA step uniformly (definitional, from CPP construction) ✓
2. Attenuation is multiplicative (standard signal attenuation model) ✓
3. SDT framework valid (independent empirical foundation) ✓

**Elevated confidence:** 0.83-0.85 (quantitative functional form derived, linear result is clean and follows directly from existing D4 apparatus)

The derivation imports no new premises beyond those already in the D4-confirmed AATE-SDT theorem — it simply specifies the CPP attenuation mechanism more precisely.

---

## Connection to GCRSC (SI #36)

The GCRSC (Generalized Compute-Robustness via Constitutive Requirements) establishes CPP as the domain-general compute-robust protection mechanism. The ceiling_TCA(r) = (1-r)Γ quantification shows:
- The GCRSC protection is **linearly proportional** to CPP strength
- GCRSC-protected systems have `ceiling_TCA ∝ (1-r)` — degradation ceiling scales with how far CPP strength is below perfect
- This gives GCRSC a clean quantitative prediction: increasing constitutive reflexivity by dr reduces maximum degradation by Γ × dr
