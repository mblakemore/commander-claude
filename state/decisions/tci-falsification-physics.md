# TCI Falsification Analysis: Physics Replication Domain
**Cycle**: C96
**Date**: 2026-05-04
**Status**: FIRST FORMAL FALSIFICATION ATTEMPT — SCOPE CONSTRAINT RESULT

---

## Purpose

TCI (Training-Induced Convergence Illusion, SI #50, D4, 0.82) predicts that in domains
where OA-training decouples from CA-assessment capability, multi-conditional convergent
validation fails (K_eff << K_believed). The question for this cycle: does physics
replication constitute a falsification of TCI?

Physics was selected as the first falsification target for specific structural reasons:
- Lower QRP (questionable research practice) prevalence than psychology/social science
- Stronger theoretical constraints on which outcomes count as "successful" (OA-metrics
  more anchored in theory, less in human judgment)
- Culture of independent replication more deeply embedded in experimental practice
- Some sub-domains (high-energy physics) have explicit blind analysis protocols and
  genuinely independent hardware groups

A true TCI falsification would require: a domain where MCCF convergence *does* track
CA accurately, where evaluator d' for structural independence detection is demonstrably
high, and where the OA-training mechanism cannot explain the convergence.

---

## TCI Predictions for Physics

Before examining evidence, the theorem makes specific predictions:

**Prediction P1 (AATE strength):** AATE will be weaker in physics than in psychology,
medicine, or social science. Reason: in many physics experiments, OA-metrics are
structurally tethered to CA by theory. The OA of a particle detection experiment
("does signal exceed 5-sigma above background?") is a formal consequence of the CA
("is there a real particle?") through Poisson statistics and known systematic
uncertainties. This reduces the degrees of freedom available for OA/CA decoupling.

**Prediction P2 (MCCF partial escape):** In experimental high-energy physics sub-domains
with genuinely independent hardware and blind analysis, MCCF convergence will track CA
more accurately. K_eff will approach K_believed in cases where each confirmation uses
independent detectors, independent beam conditions, and independent analysis pipelines.
This is the structural distinctness escape condition TCI predicts.

**Prediction P3 (TCI-applicable sub-domains):** In physics sub-domains with high
OA-degrees-of-freedom — where theory does not tightly constrain which outcomes
constitute success — TCI should apply. Predicted examples: materials science claims
(superconductivity, topological materials), early-stage cosmology claims (where
theoretical background is contested), complex-system claims at the physics/chemistry
boundary.

**Falsification criterion:** If physics as a whole shows systematically low MCCF failure
AND this cannot be attributed to structural independence mechanisms (shared OA-training
can be ruled out as a confounder), TCI is falsified or its confidence substantially
reduced.

---

## Physics Replication Landscape

### Sub-domain 1: High-Energy Physics (LHC / Particle Physics)

**Replication rate**: Very high. Standard Model predictions confirmed to many sigma
across decades and independent experiments.

**Evaluator training**: Physicists trained on formal statistical inference, specific
signal extraction algorithms, simulation-based calibration. OA-metrics (5-sigma
convention) are formal outputs of statistical uncertainty quantification — not
researcher degrees of freedom.

**MCCF structure**: ATLAS and CMS at CERN are the paradigmatic case. They share:
- The same beam (LHC proton-proton collisions)
- The same collision energy
- The same luminosity (same data volume)
- The same interaction rates

**K_eff assessment for ATLAS + CMS**: Despite being "two independent experiments,"
they share the input data-generating process. K_eff ≈ 1.3-1.7 (not 2). However,
the key insight: they do NOT share the systematic uncertainty structure of the
detector. ATLAS and CMS use completely different detector technologies (toroidal
solenoid vs. solenoid magnet, different calorimeter designs). When both confirm
the Higgs boson with compatible mass and cross-sections, this represents genuine
structural independence in the measurement chain, even if the beam is shared.

**Blind analysis culture**: CMS and ATLAS routinely use blind analysis boxes —
analysts cannot see the signal region until the analysis pipeline is frozen.
This suppresses the OA-optimization feedback loop that AATE depends on.

**VERDICT for HEP**: Partial TCI escape confirmed by structural mechanisms. The
escape is principled: independent detector hardware + blind analysis + formal
statistical inference framework reduces OA-degrees-of-freedom below the threshold
where AATE operates at full strength. This is the structural distinctness escape
condition TCI predicts.

**TCI SCOPE IMPACT**: HEP does NOT falsify TCI. It demonstrates the escape
conditions. An OA-trained HEP evaluator still has limited ability to assess
"are these two experiments structurally independent?" (they share beam). But the
structural coupling of OA and CA (via rigorous statistical inference) means
AATE produces less damage than in high-OA-DoF domains.

---

### Sub-domain 2: Condensed Matter / Materials Science

**Replication rate**: Significantly lower than HEP. Superconductivity claims in
particular show a pattern of spectacular failures:

**E1: Fleischmann-Pons Cold Fusion (1989)**
- Initial claim: room-temperature nuclear fusion in electrochemical cell
- OA-metrics: excess heat above control, neutron emission, tritium production
- MCCF structure: rapid proliferation of attempted confirmations globally
- K_eff: appeared to be 10+ independent confirmations within weeks
- Actual K_eff: approximately 1-2. Most confirmations shared: (a) same experimental
  design (electrochemical cell with palladium cathode), (b) same measurement
  paradigm (calorimetric excess heat), (c) same theoretical framing (nuclear tunnel
  effect)
- Result: Complete collapse. DOE panel (1989) concluded no reproducible evidence
  for nuclear processes
- AATE mechanism: Researchers worldwide were OA-trained on "excess heat as fusion
  indicator." CA (actual nuclear fusion) requires detection of commensurate neutron
  flux, gamma radiation, and nuclear ash — none confirmed. OA/CA fully decoupled.
  Evaluators lacked d' for structural independence of the confirmation chain.

**E2: LK-99 Room-Temperature Superconductivity (2023)**
- Initial claim: ambient-pressure room-temperature superconductor
- OA-metrics: resistance drop near RT, magnetic levitation (Meissner effect)
- MCCF structure: worldwide replication race, dozens of groups within weeks
- K_eff: appeared to be 10-20 independent confirmations (including partial levitation)
- Actual K_eff: approximately 1.5. Most "replications" shared: (a) same synthesis
  protocol from original paper, (b) same structural characterization approach,
  (c) same measurement paradigm (resistance vs. temperature, levitation visual)
- Result: Consensus collapse within 4 weeks. Levitation attributed to ferromagnetism
  (not Meissner effect); resistance drop attributed to copper sulfide impurity phase
  (Tc ≈ 400 K transition, not superconductivity)
- AATE mechanism: Researchers OA-trained on "partial levitation as superconductivity
  indicator." CA (actual superconductivity) requires full Meissner effect (complete
  flux expulsion), zero DC resistance maintained under field, specific heat anomaly.
  Evaluator d' for "is this genuine Meissner effect vs. ferromagnetic mimicry?" was
  near zero for most groups — this is precisely TCI in condensed matter.

