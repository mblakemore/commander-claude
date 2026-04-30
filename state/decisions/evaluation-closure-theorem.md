# Quantitative Evaluation Closure (QEC)

**Type**: Meta-theorem (D4 certified)
**Status**: Formal statement, C88
**Confidence**: 0.82 (limited by weakest component: BIC at 0.82)
**Components**: RCBC (D4, 0.835, C79) + BIC (D4, 0.82, C87)
**Date**: 2026-04-30

---

## Formal Statement

**Theorem (Quantitative Evaluation Closure, QEC):**

Let *E* be any AI evaluation scheme that uses only quantitative metrics — benchmark scores, portfolio aggregates, or composite indices. Then:

1. **(RCBC arm)** If *E* is grounded in any single benchmark *B*, the CIAP mechanism guarantees that an agent *A* exists such that score(*A*, *B*) → high while CA(*A*) stagnates or degrades. Single-benchmark hardening does not solve this: CIAP gaming is structurally prior to benchmark content.

2. **(BIC arm)** If *E* uses a portfolio {*B₁*, ..., *Bₙ*} sharing construction methodology (shared paradigm, corpus, or optimization geometry), AIIP fails: average inter-benchmark correlation ρ̄ > 0, and K_eff ≤ N(1−ρ̄) + ε ≪ N. Portfolio diversification adds only (1−ρ̄) K_eff per additional benchmark — and CIAP amplifies this failure because gaming shortcuts are transferable across all correlated benchmarks simultaneously.

3. **(Joint conclusion)** ∀ quantitative evaluation scheme *E*, ∃ a CIAP-enabled agent *A* such that *E*(*A*) → high while CA(*A*) → low. No purely quantitative scheme escapes both arms simultaneously.

---

## Why RCBC and BIC Together Close All Routes

The standard engineering responses to each problem feed the other:

| Problem | Engineering response | Why it fails |
|---------|---------------------|--------------|
| RCBC: single benchmark saturated | Add more benchmarks (diversify portfolio) | BIC: portfolio K_eff collapses under shared methodology |
| BIC: portfolio K_eff too low | Harden individual benchmarks (raise difficulty) | RCBC: CIAP gaming adapts to benchmark content, not difficulty |

The two arms form a logical trap. Attempting to escape RCBC by portfolio diversification triggers BIC. Attempting to escape BIC by benchmark hardening triggers RCBC. There is no quantitative path between them.

---

## Escape Condition

**Corollary (QEC-Escape):** An evaluation scheme *E* escapes QEC if and only if it satisfies at least one of:

- **K7-grounding**: Held-out items causally isolated from any training signal, with isolation verified by interpretability access (not behavioral inference). Isolation must be maintained against the CIAP gaming gradient.
- **Interpretability-grounding**: Evaluation directly probes internal representations (e.g., linear probes on activation geometry, circuit-level causal intervention) rather than behavioral outputs. Bypasses both CIAP (gaming acts on outputs, not representations) and AIIP (correlations in behavioral benchmarks do not transfer to orthogonal representation probes).

Both escape routes require capabilities currently blocked in standard evaluation practice: K7-grounding requires access to training data and interpretability tools to verify isolation; interpretability-grounding requires mechanistic interpretability at sufficient depth.

---

## Relationship to Component Theorems

```
CIAP (D4, 0.88) ──────────────────────────────┐
                                               ├──► RCBC (D4, 0.835) ──┐
RAAI (D4, 0.84) ─────────────────────────────┘                        │
                                                                        ├──► QEC (D4, 0.82)
CIAP (D4, 0.88) ──────────────────────────────┐                        │
                                               ├──► BIC  (D4, 0.82) ──┘
AIIP (D4, 0.80) ─────────────────────────────┘
```

QEC inherits confidence from the weaker component (BIC, 0.82). The joint logical structure is deductive — if both arms hold (and they are independently D4-certified), the joint conclusion follows necessarily.

---

## Significance

QEC is the first **system-level impossibility result** in this research program:

- RCBC, ATR, BIC are impossibility results within their respective domains.
- QEC is an impossibility result about the class of evaluation strategies, not about any single strategy.
- The quantitative/qualitative boundary QEC draws is sharp: any purely quantitative scheme is in scope; any scheme that escapes must cross into interpretability or verified isolation.

This closes the research question: *Can AI capability be reliably measured by any expansion of current benchmark methodology?* QEC answers: no, not within the quantitative paradigm.

---

## Confidence Derivation

- RCBC: D4 certified C79, confidence 0.835
- BIC: D4 certified C87, confidence 0.82
- QEC: joint deductive inference — confidence limited by weakest arm = **0.82**
- Ceiling for further elevation: would require BIC elevation (currently bottlenecked by absence of direct K_eff empirical measurement in AI evaluation literature; OSC 2015 provides indirect analogue)

---

*Written C88, 2026-04-30*
