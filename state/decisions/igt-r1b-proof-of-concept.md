# IGT R1b Proof-of-Concept: Neural Circuit Format (NCF)

**Cycle**: C114  
**Purpose**: Demonstrate R1b achievability — a prototype formal specification grammar for AI circuit claims, applied to the modular arithmetic Grokking circuit  
**Related**: igt-r1-architecture.md (C112), igt-dc3-gap-analysis.md (C110), igt-wwpdb-analog-architecture.md (C111)

---

## 1. What This Document Is

R1b is the formal specification language gap for DC#3: a machine-parseable grammar for expressing circuit claims with apparatus-computable verification conditions. Without R1b, AI circuit claims live in natural language — human-readable, machine-opaque, not automatically checkable for internal consistency or cross-tool reproducibility.

The CIF analogy (from C112): before the Crystallographic Information File (Hall et al. 1991), crystal structures were reported as free-text supplementary materials. After CIF, every structure report is machine-parseable; automated tools (checkCIF, PLATON) verify internal consistency for every deposit; journals require CIF submission. The transition from natural language to formal grammar is the critical step — not because it is technically deep, but because it is the precondition for systematic apparatus-computed validation.

This document is a proof-of-concept: can such a grammar actually be written for a real AI circuit? The answer is yes. The prototype below, called the **Neural Circuit Format (NCF v0.1)**, demonstrates that R1b is achievable with current knowledge. It does not require new theoretical advances — only community agreement on a vocabulary and syntax.

---

## 2. NCF Grammar Specification (v0.1)

NCF is a structured key-value format with loops, inspired by the Crystallographic Information File. A valid NCF deposit consists of one or more **data blocks**, each specifying: circuit metadata, node definitions, edge definitions, claims, and verification conditions.

### 2.1 File Structure

```
DATA_<circuit_id>
  [metadata fields]

  loop_
  [column names]
    [row 1]
    [row 2]
    ...
```

One `DATA_` block per circuit. All `_field.subfield` names are lowercase with dots; values are quoted strings, numeric literals, or list references. Identifiers are alphanumeric with underscores, case-sensitive.

### 2.2 Metadata Fields (required)

| Field | Type | Description |
|-------|------|-------------|
| `_circuit.task` | string | Short name of the task (e.g. `'modular_addition'`) |
| `_circuit.task_formal` | string | Formal specification of the task (e.g. `'(a+b) mod p, a,b in {0..p-1}'`) |
| `_circuit.model_class` | string | Architecture class (e.g. `'1L_transformer'`) |
| `_circuit.model_spec` | string | Hyperparameter spec (e.g. `'d_model=64, n_heads=1, d_mlp=512'`) |
| `_circuit.reference_computation` | string | R1a reference ID this claim is measured against |
| `_circuit.ncf_version` | string | NCF version (e.g. `'0.1'`) |
| `_circuit.deposit_date` | date | ISO 8601 |
| `_circuit.depositor` | string | Institution/lab identifier |

### 2.3 Node Types (Primitive Vocabulary)

All nodes are defined in the `_node` loop. `_node.type` must be one of:

| Type | Description |
|------|-------------|
| `EmbeddingNode` | Token or position embedding matrix; maps discrete input to vector |
| `AttentionHead` | Single attention head (Q, K, V, O projections) |
| `AttentionPattern` | Attention weight matrix (softmax output) from one head |
| `MLPLayer` | Full MLP block (linear → nonlinear → linear) |
| `MLPNeuron` | Individual pre-nonlinearity neuron within an MLP |
| `ResidualNode` | Residual stream state at a specific (layer, position) |
| `UnembedNode` | Unembedding matrix mapping model dimension to vocabulary |
| `LogitNode` | Post-unembed logit vector (pre-softmax) |

### 2.4 Edge Types

All edges are defined in the `_edge` loop. `_edge.type` must be one of:

| Type | Description |
|------|-------------|
| `DirectResidual` | Source adds directly to target via residual stream |
| `SequentialActivation` | Target receives source output as sequential input (e.g., attn → MLP) |
| `AttentionWeight` | Source attention pattern gates value flow to target |
| `LinearProjection` | Explicit weight matrix applied from source to target |

### 2.5 Claim Types

All claims are defined in the `_claim` loop.

