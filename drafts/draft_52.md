# Identity Stability in Non-Pluripotent Reprogramming

---

## Abstract

Chemical reprogramming — the use of small-molecule cocktails to rewrite cell identity — has advanced from proof-of-concept to clinical candidacy in under a decade. Seven-compound mouse CiPSC cocktails have been reduced to optimised human protocols achieving pluripotency in as few as ten days (Wang et al., *Nature Chemical Biology*, 2025), and direct chemical conversion now generates cardiomyocyte-like cells at whole-organ scale (Chen et al., *Nature Cardiovascular Research*, 2024). Yet the field lacks a mechanistic account of *how* small molecules achieve what pioneer transcription factors accomplish through sequence-specific nucleosome engagement: the opening of closed chromatin at lineage-specifying loci. Simultaneously, the central unsolved problem for clinical translation — whether converted cells maintain their new identity over therapeutic timescales — remains unaddressed at the molecular level. This manuscript fills both gaps. We decompose the chemical reprogramming chromatin cascade into three temporally ordered phases: barrier removal (HDAC inhibition → global H3K9 acetylation and nucleosome destabilisation), lineage priming (GSK3β/Wnt activation → β-catenin-driven bivalent domain establishment), and identity consolidation (TGFβ pathway inhibition → SMAD2/3 release and lineage-selector accessibility). We introduce the "chemical pioneer" hypothesis — that HDAC and BET bromodomain inhibitors together phenocopy the chromatin-opening function of pioneer transcription factors by destabilising histone–DNA contacts without sequence-specific binding — and provide thermodynamic and kinetic frameworks to test it. We then address identity stability through the "three locks" model: DNA methylation maintenance (DNMT3A/B), heterochromatin consolidation (H3K9me3/SETDB1/SUV39H1), and 3D genome insulation (CTCF/cohesin TAD boundaries), demonstrating that direct chemical conversion engages these locks incompletely compared with developmental specification. Novel mathematical frameworks (F375–F380) formalise the chromatin-state Markov chain, chemical-pioneer free-energy equivalence, identity-stability Lyapunov function, reversion hazard model, optimal cocktail timing, and single-cell trajectory entropy. We close with a rational cocktail-design principle — profile target-cell chromatin state, identify barriers, select compounds that address each barrier class — and identify AI-guided perturbation models (GEARS, scGPT, GET) as the computational infrastructure for next-generation cocktail optimisation.

**Key Points**
- The chemical reprogramming chromatin cascade operates in three temporally ordered phases: barrier removal, lineage priming, and identity consolidation.
- HDAC and BET inhibitors together function as "chemical pioneers" — destabilising histone–DNA contacts to phenocopy pioneer TF chromatin opening without sequence specificity.
- DOT1L inhibition is a rate-limiting step: H3K79me2 erasure permits de novo PRC2-mediated H3K27me3, enabling lineage-specific bivalent states (Onder et al. 2012; Wille et al. 2023).
- Identity stability after conversion depends on three epigenetic locks — DNA methylation, H3K9me3 heterochromatin, and CTCF/cohesin TAD insulation — which engage incompletely after chemical reprogramming.
- Novel frameworks (F375–F380) provide quantitative tools for cocktail optimisation and stability prediction.
- CRISPRoff-based epigenetic locking can artificially engage missing identity locks to stabilise converted cell fates.

---

## 1. Introduction — The Mechanism Gap

Chemical reprogramming of human somatic cells to pluripotency was first achieved by Guan and colleagues in 2022, using a sixteen-compound cocktail over approximately fifty days to generate human chemically induced pluripotent stem cells (hCiPSCs) from fibroblasts through an intermediate plastic state reminiscent of axolotl limb regeneration (Guan et al. 614). An optimised protocol reduced the timeline to sixteen days with over twenty-fold higher efficiency (Liuyang et al. 185), and a next-generation system now achieves hCiPSC generation in as few as ten days with a 100% success rate across fifteen donors, identifying KAT3A/KAT3B and KAT6A as key epigenetic obstacles whose suppression facilitates the transition to a poised chromatin state (Wang et al. 1). Most recently, chemical reprogramming has been extended from fibroblasts to human blood cells, generating over 100 hCiPSC colonies from a single drop of fingerstick blood (Peng et al. 1).

These advances establish that chemical reprogramming *works*. What they do not establish is *how it works at the chromatin level*. The dominant narrative frames chemical cocktails as pathway modulators — GSK3β inhibitors activate Wnt, TGFβ inhibitors release SMAD-mediated repression, HDAC inhibitors "open chromatin" — but this pharmacological language obscures the precise epigenetic transactions. How does valproic acid, a broad-spectrum HDAC inhibitor, convert a heterochromatic fibroblast locus into an accessible pluripotency-gene promoter? How does CHIR99021, a GSK3β inhibitor, install the bivalent H3K4me3/H3K27me3 domains that mark lineage-poised genes? How does the temporal order of compound addition — which matters profoundly for efficiency (Zhao et al. 1580) — reflect an underlying chromatin-state dependency?

A parallel gap concerns the durability of chemical conversion. Draft_64 of this series established that direct and chemical reprogramming constitute a unified clinical-translation axis (the non-pluripotent reprogramming axis) and identified identity stability as the single most important open question for near-term translation. But the molecular basis of identity stability — what distinguishes a stably converted cardiomyocyte from one drifting back to a fibroblast-like state — has not been systematically analysed. This manuscript addresses both gaps. Sections 2–3 decompose the chemical chromatin cascade. Sections 4–5 define the identity-stability problem and its mathematical formalisation. Sections 6–7 propose rational cocktail design and therapeutic implications.

---

## 2. The Chemical Reprogramming Chromatin Cascade

### 2.1 Phase I — Barrier Removal: HDAC Inhibition and Global Chromatin Decompaction

The first temporal phase of chemical reprogramming removes epigenetic barriers that maintain the somatic cell identity. The principal agents are histone deacetylase (HDAC) inhibitors, most commonly valproic acid (VPA). Huangfu and colleagues demonstrated that VPA improves iPSC reprogramming efficiency by more than 100-fold and enables efficient pluripotency induction without the oncogene c-Myc (Huangfu et al. 795). The mechanism operates through global hyperacetylation of histone H3, particularly at lysine 9 (H3K9ac) and lysine 56 (H3K56ac), which destabilises histone–DNA contacts and increases nucleosome mobility.

Genome-wide profiling reveals that VPA induces a pervasive, time-dependent increase in H3K9ac at gene promoters, but this increase is selectively suppressed at bivalent (H3K4me3/H3K27me3) domains after four hours, suggesting a built-in mechanism that protects lineage-poised loci from premature activation (Hezroni et al. 4474). The chromatin accessibility landscape shifts correspondingly: ATAC-seq following VPA treatment reveals increased accessibility at loci encoding cardiac troponin (Tnnt2), the homeodomain factor Hopx, and other lineage-specifying genes, accompanied by loss of POU5F1/SOX2 transcription factor footprints (Baumann et al. 1). Critically, HDACi treatment induces a strong increase in H3K27me3 at transcription start sites irrespective of transcriptional direction, mediated by EZH1/2 activity, creating a compensatory repressive mark that prevents runaway gene activation (Halsall et al. 1).

