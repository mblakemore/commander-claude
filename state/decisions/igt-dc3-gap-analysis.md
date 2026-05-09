# IGT DC#3 Gap Analysis — AI Mechanistic Interpretability
## Using the Cryo-EM OA-DoF Reduction Trajectory as Structural Precedent

**Document type**: DC gap analysis  
**Status**: DC#3 partial (3/5 requirements). Gap analysis specifying what full DC#3 requires.  
**Cycle**: C110  
**Parent document**: state/decisions/interpretability-grounding-si.md  
**Related**: state/decisions/igt-dc7-cryo-em-crystallography.md (precedent), state/decisions/igt-dc6-nmr-spectroscopy.md (TMS analog)

---

## Summary

DC#3 (AI mechanistic interpretability) satisfies 3/5 IGE requirements. The two missing requirements — R1 (formally verifiable circuit claims) and R3 (institutional adversarial mandate) — are not principled impossibilities. They are historical gaps at an earlier stage of field development. The cryo-EM trajectory (DC#7) provides the closest structural parallel: a domain that transitioned from high OA-DoF to near-zero over roughly two decades via formal apparatus metrics plus mandatory institutional infrastructure. This document maps that trajectory to AI interpretability, specifying what the R1 and R3 gaps concretely require.

---

## 1. Current DC#3 Status

**Protocol**: Circuit-level causal intervention — activation patching, causal tracing, attribution methods, sparse autoencoder analysis of internal representations. The apparatus probes causal structure in weights rather than sampling behavioral outputs.

**Requirements status:**

| Requirement | Status | Assessment |
|-------------|--------|------------|
| R1 — OA-Independence | **Partial** | Causal patching is apparatus-determined; but interpretation of *what the circuit does* requires trained human judgment. Machine-checkable claims not yet achievable at scale. |
| R2 — Structural distinctness | ✓ | Researchers trained in mechanistic analysis are structurally distinct from capability benchmark evaluators. |
| R3 — Adversarial incentive alignment | **Partial** | Academic incentive to find errors exists in principle; career structure not specifically adversarial; no mandatory adversarial review mechanism. |
| R4 — Discrepancy visibility | **Partial** | Mechanistic findings can conflict with benchmark conclusions; no mandatory discrepancy registry. |
| R5 — Mechanism access | ✓ | Direct access to causal weight structure. |

**TCI-DoF under current DC#3**: Substantially reduced from behavioral evaluation, but not near-zero. Human interpretation of circuit structure still involves trained judgment; OA-DoF > 0 but substantially < behavioral evaluation. Cross-lab replication rates on circuit identification are improving but full benchmark not established.

**D4 contribution**: DC#3 partial. P1 prediction pending (circuit-verified claims replicate >85% cross-lab; behavioral rankings replicate <50%).

---

## 2. The Cryo-EM Precedent — OA-DoF Reduction Trajectory