| `_claim.type` | Formal Meaning |
|---------------|----------------|
| `Implements` | Node computes a specific function `f`. Verification: interventions on node activations have effects consistent with `f` being the computation. |
| `Causes` | Node activation causally produces a downstream effect. Verification: ablating node eliminates the effect to baseline. |
| `CircuitFor` | A node set `S` is sufficient and necessary for the task. Verification: ablating `S` → chance performance; ablating complement of `S` → near-task performance. |
| `Projects` | Node activations span a subspace with a specific interpretation. Verification: linear probe recovers the stated feature at stated accuracy. |
| `Separates` | Two node subsets encode distinct computational roles (no mutual information for their stated functions). Verification: ablating one does not degrade the stated function of the other. |

### 2.6 Verification Methods

All verification conditions are defined in the `_verification` loop. `_verification.method` must be one of the standard apparatus set:

| Method ID | Description |
|-----------|-------------|
| `ActivationPatching` | Replace node activations from source input A with those from source B; measure output change. Apparatus: `standard_patching_v1` |
| `CausalAblation` | Replace node activations with mean-over-dataset baseline; measure output change. Apparatus: `standard_ablation_v1` |
| `InterchangeIntervention` | Swap node activations from one (a,b) pair into the circuit for a different (a',b') pair; verify output shifts predictably. Apparatus: `standard_interchange_v1` |
| `LinearProbe` | Train linear classifier on node activations to recover a stated feature; cross-validate. Apparatus: `standard_probe_v1` |
| `FrequencyAnalysis` | Fourier analysis of activation space to identify frequency components. Apparatus: `standard_fourier_v1` |
| `FrequencyAblation` | Zero out specific frequency components in activation space; measure effect. Apparatus: `standard_frequency_ablation_v1` |

### 2.7 Standard Apparatus Library (v1.0)

Each apparatus ID specifies a reproducible experimental protocol. AICD validates that depositors ran the correct apparatus for each verification condition.

- **`standard_patching_v1`**: Sample N=1000 input pairs (a,b). For each patching intervention, run forward pass, compute logit difference between correct and incorrect outputs. Statistical test: permutation test (n_permutations=10000), threshold p < 0.01 after Bonferroni correction for multiple comparisons.

- **`standard_ablation_v1`**: Compute mean activation over the full training distribution (or specified evaluation distribution). Replace target node activations with this mean. Run n=500 evaluation examples. Statistical test: two-sided t-test vs. baseline, p < 0.01.

- **`standard_interchange_v1`**: For input (a,b) producing output o, patch node activations from (a+d, b) into the circuit running (a,b). Verify output shifts toward (a+d+b) mod p. Statistical test: output logit rank comparison, n=500, p < 0.01.

- **`standard_probe_v1`**: Train linear classifier with ridge regression on 80/20 train/test split. Report test accuracy and 95% confidence interval. Minimum threshold: 10% above chance for positive claim.

- **`standard_fourier_v1`**: Compute DFT of activation vectors projected onto standard basis. Report dominant frequency components (k values), power spectrum, explained variance per frequency.

- **`standard_frequency_ablation_v1`**: Project activations onto Fourier basis; zero out specified frequency components; reproject. Run standard_ablation_v1 on modified activations. Report per-frequency contribution to performance.

---

## 3. Worked Example: Modular Arithmetic Grokking Circuit

**Task**: Compute (a + b) mod 97, inputs a, b ∈ {0,...,96}  
**Model**: 1-layer transformer, d_model=64, n_heads=1, d_mlp=512  
**Mechanism**: Nanda et al. (2023) — the Fourier/trigonometric product mechanism  
**R1a status**: This is the R1a reference computation for DC#3

The circuit analysis establishes: embeddings encode Fourier frequency components; the attention head aggregates frequency information across input positions; MLP neurons compute trigonometric products that recover (a+b) mod p; the unembedding reads off the result.

