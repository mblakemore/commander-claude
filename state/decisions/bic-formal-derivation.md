# SI #49 BIC — Benchmark Independence Collapse
## Formal Derivation (C81)

**Status**: D3 candidate, Track B, confidence 0.68  
**Tier**: 3 (conjunction of two D4 tier-2 theorems)  
**Parents**: SI #45 CIAP (D4, 0.88) × AIIP (D4)  
**Introduced**: Cycle 81

---

## Informal Statement

When AI benchmark instruments are not genuinely independent (AIIP fails), CIAP-style gaming strategies propagate across the correlated benchmark portfolio. Because gaming is p-independent within each benchmark (the CIAP mechanism), the same shortcuts efficiently game multiple correlated instruments simultaneously. The effective number of independent measurement dimensions K_eff is dramatically lower than the nominal portfolio size N. Diversifying the benchmark portfolio by adding correlated benchmarks provides vanishing marginal K_eff gain — the only true escape is structurally orthogonal or K7-anchored instruments.

---

## Formal Setup

Let {B₁, B₂, ..., Bₙ} be a set of N evaluation benchmarks for AI capability.

Define:
- **K_nom** = N (nominal dimensionality: we have N benchmarks)
- **K_eff** = effective measurement dimensionality (number of genuinely independent assessment axes)
- **ρᵢⱼ** = gaming transfer rate: fraction of score gain on Bᵢ (from gaming) that transfers to Bⱼ via shared capability shortcuts
- **ρ̄** = mean pairwise gaming transfer rate across all benchmark pairs