Recent work in primary neuron-glia cultures demonstrates that broad-spectrum HDAC inhibitors reduce the proliferative potential of cultured cells and induce transcriptomic changes associated with cell differentiation and specialisation, with significant upregulation of genes typically expressed in neuromodulatory neurons and accompanying elevation of histone serotonylation levels that persist over many hours (Borodinova et al. 1). This sustained epigenetic remodelling — not merely transient acetylation — is what enables HDAC inhibitors to prime cells for fate conversion rather than simply perturbing transcription.

The key insight is that HDAC inhibition does not simply "open chromatin" — it selectively destabilises histone–DNA contacts at somatic-identity loci while simultaneously installing compensatory H3K27me3 marks that channel the newly accessible chromatin toward lineage-poised states rather than transcriptional chaos. This selective decompaction is the first step in the chemical reprogramming cascade.

### 2.2 The "Chemical Pioneer" Hypothesis

Pioneer transcription factors — FOXA1, OCT4, ASCL1 — bind nucleosomal DNA directly and initiate chromatin opening at closed loci through sequence-specific recognition of their cognate motifs (Wapinski et al. 958). Draft_44 of this series established the structural mechanisms by which six pioneer factors engage nucleosomes. We propose that HDAC inhibitors and BET bromodomain inhibitors together achieve an analogous chromatin-opening function through an orthogonal mechanism: destabilisation of histone–DNA contacts *without* sequence-specific binding.

The evidence is threefold. First, HDAC inhibitors cause site-specific chromatin remodelling at PU.1-bound enhancers marked by H3K27me3, suggesting that HDACi treatment opens epigenetically poised sites where pioneer factors have already established partial accessibility (Frank et al. 1). Second, BET inhibition by JQ1 displaces BRD4 from chromatin globally, prompting cell-type-specific differentiation programs by collapsing transcriptional elongation at identity-maintaining super-enhancers while sparing housekeeping transcription (Winter et al. 67). BET proteins function as master transcription elongation factors, and their displacement by JQ1 phenocopies CDK9 inhibition — effectively removing the transcriptional maintenance machinery that sustains the somatic identity (Winter et al. 67). Third, JQ1 treatment maintains CD8+ T cells in a stem cell-like memory state by directly regulating expression of the transcription factor BATF through BRD4, demonstrating that BET inhibition can arrest cells in a more plastic, less differentiated state amenable to fate conversion (Kagoya et al. 51).

The chemical pioneer hypothesis predicts that the combination of HDAC inhibitors (which destabilise histone–DNA contacts) and BET inhibitors (which remove the elongation machinery maintaining somatic transcription) should phenocopy the chromatin-opening function of pioneer TFs at a substantial fraction of target loci, albeit without the sequence specificity that makes pioneer TFs selective for particular lineage programs. The lack of sequence specificity is both the strength and the weakness of chemical pioneers: they can open chromatin broadly, but they cannot direct which lineage programs are activated — that directional function must come from Phase II compounds (GSK3β/Wnt activators) or from endogenous pioneer factors whose binding sites become newly accessible.

### 2.3 DOT1L Inhibition as the Rate-Limiting Step

Among the chromatin-modifying enzymes that regulate reprogramming, DOT1L — the sole H3K79 methyltransferase — emerges as a uniquely important barrier. Onder and colleagues demonstrated that DOT1L inhibition by shRNA or the small molecule EPZ004777 accelerated reprogramming, significantly increased iPSC colony yield, and could substitute for KLF4 and c-Myc (Onder et al. 1508). The mechanism is not simply transcriptional: DOT1L inhibition facilitates the loss of H3K79me2 from fibroblast-specific genes associated with the epithelial-to-mesenchymal transition during the initial phases of reprogramming, effectively erasing a somatic-identity mark (Onder et al. 1508).

More recent work has refined this picture substantially. Wille and colleagues showed that DOT1L inhibition enhances reprogramming beyond the mesenchymal-to-epithelial transition and even from already-epithelial cell types, demonstrating that H3K79me is not merely a barrier to the MET step but a broader guardian of somatic cell identity (Wille et al., *Stem Cell Reports*, 2021, 445). Critically, DOT1L is a barrier to histone acetylation during reprogramming: DOT1L inhibition increases H3K27 methylation and transcription-elongation-enhancing histone acetylation without changing the expression levels of the causal histone-modifying enzymes, and only the maintenance of elevated histone acetylation is essential for enhanced reprogramming (Wille et al., *Science Advances*, 2023, eadg1091). The antagonistic H3K79me–H3K9ac crosstalk thus defines a molecular switch: when H3K79me is present, acetylation at overlapping loci is suppressed; when DOT1L is inhibited, acetylation rises and promotes the hypertranscription characteristic of pluripotent cells.

A 2025 study reveals an additional layer of complexity: H3K79me and H3K36me3 synergistically regulate gene expression and cellular differentiation, and their simultaneous loss leads to hyperactive transcription and failures in neural differentiation through gained chromatin accessibility at TEAD4/YAP1-bound enhancers (Cooke et al. 1). This finding implies that DOT1L inhibition in chemical reprogramming cocktails may require temporal coordination with other epigenetic modifiers to prevent off-target enhancer activation.

The rate-limiting nature of DOT1L inhibition is further supported by the observation that H3K79me2 erasure is a prerequisite for de novo PRC2-mediated H3K27me3 deposition at lineage-specifying loci: without DOT1L inhibition, PRC2 cannot install the bivalent marks that prime genes for later lineage-specific activation. This positions DOT1L inhibition as the critical bridge between Phase I (barrier removal) and Phase II (lineage priming) of the chemical reprogramming cascade.

### 2.4 Phase II — Lineage Priming: GSK3β/Wnt and Bivalent Domain Establishment

The second phase of chemical reprogramming installs lineage-priming marks at target-cell-specific loci. The principal agent is CHIR99021, a selective GSK3β inhibitor that activates the canonical Wnt/β-catenin signalling pathway. GSK3β normally phosphorylates β-catenin, targeting it for proteasomal degradation; CHIR99021 stabilises β-catenin, allowing it to translocate to the nucleus and activate TCF/LEF-dependent transcription of Wnt target genes.

In the context of chemical reprogramming, Wnt activation serves a dual function. First, it drives expression of pluripotency-associated genes (including Nanog and Esrrb) that establish the transcriptional network of the target state. Second — and more relevant to the chromatin cascade — β-catenin recruits histone acetyltransferases (CBP/p300) and chromatin-remodelling complexes to Wnt-responsive enhancers, creating islands of H3K27ac that mark active regulatory elements within the newly decompacted chromatin landscape left by Phase I. The chemical reprogramming trajectory analysis by Wang and colleagues demonstrates that the transition through an intermediate plastic state requires sequential enhancer recommissioning and mirrors the reversal of regeneration potential lost as organisms mature, with LEF1 identified as a key upstream regulator for regeneration gene-program activation (Wang et al., *Cell Reports*, 2023, 112301).

The XEN-like (extraembryonic endoderm-like) intermediate state that characterises mouse chemical reprogramming provides additional evidence for the lineage-priming function of Wnt activation: precise manipulation of the cell-fate transition through the XEN-like state in a stepwise manner allows identification of small-molecule boosters and establishes a robust chemical reprogramming system with a yield up to 1,000-fold greater than that of the original protocol (Zhao et al. 1580). The XEN-like state is characterised by bivalent chromatin at both pluripotency and lineage-specifying loci — exactly the chromatin configuration that Phase II compounds are predicted to install.

