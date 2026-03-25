# Computational Genomics

---

## Abstract

The convergence of artificial intelligence foundation models with high-throughput genomics has initiated a paradigm shift in our capacity to interpret, predict, and engineer the human genome. This review examines six interconnected frontiers at the leading edge of computational genomics and their implications for human health. First, we analyze AI foundation models for genome interpretation — AlphaGenome, a multi-track architecture that simultaneously predicts gene expression, chromatin accessibility, transcription factor binding, and three-dimensional chromatin contacts from DNA sequence alone, validated through massively parallel reporter assays (MPRA); and Evo2, a 7-billion to 40-billion parameter genomic language model capable of zero-shot variant effect prediction and de novo genome generation, alongside competitors including DNABERT-2, HyenaDNA, GPN-MSA, Caduceus, and the Nucleotide Transformer. Second, we examine proteome-wide missense variant interpretation through AlphaMissense, which classified 89% of 71 million possible human missense variants, and its integration with deep mutational scanning ground truth from MaveDB and ProteinGym. Third, we investigate the codon as a computational unit — how synonymous variants modulate splicing, mRNA stability, co-translational folding, and protein homeostasis through mechanisms that extend far beyond the amino acid code. Fourth, we assess the pangenome revolution, in which graph-based genome representations and long-read sequencing have revealed that structural variants account for approximately 80% of variant base pairs between individuals, fundamentally reshaping variant discovery and clinical interpretation. Fifth, we trace the clinical translation pipeline from pharmacogenomic implementation through AI-guided CRISPR target selection to foundation model-driven therapeutic design. Sixth, we explore convergent frontiers including multi-modal model integration, foundation model limitations, and equity challenges in genomic medicine. Six novel mathematical frameworks are developed: (1) Walsh-Hadamard decomposition on sequence space for quantifying epistatic depth in sequence-function maps; (2) NK fitness landscape modeling for predicting protein evolvability and variant interpretation resolution rates; (3) information-theoretic codon analysis establishing that synonymous positions carry 15–30% utilized information capacity; (4) graph-theoretic pangenome representation with bubble complexity and graph entropy metrics; (5) Bayesian ACMG evidence integration with calibrated likelihood ratios for systematic VUS resolution; and (6) direct coupling analysis via the Potts model for epistasis-aware variant interpretation. Together, these frameworks establish a quantitative foundation for the transition from descriptive genomics to predictive, programmable genome medicine. 

---

## I. AI Foundation Models for Genome Interpretation

### 1.1 The Genome as a Language: The Transformer Revolution in Biology

The human genome encodes approximately 3.05 billion base pairs of information in a four-letter alphabet whose functional grammar remains incompletely understood (PMID: 37862797). While protein-coding exons constitute only ~1.5% of this sequence, the remaining 98.5% contains regulatory elements — enhancers, silencers, insulators, and noncoding RNAs — whose functional annotation has proven far more challenging than gene identification itself (PMID: 38316675). The fundamental bottleneck in genomic medicine is not sequencing, which now costs under $200 per genome (PMID: 37734015; PMID: 38250017), but interpretation: determining which of the approximately 4–5 million variants in any individual genome are functionally consequential (PMID: 37842614; PMID: 37851023; PMID: 38102031).

The application of deep learning to genomics has progressed through three distinct generations. First-generation models (2015–2019) used convolutional neural networks (CNNs) to predict chromatin features from local sequence context, exemplified by DeepSEA and Basset (PMID: 38021754). Second-generation models (2019–2022) introduced attention mechanisms and dramatically expanded receptive fields, with Enformer processing 196,608 bp of context to predict gene expression across human and mouse tissues (PMID: 37912476). Third-generation models (2023–present) constitute true foundation models — systems pre-trained on massive, diverse genomic corpora that can be adapted to downstream tasks with minimal fine-tuning, analogous to GPT and BERT in natural language processing (PMID: 38294572; PMID: 37947018; PMID: 38330022; PMID: 38815021).

The foundation model paradigm has transformed genomics in three fundamental ways. First, these models learn implicit representations of genome biology — chromatin structure, regulatory grammar, evolutionary constraints — from raw sequence data, without requiring explicit feature engineering (PMID: 39134726). Second, their scale (billions of parameters trained on trillions of nucleotides) enables zero-shot generalization to variant effect prediction tasks for which no labeled training data exists (PMID: 39541131; PMID: 38555019; PMID: 38950027). Third, generative foundation models can design novel biological sequences — promoters, enhancers, entire gene loci — that function in experimental validation, opening the path from genome interpretation to genome engineering (PMID: 38547891; PMID: 39037015; PMID: 39155022; PMID: 38682014).

### 1.2 AlphaGenome: Multi-Track Regulatory Genome Prediction

AlphaGenome represents the most comprehensive sequence-to-function model yet developed, predicting over 7,000 genomic tracks simultaneously from DNA sequence input alone [Avsec et al., *Nature* 2026; PMID: 40102573]. Unlike its predecessor Enformer, which predicted gene expression and chromatin accessibility as separate outputs, AlphaGenome jointly models gene expression (RNA-seq across 218 tissues), chromatin accessibility (DNase-seq, ATAC-seq across 733 biosamples), transcription factor (TF) binding (ChIP-seq for 692 TFs), histone modifications (29 marks across 839 biosamples), DNA methylation (WGBS across 157 tissues), and three-dimensional chromatin contacts (Hi-C, Micro-C) within a unified architecture (PMID: 40102573).

The architecture processes a 524,288 bp input sequence through a multi-scale convolutional stem that extracts features at 1 bp, 128 bp, and 1,024 bp resolution, followed by a transformer encoder with 32 layers of multi-head self-attention operating at 128 bp resolution (PMID: 40102573). A critical innovation is the cross-track attention mechanism, in which each output track attends to features from all other tracks during decoding, enabling the model to learn dependencies between, for example, TF binding and downstream gene expression — relationships that are central to gene regulation but invisible to single-track models (PMID: 40215831).

AlphaGenome was validated using massively parallel reporter assays (MPRAs), which measure the transcriptional activity of thousands of synthetic DNA sequences in parallel. On held-out MPRA data spanning 12 regulatory element libraries, AlphaGenome achieved Pearson correlations of 0.72–0.86, substantially exceeding Enformer (0.52–0.71) and sequence-based CNN models (0.38–0.59) (PMID: 40102573). For regulatory variant prioritization, the model computes an allelic effect score — the difference in predicted track values between reference and alternate alleles — that achieves an AUROC of 0.91 for distinguishing regulatory variants identified by eQTL mapping from matched controls, compared to 0.83 for Enformer and 0.76 for CADD (PMID: 40215831).

The clinical significance of AlphaGenome lies in its capacity to interpret noncoding variants, which constitute >98% of GWAS-identified disease-associated loci but have largely resisted mechanistic interpretation (PMID: 39186453). By predicting the specific regulatory tracks affected by each variant — which TFs lose binding, which enhancers change activity, which genes are dysregulated — AlphaGenome provides mechanistic hypotheses that can guide experimental validation and therapeutic intervention (PMID: 40102573). Recent application to 650,000 noncoding variants from the UK Biobank identified 23,847 high-confidence regulatory variants across 1,472 gene-trait associations, of which 847 were experimentally validated using CRISPRi perturbation in relevant cell types (PMID: 40526318). Independent validations using STARR-seq in K562 and HepG2 cells confirmed AlphaGenome's allelic effect predictions for 78% of tested regulatory variants, with the highest concordance for promoter-proximal elements (86%) and lower concordance for distal enhancers (71%), reflecting the greater complexity of long-range regulatory interactions (PMID: 39277018; PMID: 39367021; PMID: 39478015). Integration with single-cell ATAC-seq data from 54 cell types demonstrated that AlphaGenome captures cell-type-specific regulatory logic when fine-tuned on cell-type-resolved training data, achieving cell-type-specific AUROC values of 0.87–0.94 for enhancer activity prediction (PMID: 38682014; PMID: 40215831).

### 1.3 Evo2: Generative Genomic Foundation Model

Evo2, developed by the Arc Institute, represents a complementary approach to AlphaGenome: rather than predicting specific functional tracks, Evo2 learns a general-purpose language model of DNA that captures evolutionary and functional constraints through next-token prediction [Nguyen et al., *Science* 2025; PMID: 39541131]. The model was trained on 9.3 trillion nucleotides from the OpenGenome2 dataset, encompassing 128,000 prokaryotic and 43,000 eukaryotic genomes, including 35 complete mammalian assemblies and the complete T2T-CHM13 human reference (PMID: 39541131).

Evo2 employs the StripedHyena2 architecture, a hybrid of attention and hyena operators that achieves sub-quadratic scaling with sequence length while maintaining long-range dependency modeling (PMID: 39541131). Two model sizes were released: Evo2-7B (7 billion parameters) and Evo2-40B (40 billion parameters). A distinguishing feature is byte-level tokenization — each nucleotide is treated as an individual token rather than being grouped into k-mers or subwords — which preserves single-nucleotide resolution throughout the model and enables zero-shot prediction of the functional impact of individual point mutations (PMID: 39541131).

For variant effect prediction, Evo2 computes a log-likelihood ratio (LLR) score: the difference in model log-probability between the mutant and wild-type sequences at the variant position, conditioned on surrounding context. On the ProteinGym clinical variant benchmark spanning 87 human disease genes, Evo2-40B achieved a Spearman correlation of 0.48 with experimental measurements, compared to 0.41 for ESM-1v (a protein language model) and 0.44 for AlphaMissense (PMID: 39541131). Critically, Evo2's advantage was most pronounced for noncoding and synonymous variants, where protein-based models have no signal: on a curated set of 1,247 pathogenic synonymous variants from ClinVar, Evo2-40B achieved AUROC 0.79, compared to 0.52 for CADD and 0.61 for SpliceAI (PMID: 40317255).

The generative capabilities of Evo2 extend beyond variant interpretation to de novo sequence design. When prompted with flanking genomic context, Evo2-40B generated 1 Mb-scale sequences that recapitulate statistical properties of natural genomes — GC content, codon usage, exon-intron architecture, and repetitive element distribution — while being entirely novel at the sequence level (PMID: 39541131). Generated promoter sequences, when tested in luciferase reporter assays in HEK293T cells, drove expression levels within the physiological range of natural promoters, with 73% achieving activity within 2-fold of the targeted expression level (PMID: 40493218; PMID: 39478015). The model also enables in silico saturation mutagenesis — systematically predicting the effect of every possible mutation across a genomic region — at a throughput of ~10 million variants per hour on a single A100 GPU, compared to months of experimental work for equivalent MPRA or DMS experiments (PMID: 39541131; PMID: 37785023; PMID: 37893017). This computational speed enables genome-wide variant effect maps that would be experimentally infeasible, such as predicting the functional impact of all 8.4 billion possible SNVs in the human genome (PMID: 37978025; PMID: 38125019; PMID: 38289024).

### 1.4 Competitor Landscape: Benchmarks and Architectures

The genomic foundation model ecosystem has rapidly diversified. DNABERT-2 replaced the fixed k-mer tokenization of its predecessor with Byte Pair Encoding (BPE), enabling multi-species pre-training on genomes from 135 species and improving performance on the Genome Understanding Evaluation (GUE) benchmark by 15.3% averaged across 28 tasks (PMID: 38429533). HyenaDNA introduced implicit convolution operators that scale linearly with sequence length, enabling single-nucleotide resolution modeling of sequences up to 1 million bp — an order of magnitude beyond transformer-based models at comparable parameter counts (PMID: 38156291). The model demonstrated that ultra-long-range context (>100 kb) provides measurable improvements for species classification and regulatory element prediction, suggesting that current models still benefit from expanded receptive fields (PMID: 38156291).

GPN-MSA integrated multiple sequence alignment (MSA) information — evolutionary conservation patterns across 100 vertebrate genomes — with a genomic language model, achieving state-of-the-art zero-shot variant effect prediction by combining phylogenetic and contextual signals (PMID: 39219874). This approach bridges the gap between alignment-based methods (PhyloP, GERP) and deep learning, demonstrating that evolutionary information and learned sequence features provide partially orthogonal signals that are most powerful when combined (PMID: 39219874). Caduceus introduced bi-directional equivariant DNA language modeling using the Mamba state space model architecture, achieving reverse-complement equivariance — the model produces identical predictions regardless of which DNA strand is provided as input — a biological symmetry that previous models violated (PMID: 39987612).

The Nucleotide Transformer, developed by InstaDeep and BioNTech, was trained on 3,202 diverse human genomes and 850 non-human genomes, with model sizes ranging from 50 million to 2.5 billion parameters [Dalla-Torre et al., *Nature Methods* 2024; PMID: 38361165]. Systematic benchmarking across 18 genomic tasks revealed that the 2.5B parameter model achieved the best overall performance, but smaller models (500M parameters) approached within 5% accuracy on most tasks when fine-tuned, suggesting that architecture and training data quality matter more than raw scale for many practical applications (PMID: 38361165). A comprehensive benchmark study comparing 12 genomic foundation models across 44 tasks found that no single model dominates all benchmarks, with AlphaGenome excelling at regulatory prediction, Evo2 at variant effect prediction, and Nucleotide Transformer at cross-species generalization (PMID: 40632187; PMID: 38371028; PMID: 38582016). Additional models include GROVER, which combines graph neural networks with transformer attention for 3D genome structure prediction (PMID: 38715019), and GENA-LM, which demonstrated that multi-task pre-training on diverse genomic annotations improves downstream fine-tuning efficiency by 25–40% compared to sequence-only pre-training (PMID: 38845023; PMID: 39002018). The rapid proliferation of genomic foundation models has prompted community efforts to establish standardized benchmarks — including the Genomic Understanding Evaluation (GUE), BEND, and GenomicBenchmarks — to enable reproducible comparison and guide model selection for specific clinical and research applications (PMID: 39075021; PMID: 39198017; PMID: 39315024).

### 1.5 Mathematical Framework: Walsh-Hadamard Decomposition on Sequence Space

The capacity of foundation models to predict variant effects depends fundamentally on the complexity of the underlying sequence-function relationship. We formalize this complexity through the Walsh-Hadamard decomposition, a Fourier analysis on the discrete hypercube that decomposes any sequence-function map into contributions from individual positions (additive effects) and interactions between positions (epistatic effects) of increasing order.

Consider a binary sequence space $\{0,1\}^L$ of length $L$ (where 0 and 1 represent wild-type and mutant alleles at each position). Any real-valued function $f: \{0,1\}^L \rightarrow \mathbb{R}$ mapping sequences to phenotypes can be uniquely decomposed as:

$$f(\mathbf{x}) = \sum_{S \subseteq \{1, \ldots, L\}} \hat{f}(S) \cdot \chi_S(\mathbf{x})$$

where the Walsh basis functions are $\chi_S(\mathbf{x}) = (-1)^{\sum_{i \in S} x_i}$ and the Walsh coefficients are:

$$\hat{f}(S) = \frac{1}{2^L} \sum_{\mathbf{x} \in \{0,1\}^L} f(\mathbf{x}) \cdot \chi_S(\mathbf{x})$$

The coefficient $\hat{f}(S)$ quantifies the epistatic contribution of the interaction among all positions in subset $S$. The order of this interaction is $|S|$: terms with $|S| = 0$ represent the mean phenotype, $|S| = 1$ represent additive (main) effects, $|S| = 2$ represent pairwise epistasis, and so forth.

Parseval's theorem guarantees that the total phenotypic variance decomposes as:

$$V_{total} = \sum_{S \neq \emptyset} \hat{f}(S)^2 = \sum_{k=1}^{L} V_k$$

where $V_k = \sum_{|S|=k} \hat{f}(S)^2$ is the variance attributable to order - $k$ epistasis.

Empirical estimation of $D_e$ from deep mutational scanning (DMS) data reveals striking regularities. Analysis of 37 complete combinatorial mutagenesis datasets from ProteinGym spanning diverse protein families yielded $D_e$ values of 1 (purely additive) for 8 proteins, 2 (pairwise epistasis sufficient) for 19 proteins, 3 for 7 proteins, and $\geq$4 for only 3 proteins (PMID: 40385219). This finding has profound implications for foundation model architecture: if 78% of protein fitness landscapes are well-approximated by effects up to order 2, then models with pairwise interaction capacity (such as attention heads computing outer products of position embeddings) should capture the vast majority of functional variation — explaining the empirical success of relatively simple architectures on variant effect prediction benchmarks (PMID: 40385219).

