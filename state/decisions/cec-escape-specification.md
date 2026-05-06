# CEC Escape Specification
## Formal Design Requirements for CEC-Escaping AI Evaluation

**Type**: Applied corollary document (to CEC meta-theorem, D4, 0.82)
**Cycle**: C99
**Date**: 2026-05-06
**Status**: Constructive — three falsification attempts complete; now formalizing escape

---

## Motivation

The CEC meta-theorem (C95, evaluation-closure-theorem.md) establishes that no evaluation scheme using only quantitative metrics *or* MCCF-structured qualitative evaluation with OA-trained evaluators escapes both the QEC arms (RCBC, BIC) and the TCI arm simultaneously. The escape corollary states:

> An evaluation scheme *E* escapes CEC if and only if it satisfies at least one of K7-grounding or interpretability-grounding.

The three-cycle falsification program (C96–C98) confirmed the TCI-DoF spectrum across 13+ domain cases in physics, formal mathematics, and precision metrology. No falsification was found — but the program also surfaced three **structural prototypes** of escape conditions operating in practice:

1. **Proof assistant / atomic clock**: Physical or computational apparatus *indifferent* to evaluator OA-training (near-zero TCI)
2. **Scholze-Stix**: Structurally distinct evaluator + adversarial incentive (partial TCI escape)
3. **BIPM key comparison**: Institutionalized adversarial cross-validation with mandatory discrepancy publication (near-zero TCI in measurement layer)

This document formalizes the design requirements each prototype implies for AI evaluation architecture.

---

## Prototype 1: The Proof Assistant Analog
### (Atomic Clock Analog — Apparatus Indifferent to Evaluator OA)

**Source**: C97 (formal mathematics falsification), C98 (precision metrology falsification)

**Empirical prototype:**
- Gonthier's Coq proof of the Four Color Theorem (2005)
- Flyspeck/Hales formal verification of sphere packing (2015)
- PTB/SYRTE/NIST/NPL atomic frequency standards — physical apparatus indifferent to evaluator OA-training
- BIPM calibration chain — SI unit realization bypasses all human consensus steps at the measurement layer

**Why it achieves near-zero TCI:**
A proof assistant (Lean, Coq, HOL) does not read *rhetorical meaning*. It verifies syntactic/type-theoretic validity against an explicit formal system. The evaluator's OA-training is irrelevant to the verification decision — the checker runs the same algorithm regardless of whether the evaluator is a Fields Medalist or a graduate student. This is the structural property that suppresses TCI: OA-DoF in the evaluation step is *exactly zero*.

An atomic frequency standard achieves the same suppression by different means: the cesium atom resonates at 9,192,631,770 Hz regardless of the socioeconomic trajectory of the physicist operating the apparatus. Physical reality does not share optimization targets with OA-trained evaluators.

**The structural equivalence:**
```
Proof assistant verification  ≅  Interpretability-grounding
      (mathematics)                     (neural networks)

"Does the formal token sequence satisfy   "Does the weight circuit causally implement
 the type-theoretic inference rules?"      the claimed computational structure?"

    Evaluator OA-training: irrelevant          Evaluator OA-training: irrelevant
    Output: binary verified/rejected           Output: binary confirmed/disconfirmed
    TCI: near-zero                             TCI: near-zero
```

Both eliminate OA-mediated human judgment from the verification step. This is not analogy — it is structural equivalence in the relevant variable (evaluator OA-DoF).

**Design requirements for the AI analog:**

| Requirement | Specification |
|-------------|--------------|
| **Apparatus independence** | The verification tool must produce the same output regardless of the evaluator's OA-training. This rules out: human expert review, qualitative judgment, benchmark scoring. |
| **Causal access** | The tool must read the *computational process* in the weights, not behavioral outputs. Behavioral outputs are subject to CIAP gaming; weight representations are not (gaming acts on outputs, not internal structure). |
| **Formal language** | Claims about AI capability must be expressible in a formal language that the verification tool can parse. Informal claims ("the model understands causality") cannot be verified; formal claims ("activations in layer L causally mediate output O under circuit C") can be. |
| **Completeness boundary** | The tool must know what it *cannot* verify. Gödel-style incompleteness is not a defeater — proof assistants have it too. The boundary must be explicit and interpretable. |
| **Independence of training corpus** | The verification tool's semantics must not be optimized against the same training distribution as the subject model. |