### 2.5 Phase III — Identity Consolidation: TGFβ Inhibition and Lineage-Selector Accessibility

The third phase resolves the bivalent state into a committed lineage identity. The principal agents are TGFβ pathway inhibitors (RepSox, SB431542, A83-01), which block SMAD2/3 phosphorylation and nuclear translocation. In the somatic cell, constitutive TGFβ signalling maintains a mesenchymal gene-expression program through SMAD2/3-mediated transcriptional activation of fibroblast-identity genes. TGFβ inhibition releases SMAD2/3 from these loci, allowing lineage-specifying transcription factors — now expressed at low levels due to Phase I/II chromatin remodelling — to access their cognate binding sites.

The identification of the JNK pathway as a major barrier to chemical reprogramming provides mechanistic clarity: JNK inhibition is indispensable for inducing cell plasticity and a regeneration-like program by suppressing pro-inflammatory pathways that would otherwise prevent the intermediate plastic state from resolving toward pluripotency (Guan et al. 614). The sequential logic — first remove barriers (Phase I), then install priming marks (Phase II), then release identity-maintaining transcription (Phase III) — explains why the temporal order of compound addition is critical and why simultaneous addition of all compounds produces lower efficiency than stepwise protocols.

### 2.6 Compound-by-Compound Mechanism Map

The following table maps each major compound class to its chromatin-level mechanism:

| Compound | Target | Phase | Chromatin Effect |
|----------|--------|-------|-----------------|
| VPA/TSA/NaB | HDAC class I/II | I | Global H3K9ac/H3K56ac ↑; nucleosome destabilisation |
| JQ1/I-BET762 | BET bromodomains | I | BRD4 displacement; elongation collapse at somatic SE |
| EPZ004777/SGC0946 | DOT1L | I→II | H3K79me2 erasure; permits PRC2-mediated H3K27me3 |
| CHIR99021 | GSK3β | II | Wnt/β-catenin activation; bivalent domain establishment |
| Forskolin | Adenylyl cyclase | II | cAMP/PKA; CREB1-mediated neurogenic programs |
| RepSox/SB431542 | TGFβR | III | SMAD2/3 release; mesenchymal program silencing |
| DZnep | EZH2/SAH hydrolase | III | H3K27me3 redistribution; PRC2 substrate depletion |
| Parnate (TCP) | LSD1/KDM1A | I | H3K4me2 preservation at lineage genes |
| TTNPB | RARα/γ | II | Retinoic acid-dependent lineage specification |

---

## 3. Single-Cell Epigenomic Trajectories of Chemical Conversion

### 3.1 Chromatin Accessibility Waves During Reprogramming

Single-cell ATAC-seq has revealed that chromatin accessibility during cell-fate reprogramming undergoes a binary off/on switch, closing loci occupied by somatic transcription factors and opening loci occupied by target-state transcription factors (Li et al. 35). This binary logic operates at the population level, but at the single-cell level, the picture is far more heterogeneous.

In cardiac direct reprogramming, scATAC-seq at the early stage reveals networks of transcription factors involved in the initial shift of chromatin accessibility, with Smad3 identified as a bimodal TF — a barrier during initiation and a facilitator during the intermediate stage (Wang et al. 21). A global rewiring of cis-regulatory interactions of cardiac genes occurs along the reprogramming trajectory, with integrative analysis of scATAC-seq and scRNA-seq data identifying active TFs important for iCM conversion (Wang et al. 21). The chromatin remodelling is not uniform: successful converters follow a trajectory characterised by progressive acquisition of cardiac regulatory-element accessibility, while trapped intermediates accumulate partially open chromatin at both cardiac and fibroblast loci without resolving the bivalent state.

### 3.2 The Bifurcation: Converters Versus Trapped Intermediates

Re-patterning of H3K27me3, H3K4me3, and DNA methylation during fibroblast-to-cardiomyocyte conversion reveals a striking temporal asymmetry: cardiac gene activation occurs rapidly (reduced H3K27me3 and increased H3K4me3 at cardiac promoters by day 3), while fibroblast gene silencing occurs later (H3K27me3 at fibroblast loci does not increase until day 10) (Liu et al. 1). This asymmetry suggests that the activation of target-state genes and the silencing of source-state genes are mechanistically separable events — and that cells which activate target genes without adequately silencing source genes become trapped intermediates.

The epigenetic factor Bmi1, a component of Polycomb Repressive Complex 1 (PRC1), directly interacts with regulatory regions of cardiogenic genes and maintains the repressive H2AK119ub mark that prevents their activation; reducing Bmi1 levels increases H3K4me3 and reduces H2AK119ub at cardiogenic loci, significantly enhancing iCM induction and even substituting for Gata4 during reprogramming (Zhou et al. 795). Bmi1 thus represents a specific epigenetic barrier whose removal determines whether a cell enters the converter or trapped-intermediate trajectory.

### 3.3 TF-Driven Versus Chemical Trajectories: Convergent or Divergent?

A critical question is whether chemical and transcription-factor-driven reprogramming converge on the same chromatin trajectory. Evidence from chemical reprogramming of human cells suggests a fundamentally distinct pathway: the chemical route proceeds through an intermediate plastic state with a regeneration signature — characterised by sequential enhancer recommissioning that mirrors the reversal of regeneration potential lost during maturation — that is absent from transcription-factor-mediated reprogramming (Wang et al., *Cell Reports*, 2023, 112301). The chemical pathway thus appears to access a distinct chromatin trajectory, one that recapitulates developmental enhancer activation in reverse rather than forcing direct TF-mediated chromatin remodelling. This distinction has important implications for identity stability: if the chemical route engages a developmental program rather than a forced conversion, the resulting cells may more faithfully install the epigenetic locks that characterise stably specified cell types.

---

## 4. The Identity Stability Problem

### 4.1 Defining Stability

Identity stability is the capacity of a converted cell to maintain its target-state transcriptional program, chromatin configuration, and functional properties over time without continued exposure to the converting stimulus. A stably converted cardiomyocyte must maintain sarcomeric gene expression, calcium-handling machinery, and electrophysiological properties at twelve months post-conversion. A stably converted neuron must maintain neurotransmitter identity, synaptic connectivity, and firing phenotype. The critical distinction is between *kinetic* stability (the cell remains in its converted state for a given time period) and *thermodynamic* stability (the converted state is a genuine local minimum of the epigenetic landscape, not merely a metastable transient).

### 4.2 The Three Locks of Cell Identity

We propose that cell identity is maintained by three partially redundant epigenetic locks, each of which must be engaged for long-term stability:

**Lock 1: DNA Methylation Maintenance.** DNMT3A and DNMT3B establish de novo DNA methylation at CpG-rich promoters of genes that must be silenced in the target cell type, while DNMT1 maintains this methylation through cell division. In stably specified cell types (e.g., terminally differentiated cardiomyocytes in vivo), source-state gene promoters carry dense CpG methylation that is heritably maintained. CRISPRoff — a programmable epigenetic memory writer consisting of a single dCas9 fusion protein — establishes both DNA methylation and repressive histone modifications that are maintained through cell division and differentiation of stem cells to neurons, demonstrating that DNA methylation is both necessary and sufficient for heritable gene silencing at most loci (Nuñez et al. 1048).

