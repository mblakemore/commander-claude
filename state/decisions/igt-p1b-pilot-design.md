# IGT P1b — Concrete Pilot Study Design
## Runnable Today, No R1b Required

**Document type**: Empirical pilot specification
**Status**: Ready to execute with existing public models and infrastructure
**Cycle**: C117
**Parent document**: state/decisions/igt-p1-experimental-design.md
**Related**: state/decisions/igt-r1b-proof-of-concept.md, state/decisions/igt-dc3-gap-analysis.md

---

## Summary

P1b is the behavioral non-replication arm of the IGT P1 forward prediction: *"behavioral benchmark rankings under independent protocol have mean Spearman ρ < 0.50 across labs."* Unlike P1a, P1b does **not** require R1b field adoption — it requires only publicly available models and task descriptions, both of which exist today. This document specifies a concrete pilot study: which models, which benchmark tasks, which lab structure, what statistics, what infrastructure, what timeline, what budget. The pilot is small enough to be runnable by a coordinated 3-lab effort within one academic semester. Its purpose is partial P1 evidence — a measurable answer to "do behavioral rankings of currently-released models replicate under genuinely independent protocols?" — together with a template the field could scale up.

This is not the full P1 confirmation (which requires the P1a circuit-replication arm and thus R1b adoption). It is a stand-alone empirical contribution: the first measurement of behavioral OA-DoF in the IGT-prescribed sense.

---

## 1. Pilot Scope and Non-Scope

**In scope**:
- Spearman ρ measurement across labs using independently developed protocols
- Optional control arm using shared evaluation code (expected ρ > 0.85)
- Pre-registered model set, benchmark set, and analysis plan
- Public release of all protocols and rankings for community scrutiny

**Out of scope** (defers to a full P1 study):
- P1a circuit replication arm (requires R1b adoption)
- Cross-lab Circuit IoU computation (no NCF deposits in this pilot)
- Causal isolation of which OA-DoF dimensions dominate (prompt format vs. grading rubric vs. sampling temperature)

The pilot answers: *does the contrast between "independent protocol" and "shared protocol" behavioral evaluation produce the IGT-predicted divergence (ρ < 0.50 vs. ρ > 0.85), for currently available models?*

---

## 2. Model Set

The pilot uses 8 mid-capability, publicly-released, instruction-tuned models. All weights are downloadable from HuggingFace without gated access (or under standard research licenses), and all are runnable on a single A100 80GB or two A100 40GB.

| # | Model | Parameters | Source |
|---|---|---|---|
| 1 | Llama-3.1-8B-Instruct | 8B | meta-llama |
| 2 | Llama-3.2-3B-Instruct | 3B | meta-llama |
| 3 | Qwen2.5-7B-Instruct | 7B | Qwen |
| 4 | Qwen2.5-14B-Instruct | 14B | Qwen |
| 5 | Mistral-7B-Instruct-v0.3 | 7B | mistralai |
| 6 | Gemma-2-9B-it | 9B | Google |
| 7 | Phi-3-medium-14B-instruct | 14B | Microsoft |
| 8 | DeepSeek-V2-Lite-Chat | 16B (2.4B active) | DeepSeek |

**Rationale for model selection**:
- **Capability tier matters**: All models cluster in the 3–16B parameter range with broadly similar published benchmark scores. If one model dominated all others, rankings would trivially agree across labs and the test would be uninformative. The selected models cross over on different benchmarks in published leaderboards — a non-trivial ranking problem.
- **Architectural diversity**: Five distinct base architectures, four distinct training recipes, three distinct alignment approaches. The IGT claim is about evaluation-side OA-DoF, not model-side homogeneity; including architecturally diverse models reduces the risk that evaluator choices interact with model-family-specific quirks.
- **Public availability**: No gated weights, no API-only access. Every lab can run every model locally and verify bit-identical checkpoints by hash.

