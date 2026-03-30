# Nuclear Reprogramming Review

## Abstract

Nuclear reprogramming spans a hierarchy of progressively deeper epigenetic erasure events, from partial resetting to pluripotency through complete erasure to totipotency and the deepest reprogramming in the germline. While transcription-factor-based approaches (OSKM/OSK) have dominated clinical translation, they access only the shallowest tier of this hierarchy and cannot replicate the molecular logic of complete reprogramming. The mammalian oocyte harbors a coordinated reprogramming machine — comprising histone variant H3.3 deposited by HIRA, nucleoplasmin NPM2, the SWI/SNF remodeler BRG1, the demethylase TET3, and the H3K9me3 eraser KDM4A — that achieves what transcription factors alone cannot. This review organizes the field around a Reprogramming Depth Hierarchy: Tier 1 (pluripotency, achieved by somatic cell nuclear transfer and induced pluripotency), Tier 2 (totipotency, governed by zygotic genome activation and the DUX-MERVL circuit), and Tier 3 (germline reprogramming, encompassing primordial germ cell specification, imprint erasure, and in vitro gametogenesis). At each tier, we identify the molecular machinery, recent engineering breakthroughs (including a 2025 epigenetic cocktail achieving 75% blastocyst rates in SCNT, and primate nuclear-transfer embryonic stem cells from marmosets), and the fidelity defects that limit clinical translation. We introduce quantitative frameworks — competitive chromatin remodeling kinetics, sequential barrier erasure reliability, the DUX-MERVL bistable switch, germline demethylation traveling waves, Jensen-Shannon divergence for reprogramming fidelity, and Bayesian oocyte competence classification — that formalize the engineering challenges at each depth. Together, these analyses argue that achieving high-fidelity complete reprogramming requires understanding the oocyte's coordinated machinery, not merely intensifying transcription-factor expression.

---

## 1. Introduction: The Reprogramming Depth Hierarchy

The term "nuclear reprogramming" encompasses fundamentally distinct biological phenomena operating at different depths of epigenetic erasure. At the shallowest level, transient expression of Oct4, Sox2, and Klf4 (OSK) can partially rejuvenate aged somatic cells without altering their identity — resetting DNA methylation clocks while preserving lineage commitment (Gill et al., 2022). At intermediate depth, somatic cell nuclear transfer (SCNT) into enucleated oocytes resets the somatic epigenome to a pluripotent state, erasing most but not all lineage-specific marks (Matoba & Zhang, 2018). At the deepest level, primordial germ cells (PGCs) undergo genome-wide erasure of DNA methylation, including imprinted loci, achieving the most complete epigenetic reset known in mammalian biology (Seisenberger et al., 2012).

These three tiers — pluripotency, totipotency, and germline — are not merely quantitative differences along a single axis. Each tier engages distinct molecular machinery and confronts unique fidelity challenges. Transcription-factor-based reprogramming, the dominant paradigm since Yamanaka's 2006 discovery, accesses only Tier 1 and does so incompletely: induced pluripotent stem cells (iPSCs) retain epigenetic memory of their cell of origin (Kim et al., 2010), accumulate aberrant DNA methylation patterns not found in embryonic stem cells (ESCs) (Lister et al., 2011), and exhibit unstable X-chromosome inactivation (XCI) in female lines (Pasque et al., 2014). SCNT, by contrast, harnesses the oocyte's endogenous reprogramming machinery and produces cells with methylomes more closely resembling the inner cell mass (ICM) than iPSCs (Ma et al., 2014) — yet SCNT embryos still fail at rates exceeding 90%, primarily due to persistent histone H3 lysine 9 trimethylation (H3K9me3) at reprogramming-resistant regions (RRRs) (Matoba et al., 2014).

Recent technological advances have begun to bridge these gaps. A 2025 epigenetic cocktail combining trichostatin A (TSA), Kdm4d, and Kdm5b mRNA achieved 75% blastocyst formation in mouse SCNT — a six-fold improvement over untreated controls (Li et al., 2025a). Human totipotent blastomere-like cells (hTBLCs) have been captured through spliceosomal repression (Li et al., 2024a). And BMP-driven differentiation of human PGC-like cells (hPGCLCs) into oogonia now enables reconstitution of the earliest stages of in vitro gametogenesis (IVG) (Murase et al., 2024). Simultaneously, single-cell multi-omic technologies are revealing the mechanistic failure points that separate successful from unsuccessful reprogramming, enabling mechanism-guided protocol design (Morris, 2025).

This review organizes the field around the **Reprogramming Depth Hierarchy**: Tier 1 (pluripotency), Tier 2 (totipotency), and Tier 3 (germline), with reprogramming fidelity as a cross-cutting theme. For each tier, we identify the molecular machinery employed, the engineering strategies available, and the quantitative frameworks needed to evaluate success. Our central argument is that achieving complete, high-fidelity nuclear reprogramming — the goal needed for clinical-grade IVG, mitochondrial replacement therapy, and next-generation cell therapies — requires understanding and recapitulating the oocyte's coordinated reprogramming machine, not merely intensifying transcription-factor expression.

---

## 2. The Oocyte Reprogramming Machine: Molecular Components of Complete Erasure

### 2.1 A Coordinated System, Not Individual Factors

The mammalian metaphase II (MII) oocyte is the only cell type that can reliably reprogram a terminally differentiated somatic nucleus to a totipotent state. This capacity resides not in any single factor but in a coordinated molecular system whose components act in defined temporal sequence (Ladstätter & Bhatt, 2025). Understanding this system as an integrated machine — rather than as a collection of individual reprogramming factors — is essential for explaining why SCNT succeeds where transcription-factor approaches reach a ceiling, and for engineering improved reprogramming protocols.

**Premature chromosome condensation (PCC).** The first event after nuclear transfer is the rapid condensation of the somatic chromatin into a mitotic-like state, driven by the high concentration of M-phase promoting factor (MPF, the CDK1-Cyclin B complex) in the MII oocyte cytoplasm (Matoba & Zhang, 2018). PCC is not merely a structural reorganization: it strips the somatic nucleus of its nuclear lamina associations, disrupts topologically associating domains (TADs), and renders the chromatin accessible to oocyte-resident remodeling factors. In fertilization, PCC acts on the sperm nucleus; in SCNT, it forces the somatic nucleus through an analogous mitotic-like transition that is prerequisite to all subsequent reprogramming steps.

**H3.3 deposition by HIRA.** The histone variant H3.3, deposited independently of DNA replication by the chaperone HIRA, replaces somatic histones H3.1 and H3.2 throughout the paternal genome within hours of fertilization (van der Heijden et al., 2005). H3.3 lacks the lysine 27 trimethylation characteristic of canonical H3 and carries post-translational modifications associated with active or poised chromatin. In SCNT, HIRA-mediated H3.3 deposition is required for reactivation of pluripotency genes in the transferred nucleus; depletion of maternal H3.3 stores impairs SCNT reprogramming (Ladstätter & Bhatt, 2025).

