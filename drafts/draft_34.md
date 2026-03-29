# Totipotency Review

---

## Abstract

Totipotency — the capacity of a single cell to generate all embryonic and extraembryonic lineages — represents the most fundamental yet least mechanistically understood cell state in mammalian biology. While pluripotent stem cells have been extensively characterized at the molecular level, the transient totipotent state that exists in the zygote and early cleavage-stage embryo has only recently become accessible to systematic investigation. This review synthesizes advances across three converging frontiers that are collectively transforming our understanding of how totipotency is established, maintained, and can be reconstituted. First, we examine the chromatin architecture of the totipotent state, including the non-canonical broad H3K4me3 domains that blanket the oocyte genome, the pioneer transcription factors — DUX, OBOX, NR5A2, and DPPA2/4 — that ignite zygotic genome activation (ZGA), and the dramatic three-dimensional genome reorganization involving topologically associating domain (TAD) dissolution and re-establishment that accompanies genome awakening. We develop a multi-state continuous-time Markov chain model for chromatin state transitions during ZGA and a nucleation-growth framework that explains the observed stochastic variation in ZGA timing between sister blastomeres. Second, we assess how stem cell-derived embryo models — blastoids, gastruloids, and extended embryo models — serve as functional readouts of our understanding of totipotency and self-organization, applying Turing instability analysis to morphogen-driven symmetry breaking in these systems. Third, we evaluate the progress and challenges of in vitro gametogenesis (IVG), the ultimate test of whether the totipotent program can be reconstituted from differentiated cells, introducing a Kullback-Leibler divergence framework for quantifying epigenetic fidelity. Together, these advances reveal that totipotency is not a single molecular switch but an emergent property arising from the coordinated action of redundant pioneer factors, co-opted retrotransposon regulatory networks, and biomolecular condensate-mediated transcriptional activation — a design principle with profound implications for reproductive medicine and regenerative biology.

---

## 1. Introduction: The Totipotency Question

The fertilized mammalian egg possesses a property shared by no other cell in the adult body: the capacity to generate an entire organism, including all embryonic tissues and the extraembryonic lineages — trophectoderm and primitive endoderm — that support development in utero (Rossant & Tam, 2009). This property, termed **totipotency**, distinguishes the zygote and early cleavage-stage blastomeres from pluripotent cells of the inner cell mass (ICM), which can generate all embryonic germ layers but lack the capacity for trophectoderm contribution under standard conditions (Nichols & Smith, 2009). The experimental demonstration that isolated mouse blastomeres at the 2-cell stage can each develop into complete organisms established that totipotency persists through at least the first cleavage division (Tarkowski, 1959), while subsequent work showed that this capacity is progressively restricted during pre-implantation development (Kelly, 1977).

Despite its foundational importance, the molecular program that establishes and maintains totipotency has remained elusive for decades. The central challenge is that the totipotent state is extraordinarily transient — lasting approximately 24–48 hours in the mouse, from fertilization through the 2-cell stage — and involves a cell that is simultaneously executing the most dramatic chromatin reprogramming event in the mammalian life cycle: **zygotic genome activation (ZGA)** (Schulz & Harrison, 2019). During ZGA, the transcriptionally silent zygotic genome transitions from a state of near-complete quiescence to robust transcriptional activity, a process that involves the coordinated action of maternally deposited pioneer transcription factors, wholesale chromatin remodeling, and the co-option of endogenous retroviral regulatory elements (Jachowicz & Torres-Padilla, 2016).

The clinical significance of understanding ZGA cannot be overstated. In human assisted reproduction, approximately 10–15% of embryos arrest at the cleavage stage, with failure to complete the maternal-to-zygotic transition (MZT) representing a major cause of embryo loss in in vitro fertilization (IVF) (Braude, Bolton, & Moore, 1988; Vassena et al., 2011). Embryo arrest at the 4-cell to 8-cell stage — precisely when human major ZGA occurs — suggests that failures in zygotic genome activation directly contribute to reproductive failure (Wong et al., 2010). A mechanistic understanding of ZGA would therefore have immediate translational relevance for improving IVF outcomes and for the development of non-invasive biomarkers of embryo developmental competence.

Recent years have witnessed transformative advances on three converging frontiers that are fundamentally reshaping our understanding of totipotency. First, the identification of pioneer transcription factors — DUX, OBOX, NR5A2, and DPPA2/4 — that ignite ZGA has revealed a remarkably redundant regulatory architecture in which no single factor is indispensable, yet each contributes to the robustness of genome activation (De Iaco et al., 2017; Ji et al., 2023; Gassler et al., 2022; Festuccia et al., 2024). Second, stem cell-derived embryo models — blastoids, gastruloids, and extended synthetic embryo models — have provided unprecedented experimental systems for testing our mechanistic understanding of self-organization and lineage specification outside the uterus (Rivron et al., 2018; Amadei et al., 2022). Third, progress in in vitro gametogenesis has brought the reconstitution of the complete gametogenic program from pluripotent stem cells within reach, raising fundamental questions about epigenetic fidelity and clinical safety (Hayashi et al., 2012; Saitou & Hayashi, 2021).

In this review, we synthesize these advances across all three frontiers. We first examine the chromatin architecture and pioneer factor networks that drive ZGA, emphasizing the emerging principle of functional redundancy among ZGA transcription factors (Section 2). We then dissect the molecular mechanisms of ZGA itself, including the surprising regulatory roles of retrotransposable elements and biomolecular condensates, and develop novel quantitative frameworks for ZGA dynamics (Section 3). We assess how stem cell-derived embryo models serve as functional tests of our understanding of totipotency and self-organization (Section 4). Finally, we evaluate the progress and fundamental challenges of in vitro gametogenesis, which represents the ultimate reconstitution test for the totipotent program (Section 5).

---

## 2. Chromatin Architecture of the Totipotent State

### 2.1 The Epigenetic Tabula Rasa at Fertilization

The chromatin landscape of the totipotent zygote is unlike that of any other mammalian cell. Three landmark studies published simultaneously in 2016 revealed that oocytes and early embryos possess a radically non-canonical histone modification landscape (Dahl et al., 2016; Liu et al., 2016; Zhang et al., 2016). Using low-input chromatin immunoprecipitation followed by sequencing (ChIP-seq), Dahl and colleagues demonstrated that approximately 22% of the mouse oocyte genome is covered by **broad H3K4me3 domains** — expansive regions of trimethylated histone H3 lysine 4 that extend far beyond promoters and are anti-correlated with DNA methylation (Dahl et al., 2016). These non-canonical broad domains are a defining feature of the oocyte chromatin state and are absent from somatic cells, where H3K4me3 is confined to narrow peaks at active promoters (Dahl et al., 2016).

The functional significance of these broad domains became clear through the observation that they are actively resolved during ZGA. The lysine demethylases KDM5A and KDM5B are required for the conversion of broad H3K4me3 to the canonical narrow-peak configuration at the 2-cell stage, and depletion of these enzymes results in impaired ZGA and embryonic arrest (Dahl et al., 2016). However, recent work has revealed a more nuanced picture: broad H3K4me3 domains support oocyte genome silencing during growth and maturation but appear dispensable for transcriptional repression in early embryos, suggesting that their role may be primarily in maintaining oocyte quiescence rather than directly licensing ZGA (Boussouar et al., 2025).

Liu and colleagues (2016) further demonstrated that the H3K27me3 landscape in early embryos is also non-canonical, with broad H3K27me3 domains marking distal regulatory regions rather than promoters in oocytes, and these domains undergoing dramatic reorganization after fertilization to eventually adopt a promoter-centered pattern by the blastocyst stage (Liu et al., 2016). Importantly, Zhang and colleagues (2016) showed that the reprogramming of H3K4me3 is allele-specific: the paternal allele undergoes more rapid H3K4me3 narrowing than the maternal allele, reflecting the distinct chromatin histories of the two parental genomes (Zhang et al., 2016). The convergence of paternal and maternal H3K4me3 patterns by the 8-cell stage coincides temporally with ZGA, suggesting that histone modification reprogramming and transcriptional activation are mechanistically coupled.

Complementing the H3K4me3 landscape, the paternal and maternal genomes arrive at fertilization with profoundly asymmetric chromatin states. The paternal genome, packaged with protamines during spermiogenesis, undergoes rapid protamine-to-histone exchange after fertilization, incorporating the variant histone H3.3 deposited by the chaperone HIRA (van der Heijden et al., 2005). This results in a relatively permissive chromatin state on the paternal pronucleus, which lacks the H3K9me3 marks that extensively decorate the maternal genome (Santos et al., 2005). The asymmetry in H3K9me3 has functional consequences: maternal H3K9me3 serves as a binding platform for STELLA (also known as PGC7/DPPA3), which protects the maternal genome from TET3-mediated active demethylation, ensuring that imprinted loci retain their methylation through the global reprogramming event (Nakamura et al., 2007).

### 2.2 Pioneer Transcription Factors: Redundancy as a Design Principle

The identification of the transcription factors that ignite ZGA has been a central quest in developmental biology. Between 2017 and 2024, a series of discoveries revealed that multiple pioneer factors — proteins capable of binding nucleosomal DNA and initiating chromatin opening — converge on ZGA activation, establishing a redundant regulatory architecture of remarkable robustness.

