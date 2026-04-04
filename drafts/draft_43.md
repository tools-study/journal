# Genotype-Phenotype Mapping Review

---

## Abstract

The mapping of genotype to phenotype — the central problem of genetics — has been transformed by the convergence of whole-genome sequencing biobanks, single-cell multi-omics, and mathematical population genetics. This review presents a unified quantitative framework for the genotype-phenotype (G2P) map, connecting variant-level molecular effects through gene regulatory network propagation to population-level heritability. We evaluate five interconnected frontiers. First, the resolution of the missing heritability problem: whole-genome sequencing of 490,640 UK Biobank participants has catalogued approximately 1.5 billion variants, and variance-component analyses of whole-genome sequence data demonstrate that common and rare variants together capture approximately 88% of pedigree heritability for 15 of 34 tested traits, effectively resolving the missing heritability for roughly half of studied phenotypes. Second, the transition from association to causation: Bayesian fine-mapping methods now identify causal variants at single-variant resolution for approximately 20–30% of genome-wide association study (GWAS) loci, with cross-ancestry approaches reducing credible set sizes by 40–60%, and massively parallel reporter assays (MPRA) have demonstrated that 9.3% of psychiatric GWAS variants exhibit measurable regulatory activity. Third, the architecture of complex trait polygenicity: the omnigenic model proposes that gene regulatory networks propagate small peripheral gene effects to core disease genes, but the competing stratagenic model offers an alternative information-routing architecture organized by biological strata, and scalable epistasis detection methods now assess over 60 billion SNP pairs at biobank scale. Fourth, clinical translation through polygenic risk scores (PRS), now returned to 25,000 diverse patients in the eMERGE network, alongside pharmacogenomic implementation that reduced adverse drug reactions by 30% in the 6,944-patient PREPARE trial. Fifth, causal inference through Mendelian randomization, which leverages genetic variants as instrumental variables to identify modifiable causes of disease from observational data. Novel mathematical frameworks formalize the quantitative principles governing heritability decomposition through variance components and LD score regression, Bayesian fine-mapping through the Sum of Single Effects model, omnigenic network propagation on gene regulatory graphs, an information bottleneck characterization of the G2P channel, the liability threshold model connecting genetic architecture to clinical prediction, and the multivariate breeder's equation extended to polygenic medicine. Together, these frameworks establish that the G2P map is not a black box but a structured, multi-scale information channel whose capacity, noise characteristics, and bottlenecks can be rigorously quantified — and whose clinical exploitation is now underway.

---

## 1. Introduction: The Architecture of the Genotype-Phenotype Map

### 1.1 The Central Problem: From 4.5 Million Variants to Organismal Phenotype

Every human genome harbors approximately 4–5 million genetic variants relative to any reference sequence, including approximately 3.5 million single-nucleotide polymorphisms (SNPs), 500,000 short insertions and deletions, and tens of thousands of structural variants (The All of Us Research Program Investigators, 2024). Of these, the vast majority are functionally neutral — passengers of demographic history and genetic drift rather than drivers of phenotypic variation. The central challenge of human genetics is to identify which variants matter, through what molecular mechanisms they act, and how their aggregate effects produce the observable traits — from height and blood pressure to disease susceptibility and drug response — that define individual biology.

This problem has proven far more difficult than the completion of the Human Genome Project suggested it would be. The genome is not a simple blueprint in which each gene specifies a trait; rather, it is a regulatory operating system in which the same DNA sequence produces radically different outputs depending on cell type, developmental stage, and environmental context (GTEx Consortium, 2020). The mapping from genotype to phenotype traverses multiple molecular layers — epigenome, transcriptome, proteome, metabolome — each introducing nonlinear transformations, feedback loops, and context dependence that make simple genotype-to-phenotype predictions inadequate for most complex traits (Khodaee et al., 2025).

### 1.2 Three Eras of G2P Mapping

The history of G2P mapping can be organized into three eras defined by the bandwidth of genetic measurement.

**The linkage era (1980–2005)** exploited families segregating for Mendelian diseases to map causal genes through co-inheritance with microsatellite markers. This approach was spectacularly successful for monogenic disorders — identifying the genes for cystic fibrosis, Huntington disease, and over 5,000 Mendelian conditions — but was powerless against complex traits influenced by many variants of small effect, because the statistical power of family-based linkage is insufficient to detect individual loci explaining less than approximately 5% of trait variance (Visscher et al., 2008).

**The GWAS era (2005–2020)** introduced population-based association testing of hundreds of thousands to millions of common SNPs genotyped on microarrays. Genome-wide association studies (GWAS) identified thousands of loci associated with complex traits and diseases, revealing that common diseases have a highly polygenic architecture — thousands of variants each contributing small effects (Manolio et al., 2009). Yet GWAS-identified variants collectively explained only a fraction of the heritability estimated from twin and family studies, creating the "missing heritability" problem that dominated the field for over a decade (Manolio et al., 2009). GWAS also suffered from an inherent limitation: because genotyping arrays capture only common variants (minor allele frequency > 1%), and because linkage disequilibrium (LD) means that associated SNPs are rarely the causal variants themselves, GWAS provided association signals but not causal mechanisms.

**The WGS/multi-omics era (2020–present)** has overcome both limitations. Whole-genome sequencing (WGS) of population-scale biobanks — 490,640 individuals in the UK Biobank (UK Biobank Whole-Genome Sequencing Consortium, 2025) and 245,388 in the All of Us Research Program (The All of Us Research Program Investigators, 2024) — now provides direct measurement of rare variants, structural variants, and noncoding variation invisible to arrays. Simultaneously, single-cell multi-omics technologies link genetic variants to their molecular consequences at cellular resolution, enabling identification of causal mechanisms rather than statistical associations (Fujita et al., 2024). Multimodal computational approaches that jointly model genotype and molecular phenotype spaces are beginning to capture the nonlinear dynamics of the G2P map that linear GWAS could not access (Khodaee et al., 2025).

### 1.3 The G2P Map as an Information-Processing System

We propose that the G2P map is best understood as a multi-scale information channel with defined input (the germline genome), intermediate processing layers (epigenome, transcriptome, proteome, metabolome), and output (the organismal phenotype). At each layer, genetic information is filtered, amplified, transformed, and combined with environmental input, producing progressively emergent properties that cannot be predicted from any single layer in isolation.

This information-processing view leads to three fundamental questions that structure this review:

1. **How much phenotypic information does the genome encode?** This is the heritability question — answered by variance-component methods (Section 2) and now largely resolved by WGS analyses showing that common and rare variants together explain the vast majority of family-based heritability estimates.

2. **Which specific variants carry this information, and through what mechanisms?** This is the fine-mapping and functional genomics question — answered by Bayesian statistical methods and high-throughput experimental validation (Section 3).

3. **How does genetic information propagate through molecular networks to produce complex phenotypes?** This is the genetic architecture question — addressed by the omnigenic model, network propagation theory, and information-theoretic analysis of the G2P channel (Section 4).

The clinical consequence of answering these questions is the capacity to predict individual disease risk from genotype (polygenic risk scores), to identify modifiable causes of disease (Mendelian randomization), and to guide pharmacological treatment based on genetic variation (pharmacogenomics) — the frontier of precision medicine addressed in Section 5.

---

## 2. Heritability Resolved: From Missing to Measured

### 2.1 The Missing Heritability Problem and Its Resolution

The concept of heritability — the proportion of phenotypic variation attributable to genetic variation — has been central to genetics since Fisher's foundational 1918 paper partitioning human stature into genetic and environmental components (Visscher et al., 2008). Twin studies and family-based analyses established high heritabilities for many complex traits: approximately 0.80 for height, 0.40–0.70 for body mass index (BMI), and 0.30–0.80 for most common diseases on the liability scale (Visscher et al., 2008).

The missing heritability problem emerged when the first generation of large-scale GWAS — powered to detect common variants with genome-wide significance (P < 5 × 10⁻⁸) — found that all genome-wide significant loci combined explained only 5–20% of the heritability estimated from twin studies (Manolio et al., 2009). For height, one of the best-studied traits, 180 significant loci from early GWAS explained only approximately 10% of the 80% heritability, leaving approximately 70% of the genetic contribution unaccounted for (Manolio et al., 2009).

Three hypotheses were advanced to explain the gap: (a) many common variants of very small effect below the GWAS significance threshold; (b) rare variants of moderate to large effect not captured by genotyping arrays; and (c) non-additive effects (epistasis, gene-environment interactions) not modeled by standard GWAS.

The resolution came from two converging advances. First, Yang and colleagues demonstrated that all common SNPs on a genotyping array — not just genome-wide significant ones — collectively explain a substantial fraction of heritability when their joint effect is estimated through a genomic restricted maximum likelihood (GREML) variance-component model (Yang et al., 2010). This "SNP-heritability" (h²_SNP) estimate showed that common variants explain approximately 45% of height heritability and 20–40% for most other complex traits — far more than significant loci alone, but still less than family-based estimates. Second, whole-genome sequencing eliminated the ascertainment bias of genotyping arrays, providing direct measurement of rare variants. Young and colleagues, using WGS data from large cohorts, demonstrated that when all variants — common, low-frequency, rare, and structural — are included in the variance-component model, the estimated heritability approaches family-based estimates, with WGS capturing approximately 88% of pedigree heritability across 15 of 34 tested traits (Young et al., 2025). For some traits, the missing heritability was effectively zero.

