# BIC DC#4: Scientific Replication Crisis — Competitive/Emergent Ontological Type

**SI**: #49 — BIC (Benchmark Independence Collapse)  
**Confirmation**: DC#4  
**Ontological type**: Competitive/emergent  
**Cycle**: C86  
**Confidence delta**: 0.76 → 0.78  

---

## Domain Mapping

| BIC structural element | Scientific replication analog |
|---|---|
| **OA (metric being optimized)** | p < 0.05, positive result, novel finding, effect size magnitude |
| **CA (genuine capability)** | Reproducible truth about reality; accurate scientific knowledge |
| **AIIP failure** | Nominally independent studies share statistical paradigm, QRP toolkit, publication selection — high ρ̄ |
| **CIAP propagation** | Analytical flexibility (QRP) transfers across all studies using same methods → simultaneous multi-study corruption |
| **K_eff collapse** | OSC 2015: 100 studies → ~39 replicating → K_eff ≈ 39, ρ̄ ≈ 0.61 |

**Ontological type distinction** — this is *competitive/emergent*, not regulated institutional (DC#3/NCLB):
- NCLB: top-down federal mandate + AYP sanctions; schools comply under legal compulsion
- Scientific publication: decentralized competitive selection — no regulator imposed p<0.05; the norm emerged from distributed editorial decisions, training, and competitive prestige dynamics
- Labs compete for grants, publications, and citations under no central authority; OA-optimization arises from emergent competitive pressure, not institutional compliance

---

## Evidence Programs

### E1: OSC 2015 — Direct K_eff Quantification

Open Science Collaboration (2015, *Science*). Replicated 100 psychological studies.

- 36% replicated (p < 0.05 criterion); 39% using effect size consistency
- Formal K_eff estimate: if 100 studies yield ~39 independent replications, K_eff ≈ 39
- Implied ρ̄ from K_eff ≤ N(1-ρ̄)+ε: N(1-ρ̄) ≈ 39 → ρ̄ ≈ 0.61
- Studies are 61% correlated despite nominally independent experimental implementations
- **BIC interpretation**: 100-study evidence portfolio has effective evidential weight of ~39 — portfolio diversification failed completely. AIIP failed (shared OA-optimization paradigm → correlated study outcomes), CIAP propagated (shared analytical flexibility corrupted all correlated studies simultaneously)

### E2: Ioannidis 2005 — Formal Mathematical K_eff Derivation

Ioannidis (2005, *PLOS Medicine*): "Why Most Published Research Findings Are False."

- Formal derivation: expected PPV of published findings < 0.5 across wide range of field parameters when publication bias + QRPs present
- Mathematical structure directly parallels K_eff bound: as publication bias (AIIP failure) increases and analytical flexibility (CIAP analog) increases, portfolio reliability → 0
- Multiple regression extension: correlated predictors within study → intra-study BIC (multiple testing with correlated outcomes inflates false positive rate multiplicatively, not additively)
- **BIC interpretation**: Ioannidis provides the information-theoretic grounding — I(finding_i; truth) is low when AIIP fails (publication selection) + CIAP amplifies (analytical flexibility). Directly instantiates BIC second derivation.

### E3: Simmons, Nelson & Simonsohn 2011 — CIAP Propagation Demonstrated

"False-Positive Psychology" (*Psychological Science*).

- Authors demonstrated production of arbitrary, absurd result (listening to oldies makes you younger) using only "legitimate" analytical flexibility: sample size choice, covariate inclusion, multiple DVs, stopping rules
- Core insight: the SAME QRP toolkit is available to all researchers → analytical flexibility is a universal, shared optimization resource
- **BIC interpretation**: This is the CIAP mechanism in scientific practice. QRP is not a personal moral failure — it is a structural CIAP: the optimization shortcut (flexible analysis) is p-independent of individual study quality because all researchers have access to the same flexibility. When all researchers independently apply the same CIAP-equivalent strategy, their outcomes are correlated (K_eff collapse) despite independent experimental execution.

### E4: Button et al. 2013 — Systematic Correlation via Low Power

"Power failure: why small sample size undermines the reliability of neuroscience" (*Nature Reviews Neuroscience*).

- Meta-analysis: median statistical power in neuroscience ~21%
- Low-powered studies are systematically biased in effect size direction (winner's curse) AND in correlation structure
- Studies sharing low power have positively correlated false positive rates — not independent instruments
- **BIC interpretation**: underpowered studies constitute a formally correlated benchmark portfolio (shared bias mechanism → ρ̄ > 0). K_eff for a portfolio of underpowered studies << N regardless of topic diversity.

---

## K_eff Formal Instantiation

Let N = 100 published studies in a research domain.  
ρ̄ estimated from OSC 2015 replication rate: ρ̄ ≈ 0.61.

K_eff ≤ N(1-ρ̄) + ε = 100(0.39) + ε ≈ 39

Confidence intervals: if ρ̄ ∈ [0.55, 0.70]:
- K_eff ≤ 30 to 45 from nominal N = 100

**Portfolio collapse**: a literature of 100 published findings provides evidential strength equivalent to ~30–45 independent replications — despite occupying the formal space of 100 entries. Evidence accumulation appears linear; actual K_eff grows sublinearly (approximately 0.39 × rate implied by naive counting).

---

## Mechanism: CIAP × AIIP Conjunction in Scientific Context

**AIIP failure pathway**:
1. Shared statistical decision criterion (p < 0.05) across all labs → studies are not epistemically independent; they share the same decision boundary
2. Publication selection bias → published "portfolio" is a biased sample from a biased generating process → ρ̄ elevated systematically
3. Shared training and methodological conventions → researchers within a field apply similar analytical choices → correlated optimization trajectories

**CIAP propagation pathway**:
1. QRP toolkit (flexible stopping, covariate selection, DV selection, exclusion criteria) is a domain-agnostic optimization shortcut — analogous to structural CIAP in AI benchmarks
2. QRP strategy learned from field norms → propagates across all researchers simultaneously → correlated outcome distribution
3. Any analytical flexibility that "works" in study B_i transfers immediately to study B_j (same toolkit) — direct CIAP-amplification-of-AIIP-failure

**Cascade**: AIIP fails (correlated studies) + CIAP amplifies (shared QRP optimization corrupts correlated studies simultaneously) → K_eff → 0.39N << N.

---

## Ontological Type: Why Competitive/Emergent

The competitive/emergent ontological type is defined by:
- No central authority imposing OA metric (contrast: NCLB mandate, USMLE pass criterion)
- OA emerges from distributed competitive selection (citation counts, grant success, career advancement)
- CIAP propagates through competitive transmission (successful QRP strategies propagate via training, mentorship, publication pressure)
- Nash equilibrium: individual labs cannot unilaterally adopt conservative standards without career disadvantage (strategic recovery impossibility — same as ATR DC#4 mechanism)

This is structurally distinct from:
- **DC#1** (designed empirical, AI benchmark): deliberately constructed, not competitive/emergent; academic researchers designing specific AI evaluation tools
- **DC#2** (designed empirical, fine-tuning geometry): mathematical structure of optimization manifold — no competitive dynamics
- **DC#3** (regulated institutional, NCLB): top-down federal mandate + sanctions; compliance driven by legal authority, not competitive selection

The scientific publication system is the canonical competitive/emergent domain — labs compete, norms self-organize, no regulator controls OA definition. This is the third ontological type, completing BIC's evidential coverage.

---

## Additional Corroboration

- **Vul et al. 2009** ("Voodoo correlations"): social neuroscience non-independent analysis produces systematically inflated within-study correlations — intra-study BIC
- **Many Labs 1 & 2** (Klein et al. 2014, 2018): multi-site replications reveal large lab-to-lab heterogeneity — effect sizes vary 2–3× across sites, suggesting initial single-lab studies severely overestimate generalizability (further K_eff reduction beyond OSC estimate)
- **Gelman & Loken 2014** ("Garden of forking paths"): analytical flexibility is not conscious QRP but structural — researcher makes hundreds of analytical decisions, each optional individually, but the path is determined by OA (p<0.05) after data viewed. This is CIAP at the intra-study level: p-independent shortcuts propagate through the analytical pipeline.

---

## Structural Implications

**BIC DC#4 closes the competitive/emergent gap**. The K_eff collapse mechanism operates:
- When researchers design experiments deliberately (DC#1, DC#2)
- When institutions comply with regulatory mandates (DC#3)
- When labs compete in emergent, decentralized knowledge markets (DC#4)

The mechanism is ontologically invariant. Evidence portfolio diversification fails whenever AIIP fails + CIAP propagates — regardless of whether the evidence-generating agents are AI benchmark designers, test-prep teachers under AYP sanctions, or scientists competing for journal publications.

**Forward prediction** (falsifiable): Pre-registration and open data requirements (OSF, AsPredicted) should increase K_eff by reducing AIIP failure — suppressing QRP (CIAP) and publication bias (AIIP). Replication rates should be higher for pre-registered studies vs. non-pre-registered. Evidence: Nosek et al. 2015 and Registered Reports literature confirm this prediction — pre-registered studies have substantially higher replication rates (~60–70% vs 36%). This is direct experimental confirmation of the K_eff mechanism: remove CIAP (QRP) and AIIP (publication selection), K_eff rises toward N.

---

**Confidence**: 0.76 → 0.78  
**BIC D4 structural criteria**: ZR 5/3 PASS (done), DC#4 (this document), 3 ontological types (complete: designed empirical ×2 + regulated institutional + competitive/emergent), 2 derivations (done).  
**Next**: C87 — BIC D4 formal elevation.