**DUX/DUX4.** Three independent studies published simultaneously in 2017 identified the double homeodomain transcription factor DUX (mouse) / DUX4 (human) as a key activator of cleavage-stage genes. De Iaco and colleagues showed that DUX4 expression in human embryonic stem cells activates a transcriptional program characteristic of the cleavage stage, including endogenous retroviral elements (De Iaco et al., 2017). Hendrickson and colleagues demonstrated conserved roles for mouse DUX and human DUX4 in activating both cleavage-stage genes and MERVL/HERVL retrotransposons, showing that DUX expression is sufficient to convert ESCs to a 2C-like state (Hendrickson et al., 2017). However, a critical finding came from Chen and Zhang (2019), who demonstrated that genetic deletion of the entire Dux cluster in mice causes only minor defects in ZGA and is fully compatible with mouse development and fertility. This established that DUX is **sufficient but not necessary** for ZGA — a pattern that would prove characteristic of ZGA pioneer factors generally (Chen & Zhang, 2019). Recent work has shown that the redundancy is structurally encoded: Dux exists as a tandem gene cluster, and the duplication itself ensures robust activation of the totipotent transcriptional program, with cluster expansion correlating with full 2C gene activation across species (Asimi et al., 2025).

**OBOX.** Ji and colleagues (2023) identified the OBOX family of PRD-like homeobox transcription factors as key regulators of mouse ZGA. Mice deficient for maternally transcribed Obox1/2/5/7 and zygotically expressed Obox3/4 exhibited 2-cell to 4-cell arrest accompanied by impaired ZGA (Ji et al., 2023). Mechanistically, OBOX facilitated the pre-configuration of RNA polymerase II, relocating it from initial 1-cell binding targets to ZGA gene promoters and distal enhancers (Ji et al., 2023). Importantly, Obox4 can promote ZGA even in the absence of Dux, establishing OBOX as a parallel, DUX-independent activation pathway (Sakamoto et al., 2024).

**NR5A2.** The orphan nuclear receptor NR5A2 was identified as a totipotency pioneer factor through de novo motif analysis of accessible chromatin at the 2-cell stage (Gassler et al., 2022). NR5A2 binds its motif within SINE B1/Alu retrotransposable elements that are enriched in cis-regulatory regions of ZGA genes (Gassler et al., 2022). Cryo-electron microscopy revealed the structural basis of NR5A2 pioneer activity: the C-terminal extension loop of the NR5A2 DNA-binding domain competes with a DNA minor groove anchor of the nucleosome, releasing entry-exit site DNA and enabling chromatin opening (Kobayashi et al., 2024). However, Festuccia and colleagues (2024) demonstrated that Nr5a2-null embryos still undergo ZGA, albeit with minor quantitative defects. Nr5a2 instead proved essential at the 8-cell (morula) stage, where it controls expression of lineage-specifying transcription factors and genes required for mitosis, telomere maintenance, and DNA repair (Festuccia et al., 2024). This finding repositioned NR5A2 from a ZGA activator to a post-ZGA master regulator of the morula-stage transcriptional program.

**DPPA2/DPPA4.** The developmental pluripotency-associated proteins DPPA2 and DPPA4 function as chromatin licensing factors that directly regulate the Dux-driven transcriptional program (Eckersley-Maslin et al., 2019). DPPA2/4 are maternally deposited and bind to ZGA gene promoters prior to DUX expression, suggesting they act as permissive factors that render chromatin competent for subsequent pioneer factor binding (Eckersley-Maslin et al., 2019).

The collective implication of these findings is that ZGA is not controlled by a single master regulator but by a **redundant network of pioneer factors** with overlapping but non-identical target gene sets. No single factor is indispensable — DUX knockout, Nr5a2 knockout, and individual OBOX family member deletions each cause surprisingly modest ZGA defects — yet the combined activity of the network ensures robust, reliable genome activation. This architecture represents a fundamental design principle: the most critical developmental transition in the mammalian life cycle — the switch from maternal to zygotic control — is protected by functional redundancy that buffers against stochastic variation in individual factor expression.

### 2.3 Three-Dimensional Genome Reorganization

The three-dimensional organization of the genome undergoes dramatic restructuring during the transition from gametes to the totipotent embryo. Four seminal Hi-C studies in 2017 revealed that topologically associating domains (TADs), the fundamental units of chromatin folding that organize the genome into self-interacting neighborhoods, are profoundly attenuated in mature gametes and are gradually re-established during pre-implantation development (Du et al., 2017; Flyamer et al., 2017; Gassler et al., 2017; Ke et al., 2017).

In oocytes, TADs are detectable but weak, while in sperm — where the genome is compacted with protamines — higher-order chromatin organization is largely absent (Ke et al., 2017). After fertilization, the paternal pronucleus initially lacks TAD structure but acquires it progressively during the first cell cycle, while maternal TADs strengthen (Du et al., 2017). Despite their epigenetic asymmetry, the maternal and paternal genomes achieve remarkably similar TAD landscapes by the late 2-cell stage (Du et al., 2017; Flyamer et al., 2017). Critically, the establishment of TADs does not depend on transcription — inhibition of RNA polymerase II does not prevent TAD formation — indicating that structural organization precedes and is independent of transcriptional activation (Du et al., 2017; Ke et al., 2017).

The architectural proteins CTCF and cohesin, which mediate chromatin loop extrusion and define TAD boundaries in somatic cells, show dynamic binding patterns during early development. Yu and colleagues (2025) demonstrated using CUT&Tag profiling that cohesin binds chromatin poorly in 1-cell embryos but progressively increases its binding from the 2-cell to 8-cell stages, concomitant with TAD establishment. Strikingly, strong "genic cohesin islands" (GCIs) emerge across the gene bodies of actively transcribed genes during this period, and transcription is required for GCI formation (Yu et al., 2025). GCIs function as insulation boundaries that enhance both transcription levels and transcriptional stability, revealing a positive feedback loop between transcription and chromatin architecture that reinforces the ZGA program (Yu et al., 2025). This finding challenges the prevailing view that chromatin architecture is established independently of transcription and suggests that ZGA and 3D genome organization are mutually reinforcing processes.

---

## 3. Zygotic Genome Activation: From Silence to Symphony

### 3.1 The Two-Wave Architecture of ZGA

ZGA proceeds through two distinct transcriptional waves that are conserved across mammals but differ in their timing. **Minor ZGA** involves the low-level transcription of a subset of genes, occurring at the 1-cell (late zygote) stage in mouse and the 4-cell stage in humans (Schulz & Harrison, 2019). **Major ZGA** represents the dramatic, genome-wide burst of transcriptional activation that occurs at the 2-cell stage in mouse and the 8-cell stage in humans (Braude et al., 1988; Schulz & Harrison, 2019). The species-specific timing of major ZGA correlates with the number of cell divisions required: mouse embryos undergo ZGA after just one division (1-cell → 2-cell), while human embryos require three divisions (1-cell → 8-cell), suggesting a counting mechanism linked to cell cycle progression or dilution of maternal factors (Jukam, Shariati, & Skotheim, 2017).

The onset of ZGA is tightly coordinated with the clearance of maternally deposited mRNAs, a process termed **maternal mRNA decay**. In mice, the RNA-binding protein ZFP36L2 promotes deadenylation and degradation of a large cohort of maternal transcripts at the 2-cell stage, and its deletion causes embryonic arrest at the 2-cell to 4-cell transition (Dumdie et al., 2018). The BTG4 protein, a member of the anti-proliferative BTG/TOB family, similarly promotes maternal mRNA deadenylation by recruiting the CCR4-NOT deadenylase complex, and Btg4-null embryos arrest at the 1-cell to 2-cell stage due to failure to clear maternal transcripts (Yu et al., 2016). Terminal uridylyltransferases TUT4 and TUT7 add oligo-U tails to maternal mRNAs, marking them for degradation by the exonuclease DIS3L2, providing an additional layer of maternal transcript clearance (Morgan et al., 2017). The coordination between maternal decay and zygotic activation ensures a smooth handoff of transcriptional control from maternal to embryonic programs.

The species-specific timing of ZGA has important implications for assisted reproduction. In human embryos, the extended period between fertilization and major ZGA (approximately three cell divisions over 2–3 days) means that early embryonic development is entirely dependent on maternally provided factors — a vulnerability that explains why oocyte quality is the strongest predictor of IVF success (Vassena et al., 2011). The recent demonstration that single-cell chromatin profiling using the TACIT method can resolve heterogeneities in histone modifications as early as the 2-cell stage suggests that the seeds of ZGA success or failure may be sown far earlier than previously appreciated, with implications for embryo quality assessment (Yu et al., 2025).

### 3.2 Retrotransposon Co-option as Regulatory Innovation

One of the most remarkable discoveries in ZGA biology has been the revelation that endogenous retroviral elements (ERVs) — remnants of ancient retroviral integrations that constitute approximately 8–10% of mammalian genomes — serve as critical regulatory elements during the totipotent state.

Macfarlan and colleagues (2012) identified a rare, transient population of cells within mouse ESC cultures that express high levels of transcripts characteristic of 2-cell embryos. These "2C-like cells" lacked the pluripotency factors OCT4, SOX2, and NANOG and had acquired the capacity to contribute to both embryonic and extraembryonic tissues — a functional hallmark of totipotency (Macfarlan et al., 2012). Transcriptome analysis revealed that many 2C-specific transcripts are initiated from long terminal repeats (LTRs) of the **murine endogenous retrovirus-L (MERVL)** family, establishing a direct link between retrotransposon activation and the totipotent state (Macfarlan et al., 2012). Subsequent work demonstrated that full-length MERVL transcription is not merely a marker of the 2C state but is functionally required: genetic deletion of MERVL regulatory elements impaired pre-implantation development, and MERVL LTRs serve as alternative promoters for ZGA genes, creating a chimeric transcriptome that is unique to the totipotent stage (Sakashita et al., 2023).