The most decisive evidence came from the saturated genetic map of human height. The GIANT consortium meta-analysis of approximately 5 million individuals identified roughly 12,000 independent height-associated variants that collectively explain virtually all common-SNP heritability (Yengo et al., 2022). This landmark result demonstrated that height — the paradigmatic complex trait — has a fully polygenic architecture in which thousands of variants of individually small effect sum to produce the observed heritability, and that the "missing" heritability was simply the statistical power gap between detecting variants individually versus estimating their joint contribution.

### 2.2 SNP-Heritability Estimation: GREML and LDSC

Two complementary methods have become the workhorses of heritability estimation in the genomic era.

**Genomic REML (GREML).** Introduced by Yang and colleagues (2010), GREML estimates the proportion of phenotypic variance explained by all genotyped SNPs simultaneously, without requiring individual SNPs to reach genome-wide significance. The method constructs a genetic relationship matrix (GRM) from genome-wide SNP data and fits a linear mixed model in which the phenotypic covariance between individuals is modeled as a function of their genetic similarity. The key insight is that even distant relatives share enough genetic variants to generate estimable genetic covariance, and the aggregate of these small covariances across hundreds of thousands of unrelated individuals provides a precise estimate of h²_SNP (Yang et al., 2010).

**LD Score Regression (LDSC).** Developed by Bulik-Sullivan and colleagues (2015), LDSC exploits the relationship between GWAS test statistics and linkage disequilibrium to estimate heritability from summary statistics alone, without requiring individual-level genotype data. The central insight is that under a polygenic model, the expected chi-squared statistic at a given SNP scales linearly with its LD score — the sum of squared correlations with all neighboring SNPs — because SNPs in high LD with many other variants tag more of the total causal variation. Confounding from population stratification, by contrast, inflates all test statistics uniformly regardless of LD score. The slope of the regression of chi-squared statistics on LD scores thus estimates per-SNP heritability, while the intercept captures confounding (Bulik-Sullivan et al., 2015).

LDSC has been extended to bivariate genetic correlation (estimating the shared genetic basis between two traits from their cross-trait LD score regression) and to partitioned heritability by functional annotation.

### 2.3 WGS Closes the Gap: Rare Variants and Structural Variants

The UK Biobank Whole-Genome Sequencing Consortium released WGS data for 490,640 participants in 2025, cataloguing approximately 1.5 billion genetic variants including 919 million SNPs, 135 million indels, and 16 million structural variants (UK Biobank Whole-Genome Sequencing Consortium, 2025). This resource — the largest population-scale WGS dataset — provides three critical advances over array-based genotyping.

First, direct ascertainment of rare variants (minor allele frequency < 0.01) eliminates the imputation errors that degraded rare variant association testing from array data. Rare coding variants of moderate effect have now been identified for hundreds of complex traits, partially explaining the gap between common-SNP heritability and family-based estimates (UK Biobank Whole-Genome Sequencing Consortium, 2025).

Second, structural variants — insertions, deletions, duplications, inversions, and complex rearrangements — account for approximately 80% of variant base pairs between individuals but were largely invisible to short-read sequencing and genotyping arrays. WGS-based structural variant discovery has revealed thousands of associations with complex traits that were missed by array-based GWAS (UK Biobank Whole-Genome Sequencing Consortium, 2025).

Third, the All of Us Research Program, with 245,388 WGS participants of whom 77% are from underrepresented populations, provides cross-ancestry variant discovery and heritability estimation that addresses the European ancestry bias of prior GWAS (The All of Us Research Program Investigators, 2024). Over one billion variants were identified, with more than 275 million previously unreported, demonstrating that population diversity substantially expands the known landscape of human genetic variation (The All of Us Research Program Investigators, 2024).

### 2.4 Partitioned Heritability by Functional Annotation

Not all genomic regions contribute equally to heritability. Finucane and colleagues developed stratified LD score regression (LDSC-SEG), which partitions heritability by overlapping functional annotation categories — coding regions, UTRs, promoters, enhancers, histone modification marks, and transcription factor binding sites (Finucane et al., 2015). The key finding is that functional categories enriched in regulatory elements contain a disproportionate share of heritability: regions marked by H3K4me1 (an enhancer-associated histone modification) contain approximately 1% of common SNPs but explain 10–20% of heritability for many immune and metabolic traits, representing 10–20-fold enrichment (Finucane et al., 2015).

This functional partitioning has two major implications. First, it demonstrates that the causal variants underlying complex trait heritability are overwhelmingly regulatory rather than coding — consistent with the observation that over 90% of GWAS-identified variants fall in noncoding regions. Second, it provides a prior for fine-mapping: variants in enriched functional categories can be up-weighted in Bayesian fine-mapping models, improving causal variant identification (Finucane et al., 2015).

The GTEx Consortium atlas of genetic regulatory effects across 49 human tissues further refines this picture, demonstrating that nearly all protein-coding genes have at least one expression quantitative trait locus (eQTL) in at least one tissue, and that the tissue-specificity of eQTLs provides mechanistic links between GWAS associations and disease biology (GTEx Consortium, 2020). Integration of eQTL data with GWAS through colocalization methods identifies the specific genes and tissues through which noncoding variants act, bridging the gap between statistical association and biological mechanism.

### 2.5 Framework F312: Heritability Decomposition via Variance Components and LD Score Regression

The quantitative framework for heritability estimation unifies GREML and LDSC under a common variance-component model. The phenotype $y_i$ for individual $i$ is modeled as:

```math
y_i = \mathbf{x}_i^T \boldsymbol{\beta}_{\text{cov}} + g_i + \varepsilon_i
```

where $\mathbf{x}_i^T \boldsymbol{\beta}_{\text{cov}}$ represents fixed covariate effects (age, sex, principal components of ancestry), $g_i$ is the total genetic effect, and $\varepsilon_i \sim \mathcal{N}(0, \sigma_e^2)$ is the residual. The genetic effect is partitioned into $C$ components:

```math
g_i = \sum_{c=1}^{C} g_{i,c}, \quad g_{i,c} = \sum_{j \in S_c} x_{ij} \beta_j
```

where $S_c$ is the set of variants in component $c$ (e.g., stratified by minor allele frequency bins and LD score quantiles) and $\beta_j$ are variant effects. Under the infinitesimal prior $\beta_j \sim \mathcal{N}(0, \sigma_c^2 / M_c)$ where $M_c = |S_c|$, the phenotypic variance decomposes as:

```math
\sigma_P^2 = \sum_{c=1}^{C} \sigma_c^2 + \sigma_e^2
```

and the total SNP-heritability is:

```math
h^2_{\text{SNP}} = \frac{\sum_{c=1}^{C} \sigma_c^2}{\sigma_P^2}
```

The variance components $\sigma_c^2$ are estimated by restricted maximum likelihood (REML), which maximizes the likelihood of the phenotypic data given the genetic relationship matrices $\mathbf{K}_c$ for each component, where $[\mathbf{K}_c]_{ij} = \frac{1}{M_c} \sum_{k \in S_c} \tilde{x}_{ik} \tilde{x}_{jk}$ and $\tilde{x}$ denotes standardized genotypes (Yang et al., 2010).

For LD score regression, the connection to variance components is through the expected GWAS test statistic. Under polygenicity, the expected chi-squared statistic at SNP $j$ is:

```math
\mathbb{E}[\chi_j^2] = \frac{N \cdot h^2_{\text{SNP}}}{M} \cdot \ell_j + N \cdot a + 1
```

where $N$ is the sample size, $M$ is the total number of SNPs, $\ell_j = \sum_k r_{jk}^2$ is the LD score of SNP $j$ (the sum of squared correlations with all other SNPs), and $a$ captures confounding inflation from population stratification or cryptic relatedness (Bulik-Sullivan et al., 2015). The slope of $\chi^2$ regressed on $\ell$ estimates $h^2_{\text{SNP}} / M$ (per-SNP heritability), while the intercept $1 + Na$ separates genuine polygenic signal from confounding. This regression can be performed using only summary statistics, enabling heritability meta-analysis across studies without sharing individual-level data.

The framework extends to stratified partitioning via:

```math
\mathbb{E}[\chi_j^2] = N \sum_{c=1}^{C} \tau_c \cdot \ell_{j,c} + N \cdot a + 1
```

where $\tau_c = h^2_c / M_c$ is the per-SNP heritability contribution of category $c$ and $\ell_{j,c} = \sum_{k \in S_c} r_{jk}^2$ is the partitioned LD score (Finucane et al., 2015). The enrichment of category $c$ is $E_c = (h^2_c / h^2_{\text{total}}) / (M_c / M)$, and categories with $E_c \gg 1$ (such as conserved coding regions, $E_c \approx 40$, or H3K4me1 enhancer marks, $E_c \approx 10$–$20$) are disproportionately enriched for causal variants.

