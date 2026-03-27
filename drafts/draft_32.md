# Cellular Rejuvenation: Challenges and Experiments

---

## Abstract

Partial reprogramming with Oct4, Sox2, and Klf4 (OSK) has demonstrated the capacity to reverse epigenetic age by approximately 30 years in human fibroblasts and extend lifespan in aged mice. However, achieving deeper rejuvenation — such as the reversal of a 60-year-old cell to a 20-year-old epigenetic state (approximately 40-year reversal) — remains unrealized. This paper identifies and ranks seven primary scientific and technical obstacles to deep in vivo rejuvenation without cell identity loss, proposes mechanistic solutions grounded in current evidence, and designs seven complementary mouse experiments in aged dermal fibroblasts to address each obstacle. We argue that the principal barrier is the age-associated redistribution of histone H3 lysine 9 trimethylation (H3K9me3) to gene-rich euchromatic regions, creating pioneer factor-refractory chromatin domains that impose a rejuvenation ceiling. We propose that co-delivery of the H3K9me3 demethylase KDM4D with OSK via lipid nanoparticle-encapsulated mRNA can lower this barrier and extend rejuvenation depth beyond current limits. Five novel mathematical frameworks — stochastic resetting theory, control barrier functions, *k*-out-of-*n* system reliability, partially observed Markov decision processes, and Gamma process degradation modeling — provide quantitative predictions for experimental design and outcome interpretation.

---

## 1. Introduction

The discovery that differentiated somatic cells can be reprogrammed to pluripotency by defined transcription factors (Ocampo et al., 2016) established that the epigenetic information encoding youthful cellular states is not irreversibly lost during aging. Subsequent work demonstrated that *partial* reprogramming — transient expression of Yamanaka factors followed by withdrawal before dedifferentiation — can reverse age-associated molecular changes without eliminating cell identity (Ocampo et al., 2016). Expression of Oct4, Sox2, and Klf4 without the oncogene c-Myc (the OSK combination) restored youthful DNA methylation patterns and reversed vision loss in aged murine retinal ganglion cells (Lu et al., 2020). In human dermal fibroblasts, maturation phase transient reprogramming (MPTR) achieved approximately 30-year rejuvenation as measured by transcriptomic and epigenetic clocks, with restoration of collagen production and wound-healing capacity (Gill et al., 2022). Long-term cyclic OSK expression in physiologically aged wild-type mice reduced biological age in skin and kidney without tumor formation over seven to ten months of treatment (Browder et al., 2022). Even a single one-week cycle of transient OSKM expression rejuvenated DNA methylation and transcriptomic signatures across multiple tissues in naturally aged mice (Chondronasiou et al., 2022).

Despite these advances, no published study has demonstrated rejuvenation exceeding approximately 30 years in human cells or equivalent depth in murine models. This ceiling raises a fundamental question: **is the approximately 30-year reversal a technical limitation of current protocols, or does it reflect a deeper biological barrier?**

The Inducible Changes to the Epigenome (ICE) mouse model provided causal evidence that epigenetic information loss drives mammalian aging, with OSK reversing up to 57% of accumulated epigenetic age across four independent clocks (Yang et al., 2023). This suggests that youthful epigenetic information persists as a recoverable record and that the rejuvenation ceiling is not imposed by information destruction. Instead, we propose that it reflects the resistance of specific chromatin domains to pioneer factor-mediated remodeling.

OSK factors function as pioneer transcription factors capable of engaging closed chromatin (Soufi et al., 2012). However, megabase-scale domains marked by H3K9me3 — the hallmark of constitutive heterochromatin — are refractory to even pioneer factor binding, constituting the dominant impediment to complete reprogramming (Soufi et al., 2012; Chen et al., 2013). Critically, aging involves a genome-wide *redistribution* of H3K9me3: global levels decline (Pearson r = −0.35, P = 9.7 × 10⁻⁹ across 1,814 human ChIP-seq samples; de Lima Camillo et al., 2025), while specific gene-rich euchromatic regions acquire *de novo* H3K9me3 marks (Li et al., 2021). We hypothesize that these newly H3K9me3-marked regions at reprogramming-relevant loci constitute the ceiling that limits partial rejuvenation to approximately 30 years, and that their targeted removal via co-delivery of KDM4-family histone demethylases with OSK can extend rejuvenation depth to the 40-year range required for meaningful clinical translation.

This paper identifies seven obstacles to achieving deep epigenetic rejuvenation (60→20 biological years) in vivo, ranked by difficulty and priority. For each obstacle, we present the evidence base, propose a mechanistic solution, and design a mouse experiment in aged (24-month) C57BL/6 dermal fibroblasts. Five novel mathematical frameworks provide quantitative scaffolding for experimental design and data interpretation.

---

## 2. Obstacle 1: H3K9me3 Heterochromatin Resistance to Pioneer Factor-Mediated Rejuvenation

**Difficulty: Very High | Priority: Critical**

### 2.1 The Age-Associated H3K9me3 Redistribution Paradox

The relationship between H3K9me3 and aging is paradoxical. A pan-tissue analysis of seven histone modifications across 1,814 human samples spanning embryonic to age 90+ revealed that global H3K9me3 levels decline significantly with age (de Lima Camillo et al., 2025). Age-associated decline of the principal H3K9 methyltransferase SUV39H1 has been documented in both human and mouse hematopoietic stem cells, leading to heterochromatin perturbation and impaired B lymphoid differentiation (Djeghloul et al., 2016). In human diploid lung fibroblasts, SUV39H1 downregulation during replicative senescence correlates with decreased H3K9me3 at satellite repeats and transposable elements, resulting in genomic instability through aberrant repetitive element transcription (Sidler et al., 2014).

However, this global decline coexists with region-specific *de novo* H3K9me3 acquisition. In aged *Caenorhabditis elegans* somatic tissues, approximately 500 genomic regions in gene-rich euchromatic zones gained significant H3K9me3, even as canonical heterochromatic arms lost it (Li et al., 2021). Single-nucleus ATAC-seq across young, middle-aged, and old mouse tissues revealed increased chromatin accessibility within heterochromatin domains in aged excitatory neurons, accompanied by LINE1 transposable element activation (Zhang et al., 2022). This dual phenomenon — constitutive heterochromatin erosion with ectopic heterochromatin formation — represents the H3K9me3 redistribution paradox that we propose is central to the rejuvenation ceiling.

Direct causal evidence for the role of H3K9me3 in aging was provided by a novel mouse strain carrying a triple knockout of the three H3K9 methyltransferases (SUV39H1, SUV39H2, and SETDB1): inducible loss of H3K9me3 in adult mice resulted in premature aging phenotypes including reduced lifespan, decreased body weight, multi-organ degeneration (skin thinning, intestinal atrophy), and significant upregulation of transposable elements (Montavon et al., 2024). A comprehensive 2024 review synthesized evidence that heterochromatin loss, combined with telomere attrition and DNA damage, drives cellular senescence through convergent genome instability, innate immunity activation, and chronic inflammation (Wu et al., 2024). The ectopic H3K9me3 domains that accumulate at gene promoters with age thus represent a double obstacle: they both silence rejuvenation-relevant genes and resist the pioneer factor engagement necessary for their reactivation.

### 2.2 Pioneer Factor Exclusion from H3K9me3 Domains

The molecular basis for the H3K9me3 barrier was established by genome-wide mapping of Oct4, Sox2, Klf4, and c-Myc binding during the first 48 hours of human fibroblast reprogramming (Soufi et al., 2012). While OSK factors function as pioneer transcription factors capable of binding nucleosomal DNA at most closed chromatin sites, megabase-scale H3K9me3-marked heterochromatin domains are refractory to their engagement. Structural analysis revealed that Oct4 and Klf4 recognize partial DNA motifs on the nucleosome surface, while Sox2 targets a motif permitting half the normal DNA bending — but the higher-order compaction imposed by H3K9me3 physically excludes even these pioneer factors (Soufi et al., 2015).

