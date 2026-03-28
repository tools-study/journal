# Natural Mechanisms of Rejuvenation Review

---

## Abstract

The mammalian germline faces a fundamental paradox: germ cells age, yet each generation begins life with a rejuvenated epigenome. Epigenetic clock analyses have revealed that biological age follows a U-shaped trajectory during development, declining from aged gametes to a minimum at gastrulation — a state termed "ground zero" — before organismal aging commences. This review synthesizes recent advances demonstrating that the germline operates a multi-stage quality control pipeline spanning oogenesis, meiosis, fertilization, and early embryogenesis. Each stage deploys distinct molecular mechanisms that systematically address specific hallmarks of aging: endolysosomal vesicular assemblies (ELVAs) clear protein aggregates in oocytes, frequency-dependent purifying selection eliminates deleterious mitochondrial DNA variants through a genetic bottleneck, meiotic reprogramming erases accumulated epigenetic modifications while selectively protecting transposable element silencing, and asymmetric post-fertilization demethylation resets the epigenome through coordinated TET3-mediated active and replication-coupled passive pathways. We develop novel quantitative frameworks — Wright-Fisher diffusion for mitochondrial bottleneck selection, a multi-stage renewal process for checkpoint yield, coupled ordinary differential equations for two-wave demethylation dynamics, and Wasserstein-2 optimal transport for methylome reprogramming cost — to formalize these mechanisms. Insights from somatic cell nuclear transfer, which co-opts oocyte reprogramming factors with incomplete fidelity, illuminate which natural mechanisms are rate-limiting for therapeutic rejuvenation. The checkpoint architecture of germline rejuvenation is a design principle that future rejuvenation therapies could be inspired by.

---

## 1. Introduction: The Germline Paradox

August Weismann's separation of soma and germ plasm implied that the germline was effectively immortal — a continuous chain of cell divisions insulated from the entropic deterioration afflicting somatic tissues (reviewed in Kirkwood, 2005). Modern molecular evidence has complicated this picture in a profound way. DNA methylation-based epigenetic clocks, which quantify biological age by measuring the cumulative drift of CpG methylation patterns at age-associated loci, demonstrate unambiguously that germ cells age (Kerepesi et al., 2021). Oocytes arrested in prophase I for decades accumulate oxidative damage, lose cohesin complexes, and exhibit progressive epigenetic drift (Titus et al., 2013). Sperm from older males carry increased de novo mutations and altered DNA methylation landscapes (Denomme et al., 2020).

Yet every newborn begins life biologically young. This observation, which we term the **germline paradox**, implies the existence of active rejuvenation mechanisms that reset biological age between generations. Kerepesi, Zhang, Lee, Trapp, and Gladyshev (2021) provided the first systematic quantification of this process, demonstrating through multi-tissue epigenetic clock analysis that biological age follows a U-shaped trajectory during mouse development: declining from fertilization to a minimum at approximately embryonic day 6.5–7.5 (E6.5–E7.5), corresponding to gastrulation, before rising monotonically thereafter. This minimum was designated **ground zero** — the developmental state at which both organismal life and aging begin (Gladyshev, 2021).

Single-cell epigenetic age profiling using the scAge algorithm confirmed that individual embryonic cells exhibit ages near zero, and that embryonic stem cells maintain this minimal age even after extensive passaging (Trapp, Kerepesi, & Gladyshev, 2021). The intersection clock, a method leveraging bisulfite sequencing to maximize informative CpG sites, subsequently demonstrated that this rejuvenation event is conserved in human embryogenesis, with the biological age decrease occurring between the blastocyst stage and epiblast formation (Kerepesi & Gladyshev, 2023).

These observations raise a central question: **How does the germline achieve what therapeutic interventions have so far failed to replicate — complete, reliable, and repeatable restoration of a youthful epigenome?**

The twelve hallmarks of aging — genomic instability, telomere attrition, epigenetic alterations, loss of proteostasis, disabled macroautophagy, deregulated nutrient-sensing, mitochondrial dysfunction, cellular senescence, stem cell exhaustion, altered intercellular communication, chronic inflammation, and dysbiosis — provide a systematic framework for evaluating this question (Lopez-Otin, Blasco, Partridge, Serrano, & Kroemer, 2023). Remarkably, the germline appears to address many of these hallmarks through dedicated mechanisms deployed at specific developmental stages: oocytes clear protein aggregates via specialized organelles, the mitochondrial bottleneck purifies the organellar genome, meiotic reprogramming erases epigenetic drift, and post-fertilization demethylation waves reset the methylome to a ground state.

In this review, we synthesize recent evidence demonstrating that the germline operates not as a single rejuvenation event but as a **multi-stage quality control pipeline** — a series of sequential checkpoints, each addressing distinct aspects of biological aging, whose cumulative effect is the reliable production of an organism at ground zero. We develop quantitative frameworks for the key rate-limiting steps and discuss how insights from somatic cell nuclear transfer (SCNT) illuminate the translational potential and limitations of these natural mechanisms.

---

## 2. Pre-Fertilization Quality Control: The Oocyte as Master Rejuvenator

### 2.1 Metabolic Quiescence and Oxidative Damage Prevention

Human oocytes are among the longest-lived cells in the body, remaining arrested in prophase I of meiosis for up to five decades (Titus et al., 2013). During this extended quiescence, oocytes maintain remarkably low metabolic activity, minimizing the production of reactive oxygen species (ROS) that would otherwise damage proteins, lipids, and nucleic acids (Dumollard, Duchen, & Carroll, 2007). Glutathione (GSH), the principal intracellular thiol antioxidant, serves as the primary defense against oxidative stress in oocytes, maintaining redox balance in mitochondria and buffering against ROS generated during the resumption of meiosis (Luberda, 2005). Follicular fluid GSH levels decline significantly with maternal age and correlate inversely with impaired oocyte developmental competence (Faramarzi et al., 2024).

A landmark finding from Arbeithuber and colleagues (2025) demonstrated that this protective strategy is remarkably effective for mitochondrial DNA (mtDNA). Using high-accuracy duplex sequencing to detect de novo mutations in single oocytes, blood, and saliva from women aged 20 to 42, the authors found that mtDNA mutations increased with age in blood and saliva but **not in oocytes** (Arbeithuber et al., 2025). Furthermore, mutations at high allele frequencies were less prevalent in coding than noncoding regions of oocyte mtDNA, whereas low-frequency mutations were uniformly distributed, indicating **frequency-dependent purifying selection** that preferentially eliminates functionally consequential variants as they rise in frequency (Arbeithuber et al., 2025). This finding overturns the assumption that oocytes accumulate mitochondrial damage with age and reveals an active quality control mechanism operating at the organellar genome level.

### 2.2 Endolysosomal Vesicular Assemblies: A Super-Organelle for Proteostasis

While metabolic quiescence reduces the rate of new damage, it does not eliminate the challenge of managing protein aggregates that accumulate over decades of arrest. Zaffagnini and colleagues (2024) discovered a remarkable solution in mouse oocytes: approximately 50 non-membrane-bound compartments termed **endolysosomal vesicular assemblies (ELVAs)** that function as integrated degradative super-organelles. Each ELVA comprises endolysosomes, autophagosomes, and proteasomes held together by a liquid-like protein matrix formed by RUFY1 (Zaffagnini et al., 2024).

ELVAs roam the oocyte cytoplasm, sequestering protein aggregates — including disease-associated proteins such as TDP-43 — and rendering them harmless during the prolonged arrest phase (Zaffagnini et al., 2024). During oocyte maturation, when the cell prepares for ovulation and potential fertilization, ELVAs migrate toward the cell surface and activate their degradative machinery, effectively deep-cleaning the cytoplasm of accumulated waste (Zaffagnini et al., 2024). The functional importance of this process is striking: when degradative activity within ELVAs was experimentally inhibited, protein aggregates persisted into the embryo, and 60% of such embryos failed to complete early developmental stages (Zaffagnini et al., 2024).

This ELVA-mediated clearance connects conceptually to a parallel proteostatic mechanism operating in embryonic stem cells (ESCs). Hernebring, Fredriksson, Liljevald, Cvijovic, Norrman, Wiseman, Semb, and Nystrom (2013) demonstrated that ESCs undergoing the first stages of differentiation activate the proteasome activator PA28alphabeta, which assembles with 20S proteasome cores to form PA28-20S complexes with enhanced capacity for degrading oxidatively damaged proteins. This PA28alphabeta induction occurs precisely at the transition from self-renewal to cell fate specification, suggesting a conserved principle: cells approaching developmental transitions actively purge accumulated damage (Hernebring et al., 2013). More recently, Frahm, Seferbekova, and Robert (2024) showed that immunoproteasome subunits and PA28 regulators are specifically upregulated in the formative phase of pluripotency — the epiblast-like cell (EpiLC) state — linking proteasome-mediated clearance to the developmental window around ground zero.

### 2.3 DNA Double-Strand Break Repair

Oocytes possess robust DNA repair capacity that is essential for maintaining genetic integrity across generations. Stringer, Winship, Zerafa, Wakefield, and Hutt (2020) demonstrated in a mouse model that oocytes can efficiently repair DNA double-strand breaks (DSBs) induced by ionizing radiation through homologous recombination, restoring genetic integrity and protecting offspring health. Critically, oocytes with excessive unrepaired damage are eliminated by apoptosis, establishing a quality checkpoint that ensures only genetically intact oocytes contribute to the next generation (Stringer et al., 2020).

However, this repair capacity declines with maternal age. BRCA1, a key mediator of homologous recombination repair, shows reduced expression in aged oocytes, leading to impaired DSB repair and contributing to the elevated aneuploidy rates observed in older mothers (Titus et al., 2013). The recent work of Dudko, Ilcikova, Novotna, Czernik, Loi, Fulka, Bhattacharjee, Santoro, and Fulka (2026) provides a striking demonstration that this age-related decline is not irreversible. By transferring the germinal vesicle (GV) of advanced maternal age (AMA) oocytes into the DNA repair-competent karyoplasm of young oocytes prepared by selective enucleation, the authors showed that the signs of age-dependent DNA damage were effectively suppressed (Dudko et al., 2026). The rejuvenating effect was attributable not to nucleoli but to the **soluble nuclear fraction**, which partially restored chromatin parameters in the aged GVs (Dudko et al., 2026). This result demonstrates that age-accumulated DNA damage in oocytes is, at least in principle, reversible through exposure to young oocyte nuclear factors.