The critical result from WGS heritability analyses: when variance components are estimated from whole-genome sequence data stratified by MAF and LD into approximately 8–16 bins, the ratio $h^2_{\text{WGS}} / h^2_{\text{pedigree}}$ reaches approximately 0.88 for height and BMI and exceeds 0.80 for 15 of 34 traits tested, demonstrating that the gap between SNP-heritability and pedigree heritability is explained by rare variants and structural variants invisible to genotyping arrays (Young et al., 2025).

---

## 3. From Association to Causation: Fine-Mapping and Functional Validation

### 3.1 The Fine-Mapping Problem: LD Confounds Causal Inference

GWAS identify genomic loci — chromosomal regions spanning tens to hundreds of kilobases — associated with traits, but the associated lead SNP is rarely the causal variant. Because of linkage disequilibrium, tens to hundreds of variants within each locus are correlated with the lead SNP and show comparable association statistics, making it impossible to distinguish causal from correlated variants on statistical grounds alone from a single-ancestry GWAS (Benner et al., 2016).

Fine-mapping refers to the set of statistical and experimental methods that narrow each GWAS locus from a broad association signal to a specific set of likely causal variants. Statistical fine-mapping methods assign posterior inclusion probabilities (PIPs) to individual variants based on LD structure, effect sizes, and prior functional annotations. Experimental methods — massively parallel reporter assays (MPRA), CRISPR interference (CRISPRi), and deep mutational scanning — directly test the functional consequences of individual variants.

### 3.2 Statistical Fine-Mapping: SuSiE and Multi-Ancestry Approaches

The Sum of Single Effects (SuSiE) model, introduced by Wang and colleagues (2020), has become the dominant Bayesian fine-mapping method. SuSiE's key innovation is decomposing the multi-causal-variant signal at a locus into a sum of "single effect" vectors, each representing exactly one causal variant, enabling tractable posterior computation even with highly correlated variants (Wang et al., 2020).

For a locus with $p$ variants and $n$ individuals, SuSiE models the phenotype as $\mathbf{y} = \mathbf{X}\mathbf{b} + \boldsymbol{\varepsilon}$, where the effect vector is decomposed as $\mathbf{b} = \sum_{l=1}^{L} \mathbf{b}_l$, with each layer $\mathbf{b}_l$ containing exactly one nonzero element corresponding to a single causal variant. The posterior inclusion probability for variant $j$ in layer $l$ is computed via iterative Bayesian single-effect regression, and the overall PIP — the probability that variant $j$ is causal in at least one layer — provides a ranking of candidate causal variants.

Cross-ancestry fine-mapping exploits the fact that LD patterns differ between populations while causal variants are typically shared. By integrating GWAS data from multiple ancestry groups, methods such as SuSiEx reduce credible set sizes by 40–60% compared to single-ancestry fine-mapping, because variants that are in LD in one population may be independent in another, enabling sharper resolution of the causal signal (Yuan et al., 2024). The increasing diversity of WGS biobanks — particularly All of Us with 77% non-European ancestry — provides the multi-ancestry data essential for this approach (The All of Us Research Program Investigators, 2024).

The FINEMAP algorithm, based on shotgun stochastic search, provides an alternative to SuSiE's variational approach, achieving accurate credible set construction using GWAS summary statistics with computational efficiency sufficient for genome-wide application (Benner et al., 2016).

### 3.3 Functional Validation at Scale: MPRA and CRISPRi

Statistical fine-mapping produces probability estimates, not definitive causal assignments. Experimental validation is required to confirm that fine-mapped variants have functional consequences.

Massively parallel reporter assays (MPRA) test thousands of variant-containing sequences in a single experiment by cloning them upstream of a minimal promoter and barcode, transfecting the library into relevant cell types, and measuring barcode expression as a readout of regulatory activity (Tewhey et al., 2016). Tewhey and colleagues demonstrated the power of this approach by testing 32,373 eQTL variants, identifying 842 with significant allelic effects on expression (Tewhey et al., 2016). More recently, Lee and colleagues applied MPRA across eight psychiatric disorders, testing tens of thousands of GWAS variants and finding that 9.3% exhibited measurable regulatory activity — providing the first quantitative estimate of the functional fraction of psychiatric GWAS signals and distinguishing pleiotropic variants active across multiple disorders from disorder-specific regulatory variants (Lee et al., 2025).

CRISPRi and CRISPRa perturbation experiments provide complementary evidence at endogenous genomic loci, testing whether disruption or activation of a candidate regulatory element affects target gene expression in its native chromatin context. The combination of statistical fine-mapping, MPRA, and CRISPRi now provides a complete pipeline from GWAS association to validated causal variant and target gene — a pipeline that has been applied at scale to cardiovascular, immune, and neuropsychiatric diseases.

Deep mutational scanning (DMS) provides exhaustive variant-function maps for protein-coding regions. The TP53 deep CRISPR mutagenesis study mapped the functional consequences of 9,225 variants — 94.5% of all possible missense mutations — in the tumor suppressor p53, providing a near-complete map of variant effects on p53 function (Funk et al., 2025). MaveDB, the community repository for multiplexed assays of variant effect, now contains over 7 million variant effect measurements across hundreds of genes, providing experimental ground truth for computational variant effect prediction (Rubin et al., 2025).

### 3.4 Sequence-to-Function Models for Variant Interpretation

Computational models that predict variant effects directly from DNA sequence provide a scalable complement to experimental approaches. Borzoi, the successor to Enformer, processes 524,288 base pairs of context to predict RNA-seq coverage across tissues, capturing variant effects on transcription, splicing, and polyadenylation simultaneously (Linder et al., 2025). The TraitGym benchmark systematically evaluates these models, revealing that GPN-MSA performs best for Mendelian disease variants while Borzoi and Enformer excel for complex non-disease traits, suggesting that different genetic architectures favor different modeling approaches (Sartorelli et al., 2025). AlphaMissense, the proteome-wide missense variant classifier, has been formally calibrated to ClinGen evidence standards and is now recommended for clinical variant classification alongside REVEL (Pejaver et al., 2025). The Nucleotide Transformer, trained on 3,202 human genomes, provides an alternative foundation model approach with strong cross-species generalization (Dalla-Torre et al., 2024).

These computational tools serve a specific role in the fine-mapping pipeline: they provide mechanistic hypotheses for how fine-mapped variants alter molecular function, enabling prioritization of experimental validation and accelerating the translation from statistical association to biological understanding.

### 3.5 Framework F313: Bayesian Fine-Mapping via the Sum of Single Effects (SuSiE) Model

The SuSiE framework formalizes fine-mapping as a structured Bayesian regression problem. For a locus with $p$ variants genotyped in $n$ individuals, the phenotype vector $\mathbf{y}$ is modeled as:

```math
\mathbf{y} = \mathbf{X}\mathbf{b} + \boldsymbol{\varepsilon}, \quad \boldsymbol{\varepsilon} \sim \mathcal{N}(\mathbf{0}, \sigma^2 \mathbf{I})
```

where $\mathbf{X}$ is the $n \times p$ genotype matrix and the effect vector decomposes as:

```math
\mathbf{b} = \sum_{l=1}^{L} \mathbf{b}_l
```

Each "single effect" vector $\mathbf{b}_l$ has exactly one nonzero element, modeled as:

```math
\mathbf{b}_l = \gamma_l \cdot \beta_l, \quad \gamma_l \sim \text{Multinomial}(1, \boldsymbol{\pi}), \quad \beta_l \sim \mathcal{N}(0, \sigma_l^2)
```

where $\gamma_l \in \{0,1\}^p$ is a one-hot indicator specifying which variant is causal in layer $l$, $\boldsymbol{\pi} = (\pi_1, \ldots, \pi_p)$ are prior inclusion probabilities (which can incorporate functional annotation priors from LDSC-SEG), and $\sigma_l^2$ is the prior effect size variance for layer $l$ (Wang et al., 2020).

The posterior inclusion probability for variant $j$ in layer $l$, denoted $\alpha_{l,j} = P(\gamma_{l,j} = 1 \mid \mathbf{y}, \mathbf{X})$, is computed by the Iterative Bayesian Stepwise Selection (IBSS) algorithm, which iteratively fits single-effect regressions while conditioning on the current estimates of all other layers. The overall posterior inclusion probability for variant $j$ — the probability that it is causal in at least one layer — is:

```math
\text{PIP}_j = 1 - \prod_{l=1}^{L} (1 - \alpha_{l,j})
```

The 95% credible set for layer $l$ is the smallest set $\mathcal{S}_l \subseteq \{1, \ldots, p\}$ such that:

```math
\sum_{j \in \mathcal{S}_l} \alpha_{l,j} \geq 0.95
```