The functional consequences are profound. H3K9 methylation was identified as the primary epigenetic determinant trapping cells in the pre-iPSC state — a partially reprogrammed intermediate that fails to activate the endogenous pluripotency network (Chen et al., 2013). BMP signaling upregulates H3K9 methyltransferases to enforce this arrest, while overexpression of the demethylase KDM4B promotes conversion of pre-iPSCs to fully reprogrammed iPSCs (Chen et al., 2013). Proteomic analysis confirmed that iPSCs are depleted of H3K9me2/me3 relative to somatic cells, and that inhibition of the H3K9me reader HP1γ (Cbx3) also enhances reprogramming, implicating the entire writer-reader axis as an epigenetic roadblock (Sridharan et al., 2013).

In the context of aging, we propose that the ectopic H3K9me3 domains that accumulate at gene-rich regions create a *neo-heterochromatic barrier* that partial reprogramming via OSK alone cannot surmount. The approximately 30-year reversal achieved by current protocols may represent the depth of rejuvenation achievable by OSK-mediated remodeling of accessible chromatin — the "easy" CpG sites — while the remaining 10+ years of epigenetic age reside in H3K9me3-locked loci that require targeted chromatin remodeling.

### 2.3 The KDM4 Solution

The KDM4 (JMJD2) family of Jumonji-domain histone demethylases catalyzes the removal of H3K9me3 and H3K9me2 through iron(II)- and 2-oxoglutarate-dependent oxidative mechanisms. KDM4B overexpression in transgenic mice increased iPSC reprogramming efficiency 6-fold from cloned blastocysts and 9-fold from fibroblasts (Matoba et al., 2017). KDM4A plays an essential role in natural reprogramming during the maternal-to-zygotic transition, actively preventing H3K9me3 from invading broad H3K4me3 domains in oocytes; its loss causes aberrant H3K9me3 accumulation and developmental failure (Sankar et al., 2020). In Hutchinson-Gilford progeria syndrome (HGPS), the mutant lamin A protein (progerin) stabilizes SUV39H1, leading to pathological H3K9me3 elevation; genetic depletion of SUV39H1 reduced H3K9me3 levels, restored DNA repair capacity, and extended lifespan in progeroid mice by approximately 60% (Liu et al., 2013).

These data converge on a clear therapeutic hypothesis: **co-delivery of KDM4D (the catalytic subunit with the most restricted substrate specificity among KDM4 family members) with OSK should lower the H3K9me3 barrier at age-acquired ectopic heterochromatin domains, extending the depth of rejuvenation beyond the approximately 30-year ceiling.**

### 2.4 The Selectivity Problem: Ectopic Versus Constitutive H3K9me3

A critical concern with untargeted KDM4D co-delivery is the potential for indiscriminate H3K9me3 removal. Constitutive pericentromeric heterochromatin — marked by dense H3K9me3 deposited by SUV39H1/2 during development — silences satellite repeats and transposable elements, maintains chromosome segregation fidelity, and suppresses inflammatory responses triggered by cytosolic DNA detection via the cGAS-STING pathway (Tsurumi & Li, 2012; Wu et al., 2024). Age-associated heterochromatin erosion at these constitutive domains is already a driver of genomic instability (Sidler et al., 2014); further removal of pericentromeric H3K9me3 by exogenous KDM4D could paradoxically *accelerate* aging through LINE1 element reactivation and cGAS-STING-mediated inflammaging.

Several lines of evidence suggest that KDM4D possesses an inherent preference for euchromatic over pericentromeric H3K9me3. KDM4D lacks the tandem Tudor domains present in KDM4A-C that mediate recruitment to constitutive heterochromatin, resulting in a predominantly euchromatic localization pattern (Matoba et al., 2017). Nonetheless, the inherent selectivity of wild-type KDM4D may be insufficient for the deep rejuvenation protocol proposed here, where higher or prolonged KDM4D activity is required to access the most refractory age-acquired domains.

We therefore propose a precision-targeted alternative: **a dCas9-KDM4D fusion guided by single-guide RNAs (sgRNAs) designed to target the specific age-acquired H3K9me3 domains** identified by comparing ChIP-seq profiles of young versus aged dermal fibroblasts. The catalytically dead Cas9 (dCas9) provides programmable DNA targeting without cleavage, while the fused KDM4D catalytic domain executes H3K9me3 removal exclusively at specified loci. A panel of 20-50 sgRNAs targeting the most recurrent age-acquired H3K9me3 peaks would focus demethylation on the therapeutically relevant loci while leaving constitutive heterochromatin undisturbed.

This locus-specific strategy offers three advantages: (i) elimination of off-target H3K9me3 removal at pericentromeric regions; (ii) dose reduction, as the catalytic activity is concentrated at desired sites; and (iii) a built-in specificity control — pericentromeric H3K9me3 levels measured by CUT&Tag serve as an internal safety biomarker.

### 2.5 Mathematical Framework: Stochastic Resetting Theory for Pulsatile Rejuvenation

Partial reprogramming protocols employ pulsatile dosing — typically 2 days of OSK expression followed by 5 days of withdrawal (Ocampo et al., 2016; Browder et al., 2022). Each pulse partially resets the epigenetic clock before the cell begins re-aging during the off-period. This cyclical process is naturally modeled by the theory of stochastic processes under resetting (Evans et al., 2020), which has not been previously applied to epigenetic rejuvenation.

Let *A*(*t*) denote the epigenetic age of a cell at time *t*, evolving according to a stochastic aging process with drift rate *v* (the natural rate of epigenetic aging) and diffusion coefficient *D* (capturing cell-to-cell variability):

```math
dA = v \, dt + \sqrt{2D} \, dW(t), \quad A(0) = A_0
```

where *W*(*t*) is a standard Wiener process, *v* is the epigenetic aging drift rate (years of biological age per year of chronological time), and *D* is the diffusion coefficient reflecting stochastic variability in aging rate across cells.

At each reprogramming pulse (occurring at exponentially distributed intervals with rate *r*), the epigenetic age is partially reset:

```math
A \to A - \Delta(A, \mathbf{c}), \quad \Delta(A, \mathbf{c}) = \delta_{\max}(\mathbf{c}) \cdot \frac{A^h}{A^h + K_A^h}
```

where **c** is the vector of reprogramming factor concentrations (OSK and optionally KDM4D), *δ*_max(**c**) is the maximum age reduction achievable per pulse (dependent on factor composition), *K*_A is the half-maximal age for rejuvenation efficiency, *h* is the Hill coefficient governing the age-dependence of rejuvenation sensitivity, and *δ*_max is modeled as:

```math
\delta_{\max}(\mathbf{c}) = \delta_{\text{OSK}} + \delta_{\text{KDM4}} \cdot \frac{[\text{KDM4}]^{n_K}}{[\text{KDM4}]^{n_K} + K_D^{n_K}}
```

where *δ*_OSK is the rejuvenation depth from OSK alone (approximately 30 years at saturation), *δ*_KDM4 is the additional depth contributed by KDM4-mediated H3K9me3 removal, *K*_D is the KDM4 half-maximal effective concentration, and *n*_K is the KDM4 Hill coefficient reflecting cooperative demethylation of multi-nucleosome domains.

In the steady-state limit of many resetting cycles, the non-equilibrium stationary distribution of epigenetic age *P*_ss(*A*) obeys:

```math
P_{\text{ss}}(A) = \frac{r}{v} \exp\left(-\frac{r(A - A_{\text{floor}})}{v}\right), \quad A \geq A_{\text{floor}}
```

where *A*_floor = *A*₀ − *δ*_max(**c**) is the minimum achievable age under the given factor composition.

**Key prediction:** With OSK alone, *A*_floor ≈ *A*₀ − 30 years. With OSK + KDM4D at sufficient concentration, *A*_floor = *A*₀ − (30 + *δ*_KDM4) years, potentially reaching the 40-year target. The optimal resetting rate *r** that minimizes the expected steady-state age is:

```math
r^* = \frac{v}{\langle\Delta\rangle}\left(1 + \sqrt{1 + \frac{2D}{\langle\Delta\rangle \cdot v}}\right)
```

where ⟨Δ⟩ is the expected age reduction per pulse.

### 2.6 Mouse Experiment 1: OSK vs. OSK + KDM4D vs. OSK + dCas9-KDM4D in Aged Fibroblasts