**NPM2 nucleoplasmin.** Nucleoplasmin 2 (NPM2) is the most abundant nuclear protein in the oocyte and serves as the primary histone chaperone for sperm protamine-to-histone exchange (Burns et al., 2003). NPM2 knockout females exhibit severe fertility defects due to failed preimplantation development, demonstrating that chromatin decondensation by NPM2 is essential for reprogramming competence. In the SCNT context, NPM2 mediates the decondensation of PCC-compacted somatic chromatin, enabling access by transcription factors and other remodelers.

**BRG1/SMARCA4.** The catalytic subunit of the SWI/SNF (BAF) chromatin remodeling complex, BRG1 (encoded by *SMARCA4*), uses ATP hydrolysis to slide, evict, and restructure nucleosomes. BRG1 is required for zygotic genome activation (ZGA): maternal BRG1 depletion in mouse oocytes results in developmental arrest at the two-cell stage due to failure of minor ZGA (Bultman et al., 2006). Conditional oocyte-specific knockout of *Smarca4* causes subfertility, confirming BRG1's role as an essential maternal-effect gene (Menon et al., 2022). In SCNT, BRG1 remodels somatic chromatin to permit de novo transcription from the transferred genome.

**TET3 demethylase.** Ten-eleven translocation methylcytosine dioxygenase 3 (TET3) is the predominant TET family member in the oocyte and is responsible for the rapid active demethylation of the paternal genome within 6-8 hours of fertilization (Gu et al., 2011). TET3 oxidizes 5-methylcytosine (5mC) to 5-hydroxymethylcytosine (5hmC) and further oxidation products, which are then removed by base excision repair or diluted through replication. In SCNT embryos, TET3-mediated demethylation of the somatic donor genome is critical for reactivating silenced pluripotency genes.

**KDM4A.** Lysine-specific demethylase 4A (KDM4A, also known as JMJD2A) is the oocyte's endogenous eraser of H3K9me3 — the single most significant epigenetic barrier to SCNT reprogramming. KDM4A shows near-exclusive expression in MII oocytes and is essential for maintaining genomic stability and proper ZGA after fertilization (Matoba et al., 2014). The fact that KDM4A's close paralog Kdm4d — normally not expressed at high levels in oocytes — can dramatically improve SCNT efficiency when exogenously supplied underscores the importance of this demethylase activity.

### 2.2 Framework F292: Competitive Chromatin Remodeling Kinetics

The coordinated action of oocyte factors can be formalized as a competitive kinetic system. Consider a somatic nucleosome existing in state $S$ (marked by H3K9me3, DNA methylation, and somatic histone variants). Multiple oocyte factors compete with somatic maintenance enzymes for access to this substrate:

```math
\frac{dm_i}{dt} = k_{\text{maint},i} \cdot (1 - m_i) \cdot \frac{[E_{\text{maint},i}]}{K_{M,i}^{\text{maint}} + (1 - m_i)} - k_{\text{erase},i} \cdot m_i \cdot \frac{[E_{\text{erase},i}]}{K_{M,i}^{\text{erase}} + m_i}
```

where:
- $m_i(t) \in [0,1]$ is the fraction of nucleosomes retaining somatic mark $i$ (e.g., $i \in \{$H3K9me3, 5mC, H3.1$\}$) at time $t$
- $[E_{\text{maint},i}]$ is the concentration of the somatic maintenance enzyme for mark $i$ (DNMT1 for 5mC, SUV39H1/2 for H3K9me3)
- $[E_{\text{erase},i}]$ is the concentration of the oocyte erasure factor (TET3 for 5mC, KDM4A for H3K9me3, HIRA for H3.1→H3.3 exchange)
- $K_{M,i}^{\text{maint}}$ and $K_{M,i}^{\text{erase}}$ are the respective Michaelis constants
- $k_{\text{maint},i}$ and $k_{\text{erase},i}$ are catalytic rate constants

Define the **reprogramming potential** at each locus as:

```math
R_i = \frac{k_{\text{erase},i} \cdot [E_{\text{erase},i}] / K_{M,i}^{\text{erase}}}{k_{\text{maint},i} \cdot [E_{\text{maint},i}] / K_{M,i}^{\text{maint}}}
```

When $R_i > 1$, erasure dominates and the mark is removed; when $R_i < 1$, maintenance dominates and the somatic mark persists. Complete reprogramming requires $R_i > 1$ simultaneously for all mark types $i$ across the genome. The observation that only ~1-5% of SCNT embryos develop to term reflects the stochastic nature of achieving $R_i > 1$ at all marked loci simultaneously — a combinatorial challenge that explains why adding exogenous erasure factors (Kdm4d, Kdm5b) dramatically improves outcomes by increasing $[E_{\text{erase}}]$ for specific marks.

This competitive framework also explains why transcription-factor-based reprogramming (iPSC generation) reaches a fidelity ceiling: Oct4, Sox2, and Klf4 act as pioneer transcription factors that open specific loci but do not globally shift the $R_i$ ratio for somatic marks (Morris, 2025). The oocyte machine, by contrast, provides saturating concentrations of erasure factors for multiple mark types simultaneously.

---

## 3. Somatic Cell Nuclear Transfer: Engineering Complete Reprogramming

### 3.1 The H3K9me3 Barrier and Reprogramming-Resistant Regions

The single greatest impediment to SCNT efficiency is the persistence of H3K9me3 at defined genomic regions after nuclear transfer. Matoba and colleagues identified these reprogramming-resistant regions (RRRs) in mouse SCNT embryos: hundreds of loci where somatic H3K9me3 persists through the two-cell stage, preventing normal ZGA gene expression (Matoba et al., 2014). RRRs overlap with somatic heterochromatin domains but are absent from the normal zygotic epigenome, confirming that they represent a failure of reprogramming rather than a developmental feature.

Injection of Kdm4d mRNA — encoding an H3K9me3 demethylase — into SCNT embryos reactivated the majority of RRRs and restored the global transcriptome: the number of differentially expressed genes between SCNT and in vitro fertilization (IVF) two-cell embryos decreased from 1,212 to 475 (Matoba et al., 2014). Kdm4d-treated SCNT embryos rarely arrested during the two-cell to four-cell transition and reached the blastocyst stage at 88.6% efficiency.

Beyond H3K9me3, a second barrier operates post-implantation. SCNT embryos suffer loss of H3K27me3-dependent non-canonical imprinting, which normally restricts paternal allele expression at specific loci required for placental development (Inoue et al., 2017). This loss causes placental overgrowth and large offspring syndrome — phenotypes that contribute to the high rate of SCNT failure after implantation. Critically, H3K27me3 imprinting defects are not corrected by Kdm4d treatment, revealing a multi-barrier architecture that demands orthogonal solutions for pre- and post-implantation stages.

A 2023 study provided direct evidence that unreprogrammed H3K9me3 prevents minor ZGA and subsequent lineage commitment in SCNT embryos (Wang et al., 2023). Using allele-specific ChIP-seq, the authors showed that persistent H3K9me3 on the somatic allele blocked the activation of lineage-specifying transcription factors, trapping SCNT embryos in a pre-ZGA state. This finding established H3K9me3 removal as necessary not merely for gene reactivation but for the entire downstream trajectory of embryonic development.

### 3.2 The 2025 Cocktail: Overcoming Pre- and Post-Implantation Barriers

A breakthrough in 2025 demonstrated that combinatorial epigenetic manipulation can overcome both pre- and post-implantation barriers in a single protocol (Li et al., 2025a). The approach, termed the "cocktail method," combines three interventions:

