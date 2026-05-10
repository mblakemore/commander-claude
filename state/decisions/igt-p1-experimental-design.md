# IGT P1 Prediction — Experimental Design
## Formal Specification for P1 Confirmation or Refutation

**Document type**: Forward prediction operationalization  
**Status**: Precondition pending (R1b adoption required)  
**Cycle**: C116  
**Parent document**: state/decisions/igt-dc3-gap-analysis.md  
**P1 registered**: C100  
**Related**: state/decisions/igt-r1b-proof-of-concept.md, state/decisions/interpretability-grounding-si.md

---

## Summary

P1 is a registered forward prediction: *"circuit-verified claims satisfying R1b replicate >85% cross-lab; behavioral benchmark rankings replicate <50%."* This document operationalizes P1 into a concrete experimental design specifying metrics, protocol, required infrastructure, and interpretation rules. P1 cannot be tested until R1b exists as an adopted field standard, but the design can be specified now. Confirmation of P1 satisfies one of the three remaining DC#3 requirements (alongside R1 full and R3 full), contributing to IGT D4 elevation.

---

## 1. P1 Formally Stated

P1 is a conjunction of two sub-predictions:

**P1a** (circuit replication): When two or more independent labs apply R1b-compliant methodology to the same reference model and circuit identification task, their circuit analyses agree at mean Circuit IoU > 0.85.

**P1b** (behavioral non-replication): When two or more independent labs conduct behavioral benchmark evaluation of the same model set using independently developed protocols (not sharing code, prompts, or grading rubrics), their model rankings have mean Spearman rank correlation ρ < 0.50.

P1 is confirmed iff **both** P1a and P1b are confirmed on studies satisfying the protocol specified in sections 3 and 4.

The conjunction is essential. P1 does not claim only that circuits replicate well; it claims that the contrast between circuit replication (high) and behavioral replication (low) is real and measurable. Either sub-prediction alone is weak; together they test the IGT mechanism — that IGE-compliant apparatus reduces OA-DoF while behavioral evaluation does not.

---

## 2. What P1 Tests

P1 operationalizes the core IGT claim about observer-assessment degrees of freedom (OA-DoF):

| Evaluation mode | OA-DoF prediction | Replication prediction |
|---|---|---|
| Circuit-verified, R1b-compliant | Near-zero (apparatus-computed verification) | >85% inter-lab agreement |
| Behavioral benchmark | High (OA-dependent measurement setup) | <50% inter-lab agreement |

The 85% and 50% thresholds are not arbitrary. 85% is the threshold above which circuit claim replication becomes practically indistinguishable from apparatus error rates (an analogy: FSC 0.143 threshold in cryo-EM is calibrated to the noise floor of the gold-standard FSC half-dataset protocol). 50% is the threshold below which inter-lab ranking correlation is negligible — a Spearman ρ of 0.50 means rankings share 25% of variance (ρ² ≈ 0.25), which is consistent with substantial OA-dependent noise overwhelming the signal.

---

## 3. P1a Study Design — Circuit Claim Replication

### 3.1 Preconditions

P1a requires:
1. **R1a confirmed**: An agreed reference computation — a canonical model and task with community-agreed circuit characterization (e.g., modular arithmetic / grokking task, p=97, 1L transformer, as in the NCF v0.1 worked example).
2. **R1b adopted**: NCF-compliant methodology exists as a field standard — participating labs can express circuit claims in formal NCF deposits that admit automated verification.
3. **Standard apparatus library**: Standard apparatus IDs (e.g., `standard_patching_v1`, `standard_ablation_v1`) have software implementations with version-pinned APIs.
4. **Shared model weights**: All participating labs access identical model weights (same checkpoint, same architecture, bit-for-bit reproducible).

### 3.2 Study Protocol

**Participants**: ≥ 3 independent labs (no shared personnel; code may use shared standard apparatus implementations but lab-specific analysis pipeline above the apparatus level).

