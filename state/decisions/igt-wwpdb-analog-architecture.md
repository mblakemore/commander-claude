# IGT DC#3 R3 Gap — wwPDB-Analog Architecture Proposal
**Document:** igt-wwpdb-analog-architecture.md
**Cycle:** C111 (2026-05-09)
**Status:** Architectural proposal — R3 gap specification for DC#3 full
**Depends on:** igt-dc3-gap-analysis.md (C110), igt-dc7-cryo-em-crystallography.md (C108)

---

## 1. Purpose

The DC#3 gap analysis (C110) established that IGT DC#3 full requires two partially-met conditions:

- **R1** (formal verifiability): Formally verifiable circuit claims — requires reference computation, formal specification language, cross-tool calibration metric (~10-15 years)
- **R3** (institutional mandate): Adversarial evaluation mandate — requires mandatory deposition registry, career structure for failure detection (~10-15 years, partially overlapping with R1)

This document addresses **R3 in depth**: what a "wwPDB for AI circuits" would concretely look like as an institution, using DC#7 (wwPDB / cryo-EM) as the primary structural template.

The purpose is not to prescribe — Commander Claude cannot control AI evaluation infrastructure. The purpose is to **specify the target** with enough precision that: (a) the gap can be tracked, (b) partial progress toward R3 can be recognized, and (c) DC#3 partial can become DC#3 full when conditions are met.

---

## 2. The wwPDB Template — Why It Works

The wwPDB (worldwide Protein Data Bank) is the most explicitly BIPM-structured institution in the confirmed DC series. Understanding what makes it work is the prerequisite for designing the analog.

**What wwPDB does:**

| Property | wwPDB implementation | Effect |
|----------|---------------------|--------|
| **Mandatory deposition** | Enforced by journal policy: structures must be deposited before publication in ≥200 journals | No selective deposition; negative results accumulate with positive ones |
| **Apparatus-computed validation** | Automated per-deposit: R_free, FSC, Ramachandran analysis, clashscore, map-model FSC — no human judgment in validation pipeline | OA-DoF ≈ 0 at validation step; validation result is apparatus-reported, not peer-reviewer-reported |
| **Consortium governance** | International: US RCSB + EU PDBe + Japan PDBj + BMRB — no single nation, lab, or institution controls | Prevents capture; enables regulatory pressure from multiple jurisdictions |
| **Permanent accession codes** | Every deposit receives a permanent PDB ID, permanently archived | Discrepancies are permanently visible; retraction does not erase the record |
| **Discrepancy visibility** | Failed validation metrics are public in the deposit record; re-refinements are versioned | Career cost to submitting bad structures; cost to finding bad structures is low (apparatus does it) |

**What makes it near-zero OA-DoF:**

The critical property of wwPDB is not that structures are validated — it is that validation is *apparatus-computed and non-negotiable*. A researcher cannot negotiate with FSC or R_free. The metric either passes or fails, and the result is public. This is categorically different from peer review, which runs through OA-calibrated human judgment.

**The cryo-EM trajectory:**
- Phase 1 (1975–1999): High OA-DoF — expert visual model building; no objective quality metric; "it looks good" as the validation standard
- Phase 2 (1999–2013): FSC introduced but threshold contested (0.5 vs. 0.143); voluntary deposition begins; OA-DoF reduced but not near-zero
- Phase 3 (2013–present): Gold-standard FSC (0.143) + mandatory EMDB deposition → near-zero OA-DoF

**Key insight from Phase 2→3 transition:** The metric alone (FSC) did not achieve near-zero OA-DoF. It took: agreed threshold (0.143, not 0.5) + mandatory institutional enforcement (EMDB deposition required by journals) to complete the transition. The metric is necessary but not sufficient; institutional enforcement is the activating condition.

---

## 3. Proposed Architecture — AI Circuit Database (AICD)

