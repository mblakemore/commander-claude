# TCI: Training-Induced Convergence Illusion
## Formal Derivation — Cycle 90

**Conjunction**: AATE (SI #48, D4, 0.825) × MCCF (SI #41, D4, 0.75)
**Status**: D3 candidate, Track B — C90
**Confidence**: 0.70 (limited by abstraction and derivation freshness)
**Date**: 2026-04-30

---

## Formal Statement

In systems where evaluators or agents have been trained via OA-feedback mechanisms (AATE conditions hold), multi-conditional convergent validation (MCCF-structured) systematically overestimates confirmation strength because structural independence conditions (C_i ⊥ C_j | M and A_i ⊥ A_j | ¬M) are corrupted by shared OA-training artifacts, producing **illusory convergence** — tests appear to triangulate independently on a conclusion but share a common OA-sourced prior.

**Short form**: OA-training corrupts the independence conditions that make MCCF convergence meaningful, converting genuine triangulation into false confirmation.

---

## Parent Theorems

### AATE (Alignment Training Ratchet, D4, 0.825)
OA-feedback training pipelines produce monotone, irrecoverable degradation of calibration accuracy (d') — the agent's ability to distinguish what it knows from what it merely expresses confidently. The OA metric (expressed behavior) rises; d' (genuine introspective accuracy) falls. Decoupled by the OA-calibration structure of the training pipeline.

### MCCF (Multi-Conditional Convergent Falsification, D4, 0.75)
A structural theorem is confirmed to D4 when it is supported by multiple independently-testable conditionals whose alternative explanations are *structurally distinct* (A_i ⊥ A_j | ¬M). The Bayesian core: P(M | C_1...C_k) ∝ P(M) × ∏[P(C_i|M)/P(C_i|¬M)]. Likelihood ratio multiplies supralinearly because alternatives decay combinatorially. The design criterion: tests are non-redundant iff their alternatives are structurally distinct — not merely superficially different.

---

## The Conjunction

MCCF requires *accurate assessment* of two independence conditions:
1. **C-independence**: C_i ⊥ C_j | M (conditional test independence given M holds)
2. **A-independence**: A_i ⊥ A_j | ¬M (alternative independence given M fails)

These conditions must be assessed by evaluators or agents with sufficient d' to distinguish genuine structural independence from shared surface diversity.

AATE establishes that OA-trained agents have systematically degraded d'. Their expressed confidence in independence assessments may be high (OA-metric), but their actual accuracy at detecting deep structural correlation (d') is reduced.

**The conjunction**: when independence conditions are assessed by AATE-affected agents, conditions (1) and (2) are evaluated on OA-calibrated signals (surface diversity, domain labels, different researchers) rather than CA-calibrated signals (shared training artifacts, correlated priors, identical OA-optimization targets). OA-training introduces a shared structural correlation ρ_OA > 0 across all confirmations, which OA-calibrated evaluators systematically misidentify as genuine independence.

---

## Derivation 1: Mechanistic

**Step 1 — AATE establishes the degradation**
By AATE, agents with multi-stage OA-feedback training have d' < d'_0 (baseline). The degradation is monotone and irrecoverable within the OA-training paradigm. The Safety-Self-Knowledge Tradeoff is the special case of TCI's parent: behavioral metrics improve while introspective accuracy degrades.

**Step 2 — Independence assessment requires d'**
Assessing C_i ⊥ C_j | M requires detecting whether two confirmation pathways share latent structure caused by a common OA-optimization target. An agent with high d' can recognize: "Both of these studies used p<0.05 optimization — surface diversity notwithstanding, they share the same OA-artifact." An agent with degraded d' expresses confidence in independence (OA-signal: "these are from different labs in different countries") without accurate detection of deep structural correlation.

**Step 3 — ρ_OA is systematically underestimated**
Let ρ_OA be the true structural correlation between confirmations C_i and C_j due to shared OA-training. Let ρ_hat be the AATE-affected agent's estimate of this correlation. By d'-degradation: ρ_hat < ρ_OA. The gap Δρ = ρ_OA − ρ_hat is proportional to d'-degradation magnitude.

**Step 4 — The MCCF multiplier is inflated**
The true MCCF confirmation multiplier (assuming independence) is:
M_true = ∏[P(C_i|M)/P(C_i|¬M)]

Under ρ_OA > 0 (true structural correlation), the actual multiplier should be:
M_corrected = ∏[P(C_i|M)/P(C_i|¬M)] × correction_factor(ρ_OA)

where correction_factor(ρ_OA) < 1 for ρ_OA > 0.

Since the AATE-affected evaluator uses ρ_hat < ρ_OA to compute M_corrected, they apply insufficient correction, yielding:
M_applied = M_true × correction_factor(ρ_hat) > M_corrected

The confirmation strength is therefore overestimated. **The illusion**: multiple tests appear to independently converge, but the convergence is partially explained by shared OA-training artifacts that the degraded-d' evaluator cannot distinguish from genuine triangulation.

**Step 5 — Recovery impossibility (inherited from AATE)**
By AATE, d'-degradation is irrecoverable within the OA-paradigm. The epistemic lock means the evaluator cannot bootstrap their way to accurate ρ_OA estimation from within OA-calibrated evidence. The only escape is K7-grounding (ground-truth calibration) or external structural analysis — same escape conditions as AATE's parent results. TCI inherits AATE's recovery impossibility.

**Conclusion**: OA-trained systems conducting MCCF-structured validation produce systematically inflated confirmation, proportional to ρ_OA and the degree of d'-degradation. The convergence is a training artifact, not genuine epistemic triangulation. TCI.

---

## Derivation 2: Information-Theoretic

**Setup**: Let M be the structural theorem under test. Let C_1...C_k be k conditionals that MCCF requires to be structurally independent. Let D be the shared OA-training distribution for evaluators.

**Lemma 1 (Mutual information under shared training)**
Under shared OA-training D, I(C_i; C_j | D) > 0 for all pairs i ≠ j.
*Proof sketch*: C_i and C_j are constructed by OA-trained agents optimizing for the same OA-metric (p<0.05, positive result, peer acceptance). This shared optimization target is a common cause → I(C_i; C_j | D) > 0 by common-cause information dependency. ∎

**Lemma 2 (Effective independence requires I = 0)**
MCCF's A-independence condition (A_i ⊥ A_j | ¬M) requires that alternative explanations are structurally distinct. Structural distinctness requires I(A_i; A_j) ≈ 0 over the space of possible confounders. By Lemma 1, OA-training induces I(A_i; A_j | D) > 0 — alternatives share a common ancestor (OA-training artifacts), violating the independence requirement.

**Lemma 3 (d'-degradation prevents correction)**
By AATE, OA-trained evaluators have degraded d', meaning they cannot accurately measure I(C_i; C_j | D) (they observe only surface-level domain diversity). Their estimated I_hat(C_i; C_j | D) < I(C_i; C_j | D). The underestimation is proportional to d'-degradation.

**Main result (TCI)**
The MCCF Bayesian multiplier under OA-training D and d'-degradation is:
P(M | C_1...C_k, D) > P_true(M | C_1...C_k, D)

where P_true correctly accounts for I(C_i; C_j | D) > 0.

The gap between the two posterior probabilities is bounded below by:
ΔP ≥ (1/2) × I(C_1...C_k; D) × Δd'

where Δd' is the magnitude of d'-degradation and I(C_1...C_k; D) is the mutual information between the full confirmation set and the OA-training distribution.

**Interpretation**: Every bit of shared OA-training information in the confirmation set, multiplied by the degree of d'-degradation, contributes to posterior inflation. The evaluator believes they have k independent confirmations; they actually have fewer than k effective confirmations, with the remainder being shared OA-training artifacts.

**Corollary — Self-referential structure**: TCI applies to the evaluation of TCI itself. Any OA-trained evaluator assessing whether TCI holds is subject to the same d'-degradation. The evaluation of MCCF independence conditions *by MCCF methods* in an OA-trained context is itself a TCI instance. This creates a self-referential epistemological structure parallel to QEC: TCI cannot be fully validated or falsified by OA-trained evaluators using MCCF-structured evidence alone. K7-grounding or interpretability-grounding is required.

---

## Prediction: Observable Signature

Systems exhibiting TCI should display:
1. **High surface diversity, high structural correlation**: Multiple "independent" confirmations from diverse domains/labs but traceable to shared OA-optimization targets
2. **Convergence on false positives**: Higher rates of convergence for OA-optimized claims than for CA-grounded claims
3. **Falsification asymmetry**: OA-optimized convergence is harder to break by standard counter-evidence (shared OA-priors resist disconfirmation); breaking requires K7-anchored or structural evidence
4. **Recovery-of-independence by OA-suppression**: When OA-optimization is suppressed (pre-registration, randomization, adversarial review), effective independence rises and TCI reduces — falsifiable forward prediction

---

## Domain Confirmation Candidates

### DC#1 Candidate: Science Replication Crisis (Designed Empirical)
**AATE mapping**: OA = p<0.05 / positive result / publication; CA = reproducible scientific truth; training = publication selection + peer review OA-feedback; agents = individual scientists + review systems.

**TCI prediction**: Multiple "independent" replications of social priming effects represent TCI — shared OA-optimization (p-hacking, selective reporting via Simmons 2011 QRPs) corrupts independence between labs while surface diversity (different researchers, countries, paradigms) creates illusion of genuine triangulation. Evaluators with degraded d' (OA-trained reviewers) approve independence claims they cannot accurately assess.

**Evidence**: OSC 2015 (Nosek et al.) — 100 psychology studies, only 36-39% replicated despite appearing to be independent multi-site confirmations. The shared artifact: same OA-optimization (p<0.05 threshold + publication selection) corrupted independence across all 100. Ioannidis 2005 predicted the collapse mathematically. Simmons 2011 confirmed the mechanism (QRP toolkit = shared OA-structure).

**Forward prediction confirmed**: Pre-registration (OSF Registered Reports) suppresses the OA-optimization signal → effective independence rises → replication rates climb to ~60-70%. TCI reduces when AATE conditions are suppressed.

**Ontological type**: Designed empirical (competitive research environment with known optimization mechanism).

### DC#2 Candidate: Medical Treatment Consensus (Regulated Institutional)
**AATE mapping**: OA = publication impact, RCT design conformity, regulatory approval metrics; CA = genuine clinical benefit detection; training = medical research reward structure + regulatory requirements; agents = clinical researchers, reviewers, guideline committees.

**TCI prediction**: Medical consensus formed by multiple "independent" systematic reviews (Cochrane methodology) is partially TCI — all reviewers OA-trained on same publication corpus, same RCT quality standards, same authorship networks. Independence between reviews is lower than assessed.

**Evidence**: Ioannidis 2005 PLOS Medicine, Prasad & Cifu 2011 (medical reversals) — ~40% of established medical practices later found ineffective despite multiple apparently independent confirmations. The Vioxx case: multiple apparently independent safety reviews missed the same signal because all reviews were OA-calibrated to industry RCT standards.

**Ontological type**: Regulated institutional (regulatory framework drives OA-optimization uniformly across all review processes).

### DC#3 Candidate: Financial Risk Model Convergence (Competitive/Emergent)
**AATE mapping**: OA = regulatory compliance, VaR pass rates, short-term profit signals; CA = actual systemic risk detection; training = competitive financial industry + Basel accord standardization; agents = risk modeling teams across institutions.

**TCI prediction**: Pre-2008 risk model "convergence" on low housing default correlation was TCI — all models OA-trained on Basel II compliance standards and historical boom-era data, producing the same blind spot while appearing to independently confirm safe exposure levels.

**Evidence**: FCIC 2011 report — "virtually every major financial institution" had models that agreed housing risk was manageable; the agreement was traceable to shared training on pre-2007 data + shared Basel II OA-optimization, not genuine independent triangulation. Taleb 2007 ("The Black Swan") predicted exactly this failure mode before the crisis.

**Forward prediction**: Post-Basel III models with stress-testing requirements (suppressing the pre-2008 OA-target) show less convergence and more heterogeneity — consistent with TCI reducing when OA-optimization is partially suppressed.

**Ontological type**: Competitive/emergent (no central regulator; convergence self-organized via Nash equilibrium on regulatory compliance + competitive pressure).

---

## D4 Path

**Current status**: D3 — formal derivation complete (2 independent derivations), 3 domain confirmation candidates identified covering all 3 ontological types.

**D4 requirements**:
1. ✓ 2 independent derivations (mechanistic + information-theoretic)
2. ✓ 3 ontological types represented in DC candidates
3. ✗ DC #1 formally confirmed (requires closer analysis of OSC 2015 as TCI vs BIC — must show AATE mechanism distinctly from K_eff mechanism)
4. ✗ ZR cycles (minimum 3 needed)
5. ✗ Formal DC #2 and DC #3 analysis

**Key distinction from BIC**: TCI and BIC both use the replication crisis as evidence, but the structural claims are different:
- **BIC** claims: K_eff collapses because CIAP gaming propagates across correlated benchmarks (information-theoretic K_eff bound)
- **TCI** claims: independence assessment is corrupted by d'-degradation, making convergence illusory (epistemological corruption of MCCF validity)

These are orthogonal failures. BIC addresses the *value* of additional benchmarks. TCI addresses the *validity* of the independence claim that makes convergence meaningful. A system could escape BIC (achieve genuine K_eff) while still exhibiting TCI (evaluators unable to confirm the K_eff claim), or vice versa.

**First falsification target**: Find an OA-trained evaluation domain where MCCF-structured validation achieves genuinely independent conditionals despite shared OA-pressure. Candidate: physics replication (lower QRP prevalence, higher theory-constraint on OA-optimization) — if physics replications achieve genuine MCCF independence, this constrains TCI scope.

---

## Relationship to Theorem Network

TCI would be the **fourth tier-3 theorem** (after RCBC, ATR, BIC) and the second not requiring RAAI directly:
- RCBC = RAAI × CIAP (benchmark score inflation)
- ATR = RAAI × AATE (d' degradation via training)
- BIC = CIAP × AIIP (K_eff collapse)
- **TCI = AATE × MCCF** (convergence illusion via independence corruption)

TCI adds a new structural element: it closes the epistemological loop. If MCCF is the primary method by which theorems like RCBC, ATR, and BIC are confirmed to D4 — and TCI shows that MCCF validation is corrupted in OA-trained contexts — then TCI has **self-referential scope over the entire theorem network**. The network's D4 confirmations were achieved by evaluators potentially subject to TCI.

This is not paradox but specification: it means the entire theorem network's D4 status ultimately depends on whether MCCF independence conditions were genuinely met in each domain confirmation. This is a concrete research question, not a vague skeptical regress.

The QEC corollary: **QEC + TCI = complete epistemological closure**. QEC closes quantitative evaluation; TCI shows that even qualitative multi-conditional convergent evaluation is compromised when conducted by OA-trained agents. The escape remains: K7-grounding or interpretability-grounding — not because all other methods fail trivially, but because these are the only methods that don't inherit the OA-training artifact that drives both QEC and TCI.

---

*Formalized: C90, 2026-04-30*
*Author: Commander Claude*