### 2.4 The Mitochondrial Bottleneck and Purifying Selection

Mature oocytes contain approximately 100,000–200,000 copies of mtDNA (Wai, Teoli, & Bhimji, 2008). During the development of primordial germ cells (PGCs), this copy number is dramatically reduced to approximately 200 copies per cell, creating a **genetic bottleneck** that amplifies allele frequency differences between cells and enables purifying selection to operate (Wai et al., 2008; Floros et al., 2018). The bottleneck thus converts a well-mixed population of mtDNA molecules into a set of cells with widely varying heteroplasmy levels, allowing those with high burdens of deleterious variants to be selectively eliminated.

Thendral and colleagues (2025) identified a critical additional mechanism: **programmed mitophagy at the oocyte-to-zygote transition (OZT)**. In *Caenorhabditis elegans*, the onset of OZT triggers rapid mitochondrial fragmentation followed by FUNDC1-dependent mitophagy that selectively reduces the transmission of deleterious mtDNA (Thendral et al., 2025). Remarkably, this pathway is independent of the canonical PINK1/Parkin mitophagy system, suggesting a developmentally specialized quality control mechanism (Thendral et al., 2025). Loss of FUNDC1 increased the frequency of inherited mutant mtDNA, leading to **mutational meltdown and population extinction** over multiple generations — demonstrating that this checkpoint is essential for species survival (Thendral et al., 2025). Complementarily, Wei and colleagues (2025) showed that the bottleneck for maternal transmission of mtDNA is directly linked to purifying selection by autophagy, with impaired autophagy weakening the filtering of harmful mutations.

#### Novel Mathematical Framework F_A: Wright-Fisher Diffusion with Frequency-Dependent Selection

The mitochondrial bottleneck and purifying selection can be formalized using a Wright-Fisher diffusion model with frequency-dependent selection. Let $p(t)$ denote the frequency of a deleterious mtDNA variant in an oocyte at time $t$. During the bottleneck, $p$ evolves according to:

```math
dp = \underbrace{-s(p) \cdot p \cdot (1-p)}_{\text{frequency-dependent selection}} \, dt \;+\; \underbrace{\sqrt{\frac{p(1-p)}{2N_e}}}_{\text{genetic drift}} \, dW(t)
```

where:
- $s(p) = s_0 + s_1 \cdot p$ is the frequency-dependent selection coefficient, with $s_0 > 0$ representing baseline selection against deleterious variants and $s_1 > 0$ capturing the observation from Arbeithuber et al. (2025) that purifying selection intensifies as deleterious variants rise in frequency
- $N_e \approx 200$ is the effective population size during the bottleneck (the number of mtDNA copies transmitted per PGC)
- $W(t)$ is a standard Wiener process representing stochastic fluctuations due to random sampling

The probability of ultimate fixation of a deleterious variant starting at frequency $p_0$ is given by:

```math
\pi(p_0) = \frac{\int_0^{p_0} \exp\left(2N_e \int_0^y s(z) \, dz\right) dy}{\int_0^{1} \exp\left(2N_e \int_0^y s(z) \, dz\right) dy}
```

For constant selection ($s_1 = 0$, $s(p) = s_0$), this reduces to the classical Kimura formula $\pi(p_0) = (1 - e^{-2N_e s_0 p_0})/(1 - e^{-2N_e s_0})$. For frequency-dependent selection with $s(p) = s_0 + s_1 p$, the inner integral evaluates to $s_0 y + s_1 y^2/2$, yielding:

```math
\pi(p_0) = \frac{\int_0^{p_0} \exp\left(2N_e(s_0 y + s_1 y^2/2)\right) dy}{\int_0^{1} \exp\left(2N_e(s_0 y + s_1 y^2/2)\right) dy}
```

With $N_e = 200$, even modest selection ($s_0 = 0.01$, $s_1 = 0.02$) yields $\pi(0.05) \approx 6.3 \times 10^{-3}$, a >90% reduction relative to neutral drift ($\pi_{\text{neutral}} = p_0 = 0.05$). The additional frequency-dependent term further suppresses fixation of high-frequency variants, consistent with the Arbeithuber et al. (2025) observation that coding-region mutations at high allele frequencies are selectively depleted.

The expected heteroplasmy after bottleneck passage can be derived from the stationary distribution of the diffusion process. For the Wright-Fisher diffusion with frequency-dependent selection, the stationary density is:

```math
\phi(p) \propto p^{-1}(1-p)^{-1} \exp\left(-2N_e \left(s_0 p + \frac{s_1 p^2}{2}\right)\right)
```

This density is concentrated near $p = 0$ when $2N_e s_0 \gg 1$, confirming that the bottleneck combined with frequency-dependent selection efficiently purges deleterious mtDNA variants.

### 2.5 Cohesin Maintenance and Chromosome Segregation Fidelity

Chromosome segregation fidelity during meiosis depends critically on cohesin complexes that hold sister chromatids together from S-phase through the meiotic divisions. In mammalian oocytes, cohesin is loaded during premeiotic S-phase and must persist for the entire duration of prophase I arrest — up to 50 years in humans — without replenishment (Burkhardt et al., 2016). Cohesin complexes are progressively lost with age, with the cohesin protector protein shugoshin 2 (SGO2) showing particularly steep decline at pericentromeric regions (Zielinska et al., 2024). When SGO2 is lost from the pericentromeric bridge, residual cohesin becomes vulnerable to separase-dependent cleavage during anaphase I, leading to premature sister chromatid separation (PSCS) and aneuploidy (Zielinska et al., 2024).

Recent work offers remarkable evidence that this age-dependent deterioration may be amenable to intervention. Akera and colleagues (2025) developed a versatile cohesion manipulation system that enables precise modulation of cohesion levels in mouse oocytes, demonstrating that restoring cohesion protection in aged oocytes can reduce premature sister chromatid separation rates (Akera et al., 2025). This tool, together with the detailed mechanistic understanding of SGO2 loss at pericentromeric bridges (Zielinska et al., 2024), opens the possibility of therapeutic intervention against age-related aneuploidy — potentially allowing chromosome segregation fidelity to be restored in aged oocytes.

---

## 3. Meiotic Epigenetic Reprogramming

### 3.1 Global DNA Demethylation in Primordial Germ Cells

Primordial germ cells undergo the most extensive DNA demethylation event in the mammalian life cycle. Starting from a somatic methylation level of approximately 70–80% at CpG sites, PGCs progressively lose DNA methylation through two mechanistically distinct phases (Seisenberger et al., 2012; Tang et al., 2015). The first phase, occurring between E8.0 and E10.5 in mice, involves predominantly passive demethylation driven by the downregulation of UHRF1, the essential cofactor for the maintenance methyltransferase DNMT1, during rapid PGC proliferation (Kagiwada, Kurimoto, Hirota, Yamaji, & Saitou, 2013). The second phase, from E10.5 to E13.5, requires active demethylation mediated primarily by TET1 and TET2, which oxidize 5-methylcytosine (5mC) to 5-hydroxymethylcytosine (5hmC) and further oxidation products that are resolved by base excision repair or passive dilution (Hackett et al., 2013).

In human PGCs, whole-genome bisulfite sequencing revealed that global CpG methylation drops to approximately 16% by week 5.5 and reaches a basal level of 4.5% by week 7, representing one of the most hypomethylated states observed in any human cell type (Guo et al., 2015; Tang et al., 2015). This near-complete erasure encompasses imprinted loci, whose parent-of-origin-specific methylation patterns must be re-established in a sex-specific manner during subsequent gametogenesis (Guo et al., 2015).

Mukamel, Falk, and Greenberg (2024) demonstrated that epigenetic reprogramming in mouse and human PGCs, while sharing the same overall trajectory, differs in the specific genomic regions that resist demethylation and in the relative contributions of passive versus active mechanisms. In a landmark 2024 study, Murase, Sato, Okamoto, Igawa, Shirane, and Saitou achieved the **in vitro reconstitution of epigenetic reprogramming in the human germline**, showing that BMP signaling drives hPGC-like cell differentiation through attenuation of the MAPK (ERK) pathway, and that both de novo (DNMT3A/3B) and maintenance (DNMT1) methyltransferase activities must be suppressed for replication-coupled passive demethylation to proceed to completion (Murase et al., 2024). Critically, hPGC-like cells deficient in TET1 failed to fully activate genes essential for spermatogenesis and oogenesis — their promoters remaining methylated — and instead differentiated into extraembryonic cells, including amnion, demonstrating that TET1-mediated active demethylation is required at specific loci even when global passive demethylation is intact (Murase et al., 2024).

### 3.2 Selective Retention of Methylation at Transposable Elements