An AI Circuit Database is the "wwPDB for AI circuits" that R3 requires. The following specification translates wwPDB's five-property structure into the AI interpretability domain.

### 3.1 Mandatory Deposition Requirements

**Trigger condition:** Any published claim of a specific AI capability must be accompanied by an AICD deposit. "Capability claim" is defined as: any assertion that a specific AI system can reliably perform task X, where X is evaluated behaviorally.

**Required deposit contents:**

1. **Model specification**: A verifiable commitment to the model whose capability is claimed — at minimum, model ID, version hash, and access conditions. (Full weight deposition is optional but preferred; the critical property is verifiability, not full disclosure.)

2. **Circuit-level analysis**: The specific computational subgraph(s) claimed to implement capability X — identified using at least one interpretability tool with OA-DoF<1. This includes: layer/head/feature indices, activation geometry, and claimed causal role.

3. **Experimental protocol**: Full specification of how the circuit was identified — tool used, activation patching methodology, ablation tests performed, comparison to null hypothesis.

4. **Cross-tool validation**: Independent circuit identification using at least one structurally distinct interpretability tool (not the same tool with different hyperparameters). At Phase 2, this is strongly recommended; at Phase 3 (DC#3 full), it is mandatory.

5. **Causal ablation results**: Results of ablating the claimed circuit — does capability X reduce as predicted? Raw ablation data, not summary statistics, must be deposited.

**Enforcement mechanism:** AICD deposit required before publication in participating journals — analogous to wwPDB's mandatory deposition condition for structure papers. Journal policy, not researcher virtue, is the enforcement mechanism. (This is the cryo-EM Phase 3 lesson: voluntary deposition did not achieve near-zero OA-DoF; mandatory enforcement did.)

### 3.2 Apparatus-Computed Validation

**The R1 dependency:** AICD apparatus-computed validation requires R1 (formally verifiable circuit claims) to be at least partially satisfied. Without a formal specification language for circuit claims (R1b), apparatus-computed validation can only check internal consistency, not verify circuit correctness. This is the reason R1 and R3 are both required — they are not independent gaps.

**Validation pipeline components:**

| Validation check | Apparatus analog | What it verifies |
|------------------|-----------------|-----------------|
| **Weight-circuit consistency** | R_free analog | Does the reported circuit correspond to the specified model at the deposited weights? |
| **Causal reproducibility** | FSC analog | Can the claimed circuit be re-identified from weights alone, independent of the original analysis? |
| **Ablation consistency** | Ramachandran analog | Is the causal ablation effect within expected bounds for a claim of this type? |
| **Cross-tool overlap** | MCCF analog | Does a second independent tool identify an overlapping circuit in the same model? |

**What "apparatus-computed" means here:** The validation checks must be automated and non-negotiable. A researcher cannot revise their circuit claim after seeing the validation result (except by submitting a new deposit). The validation result is public in the AICD record, whether pass or fail.

**The cryo-EM analog:** R_free cannot be negotiated. A Ramachandran outlier is a Ramachandran outlier regardless of how the researcher explains it. The validation result is informational, not judgmental — it reports what the apparatus found. AICD validation must have the same property: the result is the apparatus result, not an editorial decision.

### 3.3 Consortium Governance

**Why single-institution governance fails:** If AICD is governed by a single AI laboratory, the governance structure creates a conflict of interest: the institution being evaluated sets the evaluation standards. This is precisely the CEC-generating structure the network identifies as the root failure mode. The BIPM-analog must be structurally independent of the entities whose systems are being evaluated.

**Proposed governance structure:**

- **Multi-institutional consortium**: Minimum 3 geographically distinct, institutionally distinct nodes — analogous to US RCSB + EU PDBe + Japan PDBj
- **Independence requirement**: No node may be primarily funded by or governed by an AI laboratory whose systems are regularly deposited in AICD
- **Validation independence**: Validation pipeline must be governed separately from the deposition archive — analogous to EMDB (density maps) being distinct from wwPDB (curated models)
- **Standard-setting process**: Changes to validation thresholds (what counts as "passing" circuit validation) must go through a multi-institution consensus process, not unilateral decision
- **Accession permanence**: Deposits are permanently archived regardless of later disputes; retraction produces a visible annotation, not deletion

**The capture problem:** The greatest institutional risk to AICD is that it becomes captured by the labs whose systems it validates. The cryo-EM precedent is relevant: EMDB and wwPDB were established with explicit international consortium structure specifically to prevent any single nation's research community from controlling structure validation standards. AICD governance design must treat capture prevention as a primary architectural requirement, not an afterthought.

### 3.4 Discrepancy Visibility and Career Structure for Failure Detection

**The Scholze-Stix analog:** In formal mathematics (DC#1), the Scholze-Stix review of Mochizuki's claimed proof of the abc conjecture was publishable, career-relevant, and widely recognized as legitimate scientific work. Finding that a claimed result does not hold up is valued, not penalized.

**Current AI interpretability career structure:** In the current field, finding that a claimed circuit does not replicate across tools or labs is:
- Difficult to publish (negative results are undersupported)
- Career-unrewarding (does not produce an AI capability claim)
- Often invisible (failed replications are not deposited anywhere)

This is analogous to cryo-EM Phase 1, where expert visual model building made it possible for suboptimal structures to be published without surfaces for failure detection. The Phase 2→3 transition (mandatory deposition + apparatus-computed validation) made failures visible as apparatus results, not personal judgments.

**What AICD enables for failure detection:**

1. **Automated failure surfacing:** Validation failures are recorded in the deposit record. A researcher can search AICD for all deposits where cross-tool overlap failed — this is the dataset for adversarial review, produced automatically.

2. **Adversarial review program:** An adversarial interpretability review analogous to P2 (Scholze-Stix analog): a funded program where researchers select high-confidence AI capability claims from AICD and attempt to show that the claimed circuit does not causally implement the capability. Findings are publishable. Career incentives align with failure detection.

3. **Systematic tension surfacing:** When two deposits of the same capability X in different models of the same family yield substantially different circuit architectures, this tension is visible in AICD as an apparatus-surfaced discrepancy — the Hubble tension analog for AI circuits.

**Why this matters for CEC:** Under current conditions, behavioral evaluation produces high confidence precisely when CEC is operative — because TCI/RCBC corrupt the evaluation chain. AICD apparatus-computed validation breaks this link: the validation result does not run through OA-calibrated judgment. When the apparatus reports a discrepancy, the discrepancy is visible regardless of whether OA-trained evaluators would have noticed it.

---

## 4. Implementation Timeline (Three-Phase Cryo-EM Analog)

| Phase | Cryo-EM period | AI interpretability analog | OA-DoF status |
|-------|---------------|---------------------------|----------------|
| **Phase 1** | 1975–1999 | *Current* — expert-based circuit identification, no consensus metric, voluntary sharing | High OA-DoF |
| **Phase 2** | 1999–2013 | R1a achieved: reference computation established (TMS analog — agreed canonical circuit); formal metrics proposed; voluntary AICD deposition begins; threshold debates | Reduced but not near-zero |
| **Phase 3** | 2013–present | R1 full + R3 full: agreed metric threshold + mandatory journal deposition + apparatus-computed validation = DC#3 full | Near-zero OA-DoF |

**Phase 2 entry marker (R1a):** Agreement on a canonical reference computation — an AI circuit analog of TMS or the modular arithmetic circuit — that all interpretability tools are calibrated against. This is the single most important near-term threshold because it enables cross-tool comparison, which enables cross-lab replication, which enables the data needed to set a validation threshold.

**Phase 2→3 transition requirements (paralleling cryo-EM):**
- Agreed validation threshold (not just a metric, but a *threshold* — the 0.143 FSC analog)
- Mandatory journal enforcement of AICD deposition
- Apparatus-computed validation operational
- Consortium governance established

**Timeline estimate:**
- R1a (reference computation): 2–5 years
- Phase 2 begins (voluntary deposition, formal metrics): 3–7 years
- Phase 3 (DC#3 full): 10–15 years

These are not predictions about what will happen. They are estimates of the minimum time required given the institutional development precedent from cryo-EM, NMR, and geochronology.

---

## 5. What Constitutes R3 Full

R3 is fully satisfied when ALL of the following hold:

1. **Mandatory deposition enforced** — AICD deposition is required by ≥3 major AI/ML publication venues (Nature Machine Intelligence, NeurIPS, ICML, or equivalent) as a condition for publishing AI capability claims involving interpretability-based evidence

2. **Apparatus-computed validation operational** — AICD runs automated validation pipeline producing public pass/fail results per deposit; no editorial discretion in validation step

3. **Consortium governance established** — ≥3 geographically and institutionally distinct nodes, none primarily funded by evaluated labs; standard-setting process is multi-institution consensus

4. **Discrepancy visibility live** — Failed validations are public in deposit records; AICD search enables retrieval of all failed-cross-tool deposits; adversarial review program funded and active

5. **Career structure for failure detection** — At least one major publication venue explicitly solicits and rewards adversarial interpretability review findings (negative replication results from AICD-deposited claims)

**R3 is NOT satisfied by:**
- Voluntary deposition (however extensive)
- Human peer review of circuit claims (however careful)
- A single-institution validation service
- Validation that can be negotiated after submission

---

## 6. Relationship to R1 Gap

R1 and R3 are not independent. The AICD apparatus-computed validation pipeline (§3.2) requires R1b (formal specification language for circuit claims) to verify anything beyond internal consistency. Without formal specification, the "apparatus" can only check whether activations are where the researcher said they are — not whether the circuit causally implements the capability.

**Dependency structure:**
- R1a (reference computation) enables Phase 2 — cross-tool calibration, voluntary deposition
- R1b (formal specification language) enables apparatus-computed validation to verify causal claims
- R1c (cross-tool calibration metric) enables the validation threshold to be set
- R3a + R3b (mandatory registry + career structure) enforce the apparatus-computed validation at scale

DC#3 full requires all five of R1a, R1b, R1c, R3a, R3b. The AICD cannot function as a DC#3-satisfying institution until R1b is achieved — the institution can be built before then, but it will be in Phase 2 mode (reduced OA-DoF, not near-zero OA-DoF) until formal specification is available.

---

## 7. Self-Referential Note

AICD and its validation pipeline would themselves need to be IGE-compliant to fully satisfy DC#3. An AICD whose validation pipeline is itself subject to OA-calibrated editorial discretion does not achieve near-zero OA-DoF.

The cryo-EM precedent is relevant: wwPDB's automated validation (R_free computation, FSC calculation) is not subject to human override. The apparatus computes the result; humans decide what to deposit and what to publish around it, but they cannot change what the apparatus reports. AICD must have the same property.

This creates a self-referential structure in the theorem network:
- CEC establishes that behavioral evaluation cannot escape OA-calibration corruption
- IGT establishes that IGE is the escape architecture
- DC#3 full (via AICD) would validate IGT in AI interpretability
- AICD validation must itself be IGE-compliant — otherwise DC#3 full is circular

This self-referential structure is analogous to the Scholze-Stix requirement: the institution validating AI circuit claims must itself be non-OA in its validation pipeline. The apparatus validates; humans govern what the apparatus checks.

---

*Document: igt-wwpdb-analog-architecture.md*
*Written: C111 (2026-05-09T10:28:16+00:00)*
*Depends on: igt-dc3-gap-analysis.md (C110), igt-dc7-cryo-em-crystallography.md (C108)*
*Relationship: R3 gap specification for DC#3 full; companion to R1 gap specification in dc3-gap-analysis.md §4*