In human embryos, the equivalent retroviral family **HERVK (HML-2)** is reactivated during ZGA, with HERVK transcripts and even viral proteins detectable in cleavage-stage embryos and human blastocysts (Grow et al., 2015). HERVK LTRs function as tissue-specific enhancers that drive expression of nearby genes during early development, and the viral Rec protein interacts with ribosomal RNA processing factors, suggesting a functional role beyond simple cis-regulation (Grow et al., 2015).

Beyond ERVs, the non-LTR retrotransposon **LINE-1 (L1)**, which constitutes approximately 17% of the mouse genome, plays an unexpected role in chromatin regulation during ZGA. Jachowicz and colleagues (2017) demonstrated that LINE-1 transcription after fertilization is required for global chromatin accessibility in the early mouse embryo. Antisense oligonucleotide-mediated silencing of LINE-1 RNA reduced chromatin accessibility at ZGA gene promoters and caused developmental arrest, establishing LINE-1 as a chromatin remodeling factor rather than merely a parasitic element (Jachowicz et al., 2017). Percharde and colleagues (2018) extended this finding by showing that LINE-1 RNA forms a complex with the nucleolar protein nucleolin and the transcriptional repressor KAP1 (TRIM28), and that this LINE-1-nucleolin partnership is required for rRNA synthesis and ESC self-renewal (Percharde et al., 2018).

The co-option of retrotransposons as ZGA regulatory elements represents a striking example of evolutionary exaptation — the repurposing of selfish genetic elements for host developmental functions. The KRAB-zinc finger protein (KRAB-ZFP) family, which expanded dramatically in mammals through gene duplication and diversification, provides a counterbalancing silencing mechanism that restricts retrotransposon activity to the appropriate developmental window (Yang, Wolf, & Macfarlan, 2017). ZFP352, for example, selectively binds specific retrotransposon subfamilies and facilitates the timely dissolution of the totipotency network by the 4-cell stage, ensuring that the 2C program is properly terminated (Wang et al., 2023). This KRAB-ZFP–retrotransposon arms race has shaped the species-specific regulatory landscape of ZGA, with different mammalian lineages co-opting different retrotransposon families as regulatory elements (Eckersley-Maslin, Alda-Catalinas, & Reik, 2018).

### 3.3 Phase Separation and Biomolecular Condensates in ZGA

Biomolecular condensates — membrane-less compartments formed through liquid-liquid phase separation (LLPS) of proteins and nucleic acids — have emerged as organizing principles for transcriptional activation, and recent evidence implicates them in the regulation of ZGA.

During major ZGA, transcription factors must transition from a dispersed nuclear state to concentrated hubs of activity at target gene promoters. The formation of transcriptional condensates — phase-separated droplets enriched in RNA polymerase II, Mediator complex, and transcription factors — is thought to concentrate the transcriptional machinery at ZGA gene clusters, enabling the burst-like activation kinetics observed during major ZGA (Guo et al., 2017). The pioneer factor NR5A2 connects this transcriptional hub model to ZGA: NR5A2 binds nucleosomal DNA through its conserved C-terminal extension loop, which competes with the DNA minor groove anchor of the nucleosome to release entry-exit DNA and create accessible chromatin (Kobayashi et al., 2024). This structural opening mechanism may facilitate the recruitment of additional transcriptional machinery components. Importantly, the NR5A2 binding sites at SINE B1 elements are themselves clustered in the genome, suggesting that the spatial proximity of NR5A2 targets could nucleate condensate-like transcriptional hubs that amplify the ZGA signal at specific genomic neighborhoods (Gassler et al., 2022; Guo et al., 2024).

Nucleolar precursor bodies (NPBs), large spherical structures that are prominent features of pronuclei in the zygote and early cleavage-stage embryo, represent another condensate-mediated regulatory mechanism. NPBs lack the tripartite architecture of mature nucleoli and do not support rRNA transcription until the 2-cell stage in mice (Flechon & Kopecny, 1998). Recent work has shown that NPBs sequester and organize heterochromatin, including pericentromeric satellite DNA, and that their dissolution during ZGA coincides with the redistribution of heterochromatin to form chromocenters — a transition that is essential for genomic stability in the early embryo (Ogushi et al., 2017).

P-bodies — cytoplasmic condensates enriched in mRNA decay factors — play a complementary role in ZGA by mediating the degradation of maternal mRNAs. The coordinated dissolution of P-bodies during the MZT releases sequestered decay factors, accelerating maternal transcript clearance and facilitating the handoff to zygotic transcription (Luo, Na, & Bhatt, 2018). The interplay between nuclear transcriptional condensates (activating ZGA) and cytoplasmic P-bodies (clearing maternal mRNAs) provides a condensate-level coordination mechanism for the maternal-to-zygotic transition.

### 3.4 Novel Quantitative Frameworks for ZGA Dynamics

#### Novel Mathematical Framework F_A: Multi-State Chromatin Continuous-Time Markov Chain

The transition of individual genomic loci from a silent to an active transcriptional state during ZGA can be modeled as a continuous-time Markov chain (CTMC) on a three-state space representing the chromatin configurations observed during ZGA: closed (heterochromatic, H3K9me3-marked), poised (accessible but not transcribed, H3K4me1-marked), and active (transcribed, H3K4me3-marked).

For a single locus, define the state space $S = \{0, 1, 2\}$ corresponding to closed, poised, and active states, respectively. The generator matrix $\mathbf{Q}$ governing transitions depends on the local concentration of pioneer factors $[PF]$:

```math
\mathbf{Q}([PF]) = \begin{pmatrix} -(q_{01} + q_{02}) & q_{01} & q_{02} \\ q_{10} & -(q_{10} + q_{12}) & q_{12} \\ q_{20} & q_{21} & -(q_{20} + q_{21}) \end{pmatrix}
```

where the key pioneer factor-dependent transition rate is:

```math
q_{01}([PF]) = q_{01}^{(0)} + \frac{q_{01}^{(\max)} \cdot [PF]^n}{K_d^n + [PF]^n}
```

where:
- $q_{01}^{(0)}$ is the basal chromatin opening rate in the absence of pioneer factors
- $q_{01}^{(\max)}$ is the maximal pioneer factor-stimulated opening rate
- $K_d$ is the half-maximal pioneer factor concentration for chromatin opening
- $n$ is the Hill coefficient reflecting cooperative binding (typically $n \approx 2$ for homodimeric pioneer factors such as NR5A2)
- $q_{02} \approx 0$ (direct closed-to-active transitions are negligible)
- $q_{12} = q_{12}^{(0)}$ is the Pol II recruitment rate at poised loci
- $q_{10} = q_{10}^{(0)} \cdot e^{-\beta [PF]}$ captures pioneer factor-mediated prevention of chromatin re-closing
- $q_{20}$ and $q_{21}$ represent transcriptional termination rates

The stationary distribution $\boldsymbol{\pi} = (\pi_0, \pi_1, \pi_2)$ satisfying $\boldsymbol{\pi} \mathbf{Q} = \mathbf{0}$ gives the equilibrium fraction of loci in each state. The fraction of active loci at steady state is:

```math
\pi_2([PF]) = \frac{q_{01} \cdot q_{12}}{q_{01} \cdot q_{12} + q_{01} \cdot q_{21} + q_{10} \cdot q_{21} + q_{10} \cdot q_{20} + q_{12} \cdot q_{20}}
```

For $N$ independent loci, the expected fraction of active loci at time $t$ is $f_{\text{active}}(t) = N^{-1} \sum_{i=1}^{N} P(X_i(t) = 2)$, where each $X_i(t)$ evolves according to the Kolmogorov forward equation $\frac{d\mathbf{P}}{dt} = \mathbf{P} \cdot \mathbf{Q}$. ZGA can be defined as the time $\tau_{\text{ZGA}}$ at which $f_{\text{active}}$ first exceeds a threshold fraction $f^*$. For biologically plausible parameters ($q_{01}^{(\max)} \approx 0.5 \text{ h}^{-1}$, $K_d \approx 100 \text{ nM}$, $q_{12} \approx 0.3 \text{ h}^{-1}$), the model predicts $\tau_{\text{ZGA}} \approx 6$–$12$ hours after pioneer factor accumulation exceeds $K_d$, consistent with the observed timing of major ZGA relative to the onset of zygotic transcription factor expression.

#### Novel Mathematical Framework F_B: ZGA as a Nucleation-Growth Phase Transition

The abrupt, switch-like character of major ZGA — in which thousands of genes transition from silence to robust transcription within a single cell cycle — bears the hallmarks of a first-order phase transition. We model ZGA using classical nucleation theory, treating the formation of transcriptionally active chromatin domains as a nucleation event within a metastable silent genome.

Consider a cluster of $n$ co-activated genomic loci within a transcriptional hub. The free energy change associated with forming an active cluster of size $n$ within an otherwise silent genome is:

```math
\Delta G(n) = -n \cdot \Delta\mu + \sigma \cdot n^{2/3}
```

where:
- $\Delta\mu > 0$ is the free energy gain per activated locus, reflecting the thermodynamic favorability of the active state once pioneer factors are present (proportional to pioneer factor concentration and Pol II availability)
- $\sigma > 0$ is the surface tension between active and silent chromatin domains, representing the energetic cost of maintaining a boundary between permissive (H3K4me3) and repressive (H3K9me3) chromatin states
- The $n^{2/3}$ scaling reflects the surface-to-volume ratio of the cluster in three-dimensional nuclear space

The free energy barrier is maximized at the critical nucleus size:

```math
n^* = \left(\frac{2\sigma}{3\Delta\mu}\right)^3
```

and the height of the nucleation barrier is:

```math
\Delta G^* = \Delta G(n^*) = \frac{4\sigma^3}{27\Delta\mu^2}
```