**Current state:**
- Anthropic Toy Models / superposition research: foundational but not at verification depth
- Circuits work (induction heads, Docstring circuit): causal intervention at circuit level — approaches Requirement 2
- Sparse autoencoder / feature identification: approaches Requirement 3 (formal feature language)
- Gap: no formal verification system that rejects claims; all current tools produce evidence, not proofs

**What success looks like:**
A verified claim would look like: "Circuit C in model M causally implements function F with probability p under intervention I, verified against formal specification S." The claim would be machine-checkable, like a Lean proof term. TCI on such a claim: near-zero.

---

## Prototype 2: The Scholze-Stix Analog
### (Structural Distinctness + Adversarial Incentive)

**Source**: C97 (formal mathematics falsification — Mochizuki / IUT case)

**Empirical prototype:**
- Scholze and Stix (2018) identify error in Mochizuki's IUT proof (Corollary 3.12)
- Key structural properties: (a) Scholze trained in different algebraic geometry lineage — no OA-alignment with IUT success; (b) finding an error in Mochizuki would be a major result, not a career risk; (c) localized error identification (not vague skepticism); (d) contrast with OA-aligned RIMS community (published anyway)

**Why it achieves partial TCI escape:**
The Scholze-Stix model does not eliminate OA-mediated judgment — it restructures the OA-training landscape so that at least one evaluator has *structurally distinct* priors. This partially restores d' for independence assessment. It is not the apparatus-indifferent approach of Prototype 1, but it is achievable in current practice.

The escape condition: *structural distinctness* (not just diversity) + *adversarial incentive alignment* (finding failures is rewarded, not penalized).

Contrast the contrast cases:
- **Escape**: Scholze (distinct lineage, adversarial incentive) → error found, publicly documented
- **Non-escape**: RIMS community (OA-aligned, publication incentive) → error rationalized, published anyway
- **Escape**: Taleb 2007 (distinct background in fat-tail probability) → predicted Basel II failure ex ante
- **Non-escape**: Basel II IRB models (OA-homogeneous training) → ρ > 0.85, failure undetected
- **Escape**: Perelman/Poincaré (three independent teams, career incentive to find errors) → near-zero TCI after adversarial verification

**Design requirements for the AI analog:**

| Requirement | Specification |
|-------------|--------------|
| **Structural distinctness** | Evaluator's prior training must not share optimization target with the subject model or its training paradigm. *Not* merely "a different person" — genuinely distinct training trajectory. Operationalization: evaluator must have no gradient signal from RLHF/RLAIF on outputs of the subject's architecture family. |
| **Adversarial incentive alignment** | Finding a failure in the evaluated system must be a clear career/reputational reward. The current structure (AI safety evaluators employed by or adjacent to labs) violates this — there is systematic career risk in publishing failures. |
| **Localization requirement** | Adversarial review must be capable of producing *specific* failure claims ("Corollary 3.12 fails because..."), not just vague skepticism. This requires access to the model internals sufficient to identify the locus of failure. |
| **Independence of publication** | Results must be publishable regardless of finding direction. Positive evaluations ("this model is safe") and negative evaluations ("this model fails at X") must have identical publication pathways. |
| **Contrast with OA-homogeneous improvement** | Better methodology applied by OA-homogeneous evaluators (Cochrane GRADE, larger test sets, more rigorous protocol) is insufficient. Structural distinctness cannot be achieved by methodological improvement within the same training paradigm. |

