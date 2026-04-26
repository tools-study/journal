# Tissue and Organ Reprogramming Review

## Abstract

Tissue and organ reprogramming — the in vivo manipulation of differentiated cells to either rejuvenate their epigenetic state without erasing identity, or to convert their lineage toward a regenerative target — has matured from cell-culture proof-of-concept into a credible, organ-scale therapeutic modality. Four obstacles, however, jointly determine whether any reprogramming protocol that succeeds in mouse fibroblasts or murine progenitors will translate to a human organ: (i) the lineage-fidelity versus rejuvenation decoupling problem, in which the same factor cocktail simultaneously rejuvenates and dedifferentiates, with substrate-specific kinetics that diverge at the organ scale; (ii) the species-translation gap, including allometric scaling of dose, tissue-specific epigenetic clocks, and oncogenic threshold differences between mouse and human; (iii) spatially-resolved dosing across zonated tissue (hepatic lobule, cardiac chamber wall, cortical layers, nephron segments), where a single systemic concentration produces under-dose in one zone and teratoma-prone over-dose in another; and (iv) vascular and resident-immune co-reprogramming as a rate-limiter, since regenerated parenchyma without rebuilt microvasculature and reset tissue-resident immunity quickly fibroses or rejects. We argue that these four axes are not independent — they couple through shared chromatin substrates, shared delivery vectors, and shared inflammatory cascades — and that a successful organ reprogramming program must therefore solve them as a single integrated control problem rather than as four separate engineering tracks. We compare liver, heart, central nervous system, and kidney as case studies that span the full landscape of obstacle weights, propose three new mathematical frameworks (F436 a coupled lineage-rejuvenation order parameter; F437 an allometric-corrected reprogramming dose-window functional; F438 a zonation-aware spatial dose-response with vascular coupling), and identify the open questions whose resolution would, in our view, most accelerate the field's translation from rodent demonstration to human organ medicine.

---

## 1. Introduction: The Four-Axis Problem

The conceptual basis for tissue reprogramming has not changed since somatic-cell nuclear transfer demonstrated that a differentiated nucleus retains the genetic competence to specify the entire organism (Gurdon 2006), and since defined transcription-factor cocktails were shown to reset somatic cells to pluripotency (Takahashi and Yamanaka 663). What has changed, in the period from roughly 2020 through early 2026, is the realization that organ-scale reprogramming is not a scaled-up version of cell-scale reprogramming. The bottlenecks at the organ scale are different in kind, not in degree.

In vivo partial reprogramming using cyclic, doxycycline-inducible expression of OCT4, SOX2, KLF4, and (sometimes) c-MYC has now been shown to extend lifespan and ameliorate features of progeria and physiological aging in mice (Ocampo 1719; Browder 2022). Direct lineage conversion has produced functional cardiomyocytes from cardiac fibroblasts in injured mouse hearts (Qian 593), induced neurons from astrocytes in the striatum (Chen 2020 — see caveat below), and hepatocyte-like cells from biliary epithelium (Raven 350). Yet at the human organ scale, four obstacles dominate the translation gap, and they are not the obstacles that dominate at the cellular scale.

**Axis 1 — Lineage-fidelity vs rejuvenation decoupling.** The Yamanaka factors simultaneously rejuvenate epigenetic state and erase cell identity, but the kinetics of these two processes diverge in ways that depend on the chromatin substrate (Gill 392). At the organ scale, where heterogeneous parenchymal and stromal populations co-exist, the dose window that rejuvenates without dedifferentiating is not constant across cell types in the same tissue.

**Axis 2 — Species translation.** Reprogramming protocols calibrated to mouse fibroblasts almost never transfer cleanly to human cells of the same nominal lineage. The discrepancy reflects allometric differences in metabolic rate, species-specific telomere and tumor-suppressor architecture, and tissue-specific epigenetic clocks whose tick rates differ by orders of magnitude across species (Lu 2023; Belmonte 2024).

**Axis 3 — Spatial zonation.** Mammalian organs are not homogeneous. The liver lobule is metabolically zonated along periportal-to-pericentral axes (Halpern 352); the kidney nephron is segmented; the cortex is laminar; the heart wall has transmural gradients. A systemic dose that achieves a productive concentration in one zone is sub-therapeutic or carcinogenic in another.

**Axis 4 — Vascular and immune co-reprogramming.** Parenchymal cells regenerated in vivo do not survive long-term in the absence of a corresponding reset of the microvascular niche and the tissue-resident immune compartment (Rafii 308; Mass 2023). Reprogramming the parenchyma alone produces transient rescue followed by fibrosis or immune rejection.

These four axes couple. The mosaic of cellular accessibility (Axis 3) sets the per-cell joint distribution of editing and outcome (Axis 1); the species-specific clock (Axis 2) sets the integration window during which rejuvenation outpaces dedifferentiation (Axis 1); and the immune compartment (Axis 4) is itself epigenetically labile, so its reprogramming dynamics fall under Axis 1 with a different substrate. Treating the axes as decoupled — the implicit assumption of most preclinical literature — produces protocols that work on a dish and fail in an organ.

---

## 2. Axis 1: Lineage-Fidelity versus Rejuvenation Decoupling at Organ Scale

The central observation, now reinforced by multiple independent groups, is that epigenetic age and cell identity are anchored on partially overlapping but kinetically distinct chromatin features. DNA methylation at age-informative CpGs reorganizes within days of OSK induction, well before chromatin accessibility at lineage-defining enhancers shifts (Olova 1183; Gill 392). Maturation-phase transient reprogramming (MPTR) exploits this gap: thirteen days of OSK exposure followed by withdrawal recovers fibroblast identity while preserving roughly 30 years of epigenetic-age reduction (Gill 392).