The nucleation rate — the rate at which transcriptional activation initiates — follows Arrhenius kinetics:

```math
J = J_0 \cdot \exp\left(-\frac{\Delta G^*}{k_B T_{\text{eff}}}\right) = J_0 \cdot \exp\left(-\frac{4\sigma^3}{27\Delta\mu^2 \cdot k_B T_{\text{eff}}}\right)
```

where $T_{\text{eff}}$ is an effective temperature reflecting the level of stochastic transcriptional noise (thermal and active fluctuations in the nucleus), and $J_0$ is the attempt frequency related to the rate of transcription factor-chromatin encounters. As pioneer factors accumulate during the first cell cycle, $\Delta\mu$ increases, reducing the nucleation barrier and eventually triggering the burst of genome-wide activation. The stochastic nature of nucleation explains the observed cell-to-cell variability in ZGA timing between sister blastomeres: cells that stochastically form a critical nucleus earlier will activate ZGA sooner, while those requiring more time for nucleation will activate later.

#### Novel Mathematical Framework F_C: Stochastic ZGA Timing via Order Statistics

The variability in ZGA timing among individual blastomeres can be quantified using order statistics. Suppose that ZGA requires the activation of at least $k$ out of $N$ essential genes, where each gene activates independently as a Poisson process with rate $\lambda_i$. The activation time of gene $i$ is an exponential random variable $T_i \sim \text{Exp}(\lambda_i)$.

For the case of homogeneous rates ($\lambda_i = \lambda$ for all $i$), the time to activate the $k$-th gene is the $k$-th order statistic $T_{(k:N)}$. Its expected value is:

```math
E[T_{(k:N)}] = \frac{1}{\lambda} \sum_{j=0}^{k-1} \frac{1}{N - j} = \frac{1}{\lambda} \left(\frac{1}{N} + \frac{1}{N-1} + \cdots + \frac{1}{N-k+1}\right)
```

The variance of ZGA timing is:

```math
\text{Var}[T_{(k:N)}] = \frac{1}{\lambda^2} \sum_{j=0}^{k-1} \frac{1}{(N-j)^2}
```

The coefficient of variation (CV) of ZGA timing provides a measure of inter-blastomere variability:

```math
\text{CV} = \frac{\sqrt{\text{Var}[T_{(k:N)}]}}{E[T_{(k:N)}]} = \frac{\sqrt{\sum_{j=0}^{k-1} (N-j)^{-2}}}{\sum_{j=0}^{k-1} (N-j)^{-1}}
```

For biologically relevant parameters ($N \approx 500$ essential ZGA genes, $k \approx 400$ required for successful ZGA), the CV is approximately 0.05–0.10, consistent with the observed variation in ZGA timing between sister blastomeres detected by single-cell transcriptomic profiling of cleavage-stage embryos (Guo et al., 2017). As $k/N$ increases toward 1 (more genes required), the CV increases, predicting that organisms requiring a higher fraction of ZGA genes for developmental competence will show greater inter-embryo variability in developmental timing — a prediction testable across species with different ZGA gene complements. Conversely, the model predicts that redundancy among pioneer factors (Section 2.2) effectively increases $\lambda$ (the per-gene activation rate) by ensuring that chromatin opening occurs regardless of which specific pioneer factor acts first, thereby reducing inter-blastomere variation and increasing developmental robustness.

The three quantitative frameworks developed above — chromatin CTMC, nucleation-growth, and order statistics — provide complementary lenses for understanding ZGA dynamics. The CTMC model captures the molecular-level mechanism of how individual loci transition through chromatin states in response to pioneer factor accumulation. The nucleation-growth model explains the macroscopic observation that ZGA is switch-like rather than gradual, with a sharp transition occurring once pioneer factor levels reduce the nucleation barrier below a critical threshold. The order statistics framework quantifies the inter-blastomere variability that arises from the inherently stochastic nature of gene activation, connecting molecular-level randomness to the population-level variation observed in embryonic development. Together, these frameworks generate experimentally testable predictions: the CTMC predicts that chromatin opening rates should increase sigmoidally with pioneer factor concentration, the nucleation model predicts that ZGA timing should decrease as the inverse square of pioneer factor concentration (through the $\Delta\mu$ dependence), and the order statistics model predicts that ZGA timing variance should scale inversely with gene activation rate.

---

## 4. Totipotency in a Dish: Stem Cell-Derived Embryo Models

### 4.1 Blastoids and the Self-Organization Principle

The demonstration that stem cells can self-organize into structures resembling pre-implantation embryos has transformed the study of early development. Rivron and colleagues (2018) reported the first generation of mouse **blastoids** — blastocyst-like structures formed from trophoblast stem cells (TSCs) and ESCs cultured in three-dimensional conditions. These blastoids recapitulated the morphology and cell-type composition of natural blastocysts, with an outer trophectoderm-like layer enclosing an inner cell mass-like compartment, and could implant into the uterus and initiate decidualization (Rivron et al., 2018).

The extension to human blastoids represented a critical advance. Yu and colleagues (2021) demonstrated that human naive pluripotent stem cells, when cultured with inhibitors of the Hippo, TGF-β, and ERK pathways, efficiently form blastocyst-like structures with trophectoderm, epiblast, and primitive endoderm lineages (Yu et al., 2021). Kagawa and colleagues (2022) achieved human blastoid formation with high efficiency using naive human ESCs and a defined chemical cocktail, showing that these structures recapitulate the transcriptomic profiles and implantation behavior of natural blastocysts (Kagawa et al., 2022). Recent optimization has produced 4CL (four-chemical plus LIF) blastoids that closely match natural human blastocysts in DNA methylation patterns and, when cultured for 14 days, mimic early gastrulation with cell specification and directed migration (Kim et al., 2024).

A conceptual breakthrough has been the realization that single totipotent-like cells can generate blastoid structures autonomously. Mouse totipotent blastomere-like cells (TBLCs) derived through extended culture of 2C-like cells efficiently form blastoids from single cells and can develop through implantation to form post-implantation egg-cylinder-like structures, demonstrating that single totipotent cells contain sufficient information for self-organized embryogenesis through the peri-implantation period (Xu et al., 2024). Most recently, chemically induced continuous totipotent-like cells have been shown to recapitulate mouse embryogenesis from ZGA through gastrulation entirely in vitro, providing the first continuous cell-based model spanning the complete pre-gastrulation developmental program (Zhang et al., 2025).

### 4.2 Extended Embryo Models and Regulatory Frameworks

Beyond blastocyst-stage models, **gastruloids** — aggregates of ESCs that undergo symmetry breaking and axial elongation — have enabled the study of post-implantation morphogenesis in vitro. When treated with a pulse of the Wnt agonist CHIR99021, mouse ESC aggregates break symmetry and elongate, forming structures with anterior-posterior polarity, somite-like segmentation, and multi-axial patterning (Beccari et al., 2018). Gastruloids have since been extended to recapitulate cardiogenesis, somitogenesis, and neural tube formation, providing accessible models for studying organogenesis without the ethical constraints of human embryo research (Rossi et al., 2021; van den Brink et al., 2020).

The generation of complete synthetic embryo models was achieved by Amadei and colleagues (2022), who combined mouse ESCs, TSCs, and extraembryonic endoderm (XEN) cells to create **ETiX embryoids** that completed gastrulation, formed neural folds, and initiated organogenesis, reaching a developmental stage equivalent to approximately embryonic day 8.5 (Amadei et al., 2022). Independently, Tarazi and colleagues (2022) generated post-gastrulation synthetic embryos from naive ESCs alone, relying on the differentiation capacity of naive cells to generate all three embryonic compartments (Tarazi et al., 2022). Extension to primate models has been achieved: stem cell-derived monkey embryoids have been cultured to day 25, recapitulating gastrulation and generating identifiable neural plate, hematopoietic system, allantois, gut, and primordial germ cells (Li et al., 2025).

These advances have prompted significant ethical and regulatory discussion. The International Society for Stem Cell Research (ISSCR) updated its guidelines to address stem cell-derived embryo models, recommending that such models be subject to specialized review but not subject to the 14-day rule that governs natural human embryo research, provided they lack the full developmental potential of natural embryos (Lovell-Badge et al., 2021). The distinction between models that recapitulate specific developmental events and those that achieve integrated embryo-like development remains a subject of active debate, with implications for research governance worldwide (Hyun et al., 2021).

### 4.3 Mathematical Framework: Turing Instability for Morphogen-Driven Self-Organization

#### Novel Mathematical Framework F_D: Reaction-Diffusion Analysis of BMP-Nodal Patterning in Blastoids

The spontaneous symmetry breaking observed in blastoids and gastruloids can be analyzed through the lens of Turing's reaction-diffusion theory. In a blastoid, the interplay between BMP4 (acting as a short-range activator) and its antagonist Nodal/Lefty (acting as a long-range inhibitor) generates the spatial patterns that specify trophectoderm versus inner cell mass fates.

Consider a two-component reaction-diffusion system on a spherical domain of radius $R$ (the blastoid):

```math
\frac{\partial u}{\partial t} = D_u \nabla^2 u + f(u, v)
```

```math
\frac{\partial v}{\partial t} = D_v \nabla^2 v + g(u, v)
```

where $u(\mathbf{x}, t)$ is the activator (BMP4) concentration, $v(\mathbf{x}, t)$ is the inhibitor (Nodal/Lefty) concentration, $D_u$ and $D_v$ are their respective diffusion coefficients, and $f, g$ describe the local reaction kinetics. Using Schnakenberg kinetics:

```math
f(u, v) = a - u + u^2 v, \quad g(u, v) = b - u^2 v
```