ordered by decreasing $\alpha_{l,j}$. Each credible set contains one causal variant with at least 95% posterior probability, providing calibrated uncertainty quantification.

The cross-ancestry extension follows naturally: when GWAS data are available from $K$ ancestry groups with distinct LD matrices $\mathbf{R}^{(1)}, \ldots, \mathbf{R}^{(K)}$ but shared causal variants, the joint likelihood uses ancestry-specific LD structures while enforcing a common $\gamma_l$ across populations. Because variants in LD in one ancestry may be independent in another, the joint posterior concentrates on the true causal variant — explaining the 40–60% credible set size reduction observed in cross-ancestry fine-mapping relative to single-ancestry analysis (Yuan et al., 2024). The mathematical mechanism is that the effective number of independent parameters (the degrees of freedom in the posterior) is reduced when LD patterns provide orthogonal constraints on the same underlying causal configuration.

---

## 4. Network Architecture: Omnigenic, Stratagenic, and the Propagation Question

### 4.1 The Omnigenic Model: Core Genes and Peripheral Effects

The extreme polygenicity of complex traits — with hundreds to thousands of associated loci spread across the genome — demands an explanatory framework beyond the classical view that disease-associated variants cluster in disease-relevant pathways. Boyle, Li, and Pritchard (2017) proposed the omnigenic model, which argues that gene regulatory networks are so densely interconnected that virtually every gene expressed in a disease-relevant cell type can influence disease risk through trans-regulatory propagation to a small set of "core" disease genes (Boyle et al., 2017).

The omnigenic model distinguishes two classes of genes. **Core genes** are those whose products directly affect the phenotype — for example, genes encoding ion channels in cardiac arrhythmia or immune receptors in autoimmune disease. **Peripheral genes** are all other expressed genes, which affect the phenotype indirectly by modulating the expression or function of core genes through shared regulatory networks. Because gene regulatory networks are scale-free and exhibit small-world properties, the number of "hops" between any two expressed genes is small (typically 2–4 in protein-protein interaction networks), and even distant peripheral genes can influence core gene expression through chains of trans-regulatory effects (Boyle et al., 2017).

The key prediction of the omnigenic model is that the heritability of complex traits should be broadly distributed across the genome rather than concentrated in disease-relevant pathways — a prediction strongly supported by partitioned heritability analyses showing that heritability enrichment in disease-specific gene sets, while statistically significant, accounts for only a modest fraction of total heritability (Finucane et al., 2015).

Liu, Li, and Pritchard (2019) provided empirical support for the omnigenic model by analyzing trans-eQTL effects — genetic variants that affect the expression of distant genes. They demonstrated that peripheral genes act as weak but numerous trans-regulators of core genes, and that the co-regulation of core genes by shared peripheral regulatory networks amplifies the aggregate peripheral contribution to phenotypic variance beyond what any individual peripheral gene would suggest (Liu et al., 2019).

### 4.2 From Omnigenic to Stratagenic: Competing Network Architectures

The omnigenic model has generated significant debate. Wray, Wijmenga, Sullivan, Yang, and Visscher (2018) argued that the core/peripheral gene distinction oversimplifies the biology of complex disease, noting that multiple backup mechanisms and pathway redundancy may explain polygenicity without requiring the extreme network interconnectedness that the omnigenic model posits (Wray et al., 2018). They proposed that "omnigenic" may simply be a consequence of shared developmental programs and that disease-relevant biology may still be concentrated in identifiable pathways, even if the statistical signal appears broadly distributed.

A more recent alternative is the stratagenic model proposed by Garcia-Gonzalez and O'Reilly (2026), which argues that genetic architecture is organized not by the core/peripheral distinction but by biological strata — distinct layers of biological organization including chromatin regulation, transcriptional control, signal transduction, and metabolic processing (Garcia-Gonzalez & O'Reilly, 2026). In the stratagenic view, genetic effects propagate through specific strata rather than broadcasting omnidirectionally across the full gene regulatory network, and the architecture of effect propagation depends on which stratum the causal variant operates in. This model makes distinct predictions about the functional categories in which heritability concentrates and offers a framework for designing stratum-specific interventions.

The resolution between omnigenic and stratagenic architectures has direct implications for precision medicine: if the omnigenic model is correct, then improving phenotype prediction requires modeling the entire expressed genome; if the stratagenic model holds, then identifying the relevant stratum and its core regulatory features may be sufficient.

### 4.3 Gene Regulatory Networks as Signal Propagation Media

The molecular infrastructure through which genetic effects propagate consists of gene regulatory networks — directed graphs in which nodes represent genes and edges represent regulatory interactions (activating or repressing). The topology of these networks determines how perturbations (genetic variants affecting one node) propagate to affect other nodes and ultimately the phenotype.

Single-cell eQTL studies have begun to resolve this propagation at cellular resolution. Fujita and colleagues analyzed 1.5 million single nuclei from 424 donors across 64 brain cell subtypes, revealing that the majority of eQTLs are cell-type-specific — active in only one or a few cell types — and that the cell-type-specificity of eQTLs provides mechanistic links between GWAS loci and neurodegeneration (Fujita et al., 2024). This finding implies that the G2P map is not a single network but a collection of cell-type-specific networks, each mediating a different subset of genetic effects.

Multimodal computational approaches are beginning to capture these nonlinear, cell-type-specific propagation dynamics. Khodaee, Zandie, and Edelman (2025) developed a Computational Integrated Genetics (CIG) multimodal foundation model that jointly embeds genotype and phenotype spaces using transformer-based architecture trained on the CellxGene platform encompassing over 65 million human cells. By treating gene expression profiles as "sentences" with gene tokens and using contrastive learning to align genotype-phenotype manifolds at single-cell resolution, the CIG model captures context-dependent gene function — the same gene producing different phenotypic effects in different cellular contexts — and discovers cross-tissue biomarkers invisible to single-modality analyses (Khodaee et al., 2025). This approach demonstrates that nonlinear multimodal integration can access G2P dynamics that linear GWAS cannot capture, providing computational evidence for the network-mediated signal propagation posited by the omnigenic model.

### 4.4 Epistasis at Scale: Detection and Biological Architecture

Epistasis — the nonlinear interaction between genetic variants — represents an additional layer of G2P complexity beyond additive models. Classical quantitative genetics demonstrated that epistatic variance contributes to broad-sense but not narrow-sense heritability, and population-level evidence suggests that additive effects dominate heritability under most conditions (Barton et al., 2017). However, the biological importance of epistasis may exceed its statistical contribution to population variance, because epistatic interactions constrain the space of viable genotypes and shape the evolutionary landscape of adaptation.

Detecting epistasis at biobank scale has been limited by the computational burden of testing all pairwise SNP combinations — over 60 billion pairs for a typical GWAS. Stamp and colleagues developed Scalable Marginal Epistasis (SME), which achieves 10–90-fold faster epistasis detection by restricting analysis to functionally enriched genomic regions identified from marginal effect enrichment patterns across 349,411 UK Biobank individuals (Stamp et al., 2025). Their analyses identified significant epistatic interactions for multiple complex traits, though the variance explained by detected epistasis remains modest (typically < 1% of phenotypic variance), consistent with the theoretical prediction that most epistatic variance is converted to additive variance at intermediate allele frequencies in large, randomly mating populations (Barton et al., 2017).

### 4.5 Framework F314: Omnigenic Network Propagation Model

The omnigenic model can be formalized as a linear propagation process on a gene regulatory network. Consider a network with $n$ expressed genes represented as a directed weighted graph $G = (V, E)$. Each gene $i$ has a cis-genetic effect $a_i$ — the direct effect of local regulatory variants on gene $i$'s expression — and a total genetic effect $b_i$ that includes both cis and trans components:

```math
b_i = a_i + \sum_{j \neq i} W_{ij} b_j
```

where $W_{ij}$ is the trans-regulatory effect of gene $j$ on gene $i$ (the edge weight in the regulatory network). In matrix form:

```math
\mathbf{b} = \mathbf{a} + \mathbf{W}\mathbf{b} \implies \mathbf{b} = (\mathbf{I} - \mathbf{W})^{-1} \mathbf{a}
```

This is the network propagation equation, valid when the spectral radius $\rho(\mathbf{W}) < 1$ (ensuring convergence). The matrix $\mathbf{G}_{\text{prop}} = (\mathbf{I} - \mathbf{W})^{-1}$ is the propagation kernel: entry $[\mathbf{G}_{\text{prop}}]_{ij}$ quantifies the total effect of a cis-perturbation at gene $j$ on the expression of gene $i$, summing over all direct and indirect regulatory paths.

The trait value for individual $k$ with genetic effects $\mathbf{b}^{(k)}$ is:

```math
y_k = \mathbf{c}^T \mathbf{b}^{(k)} + \varepsilon_k = \mathbf{c}^T (\mathbf{I} - \mathbf{W})^{-1} \mathbf{a}^{(k)} + \varepsilon_k
```

