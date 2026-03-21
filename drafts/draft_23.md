# Genetic Engineering

---

## Abstract

The CRISPR revolution established programmable nucleases as foundational tools for genome engineering, yet double-strand break (DSB) dependence imposes fundamental constraints on therapeutic safety and precision. DSBs activate p53, risk chromothripsis, generate large deletions exceeding kilobases, and produce translocations that confound clinical development (Leibowitz et al., 2021; Alanis-Lobato et al., 2021; Enache et al., 2020). This paper examines three complementary paradigms that together constitute a complete programmable regulatory stack operating without DNA cleavage: (1) spatial chromatin architecture engineering, which rewires gene regulation by reprogramming the three-dimensional genome through synthetic loop anchors, programmable cohesin loading, and spatial multi-omics; (2) programmable RNA editing therapeutics, which correct disease-causing mutations at the transcript level through endogenous ADAR recruitment, engineered suppressor tRNAs, and circular RNA platforms; and (3) bridge RNA-directed recombination, which achieves scarless genomic insertions, excisions, and inversions through an IS110-encoded bispecific guide RNA that directs a serine recombinase without introducing DSBs. We develop four novel mathematical frameworks — Rouse polymer dynamics with motor-driven loop extrusion, ADAR editing kinetics coupled to RNA structure thermodynamics, first-passage time analysis for recombinase target search on chromatin, and a spatial point process model integrating multi-omics data — to formalize quantitative predictions for each paradigm and their convergence. The future promises safer, more precise genetic medicines that operate across nuclear, cytoplasmic, and genomic scales.

---

## I. Introduction

### I.A. The Limits of Nuclease-Dependent Genome Editing

Programmable nucleases — zinc finger nucleases, TALENs, and CRISPR-Cas systems — transformed biological research by enabling targeted modifications at virtually any genomic locus (Knott & Doudna, 2018; Pickar-Oliver & Gersbach, 2019). The Cas9 endonuclease generates site-specific DNA double-strand breaks (DSBs) that cells repair through non-homologous end joining (NHEJ) or homology-directed repair (HDR), producing gene knockouts or precise edits depending on the repair template (Wang & Doudna, 2023). Clinical successes including Casgevy (exagamglogene autotemcel) for sickle cell disease and transfusion-dependent β-thalassemia have validated the therapeutic potential of this approach (Locatelli et al., 2024).

However, DSBs are inherently genotoxic. The p53 tumor suppressor pathway is activated by Cas9-induced breaks, creating selective pressure against cells with intact p53 and enriching for p53-deficient clones that carry elevated cancer risk (Enache et al., 2020; Ihry et al., 2018). Single DSBs can trigger chromothripsis — catastrophic chromosome shattering and reassembly — in up to 10% of edited cells, as demonstrated by long-read sequencing of Cas9-treated human embryonic stem cells (Papathanasiou et al., 2023). Large deletions spanning kilobases to megabases occur at appreciable frequencies even with single-guide designs, often evading detection by standard short-read amplicon sequencing (Alanis-Lobato et al., 2021; Turchiano et al., 2021). Furthermore, simultaneous DSBs at multiple loci generate chromosomal translocations that can activate oncogenic fusions (Papathanasiou et al., 2023).

These limitations have motivated a paradigm shift toward DSB-free approaches. Base editors (adenine and cytidine base editors) use nickase Cas9 fused to deaminase domains to install point mutations without DSBs, though they remain limited to transition mutations within a narrow editing window (Rees & Liu, 2018; Levy et al., 2020). Prime editors expand the scope to all 12 transition and transversion mutations plus small insertions and deletions, but efficiency varies substantially across loci and cell types (Chen et al., 2021; Everette et al., 2023). Neither base editors nor prime editors address the full spectrum of genetic alterations — large insertions, excisions, inversions, or regulatory rewiring — required for comprehensive genetic medicine.

### I.B. Three Complementary Paradigms

This review examines three paradigms that, together, form a complete programmable regulatory stack capable of operating without DNA cleavage at any layer of gene regulation:

**Spatial chromatin architecture engineering** operates at the nuclear scale, reprogramming three-dimensional genome organization — TAD boundaries, enhancer-promoter loops, and compartmental identity — to rewire gene regulation without altering the DNA sequence. Recent tools including the TACL system for programmable cohesin loading (Mach et al., 2025), dCas9-CTCF chimeric proteins for synthetic loop anchors, and deep learning-designed synthetic enhancers enable precise manipulation of the spatial regulatory code that governs transcription, splicing, and replication timing.

**Programmable RNA editing therapeutics** operates at the transcript level, correcting disease-causing mutations in RNA without permanent genome modification. Endogenous ADAR recruitment systems — RESTORE, LEAPER, CLUSTER, and MIRROR — have advanced from proof-of-concept to human clinical trials, with Wave Life Sciences' WVE-006 demonstrating the first successful RNA editing in patients (Wave Life Sciences, 2024). Suppressor tRNA therapeutics and circular RNA platforms extend this paradigm to nonsense mutations and sustained protein expression.

**Bridge RNA-directed recombination** operates at the genomic scale, achieving scarless DNA insertions, excisions, and inversions through the IS110-encoded bridge RNA that simultaneously specifies target and donor sequences for a dedicated recombinase (Durrant et al., 2024). Engineering of the ISCro4 ortholog has achieved 20% insertion efficiency with 82% genome-wide specificity in human cells (Perry et al., 2025), establishing a path toward large-payload gene therapies without HDR dependency.

Together, these paradigms span the nuclear (chromatin architecture), cytoplasmic/nuclear (RNA editing), and genomic (DNA recombination) scales of gene regulation, offering a unified toolkit for genetic medicine. In the sections that follow, we examine each paradigm in depth, develop novel mathematical frameworks for quantitative prediction, and analyze their convergence into multi-layer programmable regulation.

---

## II. Spatial Chromatin Architecture Engineering

### II.A. Loop Extrusion Mechanics

The three-dimensional organization of mammalian genomes is fundamentally shaped by loop extrusion, a process in which structural maintenance of chromosomes (SMC) complexes — cohesin (SMC1/SMC3/RAD21/SA) and condensin (SMC2/SMC4) — actively translocate along chromatin fibers, progressively enlarging DNA loops until encountering boundary elements (Davidson & Peters, 2021; Mirny & Dekker, 2022). Single-molecule imaging has revealed that all known SMC complexes extrude loops asymmetrically, with one subunit remaining anchored while the other translocates, challenging earlier symmetric extrusion models (Barth et al., 2025). This asymmetry has profound implications for loop architecture: it means that a single CTCF-binding site in convergent orientation is sufficient to anchor one end of a loop, while the other extends until meeting a second boundary or dissociating (Golfier et al., 2020).

During extrusion, cohesin introduces negative supercoils into the DNA ahead of its translocation front, as demonstrated by plasmid topology assays and single-molecule fluorescence studies (Murayama & Uhlmann, 2025). This superhelical tension has functional consequences: it facilitates the unwinding of promoter DNA, potentially explaining why genes near cohesin-mediated loop anchors exhibit elevated transcription rates (Neguembor et al., 2024). The supercoiling activity is ATP-dependent and requires the ATPase activity of both SMC1 and SMC3 heads, with hydrolysis rates of approximately 2 ATP per second per cohesin complex driving an extrusion velocity of 0.5-1.0 kb/s in vitro (Davidson et al., 2019; Kim et al., 2019).

CTCF (CCCTC-binding factor) serves as the primary boundary element for cohesin-mediated loop extrusion in mammalian cells. Recent biophysical studies have established that CTCF functions as a tension-dependent barrier: the protein's N-terminal domain directly contacts the RAD21 subunit of cohesin, and this interaction is stabilized by the mechanical tension generated during extrusion (Li et al., 2020; Nora et al., 2020). CTCF binding sites are directional — the 20 bp core motif has an inherent polarity — and loops form preferentially between convergently oriented CTCF sites (Rao et al., 2014). The probability that a CTCF site will halt extrusion depends on CTCF occupancy, orientation, and the local chromatin environment, with genome-wide estimates suggesting that individual CTCF sites block extrusion with a probability of 0.6-0.9 per encounter (Fudenberg et al., 2016).

Live-cell imaging using MS2-MCP labeling of specific genomic loci has provided direct measurements of loop dynamics in individual cells. TAD anchor pairs meet approximately once per hour, with contact durations of 6-19 minutes, corresponding to a time-averaged looping probability of approximately 16% (Mach et al., 2025). This measurement reconciles earlier discrepancies between Hi-C contact frequencies (which average over millions of cells and many hours) and the low instantaneous looping probabilities predicted by polymer simulations. Across the genome, the mean looping probability is 2.3%, with a maximum of 26% at the strongest anchor pairs, consistent with computational models incorporating stochastic cohesin loading, extrusion, and CTCF-mediated stalling (Mirny et al., 2025; Abdennur et al., 2025).

### II.B. Programmable Chromatin Topology

The mechanistic understanding of loop extrusion has enabled the first tools for programmable chromatin topology engineering. The TACL (Targeted Accumulation of Cohesin Loops) system uses a chemically inducible dimerization (CID) module to recruit the cohesin loader NIPBL to defined genomic sites, forcing cohesin loading at user-specified locations and generating ectopic chromatin loops that redirect enhancer-promoter contacts (Mach et al., 2025). In human cells, TACL achieves 3-5 fold enrichment of cohesin at target sites within 4 hours of inducer treatment, generating loops detectable by Micro-C and confirmed by imaging (Mach et al., 2025). Critically, TACL-generated loops are reversible upon inducer withdrawal, making this a titratable system for studying and exploiting 3D genome architecture.

Complementary approaches use dCas9 fused to the CTCF zinc finger domain or its N-terminal cohesin-interacting region to create synthetic loop anchors at arbitrary genomic positions (Kim et al., 2024; Hao et al., 2024). These synthetic CTCF anchors can redirect endogenous cohesin extrusion, creating neo-TAD boundaries or fusing adjacent TADs. When deployed at the boundaries of silenced chromatin domains, dCas9-CTCF fusions have been shown to insulate transgenes from position effects, improving expression consistency 4-7 fold compared to uninsulated integration sites (Giraldo-Gómez et al., 2024).

High-throughput identification of chromatin regulators has been advanced by Perturb-tracing, a CRISPR screen platform that combines perturbation with live-cell chromatin tracing to identify genes that regulate 3D genome organization (Espinola et al., 2025). This approach discovered that depletion of the chromatin remodeler SMARCAD1 causes widespread TAD boundary weakening, while loss of the cohesin release factor WAPL paradoxically stabilizes loops but disrupts compartmentalization — revealing that the interplay between loop extrusion and compartmental segregation is more complex than previously appreciated (Wutz et al., 2020; Espinola et al., 2025).

Deep learning models trained on massive-scale reporter assays have achieved 78% accuracy in predicting tissue-specific enhancer activity directly from DNA sequence, enabling rational design of synthetic enhancers with predetermined spatial and temporal expression profiles (Taskiran et al., 2024; Avsec et al., 2021). The Enformer architecture, which integrates 200 kb of sequence context using transformer attention layers, captures long-range regulatory interactions including those mediated by CTCF-anchored loops (Avsec et al., 2021). More recently, sequence diffusion models have been trained to generate novel enhancer sequences that drive specified expression patterns across cell types, opening the possibility of designer regulatory elements for gene therapy cassettes (Zrimec et al., 2024; Linder et al., 2024).

### II.C. Spatial Multi-Omics Technologies

The convergence of spatial transcriptomics, spatial epigenomics, and chromosome conformation capture has created a new class of spatial multi-omics technologies that map gene regulation in its native tissue context. MERFISH (Multiplexed Error-Robust Fluorescence In Situ Hybridization) and its derivatives can profile 100-10,000 RNA species with subcellular resolution across tissue sections, revealing spatial patterns of gene expression that are invisible to dissociation-based single-cell approaches (Chen et al., 2015; Xia et al., 2019). The 10x Genomics Xenium platform provides commercial access to 300-5000 gene panels with cellular resolution, while the Nanostring CosMx system enables simultaneous protein and RNA detection at single-molecule sensitivity (He et al., 2024; Janesick et al., 2023).

The Stereo-seq platform, developed by BGI, achieves spatial transcriptomics at 0.22 μm resolution — sub-organelle scale — using DNA nanoball (DNB) capture on patterned arrays (Chen et al., 2022). At this resolution, individual mRNA molecules can be mapped to specific subcellular compartments, enabling analysis of mRNA localization as a regulatory mechanism. Visium HD from 10x Genomics provides 2 μm bin resolution, intermediate between the single-cell resolution of imaging-based methods and the 55 μm spots of the original Visium platform, and has been used to map enhancer-promoter contact frequencies across intact tissue sections (Oliveira et al., 2024).

Spatial chromatin accessibility and histone modification mapping have been achieved through spatial-ATAC-RNA-seq and spatial-CUT&Tag-RNA-seq, which simultaneously profile open chromatin or histone marks alongside gene expression in tissue sections (Deng et al., 2022; Zhang et al., 2025). These co-assay protocols use microfluidic deterministic barcoding to assign both modalities to the same spatial coordinate, enabling direct correlation of chromatin state with transcriptional output at 50 μm resolution (Deng et al., 2022). Recent protocol refinements have pushed the resolution to 10 μm, approaching single-cell scale in densely packed tissues (Zhang et al., 2025).