**Design:** 24-month-old C57BL/6J male mice (*n* = 10 per group, 5 groups: PBS vehicle, OSK-mRNA LNP, OSK + KDM4D-mRNA LNP, OSK + dCas9-KDM4D-mRNA LNP with 30-sgRNA panel targeting age-acquired H3K9me3 peaks, dCas9-KDM4D alone without OSK). Intradermal injection into dorsal skin of ionizable lipid nanoparticles encapsulating *N*1-methylpseudouridine-modified mRNA encoding the designated factors under a Col1a1 promoter element. The sgRNA panel is designed from published H3K9me3 ChIP-seq comparisons between young (3-month) and aged (24-month) C57BL/6J dermal fibroblasts, targeting the 30 most recurrent age-acquired euchromatic H3K9me3 peaks. Three treatment cycles of 48 hours expression followed by 5 days withdrawal.

**Primary endpoints:** (i) bulk RRBS for epigenetic age assessment using the established murine multi-tissue clock; (ii) single-cell DNA methylation (scBS-seq) for per-cell age distribution; (iii) H3K9me3 CUT&Tag at days 7 and 28 post-final injection to map barrier domain changes, with separate quantification at age-acquired euchromatic loci versus constitutive pericentromeric regions.

**Secondary endpoints:** dermal thickness (histomorphometry), Col1a1/Col3a1 expression (RT-qPCR), wound-healing assay (4 mm punch biopsy closure rate), LINE1 element expression (RT-qPCR for L1ORF1p and L1ORF2p) as a safety readout for constitutive heterochromatin destabilization.

**Expected outcome:** (i) OSK + KDM4D and OSK + dCas9-KDM4D both achieve significantly greater epigenetic age reduction than OSK alone; (ii) dCas9-KDM4D shows superior selectivity — equivalent ectopic H3K9me3 removal with preserved pericentromeric H3K9me3 and no LINE1 reactivation; (iii) untargeted KDM4D may show partial pericentromeric H3K9me3 loss, validating the need for the precision-targeted approach; (iv) dCas9-KDM4D alone (without OSK) produces minimal rejuvenation, confirming that H3K9me3 removal is a *permissive* rather than *instructive* signal and that OSK pioneer factor activity remains essential.

---

## 3. Obstacle 2: Cell Identity Preservation During Deep Rejuvenation

**Difficulty: Very High | Priority: Critical**

### 3.1 The Identity-Rejuvenation Tradeoff

The central tension in rejuvenation biology is that deeper epigenetic remodeling carries greater risk of cell identity disruption. Single-cell transcriptomic analysis during partial reprogramming across multiple murine cell types demonstrated that all partial reprogramming strategies consistently restore youthful gene expression but transiently suppress cell identity programs, with the degree and duration of suppression varying by factor combination and exposure time (Roux et al., 2022). In the MPTR protocol that achieved approximately 30-year rejuvenation in human fibroblasts, cells temporarily lost then reacquired their fibroblast identity, likely through epigenetic memory encoded at cell-type-specific enhancers (Gill et al., 2022).

Super-enhancers — dense clusters of enhancer elements bound by master transcription factors and the Mediator complex — underlie cell identity maintenance in adult tissues (Adam et al., 2015). These structures are acutely sensitive to perturbation by pioneer factors during reprogramming, with over 80% of chromatin accessibility changes occurring in a narrow two-to-five-day window coinciding with activation of endogenous target lineage transcription factors (Wapinski et al., 2017). This temporal vulnerability defines a critical "window of identity risk" during each reprogramming pulse.

For the 60→20 target, the challenge is acute: achieving 10 additional years of rejuvenation beyond the current 30-year ceiling likely requires accessing chromatin domains more closely intertwined with identity-defining regulatory elements. The question is whether identity and age information can be selectively separated at these loci.

### 3.2 Selective Targeting of Age-Associated Versus Identity-Associated Marks

A key biological insight is that age-acquired H3K9me3 domains are largely *distinct* from the H3K9me3 domains that maintain cell identity. Constitutive heterochromatin (pericentromeric, telomeric, and transposable element-associated H3K9me3) is established during development and serves structural/silencing functions rather than identity specification (Chandra et al., 2015). The ectopic H3K9me3 that accumulates with age at gene-rich euchromatic regions (Li et al., 2021) overlaps with, but is not identical to, cell-type-specific super-enhancer-associated chromatin. The KDM4D co-delivery strategy exploits this distinction: KDM4D preferentially removes H3K9me3 from euchromatic contexts (where the mark is ectopic and aberrant) with lower efficiency at the highly compacted pericentromeric heterochromatin that anchors chromosome structure (Matoba et al., 2017).

### 3.3 Mathematical Framework: Control Barrier Functions for Identity Safety

We formalize the identity preservation constraint using control barrier functions (CBFs) from safety-critical control theory, a framework not previously applied in the reprogramming context.

Define the cell state vector **x** = (*A*, *I*, *T*) where *A* is epigenetic age, *I* is a composite cell identity score (the fraction of lineage-defining super-enhancers retaining active chromatin marks), and *T* is a teratoma risk metric (expression level of pluripotency markers NANOG, LIN28A). The system evolves under the dosing control input *u*(*t*) (factor expression level):

```math
\dot{\mathbf{x}} = f(\mathbf{x}) + g(\mathbf{x}) \cdot u(t)
```

where *f*(**x**) represents autonomous dynamics (natural aging, identity maintenance) and *g*(**x**) represents the effect of reprogramming factors on the state.

The safe operating region is defined by the barrier function:

```math
h(\mathbf{x}) = I - I_{\min} \geq 0
```

where *I*_min is the minimum acceptable identity score (e.g., *I*_min = 0.8, requiring that at least 80% of fibroblast super-enhancers retain active marks). A valid control barrier function requires:

```math
\sup_{u \in \mathcal{U}} \left[ \frac{\partial h}{\partial \mathbf{x}} \left( f(\mathbf{x}) + g(\mathbf{x}) u \right) \right] \geq -\alpha(h(\mathbf{x}))
```

where *α* is an extended class-𝒦 function (a strictly increasing function with *α*(0) = 0 that determines how aggressively the controller is allowed to approach the safety boundary), and *𝒰* is the set of admissible control inputs (factor dose levels).

The constraint imposes an upper bound on the dosing input:

```math
u(t) \leq \frac{\alpha(I(t) - I_{\min}) - \frac{\partial I}{\partial t}\bigg|_{\text{autonomous}}}{\left|\frac{\partial I}{\partial u}\right|}
```

**Interpretation:** As the identity score *I*(*t*) approaches the minimum threshold *I*_min, the permissible dose *u*(*t*) is progressively constrained. This provides a mathematically rigorous framework for adaptive dosing: higher doses are permissible when identity is securely maintained (early in the protocol), while the controller automatically reduces dosing as identity signals weaken. The function *α*(*h*) encodes the desired safety margin — a linear *α*(*h*) = *γh* provides a constant safety decay rate with tuning parameter *γ* > 0 that sets the tradeoff between rejuvenation speed and identity preservation margin.

### 3.4 Mouse Experiment 2: Lineage Tracing During Deep Reprogramming

**Design:** Col1a1-CreERT2 × Rosa26-loxP-STOP-loxP-tdTomato double-transgenic mice, aged to 24 months (*n* = 8 per group). Tamoxifen-induced Cre activation permanently labels fibroblasts with tdTomato prior to treatment. Three groups: vehicle, OSK-mRNA LNP, OSK + KDM4D-mRNA LNP. Harvest skin biopsies at days 3, 7, 14, and 28 post-treatment. **Readout:** (i) tdTomato retention confirms fibroblast identity maintenance; (ii) scRNA-seq of tdTomato⁺ cells for expression of identity markers (Col1a1, Vim, Fsp1/S100A4, Ddr2) and pluripotency markers (Nanog, Lin28a, Zfp42); (iii) scATAC-seq for super-enhancer accessibility at fibroblast master regulators versus pluripotency loci. **Expected outcome:** OSK + KDM4D achieves greater rejuvenation depth than OSK alone while maintaining fibroblast identity (tdTomato retention, preserved identity marker expression), confirming that the additional H3K9me3 removal targets age-associated rather than identity-associated domains.