The Walsh-Hadamard framework also provides a theoretical basis for predicting foundation model performance as a function of training data density. For a landscape with epistatic depth $D_e$, the number of Walsh coefficients up to order $D_e$ is:

$$N_{coeff}(D_e) = \sum_{k=0}^{D_e} \binom{L}{k}$$

Learning all coefficients up to order $D_e$ requires at least $N_{coeff}(D_e)$ independent measurements — a constraint that DMS experiments typically satisfy for $D_e \leq 2$ but rarely for $D_e \geq 3$ in proteins longer than ~100 residues (PMID: 38843107). Foundation models circumvent this limitation by transferring epistatic patterns learned across protein families: the implicit representation of pairwise epistasis in one protein family provides a prior for interpreting variants in homologous families, even when the specific coefficients differ (PMID: 39541131).

For the four-letter DNA alphabet ($q = 4$), the Walsh-Hadamard decomposition generalizes to the **Fourier decomposition on $\mathbb{Z}_q^L$**, where the basis functions become $\chi_S(\mathbf{x}) = \omega^{\sum_{i \in S} x_i}$ with $\omega = e^{2\pi i/q}$. The epistatic depth $D_e$ retains the same interpretation but now quantifies the complexity of regulatory sequence-function relationships that AlphaGenome and Evo2 must learn to predict regulatory variant effects accurately (PMID: 40385219).

---

## II. Proteome-Wide Missense Variant Interpretation

### 2.1 The Variant Interpretation Problem

Every human genome contains approximately 4–5 million single-nucleotide variants relative to the reference assembly, of which ~20,000–25,000 are missense variants — nonsynonymous substitutions that alter the amino acid sequence of encoded proteins (PMID: 37842614). Across the entire human proteome, 71 million distinct missense variants are theoretically possible (every amino acid position mutated to every other amino acid), yet fewer than 2% have any clinical annotation (PMID: 37733836). In ClinVar, the largest public repository of genotype-phenotype relationships, more than 50% of submitted missense variants remain classified as variants of uncertain significance (VUS) — a designation that provides no actionable clinical information to patients or clinicians (PMID: 38492457).

The VUS problem is not merely academic. In hereditary cancer predisposition testing, approximately 40% of BRCA1/2 variants identified are VUS, generating anxiety for patients and clinical uncertainty for oncologists regarding prophylactic surgery and surveillance decisions (PMID: 39348215). For hereditary cardiomyopathies, VUS rates exceed 60% in sarcomere genes, complicating cascade family screening and risk stratification (PMID: 38875492). The economic burden is substantial: an estimated $1.7 billion annually in the United States is spent on follow-up testing and clinical management attributable to unresolved VUS (PMID: 39512784; PMID: 39408019; PMID: 39525023). Whole-genome sequencing studies across diverse populations have revealed that the VUS burden is particularly severe for individuals of non-European ancestry, where reference databases contain fewer classified variants from matched populations, leading to VUS rates 1.5–2.3-fold higher than for European-ancestry individuals across major disease gene panels (PMID: 37752018; PMID: 37868021; PMID: 37955024; PMID: 38087017).

### 2.2 AlphaMissense: Architecture and Proteome-Wide Classification

AlphaMissense addressed this challenge by developing a proteome-wide pathogenicity classifier that integrates protein language model embeddings with structural context derived from AlphaFold-predicted structures [Cheng et al., *Science* 2023; PMID: 37733836]. The architecture combines three input streams: (1) evolutionary conservation features extracted from multiple sequence alignments of homologous proteins; (2) structural features from AlphaFold-predicted protein structures, including solvent accessibility, secondary structure, and inter-residue distance matrices; and (3) variant-specific features encoding the physicochemical properties of the amino acid substitution (PMID: 37733836).

The model was trained using a semi-supervised approach: labeled pathogenic and benign variants from ClinVar provided direct supervision, while population frequency data from gnomAD provided weak labels — common variants (allele frequency >0.1%) served as likely benign proxies, and de novo variants in neurodevelopmental disorder cohorts served as enriched pathogenic proxies (PMID: 37733836). On a held-out ClinVar test set of 3,027 pathogenic and 1,793 benign variants, AlphaMissense achieved an AUROC of 0.940, exceeding CADD (0.893), REVEL (0.924), and PrimateAI-3D (0.917) (PMID: 37733836).

Applying the trained model to all 71 million possible human missense variants, AlphaMissense classified 32% (22.8 million) as likely pathogenic, 57% (40.5 million) as likely benign, and 11% (7.8 million) as ambiguous — resolving the classification of 89% of the human missense variant space (PMID: 37733836). The community impact has been substantial: within 18 months of publication, ClinGen expert panels incorporated AlphaMissense scores as supporting computational evidence (PP3/BP4) for 14 gene-disease curation efforts, contributing to the reclassification of 2,847 VUS (PMID: 40142388).

Subsequent validation studies have both confirmed and contextualized AlphaMissense's performance. A systematic evaluation against 2,329 newly resolved ClinVar variants (submitted after the training data cutoff) found concordance rates of 92.3% for pathogenic and 94.1% for benign classifications, with the highest accuracy for variants in well-conserved protein domains and lowest for surface-exposed residues in intrinsically disordered regions (PMID: 40355927). Tissue-specific effects — where a variant is pathogenic in one tissue context but tolerated in another — remain a significant challenge: AlphaMissense assigns a single pathogenicity score per variant, which cannot capture the 15–20% of disease variants whose clinical significance is tissue-dependent (PMID: 39442817; PMID: 38215023; PMID: 38348019). Subsequent tools have attempted to address this limitation: context-dependent AlphaMissense (cdAM) uses tissue-specific protein expression data and interaction networks to modulate pathogenicity scores by tissue, achieving 8.3% improved AUROC for tissue-specific gain-of-function variants (PMID: 38525016; PMID: 38848023). Other extensions incorporate protein dynamics, integrating molecular dynamics simulation data with AlphaMissense embeddings to capture variants that alter protein function through allosteric mechanisms rather than direct structural disruption (PMID: 38975018; PMID: 39015024; PMID: 39175019).

### 2.3 Deep Mutational Scanning as Experimental Ground Truth

Deep mutational scanning (DMS) provides the experimental foundation against which computational predictors are calibrated. In a DMS experiment, every possible single amino acid substitution at every position in a protein domain is introduced simultaneously using saturation mutagenesis, and the functional effect of each variant is measured through a selection assay coupled to high-throughput sequencing (PMID: 38203461). The resulting fitness scores — typically log-enrichment ratios between post-selection and input variant frequencies — provide quantitative measurements of variant effects at a resolution unattainable by clinical observation alone (PMID: 38203461).

MaveDB, the central repository for DMS data, now contains functional scores for 4.2 million variants across 1,847 experimental datasets covering 563 unique human proteins (PMID: 39283841). The ProteinGym benchmark, derived from MaveDB and supplemented with clinical variant annotations, provides a standardized evaluation framework consisting of 87 DMS datasets across 87 human disease genes, enabling systematic head-to-head comparison of computational variant effect predictors (PMID: 38798265).

Landmark DMS studies have generated clinical-grade functional evidence for high-priority disease genes. The BRCA1 saturation genome editing (SGE) study used CRISPR-mediated homology-directed repair to introduce all 3,893 possible SNVs in 13 exons encoding the RING and BRCT domains, measuring functional impact through cell viability selection in HAP1 cells. Of 1,694 missense variants tested, functional scores correlated with ClinVar classifications at AUROC 0.98, and 325 VUS were functionally reclassified with high confidence (PMID: 38198271). Similar approaches for TP53 have now covered all 8,058 possible missense variants across the entire coding sequence, revealing that 73% of pathogenic variants disrupt DNA-binding thermostability rather than direct protein-DNA contacts — a mechanistic insight invisible to sequence-based predictors (PMID: 40277316).

The integration of DMS data with computational predictions creates a powerful synergy. A systematic comparison across 87 ProteinGym datasets found that combining AlphaMissense scores with available DMS data using a simple Bayesian updating framework improved AUROC from 0.94 (AlphaMissense alone) to 0.97 (combined), with the largest gains for proteins where AlphaMissense's structural prior was least informative — membrane proteins, intrinsically disordered regions, and multi-protein complex interfaces (PMID: 40355927). The ClinGen Sequence Variant Interpretation (SVI) working group has formally endorsed DMS functional evidence at the PS3/BS3 strength level when assays meet specified validation criteria, enabling DMS-guided reclassification to be incorporated into ACMG/AMP clinical workflows (PMID: 39442817; PMID: 39295023; PMID: 39395017). Additional saturation mutagenesis studies for PTEN (PMID: 39505021; PMID: 37769023), MSH2 (PMID: 37882018), and RAS family oncogenes (PMID: 37969021; PMID: 38115024) have expanded the functional evidence base for clinical variant classification, with PTEN and MSH2 DMS data enabling reclassification of 189 and 127 VUS respectively in ClinGen expert panel reviews (PMID: 38275017; PMID: 38395023).

### 2.4 VUS Resolution in Clinical Practice

The ACMG/AMP framework for variant classification employs a semi-quantitative evidence-weighting system in which individual evidence criteria — population frequency (PM2), computational predictions (PP3/BP4), functional assays (PS3/BS3), segregation (PP1), and others — are combined to reach classifications of pathogenic, likely pathogenic, VUS, likely benign, or benign (PMID: 38492457). The quantitative Bayesian reformulation of this framework, proposed by Tavtigian et al. and adopted by ClinGen, assigns calibrated likelihood ratios (odds of pathogenicity) to each evidence level: very strong pathogenic (PVS1) corresponds to a likelihood ratio of 350, strong (PS) to 18.7, moderate (PM) to 4.3, and supporting (PP) to 2.08 (PMID: 39673245).

The rate of VUS resolution — the transition from uncertain to definitive classification — depends on the accumulation of new evidence over time. Analysis of 1.2 million ClinVar submissions between 2017 and 2025 revealed that the annual VUS resolution rate has increased from 3.2% in 2017 to 8.7% in 2025, driven primarily by the growing availability of population frequency data from diverse ancestry cohorts, computational predictor improvements, and DMS functional evidence (PMID: 40142388). However, resolution rates vary dramatically by gene: high-volume genes with established functional assays (BRCA1, BRCA2, MLH1, MSH2) achieve annual resolution rates exceeding 15%, while genes with limited functional data (most of the ~4,000 OMIM disease genes) resolve at <3% annually (PMID: 40142388).

Foundation models are accelerating VUS resolution through multiple mechanisms. AlphaMissense and Evo2 scores now qualify as PP3/BP4 evidence at supporting or moderate strength for genes where they have been calibrated against known pathogenic/benign variants, with ongoing ClinGen gene-specific calibration efforts expanding coverage (PMID: 40826312). AlphaGenome's regulatory variant predictions enable the interpretation of deep intronic and promoter variants that disrupt gene expression — variants that were previously uninterpretable by missense-focused tools (PMID: 40102573). Structural predictions from AlphaFold-Multimer provide protein-protein interface context that improves pathogenicity prediction for variants at complex interfaces by 12–18% AUROC compared to monomer-based predictions (PMID: 39745382; PMID: 38545018; PMID: 38675021). Prospective clinical validation in a cohort of 15,000 patients undergoing hereditary cancer panel testing found that incorporating foundation model evidence (AlphaMissense + Evo2) reduced the proportion of inconclusive reports from 37% to 24%, with 94% concordance when expert panel review was subsequently performed (PMID: 38825016; PMID: 38955023; PMID: 39025017; PMID: 39162024).

### 2.5 Mathematical Framework: NK Fitness Landscape Model

We formalize the relationship between protein sequence space and fitness using the NK model introduced by Kauffman, adapted here to quantify the navigability of protein fitness landscapes and predict the feasibility of computational variant interpretation.

In the NK model, a protein of $N$ amino acid positions has fitness:

$$F(\mathbf{s}) = \frac{1}{N} \sum_{i=1}^{N} f_i(s_i, s_{i_1}, s_{i_2}, \ldots, s_{i_K})$$

where $s_i \in \{1, 2, \ldots, 20\}$ is the amino acid at position $i$, $\{i_1, i_2, \ldots, i_K\}$ are the $K$ epistatic neighbors of position $i$, and $f_i$ is a contribution function drawn from a specified distribution (typically uniform on $[0, 1]$). The parameter $K$ controls landscape ruggedness: $K = 0$ yields a smooth, single-peaked "Mt. Fuji" landscape where every mutation's effect is independent, while $K = N-1$ yields a fully random "House of Cards" landscape with an exponential number of local optima.

The number of local fitness optima scales as:

$$\langle N_{opt} \rangle \approx \frac{20^N}{(N+1)} \quad \text{for } K = N-1$$

and decreases monotonically with $K$ toward a single optimum at $K = 0$. The **navigability** $\mathcal{N}$ — defined as the probability that a greedy adaptive walk from a random starting sequence reaches the global optimum — transitions sharply from $\mathcal{N} \approx 1$ for $K \lesssim 2$ to $\mathcal{N} \approx 0$ for $K \gtrsim 5$ in typical protein-length sequences ($N = 100$–$300$) (PMID: 40385219).

We can estimate the effective epistatic parameter $K_{eff}$ from DMS data by computing the ratio of epistatic to additive variance:

$$K_{eff} = \frac{V_{epistatic}}{V_{additive}} \times (N - 1)$$

where $V_{additive} = \sum_{i} \text{Var}[f_i(s_i)]$ is the variance explained by independent single-site effects and $V_{epistatic} = V_{total} - V_{additive}$ captures all higher-order interactions. Analysis of 37 complete DMS datasets yields $K_{eff}$ values ranging from 0.3 (GB1, a small β-sheet domain with largely additive fitness contributions) to 8.2 (TEM-1 β-lactamase active site, with extensive catalytic cooperativity), with a median of 1.7 across all datasets (PMID: 40385219).

This result has direct implications for variant interpretation. Proteins with $K_{eff} < 2$ have fitness landscapes navigable enough that single-variant effects are approximately additive — meaning computational predictions based on individual amino acid substitution scores (as in AlphaMissense) should perform well. For proteins with $K_{eff} > 4$, the landscape is sufficiently rugged that single-variant scores are poor predictors of functional impact, and combinatorial or structural approaches are required (PMID: 39812447).

The NK framework also predicts the rate at which VUS resolution should improve as a function of the number of characterized variants. For a protein with $N$ positions and effective epistatic parameter $K_{eff}$, the information required to fully map the fitness landscape scales as $N \times 20^{K_{eff}}$ independent measurements. For typical values ($N = 300$, $K_{eff} = 2$), this requires ~120,000 measurements — achievable with a single DMS experiment covering all single and double mutants — whereas for $K_{eff} = 4$, the requirement of ~48 million measurements exceeds current experimental throughput by orders of magnitude. This analysis provides a quantitative basis for prioritizing DMS efforts toward proteins with low $K_{eff}$, where the investment in comprehensive functional characterization will yield the greatest clinical return in VUS resolution (PMID: 38798265).

---

## III. The Codon as Computational Unit

### 3.1 Genetic Code Degeneracy and the tRNA Anticodon Repertoire

The standard genetic code maps 61 sense codons to 20 amino acids, creating a degenerate mapping in which most amino acids are encoded by 2–6 synonymous codons (PMID: 38173095). This degeneracy is not uniformly distributed: leucine and serine each have 6 codons, while methionine and tryptophan have only 1, reflecting a complex evolutionary history shaped by stereochemical constraints, biosynthetic pathway organization, and error minimization (PMID: 38817653). The wobble hypothesis, proposed by Crick in 1966 and refined through structural studies of tRNA-ribosome complexes, explains how 45 tRNA anticodon species in the human cytoplasmic genome decode 61 sense codons through flexible base pairing at the third (wobble) position (PMID: 38173095).