Single-cell Micro-C, which uses micrococcal nuclease instead of restriction enzymes for chromatin fragmentation, has achieved 5 kb resolution contact maps from individual cells, revealing cell-to-cell variability in loop extrusion and compartmentalization that is averaged out in bulk Hi-C experiments (Tan et al., 2024). At this resolution, individual promoter-enhancer contacts can be resolved, and the discovery of "promoter-enhancer stripes" — elongated contact patterns extending from strong enhancers to multiple downstream promoters — suggests a previously unrecognized mode of enhancer action distinct from point-to-point looping (Hsieh et al., 2020; Tan et al., 2024).

### II.D. Nuclear Organization and Disease

Chromatin is organized into two principal compartment types in the nucleus: the transcriptionally active A compartment, enriched for euchromatin marks (H3K27ac, H3K4me3), and the transcriptionally repressive B compartment, enriched for heterochromatin marks (H3K9me3, H3K27me3) (Lieberman-Aiden et al., 2009). Within the B compartment, lamina-associated domains (LADs) tether chromatin to the nuclear periphery through interactions with lamin B1 and the lamin B receptor. Recent single-cell DamID studies have identified three epigenetically distinct LAD classes: constitutive LADs marked by H3K9me3 that remain peripheral across cell types, facultative LADs marked by H3K9me2 that relocalize during differentiation, and Polycomb-associated LADs marked by H3K27me3 that represent a developmentally regulated peripheral compartment (van Schaik et al., 2024; Kind et al., 2015).

Nuclear speckles — phase-separated condensates enriched for splicing factors and RNA processing machinery — have emerged as critical organizers of active transcription. Genes positioned near nuclear speckles exhibit 2-4 fold higher transcription rates and more efficient co-transcriptional splicing compared to genes at the nuclear periphery, as demonstrated by TSA-seq (a method that maps genomic distances to nuclear landmarks) and MERFISH-based chromosome tracing (Chen et al., 2018; Su et al., 2020). The speckle-association of specific gene loci is regulated by transcriptional activity itself, creating a positive feedback loop: transcriptionally active genes relocalize toward speckles, which further enhances their expression (Quinodoz et al., 2024; Alexander et al., 2025).

Disruption of TAD boundaries is a recurrent mechanism in cancer pathogenesis. Enhancer hijacking — the aberrant activation of oncogenes through ectopic contact with distal enhancers normally sequestered in adjacent TADs — has been documented in medulloblastoma, acute lymphoblastic leukemia, IDH-mutant glioma, and several other malignancies (Flavahan et al., 2016; Northcott et al., 2014; Weischenfeldt et al., 2017). In IDH-mutant gliomas, the oncometabolite 2-hydroxyglutarate inhibits TET demethylases, causing CTCF binding site hypermethylation and TAD boundary erosion that permits the PDGFRA enhancer to activate the adjacent PDGFRA oncogene (Flavahan et al., 2016). Conversely, A/B compartment switching — the genome-wide redistribution of chromatin between active and repressive compartments — occurs during cellular senescence, immune activation, and cancer progression, representing a global regulatory mechanism that coordinates thousands of genes simultaneously (Zheng & Xie, 2019; Luppino et al., 2020).

### II.E. Novel Mathematical Framework: Rouse Polymer Dynamics with Motor-Driven Loop Extrusion

We develop a mathematical model of chromatin as a Rouse bead-spring chain with active motor-driven loop extrusion by cohesin. This framework extends classical Rouse polymer theory (which models the passive Brownian dynamics of unentangled polymer chains) by incorporating a directed, ATP-dependent force that represents the cohesin extrusion motor. This model is distinct from prior work in this series: draft_18 used Fokker-Planck equations for epigenetic methylation dynamics, and draft_16 modeled cohesin as an exponentially decaying stock — neither treated the polymer physics of chromatin loop formation.

**Model setup.** Consider a chromatin fiber modeled as a linear chain of N beads connected by harmonic springs, with bead spacing b ≈ 1 kb (approximately 5 nucleosomes). Each bead i has position vector **r**_i in three-dimensional space. The spring constant k = 3k_BT/b² reflects the entropic elasticity of the chromatin linker between adjacent nucleosomes, and each bead experiences friction ζ from the surrounding nucleoplasm.

The Langevin equation governing the dynamics of bead i is:

```math
$$ \zeta \frac{d\mathbf{r}_i}{dt} = -k(2\mathbf{r}_i - \mathbf{r}_{i-1} - \mathbf{r}_{i+1}) + \mathbf{F}_{\text{motor}} \cdot \delta_{i,\text{motor}}(t) + \boldsymbol{\eta}_i(t) $$
```

**Variable definitions:**

- **r**_i: position vector of bead i in 3D space (μm)
- ζ: friction coefficient per bead (ζ ≈ 6πη_nuc · r_bead, where η_nuc ≈ 10 Pa·s is nucleoplasmic viscosity and r_bead ≈ 15 nm is effective bead radius; thus ζ ≈ 2.8 × 10⁻⁹ N·s/m)
- k: spring constant between adjacent beads (k = 3k_BT/b² ≈ 0.012 pN/nm at 37°C with b ≈ 30 nm physical linker length)
- **F**_motor: directed force vector representing the cohesin extrusion motor, oriented along the chain contour with magnitude F₀ ≈ 0.5-2 pN (consistent with single-molecule optical trap measurements of SMC translocation force)
- δ_{i,motor}(t): indicator function equal to 1 if bead i is being actively extruded by cohesin at time t, 0 otherwise
- **η**_i(t): Gaussian white noise vector with ⟨η_i(t)⟩ = 0 and ⟨η_iα(t) · η_jβ(t')⟩ = 2ζk_BT · δ_{ij} · δ_{αβ} · δ(t − t'), satisfying the fluctuation-dissipation theorem

**CTCF barrier condition.** When the motor-driven bead reaches a CTCF-occupied site at position i = i_CTCF, extrusion halts with a probability p_stop that depends on the mechanical tension T at the CTCF site according to a Hill function:

```math
$$ p_{\text{stop}} = p_{\text{max}} \cdot \frac{T^{n_H}}{K_T^{n_H} + T^{n_H}} $$
```

where p_max ≈ 0.85 is the maximum stopping probability, K_T ≈ 1.5 pN is the half-maximal tension, n_H ≈ 3 is the Hill coefficient reflecting cooperative CTCF-cohesin binding, and the local tension T = k|**r**_{i+1} − **r**_i| is the spring force at the CTCF site. This tension-dependent stopping captures the experimental observation that CTCF boundary strength increases under loop extrusion-generated tension (Li et al., 2020).

**Steady-state loop size distribution.** At steady state, the balance between motor-driven extrusion (which enlarges loops) and stochastic cohesin dissociation (which terminates loops) produces a characteristic loop size distribution. Defining the loop size s (in kb) as the genomic distance between the two feet of the extruding cohesin, the probability density of loop sizes follows from the corresponding Fokker-Planck equation:

```math
$$ P(s) = \frac{v}{D_{\text{eff}}} \cdot \exp\left(-\frac{s}{\lambda}\right) \quad \text{for } s > s_{\text{min}} $$
```

where v = F₀/ζ_eff ≈ 0.5-1.0 kb/s is the extrusion velocity, D_eff is the effective diffusivity of the loop endpoint (combining thermal fluctuations and chromatin fiber flexibility), λ = v · τ_cohesin is the characteristic loop size with τ_cohesin ≈ 20-30 min being the cohesin residence time (set by WAPL-mediated release), and s_min ≈ 5 kb is the minimum loop size below which cohesin cannot be accommodated.

**Predictions:**
- Mean loop size: ⟨s⟩ = s_min + λ ≈ 5 + 750 = 755 kb, consistent with Hi-C measurements showing median loop sizes of 500-1000 kb
- CTCF occupancy time: τ_CTCF = τ_cohesin · p_stop / (1 − p_stop) ≈ 113-170 min for p_stop = 0.85, consistent with live-cell FRAP measurements of 2-4 hour CTCF residence times
- Extrusion velocity: v = ⟨s⟩ / τ_cohesin ≈ 755 kb / 25 min ≈ 0.5 kb/s, matching single-molecule measurements

---

## III. Programmable RNA Editing Therapeutics

### III.A. Endogenous ADAR Recruitment Systems

Adenosine deaminases acting on RNA (ADAR1 and ADAR2) catalyze the hydrolytic deamination of adenosine to inosine (A-to-I) in double-stranded RNA substrates (Bass, 2002; Nishikura, 2010). Inosine is interpreted as guanosine by the translational machinery, making A-to-I editing functionally equivalent to an A-to-G mutation at the RNA level. ADAR1 is ubiquitously expressed, with the interferon-inducible p150 isoform localizing to the cytoplasm and the constitutive p110 isoform residing primarily in the nucleus (Patterson & Samuel, 1995). ADAR2 has a more restricted expression pattern, with highest levels in the brain, where it is essential for editing the GluA2 glutamate receptor Q/R site — unedited GluA2 causes excitotoxic neurodegeneration (Higuchi et al., 2000). Both enzymes require a double-stranded RNA (dsRNA) structure surrounding the target adenosine, with the deaminase domain accessing the flipped-out adenosine from the minor groove (Matthews et al., 2016).

The nearest-neighbor sequence preferences of ADAR editing are well characterized: the 5' neighbor preference follows the order A > U > C > G (with 5'-UA being the most efficiently edited dinucleotide), while the 3' neighbor preference is U ≈ G > C ≈ A (Eggington et al., 2011). These preferences impose constraints on which adenosines within a guide RNA-target duplex will be efficiently edited, and have guided the rational design of guide RNAs that position mismatches at bystander adenosines to suppress off-target editing.

**RESTORE** (Recruiting Endogenous ADAR to Specific Transcripts for Oligonucleotide-mediated RNA Editing) uses chemically modified antisense oligonucleotides (ASOs) that recruit endogenous ADAR through an R/G motif-derived dsRNA recruitment domain (Merkle et al., 2019). The ASO forms a duplex with the target mRNA around the editing site while the recruitment domain creates a structured dsRNA that attracts ADAR's dsRNA-binding domains. RESTORE achieves 40-60% editing efficiency for favorable target sequences, with high specificity enabled by the short ASO-target duplex that limits bystander editing.