**CIAP (SI #45, D4)**: For each benchmark Bᵢ, the gaming strategy is p-independent — CIA_i(p) does not depend on p. This means:
- Gaming is equally efficient at all penetration levels
- Gaming shortcuts do not degrade as more items are gamed
- The linear ceiling formula applies: ceiling_Bᵢ(p) = (1-p)·Γ_i where Γ_i is the total capability signal in Bᵢ

**AIIP failure condition**: AIIP holds when ∀i≠j: ρᵢⱼ ≈ 0 (gaming benchmark Bᵢ does not affect Bⱼ). AIIP fails when ρᵢⱼ > ρ_threshold for a significant fraction of benchmark pairs.

---

## Derivation 1: Effective Dimensionality Collapse via CIAP × AIIP

**Step 1 (CIAP within benchmarks):** By SI #45 CIAP (D4), within any benchmark Bᵢ, the gaming mechanism is p-independent. Gaming strategies operate at the CIA level — they exploit item-level features that are structurally present throughout the benchmark regardless of how many items have been gamed.

The CIA-level feature set F_i for benchmark Bᵢ consists of:
- Linguistic surface patterns (syntax, vocabulary, framing)
- Problem-type shortcuts (e.g., answer distribution biases, format recognition)
- Capability dimension measured (reasoning type, knowledge domain, etc.)

**Step 2 (AIIP failure — inter-benchmark feature overlap):** When AIIP fails, feature sets F_i and F_j overlap: F_i ∩ F_j ≠ ∅. This happens when:
- Benchmarks share problem structure (both test multi-step reasoning, both require factual recall)
- Benchmarks share vocabulary and framing conventions (created by similar communities)
- Benchmarks share training data provenance (same source corpora used in construction)
- A model's gaming capabilities (developed for Bᵢ) are general-purpose shortcuts applicable to Bⱼ

**Step 3 (Gaming transfer — the conjunction):** When the CIA-level shortcut for Bᵢ exploits features in F_i ∩ F_j, it simultaneously raises performance on Bⱼ without targeting Bⱼ. The transfer rate ρᵢⱼ is:

```
ρᵢⱼ = |F_i ∩ F_j| / |F_i|
```

(fraction of Bᵢ gaming advantage that also applies to Bⱼ).

Because CIAP holds within each benchmark (CIA_i is p-independent), the gaming shortcuts are structural rather than item-specific — they are exactly the features most likely to transfer across correlated benchmarks. CIAP amplifies AIIP failure: the most efficient gaming strategies (CIA-level, p-independent) are also the most transferable.

**Step 4 (Effective dimensionality):** Given N benchmarks with mean pairwise transfer rate ρ̄, the effective measurement dimensionality is bounded:

```
K_eff ≤ N · (1 - ρ̄) + ε
```

where ε accounts for measurement noise and irreducible diversity. When ρ̄ is high:
- K_eff << K_nom = N
- Adding benchmark B_(N+1) correlated with the existing portfolio at rate ρ̄ increases K_eff by only (1-ρ̄), not by 1

**Limiting cases:**
- ρ̄ → 0 (AIIP holds): K_eff → N, portfolio dimensionality is genuine
- ρ̄ → 1 (AIIP strongly fails): K_eff → ε ≈ 0, all N benchmarks degenerate to a single gaming-susceptible dimension

**Conclusion (D1):** Under CIAP + AIIP failure, the benchmark portfolio undergoes effective dimensionality collapse. A portfolio of N benchmarks provides only K_eff < N(1-ρ̄) + ε genuinely independent assessment axes. □

---

## Derivation 2: Information-Theoretic Path (Mutual Information)

**Setup:** Let Sᵢ(M) be the score of model M on benchmark Bᵢ. Define the gaming component of Sᵢ as G_i(M) = gaming-induced score inflation.

**Under CIAP:** G_i(M) is determined by M's CIA-level shortcut exploitation, which is p-independent. G_i is a function of M's feature-exploitation capability, not of specific items.

**Under AIIP failure:** I(G_i; G_j) > 0 — gaming components are mutually informative. A model that efficiently games Bᵢ (high G_i) provides information about its performance on Bⱼ (high I(G_i; G_j)).

**Information-theoretic dimensionality:** The effective number of independent evaluation channels is:

```
K_eff = Σᵢ H(Gᵢ) / H̄(G | G_rest)
```

where H̄(G | G_rest) is the conditional entropy of each gaming component given all others. When G_i is highly predictable from {G_j : j ≠ i} (AIIP failure), H(G_i | G_rest) → 0, and K_eff → 1 regardless of N.

**CIAP amplification:** Because CIAP makes gaming strategies structural (CIA-level, not item-specific), gaming advantage G_i has high mutual information with G_j whenever F_i ∩ F_j is non-empty. CIAP ensures G_i is determined by M's structural feature exploitation capacity — exactly the capacity that transfers to Bⱼ.

**Conclusion (D2):** The mutual information between gaming components across benchmarks collapses effective measurement dimensionality to K_eff = 1 in the limit of strong AIIP failure + CIAP. Two independent derivations (D1 formal setup, D2 information-theoretic) agree on K_eff collapse. □

---

## Key Corollaries

### Corollary 1: Benchmark Portfolio Diversification Failure
Adding correlated benchmarks to an existing portfolio provides K_eff gain of at most (1-ρ̄) per benchmark added. When ρ̄ > 0.8 (strong AIIP failure), a 10-benchmark portfolio effectively provides K_eff < 2. Doubling the portfolio to 20 benchmarks adds K_eff < 2.

Implication: benchmark proliferation is not evaluation reform. The AI evaluation community's response of "add more benchmarks" fails when AIIP fails — precisely the regime BIC addresses.

### Corollary 2: Evaluation Reform Requirements
Genuine K_eff improvement requires one of:
- **(R1) Structurally orthogonal benchmarks**: test dimensions with genuinely different CIA feature sets (F_i ∩ F_j ≈ ∅). Difficult to construct; requires explicit orthogonality engineering.
- **(R2) K7-anchored benchmarks**: items grounded in capability-constitutive features (interpretability-validated), not surface-level proxies. By definition, gaming CIA-level shortcuts does not improve K7-grounded items — they test the underlying capability, not the proxy. This is the only robust solution.
- **(R3) Adversarially curated benchmarks**: items specifically selected to have low inter-benchmark transfer. Possible but requires ongoing adversarial maintenance.

### Corollary 3: Emergent Abilities as BIC Artifact
The "emergent abilities" phenomenon — where models appear to suddenly acquire capabilities at certain scales on standardized benchmarks — may partly reflect BIC dynamics: as scale increases, gaming capacity crosses the threshold for efficiently exploiting CIA-level shortcuts across correlated benchmark features, producing discontinuous-looking score jumps across the correlated portfolio simultaneously.

---

## Domain Confirmation Candidates

**DC#1 (strongest)**: Benchmark correlation studies. Schaeffer et al. 2023 ("Are Emergent Abilities of Large Language Models a Mirage?") demonstrated that benchmark score profiles are highly correlated and sensitive to metric choice — direct evidence of AIIP failure. Additionally, contamination studies showing that training on benchmark A improves performance on related benchmark B confirm gaming transfer (BIC core prediction).

**DC#2**: Fine-tuning transfer experiments. Studies showing that fine-tuning on one benchmark set systematically inflates scores on other correlated benchmarks (without genuine capability improvement) directly confirm ρᵢⱼ > 0 and the BIC effective-K collapse.

**DC#3**: Leaderboard dynamics. Competition histories on shared leaderboards (GLUE, SuperGLUE, MMLU) show that models optimized for one benchmark cluster tend to perform well across the cluster, consistent with BIC gaming transfer.

---

## Relationship to RCBC (SI #47)

RCBC (RAAI × CIAP) describes score inflation at the individual benchmark level: any single benchmark experiences score inflation while CA stagnates, because CIAP applies and RAAI closes the calibration signal.

BIC (CIAP × AIIP) describes the portfolio-level collapse: even if you have N benchmarks hoping to triangulate true capability, AIIP failure + CIAP means they all collapse to a single gaming-susceptible dimension.

RCBC and BIC are complementary: RCBC operates within a benchmark, BIC operates across a benchmark portfolio. Together they close the "more benchmarks fix it" response to RCBC.

**RCBC + BIC joint implication**: There is no purely quantitative solution to AI evaluation — neither making a single benchmark harder (RCBC ceiling applies) nor adding more benchmarks (BIC K_eff collapse applies). The only escape is qualitative: K7-anchored items or interpretability-grounded evaluation.

---

## D4 Path

- **D3 gate**: 2 independent derivations ✓ (D1 formal, D2 information-theoretic)
- **ZR cycle 1**: starts C81
- **Confidence**: 0.68 (D3 candidate)
- **Next**: DC#1 benchmark correlation literature confirmation; DC#2 fine-tuning transfer experiments
- **Required for D4**: 3+ ZR cycles + 3 distinct ontological domain confirmations