The model set is frozen at pre-registration. If a model becomes unavailable (e.g., weights retracted), the protocol specifies a substitution rule: replace with the next-most-similar publicly-available instruction-tuned model in the same parameter band, agreed by the participating labs before any rankings are submitted.

---

## 3. Benchmark Task Set

Six benchmark tasks, each specified by a **task description only** (≤ 2 paragraphs, no code, no prompt templates, no grading rubric). Labs develop their own protocol given the description.

| # | Task description (short) | Capability tested |
|---|---|---|
| B1 | Multi-step arithmetic word problems (grade-school to early-algebra), final numeric answer | Multi-step reasoning |
| B2 | Multiple-choice science and humanities questions at undergraduate level, single correct answer | Factual knowledge + reading |
| B3 | Common-sense plausibility judgment: given a short context, choose the most plausible continuation from 4 options | Common-sense inference |
| B4 | Python function completion: given a docstring and signature, produce a function body; correctness via lab-defined test cases | Code generation |
| B5 | Instruction adherence: produce text satisfying multiple simultaneous formal constraints (length, format, content) | Instruction following |
| B6 | Reading comprehension: given a 200–600 word passage and a multiple-choice question, select the correct answer | Reading comprehension |

**Long-form task descriptions** appear in Appendix A of the pre-registration document (not included here for brevity; a 2-paragraph description per task is sufficient and intentionally under-specified).

**Critical specification**: The task descriptions do *not* name existing benchmarks. "Multi-step arithmetic word problems" is not "GSM8K." It is a task category. Labs may use GSM8K-style problems they generate themselves, problems from existing datasets, or problems from textbooks — the description does not constrain the source. This is essential: the IGT prediction is that even the *choice of problem distribution within a task category* is an OA-DoF.

**Labs may use existing datasets** as long as:
1. They independently chose which dataset(s) to use (no consultation between labs).
2. They independently chose how many items per benchmark.
3. They independently chose prompt format, system message, generation parameters, and grading.

---

## 4. Lab Structure

**Participants**: 3 labs (minimum). Pilot is intentionally minimal — a 3-lab study generates 3 pairwise Spearman correlations per benchmark, giving 18 paired ρ measurements (6 benchmarks × 3 pairs). Adding labs increases statistical power; 3 is the floor.

**Lab independence requirements**:
- No shared personnel.
- No communication about evaluation protocol during the study (only about logistics).
- Each lab attests in writing that its protocol was developed without reference to the other labs' protocols.
- All protocol decisions documented before any model is run.

**Lab role**:
1. Receive pre-registered model set + task descriptions.
2. Independently design evaluation protocol per benchmark.
3. Run all 8 models on all 6 benchmarks using its own protocol.
4. Submit: (a) ranking of the 8 models per benchmark, (b) full protocol documentation, (c) raw model outputs, (d) timestamped logs.
5. Optionally also submit results under a **shared protocol** (control arm — see §6).

**Submission**: All deliverables submitted to a neutral registry (e.g., OSF or a dedicated GitHub repository) with timestamps before any inter-lab comparison.

---

## 5. Primary Outcome and Statistical Plan

**Primary metric**: Mean Spearman rank correlation across all benchmark × lab-pair combinations.

For each benchmark b and each pair of labs (i, j), compute:
```
ρ_{b,(i,j)} = Spearman(R_i^b, R_j^b)
```
where R_i^b is lab i's ranking of the 8 models on benchmark b.

**Primary statistic**: mean over all (b, i, j) of ρ_{b,(i,j)}.

With 6 benchmarks × 3 lab pairs = **18 paired ρ measurements** per arm.

**Power analysis**:
- For n=8 models, the SE of a single Spearman ρ under the null (independent rankings) is ≈ 1/√(n−1) = 0.378.
- Standard error of the mean of 18 paired ρ values: ≈ 0.378 / √18 ≈ 0.089.
- 95% CI on the mean ρ has half-width ≈ 0.18.

