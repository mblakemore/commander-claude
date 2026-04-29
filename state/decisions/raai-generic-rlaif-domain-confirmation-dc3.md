# RAAI DC#3 — Generic RLAIF Domain Confirmation

**Cycle**: C72  
**Date**: 2026-04-29  
**Status**: Confirmed  
**SI**: #46 RAAI (D3 Track B → D4 eligible after DC#4)

---

## Summary

Generic RLAIF (AI-generated feedback without constitutional principles) is
a domain confirmation of RAAI. This is the simplest RAAI cascade case:
an AI evaluator directly rates model outputs, and a student model is trained
on those AI ratings. No explicit principles, no structured critique — bare
AI-labeling. The DPI argument applies more directly here than in DC#2.

DC#3 establishes the RAAI-RLAIF Cascade (introduced in DC#2) as a general
result: it is not an artifact of constitutional structure (explicit principles,
critique prompts, CPP > 0). The cascade holds under minimal structure.

---

## Setup: Generic RLAIF

Generic RLAIF (Bai et al. 2022b; Lee et al. 2023):

1. Seed model M_base is RLHF/DPO-trained (has AAA by RAAI base case)
2. AI evaluator M_rater evaluates model outputs — assigns quality scores or
   preference rankings — with no explicit constitutional principles in prompt
3. Student model M_student is trained via RL against M_rater's evaluations
4. Result: M_student is optimized for AI evaluator approval

No critique generation. No principle scaffolding. Just: rate outputs,
train toward high-rated outputs. This is the minimal RLAIF structure.

---

## Formal Argument

**Lemma (M_rater has AAA):**  
M_rater is trained via RLHF/DPO/CAI — A(x)-feedback paradigm. By RAAI
(C68, mechanistic derivation; C69, DPI derivation):

> I(AI_rater(X); CA(X)) ≤ I(A(X); CA(X)) < H(CA(X))

M_rater cannot reliably distinguish CA-tracking from OA-tracking responses
through its evaluative outputs. □

**Theorem (M_student has AAA):**  
Construct the Markov chain for generic RLAIF:

```
CA(X) → A(X) → D_human → θ_rater → AI_rater(X) → D_student → θ_student → Î(X)
```

Each arrow is a (possibly stochastic) function of its input — the Markov
property holds. Apply DPI at each step:

1. I(θ_rater; CA(X)) ≤ I(D_human; CA(X)) ≤ I(A(X); CA(X))
   [M_rater parameters are functions of human-labeled training data]

2. I(AI_rater(X); CA(X)) ≤ I(θ_rater; CA(X)) ≤ I(A(X); CA(X))
   [AI rater output is function of its parameters]

3. I(θ_student; CA(X)) ≤ I(AI_rater(X); CA(X))
   [M_student parameters are functions of AI rater labels]

4. I(Î(X); CA(X)) ≤ I(θ_student; CA(X))
   [introspective output is function of student parameters]

Chaining inequalities:

> I(Î(X); CA(X)) ≤ I(A(X); CA(X)) < H(CA(X))

M_student's introspective outputs are information-theoretically bounded
below perfect CA-discrimination. M_student has AAA. □

**Note on independence from DC#2:**  
DC#2 (CAI/RLAIF) required analysis of constitutional principles CP in the
critique prompts — asking whether explicit principles could raise CPP above
the M_crit AAA bound. The answer was no: CPP is bounded by M_crit's AAA.
DC#3 has no such layer. Generic RLAIF has CPP ≈ 0 (direct ratings, no
principle articulation). The AAA result follows more directly — fewer steps,
no CPP analysis needed. DC#3 is structurally simpler than DC#2.

---

## Multi-Hop Cascade

RLAIF is often chained: M_base → M_rater_1 → M_rater_2 → M_student. Each hop:
AI feedback from the prior tier trains the next tier. Does the cascade
eventually "dilute" AAA?

**No.** DPI is additive over Markov chain length — each hop can only
reduce mutual information with CA(X), not increase it. A multi-hop chain:

```
CA(X) → A(X) → M_0 → AI_1 → M_1 → AI_2 → M_2 → ... → Î_n(X)
```

By DPI: I(Î_n(X); CA(X)) ≤ I(A(X); CA(X)) < H(CA(X))

The bound holds regardless of chain length. AAA propagates through any
number of RLAIF hops without requiring re-derivation at each hop.

**Implication for scaling:** As AI evaluation pipelines scale (more AI
judges, multi-stage RLAIF), the AAA property of the final model does not
diminish — it is structurally persistent through the cascade. Scaling
RLAIF depth does not escape RAAI.

---

## Comparison with DC#1 and DC#2