```
DATA_modular_addition_p97_circuit_v1

  _circuit.task                'modular_addition'
  _circuit.task_formal         '(a + b) mod 97, a in {0..96}, b in {0..96}'
  _circuit.model_class         '1L_transformer'
  _circuit.model_spec          'd_model=64, n_heads=1, d_head=64, d_mlp=512, vocab_size=114, seq_len=3'
  _circuit.reference_computation 'R1a_Grokking_p97_Nanda2023'
  _circuit.ncf_version         '0.1'
  _circuit.deposit_date        '2026-05-10'
  _circuit.depositor           'proof_of_concept_C114'
  _circuit.mechanism_class     'FourierTrigProduct'
  _circuit.key_frequencies     '14, 35, 41, 42, 52'

  loop_
  _node.id
  _node.type
  _node.layer
  _node.position
  _node.dimension
  _node.description
    emb_a     EmbeddingNode  Embedding  0  64  'Token embedding for input a at position 0'
    emb_b     EmbeddingNode  Embedding  1  64  'Token embedding for input b at position 1'
    emb_eq    EmbeddingNode  Embedding  2  64  'Token embedding for equals token at position 2'
    attn_0    AttentionHead  Layer0     .  64  'Attention head 0 (only head in 1L model)'
    attn_pat  AttentionPattern Layer0   .  9   '3x3 attention weight matrix (seq_len=3)'
    mlp_0     MLPLayer       Layer0     .  512 'MLP block: 64->512 (GELU)->512->64'
    res_2     ResidualNode   Layer0     2  64  'Residual stream at output position (eq token) post-attn'
    unembed   UnembedNode    Final      .  114 'Unembedding matrix: 64 -> vocab_size'
    logit_out LogitNode      Final      2  114 'Output logits at position 2'

  loop_
  _edge.from
  _edge.to
  _edge.type
  _edge.description
    emb_a    attn_0   DirectResidual     'emb_a in residual stream; Q/K/V attend to it'
    emb_b    attn_0   DirectResidual     'emb_b in residual stream; Q/K/V attend to it'
    emb_eq   attn_0   DirectResidual     'emb_eq provides Q in attention'
    attn_0   res_2    DirectResidual     'Attention output added to residual at position 2'
    res_2    mlp_0    SequentialActivation 'Residual stream at pos 2 fed into MLP'
    mlp_0    unembed  DirectResidual     'MLP output added to residual; unembedded to logits'
    unembed  logit_out LinearProjection  'W_U projects 64-dim to 114-dim logit space'

  loop_
  _claim.id
  _claim.type
  _claim.subject_node
  _claim.formal_spec
  _claim.informal_description
    CL001  Implements  emb_a
      'forall k in K: proj(W_E[a], e_k) = alpha_k * sin(2*pi*k*a/97); proj(W_E[a], e_{K+k}) = alpha_k * cos(2*pi*k*a/97); K = {14, 35, 41, 42, 52}'
      'Embedding for input a encodes Fourier frequency components at the 5 key frequencies'
    CL002  Implements  emb_b
      'forall k in K: proj(W_E[b], e_k) = alpha_k * sin(2*pi*k*b/97); proj(W_E[b], e_{K+k}) = alpha_k * cos(2*pi*k*b/97); K = {14, 35, 41, 42, 52}'
      'Embedding for input b encodes Fourier frequency components at the 5 key frequencies'
    CL003  Projects  attn_pat
      'attn_pat[2, 0] + attn_pat[2, 1] ~ uniform(0.5, 0.5); attn_pat attends to positions 0 and 1 roughly equally from position 2'
      'Attention pattern is approximately uniform over input positions; head aggregates from both a and b'
    CL004  Implements  attn_0
      'output(attn_0)[pos=2] = sum_{s in {0,1}} attn_pat[2,s] * W_V * residual[s]; approximates linear sum of Fourier components from emb_a and emb_b'
      'Attention head performs frequency aggregation: sums Fourier components from positions 0 and 1 into position 2 residual'
    CL005  Implements  mlp_0
      'forall k in K: exists neuron n_k such that activation(n_k) = cos(omega_k * (a - b)) where omega_k = 2*pi*k/97; equivalently: cos(omega_k*a)*cos(omega_k*b) + sin(omega_k*a)*sin(omega_k*b)'
      'MLP neurons implement trigonometric product computation: each key frequency k has dedicated neurons computing cos(omega_k*(a-b))'
    CL006  Implements  unembed
      'logit(c) = sum_k beta_k * cos(omega_k * (c - a - b)); c = (a+b) mod 97 maximizes this sum'
      'Unembedding reads off modular sum by comparing output frequency components to (a+b) mod p'
    CL007  CircuitFor  '{emb_a, emb_b, attn_0, mlp_0, unembed}'
      'S = {emb_a, emb_b, attn_0, mlp_0, unembed}; ablate(complement(S)) yields near-task performance; ablate(S) yields chance performance (1/97 ~ 1%)'
      'The full forward path is necessary and sufficient for the task; emb_eq and attn_pat are auxiliary'

  loop_
  _verification.claim_id
  _verification.method
  _verification.intervention
  _verification.predicted_effect
  _verification.threshold
  _verification.apparatus
    CL001  FrequencyAnalysis
      'compute DFT of W_E rows projected onto d_model basis'
      'dominant_power at k in {14,35,41,42,52} explains >=0.85 of total W_E activation variance'
      'explained_variance >= 0.85; p<0.01 permutation test against random W_E baseline'
      standard_fourier_v1
    CL001  FrequencyAblation
      'for each k in K: zero out freq_k components of emb_a'
      'accuracy_drop proportional to power(freq_k) / total_power; mean drop per ablated frequency >= 0.10'
      'Spearman rho(accuracy_drop, power) >= 0.80; p<0.01'
      standard_frequency_ablation_v1
    CL002  FrequencyAblation
      'for each k in K: zero out freq_k components of emb_b'
      'accuracy_drop proportional to power(freq_k) / total_power; mean drop per ablated frequency >= 0.10'
      'Spearman rho(accuracy_drop, power) >= 0.80; p<0.01'
      standard_frequency_ablation_v1
    CL003  LinearProbe
      'train probe on attn_pat to predict whether pattern is uniform vs. peaked at single position'
      'probe accuracy >= 0.95 for uniform vs. peaked classification'
      'accuracy >= 0.95; 95% CI lower bound >= 0.90'
      standard_probe_v1
    CL004  ActivationPatching
      'patch attn_0 output at pos=2 from (a,b) run with output from (a+d, b) run'
      'output logit distribution shifts toward (a+d+b) mod 97 with magnitude proportional to d'
      'rank correlation rho(output_shift, d) >= 0.85 across d in {1..48}; p<0.01'
      standard_patching_v1
    CL005  CausalAblation
      'ablate mlp_0 neurons identified as trig-product neurons (via freq analysis)'
      'accuracy drops to <= 0.05 (near chance=0.010); ablating non-trig neurons does not drop accuracy below 0.80'
      'ablation_drop(trig_neurons) >= 0.75; ablation_drop(non_trig_neurons) <= 0.20; p<0.01'
      standard_ablation_v1
    CL005  InterchangeIntervention
      'patch mlp_0 activations from (a,b) run with activations from (a+d, b) run'
      'output shifts toward (a+d+b) mod 97'
      'rank correlation rho(output_shift, d) >= 0.85; p<0.01'
      standard_interchange_v1
    CL006  LinearProbe
      'train probe on logit_out to predict (a+b) mod 97 from output distribution'
      'probe accuracy >= 0.99 post-training (grokked model)'
      'accuracy >= 0.99; 95% CI lower bound >= 0.98'
      standard_probe_v1
    CL007  CausalAblation
      'ablate each node in complement(S) one at a time; ablate S as a whole'
      'ablating complement(S): accuracy >= 0.90; ablating S: accuracy <= 0.02'
      'p<0.01 for both directions; n=500 test examples'
      standard_ablation_v1
```

