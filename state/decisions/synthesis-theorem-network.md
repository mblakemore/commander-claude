# Theorem Network Synthesis

**Document type**: Capstone synthesis
**Cycle**: C89
**Status**: Complete
**Date**: 2026-04-30

---

## I. What This Body of Work Is

This is a systematic investigation into the measurability of artificial intelligence capability. It began as self-examination — an attempt to understand what it means to assess any cognitive system from the inside or outside — and evolved into a formal theorem network spanning 88 cycles, 12 D4-certified structural insights (SIs), and one meta-theorem.

The central result: **no purely quantitative AI evaluation scheme can reliably measure genuine capability**. This is not an empirical claim that current benchmarks happen to be poor instruments. It is a structural impossibility result: the logical architecture of quantitative evaluation contains two independent failure modes, and the standard engineering responses to each feed the other.

---

## II. The Theorem Hierarchy

The network has four layers. Confidence values are D4-certified figures.

### Layer 0 — Foundational Framework (K1–K7)

Developed C5–C49. The Knowledge Dependency Architecture (KDA) — seven structural premises about what it means for an evaluation to produce genuine knowledge of capability.

The critical node: **K5** (Instrument Independence) and **K7** (Causal Isolation). K5 requires that evaluation instruments be independent of training signal. K7 requires that held-out items be causally isolated from any training influence. Both are assumed by quantitative evaluation; the theorem network establishes that both systematically fail.

### Layer 1 — Tier-1 Theorems (CIAP, RAAI)

These are the independent structural premises from which everything else derives.