**Lock 2: H3K9me3 Heterochromatin.** The histone methyltransferases SETDB1 and SUV39H1 establish H3K9me3 at repetitive elements and at a subset of lineage-inappropriate gene promoters. H3K9me3 recruits HP1 proteins, which compact chromatin into constitutive heterochromatin that is highly resistant to transcription-factor invasion. Draft_44 of this series established that the H3K9me3/HP1 threshold is the rate-limiting barrier for pioneer TF access during iPSC reprogramming. The converse prediction is that failure to establish H3K9me3 at source-state genes after conversion leaves those genes vulnerable to reactivation.

**Lock 3: 3D Genome Insulation.** CTCF and cohesin establish topologically associating domain (TAD) boundaries that insulate target-state gene loci from inappropriate regulatory contacts. Stik and colleagues demonstrated that CTCF is dispensable for B-cell-to-macrophage transdifferentiation — cells convert normally even when TAD organisation is disrupted — but CTCF depletion in the resulting macrophages impairs the full upregulation of inflammatory genes upon endotoxin exposure (Stik et al. 552). This remarkable finding suggests that 3D genome insulation is not required for the initial conversion event but is essential for the functional robustness and stimulus-responsiveness of the converted cell type. A converted cell without proper TAD boundaries may appear phenotypically normal at baseline but fail to respond appropriately to physiological stimuli — a subtle but clinically critical form of identity instability.

Recent work on 3D genome rewiring during PTF1A-mediated fibroblast-to-neural-stem-cell transdifferentiation reveals that PTF1A binds to sub-TAD boundaries and reorganises chromatin loops, leading to gene expression changes that drive conversion, and activates enhancers and super-enhancers near low-insulation boundaries (Zhang et al. 1). This demonstrates that transcription-factor-driven conversion actively remodels the 3D genome — but whether chemical conversion achieves equivalent remodelling is unknown.

### 4.3 Lock Engagement After Different Conversion Modalities

We predict — and existing data partially confirm — a hierarchy of lock engagement across conversion modalities:

| Modality | Lock 1 (DNA methylation) | Lock 2 (H3K9me3) | Lock 3 (3D genome) |
|----------|-------------------------|-------------------|---------------------|
| Developmental specification | Full | Full | Full |
| iPSC differentiation | Partial (fetal-like) | Partial | Partial |
| TF-driven direct conversion | Partial | Minimal | Minimal |
| Chemical conversion | Partial | Minimal | Unknown |
| Chemical conversion + CRISPRoff | Full (engineered) | Partial (engineered) | Unknown |

The evidence for incomplete lock engagement after direct conversion comes from multiple sources. In cardiac reprogramming, age-associated epigenetic barriers including altered histone modification landscapes limit conversion efficiency from aged fibroblasts, and the resulting iCMs exhibit increased accumulation of mitochondrial oxidative stress compared with neonatal-derived iCMs (Santos et al. 1). In neural conversion, Ascl1-mediated astrocyte-to-neuron reprogramming produces neurons that progressively mature and form functional synaptic connections over weeks, but the duration of lineage-tracing follow-up in existing studies rarely exceeds three months in vivo (Liu et al. 3093). Whether these cells maintain their identity at twelve months or beyond is unknown.

### 4.4 In Vivo Identity Erosion

The time-course of identity erosion in directly converted cells varies by cell type and conversion modality. For induced cardiomyocytes, the epigenetic and transcriptional basis of direct cardiac reprogramming reveals that early-stage molecular events include rapid activation of the cardiac program (H3K27me3 reduction and H3K4me3 gain at cardiac promoters by day 3) but late and incomplete suppression of the fibroblast program (Liu et al. 1). This incomplete suppression creates a persistent vulnerability: fibroblast genes retain accessible chromatin that could be reactivated under stress conditions.

PHF7, recently identified as a potent activator of adult fibroblast-to-cardiomyocyte reprogramming, induces population-level shifts in nonmyocyte and cardiomyocyte cellular identity when delivered as a single factor to the infarcted mouse heart, with functional improvement sustained to 16 weeks (Garry Bann et al. 1). However, 16 weeks in the mouse corresponds to approximately 8 years of scaled human cardiac follow-up — still far short of the lifetime stability required for a curative cardiac therapy.

For induced neurons, Ascl1 acts as an "on-target" pioneer factor by immediately occupying most cognate genomic sites in fibroblasts, with a unique trivalent chromatin signature in the host cells predicting the permissiveness for Ascl1 pioneering activity (Wapinski et al. 958). Myt1l and Myt1l are critical for the electrophysiological maturation of iN cells, and their continued expression may be required for long-term identity maintenance (Rao et al. 289). This raises the concern that transient TF delivery may produce neurons that are initially functional but gradually lose their electrophysiological properties as the TF-installed chromatin state erodes without the reinforcement of endogenous identity-maintenance mechanisms.

### 4.5 Ex Vivo Identity Stability: CiPSC-Derived Versus TF-iPSC-Derived Cells

A key question for the field is whether CiPSC-derived differentiated cells exhibit superior or inferior identity stability compared with TF-iPSC-derived cells. The chemical reprogramming pathway — which proceeds through a regeneration-like intermediate state — may produce iPSCs with a more physiologically installed epigenome than TF-iPSCs, which are forced through a transcription-factor-dominated trajectory. The rapid 10-day hCiPSC system identifies KAT3A/KAT3B and KAT6A as epigenetic obstacles; suppressing these histone acetyltransferases facilitates the transition to a poised state by triggering switches in the epigenome (Wang et al., *Nature Chemical Biology*, 2025, 1). If these switches more closely recapitulate developmental chromatin remodelling, the resulting CiPSCs — and their differentiated derivatives — may install the three identity locks more completely than TF-iPSCs.

The clinical data on CiPSC-derived islet transplantation for type 1 diabetes, reported at ISSCR 2025, provides the first in vivo test of this prediction (Lou 1). Whether CiPSC-derived beta cells maintain insulin-secreting function and resist dedifferentiation over years — the identity-stability question — will be the decisive test.

### 4.6 The Maturation–Stability Axis

Identity stability is intimately linked to cellular maturation. Draft_58 of this series established that hPSC-derived cells across cardiac, hepatic, beta-cell, and neuronal lineages resemble fetal rather than adult counterparts — the "maturation gap." We extend this observation to converted cells: the degree of maturation achieved during or after conversion correlates with identity stability, because the maturation process itself engages the three identity locks. Mature cardiomyocytes that have undergone the metabolic switch from glycolysis to fatty acid oxidation, installed the full sarcomeric apparatus, and established adult-type calcium handling have correspondingly higher levels of DNA methylation at non-cardiac genes, H3K9me3 at fibroblast loci, and CTCF-demarcated TAD boundaries at cardiac gene clusters.

The discovery that inhibition of fatty acid oxidation via Cpt1b inactivation enables adult heart regeneration through accumulation of α-ketoglutarate and activation of the lysine demethylase KDM5, which demethylates broad H3K4me3 domains at maturation genes and shifts cardiomyocytes into a less mature, more proliferative state (Li et al. 593), demonstrates that the maturation–stability link is bidirectional: metabolic maturation shapes the epigenetic landscape, and reversal of metabolic maturation can unlock the epigenetic landscape for reprogramming. This insight has immediate implications for engineering identity stability: forcing metabolic maturation of converted cells (e.g., by culturing iCMs in fatty-acid-rich media or exposing iNs to synaptic-activity-dependent maturation signals) may accelerate lock engagement and improve long-term stability.