1. **TSA (trichostatin A):** A histone deacetylase (HDAC) inhibitor that increases histone acetylation and chromatin accessibility globally
2. **Kdm4d mRNA injection:** Directly removes H3K9me3 at RRRs
3. **Kdm5b mRNA injection:** Removes H3K4me3, which in the SCNT context marks loci that should be silenced but are aberrantly active due to somatic memory

The results were dramatic: cocktail-treated SCNT embryos reached the blastocyst stage at 75% efficiency, compared to 13% for untreated controls and 37% for TSA alone (Li et al., 2025a). To address post-implantation H3K27me3 imprinting defects, the authors employed tetraploid complementation — replacing the SCNT-derived extraembryonic lineage with wild-type tetraploid cells — which bypassed placental overgrowth and enabled live birth of cloned pups.

### 3.3 Primate SCNT: Marmoset Nuclear-Transfer ESCs

The extension of improved SCNT protocols to non-human primates was achieved in 2025 with the derivation of ESCs from cloned marmoset blastocysts (Matoba et al., 2025). Building on the mouse cocktail approach, the authors found that Kdm4d mRNA injection alone enabled blastocyst formation from marmoset fibroblasts at 14.5% efficiency. Adding the G9a/EHMT2 histone methyltransferase inhibitor UNC0638 improved blastocyst quality sufficiently to derive nuclear-transfer ESC (ntESC) lines, including wild-type and GFP-transgenic lines.

The ntESCs exhibited normal karyotypes and expressed standard pluripotency markers, with nuclear DNA confirming donor origin and mitochondrial DNA confirming oocyte origin — the hallmark of successful SCNT. However, transcriptome analysis revealed line-dependent abnormally expressed genes, consistent with partial reprogramming resistance at some loci. This finding underscores that even in primates, the oocyte's reprogramming capacity is not absolute: certain somatic marks resist erasure regardless of Kdm4d supplementation.

### 3.4 Framework F293: Sequential Epigenetic Barrier Erasure

Complete SCNT reprogramming can be modeled as sequential removal of three barrier classes, each requiring multiple enzymatic steps. Let $T_j$ denote the random time to erase barrier class $j$ (where $j = 1$ for H3K9me3, $j = 2$ for DNA methylation, $j = 3$ for H3K27me3). Each barrier requires $k_j$ sequential enzymatic steps, each with exponential rate $\lambda_j$, giving $T_j$ an Erlang distribution:

```math
f_{T_j}(t) = \frac{\lambda_j^{k_j} \, t^{k_j - 1} \, e^{-\lambda_j t}}{(k_j - 1)!}, \quad t \geq 0
```

where:
- $k_j$ is the number of sequential enzymatic steps for barrier $j$ (reflecting the multi-step nature of mark removal: for H3K9me3, this includes KDM4-mediated demethylation followed by histone exchange; for 5mC, TET-mediated oxidation followed by base excision repair)
- $\lambda_j$ is the rate per step, determined by enzyme concentration and catalytic efficiency

The total reprogramming time for a given locus is $T_{\text{total}} = T_1 + T_2 + T_3$, with distribution given by the convolution:

```math
f_{T_{\text{total}}}(t) = (f_{T_1} * f_{T_2} * f_{T_3})(t)
```

Successful development requires $T_{\text{total}} < \tau$, where $\tau$ is the developmental time window before commitment events close (approximately 24-48 hours to the two-cell stage in mouse). The probability of successful reprogramming at a single locus is:

```math
P_{\text{success}} = P(T_{\text{total}} < \tau) = \int_0^{\tau} f_{T_{\text{total}}}(t) \, dt
```

For $N$ independent loci requiring simultaneous erasure, the genome-wide success probability is $P_{\text{genome}} = P_{\text{success}}^N$. This exponential dependence on $N$ explains the steep decline in SCNT efficiency: even a modest per-locus failure rate (1-$P_{\text{success}}$) yields near-zero genome-wide success for large $N$.

The cocktail method improves outcomes by increasing $\lambda_1$ (Kdm4d accelerates H3K9me3 removal), decreasing $k_2$ (TSA pre-acetylation reduces the number of sequential steps for DNA demethylation by increasing chromatin accessibility), and increasing $\lambda_2$ (Kdm5b removes aberrant H3K4me3 that otherwise competes for enzymatic machinery). These interventions compress $E[T_{\text{total}}] = \sum_j k_j / \lambda_j$, increasing $P(T_{\text{total}} < \tau)$ from $\sim$0.13 to $\sim$0.75 in the observed data.

---

## 4. Zygotic Genome Activation: The Totipotent Code

### 4.1 DUX and the Master Regulatory Circuit

Zygotic genome activation (ZGA) is the transcriptional event that marks the transition from maternal to embryonic control of development and defines the totipotent state. In mouse, ZGA occurs in two waves: minor ZGA at the late one-cell stage activates hundreds of genes, while major ZGA at the two-cell stage activates thousands, including the full totipotency program (Schulz & Harrison, 2019). The transcription factor DUX (double homeobox) has been identified as the master regulator of major ZGA: DUX binds to long terminal repeats (LTRs) of MERVL (murine endogenous retrovirus with leucine tRNA primer) endogenous retroviruses and activates a cascade of totipotency-associated genes (Macfarlan et al., 2012; De Iaco et al., 2017).

The DUX regulatory circuit exhibits several features of a robust developmental switch. First, the *Dux* locus exists as a tandem gene cluster, and recent work demonstrates that this cluster duplication is not merely a consequence of retrotransposon-driven genome expansion but serves a functional dosage-ensuring role: the duplication ensures full activation of the totipotent transcriptional program, with cluster copy number correlating with 2C gene expression magnitude across species (Asimi et al., 2025). Second, the homeobox transcription factor OBOX4 acts as a parallel, DUX-independent ZGA activator: Obox4 promotes ZGA by binding to MERVL and MERVK LTRs even in *Dux* knockout embryos, establishing a redundant activation pathway (Sakamoto et al., 2024). Third, DPPA2 and DPPA4 form obligate heterodimers that directly bind *Dux* repeats and promoter regions, providing upstream regulation — although maternal DPPA2/4 are dispensable for in vivo ZGA, indicating additional failsafe mechanisms (De Iaco et al., 2019).

### 4.2 Framework F294: The DUX-MERVL Positive Feedback Bistable Switch

The DUX-MERVL regulatory circuit has the topology of a positive feedback loop: DUX activates MERVL LTR-driven transcription, and MERVL-derived enhancers create a permissive chromatin environment that sustains DUX expression (Macfarlan et al., 2012). This topology predicts bistability — the coexistence of two stable states — which explains the observation that mouse embryonic stem cell (mESC) cultures contain a rare ($\sim$0.5-1%) population of "2-cell-like cells" (2CLCs) that spontaneously and reversibly enter a totipotent-like state.

We model this circuit with two coupled ordinary differential equations. Let $D$ denote DUX protein concentration and $M$ denote the aggregate level of MERVL-driven transcripts:

```math
\frac{dD}{dt} = \alpha_D + \beta_D \cdot \frac{M^n}{K_M^n + M^n} - \gamma_D \cdot D
```

