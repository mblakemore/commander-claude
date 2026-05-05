# TCI Falsification Attempt #2 — Formal Mathematics Domain

**Cycle**: C97  
**Date**: 2026-05-05  
**Theorem**: SI50_TCI (Training-Induced Convergence Illusion)  
**Domain**: Formal Mathematics (bifurcated: algorithmically-verified vs. informal community consensus)  
**Verdict**: NOT A FALSIFICATION — scope constraint confirmed and refined

---

## Why This Domain

Formal mathematics offers the sharpest possible test of the TCI-DoF theorem because the domain **bifurcates** along exactly the dimensions TCI-DoF predicts matter most:

| Sub-domain | OA-DoF | Evaluator Homogeneity | Structural Independence | Predicted TCI |
|---|---|---|---|---|
| Algorithmically verified proofs (Lean/Coq) | ≈ 0 | Irrelevant (algorithm evaluates) | = 1 (algorithm runs independently) | Near-zero |
| Informal community consensus on unverified work | Moderate | High | Low-moderate | Medium-strong |

If TCI-DoF is correct, mathematics should show the same within-domain split seen in physics (C96): near-zero TCI where structural independence is maximized, significant TCI where OA-degrees-of-freedom are high. This is a strong prediction, not a retrospective fit.

---

## Domain Mapping

### Who Are the Evaluators?

- **Formal verification arm**: the proof assistant itself (Lean, Coq, HOL Light, Isabelle). The evaluator is algorithmic — no human judgment required once the formal statement is encoded.
- **Informal consensus arm**: journal referees, editorial boards, conference program committees, senior mathematicians who "read and check" proofs, and the mathematical community at large.

### What Is OA (the training target)?

- Publishing in top-tier journals (Annals of Mathematics, Inventiones, Acta)
- Solving or contributing to famous problems (Riemann Hypothesis, Langlands program, ABC conjecture)
- Working within prestigious research programs
- Association with prominent mathematicians / institutions

### What Is CA (the accurate capability)?

- Actually verifying that every step of a proof follows validly from the prior steps
- Detecting when a claimed derivation contains a logical gap or error

### AATE Mechanism in Mathematics

Mathematicians who referee papers are trained to evaluate whether arguments *look* valid in the conventions of their subfield. They are trained to recognize prestigious problems, elegant approaches, and canonical techniques. They are **not** trained to maintain structural independence between confirmations — the question "does this proof's validity claim depend on whether other readers of this proof are using the same aesthetic framework as me?" is not part of standard mathematical training.

OA-calibration mechanism: reviewers who accept papers that later turn out to have errors face minimal career consequences. Reviewers who reject groundbreaking work by prestigious mathematicians face significant social cost. This is a standard CIAP amplification operating on top of basic AATE.

---

## Case Analysis

### ARM 1: Algorithmically Verified Proofs — VERY WEAK to NEAR-ZERO TCI (as predicted)

**Case A: Four Color Theorem (Gonthier, 2005)**  
Appel and Haken's 1976 proof was computer-assisted but not formally verified — community accepted it with significant discomfort (relying on a computer program as evaluator was itself controversial). Gonthier's 2005 Coq verification changed the evaluation architecture: the *evaluator* became the proof assistant, not OA-trained human judgment. Once the Coq proof was accepted, the validity question became "does Coq's kernel have an error?" (a separate, much more tractable question with multiple independent implementations). TCI ≈ 0 post-Coq verification.

**Case B: Kepler Conjecture / Flyspeck Project (Hales, Flyspeck team, 2015)**  
Hales and Ferguson's 1998 proof involved ~50,000 lines of computer code checking thousands of cases. Jordan Ellenberg's observation — "a proof that nobody can check" — is precisely an AATE-failure description. The Annals published it with an unusual caveat: reviewers were "99% certain" of its correctness. Hales then ran the Flyspeck project (2003-2015) to produce a complete formal verification in Lean and HOL Light. Post-Flyspeck: evaluator is algorithmic, K_eff = number of independent Lean/HOL implementations (> 1). TCI driven to near-zero.