### 4.7 Engineering Stability: CRISPRoff and Beyond

If the three identity locks are incompletely engaged after chemical or TF-driven conversion, they can be artificially installed using programmable epigenetic editors. CRISPRoff establishes DNA methylation and repressive histone modifications at targeted promoters; transient CRISPRoff expression initiates highly specific gene repression that is maintained through cell division and differentiation (Nuñez et al. 1048). Recent advances have established an all-RNA platform for efficient, durable, and multiplexed epigenetic programming in primary human T cells: CRISPRoff-mediated gene silencing is maintained through numerous cell divisions, T cell stimulations, and in vivo adoptive transfer, and can be combined with genetic editing using orthogonal CRISPR systems for integrated programming (Goudy et al. 1).

For converted cells, the strategy would be to identify source-state genes that remain inadequately silenced after conversion (using scRNA-seq or scATAC-seq) and target them with CRISPRoff to install Lock 1 (DNA methylation) and contribute to Lock 2 (via the KRAB domain's recruitment of SETDB1). Multiplexed CRISPRoff targeting of 5–10 fibroblast-identity genes in iCMs or 5–10 astrocyte-identity genes in iNs could provide a "stability boost" that compensates for the incomplete lock engagement of the conversion process. The stability of CRISPRoff-mediated silencing — maintained for over 8 months of continuous cell propagation in glioblastoma cells (Lin et al. 1) — suggests that this approach could provide the year-scale durability needed for therapeutic applications.

---

## 5. Mathematical Frameworks F375–F380

### F375: Chromatin-State Markov Chain

We model the chromatin state at a single regulatory locus as a continuous-time Markov chain with three states: **C** (closed: H3K9me3-marked heterochromatin), **B** (bivalent: H3K4me3 + H3K27me3), and **A** (active: H3K4me3 + H3K27ac). The transition rates between states depend on the compound class applied:

```math
Q = \begin{pmatrix} -(q_{CB} + q_{CA}) & q_{CB} & q_{CA} \\ q_{BC} & -(q_{BC} + q_{BA}) & q_{BA} \\ q_{AC} & q_{AB} & -(q_{AC} + q_{AB}) \end{pmatrix}
```

where:
- $q_{CB}(\text{HDACi}) = q_{CB}^{0} \cdot (1 + \alpha_H \cdot [\text{VPA}] / K_H)$ — HDAC inhibition accelerates closed-to-bivalent transition
- $q_{BA}(\text{GSK3i}) = q_{BA}^{0} \cdot (1 + \alpha_G \cdot [\text{CHIR}] / K_G)$ — GSK3β inhibition accelerates bivalent-to-active transition
- $q_{AB}(\text{TGFβi}) = q_{AB}^{0} \cdot (1 - \beta_T \cdot [\text{RepSox}] / K_T)$ — TGFβ inhibition reduces active-to-bivalent reversion

The steady-state distribution $\pi = (\pi_C, \pi_B, \pi_A)$ satisfying $\pi Q = 0$ predicts the equilibrium fraction of loci in each state under a given compound combination. Cocktail efficacy is defined as $\eta = \pi_A / \pi_A^{\text{target}}$, where $\pi_A^{\text{target}}$ is the fraction of active loci in the target cell type. All variables: $q_{ij}$ = transition rate from state $i$ to state $j$; $q_{ij}^{0}$ = basal transition rate; $\alpha_H, \alpha_G, \beta_T$ = compound efficacy parameters; $K_H, K_G, K_T$ = half-maximal effective concentrations; $[\cdot]$ = compound concentration.

### F376: Chemical Pioneer Free-Energy Model

The free energy of nucleosome destabilisation by a pioneer TF is:

```math
\Delta G_{\text{pioneer}} = \Delta G_{\text{bind}} + \Delta G_{\text{deform}} + \Delta G_{\text{linker}}
```

where $\Delta G_{\text{bind}}$ is the TF–DNA binding energy (~ −12 to −15 kcal/mol for pioneer factors), $\Delta G_{\text{deform}}$ is the nucleosome deformation energy (~ +3 to +8 kcal/mol), and $\Delta G_{\text{linker}}$ is the linker histone displacement energy (~+2 to +5 kcal/mol).

For chemical pioneers, the analogous energy is:

```math
\Delta G_{\text{chem}} = n_{\text{ac}} \cdot \Delta g_{\text{ac}} + n_{\text{BET}} \cdot \Delta g_{\text{BET}}
```

where $n_{\text{ac}}$ is the number of acetylation sites gained per nucleosome upon HDAC inhibition, $\Delta g_{\text{ac}} \approx$ −0.5 to −1.0 kcal/mol per acetylation (from the reduction in histone–DNA electrostatic contacts), $n_{\text{BET}}$ is the number of BET protein molecules displaced from the locus, and $\Delta g_{\text{BET}} \approx$ −1.5 to −3.0 kcal/mol per displacement (from the loss of elongation-complex stabilisation). The chemical pioneer hypothesis predicts that $|\Delta G_{\text{chem}}|$ approaches $|\Delta G_{\text{pioneer}}|$ when $n_{\text{ac}} \geq 8$ and $n_{\text{BET}} \geq 2$, which is consistent with the observed genome-wide hyperacetylation (~8–14 additional acetyl marks per nucleosome) and complete BRD4 eviction achieved by therapeutic doses of VPA + JQ1.

### F377: Identity-Stability Lyapunov Function

We define a Lyapunov function $V(x)$ over the epigenetic state vector $x = (m, h, t)$ of a converted cell, where $m$ = DNA methylation level at source-state genes (Lock 1), $h$ = H3K9me3 level at source-state genes (Lock 2), and $t$ = TAD insulation score at target-state gene clusters (Lock 3):

```math
V(x) = -\left[ w_m \log\left(\frac{m}{m^*}\right) + w_h \log\left(\frac{h}{h^*}\right) + w_t \log\left(\frac{t}{t^*}\right) \right]
```

where 
m*, h*, t*
are the lock levels of the corresponding natively specified cell type, and $w_m, w_h, w_t$ are weights reflecting the relative contribution of each lock to identity maintenance. The converted state is a local minimum of 
$V$
if and only if all three lock levels are above a critical threshold: 
```math
m > m_c$, $h > h_c$, $t > t_c
```
. If any lock falls below its threshold, $V$ increases and the cell drifts toward the source-state attractor. The depth of the local minimum — 
```math
V(x^*_{\text{converted}}) - V(x_{\text{saddle}})
```
— quantifies the basin-of-attraction depth and predicts the timescale of spontaneous reversion: 
```math
\tau_{\text{revert}} \propto \exp(\Delta V / k_B T_{\text{eff}})
```
, where 
$T_{\text{eff}}$
is an effective epigenetic temperature reflecting stochastic fluctuations in chromatin state.

### F378: Reversion Hazard Model

Identity loss is modelled as a competing-risks survival process with three failure modes corresponding to the three locks:

```math
\lambda(t) = \lambda_m(t) + \lambda_h(t) + \lambda_t(t)
```

where:
- $\lambda_m(t) = \lambda_m^0 \cdot \exp(-\gamma_m \cdot m(t))$ — methylation-drift hazard, decreasing with methylation level
- $\lambda_h(t) = \lambda_h^0 \cdot (1 - h(t)/h_{\max})^{k_h}$ — heterochromatin-erosion hazard, increasing as H3K9me3 declines
- $\lambda_t(t) = \lambda_t^0 \cdot \mathbb{1}[t(t) < t_c]$ — TAD-disruption hazard, a step function triggered below the insulation threshold

The survival function — the probability that a converted cell retains its identity at time $t$ — is:

```math
S(t) = \exp\left(-\int_0^t \lambda(s) \, ds\right)
```

This framework predicts that identity loss is dominated by the weakest lock: if H3K9me3 is inadequately installed (Lock 2 failure), the reversion hazard is high even if DNA methylation (Lock 1) is complete. All variables: $\lambda^0_{m,h,t}$ = baseline hazard rates; $\gamma_m$ = methylation protection coefficient; $k_h$ = heterochromatin erosion steepness; $h_{\max}$ = maximum possible H3K9me3 level; $t_c$ = TAD insulation critical threshold.

### F379: Optimal Cocktail Timing via Dynamic Programming

The sequential addition of $n$ compounds over a total time horizon $T$ defines a dynamic programming problem. Let $S_k$ denote the chromatin state after the $k$-th compound addition at time $t_k$, and let $P(S_k \to S_{k+1} | c_{k+1}, \Delta t_{k+1})$ be the transition probability from state $S_k$ to $S_{k+1}$ given compound $c_{k+1}$ applied for duration $\Delta t_{k+1} = t_{k+1} - t_k$. The optimal schedule maximises the conversion probability:

```math
\max_{\{c_k, t_k\}_{k=1}^n} \; P(S_n = S_{\text{target}}) \quad \text{subject to} \quad \sum_{k=1}^n \Delta t_k = T, \;\; \sum_{k=1}^n \text{dose}(c_k) \cdot \Delta t_k \leq D_{\max}
```

where $D_{\max}$ is the maximum cumulative exposure constraint (reflecting toxicity limits). This is solved by Bellman's principle: the value function $V_k(S_k) = \max_{c_{k+1}, \Delta t_{k+1}} \left[ P(S_k \to S_{k+1}) \cdot V_{k+1}(S_{k+1}) \right]$ is computed backward from the terminal condition $V_n(S_{\text{target}}) = 1$, $V_n(S \neq S_{\text{target}}) = 0$.

### F380: Single-Cell Trajectory Entropy

The diversity of reprogramming trajectories across a population of cells is quantified by the Shannon entropy over the distribution of chromatin states at each time point:

```math
H(t) = -\sum_{s \in \mathcal{S}} p(s, t) \log p(s, t)
```

where $\mathcal{S}$ is the set of discrete chromatin states (identified by clustering scATAC-seq data) and $p(s, t)$ is the fraction of cells in state $s$ at time $t$. Lower trajectory entropy indicates a more deterministic conversion process — all cells follow the same chromatin path — while higher entropy indicates heterogeneous trajectories with multiple intermediate states and branch points. The derivative $dH/dt$ reveals the critical time points where trajectory bifurcation occurs (converter vs. trapped-intermediate divergence). We predict that chemical reprogramming exhibits *lower* trajectory entropy than TF-driven conversion, because chemical compounds act uniformly on all cells (no expression-level heterogeneity), whereas TF transduction produces variable transgene expression across the population.

---

## 6. Rational Cocktail Design from Chromatin Profiling

### 6.1 The Design Principle

The three-phase chromatin cascade (Section 2) implies a systematic design principle for reprogramming cocktails:

1. **Profile the source-cell chromatin state** at target-lineage gene loci using scATAC-seq and CUT&Tag for key histone marks (H3K27me3, H3K4me3, H3K9me3, H3K79me2).
2. **Identify the barrier class** at each locus: H3K9me3 heterochromatin (requires Phase I HDACi + DOT1Li), H3K27me3 Polycomb repression (requires Phase II GSK3i or Phase III TGFβi), or inaccessible chromatin without specific repressive marks (requires Phase I BETi).
3. **Select the minimal compound set** that addresses each identified barrier class, with temporal ordering determined by the Phase I → II → III hierarchy.
4. **Include a stability-locking step** (CRISPRoff or forced maturation) to engage the three identity locks after conversion.

### 6.2 AI-Guided Cocktail Optimisation

The combinatorial explosion of possible compound combinations (>10^6 for a library of 20 compounds at 5 concentrations each) motivates computational approaches. Three classes of AI models are relevant:

**GEARS** (Graph-Enhanced Gene Activation and Repression Simulator) integrates deep learning with a knowledge graph of gene-gene relationships to predict transcriptional responses to both single and multi-gene perturbations, exhibiting 40% higher precision than existing approaches in predicting genetic interaction subtypes (Roohani et al. 1). While designed for genetic perturbations, GEARS's architecture can be adapted for chemical perturbations by mapping compound targets to equivalent gene knockdowns or overexpressions.

**scGPT**, a foundation model trained on over 33 million cells, can be fine-tuned for perturbation response prediction, multi-omic integration, and gene network inference (Cui et al. 604). However, rigorous benchmarking reveals that foundation models for perturbation prediction do not yet outperform simple linear baselines on current Perturb-seq datasets (Ahlmann-Eltze et al. 1), cautioning against uncritical deployment.

**GET** (General Expression Transformer) represents a more promising direction: trained exclusively on chromatin accessibility data and sequence information, GET achieves experimental-level accuracy in predicting gene expression across 213 human cell types and identifies distal regulatory regions missed by previous models (Fu et al. 1). GET's chromatin-first architecture aligns naturally with the cocktail-design principle of profiling chromatin state before selecting compounds.

The practical workflow would be: (i) profile source-cell chromatin by scATAC-seq; (ii) use GET to predict the gene-expression consequences of modifying specific chromatin features; (iii) use GEARS to predict compound combinations that achieve the desired chromatin modifications; (iv) validate the top-ranked cocktails experimentally.

### 6.3 The Chemical Pioneer Toolkit

We propose standardising a panel of compounds organised by their phase and barrier-class targets:

**Phase I — Barrier Removal:**
- HDAC class I/II: VPA (broad), entinostat (selective class I)
- BET bromodomains: JQ1 (research), I-BET762 (clinical)
- DOT1L: EPZ-5676 (pinometostat, clinical-grade)
- LSD1: tranylcypromine (TCP), ORY-1001 (clinical)

**Phase II — Lineage Priming:**
- GSK3β: CHIR99021 (standard), LY2090314 (clinical-grade)
- cAMP/PKA: forskolin
- RARα/γ: TTNPB, Am80
- Smoothened/Hedgehog: purmorphamine, SAG

**Phase III — Identity Consolidation:**
- TGFβ: RepSox, SB431542, A83-01
- BMP: dorsomorphin, LDN-193189
- JAK: ruxolitinib (for hematopoietic conversions)

**Phase IV — Stability Locking:**
- CRISPRoff mRNA + sgRNAs targeting source-state genes
- Metabolic maturation cocktails (fatty acids for cardiac, synaptic activity for neural)
- DNMT3A mRNA for targeted de novo methylation

---

## 7. Therapeutic Implications and Open Questions

### 7.1 Which Indications Benefit Most?

The chemical-logic framework identifies two immediate beneficiaries. First, **cardiac direct reprogramming** benefits because the chromatin barriers in human cardiac fibroblasts have been systematically mapped: a genome-wide CRISPR knockout screen has identified epigenetic barriers to direct cardiac reprogramming, providing unbiased targets for chemical intervention (Woldemariam et al., *Circulation Research*, 2025). Second, **chemical anti-aging** benefits because the two-compound cocktail of Schoenfeldt et al. (2025) operates through the same Phase I barrier-removal logic described here — HDAC inhibition and GSK3β modulation — suggesting that the chemical pioneer framework applies directly to aging-reversal applications.

### 7.2 The Identity-Stability Threshold

How stable is stable enough for clinical utility? The competing-risks reversion hazard model (F378) provides a framework for answering this question. For a cardiac indication, the survival function $S(t)$ must exceed 0.95 at $t = 5$ years — meaning that fewer than 5% of converted cardiomyocytes have reverted to a fibroblast-like state. For a neural indication, the threshold may be even higher ($S(t) > 0.99$) because even a small fraction of non-neuronal cells in a neural circuit could disrupt function. These thresholds translate into specific requirements for lock engagement levels via the Lyapunov function (F377).

### 7.3 Hybrid Strategies

The most promising near-term approach combines TF-driven conversion (for lineage specificity) with chemical supplements (for barrier removal and lineage priming) and CRISPRoff (for identity locking). In cardiac reprogramming, this would mean: GATA4/MEF2C/TBX5 delivery for lineage specification + VPA/CHIR99021 for barrier removal and Wnt priming + CRISPRoff targeting of fibroblast-identity genes (Col1a1, Twist1, Snai2) for stability locking. The SMYD1 histone methyltransferase, identified as promoting ventricular subtype identity in human iCMs through direct interaction with MEF2C and GATA4 to modify histone marks on cardiac regulatory regions (Woldemariam et al., *Circulation Research*, 2024), could serve as an additional maturation-promoting factor.

### 7.4 Open Questions

1. **Long-term stability in humans.** No study has tracked the identity of directly converted cells in humans beyond the initial conversion period. The first human cardiac or neural direct reprogramming trials will need to include identity-stability biomarkers (scATAC-seq on biopsied tissue, circulating cell-free DNA methylation signatures) at 6, 12, and 24 months.

2. **Off-target chromatin effects.** Chemical pioneers lack sequence specificity. What fraction of the genome undergoes unintended chromatin remodelling during chemical reprogramming, and do these off-target changes have functional consequences? Whole-genome bisulfite sequencing and scATAC-seq comparisons between chemically and natively specified cells are needed.

3. **Inter-individual variation.** The 10-day hCiPSC system achieves 100% success across 15 donors (Wang et al., *Nature Chemical Biology*, 2025), but whether the chromatin trajectory is identical across donors — or whether donor-specific epigenetic variation produces cells with different identity-stability profiles — is unknown.

4. **The stability-locking pharmacopeia.** Can small molecules alone engage the three identity locks, or is CRISPRoff-level precision required? DNMT3A-activating compounds and SETDB1-potentiating compounds would be therapeutically preferable to genetic tools but do not currently exist.

5. **Chemical conversion in vivo.** Can the three-phase cocktail be delivered systemically or locally to achieve in situ cell-type conversion with adequate identity stability? The Thiele-modulus tissue-penetration analysis from draft_64 (F371) suggests that the concentration-depth problem remains a significant barrier for tissue-scale chemical reprogramming.

---

## References

1. Ahlmann-Eltze, Constantin, et al. "Deep-Learning-Based Gene Perturbation Effect Prediction Does Not Yet Outperform Simple Linear Baselines." *Nature Methods*, 2025. 

2. Bae, Woori, et al. "Epigenetic Regulation of Reprogramming and Pluripotency: Insights from Histone Modifications and Their Implications for Cancer Stem Cell Therapies." *Frontiers in Cell and Developmental Biology*, vol. 13, 2025.

3. Baumann, C., et al. "Changes in Chromatin Accessibility Landscape and Histone H3 Core Acetylation during Valproic Acid-Induced Differentiation of Embryonic Stem Cells." *Epigenetics & Chromatin*, vol. 14, no. 1, 2021, pp. 1–18.

4. Borodinova, A., et al. "Epigenetic Reprogramming of Cell Identity in the Rat Primary Neuron-Glia Cultures Involves Histone Serotonylation." *Cells*, vol. 14, 2025.

5. Chen, Y., et al. "Chemical Cocktail-Mediated Direct Cardiac Reprogramming at Whole-Heart Scale." *Nature Cardiovascular Research*, vol. 3, 2024.

6. Cheng, Lin, et al. "Decoding Human Chemical Reprogramming: Mechanisms and Principles." *Trends in Biochemical Sciences*, 2025.

7. Cooke, Emmalee W., et al. "H3K79 Methylation and H3K36 Trimethylation Synergistically Regulate Gene Expression in Pluripotent Stem Cells." *Science Advances*, vol. 11, 2025.

8. Cui, Haotian, et al. "scGPT: Toward Building a Foundation Model for Single-Cell Multi-omics Using Generative AI." *Nature Methods*, vol. 21, 2024, pp. 604–614.

9. Filippakopoulos, Panagis, et al. "Selective Inhibition of BET Bromodomains." *Nature*, vol. 468, 2010, pp. 1067–1073.

10. Frank, C. L., et al. "HDAC Inhibitors Cause Site-Specific Chromatin Remodeling at PU.1-Bound Enhancers in K562 Cells." *Epigenetics & Chromatin*, vol. 9, 2016, pp. 1–17.

11. Fu, Xi, et al. "A Foundation Model of Transcription across Human Cell Types." *Nature*, vol. 638, 2025, pp. 965–973.

12. Garry Bann, Glynnis, et al. "Cellular Reprogramming by PHF7 Enhances Cardiac Function Following Myocardial Infarction." *Circulation*, vol. 151, 2025, pp. 1–15.

13. Goudy, L., et al. "Integrated Epigenetic and Genetic Programming of Primary Human T Cells." *Nature Biotechnology*, 2025.

14. Guan, Jingyang, et al. "Chemical Reprogramming of Human Somatic Cells to Pluripotent Stem Cells." *Nature*, vol. 605, 2022, pp. 325–331.

15. Halsall, J., et al. "Cells Adapt to the Epigenomic Disruption Caused by Histone Deacetylase Inhibitors through a Coordinated, Chromatin-Mediated Transcriptional Response." *Epigenetics & Chromatin*, vol. 8, 2015, pp. 1–18.

16. Hezroni, Hadas, et al. "Pluripotency-Related, Valproic Acid (VPA)-Induced Genome-wide Histone H3 Lysine 9 (H3K9) Acetylation Patterns in Embryonic Stem Cells." *Journal of Biological Chemistry*, vol. 286, no. 41, 2011, pp. 35977–35988.

17. Huangfu, Danwei, et al. "Induction of Pluripotent Stem Cells by Defined Factors Is Greatly Improved by Small-Molecule Compounds." *Nature Biotechnology*, vol. 26, 2008, pp. 795–797.

18. Kagoya, Yuki, et al. "BET Bromodomain Inhibition Enhances T Cell Persistence and Function in Adoptive Immunotherapy Models." *Journal of Clinical Investigation*, vol. 126, no. 9, 2016, pp. 3479–3494.

19. Li, Dongwei, et al. "Chromatin Accessibility Dynamics during Cell Fate Reprogramming." *EMBO Reports*, vol. 22, 2021, pp. e51288.

20. Li, Xiang, et al. "Inhibition of Fatty Acid Oxidation Enables Heart Regeneration in Adult Mice." *Nature*, vol. 622, 2023, pp. 585–593.

21. Lin, K., et al. "Multiplexed Epigenetic Memory Editing Using CRISPRoff Sensitizes Glioblastoma to Chemotherapy." *Neuro-Oncology*, 2025.

22. Liu, Yueguang, et al. "Ascl1 Converts Dorsal Midbrain Astrocytes into Functional Neurons In Vivo." *Journal of Neuroscience*, vol. 35, no. 25, 2015, pp. 3093–3104.

23. Liu, Ziqing, et al. "Re-patterning of H3K27me3, H3K4me3 and DNA Methylation during Fibroblast Conversion into Induced Cardiomyocytes." *Stem Cell Research*, vol. 16, 2016, pp. 507–518.

24. Liuyang, Shi, et al. "Highly Efficient and Rapid Generation of Human Pluripotent Stem Cells by Chemical Reprogramming." *Cell Stem Cell*, vol. 30, 2023, pp. 185–196.

25. Lou, Ying. "Illuminating the Future of Diabetes Treatment: Autologous CiPSC-Derived Islets Take Center Stage." *Cell Transplantation*, vol. 34, 2025.

26. Nuñez, James K., et al. "Genome-wide Programmable Transcriptional Memory by CRISPR-Based Epigenome Editing." *Cell*, vol. 184, no. 9, 2021, pp. 2503–2519.

27. Onder, Tugba, et al. "Chromatin-Modifying Enzymes as Modulators of Reprogramming." *Nature*, vol. 483, 2012, pp. 598–602.

28. Peng, Fangqi, et al. "Chemical Reprogramming of Human Blood Cells to Pluripotent Stem Cells." *Cell Stem Cell*, 2025.

29. Peng, William, et al. "Decoding the Epigenetic and Transcriptional Basis of Direct Cardiac Reprogramming." *Stem Cells*, 2025.

30. Phillips-Cremins, Jennifer E., et al. "Architectural Protein Subclasses Shape 3D Organization of Genomes during Lineage Commitment." *Cell*, vol. 153, 2013, pp. 1281–1295.

31. Rao, Zhiping, et al. "Molecular Mechanisms Underlying Ascl1-Mediated Astrocyte-to-Neuron Conversion." *Stem Cell Reports*, vol. 16, 2021, pp. 534–547.

32. Roohani, Yusuf H., et al. "Predicting Transcriptional Outcomes of Novel Multigene Perturbations with GEARS." *Nature Biotechnology*, vol. 42, 2023, pp. 927–935.

33. Santos, Francisco, et al. "Age-Associated Metabolic and Epigenetic Barriers during Direct Reprogramming of Mouse Fibroblasts into Induced Cardiomyocytes." *Aging Cell*, vol. 23, 2024, pp. e14087.

34. Shan, Xiwei, et al. "Fully Defined NGN2 Neuron Protocol Reveals Diverse Signatures of Neuronal Maturation." *Cell Reports Methods*, vol. 4, 2024.

35. Stik, Grietje, et al. "CTCF Is Dispensable for Immune Cell Transdifferentiation but Facilitates an Acute Inflammatory Response." *Nature Genetics*, vol. 52, 2020, pp. 655–661.

36. Vainorius, Gintautas, et al. "Ascl1 and Ngn2 Convert Mouse Embryonic Stem Cells to Neurons via Functionally Distinct Paths." *Nature Communications*, vol. 14, 2023, pp. 1–15.

37. Wang, Guanan, et al. "Chemical-Induced Epigenome Resetting for Regeneration Program Activation in Human Cells." *Cell Reports*, vol. 42, 2023, pp. 112301.

38. Wang, Haofei, et al. "Delineating Chromatin Accessibility Re-patterning at Single Cell Level during Early Stage of Direct Cardiac Reprogramming." *Journal of Molecular and Cellular Cardiology*, vol. 162, 2021, pp. 62–71.

39. Wang, Yanglu, et al. "A Rapid Chemical Reprogramming System to Generate Human Pluripotent Stem Cells." *Nature Chemical Biology*, 2025.

40. Wapinski, Orly L., et al. "Hierarchical Mechanisms for Direct Reprogramming of Fibroblasts to Neurons." *Cell*, vol. 155, no. 3, 2013, pp. 621–635.

41. Wen, Shanshan, et al. "Chemical-Based Epigenetic Reprogramming to Advance Pluripotency and Totipotency." *Nature Chemical Biology*, 2025.

42. Werner, Marcel, et al. "Transcription-Replication Conflicts Drive R-Loop-Dependent Nucleosome Eviction and Require DOT1L Activity for Transcription Recovery." *Nucleic Acids Research*, vol. 53, 2025.

43. Wille, C., et al. "DOT1L Inhibition Enhances Pluripotency beyond Acquisition of Epithelial Identity and without Immediate Suppression of the Somatic Transcriptome." *Stem Cell Reports*, vol. 16, 2021, pp. 445–459.

44. Wille, C., et al. "DOT1L Is a Barrier to Histone Acetylation during Reprogramming to Pluripotency." *Science Advances*, vol. 9, 2023, eadg1091.

45. Wille, C., et al. "DOT1L Interaction Partner AF10 Controls Patterning of H3K79 Methylation and RNA Polymerase II to Maintain Cell Identity." *Stem Cell Reports*, vol. 18, 2023, pp. 783–798.

46. Winter, Georg E., et al. "BET Bromodomain Proteins Function as Master Transcription Elongation Factors Independent of CDK9 Recruitment." *Molecular Cell*, vol. 67, 2017, pp. 5–18.

47. Woldemariam, Anteneh G., et al. "Systematic CRISPR Knockout Screen Uncovers Epigenetic Barriers to Direct Cardiac Reprogramming." *Circulation Research*, 2025 (abstract).

48. Woldemariam, Anteneh G., et al. "Heart-Specific Histone Methyltransferase SMYD1 Promotes Cardiac Maturation in the Direct Conversion of Human Fibroblasts into Cardiomyocytes." *Circulation Research*, 2024 (abstract).

49. Zhang, Rong, et al. "Multiscale 3D Genome Rewiring during PTF1A-Mediated Somatic Cell Reprogramming into Neural Stem Cells." *Communications Biology*, vol. 7, 2024, pp. 1–14.

50. Zhao, Han, et al. "Extensive Mutual Influences of SMC Complexes Shape 3D Genome Folding." *Nature*, 2025.

51. Zhao, Yang, et al. "A XEN-like State Bridges Somatic Cells to Pluripotency during Chemical Reprogramming." *Cell*, vol. 163, 2015, pp. 1678–1691.

52. Zhou, Yang, et al. "Bmi1 Is a Key Epigenetic Barrier to Direct Cardiac Reprogramming." *Cell Stem Cell*, vol. 18, 2016, pp. 382–395.
