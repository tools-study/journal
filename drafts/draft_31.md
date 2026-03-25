# Synthetic Regulatory Genomics Review

## Abstract

The convergence of massively parallel reporter assays, deep learning, and synthetic biology has transformed our capacity to read, predict, and write the regulatory code governing gene expression. This review synthesizes advances across the rapidly maturing field of synthetic regulatory genomics, from high-throughput functional characterization of cis-regulatory elements to the de novo design of synthetic enhancers and promoters with programmable cell-type specificity. We examine how quantitative models trained on data from massively parallel reporter assays (MPRAs) and self-transcribing active regulatory region sequencing (STARR-seq) now enable the rational design of synthetic regulatory elements that outperform their natural counterparts. We survey the state of the art in deep learning architectures — including Enformer, Borzoi, and sequence diffusion models — that predict gene expression from DNA sequence and generate novel regulatory elements with specified activity profiles. We further review advances in synthetic gene circuits for mammalian cells, encompassing CRISPRa/CRISPRi-based feedback controllers, synthetic Notch receptors, and logic-gated CAR-T cells. The integration of engineered regulatory elements with three-dimensional genome architecture, tissue engineering, and cell-free prototyping systems is discussed. Finally, we identify critical open questions regarding enhancer grammar, chromatin context dependence, and the clinical translation of synthetic regulatory elements for next-generation gene and cell therapies.

---

## 1. Introduction

**Synthetic regulatory elements designed by machine learning now outperform natural genomic sequences in driving cell-type-specific gene expression**, marking a paradigm shift in our ability to program cellular behavior at the transcriptional level. This capability — unimaginable a decade ago — has emerged from the convergence of three technological revolutions: massively parallel functional genomics, deep learning for sequence-to-function prediction, and scalable mammalian synthetic biology.

The human genome encodes an estimated **1 million candidate cis-regulatory elements** (cCREs), yet the functional logic governing how combinations of transcription factor binding sites encode cell-type-specific expression patterns remains incompletely understood (Agarwal et al., 2025). Classical approaches to dissecting regulatory element function — testing one element at a time with luciferase reporters — were fundamentally rate-limiting. The development of massively parallel reporter assays (MPRAs) shattered this bottleneck, enabling simultaneous quantitative measurement of hundreds of thousands of sequences in a single experiment (Klein et al., 2020). Concurrently, deep learning models progressed from predicting chromatin accessibility at individual loci to modeling gene expression across entire chromosomal domains, with architectures like Enformer processing **196 kilobases** of input sequence (Avsec et al., 2021) and its successor Borzoi extending this to **524 kilobases** with RNA-seq-level resolution (Linder et al., 2025).

These advances have converged to enable a "design-build-test-learn" cycle for regulatory DNA. Machine learning models trained on MPRA data can now design synthetic enhancers with specified cell-type activity profiles, and generative approaches including diffusion models produce entirely novel sequences that achieve tissue-specific gene regulation in vivo (Gosai et al., 2024; DaSilva et al., 2026; Taskiran et al., 2024). When integrated with synthetic gene circuit engineering — including logic gates, feedback controllers, and engineered receptors — these tools open the door to fully programmable cellular behavior for therapeutic applications ranging from precision gene therapy to smart CAR-T cells.

This review provides a comprehensive synthesis of the field as of early 2026, organized around the central theme of engineering transcriptional control for programmable cell behavior. We trace the pathway from functional characterization of natural regulatory elements, through computational prediction and design, to the construction of synthetic circuits and their integration into therapeutic and tissue engineering contexts.

---

## 2. Massively parallel reporter assays decode the cis-regulatory grammar

### From thousands to hundreds of thousands of elements in a single experiment

The development of lentiviral MPRAs (lentiMPRAs) represented a critical advance over episomal reporter assays by integrating reporter constructs into chromatin, thereby capturing the influence of nucleosome positioning and epigenetic modifications on regulatory element function. A systematic evaluation of nine MPRA designs by Klein et al. (2020) demonstrated that while episomal and integrated enhancer activities correlate well (Pearson R > 0.8), chromatin context meaningfully modulates quantitative output, particularly for weaker elements.

The field reached an inflection point in January 2025 when Agarwal et al. (2025) reported the largest lentiMPRA study to date, testing **over 680,000 sequences** representing extensively annotated cCREs across three ENCODE cell types (HepG2, K562, and WTC11). This landmark study found that **41.7% of tested cCREs were active** in at least one cell type, with promoter 200-nucleotide cores functioning as largely non-cell-type-specific activation switches, while enhancers displayed substantially greater tissue specificity. The study also demonstrated that sequence-based machine learning models trained on this data could predict both cCRE function and the effects of genetic variants with high accuracy.

In parallel, Deng et al. (2024) applied lentiMPRA to **102,767 open chromatin regions** in primary mid-gestation human cortical cells and cerebral organoids, identifying 46,802 active enhancer sequences and **164 disorder-associated variants** that significantly altered enhancer activity. The concordance between organoid and primary tissue measurements validated organoids as scalable platforms for regulatory element characterization — a finding with important implications for studying inaccessible human tissues.

### Enhancer-promoter compatibility follows multiplicative logic

A foundational question in regulatory genomics concerns how enhancers and promoters communicate to produce quantitative expression outputs. Bergman et al. (2022) addressed this directly by developing ExP STARR-seq, a combinatorial assay testing **1,000 enhancers × 1,000 promoters** in K562 cells. Their key finding was that a multiplicative model of enhancer and promoter intrinsic activities explained **R² = 0.82** of the variance in RNA output, spanning a greater than 250,000-fold expression range. Intrinsic promoter activity accounted for 48% and enhancer activity for 27% of total variance, with the interaction term capturing the remainder.

This multiplicative framework has been extended by Martinez-Ara et al. (2024), who tested approximately 69,000 enhancer-enhancer-promoter combinations in mouse embryonic stem cells. They found that enhancer pairs combine **near-additively**, but promoter identity critically modulates this integration, with developmental promoters showing stronger enhancer responsiveness than housekeeping promoters. An observed sublinear scaling exponent (< 1) suggests diminishing returns at high total enhancer input — a finding consistent with transcriptional bursting models where enhancers increase burst frequency rather than amplitude.

### Single-cell MPRAs resolve cell-type-specific regulatory activity