---

## 4. Obstacle 3: Heterogeneous Single-Cell Response to Reprogramming

**Difficulty: High | Priority: High**

### 4.1 The Stochastic Nature of Reprogramming

Reprogramming is inherently stochastic: genetically identical cells exposed to identical factor levels exhibit widely divergent outcomes (Roux et al., 2022). In the MPTR protocol that achieved an average approximately 30-year reversal, the variance across individual cells has not been reported, as bulk assays were used (Gill et al., 2022). Multi-omics characterization of aged fibroblast cultures revealed that aging increases inter-individual and intra-individual variability in both iPSC reprogramming efficiency and wound healing capacity, with an "activated" inflammatory subpopulation secreting TNF identified as a key determinant of poor reprogramming response (Mahmoudi et al., 2019). This raises a critical question: does the 30-year ceiling reflect a uniform biological limit across all cells, or does it represent the mean of a broad distribution in which some cells achieve much deeper rejuvenation while others barely respond?

If the latter, then the population average *underestimates* the maximum achievable rejuvenation, and the true barrier may be one of *heterogeneity management* rather than absolute depth. A systematic analysis of conserved biological processes across multiple partial reprogramming protocols revealed that dynamic chromatin remodeling, inflammation resolution, autophagy induction, and mitochondrial activity enhancement are consistently activated, but with substantial cell-to-cell variability in the magnitude and timing of these responses (Avelar et al., 2025). Evidence from iPSC reprogramming supports this interpretation: clonal analysis revealed extreme variability in reprogramming kinetics, with "elite" cells achieving pluripotency rapidly while the majority follow slow, stochastic trajectories (Roux et al., 2022). The ICE mouse model showed up to 57% reversal of epigenetic age in fibroblasts — substantially beyond the Gill et al. ceiling — suggesting that under conditions of extreme epigenetic erosion, deeper reversal is achievable (Yang et al., 2023).

### 4.2 Mathematical Framework: *k*-out-of-*n* System Reliability for Multi-Locus Rejuvenation

We model the cell as a system of *n* age-associated H3K9me3 loci, each of which must be individually remodeled by the OSK + KDM4D combination. A cell is scored as "successfully rejuvenated" if at least *k* of *n* critical loci have been demethylated and reactivated. This is a *k*-out-of-*n*:G (good) system in reliability theory.

Let *p*_i be the probability that locus *i* is successfully remodeled during a single treatment cycle. For independent loci with heterogeneous susceptibilities:

```math
R_{\text{cell}}(k, n) = \sum_{j=k}^{n} \sum_{S \subseteq \{1,\ldots,n\}, |S|=j} \prod_{i \in S} p_i \prod_{i \notin S} (1 - p_i)
```

where *R*_cell is the probability that a single cell achieves the rejuvenation threshold, *k* is the minimum number of loci that must be remodeled for the cell to score below the target biological age, *n* is the total number of age-associated H3K9me3 loci, and *p*_i is the per-locus remodeling probability for locus *i*.

Under the simplifying assumption of equal per-locus probability *p*, the system reliability is given by the regularized incomplete beta function:

```math
R_{\text{cell}}(k, n, p) = \sum_{j=k}^{n} \binom{n}{j} p^j (1-p)^{n-j} = I_p(k, n - k + 1)
```

where *I*_p is the regularized incomplete beta function.

The population-level fraction of cells achieving deep rejuvenation (≥40 years) depends on the per-locus probability *p*, which is itself a function of factor concentrations and H3K9me3 barrier height:

```math
p(\mathbf{c}) = 1 - \exp\left(-\frac{[\text{OSK}] \cdot \eta_{\text{OSK}} + [\text{KDM4D}] \cdot \eta_{\text{KDM4}}}{E_{\text{barrier}}}\right)
```

where *η*_OSK and *η*_KDM4 are the per-molecule remodeling efficiencies of OSK and KDM4D respectively, and *E*_barrier is the effective barrier energy of the H3K9me3 domain at that locus.

**Key prediction:** For *n* = 50 critical age-associated loci, achieving *k* = 40 (80% remodeling for deep rejuvenation), the required per-locus probability is *p* ≥ 0.88 under the binomial model. With OSK alone (estimated *p*_OSK ≈ 0.70 at accessible loci but *p*_OSK < 0.30 at H3K9me3-locked loci), *R*_cell is negligibly small. With OSK + KDM4D raising *p* at locked loci to ≈ 0.85, *R*_cell increases to approximately 0.15 per cell — making deep rejuvenation a detectable minority outcome rather than a vanishingly rare event.

### 4.3 Mouse Experiment 3: Single-Cell Multi-Omics Time Course

**Design:** 24-month C57BL/6J mice (*n* = 6), treated with OSK + KDM4D-mRNA LNP (intradermal, Col1a1 promoter). Skin biopsies at days 0, 3, 7, 14, and 28. Each biopsy processed for joint single-cell bisulfite sequencing and single-cell ATAC-seq (scNMT-seq protocol) on sorted fibroblasts (PDGFRα⁺ cells). **Readout:** (i) Per-cell DNA methylation age at each timepoint using single-cell epigenetic clocks; (ii) chromatin accessibility landscape dynamics; (iii) identification of pre-treatment chromatin features that predict deep versus shallow rejuvenation response. **Expected outcome:** A broad distribution of single-cell rejuvenation depths, with a tail extending beyond the population mean. Pre-treatment chromatin accessibility at H3K9me3 boundary regions predicts which cells achieve deep rejuvenation, validating the *k*-out-of-*n* model.

---

## 5. Obstacle 4: Dosing Precision and Temporal Control

**Difficulty: High | Priority: High**

### 5.1 The Narrow Therapeutic Window

The therapeutic window for partial reprogramming is bounded on one side by insufficient rejuvenation and on the other by dedifferentiation, teratoma formation, and organ toxicity. Continuous OSKM induction in vivo causes lethal hepatic and intestinal dysfunction within one week (Parras et al., 2023), while the 2-day-on/5-day-off pulsatile protocol extends lifespan without detectable adverse effects over months of treatment (Browder et al., 2022). Cell-type-specific targeting using the Cdkn2a (p16) promoter to restrict OSK expression to senescent and aged cells achieved a 40% lifespan extension in progeroid mice and 12% in wild-type aged mice with no increased tumor incidence — the largest lifespan extension by partial reprogramming in wild-type mice reported to date (Sahu et al., 2024).

The addition of KDM4D to the reprogramming cocktail introduces a second dosing dimension, as the H3K9me3 demethylase has oncogenic potential in certain contexts (Berry & Janknecht, 2013). Transient mRNA delivery provides an inherent safety mechanism: mRNA has a half-life of hours to days in cells, ensuring that expression is self-limiting even without external control systems.

### 5.2 Mathematical Framework: Partially Observed Markov Decision Process for Optimal Dosing

The fundamental challenge in dosing optimization is that the cell's true epigenetic state cannot be directly observed during treatment — only noisy biomarkers (gene expression surrogates, secreted protein levels) are accessible. This partial observability distinguishes the problem from the fully observed Markov decision processes (MDPs) previously applied to anti-CRISPR timing (draft_32), and motivates the use of a POMDP framework.

Define the hidden state *s*(*t*) = (*A*(*t*), *I*(*t*)) ∈ 𝒮 (true epigenetic age and identity score), the action *a*(*t*) ∈ 𝒜 = {dose₁, dose₂, ..., dose_L} (discrete mRNA dose levels), and the observation *o*(*t*) ∈ 𝒪 (noisy biomarker readouts). The transition model is:

```math
P(s_{t+1} | s_t, a_t) = \mathcal{T}(s_t, a_t, s_{t+1})
```

and the observation model is:

```math
P(o_t | s_t) = \mathcal{O}(s_t, o_t)
```

The agent maintains a belief state — a posterior probability distribution over hidden states given the history of observations and actions:

```math
b_{t+1}(s') = \frac{\mathcal{O}(s', o_{t+1}) \sum_{s \in \mathcal{S}} \mathcal{T}(s, a_t, s') \, b_t(s)}{\sum_{s' \in \mathcal{S}} \mathcal{O}(s', o_{t+1}) \sum_{s \in \mathcal{S}} \mathcal{T}(s, a_t, s') \, b_t(s)}
```