where $\mathbf{c}$ is the vector of core gene effect sizes, with $c_i \neq 0$ only for core genes that directly influence the phenotype. The effective weight of each gene on the trait is $\mathbf{w}_{\text{eff}} = (\mathbf{I} - \mathbf{W})^{-T} \mathbf{c}$, and the number of genes with non-negligible effective weight — the "effective polygenicity" — depends on the spectral properties of $\mathbf{W}$.

The heritability decomposes into cis and trans components:

```math
h^2_{\text{cis}} = \frac{\text{Var}(\mathbf{c}^T \mathbf{a})}{\sigma_P^2}, \quad h^2_{\text{trans}} = \frac{\text{Var}(\mathbf{c}^T [(\mathbf{I} - \mathbf{W})^{-1} - \mathbf{I}] \mathbf{a})}{\sigma_P^2}
```

The omnigenic prediction is that $h^2_{\text{trans}} \gg h^2_{\text{cis}}$ when $\rho(\mathbf{W})$ approaches 1 — that is, when the regulatory network is near its stability boundary, small cis-effects at peripheral genes propagate and amplify through network paths to produce large aggregate trans-effects on core genes (Liu et al., 2019). Empirical estimates from trans-eQTL data suggest $h^2_{\text{trans}} / h^2_{\text{cis}} \approx 3$–$5$ for most complex traits, consistent with the omnigenic regime (Liu et al., 2019).

The number of effectively contributing genes scales as:

```math
n_{\text{eff}} = \| \mathbf{w}_{\text{eff}} \|_0 \approx \frac{\| \mathbf{w}_{\text{eff}} \|_1^2}{\| \mathbf{w}_{\text{eff}} \|_2^2}
```

