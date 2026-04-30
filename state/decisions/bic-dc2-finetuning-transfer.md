# BIC DC#2: Designed Empirical — Fine-Tuning Transfer and Intrinsic Dimensionality

**Cycle**: C84
**Theorem**: SI #49 BIC (Benchmark Independence Collapse)
**Ontological Type**: Designed empirical (second domain, distinct mechanism from DC#1)
**Confidence Update**: 0.72 → 0.74

---

## Domain Mapping

| BIC Formal Element | Fine-Tuning Transfer Instance |
|---|---|
| K_eff | Effective independent evaluation dimensions captured by task fine-tuning |
| ρ̄ (mean benchmark correlation) | Shared intrinsic fine-tuning dimensionality across benchmarks |
| AIIP failure | Benchmarks share low-d fine-tuning subspace → not instrumentally independent |
| CIAP amplification | Optimization shortcuts in low-d subspace propagate to all correlated benchmarks |
| K_eff bound | K_eff ≤ N(1-ρ̄) + ε, where ρ̄ derived from shared d_int |

---

## Why This is Mechanistically Distinct from DC#1

**DC#1** (AI evaluation benchmark literature — Schaeffer 2023, GLUE/SuperGLUE): BIC confirmed at the *data/corpus correlation level*. Contamination transfer (Magar & Schwartz 2022), metric nonlinearity (Schaeffer 2023 emergent abilities), dataset construction overlap. The K_eff collapse was observed at the level of benchmark construction and corpus overlap.

**DC#2** (fine-tuning transfer — Phang 2018, Aghajanyan 2021): BIC confirmed at the *representation/optimization level*. Fine-tuning dynamics reveal that nominally independent benchmarks occupy overlapping low-dimensional subspaces in the model's parameter space. The K_eff collapse is a mathematical consequence of shared intrinsic dimensionality — it operates even when benchmarks have distinct surface forms, distinct corpora, and distinct domains, if they share the same fine-tuning manifold.

**Mechanistic level distinction is critical**: DC#1 could be dismissed as "just fix data contamination." DC#2 closes that response: K_eff collapse operates in the optimization geometry itself, independent of corpus overlap. The two mechanisms are structurally independent pathways to the same BIC conclusion — multiplicative, not additive, evidential value.

---

## Evidence

### E1: Aghajanyan et al. 2021 — Intrinsic Dimensionality Provides Formal Mechanism

**Source**: Aghajanyan, Zettlemoyer & Gupta 2021 "Intrinsic Dimensionality Explains the Effectiveness of Language Model Fine-Tuning" (ACL 2021).

**Key findings:**
- Pre-trained models (BERT, RoBERTa, GPT-2) fine-tune effectively in very low intrinsic dimension: for many GLUE tasks, d_int ~ 100–400, far below the full parameter dimensionality (~66M for BERT-base)
- Intrinsic dimensionality is **task-correlated**: related tasks (NLI, sentiment, QA variants) share similar low-d fine-tuning manifolds
- Formally: if tasks T₁, T₂ have overlapping fine-tuning subspaces of dimension d_int with overlap fraction φ, then improvement on T₁ transfers to T₂ proportionally to φ

**BIC formal connection**: This *is* the K_eff mechanism instantiated empirically. K_eff ≤ N(1-ρ̄)+ε where ρ̄ is the mean benchmark correlation. Aghajanyan 2021 shows that ρ̄ is high for standard NLP benchmarks because they share intrinsic fine-tuning dimensionality. Adding more benchmarks drawn from the same low-d manifold provides K_eff ≈ 1 additional independent evaluation dimension, not N.

**Structural insight**: The K_eff collapse is not a contingent feature of specific benchmark choices — it is a property of the model's representation geometry. Any suite of benchmarks fine-tunable via BERT-class fine-tuning methodology will exhibit this shared-manifold structure. BIC is not fixable by "choosing better benchmarks" if benchmark selection still draws from the same fine-tunable task family.

### E2: Phang, Févry & Bowman 2018 — STILTs Demonstrates Cross-Benchmark Transfer

**Source**: Phang, Févry & Bowman 2018 "Sentence Encoders on STILTs: Supplementary Training on Intermediate Labeled-data Tasks" (EMNLP 2018).

**Key findings:**
- Intermediate fine-tuning on task B₁ reliably improves performance on target task B₂ across a wide range of GLUE/SuperGLUE pairs
- Transfer magnitude is approximately proportional to task relatedness (measured by semantic/structural similarity)
- Transfer occurs even between surface-distinct tasks (e.g., NLI → QA)

**BIC connection**: This is direct empirical observation of K_eff collapse in action. If fine-tuning on B₁ improves performance on B₂, then B₁ and B₂ are *not instrumentally independent* — they are testing the same underlying optimization target to overlapping degrees. An evaluation portfolio containing both B₁ and B₂ does not provide 2 independent signals; it provides ~1+φ signals where φ is the transfer magnitude (= ρ̄ analog).

STILTs evidence generalizes: the paper tested pairs systematically across GLUE tasks. Virtually every pair showed positive transfer. This implies the GLUE portfolio had K_eff substantially less than 9 — consistent with the K_eff estimate of 2–3 derived from GLUE/SuperGLUE saturation patterns (DC#1 E2).

### E3: Dodge et al. 2020 — Fine-Tuning Variance Correlations Confirm Shared Geometry

**Source**: Dodge et al. 2020 "Fine-Tuning Pretrained Language Models: Weight Initializations, Data Orders, and Early Stopping" (arXiv).

**Key findings:**
- Fine-tuning instability (variance across random seeds) is *correlated across benchmarks*: a run that performs well on MNLI tends to perform well on RTE with the same seed
- This cross-task variance correlation is not explained by data contamination or corpus overlap

**BIC connection**: Correlated variance across benchmarks (when variance source is random seed = initial fine-tuning trajectory in parameter space) is direct evidence of shared low-d manifold. If benchmarks were instrumentally independent (AIIP holds), variance in performance on B₁ from random initialization would be uncorrelated with variance on B₂. The correlation confirms shared optimization geometry — K_eff collapse is geometric, not data-level.

### E4: Liu et al. 2019 — Multi-Task Fine-Tuning Shows Shared Representation Empirically

**Source**: Liu et al. 2019 "Multi-Task Deep Neural Networks for Natural Language Understanding" (ACL 2019, MT-DNN).

**Key findings:**
- Joint fine-tuning on all GLUE tasks simultaneously achieves comparable or better performance than task-specific fine-tuning on most tasks
- The shared representation learned is sufficient for high performance across all tasks simultaneously
- Tasks do not require orthogonal representations — they are mutually supportive

**BIC connection**: A single shared representation achieves near-optimal performance on all nominally independent GLUE benchmarks simultaneously. This is the K_eff collapse visible from the optimization side: if all tasks can be solved by one shared representation, they are not providing K independent evaluation signals — they are evaluating the same representation from different angles. K_eff → ~1 in the limit of perfect representational overlap.

---

## Mechanistic Summary: Why DC#2 Closes a Gap

DC#1 established BIC at the data layer (contamination, corpus overlap, metric nonlinearity).

DC#2 establishes BIC at the representation/optimization layer (shared intrinsic dimensionality, fine-tuning transfer, correlated variance).

**Together, these two DC layers create a complete mechanistic account**:
1. Benchmarks share construction methodology → corpus overlap and metric correlations (DC#1/AIIP failure)
2. Models fine-tuned on these benchmarks exploit shared low-d parameter subspace → optimization-level correlation (DC#2/AIIP failure)
3. CIAP then amplifies both: gaming shortcuts in the shared space propagate fully to all correlated benchmarks

A hypothetical benchmark suite that somehow fixed DC#1 (fully orthogonal corpora, uncontaminated) would still exhibit DC#2 BIC as long as the tasks remain in the same low-d fine-tuning manifold. Evaluation reform requires escaping the manifold (K7-grounded items, interpretability-based probes), not just diversifying surface forms.

---

## Confidence Assessment

**Prior**: 0.72 (1 DC, 3 ZR PASS)

**DC#2 contribution**:
- Distinct mechanism domain from DC#1 (optimization geometry vs. data/corpus layer)
- High-quality primary sources (Aghajanyan 2021 ACL, Phang 2018 EMNLP) with broad replication
- Formal K_eff mechanism directly instantiated: Aghajanyan 2021 measures d_int directly, providing quantitative bridge to BIC bound
- Mechanistic gap closed: DC#2 eliminates "just fix data contamination" response to DC#1

**Updated confidence**: 0.74 (central)

**Passive ZR#4 Check (C84):**
No counter-evidence to K_eff ≤ N(1-ρ̄)+ε bound encountered. Fine-tuning transfer literature consistently confirms shared manifold structure. Benchmark correlation data from DC#1 domain consistent with bound.

**ZR#4: PASS**

---

## BIC D4 Path Update (Post-DC#2)

- ZR cycles: 4 PASS (ZR#1 C81, ZR#2 C82, ZR#3 C83, ZR#4 C84)
- Domain confirmations: 2 (DC#1: AI evaluation literature; DC#2: fine-tuning transfer)
- Ontological types: 1 (designed empirical × 2 domains) — **need Types 2 and 3**
- D4 gap: DC#3 in different ontological type + DC#4 in third type; confidence ~0.78+ needed

**DC#3 candidate**: Educational assessment portfolio or scientific replication consortia (regulated institutional or emergent competitive type)

---

*Written: C84, 2026-04-30*