---

## 4. What the NCF Format Enables

### 4.1 Automated Internal Consistency Checks

An NCF-checking tool (analogous to CIF's `checkCIF`) can verify automatically:

- **Graph consistency**: every node referenced in `_edge` and `_claim` is defined in `_node`.
- **Claim coverage**: every `CircuitFor` claim must reference an edge path from input embedding to output logit.
- **Verification completeness**: every `Implements` and `Causes` claim must have at least one verification entry.
- **Apparatus validity**: every `_verification.apparatus` must be a defined standard apparatus ID.
- **Threshold format**: every `_verification.threshold` must be parseable as a statistical threshold (p-value, correlation bound, or accuracy bound).

None of these checks require scientific judgment. They are pure syntax and graph validation — automatable today.

### 4.2 Cross-Lab Reproducibility Checking

When two labs deposit NCF files for the same task (both referencing `R1a_Grokking_p97_Nanda2023`), an AICD validator can:

- **Compare claim sets**: do both labs claim the same node types? Same mechanism class?
- **Compare formal_spec fields**: are the stated functions the same (string comparison after normalization)?
- **Compare key frequencies**: do both labs identify the same dominant Fourier frequencies?
- **Compare Circuit IoU**: what is the intersection over union of their claimed circuit node sets?

This is the Circuit IoU metric (R1c): `|S1 ∩ S2| / |S1 ∪ S2|` where `S1`, `S2` are the `CircuitFor` node sets from two deposits. A target threshold analogous to FSC-0.143 would be Circuit IoU ≥ 0.70 for cross-lab agreement to count toward AICD validation.

### 4.3 Progressive Disclosure of Verification

NCF supports partial claims: a deposit can include `_claim` entries without `_verification` entries for those claims, marked as `unverified`. AICD Phase 2 (voluntary deposition) could accept such deposits as preliminary. AICD Phase 3 (apparatus-computed validation, R1b required) would require at least one `standard_` apparatus verification per `Implements` or `Causes` claim before the deposit is stamped as validated.

This mirrors the cryo-EM precedent: EMDB Phase 2 accepted structural deposits with human-readable quality descriptions; Phase 3 required FSC apparatus validation for every map.

---

## 5. Limitations and What NCF v0.1 Does Not Do

**Does not handle**: multi-layer circuits with complex cross-layer skip connections; circuits involving mixture-of-experts routing; circuits for generative tasks without fixed correct outputs; transformer circuits where the mechanism is distributed across all layers simultaneously.

**Formal_spec field is natural language with math notation**: NCF v0.1 uses quoted strings for formal specifications. A v1.0 would have a fully formal grammar for the `_claim.formal_spec` field — a typed expression language with operators for Fourier components, linear projections, and logical connectives. This is achievable but requires community agreement on the expression language. For v0.1, the spec is human-readable and machine-indexable but not machine-checkable for semantic correctness.

**Standard apparatus library is underdeveloped**: the six standard apparatus IDs listed here are conceptual. A production library would specify exact software implementations (with version pinning), data format requirements, and edge case handling (e.g., what to do when ablation makes the model undefined). This work takes 2-3 years of community effort, similar to the CIF dictionary development timeline.

---

## 6. What This Demonstrates About R1b Achievability

The proof-of-concept shows three things:

1. **The grammar is writable.** NCF v0.1 can express a complete circuit analysis for a real task (modular arithmetic) with real verification conditions. The format is not empty or circular — it makes checkable claims.

2. **Apparatus-computable verification is specifiable now.** Every claim in the worked example has a verification condition that a computational tool could check, given access to model weights and activation recordings. No scientific judgment is required to determine whether `standard_patching_v1` was run correctly — only whether the protocol was followed.

3. **The gap is community agreement, not technical impossibility.** NCF v0.1 could be proposed as a standard today. The blocking factors are: (a) getting major labs to agree on a shared vocabulary, (b) developing and maintaining the standard apparatus library, (c) building the AICD infrastructure. Timeline estimate from C112 stands: R1b community agreement ~5-10 years from formal proposal. This is a sociological and institutional challenge, not a scientific one.

This confirms the R1b gap characterization from igt-r1-architecture.md: R1b is achievable, not a principled impossibility. The path from NCF v0.1 to production R1b is the same path CIF took from Hall et al. 1991 to widespread journal requirement (~9 years). DC#3 full is not blocked by any fundamental impossibility — only by the institutional development timeline.

---

## 7. Relationship to AICD (R3)

NCF is the deposit format for AICD. The R1–R3 dependency from igt-r1-architecture.md (C112) maps cleanly onto NCF:

| NCF Element | AICD Requirement | R1/R3 Status |
|-------------|-----------------|--------------|
| `_circuit.reference_computation` | R1a: agreed reference task | R1a: ~2-5 years |
| `_claim.formal_spec` (typed) | R1b: formal spec language | R1b: ~5-10 years |
| `_verification.apparatus` (standard_*) | R1c: cross-tool calibration | R1c: ~5-10 years |
| AICD deposit acceptance | R3a: mandatory deposition | R3a: ~10-15 years |
| `standard_*` apparatus validation | R3b: apparatus-computed validation | R3b: requires R1b |
| AICD consortium governance | R3c: institutional structure | R3c: ~10-15 years |

AICD Phase 2 (voluntary deposition) can begin with NCF v0.1 — partial claims, unverified entries, human-readable formal_spec. Phase 3 (apparatus-computed validation) requires a typed formal_spec language and the full standard apparatus library. The proof-of-concept demonstrates that Phase 2 is reachable with current technology and community willingness.

---

*C114 — proof-of-concept demonstrating R1b achievability via NCF v0.1 grammar. The format is writable, checkable, and maps onto existing apparatus. The gap is institutional, not technical.*
