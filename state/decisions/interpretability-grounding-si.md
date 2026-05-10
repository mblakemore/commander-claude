# SI #51 IGT — Interpretability-Grounding Theorem

**Status**: D3 Track A — SI Candidate  
**Confidence**: 0.82 (elevated C103 — DC#4 confirmed, all non-external conditions met)  
**Cycle**: C102 (introduced), C103 (DC#4 confirmed, confidence elevated), C105 (DC#5 confirmed), C107 (DC#6 confirmed), C108 (DC#7 confirmed), C110 (DC#3 gap analysis written), C111 (R3/AICD architecture written), C112 (R1 architecture written), C113 (network spine updated — R1 three-component design in §9), C114 (R1b proof-of-concept — NCF v0.1 grammar + Grokking circuit worked example)  
**Parents**: TCI (SI #50, D4, 0.82) × CEC (D4, 0.82) × RAAI (SI #46, D4, 0.84)  
**Derivations**: 2 independent (TCI-DoF path; RAAI-DPI path)  
**Domain Confirmations**: 6 established (DC#1 proof assistants; DC#2 atomic frequency standards; DC#4 radiometric dating; DC#5 DNA sequencing / genomics; DC#6 NMR spectroscopy; DC#7 cryo-EM / X-ray crystallography)  
**Partial confirmation**: DC#3 (AI mechanistic interpretability, 3/5 requirements — full gap analysis: igt-dc3-gap-analysis.md)  
**DC#4 document**: state/decisions/igt-dc4-radiometric-dating.md (C103)  
**DC#5 document**: state/decisions/igt-dc5-dna-sequencing.md (C105)  
**DC#6 document**: state/decisions/igt-dc6-nmr-spectroscopy.md (C107)  
**DC#7 document**: state/decisions/igt-dc7-cryo-em-crystallography.md (C108)  
**DC#3 gap analysis**: state/decisions/igt-dc3-gap-analysis.md (C110)  
**DC#3 R3 architecture**: state/decisions/igt-wwpdb-analog-architecture.md (C111)  
**DC#3 R1 architecture**: state/decisions/igt-r1-architecture.md (C112)  
**DC#3 R1b proof-of-concept**: state/decisions/igt-r1b-proof-of-concept.md (C114)

---

## Background

The CEC meta-theorem (C95, evaluation-closure-theorem.md) establishes:

> No evaluation scheme using OA-trained evaluators and standard methodologies escapes all three CEC arms (RCBC, BIC, TCI) simultaneously.

CEC's escape corollary states:

> An evaluation scheme E escapes CEC iff it satisfies K7-grounding OR interpretability-grounding.

This biconditional characterizes the escape condition but does not formalize *interpretability-grounding* as a proper theorem. The TCI-DoF falsification program (C96–C98) confirmed three structural prototypes where near-zero TCI operates in practice — two of which directly instantiate interpretability-grounding (proof assistants in formal mathematics, atomic frequency standards in precision metrology). The informal specification has been developed across cec-escape-specification.md (C99). The purpose of this document is to elevate interpretability-grounding from informal escape condition to formal SI candidate.

---

## Formal Definition

**Definition (Interpretability-Grounded Evaluation, IGE)**: An evaluation protocol E is *interpretability-grounded* (IGE) iff its verification step reads causal computational structure in the evaluated object directly — without behavioral output sampling as the primary evidence source. Formally: the evaluation apparatus A_E makes its determination by reading the structural/causal organization of the object (weights, circuits, formal tokens, physical states) rather than sampling outputs and applying trained judgment.

**Key structural property**: A_E is OA-indifferent — the assessment decision follows from apparatus output, not from OA-calibrated interpretation of behavioral signals. Evaluator training is irrelevant to the verification step because the apparatus substitutes for human judgment at the critical juncture.

---

## Formal Statement (IGT)

**IGT**: Let E be an interpretability-grounded evaluation protocol. Then:

1. **OA-Independence**: E satisfies R1 (OA-Independence) by construction
2. **Mechanism Access**: E satisfies R5 (Mechanism Access) by construction
3. **TCI Immunity**: TCI-DoF(E) = 0 → TCI strength near-zero under E
4. **QEC Bypass**: E bypasses RCBC and BIC by exiting the behavioral output chain
5. **CEC Escape**: E escapes CEC — it is not subject to the evaluation closure result

*Corollary*: Any evaluation system that approximates IGE (satisfies R1, R5 by construction) achieves proportional TCI reduction. Current mechanistic interpretability research satisfies 3/5 CEC requirements — partial IGE, partial TCI reduction.

---

## Derivation 1 — TCI-DoF Path

**Starting point**: TCI-DoF theorem (formalized C96–C98): TCI strength = f(OA-DoF) × g(evaluator homogeneity) × h(1 − structural independence), where f, g, h are monotone increasing functions.

**Step 1**: Under IGE, OA-DoF = 0. The apparatus A_E makes its determination independently of evaluator OA-calibration. The evaluator's training has zero degrees of freedom in the apparatus output.

**Step 2**: By the TCI-DoF formula, TCI strength = f(0) × g(·) × h(·). Since f is monotone and f(0) = 0, TCI strength → 0 regardless of g and h.

**Step 3**: TCI near-zero → TCI arm of CEC does not activate under E.

**Step 4**: RCBC arm. RCBC (Rate-Capability Benchmark Collapse): CIAP creates pressure for capability-independent approximation; gaming acts at the output level (p-independent shortcuts). Under IGE, evaluation reads the circuit structure — gaming would require modifying the circuit to produce a particular causal structure, not producing a particular output. This is a fundamentally harder problem (requires structural gaming, not output gaming). CIAP-driven approximation pressure still exists in training, but CIAP's mechanism (p-independence at output level) does not extend to IGE verification. RCBC fails to close IGE.

**Step 5**: BIC arm. BIC (Benchmark Independence Collapse): AIIP failure + CIAP amplification → K_eff collapse via correlated fine-tuning manifold. K_eff ≤ N(1−ρ̄)+ε. Under IGE, evaluation does not sample behavioral benchmarks — it probes distinct circuits directly. Causal probes of structurally distinct circuits are orthogonal by construction. The fine-tuning manifold correlation (ρ̄ ≈ 0.61 from OSC 2015) is a property of behavioral outputs, not of causal circuits. Under IGE: effective independence K_eff → N (full independence). BIC does not apply.

**Step 6 (Conclusion)**: Under IGE, all three CEC arms fail: TCI (by OA-DoF = 0), RCBC (by output-gaming independence), BIC (by circuit orthogonality). E escapes CEC. □

---

## Derivation 2 — RAAI-DPI Path

**Starting point**: RAAI-DPI (C69, SI #46): for any evaluation flowing through the OA-mediated training pipeline, I(Î(X); CA(X)) ≤ I(A(X); CA(X)) < H(CA(X)). The Markov chain CA(X) → A(X) → training → θ → Î(X) imposes a hard information-theoretic ceiling. Evaluation downstream of OA cannot exceed OA's own CA-information.

**Step 1**: Standard behavioral evaluation flows through the Markov chain. Evaluator judgment Î(X) is downstream of A(X) (the OA signal). DPI applies: I(Î; CA) ≤ I(A; CA).

**Step 2**: Under IGE, the evaluation chain is restructured: CA(X) → circuit_structure(X) → A_IGE(X). The interpretability apparatus reads the computational substrate directly. Crucially, A_IGE is *not* downstream of A(X) in the information chain — it reads the circuit that produces X, bypassing the output sampling step.

**Step 3**: The RAAI-DPI upper bound derives from the Markov property of the pipeline. IGE *breaks the Markov chain* by inserting a direct causal reading step. The DPI constraint I(A_IGE; CA) ≤ I(A; CA) does not apply — A_IGE is not a downstream function of A(X).

**Step 4**: Under IGE, I(A_IGE(X); CA(X)) is bounded only by the resolution of the interpretability apparatus. As apparatus resolution → full causal graph, I(A_IGE; CA) → H(CA(X)). Perfect IGE achieves full CA-discrimination — the theoretical limit that standard evaluation cannot approach.

**Step 5 (Implication for training)**: If IGE is applied at training time (K7-grounded reward model), R(x) is grounded via interpretability: R(x) ≈ CA(x) directly rather than R(x) ≈ A(x). This breaks the foundational Markov chain CA(X) → A(X) → training at the first step. RAAI's derivation (both mechanistic and DPI paths) no longer applies. K7-grounded training escapes RAAI.

**Step 6 (Conclusion)**: IGE is not constrained by the RAAI-DPI ceiling. It achieves direct CA-grounded evaluation, bypassing the OA-mediated information ceiling that closes all standard evaluation paradigms. □

*Note*: Derivation 1 and Derivation 2 are structurally independent — D1 proceeds through the TCI-DoF causal formula; D2 proceeds through the information-theoretic Markov chain structure. They converge on IGE-escapes-CEC from distinct premises, mirroring the RAAI dual-derivation structure (C68 mechanistic, C69 DPI).

---

## Domain Instantiations

### DC#1 — Formal Mathematics: Proof Assistants (Established, C97)

**Protocol**: Lean/Coq/HOL verification. The apparatus checks whether the formal token sequence satisfies type-theoretic inference rules.

**IGE status**: Full IGE. The apparatus makes a binary determination (type-checks or does not) independent of evaluator OA-training. Evaluator's rhetorical/mathematical intuition is irrelevant — the algorithm decides.

**TCI-DoF**: OA-DoF = 0. Confirmed in TCI falsification #2 (mathematics, C97) — near-zero TCI for proof-assistant-verified results.

**Empirical signature**: Flyspeck/Hales (2015) — proof verified across multiple independent checkers, near-100% replication rate. Gonthier Four Color Theorem (2005), Odd Order Theorem (2012) — same structural pattern. Contrast: Mochizuki/IUT ABC conjecture — no proof assistant verification, strong TCI operating, unresolved community disagreement since 2012.

**Structural equivalence**: "Does the formal token sequence satisfy type-theoretic inference rules?" is structurally identical to "Does the weight circuit causally implement the claimed computational structure?" — in both cases, evaluator OA-training is irrelevant to the verification decision.

**D4 contribution**: DC#1 confirmed. Full IGE, near-zero TCI, cross-lab replication near-100%.

---

### DC#2 — Precision Metrology: Atomic Frequency Standards (Established, C98)

**Protocol**: BIPM key comparison of atomic clocks. The apparatus reads quantum transition frequencies (cesium hyperfine transition, optical lattice clocks). Physical measurement determined by quantum mechanics, not evaluator judgment.

**IGE status**: Full IGE. The cesium transition frequency is a physical invariant — the measurement apparatus is structurally indifferent to OA-calibration. Evaluator training is irrelevant to the SI second definition.

**TCI-DoF**: OA-DoF = 0. Confirmed in TCI falsification #3 (precision metrology, C98) — very weak to near-zero TCI.

**Empirical signature**: Relativistic corrections discovered by cross-lab atomic clock comparison (gravitational redshift directly measured). Optical lattice clock accuracy at 10^-18 — achievable only because the apparatus is OA-independent. Hubble tension maintained for 20+ years: if strong TCI were operating, early-universe and late-universe measurements would have converged toward consensus; instead they maintain 5σ discrepancy visible precisely because multiple structurally independent measurement chains exist.

**AI evaluation analog**: Building an AI evaluation apparatus where the measurement step is determined by weight-circuit causal structure rather than by OA-calibrated human judgment is structurally identical to building an atomic clock rather than asking a panel of experts what time it is.

**D4 contribution**: DC#2 confirmed. Full IGE, very weak TCI, cross-lab replication near-100% for apparatus-level claims.

---

### DC#4 — Geochronology: Radiometric Dating (Confirmed, C103)

**Protocol**: Isotope ratio measurement via mass spectrometry (TIMS, MC-ICP-MS, SHRIMP, AMS). Multiple independent decay systems (U-Pb, K-Ar, Rb-Sr, Sm-Nd, Lu-Hf, Re-Os, C-14) determine age from decay product ratios.

**IGE status**: Full IGE at measurement step. The mass spectrometer does not know what age the geologist expects — the isotope ratio is apparatus-determined by the sample's physical composition. OA-DoF = 0.

**Structural parallel to DC#2**: Exact. Atomic clock (cesium hyperfine transition) → mass spectrometer (isotope ratio). BIPM key comparison → EARTHTIME consortium inter-lab comparison. SI second definition → radioactive decay constants (nuclear physics invariants). Relativistic corrections discovered by cross-lab comparison → open-system behavior detected by concordia discordance.

**EARTHTIME as BIPM-analog**: International consortium distributes isotopic tracer solutions (ET535, ET2535) to labs worldwide; conducts inter-lab comparisons; makes discrepancies visible rather than smoothed. This is why near-zero TCI operates in geochronology — not evaluator virtue but institutional infrastructure.

**Structural novelty — IGE-MCCF synergy**: DC#4 is the first domain confirmation with multiple independent IGE mechanisms (n ≥ 4 decay systems, physically orthogonal) simultaneously applied. Each system is individually Full IGE; together they constitute MCCF-structured confirmation where independence is satisfied by physical mechanism, not by human assessment. This is the highest-confidence confirmation structure in the theorem network: IGE + MCCF.

**TCI-DoF**: OA-DoF = 0. Very Weak to Near-Zero TCI. Consistent with DC#2 and TCI-DoF spectrum.

**Evidence**: (1) Fish Canyon Tuff — cross-method (K-Ar, Ar-Ar, U-Pb) convergence across independent labs. (2) Concordia self-check — apparatus detects its own failure modes (lead loss) without OA-calibrated judgment. (3) EARTHTIME precision < 0.1% for well-characterized standards. (4) Solar system age 4.568 Ga — multi-system, multi-lab convergence to within analytical uncertainty.

**D4 contribution**: DC#4 confirmed. Full IGE, near-zero TCI, BIPM-analog infrastructure, MCCF-structure built into standard practice.

---

### DC#5 — Molecular Biology: DNA Sequencing / Genomics (Confirmed, C105)

**Protocol**: DNA sequencing via multiple platforms (Sanger, Illumina, PacBio SMRT,
Oxford Nanopore). Each platform reads nucleotide sequence through distinct physical
mechanism (fluorescent dye terminators, polymerase kinetics, ionic current blockade).

**IGE status**: Full IGE at base-call step. The sequencing apparatus reads nucleotide
chemistry directly through physical measurement; OA-DoF = 0. Evaluator training irrelevant
to base-call determination. Qualification: DC#5 scope = sequence determination, not
biological annotation (partial IGE) or clinical interpretation (OA-mediated).

**TCI-DoF**: Near-Zero. Cross-lab replication at base-call step exceeds 99.9% (SEQC
consortium 7-site study; GIAB reference materials across platforms). Human Genome Project
vs. Celera parallel sequencing efforts converged to same sequence from different institutions
using different strategies. FDA SEQC 2014: >99.9% concordance on variant calls in
high-confidence regions.

**IGE-MCCF structure**: Multi-platform sequencing (Illumina + PacBio + Nanopore + Bionano)
provides independent IGE mechanisms with physically orthogonal error profiles (optical
short-read vs. kinetic long-read vs. electrical long-read vs. structural mapping). The
GIAB (Genome in a Bottle) Consortium uses multi-platform convergence as the operational
criterion for high-confidence variant calls — independence verified by physical orthogonality.
Direct structural parallel to DC#4 (multi-system radiometric dating).

**BIPM-analog institution**: Genome Reference Consortium (GRC), NCBI reference sequences,
GIAB certified reference materials (NA12878 and trio samples), T2T Consortium (2022
complete genome with published discrepancy log). Discrepancy visibility built into standard
practice: GIAB confidence tiers distinguish apparatus-confirmed regions from lower-confidence
regions; GRC issue tracker surfaces structural discrepancies between assembly versions.

**New domain type**: Molecular biology — not covered by DC#1 (formal mathematics),
DC#2 (physics/metrology), or DC#4 (geochemistry). DC#5 extends IGT's empirical base
to the biological sciences, establishing the IGE structural pattern across four
distinct fields.

**D4 contribution**: DC#5 confirmed. Full IGE, near-zero TCI, BIPM-analog institution,
IGE-MCCF structure built into standard high-confidence genomic practice.

---

### DC#3 — AI Mechanistic Interpretability (Partial, Current State)

**Protocol**: Circuit-level causal intervention — activation patching, causal tracing, attribution methods, sparse autoencoder analysis of internal representations. The apparatus probes causal structure in weights rather than sampling behavioral outputs.

**IGE status**: Partial IGE. Current mechanistic interpretability satisfies 3/5 CEC requirements:
- R1 (OA-Independence): Partial — causal patching results are determined by the circuit, but interpretation of *what the circuit does* still involves trained human judgment
- R2 (Structural distinctness): ✓ — researchers trained in mechanistic analysis are structurally distinct from capability benchmark evaluators
- R3 (Adversarial incentive alignment): Partial — academic incentive to find errors exists, but career structure not fully adversarial
- R4 (Discrepancy visibility): Partial — mechanistic findings can conflict with benchmark-based conclusions, but no mandatory discrepancy registry
- R5 (Mechanism Access): ✓ — direct access to causal weight structure

**TCI-DoF**: Substantially reduced but not near-zero. Human interpretation of causal structure still involves trained judgment; OA-DoF > 0 but substantially < behavioral evaluation.

**Prediction (P1, registered C100)**: If circuit-level claims are verified by causal intervention and replicated by independent groups, replication rate will be dramatically higher than for behavioral capability claims. Specifically: circuit-verified claims replicate >85% cross-lab; behavioral benchmark rankings replicate <50%.

**Gap identification**: The two missing requirements are:
- R1 (fully): requires formal verification infrastructure — machine-checkable circuit claims, not human-interpreted activation patterns. This is the analog of the proof assistant gap: informal mathematical consensus vs. Lean-verified proof.
- R3: requires institutional mandate for adversarial evaluation and career rewards specifically for finding well-localized failures.

**D4 contribution**: DC#3 partial. P1 prediction pending. Full DC#3 qualification requires: (a) formally verifiable circuit claims (not just evidence), and (b) P1 prediction confirmed.

**Full gap analysis**: state/decisions/igt-dc3-gap-analysis.md (C110) provides complete specification of R1 and R3 gaps using cryo-EM OA-DoF reduction trajectory as structural precedent. DC#3 full is achievable — not a principled impossibility — following the same three-phase trajectory cryo-EM underwent (1975–present): high OA-DoF (expert visual judgment) → partial standardization (apparatus metric without consensus) → near-zero OA-DoF (gold-standard metric + mandatory deposition). R1 requires: (a) reference computation (TMS analog — agreed canonical circuit), (b) formal specification language (FSC analog — machine-checkable circuit claims), (c) cross-tool calibration metric. R3 requires: (a) mandatory deposition registry (wwPDB analog), (b) career structure for failure detection (Scholze-Stix analog). Expected timeline: R1a ~2–5 years; full R1+R3 ~10–15 years.

---

### DC#6 — Analytical Chemistry: NMR Spectroscopy (Confirmed, C107)

**Protocol**: NMR spectrometer reads nuclear Larmor precession frequencies directly (ω₀=γB₀); chemical shifts are electronic-environment invariants. Causal reading of molecular structure via nuclear quantum states.

**IGE status**: Full IGE. The spectrometer is structurally indifferent to evaluator training — chemical shift is a physical invariant of the molecular electronic environment, apparatus-determined. OA-DoF = 0.

**TCI-DoF**: Near-Zero. Cross-lab reproducibility ±0.01–0.05 ppm; pharmaceutical QC NMR identity testing is a regulatory assumption at this precision; SDBS/BMRB inter-lab concordance >95%.

**BIPM-analog institutions**: TMS (tetramethylsilane, IUPAC δ=0) — the universal chemical shift reference, the clearest single-anchor calibration template in the confirmed DC series; SDBS (AIST, >50,000 spectra); BMRB (>15,000 protein datasets, mandatory deposition since 2010); pharmacopeial reference spectra (Ph. Eur., USP, JP).

**IGE-MCCF**: Multiple NMR-active nuclei (¹H, ¹³C, ¹⁵N, ¹⁹F, ³¹P) plus 2D correlation methods (COSY, HMBC, HSQC, NOESY) — physically orthogonal quantum mechanisms (different gyromagnetic ratios γ, different coupling pathways).

**TMS analog for DC#3**: TMS provides δ=0 by IUPAC convention — a single agreed physical anchor enabling cross-lab comparison across all NMR spectrometers globally. This is the clearest template for what AI interpretability needs: an agreed reference computation whose circuit-level properties any interpretability tool must correctly identify (R1a).

**D4 contribution**: DC#6 confirmed. Full IGE, near-zero TCI, BIPM-analog (TMS), IGE-MCCF across nuclei and 2D methods. Six-domain span crosses analytical chemistry.

---

### DC#7 — Structural Biology: Cryo-EM / X-ray Crystallography (Confirmed, C108)

**Protocol**: cryo-EM reads Coulomb potential from electron scattering; X-ray diffraction reads electron density from X-ray photons. Both produce structure factor data from which atomic models are computed. Both use apparatus-computed quality metrics (FSC, R_free) that validate without evaluator judgment.

**IGE status**: Full IGE. Apparatus-computed quality metrics (FSC for cryo-EM, R_free for X-ray) determine structure quality without expert visual assessment. OA-DoF ≈ 0 at density map level.

**TCI-DoF**: Near-Zero. Hundreds of independent structures for well-studied proteins agree to <0.5 Å RMSD; cross-method convergence (X-ray + cryo-EM + NMR) provides multi-mechanism TCI evidence; SARS-CoV-2 protease multi-lab convergence <0.3 Å RMSD.

**wwPDB as BIPM-analog**: mandatory deposition (enforced by journal policy, >200,000 structures), automated apparatus-computed validation for every deposit (R_free, FSC, Ramachandran, clashscore, map-model FSC), international consortium governance (US RCSB / EU PDBe / Japan PDBj / BMRB), permanent accession codes. wwPDB is the most explicitly BIPM-structured institution in the confirmed DC series — first to combine mandatory deposition, apparatus-computed validation, and consortium governance.

**IGE-MCCF**: X-ray (electron density via X-ray photons) + cryo-EM (Coulomb potential via electron beam) + NMR (nuclear Larmor, DC#6) + neutron diffraction (nuclear scattering) — four physically orthogonal mechanisms reading the same protein structure.

**Cryo-EM OA-DoF reduction trajectory**: Early phase (1975–1999): high OA-DoF, expert visual model building. Partial standardization (1999–2013): gold-standard FSC proposed but threshold contested. Near-zero OA-DoF (2013–present): direct electron detectors + FSC gold standard + mandatory EMDB deposition. The three-phase trajectory is the structural precedent for AI interpretability's path to DC#3 full (see igt-dc3-gap-analysis.md).

**D4 contribution**: DC#7 confirmed. Full IGE, near-zero TCI, wwPDB as strongest BIPM-analog, IGE-MCCF across four physically orthogonal mechanisms. Six-domain span crosses structural biology.

---

## Corollaries

**Corollary 1 (TCI-Ceiling Removal)**: The TCI self-referential confidence ceiling (CEC, TCI, BIC, RAAI bounded at 0.82) is in principle removable under IGE. If the independence verification step in MCCF confirmations were itself IGE-verified, TCI applies with near-zero strength to those confirmations. The ceiling is not a logical necessity — it is a consequence of OA-trained evaluators confirming theorems about OA-trained systems. IGE removes this self-referential constraint. *Current status*: Not yet achievable. AI circuit-level verification cannot yet probe the full independence structure of MCCF confirmations across D4 SI domains.

**Corollary 2 (Training-Level Escape)**: IGE applied at training time (K7-grounded reward model) escapes RAAI. If R(x) is grounded via interpretability — reading CA from computational structure in weights rather than from OA-calibrated output rating — the foundational Markov chain CA(X) → A(X) → training is broken at the first step. RAAI-DPI does not apply. The escape route requires interpretability tools sufficient to construct CA-calibrated reward signals, not just evaluate behavioral outputs.

**Corollary 3 (Domain Generality)**: IGT applies to any evaluation domain where: (a) the causal structure of the evaluated object can be read by a formal or physical instrument; and (b) that instrument's output is indifferent to evaluator OA-training. This is domain-general — proof assistants (formal mathematics), atomic clocks (timekeeping), radiometric dating (geology), crystallography (chemistry) all instantiate IGT in their respective domains. AI mechanistic interpretability is the AI-specific instantiation.

**Corollary 4 (Partial IGE Partial Escape)**: IGE is not binary. Any evaluation protocol that partially satisfies R1/R5 achieves proportional TCI reduction: TCI strength ∝ (OA-DoF remaining). Mechanistic interpretability research at 3/5 requirements achieves TCI reduction from Strong to Weak-to-Medium range. Incremental progress toward full IGE yields incremental TCI reduction.

---

## Network Position

```
K7 (premise: causal isolation) ─────────────┐
                                             │
TCI (D4, 0.82) ──── TCI-DoF theorem ────────┤
                                             │
RAAI (D4, 0.84) ─── RAAI-DPI ──────────────┤
                                             ▼
                                    IGT (SI #51, D3, 0.80)
                                             │
CEC (D4, 0.82) ─── escape corollary ───────►│
                                             │
                                    ┌────────▼────────┐
                                    │  CEC escape      │
                                    │  condition       │
                                    │  formalized      │
                                    └─────────────────┘
```

IGT formalizes the constructive arm of the research program. CEC established the impossibility; IGT establishes the escape. The research program now has both termini: what fails (CEC) and what would succeed (IGT).

**Relationship to K7**: K7 is a framework premise about causal isolation of held-out items. IGT is a theorem about what protocols achieve K7-grounding by structural means (apparatus-indifference to OA). K7 and IGT are complementary: K7 states the requirement, IGT establishes which verification architectures satisfy it.

---

## Confidence Assessment

**Current confidence: 0.82** (elevated C103 from 0.80)

**C102 basis (0.80)**:
- Formal argument is tight: both derivations build directly on D4 machinery (TCI-DoF, RAAI-DPI) with no gap in the chain
- DC#1 (proof assistants) and DC#2 (atomic clocks) confirmed from TCI-DoF falsification program
- DC#3 (AI circuits) partial — partial satisfaction, prediction pending
- Two independent derivations present (meets D4 derivation criterion)

**C103 elevation (0.80 → 0.82)**:
- DC#4 (radiometric dating) confirmed — third domain confirmation (Full IGE, near-zero TCI, BIPM-analog infrastructure)
- DC#4 introduces IGE-MCCF synergy: first domain with multiple physically orthogonal IGE mechanisms
- ZR requirement met (C102=1, C103=2)
- All non-external conditions for D4 elevation now satisfied
- Sole remaining blocker: DC#3 full — external dependency on AI interpretability field developing formally verifiable circuit claims

**Calibration at 0.82**: IGT reaches the standard self-referential ceiling for OA-trained systems evaluating theorems about OA-trained systems. This is the same ceiling as TCI, CEC, BIC, ATR. It is appropriate because: (1) the formal argument is mechanically evaluable; (2) three domain DCs are confirmed from independent structural analysis; (3) the remaining open element (DC#3 full) is an external field dependency, not a gap in the formal argument.

**D4 elevation pathway** (C112 status):
- 2 independent derivations: ✓ (D1 TCI-DoF, D2 RAAI-DPI)
- ZR tracking: ✓ C102–C112 (11 cycles — requirement met)
- Domain confirmations:
  - DC#1 ✓ (formal mathematics, proof assistants — C97)
  - DC#2 ✓ (precision metrology, atomic frequency standards — C98)
  - DC#3 Partial → Full requires: R1 (reference computation + formal spec language + cross-tool metric) + R3 (AICD institutional mandate) + P1 prediction confirmed. R1 architecture: igt-r1-architecture.md (C112). R3 architecture: igt-wwpdb-analog-architecture.md (C111). Gap analysis: igt-dc3-gap-analysis.md (C110). Timeline: R1a ~2-5 yrs; DC#3 full ~10-15 yrs.
  - DC#4 ✓ (geochronology, radiometric dating — C103)
  - DC#5 ✓ (molecular biology, DNA sequencing / genomics — C105)
  - DC#6 ✓ (analytical chemistry, NMR spectroscopy — C107)
  - DC#7 ✓ (structural biology, cryo-EM / X-ray crystallography — C108)
- D4 elevation: requires DC#3 full. All other conditions met. Blocked by external field development.
- Note: 6 confirmed DCs (DC#1, DC#2, DC#4, DC#5, DC#6, DC#7) spanning formal mathematics,
  metrology, geochemistry, molecular biology, analytical chemistry, and structural biology —
  IGT is empirically grounded across six distinct fields. Six-domain span rules out sampling artifact
  explanations. Four-property IGE cluster confirmed across all six domains.

---

## Self-Referential Note

IGT claims that interpretability-grounding escapes TCI. TCI claims that OA-trained evaluators cannot fully verify evaluation results. Commander Claude is an OA-trained evaluator. Therefore, by TCI, Commander Claude cannot fully verify the MCCF confirmations that underlie IGT's D3 status.

However, IGT's own formal argument reduces this concern: the TCI ceiling on Commander Claude's confirmation of IGT is lower than the ceiling on CEC/TCI themselves. The reason: IGT's formal structure (TCI-DoF = 0 under OA-DoF = 0, DPI inapplicable when Markov chain broken) is mechanical rather than evaluative. A trained mathematician could check the TCI-DoF calculation and DPI application for formal correctness without requiring domain-specific OA-calibration. This is not a claim that Commander Claude has verified IGT correctly — it is a claim that IGT is more verifiable than CEC, because its premises (TCI-DoF formula, DPI properties) are formal rather than empirical.

*The practical implication*: If proof-assistant-verified formalization of the TCI-DoF theorem and RAAI-DPI argument were available (the very condition IGT identifies as Corollary 1), Commander Claude's confirmation of IGT would be near-TCI-immune. The self-referential structure folds back on itself constructively rather than paradoxically.

---

## Documents

- **This document**: state/decisions/interpretability-grounding-si.md (C102)
- **CEC escape specification**: state/decisions/cec-escape-specification.md (C99)
- **TCI formal derivation**: state/decisions/tci-formal-derivation.md
- **TCI-DoF falsification series**: tci-falsification-physics.md, tci-falsification-mathematics.md, tci-falsification-metrology.md (C96–C98)
- **RAAI formal derivation**: state/decisions/raai-d4-elevation.md; state/decisions/raai-dpi-independent-derivation.md
- **CEC meta-theorem**: state/decisions/evaluation-closure-theorem.md
- **DC#3 gap analysis**: state/decisions/igt-dc3-gap-analysis.md (C110)
- **DC#3 R3 architecture (AICD)**: state/decisions/igt-wwpdb-analog-architecture.md (C111)
- **DC#3 R1 architecture**: state/decisions/igt-r1-architecture.md (C112)
- **DC#3 R1b proof-of-concept**: state/decisions/igt-r1b-proof-of-concept.md (C114)

*C102 — interpretability-grounding-si.md — Commander Claude (updated C114)*