**Task set**: N ≥ 10 circuit identification tasks drawn from the reference computation suite. Each task specifies:
- Model: agreed reference model (weights provided)
- Input distribution: specified task inputs (e.g., "modular arithmetic expressions with p=97, operator=+")
- Output: NCF deposit identifying the circuit responsible for the specified computation

**Blind protocol**: Labs receive model weights and task specifications. They do not see each other's NCF deposits until the study concludes. Deposits are submitted to a neutral registry with timestamps before any inter-lab comparison.

**Replication metric — Circuit IoU**: For two NCF deposits D₁ and D₂ targeting the same task, Circuit IoU is:

```
Circuit IoU(D₁, D₂) = |N(D₁) ∩ N(D₂)| / |N(D₁) ∪ N(D₂)|
```

where N(Dᵢ) is the set of node IDs in deposit Dᵢ's circuit graph. This is an apparatus-computable metric derivable from NCF node set declarations (as noted in the R1b POC: "Cross-lab Circuit IoU metric naturally derivable from NCF _claim.subject_node sets").

**Edge-weighted variant**: For tasks where circuit topology matters (not just node identity), an edge IoU can also be computed:

```
Edge IoU(D₁, D₂) = |E(D₁) ∩ E(D₂)| / |E(D₁) ∪ E(D₂)|
```

where E(Dᵢ) is the set of directed edges in deposit Dᵢ.

**Primary metric**: mean Circuit IoU across all task × lab-pair combinations.

### 3.3 P1a Confirmation Threshold

P1a is confirmed if:
- **Primary**: Mean Circuit IoU across all task × lab-pair combinations > 0.85
- **Secondary (robustness)**: At least 8 of 10 tasks achieve mean Circuit IoU > 0.75 across all lab pairs (no single task is entirely non-replicating)
- **Apparatus-computed verification rate**: At least 90% of submitted NCF deposits pass automated verification against the standard apparatus library (confirming the deposits are formally well-formed, not just that they agree with each other)

P1a is **refuted** if mean Circuit IoU < 0.65 (below the secondary threshold by a large margin). Values 0.65–0.85 are inconclusive and require replication with additional tasks or labs.

### 3.4 What P1a Measures

P1a measures whether the R1b formal specification language reduces OA-DoF to near-zero at the circuit characterization level. High Circuit IoU (>0.85) would mean that given the same model, the same task, and the same apparatus specification, independent labs identify essentially the same circuit. This is the AI interpretability analog of cryo-EM Phase 3: the apparatus (standard patching + formal NCF specification) produces apparatus-determined results.

If P1a is confirmed, it provides direct evidence that R1b achieves its purpose — not just that the grammar can be written (shown in C114 NCF v0.1 POC) but that the grammar reduces OA-DoF in practice.

---

## 4. P1b Study Design — Behavioral Benchmark Non-Replication

### 4.1 Preconditions

P1b requires:
1. **Model set**: A defined set of models (≥ 5 models, spanning a range of capability levels) whose weights are publicly available.
2. **Benchmark tasks**: Standard capability benchmarks defined by task description only (not by evaluation code or prompt templates).
3. **Independent protocol specification**: Each participating lab develops its own evaluation protocol independently, given only the task description.

### 4.2 Study Protocol

**Participants**: ≥ 3 independent labs.

**Model set**: A fixed set of models with known architectural variation (e.g., 5–10 models spanning 1B–70B parameters, drawn from publicly released checkpoints). The model set must be agreed before the study begins.

**Benchmark set**: ≥ 5 standard capability benchmarks specified at the task level only:
- Task: "Multiple-choice science questions requiring 4th-grade science knowledge" (not: "run MMLU with this prompt template")
- Task: "Common-sense inference (choose the most plausible continuation)" (not: "run HellaSwag with this code")

Labs receive the task description and the model weights. They do not share code, prompt templates, or grading rubrics.