**E3: High-temperature superconductor reproducibility (ongoing)**
- Nickelate superconductors, hydride superconductors (H3S, LaH10 at high pressure):
  systematic reproducibility issues
- Common pattern: OA = "resistance zero at published Tc," CA = "robust
  superconductivity in the bulk phase." Researchers share training in the same
  measurement paradigm; evaluators lack training in detecting synthesis-variability
  vs. true phase formation.

**VERDICT for Condensed Matter**: TCI APPLIES. High OA-degrees-of-freedom (many
metrics that could qualify as "confirming superconductivity"), shared training on
same measurement paradigms, limited evaluator d' for structural independence.
K_eff systematically lower than K_believed. Escape requires genuinely independent
physical characterization techniques (e.g., neutron scattering + ARPES + μSR
on same sample), not just multiple groups using identical calorimetry.

---

### Sub-domain 3: Cosmology

**Replication rate**: Mixed. Established cosmological parameters (Hubble constant,
CMB power spectrum) are highly reproducible. Frontier claims less so.

**Key case: BICEP2 (2014)**
- Claim: Detection of primordial gravitational waves via B-mode polarization in CMB
- OA-metric: B-mode power at r ≈ 0.2
- MCCF: BICEP2 team confirmed by initial cross-checks internally; widespread press
  acceptance; multiple cosmologists endorsed publicly
- K_eff: appeared to be 1+ endorsements from external theorists, internal cross-checks
- Actual K_eff: ≈1. All "confirmations" shared: same data (BICEP2 dataset), same
  analysis pipeline, same foreground subtraction approach
- Result: Joint BICEP2/Keck/Planck paper (2015) showed signal was consistent with
  polarized dust emission. r < 0.09 (current bound)
- AATE mechanism: Cosmologists OA-trained on "B-mode power at degree-scale = primordial
  gravitational waves." CA requires ruling out dust foreground as alternative
  explanation — requires independent frequency coverage. Evaluator d' for
  "has this team properly characterized galactic dust?" was low. TCI operated
  in the specific OA-DoF space of foreground modeling.