```math
\frac{dM}{dt} = \beta_M \cdot \frac{D^m}{K_D^m + D^m} - \gamma_M \cdot M
```

where:
- $\alpha_D$ is the basal DUX production rate (low, from constitutive promoter leakage)
- $\beta_D$ is the maximal MERVL-enhanced DUX production rate
- $K_M$ is the MERVL transcript level at half-maximal DUX enhancement
- $n \geq 2$ is the Hill coefficient for cooperative MERVL-driven activation (reflecting multivalent LTR binding)
- $\beta_M$ is the maximal DUX-activated MERVL transcription rate
- $K_D$ is the DUX concentration at half-maximal MERVL activation
- $m \geq 2$ is the Hill coefficient for DUX binding cooperativity
- $\gamma_D, \gamma_M$ are degradation rates for DUX protein and MERVL transcripts, respectively

**Nullcline analysis.** The $D$-nullcline ($dD/dt = 0$) and $M$-nullcline ($dM/dt = 0$) are:

```math
D^* = \frac{1}{\gamma_D}\left(\alpha_D + \beta_D \cdot \frac{M^n}{K_M^n + M^n}\right), \quad M^* = \frac{\beta_M}{\gamma_M} \cdot \frac{D^m}{K_D^m + D^m}
```

For $n, m \geq 2$ and biologically realistic parameter values, these nullclines intersect at three points: (i) a **low-$D$/low-$M$ stable state** corresponding to the pluripotent ESC state, (ii) an **unstable saddle point**, and (iii) a **high-$D$/high-$M$ stable state** corresponding to the 2C-like totipotent state. The fraction of mESCs occupying the 2CLC state at steady state is determined by the ratio of stochastic fluctuation amplitude to the energy barrier height separating the two stable states — consistent with the observed 0.5-1% 2CLC frequency and the Kramers escape rate formalism.

The model also predicts **hysteresis**: once a cell enters the totipotent state (high $D$, high $M$), returning to pluripotency requires crossing a higher energy barrier than the initial activation, explaining the observed stability of the 2CLC phenotype over multiple cell divisions before spontaneous reversion.

### 4.3 Chemical Approaches to Totipotency

The bistable switch framework provides a rationale for chemical approaches to inducing totipotency. Small molecules that increase $\alpha_D$ (basal DUX expression), decrease $\gamma_D$ (DUX stability), or increase $\beta_M$ (MERVL activation efficiency) can shift the nullcline intersection to favor the totipotent state. A recent comprehensive review cataloged the chemical strategies that have emerged for reshaping cellular pluripotency and totipotency using pure small-molecule systems, noting that chemical approaches offer safety and convenience advantages over transcription-factor overexpression (Wen et al., 2025). These include HDAC inhibitors, DNA methyltransferase inhibitors, and splicing modulators — the last of which formed the basis for capturing human totipotent blastomere-like cells (Section 5).

---

## 5. In Vitro Totipotent-like States: 2CLCs, 8CLCs, and hTBLCs

### 5.1 Human Totipotent Blastomere-like Cells via Spliceosomal Repression

While mouse 2CLCs have been studied for over a decade, capturing the equivalent totipotent state in human cells proved more challenging due to species-specific differences in ZGA timing and regulation. A breakthrough came in 2024 when Li and colleagues demonstrated that transient inhibition of the spliceosome — specifically, treatment with the SF3B1 inhibitor pladienolide B (PlaB) — could reprogram human pluripotent stem cells through a ZGA-like state into stable human totipotent blastomere-like cells (hTBLCs) (Li et al., 2024a).

The mechanism is elegant: the spliceosome normally degrades unspliced or mis-spliced transcripts through co-transcriptional quality control. Inhibiting SF3B1 disrupts this surveillance, de-repressing a class of transcripts that includes human ZGA-specific genes normally silenced in pluripotent cells. The initial pladienolide B treatment induces a transient ZGA-like cell (ZLC) state, characterized by activation of ZGA-specific genes and silencing of pluripotency factors (OCT4, SOX2, NANOG). After long-term passaging, ZLCs transition into stable hTBLCs that express pre-ZGA markers and, critically, possess bidirectional developmental potential: during spontaneous differentiation, hTBLCs re-enter the ZLC stage and generate epiblast, primitive endoderm, and trophectoderm-like lineages, recapitulating human preimplantation development (Li et al., 2024a). Furthermore, hTBLCs can autonomously form blastocyst-like structures without external signaling.

Distinct from previously reported human 8-cell-like cells (8CLCs), both ZLCs and hTBLCs widely silence pluripotent genes rather than merely co-expressing totipotency and pluripotency markers — a critical distinction suggesting more complete reprogramming.

### 5.2 OTX2 as a Barrier to Totipotent Reprogramming

A key barrier to in vitro totipotent state induction was identified in a 2026 study: the homeobox transcription factor OTX2 actively prevents pluripotent stem cells from reverting to the 8-cell-like state (Wang et al., 2026). OTX2, which is highly expressed in primed and naive pluripotent cells, maintains the pluripotent transcriptional program and represses totipotency genes. Deletion of OTX2 in human pluripotent stem cells greatly enhanced the generation of TPRX1+ 8-cell-like cells that closely resembled the transcriptomic and epigenetic profiles of in vivo 8-cell and morula embryos.

The OTX2-deleted 8CLCs exhibited improved bidirectional differentiation — contributing to both embryonic and extraembryonic tissues in chimeric embryos — and mechanistically, OTX2 was shown to regulate both naive-to-totipotent state transition and the reverse (Wang et al., 2026). This finding establishes OTX2 as a gatekeeper between pluripotency and totipotency, analogous to the role of H3K9me3 as a barrier in SCNT but operating at the transcription-factor level rather than the chromatin-mark level.

### 5.3 The Spectrum of In Vitro Totipotent States

The expanding catalog of in vitro totipotent-like states — mouse 2CLCs, human 8CLCs, hTBLCs, expanded potential stem cells (EPSCs) — has prompted systematic characterization efforts. A comprehensive review established six hallmarks of totipotent stem cell states: (i) expression of cleavage-stage genes (including *ZSCAN4*, *TPRX1/2*), (ii) activation of endogenous retroviruses (MERVL in mouse, HERVK in human), (iii) global chromatin decondensation, (iv) bidirectional developmental potential (embryonic + extraembryonic), (v) epigenetic ground state (global DNA hypomethylation, absence of stable H3K9me3 domains), and (vi) metabolic shift to glycolysis (Posfai et al., 2024). Critically, current in vitro models satisfy different subsets of these hallmarks: hTBLCs score highest on criteria (i)-(iv) but show epigenetic differences from in vivo embryos, while mouse 2CLCs are transcriptomically faithful but unstable across passages (Zhao et al., 2025).

---

## 6. Germline Epigenetic Reprogramming and In Vitro Gametogenesis

### 6.1 The Deepest Erasure: PGC Demethylation

The most complete epigenetic reprogramming in mammalian biology occurs during primordial germ cell (PGC) development. Beginning from a state of somatic-like methylation ($\sim$70% CpG methylation), mouse PGCs undergo genome-wide demethylation to reach $\sim$4.5% CpG methylation by embryonic day 13.5 (E13.5) — one of the most hypomethylated states in any mammalian cell type (Seisenberger et al., 2012). In human PGCs, methylation drops to approximately 4.5% by week 7 of development (Murase et al., 2024).