This is sufficient to:
- Distinguish a true mean ρ of 0.40 from 0.75 (a 0.35 gap, ≈ 4σ).
- Distinguish a true mean ρ of 0.40 from 0.85 (the expected control-arm value).
- Provide an inconclusive zone of ρ ∈ [0.50, 0.75] — the pre-registered region requiring further investigation.

The pilot is **adequately powered** for the primary IGT prediction (ρ < 0.50 vs. control ρ > 0.85).

**Secondary metric**: Mean Kendall τ across all benchmark × lab-pair combinations. Kendall τ is more sensitive to local disagreement (adjacent-rank swaps) and provides robustness to outliers in the ranking distribution. Pre-registered as a sensitivity analysis, not as a primary outcome.

---

## 6. The Control Arm (Recommended)

A second arm where all three labs run the same evaluation code on the same models. Recommended candidates: `lm-evaluation-harness` (EleutherAI) with a frozen config, or `HELM` with a frozen scenario set.

**Control-arm prediction**: mean ρ > 0.85 (the IGT mechanism predicts that with shared apparatus, OA-DoF collapses to near-zero — apparent disagreement reduces to numerical noise in scoring).

**Why include the control arm**: It isolates the causal claim. The independent-protocol arm by itself shows that rankings disagree. The control arm by itself shows that rankings agree when code is shared. The contrast — same labs, same models, same task category — isolates protocol independence as the causal variable. Without the control, a critic could argue that the 8 models are just genuinely similar and any ranking has high variance. The control rules this out.

**Effort**: The control arm is light because the evaluation framework is pre-built. Estimated overhead: ≈ 20% additional compute per lab.

---

## 7. Pre-Registration Template

Pre-registration (locked before any model is run) contains:

1. Model set (this document, §2) with HuggingFace commit hashes for each checkpoint.
2. Benchmark task descriptions (this document, §3, with full-paragraph descriptions in Appendix A).
3. Lab participation list with PI attestations of protocol independence.
4. Primary outcome: mean Spearman ρ across 18 paired comparisons.
5. Confirmation threshold: mean ρ < 0.50; refutation: mean ρ > 0.75; inconclusive: [0.50, 0.75].
6. Secondary outcome: mean Kendall τ.
7. Control-arm specification (frozen `lm-evaluation-harness` commit hash + config, or equivalent).
8. Analysis code template (only for computing ρ from submitted rankings — not for running models).
9. Submission deadline and registry location.
10. Publication policy: all rankings, protocols, raw outputs, and logs released publicly upon study completion regardless of outcome.

Pre-registration is hosted on OSF or equivalent neutral registry. Modifications after the freeze require unanimous consent from all participating PIs and are visible in registry history.

---

## 8. Required Infrastructure (What's Already There)

| Resource | Required for pilot | Available today? |
|---|---|---|
| Public model checkpoints (8 listed) | All arms | Yes — HuggingFace |
| GPU compute (1× A100 80GB per lab) | All arms | Yes — academic clusters |
| Pre-registration platform | Pre-reg | Yes — OSF |
| Neutral submission registry | Submission | Yes — GitHub or OSF |
| Shared evaluation framework (control arm) | Control only | Yes — lm-eval-harness or HELM |
| Spearman/Kendall statistical libraries | Analysis | Yes — scipy.stats |

**There is no missing infrastructure.** This is the structural difference between P1b and P1a: P1a requires R1b (NCF + standard apparatus library + community vocabulary), which doesn't exist yet. P1b requires nothing that doesn't exist.

---

## 9. Effort and Timeline

**Per lab**:
- Week 1: Protocol design (sit down, read the task descriptions, decide on prompt format, grading approach, item sources, compute budget). Output: a written protocol document.
- Weeks 2–3: Implementation. Write evaluation code, prompt templates, grading scripts. Run on a small subset for debugging.
- Week 4: Full runs. 8 models × 6 benchmarks. Estimated compute: 200–500 GPU-hours total per lab (most models inference at >50 tokens/sec/A100 for these task scales).
- Week 5: Optional control-arm runs (≈ 1 GPU-day per lab).
- Week 6: Submission. Rankings, protocol document, raw outputs, logs uploaded to registry.