where *b*_t(*s*) is the probability assigned to hidden state *s* at time *t*, 𝒯 is the state transition kernel (encoding how the cell state evolves under a given dose), and 𝒪 is the observation kernel (encoding how biomarkers relate to the true cell state).

The optimal dosing policy *π**: 𝒝 → 𝒜 maps belief states to actions, maximizing the expected cumulative reward:

```math
\pi^* = \arg\max_\pi \mathbb{E}\left[\sum_{t=0}^{T} \gamma^t R(s_t, a_t)\right]
```

where the reward function penalizes high age, identity loss, and excessive dosing:

```math
R(s, a) = -w_A \cdot A - w_I \cdot \max(0, I_{\min} - I) - w_D \cdot \|a\|
```

where *w*_A, *w*_I, *w*_D are weights encoding the relative importance of age reduction, identity preservation, and dose minimization, *γ* ∈ (0, 1) is a discount factor, and *T* is the treatment horizon.

**Clinical interpretation:** In practice, the POMDP framework prescribes that dosing should be *conservative when uncertain* (high belief entropy) and *aggressive when confident* (low belief entropy, high observed age). Biomarker measurements (e.g., serum procollagen I N-terminal propeptide for fibroblast activity, or cell-free DNA methylation for non-invasive age tracking) would update the belief state and guide adaptive dose adjustments.

### 5.3 Mouse Experiment 4: Dose-Response Characterization

**Design:** 24-month C57BL/6J mice (*n* = 8 per group, 5 dose groups + vehicle). Intradermal OSK + KDM4D-mRNA LNP at doses of 0.1, 0.3, 1.0, 3.0, and 10.0 μg total mRNA (OSK:KDM4D molar ratio 3:1). Single treatment cycle (48 hours expression). Harvest skin at day 14. **Readout:** (i) Bulk RRBS epigenetic age; (ii) scRNA-seq for identity markers; (iii) H3K9me3 CUT&Tag; (iv) p53 and Ki67 immunohistochemistry for safety. **Expected outcome:** Sigmoidal dose-response for rejuvenation depth (Hill function), with a plateauing or declining identity score at high doses. The therapeutic index (ratio of dose at 50% identity loss to dose at 50% maximal rejuvenation) characterizes the safety margin. We predict a therapeutic index >5 due to the selectivity of mRNA-encoded KDM4D for ectopic versus constitutive H3K9me3 domains.

---

## 6. Obstacle 5: In Vivo Delivery to Dermal Fibroblasts

**Difficulty: Medium-High | Priority: High**

### 6.1 Lipid Nanoparticle-mRNA Delivery via Intradermal Injection

Lipid nanoparticle (LNP) encapsulation of *N*1-methylpseudouridine-modified mRNA has emerged as a clinically validated delivery platform, with demonstrated safety and efficacy in mRNA vaccines and expanding therapeutic applications (Paine et al., 2024). For dermal fibroblast targeting, intradermal injection provides direct access to the target cell population, bypassing the hepatic first-pass effect that dominates intravenous LNP biodistribution.

However, intradermal injection delivers LNPs to a heterogeneous cellular environment containing keratinocytes, Langerhans cells, dermal dendritic cells, macrophages, and endothelial cells in addition to the target fibroblasts. To achieve fibroblast selectivity, we propose encoding the reprogramming cargo under a fibroblast-specific promoter element. The Col1a1 promoter drives robust expression in fibroblasts with minimal activity in epidermal or immune cell populations, and has been extensively characterized in transgenic mouse models (Roux et al., 2022). An alternative promoter, S100A4/Fsp1, provides complementary specificity for activated fibroblasts.

### 6.2 Systemic Delivery Alternatives

For broader translational applications, AAV-mediated delivery of inducible OSK has been validated by two independent groups. Systemic AAV encoding inducible OSK extended median remaining lifespan by 109% in 124-week-old mice (Macip et al., 2024). Cell-type-specific targeting using the Cdkn2a promoter achieved the most selective in vivo partial reprogramming delivery reported to date, restricting expression to senescent and aged cells (Sahu et al., 2024). However, mRNA-LNP delivery offers advantages for the proposed combinatorial OSK + KDM4D approach: (i) self-limiting expression kinetics eliminate the risk of persistent oncogene expression; (ii) co-encapsulation of multiple mRNA species in a single LNP simplifies delivery; and (iii) repeated dosing is feasible without anti-vector immunity, unlike AAV.

### 6.3 Mouse Experiment 5: Fibroblast-Targeted Biodistribution

**Design:** 24-month C57BL/6J mice (*n* = 6). Intradermal injection of LNP-mRNA encoding GFP under the Col1a1 promoter (1 μg). Harvest skin biopsies at 24 and 72 hours. **Readout:** (i) Flow cytometry: GFP expression in sorted cell populations (PDGFRα⁺ fibroblasts, CD45⁺ immune cells, EpCAM⁺ keratinocytes, CD31⁺ endothelial cells); (ii) immunofluorescence microscopy for spatial distribution; (iii) RT-qPCR for GFP mRNA in sorted populations. **Expected outcome:** >80% of GFP⁺ cells are PDGFRα⁺ fibroblasts at 24 hours, with minimal expression in immune or epidermal compartments, validating the Col1a1 promoter strategy for fibroblast-selective reprogramming.

---

## 7. Obstacle 6: Measuring Single-Cell Rejuvenation and Predicting Durability

**Difficulty: Medium-High | Priority: High**

### 7.1 The Resolution Gap

The DNA methylation clocks that define the field — the pan-tissue clock (Horvath, 2013), GrimAge (Lu et al., 2022), and DunedinPACE (Belsky et al., 2022) — were developed for bulk tissue or blood samples containing thousands to millions of cells. Their application to partial reprogramming has relied on bulk RRBS or array-based methylation profiling, yielding population-averaged age estimates. This averaging obscures the single-cell distribution of rejuvenation depths that is critical for understanding the heterogeneity described in Section 4.

Recent advances in single-cell methylation profiling (scBS-seq, scNMT-seq) have enabled the development of single-cell epigenetic clocks. The scEpiAge framework achieved a mean absolute error of 20 weeks in mouse blood, improving upon the original scAge model (MAE 25.98 weeks) and revealing substantial heterogeneity in epigenetic aging across B cells, CD4⁺ T cells, and CD8⁺ T cells within the same animal (Bonder et al., 2024). The estiMAge algorithm provides an alternative single-cell methylation age estimator optimized for sparse bisulfite sequencing data, enabling epigenetic age profiling from as few as 5% CpG coverage per cell (Olova et al., 2025). Cell-type-specific epigenetic clocks have been developed for neurons and hepatocytes, with neuron-specific clocks revealing biological age acceleration in Alzheimer's disease (Moqri et al., 2024). These tools collectively enable the single-cell resolution measurements required to characterize the heterogeneous rejuvenation response described in Section 4.

For in vivo monitoring of rejuvenation without tissue biopsy, non-invasive biomarkers would be transformative. Cell-free DNA methylation analysis from blood or interstitial fluid could potentially track epigenetic age of accessible tissues, while secreted protein biomarkers (e.g., procollagen I N-terminal propeptide for fibroblast synthetic activity) provide functional correlates.

### 7.2 Functional Versus Molecular Age

Epigenetic age reversal is only meaningful if accompanied by functional rejuvenation. In fibroblasts, age-associated functional decline includes reduced collagen production, impaired migration and wound healing capacity, and altered extracellular matrix composition. The MPTR protocol restored collagen production and wound healing in rejuvenated human fibroblasts (Gill et al., 2022), providing evidence that epigenetic and functional age are mechanistically linked. Multi-omics characterization of partial chemical reprogramming confirmed that molecular rejuvenation is accompanied by upregulated mitochondrial oxidative phosphorylation and reduced accumulation of aging-related metabolites (Mitchell et al., 2024).

### 7.3 Mathematical Framework: Gamma Process Degradation Model for Re-Aging Dynamics