A major limitation of bulk MPRAs is their inability to resolve regulatory element activity across heterogeneous cell populations. Lalanne et al. (2024) addressed this by developing scQers (single-cell quantitative expression reporters), which decouple barcode detection from quantitative measurement using a circularized RNA strategy. Testing over 200 accessible chromatin regions during early mammalian differentiation, they identified 13 autonomous, cell-type-specific developmental cis-regulatory elements, with single-cell fold-changes **5–10× larger** than those detectable in bulk assays. This technology promises to dramatically expand our understanding of how regulatory elements acquire cell-type specificity during development.

The field's growing maturity is reflected in the creation of MPRAbase, a curated database encompassing **130 MPRA experiments** covering 17.7 million elements across 35 cell types and 4 organisms (Zhao et al., 2025), and in comprehensive benchmarking studies revealing substantial inconsistencies across MPRA platforms that can be mitigated by uniform analysis pipelines (Zhang et al., 2025).

### Quantitative framework: modeling enhancer output

The mathematical relationship between regulatory element composition and transcriptional output can be formalized. For a promoter *P* with intrinsic activity *α_P* receiving input from enhancers *E₁, E₂, ... Eₙ* with intrinsic activities *α_Eᵢ*, the Bergman et al. (2022) multiplicative model predicts total expression as:

```math
\text{Expression} \approx \alpha_P \cdot \prod_i (1 + \alpha_{E_i} \cdot c_i)
```


where *cᵢ* represents the contact probability between enhancer *i* and the promoter. The Martinez-Ara et al. (2024) data suggest that for multiple enhancers acting on a single promoter, a sublinear aggregation function better captures the observed diminishing returns:

```math
\text{Expression} \approx \alpha_P \cdot \left( \sum_i \alpha_{E_i} \right)^\gamma
```

where **$\gamma < 1$**. These quantitative frameworks provide the foundation for computational design of synthetic regulatory elements with predictable output levels.

---

## 3. Deep learning predicts and designs regulatory DNA from sequence

### Transformer architectures model long-range genomic interactions

The Enformer model (Avsec et al., 2021) represented a watershed moment in sequence-to-function prediction by combining convolutional layers with transformer self-attention to process **196 kb of input DNA sequence** and predict 5,313 human genomic tracks simultaneously, achieving Pearson correlations of approximately **R ≈ 0.58** for population-average CAGE gene expression. By capturing enhancer-promoter interactions spanning up to 100 kb, Enformer demonstrated that long-range regulatory information could be learned directly from sequence — though subsequent analyses revealed that its predictive power diminishes substantially beyond 10 kb from the transcription start site.