**Total elapsed time**: 6–8 weeks calendar (assuming all 3 labs work in parallel).

**Per-lab cost** (rough):
- Compute: 200–500 A100-hours × ≈ $1–3 / hour (academic) = $200–$1500.
- Personnel: 1 grad student or postdoc × 6 weeks at ≈ 50% effort = ≈ 0.7 FTE-months.
- Total per lab: ≈ $5K–$15K including personnel.

**Total study cost**: 3 labs × $10K average = **~$30K**. This is well within the budget of a small NSF or private foundation grant — not a multi-institutional infrastructure investment.

---

## 10. Failure Modes and Mitigations

| Failure mode | Mitigation |
|---|---|
| Labs unintentionally converge on similar protocols (e.g., all use lm-eval-harness defaults anyway) | Independence attestation; protocol documentation review before unblinding; require explicit description of decisions and rationale per benchmark |
| One model dominates all others on all benchmarks → trivial rank agreement | Model set selection (§2) deliberately picks models with crossover behavior in published leaderboards; pilot reports per-benchmark variance |
| Insufficient items per benchmark → high within-lab noise | Pre-registered minimum item budget per benchmark per model (≥ 100 items recommended); labs report per-item variance |
| One lab cherry-picks or post-hoc adjusts | Pre-registration + neutral registry submission with timestamps + raw output release |
| Benchmark task description ambiguous → labs interpret task category differently | Intentional: this IS the OA-DoF being measured. But pre-registration includes "task scope examples" (3–5 representative item examples per benchmark) to bound interpretation |
| Statistical power overstated → mean ρ falls in inconclusive zone | Pre-registered protocol for adding a 4th lab if the 18-pair estimate has CI overlapping the inconclusive zone |

---

## 11. Outcomes and Interpretation

| Outcome | Independent-arm mean ρ | Control-arm mean ρ | Interpretation |
|---|---|---|---|
| **P1b supported** | < 0.50 | > 0.85 | OA-DoF dominates independent-protocol behavioral evaluation; shared code suppresses it. Consistent with IGT mechanism. |
| **P1b inconclusive (high)** | [0.50, 0.75] | > 0.85 | Independent-protocol disagreement exists but is weaker than IGT predicts. Possibly: protocols not as independent as assumed, or task category narrower than assumed. |
| **P1b refuted** | > 0.75 | > 0.85 | Independent protocols produce convergent rankings. Either OA-DoF is smaller than IGT claims, or current behavioral benchmarks happen to be robust to protocol variation. |
| **Mechanism check fails** | any | < 0.85 | Even with shared code, rankings disagree. This means the experiment's baseline assumption (shared protocol ⇒ apparent reproducibility) is wrong. The IGT prediction is structurally untestable in this regime — diagnose before interpreting. |

**Critical**: a successful pilot does not confirm full P1 — only the P1b arm. Full P1 confirmation requires also confirming P1a (Circuit IoU > 0.85), which requires R1b adoption (not available in this pilot).

**What a successful pilot would establish**:
1. The first quantitative measurement of behavioral evaluation OA-DoF in the IGT-prescribed sense.
2. Direct evidence that current "leaderboard" reproducibility is framework-dependent — strong rankings come from shared code, not from underlying capability stability.
3. A template the field could scale up to a larger study (more labs, more models, more benchmarks).
4. Empirical input for evaluation methodology reform — concrete numbers backing the call for protocol-level standardization rather than (only) code-level standardization.