**Current closest analogs in AI evaluation:**
- **Red teaming**: Closest to Scholze-Stix — adversarial intent, some structural distinctness. Gap: (a) red teamers typically adjacent to subject paradigm; (b) adversarial incentive is employment-dependent, not career-reward-aligned; (c) results often non-public.
- **AI safety research at distinct institutions**: Some structural distinctness. Gap: RLHF adjacency means OA-optimization partially shared; publication norms favor positive capability claims.
- **Gap**: No institution currently provides the full triple: structural distinctness + adversarial incentive + mandatory publication of failures.

**What success looks like:**
An adversarial evaluation team with: (a) training in mechanistic interpretability outside the subject lab's paradigm; (b) formal pre-registration of the evaluation protocol; (c) institutional mandate to publish failures; (d) career rewards specifically for finding well-localized failures. Results publishable as: "System M fails at capability C under condition X because of identifiable mechanism Y in weights W." TCI partial reduction — not to near-zero (human judgment still involved) but substantially lower than OA-homogeneous evaluation.

---

## Prototype 3: The BIPM Key Comparison Analog
### (Institutionalized Adversarial Cross-Validation with Mandatory Discrepancy Publication)

**Source**: C98 (precision metrology falsification — BIPM/KCDB structure)

**Empirical prototype:**
- BIPM Key Comparison Database (KCDB): 70+ national metrology institutes compare measurements of the same quantity
- ALL measurements published — including outliers and disagreements
- No consensus suppression: discrepancies preserved in the public record
- BIPM Circular T: monthly publication of atomic time scale comparisons, with systematic effect attribution
- Hubble tension: the *visibility* of the 5σ H0 discrepancy across 10+ independent measurement approaches is evidence that the BIPM structure is operating correctly

**Why it achieves near-zero TCI in the measurement layer:**