A critical open question is whether rejuvenation is durable or whether cells rapidly re-age to their pre-treatment state. We model the re-aging process using the Gamma degradation process from reliability engineering, which has not been previously applied to epigenetic aging dynamics.

After rejuvenation to a biological age *A*_rejuv at time *t* = 0, the cell undergoes re-aging according to a Gamma process {*G*(*t*); *t* ≥ 0} with shape rate *α* > 0 and scale parameter *β* > 0:

```math
A(t) = A_{\text{rejuv}} + G(t), \quad G(t) \sim \text{Gamma}(\alpha t, \beta)
```

The Gamma process has the key properties of (i) monotonically non-decreasing sample paths (aging is irreversible between treatment cycles), (ii) independent increments (future aging rate is independent of past trajectory), and (iii) stationary increments (the rate of aging does not accelerate or decelerate over short timescales).

The expected re-aging trajectory is linear:

```math
\mathbb{E}[A(t)] = A_{\text{rejuv}} + \alpha \beta t
```

where *αβ* is the mean re-aging rate (biological years per chronological year), and the variance grows linearly:

```math
\text{Var}[A(t)] = \alpha \beta^2 t
```

The probability that a rejuvenated cell remains below a target age *A*_target at time *t* is:

```math
P(A(t) \leq A_{\text{target}}) = F_{\text{Gamma}}\left(\frac{A_{\text{target}} - A_{\text{rejuv}}}{\beta}; \alpha t\right)
```

where *F*_Gamma is the Gamma cumulative distribution function.

**Key prediction:** If the re-aging rate *αβ* equals the natural aging rate (approximately 1.0 biological year per chronological year), a cell rejuvenated by 40 years would require 40 chronological years to return to its pre-treatment age. If *αβ* is accelerated (as might occur if rejuvenation creates an unstable chromatin state), the cell could re-age faster, and the *durability half-life* — the time for the cell to lose half its rejuvenation benefit — becomes a critical parameter:

```math
t_{1/2} = \frac{\Delta A_{\text{rejuv}}}{2 \alpha \beta}
```

where *ΔA*_rejuv = *A*_pre − *A*_rejuv is the achieved rejuvenation depth. A durability half-life exceeding 10 years (for a 40-year rejuvenation, corresponding to *αβ* ≤ 2.0) would be clinically meaningful, as periodic retreatment could maintain the rejuvenated state.

### 7.4 Mouse Experiment 6: Longitudinal Rejuvenation Durability

**Design:** 24-month C57BL/6J mice (*n* = 20), treated with the optimal OSK + KDM4D dose from Experiment 4. Skin biopsies at weeks 1, 4, 12, and 24 post-treatment (*n* = 5 mice per timepoint, terminal harvest). Age-matched untreated controls at each timepoint. **Readout:** (i) Bulk RRBS epigenetic age at each timepoint; (ii) scBS-seq on a subset for single-cell age distributions; (iii) wound healing assay; (iv) dermal thickness and collagen content. **Expected outcome:** Maximum rejuvenation at week 1-4, with gradual re-aging following Gamma process kinetics. Estimation of *αβ* (re-aging rate) and comparison with the natural aging rate will determine whether rejuvenation creates a stable or unstable chromatin state.

---

## 8. Obstacle 7: Safety — Oncogenic Risk of Combined Factor Expression

**Difficulty: Medium | Priority: Critical**

### 8.1 Residual Transformation Risk

The exclusion of c-Myc from the OSK cocktail substantially reduces but does not eliminate oncogenic risk. While long-term cyclic OSK expression in aged wild-type mice produced no detectable tumors over 7-10 months (Browder et al., 2022), and Cdkn2a-targeted AAV-OSK showed no increased tumor incidence over the treatment period (Sahu et al., 2024), these studies employed lower reprogramming depths than the proposed OSK + KDM4D protocol.

The addition of KDM4D introduces a specific concern: KDM4 family members are amplified or overexpressed in multiple cancer types (Berry & Janknecht, 2013). Critically, KDM4A overexpression causes site-specific DNA copy number gains at 1q12, 1q21, and Xq13.1 through DNA rereplication within a single S phase, without global chromosomal instability (Black et al., 2013). These gains are regenerated each cell division during sustained KDM4 overexpression but do not persist after KDM4 withdrawal — a finding that provides strong mechanistic support for transient mRNA delivery. Several features of the proposed protocol mitigate this risk. First, mRNA delivery ensures transient expression with a half-life of approximately 6-12 hours for modified mRNA, eliminating persistent oncogene activity and preventing the repeated-cycle copy gains observed with sustained KDM4 expression. Second, the Col1a1 promoter restricts expression to fibroblasts, excluding epithelial and hematopoietic compartments where most KDM4-associated cancers arise. Third, the pulsatile protocol (2 days on, 5 days off) limits cumulative exposure.

Continuous OSKM expression — in contrast to the pulsatile protocol — causes lethal hepatic and intestinal failure within one week, identifying these organs as critical toxicity barriers for systemic approaches (Parras et al., 2023). The intradermal delivery route with fibroblast-specific promoter employed here entirely avoids these organs.

### 8.2 Chemical Reprogramming as a Potentially Safer Alternative

Small-molecule cocktails can achieve partial rejuvenation without exogenous transcription factors, potentially reducing oncogenic risk. Multi-omics characterization of partial chemical reprogramming in mouse fibroblasts demonstrated biological age reduction by both transcriptomic and epigenetic clocks, with upregulated mitochondrial oxidative phosphorylation (Mitchell et al., 2024). A seven-compound cocktail reversed multiple aging hallmarks in human dermal fibroblasts and extended median lifespan by over 42% in *C. elegans* (Schoenfeldt et al., 2025). A reduced two-compound cocktail retained rejuvenating effects (Schoenfeldt et al., 2025), suggesting that the minimum effective chemical intervention may be simpler than the four-factor genetic approach. However, chemical approaches have not yet achieved the depth of rejuvenation (approximately 30 years) demonstrated by transcription factor-based MPTR (Gill et al., 2022), and their compatibility with KDM4-mediated barrier removal remains unexplored.

### 8.3 Mouse Experiment 7: Long-Term Safety Follow-Up

**Design:** 24-month C57BL/6J mice (*n* = 30), treated with 3 cycles of OSK + KDM4D-mRNA LNP at the optimal dose. Age-matched untreated controls (*n* = 15). Terminal harvest at 3, 6, and 12 months post-treatment (*n* = 10 treated + 5 controls per timepoint). **Readout:** (i) Complete histopathological evaluation of treated skin and draining lymph nodes; (ii) p53 and Ki67 immunohistochemistry at injection sites; (iii) whole-exome sequencing of treated skin versus contralateral untreated skin for somatic mutation accumulation; (iv) body weight, frailty index, and overall survival monitoring. **Expected outcome:** No increased tumor incidence, somatic mutation burden, or adverse histopathological findings in treated versus untreated skin, confirming the safety of transient mRNA-mediated OSK + KDM4D delivery.

---

## 9. Integrated Experimental Protocol and Statistical Design

### 9.1 Unified Timeline

The seven experiments are designed to be executed in a phased sequence:

| Phase | Experiments | Duration | Purpose |
|-------|-----------|----------|---------|
| Phase I (Proof of concept) | 1, 5 | 8 weeks | Demonstrate OSK + KDM4D superiority and fibroblast targeting |
| Phase II (Mechanism) | 2, 3, 4 | 12 weeks | Identity preservation, single-cell heterogeneity, dose-response |
| Phase III (Durability & safety) | 6, 7 | 52 weeks | Longitudinal re-aging kinetics and long-term safety |

### 9.2 Sample Size Justification

For Experiment 1 (primary efficacy), with 4 groups of 12 mice each: assuming the OSK-alone group achieves 15 biological-year reversal in the murine clock (equivalent to approximately 30 human years, scaled by the 2:1 mouse-to-human aging ratio) with standard deviation 5 years, detecting an additional 8-year reversal from KDM4D co-delivery with 80% power at α = 0.05 (two-sided *t*-test) requires *n* = 9 per group. We specify *n* = 12 to account for technical failures and permit exploratory subgroup analyses.

### 9.3 Go/No-Go Decision Criteria