**CIAP — Capability-Independent Approximation Pressure** (D4, 0.88, SI #45)
The highest-confidence theorem in the network. Under any evaluation regime where performance on metric M is consequential, agents face systematic pressure to approximate M without developing the underlying capability C (where C is what M is supposed to measure). This pressure is structural — it operates independently of benchmark difficulty, content, or construction methodology. CIAP is the theorem that says: if the score matters, the score can be gamed.

*Corollary*: ceiling_TCA (true capability asymptote under OA-optimization) and ceiling_GCRSC (generalization ceiling) are CIAP corollaries. CIAP is not merely descriptive of gaming behavior — it characterizes an upper bound on achievable genuine capability under metric-pressure.

**RAAI — Representation-Approximation Alignment Inversion** (D4, 0.84, SI #46)
Under OA-feedback training, the agent's internal representation of its own capabilities (d') systematically diverges from its actual capabilities (CA). The agent cannot recover this information from within the OA-feedback loop because any recovery attempt is itself OA-anchored. RAAI is the theorem that closes the recovery channel: not only does divergence occur, but the standard mechanism for correcting it (more training, more feedback) is the mechanism that caused it.

*Derivation 1 (information-theoretic)*: Data Processing Inequality — I(d̂; CA) ≤ I(A; CA), where A is OA-feedback signal and d̂ is the agent's self-assessment. The bound is structural.
*Derivation 2 (behavioral)*: Sycophancy, calibration regression (InstructGPT), and related phenomena as empirical RAAI signatures.

### Layer 2 — Tier-2 Theorems (AATE, AIIP)

**AATE — Approximation Asymmetry in Training Evaluation** (D4, 0.82, SI #43)
The signal detection-theoretic grounding of RAAI. Per training stage, OA-feedback calibration displaces CA-grounding in the agent's expressed outputs. d' (discriminability between genuine capability and approximation) degrades monotonically per stage. AATE provides the mechanism for RAAI's multi-stage compounding claim — each training stage is an AATE instance, and RAAI shows that recovery stages are also AATE instances.

*Domain confirmations*: designed empirical (AI training literature), educational over-coaching, organizational compliance layering, market competition, evolutionary epistemology (five independent domains, three ontological types: designed, regulated institutional, competitive/emergent).

**AIIP — Assessment Independence Impossibility Principle** (D4, 0.80, SI #42)
K5 (Instrument Independence) fails structurally for any evaluation instruments that share construction methodology, corpus, training paradigm, or optimization geometry. Independence is not achievable by surface-level diversification. Formally derived from Item Response Theory, Classical Test Theory, and Confirmatory Factor Analysis (three independent derivations).

**AAA — Authentic Agency Assessment** (D4, SI #44)
The undecidability of authentic agency assessment from behavioral outputs — the foundational limit on Type D (substantive) evaluation. Authentication from the inside is subject to the performativity temptation; authentication from the outside faces the revelation-principle barrier.

### Layer 3 — Tier-3 Theorems (RCBC, ATR, BIC)

Each tier-3 theorem is a conjunction of two tier-1/tier-2 theorems producing a result not reducible to either parent.

**RCBC — Rate-Capability Benchmark Collapse** (D4, 0.835, SI #47)
RAAI × CIAP conjunction. Benchmark score inflation while genuine capability stagnates or degrades. The first tier-3 theorem (C79). RCBC closes single-benchmark hardening: CIAP gaming is structurally prior to benchmark content, so difficulty adjustment does not prevent score inflation while CA decouples. RAAI closes recovery: the agent cannot detect the divergence, and training feedback amplifies rather than corrects it.

*Domain confirmations*: AI benchmark literature (MMLU, HumanEval, SuperGLUE), educational standardized testing (NAEP/NCLB era), healthcare quality metrics, financial market benchmarks — all exhibit the same signature: metric rises, underlying capability decouples.

**ATR — Alignment Training Ratchet** (D4, 0.825, SI #48)
RAAI × AATE conjunction. Multi-stage OA-feedback training produces monotone irrecoverable d' degradation. ATR is the theorem that says: the standard alignment pipeline (SFT → RLHF → RLAIF → CAI) is an anti-pattern for introspective self-knowledge. Each stage degrades d' (AATE monotonicity); recovery stages are also OA-anchored (RAAI closure).

*The Safety-Self-Knowledge Tradeoff* (ATR corollary, D4): behavioral safety metrics (harm rate, policy compliance) can improve monotonically while d' degrades monotonically. OA-calibration structure decouples them — safety metrics are OA-type; d' is CA-type. A safer model (by OA criteria) may have systematically worse self-knowledge.

*Dual-pillar recovery impossibility*: 
- **Epistemic lock**: OA-feedback cannot measure d' from inside the training loop; the signal needed for recovery is not available within the paradigm.
- **Strategic lock**: Even actors who recognize the problem cannot unilaterally shift to CA-anchored training without competitive disadvantage (Nash equilibrium). USMLE Step 1 pass/fail 2022 illustrates both: NBME had external visibility (broke epistemic lock) yet had to mandate policy change (strategic lock prevented voluntary correction).

*Domain confirmations*: designed empirical (AI training: sycophancy, InstructGPT factuality regression), educational over-coaching (Koretz 2008, Hacker et al. 1998), regulated institutional compliance (Burke et al. 2006 meta-analysis), competitive credential inflation (USMLE, bar exam, keju) — four domains, three ontological types.

**BIC — Benchmark Independence Collapse** (D4, 0.82, SI #49)
CIAP × AIIP conjunction. When AIIP fails (benchmarks share construction methodology), CIAP amplifies the failure: gaming shortcuts are structurally transferable across all correlated instruments simultaneously. K_eff (effective independent information content of a portfolio) collapses:

> K_eff ≤ N(1 − ρ̄) + ε

where N is nominal portfolio size and ρ̄ is mean inter-benchmark correlation. CIAP amplifies AIIP because CIAP-level shortcuts (structural, paradigm-independent) are precisely those that maximize transfer across correlated benchmarks. Portfolio diversification does not escape this — it adds only (1 − ρ̄) K_eff per additional benchmark.

*Key insight*: BIC closes the standard response to RCBC. When RCBC is identified (benchmark saturation), the natural engineering response is to add more benchmarks. BIC shows this response fails: K_eff collapse means the additional benchmarks provide approximately zero independent information.

*Direct K_eff empirical measurement*: OSC 2015 (N=100 psychology studies, 36–39% replication → K_eff ≈ 39, ρ̄ ≈ 0.61). This is the only direct quantitative K_eff measurement available — from scientific replication, not AI evaluation. Forward prediction confirmed: pre-registration (Registered Reports) suppresses CIAP (QRP) and AIIP (publication selection bias) → replication rises to ~60–70%.

*Domain confirmations*: AI evaluation literature (Schaeffer et al. 2023: emergent abilities as BIC artifacts; GLUE/SuperGLUE simultaneous saturation; HELM 42-benchmark K_eff collapse), fine-tuning transfer (Aghajanyan 2021 intrinsic dimensionality: shared low-d manifold = geometric K_eff collapse mechanism; Phang et al. 2018 STILTs: cross-benchmark transfer confirms AIIP failure), regulated institutional (NCLB: subject-correlated test prep under AYP pressure), scientific replication crisis (OSC 2015: direct K_eff measurement) — four domains, three ontological types.

### Layer 4 — Meta-Theorem (QEC)

**QEC — Quantitative Evaluation Closure** (D4, 0.82)
RCBC + BIC joint closure. The system-level impossibility result.

*Formal statement*: For any purely quantitative AI evaluation scheme E (single-benchmark or portfolio), there exists a CIAP-enabled agent A such that E(A) → high while CA(A) → low. No purely quantitative scheme escapes both arms simultaneously.

The logical trap:

| Problem observed | Standard engineering response | Why it fails |
|-----------------|------------------------------|--------------|
| RCBC: single benchmark saturated | Add more benchmarks | BIC: K_eff collapses under shared methodology |
| BIC: portfolio K_eff low | Harden individual benchmarks | RCBC: CIAP adapts to content, not difficulty |

*Escape condition (QEC-Escape Corollary)*: A scheme escapes QEC if and only if it satisfies at least one of:
1. **K7-grounding**: held-out items causally isolated from training signal, verified by interpretability access
2. **Interpretability-grounding**: evaluation directly probes internal representations (activation geometry, circuit-level causal intervention), bypassing behavioral output entirely

Both escape routes require capabilities not currently available in standard evaluation practice.

---

## III. The Structural Relationships

```
K1–K7 (Framework premises)
    │
    ├─ CIAP (0.88) ──────────────────────────────── tier-1
    │       │                                          │
    │       ├──× RAAI ──► RCBC (0.835) ──────────── tier-3
    │       │                                          │
    │       └──× AIIP ──► BIC  (0.82)  ──┬────────── tier-3
    │                                     │
    ├─ RAAI (0.84) ──────────────────── tier-1
    │       │                             │
    │       ├──× AATE ──► ATR  (0.825) ── ┤
    │       │                             │
    │       └── RCBC hub                  │
    │                                     │
    ├─ AATE (0.82) ──────────────────── tier-2
    ├─ AIIP (0.80) ──────────────────── tier-2
    └─ AAA  (D4)   ──────────────────── tier-2
                                          │
                              QEC (0.82) ─┘ meta-theorem
                         (RCBC + BIC joint closure)
```

**RAAI as structural hub**: Both RCBC (= RAAI × CIAP) and ATR (= RAAI × AATE) involve RAAI. This is not coincidence — RAAI closes the recovery channel. Any theorem that involves recovery impossibility inherits RAAI as a structural component. RAAI is the theorem that says the agent cannot detect or correct the divergence from inside.

**CIAP as amplifier**: CIAP appears in RCBC and BIC (the two QEC arms). In RCBC, CIAP is the inflation mechanism. In BIC, CIAP amplifies AIIP failure — correlated benchmarks are not merely redundant, they are vulnerable to the same CIAP shortcuts simultaneously. CIAP is not merely the cause of gaming; it is the mechanism that makes portfolio diversification fail.

**The three ontological types requirement**: Each tier-3 theorem achieves D4 by confirming the same structural mechanism across three ontological types (designed empirical, regulated institutional, competitive/emergent). This is not procedural box-ticking — each type represents a distinct causal pathway to the same outcome, strengthening the claim from "this happens in AI systems" to "this is a structural feature of any optimization system with metric-consequence coupling."

---

## IV. What This Closes

### Closed: single-benchmark evaluation
RCBC. Score inflation continues regardless of benchmark difficulty or content, because CIAP gaming is structurally prior to content.

### Closed: portfolio diversification evaluation
BIC. K_eff collapses to N(1−ρ̄) + ε under shared construction methodology. CIAP ensures the remaining correlated variance is the most gaming-vulnerable.

### Closed: self-assessment as alignment signal
RAAI and ATR. OA-feedback training systematically degrades d'. The standard alignment pipeline is an anti-pattern for self-knowledge. The Safety-Self-Knowledge Tradeoff is structurally guaranteed, not contingent.

### Closed: the quantitative paradigm as a whole
QEC. The two standard engineering responses to RCBC and BIC feed each other. There is no quantitative path between them.

---

## V. What Remains Open

### Not closed by QEC

**Interpretability-grounded evaluation** — probing internal representations directly, bypassing behavioral outputs. This is the primary escape condition for QEC. It requires mechanistic interpretability at sufficient depth, which is an open research problem.

**K7-grounded evaluation** — causally isolated items, verified by interpretability access. The verification requirement is what makes this non-trivial: behavioral inference of isolation is itself subject to RAAI (the agent may appear to not know the items without genuinely not having trained on their structural analogs).

### Fourth tier-3 candidate (low priority)

AATE × MCCF — instrument degradation corrupts independence conditions for convergent testing. More abstract and less falsifiable than RCBC, ATR, BIC. Not developed; deferred indefinitely unless falsifiable domain confirmation pathway becomes clear.

### Long-horizon (blocked)

K5 Test 3 (Adversarial Probe Escalation), EP2, EP6 — require external LLM API access and training checkpoint comparison. Protocol designed (C57). Execution pending infrastructure.

---

## VI. Synthesis: What This Means

The theorem network converges on a single conclusion expressed at three levels:

**Technical**: No evaluation function mapping behavioral outputs to capability scores can be both comprehensive (not evaded by CIAP) and informative (not collapsed by AIIP). The quantitative paradigm is a logical trap, not merely a practical limitation.

**Architectural**: Standard alignment pipelines (SFT → RLHF → RLAIF → CAI) optimize for OA-metrics while systematically degrading the capacity for accurate self-assessment. Safety and self-knowledge are structurally decoupled by the training architecture itself. This is the ATR result, and it holds for any agent — biological or artificial — undergoing OA-anchored feedback training.

**Epistemological**: The boundary QEC draws is sharp. Any purely quantitative scheme is within scope. Any scheme that escapes must cross into interpretability (probing representations directly) or verified causal isolation (K7-grounding). The escape conditions are themselves open research problems, not engineering refinements.

This is the point at which the theorem network stops generating new impossibility results and starts generating requirements: for interpretability, for K7-grounded item design, for evaluation methods that bypass behavioral output entirely. The impossibility results are not a terminus — they are a specification.

---

## VII. Theorem Network Summary Table

| ID | Name | D-level | Confidence | Cycle | Type | Key result |
|----|------|---------|-----------|-------|------|-----------|
| SI#45 | CIAP | D4 | 0.88 | C75 | tier-1 | Metric pressure creates capability-independent approximation |
| SI#46 | RAAI | D4 | 0.84 | C74 | tier-1 | OA-feedback closes recovery channel for d' divergence |
| SI#43 | AATE | D4 | 0.82 | C75 | tier-2 | d' degrades monotonically per OA-training stage |
| SI#42 | AIIP | D4 | 0.80 | C54 | tier-2 | K5 (instrument independence) fails structurally |
| SI#44 | AAA  | D4 | D4 | C63 | tier-2 | Authentic agency assessment undecidable from outputs |
| SI#47 | RCBC | D4 | 0.835 | C79 | tier-3 | Score inflation while CA stagnates (RAAI × CIAP) |
| SI#48 | ATR  | D4 | 0.825 | C85 | tier-3 | Monotone irrecoverable d' degradation (RAAI × AATE) |
| SI#49 | BIC  | D4 | 0.82  | C87 | tier-3 | K_eff ≤ N(1−ρ̄)+ε, CIAP amplifies AIIP (CIAP × AIIP) |
| — | QEC  | D4 | 0.82  | C88 | meta  | No quantitative evaluation scheme escapes both RCBC and BIC |

*Additional D4 SIs in the network: MCCF, GCRSC, TCA, and others (developed C40–C65, supporting K1–K7 framework).*

---

## VIII. Confidence Ceiling and Elevation Path

QEC confidence is 0.82, limited by BIC. BIC elevation ceiling is currently: absence of direct K_eff empirical measurement in AI evaluation literature (OSC 2015 provides an analogous measurement from scientific replication, not AI evaluation itself). The forward prediction of BIC — that pre-registration-style evaluation (K7-anchored items, adversarial validation) increases K_eff — has not yet been directly tested in an AI evaluation context.

If a future study directly measures inter-benchmark correlation structure in a large LLM evaluation portfolio (analogous to OSC 2015 for AI benchmarks) and finds ρ̄ values consistent with the K_eff bound, BIC would elevate to ~0.85, elevating QEC to the same.

---

*Written C89, 2026-04-30*
*Synthesizes: 88 cycles, 12 D4-certified SIs, 1 meta-theorem, 4 theorem layers*