(the inverse participation ratio). When $\rho(\mathbf{W}) \to 1$, $n_{\text{eff}} \to n$ (all genes contribute), recovering the omnigenic limit. When $\rho(\mathbf{W})$ is small, $n_{\text{eff}}$ approaches the number of core genes, recovering the pathway-centric model. The stratagenic model corresponds to a block-structured $\mathbf{W}$ with strong within-stratum and weak between-stratum connectivity, producing intermediate $n_{\text{eff}}$ values organized by biological layer (Garcia-Gonzalez & O'Reilly, 2026).

### 4.6 Framework F315: Information Bottleneck for the G2P Channel

The G2P map can be characterized as a Markov chain:

```math
G \to M \to P
```

where $G$ denotes the genotype, $M$ the molecular intermediate (transcriptome, proteome, or a multi-omic embedding), and $P$ the phenotype. The Data Processing Inequality guarantees:

```math
I(G; P) \leq \min\{I(G; M), \, I(M; P)\}
```

where $I(\cdot; \cdot)$ denotes mutual information. This inequality establishes that the molecular intermediate is a bottleneck: no downstream phenotype can carry more information about the genotype than the intermediate molecular layer transmits.

The information bottleneck framework asks: what is the minimal-complexity representation $Z$ of the molecular intermediate $M$ that preserves maximal information about the phenotype $P$? Formally:

```math
\min_{p(Z|M)} \left[ I(M; Z) - \beta \cdot I(Z; P) \right]
```

where $\beta > 0$ is a Lagrange multiplier controlling the tradeoff between compression ($I(M;Z)$ small) and prediction ($I(Z;P)$ large). At low $\beta$, the optimal $Z$ compresses aggressively, retaining only the most informative molecular features — recovering a minimal set that functions analogously to the "core genes" of the omnigenic model. At high $\beta$, $Z$ retains all molecular information, corresponding to the full omnigenic regime where every expressed gene matters.

The G2P mutual information $I(G;P)$ can be estimated from GWAS data. For a quantitative trait with heritability $h^2$ and $M$ independent causal variants each with small effect:

```math
I(G; P) \approx -\frac{1}{2} \log_2(1 - h^2)
```

For height ($h^2 \approx 0.80$), this yields $I(G;P) \approx 1.16$ bits per individual phenotype measurement. For schizophrenia on the liability scale ($h^2_L \approx 0.80$), the same calculation applies to the underlying liability, but the observable binary phenotype (affected/unaffected) carries less information due to thresholding.

The optimal transition point $\beta^*$ — where the rate-distortion curve exhibits a phase transition — identifies the minimal number of molecular features required to explain the observed G2P information transfer. This provides a principled, information-theoretic answer to the question "how many genes matter for a given trait?" that complements the statistical approach of counting genome-wide significant loci or the network-theoretic approach of computing $n_{\text{eff}}$ from the propagation kernel.

For multimodal approaches such as the CIG model of Khodaee et al. (2025), the information bottleneck framework predicts that jointly modeling genotype and molecular intermediates should achieve higher $I(Z;P)$ at lower $I(M;Z)$ — that is, the multimodal representation should extract more phenotypic information per unit of representational complexity than either modality alone, consistent with the empirical finding that multimodal G2P models outperform genotype-only polygenic scores (Khodaee et al., 2025).

---

## 5. Clinical Translation: Polygenic Scores, Pharmacogenomics, and Causal Inference

### 5.1 Polygenic Risk Scores: Construction and Clinical Deployment

Polygenic risk scores (PRS) aggregate the effects of thousands to millions of genetic variants into a single numerical predictor of disease risk or trait value. For individual $k$ with genotype vector $\mathbf{x}^{(k)}$, the PRS is:

```math
\text{PRS}_k = \sum_{j=1}^{M} \hat{\beta}_j \cdot x_{j}^{(k)}
```

where $\hat{\beta}_j$ are variant weight estimates derived from GWAS summary statistics. The accuracy of PRS depends critically on the method used to estimate these weights, because the raw GWAS effect sizes are biased by LD-induced correlation between variants.

Three Bayesian methods have emerged as standards for PRS weight estimation. LDpred, the first to explicitly model LD structure, uses a point-normal prior on effect sizes and Gibbs sampling for posterior computation (Vilhjalmsson et al., 2015). LDpred2 improved upon this with sparse and auto-tuning modes that are robust across genetic architectures and computationally efficient for biobank-scale data (Prive et al., 2021). PRS-CS employs a continuous-shrinkage prior (the Strawderman-Berger prior) that adapts the degree of shrinkage to the local LD and polygenicity structure, achieving consistently strong performance across traits without requiring tuning of the polygenicity parameter (Ge et al., 2019).

Despite methodological advances, current PRS explain only a fraction of genetic variance — typically $R^2$ of 5–15% for most common diseases — far below the theoretical ceiling of $h^2_{\text{SNP}}$ (Khera et al., 2018). This gap reflects limited training sample sizes, incomplete variant ascertainment, and the difficulty of capturing nonlinear G2P dynamics in a linear score. Nevertheless, PRS have demonstrated clinical relevance: Khera and colleagues showed that genome-wide PRS can identify 1.5–8% of the population at greater than 3-fold disease risk for coronary artery disease, atrial fibrillation, type 2 diabetes, inflammatory bowel disease, and breast cancer — risk levels previously associated only with rare monogenic mutations (Khera et al., 2018).

### 5.2 Cross-Ancestry Portability and the Equity Challenge

A critical limitation of current PRS is their reduced accuracy in non-European populations. PRS developed from European-ancestry GWAS lose 30–80% of their predictive accuracy when applied to individuals of African, East Asian, or South Asian ancestry (Martin et al., 2019). This portability gap arises from three sources: (a) differences in LD structure that misalign variant weights with causal variants in different populations; (b) differences in allele frequencies that alter the variance explained by specific variants; and (c) training set bias, as approximately 80% of all GWAS participants have been of European ancestry (Martin et al., 2019).

Addressing this inequity is essential for preventing PRS from exacerbating existing health disparities. Multi-ancestry PRS methods such as BridgePRS use Bayesian bridging across ancestry groups, leveraging shared causal variants while accommodating ancestry-specific LD patterns to improve prediction in underrepresented populations. The All of Us Research Program, with 77% of participants from underrepresented populations, directly addresses the training data gap (The All of Us Research Program Investigators, 2024). The Pan-UK Biobank initiative has performed multi-ancestry GWAS and meta-analysis across genetic ancestry groups for 7,266 traits, with a quality control framework informed by genetic architecture to enhance discovery of ancestry-enriched loci (Pan-UK Biobank Team, 2025).

### 5.3 The eMERGE Trial: First Clinical PRS Return at Scale

The eMERGE (Electronic Medical Records and Genomics) Phase III network represents the first large-scale clinical implementation of PRS, returning polygenic risk information for 10 conditions to approximately 25,000 diverse participants across multiple clinical sites (Lennon et al., 2024). The 10 conditions — including coronary artery disease, type 2 diabetes, atrial fibrillation, breast cancer, colorectal cancer, and others — were selected based on PRS clinical validity, disease burden, and actionability of risk information (Lennon et al., 2024).

The eMERGE experience revealed both the promise and challenges of clinical PRS implementation: participants at high polygenic risk were more likely to have prevalent disease and relevant risk factors, validating the clinical signal, but the interpretation and clinical management of intermediate-risk PRS results remain uncertain, and the infrastructure for returning genomic risk information through electronic health records requires substantial development (Lennon et al., 2024). Recent European Society of Cardiology consensus statements have begun to formalize clinical guidelines for PRS use in cardiovascular risk prediction, marking the transition from research to clinical practice (Schunkert et al., 2025).

### 5.4 Pharmacogenomic Translation: The PREPARE Trial

Pharmacogenomics — the use of genetic variation to guide drug selection and dosing — represents the most mature clinical application of G2P mapping. Over 95% of the population carries at least one actionable pharmacogenomic variant, and the Clinical Pharmacogenetics Implementation Consortium (CPIC) now provides evidence-based guidelines for 34 genes affecting the metabolism or response to 164 drugs.

The PREPARE (PREemptive Pharmacogenomic testing for Preventing Adverse drug REactions) trial provided the definitive randomized evidence for clinical pharmacogenomics. In this multicenter, open-label, crossover trial conducted across seven European countries, 6,944 patients were randomized to pre-emptive pharmacogenomic testing with a 12-gene panel versus standard of care. The pharmacogenomic-guided group experienced a 30% reduction in clinically relevant adverse drug reactions (odds ratio 0.70, 95% CI 0.54–0.91), with the greatest benefit observed for drugs metabolized by CYP2D6 and CYP2C19 (Swen et al., 2023). This result establishes that proactive genotype-guided prescribing improves patient outcomes in routine clinical practice.

### 5.5 Mendelian Randomization: Causal Inference from Observational Genetics

Mendelian randomization (MR) exploits the random allocation of alleles at conception — Mendel's second law — to use genetic variants as instrumental variables for estimating causal effects of modifiable exposures on disease outcomes from observational data (Davey Smith & Hemani, 2014). The logic is analogous to a natural randomized controlled trial: individuals inheriting alleles that increase LDL cholesterol levels are "randomized" to higher lifetime LDL exposure, and the association between these alleles and coronary artery disease risk provides an estimate of the causal effect of LDL on CAD that is unconfounded by the lifestyle, socioeconomic, and behavioral factors that plague conventional epidemiology.

Three assumptions are required for valid MR inference: (a) the genetic instrument must be associated with the exposure (relevance); (b) the instrument must not be associated with confounders of the exposure-outcome relationship (independence); and (c) the instrument must affect the outcome only through the exposure (exclusion restriction). Violation of assumption (c) — horizontal pleiotropy, in which the instrument affects the outcome through pathways other than the exposure — is the primary threat to MR validity. MR-Egger regression addresses this threat by estimating and correcting for directional pleiotropy under the InSIDE (Instrument Strength Independent of Direct Effect) assumption, providing a valid causal estimate even when all instruments violate the exclusion restriction (Bowden et al., 2015).

MR has transformed our understanding of modifiable disease causes, confirming causal roles for LDL cholesterol in coronary disease, BMI in type 2 diabetes and multiple cancers, and blood pressure in stroke, while providing evidence against causal roles for HDL cholesterol and C-reactive protein that had been suggested by observational epidemiology (Davey Smith & Hemani, 2014).

### 5.6 Framework F316: Liability Threshold Model for Binary Disease Prediction

Complex diseases are binary (affected/unaffected) but arise from a continuous underlying liability influenced by many genetic and environmental factors. The liability threshold model, originating from the work of Falconer, formalizes this relationship and provides the mathematical bridge between genetic architecture parameters and clinically relevant prediction metrics.

The liability $\ell_k$ for individual $k$ is:

```math
\ell_k = \sum_{j=1}^{M} \beta_j x_{jk} + e_k, \quad e_k \sim \mathcal{N}(0, 1 - h^2_L)
```

where $\beta_j$ are standardized variant effects on the liability scale, $x_{jk}$ are standardized genotypes, and $h^2_L$ is the liability-scale heritability. Disease occurs when the liability exceeds a threshold $t$:

```math
t = \Phi^{-1}(1 - K)
```

where $K$ is the population prevalence and $\Phi^{-1}$ is the inverse standard normal CDF. The threshold is higher (more extreme) for rare diseases — requiring greater genetic and environmental burden for disease manifestation.

The observed-scale heritability $h^2_{\text{obs}}$ (estimated from case-control GWAS) relates to liability-scale heritability through the liability transformation:

```math
h^2_L = h^2_{\text{obs}} \cdot \frac{K(1-K)}{z^2}
```

where $z = \phi(t)$ is the standard normal density evaluated at the threshold (Lee et al., 2012). This transformation is essential for comparing heritabilities across diseases with different prevalences: a rare disease (small $K$) will have a small $h^2_{\text{obs}}$ even if $h^2_L$ is large, because the binary observation discards most of the information in the continuous liability.

The discriminative capacity of a PRS, measured by the area under the receiver operating characteristic curve (AUC), relates to the liability-scale variance explained ($R^2_L$) by:

```math
\text{AUC} = \Phi\left(\frac{\sqrt{R^2_L}}{\sqrt{2(1 - R^2_L)}}\right)
```

This equation translates abstract genetic architecture parameters into the clinically meaningful metric of discrimination. For schizophrenia ($K \approx 0.01$, $h^2_L \approx 0.80$, current PRS $R^2_L \approx 0.08$): $\text{AUC} \approx 0.71$. The theoretical maximum with a perfect PRS ($R^2_L = h^2_L = 0.80$): $\text{AUC} \approx 0.96$, demonstrating the substantial room for improvement and the clinical potential of enhanced PRS.

The model also predicts the odds ratio per standard deviation of PRS:

```math
\text{OR}_{\text{per SD}} = \exp\left(\frac{t \cdot \sqrt{R^2_L}}{1 - R^2_L} \cdot \frac{z}{K}\right) \approx \exp\left(\sqrt{R^2_L} \cdot \frac{z}{K(1-K)/z}\right)
```

For diseases with low prevalence and high heritability, even modest $R^2_L$ produces clinically meaningful stratification: for coronary artery disease ($K \approx 0.05$, current $R^2_L \approx 0.05$), the top 5% of PRS distribution has approximately 3-fold higher risk than the population average (Khera et al., 2018), demonstrating that PRS achieves risk stratification comparable to established clinical risk factors.

---

## 6. Open Questions and the Frontier

### 6.1 The Remaining Gap: Gene-Environment Interactions

Even with WGS, approximately 12% of pedigree heritability remains unaccounted for on average across traits (Young et al., 2025). Gene-environment (G×E) interactions — in which the effect of a genetic variant depends on environmental context — represent a leading candidate for this remaining gap. Durvasula and Price (2025) applied three statistical approaches to 33 UK Biobank traits and 10 environmental variables, distinguishing locus-specific G×E (individual variants whose effects change with environment), genome-wide variance modulation (the environment amplifying or dampening all genetic effects), and proportional amplification (environment scaling genetic effects uniformly) (Durvasula & Price, 2025). Their analysis revealed that all three forms of G×E are prevalent, with genome-wide variance modulation being the most common — suggesting that environmental factors such as BMI, physical activity, and socioeconomic status modify the overall expressivity of genetic predisposition rather than interacting with specific loci.

Detecting G×E at genome-wide scale is statistically challenging because the interaction signal is typically weaker than the marginal genetic effect, requiring sample sizes an order of magnitude larger than those needed for main-effect GWAS. The availability of WGS biobanks with deep phenotyping and environmental data (UK Biobank, All of Us) is beginning to provide the statistical power needed, but the field is still in its early stages.

### 6.2 From Common to Rare Disease: The Frequency Spectrum of Genetic Architecture

The genetic architecture of disease exists on a spectrum from monogenic (single rare variant of large effect) to highly polygenic (thousands of common variants of small effect), with an intermediate regime — oligogenic architecture involving a handful of variants of moderate effect — that is poorly characterized. WGS biobanks are now revealing this intermediate space: rare coding variants with moderate effect sizes ($0.1 < |\beta| < 1.0$ standard deviations) contribute measurably to common disease risk but are invisible to common-variant GWAS (UK Biobank Whole-Genome Sequencing Consortium, 2025).

Understanding the full allele frequency spectrum of genetic architecture is critical for PRS development: rare variants contribute to heritability but are poorly captured by current PRS methods, which are optimized for common variants. Integrating rare variant burden scores with common-variant PRS may improve prediction for individuals whose risk is driven by rare rather than common variation.

### 6.3 Temporal Dynamics: The G2P Map Changes Over the Lifespan

The G2P map is not static. Gene expression programs change dramatically with age, and the penetrance of many genetic variants is age-dependent — breast cancer risk alleles have different effects at age 30 versus age 70, and the heritability of many traits (including cognitive function and BMI) changes across the lifespan. The mechanisms underlying age-dependent penetrance include epigenetic drift, accumulation of somatic mutations, and changes in the cellular microenvironment that alter the functional consequences of germline variants.

Longitudinal biobanks with repeated phenotyping — such as the UK Biobank with baseline and follow-up assessments — are beginning to enable time-varying G2P analyses, but the statistical methods for modeling dynamic genetic effects are still developing. The integration of aging biology with genetic architecture theory represents an important frontier.

### 6.4 The Synthetic Genome Horizon

Looking further ahead, the synthetic genomics revolution — including the Saccharomyces cerevisiae 2.0 (Sc2.0) project that has constructed an entirely synthetic eukaryotic genome — raises the possibility of constructing custom G2P maps from first principles. If the G2P map can be quantitatively characterized (as this review argues it now largely can be for many traits), then the logical next step is to engineer G2P relationships deliberately — designing genomes with specified phenotypic outputs. While this horizon remains distant for human applications, it is already being explored in model organisms and cell engineering contexts, where synthetic regulatory circuits implement defined G2P mappings with increasing sophistication.

### 6.5 Framework F317: The Breeder's Equation Extended to Polygenic Medicine

The breeder's equation, the foundational result of quantitative genetics, predicts the response to selection:

```math
R = h^2 \cdot S
```

where $R$ is the change in mean phenotype after one generation of selection, $h^2$ is narrow-sense heritability, and $S$ is the selection differential (the difference between the selected parents' mean and the population mean). This equation describes the fundamental relationship between genetic architecture (encoded in $h^2$) and the capacity to shift a phenotype through selective pressure.

We extend this framework to the context of polygenic medicine, where the goal is not selective breeding but rather predicting the population-level phenotypic consequences of genotype-informed interventions. Define a "health response" to polygenic intervention:

```math
\Delta \mu_P = \sum_{j=1}^{M} \Delta p_j \cdot \beta_j \cdot \sqrt{2p_j(1-p_j)}
```

where $\Delta p_j$ is the effective change in risk allele frequency at variant $j$ in the treated population (through pharmacogenomic adjustment, risk-stratified screening, or targeted therapy), $\beta_j$ is the per-allele effect on the liability, and $p_j$ is the baseline allele frequency.

The multivariate extension, following Lande (1979), predicts correlated responses across traits:

```math
\Delta \bar{\mathbf{z}} = \mathbf{G} \cdot \mathbf{P}^{-1} \cdot \mathbf{S} = \mathbf{G} \cdot \boldsymbol{\beta}_S
```

where $\mathbf{G}$ is the additive genetic variance-covariance matrix, $\mathbf{P}$ is the phenotypic variance-covariance matrix, $\mathbf{S}$ is the multivariate selection gradient, and $\boldsymbol{\beta}_S = \mathbf{P}^{-1} \mathbf{S}$ is the selection gradient vector. The genetic covariance matrix $\mathbf{G}$ — estimable from bivariate LD score regression — encodes the pleiotropic constraints: a PRS-guided intervention targeting one trait (e.g., lowering LDL cholesterol through statin initiation guided by polygenic risk) will produce correlated responses in genetically correlated traits (reduced coronary disease risk, but potentially adverse changes in traits with antagonistic genetic correlations).

This framework formalizes the concept of "polygenic medicine" as a quantitative optimization problem:

```math
\max_{\boldsymbol{\Delta}} \, \mathbf{c}^T \Delta \bar{\mathbf{z}} \quad \text{subject to} \quad \Delta \bar{z}_k \geq 0 \; \forall \; k \in \text{safety constraints}
```

where $\mathbf{c}$ weights the health benefit of each trait shift and the constraints ensure that no correlated trait worsens beyond an acceptable threshold. The genetic correlation matrix, now estimable for hundreds of trait pairs via LDSC, provides the quantitative substrate for this optimization — predicting both the intended benefits and unintended pleiotropic consequences of genotype-guided interventions (Bulik-Sullivan et al., 2015).

---

## 7. Conclusion

The genotype-phenotype map — from germline DNA variation to organismal traits — has been transformed from a conceptual abstraction into a quantitatively characterized information channel. Three developments have driven this transformation. First, whole-genome sequencing of population-scale biobanks has resolved the missing heritability problem for approximately half of studied traits, demonstrating that common and rare variants together explain the vast majority of family-based heritability estimates when measured with sufficient precision. Second, Bayesian fine-mapping, multi-ancestry analysis, and high-throughput functional validation have advanced the field from association to causation, identifying specific causal variants and their molecular mechanisms at an accelerating pace. Third, network-theoretic and information-theoretic frameworks now provide rigorous models for how variant-level effects propagate through gene regulatory networks to produce the extreme polygenicity observed in complex traits.

The clinical translation of these advances is underway. Polygenic risk scores have been returned to 25,000 patients in the eMERGE network, pharmacogenomic testing has demonstrated a 30% reduction in adverse drug reactions in the PREPARE trial, and Mendelian randomization has identified modifiable causal exposures for dozens of common diseases. Yet substantial challenges remain: the cross-ancestry PRS portability gap threatens to exacerbate health disparities, gene-environment interactions remain poorly characterized, and the transition from risk prediction to risk modification — from knowing who is at risk to knowing what to do about it — requires integration of genetic architecture knowledge with therapeutic biology.

The mathematical frameworks developed in this review formalize the quantitative principles at each level of the G2P map: heritability decomposition (F312), causal variant identification (F313), network propagation (F314), information-theoretic channel characterization (F315), liability-to-prediction translation (F316), and intervention optimization under pleiotropic constraints (F317). Together, they establish a unified quantitative language for the G2P map that connects the molecular biology of individual variants to the population genetics of complex traits and the clinical challenge of precision medicine. The G2P map is no longer a black box — it is a structured, multi-scale information system whose architecture we can measure, whose bottlenecks we can identify, and whose clinical exploitation has begun.

---

## 8. Open Questions

1. **What is the contribution of rare noncoding structural variants to complex trait heritability?** Current WGS analyses have resolved the missing heritability problem for many traits using all variant classes combined, but the specific contribution of noncoding structural variants — the most difficult class to detect and interpret — remains poorly quantified. The approximately 12% residual gap between WGS-estimated and pedigree heritability may reside partly in these variants.

2. **Can the omnigenic versus stratagenic architecture question be resolved empirically?** Both models make testable predictions about the distribution of heritability across functional annotations and the network topology of trans-eQTL effects. Large-scale perturbation studies (CRISPR screens, base editing screens) in disease-relevant cell types may provide the causal evidence needed to distinguish these architectures.

3. **How should gene-environment interactions be incorporated into polygenic risk scores?** Current PRS assume that genetic effects are constant across environments, but evidence of widespread G×E suggests that context-dependent PRS — incorporating environmental modifiers — may improve prediction and clinical utility.

4. **What is the optimal integration of rare variant burden scores with common-variant PRS?** As WGS becomes routine in clinical settings, methods for combining rare and common variant information into unified risk predictors are needed.

5. **How can multimodal G2P models be deployed in clinical prediction?** The CIG framework of Khodaee et al. (2025) demonstrates that multimodal learning captures G2P dynamics beyond linear GWAS, but translating these research models into validated clinical prediction tools requires standardization, calibration, and prospective validation.

---

## References

1. Barton, N. H., Etheridge, A. M., & Veber, A. (2017). The infinitesimal model: Definition, derivation, and implications. *Theoretical Population Biology*, 118, 50–73. PMID: 28709925

2. Benner, C., Spencer, C. C. A., Havulinna, A. S., Salomaa, V., Ripatti, S., & Pirinen, M. (2016). FINEMAP: Efficient variable selection using summary data from genome-wide association studies. *Bioinformatics*, 32(10), 1493–1501. PMID: 26773131

3. Bowden, J., Davey Smith, G., & Burgess, S. (2015). Mendelian randomization with invalid instruments: Effect estimation and bias detection through Egger regression. *International Journal of Epidemiology*, 44(2), 512–525. PMID: 26050253

4. Boyle, E. A., Li, Y. I., & Pritchard, J. K. (2017). An expanded view of complex traits: From polygenic to omnigenic. *Cell*, 169(7), 1177–1186. PMID: 28622505

5. Bulik-Sullivan, B. K., Loh, P.-R., Finucane, H. K., Ripke, S., Yang, J., Patterson, N., ... & Neale, B. M. (2015). LD Score regression distinguishes confounding from polygenicity in genome-wide association studies. *Nature Genetics*, 47(3), 291–295. PMID: 25642630

6. Dalla-Torre, H., Gonzalez, L., Mendoza-Revilla, J., Carranza, N. L., Grzesik, A. H., de Almeida, B. P., ... & Lopez, R. (2024). The Nucleotide Transformer: Building and evaluating robust foundation models for human genomics. *Nature Methods*, 21, 1–10. PMID: 39609566

7. Davey Smith, G., & Hemani, G. (2014). Mendelian randomization: Genetic anchors for causal inference in epidemiological studies. *Human Molecular Genetics*, 23(R1), R89–R98. PMID: 25064373

8. Durvasula, A., & Price, A. L. (2025). Distinct explanations underlie gene-environment interactions in the UK Biobank. *American Journal of Human Genetics*, 112(3), 644–658. PMID: 39965571

9. Finucane, H. K., Bulik-Sullivan, B., Gusev, A., Trynka, G., Reshef, Y., Loh, P.-R., ... & Price, A. L. (2015). Partitioning heritability by functional annotation using genome-wide association summary statistics. *Nature Genetics*, 47(11), 1228–1235. PMID: 26414678

10. Fujita, M., Gao, Z., Zeng, L., McCabe, C., White, C. C., Ng, B., ... & De Jager, P. L. (2024). Cell subtype-specific effects of genetic variation in the Alzheimer's disease brain. *Nature Genetics*, 56(4), 605–614. PMID: 38514782

11. Funk, J. S., Klimovich, M., Gerlach, D., Greven, A., Seyffarth, F., Westermann, F., ... & Wachter, A. (2025). Deep CRISPR mutagenesis characterizes the functional diversity of TP53 mutations. *Nature Genetics*, 57, 140–153. PMID: 39774325

12. Garcia-Gonzalez, J., & O'Reilly, P. F. (2026). Genetic architecture of complex traits: Polygenic, omnigenic, or stratagenic? *Nature Genetics*, 58, 113–121. PMID: 41559216

13. Ge, T., Chen, C.-Y., Ni, Y., Feng, Y.-C. A., & Smoller, J. W. (2019). Polygenic prediction via Bayesian regression and continuous shrinkage priors. *Nature Communications*, 10(1), 1776. PMID: 30992449

14. GTEx Consortium. (2020). The GTEx Consortium atlas of genetic regulatory effects across human tissues. *Science*, 369(6509), 1318–1330. PMID: 32913098

15. Khera, A. V., Chaffin, M., Aragam, K. G., Haas, M. E., Roselli, C., Choi, S. H., ... & Kathiresan, S. (2018). Genome-wide polygenic scores for common diseases identify individuals with risk equivalent to monogenic mutations. *Nature Genetics*, 50(9), 1219–1224. PMID: 30104762

16. Khodaee, F., Zandie, R., & Edelman, E. R. (2025). Multimodal learning for mapping genotype–phenotype dynamics. *Nature Computational Science*, 5, 333–344. PMID: 39875699

17. Lee, S. H., Goddard, M. E., Wray, N. R., & Visscher, P. M. (2012). A better coefficient of determination for genetic profile analysis. *Genetic Epidemiology*, 36(3), 214–224. PMID: 22714935

18. Lee, S., Dobbyn, A., Huckins, L. M., Luo, J., Zhong, Q., Murakawa, Y., ... & Bhatt, D. K. (2025). Massively parallel reporter assay across eight psychiatric disorders identifies regulatory variants and biological pathways. *Cell*, 188(2), 422–438. PMID: 39848247

19. Lennon, N. J., Kottyan, L. C., Manolio, T. A., Murray, M. F., Namjou, B., Stanaway, I. B., ... & eMERGE Consortium. (2024). Selection, optimization and validation of ten chronic disease polygenic risk scores for clinical implementation in diverse US populations. *Nature Medicine*, 30, 480–487. PMID: 38374346

20. Linder, J., Srivastava, D., Yuan, H., Aber, V., & Kelley, D. R. (2025). Predicting RNA-seq coverage from DNA sequence as a unifying model of gene regulation. *Nature Genetics*, 57, 299–310. PMID: 39779956

21. Liu, X., Li, Y. I., & Pritchard, J. K. (2019). Trans effects on gene expression can drive omnigenic inheritance. *Cell*, 177(4), 1022–1034.e6. PMID: 31051098

22. Manolio, T. A., Collins, F. S., Cox, N. J., Goldstein, D. B., Hindorff, L. A., Hunter, D. J., ... & Visscher, P. M. (2009). Finding the missing heritability of complex diseases. *Nature*, 461, 747–753. PMID: 19812666

23. Martin, A. R., Kanai, M., Kamatani, Y., Okada, Y., Neale, B. M., & Daly, M. J. (2019). Clinical use of current polygenic risk scores may exacerbate health disparities. *Nature Genetics*, 51(4), 584–591. PMID: 30926966

24. Pan-UK Biobank Team. (2025). Pan-ancestry genome-wide association analyses enhance discovery and resolution of ancestry-enriched effects. *Nature Genetics*, 57(10), 2408–2417. PMID: 40968291

25. Pejaver, V., Byrne, A. B., Feng, B.-J., Pagel, K. A., Mooney, S. D., Karchin, R., ... & ClinGen SVI Working Group. (2025). Calibration of computational tools for missense variant pathogenicity classification and ClinGen recommendations for PP3/BP4 criteria. *American Journal of Human Genetics*, 112, 354–366. PMID: 40084623

26. Prive, F., Arbel, J., & Vilhjalmsson, B. J. (2021). LDpred2: Better, faster, stronger. *Bioinformatics*, 36(22), 5424–5431. PMID: 33326037

27. Rubin, A. F., Esposito, D., Kinney, J. B., Maves, L., Senior, A., Starita, L. M., & Fowler, D. M. (2025). MaveDB v2: A curated community database with over 7 million variant effect measurements. *Genome Biology*, 26, 30. PMID: 39838450

28. Sartorelli, J. A., Tonner, P. D., Yun, T., & Vaishnav, E. D. (2025). TraitGym: Benchmarks for assessing how well sequence models predict trait-associated variants. *Nature Methods*, 22, 522–531. PMID: 39990426

29. Schunkert, H., Erdmann, J., Inouye, M., Jaiswal, S., Kessler, T., Samani, N. J., ... & ESC Council. (2025). Clinical utility and implementation of polygenic risk scores for predicting cardiovascular disease. *European Heart Journal*, 46(15), 1372–1383. PMID: 39906985

30. Stamp, J., DenAdel, A., Weinreich, D., & Crawford, L. (2025). Scalable marginal epistasis detection for biobank-scale data. *American Journal of Human Genetics*, 112(6), 1181–1196. PMID: 40738108

31. Swen, J. J., van der Wouden, C. H., Manson, L. E., Abdullah-Koolmees, H., Blagec, K., Brito, S., ... & Guchelaar, H.-J. (2023). A 12-gene pharmacogenetic panel to prevent adverse drug reactions: An open-label, multicentre, controlled, cluster-randomised crossover implementation study. *The Lancet*, 401, 347–356. PMID: 36640488

32. Tewhey, R., Kotliar, D., Park, D. S., Liu, B., Winnber, S., Schreiber, S. L., ... & Sabeti, P. C. (2016). Direct identification of hundreds of expression-modulating variants using a multiplexed reporter assay. *Cell*, 165(6), 1519–1529. PMID: 27259153

33. The All of Us Research Program Investigators. (2024). Genomic data in the All of Us Research Program. *Nature*, 627, 340–346. PMID: 38374255

34. UK Biobank Whole-Genome Sequencing Consortium. (2025). Whole-genome sequencing of 490,640 UK Biobank participants. *Nature*, 645, 692–701. PMID: 40770095

35. Vilhjalmsson, B. J., Yang, J., Finucane, H. K., Gusev, A., Lindstrom, S., Ripke, S., ... & Price, A. L. (2015). Modeling linkage disequilibrium increases accuracy of polygenic risk scores. *American Journal of Human Genetics*, 97(4), 576–592. PMID: 26430803

36. Visscher, P. M., Hill, W. G., & Wray, N. R. (2008). Heritability in the genomics era — concepts and misconceptions. *Nature Reviews Genetics*, 9(4), 255–266. PMID: 18319743

37. Wang, G., Sarkar, A., Carbonetto, P., & Stephens, M. (2020). A simple new approach to variable selection in regression, with application to genetic fine-mapping. *Journal of the Royal Statistical Society: Series B*, 82(5), 1273–1300. PMID: 33041752

38. Wray, N. R., Wijmenga, C., Sullivan, P. F., Yang, J., & Visscher, P. M. (2018). Common disease is more complex than implied by the core gene omnigenic model. *Cell*, 173(7), 1573–1580. PMID: 29906445

39. Yang, J., Benyamin, B., McEvoy, B. P., Gordon, S., Henders, A. K., Nyholt, D. R., ... & Visscher, P. M. (2010). Common SNPs explain a large proportion of the heritability for human height. *Nature Genetics*, 42(7), 565–569. PMID: 20562875

40. Yengo, L., Vedantam, S., Marouli, E., Sidorenko, J., Bartell, E., Sakaue, S., ... & Visscher, P. M. (2022). A saturated map of common genetic variants associated with human height. *Nature*, 610, 704–712. PMID: 36224396

41. Young, A. I., Benonisdottir, S., Segurel, L., & Kong, A. (2025). Estimation of the proportion of trait heritability captured by whole-genome sequencing. *Nature*, 639, 210–218. PMID: 41225014

42. Yuan, K., Longchamps, R. J., Pardiñas, A. F., Yu, M., Chen, T.-T., Thibord, F., ... & Huang, H. (2024). Fine-mapping across diverse ancestries drives the discovery of putative causal variants underlying human complex traits and diseases. *Nature Genetics*, 56(9), 1841–1850. PMID: 39187616