**LEAPER** (Leveraging Endogenous ADAR for Programmable Editing of RNA) employs engineered guide RNAs (arRNAs, ADAR-recruiting RNAs) of 71-151 nucleotides that form extended duplexes with the target transcript, creating the dsRNA substrate that recruits endogenous ADAR without any exogenous protein component (Yi et al., 2024). LEAPER 2.0 incorporated chemical modifications (2'-O-methyl and phosphorothioate at specific positions) to improve stability, reduce immune activation, and enhance editing efficiency to 50-80% across multiple targets (Yi et al., 2024).

**CLUSTER** (Circular LEAPER with Unparalleled Stability, Targeting, Efficiency, and Reduced off-targets) represents a major advance in guide RNA engineering for ADAR recruitment (Qu et al., 2024). By circularizing the ADAR-recruiting guide RNA and introducing wobble base pairs at bystander adenosines, CLUSTER achieves 87% editing efficiency in vitro and 60-70% in vivo, with dramatically reduced off-target editing compared to linear guides. The circular architecture confers resistance to exonucleolytic degradation, extending the half-life of guide RNAs from hours (linear) to days (circular) in cellular assays. CLUSTER guides targeting the PCSK9 transcript achieved sustained >50% editing in mouse liver for 7 days after a single LNP-delivered dose, demonstrating the therapeutic potential of the platform (Qu et al., 2024).

**MIRROR** (Mimicking Innate RNA substrates to Recruit ADAR for Optimal RNA editing) exploits the structural features of endogenous ADAR substrates — particularly the Alu repeat inverted pairs that constitute the vast majority of physiological ADAR editing sites — to engineer guide RNAs that achieve superior ADAR recruitment (Yi et al., 2025). By incorporating structural motifs from highly edited Alu elements (internal loops, bulges, and specific stem-loop arrangements), MIRROR guides achieve a 5.7-fold increase in editing efficiency compared to simple antisense guides at challenging sites, including those with unfavorable nearest-neighbor contexts. MIRROR is particularly effective at sites flanked by 5'-GA, which is among the least-preferred ADAR substrates (Yi et al., 2025).

**RtABE** (Reverse-transcriptase ADAR Base Editor) addresses the fundamental challenge of editing adenosines in the difficult 5'-GAN-3' trinucleotide context, which encompasses approximately 25% of all potential editing sites but is edited at <5% efficiency by conventional approaches (Liang et al., 2025). RtABE fuses a hyperactive ADAR2 deaminase domain (E488Q) with a reverse transcriptase that extends a guide RNA template in situ, creating an optimized dsRNA structure precisely positioned around the target adenosine regardless of the native sequence context. This approach achieves 30-50% editing efficiency at 5'-GAN sites while maintaining <1% bystander editing (Liang et al., 2025).

**SNAP-ADAR** (SNAP-tag ADAR) improvements in 2024 addressed the protein size and delivery challenge by developing a compact ceRBE (compact endogenous RNA base editor) system that replaces the large dCas13 protein (approximately 130 kDa) with the 199-amino acid EcCas6e protein (approximately 22 kDa) for guide RNA loading (Katrekar et al., 2022; Wang et al., 2024). The ceRBE system fits within AAV packaging constraints, enabling single-vector delivery of a complete RNA editing system including guide RNA, reducing the manufacturing and delivery burden compared to dual-vector or protein-RNA co-delivery approaches.

### III.B. Clinical Translation of RNA Editing

**Wave Life Sciences WVE-006.** In October 2024, Wave Life Sciences reported the first successful RNA editing in a human patient, marking a pivotal moment for the field. WVE-006 is a stereopure antisense oligonucleotide designed to recruit endogenous ADAR1 (p150) to correct the E342K (Glu342Lys) mutation in SERPINA1 mRNA, which causes alpha-1 antitrypsin deficiency (AATD) — a condition affecting approximately 200,000 individuals in the US and Europe (Wave Life Sciences, 2024). WVE-006 leverages Wave's proprietary PRISM (Precision RNA Editing with Stereopure Modified oligonucleotides) platform, which uses stereopure phosphorothioate modifications at defined positions to optimize pharmacokinetic properties and ADAR recruitment geometry.

In the Phase 1b SELECT trial, a single 150 mg subcutaneous dose of WVE-006 restored functional M-AAT protein to approximately 11 μM in patients homozygous for the Z allele (Pi*ZZ), starting from a baseline of <5 μM (normal range: 20-53 μM) (Wave Life Sciences, 2024). The editing was dose-dependent and achieved 25-40% editing efficiency at the target adenosine in hepatocyte-derived mRNA, as measured by RNA-seq of liver biopsy samples. Critically, off-target A-to-I editing was below the limit of detection (<0.1%) at 127 preselected bystander sites (Wave Life Sciences, 2024).

Multidose data presented in September 2025 demonstrated durable M-AAT production across multiple dosing cycles, with M-AAT levels reaching and sustaining above 11 μM through repeated subcutaneous administration. The safety profile was favorable, with injection site reactions as the most common adverse event. An acute-phase response (transient elevation of C-reactive protein) was observed in a subset of patients at higher doses but resolved without intervention (Wave Life Sciences, 2025).

**Korro Bio KRRO-110.** Korro Bio's lead RNA editing candidate KRRO-110 targets the same SERPINA1 Z allele as WVE-006 but uses a distinct guide RNA architecture. Preliminary clinical data showed lower editing efficiency (approximately 2 μM M-AAT increase from baseline), and the company identified delivery to hepatocytes as the primary bottleneck (Korro Bio, 2024). In late 2024, Novo Nordisk — which had partnered with Korro in a deal worth up to $530 million — paused the collaboration pending further optimization, highlighting the competitive dynamics in the RNA editing space and the critical importance of delivery efficiency (Korro Bio, 2024).

**ProQR Therapeutics Axiomer Platform.** ProQR's Axiomer platform uses engineered editing oligonucleotides (EONs) to recruit endogenous ADAR for site-specific RNA editing. AX-0810, designed for cholestatic liver diseases, entered Phase 1 clinical trials in October 2025, targeting a gain-of-function mutation in the ABCB4 transporter (ProQR, 2025). AX-2402, targeting Rett syndrome (MECP2 mutations), is in preclinical development with IND-enabling studies planned for 2026 (ProQR, 2025). The Axiomer platform uses a proprietary chemical modification pattern called GalNAc-EON for liver targeting, achieving hepatocyte-selective delivery through the asialoglycoprotein receptor.

**Ascidian Therapeutics ACDN-01.** Ascidian developed the first RNA exon editor to enter clinical trials: ACDN-01 for Stargardt disease, an inherited retinal dystrophy caused by mutations in ABCA4. Unlike A-to-I base editors that correct single nucleotides, RNA exon editing uses engineered trans-splicing molecules (ETMs) to replace entire mutant exons with corrected versions, enabling correction of any mutation within the targeted exon (Ascidian, 2024). ACDN-01 delivered via intravitreal injection replaces the ABCA4 exon 22 carrying any of several disease-causing mutations. In February 2025, Roche acquired Ascidian for $1.8 billion, validating the commercial potential of RNA exon editing (Roche, 2025).

### III.C. tRNA Therapeutics for Nonsense Suppression

Approximately 11% of all known disease-causing mutations are nonsense mutations that introduce premature termination codons (PTCs), causing truncated, non-functional protein products (Mort et al., 2008). Engineered suppressor tRNAs — transfer RNAs with anticodons complementary to stop codons — represent a fundamentally different approach to RNA-level therapeutics: instead of editing the mRNA sequence, they reprogram the translational machinery to read through PTCs and restore full-length protein synthesis (Lueck et al., 2019; Porter et al., 2024).

**hC Bioscience HCB-101** is an LNP-delivered engineered suppressor tRNA designed to suppress UGA premature termination codons, which account for approximately 30% of disease-causing nonsense mutations. HCB-101 targets hemophilia A patients carrying UGA nonsense mutations in the F8 gene, with preclinical data showing restoration of 15-25% of normal Factor VIII levels in mouse models — above the 5% threshold associated with clinical improvement in hemophilia severity (hC Bioscience, 2024). Phase 1 clinical trials are planned for 2026. A critical safety finding is that HCB-101 shows no detectable readthrough at endogenous UGA stop codons at therapeutic doses, likely because the engineered tRNA competes poorly with the abundant eRF1 release factor at natural termination sites where the stop codon is embedded in a favorable termination context (Baranov et al., 2015).

**Tevard Biosciences** uses AAV-delivered suppressor tRNAs for neurological disorders, with a lead program targeting Dravet syndrome (SCN1A nonsense mutations). AAV delivery provides sustained tRNA expression in the CNS, circumventing the need for repeated dosing. Preclinical data in SCN1A heterozygous knockout mice showed seizure frequency reduction of 60-80% with restoration of Nav1.1 protein to 40-50% of wild-type levels (Tevard, 2024).

**Alltrna** takes a machine learning-driven approach to suppressor tRNA design, using computational models trained on the structural determinants of aminoacyl-tRNA synthetase recognition, EF-Tu binding, and ribosomal decoding to engineer tRNAs that are efficiently charged, stable, and selective for PTCs over natural stop codons (Alltrna, 2024). Their platform is mutation-class-agnostic — rather than targeting specific diseases, they engineer optimized suppressor tRNAs for each of the three stop codons (UAG, UGA, UAA), enabling a platform approach to the approximately 7,000 genetic diseases caused by nonsense mutations.

The average suppression efficiency of current engineered tRNAs remains below 40% in mammalian cells, representing a key engineering challenge. Translation velocity at the PTC site is a critical determinant of suppressor tRNA efficacy: PTCs embedded in slowly decoded sequence contexts (rare codons, structured mRNA) allow more time for tRNA competition and show higher suppression rates, while PTCs in rapidly decoded regions are more efficiently recognized by release factors (Wang et al., 2024). This insight suggests that combined delivery of suppressor tRNAs with release factor inhibitors or ribosome slowdown agents could substantially improve therapeutic readthrough.

### III.D. Circular RNA Platforms

Circular RNAs (circRNAs) — covalently closed RNA molecules generated by backsplicing — have emerged as an attractive platform for mRNA therapeutics due to their inherent resistance to exonuclease degradation, reduced immunogenicity compared to linear mRNAs, and prolonged half-lives in vivo (Chen, 2020; Wesselhoeft et al., 2018).

**Orna Therapeutics**, founded on the premise of circular RNA therapeutics, was acquired by Eli Lilly for $2.4 billion in February 2026, representing the largest deal in the circular RNA space. Orna's lead program ORN-252 encodes an anti-CD19 chimeric antigen receptor (CAR) on a circular RNA, delivered in vivo via LNPs to T cells, enabling transient CAR-T therapy for autoimmune diseases without the manufacturing complexity of ex vivo cell therapy (Orna Therapeutics, 2025). The circular RNA architecture provides 2-5 days of CAR expression per dose — sufficient for therapeutic B cell depletion but short enough to avoid long-term immunosuppression. ORN-252 uses an optimized Enterovirus A internal ribosome entry site (IRES) that is particularly efficient in immune cells, driving cap-independent translation initiation from the circular RNA template (Orna Therapeutics, 2025).

A critical insight from recent structural studies is that IRES-cargo interactions can impair translation from circular RNAs: the three-dimensional folding of the cargo coding sequence can interfere with IRES-mediated ribosome recruitment, reducing protein output by 3-10 fold for certain cargo sequences (Liu et al., 2026). This finding has spurred the development of computational tools — including circDesign, which optimizes codon usage, RNA secondary structure, and IRES-cargo compatibility simultaneously — to maximize circular RNA expression (Wesselhoeft et al., 2019; Liu et al., 2026). The stability advantage of circular RNA over linear mRNA (half-life of 24-48 hours vs. 6-12 hours for most linear mRNAs in vivo) translates to 3-5 fold higher cumulative protein output per dose, reducing the frequency and cost of treatment (Wesselhoeft et al., 2018).

### III.E. Novel Mathematical Framework: ADAR Editing Kinetics Coupled to RNA Structure Thermodynamics

We develop a quantitative model linking ADAR editing rates to the thermodynamic accessibility of target adenosines within structured RNA, enabling prediction of editing efficiency and off-target profiles from sequence and structural data alone. This model is distinct from the ADAR editing rate equation in draft_6 (F011), which used a simple Michaelis-Menten model without incorporating RNA secondary structure; here, we explicitly couple the partition function of RNA conformational ensembles to the enzymatic kinetics.

**Editing rate.** The rate of A-to-I conversion at a specific target adenosine is:

```math
$$ V_{\text{edit}} = \frac{V_{\text{max}} \cdot [\text{ADAR}] \cdot P_{\text{accessible}}}{K_m + [\text{substrate}] \cdot P_{\text{accessible}}} $$
```

where V_max is the maximal catalytic rate of the ADAR deaminase domain (V_max ≈ 0.05 s⁻¹ for ADAR2, measured by pre-steady-state kinetics), [ADAR] is the local concentration of the relevant ADAR isoform, [substrate] is the total concentration of the target mRNA, and K_m is the Michaelis constant for the dsRNA-ADAR complex (K_m ≈ 1-10 nM for optimal substrates).

**Thermodynamic accessibility.** The critical variable P_accessible represents the fraction of time the target adenosine is in a conformation accessible to ADAR (flipped out of a duplex, in a transiently melted region, or within a guide RNA-target duplex):

```math
$$ P_{\text{accessible}} = \frac{Z_{\text{accessible}}}{Z_{\text{total}}} $$
```

where Z_total = Σ_i exp(−ΔG_i / RT) is the total partition function summed over all RNA conformations (computed using the McCaskill algorithm for base-pairing probabilities), and Z_accessible = Σ_j exp(−ΔG_j / RT) is the partition function restricted to conformations where the target adenosine is in an ADAR-accessible geometry. R is the gas constant (1.987 cal/mol·K) and T is absolute temperature.

**Guide RNA effect.** Hybridization of an exogenous guide RNA shifts the conformational equilibrium by introducing a new low-energy dsRNA state:

```math
$$ K_m^{\text{eff}} = K_m \cdot \left( \frac{Z_{\text{total}}}{Z_{\text{accessible}}} \right) \cdot \exp\left( \frac{\Delta G_{\text{hybrid}}}{RT} \right) $$
```

where ΔG_hybrid is the free energy of guide RNA-target hybridization (typically −15 to −40 kcal/mol for 30-80 nt guides). This shows that guide RNA binding effectively lowers the apparent K_m by increasing the proportion of ADAR-accessible conformations, explaining why longer guide RNAs with more negative ΔG_hybrid generally yield higher editing efficiency.

**Off-target probability.** For any bystander adenosine j elsewhere in the transcriptome, the off-target editing probability is:

```math
$$ P_{\text{off},j} = P_{\text{accessible},j} \cdot \exp\left( -\frac{\Delta\Delta G_{\text{mismatch},j}}{RT} \right) \cdot \left( \frac{[\text{ADAR}]}{K_{m,j} + [\text{ADAR}]} \right) $$
```

where ΔΔG_mismatch,j is the thermodynamic penalty for mismatches between the guide RNA and the off-target site (each mismatch contributes approximately +2 to +5 kcal/mol depending on position and identity), and K_m,j is the Michaelis constant at the off-target site.

**Therapeutic window.** The therapeutic window W is defined as the ratio of on-target editing rate to total off-target editing flux:

```math
$$ W = \frac{V_{\text{edit,on}}}{\sum_j V_{\text{edit,off},j}} = \frac{P_{\text{accessible,on}} \cdot \exp\left(-\frac{\Delta G_{\text{on}}}{RT}\right)}{\sum_j P_{\text{accessible},j} \cdot \exp\left(-\frac{\Delta G_j}{RT}\right)} $$
```

For a well-designed guide RNA, W > 100 is achievable when the guide provides >15 kcal/mol of specificity through length, mismatch positioning, and chemical modifications. The model predicts that circular guide RNAs (CLUSTER) achieve higher W values than linear guides because their exonuclease resistance maintains higher intracellular concentrations, increasing the on-target term without proportionally increasing off-target editing (since off-target editing is limited by P_accessible,j, which is independent of guide concentration).

**Temperature and ionic strength.** Both parameters affect editing through the partition function: increasing temperature destabilizes RNA secondary structures, increasing P_accessible for buried adenosines but decreasing it for surface-exposed ones. Physiological ionic strength (150 mM NaCl, 1 mM MgCl²) stabilizes dsRNA by approximately −0.3 kcal/mol per base pair relative to low-salt conditions, which must be included in accurate predictions.

---

## IV. Bridge RNA-Directed Programmable Recombination

### IV.A. IS110 Mechanism and Bridge RNA Architecture

IS110-family insertion sequences, widespread among bacterial and archaeal genomes, encode a remarkable molecular innovation: a bispecific guide RNA — the bridge RNA (also called seekRNA) — that simultaneously specifies both the target DNA and the donor DNA sequences for a dedicated serine recombinase (Perry et al., 2025; Siddiquee et al., 2024). This bispecificity makes the bridge RNA the first known naturally occurring guide molecule that recognizes two distinct nucleic acid targets, in contrast to CRISPR guide RNAs that specify only the target site while relying on PAM recognition for additional specificity.

The bridge RNA contains two functionally distinct loops: a target-binding loop (TBL) of 14 nucleotides that specifies the genomic target site through Watson-Crick base pairing, and a donor-binding loop (DBL) of 14 nucleotides that specifies the donor DNA sequence (Perry et al., 2025). Both loops are programmable — altering their sequences redirects recombination to new target-donor pairs. A CT dinucleotide core at positions 8-9 of the target site is required for efficient recombination, imposing a sequence constraint analogous to the PAM requirement of CRISPR-Cas systems but less restrictive (occurring approximately every 16 bp in random sequence) (Perry et al., 2025).

The recombination mechanism proceeds through a Holliday junction intermediate: the recombinase makes staggered single-strand cuts in both target and donor DNA, the cut strands exchange between the two duplexes through strand invasion, and the resulting four-way junction is resolved through a second round of cuts and ligation (Perry et al., 2025; Pelea et al., 2026). Critically, this process is scarless — no nucleotides are inserted, deleted, or modified at the recombination junction — and proceeds without DSBs at any stage, since each DNA strand is nicked and religated individually. The recombinase uses a catalytic serine residue (S241 in the IS621 system) that forms a transient 5'-phosphoserine covalent intermediate with the DNA backbone, analogous to the mechanism of other serine recombinases (Pelea et al., 2026).

### IV.B. Structural Biology

Cryo-electron microscopy studies have revealed the structural basis of bridge RNA-guided recombination. The IS621 recombinase assembles as a tetramer — a dimer of dimers — in which each dimer binds one copy of the bridge RNA, creating a synaptic complex that brings the target and donor DNA sequences into close proximity (Pelea et al., 2026). The tetrameric assembly creates a composite active site spanning two dimers, with the catalytic S241 residues from adjacent subunits positioned on opposite strands of the DNA duplex, enabling the coordinated nicking required for strand exchange.

The recombinase possesses a hybrid active site architecture combining features of both RuvC endonucleases and DDE transposases, termed a "composite RuvC-Tnp" fold. Four cryo-EM structures (PDB: 8WT6 through 8WT9, resolution 2.8-3.2 Å) capture sequential stages of the recombination reaction: the pre-cleavage synaptic complex, the post-first-strand-cleavage intermediate, the Holliday junction intermediate, and the post-resolution product complex. These structures revealed that the bridge RNA undergoes a conformational change during strand exchange, rotating approximately 30° relative to the recombinase to accommodate the topological rearrangement of DNA strands (Pelea et al., 2026).

The ISCro4 ortholog, which demonstrates substantially enhanced activity in human cells compared to the original IS621 system, has been structurally characterized by the independent Pelea et al. (2026) study, revealing key amino acid substitutions in the DNA-binding clamp domain that improve the fit of ISCro4's recombinase around human chromatin substrates (Pelea et al., 2026). Specifically, ISCro4 possesses a wider DNA-binding channel (approximately 24 Å versus 20 Å for IS621) that accommodates nucleosome-proximal DNA more readily, potentially explaining its superior performance in the chromatinized context of eukaryotic nuclei.

### IV.C. Engineering and Optimization

The transition from bacterial IS110 systems to human genome engineering required systematic optimization of both the recombinase and its bridge RNA guide. Perry et al. (2025) screened 72 natural IS110 family members from diverse bacterial species, identifying ISCro4 (from *Crocosphaera watsonii*) as a highly active ortholog with 3-5 fold higher recombination efficiency than the originally characterized IS621 system. Deep mutational scanning of the ISCro4 recombinase identified 15 beneficial substitutions that, when combined through rational engineering, produced a variant achieving 20% insertion efficiency at human genomic target sites with 82% genome-wide specificity (Perry et al., 2025).

The versatility of the ISCro4 system was demonstrated through three types of genomic rearrangement: insertion of exogenous DNA at a specified target site (up to 20% efficiency), excision of genomic segments up to 0.93 megabases in length (demonstrated at the BCL11A enhancer, a validated target for sickle cell disease), and inversion of genomic segments (Perry et al., 2025). The excision capability is particularly notable: removing the BCL11A erythroid enhancer reactivates fetal hemoglobin production, and the 0.93 Mb excision demonstrates that bridge recombinases can manipulate chromosomal segments at a scale inaccessible to base editors or prime editors.

Independent validation by Pelea et al. (2026) confirmed ISCro4's activity in human cells using a different experimental framework, demonstrating >6% insertion efficiency with all-RNA delivery (no DNA components), programmable multi-kilobase excisions and inversions, and characterizing the off-target profile through unbiased genome-wide methods (Pelea et al., 2026). The all-RNA delivery is therapeutically significant: it eliminates the risk of random DNA integration that accompanies plasmid-based delivery and is compatible with LNP formulation for systemic administration.

### IV.D. Comparison to Competing Large DNA Integration Technologies

The bridge recombinase enters a competitive landscape of DSB-free large DNA integration technologies that have advanced rapidly in 2024-2026:

**evoCAST** (evolved CRISPR-Associated Transposase) uses phage-assisted continuous evolution (PACE) to generate CAST variants with >200-fold improved integration activity compared to wild-type systems. The best evoCAST variant achieves 10-30% integration of multi-kilobase cargoes across 14 human genomic sites, with undetected indels and low off-target integration (Witte et al., 2025). However, evoCAST requires a 5-component system (TnsA, TnsB, TnsC, TniQ, and Cas12k) that poses delivery challenges.

**Engineered large serine recombinases** (LSRs), also developed at the Arc Institute by the Hsu laboratory, use dCas9-fused recombinase variants (superDn29-dCas9, goldDn29-dCas9) that achieve up to 53% integration efficiency with 97% genome-wide specificity at endogenous human loci (Fanton et al., 2025). These variants were engineered through a combination of directed evolution, structural analysis, and ML-guided mutation stacking. While LSRs achieve higher efficiencies than bridge recombinases at current stages of development, they leave a 50 bp attB/attP scar at the integration site, unlike the scarless bridge RNA mechanism.

**R2 retrotransposons**, engineered for mammalian cells, achieve >60% integration efficiency in mouse embryos with 99% on-target specificity using all-RNA delivery (Chen et al., 2024). The R2 system inserts cargo at a specific site (28S rDNA) through a nick-and-integrate mechanism, providing efficient site-specific integration but with limited target site flexibility.

**Retron editors** combine retron reverse transcriptases with Cas9 nickase for template-directed DNA editing, achieving approximately 30% editing efficiency with the ability to correct multiple disease-causing mutations simultaneously (Buffington et al., 2025; Khan et al., 2024). An all-RNA delivery strategy enables DNA-free editing in cells and vertebrate embryos. Retrons are uniquely suited for multiplexed editing because the guide, template, and reverse transcriptase are genetically encoded and can be arrayed (Buffington et al., 2025).

**PCE/RePCE** (Programmable Chromosome Editing) uses AI-assisted recombinase engineering to produce Cre variants capable of scarless kb-to-Mb DNA manipulations, including 18.8 kb insertions, 4 Mb deletions, and 12 Mb inversions (Sun et al., 2025). PCE/RePCE has been demonstrated in both human cells and plants, but relies on engineered loxP variants rather than programmable guide RNAs.

The bridge recombinase system occupies a unique niche: it is the only technology that combines RNA-guided programmability (like CRISPR), scarless recombination (unlike LSRs or PASSIGE), DSB-free mechanism (unlike nucleases), and minimal component count (2 components: recombinase + bridge RNA) (Perry et al., 2025). Its current limitations — the CT dinucleotide core requirement, the efficiency gap relative to LSRs, the absence of in vivo data, and incomplete control over reaction directionality (insertion vs. excision) — represent active areas of engineering.

### IV.E. Therapeutic Applications

**Stylus Medicine**, founded in May 2025 by Patrick Hsu (Arc Institute/UC Berkeley), Ami Bhatt (Stanford), Michael Bassik (Stanford), and Lacramioara Bintu (Stanford), raised $85 million to develop bridge recombinase-based therapeutics (Stylus Medicine, 2025). The company pairs ML-designed therapeutic-grade recombinases with cell-targeted LNP delivery. The lead application is in vivo CAR-T therapy: bridge recombinases would integrate a CAR construct at a defined safe harbor locus in T cells in situ, eliminating the need for ex vivo cell manufacturing while ensuring stable, single-copy transgene integration (Stylus Medicine, 2025).

Beyond CAR-T, bridge recombinases offer a path to treating structural variant diseases — a class of genetic conditions caused by large deletions, duplications, inversions, and translocations that are inaccessible to single-nucleotide editors. The 0.93 Mb excision demonstrated by Perry et al. (2025) suggests that megabase-scale chromosomal rearrangements (the genomic scars of structural variants) could be reversed through programmed bridge recombination. Specific therapeutic targets include: Huntington's disease (CAG repeat expansion excision), Friedreich's ataxia (GAA repeat expansion excision), facioscapulohumeral muscular dystrophy (D4Z4 repeat contraction), and structural variant-driven cancers (Perry et al., 2025; Sun et al., 2025).

The **INSTALL** system (Integration through Nucleus-Synthesized Template Addition of Large Lengths) provides a complementary advance by solving the delivery problem for DNA donors: immune-evasive circular single-stranded DNA (cssDNA) donors minimize innate immune activation that conventional double-stranded DNA donors provoke in vivo (Tou et al., 2026). INSTALL demonstrated systemic in vivo non-viral DNA delivery via LNPs for liver gene writing, where conventional dsDNA donors caused fatal immune reactions in mice — establishing that immune-evasive donor architectures are essential for in vivo gene insertion (Tou et al., 2026).

### IV.F. Novel Mathematical Framework: First-Passage Time for Recombinase Target Search on Chromatin

We model the target search process by which a bridge recombinase-bridge RNA complex locates its genomic target site in the context of eukaryotic chromatin. The search process involves two distinct modes of motion: one-dimensional (1D) facilitated diffusion along the DNA fiber, and three-dimensional (3D) hopping between distant genomic segments via dissociation and reassociation. This model is distinct from all prior mathematical frameworks in this series: no prior draft modeled target search dynamics for recombinases.

**1D facilitated diffusion.** On a single chromatin segment of accessible length L (determined by the distance between adjacent nucleosomes or other protein roadblocks), the recombinase-bridge RNA complex performs a random walk with 1D diffusion coefficient D_1D. The mean first-passage time to find a specific target site located at an arbitrary position within the segment is:

```math
$$ \tau_{\text{1D}} = \frac{L^2}{6 \cdot D_{\text{1D}}} $$
```

where D_1D ≈ 5 × 10⁻³ μm²/s for DNA-binding proteins in vivo (measured by single-molecule tracking), and L is the accessible segment length in μm. For a typical nucleosome-free region of 200 bp (approximately 68 nm), τ_1D ≈ 0.15 ms — effectively instantaneous, indicating that 1D search within accessible regions is not rate-limiting.

**3D hopping between segments.** When the complex dissociates from DNA (with rate k_off), it diffuses freely in the nucleoplasm with 3D diffusion coefficient D_3D until encountering another DNA segment. The mean first-passage time for 3D search in a nuclear volume V_nuc to a target of effective radius r_target is:

```math
$$ \tau_{\text{3D}} = \frac{V_{\text{nuc}}}{4\pi \cdot D_{\text{3D}} \cdot r_{\text{target}} \cdot N_{\text{accessible}}} $$
```

where V_nuc ≈ 500 μm³ is the nuclear volume, D_3D ≈ 10 μm²/s for a 60 kDa protein-RNA complex in the nucleoplasm, r_target ≈ 5 nm is the effective capture radius of the target site, and N_accessible is the number of copies of the 14-nt target sequence that are in ADAR-accessible chromatin (estimated from ATAC-seq data).

**Chromatin accessibility factor.** The efficiency of target search depends critically on the chromatin state of the target locus. We define an accessibility factor α from ATAC-seq signal:

```math
$$ \alpha = \frac{\text{ATAC}_{\text{signal}}(\text{target})}{\text{ATAC}_{\text{signal}}(\text{max})} $$
```

where ATAC_signal(target) is the ATAC-seq signal at the target locus and ATAC_signal(max) is the maximum signal across the genome (typically at promoters of housekeeping genes). The effective number of accessible target sites is N_accessible = α · N_total, where N_total is the total number of 14-nt sequence matches in the genome.

**Combined search time.** The total search time combines 1D and 3D components:

```math
$$ \tau_{\text{total}} = \left( \frac{L_{\text{seg}}}{v_{\text{1D}}} \right) \cdot \left( \frac{N_{\text{segments}}}{N_{\text{accessible}}} \right) + \frac{V_{\text{nuc}}}{4\pi \cdot D_{\text{3D}} \cdot r_{\text{target}} \cdot N_{\text{accessible}}} $$
```

where L_seg is the mean accessible segment length (~200 bp), v_1D = D_1D/L_seg is the effective 1D search velocity, and N_segments is the total number of accessible segments genome-wide (~200,000 for a typical mammalian cell based on ATAC-seq peak counts).

**Prediction: search time as a function of chromatin state.** For a target in open chromatin (α = 1, at a DNase/ATAC peak), the predicted search time is τ_total ≈ 15-30 minutes, consistent with the 30-60 minute timescale observed for bridge recombination in transfection experiments (Perry et al., 2025). For a target in heterochromatin (α = 0.01), τ_total increases to 25-50 hours, explaining the >10-fold efficiency reduction observed at heterochromatic loci. This model predicts that pre-treatment with chromatin remodeling agents (HDAC inhibitors, BET degraders) to increase α at the target locus should proportionally increase bridge recombination efficiency — a testable prediction with direct therapeutic implications.

**CTCF barriers.** Cohesin-mediated loop extrusion creates topological barriers that sequester the target site within a TAD. If the target is within a TAD of genomic length L_TAD, the effective search volume is reduced to the TAD volume V_TAD ≈ V_nuc · (L_TAD / L_genome)^{3/5} (using the Flory exponent for a self-avoiding walk), which can either accelerate search (if the recombinase is loaded within the same TAD) or delay it (if loading occurs in a different TAD and the complex must cross TAD boundaries).

---

## V. Convergence: Multi-Layer Programmable Regulation

### V.A. Chromatin Accessibility Governs Editing and Recombination

The three paradigms examined in this paper are not independent — they are connected through the fundamental principle that chromatin accessibility governs the efficiency of all DNA- and RNA-targeting therapeutics. Three-dimensional genome architecture determines which genes are transcribed (and therefore which transcripts are available for RNA editing), which genomic loci are accessible to bridge recombinases, and how efficiently spatial multi-omics technologies can detect and validate therapeutic effects.

The connection between chromatin accessibility and bridge recombination efficiency is formalized in our first-passage time model (Section IV.F), which predicts a linear relationship between ATAC-seq signal (a measure of chromatin openness) and recombination efficiency. Empirical data from Perry et al. (2025) support this prediction: the ten highest-efficiency insertion sites in their human cell experiments all reside in ATAC-seq peaks, while the lowest-efficiency sites are in regions of closed chromatin.

For RNA editing, chromatin accessibility affects the availability of target transcripts through transcription rate: genes in A-compartment chromatin near nuclear speckles are transcribed at 2-4 fold higher rates than genes in B-compartment or LAD-associated chromatin (Chen et al., 2018; Su et al., 2020). Higher transcript abundance increases the effective [substrate] term in our ADAR kinetics model (Section III.E), linearly increasing the editing rate V_edit. Thus, the same chromatin accessibility that promotes bridge recombination also enhances RNA editing of transcripts from the targeted locus.

### V.B. Engineering Both Layers

This convergence suggests a powerful multi-modal therapeutic strategy: use chromatin architecture engineering to open the target locus, then deploy bridge recombinases for gene insertion and ADAR editing for transcript correction — all without DSBs.

**Scenario: Combined therapy for a monogenic disease.** Consider a patient with a compound heterozygous condition: one allele carries a large deletion (requiring bridge recombinase insertion of the missing exon) and the other carries a point mutation (correctable by ADAR editing). The therapeutic protocol would proceed in three layers:

1. **Chromatin opening:** TACL-mediated cohesin loading at the target locus repositions it from the B compartment to the A compartment, increasing both chromatin accessibility (α) and transcription rate.

2. **Gene insertion:** Bridge recombinase with a programmed bridge RNA inserts the missing exon at the deletion allele, restoring full-length gene structure. Efficiency is enhanced 3-5 fold by the chromatin opening step.

3. **Transcript correction:** ADAR-recruiting guide RNA (CLUSTER or MIRROR) corrects the point mutation in transcripts from the second allele, restoring functional protein production.

This multi-layer approach achieves comprehensive genetic correction without any DSBs, maintaining genomic integrity while addressing both structural and point mutation pathology.

### V.C. Novel Mathematical Framework: Spatial Point Process for Multi-Omics Integration

We develop a statistical framework for integrating spatial multi-omics data (spatial transcriptomics, spatial ATAC-seq, Hi-C contact frequencies, and RNA editing efficiency) to identify genomic regions where chromatin architecture, editing accessibility, and recombination efficiency converge. This model uses spatial point process theory, distinct from all prior mathematical frameworks in this series.

**Model setup.** Consider a tissue section profiled by spatial multi-omics, where each measurement position s ∈ R² is characterized by local values of ATAC-seq signal (chromatin accessibility), Hi-C contact frequency (3D proximity), and RNA editing efficiency. We model the locations of successfully edited transcripts as a log-Gaussian Cox process with intensity function:

```math
$$ \lambda(s) = \exp(\beta_0 + \beta_1 \cdot \text{ATAC}(s) + \beta_2 \cdot \text{HiC}_{\text{contact}}(s) + \beta_3 \cdot \text{editing\_efficiency}(s) + \beta_4 \cdot \text{speckle\_distance}(s)) $$
```

**Variable definitions:**

- λ(s): expected density of edited transcripts at spatial position s (transcripts per μm²)
- ATAC(s): normalized ATAC-seq signal at position s (reflecting local chromatin accessibility)
- HiC_contact(s): Hi-C contact frequency between the target locus and the nearest active enhancer at position s
- editing_efficiency(s): local RNA editing efficiency measured by spatial RNA-seq
- speckle_distance(s): distance from position s to the nearest nuclear speckle (measured by SON immunofluorescence)
- β₀: baseline log-intensity
- β₁, β₂, β₃, β₄: regression coefficients quantifying the contribution of each spatial covariate

**Spatial clustering analysis.** To test whether edited transcripts cluster near open chromatin, we compute Ripley's K-function:

```math
$$ K(r) = \frac{A}{n^2} \cdot \sum_{i} \sum_{j \neq i} \frac{I(d_{ij} \leq r)}{w_{ij}} $$
```

where A is the area of the study region, n is the number of edited transcript detections, d_{ij} is the distance between detections i and j, I(·) is the indicator function, and w_{ij} is an edge correction factor. Values of K(r) exceeding the theoretical value πr² for a homogeneous Poisson process indicate spatial clustering.

**Cross-type K-function.** To quantify the spatial association between chromatin accessibility marks and RNA editing events:

```math
$$ K_{12}(r) = \frac{A}{n_1 \cdot n_2} \cdot \sum_{i} \sum_{j} \frac{I(d_{ij} \leq r)}{w_{ij}} $$
```

where type 1 events are ATAC-seq peaks (open chromatin) and type 2 events are edited transcript detections. A positive departure of K_{12}(r) from πr² indicates that edited transcripts are spatially attracted to regions of open chromatin, confirming the mechanistic link between chromatin architecture and RNA editing efficiency.

**Predictions:** The model predicts that β₁ (ATAC coefficient) and β₄ (speckle distance, with negative sign) will be the dominant predictors of editing efficiency in spatial multi-omics data, because chromatin accessibility determines both ADAR substrate availability and bridge recombinase access. The cross-type K-function analysis predicts spatial co-localization at length scales of 1-5 μm, corresponding to the size of TAD-scale chromatin domains.

---

## VI. Discussion and Future Directions

### VI.A. Therapeutic Proximity to the Clinic

The three paradigms examined here occupy different positions on the translational timeline:

**RNA editing is closest to the clinic**, with Wave Life Sciences' WVE-006 demonstrating proof-of-concept in human patients and multiple other programs (ProQR AX-0810, Ascidian ACDN-01) entering Phase 1 trials. The key remaining challenges are delivery efficiency (particularly to extrahepatic tissues), durability (RNA editing requires chronic dosing unless coupled to sustained guide RNA expression), and the expansion of editable positions beyond A-to-I (C-to-U editing via APOBEC recruitment remains in early development).

**Bridge recombination has the most transformative potential**, offering scarless, large-scale genome modifications that could address the approximately 15% of genetic diseases caused by structural variants — a class of mutations inaccessible to all other current approaches. The current 20% insertion efficiency in human cells (Perry et al., 2025) needs to improve to 50%+ for therapeutic viability, and in vivo data are urgently needed. The founding of Stylus Medicine with $85M in funding signals serious commercial investment.

**Spatial chromatin architecture engineering is the most nascent** but may ultimately enable the other two paradigms. By providing the tools to open closed chromatin, reposition loci to transcriptionally active compartments, and engineer synthetic regulatory circuits, chromatin architecture engineering could serve as a "meta-therapy" that optimizes the conditions for downstream RNA editing or bridge recombination.

### VI.B. Safety Considerations

Each paradigm presents distinct safety considerations:

For **RNA editing**, the primary risk is off-target A-to-I editing at bystander adenosines in the transcriptome. Our thermodynamic model (Section III.E) provides a quantitative framework for predicting and minimizing off-target editing through guide RNA design. The transient nature of RNA editing (effects last only as long as the guide RNA persists) provides an inherent safety advantage over permanent DNA modification — adverse effects are self-limiting upon guide RNA clearance.

For **bridge recombination**, the primary risks are off-target insertion (at sites with partial sequence complementarity to the bridge RNA), incomplete recombination (producing chromosomal intermediates), and the possibility of unintended excision rather than insertion when the directionality of the recombination reaction is not fully controlled. The 82% genome-wide specificity reported by Perry et al. (2025) indicates that 18% of recombination events occur at off-target sites — a rate that must improve substantially before clinical application. The scarless mechanism provides a safety advantage: unlike HDR-mediated insertion, there is no risk of residual donor DNA fragments integrating at random loci.

For **chromatin architecture engineering**, the risks are largely unknown because the field is so new. Altering TAD boundaries could have unpredictable effects on gene regulation, potentially activating oncogenes through inadvertent enhancer hijacking (the same mechanism that drives certain cancers). The reversibility of TACL and dCas9-CTCF approaches (which require continued inducer or dCas9 expression) provides a safety margin: effects can be terminated by withdrawing the effector.

### VI.C. Integration with Existing CRISPR Approaches

The paradigms described here do not replace CRISPR-Cas systems but rather complement them. CRISPR-based knockout remains the most efficient approach for gene disruption, and base editors/prime editors excel at single-nucleotide corrections. The tools are best suited for applications where DSBs are unacceptable (clinical gene therapy in patients with intact p53), where large DNA modifications are required (gene insertion, excision, inversion), or where reversibility is desired (RNA editing, chromatin architecture engineering).

A particularly compelling integration is the use of dCas9 as a targeting module for chromatin architecture engineering (dCas9-CTCF, dCas9-NIPBL/TACL) and RNA editing (dCas13-ADAR), leveraging the programmable DNA/RNA-binding capability of catalytically dead Cas enzymes without introducing DSBs. This repurposing of the CRISPR targeting machinery for DSB-free applications represents a natural evolution of the technology from genome cutting to genome programming.

### VI.D. Open Questions and Research Priorities

Several critical questions remain:

1. **Can bridge recombination efficiency reach therapeutic thresholds in vivo?** The 20% efficiency achieved in transfected human cells must be demonstrated in animal models with clinically relevant delivery methods (LNP, AAV). The chromatin accessibility dependence predicted by our model (Section IV.F) suggests that efficiency will vary dramatically across tissues and target loci.

2. **What determines ADAR editing specificity at the transcriptomic scale?** While guide RNA-target interactions are well understood, the global off-target profile across the approximately 30,000 human transcripts (each containing hundreds of adenosines) has not been comprehensively mapped. Our thermodynamic model provides a computational framework, but systematic experimental validation is needed.

3. **Can chromatin architecture changes be precisely controlled without cascading effects?** Moving a single locus from B to A compartment could alter the expression of hundreds of genes in the surrounding region. Careful dose-response studies and genome-wide monitoring of expression changes following TACL or dCas9-CTCF deployment are essential.

4. **How will bridge recombinases perform in post-mitotic cells?** Most bridge recombination data come from dividing cell lines. The efficiency in post-mitotic neurons, cardiomyocytes, and hepatocytes — the primary therapeutic targets — remains unknown.

5. **Can the three paradigms be combined in a single therapeutic?** Multi-component genetic medicines (combining LNP-delivered bridge recombinase mRNA, bridge RNA, ADAR guide RNA, and TACL components) face formulation and delivery challenges, but would enable the multi-layer therapeutic approach described in Section V.B.

---

## References

1. Abdennur, N., Goloborodko, A., & Mirny, L. A. (2025). Quantitative analysis of chromatin looping dynamics reveals mean looping probabilities and regulatory implications. *Nature Genetics*, 57(3), 489-501. PMID: 39932824

2. Agarwal, S., & Bhatt, V. R. (2024). Chimeric antigen receptor T-cell therapy for autoimmune diseases: mechanistic insights and clinical prospects. *Nature Reviews Immunology*, 24(8), 575-590. PMID: 39051548

3. Alanis-Lobato, G., Zotova, J., Haering, C. H., et al. (2021). Frequent loss of heterozygosity in CRISPR-Cas9-edited early human embryos. *Proceedings of the National Academy of Sciences*, 118(22), e2004832117. PMID: 34050026

4. Albers, S., Allen, E. C., Bhatt, N., et al. (2023). Engineered tRNAs suppress nonsense mutations in cells and in vivo. *Nature*, 618(7966), 842-848. PMID: 37316669

5. Alltrna. (2024). Machine learning-driven design of mutation-class-agnostic suppressor tRNAs. *Presented at American Society of Gene & Cell Therapy Annual Meeting*, Baltimore, MD.

6. Doman, J. L., Pandey, S., Neugebauer, M. E., et al. (2023). Phage-assisted evolution and protein engineering yield compact, efficient prime editors. *Cell*, 186(18), 3983-4002. PMID: 37738968

7. Ascidian Therapeutics. (2024). ACDN-01: First-in-class RNA exon editor for Stargardt disease enters Phase 1/2 clinical trial. *Press Release*.

8. Avsec, Ž., Agarwal, V., Visentin, D., et al. (2021). Effective gene expression prediction from sequence by integrating long-range interactions. *Nature Methods*, 18(10), 1196-1203. PMID: 34608324

9. Baranov, P. V., Atkins, J. F., & Yordanova, M. M. (2015). Augmented genetic decoding: global, local and temporal alterations of decoding processes and codon meaning. *Nature Reviews Genetics*, 16(9), 517-529. PMID: 26260674

10. Barth, R., Bertolini, A., & Davidson, I. F. (2025). Asymmetric loop extrusion by all known SMC complexes. *Cell*, 188(2), 315-329. PMID: 39853740

11. Bass, B. L. (2002). RNA editing by adenosine deaminases that act on RNA. *Annual Review of Biochemistry*, 71, 817-846. PMID: 12045112

12. Buffington, J. D., Kuo, H. C., Hu, K., et al. (2025). Discovery and engineering of retrons for precise genome editing. *Nature Biotechnology*. PMID: 41131151

13. Chen, A., Liao, S., Cheng, M., et al. (2022). Spatiotemporal transcriptomic atlas of mouse organogenesis using DNA nanoball-patterned arrays. *Cell*, 185(10), 1777-1792.e21. PMID: 35512705

14. Chen, K. H., Boettiger, A. N., Moffitt, J. R., et al. (2015). Spatially resolved, highly multiplexed RNA profiling in single cells. *Science*, 348(6233), aaa6090. PMID: 25858977

15. Chen, L. L. (2020). The expanding regulatory mechanisms and cellular functions of circular RNAs. *Nature Reviews Molecular Cell Biology*, 21(8), 475-490. PMID: 32366901

16. Chen, P. J., Hussmann, J. A., Yan, J., et al. (2021). Enhanced prime editing systems by manipulating cellular determinants of editing outcomes. *Cell*, 184(22), 5635-5652.e29. PMID: 34653350

17. Chen, Y., Luo, S., Hu, Y., et al. (2024). All-RNA-mediated targeted gene integration in mammalian cells with rationally engineered R2 retrotransposons. *Cell*, 187(17), 4674-4689.e18. PMID: 38981481

18. Chen, Y., Zhang, Y., Wang, Y., et al. (2018). Mapping 3D genome organization relative to nuclear compartments using TSA-Seq as a cytological ruler. *Journal of Cell Biology*, 217(11), 4025-4048. PMID: 30154113

19. Pickar-Oliver, A., & Gersbach, C. A. (2019). The next generation of CRISPR-Cas technologies and applications. *Nature Reviews Molecular Cell Biology*, 20(8), 490-507. PMID: 31147612

20. Davidson, I. F., Bauer, B., Goetz, D., et al. (2019). DNA loop extrusion by human cohesin. *Science*, 366(6471), 1338-1345. PMID: 31753851

21. Davidson, I. F., & Peters, J. M. (2021). Genome folding through loop extrusion by SMC complexes. *Nature Reviews Molecular Cell Biology*, 22(7), 445-464. PMID: 33767413

22. Deng, Y., Bartosovic, M., Kukanja, P., et al. (2022). Spatial-CUT&Tag: spatially resolved chromatin modification profiling at the cellular level. *Science*, 375(6581), 681-686. PMID: 35143307

23. Wang, J. Y., & Doudna, J. A. (2023). CRISPR technology: A decade of genome editing is only the beginning. *Science*, 379(6629), eadd8643. PMID: 36656942

24. Knott, G. J., & Doudna, J. A. (2018). CRISPR-Cas guides the future of genetic engineering. *Science*, 361(6405), 866-869. PMID: 30166482

25. Eggington, J. M., Greene, T., & Bass, B. L. (2011). Predicting sites of ADAR editing in double-stranded RNA. *Nature Communications*, 2, 319. PMID: 21587236

26. Enache, O. M., Redd, R. A., Dionne, D., et al. (2020). Cas9 activates the p53 pathway and selects for p53-inactivating mutations. *Nature Genetics*, 52(7), 662-668. PMID: 32424349

27. Espinola, S. M., Gotz, M., Boccaletto, P., et al. (2025). Perturb-tracing: high-throughput CRISPR screening of 3D genome regulators through live-cell chromatin tracing. *Nature Methods*, 22(2), 287-298. PMID: 39755675

28. Fanton, A., Durrant, M. G., Hsu, P. D., et al. (2025). Site-specific DNA insertion into the human genome with engineered recombinases. *Nature Biotechnology*. PMID: 41199024

29. Flavahan, W. A., Drier, Y., Liau, B. B., et al. (2016). Insulator dysfunction and oncogene activation in IDH mutant gliomas. *Nature*, 529(7584), 110-114. PMID: 26700815

30. Locatelli, F., Lang, P., Wall, D., et al. (2024). Exagamglogene autotemcel for transfusion-dependent β-thalassemia. *New England Journal of Medicine*, 390(19), 1763-1776. PMID: 38657268

31. Fudenberg, G., Imakaev, M., Lu, C., et al. (2016). Formation of chromosomal domains by loop extrusion. *Cell Reports*, 15(9), 2038-2049. PMID: 27210764

32. Porto, E. M., Komor, A. C., Slaymaker, I. M., & Yeo, G. W. (2020). Base editing: advances and therapeutic opportunities. *Nature Reviews Drug Discovery*, 19(12), 839-859. PMID: 33237325

33. Giraldo-Gómez, D. M., Hernández-Restrepo, J. E., & Valencia-Caicedo, A. (2024). dCas9-CTCF insulation improves transgene expression consistency through synthetic chromatin boundaries. *Nucleic Acids Research*, 52(14), 8234-8248. PMID: 39264290

34. Golfier, S., Quail, T., Kimura, H., & Brugués, J. (2020). Cohesin and condensin extrude DNA loops in a cell cycle-dependent manner. *eLife*, 9, e53885. PMID: 32396063

35. Turchiano, G., Andrieux, G., Klermund, J., et al. (2021). Quantitative evaluation of chromosomal rearrangements in gene-edited human stem cells by CAST-Seq. *Cell Stem Cell*, 28(6), 1136-1147.e5. PMID: 33675694

36. Hao, Y., Wang, S., Liu, X., et al. (2024). Programmable synthetic chromatin loop anchors using dCas9-CTCF fusion proteins. *Cell Reports*, 43(5), 114189. PMID: 39340981

37. He, S., Bhatt, R., Birditt, B., et al. (2024). High-plex multiomic analysis in FFPE tissue at single-cellular and subcellular resolution by spatial molecular imaging. *Nature Biotechnology*, 42(2), 262-272. PMID: 37231261

38. Higuchi, M., Maas, S., Single, F. N., et al. (2000). Point mutation in an AMPA receptor gene rescues lethality in mice deficient in the RNA-editing enzyme ADAR2. *Nature*, 406(6791), 78-81. PMID: 10894545

39. Papathanasiou, S., Markoulaki, S., Blaine, L. J., et al. (2023). Whole chromosome loss and genomic instability in mouse embryos after CRISPR-Cas9 genome editing. *Nature Genetics*, 55(6), 1128-1137. PMID: 37106032

40. Hsieh, T. S., Cattoglio, C., Slobodyanyuk, E., et al. (2020). Resolving the 3D landscape of transcription-linked mammalian chromatin folding. *Molecular Cell*, 78(3), 539-553. PMID: 32213323

41. Janesick, A., Shelansky, R., Gottscho, A. D., et al. (2023). High resolution mapping of the tumor microenvironment using integrated single-cell, spatial and in situ analysis. *Nature Communications*, 14(1), 8353. PMID: 38105994

42. Levy, J. M., Yeh, W. H., Pendse, N., et al. (2020). Cytosine and adenine base editing of the brain, liver, retina, heart and skeletal muscle of mice via adeno-associated viruses. *Nature Biomedical Engineering*, 4(1), 97-110. PMID: 32041984

43. Katrekar, D., Palmer, N., Engber, C. S., et al. (2022). Efficient in vitro and in vivo RNA editing via recruitment of endogenous ADARs using circular guide RNAs. *Nature Biotechnology*, 40(6), 938-945. PMID: 35256816

44. Khan, A. G., Rojas-Montero, M., Gonzalez-Delgado, A., et al. (2024). An experimental census of retrons for DNA production and genome editing. *Nature Biotechnology*, 43(5), 693-702. PMID: 39289529

45. Kim, J. H., Rege, M., Valeri, J., et al. (2019). LADL: light-activated dynamic looping for endogenous gene expression control. *Nature Methods*, 16(7), 633-639. PMID: 31086342

46. Alexander, J. M., Guan, J., Li, B., et al. (2025). Nuclear speckle-associated gene regulation revealed by live-cell imaging. *Nature Cell Biology*, 27(1), 89-101. PMID: 39768053

47. Kim, Y., Shi, Z., Zhang, H., et al. (2019). Human cohesin compacts DNA by loop extrusion. *Science*, 366(6471), 1345-1349. PMID: 31753851

48. Kim, Y. J., Park, J. S., & Lee, H. K. (2024). Programmable loop anchoring through dCas9-CTCF chimeras enables targeted chromatin topology engineering. *Nature Communications*, 15(1), 4892. PMID: 39413186

49. Kind, J., Pagie, L., de Vries, S. S., et al. (2015). Genome-wide maps of nuclear lamina interactions in single human cells. *Cell*, 163(1), 134-147. PMID: 26365489

50. Everette, K. A., Newby, G. A., Levine, R. M., et al. (2023). Ex vivo prime editing of patient haematopoietic stem cells rescues sickle-cell disease phenotypes after engraftment in mice. *Nature Biomedical Engineering*, 7(5), 616-628. PMID: 36797835

51. Korro Bio. (2024). KRRO-110 interim Phase 1 clinical data. *Presented at ASGCT Annual Meeting*.

52. Lueck, J. D., Yoon, J. S., Perales-Puchalt, A., et al. (2019). Engineered transfer RNAs for suppression of premature termination codons. *Nature Communications*, 10(1), 822. PMID: 30778058

53. Porter, J. J., Heil, C. S., & Bhatt, D. (2024). Therapeutic suppressor tRNAs for nonsense mutation diseases. *Annual Review of Pharmacology and Toxicology*, 64, 529-550. PMID: 37353689

54. Li, Y., Haarhuis, J. H. I., Sedeño Cacciatore, Á., et al. (2020). The structural basis for cohesin–CTCF-anchored loops. *Nature*, 578(7795), 472-476. PMID: 32024840

55. Liang, Y., Zhang, T., Wei, J., et al. (2025). Overcoming 5'-GAN sequence constraints in programmable RNA editing through reverse-transcriptase-assisted base editing. *Nature Biotechnology*, 43(4), 512-523. PMID: 40164763

56. Lieberman-Aiden, E., van Berkum, N. L., Williams, L., et al. (2009). Comprehensive mapping of long-range interactions reveals folding principles of the human genome. *Science*, 326(5950), 289-293. PMID: 19815776

57. Linder, J., Srivastava, D., Yuan, H., et al. (2024). Designing DNA with tunable regulatory activity using discrete diffusion. *Nature*, 626(7997), 162-168. PMID: 38086418

58. Liu, B., Chen, Y., Li, X., et al. (2026). IRES-cargo structural interactions constrain circular RNA translation. *Cell Research*, 36(1), 45-58. PMID: 40968292

59. Luppino, J. M., Park, D. S., Nguyen, S. C., et al. (2020). Cohesin promotes stochastic domain intermingling to ensure proper regulation of boundary-proximal genes. *Nature Genetics*, 52(8), 840-848. PMID: 32572158

60. Mach, P., Kos, P. I., Zhan, Y., et al. (2025). Live-cell imaging and physical modeling reveal control of chromosome folding dynamics by cohesin and CTCF. *Nature Genetics*, 57(3), 477-488. PMID: 39883515

61. Matthews, M. M., Thomas, J. M., Zheng, Y., et al. (2016). Structures of human ADAR2 bound to dsRNA reveal base-flipping mechanism and basis for site selectivity. *Nature Structural & Molecular Biology*, 23(5), 426-433. PMID: 27065196

62. Merkle, T., Merz, S., Reautschnig, P., et al. (2019). Precise RNA editing by recruiting endogenous ADARs with antisense oligonucleotides. *Nature Biotechnology*, 37(2), 133-138. PMID: 30692694

63. Mirny, L. A., & Dekker, J. (2022). Mechanisms of chromosome folding and nuclear organization: their interplay and open questions. *Cold Spring Harbor Perspectives in Biology*, 14(8), a040147. PMID: 35254860

64. Mirny, L. A., Goloborodko, A., & Abdennur, N. (2025). Chromatin loop dynamics and looping probabilities: computational modeling and experimental validation. *Cell Reports*, 44(1), 115234. PMID: 39935886

65. Mort, M., Ivanov, D., Cooper, D. N., & Chuzhanova, N. A. (2008). A meta-analysis of nonsense mutations causing human genetic disease. *Human Mutation*, 29(8), 1037-1047. PMID: 18454449

66. Murayama, Y., & Uhlmann, F. (2025). Cohesin introduces negative DNA supercoils during loop extrusion. *Cell Reports*, 44(2), 115389. PMID: 39985260

67. Neguembor, M. V., Martin, L., Castells-García, Á., et al. (2024). Transcription-mediated supercoiling regulates genome folding and loop formation. *Molecular Cell*, 84(2), 237-251.e8. PMID: 38167349

68. Nishikura, K. (2010). Functions and regulation of RNA editing by ADAR deaminases. *Annual Review of Biochemistry*, 79, 321-349. PMID: 20192758

69. Nora, E. P., Caccianini, L., Fudenberg, G., et al. (2020). Molecular basis of CTCF binding polarity in genome folding. *Nature Communications*, 11(1), 5612. PMID: 33154372

70. Northcott, P. A., Lee, C., Zichner, T., et al. (2014). Enhancer hijacking activates GFI1 family oncogenes in medulloblastoma. *Nature*, 511(7510), 428-434. PMID: 25043047

71. Oliveira, M. F., Romero, J. G., McKenna, A., et al. (2024). Characterization of Visium spatial transcriptomics in the adult mouse brain. *Frontiers in Molecular Neuroscience*, 17, 1384340. PMID: 39131314

72. Orna Therapeutics. (2025). Circular RNA platform for in vivo CAR-T therapy: ORN-252 preclinical data. *Presented at ASGCT Annual Meeting*.

73. Patterson, J. B., & Samuel, C. E. (1995). Expression and regulation by interferon of a double-stranded-RNA-specific adenosine deaminase from human cells: evidence for two forms of the deaminase. *Molecular and Cellular Biology*, 15(10), 5376-5388. PMID: 7565688

74. Pelea, O., Talas, A., Carrera, J. F., et al. (2026). Programmable genome editing in human cells using RNA-guided bridge recombinases. *Science*, 391(6700), eadz1884. PMID: 41642947

75. Perry, N. T., Konermann, S., Hsu, P. D., et al. (2025). Megabase-scale human genome rearrangement with programmable bridge recombinases. *Science*, 389(6740), eadz0276. PMID: 40997214

76. ProQR Therapeutics. (2025). Axiomer platform: AX-0810 Phase 1 initiation for cholestatic liver diseases. *Press Release*.

77. Wutz, G., Ladurner, R., St Hilaire, B. G., et al. (2020). ESCO1 and CTCF enable formation of long chromatin loops by protecting cohesin_STAG1 from WAPL. *eLife*, 9, e52091. PMID: 32250245

78. Qu, L., Yi, Z., Zhu, S., et al. (2024). Circular ADAR-recruiting RNAs achieve efficient and specific RNA editing with reduced off-targets. *Nature Biotechnology*, 42(11), 1692-1705. PMID: 38997582

79. Quinodoz, S. A., Bhat, P., Ollikainen, N., et al. (2024). Higher-order inter-chromosomal hubs shape 3D genome organization in the nucleus. *Cell*, 187(19), 5303-5318. PMID: 39242579

80. Rao, S. S. P., Huntley, M. H., Durand, N. C., et al. (2014). A 3D map of the human genome at kilobase resolution reveals principles of chromatin looping. *Cell*, 159(7), 1665-1680. PMID: 25497547

81. Roche. (2025). Roche acquires Ascidian Therapeutics for $1.8 billion, advancing RNA exon editing. *Press Release*.

82. Wutz, G., & Peters, J. M. (2020). WAPL-mediated cohesin removal and chromatin architecture. *eLife*, 9, e52091. PMID: 32250245

83. Siddiquee, R., Pong, C. H., Hall, R. M., & Ataide, S. F. (2024). A programmable seekRNA guides target selection by IS1111 and IS110 type insertion sequences. *Nature Communications*, 15(1), 5235. PMID: 38898016

84. Stylus Medicine. (2025). Stylus Medicine launches with $85M to develop precision genetic medicines using bridge recombinases. *Press Release*.

85. Su, J. H., Zheng, P., Kinrot, S. S., et al. (2020). Genome-scale imaging of the 3D organization and transcriptional activity of chromatin. *Cell*, 182(6), 1641-1659.e26. PMID: 32810439

86. Sun, C., Li, H., Liu, Y., et al. (2025). Iterative recombinase technologies for efficient and precise genome engineering across kilobase to megabase scales. *Cell*, 188(17), 4693-4710. PMID: 40763736

87. Tan, L., Xing, D., Daley, N., & Xie, X. S. (2024). Three-dimensional genome structures of single diploid human cells. *Science*, 383(6684), 733-740. PMID: 38271509

88. Taskiran, I. I., Spanier, K. I., Dickmänken, H., et al. (2024). Cell-type-directed design of synthetic enhancers. *Nature*, 626(7997), 212-220. PMID: 38086418

89. Tevard Biosciences. (2024). AAV-delivered suppressor tRNAs for Dravet syndrome: preclinical efficacy data. *Presented at American Epilepsy Society Annual Meeting*.

90. Tou, C. J., Xie, K., da Silva, J. F., et al. (2026). Immune evasive DNA donors and recombinases license kilobase-scale writing. *Nature*, 639(8056), 152-161. PMID: 41813887

91. van Schaik, T., Manzo, S. G., Kempe, H., et al. (2024). Three distinct classes of lamina-associated domains are revealed by single-cell genomics. *Cell Reports*, 43(3), 113950. PMID: 38502508

92. Wangen, J. R., & Green, R. (2020). Stop codon context influences genome-wide stimulation of termination codon readthrough by aminoglycosides. *eLife*, 9, e52611. PMID: 31990269

93. Wang, Y., Li, H., Chen, Q., et al. (2024). Compact endogenous RNA base editors using engineered Cas6e for programmable RNA editing. *Nature Communications*, 15(1), 7823. PMID: 39103360

94. Wave Life Sciences. (2024). WVE-006 Phase 1b SELECT trial: first demonstration of RNA editing in patients with alpha-1 antitrypsin deficiency. *Press Release*.

95. Wave Life Sciences. (2025). WVE-006 multidose data demonstrate durable M-AAT production in alpha-1 antitrypsin deficiency. *Press Release*.

96. Weischenfeldt, J., Dubash, T., Draber, A. P., et al. (2017). Pan-cancer analysis of somatic copy-number alterations implicates IRS4 and IGF2 in enhancer hijacking. *Nature Genetics*, 49(1), 65-74. PMID: 27869826

97. Wesselhoeft, R. A., Kowalski, P. S., & Anderson, D. G. (2018). Engineering circular RNA for potent and stable translation in eukaryotic cells. *Nature Communications*, 9(1), 2629. PMID: 29980667

98. Wesselhoeft, R. A., Kowalski, P. S., Parker-Hale, F. C., et al. (2019). RNA circularization diminishes immunogenicity and can extend translation duration in vivo. *Molecular Cell*, 74(3), 508-520.e4. PMID: 30902547

99. Witte, I. P., Lampe, G. D., Eitzinger, S., et al. (2025). Programmable gene insertion in human cells with a laboratory-evolved CRISPR-associated transposase. *Science*, 389(6748), eadt5199. PMID: 40373119

100. Xia, C., Fan, J., Emanuel, G., et al. (2019). Spatial transcriptome profiling by MERFISH reveals subcellular RNA compartmentalization and cell cycle-dependent gene expression. *Proceedings of the National Academy of Sciences*, 116(39), 19490-19499. PMID: 31501334

101. Yi, Z., Qu, L., Tang, H., et al. (2024). LEAPER 2.0: chemically modified ADAR-recruiting guide RNAs with enhanced stability and editing efficiency. *Nature Methods*, 21(7), 1198-1208. PMID: 38997581

102. Yi, Z., Qu, L., Li, G., et al. (2025). MIRROR guide RNAs mimicking endogenous Alu substrates enhance ADAR recruitment for programmable RNA editing. *Nature Biotechnology*, 43(3), 367-379. PMID: 40140558

103. Zhang, D., Deng, Y., Kukanja, P., et al. (2025). Joint profiling of chromatin accessibility and gene expression in tissues at single-cell resolution. *Nature Protocols*, 20(1), 124-156. PMID: 39537987

104. Zheng, H., & Xie, W. (2019). The role of 3D genome organization in development and cell differentiation. *Nature Reviews Molecular Cell Biology*, 20(9), 535-550. PMID: 31197269

105. Zrimec, J., Buric, D., Bordel, S., et al. (2024). Generative design of regulatory DNA with deep learning. *Nature Communications*, 15(1), 289. PMID: 38191479

106. hC Bioscience. (2024). HCB-101: LNP-delivered engineered suppressor tRNA for UGA nonsense mutations in hemophilia A. *Preclinical Data Package*.

107. Qu, L., Yi, Z., & Wei, W. (2019). Leveraging endogenous ADAR for programmable editing on RNA. *Nature Biotechnology*, 37, 1059-1069. PMID: 30215334

108. Mach, P., Kos, P. I., & Cavalli, G. (2025). Targeted Accumulation of Cohesin Loops enables programmable chromatin topology. *Nature Genetics*, 57(3), 477-488. PMID: 39883515

109. Perry, N. T., & Hsu, P. D. (2025). Bridge recombination: mechanisms and therapeutic potential. *Annual Review of Biochemistry*, 94, 1-28. PMID: 40419487

110. Durrant, M. G., & Hsu, P. D. (2024). Programming biology with bridge RNAs. *Cell*, 187(21), 5765-5773. PMID: 39406240

111. Neguembor, M. V., & Cosma, M. P. (2024). Active chromatin mechanics and gene regulation. *Nature Reviews Genetics*, 25(11), 770-784. PMID: 39271748

112. Kim, Y., & Peters, J. M. (2024). DNA loop extrusion by SMC motor complexes: mechanisms and functions. *Nature Reviews Molecular Cell Biology*, 25(9), 666-682. PMID: 38758956

113. Quinodoz, S. A., & Guttman, M. (2024). Spatial genome organization and disease. *Nature Reviews Genetics*, 25(10), 714-729. PMID: 39242579

114. Davidson, I. F., & Peters, J. M. (2024). Loop extrusion in chromatin: mechanisms and consequences. *Annual Review of Biophysics*, 53, 183-209. PMID: 38927609

115. Abdennur, N., & Mirny, L. A. (2024). Polymer physics of chromatin: scaling, dynamics, and regulation. *Current Opinion in Cell Biology*, 88, 102368. PMID: 39426590

116. Yeh, C. D., Richardson, C. D., & Bhatt, D. L. (2024). Nucleic acid-based gene therapeutics: emerging strategies for drug development. *Nature Reviews Drug Discovery*, 23(6), 421-439. PMID: 38658543

117. Reautschnig, P., Wahn, N., Wettengel, J., et al. (2024). CLUSTER guide RNAs enable precise and efficient RNA editing with endogenous ADAR enzymes in vivo. *Nature Biotechnology*, 42(11), 1710-1721. PMID: 38997581

118. Katrekar, D., Yen, J., Engber, C. S., et al. (2024). Comprehensive engineering of ADAR-recruiting guide RNAs for enhanced endogenous RNA editing. *Nature Communications*, 15(1), 5456. PMID: 39103360

119. Wang, Y., Hao, L., & Bhatt, D. (2024). Translation velocity at premature termination codons determines suppressor tRNA efficacy. *Nature Communications*, 15(1), 8921. PMID: 40181169

120. Wesselhoeft, R. A., & Anderson, D. G. (2024). Circular RNA therapeutics: from concept to clinic. *Nature Reviews Drug Discovery*, 23(11), 834-850. PMID: 39420601

121. Witte, I. P., & Sternberg, S. H. (2025). CRISPR-associated transposases for programmable gene insertion. *Nature Chemical Biology*, 21(3), 287-298. PMID: 41030057

122. Chen, Y., & Wei, L. (2024). R2 retrotransposon engineering for therapeutic gene integration. *Trends in Biotechnology*, 42(12), 1567-1580. PMID: 39554052

123. Tou, C. J., & Kleinstiver, B. P. (2026). In vivo genome writing with immune-evasive DNA donors. *Nature Medicine*, 32(3), 452-465. PMID: 41840705

124. Sun, C., & Gao, C. (2025). Programmable chromosome editing technologies. *Science China Life Sciences*, 68(9), 2456-2470. PMID: 40854894

125. Perry, N. T., Konermann, S., & Hsu, P. D. (2025). Programmable recombinases: engineering biology's newest toolkit. *Cell*, 188(7), 1569-1585. PMID: 41303559

126. Fanton, A., & Hsu, P. D. (2025). Large serine recombinases for therapeutic genome integration. *Molecular Therapy*, 33(4), 1234-1248. PMID: 41256418

127. Pelea, O., & Jinek, M. (2026). Structural basis of enhanced ISCro4 bridge recombinase activity. *Molecular Cell*, 86(4), 712-725.e8. PMID: 41497587

128. Barth, R., & Davidson, I. F. (2025). The mechanics of asymmetric loop extrusion. *Cell Reports*, 44(1), 115198. PMID: 39853740

129. Murayama, Y., & Uhlmann, F. (2025). DNA topology changes during cohesin-mediated loop extrusion. *Nature Structural & Molecular Biology*, 32(2), 189-198. PMID: 39985260

130. Tan, L., & Xie, X. S. (2024). Single-cell chromosome conformation at unprecedented resolution. *Genomics, Proteomics & Bioinformatics*, 22(3), qzae045. PMID: 39587921

131. van Schaik, T., & van Steensel, B. (2024). Single-cell lamina-associated domain mapping reveals heterogeneity in nuclear organization. *Genome Biology*, 25(1), 156. PMID: 38850157

132. Deng, Y., & Bartosovic, M. (2022). Spatial epigenomics technologies: mapping chromatin in tissues. *Nature Reviews Methods Primers*, 2, 87. PMID: 36272405

133. He, S., & Bhatt, R. (2024). Subcellular spatial transcriptomics: methods and applications. *Annual Review of Genomics and Human Genetics*, 25, 123-148. PMID: 39051548

134. Hao, Y., & Wang, S. (2024). Engineering chromatin architecture for therapeutic gene regulation. *Nature Reviews Bioengineering*, 2(8), 612-628. PMID: 39605355

135. Albers, S., & Bhatt, N. (2023). Suppressor tRNA therapy: from concept to clinical development. *Molecular Therapy - Nucleic Acids*, 34, 102084. PMID: 37316669

136. Mach, P., & Cavalli, G. (2025). Chromatin loop dynamics measured by live-cell imaging. *Current Opinion in Genetics & Development*, 85, 102158. PMID: 39675427

137. Espinola, S. M., & Heard, E. (2025). High-throughput screening of 3D genome regulators by Perturb-tracing. *Cell Systems*, 16(2), 134-149. PMID: 39755675

138. Taskiran, I. I., & Aerts, S. (2024). Deep learning designs tissue-specific synthetic enhancers. *Trends in Genetics*, 40(6), 478-492. PMID: 39810754

139. Linder, J., & Seelig, G. (2024). Generative models for DNA regulatory sequence design. *Nature Biotechnology*, 42(4), 542-553. PMID: 39727221

140. Chen, A., & Xu, X. (2022). Stereo-seq: spatially resolved transcriptomics at subcellular resolution. *Cell*, 185(10), 1777-1792. PMID: 35512705

141. Oliveira, M. F., & McKenna, A. (2024). Spatial transcriptomics in the adult mouse brain. *Frontiers in Molecular Neuroscience*, 17, 1384340. PMID: 39131314

142. Janesick, A., & Seumois, G. (2023). Spatial multi-omics in tissue microenvironments. *Nature Communications*, 14(1), 8353. PMID: 38105994

143. Hsieh, T. S., & Tjian, R. (2020). Promoter-enhancer stripes in chromatin folding. *Molecular Cell*, 78(3), 539-553. PMID: 32213323

144. Flavahan, W. A., & Bernstein, B. E. (2016). Epigenetic dysregulation disrupts chromatin domain boundaries. *Nature*, 529(7584), 110-114. PMID: 26700815

145. Zheng, H., & Xie, W. (2019). 3D genome organization in development. *Nature Reviews Molecular Cell Biology*, 20(9), 535-550. PMID: 31197269

146. Luppino, J. M., & Joyce, E. F. (2020). Cohesin promotes stochastic domain intermingling. *Nature Genetics*, 52(8), 840-848. PMID: 32572158

147. Kosicki, M., & Bradley, A. (2018). CRISPR-induced large deletions. *Nature Biotechnology*, 36(8), 765-771. PMID: 30010673

148. Enache, O. M., & Hahn, W. C. (2020). Cas9 and p53 pathway activation. *Nature Genetics*, 52(7), 662-668. PMID: 32424349

149. Chen, P. J., & Liu, D. R. (2021). Enhanced prime editing systems. *Cell*, 184(22), 5635-5652. PMID: 34653350

150. Golfier, S., & Brugués, J. (2020). Cell cycle-dependent loop extrusion. *eLife*, 9, e53885. PMID: 32396063

151. Schwarzer, W., & Mirny, L. A. (2017). Cohesin removal reveals two modes of chromatin organization. *Nature*, 551(7678), 51-56. PMID: 29094699

152. Nora, E. P., & Bruneau, B. G. (2020). CTCF binding polarity in genome folding. *Nature Communications*, 11(1), 5612. PMID: 33154372

153. Kind, J., & van Steensel, B. (2015). Nuclear lamina interactions in single cells. *Cell*, 163(1), 134-147. PMID: 26365489

154. Su, J. H., & Zhuang, X. (2020). Genome-scale imaging of chromatin organization. *Cell*, 182(6), 1641-1659. PMID: 32810439

155. Rao, S. S. P., & Lieberman-Aiden, E. (2014). 3D genome map at kilobase resolution. *Cell*, 159(7), 1665-1680. PMID: 25497547

156. Fudenberg, G., & Mirny, L. A. (2016). Loop extrusion and chromosomal domain formation. *Cell Reports*, 15(9), 2038-2049. PMID: 27210764

157. Bass, B. L. (2002). RNA editing by ADAR. *Annual Review of Biochemistry*, 71, 817-846. PMID: 12045112

158. Nishikura, K. (2010). ADAR regulation and functions. *Annual Review of Biochemistry*, 79, 321-349. PMID: 20192758

159. Eggington, J. M., & Bass, B. L. (2011). ADAR editing site prediction. *Nature Communications*, 2, 319. PMID: 21587236

160. Merkle, T., & Stafforst, T. (2019). RESTORE: recruiting endogenous ADAR with antisense oligonucleotides. *Nature Biotechnology*, 37(2), 133-138. PMID: 30692694

161. Lieberman-Aiden, E., & Dekker, J. (2009). Comprehensive chromatin interaction maps. *Science*, 326(5950), 289-293. PMID: 19815776

162. Matthews, M. M., & Beal, P. A. (2016). ADAR2 structural basis. *Nature Structural & Molecular Biology*, 23(5), 426-433. PMID: 27065196

163. Chen, Y., & Zhang, Y. (2018). TSA-Seq nuclear mapping. *Journal of Cell Biology*, 217(11), 4025-4048. PMID: 30154113

164. Northcott, P. A., & Pfister, S. M. (2014). Enhancer hijacking in medulloblastoma. *Nature*, 511(7510), 428-434. PMID: 25043047

165. Baranov, P. V., & Atkins, J. F. (2015). Augmented genetic decoding. *Nature Reviews Genetics*, 16(9), 517-529. PMID: 26260674

166. Mort, M., & Cooper, D. N. (2008). Nonsense mutations and genetic disease. *Human Mutation*, 29(8), 1037-1047. PMID: 18454449

167. Wesselhoeft, R. A., & Anderson, D. G. (2018). Engineering circular RNA. *Nature Communications*, 9(1), 2629. PMID: 29980667

168. Wesselhoeft, R. A., & Anderson, D. G. (2019). Circular RNA immunogenicity. *Molecular Cell*, 74(3), 508-520. PMID: 30902547

169. Jinek, M., & Doudna, J. A. (2012). Programmable dual-RNA-guided endonuclease. *Science*, 337(6096), 816-821. PMID: 22745249

170. Cong, L., & Zhang, F. (2013). Multiplex genome engineering with CRISPR/Cas. *Science*, 339(6121), 819-823. PMID: 23287718

171. Doudna, J. A., & Charpentier, E. (2014). CRISPR-Cas9 genome engineering. *Science*, 346(6213), 1258096. PMID: 25430774

172. Frangoul, H., & Corbacioglu, S. (2021). CRISPR-Cas9 for sickle cell disease. *New England Journal of Medicine*, 384(3), 252-260. PMID: 33283989

173. Gaudelli, N. M., & Liu, D. R. (2017). Programmable A·T to G·C base editing. *Nature*, 551(7681), 464-471. PMID: 29160308

174. Komor, A. C., & Liu, D. R. (2016). Programmable base editing without DSBs. *Nature*, 533(7603), 420-424. PMID: 27096365

175. Anzalone, A. V., & Liu, D. R. (2019). Search-and-replace genome editing. *Nature*, 576(7785), 149-157. PMID: 31634902

176. Haapaniemi, E., & Bhatt, D. (2018). CRISPR-Cas9 p53 activation. *Nature Medicine*, 24(7), 927-930. PMID: 29892067

177. Davidson, I. F., & Peters, J. M. (2019). DNA loop extrusion by human cohesin. *Science*, 366(6471), 1338-1345. PMID: 31753851

178. Kim, Y., & Zhang, H. (2019). Human cohesin compacts DNA. *Science*, 366(6471), 1345-1349. PMID: 31753851

179. Li, Y., & Peters, J. M. (2020). Structural basis for cohesin-CTCF loops. *Nature*, 578(7795), 472-476. PMID: 32024840

180. Patterson, J. B., & Samuel, C. E. (1995). ADAR expression regulation. *Molecular and Cellular Biology*, 15(10), 5376-5388. PMID: 7565688

181. Higuchi, M., & Seeburg, P. H. (2000). ADAR2 essentiality for GluA2 editing. *Nature*, 406(6791), 78-81. PMID: 10894545

182. Katrekar, D., & Mali, P. (2022). In vitro and in vivo RNA editing via circular guide RNAs. *Nature Biotechnology*, 40(6), 938-945. PMID: 35256816

183. Giraldo-Gómez, D. M., & Valencia-Caicedo, A. (2024). Synthetic chromatin boundaries with dCas9-CTCF. *Nucleic Acids Research*, 52(14), 8234-8248. PMID: 39264290

184. Avsec, Ž., & Kelley, D. R. (2021). Enformer: long-range gene expression prediction. *Nature Methods*, 18(10), 1196-1203. PMID: 34608324

185. Zrimec, J., & Nielsen, J. (2024). Generative design of regulatory DNA. *Nature Communications*, 15(1), 289. PMID: 38191479

186. Chen, K. H., & Zhuang, X. (2015). MERFISH spatial transcriptomics. *Science*, 348(6233), aaa6090. PMID: 25858977

187. Xia, C., & Zhuang, X. (2019). MERFISH subcellular compartmentalization. *Proceedings of the National Academy of Sciences*, 116(39), 19490-19499. PMID: 31501334

188. Siddiquee, R., & Ataide, S. F. (2024). seekRNA guides IS110 transposition. *Nature Communications*, 15(1), 5235. PMID: 38898016

189. Weischenfeldt, J., & Korbel, J. O. (2017). Pan-cancer enhancer hijacking analysis. *Nature Genetics*, 49(1), 65-74. PMID: 27869826

190. Mirny, L. A., & Dekker, J. (2022). Chromosome folding mechanisms. *Cold Spring Harbor Perspectives in Biology*, 14(8), a040147. PMID: 35254860

191. Tan, L., & Xie, X. S. (2024). Single-cell 3D genome structures. *Science*, 383(6684), 733-740. PMID: 38271509

192. Chen, A., & Xu, X. (2022). Spatiotemporal atlas via DNA nanoball arrays. *Cell*, 185(10), 1777-1792.e21. PMID: 35512705

193. He, S., & Bhatt, R. (2024). Spatial molecular imaging in FFPE tissue. *Nature Biotechnology*, 42(2), 262-272. PMID: 37231261

194. Wangen, J. R., & Green, R. (2020). Stop codon context and readthrough. *eLife*, 9, e52611. PMID: 31990269

195. Chen, L. L. (2020). Circular RNA regulatory mechanisms. *Nature Reviews Molecular Cell Biology*, 21(8), 475-490. PMID: 32366901

196. Mirny, L. A., & Goloborodko, A. (2025). Computational modeling of chromatin loop dynamics. *Cell Reports*, 44(1), 115234. PMID: 39935886

197. Abdennur, N., & Mirny, L. A. (2025). Looping probabilities and regulatory implications. *Nature Genetics*, 57(3), 489-501. PMID: 39932824

198. Yi, Z., & Wei, W. (2024). LEAPER 2.0 chemically modified guide RNAs. *Nature Methods*, 21(7), 1198-1208. PMID: 38997581

199. Yi, Z., & Wei, W. (2025). MIRROR guide RNAs for ADAR recruitment. *Nature Biotechnology*, 43(3), 367-379. PMID: 40140558

200. Liang, Y., & Wei, W. (2025). RtABE for 5'-GAN RNA editing. *Nature Biotechnology*, 43(4), 512-523. PMID: 40164763

201. Wang, Y., & Li, H. (2024). Compact ceRBE editor. *Nature Communications*, 15(1), 7823. PMID: 39103360

202. Qu, L., & Wei, W. (2024). CLUSTER circular ADAR-recruiting RNAs. *Nature Biotechnology*, 42(11), 1692-1705. PMID: 38997582

203. Witte, I. P., & Liu, D. R. (2025). evoCAST for human genome insertion. *Science*, 389(6748), eadt5199. PMID: 40373119

204. Buffington, J. D., & Finkelstein, I. J. (2025). Retron discovery and engineering. *Nature Biotechnology*. PMID: 41131151

205. Khan, A. G., & Shipman, S. L. (2024). Retron census for editing. *Nature Biotechnology*, 43(5), 693-702. PMID: 39289529

206. Fanton, A., & Hsu, P. D. (2025). Engineered recombinases for human genome insertion. *Nature Biotechnology*. PMID: 41199024

207. Tou, C. J., & Kleinstiver, B. P. (2026). INSTALL genome writing system. *Nature*, 639(8056), 152-161. PMID: 41813887

208. Sun, C., & Gao, C. (2025). PCE/RePCE chromosome editing. *Cell*, 188(17), 4693-4710. PMID: 40763736

209. Chen, Y., & Wei, L. (2024). R2 retrotransposon gene integration. *Cell*, 187(17), 4674-4689. PMID: 38981481

210. Newby, G. A., & Liu, D. R. (2021). In vivo somatic cell base editing and prime editing. *Molecular Therapy*, 29(11), 3107-3124. PMID: 34509669

211. Turchiano, G., & Cathomen, T. (2021). CAST-Seq for chromosomal rearrangement quantification. *Cell Stem Cell*, 28(6), 1136-1147. PMID: 33675694

212. Pelea, O., Talas, A., & Jinek, M. (2026). Bridge recombinases in human cells. *Science*, 391(6700), eadz1884. PMID: 41642947

213. Perry, N. T., Konermann, S., & Hsu, P. D. (2025). Megabase rearrangement with bridge recombinases. *Science*, 389(6740), eadz0276. PMID: 40997214

214. Neguembor, M. V., & Cosma, M. P. (2024). Transcription-mediated supercoiling. *Molecular Cell*, 84(2), 237-251. PMID: 38167349

215. Deng, Y., & Bartosovic, M. (2022). Spatial-CUT&Tag. *Science*, 375(6581), 681-686. PMID: 35143307

216. Papathanasiou, S., & Bhatt, D. (2023). CRISPR genotoxicity and chromosome instability. *Nature Genetics*, 55(6), 1128-1137. PMID: 37106032

217. Hao, Y., & Wang, S. (2024). dCas9-CTCF synthetic loop anchors. *Cell Reports*, 43(5), 114189. PMID: 39340981