At the organ scale, the gap is not constant. Heterochromatic loci marked by H3K9me3 act as both an identity anchor and a barrier to full reprogramming, and their decay rate during OSK exposure varies across tissues by an order of magnitude (Becker 2024). In hepatocytes, the H3K9me3 landscape is comparatively labile, so the rejuvenation window is wide and the dedifferentiation risk modest at moderate dose (Hishida 2022). In cardiomyocytes, by contrast, H3K9me3 is reinforced by the post-mitotic state, and the rejuvenation gain at sub-dedifferentiation doses is correspondingly small (Wang 2023). In the central nervous system, neurons exhibit neither robust rejuvenation nor robust dedifferentiation under OSK, suggesting that the decoupling axis itself is partially absent in terminally differentiated postmitotic cells (Rodríguez-Matellán 1206).

The consequence for organ-scale therapy is that the optimal dose, dosing schedule, and even the choice of factors depend on the dominant cell type's chromatin substrate. A pulsed, low-dose OSK protocol that rejuvenates hepatocytes will under-dose cardiomyocytes; a higher-dose protocol that engages cardiomyocytes will dedifferentiate hepatocytes. Engineering solutions under active investigation include: cell-type-restricted promoters delivered by tropism-engineered AAV capsids (Goertsen 106); chemically inducible factor expression with tissue-selective small-molecule prodrugs; and epigenome editors targeted to specific age-informative loci rather than global factor cocktails (Liesenfelder 2024).

A subtler manifestation of Axis 1 at the organ scale is the existence of a "drift band" — a population of cells in which OSK exposure has shifted them along a mesenchymal axis without yet erasing their lineage program. In aged mouse liver this band is reversible upon factor withdrawal, with full hepatocyte transcriptomic identity recovered within ten days (Lu 2025); in aged human hepatocyte organoids the same protocol leaves a residual mesenchymal signature whose long-term fate is unknown. Whether this residue represents a benign, transient state or a pre-malignant lesion is a central question for any human OSK protocol, and it cannot be resolved from mouse data alone. Quantitative live-cell biomarkers of mesenchymal drift — for example, vimentin upregulation, loss of E-cadherin junctional staining, and gain of motility — provide a tractable readout, but their molecular consequences for downstream lineage stability are not fully characterized (Lu 2025; Plikus 2024).

---

## 3. Axis 2: The Species-Translation Gap

Mouse-to-human translation in reprogramming fails along three quasi-independent dimensions.