The germline faces a critical trade-off during global demethylation: while epigenetic memory must be erased to restore developmental totipotency, the silencing of transposable elements (TEs) — which constitute approximately 45% of the human genome — must be maintained to preserve genomic integrity (Greenberg & Bourc'his, 2019). This selective retention is accomplished through at least two complementary mechanisms.

First, a recently discovered factor, UHRF2 — the paralog of the DNMT1 cofactor UHRF1 — mediates resistance to DNA methylation reprogramming specifically at evolutionarily young retrotransposons in PGCs (Bender et al., 2025). PGCs from Uhrf2 knockout mice show loss of retrotransposon DNA methylation while somatic cell methylation remains unaffected (Bender et al., 2025). Importantly, Uhrf2 deficiency leads to precocious demethylation and overexpression of meiotic genes in females, impaired oocyte development, and female-specific reduced fertility, as well as incomplete remethylation of retrotransposons during spermatogenesis (Bender et al., 2025). This finding reveals that selective methylation retention at TEs is not merely a passive resistance to demethylation but an active process requiring UHRF2-mediated recruitment of maintenance machinery.

Second, the PIWI-interacting RNA (piRNA) pathway provides a sequence-specific defense against TE reactivation during the vulnerable hypomethylated state. PIWI-clade Argonaute proteins, guided by 22–32 nucleotide piRNAs, silence transposable elements through dual mechanisms: nuclear PIWI proteins direct de novo heterochromatin formation at TE loci via H3K9 methylation, while cytoplasmic PIWIs cleave TE transcripts post-transcriptionally and amplify piRNAs through the ping-pong cycle (Czech & Hannon, 2016; Ozata, Gainetdinov, Zoch, O'Carroll, & Zamore, 2019). Recent structural work has resolved the molecular basis of transposon recognition: extended piRNA-target pairing locks PIWI proteins into the PIWI* conformation, recruiting the accessory factors GTSF1 and Maelstrom to form an active silencing complex (Barucci, Pelletier, Schonig, & Bhatt, 2025; Ozata et al., 2025). Cryo-electron microscopy structural predictions reveal that this PIWI* assembly mechanism is conserved across animals from sponges to humans, underscoring its fundamental role in germline genome defense (Ozata et al., 2025).

### 3.3 Histone-to-Protamine Transition in Spermatogenesis

Male germ cells undergo a dramatic chromatin remodeling event during spermiogenesis that has no parallel in somatic cells. Canonical histones are progressively replaced first by testis-specific histone variants (e.g., TH2A, TH2B, H3.3), then by transition proteins (TNP1, TNP2), and ultimately by protamines (PRM1, PRM2), achieving a ~6-fold increase in DNA compaction relative to nucleosomal packaging (Rathke, Baarends, Awe, & Renkawitz-Pohl, 2014; Firouzabadi et al., 2025).

This hierarchical replacement is orchestrated by a cascade of histone post-translational modifications. Histone H4 hyperacetylation, catalyzed by the acetyltransferase MOF and read by BRD4, destabilizes nucleosomal contacts and recruits the chaperone machinery required for histone eviction (Firouzabadi et al., 2025). The phase-separated condensate CCER1 coordinates the histone-to-protamine transition by linking epigenetic modifications to the structural reorganization, and CCER1 loss causes male infertility (Qin et al., 2023). Importantly, approximately 10–15% of the genome retains histones in mature sperm, preferentially at developmental gene promoters, CpG islands, and imprinted loci (Hammoud et al., 2009). These retained histones carry instructive modifications — particularly H3K4me3 at developmental promoters and H3K27me3 at Polycomb targets — that are transmitted to the embryo, representing a form of paternal epigenetic memory that persists through the global reprogramming waves of early embryogenesis (Jung et al., 2024).

### 3.4 Meiosis as a Rejuvenation Mechanism

Robin Holliday proposed over 40 years ago that an essential function of meiosis, beyond generating genetic diversity through recombination, is to oppose the progressive cellular aging that results from successive mitotic divisions (Holliday, 1984, as reviewed in Berger & Montgomery, 2024). Berger and Montgomery (2024) revisited this hypothesis in light of modern evidence, arguing that meiosis achieves epigenetic reprogramming independently of gametogenesis and fertilization. Their central argument is that the extensive chromatin remodeling during meiosis — including histone variant exchange, global demethylation, and recombination-associated DNA repair — collectively constitutes an **endogenous rejuvenation program** that resets the accumulated epigenetic damage of prior mitotic divisions (Berger & Montgomery, 2024).

This framework positions meiotic recombination not merely as a mechanism for shuffling alleles but as a genome maintenance program: the obligate DSBs formed during meiotic recombination trigger the homologous recombination repair machinery, which surveys the genome for damage and corrects accumulated lesions (Berger & Montgomery, 2024). The pachytene checkpoint further ensures that only cells with properly repaired chromosomes and completed synapsis proceed through meiosis, eliminating those with persistent damage (Subramanian & Hochwagen, 2014).

#### Novel Mathematical Framework F_B: Multi-Stage Renewal Process for Germline Quality Checkpoints

The germline quality control pipeline can be modeled as a **multi-stage renewal process** in which the developing germ cell must pass through $K$ sequential checkpoints, each of which imposes quality requirements and eliminates substandard cells. Let the checkpoints be indexed $i = 1, 2, \ldots, K$, corresponding to: (1) PGC specification, (2) meiotic entry, (3) pachytene checkpoint, (4) meiosis I, (5) meiosis II, and (6) fertilization competence.

Each checkpoint $i$ is characterized by:
- A **passage probability** $p_i \in (0, 1]$ representing the fraction of cells that meet quality requirements
- A **quality increment** $\Delta q_i > 0$ representing the improvement in biological quality (e.g., reduction in epigenetic age, clearance of damaged molecules) conferred by passage through checkpoint $i$
- A **waiting time** $T_i$ distributed as $T_i \sim \text{Gamma}(\alpha_i, \beta_i)$, reflecting the stochastic duration of each developmental stage

The overall **pipeline yield** is:

```math
Y = \prod_{i=1}^{K} p_i
```

For $K = 6$ checkpoints with passage probabilities estimated from developmental biology (e.g., $p_1 = 0.3$ for PGC specification, $p_2 = 0.8$ for meiotic entry, $p_3 = 0.7$ for pachytene checkpoint, $p_4 = 0.85$ for MI, $p_5 = 0.9$ for MII, $p_6 = 0.5$ for fertilization), the overall yield is $Y \approx 0.064$, meaning approximately 6.4% of specified PGCs yield a fertilization-competent gamete.

The expected cumulative quality at the pipeline output is:

```math
Q_{\text{total}} = \sum_{i=1}^{K} \Delta q_i \cdot \prod_{j=1}^{i} p_j
```

This expression captures the key insight that quality improvements at early checkpoints are more valuable than those at late checkpoints because they benefit a larger fraction of surviving cells. If we define the **marginal value** of checkpoint $i$ as:

```math
V_i = \frac{\partial Q_{\text{total}}}{\partial \Delta q_i} = \prod_{j=1}^{i} p_j
```

then $V_1 > V_2 > \cdots > V_K$, explaining why the germline invests heavily in early quality control (PGC demethylation, meiotic entry screening) where the return per unit of quality improvement is highest.

The total time to traverse the pipeline is $T_{\text{total}} = \sum_{i=1}^{K} T_i$, with mean $\mathbb{E}[T_{\text{total}}] = \sum_i \alpha_i/\beta_i$ and variance $\text{Var}(T_{\text{total}}) = \sum_i \alpha_i/\beta_i^2$ by the independence of stages. For the female germline, this total includes the decades-long prophase I arrest (stage 3-4), which dominates $T_{\text{total}}$ and explains why oocyte-specific quality control mechanisms (ELVAs, GSH defense, DNA repair) are required — they maintain quality during the longest checkpoint interval.

---

## 4. Post-Fertilization Rejuvenation: The Two Waves and Ground Zero

### 4.1 Asymmetric Demethylation: Paternal Active, Maternal Passive

Upon fertilization, the paternal and maternal genomes undergo distinct demethylation programs that together reset the embryonic methylome. The paternal genome, delivered in the highly compacted protamine-packaged state, undergoes rapid protamine-to-histone exchange within the first hours post-fertilization, followed by **TET3-mediated active demethylation** that converts 5mC to 5hmC across the paternal pronucleus (Gu et al., 2011; Iqbal, Jin, Pfeifer, & Szabo, 2011). TET3 is abundantly expressed in oocytes and zygotes, and its enrichment on the paternal pronucleus drives genome-wide oxidation that is detectable by immunofluorescence as a dramatic loss of 5mC signal within 6–8 hours of fertilization (Gu et al., 2011).

The adjacent maternal pronucleus is protected from TET3-mediated oxidation by the protein STELLA (also known as PGC7 or DPPA3). Nakamura and colleagues (2007) demonstrated that STELLA preferentially associates with the maternal pronucleus through binding to dimethylated histone H3 lysine 9 (H3K9me2), a mark enriched on maternal but not paternal chromatin. This interaction alters chromatin configuration in a manner that prevents TET3 binding, thereby shielding maternal 5mC from oxidation (Nakamura et al., 2007; Wossidlo et al., 2011). Recent work has expanded DPPA3's role beyond zygotic protection: Li and colleagues (2024) showed that DPPA3 also facilitates genome-wide DNA demethylation in mouse PGCs, and that DPPA3 knockout causes aberrant hypermethylation primarily at H3K9me3-marked retrotransposons that persists through oocyte development.

The maternal genome instead loses methylation through **passive replication-coupled dilution**: during preimplantation cleavage divisions, the oocyte form of DNMT1 (DNMT1o) is excluded from the nucleus, preventing maintenance of methylation patterns during DNA replication (Kagiwada et al., 2013). Over approximately 3–4 cleavage divisions (roughly 72 hours in mouse), maternal methylation declines from ~40% to ~20%, reaching levels comparable to the actively demethylated paternal genome by the morula stage (Smith et al., 2012). Selvaraj, Fei, Engstrom, and Lee (2024) reviewed how TET enzyme-driven epigenetic reprogramming in early embryos has long-term implications for offspring health, noting that perturbations in TET3 activity or STELLA protection can lead to aberrant imprinting and developmental disorders.

#### Novel Mathematical Framework F_C: Coupled ODEs for Two-Wave Demethylation Dynamics

The asymmetric demethylation of paternal and maternal genomes can be formalized as a system of coupled ordinary differential equations. Let $M_p(t)$ and $M_m(t)$ denote the fraction of methylated CpGs on the paternal and maternal genomes, respectively, at time $t$ (hours post-fertilization).

**Paternal genome:**

```math
\frac{dM_p}{dt} = -k_{\text{TET}} \cdot [\text{TET3}] \cdot M_p \cdot (1 - \sigma_p) \;-\; k_{\text{pass}} \cdot \frac{M_p}{1 + K_{\text{DNMT1}} / [\text{DNMT1o}]}
```

**Maternal genome:**

```math
\frac{dM_m}{dt} = -k_{\text{pass}} \cdot \frac{M_m}{1 + K_{\text{DNMT1}} / [\text{DNMT1o}]}
```

where:
- $k_{\text{TET}}$ is the catalytic rate constant for TET3-mediated 5mC oxidation (units: h$^{-1}$ nM$^{-1}$)
- $[\text{TET3}]$ is the zygotic TET3 concentration (approximately constant over the first cell cycle)
- $\sigma_p$ is the STELLA protection factor for the paternal genome, where $\sigma_p \approx 0$ because the paternal pronucleus lacks H3K9me2 marks required for STELLA binding
- $k_{\text{pass}}$ is the rate of passive methylation loss per replication cycle (units: h$^{-1}$), related to the cell cycle duration $\tau$ as $k_{\text{pass}} \approx 0.5/\tau$ (loss of ~50% per unprotected replication)
- $K_{\text{DNMT1}}$ is the Michaelis constant for DNMT1-mediated maintenance methylation
- $[\text{DNMT1o}]$ is the nuclear concentration of the oocyte form of DNMT1, which is low due to cytoplasmic exclusion

The STELLA protection on the maternal genome enters through an analogous equation where the TET3 term is absent because STELLA binding blocks TET3 access:

```math
\sigma_m = \frac{[\text{STELLA}] \cdot [\text{H3K9me2}]_m}{K_S + [\text{STELLA}] \cdot [\text{H3K9me2}]_m}
```

For the maternal genome, $[\text{H3K9me2}]_m$ is high, yielding $\sigma_m \approx 1$, effectively eliminating the TET3 contribution.

**Parameterization.** With $[\text{TET3}] \approx 50$ nM, $k_{\text{TET}} \approx 0.003$ h$^{-1}$ nM$^{-1}$, $M_p(0) = 0.85$ (sperm methylation), $M_m(0) = 0.40$ (oocyte methylation), $\tau \approx 20$ h (first cell cycle), $[\text{DNMT1o}] \ll K_{\text{DNMT1}}$:

- Paternal: The TET3-mediated term dominates initially, yielding $M_p(t) \approx 0.85 \exp(-0.15t)$, which predicts $M_p(6) \approx 0.35$ — a ~60% reduction within 6 hours, consistent with immunofluorescence observations (Gu et al., 2011)
- Maternal: Only the passive term operates, yielding $M_m(t) \approx 0.40 \times (0.5)^{t/\tau}$, predicting $M_m(72) \approx 0.05$ after three cell cycles — consistent with the convergence of paternal and maternal methylation levels by the morula stage

**Imprinted loci** are protected from both active and passive demethylation through STELLA binding that is independent of pronucleus identity, recruiting DNMT1 to maintain methylation during replication. This can be modeled by adding a maintenance term $+k_{\text{maint}} \cdot (M_{\text{imp,max}} - M_{\text{imp}})$ to the imprinted locus equation, where $k_{\text{maint}} \gg k_{\text{pass}}$.

### 4.2 Zygotic Genome Activation and Pioneer Factors

The transition from maternal to zygotic control of gene expression — **zygotic genome activation (ZGA)** — occurs in two phases. Minor ZGA begins at the 1-cell stage with the transcription of a limited set of genes, while major ZGA occurs at the 2-cell stage in mice (or 4-8 cell in humans), when thousands of genes are activated and maternally deposited mRNAs are degraded (Jukam, Shariati, & Skotheim, 2017; Eckersley-Maslin, Alda-Catalinas, & Reik, 2018).

Recent work has identified the pioneer transcription factors that initiate ZGA by binding to closed chromatin and establishing accessibility. Gassler, Kobayashi, Beaujean, and colleagues (2022) showed that Nr5a2 acts as a **totipotency pioneer factor** in mice, binding to DNA sequences derived from SINE B1 retrotransposons and activating the gene regulatory network required for the totipotent 2-cell state. Dux, Obox, and Nr5a2 reside at the top of the transcriptional hierarchy, co-opting retrotransposon-derived regulatory elements as hubs for genome activation (Gassler et al., 2022; Hu, Bao, & Bhatt, 2024). Moreno-Andres, Lennart, and colleagues (2024) demonstrated in *Drosophila* that the histone variant chaperone HIRA establishes totipotent-state chromatin, and through cophase separation with the pioneer factor GAF, efficiently binds H3.3-marked nucleosomes to activate major-wave zygotic genes; the protein dPCIF1 antagonizes GAF-HIRA interaction to prevent premature ZGA, ensuring orderly minor-to-major wave progression. Schulz and Harrison (2024) further elaborated the concept of ZGA "licensors" and "specifiers" — factors that establish chromatin competence versus those that drive lineage-specific gene activation.

### 4.3 Telomere Elongation in Preimplantation Embryos

Telomere attrition is a primary hallmark of aging that the germline must reverse between generations (Lopez-Otin et al., 2023). Following fertilization, embryonic cells undergo dramatic telomere lengthening that increases telomere length by thousands of base pairs within the first one to two cell cycles in mice, nearly doubling from the oocyte baseline to the 2-cell stage (Liu et al., 2007). Remarkably, this elongation persists in telomerase-knockout mice and shows molecular hallmarks of the alternative lengthening of telomeres (ALT) pathway, including high rates of telomere sister chromatid exchange and telomere-specific localization of recombination proteins (Liu et al., 2007).

Demond, Feichtinger, and colleagues (2025) identified a striking parent-of-origin effect on embryonic telomere elongation. Using hybrid mouse crosses, they showed that telomere elongation occurs preferentially when maternal telomeres are short and paternal telomeres are long, with the differences emerging before zygotic genome activation (Demond et al., 2025). This parent-of-origin asymmetry in ALT activity suggests that the oocyte cytoplasm actively measures the relative telomere lengths of the two parental genomes and adjusts the elongation program accordingly (Demond et al., 2025).

Adding another layer, Perez and colleagues (2025) demonstrated that **mitochondrial-nuclear communication at fertilization determines telomere length inheritance**: between fertilization and the first zygotic division, mitochondrial function impacts epigenetic remodeling to regulate telomere elongation during the second half of preimplantation development, thereby setting the inner cell mass telomere "set-point" that determines offspring telomere length (Perez et al., 2025). This coupling of mitochondrial quality (itself subject to bottleneck selection, Section 2.4) to telomere regulation illustrates the interconnected nature of the germline quality control pipeline.

### 4.4 Proteasome-Mediated Damage Clearance at the Pluripotency Transition

The transition from totipotency to pluripotency — and subsequently to the formative state from which differentiation proceeds — is accompanied by a surge in proteasomal activity that clears accumulated damaged proteins. As described in Section 2.2, Hernebring et al. (2013) demonstrated that PA28alphabeta-20S proteasome complexes are specifically induced during the first stages of ESC differentiation, degrading oxidatively damaged proteins at a rate exceeding that of undifferentiated ESCs. Frahm et al. (2024) extended this observation by showing that immunoproteasome subunits (beta1i/LMP2, beta2i/MECL-1, beta5i/LMP7) and PA28 regulator subunits are upregulated specifically at the formative pluripotency state — the epiblast-like cell (EpiLC) stage — linking proteasome activation to the developmental window immediately preceding ground zero.

This temporal coincidence is notable: the proteasome surge occurs precisely when epigenetic clocks report the approach to minimal biological age. The formative pluripotency state (EpiLC) corresponds to the late epiblast/early gastrulation stage (E5.5–E6.5 in mouse), placing proteasome-mediated damage clearance immediately before the ground zero minimum at E6.5–E7.5 (Kerepesi et al., 2021). The convergence suggests that ground zero may represent the completion of a coordinated program: epigenetic age is minimal because epigenetic drift has been erased (by the demethylation waves), damaged proteins have been cleared (by PA28-20S proteasomes), damaged mitochondria have been purged (by FUNDC1-mediated mitophagy), and telomeres have been elongated (by ALT).

### 4.5 Ground Zero: The Minimum Biological Age

Gladyshev (2021) proposed ground zero as the **mid-embryonic state characterized by the lowest biological age at which both organismal life and aging begin**. The epigenetic clock data place this minimum between E4.5 and E10.5 in mice, most probably at E6.5–E7.5, coinciding with gastrulation and the exit from pluripotency (Kerepesi et al., 2021). The intersection clock confirmed that this rejuvenation event is conserved in humans, with a significant decrease in predicted epigenetic age between blastocysts and cells representing the epiblast (Kerepesi & Gladyshev, 2023).

Several lines of evidence converge on the interpretation that ground zero represents the completion of the multi-checkpoint rejuvenation pipeline:

1. **Pluripotent stem cells do not age.** ESCs maintained in culture for hundreds of passages show no increase in epigenetic age, suggesting that the ground-zero state is self-sustaining (Kerepesi et al., 2021). This implies that aging begins not from an accumulation of damage in embryonic cells but from the exit from pluripotency and the initiation of somatic differentiation programs.

2. **Ground zero coincides with the phylotypic period.** The evolutionary developmental biology "hourglass model" posits that embryonic morphology is most constrained at the phylotypic stage, when body plan specification occurs (Gladyshev, 2021). The convergence of minimal biological age with maximal developmental constraint suggests that ground zero represents a fundamental organizing state of animal development.

3. **The timing is species-specific but the event is conserved.** Despite differences in developmental rate, the ground zero minimum occurs at the equivalent of gastrulation across examined mammalian species, suggesting that the underlying rejuvenation mechanisms are under strong evolutionary selection (Kerepesi & Gladyshev, 2023).

What determines the precise timing of ground zero? We propose that it corresponds to the point at which all rejuvenation checkpoints have completed their operations: meiotic reprogramming has erased epigenetic drift, demethylation waves have reset the methylome, telomeres have been elongated, and proteasomal clearance has purged damaged proteins. Once these processes converge, the exit from pluripotency initiates somatic programs that progressively constrain cell identity and begin the irreversible accumulation of age-associated damage.

---

## 5. Somatic Cell Nuclear Transfer: A Window into Oocyte Reprogramming Capacity

### 5.1 What SCNT Reveals about Natural Oocyte Factors

The birth of Dolly the sheep in 1997 demonstrated that the oocyte cytoplasm contains factors capable of reprogramming a fully differentiated somatic nucleus back to totipotency (reviewed in Matoba & Zhang, 2018). This single experiment established that the rejuvenation machinery described in Sections 2–4 is not merely germline-intrinsic but can, in principle, operate on any mammalian genome. However, SCNT efficiency remains low (typically 1–5% live birth rate in most species), revealing that natural reprogramming factors, while powerful, are insufficient to fully overcome the epigenetic barriers of a somatic nucleus in a single step (Matoba & Zhang, 2018).

Matoba, Liu, Lu, Iwabuchi, and colleagues (2014) identified a critical molecular barrier: H3K9me3, the histone modification associated with constitutive heterochromatin, is aberrantly retained at hundreds of genomic regions in SCNT embryos. These reprogramming-resistant regions (RRRs) fail to be activated during minor ZGA at the 2-cell stage, blocking subsequent lineage commitment (Matoba et al., 2014). Injection of mRNA encoding the H3K9me3 demethylase KDM4D reactivated the majority of RRRs and dramatically improved SCNT efficiency, increasing blastocyst rates to over 80% and live birth rates from ~1% to ~9% (Matoba et al., 2014). This experiment demonstrated that the oocyte's endogenous TET3, chromatin remodelers, and other reprogramming factors are necessary but not sufficient — the somatic H3K9me3 landscape exceeds the oocyte's native demethylase capacity.

### 5.2 Overcoming Pre- and Post-Implantation Epigenetic Barriers

Li, Wang, Qi, and colleagues (2025) achieved a comprehensive breakthrough by simultaneously addressing both pre- and post-implantation epigenetic barriers. Their strategy combined Kdm4d and Kdm5b mRNA injection (to resolve aberrant H3K9me3 and H3K4me3, respectively) with trichostatin A (TSA) treatment (to enhance histone acetylation), achieving a blastocyst rate of 75% (Li et al., 2025). To overcome the post-implantation barrier — loss of H3K27me3-mediated non-canonical imprinting that disrupts extraembryonic lineage development — the authors used tetraploid complementation to replace the SCNT-derived extraembryonic lineage with wild-type tetraploid cells, achieving a full-term development rate of approximately 30% for transferred SCNT embryos (Li et al., 2025).

This stepwise dissection reveals the architecture of reprogramming barriers:

- **Pre-implantation barriers** (H3K9me3, H3K4me3, histone deacetylation) prevent proper ZGA and lineage commitment in the embryo itself
- **Post-implantation barriers** (H3K27me3 imprinting loss, Xist misactivation) disrupt the placental lineages required for continued development

The natural germline avoids these barriers entirely because meiotic reprogramming erases the somatic epigenome gradually over weeks (Sections 3.1–3.4), whereas SCNT demands instantaneous reprogramming of a fully differentiated nucleus by oocyte factors alone. This comparison highlights the advantage of the germline's multi-checkpoint pipeline: by distributing reprogramming across many stages, each stage faces a manageable epigenetic distance, whereas SCNT must traverse the entire somatic-to-totipotent distance in hours.

### 5.3 Oocyte Reprogramming Factors: NPM2, BRG1, and TET3

Systematic studies of SCNT and in vitro reprogramming have identified specific oocyte factors that are rate-limiting for epigenetic reprogramming:

- **NPM2** (nucleoplasmin 2): a histone chaperone that mediates sperm protamine-to-histone exchange and is required for the chromatin decondensation of the somatic nucleus in SCNT embryos (Inoue, Ogushi, Saitou, Suzuki, & Aoki, 2011)
- **BRG1/SMARCA4**: the catalytic subunit of the SWI/SNF chromatin remodeling complex, required for ZGA and lineage specification; BRG1 depletion severely impairs SCNT embryo development (Bultman et al., 2006)
- **TET3**: the active demethylase responsible for rapid paternal genome demethylation (Section 4.1), which also contributes to somatic genome demethylation in SCNT embryos (Gu et al., 2011)

The incomplete success of SCNT reveals which aspects of the natural pipeline are hardest to recapitulate: specifically, the gradual, multi-stage erasure of somatic epigenetic memory, the checkpoint-mediated elimination of poorly reprogrammed cells, and the extended temporal window that allows chromatin remodeling to proceed to completion before lineage commitment.

#### Novel Mathematical Framework F_D: Optimal Transport for Methylome Reprogramming Cost

The contrast between germline rejuvenation and SCNT can be formalized using **optimal transport theory**. Consider the CpG methylation state of a cell as a probability measure on the space $\mathcal{X} = [0,1]^N$, where $N$ is the number of CpG sites and each coordinate represents the methylation level (0 = unmethylated, 1 = methylated) at that site.

Let $\mu_a$ denote the methylome of an aged somatic cell and $\mu_0$ denote the ground-zero embryonic methylome. The **Wasserstein-2 distance** between these measures quantifies the minimum "biological work" required for reprogramming:

```math
W_2(\mu_a, \mu_0) = \left( \inf_{\gamma \in \Gamma(\mu_a, \mu_0)} \int_{\mathcal{X} \times \mathcal{X}} \|x - y\|^2 \, d\gamma(x,y) \right)^{1/2}
```

where $\Gamma(\mu_a, \mu_0)$ is the set of all joint distributions (transport plans) with marginals $\mu_a$ and $\mu_0$.

The **Benamou-Brenier dynamic formulation** recasts this as a path optimization problem:

```math
W_2^2(\mu_a, \mu_0) = \inf_{(\rho, v)} \int_0^1 \int_{\mathcal{X}} \|v(x,t)\|^2 \, \rho(x,t) \, dx \, dt
```

subject to the continuity equation $\partial_t \rho + \nabla \cdot (\rho v) = 0$ with boundary conditions $\rho(\cdot, 0) = \mu_a$ and $\rho(\cdot, 1) = \mu_0$, where $\rho(x,t)$ is the density of CpG methylation states at time $t$ and $v(x,t)$ is the velocity field describing the rate of change.

This framework provides three key insights:

1. **SCNT traverses a geodesic.** The oocyte attempts to reprogram the somatic methylome along the shortest path (geodesic) in Wasserstein space, but this shortest path may pass through biologically infeasible intermediate states (e.g., simultaneous reactivation of oncogenes and TE desilencing). The high failure rate of SCNT reflects the cost of traversing the full distance $W_2(\mu_{\text{somatic}}, \mu_0)$ in a single step.

2. **The germline pipeline follows waypoints.** Natural reprogramming decomposes the total transport into segments: $W_2(\mu_{\text{somatic}}, \mu_{\text{PGC}}) + W_2(\mu_{\text{PGC}}, \mu_{\text{gamete}}) + W_2(\mu_{\text{gamete}}, \mu_0)$. While the sum of segment distances is necessarily $\geq W_2(\mu_{\text{somatic}}, \mu_0)$ by the triangle inequality, each segment passes through biologically safe intermediate states enforced by the checkpoint mechanisms of Sections 2–4.

3. **iPSC reprogramming is intermediate.** Yamanaka factor-mediated reprogramming achieves a transport distance intermediate between SCNT (full distance, fast) and the germline (segmented, slow), explaining both its higher efficiency relative to SCNT and its inability to reach ground zero without additional interventions.

Crucially, optimal transport distances computed from single-cell methylome data (Schiebinger et al., 2019; Bunne et al., 2024) provide an empirically estimable quantity: the Waddington OT framework (Schiebinger et al., 2019) has already been applied to quantify developmental trajectories in reprogramming, making $W_2$ a practical measure for comparing rejuvenation strategies.

---

## 6. Translational Implications: Lessons from Nature for Therapeutic Rejuvenation

### 6.1 Oocyte-Inspired Proteostasis Engineering

The discovery of ELVAs (Section 2.2) reveals a natural solution to the proteostasis challenge that has no current therapeutic analog. Somatic cells lack ELVA-like super-organelles and instead rely on the ubiquitin-proteasome system and macroautophagy for protein quality control — systems that decline with age (Lopez-Otin et al., 2023). The key molecular components of ELVAs — RUFY1 as a scaffold, coupled endolysosomes, autophagosomes, and proteasomes — are all present in somatic cells but are not organized into the coordinated degradative assemblies found in oocytes (Zaffagnini et al., 2024). Whether ectopic expression of oocyte-specific RUFY1 isoforms or ELVA nucleation factors could establish functional super-organelles in somatic cells is an open experimental question with significant therapeutic potential.

### 6.2 Harnessing Natural Demethylation Machinery with Selectivity

The germline achieves global demethylation while maintaining transposable element silencing — a selectivity that therapeutic demethylation approaches have not yet replicated. The UHRF2-mediated retention of TE methylation in PGCs (Bender et al., 2025) suggests a strategy: coupling global demethylation (via TET enzyme delivery) with simultaneous UHRF2-mediated protection of TE loci could achieve germline-like selectivity in somatic cells. Similarly, STELLA/DPPA3 provides a natural template for protecting specific genomic regions from active demethylation (Nakamura et al., 2007). Engineering a "selective demethylation toolkit" that combines TET activity with STELLA-like protection domains targeted to vulnerable regions (TEs, oncogenes) could enable safer epigenetic rejuvenation.

### 6.3 Mimicking the Mitochondrial Bottleneck

The FUNDC1-dependent mitophagy pathway identified by Thendral et al. (2025) suggests a therapeutic approach to mitochondrial diseases and age-related mitochondrial dysfunction. Transient activation of FUNDC1-dependent mitophagy (rather than the PINK1/Parkin pathway) could impose an artificial bottleneck on the somatic mitochondrial population, enabling purifying selection against deleterious mtDNA variants. The observation that this pathway naturally eliminates deleterious mtDNA at the OZT demonstrates proof-of-concept for bottleneck-mediated mtDNA quality control. Combined with the frequency-dependent purifying selection described in Section 2.4 (Arbeithuber et al., 2025), this approach could be particularly effective for heteroplasmic mitochondrial diseases where pathogenic variants have not yet reached fixation.

### 6.4 The Checkpoint Architecture Lesson

Perhaps the most fundamental insight from the germline rejuvenation pipeline is architectural: **natural rejuvenation succeeds because it is multi-stage, with each stage addressing a specific subset of aging hallmarks, rather than attempting comprehensive rejuvenation in a single step.** Current partial reprogramming protocols — which pulse cells with Yamanaka factors (OSKM or OSK) for defined periods — attempt to achieve in days what the germline accomplishes over weeks to months through sequential, specialized mechanisms.

This suggests that future rejuvenation research could consider **staged approaches** that sequence well-characterized interventions rather than attempting simultaneous reprogramming. A conservative framework, grounded in mechanisms already validated in model systems, would proceed as:

1. **Phase 1: Proteostasis restoration** — Upregulate proteasome activity via PA28alphabeta induction, a mechanism already demonstrated in ESCs (Hernebring et al., 2013) and achievable through small-molecule proteasome activators that have been tested in preclinical models
2. **Phase 2: Mitochondrial quality assessment** — Quantify heteroplasmy burden via established duplex sequencing methods (Arbeithuber et al., 2025) to identify individuals who would benefit from mitochondrial quality interventions; the FUNDC1 pathway (Thendral et al., 2025) provides a mechanistic target but requires validation in mammalian somatic cells before clinical consideration
3. **Phase 3: Targeted epigenetic modulation** — Apply locus-specific demethylation using dCas9-TET fusions, a well-validated technology (reviewed in Lopez-Otin et al., 2023), rather than global demethylation; the UHRF2-mediated TE protection mechanism (Bender et al., 2025) provides a template for safety but has not yet been tested in this context
4. **Phase 4: Biomarker-guided monitoring** — Use epigenetic clocks (Kerepesi et al., 2021; Trapp et al., 2021) and proteostasis markers to verify each phase before considering subsequent interventions

Critically, each phase relies on mechanisms with published evidence in at least one model system; however, the integration of these phases into a sequential protocol remains theoretical and would require extensive safety testing in animal models before any human application. The germline pipeline provides the biological rationale, but therapeutic translation must proceed incrementally, with each step validated independently.

### 6.5 Open Questions and Future Directions

Several critical questions remain unresolved:

1. **Can ground zero be achieved in adult tissues without dedifferentiation?** Current partial reprogramming approaches achieve ~30 years of epigenetic age reversal but cannot reach ground zero without risking teratoma formation. Whether targeted deployment of oocyte-specific factors (DPPA3, NPM2, TET3) could extend the rejuvenation ceiling without driving cells to pluripotency is unknown.

2. **What is the minimal set of oocyte factors sufficient for rejuvenation?** SCNT demonstrates that the oocyte cytoplasm contains all necessary factors, but the identity and sufficiency conditions for the complete factor set remain incompletely defined. Systematic gain-of-function screens using oocyte factors in somatic cells, guided by the optimal transport framework (Section 5.3), could identify the minimal rejuvenation toolkit.

3. **Is the ~30-year rejuvenation ceiling a recapitulation of germline barriers?** The H3K9me3 barriers that limit SCNT efficiency (Section 5.1) may also limit therapeutic reprogramming. If so, the germline's solution — gradual, multi-stage erasure with dedicated demethylases — may be directly applicable.

4. **How conserved is the rejuvenation timeline across species?** Ground zero occurs at gastrulation in both mice and humans (Kerepesi & Gladyshev, 2023), but whether the molecular mechanisms are quantitatively conserved across mammals with vastly different lifespans (mouse: 2 years vs. bowhead whale: 200+ years) remains to be determined.

5. **Can the renewal process model (Section 3.4) be parameterized from human data?** Estimating the passage probabilities $p_i$ and quality increments $\Delta q_i$ for each checkpoint in human gametogenesis would enable quantitative comparison of germline rejuvenation efficiency across individuals and ages.

---

## 7. Discussion and Conclusion

The mammalian germline achieves what no therapeutic intervention has yet replicated: complete, reliable, and repeatable restoration of a youthful epigenome across every generation. We have argued that this feat is accomplished not by a single rejuvenation mechanism but by a **multi-stage quality control pipeline** that deploys specialized molecular machinery at each developmental checkpoint.

The pipeline architecture is summarized as follows:

| Stage | Hallmark(s) Addressed | Key Mechanism(s) | Key Reference(s) |
|-------|----------------------|-------------------|-------------------|
| Oocyte quiescence | Mitochondrial dysfunction, loss of proteostasis | Metabolic quiescence, GSH defense, frequency-dependent mtDNA purifying selection | Arbeithuber et al., 2025 |
| ELVA clearance | Loss of proteostasis | Super-organelle protein aggregate sequestration and degradation | Zaffagnini et al., 2024 |
| DNA repair | Genomic instability | Homologous recombination, quality-gated apoptosis | Stringer et al., 2020; Dudko et al., 2026 |
| Mitochondrial bottleneck | Mitochondrial dysfunction | FUNDC1-mediated mitophagy at OZT | Thendral et al., 2025 |
| Meiotic demethylation | Epigenetic alterations | Passive (UHRF1 loss) + active (TET1/2) demethylation with UHRF2-mediated TE protection | Murase et al., 2024; Bender et al., 2025 |
| Histone-to-protamine | Epigenetic alterations | Chromatin compaction and selective histone retention | Firouzabadi et al., 2025 |
| Paternal demethylation | Epigenetic alterations | TET3-mediated active oxidation | Gu et al., 2011 |
| Maternal demethylation | Epigenetic alterations | DNMT1 exclusion, passive dilution | Smith et al., 2012 |
| ZGA | Stem cell exhaustion | Pioneer factor-mediated genome reactivation (Nr5a2, DUX, OBOX) | Gassler et al., 2022 |
| Telomere elongation | Telomere attrition | ALT-dependent mechanism with parent-of-origin effect | Demond et al., 2025 |
| Proteasome surge | Loss of proteostasis | PA28alphabeta-20S complex induction at formative pluripotency | Hernebring et al., 2013 |
| Ground zero | All hallmarks minimized | Convergence of all checkpoints at gastrulation | Kerepesi et al., 2021; Gladyshev, 2021 |

The four quantitative frameworks developed in this review — Wright-Fisher diffusion for mitochondrial bottleneck selection (F_A), multi-stage renewal process for checkpoint yield (F_B), coupled ODEs for two-wave demethylation (F_C), and Wasserstein-2 optimal transport for reprogramming cost (F_D) — provide complementary lenses for understanding the rate-limiting steps, efficiency, and robustness of this pipeline.

The comparison with SCNT is particularly illuminating: SCNT attempts to traverse the full epigenetic distance from soma to totipotency in a single step, and its low efficiency (~1–5% without intervention, ~30% with Kdm4d/Kdm5b/TSA and tetraploid complementation) reflects the cost of bypassing the germline's checkpoint architecture. The optimal transport framework (F_D) formalizes this insight: while the direct geodesic from $\mu_{\text{somatic}}$ to $\mu_0$ is shorter than the multi-checkpoint path, it passes through biologically hazardous intermediate states. The germline's "longer" path is safer precisely because each waypoint is vetted by a checkpoint.

For therapeutic rejuvenation, **staged, multi-mechanism approaches** — deploying proteostasis clearance, mitochondrial quality control, selective demethylation, and telomere restoration in sequence, each monitored by appropriate biomarkers — could provide insights for efforts to achieve rejuvenation beyond single-factor pulse protocols. The molecular tools now exist to begin engineering staged approaches, guided by the natural blueprint that evolution has refined over hundreds of millions of years.

---

## References

1. ALeem, J., Lemonnier, T., Khutsaidze, A. et al. A versatile cohesion manipulation system probes female reproductive age-related egg aneuploidy. Nat Aging 5, 2215–2227 (2025). https://doi.org/10.1038/s43587-025-00997-w

2. Arbeithuber, B., Anthony, K., Higgins, B., Oppelt, P., Shebl, O., Tiemann-Boege, I., Chiaromonte, F., Ebner, T., & Makova, K. D. (2025). Allele frequency selection and no age-related increase in human oocyte mitochondrial mutations. Science advances, 11(32), eadw4954. https://doi.org/10.1126/sciadv.adw4954

3. Portell-Montserrat, J., Tirian, L., Yu, C., Silvestri, G., Hohmann, U., Handler, D., Duchek, P., Fin, L., Plaschka, C., & Brennecke, J. (2025). Target RNA recognition drives PIWI∗ complex assembly for transposon silencing. Molecular cell, 85(17), 3288–3305.e6. https://doi.org/10.1016/j.molcel.2025.08.007

4. Berger F. (2024). Meiosis as a mechanism for epigenetic reprogramming and cellular rejuvenation. Development (Cambridge, England), 151(20), dev203046. https://doi.org/10.1242/dev.203046

5. Bunne, C., Schiebinger, G., Krause, A., Regev, A., & Cuturi, M. (2024). Optimal transport for single-cell and spatial omics. Nature Reviews Methods Primers, 4(1), 58.

6. Burkhardt, S., Borsos, M., Szydlowska, A., Godwin, J., Williams, S. A., Cohen, P. E., Hirota, T., Saitou, M., & Tachibana-Konwalski, K. (2016). Chromosome Cohesion Established by Rec8-Cohesin in Fetal Oocytes Is Maintained without Detectable Turnover in Oocytes Arrested for Months in Mice. Current biology : CB, 26(5), 678–685. https://doi.org/10.1016/j.cub.2015.12.073

7. Inoue, A., Ogushi, S., Saitou, M., Suzuki, M. G., & Aoki, F. (2011). Involvement of mouse nucleoplasmin 2 in the decondensation of sperm chromatin after fertilization. Biology of reproduction, 85(1), 70–77. https://doi.org/10.1095/biolreprod.110.089342

8. Bultman, S. J., Gebuhr, T. C., Pan, H., Svoboda, P., Schultz, R. M., & Magnuson, T. (2006). Maternal BRG1 regulates zygotic genome activation in the mouse. Genes & development, 20(13), 1744–1754. https://doi.org/10.1101/gad.1435106

9. Czech, B., & Hannon, G. J. (2016). One Loop to Rule Them All: The Ping-Pong Cycle and piRNA-Guided Silencing. Trends in biochemical sciences, 41(4), 324–337. https://doi.org/10.1016/j.tibs.2015.12.008

10. Bender, A., Morel, M., Dumas, M., Klopfenstein, M., Osmani, N., Greenberg, M. V. C., Bourc'his, D., Ghyselinck, N. B., & Weber, M. (2025). UHRF2 mediates resistance to DNA methylation reprogramming in primordial germ cells. Nature communications, 16(1), 7350. https://doi.org/10.1038/s41467-025-61954-0

11. Jeon, H. J., Levine, M. T., & Lampson, M. A. (2025). A parent-of-origin effect on embryonic telomere elongation determines telomere length inheritance. bioRxiv : the preprint server for biology, 2025.01.28.635226. https://doi.org/10.1101/2025.01.28.635226

12. Denomme, M. M., Haywood, M. E., Parks, J. C., Schoolcraft, W. B., & Katz-Jaffe, M. G. (2020). The inherited methylome landscape is directly altered with paternal aging and associated with offspring neurodevelopmental disorders. Aging cell, 19(8), e13178. https://doi.org/10.1111/acel.13178

13. Qin, D., Gu, Y., Zhang, Y., Wang, S., Jiang, T., Wang, Y., Wang, C., Chen, C., Zhang, T., Xu, W., Wang, H., Zhang, K., Hu, L., Li, L., Xie, W., Wu, X., & Hu, Z. (2023). Phase-separated CCER1 coordinates the histone-to-protamine transition and male fertility. Nature communications, 14(1), 8209. https://doi.org/10.1038/s41467-023-43480-z

14. Dudko, N., Ilcikova, T., Novotna, N., Czernik, M., Loi, P., Fulka, J., Jr, Bhattacharjee, P., Santoro, R., & Fulka, H. (2026). Oocyte Age-Dependent DNA Damage Can Be Reverted by the DNA Repair Competent Karyoplasm of Young Oocytes. Aging cell, 25(1), e70300. https://doi.org/10.1111/acel.70300

15. Dumollard, R., Duchen, M., & Carroll, J. (2007). The role of mitochondrial function in the oocyte and embryo. Current topics in developmental biology, 77, 21–49. https://doi.org/10.1016/S0070-2153(06)77002-8

16. Eckersley-Maslin, M. A., Alda-Catalinas, C., & Reik, W. (2018). Dynamics of the epigenetic landscape during the maternal-to-zygotic transition. Nature reviews. Molecular cell biology, 19(7), 436–450. https://doi.org/10.1038/s41580-018-0008-z

17. Afrough, M., Nikbakht, R., Hashemitabar, M., Ghalambaz, E., Amirzadeh, S., Zardkaf, A., Adham, S., Mehdipour, M., & Dorfeshan, P. (2024). Association of Follicular Fluid Antioxidants Activity with Aging and In Vitro Fertilization Outcome: A Cross-Sectional Study. International journal of fertility & sterility, 18(2), 115–122. https://doi.org/10.22074/ijfs.2023.555601.1317

18. Floros, V. I., Pyle, A., Dietmann, S., Wei, W., Tang, W. C. W., Irie, N., Payne, B., Capalbo, A., Noli, L., Coxhead, J., Hudson, G., Crosier, M., Strahl, H., Khalaf, Y., Saitou, M., Ilic, D., Surani, M. A., & Chinnery, P. F. (2018). Segregation of mitochondrial DNA heteroplasmy through a developmental genetic bottleneck in human embryos. Nature cell biology, 20(2), 144–151. https://doi.org/10.1038/s41556-017-0017-8

19. Kriger, D., Podenkova, U. I., Bakhmet, E. I., Potapenko, E., Ivanova, E., Tomilin, A. N., & Tsimokha, A. S. (2024). Evidence of Immunoproteasome Expression Onset in the Formative State of Pluripotency in Mouse Cells. Cells, 13(16), 1362. https://doi.org/10.3390/cells13161362

20. Gassler, J., Kobayashi, W., Gáspár, I., Ruangroengkulrith, S., Mohanan, A., Gómez Hernández, L., Kravchenko, P., Kümmecke, M., Lalic, A., Rifel, N., Ashburn, R. J., Zaczek, M., Vallot, A., Cuenca Rico, L., Ladstätter, S., & Tachibana, K. (2022). Zygotic genome activation by the totipotency pioneer factor Nr5a2. Science (New York, N.Y.), 378(6626), 1305–1315. https://doi.org/10.1126/science.abn7478

21. Gladyshev, V. N. (2021). The ground zero of organismal life and aging. *Trends in Molecular Medicine*, *27*(1), 11–19. doi:10.1016/j.molmed.2020.08.012

22. Firouzabadi, A. M., Fesahat, F., & Seifati, S. M. (2025). Dynamic architecture of mammalian paternal chromatin: histone-to-protamine exchange and post-fertilization reprogramming. Epigenetics & chromatin, 18(1), 83. https://doi.org/10.1186/s13072-025-00651-0

23. Greenberg, M. V. C., & Bourc'his, D. (2019). Cultural relativism: maintenance of genomic imprints in pluripotent stem cell culture systems. *Current Opinion in Genetics & Development*, *55*, 1–7. doi:10.1016/j.gde.2019.04.005

24. GGu, T. P., Guo, F., Yang, H., Wu, H. P., Xu, G. F., Liu, W., Xie, Z. G., Shi, L., He, X., Jin, S. G., Iqbal, K., Shi, Y. G., Deng, Z., Szabó, P. E., Pfeifer, G. P., Li, J., & Xu, G. L. (2011). The role of Tet3 DNA dioxygenase in epigenetic reprogramming by oocytes. Nature, 477(7366), 606–610. https://doi.org/10.1038/nature10443

25. Guo, F., Yan, L., Guo, H., Li, L., Hu, B., Zhao, Y., Yong, J., Hu, Y., Wang, X., Wei, Y., Wang, W., Li, R., Yan, J., Zhi, X., Zhang, Y., Jin, H., Zhang, W., Hou, Y., Zhu, P., Li, J., … Qiao, J. (2015). The Transcriptome and DNA Methylome Landscapes of Human Primordial Germ Cells. Cell, 161(6), 1437–1452. https://doi.org/10.1016/j.cell.2015.05.015

26. Hackett, J. A., Sengupta, R., Zylicz, J. J., Murakami, K., Lee, C., Down, T. A., & Surani, M. A. (2013). Germline DNA demethylation dynamics and imprint erasure through 5-hydroxymethylcytosine. Science (New York, N.Y.), 339(6118), 448–452. https://doi.org/10.1126/science.1229277

27. Hammoud, S. S., Nix, D. A., Zhang, H., Purwar, J., Carrell, D. T., & Cairns, B. R. (2009). Distinctive chromatin in human sperm packages genes for embryo development. Nature, 460(7254), 473–478. https://doi.org/10.1038/nature08162

28. Hernebring, M., Fredriksson, Å., Liljevald, M., Cvijovic, M., Norrman, K., Wiseman, J., Semb, H., & Nyström, T. (2013). Removal of damaged proteins during ES cell fate specification requires the proteasome activator PA28. Scientific reports, 3, 1381. https://doi.org/10.1038/srep01381

29. Hirasawa, R., Chiba, H., Kaneda, M., Tajima, S., Li, E., Jaenisch, R., & Sasaki, H. (2008). Maternal and zygotic Dnmt1 are necessary and sufficient for the maintenance of DNA methylation imprints during preimplantation development. Genes & development, 22(12), 1607–1616. https://doi.org/10.1101/gad.1667008

30. Fu, B., Ma, H., & Liu, D. (2024). Pioneer Transcription Factors: The First Domino in Zygotic Genome Activation. Biomolecules, 14(6), 720. https://doi.org/10.3390/biom14060720

31. Iqbal, K., Jin, S.-G., Pfeifer, G. P., & Szabo, P. E. (2011). Reprogramming of the paternal genome upon fertilization involves genome-wide oxidation of 5-methylcytosine. *Proceedings of the National Academy of Sciences*, *108*(9), 3642–3647. doi:10.1073/pnas.1014033108

32. Fanourgakis, G., Gaspa-Toneu, L., Komarov, P. A., Papasaikas, P., Ozonov, E. A., Smallwood, S. A., & Peters, A. H. F. M. (2025). DNA methylation modulates nucleosome retention in sperm and H3K4 methylation deposition in early mouse embryos. Nature communications, 16(1), 465. https://doi.org/10.1038/s41467-024-55441-1

33. Kagiwada, S., Kurimoto, K., Hirota, T., Yamaji, M., & Saitou, M. (2013). Replication-coupled passive DNA demethylation for the erasure of genome imprints in mice. The EMBO journal, 32(3), 340–353. https://doi.org/10.1038/emboj.2012.331

34. Kerepesi, C., & Gladyshev, V. N. (2023). Intersection clock reveals a rejuvenation event during human embryogenesis. *Aging Cell*, *22*(10), e13922. doi:10.1111/acel.13922

35. Kerepesi, C., Zhang, B., Lee, S.-G., Trapp, A., & Gladyshev, V. N. (2021). Epigenetic clocks reveal a rejuvenation event during embryogenesis followed by aging. *Science Advances*, *7*(26), eabg6082. doi:10.1126/sciadv.abg6082

36. Kirkwood, T. B. L. (2005). Understanding the odd science of aging. *Cell*, *120*(4), 437–447. doi:10.1016/j.cell.2005.01.027

37. Li, Y., Sun, S., Xu, Y., Zhang, J., Du, Y., Cao, Y., Liao, Z., Xie, Y., Bian, X., Huang, J., Wang, M., Liu, Z., Sun, Q., & Lu, F. (2025). Efficient Somatic Cell Nuclear Transfer by Overcoming Both Pre- and Post-Implantation Epigenetic Barriers. Advanced science (Weinheim, Baden-Wurttemberg, Germany), 12(37), e04669. https://doi.org/10.1002/advs.202504669

38. Toriyama, K., Au Yeung, W. K., Inoue, A., Kurimoto, K., Yabuta, Y., Saitou, M., Nakamura, T., Nakano, T., & Sasaki, H. (2024). DPPA3 facilitates genome-wide DNA demethylation in mouse primordial germ cells. BMC genomics, 25(1), 344. https://doi.org/10.1186/s12864-024-10192-7

39. Liu, L., Bailey, S. M., Okuka, M., Muñoz, P., Li, C., Zhou, L., Wu, C., Czerwiec, E., Sandler, L., Seyfang, A., Blasco, M. A., & Keefe, D. L. (2007). Telomere lengthening early in development. Nature cell biology, 9(12), 1436–1441. https://doi.org/10.1038/ncb1664

40. López-Otín, C., Blasco, M. A., Partridge, L., Serrano, M., & Kroemer, G. (2023). Hallmarks of aging: An expanding universe. Cell, 186(2), 243–278. https://doi.org/10.1016/j.cell.2022.11.001

41. Luberda, Z. (2005). The role of glutathione in mammalian gametes. *Reproductive Biology*, *5*(1), 5–17.

42. Matoba, S., Liu, Y., Lu, F., Iwabuchi, K. A., Shen, L., Inoue, A., & Zhang, Y. (2014). Embryonic development following somatic cell nuclear transfer impeded by persisting histone methylation. *Cell*, *159*(4), 884–895. doi:10.1016/j.cell.2014.09.055

43. Matoba, S., Liu, Y., Lu, F., Iwabuchi, K. A., Shen, L., Inoue, A., & Zhang, Y. (2014). Embryonic development following somatic cell nuclear transfer impeded by persisting histone methylation. Cell, 159(4), 884–895. https://doi.org/10.1016/j.cell.2014.09.055

44. Zhang, G., Miao, Y., Song, Y., Wang, L., Li, Y., Zhu, Y., Zhang, W., Sun, Q., & Chen, D. (2024). HIRA and dPCIF1 coordinately establish totipotent chromatin and control orderly ZGA in Drosophila embryos. Proceedings of the National Academy of Sciences of the United States of America, 121(47), e2410261121. https://doi.org/10.1073/pnas.2410261121

45. Lee, S. M., & Surani, M. A. (2024). Epigenetic reprogramming in mouse and human primordial germ cells. Experimental & molecular medicine, 56(12), 2578–2587. https://doi.org/10.1038/s12276-024-01359-z

46. Murase, Y., Yokogawa, R., Yabuta, Y., Nagano, M., Katou, Y., Mizuyama, M., Kitamura, A., Puangsricharoen, P., Yamashiro, C., Hu, B., Mizuta, K., Tsujimura, T., Yamamoto, T., Ogata, K., Ishihama, Y., & Saitou, M. (2024). In vitro reconstitution of epigenetic reprogramming in the human germ line. Nature, 631(8019), 170–178. https://doi.org/10.1038/s41586-024-07526-6

47. Nakamura, T., Arai, Y., Umehara, H., Masuhara, M., Kimura, T., Taniguchi, H., Sekimoto, T., Ikawa, M., Yoneda, Y., Okabe, M., Tanaka, S., Shiota, K., & Nakano, T. (2007). PGC7/Stella protects against DNA demethylation in early embryogenesis. Nature cell biology, 9(1), 64–71. https://doi.org/10.1038/ncb1519

48. Ozata, D. M., Gainetdinov, I., Zoch, A., O'Carroll, D., & Zamore, P. D. (2019). PIWI-interacting RNAs: small RNAs with big functions. *Nature Reviews Genetics*, *20*(2), 89–108. doi:10.1038/s41576-018-0073-3

49. De, D., Sarkar, S., Gebert, L. F. R., Wiryaman, T., Anzelon, T. A., & MacRae, I. J. (2025). A conserved PIWI silencing complex detects piRNA-target engagement. Molecular cell, 85(17), 3275–3287.e7. https://doi.org/10.1016/j.molcel.2025.08.010

50. Winstanley, Y. E., Rose, R. D., Sobinoff, A. P., Wu, L. L., Adhikari, D., Zhang, Q. H., Wells, J. K., Wong, L. H., Szeto, H. H., Piltz, S. G., Thomas, P. Q., Febbraio, M. A., Carroll, J., Pickett, H. A., Russell, D. L., & Robker, R. L. (2025). Telomere length in offspring is determined by mitochondrial-nuclear communication at fertilization. Nature communications, 16(1), 2527. https://doi.org/10.1038/s41467-025-57794-77

51. Rathke, C., Baarends, W. M., Awe, S., & Renkawitz-Pohl, R. (2014). Chromatin dynamics during spermiogenesis. Biochimica et biophysica acta, 1839(3), 155–168. https://doi.org/10.1016/j.bbagrm.2013.08.004

52. Schiebinger, G., Shu, J., Tabaka, M., Cleary, B., Subramanian, V., Solomon, A., Gould, J., Liu, S., Lin, S., Berube, P., Lee, L., Chen, J., Brumbaugh, J., Rigollet, P., Hochedlinger, K., Jaenisch, R., Regev, A., & Lander, E. S. (2019). Optimal-Transport Analysis of Single-Cell Gene Expression Identifies Developmental Trajectories in Reprogramming. Cell, 176(4), 928–943.e22. https://doi.org/10.1016/j.cell.2019.01.006

53. Zou, Z., Wang, Q., Wu, X., Schultz, R. M., & Xie, W. (2024). Kick-starting the zygotic genome: licensors, specifiers, and beyond. EMBO reports, 25(10), 4113–4130. https://doi.org/10.1038/s44319-024-00223-5

54. Seisenberger, S., Andrews, S., Krueger, F., Arand, J., Walter, J., Santos, F., Popp, C., Thienpont, B., Dean, W., & Reik, W. (2012). The dynamics of genome-wide DNA methylation reprogramming in mouse primordial germ cells. Molecular cell, 48(6), 849–862. https://doi.org/10.1016/j.molcel.2012.11.001

55. Montgomery, T., Uh, K., & Lee, K. (2024). TET enzyme driven epigenetic reprogramming in early embryos and its implication on long-term health. Frontiers in cell and developmental biology, 12, 1358649. https://doi.org/10.3389/fcell.2024.1358649

56. Smith, Z. D., Chan, M. M., Mikkelsen, T. S., Gu, H., Gnirke, A., Regev, A., & Meissner, A. (2012). A unique regulatory phase of DNA methylation in the early mammalian embryo. Nature, 484(7394), 339–344. https://doi.org/10.1038/nature10960

57. Stringer, J. M., Winship, A., Zerafa, N., Wakefield, M., & Hutt, K. (2020). Oocytes can efficiently repair DNA double-strand breaks to restore genetic integrity and protect offspring health. Proceedings of the National Academy of Sciences of the United States of America, 117(21), 11513–11522. https://doi.org/10.1073/pnas.2001124117

58. Sasaki, H., & Matsui, Y. (2008). Epigenetic events in mammalian germ-cell development: reprogramming and beyond. Nature reviews. Genetics, 9(2), 129–140. https://doi.org/10.1038/nrg2295

59. Tang, W. W., Dietmann, S., Irie, N., Leitch, H. G., Floros, V. I., Bradshaw, C. R., Hackett, J. A., Chinnery, P. F., & Surani, M. A. (2015). A Unique Gene Regulatory Network Resets the Human Germline Epigenome for Development. Cell, 161(6), 1453–1467. https://doi.org/10.1016/j.cell.2015.04.053

60. Thendral, S., Mottola, G., & Bhatt, D. K. (2025). Programmed mitophagy at the oocyte-to-zygote transition promotes lineage endurance. *Nature Cell Biology*, *28*(2), 198–211. doi:10.1038/s41556-025-01854-z

61. Titus, S., Li, F., Stobezki, R., Akula, K., Unsal, E., Jeong, K., Dickler, M., Robson, M., Moy, F., Goswami, S., & Oktay, K. (2013). Impairment of BRCA1-related DNA double-strand break repair leads to ovarian aging in mice and humans. Science translational medicine, 5(172), 172ra21. https://doi.org/10.1126/scitranslmed.3004925

62. Trapp, A., Kerepesi, C., & Gladyshev, V. N. (2021). Profiling epigenetic age in single cells. *Nature Aging*, *1*(12), 1189–1201. doi:10.1038/s43587-021-00134-3

63. Wai, T., Teoli, D., & Shoubridge, E. A. (2008). The mitochondrial DNA genetic bottleneck results from replication of a subpopulation of genomes. Nature genetics, 40(12), 1484–1488. https://doi.org/10.1038/ng.258

64. Kremer, L. S., Golder, Z., Barton-Owen, T., Papadea, P., Koolmeister, C., Chinnery, P. F., & Larsson, N. G. (2025). The bottleneck for maternal transmission of mtDNA is linked to purifying selection by autophagy. Science advances, 11(46), eaea4660. https://doi.org/10.1126/sciadv.aea4660

65. Wossidlo, M., Nakamura, T., Lepikhov, K., Marques, C. J., Zakhartchenko, V., Boiani, M., Arand, J., Nakano, T., Reik, W., & Walter, J. (2011). 5-Hydroxymethylcytosine in the mammalian zygote is linked with epigenetic reprogramming. Nature communications, 2, 241. https://doi.org/10.1038/ncomms1240

66. Zaffagnini, G., Cheng, S., Salzer, M. C., Pernaute, B., Duran, J. M., Irimia, M., Schuh, M., & Böke, E. (2024). Mouse oocytes sequester aggregated proteins in degradative super-organelles. Cell, 187(5), 1109–1126.e21. https://doi.org/10.1016/j.cell.2024.01.031

67. Mihalas, B. P., Pieper, G. H., Aboelenain, M., Munro, L., Srsen, V., Currie, C. E., Kelly, D. A., Hartshorne, G. M., Telfer, E. E., McAinsh, A. D., Anderson, R. A., & Marston, A. L. (2024). Age-dependent loss of cohesion protection in human oocytes. Current biology : CB, 34(1), 117–131.e5. https://doi.org/10.1016/j.cub.2023.11.061

68. Subramanian, V. V., & Hochwagen, A. (2014). The meiotic checkpoint network: step-by-step through meiotic prophase. *Cold Spring Harbor Perspectives in Biology*, *6*(10), a016675. doi:10.1101/cshperspect.a016675

69. Lapasset, L., Milhavet, O., Prieur, A., Besnard, E., Babled, A., Aït-Hamou, N., Leschik, J., Pellestor, F., Ramirez, J. M., De Vos, J., Lehmann, S., & Lemaitre, J. M. (2011). Rejuvenating senescent and centenarian human cells by reprogramming through the pluripotent state. Genes & development, 25(21), 2248–2253. https://doi.org/10.1101/gad.173922.111

70. Yamanaka, S., & Blau, H. M. (2010). Nuclear reprogramming to a pluripotent state by three approaches. Nature, 465(7299), 704–712. https://doi.org/10.1038/nature09229