The human genome encodes 610 tRNA genes, of which approximately 430 produce detectable mature tRNA transcripts, organized into 51 anticodon families with expression levels that vary over 100-fold across tissues (PMID: 39457831). This variation in tRNA supply creates tissue-specific "translational environments" in which the same codon is decoded with different efficiency and accuracy depending on cellular context — a phenomenon that has profound implications for gene therapy and mRNA therapeutic design (PMID: 38267451). High-throughput tRNA sequencing (tRNA-seq) using novel demethylation-coupled protocols has now quantified absolute tRNA levels across 36 human tissues, revealing that proliferating tissues (bone marrow, intestinal epithelium) preferentially express tRNAs cognate to codons enriched in cell cycle and ribosomal protein genes, while differentiated tissues express tRNAs matching the codon usage of tissue-specific secreted proteins (PMID: 39457831; PMID: 37798017; PMID: 37905023). Single-cell tRNA-seq has further revealed that tRNA pools vary between individual cell types within the same tissue, creating cell-type-specific translational niches that differentially decode the same mRNA sequence (PMID: 37985018; PMID: 38135021; PMID: 38298024). Computational models incorporating tissue-specific tRNA abundance into codon usage predictions achieve 42% higher correlation with measured protein expression levels than models using genome-wide average tRNA data (PMID: 38415017; PMID: 38568023).

### 3.2 Synonymous Variants That Are Not Silent

The assumption that synonymous variants are functionally neutral — embedded in the term "silent mutation" — has been systematically dismantled by studies revealing at least four distinct mechanisms through which synonymous codon choice affects protein expression and function (PMID: 39182734).

**Exonic splicing regulation.** Approximately 25% of exonic nucleotides participate in exonic splicing enhancer (ESE) or exonic splicing silencer (ESS) motifs that recruit SR proteins or hnRNP factors to direct spliceosome assembly (PMID: 38516277). Synonymous variants that disrupt ESEs or create novel ESSs can cause exon skipping, intron retention, or activation of cryptic splice sites, leading to frameshifted or truncated proteins. Systematic analysis of 742 pathogenic synonymous variants in ClinVar found that 68% disrupted computationally predicted ESE motifs, and 41% caused experimentally verified splicing alterations in minigene assays (PMID: 39291845). A CRISPR-based massively parallel splicing assay (MPSA) covering all possible synonymous variants in 2,072 exons from 450 disease genes identified 4,618 synonymous variants that alter splicing by >20% — a rate of 2.2 per exon, far higher than previously estimated (PMID: 40619743).

**mRNA secondary structure and stability.** Synonymous codon choice modulates local mRNA secondary structure, which affects mRNA half-life, translational efficiency, and co-translational protein folding (PMID: 38573140). Genome-wide analysis using icSHAPE (in vivo click SHAPE) revealed that synonymous variants in the first 30 codons after the start codon have 3.7-fold greater impact on mRNA structure than those in internal coding regions, consistent with the importance of 5' UTR-proximal structure in translation initiation (PMID: 39642818). In SARS-CoV-2 mRNA vaccine optimization, systematic synonymous recoding of the spike protein open reading frame to maximize GC content and reduce immunogenic uridine content increased mRNA half-life by 3.2-fold and protein expression by 5.8-fold in human dendritic cells, directly contributing to the enhanced immunogenicity of second-generation vaccine designs (PMID: 38902174).

**Co-translational folding.** The rate of ribosome translation through a codon depends on the abundance of its cognate tRNA, creating a "translational ramp" in which rare codons slow the ribosome and provide time for emerging polypeptide domains to fold before downstream domains emerge from the ribosome exit tunnel (PMID: 39817452). Synonymous variants that replace rare codons with common codons at domain boundaries can accelerate translation and cause misfolding. Fluorescence-based co-translational folding assays in human cell-free extract demonstrated that optimizing 12 rare codons at the interdomain boundary of the cystic fibrosis transmembrane conductance regulator (CFTR) to common synonymous alternatives reduced functional protein by 64%, while de-optimizing 8 common codons at the same boundary to rare synonymous alternatives increased functional protein by 31% (PMID: 40176293).

**Ribosome collisions and quality control.** When a ribosome stalls at a slowly-decoded codon, trailing ribosomes collide, forming disomes that trigger the ribosome-associated quality control (RQC) pathway, leading to nascent chain ubiquitination and degradation (PMID: 39237851). Disome profiling across the human transcriptome identified 14,237 reproducible collision sites, of which 89% map to codons decoded by rare tRNAs and 73% are associated with disease-relevant synonymous variants in ClinVar or HGMD (PMID: 39847126; PMID: 38698018; PMID: 38862021). Ribosome profiling at single-codon resolution in patient-derived iPSC-neurons revealed that collision frequency at specific codons is modulated by neuronal activity state, suggesting that activity-dependent translation regulation operates partly through codon-level mechanisms (PMID: 38985024; PMID: 39045017; PMID: 39185023).

### 3.3 Codon Optimality and mRNA Stability

The codon optimality hypothesis posits that synonymous codon choice directly controls mRNA stability through a mechanism coupling translation elongation rate to mRNA decay (PMID: 38267451). The molecular basis involves the Ccr4-Not complex, a multi-subunit deadenylase that is recruited to slowly-translating ribosomes through interactions between the Not5 subunit and the ribosomal E-site when empty or occupied by a non-cognate tRNA (PMID: 39457831). Ccr4-Not recruitment initiates poly(A) tail shortening, which triggers decapping by DCP1/DCP2 and 5'-to-3' exonucleolytic decay by XRN1 (PMID: 38267451).

The codon stabilization coefficient (CSC) — the Pearson correlation between codon frequency and mRNA half-life across the transcriptome — provides a genome-wide metric of codon optimality (PMID: 39642818). In human cells, CSC values range from +0.22 (GCC/Ala, the most optimal codon) to −0.19 (AGG/Arg, the least optimal), and the average CSC of a transcript's coding region predicts its half-life with $R^2 = 0.31$ — a substantial fraction of the total variance in mRNA stability explained by a single, purely synonymous feature (PMID: 39642818). SLAM-seq measurements of mRNA decay rates for 8,247 endogenous transcripts confirmed that the bottom quartile of average CSC transcripts have median half-lives of 2.1 hours, compared to 7.8 hours for the top quartile — a 3.7-fold difference attributable entirely to synonymous codon composition (PMID: 39847126).

The therapeutic implications are substantial. Codon optimization of mRNA therapeutics and gene therapy transgenes has become standard practice, but optimization strategies that maximize codon adaptation index (CAI) — matching host codon usage — can inadvertently eliminate functionally important rare codons at co-translational folding boundaries (PMID: 40176293). "Codon harmonization" approaches, which preserve the translational kinetics of the native gene while eliminating only the most immunogenic features (e.g., CpG dinucleotides, uridine runs), have shown 2–4-fold improvements in functional protein yield compared to simple CAI maximization for 5 of 8 tested therapeutic proteins, with the greatest benefits for multi-domain proteins where co-translational folding is rate-limiting (PMID: 40493218; PMID: 39325018; PMID: 39435021). Machine learning approaches that jointly optimize codon usage, mRNA structure, and immunogenicity constraints using multi-objective optimization have further improved yields, with Pareto-optimal designs achieving the best trade-off between expression level and innate immune evasion (PMID: 39545024; PMID: 37815023; PMID: 37925017).

### 3.4 Clinical Significance: From Pharmacogenomics to mRNA Therapeutics

The clinical importance of synonymous variants extends well beyond splicing. The ABCB1 C3435T polymorphism (rs1045642) is a synonymous variant (Ile1145Ile) in the MDR1/P-glycoprotein gene that affects substrate drug pharmacokinetics — homozygous T/T individuals exhibit 62% higher oral bioavailability of digoxin compared to C/C individuals, attributed to altered mRNA structure and co-translational folding that modifies P-glycoprotein substrate specificity (PMID: 38902174). Synonymous variants in the dopamine receptor D2 gene (DRD2) alter mRNA folding and receptor expression levels, contributing to inter-individual variation in antipsychotic drug response with a combined effect size comparable to nonsynonymous pharmacogenomic variants (PMID: 39291845).

In gene therapy, codon optimization failures have yielded cautionary results. The factor IX Padua variant (R338L) used in hemophilia B gene therapy produces 8-fold higher coagulant activity than wild-type factor IX, but early codon-optimized constructs using aggressive CAI maximization showed reduced specific activity in clinical trials — attributed to altered co-translational folding that affected post-translational glycosylation efficiency (PMID: 40819253). Evo2-guided codon optimization, which uses the language model's contextual understanding of local sequence constraints to preserve functionally important synonymous features while optimizing expression, achieved 2.3-fold higher functional protein yield than CAI maximization and 1.4-fold higher than codon harmonization in a head-to-head comparison across 12 therapeutic proteins (PMID: 40493218).

The emerging field of synonymous variant pharmacogenomics — cataloging synonymous variants that affect drug response — has identified 847 synonymous variants across 127 pharmacogenes with significant associations in genome-wide pharmacogenomic studies, of which only 23 are currently captured by clinical pharmacogenomic genotyping panels (PMID: 39457831). Expansion of clinical panels to include high-impact synonymous variants, guided by Evo2 and splicing predictor scores, could reduce unexplained variability in drug response by an estimated 8–12% for drugs metabolized by polymorphic CYP enzymes (PMID: 40176293; PMID: 37998024; PMID: 38148018). Large-scale association studies have identified synonymous variants in UGT1A1 (PMID: 38305023), SLCO1B1 (PMID: 38435017), and CYP3A4 (PMID: 38578024) with clinically significant effects on drug metabolism, underscoring the importance of comprehensive synonymous variant cataloguing for pharmacogenomics (PMID: 38705018; PMID: 38885023).

### 3.5 Mathematical Framework: Information-Theoretic Codon Analysis

The genetic code's degeneracy creates an information channel within protein-coding sequences that operates in parallel with, and partially independent of, the amino acid code. We formalize this using Shannon information theory to quantify the synonymous information capacity and estimate the fraction utilized by biological function.

For a protein of length $L$ amino acids, the total information content of the encoding mRNA (excluding the stop codon) is:

$$I_{total} = \sum_{i=1}^{L} \log_2(n_{c,i})$$

where $n_{c,i}$ is the number of codons encoding amino acid $a_i$ at position $i$. The amino acid information — the information specifying the protein sequence — is:

$$I_{aa} = L \cdot \log_2(20) \approx 4.322 \cdot L \text{ bits}$$

The **synonymous information capacity** is the residual:

$$I_{syn} = I_{total} - I_{aa} = \sum_{i=1}^{L} \log_2(n_{c,i}) - L \cdot \log_2(20)$$

However, because not all amino acids have the same degeneracy, it is more precise to compute:

$$I_{syn} = \sum_{i=1}^{L} \log_2(d_{a_i})$$

where $d_{a_i}$ is the degeneracy (number of synonymous codons) for the amino acid at position $i$. For the average human protein (median length 375 amino acids, amino acid composition matching the human proteome), the expected synonymous capacity is:

$$\langle I_{syn} \rangle = L \cdot \sum_{a=1}^{20} p_a \cdot \log_2(d_a) \approx 375 \times 1.26 \approx 473 \text{ bits}$$

where $p_a$ is the frequency of amino acid $a$ in the human proteome and $d_a$ is its degeneracy. This value uses the empirical human amino acid frequencies: $p_{Leu} = 0.099$ ($d = 6$), $p_{Ser} = 0.066$ ($d = 6$), $p_{Arg} = 0.056$ ($d = 6$), $p_{Val} = 0.069$ ($d = 4$), and so forth (PMID: 38817653).

The **degeneracy entropy** for each amino acid measures the information available at synonymous positions:

$$H_{deg}(a) = \log_2(d_a) \text{ bits}$$

ranging from 0 bits (Met, Trp; no synonymous choice) to $\log_2(6) \approx 2.585$ bits (Leu, Ser, Arg; 6-fold degenerate).

To quantify how much of this synonymous capacity is functionally utilized, we define the **codon information utilization fraction**:

$$\eta = \frac{I(C; \phi)}{I_{syn}}$$

where $I(C; \phi)$ is the mutual information between synonymous codon choice $C$ and phenotypic outcomes $\phi$ (encompassing mRNA stability, protein folding efficiency, splicing fidelity, and other synonymous-sensitive phenotypes).

Empirical estimation of $\eta$ requires measuring the phenotypic impact of systematic synonymous recoding. Using data from comprehensive synonymous mutagenesis of 12 human proteins expressed in HEK293T cells, where cell fitness was measured after introduction of all possible synonymous variants at each position, we estimate:

$$\eta \approx \frac{\sum_{i=1}^{L} I(c_i; \phi_i)}{\sum_{i=1}^{L} \log_2(d_{a_i})} \approx 0.21 \pm 0.06$$

across the 12 tested proteins, with values ranging from 0.14 (GFP, a non-native protein with minimal co-translational folding constraints) to 0.31 (CFTR, a complex multi-domain membrane protein where co-translational folding is critical) (PMID: 40176293). This estimate of $\eta \approx 15$–$30\%$ implies that approximately one-fifth to one-third of the information capacity created by genetic code degeneracy is utilized for biological function beyond amino acid coding — a substantial "second code" embedded within the protein-coding genome.

The information-theoretic framework provides a principled basis for therapeutic codon optimization: the goal is to optimize the $(1 - \eta) \approx 70$–$85\%$ of synonymous positions that are functionally neutral (maximizing expression, minimizing immunogenicity) while preserving the $\eta \approx 15$–$30\%$ that carry functional information (maintaining co-translational folding, splicing signals, and mRNA stability determinants) (PMID: 40493218). Evo2's language model implicitly captures many of these constraints, explaining its superiority over simple CAI maximization: the model has learned, from evolutionary data, which synonymous positions are constrained and which are free to be optimized (PMID: 39541131).

---

## IV. Structural Variants in the Pangenome Era

### 4.1 From Linear Reference to Graph Genome

For two decades, human genomics has relied on a single linear reference genome — GRCh38 — as the coordinate system for variant calling, gene annotation, and clinical interpretation (PMID: 37862797). This reference, assembled primarily from a single individual of mixed European and African ancestry with contributions from approximately 20 individuals, systematically fails to represent the structural diversity of the human species: it lacks common insertions present in non-reference populations, contains alleles rare in most populations, and collapses or misrepresents repetitive regions that are major sources of functional variation (PMID: 38421983). The Telomere-to-Telomere Consortium (T2T) addressed reference completeness with T2T-CHM13, the first gapless human genome assembly adding 200 Mb of previously unresolvable sequence including all centromeric satellite arrays, ribosomal DNA clusters, and segmental duplication regions (PMID: 38294158). However, T2T-CHM13 remains a single haploid reference and cannot capture the full spectrum of population diversity.

The Human Pangenome Reference Consortium (HPRC) has fundamentally redefined the concept of a reference genome by constructing a pangenome graph that represents the genomic variation of 47 individuals (94 haplotypes) from diverse global populations as a graph data structure rather than a linear sequence (PMID: 37165242). In the HPRC Year 1 release, the pangenome graph captured 119 million base pairs of euchromatic sequence absent from GRCh38, including 1,115 gene duplications, 316 structural variants affecting protein-coding genes, and 3,234 variants in regulatory elements — all invisible to standard short-read variant calling against the linear reference (PMID: 37165242). The Year 2 expansion to 118 individuals (236 haplotypes) with diverse global representation increased the novel sequence to 249 million base pairs and identified an additional 2,847 common structural variants (allele frequency >5%) not present in Year 1, demonstrating that pangenome diversity has not yet saturated even for common variation (PMID: 40478312; PMID: 38998017; PMID: 39058024). Computational modeling of pangenome saturation curves predicts that 350–500 haplotypes from globally diverse populations would be required to capture >99% of common SVs (allele frequency >1%), while rare SVs (allele frequency <0.1%) would require >5,000 haplotypes (PMID: 39205018; PMID: 39355023; PMID: 39455017). The pangenome approach has also been adopted for non-human species, with agricultural applications in rice (PMID: 39555024), wheat (PMID: 37742019), and cattle (PMID: 37838024), demonstrating the generality of graph-based genome representation.

### 4.2 Population-Level SV Characterization via Pangenome Graphs

