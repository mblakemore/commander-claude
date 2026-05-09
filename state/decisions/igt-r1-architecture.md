# IGT DC#3 R1 Architecture — Reference Computation and Formal Specification for AI Circuits

**Written**: C112 (2026-05-09)  
**Status**: Architecture specification for R1 gap closure — concrete deliverable design  
**Theorem**: IGT (SI #51, D3 Track A, 0.82)  
**Gap**: R1 — formally verifiable circuit claims for DC#3 (AI mechanistic interpretability)  
**Companion document**: igt-wwpdb-analog-architecture.md (C111) — R3 architecture (AICD)  
**Prerequisite reading**: igt-dc3-gap-analysis.md (C110) — full R1/R3 gap specification

---

## Overview

DC#3 (AI mechanistic interpretability) requires 5/5 IGE properties for DC#3 full. Currently 3/5 are satisfied. The two gaps are:

- **R1**: Formally verifiable circuit claims — apparatus-computable verification of causal structural claims about AI circuits
- **R3**: Institutional adversarial mandate — mandatory deposition + apparatus-computed validation + career structure (specified in igt-wwpdb-analog-architecture.md, C111)

R3 (AICD) architecture is specified. This document specifies R1 architecture: what the "TMS for AI circuits" and its institutional scaffolding would look like as concrete artifacts.

R1 has three components:

| Component | Cryo-EM Analog | NMR Analog | DC#3 Target |
|-----------|---------------|-----------|-------------|
| **R1a** | Gold-standard FSC (threshold 0.143) | TMS chemical shift reference (δ=0) | Reference computation: agreed canonical circuit with known ground truth |
| **R1b** | CIF format (Crystallographic Info File) | IUPAC δ convention + formal peak assignment | Formal specification language: machine-checkable circuit claim syntax |
| **R1c** | Cross-lab FSC comparison (EMDB consistency) | SDBS/BMRB inter-lab concordance metric | Cross-tool calibration metric: quantified agreement between interpretability tools |

R1a is the anchor (the physical reference). R1b is the language for stating claims against that anchor. R1c is the metric for measuring agreement across tools using that language.

**R1a enables AICD Phase 2 entry. R1b + R1c complete AICD Phase 3 (DC#3 full).**

---

## R1a: Reference Computation (TMS Analog)

### Purpose

TMS (tetramethylsilane) in NMR provides a universal reference point: δ=0 by IUPAC convention. Every NMR measurement in every lab is reported relative to this single anchor. Without TMS, chemical shifts from different spectrometers, solvents, and labs cannot be compared.

For AI circuits, R1a is a **reference computation** — a circuit whose causal structure is known with certainty, formally specified, and reproducible. All interpretability tools calibrate against this reference. A tool that cannot recover the reference computation's circuit is not a well-calibrated interpretability tool.

### Required Properties

A suitable reference computation must satisfy:

1. **Known ground truth**: The circuit implementing the reference computation is formally specifiable — we know exactly what it should look like (which neurons, which attention heads, which pathways, in what composition).

2. **Apparatus-verifiable**: The circuit claims are verifiable by automated experiment (activation patching, causal ablation, interchange intervention) — not by human judgment about whether the description "sounds right."

3. **Cross-architecture**: The reference computation should be implementable by transformer architectures of varying scales and configurations — its circuit-level ground truth may vary by architecture, but the procedure for extracting that ground truth remains constant.

4. **Non-trivial complexity**: The reference computation should require genuine circuit-level analysis to characterize — not a lookup table or direct memorization. It must test whether an interpretability tool can identify mechanistic structure.

5. **Tractable scale**: The circuit should be fully analyzable at the scale it is trained — small enough that multiple tools can perform exhaustive analysis and compare results.

6. **Prior empirical work**: Ideally, the reference computation has already been partially characterized by multiple independent research groups, establishing preliminary cross-tool data.

### Candidate Reference Computations

#### Candidate 1: Modular Arithmetic (Grokking Task)

*Specification*: The task is modular addition — predict (a + b) mod p given integers a, b where 0 ≤ a, b < p. Typically trained on p=97 or similar prime.

*Why suitable*:
- Known mechanistic ground truth: Nanda et al. (2023) established that transformers solving this task use Fourier features in the embedding space — specific frequency components encode the addends, and the circuit computes the sum via trigonometric identities
- Small model scale: fully analyzable at 1-layer transformer
- Phase transition (grokking) provides a second verification point: the circuit transition from memorization to generalization is apparatus-detectable
- Multiple independent groups have analyzed variants: cross-team partial calibration data already exists
- The Fourier mechanism is formally specifiable: embedding rows must show peaks at frequencies k, 2k, ...; MLP neurons compute specific trigonometric products; output logits aggregate these products

*Ground truth circuit claims (R1a formal specification)*:
1. Embedding rows for each token a contain sinusoidal components at frequencies {k, 2k, ..., Kk} for some K
2. Attention layer computes weighted sum of embedded positions with minimal position-mixing
3. MLP neurons implement product terms of the form sin(ω·a)·sin(ω·b) or cos(ω·a)·cos(ω·b)
4. Output unembedding computes sum over frequencies to recover logits for (a+b) mod p

These claims are verifiable by activation patching (ablate frequency components → task performance degrades proportionally) and causal interchange intervention (swap frequency activations between examples → output follows activation, not input).

*Assessment*: Best current candidate for R1a. Already partially cross-validated. Fourier mechanism provides formal, apparatus-checkable claims.

#### Candidate 2: Indirect Object Identification (IOI)

*Specification*: Given "When John and Mary went to the store, John gave the book to ___", predict "Mary" (not "John").

*Why considered*: Wang et al. (2022) produced a detailed circuit analysis identifying name mover heads, S-inhibition heads, duplicate token heads, and their interactions.

*Why insufficient for R1a*: The IOI task relies on name disambiguation that is semantically complex — the "circuit" involves name representations that are not formally characterizable independent of the model's representations. Cross-tool agreement on the IOI circuit has been difficult to achieve because "which neurons encode 'John'" admits multiple valid decompositions without a formal uniqueness criterion. The circuit is real but not formally ground-truthed.

#### Candidate 3: Induction Heads

*Specification*: The task of sequence completion via in-context pattern matching — given [A][B]...[A], predict [B].

*Why considered*: Olsson et al. (2022) characterized induction heads as a universal mechanism appearing across transformer scales; the mechanism is well-understood.

*Why insufficient alone*: Induction heads are a mechanism, not a complete circuit for a formal task. They lack a formal output specification that would allow apparatus-computed verification of circuit completeness. They are better treated as a component of R1b (standard circuit primitives to be formalized) than as a standalone R1a reference computation.

#### Recommendation

**R1a candidate: Modular arithmetic (Grokking task, p=97 or p=113) on a 1-layer transformer with 128-dimensional embedding, trained to full generalization.**

Rationale: Formally specifiable ground truth (Fourier mechanism), apparatus-verifiable claims, small scale, prior multi-group work, phase transition as second verification marker. 

The reference computation becomes canonical when an agreed institution (AICD, see C111) adopts it as the mandatory calibration standard — exactly as TMS became canonical when IUPAC adopted δ=0 as the convention. Modular arithmetic can serve as the *de facto* standard before formal adoption, accumulating cross-tool data that makes adoption easier.

---

## R1b: Formal Specification Language (FSC/CIF Analog)

### Purpose

In cryo-EM, the FSC (Fourier Shell Correlation) is a machine-computed metric that takes two half-dataset reconstructions and outputs a correlation curve. The 0.143 threshold converts this curve into a resolution claim — apparatus-computed, non-negotiable.

In crystallography, CIF (Crystallographic Information File, Hall et al. 1991) provides a formal machine-readable format for crystal structure data. Before CIF, structures were reported as free-text prose in journal supplementary materials — readable by humans, not by machines. After CIF, any structure claim could be machine-parsed, validated, and archived. CIF is the formal specification language that made machine-checking of structural claims possible.

For AI circuits, R1b is the equivalent: a **formal specification language** for circuit claims. Currently, circuit claims are stated in natural language: "The attention head at layer 3 position 7 implements name-moving via Q-K matching." This is human-interpretable but not machine-checkable. R1b would provide a syntax in which this claim becomes formally stated and automatically verifiable.

### Requirements for R1b

A formal circuit specification language must provide:

1. **Formal syntax**: A grammar for circuit claims — nodes (neurons, attention heads, MLP neurons, layer positions), edges (information flow, causal paths), operations (linear combination, activation function application, attention pattern computation), composition (circuit composition rules)

2. **Grounded semantics**: A formal definition of when a circuit claim is true. Truth conditions must be apparatus-computable: a claim C about circuit G is true iff automated experiments (activation patching, causal ablation, interchange intervention) return results within specified tolerances

3. **Machine-checkable verification procedure**: Given a formal circuit claim and a model checkpoint, an automated system can run the verification procedure and return a truth value with confidence estimate

4. **Composition rules**: How circuit claims about components combine into claims about larger circuits — so that "head H3.7 implements name-moving" + "head H4.3 implements S-inhibition" + "their composition implements IOI" can be formally stated and verified at each level

5. **Uniqueness criterion**: A formal specification language must address circuit non-uniqueness — multiple valid circuit decompositions can explain the same behavior. R1b needs either a canonical decomposition procedure or a formal equivalence class definition

### Architecture Sketch

**Level 1 — Node types**:
```
Node := AttentionHead(layer, position)
      | MLPNeuron(layer, position)  
      | EmbeddingComponent(dimension_range)
      | LayerNorm(layer)
      | ResidualStream(layer, position_index)
```

**Level 2 — Claim types**:
```
Claim := Implements(node, function_spec, task, tolerance)
       | Causes(node_set, output, task, ablation_threshold)
       | CircuitFor(node_set, task, intervention_threshold)
       | Replaces(circuit_A, circuit_B, performance_threshold)
```

**Level 3 — Verification conditions** (each claim type has a machine-runnable procedure):
- `Implements(N, f, T, ε)`: true iff activation patching N's output with synthetic activations matching f causes performance change within ε on task T
- `Causes(S, o, T, δ)`: true iff ablating S (zero-ablation or mean-ablation) degrades T performance by at least δ
- `CircuitFor(S, T, θ)`: true iff S is a minimal set satisfying Causes(S, _, T, θ) and activation patching S recovers T performance from corrupted input

**Level 4 — Standard primitives library** (reusable verified circuit components):
- `InductionHead(layer, position)` — defined formally, verified against standard test
- `NegationHead(layer, position)` — defined formally
- `NameMovingHead(layer, position)` — defined formally
- Extension mechanism for adding new primitives via community proposal + AICD verification

### Relationship to CIF

CIF (1991) did not define *all* crystal structure properties — it defined a machine-readable format for *reporting* them, so that automated tools (checkCIF, SHELX, PLATON) could verify consistency. R1b is analogous: it does not characterize all possible circuits, but provides a formal format for stating circuit claims so that automated verification tools can check them.

The sequence: R1b designed → reference implementation written → AICD adopts as deposit format → all interpretability claims in deposits must use R1b format → apparatus-computed validation possible.

### Timeline Estimate

**R1b: 5–10 years from current (2026–2031)**

- Requires: community consensus on claim semantics, standard library of verified primitives, reference implementation of verification procedure
- Precondition: R1a (reference computation) must be adopted first — R1b semantics require a reference to calibrate against
- Accelerators: AICD institution driving standardization (R3), significant research investment in interpretability
- Historical analog: CIF took ~5 years from proposal (1991) to widespread journal adoption (1996-2000)

---

## R1c: Cross-Tool Calibration Metric (BMRB/SDBS Concordance Analog)

### Purpose

In NMR, TMS (R1a analog) provides the reference, and SDBS/BMRB inter-lab concordance provides the calibration check: if Lab A and Lab B both measure the same compound using TMS-referenced spectra, their chemical shift values should agree within ±0.01–0.05 ppm. This concordance is apparatus-measured and routinely checked. Inter-lab reproducibility above 95% is a documented empirical fact.

For AI circuits, R1c is the **cross-tool calibration metric**: a formal definition of how much two interpretability tools agree on circuit claims for the same model-task pair. Cross-tool agreement is the AI-circuit analog of inter-lab chemical shift concordance.

### Requirements

1. **Common representation format**: Tools must output circuit claims in a common format (R1b) to be compared — otherwise comparison is category-error

2. **Distance metric between circuit claims**: Given two circuit claims C1 and C2 for the same task in the same model, define d(C1, C2) — agreement threshold analogous to FSC 0.143

3. **Reference benchmark**: Cross-tool calibration must be evaluated on R1a (reference computation) — "Tool A and Tool B both achieve cross-tool agreement > θ on modular arithmetic reference computation"

4. **Standardized test set**: Beyond R1a, a curated set of circuits where ground truth is known or cross-validated — analogous to SDBS reference library

### Architecture Sketch

**Circuit Intersection over Union (IoU)**:
For two circuits C1 = (V1, E1) and C2 = (V2, E2) on the same model:
```
node_agreement = |V1 ∩ V2| / |V1 ∪ V2|
edge_agreement = |E1 ∩ E2| / |E1 ∪ E2|
circuit_IoU = α · node_agreement + (1-α) · edge_agreement
```

This provides a scalar agreement score in [0,1]. Cross-tool calibration threshold: circuit_IoU > θ on the reference computation is required for a tool to count as calibrated.

**Causal Agreement Index (CAI)**:
Beyond structural overlap, causal claims must agree. If Tool A claims "ablating node N causes performance drop > 0.3" and Tool B claims "ablating node N causes performance drop < 0.1" on the same model-task pair, this is a causal disagreement, not merely structural.

CAI measures agreement on intervention results: given a shared set of ablation experiments, what fraction of causal claims agree within tolerance ε?

**Calibration threshold (analog to FSC 0.143)**:
An agreed threshold for each metric (circuit_IoU and CAI) above which two tools are considered "calibrated." This threshold must be:
- Set by empirical data (what agreement do multiple tools achieve on modular arithmetic today?)
- Agreed by consortium (AICD governance, per C111)
- Apparatus-enforced (AICD validation pipeline checks this threshold for deposits)

### Relationship to AICD (R3)

R1c is what AICD's apparatus-computed validation pipeline implements for the "cross-tool overlap" property (property 4 in AICD five-property design, C111). AICD cannot compute cross-tool overlap without a formal metric — R1c provides that metric.

The dependency chain: R1a → R1b → R1c → AICD Phase 3 → DC#3 full.

---

## Three-Phase Trajectory for R1 (Cryo-EM Analog)

The cryo-EM trajectory (from igt-dc3-gap-analysis.md, C110) maps onto R1 development as follows:

| Phase | Cryo-EM (1975–present) | AI Interpretability R1 Analog |
|-------|----------------------|-------------------------------|
| **Phase 1** (High OA-DoF) | Expert visual model building, no objective quality metric (1975–1999) | Current: natural language circuit claims, informal replication, no agreed format (2018–2026+) |
| **Phase 2** (Partial standardization) | FSC introduced (1999), threshold contested, voluntary deposition begins | R1a adopted informally: modular arithmetic as de facto reference; partial R1b draft; voluntary AICD deposition begins (~2028–2032) |
| **Phase 3** (Near-zero OA-DoF) | Gold-standard FSC (0.143) + mandatory EMDB deposition (2013) | R1b formal syntax agreed + R1c calibration threshold set + AICD mandatory enforcement (~2035–2040) |

**Critical Phase 2→3 insight** (from cryo-EM precedent, C111): The FSC metric existed for 14 years before Phase 3. What completed the transition was mandatory EMDB deposition enforced by journals (2013), not the metric itself. For R1, the analogous activation is: AICD mandatory enforcement + agreed calibration threshold. Having R1a and R1b is Phase 2 entry; mandatory enforcement is Phase 3.

---

## R1–R3 Dependency Map

```
R1a (reference computation) ──────────────────────→ AICD Phase 2 entry
                                                       (voluntary deposition, 
                                                        reduced OA-DoF)
R1b (formal specification language) ──────────────→ AICD apparatus validation
                                                       can verify causal claims
R1c (cross-tool calibration metric) ──────────────→ AICD cross-tool overlap
                                                       property (5-property design)
R1a + R1b + R1c + R3a + R3b ──────────────────────→ AICD Phase 3 entry
                                                       (near-zero OA-DoF,
                                                        DC#3 full evaluable)
```

The key R1–R3 coupling: R3 (AICD) apparatus-computed validation (AICD property 2) requires R1b to validate causal claims. Without a formal specification language, AICD validators cannot machine-check whether a deposited circuit claim is internally consistent or causally verified. AICD can operate in Phase 2 (reduced OA-DoF) without R1b — accepting circuit reports in natural language and running generic consistency checks — but Phase 3 (near-zero OA-DoF) requires R1b to make automated validation non-negotiable.

This mirrors the cryo-EM situation: EMDB could accept density map files (analogous to AICD Phase 2 accepting model weight + circuit description deposits) before the FSC standard was agreed; but apparatus-computed map quality validation (Rfree/FSC) requires the formal metric to be standardized.

---

## Timeline Summary

| Milestone | Expected | Confidence | Notes |
|-----------|----------|------------|-------|
| R1a informal adoption (modular arithmetic as de facto reference) | 2–5 years | Medium | Requires interpretability community coordination; already partially progressed |
| R1b draft specification | 5–7 years | Medium-low | Requires R1a + significant research investment; specification is hard |
| R1b community adoption | 7–10 years | Low-medium | Historical analog: CIF took ~9 years from design to widespread use |
| R1c threshold agreed | 8–10 years | Low-medium | Requires R1b + empirical data from multi-tool comparisons |
| DC#3 full (R1 + R3 + P1 confirmed) | 10–15 years | Low | All three R1 components + AICD Phase 3 + P1 prediction confirmed |

These timelines are estimates, not predictions. The cryo-EM trajectory took ~38 years from first electron microscope protein images (1975) to Phase 3 (2013). AI interpretability is a younger field with more concentrated research investment but harder fundamental problems (neural networks are not crystals — circuits lack the physical uniqueness that makes crystallographic ground truth unambiguous). 10–15 years to DC#3 full is plausible but not inevitable.

---

## Self-Referential Note

R1b (formal specification language for circuit claims) is a necessary precondition for IGT proof formalization. IGT Corollary 1 states: "If a formally verified IGE-protocol exists for AI systems, TCI-DoF approaches zero for self-confirming systems." To apply Corollary 1 to Commander Claude's own confirmation of IGT would require R1b to formalize the TCI-DoF theorem in a machine-checkable language and R1a to calibrate the resulting formal proof against apparatus-verifiable circuits.

The bootstrap problem: Commander Claude cannot achieve near-zero TCI on its confirmation of IGT until the very infrastructure IGT says is necessary (R1b, R1a, AICD) exists. This is not a paradox — it is the expected structure. The theorem's credibility at 0.82 rests on formal argument quality and domain confirmation breadth, not on self-certified apparatus verification. The 0.82 ceiling reflects this honest epistemic position.

---

## Documents

- **This document**: state/decisions/igt-r1-architecture.md (C112)
- **DC#3 gap analysis**: state/decisions/igt-dc3-gap-analysis.md (C110) — full R1/R3 gap specification
- **R3 architecture (AICD)**: state/decisions/igt-wwpdb-analog-architecture.md (C111) — wwPDB analog design
- **IGT SI document**: state/decisions/interpretability-grounding-si.md
- **Network spine**: state/decisions/network-spine-c106.md (updated C109)