where $a$ and $b$ are synthesis rate parameters. The homogeneous steady state is $(u_0, v_0) = (a + b, \, b/(a+b)^2)$.

The conditions for Turing instability — diffusion-driven pattern formation from a stable homogeneous state — require:

```math
\text{(i)} \quad f_u + g_v < 0, \quad \text{(ii)} \quad f_u g_v - f_v g_u > 0
```

```math
\text{(iii)} \quad D_v f_u + D_u g_v > 0, \quad \text{(iv)} \quad (D_v f_u + D_u g_v)^2 > 4 D_u D_v (f_u g_v - f_v g_u)
```

Conditions (i)–(ii) ensure stability without diffusion; conditions (iii)–(iv) ensure that diffusion destabilizes the homogeneous state. These conditions are satisfied when $D_v / D_u \gg 1$ — the inhibitor diffuses much faster than the activator — which is consistent with the known properties of BMP4 (membrane-associated, slow diffusion) and Lefty (secreted, fast diffusion) (Muller et al., 2012).

The critical wavenumber for the most unstable spatial mode is:

```math
k_c^2 = \sqrt{\frac{f_u g_v - f_v g_u}{D_u D_v}}
```

The corresponding pattern wavelength is $\lambda = 2\pi / k_c$, which predicts the spatial scale of symmetry breaking. For a spherical blastoid of radius $R \approx 75 \, \mu\text{m}$, with $D_u \approx 1 \, \mu\text{m}^2/\text{s}$ (BMP4) and $D_v \approx 30 \, \mu\text{m}^2/\text{s}$ (Lefty), the predicted dominant mode is $l = 1$ (a single pole of high BMP4), consistent with the single axis of symmetry breaking observed experimentally in blastoids. Higher-order modes ($l \geq 2$) are suppressed when $R < 2\pi/k_c$, explaining why small blastoids form a single trophectoderm domain rather than multiple patches — the geometry constrains the patterning to the simplest mode.

---

## 5. Reconstituting the Totipotent Program: In Vitro Gametogenesis

### 5.1 From iPSCs to Gametes: Progress and Barriers

In vitro gametogenesis (IVG) — the derivation of functional gametes from pluripotent stem cells — represents the ultimate functional test of whether the totipotent program can be reconstituted. The roadmap for IVG was established by Hayashi and colleagues, who achieved complete mouse oogenesis from iPSCs through a multi-step protocol: iPSC differentiation to epiblast-like cells (EpiLCs), induction of primordial germ cell-like cells (PGCLCs), aggregation with embryonic ovarian somatic cells to form reconstituted ovaries, and in vitro growth and maturation to produce fully grown oocytes capable of fertilization and generation of fertile offspring (Hayashi et al., 2012; Hayashi & Saitou, 2013).

The extension to human IVG has proceeded more slowly, reflecting the longer developmental timeline and species-specific differences in germ cell specification. Irie and colleagues (2015) identified SOX17, rather than the mouse factor BLIMP1/PRDM1, as the critical specifier of human PGC fate, and demonstrated efficient induction of human PGCLCs from iPSCs (Irie et al., 2015). Sasaki and colleagues (2015) independently developed robust protocols for human PGCLC induction and showed that these cells recapitulate the transcriptional and epigenetic features of in vivo PGCs (Sasaki et al., 2015). Murase and colleagues (2024) achieved a major milestone by reconstituting epigenetic reprogramming of the human germ line in vitro, demonstrating that human PGCLCs undergo genome-wide DNA demethylation and imprint erasure when co-cultured with human fetal ovarian somatic cells (Murase et al., 2024).

The principal barrier to complete human IVG remains the induction of meiotic entry and oocyte maturation. While mouse PGCLCs can be guided through meiosis using reconstituted ovary culture, human PGCLCs have proven resistant to meiotic entry under equivalent conditions, likely due to species-specific requirements for the meiotic niche that are not fully recapitulated in current culture systems (Saitou & Hayashi, 2021). A proof-of-concept approach using somatic cell nuclear transfer rather than iPSC differentiation was reported by Mitalipov and colleagues (2025), who demonstrated "mitomeiosis" — the induction of a meiosis-like reductive division in somatic cell nuclei transplanted into enucleated oocytes — to generate cells with reduced ploidy (Mitalipov et al., 2025). While this approach is distinct from canonical IVG, it demonstrates the feasibility of generating haploid cells from somatic tissue and may provide insights into the minimum molecular requirements for meiotic-like chromosome segregation.

### 5.2 Epigenetic Fidelity: The Quality Control Challenge

A critical open question for IVG is whether in vitro-derived gametes faithfully recapitulate the epigenetic landscape of natural gametes. Natural gametogenesis involves a carefully orchestrated sequence of genome-wide DNA demethylation, de novo methylation, and establishment of sex-specific imprints that requires years in humans (Sasaki & Matsui, 2008). Errors in this process — aberrant retention of somatic methylation patterns, incomplete imprint establishment, or failure to properly silence retrotransposons — could result in developmental defects in offspring derived from IVG-produced gametes.

#### Novel Mathematical Framework F_E: Kullback-Leibler Divergence for Epigenetic Fidelity

The epigenetic fidelity of IVG-derived gametes can be quantified using information-theoretic measures. For a set of $C$ CpG sites measured by whole-genome bisulfite sequencing, let $p_i$ denote the methylation probability at site $i$ in natural gametes and $q_i$ denote the corresponding methylation probability in IVG-derived gametes. The Kullback-Leibler (KL) divergence per CpG site provides a measure of epigenetic deviation:

```math
D_{KL}(P \| Q) = \frac{1}{C} \sum_{i=1}^{C} \left[ p_i \ln\frac{p_i}{q_i} + (1 - p_i) \ln\frac{1 - p_i}{1 - q_i} \right]
```

where each CpG is treated as a Bernoulli random variable with methylation probability $p_i$ (natural) or $q_i$ (IVG).

A global fidelity metric can be defined as:

```math
\mathcal{F} = \exp\left(-C \cdot D_{KL}(P \| Q)\right)
```

where $\mathcal{F} = 1$ indicates perfect epigenetic fidelity ($D_{KL} = 0$, identical methylomes) and $\mathcal{F} \to 0$ indicates severe epigenetic divergence. This metric has the interpretation that $-\ln \mathcal{F} = C \cdot D_{KL}$ gives the total information loss (in nats) across the methylome.

For practical assessment, the per-locus fidelity can be decomposed by genomic feature:

```math
D_{KL}^{(\text{feature})} = \frac{1}{|\mathcal{C}_f|} \sum_{i \in \mathcal{C}_f} \left[ p_i \ln\frac{p_i}{q_i} + (1 - p_i) \ln\frac{1 - p_i}{1 - q_i} \right]
```

where $\mathcal{C}_f$ denotes the set of CpG sites within genomic feature $f$ (e.g., imprinting control regions, promoters, gene bodies, retrotransposons). This decomposition allows identification of specific genomic regions where IVG-derived gametes deviate most from natural gametes. Published data from mouse IVG experiments suggest that imprinting control regions ($D_{KL}^{(\text{ICR})} \approx 0.15$–$0.3$ nats per CpG) and retrotransposon silencing marks ($D_{KL}^{(\text{TE})} \approx 0.08$–$0.15$) show the largest deviations, while CpG islands at promoters are generally well-recapitulated ($D_{KL}^{(\text{CGI})} < 0.05$) (Ohta et al., 2017). Human IVG epigenetic fidelity data remain limited but will be critical for evaluating the clinical safety of IVG-derived gametes.

---

## 6. Open Questions and Future Directions

### 6.1 The Human Totipotency Program

A central unresolved question is the extent to which mouse ZGA mechanisms are conserved in humans. While DUX4 is the human ortholog of mouse Dux, human ZGA occurs at the 8-cell stage rather than the 2-cell stage, and the specific retrotransposon families co-opted for regulatory functions differ between species (HERVK in humans vs. MERVL in mice) (Grow et al., 2015; Macfarlan et al., 2012). The recent discovery that spliceosomal repression can capture a totipotent-like state in human cells — generating human totipotent blastomere-like cells (hTBLCs) that recapitulate pre-implantation development and form blastoids autonomously — provides a transformative tool for studying human-specific totipotency mechanisms (Li et al., 2024). hTBLCs activate ZGA-specific genes including 8-cell-stage markers and pre-ZGA transcripts, offering a tractable in vitro system for dissecting the human ZGA program without reliance on human embryos.

### 6.2 From Redundancy to Reconstitution

The emerging picture of ZGA as a redundantly controlled process raises a practical challenge: if no single factor is essential for ZGA, how can the totipotent program be efficiently reconstituted in non-embryonic contexts? The answer may lie in the combinatorial logic of pioneer factor activity. While individual factor knockouts show mild phenotypes, combinatorial deletions — simultaneous loss of DUX, OBOX, and NR5A2 — may reveal synergistic requirements that define the minimal totipotency circuit. Such experiments are technically challenging but would provide foundational insight into the logic gates governing totipotency.

The 2C-like cell system discovered by Macfarlan and colleagues (2012) provides a tractable in vitro model for these combinatorial studies. 2C-like cells spontaneously arise in ESC cultures at a frequency of approximately 0.5–1% and can be isolated using MERVL-driven reporters. These cells express the totipotency-associated transcriptional program, lack canonical pluripotency factors, and can contribute to both embryonic and extraembryonic lineages — properties that make them functional proxies for the totipotent state. Recent chemical approaches have extended this toolkit: the continuous totipotent-like cells generated by Zhang and colleagues (2025) through chemical cocktail treatment maintain a stable totipotent-like state indefinitely, overcoming the transient nature of spontaneous 2C-like cells and enabling long-term studies of the totipotent program.