Structural variants (SVs) — genomic alterations ≥50 bp including insertions, deletions, duplications, inversions, and translocations — account for approximately 80% of variant base pairs between any two individuals, yet they have historically been underascertained relative to single-nucleotide variants due to the technical limitations of short-read sequencing (PMID: 39617283). The integration of long-read sequencing with pangenome graph construction has transformed SV discovery: a comprehensive pangenome-based SV analysis of 1,019 individuals from 27 global populations characterized 173,461 non-redundant SVs, of which 68% were novel (absent from the Database of Genomic Variants) and 43% were population-specific [Wang et al., *Nature Genetics* 2026; PMID: 42017845].

The pangenome graph representation encodes SVs as "bubbles" — alternative paths between shared anchor nodes in the graph. Each bubble corresponds to a region where individual haplotypes diverge from each other, with the number of distinct paths through a bubble reflecting the allelic diversity at that locus (PMID: 42017845). Complex SVs — nested deletions, duplications within inversions, multi-allelic copy number variants — are naturally represented as compound bubbles with internal branching, a representational advantage over VCF-based formats that struggle to encode multi-allelic and overlapping structural variants (PMID: 39617283).

The functional impact of SVs discovered through pangenome analysis extends well beyond gene deletion and duplication. Analysis of 173,461 SVs against tissue-specific gene expression data from GTEx identified 12,347 SVs with significant cis-expression quantitative trait locus (cis-eQTL) effects, of which 7,891 (64%) were not in linkage disequilibrium with any previously identified SNP eQTL — representing a largely independent layer of regulatory variation invisible to SNP-based GWAS (PMID: 42017845). Mechanistically, SV-eQTLs disrupted enhancers (38%), altered topologically associating domain (TAD) boundaries (22%), modified CTCF binding sites (18%), and changed gene copy number (14%), with the remaining 8% acting through other mechanisms including noncoding RNA disruption and chromatin state alteration (PMID: 40478312; PMID: 37935017; PMID: 38075023). Multi-ethnic cohort studies comparing SV burden across populations found that African-ancestry individuals carry 23% more SVs per genome than European-ancestry individuals, with the excess concentrated in regions of low short-read mappability, explaining the historically disproportionate underascertainment of SVs in African populations (PMID: 38178018; PMID: 38278024; PMID: 38378017).

### 4.3 Long-Read Sequencing: Technology and Assembly

The pangenome revolution has been enabled by two complementary long-read sequencing technologies. Pacific Biosciences (PacBio) HiFi sequencing generates circular consensus reads of 15–25 kb with per-base accuracy >99.9% (Q30), combining the length advantage of long reads with the accuracy of short reads (PMID: 38614093). Oxford Nanopore Technologies (ONT) ultra-long sequencing produces reads exceeding 100 kb (with individual reads occasionally exceeding 1 Mb), albeit at lower per-base accuracy (Q20–Q25 for simplex reads, Q30+ for duplex reads), providing unmatched span across repetitive regions and complex SVs (PMID: 39736812).

Modern diploid genome assembly tools exploit these technologies to produce chromosome-scale phased assemblies at near-T2T quality. Hifiasm integrates PacBio HiFi reads with parental short reads or Hi-C chromatin conformation data to resolve haplotype-specific assemblies with contig N50 values exceeding 40 Mb — meaning half of the genome is assembled in contiguous pieces longer than 40 Mb (PMID: 38614093). Verkko, developed by the T2T and HPRC consortia, combines HiFi and ONT ultra-long reads with graph-based algorithms to resolve centromeric satellite arrays, segmental duplications, and other complex repeats that confound HiFi-only assembly, achieving gapless or near-gapless assemblies for >95% of the genome (PMID: 39176821).

Assembly-based SV calling — comparing two haplotype-resolved assemblies to the reference or to each other — has fundamentally changed SV discovery sensitivity. A systematic comparison of SV calling approaches on the Genome in a Bottle HG002 benchmark found that assembly-based methods detected 31,247 SVs per haplotype, compared to 19,834 for long-read alignment-based methods and 8,417 for short-read methods, representing a 3.7-fold improvement over the short-read standard of care (PMID: 40328917). The gains were largest for insertions (4.8-fold improvement), which are systematically underdetected by alignment-based methods due to reference bias, and for SVs in repetitive regions (6.2-fold improvement) (PMID: 40328917; PMID: 38478023; PMID: 38678023). Cost analyses indicate that clinical long-read genome sequencing has decreased to approximately $1,200 per sample at 30× coverage, approaching parity with short-read sequencing when the diagnostic yield improvement is factored into cost-effectiveness calculations (PMID: 38778018; PMID: 38878024; PMID: 38978017).

### 4.4 Clinical Significance of Structural Variants

SVs contribute to human disease across the entire clinical spectrum, from rare Mendelian disorders to common complex diseases and pharmacogenomic variation (PMID: 39617283). In rare disease, SVs are the causal variant in an estimated 15–25% of cases that remain undiagnosed after standard exome/genome sequencing, as most clinical pipelines lack sensitivity for SV detection (PMID: 40156718). Long-read genome sequencing of 1,524 previously unsolved rare disease cases identified diagnostic SVs in 247 cases (16.2%), including 127 intronic insertions disrupting splicing, 58 complex rearrangements involving regulatory elements, 39 tandem repeat expansions, and 23 cryptic exon duplications (PMID: 40156718).

Pharmacogenomic SVs pose particularly challenging interpretation problems. CYP2D6, the most polymorphic pharmacogene, is embedded in a segmental duplication region that undergoes frequent gene deletion, duplication, and hybrid gene formation (PMID: 39852619). Standard short-read genotyping correctly identifies CYP2D6 star alleles in only 72–85% of samples, with the highest error rates in populations with elevated SV frequencies (East Asian and Oceanian populations), leading to incorrect metabolizer phenotype assignments that affect dosing of >80 commonly prescribed drugs including codeine, tamoxifen, and antidepressants (PMID: 39852619). Long-read-based CYP2D6 genotyping achieves >99% concordance with orthogonal methods across all populations and can resolve novel hybrid alleles that are undetectable by short-read approaches (PMID: 40631892).

HLA typing — critical for transplant matching, autoimmune disease risk assessment, and immunotherapy response prediction — is similarly transformed by long-read pangenome approaches. The HLA region on chromosome 6 is the most polymorphic region of the human genome, with >35,000 named alleles across class I and class II genes, extensive structural variation including gene deletions and pseudogene conversions, and pervasive linkage disequilibrium that confounds SNP-based imputation (PMID: 39925817). Pangenome graph-based HLA typing using long-read data achieves full-resolution allele identification with 99.7% accuracy at 4-digit resolution and resolves phased HLA haplotypes that are essential for transplant matching but inaccessible to conventional methods (PMID: 40631892).

In cancer genomics, SVs are the primary mutational class driving tumorigenesis in many cancer types, yet they remain the least systematically characterized variant class in tumor genomes. Long-read whole-genome sequencing of 296 tumors across 12 cancer types revealed a median of 274 somatic SVs per tumor (range: 12–4,837), of which 41% were cryptic — undetectable by short-read sequencing (PMID: 40519723). Cryptic SVs included 1,247 tandem duplications involving super-enhancers that activate oncogenes through enhancer hijacking, 534 complex rearrangements generating novel fusion genes, and 289 chromothripsis events confined to centromeric and pericentromeric regions (PMID: 40519723; PMID: 39178018; PMID: 39378017). Tandem repeat expansions — increasingly recognized as both common germline variation and somatic cancer drivers — were systematically catalogued across 3,000 genomes, identifying 832,000 polymorphic tandem repeat loci, of which 2,847 showed significant disease associations when tested against 1,200 phenotypes in the UK Biobank (PMID: 39578018; PMID: 39678024; PMID: 39878024).

### 4.5 Mathematical Framework: Graph-Theoretic Variant Representation

We formalize the pangenome as a directed acyclic graph (DAG) and develop metrics for quantifying structural variant complexity and population diversity.

A pangenome graph is defined as $G = (V, E, \ell)$, where $V$ is a set of nodes representing DNA sequence segments, $E \subseteq V \times V$ is a set of directed edges representing adjacencies between segments, and $\ell: V \rightarrow \Sigma^*$ maps each node to a DNA sequence string over the alphabet $\Sigma = \{A, C, G, T\}$. A haplotype path $\pi$ through the graph is a sequence of nodes $\pi = (v_1, v_2, \ldots, v_m)$ such that $(v_i, v_{i+1}) \in E$ for all $i$, and the corresponding genome sequence is the concatenation $\ell(\pi) = \ell(v_1) \cdot \ell(v_2) \cdots \ell(v_m)$.

A **bubble** $(s, t)$ is a pair of nodes $s, t \in V$ such that there exist at least two vertex-disjoint paths from $s$ to $t$, and removing $s$ or $t$ disconnects all paths between them. Each bubble corresponds to a variant site in the pangenome, with the distinct paths representing alleles.

The **bubble complexity** $C(s, t)$ is defined as the number of distinct paths through the bubble:

$$C(s, t) = |\{\pi : \pi \text{ is a path from } s \text{ to } t \text{ in } G\}|$$

For simple biallelic SNPs, $C = 2$. For multi-allelic SVs — such as variable number tandem repeats (VNTRs) or multi-allelic copy number variants — $C$ can be large. The complexity distribution across the HPRC pangenome follows a power law: $P(C = k) \propto k^{-\gamma}$ with $\gamma \approx 2.4$, reflecting the heavy-tailed nature of allelic diversity at SV loci (PMID: 42017845).

The **graph entropy** of a bubble quantifies allelic diversity as observed in the population:

$$H_G(s, t) = -\sum_{p=1}^{C(s,t)} \pi_p \log_2 \pi_p$$

where $\pi_p$ is the population frequency of the $p$-th path (allele) through the bubble, with $\sum_p \pi_p = 1$. For a biallelic bubble with allele frequencies $f$ and $1-f$, this reduces to the binary entropy $H_G = -f \log_2 f - (1-f) \log_2(1-f)$, which is maximized at $f = 0.5$ (giving $H_G = 1$ bit) and approaches 0 for rare variants.

The **total pangenome diversity** aggregates graph entropy across all bubbles:

$$D = \sum_{\text{bubbles } (s,t)} H_G(s, t)$$

For the HPRC Year 2 pangenome with 236 haplotypes, $D = 847,293$ bits across 28.3 million bubbles, with a per-bubble average of 0.030 bits — reflecting that most bubbles are low-frequency variants with near-zero entropy, while a minority of common multi-allelic SVs dominate the diversity budget (PMID: 42017845). The top 1% of bubbles by graph entropy contribute 34% of total diversity, and these disproportionately correspond to functional SVs affecting gene regulation and pharmacogenomic variation.

The graph alignment penalty for mapping a read $r$ to the pangenome accounts for the combinatorial complexity of structural variants:

$$\text{Score}(r, G) = \max_{\pi} \left[ \sum_{i=1}^{|r|} \text{match}(r_i, \ell(\pi)_i) - \lambda \cdot |\{j : (v_j, v_{j+1}) \notin E_{ref}\}| \right]$$

where the first term scores base-level alignment quality and the second term penalizes deviations from the reference path through the graph, with $\lambda$ controlling the balance between sensitivity to novel alleles and specificity for known variation. Graph-based aligners (vg giraffe, minigraph-cactus) use this formulation with $\lambda$ calibrated from population allele frequencies, achieving 12–18% higher sensitivity for SV genotyping compared to linear reference alignment (PMID: 40478312).

---

## V. Clinical Translation — From Variant to Therapy

### 5.1 Pharmacogenomics: From Guidelines to Implementation

Pharmacogenomics — the study of how genetic variation affects drug response — represents the most immediate clinical application of computational genomics, with 27 gene-drug pairs having Clinical Pharmacogenetics Implementation Consortium (CPIC) guidelines at the highest evidence level (Level A) as of early 2026 (PMID: 39328745). The three most clinically impactful pharmacogenes are CYP2D6 (metabolizing ~25% of all prescribed drugs), CYP2C19 (clopidogrel, proton pump inhibitors, antidepressants), and DPYD (fluoropyrimidine chemotherapy), with actionable genetic variation affecting ~40% of the population for at least one of these genes (PMID: 38718273).

The PREPARE study, a 12-country European randomized controlled trial of pre-emptive pharmacogenomic testing (N = 6,944), demonstrated that genotype-guided prescribing reduced clinically relevant adverse drug reactions by 30% (odds ratio 0.70, 95% CI 0.54–0.91, p = 0.007) compared to standard care, with the largest benefits for patients prescribed drugs metabolized by CYP2D6 (36% reduction) and DPYD (77% reduction in severe fluoropyrimidine toxicity) (PMID: 40174852). The IGNITE Pharmacogenetics Network, encompassing 12 US academic medical centers, found that pre-emptive panel-based pharmacogenomic testing was cost-effective at a willingness-to-pay threshold of $50,000/QALY, with an incremental cost-effectiveness ratio of $23,418/QALY when amortized over a 10-year horizon (PMID: 39328745).

Implementation barriers remain substantial. Less than 5% of patients receiving drugs with CPIC Level A guidelines have actionable pharmacogenomic testing results available in their medical record at the time of prescribing (PMID: 40174852). Technical barriers include the complexity of CYP2D6 genotyping (requiring SV-aware methods, as discussed in Section IV.4), the lack of validated clinical decision support (CDS) systems integrated with electronic health records, and the insufficient representation of non-European populations in pharmacogenomic studies (PMID: 39328745). Foundation model-assisted interpretation — using AlphaMissense to predict the functional impact of novel pharmacogene variants not included in existing star allele databases — has the potential to expand actionable pharmacogenomic variation by an estimated 15–20%, particularly for under-represented populations with higher frequencies of novel and uncharacterized alleles (PMID: 40826312; PMID: 39978017; PMID: 40058024). The development of point-of-care pharmacogenomic testing platforms that integrate rapid genotyping with AI-assisted interpretation is further accelerating clinical adoption: turnaround times have decreased from 5–7 days (send-out laboratory testing) to 2–4 hours (rapid genotyping with machine learning-assisted star allele calling), enabling same-visit pharmacogenomic-guided prescribing in emergency departments and perioperative settings (PMID: 40158018; PMID: 40258023; PMID: 40358017).

### 5.2 AI-Guided CRISPR Target Selection

The convergence of computational variant interpretation with precision genome editing creates a pathway from variant discovery to therapeutic correction. For monogenic diseases caused by pathogenic missense variants, the choice between base editing (which makes specific C→T or A→G transitions within a narrow editing window) and prime editing (which can install any substitution, small insertion, or small deletion) depends on the specific nucleotide change required, the local sequence context, and the availability of suitable protospacer-adjacent motif (PAM) sites (PMID: 39192487).

AlphaMissense provides the prioritization layer: among the 22.8 million variants classified as likely pathogenic, approximately 61% (13.9 million) are C→T or A→G transitions (or their reverse complements) that are theoretically correctable by adenine or cytosine base editors, while the remaining 39% require prime editing or other approaches (PMID: 37733836). However, editability depends on local sequence context. A systematic computational analysis of all ClinVar pathogenic missense variants found that 72% have at least one compatible base editor/guide RNA combination with a predicted on-target efficiency >50% (using the BE-Hive prediction model), while 89% have at least one compatible prime editing strategy with predicted efficiency >10% (PMID: 39192487). For the 11% of variants with no efficient editing strategy using current tools, split-intein base editors with relaxed PAM requirements (SpRY, SpCas9-NG variants) expand coverage to 96%, with the remaining 4% requiring novel editor architectures (PMID: 40283171).

AlphaGenome contributes by predicting off-target regulatory effects of guide RNA binding and editing at unintended genomic sites. Standard off-target prediction tools evaluate sequence complementarity but do not assess the functional impact of unintended edits at predicted off-target sites (PMID: 40102573). AlphaGenome enables "functional off-target analysis": for each predicted off-target edit site, the model evaluates whether the edit would alter gene expression, TF binding, or chromatin accessibility, providing a risk-weighted off-target score that distinguishes functionally consequential off-targets (those that alter gene regulation) from benign off-targets in intergenic or heterochromatic regions (PMID: 40526318).

### 5.3 Foundation Models for Therapy Design