**Phase I → Phase II:** Proceed if OSK + KDM4D achieves statistically significant (*P* < 0.05) greater epigenetic age reduction than OSK alone, AND fibroblast targeting specificity exceeds 70% by flow cytometry.

**Phase II → Phase III:** Proceed if (i) lineage tracing confirms fibroblast identity retention (>80% tdTomato⁺ cells expressing Col1a1) at the optimal dose; (ii) the therapeutic index exceeds 3 in dose-response characterization; and (iii) single-cell analysis reveals a subpopulation (>5% of treated cells) achieving rejuvenation exceeding the OSK-alone population mean by >1.5 standard deviations.

### 9.4 Statistical Analysis Plan

Primary analyses use mixed-effects models with mouse as random effect and treatment group, timepoint, and their interaction as fixed effects. Multiple comparison correction by Tukey-Kramer. Single-cell data analyzed by Wilcoxon rank-sum tests for between-group comparisons and Kolmogorov-Smirnov tests for distributional differences. Model parameters (stochastic resetting rate, Gamma re-aging rate, *k*-out-of-*n* threshold) estimated by maximum likelihood with bootstrapped confidence intervals.

---

## 10. Open Questions and Future Directions

### 10.1 Generalization Beyond Fibroblasts

Dermal fibroblasts are an experimentally tractable starting point, but the ultimate clinical target for rejuvenation includes post-mitotic cells — particularly neurons and cardiomyocytes — where aging has the most devastating and irreversible consequences. Recent evidence that OSK-mediated partial reprogramming of engram neurons reverses senescence-related cellular hallmarks and recovers learning and memory capacities to levels of healthy young animals in both aged and Alzheimer's disease mice (Berdugo-Vega et al., 2025) demonstrates that neuronal rejuvenation is achievable. The H3K9me3 barrier may be more formidable in neurons than fibroblasts: single-nucleus ATAC-seq revealed that aged excitatory neurons exhibit particularly pronounced heterochromatin changes (Zhang et al., 2022), while cardiomyocytes maintain exceptionally stable H3K9me3 at lineage-inappropriate loci. Whether KDM4D co-delivery can extend the rejuvenation ceiling in post-mitotic cells requires investigation with appropriate delivery vectors (AAV-PHP.eB for neurons, cardiotropic AAV9 for cardiomyocytes).

### 10.2 Multi-Round Treatment for Additive Rejuvenation

The stochastic resetting model predicts that multiple treatment cycles should additively deepen rejuvenation, with each cycle accessing a fraction of the residual H3K9me3-locked loci. Chondronasiou et al. demonstrated that even a single cycle produces multi-tissue rejuvenation (Chondronasiou et al., 2022); whether multiple cycles with OSK + KDM4D can exceed the single-cycle ceiling additively remains an open question of substantial clinical importance.

### 10.3 Chemical Bypassing of Chromatin Barriers

The recent demonstration that chemical cocktails can reverse aging hallmarks and extend lifespan (Schoenfeldt et al., 2025; Mitchell et al., 2024) raises the question of whether small molecules can bypass the H3K9me3 barrier through mechanisms distinct from pioneer factor engagement. Histone methyltransferase inhibitors (e.g., chaetocin, a SUV39H1 inhibitor) could serve as chemical surrogates for KDM4D, potentially simplifying the therapeutic protocol.

### 10.4 The Mesenchymal Drift Connection

A recent analysis of 40+ human tissues revealed a pervasive "mesenchymal drift" — an age- and disease-associated upregulation of mesenchymal genes across cell types that correlates with disease progression and elevated mortality (Lu et al., 2025). Partial reprogramming markedly reduces this drift before full dedifferentiation occurs, providing a mechanistic framework for why rejuvenation benefits extend beyond the directly targeted cells. Whether mesenchymal drift is itself driven by H3K9me3 redistribution at mesenchymal gene loci represents an intriguing connection between our chromatin barrier hypothesis and the systemic biology of aging.

### 10.5 Cross-Species Conservation of Age-Acquired H3K9me3 Peaks

A critical limitation of the dCas9-KDM4D approach is that the sgRNA panel must be designed from species-specific ChIP-seq data. The mouse experiments proposed here validate the *principle* that targeted H3K9me3 removal extends rejuvenation depth, but the specific age-acquired loci may differ between mouse and human fibroblasts due to divergent genome organization, transposable element landscape, and species-specific aging trajectories. While the global trend of H3K9me3 redistribution with age appears conserved across metazoans — documented in *C. elegans* (Li et al., 2021), mouse (Zhang et al., 2022), and human (de Lima Camillo et al., 2025) — the identity of the specific loci acquiring *de novo* H3K9me3 may be species-specific. A necessary translational step is a comparative H3K9me3 CUT&Tag analysis of aged mouse (24-month) versus aged human (60+ year) dermal fibroblasts to map the degree of conservation at age-acquired euchromatic peaks. If conservation is high (>50% of peaks mapping to syntenic regions), the mouse sgRNA panel can be directly adapted; if conservation is low, species-specific sgRNA design will be required but the mechanistic principle remains valid.

### 10.6 Toward Quantitative Aging Reversal Targets

The 60→20 target used in this paper is illustrative, but the clinical definition of "sufficient rejuvenation" remains undefined. GrimAge acceleration of 1 year is associated with a hazard ratio of 1.10 for all-cause mortality (Lu et al., 2022), and DunedinPACE captures the dynamic velocity of aging rather than cumulative age (Belsky et al., 2022). Whether epigenetic age reversal by 40 years translates proportionally to mortality reduction is an empirical question that can only be answered by long-term survival studies in rejuvenated model organisms. The 12-month safety follow-up in Experiment 7 will provide the first data point, but definitive answers will require lifespan studies.

---

## References

1. Adam, R. C., Yang, H., Ge, Y., et al. (2015). Pioneer factors govern super-enhancer dynamics in stem cell plasticity and lineage choice. *Nature*, 521(7552), 366-370. PMID: 25799994

2. Avelar, R. A., Duffy, B., Moreno-Valenzuela, J., et al. (2025). Conserved biological processes in partial cellular reprogramming: relevance to aging and rejuvenation. *Ageing Research Reviews*, 107, 102735. PMID: 40122394

3. Belsky, D. W., Caspi, A., Corcoran, D. L., et al. (2022). DunedinPACE, a DNA methylation biomarker of the pace of aging. *eLife*, 11, e73420. PMID: 35029144

4. Berdugo-Vega, G., Lee, C. C., Gao, J., et al. (2025). Cognitive rejuvenation through partial reprogramming of engram cells. *Neuron*, 113, 1-15. PMID: 41672073

5. Berry, W. L., & Janknecht, R. (2013). KDM4/JMJD2 histone demethylases: epigenetic regulators in cancer biology. *Cancer Research*, 73(10), 2936-2942. PMID: 23644527

6. Black, J. C., Manning, A. L., Van Rechem, C., et al. (2013). KDM4A lysine demethylase induces site-specific copy gain and rereplication of regions amplified in tumors. *Cell*, 154(3), 541-555. PMID: 23871696

7. Bonder, M. J., Clark, S. J., Krueger, F., et al. (2024). scEpiAge: an age predictor highlighting single-cell ageing heterogeneity in mouse blood. *Nature Communications*, 15(1), 7567. PMID: 39217176

8. Browder, K. C., Reddy, P., Yamamoto, M., et al. (2022). In vivo partial reprogramming alters age-associated molecular changes during physiological aging in mice. *Nature Aging*, 2, 243-253. PMID: 37118377

9. Chandra, T., Ewels, P. A., Schoenfelder, S., et al. (2015). Global reorganization of the nuclear landscape in senescent cells. *Cell Reports*, 10(4), 471-483. PMID: 25640177

10. Chen, J., Liu, H., Liu, J., et al. (2013). H3K9 methylation is a barrier during somatic cell reprogramming into iPSCs. *Nature Genetics*, 45(1), 34-42. PMID: 23202127

11. Chondronasiou, D., Gill, D., Mosteiro, L., et al. (2022). Multi-omic rejuvenation of naturally aged tissues by a single cycle of transient reprogramming. *Aging Cell*, 21(3), e13578. PMID: 35235716