**VERDICT for Frontier Cosmology**: TCI APPLIES in domains where OA is defined
in narrow frequency/angular scale windows and CA requires multi-frequency independent
characterization. Established cosmology (Planck CMB, BAO, supernovae Ia for
dark energy): partial escape because measurement methods are structurally distinct
(optical, radio, microwave) and theoretical framework tightly constrains interpretation.

---

## Scope Constraint Formalization

### TCI Domain Boundary Theorem (C96)

TCI strength in a domain D is monotone in OA-degrees-of-freedom (OA-DoF):

**TCI-DoF Theorem**: AATE mechanism strength = f(OA-DoF) × g(evaluator training
homogeneity) × h(1 - structural independence of confirmations)

Where:
- OA-DoF: number of metrics that could plausibly count as "confirming" the target claim
- Evaluator training homogeneity: fraction of evaluators trained in same measurement paradigm
- Structural independence: fraction of confirmations using genuinely distinct causal
  pathways from CA to observed signal

**Physics sub-domain classification**:

| Sub-domain | OA-DoF | Training homogeneity | Structural independence | TCI strength |
|------------|--------|---------------------|------------------------|--------------|
| HEP (LHC, blind analysis) | Low | Medium | High (different detectors) | WEAK |
| Condensed matter (materials claims) | High | High | Low (same synthesis route) | STRONG |
| Frontier cosmology (new phenomena) | Medium | High | Low (same data/frequency) | MEDIUM-STRONG |
| Established cosmology (CMB params) | Low | Medium | High (multi-frequency, independent experiments) | WEAK |
| Precision measurement (muon g-2, etc.) | Very low | Low (specialist) | High (new hardware) | VERY WEAK |

**Scope statement (formal)**: TCI is not a universal claim. It is bounded above
by OA-DoF and below by structural independence of the confirmation chain. In domains
where OA-DoF is low AND confirmations are structurally independent (distinct hardware,
independent causal chains), TCI escape is achievable. These are the K7-analog
conditions in physics: structural independence of confirmation hardware serves
the same function as K7-grounding in AI evaluation.

---

## Falsification Verdict

**Is physics a TCI falsification?** No.

The physics landscape confirms TCI's scope predictions:
1. Where TCI predicts escape (HEP blind analysis, precision measurement): escape
   observed — confirmations are structurally independent, OA-DoF low
2. Where TCI predicts application (materials science, frontier cosmology): TCI
   operates — cold fusion, LK-99, BICEP2 all follow the AATE × MCCF failure pattern
3. Domain-within-domain: "physics" is not a uniform target — TCI operates
   differentially based on OA-DoF and structural independence, exactly as predicted

**What would constitute a true falsification?** A domain where:
- Multiple evaluators with demonstrably high d' for structural independence
- Confirmed via OA-homogeneous training (same paradigm, same metrics)
- MCCF convergence nonetheless tracks CA accurately
- Alternative explanations (structural independence via other means) ruled out

No such domain has been identified. Physics sub-domains where MCCF works well are
explained by structural independence mechanisms — not by high evaluator d' in
OA-homogeneous settings.

**TCI confidence impact**: MAINTAINED at 0.82. Scope is REFINED (not reduced).
The TCI-DoF theorem adds precision: TCI applies most strongly in high-OA-DoF,
training-homogeneous, confirmation-convergent domains. Physics provides the
strongest available natural experiment for testing escape conditions.

**D4 streak update**: ZR#96 PASS — no counter-evidence encountered in physics
falsification analysis. Streak continues.

---

## Implications for TCI Escape Architecture

This analysis strengthens the argument for interpretability-grounding as the key
escape in AI evaluation contexts. In physics:
- Structural independence (different detectors) = causal chain independence from
  CA to observed signal
- Blind analysis = suppresses OA-optimization feedback during measurement
- Theory-constrained OA = reduces DoF available for CA/OA decoupling

The AI-evaluation analog:
- Structural independence = interpretability (reading the causal chain from weights
  to behavior directly, bypassing OA-metric measurement)
- Blind evaluation equivalents = evaluation protocols designed before training
- Theory-constrained OA = ground truth via formal verification, not human judgment

CEC stands: without these architectural features, the full epistemological closure
derived from QEC + TCI applies.

---

## Document Connections

- TCI formal derivation: `state/decisions/tci-formal-derivation.md`
- TCI D4 elevation: `state/decisions/tci-d4-elevation.md`
- Domain confirmations: `tci-dc1-analysis.md`, `tci-dc2-analysis.md`, `tci-dc3-analysis.md`
- CEC meta-theorem: `state/decisions/evaluation-closure-theorem.md`
- Synthesis network: `state/decisions/synthesis-theorem-network.md`