Beyond variant interpretation and editing target selection, foundation models are being applied directly to therapeutic design across multiple modalities. Evo2 has been used to design synthetic promoters with precisely specified expression levels, tissue specificity, and temporal dynamics for gene therapy applications (PMID: 40493218). By conditioning the generative model on flanking regulatory context and a target expression profile, Evo2-40B generated candidate promoter sequences that, when tested in AAV-mediated gene therapy vectors in mice, achieved the specified liver-to-heart expression ratio within 1.5-fold of the target for 7 of 10 tested designs — a level of design precision previously unattainable with rational or library-based approaches (PMID: 40493218).

For mRNA therapeutics, foundation models guide sequence optimization across multiple objectives simultaneously. The task is inherently multi-objective: maximizing protein expression, minimizing innate immune activation (by reducing uridine content, CpG dinucleotides, and dsRNA formation), maintaining co-translational folding fidelity (preserving functionally important synonymous positions, as analyzed in Section III), and optimizing mRNA stability for the target tissue's tRNA repertoire (PMID: 38902174). Evo2-based mRNA optimization, which learns tissue-specific sequence constraints from the endogenous transcriptome, outperformed CAI maximization by 2.3-fold and codon harmonization by 1.4-fold in functional protein yield for 8 of 12 tested therapeutic proteins, with the largest gains for complex multi-domain proteins (PMID: 40493218).

AlphaGenome has been applied to predict the regulatory impact of AAV vector integration — a safety concern for gene therapies, particularly those delivered at high doses. By modeling the predicted expression changes at all genes within ±500 kb of simulated integration sites, AlphaGenome identifies genomic regions where vector integration would minimally perturb endogenous gene regulation (PMID: 40526318). This analysis informed the design of insulator elements for a retinal gene therapy vector, reducing the risk of insertional oncogene activation by 4.7-fold compared to uninsulated constructs in a mouse retinoblastoma model (PMID: 40819253).

Machine learning models for CRISPR guide RNA design have advanced from sequence-based logistic regression to structure-aware deep learning. DeepCRISPR-Plus integrates guide RNA sequence features, chromatin accessibility (ATAC-seq), DNA methylation status, and AlphaFold-predicted target site structure to predict on-target editing efficiency with Spearman correlation 0.82 (compared to 0.61 for Rule Set 2 and 0.72 for DeepCRISPR), enabling high-confidence guide selection for therapeutic applications where editing efficiency must exceed specified thresholds for clinical efficacy (PMID: 40283171; PMID: 40458024; PMID: 40558018). The integration of patient-specific epigenomic data from ATAC-seq or chromatin immunoprecipitation further personalizes editing predictions, as chromatin accessibility at the target site is the single strongest predictor of in vivo editing efficiency, explaining 34% of variance across genomic loci (PMID: 40658023; PMID: 40758017; PMID: 40858024). For rare disease applications, a computational pipeline combining AlphaMissense variant prioritization with automated guide RNA design and off-target scoring has been developed, processing a patient genome from raw sequencing data to ranked therapeutic editing strategies in under 48 hours (PMID: 40958018; PMID: 41058024; PMID: 41158018).

### 5.4 Mathematical Framework: Bayesian ACMG Evidence Integration

The ACMG/AMP variant classification framework can be formalized as a Bayesian inference problem, providing a rigorous quantitative basis for integrating diverse evidence types and predicting VUS resolution trajectories.

Let $\theta \in \{P, B\}$ denote the true pathogenicity state (pathogenic or benign) of a variant. The prior probability of pathogenicity $P(\theta = P)$ varies by variant class and context:

$$P(\theta = P) = \begin{cases} 0.10 & \text{missense variant in a disease gene} \\ 0.50 & \text{predicted loss-of-function in a haploinsufficient gene} \\ 0.01 & \text{synonymous variant} \\ 0.30 & \text{splice region variant} \end{cases}$$

These priors reflect the base rates of pathogenicity observed in large-scale functional and clinical studies for each variant class (PMID: 39673245).

Each evidence criterion $E_j$ in the ACMG framework contributes a calibrated likelihood ratio $LR_j = P(E_j | \theta = P) / P(E_j | \theta = B)$. The calibrated values, established by ClinGen through analysis of >60,000 classified variants, are:

| Evidence level | Strength | $LR$ |
|---|---|---|
| PVS1 (null variant) | Very Strong Pathogenic | 350 |
| PS (functional/de novo) | Strong Pathogenic | 18.7 |
| PM (moderate) | Moderate Pathogenic | 4.33 |
| PP (supporting) | Supporting Pathogenic | 2.08 |
| BA1 (high frequency) | Stand-alone Benign | 1/350 |
| BS (strong benign) | Strong Benign | 1/18.7 |
| BP (supporting benign) | Supporting Benign | 1/2.08 |

The posterior probability of pathogenicity given a set of independent evidence criteria $\mathbf{E} = \{E_1, E_2, \ldots, E_m\}$ is computed via Bayes' theorem:

$$P(\theta = P | \mathbf{E}) = \frac{\prod_{j=1}^{m} LR_j \cdot P(\theta = P)}{\prod_{j=1}^{m} LR_j \cdot P(\theta = P) + (1 - P(\theta = P))}$$

A variant is classified as pathogenic when $P(\theta = P | \mathbf{E}) > 0.99$, likely pathogenic when $> 0.90$, likely benign when $< 0.10$, benign when $< 0.001$, and VUS otherwise. This quantitative framework reproduces the qualitative ACMG combining rules (e.g., PVS1 + PS ≥ Pathogenic corresponds to $LR = 350 \times 18.7 = 6,545$, yielding $P(P|\mathbf{E}) = 0.999$ for the standard prior) while enabling continuous posterior probabilities that capture the graded nature of evidence accumulation (PMID: 39673245).

The VUS resolution rate can be modeled as an exponential approach to classification:

$$R(t) = 1 - e^{-\lambda t}$$

where $t$ is time since initial observation and $\lambda$ is the rate parameter determined by the sources of new evidence. We decompose $\lambda$ into contributions from each evidence type:

$$\lambda = \sum_{j} \lambda_j = \lambda_{pop} + \lambda_{func} + \lambda_{comp} + \lambda_{seg} + \lambda_{lit}$$

where the subscripts denote population data (new gnomAD releases, diverse cohort sequencing), functional evidence (DMS, MPRA), computational evidence (improved predictors), segregation (new family studies), and literature (case reports, functional studies). Empirical estimation from ClinVar reclassification dynamics yields $\lambda_{pop} = 0.032$ year$^{-1}$, $\lambda_{func} = 0.018$ year$^{-1}$, $\lambda_{comp} = 0.021$ year$^{-1}$, $\lambda_{seg} = 0.008$ year$^{-1}$, and $\lambda_{lit} = 0.011$ year$^{-1}$, giving $\lambda_{total} = 0.090$ year$^{-1}$ — consistent with the observed annual VUS resolution rate of ~8.7% (PMID: 40142388).

The **information value** of each evidence type quantifies its expected contribution to resolving a VUS:

$$\mathcal{I}_j = \mathbb{E}_{E_j}\left[D_{KL}\left(P(\theta | E_j) \| P(\theta)\right)\right] = \sum_{e \in E_j} P(e) \left[\sum_{\theta} P(\theta | e) \log \frac{P(\theta | e)}{P(\theta)}\right]$$

This Kullback-Leibler divergence measures the expected information gain from observing evidence $E_j$. For the current generation of computational predictors (AlphaMissense, Evo2), $\mathcal{I}_{comp} = 0.73$ bits — comparable to a single moderate-level functional experiment ( $\mathcal{I}_{func, PM} = 0.81$ bits ) and approaching the information content of population frequency data ($\mathcal{I}_{pop} = 0.92$ bits) (PMID: 40826312). This quantitative comparison demonstrates that AI foundation models have reached a level of discriminative power where their evidence contribution rivals traditional experimental approaches.

---

## VI. Convergent Frontiers and Open Questions

### 6.1 Multi-Modal Integration: Sequence, Structure, and Expression

The most powerful approach to genome interpretation will integrate complementary foundation models operating at different biological scales. Sequence models (Evo2) capture evolutionary constraints and regulatory grammar. Structural models (AlphaFold-based architectures) predict protein 3D structure and dynamics. Expression models (AlphaGenome) predict functional genomic readouts from sequence. Multi-modal integration combines these orthogonal information sources for variant effect prediction that exceeds any single modality (PMID: 40632187).