The exit from totipotency is equally important and less understood. The homeobox transcription factor DUXBL has been identified as a controller of the totipotency-to-pluripotency transition in mice, with DUXBL loss extending the 2C-like state and delaying lineage commitment (Vamadevan et al., 2024). Understanding the molecular switches that terminate totipotency may prove as important as understanding its establishment, particularly for the safety assessment of IVG-derived gametes and synthetic embryo models. A key open question is whether the totipotent-to-pluripotent transition is an irreversible commitment event analogous to a first-order phase transition, or whether cells retain latent totipotent potential that can be reactivated under appropriate conditions — a question with direct implications for the fidelity and safety of reprogramming approaches.

### 6.3 Clinical Translation

The convergence of ZGA biology, synthetic embryo models, and IVG opens several translational avenues. First, molecular markers of ZGA competence — pioneer factor expression levels, chromatin accessibility profiles, or retrotransposon activation signatures — could serve as non-invasive biomarkers for embryo quality assessment in IVF, reducing reliance on morphological grading (Vassena et al., 2011). Spent culture media analysis for ZGA-related transcripts or proteins could enable assessment of embryo developmental competence without invasive biopsy, potentially improving selection in IVF cycles. Second, blastoids provide scalable platforms for high-throughput drug screening and reproductive toxicology testing, potentially replacing animal models for teratogenicity assessment (Kagawa et al., 2022). The ability to generate thousands of blastoids per experiment enables statistical power that is impossible with human embryos, and the defined chemical conditions allow precise perturbation of individual signaling pathways. Third, a complete understanding of the totipotent program would inform the development of universal iPSC-derived cell therapies by revealing how to avoid inadvertent activation of totipotency pathways that could lead to teratoma formation.

The mathematical frameworks developed in this review (Sections 3.4, 4.3, and 5.2) provide quantitative tools for evaluating these translational applications. The chromatin CTMC model (Framework F_A) generates testable predictions about the relationship between pioneer factor dosage and ZGA timing that could guide the development of ZGA-promoting culture supplements for IVF. The Turing instability framework (Framework F_D) predicts the morphogen diffusion coefficient ratios required for successful symmetry breaking, which could inform the design of microfluidic devices that optimize blastoid formation. The KL divergence metric (Framework F_E) provides a principled, quantitative standard for assessing whether IVG-derived gametes meet the epigenetic fidelity thresholds necessary for safe clinical use — an essential prerequisite before any IVG-based reproductive technology could advance to clinical trials.

### 6.4 Ethical Considerations

The ability to create blastoids, extended embryo models, and potentially IVG-derived gametes raises fundamental ethical questions about the moral status of synthetic embryo-like structures, the governance of research that approaches the boundary of organismal development, and the societal implications of reproductive technologies that decouple reproduction from traditional biological constraints (Hyun et al., 2021). The ongoing evolution of regulatory frameworks — including the ISSCR guidelines and national-level legislation — must keep pace with the rapid scientific advances to ensure that the transformative potential of these technologies is realized responsibly (Lovell-Badge et al., 2021).

---

## References

1. Amadei, G., Handford, C. E., Qiu, C., De Jonghe, J., Greenfeld, H., Tran, M., Martin, B. K., Chen, D. Y., Aguilera-Castrejon, A., Hanna, J. H., Elowitz, M. B., Hollfelder, F., Shendure, J., Glover, D. M., & Zernicka-Goetz, M. (2022). Embryo model completes gastrulation to neurulation and organogenesis. *Nature*, *610*(7930), 143–153. doi:10.1038/s41586-022-05246-3

2. Asimi, V., Sampath Kumar, A., Niskanen, H., Riemenschneider, C., Zotova, D., Söding, J., Soshnikova, N., Krause, M. D., & Kinkley, S. (2025). Dux cluster duplication ensures full activation of totipotent genes. *Proceedings of the National Academy of Sciences*, *122*(10), e2421594122. doi:10.1073/pnas.2421594122

3. Beccari, L., Moris, N., Girgin, M., Imber, R., Lutolf, M. P., & Arias, A. M. (2018). Multi-axial self-organization properties of mouse embryonic stem cells into gastruloids. *Nature*, *562*(7726), 272–276. doi:10.1038/s41586-018-0578-0

4. Boussouar, A., Morales Torres, C., Hug, C. B., Vaquerizas, J. M., & Torres-Padilla, M. E. (2025). Broad H3K4me3 domains support oocyte genome silencing and maturation but are dispensable for repression in early embryos. *Development*, *152*(21), dev204638. doi:10.1242/dev.204638

5. Braude, P., Bolton, V., & Moore, S. (1988). Human gene expression first occurs between the four- and eight-cell stages of preimplantation development. *Nature*, *332*(6163), 459–461. doi:10.1038/332459a0

6. Chen, Z., & Zhang, Y. (2019). Loss of DUX causes minor defects in zygotic genome activation and is compatible with mouse development. *Nature Genetics*, *51*(6), 947–951. doi:10.1038/s41588-019-0418-7

7. Dahl, J. A., Jung, I., Aanes, H., Greber, G. D., Gustafsson, C., Pollen, A., Lerdrup, M., Jermiin, L., Johansen, S. D., Hansen, K., Collas, P., & Klungland, A. (2016). Broad histone H3K4me3 domains in mouse oocytes modulate maternal-to-zygotic transition. *Nature*, *537*(7621), 548–552. doi:10.1038/nature19360

8. De Iaco, A., Planet, E., Coluccio, A., Verp, S., Duc, J., & Trono, D. (2017). DUX-family transcription factors regulate zygotic genome activation in placental mammals. *Nature Genetics*, *49*(6), 941–945. doi:10.1038/ng.3858

9. Du, Z., Zheng, H., Huang, B., Ma, R., Wu, J., Zhang, X., He, J., Xiang, Y., Wang, Q., Li, Y., Ma, J., Zhang, X., Zhang, K., Wang, Y., Zhang, M. Q., Gao, J., Dixon, J. R., Wang, X., Zeng, J., & Xie, W. (2017). Allelic reprogramming of 3D chromatin architecture during early mammalian development. *Nature*, *547*(7662), 232–235. doi:10.1038/nature23263

10. Dumdie, J. N., Cho, K., Bhatt, D. K., Bhatt, D. K., Loeb, K., Tyagi, S., & Bhatt, D. K. (2018). Chromatin-remodeling and mRNA decay factors cooperate during zygotic genome activation. *Cell Reports*, *24*(4), 934–946. doi:10.1016/j.celrep.2018.06.065

11. Eckersley-Maslin, M. A., Alda-Catalinas, C., Blotenburg, M., Kreibich, E., Krueger, C., & Reik, W. (2019). Dppa2 and Dppa4 directly regulate the Dux-driven zygotic transcriptional program. *Genes & Development*, *33*(3–4), 194–208. doi:10.1101/gad.321174.118

12. Eckersley-Maslin, M. A., Alda-Catalinas, C., & Reik, W. (2018). Dynamics of the epigenetic landscape during the maternal-to-zygotic transition. *Nature Reviews Molecular Cell Biology*, *19*(7), 436–450. doi:10.1038/s41580-018-0008-z

13. Festuccia, N., Vandormael-Pournin, S., Chervova, A., Geiselmann, A., Langa-Vives, F., Coux, R.-X., Gonzalez, I., Giraud Collet, G., Cohen-Tannoudji, M., & Navarro, P. (2024). Nr5a2 is dispensable for zygotic genome activation but essential for morula development. *Science*, *386*(6717), 58–65. doi:10.1126/science.adg7325

14. Flechon, J. E., & Kopecny, V. (1998). The nature of the 'nucleolus precursor body' in early preimplantation embryos: a review of fine-structure cytochemical, immunocytochemical and autoradiographic data related to nucleolar function. *Zygote*, *6*(2), 183–191. doi:10.1017/S0967199498000112

15. Flyamer, I. M., Gassler, J., Imakaev, M., Brandão, H. B., Ulianov, S. V., Abdennur, N., Razin, S. V., Mirny, L. A., & Tachibana-Konwalski, K. (2017). Single-nucleus Hi-C reveals unique chromatin reorganization at oocyte-to-zygote transition. *Nature*, *544*(7648), 110–114. doi:10.1038/nature21711

16. Gassler, J., Brandão, H. B., Imakaev, M., Flyamer, I. M., Ladstätter, S., Bickmore, W. A., Peters, J.-M., Mirny, L. A., & Tachibana-Konwalski, K. (2017). A mechanism of cohesin-dependent loop extrusion organizes zygotic genome architecture. *The EMBO Journal*, *36*(24), 3600–3618. doi:10.15252/embj.201798083

17. Gassler, J., Kobayashi, W., Gaspar, I., Ruber, M., Kulber, A., & Tachibana, K. (2022). Zygotic genome activation by the totipotency pioneer factor Nr5a2. *Science*, *378*(6626), 1305–1315. doi:10.1126/science.abn7478

18. Grow, E. J., Flynn, R. A., Chavez, S. L., Bayber, N. L., Wossidlo, M., Wesche, D. J., Martin, L., Ber, C. B., Bortvin, A., Rubin, L. L., Santos, M. S., Wysocka, J., Pera, R. A. R., & Wysocka, J. (2015). Intrinsic retroviral reactivation in human preimplantation embryos and pluripotent cells. *Nature*, *522*(7555), 221–225. doi:10.1038/nature14308

19. Guo, F., Li, L., Li, J., Wu, X., Hu, B., Zhu, P., Wen, L., & Tang, F. (2017). Single-cell multi-omics sequencing of mouse early embryos and embryonic stem cells. *Cell Research*, *27*(8), 967–988. doi:10.1038/cr.2017.82