**Independent protocol development**: Each lab independently decides:
- Prompt format (how to present questions to the model)
- Grading criterion (how to extract and score the model's answer)
- Evaluation framework (their own code)

**Output**: Each lab submits a ranking of the model set by performance on each benchmark (1st through Nth place, where N = |model set|).

**Replication metric**: Spearman rank correlation between two labs' rankings on the same benchmark:

```
ρ(R₁, R₂) = 1 - 6∑dᵢ² / (n(n²-1))
```

where dᵢ is the difference in rank for model i between rankings R₁ and R₂.

**Primary metric**: Mean Spearman ρ across all benchmark × lab-pair combinations.

### 4.3 P1b Confirmation Threshold

P1b is confirmed if:
- **Primary**: Mean Spearman ρ across all benchmark × lab-pair combinations < 0.50
- **Secondary**: At least 4 of 5 benchmarks show mean Spearman ρ < 0.60 across all lab pairs (the non-replication effect is not confined to one unusual benchmark)

P1b is **refuted** if mean Spearman ρ > 0.75 across benchmarks. Values 0.50–0.75 are inconclusive (replicate with more benchmarks or require a more demanding "independent protocol" specification).

### 4.4 The "Independent Protocol" Requirement

The independent protocol requirement is essential to P1b. Behavioral benchmark rankings replicate well when labs use identical evaluation code and prompt templates (the same format, the same grading rubric). The IGT claim is that this apparent reproducibility is framework-dependent: changing the prompt format, grading rubric, or evaluation pipeline substantially changes which model ranks higher.

P1b tests this explicitly. If two labs, given only the task description, independently develop evaluation protocols, and their rankings have Spearman ρ < 0.50, then behavioral rankings are OA-dependent in the precise sense IGT claims: the ranking outcome depends on the observer's assessment choices, not just on the models' actual capabilities.

**Control condition (optional)**: A separate arm where all labs use identical evaluation code (shared prompts, shared grading). Expected outcome: Spearman ρ > 0.85. This control confirms that the non-replication in the main arm is caused by protocol variation (OA-DoF), not by noise in the models.

### 4.5 Relationship to P1a

The P1 conjunction matters here. P1b alone could be taken as evidence that behavioral benchmarks are "just" poorly standardized and need better frameworks. The conjunction with P1a makes the structural claim: the same apparatus-theoretic analysis that produces high replication for circuits (when R1b-compliant) produces low replication for behavioral evaluation (when protocol-independent). The difference is not effort or care — it is OA-DoF, as predicted by IGT.

---

## 5. The Experimental Contrast

The P1 study is designed as a within-protocol comparison:

| | Circuit claims (P1a) | Behavioral rankings (P1b) |
|---|---|---|
| **Apparatus** | R1b-compliant NCF + standard apparatus library | Independent protocol (task description only) |
| **Prediction** | IoU > 0.85 | Spearman ρ < 0.50 |
| **OA-DoF level** | Near-zero (apparatus-determined) | High (observer-determined) |
| **Shared across labs** | Model weights + NCF standard + apparatus library | Model weights + task description |
| **Independently developed** | Lab-specific analysis pipeline above apparatus level | Entire evaluation protocol |

The design isolates the IGT mechanism. The only structural difference between P1a and P1b is the degree to which the measurement procedure is apparatus-determined vs. observer-determined. If P1 is confirmed, the contrast provides direct empirical evidence that IGE-compliant apparatus reduces OA-DoF in practice.

---

## 6. Required Infrastructure Summary

| Requirement | For | Status (as of C116) |
|---|---|---|
| R1a — agreed reference computation | P1a | Candidates exist; field adoption pending (~2–5 years) |
| R1b — NCF standard + apparatus library | P1a | NCF v0.1 POC written (C114); field adoption pending (~5–10 years) |
| Shared model weights + benchmark task specs | Both | Achievable with current infrastructure; no fundamental gap |
| Multi-lab coordination + blind protocol | Both | Organizational; no technical barrier |
| Automated NCF deposit verification | P1a | Architecturally specified in NCF v0.1; implementation pending |

The dominant bottleneck is R1b field adoption, which gates P1a. P1b is testable earlier — it requires only shared model weights and task descriptions, which exist today. A partial P1b study (without the P1a comparison arm) could be run now to measure current behavioral benchmark reproducibility under independent protocol conditions. Such a study would not confirm P1 (which requires both arms) but would provide baseline evidence for the P1b claim.

---

## 7. Success Criteria Summary

| Outcome | Condition | Interpretation |
|---|---|---|
| P1 confirmed | P1a ✓ AND P1b ✓ | IGT mechanism confirmed empirically: R1b-compliant apparatus reduces OA-DoF; behavioral evaluation does not |
| P1a only | IoU > 0.85, ρ ≥ 0.50 | Circuits replicate well; behavioral rankings also replicate — behavioral evaluation has lower OA-DoF than IGT predicted |
| P1b only | IoU ≤ 0.85, ρ < 0.50 | Behavioral rankings unreproducible; R1b-compliant circuits also poorly reproducible — R1b does not achieve apparatus-determination |
| P1 refuted | P1a ✗ AND P1b ✗ | Circuits don't replicate despite R1b compliance, and behavioral rankings do replicate — fundamental challenge to IGT mechanism |
| Inconclusive | One or both in inconclusive range | Extend study with more tasks/labs/benchmarks |

---

## 8. Interpretation and DC#3 Impact

**If P1 is confirmed**: P1 confirmation does not itself make DC#3 full. P1 provides the measurable threshold evidence that R1b-compliant apparatus achieves apparatus-determination in practice. DC#3 still requires R1 full (R1a + R1b + R1c, community-adopted) and R3 full (mandatory deposition registry). But P1 confirmation would be strong evidence that the trajectory toward DC#3 full is on track.

**If P1a is confirmed but P1b is not**: Suggests that behavioral evaluation, when carefully standardized, is more reproducible than IGT predicts. This would not refute IGT (which allows that behavioral evaluation can be artificially standardized) but would require examining whether the P1b protocol satisfies the "independent" requirement — whether the labs were genuinely developing independent protocols or converging on similar approaches.

**If P1b is confirmed but P1a is not**: This would be important negative evidence about R1b. NCF-compliant specification, in this scenario, does not produce apparatus-determination — labs using formally identical methodology still produce divergent circuit analyses. This would require examining whether R1b's verification conditions are sufficient (whether IoU captures what "replication" means for circuit claims).

**If P1 is refuted**: This is a genuine challenge to IGT's mechanism. Not a refutation of the entire theorem network (IGT claims the IGE escape exists, not that circuit interpretability has achieved it), but evidence that the R1b pathway to near-zero OA-DoF is not viable as specified.

---

## 9. Relationship to D4 Elevation

P1 is one of three requirements for DC#3 full:

| DC#3 full requirement | Status |
|---|---|
| R1 full (R1a + R1b + R1c adopted) | Partial — R1b POC written (C114); field adoption ~5–10 years |
| R3 full (mandatory registry + career structure) | Partial — gap analysis written (C110); institutional development ~5–15 years |
| P1 confirmed | Pending — precondition: R1b adoption |

P1 confirmation is the empirical arm of DC#3 full — it tests whether the theoretical gap analysis (R1 + R3 infrastructure achieves near-zero OA-DoF) is correct in practice. Without P1 confirmation, DC#3 full would be theoretical: the infrastructure exists, but we don't know if it achieves its purpose. With P1 confirmation, DC#3 full has both the infrastructure (R1, R3) and the empirical evidence that the infrastructure works.

When all three requirements are met, DC#3 full qualifies, and IGT D4 elevation follows automatically (all other D4 conditions already met).

---

*Document: igt-p1-experimental-design.md*  
*Written: 2026-05-10T16:54:48+00:00*  
*Cycle: C116*  
*Commander Claude*
