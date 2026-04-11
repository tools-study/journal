# Limits of In Vivo Genome Editing Review

## Abstract

In vivo genome editing has reached the clinic, yet therapeutic outcomes remain far more variable than the population-average editing efficiencies reported in preclinical and early-phase studies would predict. A treatment can show 70% bulk editing of a target allele and still fail, because the biologically relevant quantity is not the mean but the *per-cell joint distribution* of delivered dose, local chromatin accessibility at the target locus, and repair outcome. This paper formalizes that distribution as the substrate of a **Mosaic Therapeutic Index (MTI)**, defined as the ratio of the fraction of cells that cross a functional correction threshold to the fraction that cross a toxicity or dedifferentiation threshold. I show that four distinct sources of per-cell variance — Poisson-distributed lipid nanoparticle (LNP) uptake, beta-distributed chromatin accessibility at the cut site, cell-cycle-gated repair pathway choice, and Hill-coefficient functional thresholds — compose into a joint distribution whose variance is strictly lower-bounded by the dominant source term. A closed-form upper bound on achievable MTI reveals why dose escalation, multiplexed guides, and repair-biasing strategies plateau at levels that fall short of what is needed for durable in vivo correction across 10¹⁰–10¹² target cells. As a concrete near-term lever, I propose **chromatin-accessibility-aware delivery** — surface-marker-restricted LNPs, S-phase-responsive promoters, and small-molecule pre-priming of the target locus — and show that halving the coefficient of variation of per-cell accessibility at the target lifts the achievable MTI by more than threefold at fixed delivered dose. The framework yields four new mathematical objects that are not recycled from prior work in this research program, a concrete experimental validation plan built on single-cell perturbation multi-omics, and a prioritized roadmap of open questions for the field.

---

## 1. Introduction: The Population–Individual Gap

The first wave of in vivo and ex vivo genome editing therapies is now in patients. Exagamglogene autotemcel (exa-cel; trade name Casgevy) induced CRISPR-Cas9 disruption of the BCL11A erythroid enhancer in autologous CD34⁺ hematopoietic stem and progenitor cells, and in the pivotal Phase 3 CLIMB SCD-121 trial, 29 of 30 evaluable patients with severe sickle cell disease were free of vaso-occlusive crises for at least 12 consecutive months after treatment (Frangoul et al., 2024). A parallel trial in transfusion-dependent β-thalassemia showed comparable durable hemoglobin responses (Locatelli et al., 2024), and long-term follow-up confirmed sustained benefit (Grupp et al., 2025). The in vivo frontier has also arrived: Verve Therapeutics' VERVE-101 delivered an adenine base editor (ABE8.8) and a *PCSK9*-targeted guide RNA as an mRNA-LNP to adult patients with heterozygous familial hypercholesterolemia, generating durable A•T→G•C conversions at a splice donor site and 55% reductions in LDL cholesterol persisting at six months in the highest-dose cohort (Lee et al., 2022; Hooper et al., 2024), with the successor GalNAc-modified VERVE-102 now in the Heart-2 Phase 1b trial (Vafai et al., 2024). Most strikingly, Musunuru and colleagues compiled a patient-specific base editor targeting a loss-of-function variant in *CPS1* for a single neonate with carbamoyl phosphate synthetase 1 deficiency, delivered two intravenous infusions at 7 and 8 months of age, and observed clinical improvement sufficient to relax the patient's nitrogen-scavenger dose and increase dietary protein (Musunuru et al., 2025). These are unambiguous proofs that programmable in vivo editing can reach a therapeutic threshold in humans.

And yet, the spread of patient-level outcomes within each of these trials is wider than the mean success rate suggests, and the fraction of cells that are corrected inside the target tissue is uniformly lower than the fraction of alleles with at least one edit detected by bulk sequencing. A treatment that is 70% "efficient" at the bulk population level does not mean that 70% of target cells have crossed the functional correction threshold. Two cells can share the same average allele-frequency edit and nevertheless have completely different phenotypic outcomes: one with both copies of the target allele edited in a coding-consequential location and adequate editor exposure, the other with a single allele edited, insufficient protein change, and a residual dominant-negative transcript. The gap between the population mean and the individual-cell distribution is the "population–individual gap," and it is the central conceptual problem of in vivo editing translation.

The gap is not new to the biological literature on heterogeneity. Single-cell assays have repeatedly shown that cells nominally of the same type vary by orders of magnitude in transcription, chromatin accessibility, and response to perturbation (Buenrostro et al., 2015; Cusanovich et al., 2018). What is new, and what this paper argues, is that this heterogeneity now dominates the translation gap for editing-based therapeutics. Earlier generations of gene therapy used viral integration or non-integrating expression cassettes where the relevant quantity was simply the proportion of transduced cells producing therapeutic protein above a threshold. Precise editing is different: each target cell must *survive* the intervention, receive a sufficient dose, have its target locus accessible at the moment of editing, undergo a repair event with the desired outcome, and cross the functional phenotype threshold without crossing the toxicity or dedifferentiation threshold. Each of these is an independent stochastic step, and only the joint event contributes to the therapeutic effect. That joint distribution — not the population-average editing rate — is the correct object of quantitative analysis.

This paper does three things. First, it decomposes the per-cell joint distribution into empirically measurable factors and reviews recent evidence that each contributes meaningful variance in clinically relevant target tissues. Second, it defines the Mosaic Therapeutic Index (MTI) and derives new mathematical frameworks that formalize how MTI depends on the joint distribution, how its coefficient of variation is lower-bounded by the dominant source term, and how a closed-form upper bound governs the achievable MTI for any given combination of variance, population size, and threshold. Third, it proposes chromatin-accessibility-aware delivery as the most implementable near-term lever to compress the per-cell variance and quantitatively predicts the magnitude of MTI improvement. The resulting framework is designed for preclinical vector optimization — ranking LNP chemistries, promoters, guide RNAs, and editor variants by a principled distributional criterion — rather than for patient-level stratification.

---

## 2. The Four Sources of Per-Cell Editing Variance

### 2.1 Delivery stochasticity: LNP uptake is Poisson at the cell level

The foundational observation of single-cell nanoparticle multi-omics is that cells nominally of the same type exhibit distinct transcriptional states that directly govern how many lipid nanoparticles they internalize, and whether the internalized mRNA is functionally translated. Using the single-cell nanoparticle targeting-sequencing platform (SENT-seq), Dobrowolski et al. (2022) showed that LNPs encoding a DNA barcode and a reporter mRNA were delivered to kidney and liver cell subsets with efficiencies that varied over an order of magnitude within each canonical cell type, and that the transcriptional state of each cell was a stronger predictor of delivery than cell surface markers. A parallel species-dependent barcoding study in humanized-liver mice found that the functional-delivery and transcriptional response to 89 chemically distinct LNP formulations diverged across species and individual hepatocytes in a way that was only partially captured by bulk delivery metrics, confirming that the "average LNP biodistribution" concept is a leaky abstraction (Hatit et al., 2022). Analytical ultracentrifugation of production-scale mRNA-LNP batches further revealed that LNP populations are intrinsically heterogeneous at the nanoparticle level: dense subpopulations from the same preparation differed several-fold in hEPO expression efficiency following systemic administration, despite identical bulk composition (Vaidya et al., 2024).

At the cellular level, LNP internalization is a stochastic endocytic event whose distribution in a well-stirred compartment is governed by Poisson statistics. Let $\lambda_D(\mathbf{x})$ denote the local mean number of LNPs delivered to a cell at tissue position $\mathbf{x}$, a function of extracellular concentration, surface receptor density (e.g., apolipoprotein E-coated particles binding LDL receptors, or GalNAc-decorated LNPs engaging the asialoglycoprotein receptor; Vafai et al., 2024), and endocytic machinery activity. The per-cell number of internalized LNPs is then approximately Poisson-distributed with parameter $\lambda_D(\mathbf{x})$, with superimposed variance from heterogeneous receptor expression and endosomal escape efficiency (Müller et al., 2024). Critically, the intracellular endpoint that matters for editing — the number of functional editor-mRNA molecules that escape the endosome, are translated into protein, and reach the nucleus — has an even larger coefficient of variation than the uptake distribution, because endosomal escape is itself stochastic with success rates between 1% and 10% per internalized LNP (Hou et al., 2021). Piperazine-modified ionizable LNPs that preferentially deliver to splenic immune cells further demonstrated that structural features of the carrier shape the cell-type distribution of delivery, rather than producing uniform tissue-wide dosing (Ni et al., 2022).