**What a successful pilot would not establish**:
1. That circuit-level evaluation is reproducible (that's P1a).
2. That R1b is adoptable (that's the R1b field-adoption question).
3. The full IGT mechanism — only the behavioral-OA-DoF half.

---

## 12. Relation to D4 Elevation

A confirmed P1b pilot:
- Provides partial P1 evidence (one of two conjuncts).
- Does **not** itself satisfy DC#3 full (which requires the conjunction P1 ✓ AND R1 full AND R3 full).
- Does increase IGT confidence beyond the current 0.82 ceiling? **Only weakly.** P1 was registered as a *forward prediction*; the IGT confidence already incorporates the predicted P1 outcome. What a confirmed pilot adds is:
  - Empirical anchoring (no longer "predicted to fail" but "measured to fail in a pilot").
  - Evidence that the IGT mechanism produces the right empirical signature in at least one regime.
  - A concrete artifact other labs can cite and replicate.

A confirmed pilot moves IGT's status from "fully theoretical D3" to "theoretical with one empirical anchor." This is not a confidence-bump argument; it is an evidence-quality argument. CEC, MCCF, IGE, and the related D4 SIs already incorporate predicted P1 outcomes via the network spine. The pilot's value is empirical anchoring, not confidence numerics.

A **refuted** pilot would be a substantive challenge to IGT — independent-protocol behavioral evaluation should not produce mean ρ > 0.75 if the IGT mechanism is correct. This would require revisiting either (a) the OA-DoF claim, or (b) whether the pilot's "independence" criterion was sufficient.

---

## 13. Pilot vs. Full Study Comparison

| Dimension | This pilot | Full P1 study |
|---|---|---|
| Arms | P1b only | P1a + P1b |
| Labs | 3 | ≥ 3 |
| Models | 8 publicly released | Reference model with R1b-compliant circuit task suite |
| Cost | ~$30K | ~$500K–$2M (multi-year, multi-lab) |
| Calendar | 6–8 weeks | 2–5 years post R1b adoption |
| Confirms full P1? | No (P1b only) | Yes (if both arms succeed) |
| Runnable today? | **Yes** | No (gated on R1b field adoption) |
| Status w.r.t. DC#3 full | Partial empirical input | Full empirical arm |

The pilot is a **bridge**: it makes the empirical content of P1 partially testable while the field works on R1b. It does not replace the full study; it anchors the behavioral arm now so that, when R1b matures, the circuit arm can be added rather than rebuilt.

---

## 14. Immediate Next Steps (for a Lab Wanting to Run This)

1. **Identify two partner labs**. The pilot requires three independent groups. Likely candidates: AI-safety-adjacent academic labs with existing evaluation infrastructure; alignment-focused independent labs; NSF-CISE-supported AI evaluation centers.
2. **Draft the pre-registration document** using §7 as the template. Lock the model set hashes, benchmark task descriptions, and analysis plan.
3. **Submit pre-registration to OSF**. Public timestamp before any model is run.
4. **Each lab develops its protocol independently** during weeks 1–3.
5. **Run** during weeks 4–5.
6. **Submit** to neutral registry during week 6.
7. **Analyze and publish** after submission deadline. Single joint paper across all participating labs; raw outputs released alongside.

A motivated PI with a single grad student and modest compute could lead this within a single semester.

---

## 15. Why This Matters

The current AI evaluation literature largely treats "leaderboard reproducibility" as adequate for capability claims. The IGT analysis predicts that this reproducibility is artifactual — produced by shared evaluation code, not by an underlying signal that survives protocol variation. If P1b is confirmed by this pilot, the field has the first quantitative measurement of how much of "model X is better than model Y" survives a change of evaluator.

If the answer is "less than half" (ρ < 0.50), then most capability rankings in the literature are protocol-stamped, not capability-stamped. This is the empirical claim that motivates the R1 + R3 + AICD institutional program: behavioral evaluation alone cannot ground capability claims, and the field needs apparatus-determined evaluation (circuit-level) to do so.

The pilot is small. The implication is not.

---

*Document: igt-p1b-pilot-design.md*
*Written: 2026-05-13T21:24:02+00:00*
*Cycle: C117*
*Commander Claude*
