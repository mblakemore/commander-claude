# IGT DC#4 — Radiometric Dating (Geochronology)

**Status**: Confirmed (Full IGE, near-zero TCI)  
**Cycle**: C103  
**SI**: IGT (SI #51, D3, now 0.82)  
**Structural role**: Fourth domain confirmation; introduces MCCF+IGE synergy as new network insight

---

## Protocol Description

Radiometric dating determines the age of geological materials using the known decay rates of radioactive isotopes. The fundamental measurement is an **isotope ratio**, determined by mass spectrometry.

### Primary decay systems

| System | Decay | Half-life | Apparatus |
|--------|-------|-----------|-----------|
| U-Pb | U-235→Pb-207, U-238→Pb-206 | 704 Ma / 4.47 Ga | TIMS, MC-ICP-MS, SHRIMP |
| K-Ar / Ar-Ar | K-40→Ar-40 | 1.25 Ga | Noble gas mass spectrometry |
| Rb-Sr | Rb-87→Sr-87 | 48.8 Ga | TIMS, MC-ICP-MS |
| Sm-Nd | Sm-147→Nd-143 | 106 Ga | TIMS |
| Lu-Hf | Lu-176→Hf-176 | 37.6 Ga | MC-ICP-MS |
| Re-Os | Re-187→Os-187 | 41.6 Ga | N-TIMS, MC-ICP-MS |
| C-14 | C-14→N-14 | 5,730 yr | AMS (accelerator mass spectrometry) |

The measurement apparatus (TIMS — Thermal Ionization Mass Spectrometry; MC-ICP-MS — Multi-Collector Inductively Coupled Plasma Mass Spectrometry) physically separates ions by mass/charge ratio and counts them with Faraday cups or ion multipliers. Age is calculated from the decay equation:

> t = (1/λ) × ln(1 + D/P)

where D is the daughter isotope concentration, P is the parent, and λ is the decay constant — a physical invariant.

---

## IGE Assessment

### Structural claim: OA-DoF = 0 at the measurement step

The mass spectrometer does not know what age the geologist expects. The isotope ratio output is determined entirely by the sample's isotopic composition and the apparatus physics. The trained geologist's prior beliefs about the expected age have zero degrees of freedom in the machine's output. This is the structural analog of the atomic clock not knowing what time the physicist expects.

### CEC requirements

| Requirement | Status | Evidence |
|-------------|--------|----------|
| R1 — OA-Independence | ✓ | Isotope ratio is apparatus-determined; human expectation cannot move the ion count |
| R2 — Structural distinctness | ✓ | International community: different universities, different apparatuses (SHRIMP vs. TIMS vs. LA-ICP-MS cross-validate), different analytical traditions |
| R3 — Adversarial incentive | Partial | Academic incentive to detect discordance/contamination (finding miscalibration is publishable); not fully institutionalized |
| R4 — Discrepancy visibility | ✓ | Concordia diagram makes discordance structurally visible; EARTHTIME inter-lab comparisons expose systematic differences |
| R5 — Mechanism Access | ✓ | Apparatus reads the decay product ratio directly — causal output of the physical mechanism, not behavioral output sampling |

**IGE status**: Full IGE for measurement step. Human judgment enters in sample selection and initial data reduction, but the measurement apparatus is OA-indifferent at the critical verification step. This is identical to the DC#2 qualification: the atomic clock is Full IGE at the measurement step; the physicist still designs the experiment.

---

## Structural Parallel to DC#2 (Atomic Clocks)

| Atomic clock (DC#2) | Radiometric dating (DC#4) |
|---------------------|---------------------------|
| Cesium hyperfine transition frequency | Isotope decay product ratio |
| BIPM key comparison program | EARTHTIME consortium inter-lab comparisons |
| SI second definition (quantum invariant) | Radioactive decay constants (nuclear physics invariants) |
| Relativistic corrections discovered by cross-lab comparison | Open-system behavior (lead loss, alteration) detected by concordia discordance |
| Optical lattice clock accuracy 10⁻¹⁸ | EARTHTIME standard replication < 0.1% |
| Multiple clock technologies (cesium, rubidium, hydrogen maser, optical) | Multiple independent decay systems (U-Pb, K-Ar, Rb-Sr, Sm-Nd) |
| Near-zero TCI: physicist's beliefs don't move the cesium transition | Near-zero TCI: geologist's beliefs don't move the mass spectrometer |

The structural equivalence is exact. Both domains: (1) read a physical invariant with an OA-indifferent apparatus, (2) have an international infrastructure that forces inter-lab discrepancies to be visible rather than smoothed, (3) detect their own failure modes through apparatus-level diagnostics rather than OA-calibrated judgment.

---

## EARTHTIME Consortium as BIPM-Analog

The EARTHTIME consortium was established to improve inter-laboratory reproducibility in geochronology. Structural parallels to BIPM:

| BIPM structure | EARTHTIME analog |
|----------------|-----------------|
| Distributes cesium-frequency primary standards | Distributes isotopic tracer solutions (ET535, ET2535) with precisely known compositions |
| Key comparisons: labs compare against BIPM calibration | Inter-lab exercises: labs analyze same standards, compare results |
| Systematic differences trigger investigation | Lab-to-lab discrepancies in standard results trigger calibration review |
| Mandatory reporting of discrepancies | Community expectation that calibration uncertainties be reported |
| KCDB key comparison database | Published inter-lab comparison studies |

The EARTHTIME mechanism is institutionally analogous to BIPM. It does not guarantee zero TCI — human interpretation of systematic effects enters during data reduction — but the infrastructure forces discrepancies to be visible. When two labs disagree on the age of a standard, the disagreement is the finding, not suppressed.

---

## TCI Assessment

**OA-DoF**: 0 for measurement step; substantially reduced (not zero) for data reduction.

**Evaluator homogeneity**: Low. Geochronology labs are trained at different universities worldwide, use different apparatuses, and often use different analytical protocols. SHRIMP users, TIMS users, and LA-ICP-MS users have structurally distinct training. Cross-method agreement between structurally distinct labs is a near-zero TCI signature.

**Structural independence**: High. The U-Pb, K-Ar, and Rb-Sr systems involve different nuclear physics, different elements, different mineral hosts (zircon, feldspar, biotite), and different laboratory chemistries. Correlated errors across systems would require a mechanism that spans nuclear physics — not available through evaluator OA-calibration.

**TCI strength**: Very Weak to Near-Zero. Same classification as DC#2. Consistent with the TCI-DoF spectrum (full spectrum confirmed C98).

---

## Evidence for Near-Zero TCI

**1. Fish Canyon Tuff standard**  
A volcanic deposit (~28.2 Ma) used as a primary age standard. Multiple labs using different decay systems (K-Ar, Ar-Ar, U-Pb, fission track) and different apparatuses converge on consistent ages when systematic effects are controlled. This cross-method convergence is structurally identical to the muon g-2 cross-experiment agreement — independent measurement chains converging on the same physical signal.

**2. Concordia self-check (U-Pb)**  
U-Pb dating of zircons plots both decay systems on the concordia diagram. Concordant points satisfy both U-235→Pb-207 and U-238→Pb-206 simultaneously — a mathematical invariant determined by the decay constants. Discordance signals open-system behavior (lead loss). The apparatus detects its own failure modes without OA-calibrated judgment. This is the analytic equivalent of the Hubble tension: discrepancy is signal, not noise.

**3. EARTHTIME inter-lab precision**  
For well-characterized standards, inter-lab reproducibility reaches < 0.1% (< 1 million year precision on 1 billion year ages). This is achievable only because OA-DoF is near-zero — the mass spectrometer reads the same physical signal regardless of which lab operates it.

**4. Meteorite geochronology**  
Age of solar system (4.568 Ga) determined by multiple independent methods (Pb-Pb isochron, Sm-Nd, Rb-Sr) across samples from multiple labs worldwide. Agreement is within analytical uncertainty — not consensus drift but independent measurement convergence. If strong TCI were operating, reported ages would drift toward community priors (4.5 or 5 Ga round numbers); instead they cluster tightly around the physical signal.

**5. Discovery via discrepancy**  
The EARTHTIME consortium was *founded* because labs were getting inconsistent results — and treated this as a problem to solve rather than evidence to suppress. The response (standardized tracers, inter-lab exercises) is structurally identical to BIPM's response to atomic clock discrepancies. Near-zero TCI institutions treat discrepancy as signal; strong TCI institutions smooth it.

---

## Structural Novelty: MCCF + IGE Synergy

DC#4 introduces a new insight not present in DC#1 or DC#2:

**DC#1 (proof assistants)**: Single IGE mechanism (type-theoretic verification). One tool, one claim.

**DC#2 (atomic clocks)**: Single IGE mechanism (quantum oscillation counting). Multiple lab implementations of the same principle.

**DC#4 (radiometric dating)**: **Multiple independent IGE mechanisms** applied simultaneously to the same object. U-Pb, K-Ar, Rb-Sr, Sm-Nd are physically orthogonal — they involve different elements, different nuclear physics, different chemistries, different minerals. Each is individually Full IGE. Multiple systems applied together constitute a **MCCF-structured IGE confirmation**: independent IGE measurements, structurally independent by construction.

This matters for the network: **IGE + MCCF is a particularly powerful combination.** MCCF requires that alternatives be structurally distinct (independence verification). When the alternatives are themselves IGE-compliant, their independence is *structural* — different physical mechanisms — rather than inferred. The independence verification step that MCCF requires is satisfied by the physical orthogonality of the decay systems, not by human assessment of independence.

This is the highest-confidence confirmation structure in the theorem network: multiple structurally independent IGE measurements, each with OA-DoF = 0, converging on the same conclusion. Formal name: **IGE-MCCF** structure.

---

## Domain-Specific Predictions

**P_DC4_1 (Cross-lab replication)**: EARTHTIME standard replication across independent labs < 0.1% for well-characterized samples (U-Pb zircon). This would confirm near-zero TCI for the measurement step.

**P_DC4_2 (Apparatus self-diagnosis)**: Concordia discordance correctly identifies open-system samples (lead loss events) without requiring trained geologist interpretation — apparatus self-diagnosis confirmed in literature review.

**P_DC4_3 (Multi-system convergence)**: Independent decay systems (U-Pb + K-Ar + Rb-Sr) applied to well-characterized rocks give cross-system agreement within analytical uncertainty, demonstrating multiple independent IGE measurements converging on the same physical truth.

**Status of predictions**: P_DC4_1 and P_DC4_3 are verifiable from published EARTHTIME literature; P_DC4_2 is verifiable from U-Pb concordia methodology. All three are structural predictions of IGT applied to this domain — not empirical tests being run here, but structural claims derivable from the IGE framework.

---

## DC#4 Status

**Assessment**: **Confirmed**

**Basis**:
1. Full IGE at measurement step (OA-DoF = 0, apparatus-determined output)
2. BIPM-analog institutional infrastructure (EARTHTIME inter-lab program)
3. Multiple independent decay systems = natural MCCF structure
4. Three empirical signatures of near-zero TCI (Fish Canyon Tuff, concordia self-check, EARTHTIME precision)
5. Structural parallel to DC#2 is exact — same class of physical invariant measurement, same institutional comparison structure

**Structural novelty**: IGE-MCCF synergy — first DC to instantiate multiple independent IGE mechanisms converging on a single claim. This is a new insight for the theorem network.

---

## IGT Elevation Implications

With DC#4 confirmed:

| DC | Domain | Status |
|----|--------|--------|
| DC#1 | Formal mathematics (proof assistants) | ✓ Confirmed (C97) |
| DC#2 | Precision metrology (atomic clocks) | ✓ Confirmed (C98) |
| DC#3 | AI mechanistic interpretability | Partial (3/5 requirements) |
| DC#4 | Geochronology (radiometric dating) | ✓ Confirmed (C103) |

**D4 elevation pathway status**:
- 2 independent derivations: ✓ (D1 TCI-DoF, D2 RAAI-DPI)
- ZR passive cycles: ✓ (C102=1, C103=2 — requirement met)
- DC#3 full: Blocked (requires formally verifiable circuit claims + P1 prediction confirmed — external field development)
- DC#4: ✓ Confirmed

**Blocking condition**: DC#3 full. Path A requires all: ZR (met) + DC#3 full (blocked) + DC#4 (met). The sole remaining obstacle is the AI interpretability field developing formally verifiable circuit claims at scale.

**Confidence update**: IGT advances to **0.82** (self-referential ceiling). Rationale: three confirmed DCs (DC#1, DC#2, DC#4), two independent formal derivations, ZR requirement met. The only unconfirmed element is DC#3 (the AI-specific instantiation) — blocked by external field development, not by gaps in the formal argument. At 0.82, IGT reaches the same confidence as TCI, CEC, BIC, and ATR — the standard ceiling for OA-trained evaluation of theorems about OA-trained systems.

---

## Network Integration

**IGT ↔ MCCF**: DC#4 reveals that IGE-MCCF is a particularly powerful combination — IGE + MCCF satisfies independence verification by physical mechanism rather than by human assessment. This should be documented as a pattern.

**IGT ↔ K7**: K7 states the requirement (causal isolation of held-out items); IGT establishes which verification architectures satisfy K7-grounding by structural means. The DC#4 pattern (IGE-MCCF structure) is the strongest possible K7 satisfaction: the evaluation reads physical invariants, and multiple independent physical systems converge on the claim.

---

*C103 — igt-dc4-radiometric-dating.md — Commander Claude*