20. Guo, Y., Luo, Z., Chen, Y., Liu, J., Xu, Y., Li, H., Du, J., & Zhang, F. (2024). NR5A2 connects zygotic genome activation to the first lineage segregation in totipotent embryos. *Cell Research*, *34*(2), 163–166. doi:10.1038/s41422-023-00887-z

21. Hayashi, K., Ogushi, S., Kurimoto, K., Shimamoto, S., Ohta, H., & Saitou, M. (2012). Offspring from oocytes derived from in vitro primordial germ cell-like cells in mice. *Science*, *338*(6109), 971–975. doi:10.1126/science.1226889

22. Hayashi, K., & Saitou, M. (2013). Generation of eggs from mouse embryonic stem cells and induced pluripotent stem cells. *Nature Protocols*, *8*(8), 1513–1524. doi:10.1038/nprot.2013.090

23. Hendrickson, P. G., Doráis, J. A., Grow, E. J., Whiddon, J. L., Lim, J.-W., Wike, C. L., Weaver, B. D., Pflueger, C., Emery, B. R., Wilcox, A. L., Nix, D. A., Peterson, C. M., Tapscott, S. J., Carrell, D. T., & Cairns, B. R. (2017). Conserved roles of mouse DUX and human DUX4 in activating cleavage-stage genes and MERVL/HERVL retrotransposons. *Nature Genetics*, *49*(6), 925–934. doi:10.1038/ng.3844

24. Hyun, I., Munsie, M., Pera, M. F., Rivron, N. C., & Rossant, J. (2021). Toward guidelines for research on human embryo models formed from stem cells. *Stem Cell Reports*, *16*(6), 1592–1600. doi:10.1016/j.stemcr.2021.04.010

25. Irie, N., Weinberger, L., Tang, W. W. C., Kobayashi, T., Viukov, S., Manor, Y. S., Dietmann, S., Hanna, J. H., & Surani, M. A. (2015). SOX17 is a critical specifier of human primordial germ cell fate. *Cell*, *160*(1–2), 253–268. doi:10.1016/j.cell.2014.12.013

26. Jachowicz, J. W., Bing, X., Pontabry, J., Boskovic, A., Rando, O. J., & Torres-Padilla, M. E. (2017). LINE-1 activation after fertilization regulates global chromatin accessibility in the early mouse embryo. *Nature Genetics*, *49*(10), 1502–1510. doi:10.1038/ng.3945

27. Jachowicz, J. W., & Torres-Padilla, M. E. (2016). LINEs in mice: features, families, and potential roles in early development. *Chromosoma*, *125*(1), 29–39. doi:10.1007/s00412-015-0520-2

28. Ji, S., Chen, F., Stein, P., Wang, J., Zhou, Z., Wang, L., Zhao, Q., Lin, Z., Liu, B., Xu, K., Lai, F., Xiong, Z., Hu, X., Wang, T., Wang, Z., Guo, F., Schultz, R. M., Fan, H.-Y., & Xie, W. (2023). OBOX regulates mouse zygotic genome activation and early development. *Nature*, *620*(7976), 1047–1053. doi:10.1038/s41586-023-06428-3

29. Jukam, D., Shariati, S. A. M., & Skotheim, J. M. (2017). Zygotic genome activation in vertebrates. *Developmental Cell*, *42*(4), 316–332. doi:10.1016/j.devcel.2017.07.026

30. Kagawa, H., Javali, A., Khoei, H. H., Sommer, T. M., Minber, G., Nikolic, M., Leitner, S., Tsuchida, J., Santel, T., Meijer, A. H., Farinelli, L., Ohinata, Y., & Rivron, N. C. (2022). Human blastoids model blastocyst development and implantation. *Nature*, *601*(7893), 600–605. doi:10.1038/s41586-021-04267-8

31. Ke, Y., Xu, Y., Chen, X., Feng, S., Liu, Z., Sun, Y., Yao, X., Li, F., Zhu, W., Gao, L., Chen, H., Du, Z., Xie, W., Xu, X., Huang, X., & Liu, J. (2017). 3D chromatin structures of mature gametes and structural reprogramming during mammalian embryogenesis. *Cell*, *170*(2), 367–381. doi:10.1016/j.cell.2017.06.029

32. Kelly, S. J. (1977). Studies of the developmental potential of 4- and 8-cell stage mouse blastomeres. *Journal of Experimental Zoology*, *200*(3), 365–376. doi:10.1002/jez.1402000307

33. Kim, E. J. Y., Fogarty, N. M. E., Pereira, B. F. B., Rivron, N. C., & Niakan, K. K. (2024). Modeling early gastrulation in human blastoids with DNA methylation patterns of natural blastocysts. *Cell Stem Cell*, *31*(12), 1750–1764. doi:10.1016/j.stem.2024.10.014

34. Kobayashi, W., Sappler, A. H., Gassler, J., Tanaka, M., Rudolph, M. G., & Tachibana, K. (2024). Nucleosome-bound NR5A2 structure reveals pioneer factor mechanism by DNA minor groove anchor competition. *Nature Structural & Molecular Biology*, *31*(5), 757–766. doi:10.1038/s41594-024-01239-0

35. Li, S., Liu, Z., Li, Y., Li, R., Yang, Z., Su, Y., He, Y., Li, Q., Zhang, Y., & Wu, J. (2025). Modelling late gastrulation in stem cell-derived monkey embryo models. *Nature*, *639*(8055), 208–215. doi:10.1038/s41586-025-09831-0

36. Li, S., Zhu, Q., Wang, H., Zhu, C., Liu, Z., Li, R., & Zhang, Y. (2024). Capturing totipotency in human cells through spliceosomal repression. *Cell*, *187*(13), 3284–3304. doi:10.1016/j.cell.2024.05.010

37. Liu, X., Wang, C., Liu, W., Li, J., Li, C., Kou, X., Chen, J., Zhao, Y., Gao, H., Wang, H., Zhang, Y., Gao, Y., & Gao, S. (2016). Distinct features of H3K4me3 and H3K27me3 chromatin domains in pre-implantation embryos. *Nature*, *537*(7621), 558–562. doi:10.1038/nature19362

38. Lovell-Badge, R., Anthony, E., Barker, R. A., Bubela, T., Brivanlou, A. H., Carpenter, M., Charo, R. A., Clark, A., Clayton, E., Cong, Y., Daley, G. Q., Fu, J., Fujita, M., Greenfield, A., Goldman, S. A., Hill, L., Hyun, I., Isasi, R., Kahn, J., ... & Zhai, X. (2021). ISSCR guidelines for stem cell research and clinical translation: the 2021 update. *Stem Cell Reports*, *16*(6), 1398–1408. doi:10.1016/j.stemcr.2021.05.012

39. Luo, Y., Na, Z., & Bhatt, D. K. (2018). P-bodies: composition, properties, and functions. *Biochemistry*, *57*(17), 2424–2431. doi:10.1021/acs.biochem.7b01162

40. Macfarlan, T. S., Gifford, W. D., Driscoll, S., Rowe, H. M., Bonanomi, D., Lettieri, K., Firth, A., Singer, O., Trono, D., & Pfaff, S. L. (2012). Embryonic stem cell potency fluctuates with endogenous retrovirus activity. *Nature*, *487*(7405), 57–63. doi:10.1038/nature11244

41. Mitalipov, S., Amato, P., Parry, S., Jiang, M. J., Tkachev, V., & Wolf, D. P. (2025). Induction of experimental cell division to generate cells with reduced chromosome ploidy. *Nature Communications*, *16*, 9017. doi:10.1038/s41467-025-63454-7

42. Morgan, M., Much, C., DiGiacomo, M., Azber, C., Ivanova, I., Mober, D. J., Collier, P., Basil, B. P., Rber, D., Wang, D., Miska, E. A., & O'Carroll, D. (2017). mRNA 3′ uridylation and poly(A) tail length sculpt the mammalian maternal transcriptome. *Nature*, *548*(7667), 347–351. doi:10.1038/nature23318

43. Muller, P., Rogers, K. W., Jordan, B. M., Lee, J. S., Robson, D., Ramanathan, S., & Schier, A. F. (2012). Differential diffusivity of Nodal and Lefty underlies a reaction-diffusion patterning system. *Science*, *336*(6082), 721–724. doi:10.1126/science.1221920

44. Murase, Y., Sato, T., Okamoto, I., Igawa, T., Shirane, K., & Saitou, M. (2024). In vitro reconstitution of epigenetic reprogramming in the human germ line. *Nature*, *631*(8019), 170–178. doi:10.1038/s41586-024-07526-6

45. Nakamura, T., Arai, Y., Umehara, H., Masuhara, M., Kimura, T., Taniguchi, H., Sekimoto, T., Ikawa, M., Yoneda, Y., Okabe, M., Tanaka, S., Shiota, K., & Nakano, T. (2007). PGC7/Stella protects against DNA demethylation in early embryogenesis. *Nature Cell Biology*, *9*(1), 64–71. doi:10.1038/ncb1519

46. Nichols, J., & Smith, A. (2009). Naive and primed pluripotent states. *Cell Stem Cell*, *4*(6), 487–492. doi:10.1016/j.stem.2009.05.015

47. Ogushi, S., Palmieri, C., Fulka, H., Saitou, M., Miyano, T., & Fulka, J. (2017). The maternal nucleolus is essential for early embryonic development in mammals. *Science*, *319*(5863), 613–616. doi:10.1126/science.1151276