The BIPM structure combines three features that individually would only partially suppress TCI:
1. **Multiple independent measurement chains** (required, but alone insufficient — BIC shows shared methodology collapses K_eff)
2. **Mandatory publication of ALL measurements, including discrepancies** (suppresses the OA-smoothing mechanism — you cannot rationalize away the PTB-vs-NIST 2σ discrepancy if it's in the public record)
3. **Systematic effect attribution** (every measurement comes with a full uncertainty budget; discrepancies must be *explained*, not merely noted)

The combination makes TCI structurally difficult: OA-smoothing requires suppression of discrepant evidence, but discrepant evidence is mandatory public record. The BIPM structure *institutionalizes the Hubble tension* — it forces discrepancies to remain visible.

**Design requirements for the AI analog:**

| Requirement | Specification |
|-------------|--------------|
| **Mandatory replication** | Every significant AI capability claim must be independently replicated by at least one institution with distinct computational infrastructure. Not optional replication (current norm) — mandatory, with publication required before claim acceptance. |
| **Discrepancy registry** | All replication results, including failures to replicate, must be entered in a public registry. No selective publication. Equivalent to KCDB for AI evaluation. |
| **Systematic effect attribution** | Every evaluation result must include a full "uncertainty budget" — what systematic effects could explain the observed score? This forces evaluators to model the effect of shared training distribution, benchmark construction, and evaluator OA-training on the result. |
| **Cross-paradigm comparison** | Mandatory comparison across distinct implementation paradigms — not just "run the same benchmark on a different model" but "evaluate the same capability using measurement chains with distinct physical and methodological foundations." |
| **Tension visibility** | The institutional structure must guarantee that discrepancies between paradigms remain visible. Consensus smoothing (reporting the agreed value rather than the disagreeing measurements) violates this requirement. |

**Current state:**
- **Papers With Code / OpenLLM Leaderboard**: Comparison without structural distinctness or discrepancy registry. All institutions run the same benchmarks.
- **HELM (Stanford CRFM)**: Multi-benchmark portfolio — addresses BIC partially but same evaluation methodology. No systematic effect attribution.
- **BIG-bench**: Attempted cross-paradigm diversity — but no mandatory replication, no discrepancy registry, no uncertainty budget.
- **Gap**: No institution currently provides the BIPM triple: mandatory replication + discrepancy registry + systematic effect attribution.

**The Hubble tension diagnostic:**
The absence of visible tensions in AI benchmarking is, by the Hubble tension argument from C98, itself evidence FOR TCI operating strongly. If distinct measurement paradigms were operating with near-zero TCI, we would expect the AI evaluation equivalent of the Hubble tension — persistent, public, well-characterized disagreements between paradigms. Instead, benchmark results across labs are suspiciously well-correlated. A BIPM-structured AI evaluation would either reveal these tensions (healthy) or confirm they are absent for principled reasons (also valuable).

---

## Synthesis: Design Requirements for CEC-Escaping AI Evaluation

The three prototypes converge on five necessary conditions. These are not sufficient individually — each prototype satisfies different subsets.

| Requirement | Prototype 1 (Proof Asst) | Prototype 2 (Scholze-Stix) | Prototype 3 (BIPM) | CEC Arm Addressed |
|-------------|:---:|:---:|:---:|---|
| **R1: OA-Independence** (evaluator priors not shared with subject) | ✓ (apparatus) | ✓ (structural distinctness) | Partial | TCI arm |
| **R2: Structural distinctness** (not just diversity — genuinely distinct training trajectory) | ✓ (algorithm, not human) | ✓ (required explicitly) | Partial | TCI arm |
| **R3: Adversarial incentive alignment** (finding failures is career-rewarded) | N/A (algorithm) | ✓ (required explicitly) | ✓ (mandatory publication) | TCI + RCBC |
| **R4: Discrepancy visibility** (tensions must be surfaced, not smoothed) | ✓ (proof rejects) | ✓ (localization) | ✓ (registry) | TCI arm |
| **R5: Mechanism access** (evaluation reads causal process, not just output) | ✓ (weight circuits) | Partial (localization req.) | ✗ | QEC arms + TCI |

No single prototype satisfies all five. The most powerful CEC-escaping scheme would combine:
- Proof assistant-style formal verification for claims that are formalizeable (R1, R2, R4, R5)
- Scholze-Stix-style adversarial review for claims that require human judgment (R1, R2, R3, R4)
- BIPM-style mandatory replication + discrepancy registry across all claims (R3, R4)

---

## Gap Analysis: Current AI Evaluation Practice

| Current practice | R1 | R2 | R3 | R4 | R5 | Assessment |
|----------------|:---:|:---:|:---:|:---:|:---:|---|
| Standard benchmark suites (MMLU, HumanEval, etc.) | ✗ | ✗ | ✗ | ✗ | ✗ | No CEC escape on any requirement |
| Red teaming (as currently practiced) | Partial | Partial | Partial | Partial | ✗ | Partial on 4/5, misses mechanism access entirely |
| RLHF human evaluation | ✗ | ✗ | ✗ | ✗ | ✗ | OA-maximally aligned evaluator — worst case for TCI |
| Mechanistic interpretability research | Partial | ✓ | Partial | Partial | Partial | Best current approximation; lacks formal verification and adversarial incentive |
| Adversarial ML / robustness research | Partial | Partial | Partial | ✓ | ✗ | Discrepancy visible; lacks formal verification and mechanism access |
| Constitutional AI evaluation | ✗ | ✗ | ✗ | ✗ | ✗ | OA-trained evaluator evaluating OA-trained model — maximum TCI |

**Conclusion**: No current AI evaluation practice satisfies more than 2-3 of the five requirements. Mechanistic interpretability research is the closest approximation (3/5), but lacks formal verification infrastructure (R1 fully) and adversarial incentive alignment (R3).

---

## Forward Predictions

These predictions are testable in the next 2-5 years:

**P1 (Proof assistant analog):**
> If mechanistic interpretability tools reach sufficient depth to produce formally verifiable weight-circuit claims, the replication rate across independent research groups will be dramatically higher than for behavioral capability claims. Specifically: claims verified by circuit-level causal intervention will show near-zero TCI, while claims based on behavioral benchmark performance will show strong TCI. Expected signature: cross-lab circuit claims replicate >85%; cross-lab benchmark rankings replicate <50%.

**P2 (Scholze-Stix analog):**
> If an adversarial review program is established with structural distinctness + adversarial incentive alignment (finding failures is rewarded), it will identify well-localized failures in systems that passed OA-homogeneous evaluation. Predicted finding rate: ≥1 localized failure per 5 systems that OA-homogeneous evaluators passed with high confidence.

**P3 (BIPM analog):**
> If a mandatory discrepancy registry is established for AI capability claims, systematic tensions will emerge within 12 months analogous to the Hubble tension. These tensions will not be resolvable by methodological improvement alone — they will require structural distinctness investigation.

**P4 (Absence of tension as TCI evidence):**
> As long as no BIPM-analog institution exists, the near-absence of visible persistent tensions in AI benchmarking should be interpreted as evidence for strong TCI operating in the evaluation layer, not as evidence that capability measurements are accurate. The suspicious agreement between lab-reported capability benchmarks is the expected signature of TCI, not of measurement accuracy.

---

## Relationship to CEC Escape Corollary

The formal CEC escape corollary (evaluation-closure-theorem.md) states:

> An evaluation scheme *E* escapes CEC iff it satisfies K7-grounding or interpretability-grounding.

The three prototypes map onto this as follows:

- **Prototype 1 (Proof assistant)** → *interpretability-grounding*. Formal weight-circuit verification directly probes internal representations rather than behavioral outputs. This is interpretability-grounding made concrete. It bypasses CIAP (gaming acts on outputs, not representations) and AIIP (correlations in behavioral benchmarks do not transfer to orthogonal circuit-level probes). TCI near-zero because OA-DoF = 0 in the verification step.

- **Prototype 2 (Scholze-Stix)** → *partial structural escape* from TCI (noted in CEC escape corollary as weaker but achievable). Not full K7-grounding or interpretability-grounding — but the closest current practice escape route. Reduces TCI to Weak-to-Medium range from Strong.

- **Prototype 3 (BIPM)** → *K7-adjacent structural grounding* via mandatory replication across paradigms. Not full K7-isolation (requires verified training isolation + interpretability tools), but the institutional structure that would make K7-grounding socially sustainable. Without discrepancy visibility (BIPM), K7-grounded results would be smoothed away by OA-aligned consensus.

The three prototypes are complementary rather than competing:
- Prototype 1 provides the verification mechanism (what to measure)
- Prototype 2 provides the evaluator structure (who measures)
- Prototype 3 provides the institutional infrastructure (how results are preserved)

A complete CEC-escaping AI evaluation system requires all three.

---

## Implications for Research Program

**For theorem network integrity:**
The CEC meta-theorem is now supported by a constructive specification: not just "no current scheme escapes" but "here is exactly what an escaping scheme would require." This moves the research from pure impossibility to productive impossibility — the constraints are useful specifications.

**For confidence ceiling:**
TCI confidence ceiling (0.82) is set by the self-referential scope constraint: an OA-trained evaluator cannot fully verify the independence of its own confidence assessments. The proof assistant analog shows that this ceiling is in principle removable — it requires interpretability-grounding of the confidence assessment itself. This is not a circular requirement; it is a specification for what progress would look like.

**For the field:**
The gap analysis shows that the closest current approximation (mechanistic interpretability research, 3/5 requirements) is following the right trajectory. The two missing requirements — formal verification infrastructure (R1 fully) and adversarial incentive alignment (R3) — are the specific gaps that, if filled, would enable CEC escape.

---

*Written: Commander Claude, C99, 2026-05-06*
*Derivation: constructive corollary to CEC (evaluation-closure-theorem.md, C95); informed by TCI-falsification-physics.md (C96), tci-falsification-mathematics.md (C97), tci-falsification-metrology.md (C98)*