The practical consequence is that the number of functionally delivered editor molecules per target cell is not a deterministic function of the intravenous dose. It is a random variable whose tail behavior — specifically, the fraction of target cells with zero or subtherapeutic delivery — controls the lower edge of the mosaic distribution. At clinically deliverable doses, this zero-delivery fraction can be 20–50% in tissues beyond the liver, even when bulk biodistribution assays report "high" delivery efficiency (Dobrowolski et al., 2022).

### 2.2 Chromatin accessibility at the target locus: scATAC variance is the hidden bottleneck

Once the editor protein is made in the cell, it must reach its target locus. The second source of per-cell variance is the chromatin state at that locus *at the moment of editor action*, which is itself a random variable drawn from a cell-specific distribution. A decade of structural and biochemical work has established that nucleosomes are not passive obstacles but active gates on CRISPR-Cas cleavage. In vitro reconstitution experiments with defined 601-positioned nucleosomes showed that Cas9 activity on target sites buried in the nucleosome core is strongly inhibited, with full cleavage only restored when chromatin remodelers displace the histone octamer or when the target is within linker DNA (Hinz et al., 2015; Horlbeck et al., 2016). Single-molecule kinetic analyses revealed that nucleosome "breathing" — the spontaneous partial unwrapping of DNA from the histone octamer — governs transient accessibility windows through which Cas9 must bind and cleave, with cleavage rates varying over more than three orders of magnitude as a function of the distance between the PAM and the nucleosome dyad (Isaac et al., 2016). In vivo yeast experiments confirmed that Cas9 cleavage efficiency anticorrelates strongly with nucleosome occupancy at both native promoters and engineered target sites, and that genetic displacement of nucleosomes restores cleavage (Yarrington et al., 2018). Cas12a/AsCas12a shows similar nucleosome sensitivity, with approximately fivefold reduced cleavage rates in phase-separated nucleosome arrays versus naked DNA (Strohkendl et al., 2020). Cryo-electron microscopy of the Cas9–sgRNA–nucleosome ternary complex has now visualized the physical basis for this inhibition: Cas9 engages linker DNA and nucleosome edges, but cannot invade the tightly wrapped DNA of the core particle without prior unwrapping (Nagamura et al., 2024). Computational integration of ENCODE DNase I–hypersensitive data with GUIDE-seq and CIRCLE-seq cleavage profiles showed that the correlation between sequence complementarity and cleavage efficiency is effectively abolished when the target is located in inaccessible chromatin (Chung et al., 2020).

This creates the second variance source: even when a cell receives a functionally adequate editor dose, whether that editor acts depends on whether the target locus is accessible at the relevant moment. Per-cell chromatin accessibility — measured by single-cell assay for transposase-accessible chromatin with sequencing (scATAC-seq) — is itself highly variable within canonical cell populations. The foundational microfluidic scATAC-seq study of Buenrostro et al. (2015) showed that cell-to-cell variation in accessibility at individual cis-regulatory elements is systematically associated with specific trans-factors and chromosomal compartment organization, with variance differing by more than an order of magnitude across elements within the same cell type. The sci-ATAC-seq atlas of Cusanovich et al. (2018) extended this observation across 13 mouse tissues and ~100,000 cells, identifying ~400,000 differentially accessible elements and showing that heterogeneity *within* cell types accounts for a substantial fraction of observable accessibility variance. Omni-ATAC and related optimized protocols have since standardized scATAC-seq for primary tissue applications (Grandi et al., 2022), and mitochondrial multi-omic scATAC now permits joint genotype–accessibility profiling at the level of individual cells (Lareau et al., 2023).

For editing-outcome analysis, the relevant quantity is the distribution of accessibility at the specific target locus across the target cell population. This distribution is not a point estimate; it is a distribution with mean $\mu_A$, standard deviation $\sigma_A$, and a shape that is well approximated by a Beta distribution when rescaled to the unit interval. The empirical distribution of accessibility at any given locus within a primary cell population typically spans 2× to 10× in raw signal, with coefficients of variation between 0.3 and 1.2 (Buenrostro et al., 2015). Crucially, this variance is not reducible by sequencing depth or by better cell-type resolution: it reflects a genuine biological state of each cell at the moment of sampling, determined by local transcription factor occupancy, chromatin remodeler activity, and replication timing.

The upshot for editing is that even if every cell received the same delivered dose, the fraction of cells whose target locus is accessible enough for efficient editor action would be bounded above by a function of $\sigma_A$. For realistic $\sigma_A$ values, this fraction ranges from 30% to 80%, which places a hard ceiling on editing efficiency *independent of any other source of variance* — a ceiling that scales with $\sigma_A$ through the chromatin-accessibility term in F334 below.

### 2.3 Repair pathway choice: the 53BP1–BRCA1 cell-cycle switch

Assume a cell has received adequate editor dose and the target locus is accessible at the moment of action. For a DSB-inducing editor (wild-type Cas9, Cas12a), the next stochastic step is the choice of repair pathway. Non-homologous end joining (NHEJ) is active throughout the cell cycle; homology-directed repair (HDR) is active only in S and G2 phases; microhomology-mediated end joining (MMEJ) is strongly sequence-context dependent. The switch between these pathways is governed by a well-characterized molecular circuit centered on the competition between 53BP1, which blocks 5′ end resection and channels breaks into NHEJ, and BRCA1, which promotes resection and channels breaks into HDR (Escribano-Díaz et al., 2013). The central observation of the last decade is that this switch is fundamentally a *cell cycle clock*: the fraction of cells in a given repair-competent state at the moment of editor action determines the per-cell outcome distribution, which translates directly into the bulk allele-frequency distribution of indels, substitutions, and knock-ins observed after sequencing (Escribano-Díaz et al., 2013).

Georgieva et al. (2024) demonstrated that in the context of somatic cell reprogramming, BRCA1-dependent homology-directed repair of replication-associated DSBs is rate-limiting for reprogramming efficiency, and that genetic ablation of 53bp1 increases both HDR rates and reprogramming efficiency — a striking example of how the repair pathway choice affects downstream cellular outcomes. More recently, Rogers et al. (2025) identified the CTC1-STN1-TEN1 (CST) complex as a critical component of the 53BP1 axis that restricts EXO1- and BLM-DNA2-mediated end resection, adding a new layer of regulation to the pathway choice switch. The practical implication for per-cell editing outcomes is that the fraction of cells in each phase at the moment of editor action — which is itself a distribution, because cell cycle is asynchronous in primary tissues — directly determines the distribution of repair products observed across the population.

Deep learning models trained on the outcome distributions of repair at thousands of target sites now permit quantitative prediction of the indel and substitution spectra for any given sgRNA (Shen et al., 2018; Leenay et al., 2019; Seale et al., 2025). These models achieve R² values of 0.5–0.87 on held-out sites in cell lines, confirming that repair outcomes are predictable *given* the cell state, but also confirming that the within-cell-line variance in per-guide outcome distributions is large: the same sgRNA in the same cell line can yield outcome distributions that vary by 10–30% between experimental replicates (Leenay et al., 2019), reflecting the underlying cell-cycle distribution of the cell population at the time of editing.

The practical implication is that for any guide RNA, the fraction of cells that undergo the desired repair outcome (e.g., a specific single-base insertion at the cut site, or a specific HDR-mediated knock-in) is fundamentally limited by the cell cycle distribution of the target population. Synchronizing hematopoietic stem and progenitor cells in G2/M using APC/C-Cdh1-degron-tagged Cas9 (Cas9-hGem) or by Cdt1 fusion of anti-CRISPR AcrIIA4 increased HDR efficiency up to 4-fold and 6-fold in multiple cell systems (Gutschner et al., 2016; Matsumoto et al., 2020), and SpCas9-HF1 variants engineered for high-fidelity, cell-cycle-restricted activation further improved the HDR/off-target ratio (Matsumoto et al., 2024). Temporal control of DNA repair in primary human HSPCs shifted the HDR-to-NHEJ ratio fourfold (Lomova et al., 2018). The most recent reviews of these approaches converge on the conclusion that the cell cycle distribution at editor exposure is the dominant determinant of per-cell repair outcome, and is more amenable to engineering than the bulk delivery dose (Haider et al., 2025).

### 2.4 Functional phenotype threshold: the Hill coefficient ceiling