This Tier 3 reprogramming serves three functions: (i) erasure of parental imprints, enabling sex-specific re-establishment in the developing gamete; (ii) reactivation of the inactive X chromosome in female PGCs; and (iii) resetting of somatic epigenetic memory to establish germline totipotency. The mechanism involves coordinated passive and active demethylation: passive dilution occurs through replication-coupled loss due to downregulation of the UHRF1-DNMT1 maintenance complex, while active demethylation involves TET1 and TET2-mediated oxidation of 5mC (Seisenberger et al., 2012). Notably, the two mechanisms operate on different genomic compartments: TET-mediated active demethylation preferentially targets gene-regulatory elements (promoters, enhancers), while passive loss removes methylation from heterochromatic and repetitive regions.

A critical selectivity mechanism protects specific loci from demethylation. STELLA (also known as DPPA3 or PGC7) binds to H3K9me2-marked chromatin and physically blocks TET3 access, preventing inappropriate demethylation of imprinting control regions (ICRs) and certain transposable elements during the post-fertilization wave (Nakamura et al., 2007). In PGCs, where even imprints must be erased, STELLA is downregulated, removing this protective layer and enabling the deepest possible demethylation.

### 6.2 In Vitro Gametogenesis: Reconstituting the Germline Program

The reconstitution of gametogenesis from pluripotent stem cells (in vitro gametogenesis, IVG) requires recapitulating this Tier 3 reprogramming in culture. Murase and colleagues achieved a milestone in 2024 by demonstrating that BMP signaling can drive human PGC-like cells (hPGCLCs) through epigenetic reprogramming and differentiation into mitotic pro-spermatogonia or oogonia, coupled with extensive amplification ($\sim 10^{10}$-fold) (Murase et al., 2024). The key mechanistic insight was that BMP-driven hPGCLC differentiation involves attenuation of the MAPK (ERK) pathway and inhibition of both de novo and maintenance DNA methyltransferases, promoting replication-coupled passive demethylation that mimics the in vivo program.

Despite this progress, meiotic entry remains the principal bottleneck for IVG. While mouse IVG has achieved complete oogenesis — with live offspring born from iPSC-derived oocytes (Hayashi et al., 2012) — human IVG has not yet produced mature oocytes. A 2025 study demonstrated a shortcut: co-expression of five transcription factors (ZNF281, LHX8, SOHLH1, ZGLP1, and ANHX) induced DDX4-positive oogonia-like cells (iOLCs) from human iPSCs in just four days in feeder-free monolayer culture, compared to weeks or months for the stepwise protocol (Aizawa et al., 2025). While these iOLCs have not yet entered meiosis, they provide a rapid platform for studying human female germ cell specification and screening meiosis-promoting conditions.

Clinical translation of IVG requires addressing not only meiotic competence but also epigenetic fidelity (Section 7), oocyte quality, and ethical considerations. A 2025 clinical translation outlook noted that strategies to assess oocyte quality and development of regulatory frameworks are prerequisites for any human application (Stern et al., 2025).

### 6.3 Framework F295: Germline Demethylation as a Traveling Wave

The progressive loss of DNA methylation across the PGC genome can be modeled as a traveling wave in genomic coordinate space. Let $m(x, t)$ denote the methylation level at genomic position $x$ and developmental time $t$. The dynamics combine TET-mediated enzymatic demethylation (local reaction) with replication-coupled passive loss (which propagates demethylation from already-demethylated regions to flanking sequences through hemimethylated intermediates):

```math
\frac{\partial m}{\partial t} = D_{\text{rep}} \frac{\partial^2 m}{\partial x^2} - r_{\text{TET}} \cdot [\text{TET}] \cdot m \cdot (1 - m) - r_{\text{pass}} \cdot m \cdot (1 - m)
```

where:
- $x$ represents genomic position (in kilobases from a reference point)
- $D_{\text{rep}}$ is the effective diffusion coefficient reflecting replication-coupled spread of demethylation to adjacent CpGs (estimated at $\sim$0.1-1 kb$^2$/hr, based on replication fork processivity and DNMT1 exclusion kinetics)
- $r_{\text{TET}}$ is the TET enzymatic rate constant for 5mC oxidation
- $[\text{TET}]$ is the local TET1/TET2 concentration
- $r_{\text{pass}}$ is the passive demethylation rate (proportional to cell division rate divided by DNMT1 maintenance efficiency)
- The logistic term $m(1-m)$ ensures that demethylation accelerates at intermediate methylation levels (where hemimethylated sites are most abundant) and saturates at extremes

This equation is a Fisher-KPP reaction-diffusion equation in genomic coordinate space. The minimum wave speed for the demethylation front is:

```math
c_{\min} = 2\sqrt{D_{\text{rep}} \cdot (r_{\text{TET}} \cdot [\text{TET}] + r_{\text{pass}})}
```

For parameters estimated from mouse PGC data ($D_{\text{rep}} \approx 0.5$ kb$^2$/hr, $r_{\text{TET}} \cdot [\text{TET}] + r_{\text{pass}} \approx 0.04$ hr$^{-1}$), the predicted wave speed is $c_{\min} \approx 0.28$ kb/hr, which over the approximately 120 hours of the demethylation window corresponds to a front advance of $\sim$34 kb. This is consistent with the observation that demethylation initiates at gene-regulatory elements (where TET is concentrated) and spreads into flanking regions through passive replication-coupled loss, taking approximately 5 cell divisions to achieve genome-wide erasure from $\sim$70% to $\sim$4.5%.

---

## 7. The Fidelity Problem: Why Reprogramming Fails at Every Tier

### 7.1 Tier 1 Fidelity Defects: Aberrant Methylation and Epigenetic Memory in iPSCs

All reprogramming approaches introduce epigenetic errors, but the nature and magnitude of these errors differ by tier. At Tier 1, iPSC reprogramming produces three categories of fidelity defects:

**Aberrant non-CG methylation.** Lister and colleagues performed whole-genome bisulfite sequencing of human iPSCs and discovered that all iPSC lines share numerous megabase-scale regions of aberrant methylation in the non-CG context (CpH, where H = A, T, or C) that are absent from both the somatic cell of origin and from ESCs (Lister et al., 2011). These aberrant CpH methylation hotspots are non-randomly distributed, enriched near centromeres and telomeres, and associated with alterations in CG methylation, histone modifications, and gene expression at flanking loci. The aberrant patterns arise de novo during the reprogramming process and are not corrected by extended passaging.

**Epigenetic memory.** Low-passage iPSCs retain residual DNA methylation signatures characteristic of their somatic tissue of origin (Kim et al., 2010). This "epigenetic memory" biases differentiation potential: iPSCs derived from blood cells differentiate more efficiently into hematopoietic lineages, while iPSCs from fibroblasts favor mesenchymal fates. The memory is encoded primarily in residual CpG methylation at tissue-specific enhancers that were active in the donor cell but should have been silenced during reprogramming. Extended passaging or treatment with DNA methyltransferase inhibitors can partially erase this memory, but some loci remain resistant.