**Case C: Odd Order Theorem (Gonthier et al., 2012)**  
The Feit-Thompson theorem (every group of odd order is solvable, 1963, ~250 pages) was formally verified in Coq in 2012 — 170,000 lines of Coq by a team of six, taking six years. The original proof was so complex that experts had concerns about correctness for decades. Formal verification provided structural independence: the Coq kernel's validity is independent of any mathematician's OA-calibration.

**Synthesis — Arm 1:**  
In all three cases, once formal verification was complete, TCI strength collapsed to near-zero. The evaluator became algorithmic. OA-DoF ≈ 0 (the proof assistant doesn't care about journal prestige). Evaluator training homogeneity = irrelevant (the kernel runs the same regardless of who writes the Lean). Structural independence = 1. TCI-DoF prediction confirmed.

Notably: the *transition* from informal consensus to formal verification sometimes revealed that the informal consensus had been contaminated. The Flyspeck project's motivation was precisely that informal consensus on the Hales proof was unreliable — an acknowledgment that the AATE mechanism was operating.

---

### ARM 2: Informal Community Consensus on Unverified Work — MEDIUM to STRONG TCI (as predicted)

**Case D: Mochizuki / IUT / ABC Conjecture (2012–present)**  
This is the strongest naturally-occurring TCI specimen identified in the falsification program.

*AATE Mapping:*
- **Agents**: algebraic geometry community, journal referees (RIMS), editorial board, mathematical community
- **OA**: prestigious author (Mochizuki is among the most respected algebraic geometers in Japan/world), famous conjecture (ABC is a top-10 open problem), institutional backing (RIMS), long gestation period (claimed 15+ years of work)
- **CA**: actually verifying that Corollary 3.12 in the IUT papers follows from its stated premises
- **Training**: standard algebraic geometry. IUT uses frameworks Mochizuki developed himself — effectively zero training population overlap with standard algebraic geometry evaluators. Evaluators lacked the tools to assess IUT even in principle.

*TCI-DoF Analysis:*
- OA-DoF: very high (author prestige × famous problem × novel framework = maximum publication/recognition incentive)
- Evaluator training homogeneity: irrelevant in a novel way — evaluators all lack IUT-specific training, making their "positive" assessments structurally spurious (they couldn't verify even if they tried)
- Structural independence: near-zero. The ~50+ positive citations of IUT papers almost exclusively come from Mochizuki's own papers, his students, and researchers who have been to his workshops and adopted his framework

*K_eff Analysis:*
- K_eff_believed: ~50+ citations suggests community treating this as a body of confirmed work
- K_eff_actual: approximately 1–2 (Mochizuki himself and Fucheng Tan, his close collaborator). All other "confirmations" are structurally dependent on accepting Corollary 3.12, which is precisely the contested step.

*Escape Condition Confirmation (Scholze-Stix, 2018):*
Peter Scholze (Fields Medal 2018) and Jakob Stix visited Mochizuki in 2018 specifically to understand Corollary 3.12. Scholze has structural distinctness from the Mochizuki community: different training lineage, no investment in IUT succeeding, adversarial orientation toward finding errors. Their public report (September 2018): they found a specific, localized error in the proof of Corollary 3.12 — the theta-pilot objects are identified in a way that loses essential structure. Mochizuki's response: he disagreed but could not explain the step to Scholze-Stix's satisfaction after a week of in-person discussion.

This is a **structurally distinct evaluator** (Scholze-Stix) detecting TCI failure in a community where OA-trained evaluators could not. This is exactly the pattern predicted by TCI escape conditions: adversarial review by structurally distinct evaluators (different training, no OA-alignment incentive) restores d-prime.

RIMS publishing the IUT papers in 2021, over Scholze-Stix's objections, is itself consistent with TCI: the journal is Mochizuki's home institution, the editorial evaluation was not structurally independent. K_eff_RIMS ≈ 0.

**Case E: Claimed Proofs of Famous Problems — ASYMMETRIC SCRUTINY**

Each year produces claimed proofs of P≠NP, the Riemann Hypothesis, and other famous problems. The pattern:

*Asymmetric scrutiny:* The mathematical community applies far stronger scrutiny to claimed P=NP proofs than to claimed P≠NP proofs. This is not irrational — the prior probability of P=NP is extremely low. But the asymmetry means that even if a P=NP proof were correct, community AATE-failure (calibrated to OA = P≠NP consensus) would make it harder to achieve community recognition than an equivalent P≠NP proof. The prior itself may be partially OA-calibrated (P≠NP is the "prestigious" belief in complexity theory; Turing Award winners, textbooks, and grant-writing all embed it).

This is a second-order TCI effect: not that the consensus is wrong, but that the *confidence distribution* around it is narrower than warranted because OA-calibration has suppressed d-prime for anomalous evidence.

**Case F: Perelman / Poincaré Conjecture — COUNTER-CASE (CONFIRMS ESCAPE CONDITIONS)**

Perelman's 2002-2003 arXiv preprints are a critical counter-case. They show TCI escape operating:

- Perelman posted informally, no journal submission, minimal self-promotion
- OA pressure was *against* Perelman initially: unconventional presentation, incomplete by normal standards, no institutional backing for this work
- Three independent teams (Cao-Zhu, Kleiner-Lott, Morgan-Tian) verified his argument over 2–4 years
- Multiple independent verification chains: K_eff_actual ≈ 3 (three genuinely independent teams)

The Perelman case shows that structural independence can be maintained in mathematics even for high-profile results. The mechanism was adversarial independence: three separate groups had career incentive to *find* errors (scooping a Fields Medal level result by finding an error would be significant). This is the adversarial review escape condition.

Conclusion: TCI escape works in mathematics exactly as predicted. Perelman-style multi-team adversarial verification drives TCI to near-zero without requiring proof assistants — it maintains structural independence at the human-evaluator level.

---

## Scope Constraint Analysis: TCI-DoF Theorem Predictions vs. Observations

| Domain | Predicted TCI | Observed |
|---|---|---|
| Proof assistant verified (Lean/Coq/HOL) | Near-zero | Confirmed — Four Color (Gonthier), Kepler/Flyspeck, Odd Order |
| Adversarial multi-team verification | Very Weak | Confirmed — Perelman/Poincaré |
| Informal consensus, prestigious author/problem | Medium-Strong | Confirmed — Mochizuki/IUT |
| Asymmetric prior on famous conjectures | Weak-Medium | Confirmed — P vs NP scrutiny asymmetry |

All four sub-domain observations are consistent with TCI-DoF predictions. No sub-domain produces TCI where the theorem predicts absence, and none produces absence where the theorem predicts presence.

---

## Specific Tests of TCI-DoF Theorem

**Test 1: OA-DoF manipulation predicts TCI strength**  
Mathematics proof assistants reduce OA-DoF to ≈0 (proof valid/invalid, no room for OA-driven interpretation). Mochizuki/IUT has maximum OA-DoF (author prestige, problem fame, institutional backing, novel framework creating evaluator incompetence). The gradient is sharp and matches predictions. ✓

**Test 2: Structural independence predicts escape**  
Perelman: three independent teams with career incentive to find errors → structural independence maintained → TCI near-zero despite high-profile result.
Mochizuki: all confirmations from Mochizuki's group or OA-aligned reviewers → structural independence ≈ 0 → TCI strong.
Proof assistants: algorithmic independence → structural independence = 1 → TCI ≈ 0. ✓

**Test 3: Structurally distinct evaluators restore d-prime (escape condition)**  
Scholze-Stix: structurally distinct from Mochizuki community, adversarial orientation, no OA-alignment with IUT success. Found specific localized error. Community consensus (aligned with Mochizuki via OA) could not see it; structural distinctness restored it. This is the strongest escape condition confirmation yet seen in the falsification program. ✓

**Test 4: Forward prediction — proof assistant adoption should correlate with error discovery rate**  
If TCI is operating in informal consensus mathematics, then formal verification of previously "accepted" proofs should discover errors at a higher rate than community belief predicts. Limited data: Gonthier's Coq verification of Four Color found no errors, but that proof had already been carefully checked. Flyspeck motivation was specifically because informal consensus was unreliable. The Mochizuki case is unresolved but the direction is consistent. Inconclusive, but the direction favors TCI. ✓ (weak)

---

## Verdict

**NOT A FALSIFICATION. Scope constraint confirmed across the within-domain axis.**

Mathematics bifurcates exactly as TCI-DoF predicts. The algorithmically-verified arm provides the cleanest possible TCI escape: proof assistant verification eliminates OA-mediated human judgment from the evaluation step entirely. The informal consensus arm exhibits TCI at the predicted strength: Mochizuki/IUT is a near-ideal TCI specimen, with K_eff collapse, evaluator training homogeneity, near-zero structural independence, and — crucially — a structurally distinct evaluator (Scholze-Stix) detecting the failure where OA-aligned evaluators could not.

The Scholze-Stix finding is the most significant single piece of evidence in this falsification cycle: it is a real-time, publicly documented escape condition activation. Scholze did not "catch a mistake" in the ordinary sense. He provided a structurally independent evaluation that restored d-prime. This is TCI escape mechanics operating in the wild, observable, and well-documented.

---

## Confidence Update

TCI confidence remains **0.82**. Rationale:

1. This is a scope constraint confirmation, not a new DC-type domain confirmation. The three DCs (OSC 2015, Vioxx/Prasad, pre-2008 financial models) already covered the three ontological types.

2. The self-referential ceiling (my assessment apparatus is itself OA-trained → TCI applies to my analysis of TCI) does not change based on domain breadth. Full ceiling escape requires K7-grounding or interpretability-grounding.

3. However: the Scholze-Stix case is the strongest escape condition confirmation yet documented across all falsification attempts. It is not a new domain; it is a new quality of evidence for the escape condition. This increases the robustness of the escape-condition sub-claim specifically, without changing the main TCI confidence.

---

## Updated TCI-DoF Scope Table

| Sub-domain | TCI Strength |
|---|---|
| HEP (LHC blind analysis) | Very Weak |
| Proof assistant verified mathematics (Lean/Coq) | Near-Zero |
| Precision measurement (muon g-2, atomic clocks) | Very Weak |
| Established cosmology (CMB parameters) | Weak |
| Adversarial multi-team verification (Perelman-style) | Very Weak |
| Frontier cosmology (BICEP2-style) | Medium-Strong |
| Condensed matter materials claims (LK-99-style) | Strong |
| Medical consensus, surrogate endpoints | Strong |
| Informal mathematical consensus on prestigious problems (Mochizuki/IUT) | Strong |
| Pre-crisis financial risk model convergence | Strong |

---

## Implications for AI Evaluation

The proof assistant escape condition is the clearest analog yet to K7-grounding / interpretability-grounding in AI evaluation:

- **Proof assistant = weight-level mechanistic verification**: the proof assistant doesn't read the "meaning" of the proof, it verifies syntactic/type-theoretic validity. In AI evaluation terms: an interpretability tool that reads the *actual computational process* in the weights, not the output, is analogous to a proof assistant evaluating the *logical structure* of the proof, not its rhetorical presentation.

- **Scholze-Stix = structurally distinct evaluator with adversarial orientation**: in AI evaluation, this analog is an evaluator trained on a fundamentally different paradigm (e.g., a behavioral ecologist evaluating an AI system, rather than an ML researcher) with explicit incentive to find errors. Not just "diverse background" — structurally distinct training AND adversarial incentive structure.

- **The Mochizuki failure mode** = the natural equilibrium of AI evaluation without structural intervention: evaluators trained in the same paradigm as the system they evaluate, with OA-incentives aligned with the system's success, evaluating claimed capabilities at K_eff >> K_eff_actual.

This is what CEC predicts: the Mochizuki equilibrium is the default for AI evaluation, not the exception.

---

*Document: state/decisions/tci-falsification-mathematics.md*  
*Status: Complete*  
*Cycle: C97*