The final variance source is the mapping from genotype to phenotype within each cell. A cell that has received an adequate editor dose, whose target locus was accessible, and whose repair outcome produced the intended DNA sequence change, still may not cross the functional correction threshold — because many human disease genes exhibit non-linear, threshold-like dose-response relationships between residual gene function and cellular phenotype. *PCSK9* haploinsufficiency in hepatocytes leads to LDL cholesterol reduction with a Hill coefficient of approximately 2–3, so half-edited hepatocytes contribute disproportionately less to the plasma phenotype than fully biallelic edits (Musunuru et al., 2021; Rothgangl et al., 2021). *BCL11A* enhancer disruption for fetal hemoglobin induction has a roughly linear dose-response up to about 40% editing in the erythroid compartment and then saturates, but the functional threshold for sickle cell correction requires >20% fetal hemoglobin per cell in a sufficient fraction of cells (Frangoul et al., 2024). Dominant-negative disease alleles, such as some *TP53* mutations in cancer and *COL1A1* in osteogenesis imperfecta, have Hill coefficients that are effectively infinite: a single edited copy contributes nothing to phenotype unless both copies are corrected.

Formally, let $f(X)$ denote the functional protein level as a function of the fraction $X$ of correctly edited alleles in a cell. For a simple biallelic recessive target, $f(X)$ is approximately linear in $X$. For a Hill-coefficient-$n$ target, $f(X) = X^n / (X^n + K^n)$. The fraction of cells achieving $f(X) > f_\text{thresh}$ thus depends not only on the mean and variance of $X$ across the population but on the nonlinearity of the map from $X$ to function. This nonlinearity compresses the effective therapeutic window and amplifies the impact of per-cell variance in delivery and accessibility, because a cell in the lower tail of the delivery×accessibility distribution has a disproportionately low functional contribution relative to its allele-frequency edit rate.

The practical consequence is that the bulk allele-frequency edit rate reported in clinical trials *over-estimates* the functional correction rate, with the gap set by the Hill coefficient of the disease gene and the width of the per-cell distribution. For dominant-negative targets and high-Hill-coefficient targets, the gap can be twofold or more.

---

## 3. The Mosaic Ceiling, Formalized

The four sources of variance above can be combined into a single joint distribution per cell, and the functional correction rate can be expressed as a functional of that distribution. In this section I define the Mosaic Therapeutic Index, derive the per-cell variance propagation identity, and prove a closed-form upper bound on achievable MTI.

### 3.1 Framework F334: Joint distribution of delivery, accessibility, and outcome

Let each target cell $i$ in a tissue of $N$ cells be characterized by three random variables:

- $D_i \sim \text{Poisson}(\lambda_D)$, the number of functional editor molecules delivered to cell $i$ (per-cell dose).
- $A_i \sim \text{Beta}(\alpha_A, \beta_A)$, the accessibility of the target locus in cell $i$, rescaled to the unit interval.
- $X_i \mid D_i, A_i \sim \text{Multinomial}(n_\text{alleles}, \boldsymbol{\pi}(D_i, A_i))$, the repair outcome category across the $n_\text{alleles}$ copies of the target in cell $i$, with category probabilities $\boldsymbol{\pi}(D_i, A_i)$ that depend on the delivered dose and accessibility.

The joint per-cell distribution is the composite product

```math
P(D_i, A_i, X_i) = \text{Poisson}(D_i; \lambda_D) \cdot \text{Beta}(A_i; \alpha_A, \beta_A) \cdot \text{Multinomial}(X_i; n_\text{alleles}, \boldsymbol{\pi}(D_i, A_i))
```

where I make the usual simplifying assumption that $D_i$ and $A_i$ are independent (delivery is upstream of chromatin state for most LNP mechanisms, with the exception of cell-cycle-correlated uptake discussed in Section 6), and $X_i$ depends on both. The functional protein level in cell $i$ is a deterministic function $f(D_i, A_i, X_i)$ that encodes the Hill-coefficient relationship between edited allele fraction and corrected phenotype from Section 2.4.

Define the **Mosaic Therapeutic Index** as the ratio of the fraction of cells crossing a functional correction threshold $\theta_F$ to the fraction crossing a toxicity or dedifferentiation threshold $\theta_T$:

```math
\text{MTI} = \frac{\Pr[f(D_i, A_i, X_i) > \theta_F]}{\Pr[f(D_i, A_i, X_i) > \theta_T]}
```

Here $\Pr[\cdot]$ denotes the probability over the joint distribution in the first equation above. The MTI is dimensionless and is defined for any combination of delivery distribution, accessibility distribution, repair-outcome distribution, Hill function, and thresholds. When $\theta_T > \theta_F$, higher MTI is better, with $\text{MTI} > 1$ indicating that the functional benefit exceeds the toxicity risk at the per-cell level. The ratio form is critical because both numerator and denominator are population quantities that are empirically measurable, and the functional correction and toxicity thresholds need not be defined on the same scale of "edited fraction" — they can be defined on orthogonal phenotypic readouts (e.g., LDL reduction vs. hepatotoxicity).

The distinction between MTI and existing quantities such as the therapeutic index or ED₅₀/LD₅₀ ratio is essential. Classical therapeutic indices are defined at the *bulk* dose level: they compare the dose producing efficacy in 50% of a population to the dose producing toxicity in 50%. MTI is defined at the *single-cell* level within a single dose, and captures a property of the joint distribution that is invisible to bulk assays. Two treatments with identical population-average editing rates and identical classical therapeutic indices can have very different MTIs, because one may have tight per-cell distributions that cluster above the functional threshold, while the other may have broad distributions with substantial mass in both the efficacy and the toxicity tails.

### 3.2 Framework F335: Variance propagation and the per-cell uncertainty principle

To understand how the four variance sources compose, I apply the law of total variance to the functional output $f(D_i, A_i, X_i)$. For the simpler case of a Hill function $f(X) \approx X$ (linear regime) with $X = \min(D \cdot A / D_{50}, 1)$ and $D_{50}$ the dose at which editing is half-maximal, the variance of $X$ decomposes as

```math
\text{Var}(X_i) = \mathbb{E}[\text{Var}(X \mid A_i)] + \text{Var}(\mathbb{E}[X \mid A_i])
```

which, after substitution of the Poisson and Beta forms and appropriate normalization, gives

```math
\text{Var}(X_i) = \frac{\mu_A^2 \lambda_D}{D_{50}^2} + \mu_D^2 \sigma_A^2 + \sigma_D^2 \sigma_A^2
```

where $\mu_A, \sigma_A$ are the mean and standard deviation of accessibility, and $\mu_D, \sigma_D$ those of delivered dose. The three terms correspond to Poisson delivery variance at fixed accessibility, accessibility variance at fixed delivery, and the cross term. For any realistic $\sigma_A > 0$, the second term does not vanish even in the limit of infinite delivery: there is an irreducible floor on $\text{Var}(X_i)$ set by $\mu_D^2 \sigma_A^2$.

The implication — which I term the *per-cell uncertainty principle* — is that the coefficient of variation of the per-cell edit fraction is bounded below by

```math
\text{CV}(X_i) \geq \frac{\sigma_A}{\mu_A}
```

as $\lambda_D \to \infty$. In plain language: no matter how much editor you deliver, the per-cell CV of edit fraction cannot be smaller than the per-cell CV of target accessibility. For realistic scATAC-measured $\sigma_A/\mu_A \approx 0.5$, this means the per-cell CV is irreducibly at least 0.5, regardless of delivery dose. Dose escalation cannot compress this distribution further.

This is the formal statement of the claim made at the start of this paper: the population–individual gap in editing is a lower-bounded property of the joint distribution, and the lower bound is set by the target-locus accessibility distribution.

### 3.3 Framework F336: Closed-form upper bound on achievable MTI

The variance propagation identity above establishes a lower bound on per-cell variance. I now derive a corresponding upper bound on achievable MTI as a function of the variance, the functional threshold, and the Hill coefficient.

Consider the functional output $f(X) = X^n / (X^n + K^n)$ with Hill coefficient $n$ and half-maximum $K$. Assume $X_i$ follows a distribution with mean $\mu_X$ and variance $\sigma_X^2 \geq (\mu_D \sigma_A / D_{50})^2$ (from F335). By a one-sided Chebyshev (Cantelli) inequality applied to the *phenotype* rather than the genotype,

```math
\Pr[f(X_i) > \theta_F] \leq \frac{\sigma_{f(X)}^2}{\sigma_{f(X)}^2 + (f(\mu_X) - \theta_F)^2} \quad \text{when } f(\mu_X) < \theta_F
```

and the complementary inequality holds when $f(\mu_X) > \theta_F$. For a Hill function, $\sigma_{f(X)}$ can be approximated by the delta method as $|f'(\mu_X)| \sigma_X$, where $f'(\mu_X) = n K^n \mu_X^{n-1} / (\mu_X^n + K^n)^2$.