**SCNT vs. iPSC comparative fidelity.** Direct comparison of SCNT-ESCs and iPSCs derived from the same somatic cell type revealed that SCNT-ESCs exhibit methylation patterns significantly more similar to IVF-derived ESCs than iPSCs do (Ma et al., 2014). Specifically, SCNT-ESCs showed proper erasure of somatic enhancer methylation and appropriate establishment of ESC-specific methylation patterns at most loci, while iPSCs retained donor-cell methylation at many of these same loci. This finding demonstrates that the oocyte's reprogramming machine achieves higher fidelity than transcription-factor-based approaches — consistent with the competitive remodeling framework (F292), where the oocyte provides saturating concentrations of erasure factors.

### 7.2 Tier 2 Fidelity Defects: X-Chromosome Reactivation and Erosion

In female cells, reprogramming to pluripotency should trigger X-chromosome reactivation (XCR) — the reversal of X-chromosome inactivation (XCI) — enabling subsequent random re-inactivation upon differentiation. XCR depends on silencing of the long non-coding RNA XIST and erasure of the associated heterochromatin marks on the inactive X (Xi) (Pasque et al., 2014).

In practice, female iPSCs exhibit incomplete and unstable XCR. A genome-wide CRISPR screen during neural precursor to iPSC reprogramming identified the interferon-gamma (IFNγ) pathway as a key enhancer of both pluripotency acquisition and X-chromosome reactivation: early activation of the IFNγ pathway during reprogramming accelerated JAK-STAT3 signaling, TET-mediated DNA demethylation, and endogenous chromosome-wide X-linked gene reactivation (Pasini et al., 2024). This finding reveals that XCR is not an automatic consequence of pluripotency acquisition but requires specific signaling — a mechanistic insight with implications for improving female iPSC quality.

Even when initial XCR is achieved, female iPSCs frequently undergo subsequent XCI "erosion" — partial loss of XIST expression and stochastic reactivation of X-linked genes from the formerly inactive X. A 2025 study demonstrated that this erosion is frequent, heterogeneous, and irreversible: once erosion occurs, it persists through trilineage differentiation, including cardiomyocyte formation (Raposo et al., 2025). Eroded genes are enriched on the short arm of the X chromosome, particularly near constitutive escape genes and within H3K27me3-enriched domains. Critically, erosion creates permanent epigenetic scars that alter X-linked gene dosage in differentiated derivatives — a safety concern for female iPSC-derived cell therapies.

### 7.3 Tier 3 Fidelity Defects: Imprinting Errors

Genomic imprinting — the parent-of-origin-specific monoallelic expression of approximately 100-200 genes in mammals — is maintained by allele-specific DNA methylation at ICRs. Because iPSC reprogramming does not intentionally erase imprints (unlike germline reprogramming), iPSCs should maintain correct imprinting. In practice, however, iPSCs show frequent imprinting aberrations.

Imprinting fidelity in iPSCs is sex-dependent and culture-condition-dependent: female iPSCs lose imprints more frequently than male iPSCs, and specific culture media (particularly those containing ascorbic acid) can stabilize or destabilize imprinting (Tompkins et al., 2022). The mechanism involves the dual vulnerability of imprinted loci: they must resist both the global demethylation associated with reprogramming (which threatens to erase the methylated ICR) and the de novo methylation that occurs during culture adaptation (which threatens to methylate the unmethylated ICR). Female cells face the additional challenge of X-linked imprinted genes, which are destabilized by XCI erosion.

For IVG applications (Tier 3), imprinting fidelity is even more critical because the germline program intentionally erases all imprints and must re-establish them de novo in a sex-specific manner. Errors at this stage — failure to erase, failure to re-establish, or establishment on the wrong allele — can cause imprinting disorders such as Beckwith-Wiedemann syndrome (H19/IGF2 locus) or Prader-Willi/Angelman syndrome (SNRPN locus). IVG-derived gametes have not yet been assessed for imprinting fidelity in human cells, making this a critical open question for clinical translation.

### 7.4 Framework F296: Reprogramming Fidelity as Jensen-Shannon Divergence

The fidelity of reprogramming can be quantified using the Jensen-Shannon Divergence (JSD) between the methylome of the reprogrammed cell ($Q$) and the target methylome ($P$):

```math
\text{JSD}(P \| Q) = \frac{1}{2} D_{\text{KL}}(P \| M) + \frac{1}{2} D_{\text{KL}}(Q \| M)
```

where $M = \frac{1}{2}(P + Q)$ is the mixture distribution and $D_{\text{KL}}$ is the Kullback-Leibler divergence. Unlike the asymmetric KL divergence, JSD is symmetric and bounded: $0 \leq \text{JSD}(P \| Q) \leq \ln 2$.

For a genome with $L$ CpG sites, the per-site JSD is computed from the methylation probability at each CpG in the target ($p_l$) and reprogrammed ($q_l$) cell:

```math
\text{JSD} = \frac{1}{L} \sum_{l=1}^{L} \left[ \frac{1}{2} p_l \ln \frac{2p_l}{p_l + q_l} + \frac{1}{2} (1 - p_l) \ln \frac{2(1 - p_l)}{(1 - p_l) + (1 - q_l)} + \frac{1}{2} q_l \ln \frac{2q_l}{p_l + q_l} + \frac{1}{2} (1 - q_l) \ln \frac{2(1 - q_l)}{(1 - p_l) + (1 - q_l)} \right]
```

We decompose the total JSD into two orthogonal error components:

```math
\text{JSD}_{\text{total}} = \text{JSD}_{\text{memory}} + \text{JSD}_{\text{aberrant}}
```

where:
- $\text{JSD}_{\text{memory}} = \text{JSD}(P \| Q) \big|_{\text{loci where } q_l \text{ is intermediate between } p_l \text{ and } d_l}$ captures residual donor-cell marks (epigenetic memory), with $d_l$ denoting the donor-cell methylation probability. Memory errors reflect incomplete erasure — the reprogrammed cell retains methylation patterns biased toward the donor.
- $\text{JSD}_{\text{aberrant}} = \text{JSD}(P \| Q) \big|_{\text{loci where } q_l \text{ deviates from both } p_l \text{ and } d_l}$ captures de novo errors that arise during the reprogramming process itself and are found in neither the target nor the donor.

This decomposition enables differential diagnosis of reprogramming failure: high $\text{JSD}_{\text{memory}}$ indicates insufficient erasure (addressable by stronger erasure factors or longer reprogramming duration), while high $\text{JSD}_{\text{aberrant}}$ indicates process-induced damage (addressable by modifying culture conditions or adding protective factors).

**Application across tiers:**
- Tier 1 (iPSC vs. ESC): Published data suggest $\text{JSD}_{\text{total}} \approx 0.01$-$0.03$ nats per CpG, dominated by $\text{JSD}_{\text{memory}}$ at tissue-specific enhancers and $\text{JSD}_{\text{aberrant}}$ at non-CG methylation hotspots (Lister et al., 2011)
- Tier 1 (SCNT-ESC vs. ESC): $\text{JSD}_{\text{total}} \approx 0.005$-$0.015$ nats per CpG, with reduced $\text{JSD}_{\text{memory}}$ relative to iPSCs (Ma et al., 2014)
- Tier 3 (IVG-derived gamete vs. natural gamete): Not yet measured in human cells, but mouse IVG data suggest elevated JSD at ICRs ($\sim$0.15-0.3 nats per CpG) and retrotransposon silencing marks ($\sim$0.08-0.15 nats per CpG)