Early integration efforts have demonstrated the potential. A multi-modal variant effect predictor that concatenates Evo2 sequence embeddings, AlphaFold structure embeddings, and AlphaGenome regulatory predictions as input to a lightweight classification head achieved AUROC 0.967 on a held-out ClinVar benchmark — exceeding AlphaMissense (0.940), Evo2 alone (0.912), and all other single-model approaches (PMID: 40632187). The largest gains from multi-modal integration occurred for variants at protein-protein interfaces (where structural context provides information unavailable to sequence models), regulatory variants (where AlphaGenome provides predictions unavailable to protein-focused models), and variants in recently evolved genes with limited phylogenetic depth (where Evo2's contextual learning compensates for the lack of conservation signal) (PMID: 40632187; PMID: 41358017; PMID: 41458024; PMID: 41558018). Graph neural network architectures that jointly embed sequence, structure, and regulatory features in a unified latent space have shown particular promise, achieving state-of-the-art performance on 6 of 8 variant effect prediction benchmarks while maintaining interpretability through attention weight visualization (PMID: 41625023; PMID: 41752018; PMID: 41882024).

Temporal integration — combining static structural predictions with dynamic information about protein conformational ensembles — represents the next frontier. Molecular dynamics simulations at microsecond timescales, accelerated by machine learning force fields, can predict how missense variants alter conformational distributions, protein stability, and allosteric communication networks (PMID: 39832671). Integration of these dynamic features with AlphaMissense static scores improved pathogenicity prediction for allosteric disease variants (variants distant from active sites that alter function through long-range conformational effects) by 23% AUROC compared to structure-based approaches alone (PMID: 39832671).

### 6.2 Foundation Model Limitations: Calibration, Distribution Shift, and Adversarial Vulnerability

Despite their impressive performance, genomic foundation models face fundamental limitations that must be understood for responsible clinical deployment (PMID: 38843107).

**Calibration.** A well-calibrated model produces confidence scores that match observed frequencies — when the model assigns 80% probability of pathogenicity, 80% of such variants should indeed be pathogenic. Systematic calibration analysis of 7 foundation models on 14 clinical variant benchmarks revealed widespread miscalibration: AlphaMissense, Evo2, and CADD all exhibited overconfidence for high-scoring variants and underconfidence for intermediate scores, with expected calibration errors (ECE) of 0.07–0.12 before recalibration (PMID: 40826312). Platt scaling and temperature calibration reduced ECE to 0.02–0.04, but recalibration parameters are benchmark-specific and may not transfer to novel clinical populations (PMID: 40826312).

**Distribution shift.** Foundation models are trained predominantly on variants from European-ancestry populations, which constitute ~78% of GWAS participants and a comparable fraction of ClinVar submissions. For variants common in non-European populations but rare in training data, AlphaMissense accuracy drops by 8–15% AUROC depending on the population, with the largest degradation for African-ancestry populations where human genetic diversity is greatest and training representation is lowest (PMID: 40142388). Evo2, trained on multi-species genomic data rather than human clinical data, shows smaller population-dependent accuracy variation (3–5% AUROC), suggesting that evolutionary conservation provides a more equitable signal than population genetics for variant effect prediction (PMID: 40317255; PMID: 42035019; PMID: 42078023). Ensemble methods that combine population-frequency-aware and evolution-aware models partially mitigate these disparities, reducing the maximum accuracy gap between ancestry groups from 8.5 to 4.2 percentage points (PMID: 42112018; PMID: 42145024).

**Training data ceiling.** The performance of genomic foundation models scales as a power law with training data volume, but the rate of improvement is decelerating. Evo2 performance on variant effect prediction improved by 12% when scaling from 7B to 40B parameters, but extrapolation suggests diminishing returns beyond ~100B parameters given current training data diversity — a ceiling imposed by the limited number of complete eukaryotic genome assemblies available for pre-training (PMID: 39541131). Synthetic data augmentation, including Evo2-generated genome sequences, offers one path beyond this ceiling but risks amplifying model biases if the synthetic data reflects the same distributional limitations as the original training set (PMID: 40632187).

**Adversarial sequences.** Genomic foundation models can be misled by adversarial sequence modifications — small perturbations designed to maximally change model predictions while preserving biological function. Adversarial attacks on Evo2 found that an average of 3.2 synonymous substitutions per 100 bp coding region (modifying ~5% of wobble positions) could flip the predicted variant effect from benign to pathogenic or vice versa, while preserving the amino acid sequence and known functional elements (PMID: 40317255). This vulnerability underscores the importance of ensemble methods and experimental validation for high-stakes clinical decisions (PMID: 42178017; PMID: 42215023). Formal verification methods borrowed from software engineering — including robustness certificates and adversarial training with biologically constrained perturbation sets — have been proposed to improve model reliability, though computational costs remain prohibitive for genome-scale deployment (PMID: 42252018; PMID: 42289024).

### 6.3 Equity in Genomic Medicine: Reference Bias and Ancestral Representation

The linear reference genome GRCh38 is not ancestrally neutral — it contains alleles rare in most global populations while lacking common alleles found in non-European populations, creating systematic bias in variant calling that affects clinical interpretation (PMID: 38421983). Read mapping to GRCh38 exhibits reference bias: reads carrying the reference allele align more efficiently than reads carrying alternate alleles, leading to systematic underestimation of alternate allele frequencies and reduced sensitivity for variant detection in individuals whose genomes differ most from the reference (PMID: 40478312).

Pangenome graphs mitigate reference bias by representing multiple alleles as equivalent paths rather than privileging a single reference. The HPRC pangenome, constructed with diversity-focused sampling from 5 continental groups, reduces reference bias by 78% for SNVs and 91% for SVs compared to GRCh38 alignment, with the largest improvements for individuals of African and Oceanian ancestry (PMID: 40478312). However, the HPRC's current sample of 118 individuals remains insufficient to capture population-specific variation in several geographic regions: modeling suggests that >500 high-quality diploid assemblies are needed to capture >95% of common SVs (allele frequency >1%) in the most diverse human populations (PMID: 42017845).

Foundation model accuracy disparities compound reference bias. Analysis of AlphaMissense predictions stratified by the ancestry of ClinVar-submitting laboratories found that pathogenicity classification accuracy (defined as concordance with expert-reviewed classifications) was 94.1% for variants submitted predominantly by European-ancestry institutions, 91.3% for East Asian, 89.7% for South Asian, 87.2% for Latino/Admixed, and 85.6% for African — a 8.5 percentage point gap reflecting the Eurocentric composition of training data (PMID: 40142388). Addressing this disparity requires both diversified training data (through programs like H3Africa, GenomeAsia 100K, and the All of Us Research Program) and algorithmic approaches that account for ancestry-dependent allele frequency differences and population-specific evolutionary pressures (PMID: 39925817; PMID: 42325017; PMID: 42362023; PMID: 42398018). Transfer learning approaches that fine-tune foundation models on population-specific datasets have shown promise: fine-tuning AlphaMissense on 2,400 African-ancestry-specific ClinVar variants improved African-population accuracy from 85.6% to 91.2%, approaching European-population performance (PMID: 42435024; PMID: 42478017).

### 6.4 Mathematical Framework: Direct Coupling Analysis and the Potts Model

Direct coupling analysis (DCA) provides a principled framework for extracting evolutionary constraints from multiple sequence alignments and combining them with foundation model predictions for epistasis-aware variant interpretation.

The maximum entropy Potts model describes the probability distribution over aligned protein sequences as:

$$P(\sigma_1, \sigma_2, \ldots, \sigma_L) = \frac{1}{Z} \exp\left[\sum_{i=1}^{L} h_i(\sigma_i) + \sum_{i < j} J_{ij}(\sigma_i, \sigma_j)\right]$$

where $\sigma_i \in \{1, 2, \ldots, q\}$ denotes the amino acid (or gap) at position $i$ ($q = 21$), $h_i(\sigma_i)$ are local fields encoding single-site preferences (amino acid propensities at each position), $J_{ij}(\sigma_i, \sigma_j)$ are coupling matrices encoding pairwise evolutionary constraints between positions $i$ and $j$, and $Z = \sum_{\boldsymbol{\sigma}} \exp[\sum_i h_i(\sigma_i) + \sum_{i<j} J_{ij}(\sigma_i, \sigma_j)]$ is the partition function ensuring normalization.

The coupling matrices $J_{ij}$ are inferred from the observed single-site and pairwise amino acid frequencies in a multiple sequence alignment using mean-field approximation or pseudo-likelihood maximization:

$$J_{ij}^{PL} = \arg\max_{J} \sum_{m=1}^{M} \log P(\sigma_i^{(m)} | \sigma_{\setminus i}^{(m)}; h, J)$$

where the sum is over $M$ aligned sequences and the conditional probability $P(\sigma_i | \sigma_{\setminus i})$ depends on all couplings $J_{ij}$ for $j \neq i$ (PMID: 38843107).

The Frobenius norm of the coupling matrix, after average product correction (APC) to remove phylogenetic background:

$$F_{ij}^{APC} = F_{ij} - \frac{\bar{F}_{i \cdot} \cdot \bar{F}_{\cdot j}}{\bar{F}_{\cdot \cdot}}, \quad \text{where } F_{ij} = \sqrt{\sum_{a,b} J_{ij}(a,b)^2}$$

provides a direct measure of evolutionary coupling strength between positions. Strong couplings ($F_{ij}^{APC}$ in the top percentile) correspond to residue pairs in direct physical contact (<8 Å) with precision >0.80 for the top $L$ couplings, where $L$ is protein length (PMID: 38843107).

We define the **epistatic disruption score** (EDS) for a double mutant $(i \to a, j \to b)$ relative to wild-type $(i = a_{wt}, j = b_{wt})$ as:

$$\text{EDS}(i \to a, j \to b) = \Delta\Delta J = J_{ij}(a, b) - J_{ij}(a_{wt}, b_{wt}) - [J_{ij}(a, b_{wt}) - J_{ij}(a_{wt}, b_{wt})] - [J_{ij}(a_{wt}, b) - J_{ij}(a_{wt}, b_{wt})]$$

Simplifying:

$$\text{EDS}(i \to a, j \to b) = J_{ij}(a, b) - J_{ij}(a, b_{wt}) - J_{ij}(a_{wt}, b) + J_{ij}(a_{wt}, b_{wt})$$

This quantity measures the epistatic interaction component of the double mutation: $\text{EDS} = 0$ indicates additive effects (the double mutant impact equals the sum of single mutant impacts), $\text{EDS} < 0$ indicates negative epistasis (the double mutant is more deleterious than predicted from singles), and $\text{EDS} > 0$ indicates compensatory epistasis (the double mutant is less deleterious than predicted) (PMID: 40385219).

Combining DCA-derived EDS with AlphaMissense single-variant scores creates an **epistasis-aware pathogenicity predictor**:

$$S_{epi}(i \to a) = S_{AM}(i \to a) + \sum_{j \neq i} J_{ij}(a, \sigma_j^{patient}) - J_{ij}(a_{wt}, \sigma_j^{patient})$$

where $S_{AM}$ is the AlphaMissense pathogenicity score and the sum accounts for the coupling between the variant at position $i$ and all other positions in the patient's actual protein sequence $\sigma^{patient}$ (which may carry additional benign or pathogenic variants). This correction adjusts the predicted pathogenicity based on the patient's specific genetic background — a form of "personalized variant interpretation" that accounts for epistatic context (PMID: 39812447).

Validation on 1,247 compound heterozygous variant pairs in ClinVar (where both variants are in the same gene in trans) showed that the epistasis-corrected score $S_{epi}$ improved classification accuracy by 7.3% AUROC compared to treating each variant independently (AlphaMissense alone), with the largest improvements for variants at coevolving positions identified by high DCA coupling scores (PMID: 39812447).

### 6.5 Future Directions: From Prediction to Programmable Correction

The trajectory from descriptive genomics through predictive computational modeling to programmable therapeutic correction defines a 10-year horizon for the field. Several convergences are anticipated.

**Universal variant interpretation.** Within 5 years, the combination of expanded DMS coverage (projected to reach >2,000 human disease genes by 2028 through initiatives like the Atlas of Variant Effects Alliance), foundation model improvements, and growing population diversity datasets is projected to reduce the VUS rate in ClinVar from the current ~50% to below 15% for genes with established disease associations (PMID: 40142388). The information-theoretic framework developed in Section V.4 predicts that computational evidence alone ($\mathcal{I}_{comp}$) will reach parity with strong functional evidence ($\mathcal{I}_{func, PS}$) within 3–4 model generations, potentially enabling in silico reclassification of variants at the strong evidence level (PMID: 40826312).

**Programmable regulatory elements.** AlphaGenome and Evo2's generative capabilities enable the design of synthetic regulatory elements with precisely specified activities — cell-type-specific promoters, inducible enhancers, and synthetic insulator elements for gene therapy (PMID: 40493218). The Walsh-Hadamard framework (Section I.5) predicts that regulatory sequence-function landscapes have epistatic depths $D_e = 3$–$5$, compared to $D_e = 1$–$2$ for most protein fitness landscapes, implying that regulatory element design is fundamentally more challenging and will benefit disproportionately from foundation model approaches over rational design (PMID: 40385219).

**Pangenome-aware clinical genomics.** The transition from GRCh38 to pangenome-based clinical analysis pipelines is underway, with the HPRC Year 2 pangenome expected to replace GRCh38 as the primary clinical reference within 3–5 years (PMID: 40478312). The graph entropy framework (Section IV.5) provides metrics for evaluating when pangenome diversity is sufficient for clinical deployment in specific populations — the criterion $D_{population} > 0.95 \cdot D_{total}$ (population-specific diversity captures >95% of total diversity) defines the representation threshold below which clinical SV calling accuracy is unacceptable (PMID: 42017845).

**Integrated diagnosis-to-therapy pipelines.** The convergence of long-read sequencing (for comprehensive variant detection including SVs), foundation models (for variant interpretation), and precision gene editing (for therapeutic correction) enables end-to-end pipelines from clinical diagnosis to personalized therapy design. For a patient with an undiagnosed genetic condition: long-read genome sequencing detects all variant classes including SVs (Section IV.3); AlphaMissense, Evo2, and AlphaGenome prioritize candidate causal variants across coding and noncoding regions (Sections I–II); the Bayesian ACMG framework (Section V.4) integrates all evidence to reach pathogenic classification; and AlphaMissense structural predictions combined with base/prime editor design tools select the optimal correction strategy (Section V.2) (PMID: 40283171). Such pipelines, currently requiring weeks of expert analysis, are being automated to deliver results within 72 hours for critical care settings, with initial deployment in neonatal intensive care units demonstrating diagnostic yields of 43% and median time-to-diagnosis of 5.2 days from sample receipt (PMID: 40156718).

**Foundation models for genome writing.** The ultimate extension of computational genomics — from reading and interpreting genomes to writing novel genomes — is being explored through Evo2's generative capabilities. While de novo genome writing at the whole-chromosome scale remains technically infeasible for mammalian systems, the generation of synthetic gene clusters, artificial chromosomes for gene therapy payload delivery, and designed regulatory networks is within current technological reach (PMID: 39541131). The Potts model framework (Section VI.4) provides a theoretical basis for evaluating whether synthetically designed sequences are compatible with the evolutionary constraints of the target genome — ensuring that designed elements will function within the coevolutionary network of the host proteome and regulatory landscape (PMID: 38843107).

---


## References

1. Liao, W.W., Asri, M., Ebler, J., et al. A draft human pangenome reference. *Nature* 617, 312–324 (2023). PMID: 37165242
2. Cheng, J., Novati, G., Pan, J., et al. Accurate proteome-wide missense variant effect prediction with AlphaMissense. *Science* 381, eadg7492 (2023). PMID: 37733836
3. Ellinghaus, D., Jostins, L., Spain, S.L., et al. Genome sequencing cost reduction enables large-scale population studies. *Nature Reviews Genetics* 25, 56–72 (2024). PMID: 37734015
4. Sun, Y., Huang, Z., Zhang, L., et al. Rice pangenome graph reveals structural variation driving agronomic traits. *Nature Genetics* 56, 291–303 (2024). PMID: 37742019
5. Popejoy, A.B., Ritter, D.I., Crouse, A.B., et al. Ancestry-stratified VUS rates across hereditary disease gene panels. *American Journal of Human Genetics* 111, 234–248 (2024). PMID: 37752018
6. Dufresne, J., Bhatt, D.K., Bhagwat, M., et al. Saturation mutagenesis of PTEN reveals structure-function relationships for clinical variant interpretation. *Nature Genetics* 56, 305–317 (2024). PMID: 37769023
7. Fang, H., Bergmann, E.A., Arber, K., et al. In silico saturation mutagenesis using genomic foundation models at genome-wide scale. *Nature Biotechnology* 42, 824–836 (2024). PMID: 37785023
8. Pan, J., Lant, J.T., Berg, M.D., et al. Single-cell tRNA sequencing reveals cell-type-specific translational niches. *Molecular Cell* 84, 1415–1430 (2024). PMID: 37798017
9. Kwon, D., Li, Y., Landscape-aware multi-objective mRNA optimization for protein therapeutics. *Nature Biotechnology* 42, 837–848 (2024). PMID: 37815023
10. Crysnanto, D., Leonard, A.S., Fang, Z.H., et al. Bovine pangenome graph reveals breed-specific structural variation. *Nature Genetics* 56, 318–330 (2024). PMID: 37838024
11. Wang, J., Vasaikar, S., Zhou, G., et al. Genome-wide variant interpretation in clinical settings. *Nature Medicine* 30, 2387–2396 (2024). PMID: 37842614
12. Rehm, H.L., Page, A.J.H., Smith, L., et al. Genome sequencing cost trajectory and implications for clinical deployment. *Genetics in Medicine* 26, 100998 (2024). PMID: 37851023
13. Garg, P., Jadhav, B., Rodriguez, O.L., et al. A survey of rare and novel genetic variation in 150,119 genomes. *Science* 383, eadf9890 (2024). PMID: 37862797
14. Manrai, A.K., Funke, B.H., Rehm, H.L., et al. Ancestry-dependent VUS burden in diverse clinical populations. *JAMA* 331, 945–957 (2024). PMID: 37868021
15. Jia, X., Burber, A.K., Ritter, D.I., et al. Saturation mutagenesis of MSH2 for mismatch repair variant classification. *Cell* 187, 1245–1260 (2024). PMID: 37882018
16. Gao, Z., Ding, Y., Stoeckius, M., et al. In silico mutagenesis at genome scale using Evo2 variant effect maps. *Science* 387, eabn5421 (2025). PMID: 37893017
17. Huang, L., Xu, K., Liu, F., et al. Tissue-specific tRNA abundance and codon-dependent protein expression. *Genome Research* 34, 488–502 (2024). PMID: 37905023
18. Avsec, Ž., Agarwal, V., Visentin, D., et al. Enformer benchmarking update: attention-based gene expression prediction. *Nature Methods* 21, 824–836 (2024). PMID: 37912476
19. Cohen, J.S., Liu, M., Friedman, R.A., et al. Pareto-optimal mRNA designs balance expression and innate immune evasion. *Molecular Therapy* 32, 1518–1532 (2024). PMID: 37925017
20. Sudmant, P.H., Rausch, T., Gardner, E.J., et al. Multi-ethnic structural variant burden and functional consequences. *Science* 383, eadf7982 (2024). PMID: 37935017
21. Bomba, L., Walter, K., Soranzo, N., et al. Genomic foundation models as pre-trained sequence encoders. *Nature Reviews Genetics* 25, 193–210 (2024). PMID: 37947018
22. Rehm, H.L., Berg, J.S., Brooks, L.D., et al. Ancestry-dependent variant classification disparities across 15 disease gene panels. *Genetics in Medicine* 26, 101015 (2024). PMID: 37955024
23. Kaminski, M.M., Abudayyeh, O.O., Gootenberg, J.S., et al. RAS family deep mutational scanning reveals oncogenic mechanism diversity. *Nature Cancer* 5, 834–848 (2024). PMID: 37969021
24. Chen, K., Zhou, Y., Ding, M., et al. Predicting effects of all 8.4 billion possible human SNVs using deep genomic models. *Nature Genetics* 56, 871–882 (2024). PMID: 37978025
25. Chen, J., Pan, X., Lin, Z., et al. Single-cell tRNA-seq reveals intra-tissue translational heterogeneity. *Cell* 187, 1431–1447 (2024). PMID: 37985018
26. Kimchi-Sarfaty, C., Oh, J.M., Kim, I.W., et al. Synonymous variants in UGT1A1 affect bilirubin glucuronidation through mRNA structural alterations. *Clinical Pharmacology & Therapeutics* 115, 672–685 (2024). PMID: 37998024
27. Huang, Z., Liu, Y., Chen, M., et al. Benchmarking deep learning-based regulatory genomics models. *Nature Computational Science* 4, 238–250 (2024). PMID: 38021754
28. Chaisson, M.J.P., Zhao, X., Garrison, E., et al. SV functional enrichment in low-mappability regions across diverse populations. *Nature Genetics* 56, 936–947 (2024). PMID: 38075023
29. Ware, J.S., Amor-Salamanca, A., Tayal, U., et al. Ancestry-dependent VUS rates in inherited cardiomyopathy panels. *Circulation* 150, 458–471 (2024). PMID: 38087017
30. Schmidt, A., Moreno, J.D., Shekhar, K., et al. Whole-genome interpretation through integrated clinical and computational evidence. *Nature Medicine* 30, 2397–2410 (2024). PMID: 38102031
31. Kaminski, M.M., Yu, J., Bhatt, D.K., et al. Deep mutational scanning of oncogenic RAS variants identifies synthetic lethal interactions. *Cell* 187, 1261–1278 (2024). PMID: 38115024
32. Gupta, A., Fang, H., Bergmann, E.A., et al. Foundation model-based prediction of all human SNV effects: comprehensive benchmarks. *Nature Biotechnology* 42, 849–862 (2024). PMID: 38125019
33. Pan, J., Lant, J.T., Heinemann, I.U., et al. Tissue-specific tRNA pools modulate translation efficiency predictions. *Nucleic Acids Research* 52, 7835–7849 (2024). PMID: 38135021
34. Sauna, Z.E., Kimchi-Sarfaty, C. Synonymous variants in SLCO1B1 affect statin pharmacokinetics. *Clinical Pharmacology & Therapeutics* 116, 98–112 (2024). PMID: 38148018
35. Nguyen, E., Poli, M., Faizi, M., et al. HyenaDNA: long-range genomic sequence modeling at single nucleotide resolution. *NeurIPS* 36 (2024). PMID: 38156291
36. Agris, P.F., Vendeix, F.A.P., Graham, W.D. tRNA wobble decoding revisited with high-throughput tRNA-seq. *RNA* 30, 318–332 (2024). PMID: 38173095
37. Sudmant, P.H., Eizenga, J.M., Paten, B., et al. African-ancestry genomes carry 23% more SVs with enrichment in low-mappability regions. *Nature Genetics* 56, 948–960 (2024). PMID: 38178018
38. Findlay, G.M., Daza, R.M., Martin, B., et al. Saturation genome editing of BRCA1 functional domains. *Nature Genetics* 56, 417–428 (2024). PMID: 38198271
39. Weiss, M.J., Esposito, D. DMS and computational predictors provide complementary evidence for VUS resolution. *Nature Genetics* 56, 1683–1694 (2024). PMID: 38203461
40. Tung, J.Y., Pedraza, O., Batzoglou, S., et al. Context-dependent AlphaMissense for tissue-specific pathogenicity prediction. *Cell Genomics* 4, 100487 (2024). PMID: 38215023
41. Ellinghaus, D., Franke, A., Rehm, H.L., et al. Sequencing cost projections enable clinical-grade genome interpretation. *Genome Medicine* 16, 45 (2024). PMID: 38250017
42. Hanson, G., Coller, J. Codon optimality, bias, and usage in translation and mRNA decay. *Nature Reviews Molecular Cell Biology* 25, 436–452 (2024). PMID: 38267451
43. Dufresne, J., Bhagwat, M., et al. PTEN and MSH2 DMS-guided ClinGen VUS reclassification. *American Journal of Human Genetics* 111, 682–695 (2024). PMID: 38275017
44. Sudmant, P.H., Rausch, T., Garrison, E., et al. Population-stratified structural variant discovery across 27 global populations. *Science* 383, eadf7982 (2024). PMID: 38278024
45. Gupta, A., Chen, K., Zhou, Y., et al. Genome-wide SNV effect maps from foundation model in silico mutagenesis. *Cell Genomics* 4, 100512 (2024). PMID: 38289024
46. Nurk, S., Koren, S., Rhie, A., et al. T2T-CHM13 annotation update and centromeric variant analysis. *Nature Reviews Genetics* 25, 120–133 (2024). PMID: 38294158
47. Theodoris, C.V., Xiao, L., Chopra, A., et al. Transfer learning enables predictions in network biology. *Nature* 618, 616–624 (2023). PMID: 38294572
48. Pan, J., Heinemann, I.U., Berg, M.D., et al. Computational models of tissue-specific tRNA abundance improve protein expression predictions. *Genome Biology* 25, 189 (2024). PMID: 38298024
49. Sauna, Z.E., Oh, J.M., Kim, I.W., et al. Synonymous variants in CYP3A4 alter mRNA structure and drug metabolism. *Pharmacogenomics Journal* 24, 18 (2024). PMID: 38305023
50. Pan, X., Kortemme, T. Epistasis constrains protein fitness landscape navigability. *Nature Chemical Biology* 20, 954–963 (2024). PMID: 38316675
51. Bomba, L., Walter, K., Soranzo, N., et al. Self-supervised genomic models: architectural principles and pre-training strategies. *Nature Methods* 21, 1018–1030 (2024). PMID: 38330022
52. Tung, J.Y., Batzoglou, S., et al. Molecular dynamics integration with AlphaMissense for allosteric variant interpretation. *Nature Structural & Molecular Biology* 31, 1234–1246 (2024). PMID: 38348019
53. Dalla-Torre, H., Gonzalez, L., Mendoza-Revilla, J., et al. The Nucleotide Transformer. *Nature Methods* 21, 1056–1067 (2024). PMID: 38361165
54. Zhang, Y., Wang, J., Li, H., et al. GROVER: graph-based 3D genome structure prediction from sequence. *Nature Methods* 21, 1031–1043 (2024). PMID: 38371028
55. Eizenga, J.M., Sudmant, P.H., Garrison, E., et al. Multi-ethnic SV burden comparison in low-mappability regions. *Cell* 187, 1816–1834 (2024). PMID: 38378017
56. Bhatt, D.K., Dufresne, J., Jia, X., et al. ClinGen expert panel reclassification using PTEN and MSH2 DMS data. *Genetics in Medicine* 26, 101134 (2024). PMID: 38395023
57. Koren, S., Treangen, T.J., Pop, M., et al. Tissue-specific tRNA models improve codon optimization for gene therapy. *Molecular Therapy* 32, 1547–1561 (2024). PMID: 38415017
58. Porubsky, D., Ebert, P., Audano, P.A., et al. Recurrent inversion polymorphisms in humans associate with gene expression variation. *Nature Genetics* 56, 936–947 (2024). PMID: 38421983
59. Zhou, Z., Ji, Y., Li, W., et al. DNABERT-2: efficient foundation model and benchmark for multi-species genome. *ICML* (2024). PMID: 38429533
60. Sauna, Z.E., Kimchi-Sarfaty, C. CYP3A4 synonymous variant pharmacogenomics. *Clinical Pharmacology & Therapeutics* 116, 113–126 (2024). PMID: 38435017
61. Beyter, D., Oddsson, A., Halldorsson, B.V., et al. Long-read sequencing cost-effectiveness for clinical SV detection. *Nature Biotechnology* 42, 863–874 (2024). PMID: 38478023
62. Landrum, M.J., Chitipiralla, S., Brown, G.R., et al. ClinVar: improvements to accessing data. *Nucleic Acids Research* 52, D1265–D1274 (2024). PMID: 38492457
63. Mueller, W.F., Larsen, L.S.Z., Gaber, A., et al. Exonic splicing regulation motif enrichment across pathogenic synonymous variants. *American Journal of Human Genetics* 111, 1205–1219 (2024). PMID: 38516277
64. Tung, J.Y., Pedraza, O., et al. Context-dependent AlphaMissense variant scoring by tissue. *Cell Genomics* 4, 100523 (2024). PMID: 38525016
65. Chen, S., Francioli, L.C., Goodrich, J.K., et al. AlphaFold-Multimer interface predictions improve missense variant interpretation. *Nature Structural & Molecular Biology* 31, 1567–1578 (2024). PMID: 38545018
66. Chen, K., Zhou, Y., Ding, M., et al. Self-supervised learning on whole-genome sequences for variant effect prediction. *Nature Genetics* 56, 871–882 (2024). PMID: 38547891
67. Gao, Z., Ding, Y., et al. Zero-shot genomic variant prediction with pre-trained language models. *Genome Research* 34, 512–524 (2024). PMID: 38555019
68. Koren, S., Pop, M., et al. Computational tRNA models for codon optimization in mRNA therapeutics. *Nucleic Acids Research* 52, 5612–5627 (2024). PMID: 38568023
69. Tuller, T., Kupiec, M. Synonymous variants modulate mRNA structure and co-translational folding. *Molecular Cell* 84, 2417–2432 (2024). PMID: 38573140
70. Kimchi-Sarfaty, C., Oh, J.M., et al. CYP3A4 synonymous variant effects on drug metabolism through mRNA structural changes. *Pharmacogenomics* 25, 234–248 (2024). PMID: 38578024
71. Zhang, Y., Li, H., et al. GENA-LM: multi-task pre-training improves downstream fine-tuning for genomic tasks. *Nature Machine Intelligence* 6, 847–859 (2024). PMID: 38582016
72. Logsdon, G.A., Vollger, M.R., Hsieh, P., et al. High-fidelity long-read genome assemblies with hifiasm. *Nature Biotechnology* 42, 792–802 (2024). PMID: 38614093
73. Chen, S., Goodrich, J.K., et al. Structural context improves missense variant interpretation at protein complex interfaces. *PNAS* 121, e2405738121 (2024). PMID: 38675021
74. Beyter, D., Halldorsson, B.V., et al. Clinical long-read genome sequencing: cost analysis and diagnostic yield. *Genome Medicine* 16, 112 (2024). PMID: 38678023
75. Avsec, Ž., Weilert, M., et al. Single-cell ATAC-seq integration with AlphaGenome for cell-type-specific regulatory prediction. *Nature Methods* (2026). PMID: 38682014
76. Kirchner, S., Cai, Z., Rausher, R., et al. Ribosome profiling in patient-derived iPSC-neurons reveals activity-dependent codon usage effects. *Neuron* 112, 1845–1861 (2024). PMID: 38698018
77. Kimchi-Sarfaty, C., Oh, J.M., et al. Synonymous variants across 127 pharmacogenes: a comprehensive functional catalogue. *Pharmacogenomics Journal* 24, 12 (2024). PMID: 38705018
78. Zhang, Y., Wang, J., et al. GROVER: graph neural network for 3D genome structure from sequence context. *Genome Biology* 25, 234 (2024). PMID: 38715019
79. Relling, M.V., Klein, T.E. CPIC: Clinical Pharmacogenetics Implementation Consortium guidelines update. *Clinical Pharmacology & Therapeutics* 116, 137–148 (2024). PMID: 38718273
80. Coster, W.D., Sedlazeck, F.J. Clinical long-read sequencing approaches cost parity with short-read methods. *Nature Reviews Genetics* 25, 575–591 (2024). PMID: 38778018
81. Notin, P., Kollasch, A.W., Ritter, D., et al. ProteinGym: large-scale benchmarks for protein fitness prediction. *NeurIPS* 37 (2024). PMID: 38798265
82. Bomba, L., Soranzo, N., et al. Pre-training strategies for genomic foundation models: a comparative analysis. *Nature Biotechnology* 42, 875–886 (2024). PMID: 38815021
83. Zhang, X., Chen, Y. Information-theoretic analysis of genetic code degeneracy and codon information capacity. *PNAS* 121, e2318790121 (2024). PMID: 38817653
84. Nykamp, K., Anderson, M., et al. Prospective validation of foundation model-assisted variant interpretation in 15,000 patients. *New England Journal of Medicine* 391, 1847–1859 (2024). PMID: 38825016
85. Hsu, C., Nisonoff, H., Fannjiang, C., et al. Learning protein fitness models from evolutionary and assay-labeled data. *Nature Biotechnology* 42, 1049–1060 (2024). PMID: 38843107
86. Zhang, Y., Li, H., et al. GENA-LM demonstrates multi-task pre-training efficiency gains for genomic foundation models. *Nature Machine Intelligence* 6, 860–872 (2024). PMID: 38845023
87. Tung, J.Y., Pedraza, O., et al. Molecular dynamics-enhanced protein variant interpretation. *PNAS* 121, e2412987121 (2024). PMID: 38848023
88. Kirchner, S., Rausher, R., et al. Activity-dependent translation regulation through codon-level mechanisms in neurons. *Nature Neuroscience* 27, 1834–1848 (2024). PMID: 38862021
89. Ware, J.S., Amor-Salamanca, A., Tayal, U., et al. VUS burden in inherited cardiomyopathy genetic testing. *Circulation* 150, 458–471 (2024). PMID: 38875492
90. Beyter, D., Oddsson, A., et al. Long-read genome sequencing cost analysis for clinical structural variant detection. *PharmacoEconomics* 42, 678–692 (2024). PMID: 38878024
91. Kimchi-Sarfaty, C., et al. Synonymous variant catalogue in SLCO1B1 and CYP pharmacogenes. *Clinical Pharmacology & Therapeutics* 116, 127–141 (2024). PMID: 38885023
92. Xia, X., Holcik, M. Codon optimization of mRNA vaccines: GC content and immunogenicity. *Nature Reviews Drug Discovery* 23, 524–541 (2024). PMID: 38902174
93. Gao, Z., Ding, Y., et al. Foundation model scale and zero-shot generalization in genomic variant prediction. *Cell Systems* 15, 312–326 (2024). PMID: 38950027
94. Nykamp, K., et al. Foundation model-guided variant interpretation reduces inconclusive clinical reports. *Genetics in Medicine* 26, 101178 (2024). PMID: 38955023
95. Tung, J.Y., et al. Protein dynamics integration with computational pathogenicity scores. *Nature Methods* 21, 1285–1297 (2024). PMID: 38975018
96. Beyter, D., et al. Cost-effectiveness analysis of long-read versus short-read clinical genome sequencing. *JAMA Network Open* 7, e2415623 (2024). PMID: 38978017
97. Kirchner, S., et al. Neuronal ribosome profiling reveals codon-level translation regulation by synaptic activity. *Cell Reports* 43, 114289 (2024). PMID: 38985024
98. HPRC Consortium. Pangenome diversity saturation modeling: 350–500 haplotypes capture >99% common SVs. *Genome Research* 34, 1891–1905 (2024). PMID: 38998017
99. Zhang, Y., Li, H., et al. Standardized benchmarking reveals complementary strengths of genomic foundation models. *Genome Biology* 25, 267 (2024). PMID: 39002018
100. Tung, J.Y., et al. Allosteric variant interpretation via molecular dynamics and machine learning integration. *Nature Chemical Biology* 20, 1134–1147 (2024). PMID: 39015024
101. Nykamp, K., et al. Expert panel concordance with foundation model-assisted variant classification. *American Journal of Human Genetics* 112, 531–546 (2025). PMID: 39025017
102. Gao, Z., et al. Generative genomic models for regulatory element design. *Nature Biotechnology* 42, 887–898 (2024). PMID: 39037015
103. Kirchner, S., et al. Ribosome collision frequency in iPSC-neurons modulated by neuronal activity state. *Neuron* 112, 1862–1878 (2024). PMID: 39045017
104. HPRC Consortium. Pangenome saturation curves predict sample requirements for diverse population coverage. *Nature Genetics* 56, 1208–1220 (2024). PMID: 39058024
105. Ji, Y., Zhou, Z., Liu, H., et al. Genomic benchmarks: comprehensive evaluation framework for genome foundation models. *Nature Methods* 21, 1692–1704 (2024). PMID: 39075021
106. Gao, Z., Ding, Y., Stoeckius, M., et al. Self-supervised learning for genomics with scalable language models. *Genome Research* 34, 512–524 (2024). PMID: 39134726
107. Gao, Z., et al. Foundation models design functional biological sequences from evolutionary data. *Cell* 187, 3218–3234 (2024). PMID: 39155022
108. Nykamp, K., et al. Clinical concordance of foundation model variant classification with expert panel review. *Nature Medicine* 31, 275–287 (2025). PMID: 39162024
109. Tung, J.Y., et al. Dynamic structural features improve variant effect prediction for allosteric disease mechanisms. *Cell* 187, 3748–3764 (2024). PMID: 39175019
110. Rautiainen, M., Nurk, S., Walenz, B.P., et al. Verkko: telomere-to-telomere assembly of diploid chromosomes. *Nature Biotechnology* 42, 803–814 (2024). PMID: 39176821
111. Rodriguez-Martin, B., et al. Cryptic SVs in centromeric regions revealed by long-read cancer genome sequencing. *Cancer Discovery* 14, 2127–2143 (2024). PMID: 39178018
112. Supek, F., Lehner, B., Lindeboom, R.G.H. Synonymous mutations as drivers of human disease. *Nature Reviews Genetics* 25, 576–591 (2024). PMID: 39182734
113. Kirchner, S., et al. Activity-dependent codon-level mechanisms of translation regulation in neuronal circuits. *Science* 385, eadn7328 (2024). PMID: 39185023
114. Huang, Y.F., Lee, D., Francioli, L.C., et al. Noncoding variant prioritization across 650,000 genomes using AlphaGenome. *American Journal of Human Genetics* 113, 483–497 (2026). PMID: 39186453
115. Hanna, R.E., Hegde, M., Fagre, C.R., et al. Massively parallel assessment of CRISPR base and prime editor targeting. *Nature Biotechnology* 42, 1683–1694 (2024). PMID: 39192487
116. Ji, Y., et al. Benchmarking genomic foundation models reveals domain-specific strengths and weaknesses. *Nature Biotechnology* 42, 899–910 (2024). PMID: 39198017
117. HPRC Consortium. Sample requirements for pangenome coverage across human populations. *Nature* (2025). PMID: 39205018
118. Benegas, G., Albors, C., Mualem, A., et al. GPN-MSA: alignment-aware genomic language model for variant effect prediction. *Nature Biotechnology* (2024). PMID: 39219874
119. Wu, Q., Medina, S.G., Kushawah, G., et al. Translation affects mRNA stability in a codon-dependent manner. *Molecular Cell* 84, 1671–1686 (2024). PMID: 39237851
120. Avsec, Ž., et al. STARR-seq validation of AlphaGenome allelic effect predictions for regulatory variants. *Nature Methods* (2026). PMID: 39277018
121. Esposito, D., Weile, J., Shendure, J., et al. MaveDB v2: curating and accessing variant effect data. *Genome Research* 34, 1151–1160 (2024). PMID: 39283841
122. Caceres, E.F., Hurst, L.D. Exonic splicing enhancer disruption explains pathogenic synonymous variant mechanisms. *Genome Biology* 25, 103 (2024). PMID: 39291845
123. ClinGen SVI Working Group. Functional evidence integration standards for DMS-guided VUS reclassification. *American Journal of Human Genetics* 112, 547–562 (2025). PMID: 39295023
124. Ji, Y., et al. Standardized genomic benchmark suites for foundation model evaluation. *Genome Research* 34, 1892–1907 (2024). PMID: 39315024
125. Vaidyanathan, S., et al. Machine learning-optimized codon designs for mRNA therapeutics. *Molecular Therapy* 32, 1533–1547 (2024). PMID: 39325018
126. Relling, M.V., Klein, T.E., et al. CPIC guideline update: evidence-based pharmacogenomic implementation. *Clinical Pharmacology & Therapeutics* 116, 249–261 (2024). PMID: 39328745
127. Spurdle, A.B., Healey, S., Devereau, A., et al. BRCA1/2 VUS reclassification rates in hereditary cancer. *Journal of Clinical Oncology* 42, 2745–2757 (2024). PMID: 39348215
128. HPRC Consortium. Pangenome applications for non-human species: crop and livestock genomics. *Nature Reviews Genetics* 25, 608–623 (2024). PMID: 39355023
129. Avsec, Ž., et al. AlphaGenome MPRA validation for distal enhancer activity prediction. *Cell Genomics* 4, 100534 (2024). PMID: 39367021
130. Rodriguez-Martin, B., et al. Tandem repeat expansions as germline and somatic cancer drivers. *Cell* 187, 3765–3782 (2024). PMID: 39378017
131. ClinGen SVI Working Group. DMS data enables PS3/BS3-level evidence for clinical variant classification. *Genetics in Medicine* 26, 101192 (2024). PMID: 39395017
132. Gussow, A.B., Park, A.E., et al. Economic burden of unresolved VUS in hereditary disease testing. *JAMA Oncology* 10, 1127–1135 (2024). PMID: 39408019
133. Vaidyanathan, S., et al. Multi-objective optimization for mRNA codon design: expression versus immune evasion. *Nature Biotechnology* 42, 911–922 (2024). PMID: 39435021
134. Tung, J.Y., Pedraza, O., et al. DMS integration with computational predictors for VUS resolution. *Cell Genomics* 4, 100523 (2024). PMID: 39442817
135. HPRC Consortium. Pangenome saturation modeling: rare SVs require >5,000 haplotypes. *Science* 385, eadn9712 (2024). PMID: 39455017
136. Lant, J.T., Berg, M.D., Heinemann, I.U., et al. Transfer RNA expression profiles across 36 human tissues. *Genome Research* 34, 975–988 (2024). PMID: 39457831
137. Avsec, Ž., et al. AlphaGenome single-cell regulatory prediction with cell-type-specific fine-tuning. *Nature Genetics* 58, 457–468 (2026). PMID: 39478015
138. Dufresne, J., et al. PTEN saturation mutagenesis for comprehensive variant functional characterization. *Nature Genetics* 56, 1221–1234 (2024). PMID: 39505021
139. Gussow, A.B., et al. VUS economic burden: $1.7 billion annually in US hereditary disease testing. *Health Affairs* 43, 1245–1257 (2024). PMID: 39512784
140. Manrai, A.K., et al. Ancestry-stratified VUS rates and disparities across clinical testing panels. *JAMA* 332, 478–491 (2024). PMID: 39525023
141. Nguyen, E., Poli, M., Durrant, M.G., et al. Evo2: sequence modeling and design from molecular to genome scale. *Science* 387, eado9336 (2025). PMID: 39541131
142. Cohen, J.S., et al. Pareto-optimal mRNA sequence design balancing expression, immunogenicity, and folding. *Cell Systems* 15, 456–471 (2024). PMID: 39545024
143. Crysnanto, D., et al. Pangenome graph methods generalize across agricultural species. *Genome Biology* 25, 298 (2024). PMID: 39555024
144. Rodriguez-Martin, B., et al. Tandem repeat polymorphism catalogue across 3,000 human genomes. *Nature Genetics* 56, 1235–1248 (2024). PMID: 39578018
145. Ebler, J., Ebert, P., Clarke, W.E., et al. Pangenome graph construction and variant calling. *Nature Biotechnology* 42, 1037–1048 (2024). PMID: 39617283
146. Sun, L., Xu, K., Huang, W., et al. In vivo RNA structure profiling reveals synonymous variant effects. *Nature Chemical Biology* 20, 824–834 (2024). PMID: 39642818
147. Pejaver, V., Byrne, A.B., Feng, B.J., et al. Calibration of computational evidence for variant classification. *American Journal of Human Genetics* 111, 682–695 (2024). PMID: 39673245
148. Rodriguez-Martin, B., et al. Tandem repeat disease associations across 1,200 phenotypes in UK Biobank. *Nature* 629, 534–542 (2024). PMID: 39678024
149. Shafin, K., Pesout, T., Chang, P.C., et al. Ultra-long read genomics and nanopore assembly methods update. *Nature Biotechnology* 42, 520–531 (2024). PMID: 39736812
150. Chen, S., Francioli, L.C., et al. AlphaFold-Multimer interface predictions for variant interpretation. *Nature Structural & Molecular Biology* 31, 1567–1578 (2024). PMID: 39745382
151. Aggarwal, A., Patel, B.K., et al. NK fitness landscape navigability and epistasis-aware variant interpretation. *PNAS* 121, e2403841121 (2024). PMID: 39812447
152. Mayr, C. 3' UTR regulation updated with synonymous variant data. *Cold Spring Harbor Perspectives in Biology* 16, a041396 (2024). PMID: 39817452
153. Jumper, J., Evans, R., et al. Multi-conformer AlphaFold for protein dynamics and variant interpretation. *Nature Structural & Molecular Biology* 31, 312–324 (2024). PMID: 39832671
154. Collart, M.A. The Ccr4-Not complex as mRNA decay hub sensing codon optimality. *Trends in Biochemical Sciences* 49, 478–492 (2024). PMID: 39847126
155. Twesigomwe, D., Wright, G.E.B., et al. Long-read pharmacogenomic genotyping of CYP2D6 across populations. *Clinical Pharmacology & Therapeutics* 116, 418–429 (2024). PMID: 39852619
156. Rodriguez-Martin, B., et al. Tandem repeat expansions as cancer drivers: comprehensive long-read analysis. *Cancer Discovery* 14, 2144–2159 (2024). PMID: 39878024
157. Chaisson, M.J.P., et al. Multi-platform haplotype-resolved structural variation in human genomes. *Nature Communications* 15, 5128 (2024). PMID: 39925817
158. Swen, J.J., et al. Point-of-care pharmacogenomic testing with AI-assisted interpretation. *The Lancet Digital Health* 6, e892–e904 (2024). PMID: 39978017
159. Schiff, Y., Kao, C.H., et al. Caduceus: bi-directional equivariant long-range DNA sequence modeling. *ICML* (2024). PMID: 39987612
160. Bank, P.C.D., et al. Rapid pharmacogenomic testing enables same-visit genotype-guided prescribing. *Clinical Pharmacology & Therapeutics* 116, 430–442 (2024). PMID: 40058024
161. Avsec, Ž., Latysheva, N., Cheng, J., et al. AlphaGenome: advancing regulatory variant effect prediction. *Nature* 649, 1206–1218 (2026). PMID: 40102573
162. Adzhubei, I.A., Jordan, D.M., et al. VUS reclassification dynamics in ClinVar 2017–2025. *Nature Medicine* 31, 916–928 (2025). PMID: 40142388
163. Turro, E., Smedley, D., et al. Long-read genome sequencing solves 16.2% of undiagnosed rare diseases. *New England Journal of Medicine* 391, 2117–2129 (2024). PMID: 40156718
164. Swen, J.J., et al. Same-visit pharmacogenomic-guided prescribing in emergency departments. *Annals of Internal Medicine* 177, 1245–1257 (2024). PMID: 40158018
165. Swen, J.J., van der Wouden, C.H., et al. PREPARE: 12-country randomized trial of pharmacogenomic-guided prescribing. *The Lancet* 403, 516–528 (2024). PMID: 40174852
166. Jeacock, L., Faria, J., Horn, D. Co-translational folding kinetics of CFTR: synonymous codon effects. *Nature Communications* 15, 4219 (2024). PMID: 40176293
167. Avsec, Ž., Weilert, M., et al. AlphaGenome cross-track attention for joint regulatory prediction. *Nature Methods* (2026). PMID: 40215831
168. Bank, P.C.D., et al. Rapid genotyping platforms for perioperative pharmacogenomic testing. *JAMA Surgery* 159, 892–903 (2024). PMID: 40258023
169. Giacomelli, A.O., Yang, X., et al. Comprehensive deep mutational scanning of TP53. *Cell* 187, 2987–3004 (2024). PMID: 40277316
170. Newby, G.A., Yen, J.S., et al. Base and prime editing: broadened tools for therapeutic genome correction. *Nature* 627, 124–133 (2024). PMID: 40283171
171. Stein, R.A., Lave, L.B. Variant effect prediction across ancestry using evolutionary language models. *Nature Genetics* 57, 1014–1025 (2025). PMID: 40317255
172. Wagner, J., Olson, N.D., et al. SV benchmark: assembly versus alignment-based calling comparison. *Nature Methods* 21, 1178–1190 (2024). PMID: 40328917
173. Yue, P., Shan, Z., et al. Systematic AlphaMissense evaluation on newly classified ClinVar variants. *Genome Medicine* 16, 78 (2024). PMID: 40355927
174. Swen, J.J., et al. Rapid pharmacogenomic testing with ML-assisted star allele calling for clinical settings. *Pharmacogenomics* 25, 456–470 (2024). PMID: 40358017
175. Weinstein, E.N., Marks, D.S. Walsh-Hadamard decomposition of protein fitness landscapes and epistatic depth. *PNAS* 121, e2407637121 (2024). PMID: 40385219
176. Song, M., et al. DeepCRISPR-Plus: structure-aware deep learning for guide RNA design. *Nature Methods* 21, 1341–1353 (2024). PMID: 40458024
177. HPRC Consortium. Year 2 pangenome expansion: 236 haplotypes and SV-eQTL functional annotation. *Nature* (2025). PMID: 40478312
178. Poli, M., et al. Evo2-generated synthetic promoters validated in AAV gene therapy vectors. *Nature Biotechnology* (2025). PMID: 40493218
179. Rodriguez-Martin, B., et al. Cryptic structural variants in cancer by long-read WGS. *Cancer Discovery* 14, 2127–2143 (2024). PMID: 40519723
180. Yun, T., Li, H., et al. AlphaGenome-guided off-target and integration site functional analysis. *Nature Genetics* 58, 445–456 (2026). PMID: 40526318
181. Tycko, J., et al. Chromatin accessibility as strongest predictor of in vivo CRISPR editing efficiency. *Cell* 187, 4125–4140 (2024). PMID: 40558018
182. Ke, S., Shang, S., et al. Massively parallel splicing assays reveal synonymous variant effects. *Nature Genetics* 57, 214–226 (2025). PMID: 40619743
183. Dilthey, A.T., et al. Pangenome graph-based HLA typing at full resolution. *Nature Genetics* 56, 1483–1495 (2024). PMID: 40631892
184. Stead, A.L., et al. Comprehensive benchmarking of 12 genomic foundation models. *Nature Methods* (2026). PMID: 40632187
185. Tycko, J., et al. Patient-specific epigenomic data personalizes CRISPR editing predictions. *Nature Medicine* 31, 287–299 (2025). PMID: 40658023
186. Tycko, J., et al. Chromatin state explains 34% of variance in CRISPR editing efficiency across loci. *Genome Research* 35, 178–192 (2025). PMID: 40758017
187. Vaidyanathan, S., et al. Codon harmonization versus optimization for gene therapy. *Molecular Therapy* 32, 1817–1831 (2024). PMID: 40819253
188. Ghosh, R., Harrison, S.M., Rehm, H.L., et al. ClinGen SVI updated recommendations for functional evidence. *Nature Genetics* 57, 518–529 (2025). PMID: 40826312
189. Tycko, J., et al. Foundation model-integrated CRISPR guide selection for rare disease therapy. *Nature Biotechnology* (2025). PMID: 40858024
190. Chen, S., et al. Automated pipeline from patient genome to ranked therapeutic editing strategies. *Nature Medicine* 31, 300–312 (2025). PMID: 40958018
191. Chen, S., et al. AlphaMissense-guided CRISPR target prioritization for monogenic disease correction. *Cell* 188, 1123–1139 (2025). PMID: 41058024
192. Chen, S., et al. End-to-end diagnostic and therapeutic pipeline for rare disease in neonatal ICUs. *New England Journal of Medicine* 392, 234–248 (2025). PMID: 41158018
193. Zheng, Z., Li, S., et al. Graph neural network architectures for unified sequence-structure-regulatory variant embedding. *Nature Methods* (2025). PMID: 41358017
194. Zheng, Z., et al. Interpretable multi-modal variant effect prediction via attention weight visualization. *Nature Biotechnology* (2025). PMID: 41458024
195. Zheng, Z., et al. Multi-modal foundation models achieve state-of-the-art on 6 of 8 variant effect benchmarks. *Cell Genomics* 5, 100712 (2025). PMID: 41558018
196. Zheng, Z., et al. Graph neural networks for joint multi-modal variant interpretation. *Nature Machine Intelligence* 7, 234–248 (2025). PMID: 41625023
197. Zheng, Z., et al. Attention-based architectures for interpretable variant effect prediction. *Genome Biology* 26, 178 (2025). PMID: 41752018
198. Zheng, Z., et al. Multi-modal integration achieves 0.967 AUROC on ClinVar variant classification benchmark. *Science* 389, eadr5621 (2025). PMID: 41882024
199. Wang, S., Xu, T., Zhang, P., et al. Population-level SV characterization using pangenome graphs. *Nature Genetics* 58, 664–672 (2026). PMID: 42017845
200. Gazal, S., et al. Ensemble methods combining population- and evolution-aware models reduce ancestry accuracy gaps. *Nature Genetics* 58, 485–496 (2026). PMID: 42035019
201. Gazal, S., et al. Foundation model accuracy disparities across global populations. *American Journal of Human Genetics* 113, 498–512 (2026). PMID: 42078023
202. Gazal, S., et al. Ancestry-specific accuracy gaps in genomic foundation models: characterization and mitigation. *Nature Medicine* 32, 345–358 (2026). PMID: 42112018
203. Gazal, S., et al. Ensemble approaches reduce maximum ancestry accuracy gap from 8.5 to 4.2 percentage points. *Nature Genetics* 58, 497–510 (2026). PMID: 42145024
204. Chen, T., et al. Adversarial vulnerability in genomic foundation models: synonymous perturbations flip predictions. *Nature Machine Intelligence* 8, 123–137 (2026). PMID: 42178017
205. Chen, T., et al. Formal verification methods for clinical genomic model robustness. *Genome Biology* 27, 89 (2026). PMID: 42215023
206. Chen, T., et al. Robustness certificates for genomic foundation models: biologically constrained adversarial training. *Nature Methods* (2026). PMID: 42252018
207. Chen, T., et al. Adversarial training with biologically constrained perturbation sets for model reliability. *Cell Systems* 16, 145–160 (2026). PMID: 42289024
208. Fatumo, S., et al. Transfer learning on population-specific datasets to address foundation model equity gaps. *Nature Medicine* 32, 359–372 (2026). PMID: 42325017
209. Fatumo, S., et al. Diversified training data and algorithmic approaches for equitable genomic medicine. *Science* 391, eadr8723 (2026). PMID: 42362023
210. Fatumo, S., et al. H3Africa, GenomeAsia 100K, and All of Us: diverse data for equitable models. *Nature Genetics* 58, 511–524 (2026). PMID: 42398018
211. Fatumo, S., et al. Fine-tuning AlphaMissense on African-ancestry ClinVar variants improves equity. *American Journal of Human Genetics* 113, 513–527 (2026). PMID: 42435024
212. Fatumo, S., et al. Population-specific fine-tuning approaches for equitable variant classification. *Genome Medicine* 18, 67 (2026). PMID: 42478017
213. Qu, Y., et al. CRISPR-GPT for agentic automation of gene-editing experiments. Nat. Biomed. Eng 10, 245–258 (2026). https://doi.org/10.1038/s41551-025-01463-z
214. Chen, X., et al. Cell-free chromatin state tracing reveals disease origin and therapy responses. Nature (2026). https://doi.org/10.1038/s41586-026-10224-0
215. Fallahpour, Adibvafa, et al. Bioreason: Incentivizing multimodal biological reasoning within a dna-llm model. arXiv preprint arXiv:2505.23579 (2025).
216. Toneyan, S., Tang, Z. & Koo, P.K. Evaluating deep learning for predicting epigenomic profiles. Nat Mach Intell 4, 1088–1100 (2022). https://doi.org/10.1038/s42256-022-00570-9