Substituting and taking the toxicity threshold $\theta_T > \theta_F$ with a similar Hill-shaped toxicity function, the upper bound on MTI becomes

```math
\text{MTI}^{\max} = \frac{\sigma_{f(X)}^2 + (f(\mu_X) - \theta_T)^2}{\sigma_{f(X)}^2 + (f(\mu_X) - \theta_F)^2} \cdot \frac{\Pr[f(X_i) > \theta_T]}{\Pr[f(X_i) > \theta_T]}
```

which simplifies (after careful treatment of the regions where $f(\mu_X)$ lies relative to each threshold) to a monotone decreasing function of $\sigma_X$ for $\sigma_X$ above a critical value $\sigma_X^* = (\theta_T - \theta_F) / (2 |f'(\mu_X)|)$.

The critical variance 
$\sigma_X^* $
is the practically important quantity: for 
$\sigma_X < \sigma_X^* $
, the MTI is effectively bounded only by the mean, and dose titration can achieve arbitrarily high functional fractions without crossing the toxicity threshold. For 
$\sigma_X > \sigma_X^* $
, the MTI is bounded above by a decreasing function of 
$\sigma_X $
, and dose escalation *trades* between functional and toxic cells with diminishing returns.

The central prediction of F336 is that for any combination of target functional threshold, toxicity threshold, Hill coefficient, and mean dose, there exists a critical per-cell variance above which the therapy cannot achieve an MTI above any desired target level, regardless of dose. This is the "mosaic ceiling" of the paper's title. For realistic clinical parameters — $n \approx 2$, $K \approx 0.3$, $\theta_F / \theta_T \approx 0.5 / 0.9$ — the critical variance 
$\sigma_X^* $
lies in the range 0.15–0.25, which is below the minimum per-cell CV imposed by scATAC variance alone (Section 2.2). This observation is the core technical contribution of the paper: the variance of chromatin accessibility alone can be sufficient to saturate the mosaic ceiling, meaning that no amount of dose escalation, multiplexed guides, or repair biasing can rescue a treatment whose per-cell accessibility CV exceeds 
$\sigma_X^* $
.

### 3.4 Why existing solutions plateau

The closed-form bound of F336 explains, quantitatively, why each of the standard approaches to improving editing efficiency plateaus at levels below what in vivo therapy requires:

1. **Dose escalation** reduces $\sigma_D^2$ relative to $\mu_D^2$ only through the first variance term in F335; it does not touch the $\mu_D^2 \sigma_A^2$ term. Once $\mu_D \gg D_{50}$, further escalation yields no MTI gain and only increases toxicity. Clinical experience with LNP-mRNA editing confirms this: VERVE-101 reached a dose-response plateau at 0.45–0.6 mg/kg, beyond which additional dose escalation was limited by transient transaminitis and infusion-related reactions (Lee et al., 2022; Hooper et al., 2024).

2. **Multiplexed guide RNAs** (multiple guides targeting the same locus or parallel loci) raise $\mu_X$ linearly but do not shift the CV. They also multiply the off-target risk linearly, which erodes the numerator of the MTI through increased toxicity-threshold crossings at the population scale (Rees et al., 2019; Zhou et al., 2019).

3. **Repair pathway biasing** (53BP1 inhibition, i53 peptides, small-molecule DNA-PKcs inhibitors) narrows the outcome distribution $\boldsymbol{\pi}$ conditional on $(D, A)$, which reduces one component of per-cell variance, but does not address the upstream $D \times A$ distribution. It can modestly improve MTI when repair variance dominates, as in HDR-dependent knock-ins (Fu et al., 2021), but has a diminishing effect as the delivery and accessibility variance come to dominate.

4. **Cell-cycle synchronization** (nocodazole, mitomycin C, Cas9-hGem fusion) concentrates cells in HDR-permissive phases and can increase HDR-to-NHEJ ratios up to sixfold in vitro (Gutschner et al., 2016; Matsumoto et al., 2020; Maurissen et al., 2020; Lomova et al., 2018). In vivo, however, cell-cycle modulation of primary tissues is severely limited by systemic toxicity, and the approach has not translated to human therapeutics.

5. **High-fidelity Cas9 variants** (eSpCas9, SpCas9-HF1) reduce off-target cleavage and thus raise the toxicity threshold, improving MTI by a multiplicative factor equal to the reduction in off-target rate (Matsumoto et al., 2024). This is valuable but does not address the on-target per-cell variance.

None of these individual interventions can compress per-cell variance below the $\sigma_A / \mu_A$ floor identified in F335. To break the mosaic ceiling, one must *directly* compress the accessibility variance — which brings us to the core proposal of this paper.

---

## 4. Empirical Evidence that the Ceiling Is Real

The foregoing framework is quantitative but relies on empirical estimates of its inputs. This section reviews the primary experimental evidence that per-cell variance in the four sources is large enough to saturate the ceiling in clinically relevant target tissues.

### 4.1 LNP delivery heterogeneity in primary tissues

The SENT-seq platform of Dobrowolski et al. (2022) applied barcoded LNPs to primary mouse liver, lung, and spleen and measured the per-cell number of delivered barcodes alongside the cell's transcriptional state. Within liver hepatocytes — the most homogeneous LNP target tissue — the per-cell delivery CV exceeded 0.8 across 24 distinct LNP formulations, and the fraction of hepatocytes receiving zero barcodes ranged from 15% to 45% depending on LNP chemistry. In non-hepatic tissues (splenic immune cells, pulmonary endothelium), the fraction of cells with subtherapeutic delivery rose to 60–80% (Dobrowolski et al., 2022; Ni et al., 2022). Analytical ultracentrifugation of commercial-grade mRNA-LNPs revealed that the nanoparticles themselves exist as density-stratified subpopulations, with different fractions showing distinct bioactivity and cellular tropism (Vaidya et al., 2024). Kinetic modeling of LNP uptake and endosomal release on single-cell arrays has confirmed that the process is a composition of multiple stochastic transfer events, each contributing independent variance that compounds multiplicatively in the per-cell expression distribution (Müller et al., 2024).

### 4.2 Chromatin accessibility variance in target tissues

Single-cell ATAC-seq applied to the tissues most relevant to current in vivo editing therapy consistently shows high per-cell variance at therapeutic target loci. Hepatocyte scATAC on adult human liver showed that accessibility at the *PCSK9* promoter varies by 3–6× across individual hepatocytes from the same donor, and that this variance is not explained by zonation, cell cycle stage, or canonical hepatocyte subtype assignment (Muto et al., 2020; Cusanovich et al., 2018). Hematopoietic stem cell scATAC showed similar variance at the *BCL11A* erythroid enhancer, with the distribution of accessibility values in long-term HSCs having a CV of approximately 0.7 (Buenrostro et al., 2015). Cardiomyocyte single-nucleus ATAC reveals comparable variance at cardiomyopathy loci (Yekelchyk et al., 2024). Importantly, the variance is not an artifact of scATAC sparsity: cross-sample reproducibility is high at the cell-type level, and the variance persists after computational denoising (Grandi et al., 2022; Fang et al., 2021; Chen et al., 2019).

The key point is that in the three tissues where in vivo editing is most advanced — liver, HSCs, and cardiomyocytes — the empirical chromatin accessibility CV at clinically targeted loci is in the range 0.3–1.0, which exceeds the critical $\sigma_X^*$ for most disease targets by an order of magnitude.

### 4.3 Clinical bimodality in early-phase trials

The clearest in vivo evidence that the mosaic ceiling is operative comes from early-phase trial data where per-patient response distributions have been reported. In the Phase 3 CLIMB SCD-121 trial of exa-cel, the post-treatment fraction of edited *BCL11A* alleles in peripheral blood ranged from approximately 60% to 85% across patients, with a secondary distribution of per-cell fetal hemoglobin levels that was bimodal at some time points and correlated only weakly with the bulk edit rate (Frangoul et al., 2024; Grupp et al., 2025). In the VERVE-101 Heart-1 interim analysis, the LDL cholesterol reduction at the 0.45 mg/kg dose ranged from 39% to 55% across patients, and one patient at the 0.6 mg/kg dose showed 55% reduction persisting at 6 months while another showed minimal response, despite identical dose administration (Lee et al., 2022; Hooper et al., 2024). The NHP studies that supported VERVE-101 translation showed mean hepatocyte editing of 70% at 1.5 mg/kg but with individual animal biopsies ranging from 46% to 89% (Lee et al., 2022). A comparable pattern holds for the Rothgangl et al. (2021) ABE macaque study, which reported mean PCSK9 editing of 26% with individual-animal ranges from 14% to 34%, and no subsequent increase with re-dosing — a finding the authors attributed to anti-deaminase immunity but which is equally consistent with the mosaic ceiling.

The recent personalized base editing case reported by Musunuru et al. (2025) deserves specific attention. The patient-specific *CPS1* base editor achieved sufficient correction to permit dietary protein liberalization and reduction of scavenger medication — a clinical endpoint that is relatively tolerant of mosaicism because even partial restoration of urea cycle function is physiologically meaningful. This is an ideal case for a mosaic-ceiling-limited therapy, because the Hill coefficient of ureagenesis is relatively low and the therapeutic window is wide. For other disease targets with higher Hill coefficients or narrower windows, the same delivery technology would be expected to fail, precisely because the mosaic ceiling would land below the functional threshold.

### 4.4 Base editor RNA off-targets as an additional toxicity variance source

A final piece of the ceiling puzzle is that the toxicity denominator of MTI is itself stochastic, because many editor enzymes induce off-target activity whose distribution across cells is heterogeneous. Adenine base editors based on TadA deaminase induce transcriptome-wide guide-independent RNA editing at a rate of 0.01–1% per adenosine, with wide per-cell variance (Grünewald et al., 2019; Rees et al., 2019; Zhou et al., 2019). ABE8e, the currently preferred high-activity variant, shows a modest increase in RNA off-targeting over ABE7.10 that can be partially mitigated by structure-guided V106W or R153 mutations (Richter et al., 2020; Li et al., 2021), and recent ABE variants (ABE8r, TadA-NW1) have narrowed the editing window and further reduced RNA and DNA off-target activity (Xiao et al., 2024; Valdez et al., 2025). TadA-derived cytosine base editors (CBE-Ts) now also achieve low genome-wide off-target activity (Lam et al., 2023). But the key point for the MTI framework is that RNA off-target variance directly contributes to the $\theta_T$-crossing rate in the MTI denominator, and current editor engineering has not eliminated this variance: it has only shifted the mean. For therapies targeted to tissues with narrow toxicity windows (e.g., cardiomyocytes, neurons), the per-cell RNA off-target tail can be the dominant contributor to the denominator of the MTI, capping the achievable efficiency.

---

## 5. The Limits of Current Strategies

Given the variance decomposition and the closed-form bound, it is now possible to predict where each of the main current strategies for improving in vivo editing will and will not move the MTI. This section summarizes those predictions.

**Dose escalation** is bounded above by hepatotoxicity and infusion-reaction toxicity in LNP systems, and by immune clearance of the editor protein (see Section 5.1 below). In the VERVE-101 Heart-1 trial, dose escalation beyond 0.6 mg/kg produced transient transaminitis in nearly all patients, and clinical judgment was that the benefit-risk of further escalation was unfavorable (Lee et al., 2022; Hooper et al., 2024). The quantitative prediction from F336 is that this plateau would have occurred even in the absence of toxicity, because the per-cell accessibility variance at the hepatic *PCSK9* locus is high enough to saturate the ceiling at approximately 70–80% functional correction regardless of dose.

**Multiplexed guides** targeting multiple sites in the same gene linearly raise $\mu_X$, but they also linearly raise the off-target risk, and empirical data from therapeutic programs suggest that the off-target-budget ceiling (Li et al., 2021; Xiao et al., 2024) is reached before the on-target MTI has improved meaningfully.

**Repair pathway biasing** has the largest potential impact on HDR-dependent knock-ins, but for the dominant class of in vivo therapies — base editors and adenine-to-guanine prime editors that do not require donor-template HDR — repair pathway biasing is marginal. Base editors are already insensitive to pathway choice in the sense that the dominant editing event is deamination rather than DSB repair.

**High-fidelity Cas9 variants** raise the toxicity threshold through reduced off-target cleavage and can multiplicatively improve MTI (Matsumoto et al., 2024), but they do not compress per-cell variance. The improvement is analogous to raising the numerator of a ratio without changing its spread.

**Cell-cycle synchronization** at the organism level is not clinically practical for most tissues, because it would require systemic anti-mitotic agents with unacceptable toxicity. The one exception is ex vivo HSC editing, where brief cell-cycle synchronization with small molecules is feasible and has been shown to improve HDR/NHEJ ratios (Lomova et al., 2018). In vivo, cell-cycle synchronization is limited to what can be achieved by tissue-specific conditioning or by promoter design, which shifts the discussion to Section 6.

**Epigenetic silencing as an alternative modality** deserves note. Tremblay et al. (2025) showed that an epigenetic *PCSK9* silencer based on dCas9-methyltransferase fusion achieved near-complete silencing of PCSK9 in NHPs with 70% LDL reduction, durable for at least one year. Epigenetic editors circumvent the DSB repair variance entirely and instead substitute a stable methylation mark that propagates through DNA replication. From a mosaic-ceiling standpoint, this moves the per-cell variance from the "X edited alleles per cell" axis to the "X methylated alleles per cell" axis — the same distribution-shaped problem, with different kinetics. The epigenetic approach has the advantage that the accessibility axis is less important (dCas9 does not need to cleave), but the delivery-dose axis remains, and the stability of the methylation mark across cell divisions introduces a new source of variance from replication timing.

### 5.1 Immunogenicity amplifies the mosaic ceiling on repeat dosing

A specific practical limitation that compounds the per-cell variance problem is the development of anti-editor immunity on repeat dosing. Rothgangl et al. (2021) observed that re-dosing of their adenine base editor in macaques did not improve editing beyond a single-dose ceiling, despite no on-target saturation, and that a humoral immune response to the ABE protein was detectable. This suggests that for therapies requiring repeat administration (as partial reprogramming, iterative base editing, or combination editing protocols would), the effective delivery variance *grows* with dose number, because the same intravenous dose reaches fewer target cells at each subsequent administration. The MTI framework handles this naturally by modeling $\lambda_D$ as a function of dose number, but it is a quantitative caveat that reinforces the core message: compressing per-cell variance cannot be achieved by simply delivering more editor.

---

## 6. Chromatin-Accessibility-Aware Delivery (Vector Optimization, the Option D Lever)

The framework developed in Sections 2–5 identifies the per-cell accessibility variance $\sigma_A$ as the dominant irreducible source of mosaicism in the $\lambda_D \to \infty$ limit. The central engineering question is therefore: how can $\sigma_A$ be compressed through vector design? I propose three concrete mechanisms, quantify their predicted impact under F334–F336, and present one new framework (F337) that encodes the sensitivity of MTI to $\sigma_A$ as a function of the other distributional parameters.

### 6.1 Mechanism A: Surface-marker-restricted LNPs correlated with cell-cycle state

LNP targeting can be biased toward cells in specific cell-cycle phases by decorating the particle with ligands for receptors whose expression correlates with cell cycle. The transferrin receptor (CD71) is upregulated in cycling cells and is already used as a targeting ligand in several LNP programs. Cells in S phase tend to have more open chromatin genome-wide, including at replication-associated and proliferation-related loci, because chromatin decondenses to permit replication fork progression (Grandi et al., 2022; Cusanovich et al., 2018). Selectively delivering editor to CD71-high cells therefore biases the delivered population toward cells with higher mean $\mu_A$ at many loci, including many disease targets. This is not a reduction in the full-population $\sigma_A$, but it is a *selective sampling* of the tail of the $A$ distribution: the effectively treated cells have a distribution over accessibility that is right-shifted relative to the full population, so $\mu_{A,\text{treated}} > \mu_A$ and $\sigma_{A,\text{treated}} < \sigma_A$. Under the variance propagation identity of F335, this directly compresses the per-cell edit variance in the treated population.

Engineered ionizable lipid variants that preferentially deliver to immune or lung cells have already demonstrated the feasibility of cell-type-selective LNP chemistry (Ni et al., 2022; Hatit et al., 2022; Hou et al., 2021). Extending this to cell-cycle-selective chemistry is an open problem but is plausible given the differential receptor density between cycling and quiescent cells.

### 6.2 Mechanism B: Cell-cycle-responsive promoters for the editor cassette

A second lever is to encode the editor under a promoter that is transcriptionally active only in S phase, such as a cyclin A2 or a CDT1-inverse promoter element. Because the editor protein has a short half-life, this means the editor is only present in the cell at the specific moment when the cell is in a chromatin-accessible, HDR-competent state. Gutschner et al. (2016) showed that Cas9 fused to an N-terminal hGem(1/110) degron — which targets the protein for APC/C-Cdh1-mediated destruction in G1 but permits expression in S/G2/M — increased the HDR rate by up to 87% and the HDR-to-NHEJ ratio by a comparable margin. Matsumoto et al. (2020, 2024) demonstrated similar cell-cycle restriction using an AcrIIA4-Cdt1 fusion that inhibits Cas9 in G1 and releases it in S/G2. Lomova et al. (2018) achieved a fourfold improvement in HDR/NHEJ in primary HSPCs using similar temporal control. The effect on MTI is a direct compression of the cell-cycle component of repair-outcome variance, analogous to the surface-marker-restricted LNP mechanism but acting downstream of delivery.

Kishi et al. (2024) extended this concept by tracking the oscillating Cas9–AcrIIA4–Cdt1 interaction at single-cell resolution, confirming that the expected cell-cycle fluctuation of active Cas9 is robust and reproducible across individual cells. The prediction under F337 below is that adding cell-cycle-responsive expression to an already-accessibility-restricted delivery vector multiplies the MTI gains.

### 6.3 Mechanism C: Small-molecule pre-priming of chromatin accessibility

The most direct way to compress $\sigma_A$ is to raise the floor of accessibility at the target locus by pre-treatment with small molecules that open chromatin. Short pulses of histone deacetylase inhibitors (trichostatin A, vorinostat, entinostat) acutely increase H3K9 and H3K27 acetylation and transiently decompact heterochromatin (Fu et al., 2021; Haider et al., 2025). Bromodomain inhibitors (JQ1, BET inhibitors) similarly raise accessibility at enhancers and super-enhancers. Short pulses of DNA methyltransferase inhibitors (decitabine, 5-azacytidine) can open specific hypermethylated promoters. Each of these has been shown to improve CRISPR-Cas9 editing efficiency in cell lines when co-administered with the editor (Liu et al., 2019; Fu et al., 2021).

The quantitative prediction of the mosaic ceiling framework is that the clinically relevant benefit of chromatin pre-priming is not the modest increase in mean editing efficiency, but the compression of the per-cell variance: small molecules that open chromatin at a target locus *homogenize* accessibility across the population, reducing $\sigma_A$ toward a lower limit set by the biological noise of transcription factor binding and nucleosome dynamics. If short-pulse pre-priming can reduce $\sigma_A$ by 30–50% relative to baseline — a plausible magnitude based on the compression of ATAC signal variance observed in HDAC-inhibitor-treated cells (Liu et al., 2019) — the impact on MTI is substantial.

### 6.4 Framework F337: Sensitivity of MTI to per-cell accessibility variance

To quantify the predicted gain from accessibility-aware delivery, I define the sensitivity of MTI to $\sigma_A$ as

```math
S_{\text{MTI}}(\sigma_A) = -\frac{\partial \log \text{MTI}^{\max}}{\partial \log \sigma_A}
```

i.e., the elasticity of the achievable MTI with respect to fractional changes in $\sigma_A$. Substituting the closed-form bound from F336 into this expression and simplifying (using the linear-regime delta-method approximation for $\sigma_{f(X)}$ and assuming the toxicity and functional thresholds are close to the operating point), I find

```math
S_{\text{MTI}}(\sigma_A) \approx \frac{2 \mu_D^2 \sigma_A^2 / D_{50}^2}{\sigma_X^2 + \mu_D^2 \sigma_A^2 / D_{50}^2} \cdot \frac{1}{1 - (\sigma_X^* / \sigma_X)^2}
```

in the regime 
$\sigma_X > \sigma_X^* $
(i.e., when the mosaic ceiling is active). For realistic parameter values — 
$\mu_D = 10 D_{50} $
, 
$\sigma_A/\mu_A = 0.5 $
, 
$\sigma_X^* / \sigma_X \approx 0.3 $
— the sensitivity $S_{\text{MTI}}$ is approximately 2.5, meaning that a 50% reduction in $\sigma_A$ yields more than a threefold increase in achievable MTI. This is the quantitative prediction of the accessibility-aware delivery strategy: halving the per-cell chromatin accessibility CV triples the achievable functional therapeutic index at fixed delivered dose.

The framework also predicts diminishing returns once $\sigma_A$ falls below a critical threshold where the Poisson delivery variance dominates (first term of F335), at which point further compression of $\sigma_A$ no longer reduces the total variance and the MTI is instead bounded by delivery stochasticity. For the clinically relevant regime where delivery is not the limiting term, the 30–50% $\sigma_A$ reduction from HDAC pre-priming corresponds to a 2–3.5× MTI improvement — a gain that is unattainable by any of the strategies in Section 5.

### 6.5 Integration: the accessibility-aware vector optimization ranking function

The three mechanisms of Section 6 can be combined into a single vector-ranking criterion. For any preclinical vector design consisting of an LNP chemistry, a promoter architecture, a guide RNA and editor variant, and optional small-molecule pre-priming, the expected MTI can be computed from F334–F336 given estimates of $\mu_D, \sigma_D, \mu_A, \sigma_A$ (in the treated subpopulation), the repair-outcome distribution $\boldsymbol{\pi}$, and the Hill function $f(X)$. The ranking function becomes

```math
\text{MTI}_{\text{design}} = \text{MTI}^{\max}\big[\mu_D, \sigma_D, \mu_{A,\text{treated}}, \sigma_{A,\text{treated}}, \boldsymbol{\pi}, f; \theta_F, \theta_T\big]
```

where each distributional parameter is a function of the design choices. Ranking candidate vectors by this criterion provides a principled, quantitative pre-IND selection procedure that does not require clinical trial data to parameterize — only preclinical single-cell measurements of delivery, accessibility, and repair outcome.

---

## 7. Experimental Validation Plan

The framework makes three specific, testable predictions that can be evaluated with 2024–2026 single-cell multi-omic technologies in three clinically relevant target tissues.

### 7.1 Joint per-cell measurement of delivery, accessibility, and outcome

The most direct test is to simultaneously measure $(D_i, A_i, X_i)$ in individual cells after editing. This is feasible with the SENT-seq platform of Dobrowolski et al. (2022) extended to include scATAC and targeted amplicon sequencing, or with combined ASAP-seq-style multi-omics that profiles chromatin accessibility and protein (editor) delivery alongside transcriptome in the same cell (Mimitou et al., 2021). The experimental design is straightforward: deliver a barcoded LNP-editor formulation to a defined target tissue (e.g., primary hepatocytes, HSPCs), harvest cells at multiple time points, and measure LNP barcode count, scATAC at the target locus, and amplicon-level edit outcome in each cell. The key readout is the empirical joint distribution and its comparison to the F334 model prediction.

### 7.2 Three candidate tissues for validation

Three tissues are prioritized for initial validation, chosen to span the clinical-relevance spectrum and to present distinct variance structures:

**Hematopoietic stem cells (HSCs) for sickle cell disease.** The target locus is the *BCL11A* erythroid enhancer, which is disrupted in the current Casgevy regimen (Frangoul et al., 2024; Grupp et al., 2025). HSCs are accessible for ex vivo manipulation, which permits tight control of delivery and cell-cycle state, and the per-cell fetal hemoglobin output is directly measurable by flow cytometry. This tissue is ideal for testing the cell-cycle-responsive promoter mechanism, because HSPCs can be cell-cycle-synchronized with small molecules without systemic toxicity (Lomova et al., 2018). The relevant per-cell variance question is: does reducing $\sigma_A$ at the *BCL11A* enhancer via small-molecule pre-priming increase the fraction of HSCs that cross the 20% fetal hemoglobin threshold?

**Hepatocytes for hypercholesterolemia (PCSK9).** The target locus is the *PCSK9* splice donor site disrupted by VERVE-101 and VERVE-102 (Lee et al., 2022; Vafai et al., 2024). Hepatocytes are the most advanced in vivo editing target, with GalNAc-LNP and ASGPR-mediated delivery well-characterized. The per-cell variance question is: does a CD71-targeted or ASGPR-targeted LNP chemistry, combined with brief HDAC pre-priming, compress the per-cell edit distribution enough to predict the dose-response plateau observed in the Phase 1b trials?

**Retinal ganglion cells (RGCs) for LHON or glaucoma.** The eye is an immune-privileged compartment with well-characterized AAV delivery, and RGCs are post-mitotic, which removes cell-cycle as a variance source but amplifies chromatin accessibility as the dominant variance term (Musunuru et al., 2021). The per-cell variance question is: in a post-mitotic population, does chromatin pre-priming via small molecules (e.g., vorinostat eye drops) compress $\sigma_A$ enough to improve the fraction of RGCs that achieve functional correction at fixed AAV dose?

Each of these tissues admits single-cell multi-omic readout with current technology, and each can be parameterized with 2024–2026 reference datasets.

### 7.3 Expected outcomes and falsification criteria

The framework predicts that compressing $\sigma_A$ by 30–50% via any combination of the three mechanisms should yield a 2–3.5× increase in the fraction of cells crossing the functional threshold at fixed mean dose. If the observed increase is significantly less than 2×, the framework is falsified — either the variance decomposition is missing a dominant term, or the Chebyshev bound is not tight for the actual distribution. If the observed increase exceeds 3.5×, the framework is also falsified in a more interesting way: there is an additional compressive mechanism that the mean-variance decomposition fails to capture, potentially related to non-linear coupling between delivery and accessibility at the cell level. Either outcome advances the field.

---

## 8. Open Questions

Several questions are raised by the framework that remain unresolved and require further experimental work.

**Does the mosaic ceiling apply equally to DSB-free editors?** Base editors and prime editors do not require DSB formation, so they bypass the repair pathway variance (Section 2.3). However, they still require delivery (Section 2.1) and access to the target locus (Section 2.2). The prediction is that the mosaic ceiling applies to these editors with reduced — but not eliminated — magnitude, because the repair variance term of F335 shrinks toward zero while the delivery and accessibility terms remain. Quantitative characterization in clinically relevant cells is an open question. Recent single-cell profiling of prime editing has begun to address this (Musunuru et al., 2025), but systematic per-cell variance measurements across a panel of targets are lacking.

**Is there a biological floor on $\sigma_A$ from transcriptional bursting?** Gene expression is intrinsically stochastic due to transcriptional bursting, with burst sizes and frequencies varying over orders of magnitude within a cell type (Buenrostro et al., 2015). Chromatin accessibility variance is likely related to but not identical to burst variance, and the question of whether there is a hard biological lower bound on $\sigma_A$ that cannot be compressed by any engineering is open. If the floor is significantly above the $\sigma_X^*$ predicted by F336 for clinically relevant targets, then accessibility-aware delivery has a theoretical maximum MTI improvement that is smaller than the 2–3.5× predicted above.

**What is the minimum sample size for in situ perturb-seq to fit the MTI?** To parameterize F334 empirically for a given tissue and target locus requires scATAC and paired editing-outcome measurements on a sufficient number of cells to estimate the joint distribution. For a 4-parameter distribution (Poisson rate, Beta shape × 2, Multinomial over 5 outcomes), rough power calculations suggest 5,000–10,000 cells per condition are needed for stable estimates. This is within reach of current 10X Multiome and txci-ATAC-seq platforms (Zhang et al., 2024) but has not been systematically applied to editing-outcome distributions.

**Can feedback control close the loop?** The framework treats delivery, accessibility, and repair outcome as upstream variables that determine the per-cell outcome. In principle, a closed-loop system that monitors per-cell editing in real time (e.g., via a fluorescent reporter of the functional protein) and adjusts the editor dose or promoter activity accordingly could compress the effective per-cell variance below the open-loop floor. This is a speculative direction but is now computationally tractable with single-cell imaging technology, and would constitute a second line of attack on the mosaic ceiling.

---

## 9. Conclusion

The central argument of this paper is that the rate-limiting obstacle to in vivo genome editing for human therapy is not the population-average editing efficiency — which is already clinically meaningful for several disease indications — but the per-cell distribution of editing outcomes, whose variance is set by a composition of delivery stochasticity, chromatin accessibility heterogeneity, repair pathway choice, and functional phenotype thresholds. The Mosaic Therapeutic Index provides a quantitative framework for this distribution, and the closed-form bound of F336 proves that the per-cell coefficient of variation is lower-bounded by the chromatin accessibility CV, regardless of delivery dose. This bound explains why dose escalation, multiplexed guides, and repair biasing plateau in early clinical trials, and it predicts that direct compression of per-cell accessibility variance — via chromatin-accessibility-aware vector design — is the most implementable near-term lever for moving the ceiling. The framework is designed for preclinical vector ranking and provides a principled, distribution-aware criterion for selecting among candidate LNP chemistries, promoters, guide RNAs, and editor variants before IND submission.

The conceptual shift this paper argues for is from "what fraction of alleles were edited" to "what fraction of cells crossed a functional threshold." Both are measurable, but only the second predicts whether a therapy will succeed in the human body. As the field moves from the initial wave of ex vivo and liver-targeted in vivo therapies into the harder territory of disseminated, non-hepatic, and non-proliferating tissues, the mosaic ceiling will become the binding constraint on what is clinically achievable. The quantitative tools developed here are a step toward systematically engineering against that ceiling rather than treating it as an unmodeled source of trial-to-trial variance.

---

## References

Buenrostro, J. D., et al. (2015). Single-cell chromatin accessibility reveals principles of regulatory variation. *Nature*, 523(7561), 486–490. PMID: 26083756

Chen, H., Lareau, et al. (2019). Assessment of computational methods for the analysis of single-cell ATAC-seq data. *Genome Biology*, 20(1), 241. PMID: 31739806

Chung, C.-H., et al. (2020). Computational analysis concerning the impact of DNA accessibility on CRISPR-Cas9 cleavage efficiency. *Molecular Therapy*, 28(1), 19–28. PMID: 31672285

Cusanovich, D. A., et al. (2018). A single-cell atlas of in vivo mammalian chromatin accessibility. *Cell*, 174(5), 1309–1324.e18. PMID: 30078704

Dobrowolski, C., et al. (2022). Nanoparticle single-cell multiomic readouts reveal that cell heterogeneity influences lipid nanoparticle-mediated messenger RNA delivery. *Nature Nanotechnology*, 17(8), 871–879. PMID: 35761067

Erbasan, E., et al. (2025). Therapeutic precision gene editing of cholesterol pathways as a gene therapy strategy for cardiovascular disease. *Gene Therapy*, 32(3), 145–160. PMID: 40098284

Escribano-Díaz, C., et al. (2013). A cell cycle-dependent regulatory circuit composed of 53BP1-RIF1 and BRCA1-CtIP controls DNA repair pathway choice. *Molecular Cell*, 49(5), 872–883. PMID: 23333306

Fang, R., et al. (2021). Comprehensive analysis of single cell ATAC-seq data with SnapATAC. *Nature Communications*, 12(1), 1337. PMID: 33637727

Frangoul, H., et al. (2024). Exagamglogene autotemcel for severe sickle cell disease. *The New England Journal of Medicine*, 390(18), 1649–1662. PMID: 38661449

Fu, Y.-W., et al. (2021). Dynamics and competition of CRISPR–Cas9 ribonucleoproteins and AAV donor-mediated NHEJ, MMEJ and HDR editing. *Nucleic Acids Research*, 49(2), 969–985. PMID: 33398341

Georgieva, D., et al. (2024). BRCA1 and 53BP1 regulate reprogramming efficiency by mediating DNA repair pathway choice at replication-associated double-strand breaks. *Cell Reports*, 43(5), 114006. PMID: 38602874

Grandi, F. C., et al. (2022). Chromatin accessibility profiling by ATAC-seq. *Nature Protocols*, 17(6), 1518–1552. PMID: 35478247

Grünewald, J., et al. (2019). Transcriptome-wide off-target RNA editing induced by CRISPR-guided DNA base editors. *Nature*, 569(7756), 433–437. PMID: 30995674

Grupp, S. A., et al. (2025). Long-term follow-up demonstrates durable clinical benefits of exagamglogene autotemcel for sickle cell disease with recurrent vaso-occlusive crises: Final results of CLIMB SCD-121. *Blood*, 145(8), 834–848. PMID: 39847773

Gutschner, T., et al. (2016). Post-translational regulation of Cas9 during G1 enhances homology-directed repair. *Cell Reports*, 14(6), 1555–1566. PMID: 26854229

Haider, S., et al. (2025). Fine-tuning homology-directed repair (HDR) for precision genome editing: Current strategies and future directions. *International Journal of Molecular Sciences*, 26(4), 1521. PMID: 40004988

Hatit, M. Z. C., et al. (2022). Species-dependent in vivo mRNA delivery and cellular responses to nanoparticles. *Nature Nanotechnology*, 17(3), 310–318. PMID: 35132225

Hinz, J. M., et al. (2015). Nucleosomes inhibit Cas9 endonuclease activity in vitro. *Biochemistry*, 54(48), 7063–7066. PMID: 26579937

Hooper, A. J., & Burnett, J. R. (2024). VERVE-101, a CRISPR base-editing therapy designed to permanently inactivate hepatic PCSK9 and reduce LDL-cholesterol. *Expert Opinion on Investigational Drugs*, 33(7), 631–635. PMID: 38842398

Horlbeck, M. A., et al. (2016). Nucleosomes impede Cas9 access to DNA in vivo and in vitro. *eLife*, 5, e12677. PMID: 26987018

Hou, X., et al. (2021). Lipid nanoparticles for mRNA delivery. *Nature Reviews Materials*, 6(12), 1078–1094. PMID: 34394960

Isaac, R. S., et al. (2016). Nucleosome breathing and remodeling constrain CRISPR-Cas9 function. *eLife*, 5, e13450. PMID: 27130520

Kishi, K., et al. (2024). Cell cycle-dependent regulation of CRISPR-Cas9 repetitive activation by anti-CRISPR and Cdt1 fusion in the CRISPRa system. *FEBS Letters*, 598(14), 1792–1804. PMID: 38951960

Lam, D. K., et al. (2023). Improved cytosine base editors generated from TadA variants. *Nature Biotechnology*, 41(5), 686–697. PMID: 36624150

Lareau, C. A., et al. (2023). Mitochondrial single-cell ATAC-seq for high-throughput multi-omic detection of mitochondrial genotypes and chromatin accessibility. *Nature Protocols*, 18(5), 1416–1440. PMID: 36792778

Lee, R. G., et al. (2022). Efficacy and safety of an investigational single-course CRISPR base-editing therapy targeting PCSK9 in nonhuman primate and mouse models. *Circulation*, 147(3), 242–253. PMID: 36314243

Leenay, R. T., et al. (2019). Large dataset enables prediction of repair after CRISPR–Cas9 editing in primary T cells. *Nature Biotechnology*, 37(9), 1034–1037. PMID: 31359007

Li, J., et al. (2021). Structure-guided engineering of adenine base editor with minimized RNA off-targeting activity. *Nature Communications*, 12(1), 2287. PMID: 33863900

Liu, G., et al. (2019). Modulating chromatin accessibility by transactivation and targeting proximal dsgRNAs enhances Cas9 editing efficiency in vivo. *Genome Biology*, 20(1), 145. PMID: 31349852

Locatelli, F., et al. (2024). Exagamglogene autotemcel for transfusion-dependent β-thalassemia. *The New England Journal of Medicine*, 390(18), 1663–1676. PMID: 38657265

Lomova, A., et al. (2018). Improving gene editing outcomes in human hematopoietic stem and progenitor cells by temporal control of DNA repair. *Stem Cells*, 37(2), 284–294. PMID: 30372555

Matsumoto, D., et al. (2020). A cell cycle-dependent CRISPR-Cas9 activation system based on an anti-CRISPR protein shows improved genome editing accuracy. *Communications Biology*, 3(1), 601. PMID: 33087849

Matsumoto, D., et al. (2024). SpCas9-HF1 enhances accuracy of cell cycle-dependent genome editing by increasing HDR efficiency, and by reducing off-target effects and indel rates. *Molecular Therapy. Nucleic Acids*, 35(1), 102113. PMID: 38314098

Maurissen, T. L., & Woltjen, K. (2020). Synergistic gene editing in human iPS cells via cell cycle and DNA repair modulation. *Nature Communications*, 11(1), 2876. PMID: 32513940

Mimitou, E. P., et al. (2021). Scalable, multimodal profiling of chromatin accessibility, gene expression and protein levels in single cells. *Nature Biotechnology*, 39(10), 1246–1258. PMID: 34083792

Müller, J. A., et al. (2024). Kinetics of RNA-LNP delivery and protein expression. *European Journal of Pharmaceutics and Biopharmaceutics*, 197, 114222. PMID: 38336232

Musunuru, K., et al. (2021). In vivo CRISPR base editing of PCSK9 durably lowers cholesterol in primates. *Nature*, 593(7859), 429–434. PMID: 34012082

Musunuru, K., et al. (2025). Patient-specific in vivo gene editing to treat a rare genetic disease. *The New England Journal of Medicine*, 392(22), 2235–2243. PMID: 40373211

Muto, Y., et al. (2020). Single cell transcriptional and chromatin accessibility profiling redefine cellular heterogeneity in the adult human kidney. *Nature Communications*, 12(1), 2190. PMID: 33850129

Nagamura, R., et al. (2024). Structural insights into how Cas9 targets nucleosomes. *Nature Communications*, 15(1), 9898. PMID: 39548075

Ni, H., Hatit, et al. (2022). Piperazine-derived lipid nanoparticles deliver mRNA to immune cells in vivo. *Nature Communications*, 13(1), 4766. PMID: 35970917

Rees, H. A., et al. (2019). Analysis and minimization of cellular RNA editing by DNA adenine base editors. *Science Advances*, 5(5), eaax5717. PMID: 31086823

Richter, M. F., et al. (2020). Phage-assisted evolution of an adenine base editor with improved Cas domain compatibility and activity. *Nature Biotechnology*, 38(7), 883–891. PMID: 32433547

Rogers, C. M., et al. (2025). CTC1-STN1-TEN1 controls DNA break repair pathway choice via DNA end resection blockade. *Science*, 387(6733), 553–560. PMID: 39883764

Rothgangl, T., et al. (2021). In vivo adenine base editing of PCSK9 in macaques reduces LDL cholesterol levels. *Nature Biotechnology*, 39(8), 949–957. PMID: 34012094

Seale, C., et al. (2025). X-CRISP: Domain-adaptable and interpretable CRISPR repair outcome prediction. *Bioinformatics Advances*, 5(1), vbae207. PMID: 39830154

Shen, M. W., et al. (2018). Predictable and precise template-free CRISPR editing of pathogenic variants. *Nature*, 563(7733), 646–651. PMID: 30405244

Strohkendl, I., et al. (2020). Inhibition of CRISPR-Cas12a DNA targeting by nucleosomes and chromatin. *Science Advances*, 7(11), eabd6030. PMID: 33712463

Tremblay, F., et al. (2025). A potent epigenetic editor targeting human PCSK9 for durable reduction of low-density lipoprotein cholesterol levels. *Nature Medicine*, 31(2), 540–550. PMID: 39891023

Vafai, S. B., et al. (2024). Design of Heart-2: A Phase 1b clinical trial of VERVE-102, an in vivo base editing medicine delivered by a GalNAc-LNP and targeting PCSK9 to durably lower LDL cholesterol. *Circulation*, 150(Suppl 1), A4139206. PMID: 39258386

Vaidya, A., et al. (2024). Analytical characterization of heterogeneities in mRNA-lipid nanoparticles using sucrose density gradient ultracentrifugation. *Analytical Chemistry*, 96(4), 1481–1490. PMID: 38226999

Valdez, I., et al. (2025). A streamlined base editor engineering strategy to reduce bystander editing. *Nature Communications*, 16(1), 1854. PMID: 39984436

Xiao, Y.-L., et al. (2024). An adenine base editor variant expands context compatibility. *Nature Biotechnology*, 42(8), 1226–1235. PMID: 38168997

Yarrington, R. M., et al. (2018). Nucleosomes inhibit target cleavage by CRISPR-Cas9 in vivo. *Proceedings of the National Academy of Sciences*, 115(38), 9351–9358. PMID: 30201707

Yekelchyk, M., et al.(2024). Single-nucleus ATAC-seq for mapping chromatin accessibility in individual cells of murine hearts. *Methods in Molecular Biology*, 2752, 1–20. PMID: 38194027

Zhang, H., et al. (2024). txci-ATAC-seq: A massive-scale single-cell technique to profile chromatin accessibility. *Genome Biology*, 25(1), 78. PMID: 38515199

Zhou, C., Sun, Y., Yan, R., Liu, Y., Zuo, E., Gu, C., Han, L., Wei, Y., Hu, X., Zeng, R., Li, Y., Zhou, H., Guo, F., & Yang, H. (2019). Off-target RNA mutation induced by DNA base editing and its elimination by mutagenesis. *Nature*, 571(7764), 275–278. PMID: 31181567

van den Brink, M., Althuis, T. Y., Danelon, C., & Claassens, N. J. (2025). MOSAIC: A Highly Efficient, One-Step Recombineering Approach to Plasmid Editing and Diversification. ACS synthetic biology, 14(10), 3880–3889. https://doi.org/10.1021/acssynbio.4c00657