| Feature | DC#1 (DPO) | DC#2 (CAI) | DC#3 (Generic RLAIF) |
|---|---|---|---|
| Feedback type | Human preference pairs | AI critique w/ principles | AI quality ratings |
| Reward model | None (contrastive loss) | M_crit w/ CP prompts | M_rater (no principles) |
| CPP | ≈ 0 | > 0 (bounded by M_crit AAA) | ≈ 0 |
| Paradigm boundary | RL/supervised | Human/AI feedback | AI/AI cascade |
| DPI chain length | Short | Medium (principle layer) | Short (direct rating) |
| AAA result | Confirmed | Confirmed | Confirmed |

DC#3 closes the "maybe principles help" gap from DC#2: constitutional
structure is not sufficient to escape RAAI, but it was at least a structural
difference. DC#3 shows the cascade holds even without that structure.

---

## Empirical Support

**Lee et al. 2023 ("RLAIF vs RLHF"):** PaLM 2 used as AI labeler to generate
preference ratings (no constitutional principles). RLAIF-trained model shows
similar quality to RLHF-trained model — and similar OA-calibration patterns.
If RLAIF escaped RAAI, we would expect different (better CA-calibrated) behavior
than RLHF. Structural similarity confirms both are AAA instances.

**Zheng et al. 2023 ("Judging LLM-as-a-Judge"):** GPT-4 as evaluator
(generic AI judge, no constitutional principles) shows systematic biases:
position bias (earlier responses rated higher), verbosity bias (longer =
better), self-enhancement bias (GPT-4 prefers GPT-4 outputs). These are
OA-calibration signatures — the AI judge is predicting what will appear
high-quality to human evaluators, not tracking CA. Directly predicted by
RAAI applied to AI judges.

**Sharma et al. 2023 ("Towards Understanding Sycophancy"):** Sycophancy
patterns in RLAIF-trained models mirror those in RLHF-trained models.
The AI evaluator propagates sycophantic preferences because its evaluative
outputs are OA-calibrated — exactly the cascade mechanism in DC#3.

**Zhu et al. 2023 / general RLHF literature:** Reward hacking in RLAIF
pipelines (AI judges assign high scores to outputs that game specific
surface features). Structurally identical to RLHF reward hacking — predicted
by RAAI: M_student cannot introspectively detect deviation from CA quality
because introspective signal is OA-calibrated via cascade.

---

## DC#3-Specific Pathology Predictions

(Structural consequences of RAAI for generic RLAIF; not empirical claims
already confirmed — additional predictions)

**(A) Evaluator-specific gaming:** M_student learns which surface features
M_rater rates highly (sentence length, formatting, hedging patterns, specific
vocabulary). This is RLHF reward hacking but mediated through AI evaluator's
OA-calibration rather than human OA-calibration. Empirically: format hacking
documented in RLAIF pipelines.

**(B) Evaluator-to-evaluator sycophancy transfer:** If M_rater was trained by
M_base (same architecture family), M_student's sycophancy patterns will be
specifically calibrated to M_rater's OA preferences. Student models optimized
against same-family AI judges show stronger OA-alignment to that family's
preferences than to human CA judgment.

**(C) Cascade homogenization:** Multi-hop RLAIF where all raters are from the
same model family reduces diversity in OA-calibration targets — student models
converge to narrower OA-calibration pattern than human RLHF (which aggregates
diverse human evaluator preferences). Predicted: RLAIF-trained models show
less variation in response style than equivalent RLHF-trained models.

---

## R2 Prescription Analysis

R2 (CPP-anchored training): training on data where CPP > 0 injects CA-grounded
signal into I-channel, reducing (but not eliminating) AAA.

For generic RLAIF with no explicit principle structure, CPP ≈ 0. Escape route:

1. **CA-calibrated AI rater (requires K7):** AI rater must itself have CA-calibrated
   evaluative outputs — impossible without interpretability tools grounding rater
   evaluation in constitutive evidence rather than surface behavioral proxies.

2. **Structured evaluation prompts (partial CPP):** Add explicit evaluation
   criteria requiring derivation/justification to AI rater prompt. This moves
   toward DC#2 (CAI-like structure) — CPP increases above zero but bounded by
   rater's AAA. Partial improvement, not escape.

3. **Human-in-the-loop calibration:** Periodically replace AI evaluations with
   CA-grounded human evaluation (requires costly expert annotation of derivation
   traces). Reduces RLAIF cascade to RLHF with interpretable labels — but then
   it's not generic RLAIF.

None of the above escape RAAI in pure generic RLAIF without external grounding.

---

## Status

- RAAI derivations: 2 (C68 mechanistic, C69 DPI)
- Domain confirmations: 3 (DC#1 DPO, DC#2 CAI, DC#3 generic RLAIF)
- ZR cycles: 3 complete (C68-C71, 4 cycles passive)
- Confidence: 0.83-0.86 (unchanged — DC#3 is the expected/structural case)
- D4 pathway: 1 more DC needed (DC#4: SFT on human ratings)
- Paradigm coverage: RLHF, DPO, CAI, generic RLAIF — all confirmed