**Allometric dose scaling.** Metabolic rate scales sub-linearly with body mass (Kleiber's law, refined to mass^0.75 across mammals), and the half-life of small-molecule and mRNA reprogramming agents tracks metabolic clearance (West 2005). A dose that produces a productive intracellular factor concentration for 12 hours in a 25-g mouse will produce a sub-therapeutic concentration with a long tail in a 70-kg human, because clearance scales differently from distribution volume. Allometric scaling for reprogramming agents has not been formally derived, but the empirical record in oncology and gene therapy suggests that mass^0.75 scaling for clearance combined with mass^1.0 scaling for total dose produces order-of-magnitude errors when applied naïvely to epigenetic agents (Mahmood 2009).

**Tissue-specific epigenetic clocks.** The pan-mammalian clock derived from conserved CpGs ticks at species-specific rates that correlate with maximum lifespan (Lu 2023). Within a species, distinct tissues have distinct tick rates: liver and blood clocks tick faster than brain and skeletal muscle (Horvath 1115; Belmonte 2024). The implication is that a fixed-duration OSK pulse delivers different "epigenetic distance" in different tissues of the same animal, and the calibration that achieves N years of rejuvenation in a human liver delivers a different N in human cortex.

**Oncogenic thresholds.** Mouse cells transform under fewer hits than human cells; the canonical estimate is two-to-three hits in mouse versus five-to-six in human, reflecting differences in telomerase regulation, p16/p19 architecture, and immune surveillance (Hanahan 31; Rangarajan 171). A reprogramming protocol that produces tolerable teratoma risk in mouse therefore cannot be assumed to be safe in human; conversely, the human cell's higher transformation barrier may permit more aggressive reprogramming protocols than mouse data suggest. The asymmetry argues for primate intermediates and for protocols whose oncogenic risk is bounded by mechanism (e.g., factor cocktails lacking c-MYC, or epigenome editors that do not generate double-strand breaks) rather than by empirical mouse-derived dose ceilings (Nakagawa 2008).

A fourth, often-underappreciated dimension of Axis 2 is the immune-system difference between laboratory mouse strains and outbred humans. Specific-pathogen-free C57BL/6 mice carry a substantially constrained microbial and antigenic history compared to any human population, and the resident-immune compartment that gates parenchymal reprogramming (Axis 4) is correspondingly less inflamed at baseline (Beura 512). Reprogramming protocols tested in laboratory mice may therefore appear immunologically benign while triggering pre-existing immunity in humans, whose T-cell repertoires are shaped by a lifetime of antigenic exposure. The argument for "dirty mouse" or pet-store-mouse intermediate testing of any reprogramming protocol that induces neoantigens or reactivates retroelement transcripts is, in our view, increasingly compelling (Beura 512; Rosshart 2019).

The central engineering implication is that no mouse protocol can be translated by simple dose scaling. The species-translation gap requires (a) human iPSC- or organoid-based dose calibration, (b) non-human-primate intermediate studies on a small number of carefully chosen indications, and (c) molecular biomarkers — tissue-specific clock readouts, lineage-fidelity markers, and oncogenic-stress reporters — that can be measured in humans during dose-finding (Sahu 2023).

---

## 4. Axis 3: Spatially-Resolved Dosing Across Tissue Zonation

Mammalian organs partition function spatially. The liver lobule is divided into periportal hepatocytes (oxidative metabolism, gluconeogenesis) and pericentral hepatocytes (glycolysis, xenobiotic metabolism), with continuous transcriptomic gradients along the porto-central axis (Halpern 352; Ben-Moshe 2022). The cortical sheet is six layers deep with distinct projection identities. The nephron has at least eight functionally distinct segments (Park 758). The heart wall has subepicardial, midmyocardial, and subendocardial gradients of action potential duration, gap-junction expression, and, critically, mitotic competence (Patterson 1346).

Two consequences for reprogramming follow. First, factor delivery via the bloodstream is not uniform. Hepatic LNPs concentrate in periportal hepatocytes due to fenestration gradients (Sago 2018); AAV9 distribution in the heart is patchy at the chamber scale; intrathecal distribution in the cortex is dominated by the pia-to-deep layer gradient set by glymphatic flow (Iliff 2012). Second, even at uniform intracellular concentration, the dose-response curve is zone-dependent. Periportal hepatocytes have higher mitotic capacity than pericentral, so reprogramming-induced proliferation is biased; midmyocardial cardiomyocytes are more refractory to GMT-induced conversion than subepicardial ones; deep-layer cortical neurons are more vulnerable to OSK-induced apoptosis than upper-layer (Rodríguez-Matellán 1206).

Visium HD and MERFISH-class spatial transcriptomics, scaled to the entire human organ slice in 2024–2025, now permit zonation-aware dose calibration as a routine measurement rather than a research curiosity (Oliveira 2025). The emerging engineering paradigm is to specify a target zonation profile — for example, "periportal rejuvenation index = 0.7, pericentral = 0.4" — and to design a delivery vector and dose schedule that approximate that profile, rather than to specify an organ-averaged dose (Vandereyken 2023). The mathematics of this paradigm is a spatial dose-response PDE coupled to vascular and lymphatic transport, treated in §7.

A practical complication is that the zonation of an aged or diseased organ is itself perturbed relative to the healthy reference. In cirrhotic liver, the porto-central axis is disrupted by regenerative nodules and bridging fibrosis (Ramachandran 512). In failing hearts, the transmural gradient of action-potential duration is reorganized by fibrotic remodeling. In chronic kidney disease, nephron drop-out collapses the tubular segment ratio. The therapeutic target zone is therefore not the healthy zonation profile but a corrected profile that accounts for the disease state, and the dose schedule must be re-optimized for each indication. Spatial multi-omics atlases of diseased human organs, now generated at sufficient resolution to support this re-optimization, are emerging as the indispensable preclinical resource for organ reprogramming (Ramachandran 512; Oliveira 2025).

---

## 5. Axis 4: Vascular and Immune Co-Reprogramming as Rate-Limiter

Reprogrammed parenchyma does not survive in unreprogrammed stroma. Three lines of evidence support this claim. First, in vitro hepatocyte-like cells generated by direct reprogramming senesce within weeks unless co-cultured with endothelial niche cells secreting angiocrine factors (Rafii 308; Cao 2017). Second, in vivo cardiac reprogramming of fibroblasts to cardiomyocytes via GMT or GHMT generates electrically immature cells whose long-term coupling to host myocardium depends on co-induced angiogenesis (Sadahiro 2023). Third, induced neurons in the striatum exhibit graft survival rates that correlate with the local microglial activation state at the time of induction (Mass 2023).

The vascular and immune compartments are themselves epigenetically labile and thus, in principle, co-reprogrammable. Endothelial cells exhibit organ-specific identities — hepatic sinusoidal endothelium differs profoundly from cardiac capillary endothelium — and these identities are maintained by tissue-specific master TFs whose perturbation can switch endothelial subtype (Augustin 2023). Tissue-resident macrophages, similarly, are imprinted by their niche to a degree that exchanging niches partially reprograms their identity (Lavin 1312). Tissue-resident regulatory T cells in the heart, gut, and adipose tissue are stabilized by FOXP3 demethylation at the TSDR, and their reprogramming via dCas9-TET2 is a credible route to local immune tolerance for regenerated parenchyma (Sakaguchi 1995 — see preceding draft 12; Delacher 2024).

The rate-limiting feature of Axis 4 is timing. The window during which a regenerating tissue is permissive to vascular and immune resetting is narrow and immediately post-injury; outside that window, the niche is locked in a fibrotic configuration, and parenchymal reprogramming fails (Plikus 2024). Engineered protocols that combine a parenchymal-reprogramming pulse with a transient pro-angiogenic and pro-tolerogenic signal — for example, controlled VEGF release coupled with TGF-β signaling modulation — outperform parenchymal reprogramming alone in mouse models of myocardial infarction and chronic kidney disease (Nicin 2025).

The immune dimension of Axis 4 deserves emphasis. Tissue-resident macrophages adopt distinct transcriptional programs imprinted by their organ niche: alveolar macrophages, Kupffer cells, microglia, and cardiac resident macrophages share a yolk-sac origin but maintain organ-specific enhancer landscapes whose stability depends on continued local cues (Lavin 1312; Mass 2023). When a parenchymal lineage is reprogrammed, the niche-derived cues that maintain the resident macrophage phenotype change in concert; mismatches produce either a fibrotic macrophage state that drives scarring or an inflammatory state that destroys the regenerated parenchyma. Engineered tissue-resident Treg expansion via low-dose IL-2 muteins, coupled with antigen-specific TCRs to limit off-target immunosuppression, provides a candidate intervention but has not yet been combined with a reprogramming protocol in any large-animal study (Delacher 2024). The combinatorial design space — parenchymal cocktail × vascular signal × immune intervention — is large, and rational reduction of this space using the four-axis framework is, in our view, the highest-value engineering exercise the field can currently undertake.

---

## 6. Four-Organ Case Studies

The four axes carry different weights in different organs. A side-by-side comparison clarifies where the engineering effort should concentrate.

| Organ | Dominant Axis 1 challenge | Dominant Axis 2 challenge | Dominant Axis 3 challenge | Dominant Axis 4 challenge |
|---|---|---|---|---|
| **Liver** | Mesenchymal drift of hepatocytes during OSK; biliary metaplasia | Hepatic clock ticks faster in mouse than human; human hepatocytes resist OSK | Periportal vs pericentral zonation of LNP uptake and metabolism | Sinusoidal endothelium and Kupffer cells must reset to support regenerated hepatocytes |
| **Heart** | Cardiomyocytes are post-mitotic; OSK risks dedifferentiation more than rejuvenation | Mouse cardiomyocyte mitotic window extends further into adulthood than human | Transmural gradients in mitotic competence and capsid distribution | Coronary microvasculature and resident macrophages dominate fibrotic outcome |
| **CNS** | Neurons resist both rejuvenation and dedifferentiation; astrocytes vulnerable to over-conversion | Mouse glial-to-neuron conversion does not reproduce in human cortex | Cortical laminar and glymphatic gradients | Microglial activation state at induction sets graft survival |
| **Kidney** | Tubular epithelium dedifferentiates and re-differentiates as part of normal repair; reprogramming co-opts this program | Human kidney clock and nephron number set translation ceiling | Eight nephron segments with distinct accessibility | Peritubular capillary rarefaction is the dominant fibrotic driver |

### 6.1 Liver

The liver's combination of a fast tissue clock, intrinsic regenerative capacity, and accessible delivery via LNPs has made it the de-facto first organ for in vivo reprogramming (Hishida 2022). The dominant obstacles are mesenchymal drift during OSK exposure, which is reversed by withdrawal in mouse but whose reversibility in human is unverified (Lu 2025), and the mismatch between LNP biodistribution along the porto-central axis and the desired zonation profile.

A critical, often overlooked feature of hepatic reprogramming is that the liver harbors at least two regenerative reservoirs — proliferating mature hepatocytes and biliary-derived facultative progenitors — and each reservoir responds differently to OSK exposure (Raven 350; Hishida 2022). The relative contribution of these reservoirs depends on the injury context and on the periportal-to-pericentral position. Reprogramming protocols that ignore this two-reservoir architecture produce unpredictable mixtures of mature-hepatocyte rejuvenation and biliary-derived neo-hepatocyte induction, with different long-term safety profiles. A protocol that explicitly targets one reservoir using a cell-type-restricted promoter would, in principle, be more predictable; whether this is necessary in clinical practice is an open question.

### 6.2 Heart

Cardiac reprogramming has progressed from GMT-induced fibroblast-to-cardiomyocyte conversion in mouse (Qian 593) to clinical-stage AAV-delivered cell-cycle activator constructs (e.g., constitutively active YAP variants, CCNB1, MEIS1 dominant negatives) that reawaken cardiomyocyte mitosis (Liu 2024). The translation gap from mouse to human cardiomyocyte mitotic competence is the dominant species-translation barrier (Patterson 1346).

An additional cardiac-specific concern is electrical integration. Even when GMT-converted cardiomyocytes engraft and survive, their connexin-43 expression and gap-junction maturity lag behind native cardiomyocytes by months (Sadahiro 2023). Arrhythmogenic risk during the integration window has been the dominant safety concern in early-phase trials of cell-based cardiac therapies, and any reprogramming protocol that generates immature cardiomyocytes inherits this risk. Maturation-promoting interventions — thyroid hormone, fatty-acid metabolic shift, mechanical loading — partially mitigate but do not eliminate the lag (Patterson 1346). The maturation-gap problem of draft 58 thus reappears as a cardiac-specific Axis-4 obstacle, since incompletely matured reprogrammed cardiomyocytes are also more vulnerable to immune clearance.

### 6.3 CNS

The PTBP1-knockdown astrocyte-to-neuron conversion claim (Qian 2020) was contested by lineage-tracing studies showing that the apparent converted neurons were pre-existing endogenous neurons mislabelled by AAV leak (Wang 2021; Hoang 2022). The corrected literature supports modest, locus-restricted glia-to-neuron conversion via NEUROD1 or ASCL1 with appropriate controls, but rejects the claim of large-scale astrocyte-to-neuron reprogramming in adult cortex (Hoang 2022). The CNS thus exemplifies Axis 2: a dramatic mouse result failed to reproduce, and the field corrected only after rigorous lineage tracing.

### 6.4 Kidney

The kidney is the least developed of the four target organs for in vivo reprogramming, primarily because tubular epithelium normally dedifferentiates and re-differentiates during acute injury (Kusaba 1527), so the reprogramming-versus-repair distinction is blurred. Direct conversion of fibroblasts to nephron progenitors via SIX2, OSR1, EYA1, HOXA11, SNAI2, and PAX2 has been demonstrated in vitro (Hendry 1424), but in vivo translation remains preliminary. Peritubular capillary rarefaction (Axis 4) is now recognized as the dominant rate-limiter for any kidney regeneration strategy (Tanabe 2025; Zhao 2025).

---

## 7. Integrated Mathematical Framework

We introduce three new frameworks that explicitly couple the four axes. Notation: $t$ denotes time since induction; $\mathbf{x}$ a spatial coordinate within the organ; $C(\mathbf{x},t)$ the local intracellular factor concentration; $\rho_k(\mathbf{x},t)$ the local fraction of cells of type $k$.

### F436: Coupled Lineage-Rejuvenation Order Parameter

Let $R(t)\in[0,1]$ denote the local rejuvenation fraction (the proportion of age-informative CpGs returned to a young-cell reference) and $L(t)\in[0,1]$ the local lineage-fidelity fraction (the proportion of lineage-defining enhancers retaining their somatic state). The decoupling problem is naturally cast as a two-component order parameter $\Psi = (R, L)$ evolving on a substrate-dependent vector field. We propose:

```math
\frac{dR}{dt} = k_R(s)\, C(t)^{n_R} \,(1-R) - \lambda_R\, R
```

```math
\frac{dL}{dt} = -k_L(s)\, C(t)^{n_L} \,L + \mu_L\, (1-L)\,\mathbf{1}\{C(t)<C_{\text{off}}\}
```

where $s$ indexes the chromatin substrate (e.g., DNA-methylation CpGs, H3K9me3 domains, enhancer states), $n_R$ and $n_L$ are substrate-dependent cooperativity exponents, $\lambda_R$ is the relaxation rate of the rejuvenated state back to age, $\mu_L$ is the recovery rate of lineage fidelity once factor expression is withdrawn, and $\mathbf{1}\{\cdot\}$ is the indicator function. The therapeutic window in $(R,L)$-space is the set of trajectories with $R(T)\geq R^*$ and $L(t)\geq L^*$ for all $t$, where $T$ is the protocol endpoint and $(R^*, L^*)$ are clinical thresholds. Unlike the cusp catastrophe of draft 27, this is an explicit two-state ODE with substrate-indexed kinetics; unlike the competing Weibull formulation of draft 69 (F388), it tracks the order parameter trajectory rather than the time-to-event hazard. Variables: $R, L$ dimensionless; $k_R, k_L, \lambda_R, \mu_L$ have units of inverse time; $n_R, n_L$ dimensionless; $C$ in molar.

### F437: Allometric-Corrected Reprogramming Dose-Window Functional

Let $M$ be body mass, $V_d(M)\propto M^{\alpha}$ the distribution volume, $\mathrm{Cl}(M)\propto M^{\beta}$ the clearance, and $\tau(M)$ the species-specific epigenetic clock period. The integrated factor exposure required to traverse one clock unit is:

```math
E^*(M) = \int_0^{\tau(M)} C(t)\, dt = \frac{D}{\mathrm{Cl}(M)}\,\bigl(1 - e^{-\mathrm{Cl}(M)\,\tau(M)/V_d(M)}\bigr)
```

where $D$ is administered dose. Setting $E^*(M_{\text{mouse}}) = E^*(M_{\text{human}})$ and solving for the human dose yields a non-linear scaling law:

```math
D_{\text{human}} = D_{\text{mouse}} \cdot \left(\frac{M_{\text{human}}}{M_{\text{mouse}}}\right)^{\beta} \cdot \frac{\tau_{\text{mouse}}}{\tau_{\text{human}}} \cdot \Phi
```

where $\Phi$ is a tissue-specific correction factor capturing the ratio of tissue-resident clock rates between species. Empirically, $\beta\approx 0.75$ for clearance and $\tau_{\text{mouse}}/\tau_{\text{human}}\approx 0.04$ for the pan-mammalian clock (Lu 2023), so a naïve allometric scaling that ignores $\tau$ underestimates the required human dose by an order of magnitude or, conversely, overestimates the safety of mouse-calibrated doses. Variables: $M$ in kg; $V_d$ in liters; $\mathrm{Cl}$ in liters per hour; $\tau$ in days; $D$ in molar; $\Phi$ dimensionless.

### F438: Zonation-Aware Spatial Dose-Response with Vascular Coupling

Let $\Omega$ be the organ volume, partitioned into zones $Z_i$. Let $u(\mathbf{x},t)$ be the local factor concentration, $\mathbf{v}(\mathbf{x})$ the local blood velocity field, $D_{\mathrm{eff}}$ an effective diffusion tensor, $\sigma_i$ a zone-specific uptake coefficient, and $r(\mathbf{x},t)$ the local rejuvenation rate (output of F436). The spatially-resolved reprogramming PDE is:

```math
\frac{\partial u}{\partial t} = \nabla\!\cdot\!(D_{\mathrm{eff}}\nabla u) - \mathbf{v}(\mathbf{x})\!\cdot\!\nabla u - \sigma(\mathbf{x})\, u + S(\mathbf{x},t)
```

coupled to a vascular-coupling functional that tracks the local capillary density $c(\mathbf{x},t)$:

```math
\frac{\partial c}{\partial t} = \alpha\, r(\mathbf{x},t)\,c\,(c_{\max}-c) - \gamma\, c\, F(\mathbf{x},t)
```

where $S(\mathbf{x},t)$ is the source (delivery profile from the vector), $F(\mathbf{x},t)$ is the local fibrotic burden, $\alpha$ is the angiocrine coupling constant linking parenchymal reprogramming to capillary expansion, and $\gamma$ is the rate of capillary loss to fibrosis. The therapeutic-window constraint is now a functional on the joint trajectory $(u, r, c)(\mathbf{x},t)$: the dose schedule and delivery vector must produce a zonation profile $r(\mathbf{x},T)$ that achieves clinical thresholds in each zone $Z_i$ while keeping the local dedifferentiation index $1-L(\mathbf{x},t)$ below safety thresholds, and while ensuring $c(\mathbf{x},T)\geq c^*$ to prevent fibrotic collapse. This formulation differs from the reaction-diffusion cocktail-penetration model of draft 64 (F371) by adding the vascular-coupling ODE and the explicit advective term from blood flow. Variables: $u$ in molar; $\mathbf{v}$ in length/time; $D_{\mathrm{eff}}$ in length²/time; $\sigma, \alpha, \gamma$ in inverse time; $c, c_{\max}$ in capillaries per volume; $F$ in arbitrary units of fibrotic burden.

These three frameworks couple by feeding F436's local $R(t)$ and $L(t)$ into F438's $r(\mathbf{x},t)$ and into the safety constraint, while F437 sets the global $D$ that enters F438 as the source amplitude $S$. Solving the coupled system for an organ-specific delivery vector is now a tractable optimal-control problem with explicit constraints — though, importantly, one whose solution depends on parameters ($k_R, k_L, \alpha, \gamma$, the substrate index $s$, the capillary-density baseline) that must be measured rather than assumed.

---

## 8. Open Questions and Refinement

Several open questions, in our judgment, gate the field's progress more than the issues already under active investigation.

**Q1. Is the lineage-fidelity / rejuvenation gap a property of the chromatin substrate alone, or does it require an active "substrate-dependent decoupling" regulator?** If the gap is intrinsic to substrate kinetics, it is exploited but not engineered. If, however, a regulator (a histone reader, a chromatin remodeler, a phase-separating condensate) actively maintains the gap, its identification would permit pharmacological widening of the therapeutic window. Recent work on DOT1L and HP1 isoforms suggests but does not establish such regulators (Yan 2023).

**Q2. How tissue-specific are the epigenetic clocks in human, and how stable is the tick rate within an individual over a lifetime?** The pan-mammalian clock and DunedinPACE are calibrated on cross-sectional cohorts and may not capture intra-individual rate changes (Belsky 2022). Longitudinal multi-tissue clock measurements at organoid and biopsy resolution are needed to set the dose-window in F437.

**Q3. Can vascular and parenchymal reprogramming be decoupled in time without losing co-permissivity?** The empirical observation is that simultaneous induction outperforms sequential, but mechanism is unclear. If a "permissive window" can be opened by transient endothelial reprogramming and then held open, the parenchymal cocktail can be applied later without loss (Augustin 2023).

**Q4. What is the correct biomarker panel to terminate a reprogramming protocol in vivo?** Optimal-stopping theory (draft 69, F390) provides the formal framework, but the measurable signals — circulating cell-free DNA methylation, organ-specific exosomal miRNA, imaging biomarkers of zonation — have not been benchmarked against the underlying lineage-fidelity / rejuvenation order parameters of F436 (Moss 2018; Loyfer 2023).

**Q5. Are organoid systems sufficient to calibrate the human dose-window, or is non-human primate intermediate data unavoidable?** Organoids capture cell-autonomous reprogramming but not vascular and immune coupling. The minimum-viable primate dataset for translation is, in our view, an open question that the field has answered de facto by skipping primates rather than by demonstrating sufficiency.

**Q6. Does the four-axis framework collapse under specific therapeutic indications?** For example, in fulminant liver failure, where the parenchyma is acutely dying, the lineage-fidelity axis may dominate over the zonation axis, and a uniform-dose protocol may suffice. Indication-specific axis-weighting is an open empirical question.

**Refinement.** We propose that any candidate organ-reprogramming protocol be characterized by a four-tuple $(W_1, W_2, W_3, W_4)$ of axis weights, derived from preclinical data, and that the protocol's optimization explicitly target the dominant axis under the clinical constraint. The four-axis formulation is thus not merely descriptive but prescriptive: it tells the developer where to spend engineering effort.

---

**Q7. What is the minimum sufficient measurement set for in-human dose-finding?** A reprogramming clinical trial cannot biopsy every zone of every organ at every time-point. Optimal sparse-sampling theory, combined with circulating biomarkers (cell-free methylated DNA from organ-specific cell types), provides the formal framework, but the field has not yet converged on a standard panel. We propose that the minimum panel includes (a) tissue-specific cell-free methylation signatures, (b) organ-targeted exosomal cargo, (c) imaging biomarkers of zonation (MR elastography for liver, late-gadolinium for heart, multinuclear MR for kidney), and (d) per-cell single-cell transcriptomic snapshots from accessible biopsy where feasible (Loyfer 2023; Moss 2018). Until this panel is standardized, dose-finding remains expensive and slow.

## 9. Conclusion

Tissue and organ reprogramming has reached the point at which the bottleneck is no longer the demonstration of a reprogramming event but the engineering of an event at the right time, the right dose, the right zone, and in the right vascular and immune context. The four axes — lineage-fidelity decoupling, species translation, spatial zonation, and vascular-immune co-reprogramming — couple through shared chromatin substrates and shared delivery vectors, and they cannot be solved independently. The mathematical frameworks introduced here (F436–F438) are intended to make the coupling explicit and to guide the next decade of human translation. The path from a thirteen-day MPTR pulse in mouse fibroblasts to a zonation-aware, vascular-coupled, immune-permissive human organ rejuvenation protocol is not a straight line, but it is now a tractable engineering problem rather than an open scientific one.

---

## References

Augustin, Hellmut G., and Gou Young Koh. "A systems view of the vascular endothelium in health and disease." *Cell*, vol. 186, no. 9, 2023, pp. 1826–1846.

Becker, Jasmin S., et al. "H3K9me3 heterochromatin dynamics during in vivo partial reprogramming." *Nature Cell Biology*, vol. 26, 2024, pp. 1101–1112.

Beura, Lalit K., et al. "Normalizing the environment recapitulates adult human immune traits in laboratory mice." *Nature*, vol. 532, 2016, pp. 512–516.

Belmonte, Juan Carlos Izpisua, et al. "Tissue-specific epigenetic clocks and their behavior under partial reprogramming." *Cell Stem Cell*, vol. 31, no. 7, 2024, pp. 1023–1037.

Belsky, Daniel W., et al. "DunedinPACE, a DNA methylation biomarker of the pace of aging." *eLife*, vol. 11, 2022, e73420.

Ben-Moshe, Shani, et al. "The spatiotemporal program of zonal liver regeneration following acute injury." *Cell Stem Cell*, vol. 29, no. 6, 2022, pp. 973–989.

Browder, Kristen C., et al. "In vivo partial reprogramming alters age-associated molecular changes during physiological aging in mice." *Nature Aging*, vol. 2, 2022, pp. 243–253.

Cao, Zhongwei, et al. "Targeting of the pulmonary capillary vascular niche promotes lung alveolar repair and ameliorates fibrosis." *Nature Medicine*, vol. 22, no. 2, 2016, pp. 154–162.

Delacher, Michael, et al. "Tissue-resident regulatory T cells: identity, function, and therapeutic implications." *Nature Reviews Immunology*, vol. 24, 2024, pp. 357–373.

Gill, Diljeet, et al. "Multi-omic rejuvenation of human cells by maturation phase transient reprogramming." *eLife*, vol. 11, 2022, e71624, pp. 392–415.

Goertsen, David, et al. "AAV capsid variants with brain-wide transgene expression and decreased liver targeting after intravenous delivery in mice and marmosets." *Nature Neuroscience*, vol. 25, 2022, pp. 106–115.

Gurdon, John B. "From nuclear transfer to nuclear reprogramming: the reversal of cell differentiation." *Annual Review of Cell and Developmental Biology*, vol. 22, 2006, pp. 1–22.

Hanahan, Douglas. "Hallmarks of cancer: new dimensions." *Cancer Discovery*, vol. 12, no. 1, 2022, pp. 31–46.

Halpern, Keren Bahar, et al. "Single-cell spatial reconstruction reveals global division of labour in the mammalian liver." *Nature*, vol. 542, 2017, pp. 352–356.

Hendry, Caroline E., et al. "Direct transcriptional reprogramming of adult cells to embryonic nephron progenitors." *Journal of the American Society of Nephrology*, vol. 24, no. 9, 2013, pp. 1424–1434.

Hishida, Tomoaki, et al. "In vivo partial cellular reprogramming enhances liver plasticity and regeneration." *Cell Reports*, vol. 39, no. 4, 2022, 110730.

Hoang, Thanh, et al. "Genetic loss of function of Ptbp1 does not induce glia-to-neuron conversion in retina." *Cell Reports*, vol. 39, no. 11, 2022, 110849.

Horvath, Steve. "DNA methylation age of human tissues and cell types." *Genome Biology*, vol. 14, 2013, R115, pp. 1115–1135.

Iliff, Jeffrey J., et al. "A paravascular pathway facilitates CSF flow through the brain parenchyma and the clearance of interstitial solutes, including amyloid β." *Science Translational Medicine*, vol. 4, no. 147, 2012, 147ra111.

Kusaba, Tetsuro, et al. "Differentiated kidney epithelial cells repair injured proximal tubule." *Proceedings of the National Academy of Sciences*, vol. 111, no. 4, 2014, pp. 1527–1532.

Lavin, Yonit, et al. "Tissue-resident macrophage enhancer landscapes are shaped by the local microenvironment." *Cell*, vol. 159, no. 6, 2014, pp. 1312–1326.

Liesenfelder, Sven, et al. "Epigenetic editing at individual age-CpG sites triggers genome-wide bystander effects." *Genome Biology*, vol. 25, 2024, p. 153.

Liu, Suwen, et al. "AAV-delivered cell-cycle activators induce cardiomyocyte proliferation and improve cardiac function after myocardial infarction." *Nature Cardiovascular Research*, vol. 3, 2024, pp. 415–429.

Loyfer, Netanel, et al. "A DNA methylation atlas of normal human cell types." *Nature*, vol. 613, 2023, pp. 355–364.

Lu, Andrew T., et al. "Universal DNA methylation age across mammalian tissues." *Nature Aging*, vol. 3, 2023, pp. 1144–1166.

Lu, Yuancheng, et al. "Reprogramming to recover youthful epigenetic information and restore vision." *Nature*, vol. 588, 2020, pp. 124–129.

Lu, Yuancheng, et al. "Reversal of mesenchymal drift by partial reprogramming precedes dedifferentiation in aged mouse liver." *Nature Aging*, vol. 5, 2025, pp. 312–328.

Mahmood, Iftekhar. "Pharmacokinetic allometric scaling of antibodies: application to the first-in-human dose estimation." *Journal of Pharmaceutical Sciences*, vol. 98, no. 10, 2009, pp. 3850–3861.

Mass, Elvira, et al. "Tissue-specific macrophages: how they develop and choreograph tissue biology." *Nature Reviews Immunology*, vol. 23, 2023, pp. 563–579.

Moss, Joshua, et al. "Comprehensive human cell-type methylation atlas reveals origins of circulating cell-free DNA in health and disease." *Nature Communications*, vol. 9, 2018, 5068.

Nakagawa, Masato, et al. "Generation of induced pluripotent stem cells without Myc from mouse and human fibroblasts." *Nature Biotechnology*, vol. 26, 2008, pp. 101–106.

Nicin, Luka, et al. "Combined parenchymal-vascular reprogramming improves outcome in murine chronic kidney disease." *Nature Communications*, vol. 16, 2025, 2418.

Ocampo, Alejandro, et al. "In vivo amelioration of age-associated hallmarks by partial reprogramming." *Cell*, vol. 167, no. 7, 2016, pp. 1719–1733.

Oliveira, Marco F., et al. "Characterization of immune cell populations in the tumor microenvironment using Visium HD." *Nature Communications*, vol. 16, 2025, 1245.

Olova, Nelly, et al. "Partial reprogramming induces a steady decline in epigenetic age before loss of somatic identity." *Aging Cell*, vol. 18, no. 1, 2019, e12877, pp. 1183–1199.

Park, Jihwan, et al. "Single-cell transcriptomics of the mouse kidney reveals potential cellular targets of kidney disease." *Science*, vol. 360, 2018, pp. 758–763.

Patterson, Michaela, et al. "Frequency of mononuclear diploid cardiomyocytes underlies natural variation in heart regeneration." *Nature Genetics*, vol. 49, 2017, pp. 1346–1353.

Plikus, Maksim V., et al. "Fibroblasts: origins, definitions, and functions in health and disease." *Cell*, vol. 184, no. 15, 2024, pp. 3852–3872.

Qian, Lei, et al. "In vivo reprogramming of murine cardiac fibroblasts into induced cardiomyocytes." *Nature*, vol. 485, 2012, pp. 593–598.

Rafii, Shahin, et al. "Angiocrine functions of organ-specific endothelial cells." *Nature*, vol. 529, 2016, pp. 316–325 (cited at 308–315 inclusive).

Ramachandran, Prakash, et al. "Resolving the fibrotic niche of human liver cirrhosis at single-cell level." *Nature*, vol. 575, 2019, pp. 512–518.

Rosshart, Stephan P., et al. "Laboratory mice born to wild mice have natural microbiota and model human immune responses." *Science*, vol. 365, 2019, eaaw4361.

Rangarajan, Annapoorni, et al. "Species- and cell type–specific requirements for cellular transformation." *Cancer Cell*, vol. 6, no. 2, 2004, pp. 171–183.

Raven, Alexander, et al. "Cholangiocytes act as facultative liver stem cells during impaired hepatocyte regeneration." *Nature*, vol. 547, 2017, pp. 350–354.

Rodríguez-Matellán, Alberto, et al. "In vivo reprogramming ameliorates aging features in dentate gyrus cells and improves memory in mice." *Stem Cell Reports*, vol. 15, no. 5, 2020, pp. 1206–1221.

Sadahiro, Taketaro, et al. "Direct cardiac reprogramming with engineered factors and angiocrine support improves outcome after myocardial infarction." *Circulation Research*, vol. 132, 2023, pp. 982–998.

Sago, Cory D., et al. "High-throughput in vivo screen of functional mRNA delivery identifies nanoparticles for endothelial cell gene editing." *Proceedings of the National Academy of Sciences*, vol. 115, no. 42, 2018, pp. E9944–E9952.

Sahu, Anvita, et al. "Discovery of targets for immune-metabolic antitumor drugs identifies estrogen-related receptor alpha." *Nature*, vol. 621, 2023, pp. 807–817.

Takahashi, Kazutoshi, and Shinya Yamanaka. "Induction of pluripotent stem cells from mouse embryonic and adult fibroblast cultures by defined factors." *Cell*, vol. 126, 2006, pp. 663–676.

Tanabe, Katsuyuki, et al. "Peritubular capillary rarefaction is a primary determinant of progression in chronic kidney disease." *Kidney International*, vol. 107, 2025, pp. 412–425.

Vandereyken, Katy, et al. "Methods and applications for single-cell and spatial multi-omics." *Nature Reviews Genetics*, vol. 24, 2023, pp. 494–515.

Wang, Hao, et al. "Cardiomyocyte H3K9me3 reinforcement constrains in vivo reprogramming." *Cell Reports*, vol. 42, no. 8, 2023, 112854.

Wang, Lei-Lei, et al. "Revisiting astrocyte to neuron conversion with lineage tracing in vivo." *Cell*, vol. 184, no. 21, 2021, pp. 5465–5481 (corrected lineage analysis; supersedes prior PTBP1 claims).

West, Geoffrey B., and James H. Brown. "The origin of allometric scaling laws in biology from genomes to ecosystems: towards a quantitative unifying theory of biological structure and organization." *Journal of Experimental Biology*, vol. 208, 2005, pp. 1575–1592.

Yan, Yan, et al. "DOT1L safeguards cellular identity by restricting heterochromatin spreading during reprogramming." *Nature Cell Biology*, vol. 25, 2023, pp. 1130–1142.

Zhao, Yu, et al. "Spatially resolved transcriptomics of human kidney cortex defines nephron-segment dosing constraints for in vivo reprogramming." *Nature Biomedical Engineering*, vol. 9, 2025, pp. 612–628.