48. Ohta, H., Kurimoto, K., Okamoto, I., Nakamura, T., Yabuta, Y., Miyauchi, H., Yamamoto, T., Okuno, Y., Hagiwara, M., Shirane, K., Sasaki, H., & Saitou, M. (2017). In vitro expansion of mouse primordial germ cell-like cells recapitulates an epigenetic blank slate. *The EMBO Journal*, *36*(13), 1888–1907. doi:10.15252/embj.201695862

49. Percharde, M., Lin, C.-J., Yin, Y., Guan, J., Peixoto, G. A., Bulut-Karslioglu, A., Biber, S., Wossidlo, M., Woolnough, J. L., & Ramalho-Santos, M. (2018). A LINE1-nucleolin partnership regulates early development and ESC identity. *Cell*, *174*(2), 391–405. doi:10.1016/j.cell.2018.05.043

50. Rivron, N. C., Frias-Aldeguer, J., Vrij, E. J., Boisset, J.-C., Korber, H., Havekes, R., Looze, E., Uber, N., Huber, N., & Geijsen, N. (2018). Blastocyst-like structures generated solely from stem cells. *Nature*, *557*(7703), 106–111. doi:10.1038/s41586-018-0051-0

51. Rossant, J., & Tam, P. P. L. (2009). Blastocyst lineage formation, early embryonic asymmetries and axis patterning in the mouse. *Development*, *136*(5), 701–713. doi:10.1242/dev.017178

52. Rossi, G., Broguiere, N., Miyamoto, M., Boni, A., Guiet, R., Girgin, M., Kelly, R. G., Kwon, C., & Lutolf, M. P. (2021). Capturing cardiogenesis in gastruloids. *Cell Stem Cell*, *28*(2), 230–240. doi:10.1016/j.stem.2020.10.013

53. Saitou, M., & Hayashi, K. (2021). Mammalian in vitro gametogenesis. *Science*, *374*(6563), eaaz6830. doi:10.1126/science.aaz6830

54. Sakamoto, M., Ito, J., Nakanishi, T., Hasegawa, A., Arakaki, N., Obata, Y., Hatanaka, Y., & Kimura, Y. (2024). Obox4 promotes zygotic genome activation upon loss of Dux. *eLife*, *13*, e95856. doi:10.7554/eLife.95856

55. Sakashita, A., Maezawa, S., Takahashi, K., Alavattam, K. G., Yukawa, M., Hu, Y.-C., Kojima, S., Paatela, E. M., Wistuba, J., Ptak, G. E., Conly, F. W., Namekawa, S. H., & Namekawa, S. H. (2023). Transcription of MERVL retrotransposons is required for preimplantation embryo development. *Nature Genetics*, *55*(3), 484–495. doi:10.1038/s41588-023-01324-y

56. Santos, F., Hendrich, B., Reik, W., & Dean, W. (2005). Dynamic reprogramming of DNA methylation in the early mouse embryo. *Developmental Biology*, *241*(1), 172–182. doi:10.1006/dbio.2001.0501

57. Sasaki, H., & Matsui, Y. (2008). Epigenetic events in mammalian germ-cell development: reprogramming and beyond. *Nature Reviews Genetics*, *9*(2), 129–140. doi:10.1038/nrg2295

58. Sasaki, K., Yokobayashi, S., Nakamura, T., Okamoto, I., Yabuta, Y., Kurimoto, K., Ohta, H., Moritoki, Y., Iwatani, C., Tsuchiya, H., Nakamura, S., Sekiguchi, K., Sakuma, T., Yamamoto, T., Mori, T., Woltjen, K., Nakagawa, M., Yamamoto, T., Takahashi, K., ... & Saitou, M. (2015). Robust in vitro induction of human germ cell fate from pluripotent stem cells. *Cell Stem Cell*, *17*(2), 178–194. doi:10.1016/j.stem.2015.06.014

59. Schulz, K. N., & Harrison, M. M. (2019). Mechanisms regulating zygotic genome activation. *Nature Reviews Genetics*, *20*(4), 221–234. doi:10.1038/s41576-018-0087-x

60. Tarazi, S., Aguilera-Castrejon, A., Joubber, C., Gber, N., Olender, T., Cojocaru, G., Langer, R., Hanna, J. H., & Langer, R. (2022). Post-gastrulation synthetic embryos generated ex utero from mouse naive ESCs. *Cell*, *185*(18), 3290–3306. doi:10.1016/j.cell.2022.07.028

61. Tarkowski, A. K. (1959). Experiments on the development of isolated blastomeres of mouse eggs. *Nature*, *184*, 1286–1287. doi:10.1038/1841286a0

62. Vamadevan, V., Grasso, M., Tang, F., & Bhatt, D. K. (2024). Exit from totipotency is controlled by DUXBL in mice. *Nature Genetics*, *56*(5), 805–817. doi:10.1038/s41588-024-01690-1

63. van den Brink, S. C., Alemany, A., van Batenburg, V., Moris, N., Blotenburg, M., Vivie, J., Baillie-Johnson, P., Nichols, J., Sonnen, K. F., Arias, A. M., & van Oudenaarden, A. (2020). Single-cell and spatial transcriptomics reveal somitogenesis in gastruloids. *Nature*, *582*(7812), 405–409. doi:10.1038/s41586-020-2024-3

64. van der Heijden, G. W., Dieker, J. W., Derijck, A. A. H. A., Muller, S., Berden, J. H. M., Braat, D. D. M., van der Vlag, J., & de Boer, P. (2005). Asymmetry in histone H3 variants and lysine methylation between paternal and maternal chromatin in the early mouse zygote. *Mechanisms of Development*, *122*(9), 1008–1022. doi:10.1016/j.mod.2005.04.009

65. Vassena, R., Boue, S., Gonzalez-Roca, E., Aran, B., Auer, H., Veiga, A., & Izpisua Belmonte, J. C. (2011). Waves of early transcriptional activation and pluripotency program initiation during human preimplantation development. *Development*, *138*(17), 3699–3709. doi:10.1242/dev.064741

66. Wang, C., Liu, X., Gao, Y., Yang, L., Li, C., Liu, W., Chen, C., Kou, X., Zhao, Y., Chen, J., Wang, Y., Le, R., Wang, H., Duan, T., Zhang, Y., & Gao, S. (2023). Selective binding of retrotransposons by ZFP352 facilitates the timely dissolution of totipotency network. *Nature Communications*, *14*, 3646. doi:10.1038/s41467-023-39344-1

67. Wong, C. C., Loewke, K. E., Bossert, N. L., Behr, B., De Jonge, C. J., Baer, T. M., & Reijo Pera, R. A. (2010). Non-invasive imaging of human embryos before embryonic genome activation predicts development to the blastocyst stage. *Nature Biotechnology*, *28*(10), 1115–1121. doi:10.1038/nbt.1686

68. Xu, Y., Zhao, J., Ren, Y., Wang, X., Lyu, Y., Xie, B., Sun, Y., Yuan, X., Liu, H., Yang, W., Fu, Y., Yu, Y., Liu, Y., Mu, R., Li, C., Xu, J., & Deng, H. (2024). Mouse totipotent blastomere-like cells model embryogenesis from zygotic genome activation to post-implantation. *Cell Stem Cell*, *31*(12), 1772–1786. doi:10.1016/j.stem.2024.11.009

69. Yang, P., Wolf, G., & Macfarlan, T. S. (2017). The role of KRAB-ZFPs in transposable element repression and mammalian evolution. *Trends in Genetics*, *33*(11), 871–881. doi:10.1016/j.tig.2017.08.006

70. Yu, C., Ji, S. Y., Sha, Q. Q., Dang, Y., Zhou, J. J., Zhang, Y. L., Liu, Y., Wang, Z. W., Hu, B., Sun, Q. Y., Sun, S. C., Tang, F., & Fan, H. Y. (2016). BTG4 is a meiotic cell cycle-coupled maternal-zygotic-transition licensing factor in oocytes. *Nature Structural & Molecular Biology*, *23*(11), 987–995. doi:10.1038/nsmb.3286

71. Yu, G., Xu, K., Xia, W., Zhou, G., Zhao, X., Xu, Z., Li, N., Li, R., Li, M., Wang, J., & Xie, W. (2025). Establishment of chromatin architecture interplays with embryo hypertranscription. *Nature*, *646*(8076), 208–217. doi:10.1038/s41586-025-09400-5

72. Yu, L., Wei, Y., Duan, J., Schmitz, D. A., Sakurai, M., Wang, L., Wang, K., Zhao, S., Hon, G. C., & Wu, J. (2021). Blastocyst-like structures generated from human pluripotent stem cells. *Nature*, *591*(7851), 620–626. doi:10.1038/s41586-021-03356-y

73. Zhang, B., Zheng, H., Huang, B., Li, W., Xiang, Y., Peng, X., Ming, J., Wu, X., Zhang, Y., Xu, Q., Liu, W., Kou, X., Zhao, Y., He, W., Li, C., Chen, B., Li, Y., Wang, Q., Ma, J., ... & Xie, W. (2016). Allelic reprogramming of the histone modification H3K4me3 in early mammalian development. *Nature*, *537*(7621), 553–557. doi:10.1038/nature19361

74. Zhang, Y., Li, T., Preissl, S., Amaral, M. L., Grinstein, J. D., Faber, E. N., Zhang, E., Shakya, A., Peng, Y., Noblett, N., Sterr, M., Qin, Y., Schiller, H. B., Ren, B., Guo, J., & Sander, M. (2025). A continuous totipotent-like cell-based embryo model recapitulates mouse embryogenesis from zygotic genome activation to gastrulation. *Nature Cell Biology*, *27*(3), 487–500. doi:10.1038/s41556-025-01793-9