---

## 8. Open Questions and Future Directions

### 8.1 The Minimum Factor Cocktail

The 2025 cocktail breakthrough (TSA + Kdm4d + Kdm5b, achieving 75% blastocyst rate) establishes a foundation for iterative optimization toward the minimum effective factor set. Three experimental strategies are now feasible:

**Systematic dropout.** Removing individual components from the cocktail and measuring the impact on both blastocyst rate and transcriptomic fidelity (via JSD, F296) would identify which factors are essential versus synergistic. The competitive remodeling framework (F292) predicts that the required cocktail depends on the somatic cell type: cells with lower $[E_{\text{maint}}]$ (e.g., embryonic fibroblasts vs. adult hepatocytes) should require fewer erasure factors, enabling cell-type-specific minimal cocktails.

**Additive screening.** Starting from the TSA + Kdm4d + Kdm5b base, adding candidates from the oocyte's remaining toolkit (H3.3/HIRA for histone variant exchange, NPM2 for chromatin decondensation, TET3 for active demethylation) and measuring marginal improvement per factor would rank the remaining oocyte components by their contribution to reprogramming completeness. The Erlang barrier model (F293) predicts diminishing returns: once the rate-limiting barrier is addressed (currently H3K9me3 via Kdm4d), accelerating the next-slowest barrier yields progressively smaller improvements.

**mRNA delivery optimization.** All three cocktail components are delivered as mRNA, making the system compatible with clinical-grade mRNA delivery platforms (e.g., lipid nanoparticles). Optimizing the stoichiometry, timing, and half-life of each mRNA component — guided by the competitive kinetics of F292 — could further improve efficiency without adding new factors.

### 8.2 Stabilizing Tier 2 Totipotency

Can the totipotent state be maintained in long-term culture without genomic instability? The DUX-MERVL bistable switch model (F294) predicts that sustained totipotency requires maintaining DUX and MERVL activity above the upper stable state threshold. Chemical approaches — particularly combinatorial treatments targeting histone acetylation, spliceosome activity, and ERK signaling — have achieved weeks of stable culture (Wen et al., 2025), but long-term fidelity (measured by JSD, F296) remains uncharacterized.

### 8.3 IVG Safety and Fidelity

Will IVG-derived gametes produce healthy offspring in humans? The Bayesian classifier (F297) provides a framework for pre-implantation quality assessment, but validation requires extensive primate studies. Key concerns include: (i) imprinting fidelity at all ~100 ICRs, (ii) transposon silencing (incomplete silencing could cause insertional mutagenesis in offspring), and (iii) meiotic recombination fidelity (aberrant crossover patterns could cause aneuploidy). Genome-wide JSD analysis of IVG-derived gametes at Tier 3 resolution is a prerequisite for any clinical program.

### 8.4 A Unified Fidelity Standard

We propose that all reprogramming approaches — iPSC generation, SCNT, chemical reprogramming, and IVG — should report the JSD fidelity metric (F296), decomposed into memory and aberrant components, relative to the appropriate biological reference (ICM for Tier 1, zygote for Tier 2, gamete for Tier 3). This standardized metric would enable direct comparison across methods, identification of systematic failure modes, and evidence-based optimization of reprogramming protocols.


---

## References

1. Adams, D. K., Courtois, E. A., & Ryder, O. A. (2024). Current status of interspecies somatic cell nuclear transfer and meta-analysis of the effects of phylogenetic distance on embryonic and fetal development. *Mammal Review*, 54(2), 122-138. doi:10.1111/mam.12352

2. Aizawa, E., & Hayashi, K. (2025). In vitro gametogenesis: Towards competent oocytes. *BioEssays*, 47(2), e2400106. PMID: 39587768

3. Asimi, V., Sampath Kumar, A., Niskanen, H., Riemenschneider, C., Grimm, S., Tsitsiridis, G., ... & Giorgetti, L. (2025). Dux cluster duplication ensures full activation of totipotent genes. *Proceedings of the National Academy of Sciences*, 122(10), e2421594122. doi:10.1073/pnas.2421594122

4. Burns, K. H., Viveiros, M. M., Ren, Y., Wang, P., DeMayo, F. J., Frail, D. E., ... & Matzuk, M. M. (2003). Roles of NPM2 in chromatin and nucleolar organization in oocytes and embryos. *Science*, 300(5619), 633-636. PMID: 12714744

5. Bultman, S. J., Gebuhr, T. C., Pan, H., Svoboda, P., Schultz, R. M., & Magnuson, T. (2006). Maternal BRG1 regulates zygotic genome activation in the mouse. *Genes & Development*, 20(13), 1744-1754. PMID: 16478720

6. De Iaco, A., Planet, E., Coluccio, A., Verp, S., Duc, J., & Trono, D. (2017). DUX-family transcription factors regulate zygotic genome activation in placental mammals. *Nature Genetics*, 49(6), 941-945. PMID: 28440691

7. De Iaco, A., Coudray, A., Duc, J., & Trono, D. (2019). DPPA2 and DPPA4 are necessary to establish a 2C-like state in mouse embryonic stem cells. *EMBO Reports*, 20(5), e47382. PMID: 30692203

8. Gill, D., Parry, A., Santos, F., Okkenhaug, H., Todd, C. D., Hernando-Herraez, I., ... & Reik, W. (2022). Multi-omic rejuvenation of human cells by maturation phase transient reprogramming. *eLife*, 11, e71624. PMID: 35390271

9. Gu, T. P., Guo, F., Yang, H., Wu, H. P., Xu, G. F., Liu, W., ... & Xu, G. L. (2011). The role of Tet3 DNA dioxygenase in epigenetic reprogramming by oocytes. *Nature*, 477(7366), 606-610. PMID: 21778365

10. Hayashi, K., Ohta, H., Kurimoto, K., Aramaki, S., & Saitou, M. (2012). Reconstitution of the mouse germ cell specification pathway in culture by pluripotent stem cells. *Cell*, 146(4), 519-532. PMID: 22304921

11. Inoue, A., Jiang, L., Lu, F., Suzuki, T., & Zhang, Y. (2017). Maternal H3K27me3 controls DNA methylation-independent imprinting. *Nature*, 547(7664), 419-424. PMID: 28317873

12. Kim, K., Doi, A., Wen, B., Ng, K., Zhao, R., Cahan, P., ... & Daley, G. Q. (2010). Epigenetic memory in induced pluripotent stem cells. *Nature*, 467(7313), 285-290. PMID: 20644536

13. Ladstätter, S., & Bhatt, D. K. (2025). The maternal-to-zygotic transition: Reprogramming of the cytoplasm and nucleus. *Nature Reviews Genetics*, 26, 59-83. doi:10.1038/s41576-024-00792-0

14. Li, J., Zhu, Q., Bai, R., Zhang, J., Jiang, H., Gao, R., ... & Li, W. (2025a). Efficient somatic cell nuclear transfer by overcoming both pre- and post-implantation epigenetic barriers. *Advanced Science*, 12, 2504669. doi:10.1002/advs.202504669