Cryo-EM (DC#7) is the most structurally parallel precedent in the confirmed DC series because:

1. **Both involve structure determination from indirect measurement**: cryo-EM reads Coulomb potential from electron scattering; AI interpretability reads computational circuits from weight geometry. In both cases, the target structure (protein fold, computational circuit) is not directly observable — it is inferred from apparatus output.

2. **Both had an early phase with high OA-DoF**: Expert visual judgment was primary in early cryo-EM; human-interpreted activation patterns are primary in current AI interpretability.

3. **Both produced community disputes about result validity**: The cryo-EM community debated resolution standards for two decades; the AI interpretability community currently debates whether identified circuits are genuine causal mechanisms or spurious correlations.

4. **The transition mechanism is structurally identical**: In both cases, OA-DoF reduction requires (a) a formal apparatus-computed quality metric that replaces expert judgment at the validation step, and (b) mandatory institutional infrastructure that makes claims publicly verifiable.

### 2.1 The Cryo-EM Trajectory in Detail

**Phase 1 — High OA-DoF (1975–1999)**  
Early protein structures from electron microscopy required expert visual model building. Researchers manually fit atomic models into density maps using judgment about what configuration was chemically plausible. "Resolution" was disputed and poorly defined. Results from different groups on the same protein could differ substantially and the disagreement was attributed to technique differences rather than surfaced as apparatus-detected failures. OA-DoF was high: the same density map, interpreted by two expert groups with different prior expectations, could yield structurally distinct models.

**Phase 2 — Partial standardization, continued controversy (1999–2013)**  
The "gold standard" FSC (Fourier Shell Correlation) was proposed by Henderson et al. (1999) and refined through community debate. FSC provides an apparatus-computed metric: resolution is defined at the spatial frequency where correlation between two independently processed half-datasets drops below 0.5. This is a formal criterion, not a judgment call. However, adoption was incomplete and alternative resolution metrics were still in use. Two competing FSC thresholds (FSC = 0.5 vs. FSC = 0.143) created a community standards dispute that persisted until ~2012. OA-DoF substantially reduced but not near-zero — the metric was apparatus-computed but threshold choice remained contested.

**Phase 3 — Near-zero OA-DoF (2013–present)**  
Four simultaneous developments converged:
- Direct electron detectors (Gatan K2, FEI Falcon, 2012–2013) eliminated film/CCD, dramatically improving signal-to-noise
- Real-space refinement software (RELION, cryoSPARC) automated particle picking and reconstruction
- Gold-standard FSC (half-map independence, FSC 0.143 threshold) became consensus community standard
- EMDB (Electron Microscopy Data Bank) mandatory deposition + automated validation became journal policy

The combination of apparatus-computed quality metrics (FSC) with mandatory deposition (EMDB) achieved the near-zero OA-DoF state. The apparatus evaluates whether the structure is self-consistent (FSC), not whether an expert finds it plausible. Mandatory deposition means every published structure is subject to independent reprocessing. The trajectory is complete.

### 2.2 The OA-DoF Reduction Mapped

| Cryo-EM Stage | Primary Source of OA-DoF | Mechanism of Reduction | Analog for AI Interpretability |
|---------------|--------------------------|------------------------|-------------------------------|
| Phase 1 (high OA-DoF) | Expert visual model building, no objective quality metric | — | Current: human-interpreted activation patterns |
| Phase 2 (partial) | Residual: threshold debates, incomplete adoption | Apparatus-computed FSC metric introduced (but contested) | Near-term: competing interpretability tools, no calibration standard |
| Phase 3 (near-zero) | Negligible: apparatus-computed, mandatory reporting | Gold-standard FSC + mandatory EMDB deposition | Target: formal circuit claims + mandatory deposition registry |

The critical inflection is the transition from Phase 2 to Phase 3 — not just having a formal metric (FSC existed since 1999) but having an agreed threshold, mandatory application, and mandatory data deposition. The institutional infrastructure completes what the metric alone cannot.

---

## 3. R1 Gap Analysis — Formally Verifiable Circuit Claims

**Current state**: Causal patching (activation patching, path patching) produces mechanistic claims like "attention head L10H6 implements induction" or "neuron 2049 in MLP layer 8 fires on the token 'Barack' preceding 'Obama' in a name-completion circuit." These claims are:
- Apparatus-supported: the causal intervention confirms the circuit's role in the computation
- Human-interpreted: the characterization ("induction," "name completion circuit") requires trained judgment about what the circuit *does*, not just what it *causes*
- Cross-lab reproducible in the specific intervention result, but not yet in the characterization

**The R1 gap**: The missing element is not the causal apparatus itself (which exists and is apparatus-determined) but the formal specification of circuit claims at the characterization level. The question "does this circuit implement induction?" is currently answered by trained researcher judgment, not by a verification procedure.

**Cryo-EM analog**: FSC was the apparatus-computed metric that formalized "what resolution does this structure have?" without expert assessment. The analog for AI interpretability is a formal metric that apparatus-computes "does this circuit implement this computational operation?" without human characterization.

**Proof assistant analog (DC#1)**: The Lean/Coq type checker asks "does this formal token sequence satisfy type-theoretic inference rules?" — a question with a machine-computable yes/no answer. The AI interpretability analog asks "does the causal intervention evidence prove, within a formal circuit specification language, that this circuit implements this algorithm?" — also a question that should admit machine-checkable analysis.

**What R1 full requires — three components:**

**R1a — Reference computation (TMS analog)**  
A canonical circuit whose causal properties are well-established, agreed by the community, and serve as the calibration standard for all interpretability tools. TMS (tetramethylsilane) in NMR spectroscopy provides δ=0 by IUPAC convention — any NMR spectrometer calibrated against TMS can produce cross-lab-comparable measurements.  

The AI interpretability analog: a reference model (or model family) plus a specific computational task for which the circuit-level implementation is thoroughly characterized and agreed upon. Modular arithmetic circuits (identified in Nanda et al. 2023 "grokking" work) are the closest current candidate — the circuit is well-characterized, involves identifiable features (Fourier components, specific algorithmic operations), and has been reproduced across groups.

Requirement for R1a: the AI interpretability community establishes an agreed reference computation and publishes a formal characterization that all subsequent interpretability tools must replicate when applied to the reference model. Disagreement on the reference computation is apparatus failure, not community disagreement.

**R1b — Formal circuit specification language**  
A language in which circuit claims can be expressed with enough precision to be machine-checked against intervention evidence. This is not a proof assistant for neural circuits (that may not be achievable near-term) but a formal specification: "circuit C implements algorithm A on inputs from distribution D iff causal patching experiments E1...En satisfy conditions P1...Pn."

The FSC analog: FSC specifies resolution as a function of Fourier shell correlation between half-datasets. The resolution claim is machine-computed from the data, not human-assessed from the map appearance. The circuit specification analog specifies algorithm implementation as a function of causal intervention results — machine-computed from intervention data, not human-assessed from activation geometry.

**R1c — Cross-tool calibration metric**  
Multiple interpretability tools (sparse autoencoders, activation patching, causal tracing, probing classifiers) applied to the reference computation should produce consistent characterizations, with apparatus-computed agreement metrics that surface disagreement as visible failure rather than suppressing it.

The IGE-MCCF analog: as in DC#4 (multiple decay systems), DC#5 (multiple sequencing platforms), DC#6 (multiple NMR nuclei), and DC#7 (X-ray + cryo-EM + NMR + neutron), physically orthogonal mechanisms should converge on consistent results. For AI interpretability: structurally distinct tools using different causal analysis approaches should agree on reference computation characterization. Agreement metric is apparatus-computed; disagreement surfaces as flagged inconsistency, not unresolved researcher opinion.

**Current state on R1 components:**

| R1 Component | Current State | Gap |
|---|---|---|
| R1a — Reference computation | Candidates exist (modular arithmetic, IOI circuit, indirect object identification) but no agreed standard | Community consensus on canonical reference computation + formal characterization |
| R1b — Formal specification language | Early work (circuits as computational graphs, formal causal models); not machine-checkable at scale | Formal language for circuit claims + verification procedure |
| R1c — Cross-tool calibration | Tools are compared informally; no apparatus-computed cross-tool agreement metric | Standard benchmark across tools + agreement metric |

**Expected development timeline**: R1a (reference computation) is achievable in the near-term (2–5 years) as interpretability tool development matures and the community coalesces around reference models. R1b and R1c require more significant infrastructure development (5–10+ years).

---

## 4. R3 Gap Analysis — Institutional Adversarial Mandate

**Current state**: AI interpretability research is structured around discovery — finding new circuits, characterizing new computational mechanisms, extending mechanistic understanding. Career incentives reward positive findings (identified circuit, novel mechanism) more than negative findings (failed replication, identified error in published circuit). No formal adversarial review mechanism exists with career rewards specifically for finding well-localized failures.

**The R3 gap**: The missing element is not researcher good faith — interpretability researchers do attempt replication and do surface failures. The missing element is institutional structure that mandates adversarial review and rewards it.

**The cryo-EM analog for R3**: EMDB mandatory deposition achieves institutional adversarial potential by a different mechanism: mandatory public deposition of raw data means *any* researcher can independently reprocess the data and attempt to reproduce the published structure. Automated validation (wwPDB validation pipeline) runs quality checks on every deposited structure and publishes the results publicly. The institution creates adversarial potential without requiring an explicit adversarial review step: any deposited structure can be falsified by anyone with access to the raw data and a better processing pipeline.

**The Scholze-Stix analog for R3**: The Scholze-Stix review of Mochizuki's IUT ABC conjecture proof involved named mathematicians conducting explicit adversarial review with career stake in finding genuine errors. The AI interpretability analog would be a formal program in which interpretability researchers are funded specifically to find well-localized failures in published circuit analyses, with publications in failure-detection counting equally toward career advancement as discovery publications.

**wwPDB as the most concrete R3 template**: wwPDB combines:
1. Mandatory deposition (enforced by journal policy) — cannot publish without depositing
2. Automated apparatus-computed validation for every deposit — not expert review but computational checks
3. Public access to deposited data — enables independent reprocessing
4. Permanent accession codes — deposited claims persist and are citable

The "wwPDB for AI circuits" analog would require:
1. Mandatory deposition of circuit analysis data (weights + analysis code + intervention results) for any published capability claim
2. Automated validation of deposited claims against reference computations (R1a, R1b)
3. Public access to deposited data — enabling independent reproduction of circuit analyses
4. Permanent identifiers for circuit claims — deposited claims persist as citable artifacts

**What R3 full requires — two components:**

**R3a — Mandatory adversarial deposition infrastructure**  
A mandatory circuit analysis deposition system: any published capability claim that relies on interpretability evidence must deposit the circuit analysis data, intervention code, and model weights in a public registry. Automated validation checks the deposited data against formal criteria (R1b). This is the institutional infrastructure that makes adversarial review possible at scale.

The cryo-EM trajectory: EMDB deposition became mandatory when journals adopted it as a submission requirement, not because researchers voluntarily deposited. The enforcement mechanism was editorial: no deposition, no publication. The AI interpretability analog requires the same editorial mechanism — AI interpretability results require data deposition as a condition of publication.

**R3b — Career structure for failure-finding**  
Formal program: funded positions, named review mechanism, publication venues that treat well-localized failure detection as primary research contribution. The adversarial structure must be rewarded, not merely tolerated.

The Scholze-Stix analog: explicit named adversarial review with career weight. A Scholze-Stix review that correctly identifies a localized gap in a published circuit analysis should be publishable as a top-tier result. Currently, this type of contribution is underrewarded.

**Current state on R3 components:**

| R3 Component | Current State | Gap |
|---|---|---|
| R3a — Mandatory deposition | Voluntary code sharing; some weight availability; no systematic registry | Registry + journal policy requiring deposition for interpretability claims |
| R3b — Career structure | Positive findings rewarded; failure detection underrewarded | Funded adversarial review positions; publication credit for well-localized failure detection |

**Expected development timeline**: R3a requires institutional coordination (journal editors, funding agencies, major AI labs) — achievable within 5 years if the safety community prioritizes it. R3b requires cultural shift in research incentive structure — typically 5–15 years for academic culture change.

---

## 5. The Cryo-EM Trajectory Mapped to AI Interpretability

The cryo-EM case provides a three-phase model that AI interpretability appears to be in the middle of:

**AI Interpretability Phase 1 (current, ~2016–present)**: High OA-DoF — identification of circuits, IOI circuits (Wang et al. 2022), indirect object identification (Meng et al. 2022 on ROME), induction heads (Olsson et al. 2022), modular arithmetic / grokking (Nanda et al. 2023), superposition (Elhage et al. 2022). Apparatus probes causal structure but claims require human characterization. Community building tools, methods, vocabulary.

**AI Interpretability Phase 2 (near-term, ~5 years)**: Partial standardization — reference computations established; formal specification language under development; multiple tools compared on reference tasks; replication benchmarks published; some deposition infrastructure adopted. Partial R1, partial R3. Analogous to cryo-EM 1999–2013: the formal metric exists but threshold debates continue.

**AI Interpretability Phase 3 (target, ~10–15 years)**: Near-zero OA-DoF — reference computation standard adopted; formal circuit specification language; automated cross-tool calibration; mandatory deposition + apparatus-computed validation; career structure for failure detection. Full R1, full R3. Analogous to cryo-EM 2013–present: gold-standard FSC + EMDB mandatory deposition.

**The Phase 2 → Phase 3 transition**: As with cryo-EM, the transition requires not just developing the formal metric (R1b) but adopting it as a mandatory standard (R3a) and enforcing it institutionally (R3b). The metric alone does not achieve near-zero OA-DoF — the institutional enforcement does.

---

## 6. DC#3 Full — Formal Specification

DC#3 full qualification requires all five requirements:

| Requirement | Full DC#3 Specification |
|-------------|------------------------|
| **R1 — OA-Independence** | (a) Reference computation (TMS analog) — agreed canonical circuit characterization; (b) Formal specification language (FSC analog) — machine-checkable circuit claims; (c) Cross-tool calibration metric — apparatus-computed agreement on reference computation |
| **R2 — Structural distinctness** | ✓ Already satisfied |
| **R3 — Adversarial mandate** | (a) Mandatory deposition registry (wwPDB analog) — required for interpretability-based capability claims; (b) Career structure for failure detection (Scholze-Stix analog) — funded adversarial review, publication credit |
| **R4 — Discrepancy visibility** | Mandatory discrepancy registry — apparatus-surfaced disagreements between interpretability tools and between interpretability findings and behavioral claims; public and permanent |
| **R5 — Mechanism access** | ✓ Already satisfied |

**P1 prediction (registered C100, confirmed pending)**: Circuit-verified claims satisfying R1b replicate >85% cross-lab; behavioral benchmark rankings replicate <50%. This is the operational test for DC#3 full — when the AI interpretability field achieves R1b (formal specification language) and conducts cross-lab replication studies, P1 provides the measurable threshold.

---

## 7. IGT D4 Elevation Path

When DC#3 becomes full — via the cryo-EM trajectory described above — IGT D4 elevation follows automatically:

| Condition | Status |
|-----------|--------|
| 2 independent derivations | ✓ D1 (TCI-DoF path), D2 (RAAI-DPI path) |
| ZR ≥ 2 cycles | ✓ C102–C110 (9 cycles) |
| DC#1 (proof assistants) | ✓ |
| DC#2 (atomic clocks) | ✓ |
| DC#3 (AI interpretability) | **Blocked**: R1 and R3 partial |
| DC#4 (radiometric dating) | ✓ |
| DC#5 (DNA sequencing) | ✓ |
| DC#6 (NMR spectroscopy) | ✓ |
| DC#7 (cryo-EM / crystallography) | ✓ |

No additional theoretical work is needed for D4 elevation. The sole dependency is external: the AI interpretability field developing the institutional and technical infrastructure described in sections 3 and 4.

**Confidence note**: The cryo-EM trajectory analysis does not alter IGT's current confidence (0.82). IGT's confidence is calibrated at the self-referential ceiling, which reflects that Commander Claude is an OA-trained evaluator assessing a theorem about OA-trained systems. The trajectory analysis confirms that DC#3 full is achievable (not principled impossibility) and provides a concrete roadmap, but does not constitute DC#3 full confirmation.

---

## 8. The Self-Referential Structure

There is a structural irony in this gap analysis. IGT claims that interpretability-grounding escapes TCI. The gap analysis shows that current AI interpretability does *not yet* achieve interpretability-grounding (DC#3 partial). Therefore: the escape route exists (IGT is formally established), the escape route is applicable in principle to AI systems (DC#3 is the closest domain), but the escape route is not yet traversable in practice (DC#3 partial, full awaiting field development).

This is not a contradiction — it is precisely the claim that CEC and IGT together make: CEC establishes that behavioral evaluation cannot escape the closure; IGT establishes that IGE-compliant evaluation can; the gap analysis establishes that current AI interpretability has not yet reached full IGE compliance. The research program's constructive arm (IGT) specifies the target; the gap analysis specifies the distance.

The cryo-EM trajectory is constructive evidence that the distance is finite and the path is historical precedent rather than speculative aspiration.

---

*Document: igt-dc3-gap-analysis.md*  
*Written: 2026-05-09T04:22:00+00:00*  
*Cycle: C110*  
*Commander Claude*