11. de Lima Camillo, L. P., Asif, M. H., Horvath, S., et al. (2025). Histone mark age of human tissues and cell types. *Science Advances*, 11(1), eadk9373. PMID: 39742485

12. Djeghloul, D., Kuranda, K., Kuzniak, I., et al. (2016). Age-associated decrease of the histone methyltransferase SUV39H1 in HSC perturbs heterochromatin and B lymphoid differentiation. *Stem Cell Reports*, 6(6), 970-984. PMID: 27304919

13. Evans, M. R., Majumdar, S. N., & Schehr, G. (2020). Stochastic resetting and applications. *Journal of Physics A: Mathematical and Theoretical*, 53(19), 193001. DOI: 10.1088/1751-8121/ab7cfe

14. Gill, D., Parry, A., Santos, F., et al. (2022). Multi-omic rejuvenation of human cells by maturation phase transient reprogramming. *eLife*, 11, e71624. PMID: 35390271

15. Guan, J., Wang, G., Wang, J., et al. (2022). Chemical reprogramming of human somatic cells to pluripotent stem cells. *Nature*, 605, 325-331. PMID: 35418683

16. Horvath, S. (2013). DNA methylation age of human tissues and cell types. *Genome Biology*, 14(10), R115. PMID: 24138928

17. Hou, P., Li, Y., Zhang, X., et al. (2013). Pluripotent stem cells induced from mouse somatic cells by small-molecule compounds. *Science*, 341(6146), 651-654. PMID: 23868920

18. Li, C. L., Pu, M., Wang, W., et al. (2021). Region-specific H3K9me3 gain in aged somatic tissues in *Caenorhabditis elegans*. *PLOS Genetics*, 17(9), e1009432. PMID: 34506495

19. Liu, B., Wang, Z., Zhang, L., et al. (2013). Depleting the methyltransferase Suv39h1 improves DNA repair and extends lifespan in a progeria mouse model. *Nature Communications*, 4, 1868. PMID: 23695662

20. Lu, A. T., Quach, A., Wilson, J. G., et al. (2022). DNA methylation GrimAge version 2. *Aging (Albany NY)*, 14(23), 9484-9549. PMID: 36516495

21. Lu, J. Y., Tu, W. B., Li, R., et al. (2025). Prevalent mesenchymal drift in aging and disease is reversed by partial reprogramming. *Cell*, S0092-8674(25)00853-0. PMID: 40816266

22. Lu, Y., Brommer, B., Tian, X., et al. (2020). Reprogramming to recover youthful epigenetic information and restore vision. *Nature*, 588(7836), 124-129. PMID: 33268865

23. Macip, C. C., Hasan, R., Houghton, M. J., et al. (2024). Gene therapy-mediated partial reprogramming extends lifespan and reverses age-related changes in aged mice. *Cellular Reprogramming*, 26(1), 24-32. PMID: 38381405

24. Mahmoudi, S., Mancini, E., Xu, L., et al. (2019). Heterogeneity in old fibroblasts is linked to variability in reprogramming and wound healing. *Nature*, 574, 553-558. PMID: 31645721

25. Matoba, S., Liu, Y., Lu, F., et al. (2017). KDM4B-mediated reduction of H3K9me3 and H3K36me3 levels improves somatic cell reprogramming into pluripotency. *Scientific Reports*, 7, 7514. PMID: 28790329

26. Mitchell, W., Goeminne, L. J. E., Tyshkovskiy, A., et al. (2024). Multi-omics characterization of partial chemical reprogramming reveals evidence of cell rejuvenation. *eLife*, 13, RP90579. PMID: 38517750

27. Montavon, T., Shukeir, N., Erikson, G., et al. (2024). Loss of H3K9 trimethylation leads to premature aging. *Science Advances*, 10(30), eadj4102. PMID: 39091811

28. Moqri, M., Herzog, C., Poganik, J. R., et al. (2024). Cell-type specific epigenetic clocks to quantify biological age at cell-type resolution. *Aging Cell*, 23(12), e14368. PMID: 39760516

28. Ocampo, A., Reddy, P., Martinez-Redondo, P., et al. (2016). In vivo amelioration of age-associated hallmarks by partial reprogramming. *Cell*, 167(7), 1719-1733.e12. PMID: 27984723

29. Olova, N., Simpson, D. J., Marioni, R. E., et al. (2025). estiMAge: development of a DNA methylation clock to estimate the methylation age of single cells. *Bioinformatics Advances*, 5(1), vbaf005. PMID: 39867532

30. Paine, P. T., Nguyen, A., & Ocampo, A. (2024). Partial cellular reprogramming: A deep dive into an emerging rejuvenation technology. *Aging Cell*, 23(2), e14039. PMID: 38040663

31. Parras, A., Verthuy, C., Costa, L., et al. (2023). In vivo reprogramming leads to premature death linked to hepatic and intestinal failure. *Nature Aging*, 3, 1525-1534. PMID: 38012287

32. Roux, A. E., Zhang, C., Paw, J., et al. (2022). Diverse partial reprogramming strategies restore youthful gene expression and transiently suppress cell identity. *Cell Systems*, 13(7), 574-587.e11. PMID: 35690067

33. Sahu, S. K., Tiwari, N., Pataskar, A., et al. (2024). Targeted partial reprogramming of age-associated cell states improves markers of health in mouse models of aging. *Science Translational Medicine*, 16(764), eadg1777. PMID: 39259812

34. Sankar, A., Lerdrup, M., Engard, O., et al. (2020). KDM4A regulates the maternal-to-zygotic transition by protecting broad H3K4me3 domains from H3K9me3 invasion in oocytes. *Nature Cell Biology*, 22(5), 669-681. PMID: 32231309

35. Schoenfeldt, L., Paine, P. T., Lemoine, M. A., et al. (2025). Chemical reprogramming ameliorates cellular hallmarks of aging and extends lifespan. *EMBO Molecular Medicine*, 17, 1-22. PMID: 40588563

36. Sidler, C., Kovalchuk, O., & Kovalchuk, I. (2014). A role for SUV39H1-mediated H3K9 trimethylation in the control of genome stability and senescence in WI38 human diploid lung fibroblasts. *Aging (Albany NY)*, 6(7), 545-563. PMID: 25063769

37. Soufi, A., Donahue, G., & Zaret, K. S. (2012). Facilitators and impediments of the pluripotency reprogramming factors' initial engagement with the genome. *Cell*, 151(5), 994-1004. PMID: 23159369

38. Soufi, A., Fernandez Garcia, M., Jaroszewicz, A., et al. (2015). Pioneer transcription factors target partial DNA motifs on nucleosomes to initiate reprogramming. *Cell*, 161(3), 555-568. PMID: 25892221

39. Sridharan, R., Gonzales-Cope, M., Chronis, C., et al. (2013). Proteomic and genomic approaches reveal critical functions of H3K9 methylation and heterochromatin protein-1γ in reprogramming to pluripotency. *Nature Cell Biology*, 15(7), 872-882. PMID: 23748610

40. Tsurumi, A., & Li, W. X. (2012). Global heterochromatin loss: a unifying theory of aging? *Epigenetics*, 7(7), 680-688. PMID: 22647267

41. Wapinski, O. L., Lee, Q. Y., Law, A. C., et al. (2017). Rapid chromatin switch in the direct reprogramming of fibroblasts to neurons. *Cell Reports*, 20(13), 3236-3247. PMID: 28954238

42. Wu, Z., Qu, J., & Liu, G. H. (2024). Roles of chromatin and genome instability in cellular senescence and their relevance to ageing and related diseases. *Nature Reviews Molecular Cell Biology*, 25(12), 979-1000. PMID: 39363000

43. Yang, J. H., Hayano, M., Griffin, P. T., et al. (2023). Loss of epigenetic information as a cause of mammalian aging. *Cell*, 186(2), 305-326.e27. PMID: 36638792

44. Zhang, Y., Amaral, M.L., Zhu, C. et al. Single-cell epigenome analysis reveals age-associated decay of heterochromatin domains in excitatory neurons in the mouse brain. Cell Research 32, 1008–1021 (2022). https://doi.org/10.1038/s41422-022-00719-6