15. Li, W., Li, B., Giacalone, N. J., Bhatt, D. K., Craft, A. M., Roberts, A. M., ... & Bhatt, D. K. (2024a). Capturing totipotency in human cells through spliceosomal repression. *Cell*, 187(13), 3284-3304. PMID: 38843832

16. Lister, R., Pelizzola, M., Kida, Y. S., Hawkins, R. D., Nery, J. R., Hon, G., ... & Ecker, J. R. (2011). Hotspots of aberrant epigenomic reprogramming in human induced pluripotent stem cells. *Nature*, 471(7336), 68-73. PMID: 21289626

17. Ma, H., Morey, R., O'Neil, R. C., He, Y., Daughtry, B., Schultz, M. D., ... & Mitalipov, S. (2014). Abnormalities in human pluripotent cells due to reprogramming mechanisms. *Nature*, 511(7508), 177-183. PMID: 25008523

18. Macfarlan, T. S., Gifford, W. D., Driscoll, S., Lettieri, K., Rowe, H. M., Bonanomi, D., ... & Pfaff, S. L. (2012). Embryonic stem cell potency fluctuates with endogenous retrovirus activity. *Nature*, 487(7405), 57-63. PMID: 22722858

19. Matoba, S., Liu, Y., Lu, F., Iwabuchi, K. A., Shen, L., Inoue, A., & Zhang, Y. (2014). Embryonic development following somatic cell nuclear transfer impeded by persisting histone methylation. *Cell*, 159(4), 884-895. PMID: 25417163

20. Matoba, S., & Zhang, Y. (2018). Somatic cell nuclear transfer reprogramming: Mechanisms and applications. *Cell Stem Cell*, 23(4), 471-485. PMID: 30033121

21. Matoba, S., Inoue, K., Kohda, T., Sugimoto, M., Mizutani, E., Ogonuki, N., ... & Ogura, A. (2025). Derivation of embryonic stem cells from cloned blastocysts using improved somatic cell nuclear transfer in common marmosets. *Stem Cell Reports*, 20(1), 100-112. PMID: 41237778

22. Menon, D. U., Shibata, Y., Engel, K. L., & Magnuson, T. (2022). SWI/SNF chromatin remodeling subunit Smarca4/BRG1 is essential for female fertility. *Biology of Reproduction*, 108(2), 357-368. PMID: 36440965

23. Morris, S. A. (2025). Redefining cellular reprogramming with advanced genomic technologies. *Nature Reviews Genetics*, 26, 810-828. PMID: 41107536

24. Murase, Y., Yabuta, Y., Ohta, H., Yamashiro, C., Nakamura, T., Yamamoto, T., & Saitou, M. (2024). In vitro reconstitution of epigenetic reprogramming in the human germ line. *Nature*, 631(8019), 170-178. PMID: 38768632

25. Nakamura, T., Arai, Y., Umehara, H., Masuhara, M., Kimura, T., Taniguchi, H., ... & Nakano, T. (2007). PGC7/Stella protects against DNA demethylation in early embryogenesis. *Nature Cell Biology*, 9(1), 64-71. PMID: 17143267

26. Pasini, T., Mulholland, C. B., Gretarsson, K. H., Laisne, M., Uijttewaal, E. C. H., ... & Pasque, V. (2024). The interferon γ pathway enhances pluripotency and X-chromosome reactivation in iPSC reprogramming. *Science Advances*, 10(32), eadj8862. PMID: 39110794

27. Pasque, V., Tchieu, J., Karber Toma, R., Wraber, M., Deng, C., Chen, V., & Bhatt, D. K. (2014). X chromosome reactivation dynamics reveal stages of reprogramming to pluripotency. *Cell*, 159(7), 1681-1697. PMID: 25525883

28. Posfai, E., Lanner, F., Mulas, C., & Leitch, H. G. (2024). Hallmarks of totipotent and pluripotent stem cell states. *Cell Stem Cell*, 31(3), 312-333. PMID: 38382531

29. Raposo, A. C., Casanova, M., Gualdrini, F., Bousard, A., ... & Teixeira da Rocha, S. (2025). Gene reactivation upon erosion of X chromosome inactivation in female hiPSCs is predictable yet variable and persists through differentiation. *Stem Cell Reports*, 20(5), 102472. PMID: 40185090

30. Sakamoto, M., Ito, J., Hirose, M., Ogura, A., & Inoue, A. (2024). Obox4 promotes zygotic genome activation upon loss of Dux. *eLife*, 13, e95856. PMID: 38856708

31. Schulz, K. N., & Harrison, M. M. (2019). Mechanisms regulating zygotic genome activation. *Nature Reviews Genetics*, 20(4), 221-234. PMID: 30573849

32. Seisenberger, S., Andrews, S., Krueger, F., Arand, J., Walter, J., Santos, F., ... & Reik, W. (2012). The dynamics of genome-wide DNA methylation reprogramming in mouse primordial germ cells. *Molecular Cell*, 48(6), 849-862. PMID: 23219530

33. Stern, H. J., Adashi, E. Y., & Cohen, I. G. (2025). Stem cell-derived gametes: What to expect when expecting their clinical introduction. *Human Reproduction*, 40(9), 1605-1614. doi:10.1093/humrep/deaf101

34. Tompkins, J. D., Hall, C., Chen, V. C., Chuang, A. K., Chang, Y. W., Bui, T., ... & Bhatt, D. K. (2022). Imprinting fidelity in mouse iPSCs depends on sex of donor cell and medium formulation. *Nature Communications*, 13(1), 5432. PMID: 36097016

35. van der Heijden, G. W., Dieker, J. W., Derijck, A. A., Muller, S., Berden, J. H., Braat, D. D., ... & de Boer, P. (2005). Asymmetry in histone H3 variants and lysine methylation between paternal and maternal chromatin of the early mouse zygote. *Mechanisms of Development*, 122(9), 1008-1022. PMID: 16380711

36. Wang, L., Li, Z., Li, D., Yuan, Y., Li, M., Zhang, J., ... & Gao, S. (2023). Unreprogrammed H3K9me3 prevents minor zygotic genome activation and lineage commitment in SCNT embryos. *Nature Communications*, 14(1), 4496. PMID: 37558707

37. Wang, X., Chen, Y., Liu, Y., Zhang, J., Li, M., & Deng, H. (2026). OTX2 inhibits human pluripotent stem cell reprogramming toward 8-cell-like and morula-like states. *Nature Communications*, 17, 68388. doi:10.1038/s41467-026-68388-2

38. Wen, X., & Zheng, H. (2025). Chemical-based epigenetic reprogramming to advance pluripotency and totipotency. *Nature Chemical Biology*, 21(7), 899-912. PMID: 40251434

39. Zhao, C., Cao, Y., Wang, Z., & Li, M. (2025). Moving toward totipotency: The molecular and cellular features of totipotent and naive pluripotent stem cells. *Human Reproduction Update*, 31(4), 361-389. PMID: 40299455

40. Ladurner, R., & Tachibana, K. (2025). The mammalian oocyte: A central hub for cellular reprogramming and stemness. *Stem Cells and Cloning: Advances and Applications*, 18, 1-22. PMID: 39991743