Borzoi (Linder et al., 2025) advanced this paradigm by extending the input window to **524 kb**, predicting cell-type-specific RNA-seq coverage at **32-bp resolution** (versus Enformer's 128 bp) using a U-net architecture with 8 transformer blocks. By modeling RNA-seq coverage directly, Borzoi provides a unified framework for transcription, splicing, and polyadenylation, and achieves superior enhancer-gene linking at distances exceeding 45 kb compared to Enformer. The Sei model (Chen et al., 2022) complemented these approaches by learning a vocabulary of **40 sequence classes** representing distinct regulatory activities across 21,907 chromatin profiles, enabling global classification of regulatory variant effects.

Training deep learning models on genomic sequences poses unique challenges due to limited training data. The EvoAug framework (Lee et al., 2023) addressed this through evolution-inspired data augmentations — random mutations, insertions, deletions, inversions, and translocations — applied during training. Remarkably, models trained with EvoAug on only **25% of training data** outperformed the same architectures trained on the full dataset with standard augmentation, while also learning a broader repertoire of transcription factor motifs.

### From prediction to design: generative models create synthetic regulatory elements

The transition from predicting the function of existing sequences to designing novel ones marks the field's most transformative development. Three complementary generative strategies have emerged, each achieving experimental validation in 2024–2025.

**Directed evolution and gradient-based optimization.** Gosai et al. (2024) trained the Malinois neural network on MPRA data from over 750,000 sequences across three cell types, then used gradient-based and stochastic search to generate **51,000 synthetic cis-regulatory elements**. When tested experimentally, synthetic sequences **outperformed natural human genomic sequences** in driving cell-type-specific expression, and achieved tissue-specific activity when validated in vivo in zebrafish and mice. Taskiran et al. (2024) independently demonstrated that directed in silico evolution of random sequences through just 15 mutations could drive over 97% of sequences to high predicted cell-type specificity, with **75% of synthetic Kenyon cell enhancers validating as active** in transgenic Drosophila and functional minimal enhancers achievable in **fewer than 50 base pairs**.

**Diffusion models for regulatory DNA.** DaSilva et al. (2026) introduced DNA-Diffusion, a denoising diffusion probabilistic model trained on ENCODE DNase I hypersensitive site data that generates 200-bp synthetic regulatory elements with cell-type-specific activity. Validated through a **5,850-element STARR-seq library** across three cell lines, DNA-Diffusion sequences recapitulated endogenous transcription factor binding grammar while exhibiting enhanced cell-type specificity. Critically, this study demonstrated endogenous gene modulation using EXTRA-seq, reactivating the leukemia-protective gene **AXIN2** in its native genomic context — establishing a direct path toward therapeutic applications. Only 1.7% of generated sequences aligned to the training set, confirming genuine novelty rather than memorization.

**Iterative design-build-test-learn cycles.** Lal et al. (2025) demonstrated that iterative deep learning design achieves dramatic improvements through successive rounds of experimental validation and model retraining. Their HepG2-targeted synthetic enhancers achieved **9.7-fold higher expression** in HepG2 relative to K562 cells, with second-generation designs substantially outperforming first-generation sequences. Notably, functional synthetic enhancers as short as **50 bp** maintained full cell-type specificity, employing a "condensed" motif grammar more selective than that of endogenous enhancers.

De Almeida et al. (2024) applied CNN-based models with transfer learning from scATAC-seq to design tissue-specific enhancers for five Drosophila embryo tissues, achieving **78% in vivo activity** (31/40 designs) with **100% tissue specificity** for CNS and muscle targets. Foundation models have also entered the design space, with the Nucleotide Transformer (Dalla-Torre et al., 2025) — a 2.5-billion-parameter model pre-trained on 3,000+ genomes — demonstrating strong performance across 18 downstream genomic prediction tasks.

### ChromBPNet and interpretable regulatory models

The Kundaje laboratory's ChromBPNet framework (Pampari et al., 2024) provides bias-factored, base-resolution deep learning models of chromatin accessibility that automatically correct for enzymatic sequence biases in ATAC-seq and DNase-seq data. ChromBPNet has become a critical "oracle" model within design pipelines, providing base-pair-resolution evaluation of candidate regulatory sequences in the DNA-Diffusion and other generative frameworks.

---

## 4. Synthetic regulatory elements advance gene therapy and cell therapy

### Compact promoters overcome AAV packaging constraints

Adeno-associated virus (AAV) vectors impose a **~4.8 kb empirical packaging limit**, creating intense pressure to minimize promoter size while maintaining tissue-specific expression. This constraint has driven creative engineering of synthetic minimal promoters, with several achieving clinical translation.

Zahm et al. (2024) reported a library of **6,144 synthetic promoters, each under 250 bp**, constructed from four copies of transcription factor binding motifs with defined spacing geometry. These promoters achieved dynamic ranges of **50–100-fold** induction across multiple cell types and proved responsive to metabolites, mitogens, and pharmaceutical agents. At the extreme of miniaturization, Klockner et al. (2025) demonstrated that the **Calm1 promoter at only 120 bp** drives neuron-specific expression in human iPSC-derived brain organoids with performance comparable to the widely used hSyn promoter (470 bp), freeing approximately 350 bp of precious AAV cargo space for larger transgenes. The LAP2 promoter (404 bp), derived from an alphaherpesvirus latency-associated element, provides robust expression persisting over **400 days** post-injection in liver, kidney, and skeletal muscle (Maturana & Engel, 2024).

Clinical validation has been achieved for several synthetic promoter systems. The **MHCK7 promoter** drives Elevidys (delandistrogene moxeparvovec), which received FDA full approval in June 2024 for Duchenne muscular dystrophy. Greer-Short et al. (2025) reported that the TN-201 optimized expression cassette with minimal promoter and synthetic cis-regulatory elements achieved restoration of wild-type MYBPC3 protein levels at clinically relevant doses of **3 × 10¹³ vg/kg** in a hypertrophic cardiomyopathy model, reversing cardiac hypertrophy and systolic dysfunction.

### Machine learning designs therapeutic-grade regulatory elements

The integration of MPRA data with machine learning has produced synthetic regulatory elements with therapeutic potential. The Bao et al. (2022) crisprTF platform achieved **up to 25-fold greater activity than the EF1α promoter** using CRISPR-based synthetic transcription factors, with programmed control of interferon-γ production in T cells correlating directly with synthetic promoter strength. This work established that synthetic regulatory systems can achieve the expression levels required for functional immunotherapy.

The PARM model (Barbadilla-Martínez et al., 2025), trained on MPRA data querying millions of random genomic DNA fragments across **nine human cell lines**, uncovered positional preferences of transcription factors — including the surprising finding that many TFs function as repressors when binding downstream of the transcription start site. PARM can design purely synthetic strong promoters, opening the door to fully artificial regulatory elements optimized for therapeutic gene expression cassettes.

A systematic review of clinical programs reveals that synthetic or engineered promoters now underpin the majority of approved AAV gene therapies, including Roctavian for hemophilia A and Beqvez for hemophilia B, with over 25 active clinical trials utilizing tissue-specific synthetic promoters (Artemyev et al., 2024).

---

## 5. Synthetic gene circuits enable programmable mammalian cell behavior

### CRISPRa/CRISPRi-based feedback controllers achieve robust homeostasis

The construction of reliable feedback controllers in mammalian cells represents one of synthetic biology's most significant recent achievements. Frei et al. (2022) implemented the first mammalian **proportional-integral (PI) feedback controller** based on the antithetic integral feedback motif, using sense/antisense mRNA sequestration for molecular annihilation. This circuit maintained tunable expression levels despite perturbations — a property known as robust perfect adaptation (RPA) — while the proportional component reduced cell-to-cell variance.

Building on this foundation, Zhang and Zhang (2024) demonstrated a CRISPRa/anti-CRISPR antithetic integral controller where the AcrIIA4 protein robustly inhibited dCas9-VP64-mediated activation by **~23-fold**, achieving perfect adaptation in both open-loop and closed-loop configurations. This system was applied to regulate endogenous NF-κB-mediated immune responses in T cells. Fusco et al. (2024) further refined this approach with CRISPRaic, using VPR-dCas9 and AcrIIA4 enhanced with synthetic coiled-coil interaction domains that boosted inhibitory activity by **>3-fold**, creating a plug-and-play system capable of regulating any endogenous gene through guide RNA design alone.

### Logic-gated CAR-T cells move toward clinical translation

The application of synthetic gene circuits to immunotherapy has produced remarkable advances in specificity and safety. **Synthetic Notch (synNotch) receptors**, which undergo ligand-triggered proteolytic cleavage to release an intracellular transcription factor, enable IF-THEN logic: detection of antigen A by synNotch triggers transcription of a CAR targeting antigen B. This AND-gate architecture limits tonic signaling and produces less exhausted, long-lived memory T cells compared to constitutive dual-CAR approaches (Shirzadian et al., 2025).

A critical advance in antigen density discrimination was achieved through low-affinity HER2-synNotch gating of high-affinity HER2-CAR, which activated effector function against tumor cells expressing HER2 at ~10⁷ molecules per cell but **not against cells expressing ~60,000 molecules** — a threshold relevant to discriminating tumor from normal tissue. The first synNotch-CAR-T clinical trial for glioblastoma (EGFRvIII-synNotch → EphA2/IL13Rα2 Tan-CAR; NCT06186401) is now recruiting patients.

Perhaps the most conceptually striking recent advance is the demonstration of **"fuzzy logic"** in T cells by Kondo et al. (2025). By co-expressing a TCR and CAR on the same T cell, they showed that strong TCR-antigen interactions amplified CAR-mediated killing while weak TCR-antigen interactions actively antagonized it — creating continuous ternary (−1, 0, +1) modulation rather than discrete Boolean logic. Their Antagonism-Enforced Braking System (AEBS) leveraged this property: neoantigen recognition by TCR amplified CAR killing, while self-antigen recognition braked CAR function. **AEBS CAR-T cells eradicated tumors across six cancer types** with minimal toxicity against healthy tissue in humanized mouse models.

Li et al. (2022) demonstrated the complementary approach of small-molecule-controlled circuits using synthetic zinc finger transcription regulators (synZiFTRs) — compact, human-derived proteins controlled by FDA-approved drugs including grazoprevir and tamoxifen. These orthogonal drug-gated circuits enabled sequential activation of proliferation (via super-IL-2) and antitumor killing (via anti-HER2 CAR) in primary T cells, with in vivo efficacy demonstrated in NSG mice.

### Protein and RNA circuits expand the design space

Xia et al. (2024) introduced "synpoptosis" — synthetic protein circuits that proteolytically regulate engineered executioner proteins to direct cell death through either apoptosis or pyroptosis pathways. These circuits process combinations of protease inputs through logic-gate-like operations, enabling selective elimination of target cells with control over inflammatory versus non-inflammatory death modes. Delivered as modified mRNA, synpoptosis circuits operate on faster timescales than transcription-based systems.

At the RNA level, Zhang et al. (2024) developed programmable RNA-IN/RNA-OUT circuits combining CRISPR-associated protease complexes for RNA detection with protease-responsive dCas9-VPR activators for output. Their dual-nucleotide synergistic switching amplified point-mutation detection signals from undetectable (1.5-fold) to **94-fold**, with demonstrated applications including rewiring endogenous RNA signals to activate progesterone biosynthesis, monitoring adipogenic differentiation, and selective tumor cell killing.

Shao et al. (2024) expanded computational complexity by engineering tristate logic circuits using poly(A)-surrogates for translational regulation, enabling multi-layered computational gene networks that go beyond simple Boolean operations. These approaches, combined with established ribozyme-based and miRNA-responsive circuits (Teixeira & Fussenegger, 2024), provide a rich toolkit spanning all levels of gene expression regulation.

---

## 6. Three-dimensional genome architecture as a programmable layer

### Loop extrusion and CTCF insulators create the structural framework

The organization of mammalian genomes into topologically associating domains (TADs) through cohesin-mediated loop extrusion and CTCF boundary elements creates a structural framework that constrains enhancer-promoter communication. Dekker and Mirny (2024) synthesized the field's understanding into four conserved folding mechanisms: homotypic affinity-driven compartmentalization, molecular motor-driven loop extrusion, topological features including supercoiling, and tethering to subnuclear structures. They propose that gene regulatory functions of chromosome folding were co-opted from more ancient functions in genome replication and segregation.

The engineering potential of this architecture is substantial but complex. Kabirova et al. (2024) demonstrated that CRISPR-mediated deletion of TAD boundaries at the Kit locus produced **tissue-specific ectopic activation** of the neighboring Kdr gene in melanocytes but not mast cells — despite Kit being highly active in both cell types. This finding reveals that the consequences of TAD boundary manipulation depend critically on the local epigenetic landscape, challenging simplistic models of insulator function.

Clustered CTCF binding sites in mixed orientations create asymmetric insulation at TAD boundaries, with both inward- and outward-oriented sites contributing to insulator function (Huang et al., 2024). Chen et al. (2024) generated high-resolution tissue-resolved contact maps across 10 murine embryonic tissues, finding that **61% of developmental enhancers bypass neighboring genes** and fewer than 14% of enhancer-promoter interactions are invariant across tissues. Karpinska et al. (2025) further demonstrated that CTCF depletion can decouple physical enhancer-promoter proximity from transcriptional activation, suggesting that structural and functional aspects of chromatin communication are partially independent.

### Programmable chromatin looping through dCas9 tethering

Several systems now enable programmable formation of chromatin loops at specified genomic locations. The CLOuD9 system (Morgan et al., 2017) uses abscisic acid-inducible dimerization of dCas9 orthologs from *S. aureus* and *S. pyogenes* to form reversible chromatin loops, reactivating β-globin expression in K562 cells through forced enhancer-promoter contact. The LADL system (Kim et al., 2019) achieves light-inducible looping via dCas9-CIBN and CRY2 bridge proteins, enabling temporal control of enhancer redirection. More recently, dCas9-CTCF chimeric proteins incorporating the CTCF N-terminal domain with two zinc-finger domains have been shown to create de novo chromatin loops without off-target binding and can restore loops lost by CTCF binding site deletion (Do et al., 2025).

### Synthetic regulatory genomics at the locus scale

The Boeke and Maurano laboratories have pioneered "synthetic regulatory genomics" — the systematic rewriting of regulatory loci using large-scale DNA synthesis and the Big-IN integration platform, which enables scarless insertion of payloads up to 160 kb into mammalian genomes (Brosh et al., 2021). Using this approach, Pinglay et al. (2022) synthesized variant rat HoxA clusters (130–170 kb) at ectopic mouse genomic locations, demonstrating that a minimal cluster recapitulates correct chromatin remodeling and transcription patterns while distal enhancers are required for full quantitative output. Brosh et al. (2023) applied Big-IN at the Sox2 locus to demonstrate that two DHSs with key transcription factor recognition sequences were each individually sufficient for long-range Sox2 activation — revealing unexpected redundancy in apparently complex regulatory landscapes. Ordoñez et al. (2024) further showed that genomic context critically modulates the impact of regulatory element disruptions, establishing that identical perturbations produce different effects depending on their chromosomal neighborhood.

The Ren laboratory has complemented these synthetic approaches with comprehensive multimodal profiling. Chang et al. (2025) introduced Droplet Hi-C for scalable single-cell chromatin conformation profiling using commercial microfluidics, while Kubo et al. (2024) demonstrated that H3K4me1 actively facilitates enhancer-promoter interactions through cohesin recruitment during embryonic stem cell differentiation. Yu et al. (2025) provided an integrative analysis of the 3D genome and epigenome across developing mouse embryonic tissues, linking chromatin architecture to developmental gene regulatory programs.

---

## 7. Engineered morphogen gradients and regulatory elements in organoid systems

The integration of synthetic regulatory elements with tissue engineering has produced tools for spatial patterning of gene expression in three-dimensional culture systems. Afting et al. (2024) developed **DNA microbeads with tissue-mimetic tunable stiffness** that can be microinjected into organoids at any developmental stage, providing spatio-temporally controlled morphogen release that can be erased non-invasively with light. Application of Wnt-coupled DNA microbeads to medaka retinal organoids induced retinal pigmented epithelium formation while maintaining neuroretinal cell types, demonstrating programmable morphogen gradient engineering within organoids.

Mizuno et al. (2024) developed SYMPLE3D (Synthetic Morphogen system for Pattern Logic Exploration using 3D spheroids), which couples synNotch-mediated GFP detection with E-cadherin-based cell adhesion to convert morphogen gradients into **distinct tissue domains with sharp boundaries**. Their mathematical model based on differential adhesion energy captures the switch-like behavior observed experimentally, providing a theoretical framework for engineering tissue-level patterns through synthetic signaling.

Large-scale morphogen screening has been applied to organoid diversification. Amin et al. (2024) tested **14 morphogen modulators in 46 unique combinations** in human neural organoids cultured over 70 days, using single-cell multiplexed RNA sequencing to deconvolve design principles of brain region specification. This systematic approach generated highly regionalized cultures covering cell diversity across the neural axis, including rare TAC3-expressing striatal interneurons and human Purkinje neurons that developed hallmark complex dendritic branching upon neonatal rat transplantation.

The regulatory framework for organ-on-chip platforms is evolving rapidly. The FDA Modernization Act 2.0 (2022) made non-animal models formally acceptable for preclinical studies, yet surveys indicate that only **23% of life science executives** are "very familiar" with these alternatives (Srivastava et al., 2024), suggesting significant adoption gaps that may be bridged as synthetic biology tools make organ-on-chip systems more reproducible and physiologically relevant.

---

## 8. Cell-free TX-TL systems accelerate regulatory element prototyping

Cell-free transcription-translation (TX-TL) systems provide a powerful platform for rapid prototyping of synthetic regulatory elements and genetic circuits outside living cells, with experimental timescales of **hours rather than the days to weeks** required for in vivo approaches. Ekas et al. (2024) demonstrated the power of automated cell-free workflows by generating and assaying libraries of **127 MerR and 134 CadR transcription factor variants** across **3,682 unique reactions in under 48 hours** using acoustic liquid handling, achieving rapid optimization of biosensor dynamic range and selectivity.

However, fundamental limitations persist. Piorino et al. (2024) revealed a **trade-off between transcription and translation** in *E. coli*-based cell-free systems through systematic metabolic perturbation analysis, demonstrating that optimizing one process can compromise the other. Han et al. (2025) further challenged the assumption that multiple DNA templates behave independently in cell-free reactions, developing mathematical models showing that plasmid templates exhibit antagonistic or synergistic interactions — a critical consideration for prototyping multi-gene circuits.

Microfluidic approaches are extending the capabilities of cell-free systems toward continuous operation. Microfluidic chemostats enable steady-state TX-TL reactions, while compartmentalization in microdroplets and synthetic vesicles creates cell-like environments for studying gene expression with minimal reagent consumption (Maerkl, 2024). These platforms are increasingly being coupled with MPRA-like readouts to enable rapid iterative testing of synthetic regulatory designs before commitment to in vivo validation.

---

## 9. Synthesis: toward a unified design framework for programmable gene expression

The advances surveyed here converge toward a unified framework for engineering gene expression at multiple levels — from individual regulatory elements through chromatin architecture to multicellular tissue-level patterns. Several cross-cutting themes emerge.

**The predictive power of regulatory element models has crossed a critical threshold.** Machine learning models trained on MPRA data now achieve sufficient accuracy to design synthetic regulatory elements that reliably function in vivo. The convergence of Gosai et al. (2024), Taskiran et al. (2024), and de Almeida et al. (2024) — published near-simultaneously in *Nature* — established that computationally designed enhancers achieve validation rates of **68–78%** in vivo, approaching the success rates needed for practical therapeutic application.

**Generative AI has fundamentally changed regulatory element engineering.** The progression from prediction-only models (Enformer, Sei) to generative frameworks (DNA-Diffusion, in silico evolution, gradient-based optimization) parallels the broader AI revolution but carries unique biological significance: generated regulatory sequences employ a "condensed grammar" that is more efficient than natural sequences, suggesting that evolution has not fully optimized the regulatory code (Lal et al., 2025).

**Synthetic gene circuits are achieving clinical relevance.** Logic-gated CAR-T cells have advanced from proof-of-concept to clinical trials (NCT06186401, DENALI-1), with increasingly sophisticated circuit architectures — from Boolean AND gates through fuzzy logic controllers (Kondo et al., 2025) — providing the precision needed to discriminate tumor from healthy tissue.

---

## 10. Open questions and future directions

Despite remarkable progress, fundamental challenges remain that define the field's research frontier.

**Enhancer grammar remains incompletely decoded.** While models trained on MPRA data can predict enhancer activity with useful accuracy, the rules governing how transcription factor binding site combinations encode cell-type specificity are not yet understood at a level that permits fully rational design. The PARM model's discovery that many TFs switch from activating to repressing roles depending on their position relative to the TSS (Barbadilla-Martínez et al., 2025) hints at a grammar far more complex than simple motif presence/absence. Systematic perturbation of motif syntax — spacing, orientation, order, and flanking sequence — across dozens of cell types will be needed to enumerate the full regulatory code.

**Chromatin context dependence limits transferability.** Ordoñez et al. (2024) and Kabirova et al. (2024) demonstrated that identical regulatory perturbations produce different outcomes depending on genomic context. This "context sensitivity" represents a fundamental challenge for synthetic regulatory genomics: elements designed and validated in one chromosomal location may behave differently when delivered via AAV or integrated at a different locus. Comprehensive characterization of context effects — potentially through systematic Big-IN insertion of standardized test elements at hundreds of genomic locations — is needed to establish design rules for context-robust regulatory elements.

**Long-range enhancer-promoter communication mechanisms remain debated.** The observation that CTCF depletion can decouple physical proximity from transcriptional activation (Karpinska et al., 2025) challenges loop extrusion models that assume physical contact is necessary and sufficient for enhancer function. Alternative mechanisms — including phase separation, transcription factor hub formation, and chromatin modification spreading — may contribute to enhancer action at different genomic loci. Resolving these mechanisms is essential for engineering reliable long-range synthetic regulatory interactions.

**Clinical translation faces scalability and safety challenges.** While compact promoters and synthetic enhancers have demonstrated in vivo efficacy, the regulatory pathway for fully synthetic regulatory elements in human gene therapy requires demonstration of long-term stability, absence of immunogenicity against synthetic sequences, and predictable behavior across patient genetic backgrounds. The iterative design-build-test-learn cycle that has proven so effective in research contexts must be adapted for clinical-grade manufacturing under GMP conditions.

**Cell-free-to-in-vivo translation fidelity needs improvement.** The fundamental trade-offs identified in TX-TL systems (Piorino et al., 2024) and the context-dependent behavior of regulatory elements in chromatin suggest that cell-free prototyping cannot fully substitute for in vivo validation. Development of chromatin-reconstituted cell-free systems that better recapitulate nuclear regulatory environments could substantially improve the predictive value of cell-free prototyping.

Concrete experimental approaches to address these gaps include: (i) ultra-high-throughput single-cell MPRAs across complete developmental trajectories to decode temporal regulatory grammar; (ii) systematic deployment of dCas9-based chromatin looping tools at hundreds of loci to establish quantitative contact-function relationships; (iii) integration of generative AI design with Big-IN-scale genome rewriting to test thousands of synthetic locus architectures in parallel; and (iv) development of patient-derived organoid platforms for personalized validation of synthetic regulatory elements before clinical application.

---

## 11. Conclusion

Synthetic regulatory genomics has matured from a conceptual framework into a practical engineering discipline. The convergence of MPRAs testing hundreds of thousands of sequences, deep learning models that accurately predict and generate regulatory DNA, and synthetic gene circuits achieving clinical translation represents a qualitative shift in our ability to program cell behavior. Machine learning-designed enhancers now surpass their natural counterparts in specificity, synthetic promoters drive FDA-approved gene therapies, and logic-gated cellular circuits discriminate tumor from healthy tissue at the molecular level.

The next frontier lies in integration: combining designed regulatory elements with engineered 3D chromatin architecture, embedding synthetic circuits within tissue-engineered constructs, and translating computational designs through automated prototyping pipelines into clinical applications. The fundamental insight emerging from this field is that the regulatory code, while complex, is learnable and writable — and that synthetic sequences can achieve functional properties that evolution never explored.

---

## References

Afting, C., Walther, T., Drozdowski, O. M., Schlagheck, C., Schwarz, U. S., Wittbrodt, J., & Göpfrich, K. (2024). DNA microbeads for spatio-temporally controlled morphogen release within organoids. *Nature Nanotechnology*, *19*, 1849–1857.

Agarwal, V., Inoue, F., Schubach, M., Penzar, D., Martin, B. K., Ahituv, N., & Shendure, J. (2025). Massively parallel characterization of transcriptional regulatory elements. *Nature*, *639*(8054), 411–420.

Amin, N. D., Kelley, K. W., Kaganovsky, K., Onesto, M., Hao, J., Miura, Y., McQueen, J. P., Reis, N., Narazaki, G., Li, T., Kulkarni, S., Pavlov, S., & Pașca, S. P. (2024). Generating human neural diversity with a multiplexed morphogen screen in organoids. *Cell Stem Cell*, *31*(12), 1831–1846.

Artemyev, V., Gubaeva, A., Paremskaia, A. I., & colleagues. (2024). Synthetic promoters in gene therapy: Design approaches, features and applications. *Cells*, *13*(23), 1963.

Avsec, Ž., Agarwal, V., Visentin, D., Ledsam, J. R., Grabska-Barwinska, A., Taylor, K. R., Assael, Y., Jumper, J., Kohli, P., & Kelley, D. R. (2021). Effective gene expression prediction from sequence by integrating long-range interactions. *Nature Methods*, *18*(10), 1196–1203.

Bao, Z., & Chen, Y. Y. (2022). A synthetic transcription platform for programmable gene expression in mammalian cells. *Nature Communications*, *13*, 5587.

Barbadilla-Martínez, L., Klaassen, N., Franceschini-Santos, V. H., Breda, J., & van Steensel, B. (2025). Regulatory grammar in human promoters uncovered by MPRA-based deep learning. *Nature*.

Bergman, D. T., Jones, T. R., Liu, V., Ray, J., Jagoda, E., Siraj, L., Kang, H. Y., Nasser, J., Kane, M., Fulco, C. P., Lander, E. S., & Engreitz, J. M. (2022). Compatibility rules of human enhancer and promoter sequences. *Nature*, *607*(7917), 176–184.

Brosh, R., Coelho, C., Ribeiro-dos-Santos, A. M., Ellis, G., Hogan, M. S., Ashe, H. J., Somogyi, N., Ordoñez, R., Boeke, J. D., & Maurano, M. T. (2023). Synthetic regulatory genomics uncovers enhancer context dependence at the Sox2 locus. *Molecular Cell*, *83*(7), 1140–1152.

Brosh, R., Laurent, J. M., Ordoñez, R., Huang, E., Hogan, M. S., Hitchcock, A. M., Mitchell, L. A., Pinglay, S., Cadley, J. A., Luther, R. D., Truong, D. M., Boeke, J. D., & Maurano, M. T. (2021). A versatile platform for locus-scale genome rewriting and verification. *Proceedings of the National Academy of Sciences*, *118*(10), e2023952118.

Chang, L., Xie, Y., Taylor, B., Wang, Z., Sun, J., Armand, E. J., Mishra, S., Xu, J., Hu, M., & Ren, B. (2025). Droplet Hi-C enables scalable, single-cell profiling of chromatin architecture in heterogeneous tissues. *Nature Biotechnology*, *43*(10), 1694–1707.

Chen, K. M., Wong, A. K., Troyanskaya, O. G., & Zhou, J. (2022). A sequence-based global map of regulatory activity for deciphering human genetics. *Nature Genetics*, *54*(7), 1011–1020.

Chen, Z., Snetkova, V., Bower, G., & colleagues. (2024). Increased enhancer–promoter interactions during developmental enhancer activation in mammals. *Nature Genetics*, *56*(4), 675–685.

Dalla-Torre, H., Gonzalez, L., Mendoza-Revilla, J., & colleagues. (2025). Nucleotide Transformer: Building and evaluating robust foundation models for human genomics. *Nature Methods*.

DaSilva, L. F., Senan, S., Kribelbauer-Swietek, J. F., Patel, Z. M., Louis, L. K., Reddy, A. J., Gabbita, S., & Pinello, L. (2026). Designing synthetic regulatory elements using the generative AI framework DNA-Diffusion. *Nature Genetics*, *58*(1), 180–194.

de Almeida, B. P., Reiter, F., Pagani, M., & Stark, A. (2022). DeepSTARR predicts enhancer activity from DNA sequence and enables the de novo design of synthetic enhancers. *Nature Genetics*, *54*(5), 613–624.

de Almeida, B. P., Schaub, C., Pagani, M., Secchia, S., Furlong, E. E. M., & Stark, A. (2024). Targeted design of synthetic enhancers for selected tissues in the Drosophila embryo. *Nature*, *626*(7997), 207–211.

Dekker, J., & Mirny, L. A. (2024). The chromosome folding problem and how cells solve it. *Cell*, *187*(23), 6424–6450.

Deng, C., Whalen, S., Steyert, M., Ziffra, R., Przytycki, P. F., Inoue, F., Pereira, D. A., Capauto, D., Norton, S., Pollen, A. A., Nowakowski, T. J., Ahituv, N., & Pollard, K. S. (2024). Massively parallel characterization of regulatory elements in the developing human cortex. *Science*, *384*(6698), 875–880.

Do, C., Jiang, G., Cova, G., Katsifis, C. C., Narducci, D. N., & colleagues. (2025). Binding domain mutations provide insight into CTCF's relationship with chromatin and its contribution to gene regulation. *Cell Genomics*, *5*(4), 100813.

Ekas, H. M., & colleagues. (2024). An automated cell-free workflow for transcription factor engineering. *ACS Synthetic Biology*, *13*(10), 3389–3399.

Frei, T., Chang, C. H., Filo, M., Arampatzis, A., & Khammash, M. (2022). A genetic mammalian proportional–integral feedback control circuit for robust and precise gene regulation. *Proceedings of the National Academy of Sciences*, *119*(24), e2122132119.

Fusco, V., Ragazzini, F., & di Bernardo, D. (2024). A biomolecular circuit for automatic gene regulation in mammalian cells with CRISPR technology. *ACS Synthetic Biology*, *13*(12), 3917–3925.

Gosai, S. J., Castro, R. I., Fuentes, N., Butts, J. C., Mouri, K., Alasoadura, M., Kales, S., Nguyen, T. T. L., Noche, R. R., Rao, A. S., Joy, M. T., Sabeti, P. C., Reilly, S. K., & Tewhey, R. (2024). Machine-guided design of cell-type-targeting cis-regulatory elements. *Nature*, *634*(8036), 1211–1220.

Greer-Short, A., Greenwood, A., Leon, E. C., & colleagues. (2025). AAV9-mediated MYBPC3 gene therapy with optimized expression cassette enhances cardiac function and survival in MYBPC3 cardiomyopathy models. *Nature Communications*, *16*, 2196.

Han, Y., Patterson, A. T., Piorino, F., & Styczynski, M. P. (2025). A mathematical model of cell-free transcription-translation with plasmid crosstalk. *Synthetic Biology*, *10*(1), ysaf011.

Huang, H., & colleagues. (2024). Pushing the TAD boundary: Decoding insulator codes of clustered CTCF sites in 3D genomes. *BioEssays*, *46*(8), 2400121.

Kabirova, E., Ryzhkova, A., Lukyanchikova, V., Khabarova, A., Korablev, A., & Battulin, N. (2024). TAD border deletion at the Kit locus causes tissue-specific ectopic activation of a neighboring gene. *Nature Communications*, *15*, 4521.

Karpinska, M. A., Zhu, Y., Fakhraei Ghazvini, Z., Ramasamy, S., & colleagues. (2025). CTCF depletion decouples enhancer-mediated gene activation from chromatin hub formation. *Nature Structural & Molecular Biology*.

Kim, J. H., Rege, M., Valeri, J., Dunagin, M. C., & Phillips-Cremins, J. E. (2019). LADL: Light-activated dynamic looping for endogenous gene expression control. *Nature Methods*, *16*, 633–639.

Klein, J. C., Agarwal, V., Inoue, F., Keith, A., Martin, B., Kircher, M., Ahituv, N., & Shendure, J. (2020). A systematic evaluation of the design and context dependencies of massively parallel reporter assays. *Nature Methods*, *17*(11), 1083–1091.

Klockner, I., Yeturi, M., Rust, T. E., Stein, J. L., & Zylka, M. J. (2025). Compact Calm1 promoter enables AAV mediated neuron-targeted expression in human iPSC-derived brain organoids. *Scientific Reports*, *15*, 44450.

Kondo, T., Bourassa, F. X. P., Achar, S., DuSold, J., Céspedes, P. F., François, P., & Taylor, N. (2025). Engineering TCR-controlled fuzzy logic into CAR T cells enhances therapeutic specificity. *Cell*, *188*(9), 2372–2389.

Kubo, N., Chen, P. B., Hu, R., Ye, Z., Sasaki, H., & Ren, B. (2024). H3K4me1 facilitates promoter-enhancer interactions and gene activation during embryonic stem cell differentiation. *Molecular Cell*, *84*(9), 1742–1752.

La Fleur, A., Shi, Y., & Seelig, G. (2024). Decoding biology with massively parallel reporter assays and machine learning. *Genes & Development*, *38*, 924–951.

Lal, A., Biancalani, T., & Kreimer, A. (2025). Iterative deep learning design of human enhancers exploits condensed sequence grammar to achieve cell-type specificity. *Cell Systems*, 101302.

Lalanne, J.-B., Regalado, S. G., & Shendure, J. (2024). Multiplex profiling of developmental cis-regulatory elements with quantitative single-cell expression reporters. *Nature Methods*, *21*, 1015–1025.

Lee, N. K., Tang, Z., Toneyan, S., & Koo, P. K. (2023). EvoAug: Improving generalization and interpretability of genomic deep neural networks with evolution-inspired data augmentations. *Genome Biology*, *24*, 105.

Li, H. S., Israni, D. V., Gagnon, K. A., Gan, K. A., Raymond, M. H., Sander, J. D., Roybal, K. T., Joung, J. K., Wong, W. W., & Khalil, A. S. (2022). Multidimensional control of therapeutic human cell function with synthetic gene circuits. *Science*, *378*(6625), 1227–1234.

Linder, J., Srivastava, D., Yuan, H., Agarwal, V., & Kelley, D. R. (2025). Predicting RNA-seq coverage from DNA sequence as a unifying model of gene regulation. *Nature Genetics*, *57*, 949–961.

Maerkl, S. J. (2024). A comprehensive review of microfluidic approaches in cell-free synthetic biology. *Frontiers in Synthetic Biology*, *2*, 1397533.

Martinez-Ara, M., Fiers, F., Ait-Lounis, S., & van Steensel, B. (2024). Large-scale analysis of the integration of enhancer-enhancer signals by promoters. *eLife*, *13*, e91994.

Maturana, C. J., & Engel, E. A. (2024). Persistent transgene expression in peripheral tissues one year post intravenous and intramuscular administration of AAV vectors containing the alphaherpesvirus latency-associated promoter 2. *Frontiers in Virology*, *4*, 1379991.

Mizuno, K., Hirashima, T., & Toda, S. (2024). Robust tissue pattern formation by coupling morphogen signal and cell adhesion. *EMBO Reports*, *25*(11), 4803–4826.

Morgan, S. L., Mariano, N. C., Bermudez, A., Arruda, N. L., Wu, F., Luo, Y., Shanber, G., Jia, M., Chen, J., Hu, H., Bhatt, A. S., Greenleaf, W. J., & Fordyce, P. M. (2017). Manipulation of nuclear architecture through CRISPR-mediated chromosomal looping. *Nature Communications*, *8*, 15993.

Ordoñez, R., Zhang, W., Ellis, G., Zhu, Y., Ashe, H. J., Ribeiro-dos-Santos, A. M., Brosh, R., Huang, E., Hogan, M. S., Boeke, J. D., & Maurano, M. T. (2024). Genomic context sensitizes regulatory elements to genetic disruption. *Molecular Cell*, *84*, 1842–1854.

Pampari, A., Shcherbina, A., Kvon, E., Nair, S., & Kundaje, A. (2024). ChromBPNet: Bias factorized, base-resolution deep learning models of chromatin accessibility reveal cis-regulatory sequence syntax. *bioRxiv*, 2024.12.25.630221.

Pinglay, S., Bulajić, M., Rahe, D. P., Huang, E., Brosh, R., Mazzoni, E. O., & Boeke, J. D. (2022). Synthetic regulatory reconstitution reveals principles of mammalian Hox cluster regulation. *Science*, *377*, eabk2820.

Piorino, F., & Murray, R. M. (2024). Metabolic perturbations to an *Escherichia coli*-based cell-free system reveal a trade-off between transcription and translation. *ACS Synthetic Biology*, *13*(12), 3976–3990.

Shao, J., Qiu, X., Zhang, L., Li, S., & colleagues. (2024). Multi-layered computational gene networks by engineered tristate logics. *Cell*, *187*, 5064–5080.

Shirzadian, M., Moori, S., Rabbani, R., & Rahbarizadeh, F. (2025). SynNotch CAR-T cell, when synthetic biology and immunology meet again. *Frontiers in Immunology*, *16*, 1545270.

Srivastava, S. K., Foo, G. W., & colleagues. (2024). Organ-on-chip technology: Opportunities and challenges. *Biotechnology Notes*, *5*, 8–12.

Taskiran, I. I., Spanier, K. I., Dickmänken, H., Kempynck, N., Pančíková, A., Hulselmans, G., & Aerts, S. (2024). Cell-type-directed design of synthetic enhancers. *Nature*, *626*(7997), 212–220.

Teixeira, A. P., & Fussenegger, M. (2024). Synthetic gene circuits for regulation of next-generation cell-based therapeutics. *Advanced Science*, *11*(8), e2309088.

Thurm, A. R., Janer Carattini, G. L., & Bintu, L. (2025). Human synthetic biology and programmable gene regulation control. *Annual Review of Genomics and Human Genetics*, *26*, 139–161.

Xia, S., Lu, A. C., Tobin, V., Luo, K., Moeller, L., Shon, D. J., Du, R., Linton, J. M., Sui, M., Horns, F., & Elowitz, M. B. (2024). Synthetic protein circuits for programmable control of mammalian cell death. *Cell*, *187*(11), 2785–2800.

Yang, J. H., & Hansen, A. S. (2024). Enhancer selectivity in space and time: From enhancer-promoter interactions to promoter activation. *Nature Reviews Molecular Cell Biology*, *25*(7), 574–591.

Yu, M., Zemke, N. R., Chen, Z., Juric, I., Hu, R., Raviram, R., & Ren, B. (2025). Integrative analysis of the 3D genome and epigenome in mouse embryonic tissues. *Nature Structural & Molecular Biology*, *32*(3), 479–490.

Zahm, A. M., Owens, W. S., Himes, S. R., Fallon, B. S., Rondem, K. E., Bloom, J. S., Kosuri, S., Chan, H., & English, J. G. (2024). A massively parallel reporter assay library to screen short synthetic promoters in mammalian cells. *Nature Communications*, *15*, 10353.

Zhang, J., Leung, A. K.-Y., Zhu, Y., Li, Y., Yao, L., Willis, A., Pan, X., Ozer, A., Zhou, Z., Lis, J. T., & Yu, H. (2025). Comprehensive evaluation of diverse massively parallel reporter assays to functionally characterize human enhancers genome-wide. *Genome Biology*, *26*, 138.

Zhang, M., Zhang, X., Xu, Y., Xiang, Y., Zhang, B., Xie, Z., Wu, Q., & Lou, C. (2024). High-resolution and programmable RNA-IN and RNA-OUT genetic circuit in living mammalian cells. *Nature Communications*, *15*, 8768.

Zhang, Y., & Zhang, S. (2024). CRISPR perfect adaptation for robust control of cellular immune and apoptotic responses. *Nucleic Acids Research*, *52*(16), 10005–10016.

Zhao, J., Baltoumas, F. A., Konnaris, M. A., Mouratidis, I., Liu, Z., Sims, J., Agarwal, V., Pavlopoulos, G. A., Georgakopoulos-Soares, I., & Ahituv, N. (2025). MPRAbase: A massively parallel reporter assay database. *Genome Research*, *35*, 756–764.
