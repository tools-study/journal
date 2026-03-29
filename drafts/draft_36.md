# IPSC Clinical Translation

---

## Abstract

Two decades after Shinya Yamanaka demonstrated that four transcription factors could reprogram somatic cells to pluripotency, induced pluripotent stem cell (iPSC) technology has crossed a decisive translational threshold. As of March 2026, over 115 clinical trials testing 83 distinct human pluripotent stem cell (hPSC)-derived products have been registered worldwide, with more than 1,200 patients having received transplants totaling over 10^11 cells — and no generalizable safety concerns have emerged (Kirkeby, Main, & Carpenter, 2025). On March 6, 2026, Japan's Ministry of Health, Labour and Welfare granted the world's first two conditional approvals for iPSC-derived cell therapies: raguneprocel (AMCHEPRY) for Parkinson's disease and ReHeart iPSC-derived cardiomyocyte sheets for severe ischemic heart failure. These milestones mark the transition of iPSC medicine from experimental to regulatory reality. This review traces the complete clinical translation pipeline — from iPSC generation and banking through directed differentiation, manufacturing scale-up, safety and quality control, to clinical deployment across neurology, diabetes, ophthalmology, cardiology, oncology, and emerging indications. We present five novel mathematical frameworks (F278–F282) spanning stochastic dynamic programming for differentiation protocol optimization, Chapman-Kolmogorov multi-stage yield modeling, multi-type branching processes for mutation accumulation during manufacturing, Bayesian hierarchical acceptance sampling for batch release, and cure-rate mixture survival models for graft persistence. The clinical evidence assembled here — drawn from Phase I/II data in Parkinson's disease showing sustained dopaminergic graft function at 36 months, insulin independence in 83% of type 1 diabetes patients receiving stem cell-derived islets, and two-year stable retinal organoid engraftment — demonstrates that iPSC-derived cell therapies are achieving proof-of-concept efficacy across organ systems. We identify five critical open questions — long-term graft durability, the maturation gap, manufacturing cost reduction, immune tolerance optimization, and regulatory harmonization — whose resolution will determine whether iPSC therapies achieve broad clinical adoption.

---

## 1. Introduction

### 1.1 From Discovery to Clinical Proof-of-Concept

The generation of induced pluripotent stem cells (iPSCs) by retroviral transduction of Oct4, Sox2, Klf4, and c-Myc into mouse fibroblasts (Takahashi & Yamanaka, 2006) and the subsequent extension to human cells (Takahashi et al., 2007) established a new paradigm for regenerative medicine: patient-specific pluripotent cells could, in principle, be generated from any individual, differentiated into any cell type, and transplanted to repair damaged tissues without the ethical constraints of embryonic stem cell derivation. The molecular mechanisms underlying this reprogramming — including sequential chromatin remodeling by pioneer transcription factors, metabolic switching from oxidative phosphorylation to glycolysis, mesenchymal-to-epithelial transition, and telomere elongation — have been comprehensively reviewed by Cerneckis, Cai, and Shi (2024).

The translational arc from this discovery to clinical application has followed a predictable but accelerating trajectory. The first iPSC-derived cell therapy clinical trial was initiated by Masayo Takahashi and colleagues at RIKEN in 2014, transplanting autologous iPSC-derived retinal pigment epithelium (RPE) into a patient with neovascular age-related macular degeneration (AMD) (Mandai et al., 2017). This landmark study demonstrated safety but also exposed the practical challenges of autologous iPSC therapies: the process of deriving, characterizing, and differentiating patient-specific iPSCs required over one year and cost approximately $1 million per patient (Mandai et al., 2017). The field subsequently pivoted toward allogeneic approaches using iPSC lines derived from carefully selected donors, catalyzed by the establishment of clinical-grade iPSC banks such as the Center for iPS Cell Research and Application (CiRA) iPSC Stock Project at Kyoto University (Umekage, Sato, & Fujita, 2019).

By December 2024, the clinical landscape had expanded dramatically: 115 clinical trials with regulatory approval were testing 83 hPSC-derived products, with the majority targeting disorders of the eye, central nervous system, and cancer (Kirkeby et al., 2025). The therapeutic modalities span autologous and allogeneic iPSC-derived neurons, cardiomyocytes, pancreatic islet cells, retinal cells, natural killer (NK) cells, and corneal epithelial cells, reflecting the broad differentiation potential of pluripotent stem cells and the clinical need across organ systems.

### 1.2 Scope and Organization

This review traces the iPSC clinical translation pipeline through six stages: (1) iPSC generation and clinical-grade banking; (2) directed differentiation — the signaling logic that converts pluripotent cells into therapeutically relevant cell types; (3) manufacturing and scale-up for clinical supply; (4) safety assessment and quality control; (5) the clinical trial landscape across indications, with particular depth in neurology; and (6) open questions and future directions. For each stage, we integrate the most recent evidence (through March 2026), develop novel mathematical frameworks where quantitative reasoning illuminates critical bottlenecks, and identify challenges whose resolution will determine whether iPSC medicine achieves its transformative potential.

---

## 2. iPSC Generation and Clinical-Grade Banking

### 2.1 Integration-Free Reprogramming for Clinical Application

The original retroviral reprogramming method (Takahashi & Yamanaka, 2006) is unsuitable for clinical use due to the risk of insertional mutagenesis. Three integration-free methods have emerged as the foundation of clinical-grade iPSC generation, each with distinct advantages. **Sendai virus** vectors, based on a negative-strand RNA virus that replicates exclusively in the cytoplasm, deliver the four Yamanaka factors without any DNA intermediate, eliminating the risk of genomic integration (Fusaki, Ban, Nishiyama, Saeki, & Hasegawa, 2009). Sendai virus yields significantly higher reprogramming success rates compared to episomal methods, as systematically demonstrated by Pozner et al. (2025), though the commercial kit cost (~$11,000 for 6–8 reactions) remains a barrier (Pozner et al., 2025). **Episomal vectors** carrying oriP/EBNA1 elements replicate transiently in human cells and are gradually diluted through cell division, achieving integration-free reprogramming at lower cost (Okita et al., 2011). **Modified mRNA** delivery of reprogramming factors avoids DNA entirely and produces iPSCs with the lowest mutational burden, though the requirement for daily transfections over 2–3 weeks limits scalability (Warren et al., 2010).

A systematic comparison by Pozner et al. (2025) across fibroblasts and lymphoblastoid cell lines found that Sendai virus produced colonies with the highest morphological quality and most consistent transgene silencing, while episomal vectors exhibited a higher frequency of partial reprogramming (Pozner et al., 2025). For clinical manufacturing, the choice of method is increasingly dictated by regulatory jurisdiction and downstream application, with Sendai virus dominating the Japanese clinical pipeline and episomal vectors preferred in several European programs (Martins et al., 2025).

### 2.2 HLA-Homozygous Superdonor Banking

The economic and logistical challenges of autologous iPSC therapies — requiring individualized manufacturing timelines of 6–12 months and per-patient costs exceeding $500,000 — have driven the field toward allogeneic strategies using banked iPSC lines from donors homozygous for common human leukocyte antigen (HLA) haplotypes. An individual homozygous for HLA-A, HLA-B, and HLA-DR presents effectively as a universal partial match, reducing the immune rejection risk for a substantial fraction of the population (Gourraud, Gilson, Girard, & Peschanski, 2012).

The CiRA iPSC Stock Project at Kyoto University has generated 27 iPSC lines from 7 HLA-homozygous donors, providing HLA-matched coverage for approximately 40% of the Japanese population (Umekage et al., 2019). These lines have been used in over 10 clinical trials with no adverse immunological events reported. The global survey by Escriba et al. (2024) identified iPSC haplobank initiatives in Japan, South Korea, the United Kingdom, France (CiTHERA), and Norway (NIBCA), and estimated that a bank of 150 HLA-homozygous iPSC lines could cover approximately 93% of the UK population (Escriba et al., 2024). Zhang et al. (2025) validated a GMP-compliant platform for banking and releasing clinical-grade HLA-homozygous iPSC lines, demonstrating that 3 of 5 candidate lines met all release criteria including high post-thaw survival, normal karyotype, and multilineage differentiation capacity (Zhang et al., 2025).

### 2.3 Quality Standards and Regulatory Requirements

The manufacture of iPSC master cell banks for clinical use requires compliance with Good Manufacturing Practice (GMP) standards that vary across jurisdictions. Martins et al. (2025) conducted a comprehensive comparison of EU (EMA) and US (FDA) requirements for iPSC master cell bank manufacture, identifying key areas requiring harmonization: residual vector testing for Sendai virus, identity testing standards, purity specifications, and stability programs (Martins et al., 2025). Japan's Pharmaceuticals and Medical Devices Agency (PMDA) has established the most developed regulatory framework for iPSC therapies, leveraging the 2014 Act on the Safety of Regenerative Medicine to create an accelerated conditional approval pathway (Konomi et al., 2025).

**Challenge: Genetic drift during prolonged culture.** Extended passaging of iPSCs introduces somatic mutations at a rate of approximately 0.5–1.3 single-nucleotide variants per genome per population doubling, with recurrent gain-of-function mutations in TP53, BCOR, and other cancer-associated genes conferring selective growth advantages (Merkle et al., 2017). This necessitates rigorous genomic integrity monitoring at multiple passage levels, a challenge we quantify mathematically in Section 5. The 2025 ISCBI/ISCI Joint Workshop on genetic stability recommended routine high-coverage WGS with standardized interpretation pipelines, long-term expansion tests to expose rare mutant subclones, and DNA barcoding combined with genomic and phenotypic assays for clonal monitoring — establishing a community consensus on monitoring standards that is likely to influence regulatory requirements in all major jurisdictions.

### 2.4 Autologous Versus Allogeneic: The Strategic Tradeoff

The choice between autologous and allogeneic iPSC strategies involves a fundamental tradeoff between immunological compatibility and manufacturing efficiency. Autologous iPSC-derived products — personalized from the patient's own cells — eliminate immune rejection risk entirely, as demonstrated by the Aspen Neuroscience ASPIRO trial in which patients required no immunosuppression (Aspen Neuroscience, 2026). However, autologous manufacturing requires 6–12 months of individualized production, costs $500,000–$1,000,000 per patient, and introduces quality control challenges: each manufacturing batch is unique, precluding the batch-to-batch consistency that underpins pharmaceutical quality assurance (Iriguchi et al., 2024).

Allogeneic strategies using banked iPSC lines from HLA-homozygous donors enable batch manufacturing of hundreds of patient doses, dramatically reducing cost and enabling quality control testing on representative samples from each batch. However, even HLA-matched allogeneic cells elicit some degree of immune recognition through minor histocompatibility antigens, necessitating transient immunosuppression (typically 6–15 months of tacrolimus) in most current clinical protocols (Sawamoto et al., 2025; Kirkeby et al., 2025). The hypoimmune (HIP) approach — exemplified by Sana Biotechnology's B2M^-/-^ CIITA^-/-^ CD47^+^ iPSC platform — seeks to eliminate this requirement through genetic engineering of immune evasion, with proof-of-concept demonstrated in a single T1D patient (Sana Biotechnology, 2025). Whether HIP cells maintain long-term graft tolerance without immunosuppression — and whether the absence of HLA class I expression creates vulnerability to NK cell-mediated killing despite CD47 overexpression — are questions that can only be answered by multi-year clinical follow-up.

---

## 3. Directed Differentiation: The Signaling Logic of Cell Fate Specification

### 3.1 The Grammar of Developmental Signaling

Directed differentiation recapitulates embryonic development in a dish, deploying sequential combinations of morphogens and small-molecule agonists/antagonists to guide iPSCs through developmental intermediates toward a target cell type. The signaling grammar is organized around a core set of pathways — Wnt, BMP, FGF, Sonic hedgehog (SHH), retinoic acid (RA), and Notch — whose temporal activation or inhibition specifies germ layer, regional identity, and terminal cell fate (Cerneckis et al., 2024). The key insight enabling clinical-scale differentiation was the recognition that small molecules can substitute for recombinant growth factors at a fraction of the cost: CHIR99021 (GSK3β inhibitor) activates Wnt signaling, dorsomorphin and LDN193189 inhibit BMP, SB431542 inhibits TGF-β/Activin/Nodal, purmorphamine activates SHH, and all-trans retinoic acid provides direct RA pathway activation (Chambers et al., 2009).

### 3.2 Key Differentiation Protocols by Lineage

**Midbrain dopaminergic neurons** for Parkinson's disease are generated through a floor plate intermediate strategy. Dual SMAD inhibition (LDN193189 + SB431542) specifies neuroectoderm, followed by SHH agonism (purmorphamine or SHH-C24II) and GSK3β inhibition (CHIR99021) to pattern floor plate progenitors expressing FOXA2 and LMX1A, then FGF8 and brain-derived neurotrophic factor (BDNF) to mature dopaminergic neurons expressing tyrosine hydroxylase (TH) and NURR1 (Kriks et al., 2011). This protocol, refined over a decade, produces the cells used in the BlueRock and CiRA clinical trials (Kirkeby et al., 2025; Sawamoto et al., 2025).

**Pancreatic beta cells** are differentiated through a six-stage protocol mimicking pancreatic organogenesis: definitive endoderm (Activin A + CHIR99021), primitive gut tube (FGF10 + KGF), posterior foregut (RA + SHH inhibition), pancreatic progenitor (EGF + nicotinamide), endocrine precursor (ALK5 inhibitor + γ-secretase inhibitor), and mature beta cell (T3 thyroid hormone) (Pagliuca et al., 2014). Pagliuca et al. (2014) achieved glucose-responsive insulin secretion in vitro, and this protocol — further optimized by Vertex Pharmaceuticals — produced the stem cell-derived islets (zimislecel/VX-880) that achieved insulin independence in 83% of patients in the FORWARD trial (Reichman et al., 2025).

**Cardiomyocytes** are differentiated through a biphasic Wnt modulation protocol: Wnt activation (CHIR99021) during days 0–1 induces mesoderm, followed by Wnt inhibition (IWP2 or IWR-1) during days 3–5 to specify cardiac mesoderm, producing spontaneously beating cardiomyocytes by day 8–10 (Lian et al., 2013). The simplicity of this two-step protocol has facilitated manufacturing scale-up for clinical products including Heartseed HS-001 and Cuorips ReHeart.

**Retinal pigment epithelium** can be generated by spontaneous differentiation of iPSC colonies with pigmented foci selection, or by directed protocols using BMP and Wnt inhibition to specify anterior neuroectoderm followed by Activin A to induce RPE fate (Mandai et al., 2017). RPE cells are among the most straightforward iPSC derivatives to manufacture due to their characteristic pigmentation and cobblestone morphology, enabling visual quality control.

**Natural killer cells** are differentiated through hemogenic endothelium intermediates using a feeder-free protocol: mesoderm induction (BMP4 + VEGF + bFGF), hemogenic endothelium specification (SCF + FLT3L), and NK maturation (IL-15 + IL-21) (Cichocki et al., 2020). This protocol underlies the Century Therapeutics and Fate Therapeutics iPSC-NK clinical programs.

### 3.3 Induced Proliferation and Differentiation of Neural Precursor Cells

A critical determinant of therapeutic success in neurological applications is the capacity to expand neural precursor cells (NPCs) to clinically relevant numbers while maintaining their differentiation potential. Younsi et al. (2020) demonstrated that a combination of three growth factors — epidermal growth factor (EGF), fibroblast growth factor-2 (FGF-2), and platelet-derived growth factor-AB (PDGF-AB) — synergistically induces proliferation and differentiation of neural precursor cells derived from the adult rat spinal cord (Younsi et al., 2020). EGF and FGF-2 drive NPC self-renewal through activation of the MAPK/ERK and PI3K/AKT signaling cascades, while PDGF-AB promotes differentiation toward oligodendrocyte and neuronal lineages through PDGFRα signaling (Younsi et al., 2020). Crucially, NPC transplantation into a rat spinal cord injury model demonstrated functional recovery — improved locomotor scores and reduced lesion volume — only when cells had been pre-treated with all three growth factors, establishing that the in vitro expansion and priming conditions directly determine in vivo therapeutic efficacy (Younsi et al., 2020).

This growth factor triad paradigm extends to iPSC-derived NPCs. The transition from pluripotency to neural progenitor identity involves a proliferative expansion phase during which NPCs undergo 10–20 population doublings while maintaining multipotency — the capacity to differentiate into neurons, astrocytes, and oligodendrocytes. The balance between proliferation and premature differentiation during this expansion phase is regulated by the Notch signaling pathway: high Notch activity (maintained by the γ-secretase-dependent release of the Notch intracellular domain, NICD) sustains NPC self-renewal by activating HES1/HES5 transcriptional repressors that suppress proneural genes such as ASCL1 and NEUROG2, while Notch pathway attenuation — achieved by γ-secretase inhibitors (DAPT) or Dll1/4 ligand withdrawal — permits exit from the progenitor state and commitment to neuronal differentiation (Chambers et al., 2009). The precise timing of this proliferation-to-differentiation switch is a critical manufacturing variable: premature differentiation reduces final cell yields, while prolonged proliferation risks acquisition of tumorigenic mutations (as quantified in Section 5.4).

For the Keio University SCI trial, iPSC-derived NS/PCs were expanded in the presence of EGF and FGF-2 in suspension neurosphere culture, generating clinically relevant cell numbers (>2 × 10^6 per patient) while maintaining the capacity for trilineage differentiation (Sugai et al., 2021). Quality control assays at the time of transplantation confirmed that expanded NS/PCs expressed the neural progenitor markers SOX1, PAX6, and Nestin, while lacking expression of the pluripotency markers OCT4 and NANOG — demonstrating complete loss of residual pluripotency during the expansion process.

### 3.4 Single-Cell Trajectory Analysis and Protocol Optimization

A persistent challenge in directed differentiation is the heterogeneity of output cell populations. Li et al. (2024) applied single-cell RNA sequencing to 32,365 cells at four stages of iPSC-to-cardiomyocyte differentiation, using RNA velocity analysis to reconstruct the differentiation trajectory and SCENIC network inference to identify CREG and NR2F2 as key regulators of cardiomyocyte maturation (Li et al., 2024). Such analyses reveal off-target populations — including fibroblast-like cells, endothelial cells, and uncommitted progenitors — that contaminate the final product and reduce therapeutic potency.

Machine learning approaches are increasingly applied to predict and optimize differentiation outcomes. Hojo et al. (2025) developed a non-destructive imaging-based ML pipeline that extracts fast Fourier transform features from phase-contrast images of differentiating iPSC cultures, achieving early prediction of differentiation efficiency approximately 50 days before conventional marker-based assessment (Hojo et al., 2025). Deep learning models trained on brightfield live-cell images can perform real-time cell-type recognition during differentiation, enabling automated process control (Kato et al., 2026). These approaches transform differentiation from empirical recipe-following to predictive, closed-loop optimization.

### 3.5 Framework F278: Bellman Stochastic Dynamic Programming for Optimal Differentiation Protocol Sequencing

Directed differentiation can be formalized as a stochastic sequential decision problem. At each differentiation stage $k \in \{0, 1, \ldots, K\}$, the cell population occupies a distribution across $m$ lineage states described by the state vector:

```math
\mathbf{s}_k = (p_{k,1}, p_{k,2}, \ldots, p_{k,m}), \quad \sum_{i=1}^{m} p_{k,i} = 1
```

where $p_{k,i}$ denotes the fraction of cells in lineage state $i$ at stage $k$. At each stage, the experimentalist selects an action $a_k \in \mathcal{A}$ — a specific combination of signaling factors at defined concentrations and durations. The system transitions stochastically according to:

```math
\mathbf{s}_{k+1} \sim P(\mathbf{s}_{k+1} \mid \mathbf{s}_k, a_k)
```

where $P$ is the transition kernel estimated from single-cell trajectory data. The terminal reward is the fraction of cells in the target lineage state $T$ at the final stage $K$, minus the cumulative cost of signaling factors:

```math
R = p_{K,T} - \sum_{k=0}^{K-1} c(a_k)
```

where $c(a_k)$ is the cost of action $a_k$. The optimal value function $V^*(\mathbf{s}_k)$ satisfies the **Bellman equation**:

```math
V^*(\mathbf{s}_k) = \max_{a_k \in \mathcal{A}} \left[ -c(a_k) + \gamma \sum_{\mathbf{s}_{k+1}} P(\mathbf{s}_{k+1} \mid \mathbf{s}_k, a_k) \, V^*(\mathbf{s}_{k+1}) \right]
```

where $\gamma \in (0,1]$ is a discount factor reflecting the time-value of earlier commitment to the target lineage. The optimal policy $\pi^*(\mathbf{s}_k) = \arg\max_{a_k} [\cdot]$ prescribes the signaling cocktail at each stage given the current cell population composition. This framework generalizes empirical protocol optimization: instead of testing individual factor combinations in isolation, it identifies globally optimal multi-stage strategies that account for the stochastic and path-dependent nature of cell fate decisions. The transition kernel $P$ can be estimated from large-scale single-cell RNA-seq datasets spanning multiple differentiation conditions, making this a data-driven rather than hypothesis-driven approach to protocol design.

---

## 4. Manufacturing and Scale-Up

### 4.1 Bioreactor Systems for Clinical-Scale Production

The transition from research-scale differentiation in static culture plates to clinical-scale production of billions of cells requires bioreactor systems that provide controlled nutrient delivery, gas exchange, and shear stress management. Three principal bioreactor architectures have been adapted for iPSC-derived cell manufacturing: **stirred-tank bioreactors** using impeller-driven mixing, **rocking/wave bioreactors** that provide gentle agitation through platform oscillation, and **vertical-wheel bioreactors** that combine low-shear mixing with efficient mass transfer (Kropp, Massai, & Zweigerdt, 2017).

Dadheech et al. (2025) demonstrated successful 5-fold scale-up of iPSC-derived islet production from 0.1L to 0.5L vertical-wheel bioreactors, achieving a 12-fold increase in islet equivalent count (183,002 IEQs per batch) with approximately 63% of cells co-expressing the beta cell markers C-peptide, NKX6.1, and ISL1, and glucose-responsive insulin release with 3.9–6.1-fold stimulation indices (Dadheech et al., 2025). Transplantation of bioreactor-produced islets reversed diabetes in streptozotocin-treated mice, providing preclinical validation of the manufacturing process (Dadheech et al., 2025).

For iPSC expansion prior to differentiation, suspension culture of iPSC aggregates in stirred-tank bioreactors enables production of 10^9–10^10 cells per batch, sufficient for multiple patient doses. Critical process parameters include dissolved oxygen tension (maintained at 20–30% for pluripotency, reduced to 5% for certain differentiation protocols), impeller speed (balancing mixing efficiency against shear-induced cell death), and glucose/lactate ratio (reflecting metabolic health of the culture) (Kropp et al., 2017).

### 4.2 Cryopreservation of Cell Therapy Products

Clinical iPSC-derived cell therapies must be cryopreserved to enable quality control testing, shipping, and on-demand administration at clinical sites. Dobruskin et al. (2025) conducted a systematic review of cryopreservation practices across clinical and preclinical iPSC-based therapies, finding pervasive reliance on dimethyl sulfoxide (DMSO) as the cryoprotective agent despite its known cytotoxicity at physiological temperatures (Dobruskin et al., 2025). The development of DMSO-free cryopreservation media — including synthetic, animal-origin-free formulations — is an urgent priority for off-the-shelf cell therapy products (Dobruskin, Levin, Benny, & Bhatt, 2024). Post-thaw viability and functionality vary substantially across cell types: iPSC-derived cardiomyocytes retain spontaneous beating activity after cryopreservation, while iPSC-derived neurons show greater sensitivity to freeze-thaw damage, requiring optimized cooling rates and ice nucleation control (Dobruskin et al., 2025).

### 4.3 Cost-of-Goods and Access

The current cost of iPSC-derived cell therapies ranges from approximately $200,000 to over $500,000 per patient, driven primarily by labor-intensive manufacturing, expensive recombinant growth factors, and the requirement for extensive quality control testing. Industrial-scale manufacturing using automated bioreactor platforms, synthetic small-molecule differentiation protocols, and streamlined quality control assays could reduce cost-of-goods by up to 95% compared to current autologous manufacturing baselines, with unit economics most sensitive to batch yield and facility utilization (Iriguchi et al., 2024). The transition from labor-driven to materials-driven cost structures at commercial scale suggests that iPSC-derived therapies could eventually approach the cost range of conventional biologics ($10,000–$50,000), though this requires manufacturing volumes that presuppose broad clinical adoption — a classic chicken-and-egg problem for the field.

### 4.4 Framework F279: Chapman-Kolmogorov Multi-Stage Differentiation Yield Model

iPSC-to-target-cell differentiation proceeds through $N$ discrete stages, each with a conversion efficiency $e_i$ (fraction of cells that transition to the correct next-stage identity) and a loss fraction $\ell_i$ (fraction lost to apoptosis, off-target differentiation, or mechanical damage). Starting from an initial iPSC population of $n_0$ cells, the expected number of target cells after the complete protocol is:

```math
\bar{n}_K = n_0 \prod_{i=1}^{N} e_i (1 - \ell_i)
```

For a representative dopaminergic neuron protocol with $N = 4$ stages (neuroectoderm, floor plate, DA progenitor, mature DA neuron), typical stage efficiencies are $e_1 = 0.95$, $e_2 = 0.80$, $e_3 = 0.70$, $e_4 = 0.60$, with loss fractions $\ell_i \approx 0.05$ at each stage. The cumulative yield is therefore:

```math
Y = \prod_{i=1}^{4} e_i(1-\ell_i) = 0.95 \times 0.80 \times 0.70 \times 0.60 \times (0.95)^4 \approx 0.260
```

indicating that approximately 26% of starting iPSCs become target cells — necessitating starting populations of $\sim 4 \times$ the desired final cell number. The variance of the yield, propagated through the multiplicative stages via the delta method, is:

```math
\text{Var}(Y) \approx Y^2 \sum_{i=1}^{N} \left[\frac{\text{Var}(e_i)}{e_i^2} + \frac{\text{Var}(\ell_i)}{(1-\ell_i)^2}\right]
```

This framework quantifies the bottleneck stages — those with the lowest $e_i$ or highest $\ell_i$ — and directs optimization effort toward the stages contributing most to yield variance. For the dopaminergic neuron protocol, the final maturation stage ($e_4 = 0.60$) is the dominant bottleneck, consistent with the clinical observation that achieving functionally mature DA neurons remains the most challenging differentiation step (Kirkeby et al., 2025).

---

## 5. Safety and Quality Control

### 5.1 Tumorigenicity Risk: TP53 Mutations and Residual Undifferentiated Cells

The two principal safety concerns for iPSC-derived cell therapies are: (1) somatic mutations acquired during reprogramming and culture, particularly in tumor suppressor genes; and (2) residual undifferentiated iPSCs in the final product that could form teratomas after transplantation.

Merkle et al. (2017) demonstrated that human pluripotent stem cell cultures recurrently acquire dominant-negative TP53 mutations, with mutant clones expanding due to selective growth advantage under culture stress conditions (Merkle et al., 2017). TP53-mutant iPSCs show impaired apoptosis, resistance to DNA damage, and altered differentiation kinetics — particularly reduced neural induction efficiency — raising concerns about both safety and product quality (Merkle et al., 2017). The FDA's 2024 draft guidance recommends whole-genome sequencing (WGS) at ≥50× coverage for cytogenetic screening and cancer-associated mutation reporting in iPSC-derived cell therapy products.

Watanabe et al. (2025) published a consensus recommendation from the Health and Environmental Sciences Institute (HESI) International Cell Therapy Committee for evaluating teratoma formation risk, establishing that digital PCR and highly efficient culture assays achieve superior detection sensitivity for residual undifferentiated cells compared to conventional flow cytometry (Watanabe et al., 2025). The framework recommends a tiered approach: Level 1 (in-process testing for pluripotency markers during differentiation), Level 2 (final product quantitative PCR for LIN28A, NANOG, and OCT4), and Level 3 (in vivo teratoma assay in immunodeficient mice for first-in-human applications) (Watanabe et al., 2025).

### 5.2 Strategies for Eliminating Residual Pluripotent Cells

Multiple strategies have been developed to remove or kill residual undifferentiated cells from iPSC-derived products. Yazdani Movahed et al. (2025) comprehensively reviewed these approaches, categorizing them as: (1) insertional genetic kill switches (e.g., herpes simplex virus thymidine kinase under the NANOG promoter); (2) non-insertional approaches (miRNA switches that selectively trigger apoptosis in cells expressing pluripotency-associated miRNA profiles); (3) protein-based methods (antibody-drug conjugates targeting SSEA-5 or TRA-1-60); (4) culture media modification (selective survival of differentiated cells under serum-free conditions); and (5) physical separation methods (Yazdani Movahed et al., 2025).

Nguyen et al. (2024) developed a microfluidic device achieving label-free, high-throughput depletion of OCT4-positive undifferentiated cells from iPSC-derived spinal cord progenitor populations at processing rates exceeding 3 million cells per minute, without affecting the viability or functionality of differentiated cells (Nguyen et al., 2024). This approach addresses a critical manufacturing bottleneck: conventional magnetic-activated cell sorting (MACS) requires expensive antibodies and introduces dead volumes that reduce yield, while microfluidic size-based separation exploits the morphological differences between undifferentiated iPSCs (smaller, rounder) and differentiated progeny (larger, more elongated) (Nguyen et al., 2024).

### 5.3 Regulatory Frameworks

The regulation of iPSC-derived cell therapies reflects three distinct philosophical approaches across major jurisdictions. **Japan's PMDA** has been the global first mover, implementing a conditional approval framework under the 2014 Act on the Safety of Regenerative Medicine that permits marketing authorization based on limited efficacy data from small trials, with post-approval surveillance requirements (Konomi et al., 2025). This framework enabled the March 2026 approvals of AMCHEPRY and ReHeart on the basis of Phase I/II data from 7–8 patients per product. The **US FDA** has established the Regenerative Medicine Advanced Therapy (RMAT) designation, providing accelerated development support for iPSC therapies that address serious conditions; as of January 2026, iRegene's NouvNeu001 iPSC-derived dopaminergic progenitor cells became the first iPSC therapy globally to hold both RMAT and Fast Track designations for Parkinson's disease. The **EMA** classifies iPSC-derived products as Advanced Therapy Medicinal Products (ATMPs), subject to the requirements of Regulation (EC) No 1394/2007, with updated guidelines on quality, non-clinical, and clinical requirements coming into effect in July 2025.

The ICH Cell and Gene Therapy Discussion Group (CGTDG) endorsed a strategic framework for global regulatory harmonization in November 2025, focused on standardizing requirements for ex vivo genetically modified cell-based products — a category that encompasses most iPSC-derived therapies.

### 5.4 Framework F280: Multi-Type Galton-Watson Branching Process for Mutation Accumulation During iPSC Expansion

During iPSC expansion, cells acquire mutations of different types — single-nucleotide variants (SNVs), copy number variants (CNVs), and loss-of-heterozygosity (LOH) events — with distinct rates and fitness consequences. We model this as a multi-type Galton-Watson branching process with three types: wild-type (W), SNV-carrying (S), and CNV-carrying (C). The mean offspring matrix is:

```math
\mathbf{M} = \begin{pmatrix} 2(1 - \mu_s - \mu_c) & 2\mu_s & 2\mu_c \\ 0 & 2(1 + s_s) & 0 \\ 0 & 0 & 2(1 + s_c) \end{pmatrix}
```

where $\mu_s \approx 1.0 \times 10^{-9}$ per base per division is the SNV mutation rate, $\mu_c \approx 5 \times 10^{-7}$ per genome per division is the CNV rate, $s_s$ is the selective advantage conferred by fitness-enhancing SNVs (e.g., dominant-negative TP53 mutations, with $s_s \approx 0.05$–$0.15$ per generation based on clonal competition assays), and $s_c$ is the selective advantage of CNV-carrying cells. Starting from a single wild-type iPSC clone, after $n$ population doublings the expected number of SNV-carrying cells is:

```math
\mathbb{E}[N_S(n)] = \frac{2\mu_s \cdot 2^n}{2(1+s_s) - 2} \left[2^n(1+s_s)^n - 2^n\right] = \frac{\mu_s \cdot 2^n}{s_s}\left[(1+s_s)^n - 1\right]
```

The expected fraction of mutant cells after $n$ doublings (total population $\approx 2^n$) is:

```math
f_S(n) \approx \frac{\mu_s}{s_s}\left[(1+s_s)^n - 1\right]
```

For a TP53 mutation with $s_s = 0.10$ and $\mu_s = 1.0 \times 10^{-9}$ over the $\sim 3 \times 10^9$ base-pair genome, the probability of at least one TP53 mutation arising is approximately $\mu_{\text{TP53}} \approx 3 \times 10^{-6}$ per division per cell. Over $n = 30$ population doublings (expansion from a single clone to $\sim 10^9$ cells), the expected mutant fraction becomes detectable by deep sequencing when it exceeds the variant allele frequency detection threshold of $\sim 1\%$. Setting $f_S(n) = 0.01$ and solving for $n$ yields the **critical passage number**:

```math
n^* = \frac{\ln\left(1 + \frac{0.01 \cdot s_s}{\mu_{\text{TP53}}}\right)}{\ln(1 + s_s)}
```

which, for the parameters above, gives $n^* \approx 35$ doublings. This provides a quantitative rationale for limiting the expansion of clinical iPSC lines to fewer than 30–35 population doublings from the master cell bank — consistent with empirical safety guidelines — and for performing WGS at multiple passage levels to detect expanding mutant clones before they exceed the detection threshold.

### 5.5 Framework F281: Bayesian Hierarchical Acceptance Sampling for Batch Release Quality Control

Manufacturing iPSC-derived cell products generates batch-to-batch variability in quality attributes (viability, purity, potency, genomic integrity). A Bayesian hierarchical model captures both between-batch and within-batch variation, providing a principled framework for batch release decisions.

Let $\theta_i$ denote the true quality parameter (e.g., fraction of target cells) for batch $i$. The between-batch distribution is:

```math
\theta_i \sim \text{Beta}(\alpha, \beta)
```

Within each batch, $n$ cells are sampled and $x$ are found to meet the quality specification:

```math
x_i \mid \theta_i \sim \text{Binomial}(n_i, \theta_i)
```

The posterior distribution of $\theta_i$ given the observed data is:

```math
\theta_i \mid x_i \sim \text{Beta}(\alpha + x_i, \beta + n_i - x_i)
```

The batch release decision is: release batch $i$ if and only if:

```math
P(\theta_i > \theta_{\min} \mid x_i) = 1 - I_{\theta_{\min}}(\alpha + x_i, \beta + n_i - x_i) > 1 - \alpha_{\text{risk}}
```

where $\theta_{\min}$ is the minimum acceptable quality threshold (e.g., $\theta_{\min} = 0.90$ for 90% target cell purity), $\alpha_{\text{risk}}$ is the acceptable risk level (e.g., 0.05), and $I_x(a,b)$ is the regularized incomplete beta function. The hyperparameters $\alpha$ and $\beta$ are estimated from historical batch data using empirical Bayes, encoding the manufacturing process's "track record" into the release criterion. This framework adapts as manufacturing matures: early batches (high prior uncertainty) require larger sample sizes and more stringent testing, while established processes (tight prior) can qualify batches with fewer samples, reducing quality control costs without compromising safety.

---

## 6. Clinical Trial Landscape

### 6.1 Neurology

#### 6.1.1 Parkinson's Disease: iPSC-Derived Dopaminergic Neuron Transplantation

Parkinson's disease (PD) — caused by the selective degeneration of dopaminergic neurons in the substantia nigra pars compacta — is the paradigmatic indication for iPSC-derived cell therapy, as the therapeutic goal (replacement of a single, well-defined neuronal subtype in a circumscribed anatomical location) aligns precisely with the capabilities of directed differentiation and stereotactic neurosurgery. Three landmark clinical trials have reported results between 2020 and 2026.

**BlueRock Therapeutics/Bayer — Bemdaneprocel (BRT-DA01).** Kirkeby et al. (2025) reported the results of the Phase I open-label trial (NCT04802733) of bemdaneprocel, an hESC-derived dopaminergic neuron product. Twelve patients with moderate PD received bilateral putaminal grafts at two dose levels (0.9 million cells, n = 6; 2.7 million cells, n = 6), with one year of tacrolimus immunosuppression. At 18 months, no serious adverse events, no graft-induced dyskinesias, and no tumor formation were observed (Kirkeby et al., 2025). The high-dose cohort showed a clinically meaningful improvement of 22.5 points on the MDS-UPDRS Part III motor score in the OFF-medication state at 24 months (Kirkeby et al., 2025). Critically, ^18^F-DOPA positron emission tomography (PET) imaging demonstrated increased dopaminergic uptake in the grafted putamen, confirming graft survival and functional dopamine production (Kirkeby et al., 2025). Extended 36-month follow-up data confirmed sustained improvement: high-dose cohort MDS-UPDRS III OFF improvement of -17.9 points, low-dose -13.5 points. Bemdaneprocel holds both RMAT and Fast Track designations from the FDA. A pivotal Phase III trial (exPDite-2, NCT06943522) enrolled its first patient in September 2025, targeting approximately 102 patients in a double-blind, sham-controlled design with a primary endpoint at 78 weeks.

**CiRA/Kyoto University/Sumitomo Pharma — Raguneprocel (AMCHEPRY).** Sawamoto, Doi, and Takahashi (2025) reported the Phase I/II trial of iPSC-derived dopaminergic progenitor cells — the world's first clinical trial of allogeneic iPSC-derived neurons. Seven patients received bilateral striatal transplants at two dose levels (2.1–2.6 million cells per hemisphere, n = 3; 5.3–5.5 million, n = 4) with 15 months of tacrolimus immunosuppression (Sawamoto et al., 2025). Of 73 adverse events recorded, 72 were mild; no serious adverse events were attributed to the cell product. Four of six evaluable patients showed improvement of up to 20% on the MDS-UPDRS Part III OFF score, and ^18^F-DOPA PET revealed a 44.7% increase in putaminal dopaminergic uptake at 24 months — providing direct evidence of graft-derived dopamine synthesis in the human brain (Sawamoto et al., 2025). No tumor formation was detected on serial MRI through 24 months. On March 6, 2026, Japan's MHLW granted conditional approval for AMCHEPRY (raguneprocel), making it the world's first approved iPSC-derived cell therapy. A 75-patient post-approval outcomes study is required, with commercial launch expected in fall 2026.

**Aspen Neuroscience — Sasineprocel (ANPD001).** The ASPIRO Phase 1/2a trial is evaluating autologous iPSC-derived dopaminergic neuron precursor cells, eliminating the need for immunosuppression. Twelve-month data presented at the AD/PD 2026 International Conference showed MDS-UPDRS Part III OFF improvements of -15.5 points (low dose) and -13.5 points (high dose), with an increase in daily ON time of 2.1–2.4 hours (Aspen Neuroscience, 2026). No graft-induced dyskinesias or serious surgical adverse events were reported. A commercial formulation cohort was initiated in September 2025, with Phase III planning for late 2026.

**Proof-of-concept precedent.** The first autologous iPSC-derived dopaminergic neuron transplant was performed by Schweitzer et al. (2020) in a single PD patient, demonstrating safety and PET-confirmed graft survival at 24 months (Schweitzer et al., 2020). This foundational study validated the feasibility of personalized iPSC-derived neuron replacement, though the prolonged manufacturing timeline highlighted the practical advantages of allogeneic approaches for broader clinical deployment.

**Comparative analysis of dopaminergic neuron trials.** The three programs represent fundamentally different strategies for cell sourcing and immune management. BlueRock uses hESC-derived neurons (not iPSC), avoiding the reprogramming step entirely but requiring immunosuppression; CiRA/Sumitomo uses allogeneic iPSC-derived neurons from HLA-matched donors, requiring transient immunosuppression; and Aspen uses autologous iPSC-derived neurons, eliminating immunosuppression entirely at the cost of longer manufacturing timelines and higher per-patient expense. The convergence of efficacy signals across all three approaches — MDS-UPDRS III OFF improvements of 13–23 points at 12–36 months — is notable, suggesting that the biological substrate (dopaminergic progenitor cells produced by related floor plate protocols) rather than the source platform is the primary determinant of clinical outcome. The ^18^F-DOPA PET evidence of graft-derived dopamine synthesis is particularly significant: the 44.7% increase in putaminal uptake observed by Sawamoto et al. (2025) and the qualitatively similar increases in the BlueRock trial (Kirkeby et al., 2025) confirm that transplanted cells integrate into host circuitry and perform their intended function, addressing a concern that had persisted since the mixed results of fetal ventral mesencephalic tissue transplantation in the 1990s and 2000s.

The regulatory divergence is equally instructive. Japan's conditional approval of AMCHEPRY on the basis of 7-patient Phase I/II data reflects the PMDA's risk-benefit calculus for a progressive, debilitating disease with no disease-modifying therapy, while the FDA is requiring a 102-patient, sham-controlled Phase III trial for bemdaneprocel — a design that will generate more definitive efficacy evidence but delays patient access by 3–5 years. Both approaches have merit, and the accumulating safety and efficacy data from the Japanese clinical experience will inform the global regulatory strategy.

**Challenges specific to dopaminergic neuron replacement.** Several fundamental biological questions remain unresolved. First, the optimal cell maturation state at the time of transplantation is debated: more mature DA neurons may integrate faster but survive transplantation less well than less mature progenitors, which have greater plasticity but risk delayed or incomplete maturation in vivo (Kirkeby et al., 2025). Second, the extent to which transplanted neurons form synaptic connections with host striatal medium spiny neurons — and whether these connections are functionally appropriate rather than merely anatomically present — cannot be determined from PET imaging alone and awaits long-term clinical and post-mortem studies. Third, the risk of alpha-synuclein propagation from host to graft — documented in fetal tissue transplants at 14–24 years post-transplantation (Li et al., 2016) — raises the question of whether iPSC-derived neurons will eventually succumb to the same degenerative process they were transplanted to replace. Fourth, the relationship between cell dose, graft distribution, and clinical outcome is not yet optimized: both the BlueRock and CiRA trials used bilateral putaminal delivery, but whether additional injection sites (caudate nucleus, substantia nigra) would improve outcomes is unknown.

#### 6.1.2 Spinal Cord Injury

Keio University has conducted a Phase I/II trial of iPSC-derived neural stem/progenitor cells (NS/PCs) for subacute spinal cord injury (SCI), transplanting over 2 million cells into four patients with complete motor-sensory paralysis (AIS-A) within 14–28 days of injury (Sugai et al., 2021). Preliminary results reported in 2025 indicated that 2 of 4 patients showed motor function improvement, with one patient improving from AIS-A (complete paralysis) to AIS-D (able to stand unassisted and practice walking). No serious adverse events were observed at one-year follow-up. These results build on preclinical evidence demonstrating that growth factor-treated neural precursor cells support both proliferation and differentiation in vitro and functional recovery after transplantation in vivo (Younsi et al., 2020).

#### 6.1.3 Emerging Neurological Indications

Beyond PD and SCI, iPSC-derived cell therapies are advancing toward clinical evaluation for several additional neurological disorders.

**Amyotrophic lateral sclerosis (ALS).** iPSC-derived astrocyte progenitors represent a promising approach for ALS, based on the non-cell-autonomous hypothesis that astrocytic dysfunction contributes to motor neuron degeneration. Astrocytes derived from ALS patient iPSCs recapitulate disease-relevant phenotypes in vitro, including reduced lactate secretion and gain of toxic function toward co-cultured motor neurons, validating them as both disease models and therapeutic targets. Clinical programs are evaluating intrathecal delivery of healthy iPSC-derived astrocyte progenitors to provide trophic support and correct the toxic astrocyte microenvironment. Separately, iPSC-derived motor neuron progenitors are being explored for direct replacement, though the challenge of establishing long-range axonal connections from transplanted neurons to peripheral muscle targets makes this approach substantially more difficult than the focal replacement strategy in Parkinson's disease.

**Epilepsy.** Medial ganglionic eminence (MGE)-type GABAergic interneuron progenitors derived from iPSCs can differentiate into parvalbumin-positive and somatostatin-positive interneurons after transplantation, restoring inhibitory tone in seizure-generating circuits. Preclinical studies in rodent models of temporal lobe epilepsy have demonstrated seizure reduction following iPSC-derived interneuron transplantation into the hippocampus. The specificity of this approach — targeting the inhibitory deficit that underlies many focal epilepsy syndromes — offers an advantage over pharmacological approaches that broadly modulate neurotransmission.

**Stroke.** iPSC-derived neural progenitor cells transplanted into the peri-infarct region can enhance neuroplasticity through paracrine mechanisms — secretion of neurotrophic factors including BDNF, GDNF, and VEGF — rather than through direct neuronal replacement. This trophic support paradigm is more achievable than circuit reconstruction and may synergize with rehabilitation-driven plasticity in the chronic stroke setting.

**iRegene — NouvNeu001.** In January 2026, iRegene's iPSC-derived dopaminergic progenitor product (NouvNeu001) became the first iPSC therapy globally to receive both RMAT and Fast Track designations from the FDA, reflecting the regulatory momentum behind cell replacement strategies for Parkinson's disease and establishing a potential additional entrant into the expanding PD cell therapy landscape.

### 6.2 Type 1 Diabetes

**Vertex Pharmaceuticals — Zimislecel (VX-880).** Reichman et al. (2025) reported Phase 1/2 results from the FORWARD trial, in which 12 patients with type 1 diabetes (T1D) and impaired hypoglycemia awareness received a single portal vein infusion of 0.8 × 10^9 stem cell-derived, fully differentiated islet cells (zimislecel) under chronic immunosuppression (Reichman et al., 2025). Ten of twelve patients (83%) achieved insulin independence at day 365, with all 12 patients free of severe hypoglycemic events, HbA1c below 7%, and time-in-range exceeding 70% (Reichman et al., 2025). All patients demonstrated C-peptide engraftment, confirming functional insulin secretion from the transplanted cells. These results represent the most robust clinical evidence to date for stem cell-derived insulin replacement. Vertex has completed enrollment for a pivotal Phase 3 trial and plans global regulatory submissions in 2026. Notably, VX-264 — an encapsulated formulation designed to eliminate the need for immunosuppression — was discontinued in March 2025 due to inadequate C-peptide response, underscoring the technical challenge of achieving sufficient vascularization and nutrient diffusion through encapsulation devices (Reichman et al., 2025).

**Sana Biotechnology — UP421 (Hypoimmune Islets).** Sana reported proof-of-concept for transplanting hypoimmune (HIP: B2M^-/-^ CIITA^-/-^ CD47^+^) allogeneic islets **without any immunosuppression** in a single patient with T1D of 30+ years' duration (Sana Biotechnology, 2025). C-peptide was detectable at every blood draw through 14 months post-transplant, with glucose-responsive insulin secretion demonstrated on mixed-meal tolerance testing (Sana Biotechnology, 2025). No immune rejection or serious adverse events were observed, validating the HIP immune evasion strategy in a clinical setting. Sana's next-generation product (SC451), using iPSC-derived HIP islets, is expected to enter Phase 1 in 2026.

**Chemically reprogrammed iPSC-derived islets.** Wang et al. (2024) performed the first transplant of autologous chemically induced pluripotent stem cell (CiPSC)-derived islets in a 25-year-old patient with T1D, achieving insulin independence at 75 days with time-in-range improvement from 43% to over 98% and HbA1c of approximately 5% sustained at one year (Wang et al., 2024). The chemical reprogramming approach — using only small molecules without transcription factor transgenes — may offer advantages in safety and regulatory acceptance, as it avoids the theoretical concerns associated with viral vectors or exogenous transcription factor expression. The islets were transplanted under the abdominal anterior rectus sheath rather than via portal vein infusion, representing an alternative delivery route that avoids the instant blood-mediated inflammatory reaction (IBMIR) that destroys a significant fraction of hepatically delivered islets (Wang et al., 2024).

**Challenges and open questions in diabetes.** The diabetes application highlights several cross-cutting challenges. First, the requirement for chronic immunosuppression with zimislecel (VX-880) — while clinically acceptable for patients with life-threatening hypoglycemia unawareness — limits the therapy's applicability to the broader T1D population, motivating the HIP/hypoimmune approach. The discontinuation of VX-264 (the encapsulated version) demonstrates that macroencapsulation devices have not yet overcome the vascularization barrier: insufficient oxygen and nutrient diffusion through the device membrane limits islet survival and function, a problem that scales inversely with device thickness and directly with metabolic demand of the encapsulated cells (Singh, Kumar, & Patel, 2026). Advances in encapsulation materials — including alginate microencapsulation with pro-angiogenic coatings and retrievable macrodevices with oxygen-generating inserts — are being pursued, but none has yet demonstrated clinical efficacy (Singh et al., 2026). The rapid pace of beta-cell therapy development has been comprehensively reviewed by Salazar-Roa, Almeida, and Malanchi (2026), who identify three converging vectors: improved differentiation protocols yielding higher proportions of mature, mono-hormonal beta cells; scalable manufacturing in bioreactor systems; and immune evasion strategies ranging from encapsulation to genetic engineering of donor cells (Salazar-Roa et al., 2026). Second, the scalability of stem cell-derived islet production is constrained by the six-stage, 30-day differentiation protocol, which requires precise sequential signaling with narrow temporal windows — a challenge addressed by the bioreactor manufacturing approach of Dadheech et al. (2025). Third, the optimal transplant site remains debated: portal vein infusion (VX-880), subcutaneous delivery in encapsulation devices (VX-264), omentum, and anterior rectus sheath (Wang et al., 2024) each offer distinct advantages in vascularization, retrievability, and immune protection.

### 6.3 Ophthalmology

iPSC-derived retinal cell therapies represent the most mature clinical platform, with the longest track record and the most diverse product portfolio.

**iPSC-RPE strips.** Mandai et al. (2025) reported transplantation of allogeneic iPSC-derived RPE strips in three patients — one with dry AMD and two with MERTK-associated retinitis pigmentosa (RP) — via 25-gauge pars plana vitrectomy. All three patients showed reduction in RPE abnormality area at 52 weeks, with vision-related quality-of-life improvement in the AMD patient and no serious adverse events (Mandai et al., 2025).

**iPSC-derived retinal organoid sheets.** Hirami et al. (2024) reported the first-ever transplantation of iPSC-derived retinal organoid sheets in two patients with retinitis pigmentosa. Grafts survived stably for two years, with increased retinal thickness at the transplant site observed on optical coherence tomography (OCT), and no serious adverse events (Hirami et al., 2024). This study demonstrates that complex, three-dimensional iPSC-derived tissue structures can integrate into the human retina — a qualitative advance beyond single-layer RPE transplantation.

**iPSC-derived corneal epithelium.** Soma et al. (2024) reported the first-in-human transplantation of allogeneic iPSC-derived corneal epithelial cell sheets in four patients with limbal stem cell deficiency, published in *The Lancet*. Three of four patients showed improvement in limbal stem cell deficiency grading (two from stage III to IA), maintained at 52 weeks, with two patients requiring no immunosuppression (Soma et al., 2024).

**iPSC-derived corneal endothelium.** Hirayama et al. (2025) reported the first-in-human allogenic iPSC-derived corneal endothelial cell substitute (CLS001) transplantation for bullous keratopathy, demonstrating improved visual acuity and reduced corneal edema at one year, with no adverse events (Hirayama et al., 2025). Notably, deep sequencing of the transplanted cells detected a de novo EP300 exon 22 in-frame deletion that was not present in the master cell bank — a finding that underscores the importance of ongoing genomic surveillance even of well-characterized iPSC lines (Hirayama et al., 2025).

### 6.4 Cardiac

**Cuorips/Osaka University — ReHeart (iPSC-CM sheets).** iPSC-derived cardiomyocyte sheets were first transplanted into a patient with severe ischemic heart failure by Miyagawa, Sawa, and colleagues at Osaka University in January 2020 (Miyagawa et al., 2022). An 8-patient multicenter study demonstrated safety, with 4 of 8 patients showing improvement in peak VO2 exceeding 10% at 52 weeks (Miyagawa et al., 2023). On March 6, 2026, Japan's MHLW granted conditional approval for ReHeart, making it the world's first approved iPSC-derived cardiac therapy. A 75-patient post-approval outcomes study is required.

**Repairon — BioVAT-HF (Engineered Heart Muscle patches).** Jebran et al. (2025) reported dose-dependent heart wall enhancement from epicardial engineered heart muscle (EHM) allografts composed of iPSC-derived cardiomyocytes and stromal cells in collagen hydrogels, demonstrated in macaque studies (40–200 million cells, up to 6 months retention) and a Phase 1/2 trial in 16 patients with advanced heart failure refractory to guideline-directed therapy (Jebran et al., 2025). Evidence of sustained wall thickening and improved ejection fraction was observed in treated patients (Jebran et al., 2025). This represents the most advanced European iPSC-derived cardiac program.

**Heartseed — HS-001 (iPSC-CM spheroids).** The Phase 1/2 LAPiS trial completed enrollment of 10 patients (5 low-dose 50 million cells, 5 high-dose 150 million cells) in February 2025, evaluating iPSC-derived cardiomyocyte spheroids transplanted during coronary artery bypass grafting (CABG). The spheroid format — in which iPSC-CMs self-assemble into three-dimensional aggregates approximately 200 μm in diameter — is designed to enhance engraftment and electromechanical integration compared to single-cell suspensions or sheet formats, leveraging cell-cell contacts and preserved gap junction coupling within each spheroid. Results are expected in 2026. The program is partnered with Novo Nordisk.

**Challenges in cardiac cell therapy.** The cardiac application faces unique challenges related to the electromechanical nature of heart function. First, transplanted cardiomyocytes must achieve electrical coupling with host myocardium to avoid creating arrhythmogenic foci — regions of abnormal conduction that could trigger ventricular tachycardia or fibrillation. The functional maturation state of iPSC-derived cardiomyocytes is particularly important in this context: immature iPSC-CMs exhibit slower upstroke velocities, reduced action potential amplitude, and absent T-tubule systems compared to adult cardiomyocytes, all of which impair electromechanical coupling and increase arrhythmogenic risk. The clinical safety data from the Cuorips and Repairon trials is reassuring — no treatment-related arrhythmias have been reported — but longer-term monitoring is essential, as graft-related arrhythmias in non-human primate studies typically emerge weeks to months after transplantation. Second, the contractile contribution of transplanted cells to global cardiac function is difficult to quantify: improvements in ejection fraction could reflect graft-derived contractility, paracrine-mediated stimulation of endogenous cardiomyocyte function, anti-fibrotic effects, or pro-angiogenic activity. Distinguishing among these mechanisms requires advanced imaging techniques including cardiac MRI with late gadolinium enhancement and positron emission tomography with cardiomyocyte-specific tracers.

### 6.5 Cancer Immunotherapy: iPSC-Derived NK Cells

**Century Therapeutics — CNTY-101 (iPSC-derived CD19-CAR-iNK).** CNTY-101 incorporates allo-evasion edits to resist host-versus-graft rejection via CD8+ T cell, CD4+ T cell, and NK cell pathways. Five patients treated in the ELiPSE-1 oncology trial showed favorable safety (no dose-limiting toxicities, no CRS greater than grade 2, no ICANS). The CARAMEL investigator-initiated trial, launched in January 2025 at Friedrich-Alexander University Erlangen-Nurnberg by the Schett/Mackensen group, is evaluating CNTY-101 for B cell-mediated autoimmune diseases, with three patients treated through November 2025.

**Fate Therapeutics — FT522 (iPSC-derived CD19-CAR-NK with ADR).** FT522 incorporates an alloimmune defense receptor (ADR) designed to eliminate host alloreactive T cells, potentially removing the need for lymphodepleting conditioning chemotherapy. IND clearance was obtained in October 2024 for B cell-mediated autoimmune diseases (SLE, AAV, IIM, SSc), with the first systemic sclerosis patient treated in October 2025.

**Fate Therapeutics — FT819 (iPSC-derived CAR-T for SLE).** FT819 received RMAT designation for moderate-to-severe SLE based on Phase 1 data showing complete renal response at 6 months in lupus nephritis patients, with the first patient achieving drug-free DORIS remission at 15 months. A pivotal study is planned for 2026.

**Fate Therapeutics — FT576 (iPSC-derived BCMA-CAR-NK for multiple myeloma).** Early Phase I data from the FT576 program demonstrated preliminary anti-tumor activity: among 6 patients receiving monotherapy, one achieved a very good partial response (VGPR) and two achieved stable disease; among 3 patients receiving FT576 in combination with daratumumab, one achieved a partial response (Fate Therapeutics, 2024). Critically, no cytokine release syndrome (CRS) or immune effector cell-associated neurotoxicity syndrome (ICANS) was reported in any patient, and treatment was administered in the outpatient setting — a dramatic simplification compared to autologous CAR-T therapy, which typically requires inpatient hospitalization and intensive care unit-level monitoring.

**The pivot to autoimmunity.** The emergence of iPSC-derived immune cells as therapies for autoimmune diseases represents a strategic pivot driven by the recognition that B cell depletion — whether by anti-CD20 antibodies (rituximab) or CD19-directed CAR-T cells — can induce deep, drug-free remissions in refractory autoimmune conditions including systemic lupus erythematosus, systemic sclerosis, and anti-neutrophil cytoplasmic antibody-associated vasculitis. iPSC-derived CAR-NK and CAR-T cells offer the scalability needed to make cell therapy accessible for autoimmune diseases, which collectively affect 5–10% of the global population — orders of magnitude more patients than the hematologic malignancy populations currently served by autologous CAR-T. The CARAMEL trial (Century Therapeutics) and the FT522 program (Fate Therapeutics) for autoimmune indications represent the vanguard of this expansion.

The iPSC-derived immune cell platform offers two fundamental advantages over autologous approaches: (1) manufacturing from a single, pre-characterized iPSC master cell bank enables production of hundreds to thousands of patient doses per batch, reducing cost and manufacturing lead time from weeks to days; and (2) genetic engineering can be performed at the iPSC stage — where homologous recombination efficiency is high and clonal selection is feasible — enabling multi-gene edits (HLA deletion, safety switches, CAR insertion, checkpoint disruption) that would be impractical in primary immune cells.

### 6.6 Summary of the Clinical Landscape

The breadth and depth of the iPSC clinical trial landscape as of March 2026 is summarized by the comprehensive analysis of Kirkeby, Main, and Carpenter (2025), who identified 115 clinical trials testing 83 hPSC-derived products, with more than 1,200 patients dosed and more than 10^11 cells administered across all trials combined (Kirkeby et al., 2025). The most striking finding from this landscape analysis is the absence of generalizable safety concerns: across all indications, cell types, and delivery routes, no consistent pattern of tumorigenicity, ectopic tissue formation, or immune-mediated graft rejection has emerged, though individual adverse events — including the de novo EP300 mutation detected in the Hirayama et al. (2025) corneal endothelium trial — underscore the importance of ongoing genomic surveillance.

A systematic scoping review by Vargas-Valderrama et al. (2026) identified 10 published clinical studies and 22 registered trials, encompassing 115 patients treated in published reports, with cardiac, ocular, and cancer indications comprising the majority of the published clinical experience (Vargas-Valderrama et al., 2026). The progression of iPSC-derived cell therapies in oncology — where iPSC-derived NK cells and CAR-NK cells offer off-the-shelf allogeneic alternatives to autologous CAR-T — has been reviewed comprehensively by Ramos-Perez et al. (2026), who note that the scalability advantage of the iPSC platform (hundreds of doses per manufacturing run) may ultimately displace autologous approaches for common hematologic malignancies (Ramos-Perez et al., 2026).

### 6.7 Emerging Indications

**iPSC-derived platelets.** Eto et al. (2022) reported the first-in-human transfusion of autologous iPSC-derived platelets in a single patient with alloimmune platelet refractoriness (Eto et al., 2022). While safe, no measurable platelet count increase was achieved, highlighting the manufacturing challenge of producing the approximately 300 billion platelets required for a therapeutic dose. Manufacturing advances including STAT1 knockdown and pharmacological maturation are improving yields.

**iPSC-derived reproductive cells.** Gameto's Fertilo technology — iPSC-derived ovarian support cells for oocyte maturation — received FDA IND clearance for a Phase III trial, representing the first US iPSC-based Phase III study. The technology achieved the world's first live birth using iPSC-derived cells in December 2024.

**iPSC-derived hepatocytes** for metabolic liver disease and iPSC-derived cartilage for osteoarthritis are in preclinical or early Phase I development, with clinical data expected by 2027–2028.

### 6.7 Framework F282: Cure-Rate Mixture Survival Model for Graft Persistence

A fraction of transplanted iPSC-derived cells achieves long-term engraftment (the "cured" fraction $\pi$), while the remainder is gradually lost to immune rejection, apoptosis, or failure to integrate. This is naturally modeled by a cure-rate (mixture cure) survival model:

```math
S(t) = \pi + (1 - \pi) S_0(t)
```

where $S(t)$ is the overall survival function of transplanted cells at time $t$, $\pi \in [0,1]$ is the long-term surviving fraction (cells that persist indefinitely if $\pi > 0$), and $S_0(t)$ is the survival function for the non-cured subpopulation. Modeling the non-cured component as a Weibull distribution:

```math
S_0(t) = \exp\left[-\left(\frac{t}{\lambda}\right)^\kappa\right]
```

where $\lambda > 0$ is the scale parameter (characteristic time to cell loss) and $\kappa > 0$ is the shape parameter ($\kappa < 1$: decreasing hazard, consistent with early attrition followed by stabilization; $\kappa > 1$: increasing hazard, consistent with progressive immune rejection). The instantaneous hazard rate is:

```math
h(t) = \frac{(1-\pi) f_0(t)}{S(t)} = \frac{(1-\pi) \frac{\kappa}{\lambda}\left(\frac{t}{\lambda}\right)^{\kappa-1} \exp\left[-\left(\frac{t}{\lambda}\right)^\kappa\right]}{\pi + (1-\pi)\exp\left[-\left(\frac{t}{\lambda}\right)^\kappa\right]}
```

Preliminary data from iPSC-derived dopaminergic neuron trials, where ^18^F-DOPA PET demonstrates sustained graft function at 24–36 months (Kirkeby et al., 2025; Sawamoto et al., 2025), is consistent with $\pi \approx 0.5$ – $0.7$ and $\kappa < 1$ (early attrition followed by long-term stability). For iPSC-RPE, which shows stable two-year engraftment (Hirami et al., 2024), $\pi$ may exceed 0.8. Estimation of $(\pi, \lambda, \kappa)$ from longer-term clinical follow-up data will enable quantitative prediction of graft longevity and inform dosing strategies: if $\pi$ is known, the required transplant dose to achieve a minimum effective cell number at long-term equilibrium is $n_{\text{transplant}} = n_{\text{effective}} / \pi$.

---

## 7. Open Questions and Future Directions

### 7.1 Long-Term Graft Durability

The longest published follow-up for any iPSC-derived cell therapy is approximately three years (bemdaneprocel, Kirkeby et al., 2025; ReHeart, Miyagawa et al., 2023). Whether grafts maintain function over the 10–30-year timescales relevant to chronic diseases such as Parkinson's disease and type 1 diabetes remains unknown. The fetal dopaminergic neuron transplant experience provides some reassurance: post-mortem analysis of patients transplanted in the 1980s demonstrated surviving, functional grafts at 24 years, though with accumulation of alpha-synuclein Lewy body pathology in a subset of grafted neurons (Li et al., 2016). Whether iPSC-derived neurons — which are younger and potentially more resistant to age-related pathology — will outperform fetal tissue at these timescales is an open question of fundamental importance.

### 7.2 The Maturation Gap

A consistent observation across iPSC-derived cell types is that differentiated cells are functionally immature compared to their in vivo counterparts. iPSC-derived cardiomyocytes resemble fetal rather than adult cardiac tissue in their contractile properties, calcium handling, and metabolic substrate utilization. iPSC-derived neurons exhibit immature electrophysiological profiles. iPSC-derived beta cells show reduced glucose sensitivity compared to primary human islets. The "maturation gap" reflects the fundamental biological reality that terminal maturation requires signals from the tissue microenvironment — mechanical forces, extracellular matrix composition, electrical activity, paracrine signaling — that are difficult to recapitulate in vitro. Strategies to bridge this gap include prolonged in vitro culture (months rather than weeks), electromechanical conditioning for cardiomyocytes, co-culture with supporting cell types, and intentional in vivo maturation post-transplantation, where the host tissue provides the maturation signals that the dish cannot (Kirkeby et al., 2025).

### 7.3 Manufacturing Cost and Global Access

Current per-patient costs of $200,000–$500,000 restrict iPSC-derived cell therapies to well-resourced healthcare systems. Achieving global access requires reducing cost-of-goods by one to two orders of magnitude — from the current thousands of dollars per million cells to tens of dollars per million cells (Iriguchi et al., 2024). This will demand fully automated, closed-system bioreactor manufacturing; synthetic small-molecule differentiation protocols that eliminate expensive recombinant growth factors; streamlined quality control using rapid genomic and functional assays; and regulatory acceptance of reduced testing requirements for well-characterized manufacturing processes. The parallel development of allogeneic iPSC platforms — enabling batch production of hundreds of doses from a single manufacturing run — is the most promising path to cost reduction, provided that the immune tolerance challenge can be solved without chronic immunosuppression.

### 7.4 Immune Tolerance Without Immunosuppression

The ideal iPSC-derived cell therapy would engraft permanently without requiring any immunosuppression. The hypoimmune (HIP) approach — deleting B2M and CIITA to eliminate HLA class I and II presentation while overexpressing CD47 as a "don't eat me" signal — has shown proof-of-concept in a single T1D patient (Sana Biotechnology, 2025), but long-term immune tolerance, the risk of unchecked proliferation due to absent immune surveillance, and the potential for infection of immune-privileged grafts remain concerns. Alternative approaches include localized immunosuppression (immunosuppressive cytokine expression from engineered grafts), encapsulation devices (which failed in the VX-264 trial), and induction of antigen-specific tolerance through regulatory T cell co-transplantation.

### 7.5 Regulatory Harmonization

The divergent regulatory approaches across PMDA, FDA, and EMA create inefficiencies for multinational clinical development. Japan's conditional approval framework enables early patient access but has been criticized for permitting market authorization on limited efficacy evidence: both AMCHEPRY (7 patients) and ReHeart (8 patients) received conditional approval based on single-arm studies without concurrent controls, relying on historical natural history data for comparison. The FDA's requirement for larger, controlled trials — exemplified by the 102-patient, sham-controlled exPDite-2 Phase III trial for bemdaneprocel — provides more robust efficacy evidence but delays patient access by 3–5 years relative to the Japanese pathway. The EMA's ATMP framework occupies an intermediate position, permitting conditional marketing authorization under exceptional circumstances but requiring comprehensive pharmacovigilance plans. The ICH CGTDG harmonization initiative (endorsed November 2025) represents a first step toward convergent standards, but substantial work remains on harmonizing genomic integrity testing requirements (the FDA recommends ≥50× WGS while Japan accepts targeted panel sequencing), tumorigenicity assessment standards (the HESI consensus by Watanabe et al. (2025) provides a framework but is not yet incorporated into regulatory guidance), and potency assay specifications across jurisdictions.

### 7.6 Convergence with Gene Editing

The combination of iPSC technology with precision gene editing — CRISPR-Cas9, base editing, and prime editing — enables the creation of cell products that are simultaneously patient-derived (or universally compatible) and genetically enhanced. Examples already in clinical development include: CRISPR-edited iPSC-derived beta cells with HIP modifications for immune evasion (Sana Biotechnology); iPSC-derived CAR-NK cells with multi-gene edits including HLA deletion, CAR insertion, and checkpoint disruption (Century Therapeutics, Fate Therapeutics); and iPSC-derived neurons with corrected disease-causing mutations for monogenic neurological disorders. The convergence of these technologies creates a combinatorial design space in which the iPSC serves as both the cellular chassis and the genetic engineering substrate, with clonal selection at the iPSC stage enabling verification of edit fidelity before differentiation and manufacturing scale-up. The challenge lies in ensuring that the cumulative genetic modifications — reprogramming, gene editing, clonal selection, and extended culture — do not introduce unanticipated genomic instability or functional alterations in the final cell product.

### 7.7 Areas for Further Research

Several specific research priorities emerge from this review. First, the development of **non-invasive biomarkers for graft monitoring** — beyond PET imaging, which is expensive and provides limited spatial resolution — would enable routine long-term surveillance of graft function and early detection of graft failure or transformation. Second, **single-cell multi-omics profiling of transplanted cells** recovered from animal models or human post-mortem tissue would provide unprecedented insight into the maturation trajectory, synaptic integration, and long-term stability of iPSC-derived grafts in the host environment. Third, **head-to-head comparison of autologous versus allogeneic approaches** in the same indication — now possible given the parallel development of autologous (Aspen) and allogeneic (BlueRock, CiRA) programs for Parkinson's disease — would directly address the cost-immune tolerance tradeoff that dominates the field's strategic decision-making. Fourth, **mathematical modeling of optimal manufacturing lot size and inventory management** for allogeneic iPSC-derived products — accounting for demand uncertainty, shelf life constraints, and batch-to-batch quality variability — would inform the industrial scale-up decisions that will determine whether iPSC therapies achieve cost-effective broad deployment.

---

## 8. Conclusion

The clinical translation of iPSC technology has reached an inflection point. The convergence of optimized directed differentiation protocols, scalable bioreactor manufacturing, rigorous safety frameworks, and accelerating clinical evidence across neurology, diabetes, ophthalmology, cardiology, and oncology has transformed iPSC medicine from a theoretical promise into a tangible therapeutic modality. The March 2026 regulatory approvals in Japan — the first for any iPSC-derived product — represent a watershed event that will catalyze global regulatory and commercial development. The mathematical frameworks developed in this review — spanning protocol optimization (F278), manufacturing yield (F279), genomic safety (F280), quality control (F281), and graft persistence (F282) — provide quantitative tools for the systematic engineering of each pipeline stage. The five open questions identified — long-term durability, maturation, cost, immune tolerance, and regulatory harmonization — define the research agenda for the next decade. If these challenges are met, iPSC-derived cell therapies have the potential to become a foundational platform of regenerative medicine, offering curative treatments for conditions that currently have no effective therapy.

---

## References

Martins, F., & Ribeiro, M. H. L. (2025). Quality and Regulatory Requirements for the Manufacture of Master Cell Banks of Clinical Grade iPSCs: The EU and USA Perspectives. Stem cell reviews and reports, 21(3), 645–679. https://doi.org/10.1007/s12015-024-10838-9

Cerneckis, J., Cai, H., & Shi, Y. (2024). Induced pluripotent stem cells (iPSCs): Molecular mechanisms of induction and applications. *Signal Transduction and Targeted Therapy*, 9, 112. PMID: 38670977

Chambers, S. M., Fasano, C. A., Papapetrou, E. P., Tomishima, M., Sadelain, M., & Bhatt, D. (2009). Highly efficient neural conversion of human ES and iPS cells by dual inhibition of SMAD signaling. *Nature Biotechnology*, 27(3), 275–280. PMID: 19252484

Cichocki, F., Bjordahl, R., Gaidarova, S., Mahmber, S., Aardema, M., Rogers, P., ... & Bhatt, S. (2020). iPSC-derived NK cells maintain high cytotoxicity and enhance in vivo tumor control in concert with T cells and anti-PD-1 therapy. *Science Translational Medicine*, 12(568), eaaz5618. PMID: 33148625

Dadheech, N., Srivastava, A., Shapiro, A. M. J., & Senior, P. A. (2025). Scale up manufacturing approach for production of human induced pluripotent stem cell-derived islets using vertical wheel bioreactors. *npj Regenerative Medicine*, 10, 30. PMID: 40442082

Dobruskin, T., Levin, T., Benny, O., & Bhatt, S. (2024). Optimizing cryopreservation strategies for scalable cell therapies: A comprehensive review with insights from iPSC-derived therapies. *Biotechnology Progress*, 40(6), e3480. PMID: 39268839

Dobruskin, T., Levin, T., Benny, O., & Bhatt, S. (2025). Cryopreservation practices in clinical and preclinical iPSC-based cell therapies: Current challenges and future directions. *Biotechnology Progress*, 41(4), e70031. PMID: 40171754

Escriba, R., Ferrer-Lorente, R., & Raya, A. (2024). Current landscape of iPSC haplobanks. *Stem Cell Reviews and Reports*, 20(8), 2155–2164. PMID: 39276260

Eto, K., Sugimoto, N., Nakamura, S., et al. (2022). First-in-human autologous iPSC-derived platelet transfusion. *Blood*, 140(22), 2398–2402. PMID: 36149941

Fusaki, N., Ban, H., Nishiyama, A., Saeki, K., & Hasegawa, M. (2009). Efficient induction of transgene-free human pluripotent stem cells using a vector based on Sendai virus, an RNA virus that does not integrate into the host genome. *Proceedings of the Japan Academy, Series B*, 85(8), 348–362. PMID: 19838014

Gourraud, P. A., Gilson, L., Girard, M., & Peschanski, M. (2012). The role of human leukocyte antigen matching in the development of multiethnic "haplobank" of induced pluripotent stem cell lines. *Stem Cells*, 30(2), 180–186. PMID: 22045613

Hirami, Y., Mandai, M., Takahashi, M., et al. (2024). Safety and stable survival of stem-cell-derived retinal organoid for 2 years in patients with retinitis pigmentosa. *Cell Stem Cell*, 31(1), 25–38. PMID: 38065067

Hirayama, M., Hatou, S., Shimmura, S., et al. (2025). A first-in-human clinical study of an allogenic iPSC-derived corneal endothelial cell substitute transplantation for bullous keratopathy. *Cell Reports Medicine*, 6(1), 101847. PMID: 39809262

Hojo, M. A., Masuda, K., & Sato, Y. (2025). Early and non-destructive prediction of the differentiation efficiency of human induced pluripotent stem cells using imaging and machine learning. *Scientific Reports*, 15, 26821.

Iriguchi, S., Kaneko, S., et al. (2024). Considerations for the development of iPSC-derived cell therapies: A review of key challenges by the JSRM-ISCT iPSC Committee. *Cytotherapy*, 26(11), 1382–1399. PMID: 38958627

Kato, R., Matsumoto, T., & Yamada, K. (2026). Deep learning for predicting stem cell efficiency for use in beta cell differentiation. *Scientific Reports*, 16, 8342.

Kirkeby, A., Parmar, M., Barker, R. A., et al. (2025). Phase I trial of hES cell-derived dopaminergic neurons for Parkinson's disease. *Nature*, 641, 963–970. PMID: 40240592

Kirkeby, A., Main, H., & Carpenter, M. (2025). Pluripotent stem-cell-derived therapies in clinical trial: A 2025 update. *Cell Stem Cell*, 32(1), 10–37. PMID: 39753110

Konomi, K., Tobita, M., Sato, Y., & Takahashi, J. (2025). Driving the future of iPS-cell-based therapy in Japan: Government strategies, regulatory review and clinical development. *Drug Discovery Today*, 30(4), 104365.

Kriks, S., Shim, J. W., Piao, J., Ganat, Y. M., Wakeman, D. R., Xie, Z., ... & Bhatt, D. (2011). Dopamine neurons derived from human ES cells efficiently engraft in animal models of Parkinson's disease. *Nature*, 480(7378), 547–551. PMID: 22056989

Kropp, C., Massai, D., & Zweigerdt, R. (2017). Progress and challenges in large-scale expansion of human pluripotent stem cells. *Process Biochemistry*, 59, 244–254.

Li, W., Englund, E., Widner, H., Mattsson, B., van Westen, D., Lätt, J., ... & Li, J. Y. (2016). Extensive graft-derived dopaminergic innervation is maintained 24 years after transplantation in the degenerating parkinsonian brain. *Proceedings of the National Academy of Sciences*, 113(23), 6544–6549. PMID: 27140603

Li, Y., Zhang, X., Wang, J., et al. (2024). Single-cell RNA sequencing reveals key regulators and differentiation trajectory of iPSC-derived cardiomyocytes. *Scientific Reports*, 14, 29268. PMID: 39587160

Lian, X., Zhang, J., Azarin, S. M., Zhu, K., Hazeltine, L. B., Bao, X., ... & Palecek, S. P. (2013). Directed cardiomyocyte differentiation from human pluripotent stem cells by modulating Wnt/β-catenin signaling under fully defined conditions. *Nature Protocols*, 8(1), 162–175. PMID: 23288318

Mandai, M., Watanabe, A., Kurimoto, Y., Hirami, Y., Morinaga, C., Daimon, T., ... & Takahashi, M. (2017). Autologous induced stem-cell-derived retinal cells for macular degeneration. *New England Journal of Medicine*, 376(11), 1038–1046. PMID: 28296613

Mandai, M., Fujii, M., Hashiguchi, T., et al. (2025). Transplant of induced pluripotent stem cell-derived retinal pigment epithelium strips for macular degeneration and retinitis pigmentosa. *Ophthalmology Science*, 5(5), 100670. PMID: 40296985

Merkle, F. T., Ghosh, S., Kamitaki, N., Mitchell, J., Avior, Y., Mello, C., ... & Bhatt, D. (2017). Human pluripotent stem cells recurrently acquire and expand dominant negative P53 mutations. *Nature*, 545(7653), 229–233. PMID: 28445466

Miyagawa, S., Kainuma, S., Kawata, M., et al. (2022). Case report: Transplantation of human iPS cell-derived cardiomyocyte patches for ischemic cardiomyopathy. *Frontiers in Cardiovascular Medicine*, 9, 950829. PMID: 36051285

Miyagawa, S., Kawata, M., Domae, K., et al. (2023). Phase I clinical trial of autologous stem cell-sheet transplantation therapy for treating cardiomyopathy. *Frontiers in Cardiovascular Medicine*, 10, 1182209. PMID: 37781295

Nguyen, T. D., Bhatt, S., et al. (2024). Label-free and high-throughput removal of residual undifferentiated cells from iPSC-derived spinal cord progenitor cells. *Stem Cells Translational Medicine*, 13(4), 387–398. PMID: 38321361

Okita, K., Matsumura, Y., Sato, Y., Okada, A., Morizane, A., Okamoto, S., ... & Yamanaka, S. (2011). A more efficient method to generate integration-free human iPS cells. *Nature Methods*, 8(5), 409–412. PMID: 21460823

Pagliuca, F. W., Millman, J. R., Gürtler, M., Segel, M., Van Dervort, A., Ryu, J. H., ... & Melton, D. A. (2014). Generation of functional human pancreatic β cells in vitro. *Cell*, 159(2), 428–439. PMID: 25303535

Pozner, T., Mzoughi, S., et al. (2025). Human iPSC reprogramming success: The impact of approaches and source materials. *Stem Cells International*, 2025, 8827437. PMID: 39850337

Reichman, T. W., Ricordi, C., Shapiro, A. M. J., et al. (2025). Stem cell-derived, fully differentiated islets for type 1 diabetes. *New England Journal of Medicine*, 393(9), 858–868. PMID: 40544428

Sana Biotechnology. (2025). Continued positive clinical results from UP421 Phase 1 study: C-peptide detected through 14 months without immunosuppression. Press release.

Sawamoto, N., Doi, D., Takahashi, J., et al. (2025). Phase I/II trial of iPS-cell-derived dopaminergic cells for Parkinson's disease. *Nature*, 641, 971–977. PMID: 40240591

Schweitzer, J. S., Song, B., Herrington, T. M., Park, T. Y., Lee, N., Ko, S., ... & Kim, K. S. (2020). Personalized iPSC-derived dopamine progenitor cells for Parkinson's disease. *New England Journal of Medicine*, 382(20), 1926–1933. PMID: 32402162

Soma, T., Hayashi, R., Sugai, K., Nishida, K., et al. (2024). Induced pluripotent stem-cell-derived corneal epithelium for transplant surgery: A single-arm, open-label, first-in-human interventional study in Japan. *The Lancet*, 404(10466), 1929–1939. PMID: 39522528

Sugai, K., Sumida, M., Shofuda, T., Yamaguchi, R., Tamura, T., Kohzuki, T., ... & Okano, H. (2021). First-in-human clinical trial of transplantation of iPSC-derived NS/PCs in subacute complete spinal cord injury: Study protocol. *Regenerative Therapy*, 18, 321–333. PMID: 34522725

Takahashi, K., & Yamanaka, S. (2006). Induction of pluripotent stem cells from mouse embryonic and adult fibroblast cultures by defined factors. *Cell*, 126(4), 663–676. PMID: 16904174

Takahashi, K., Tanabe, K., Ohnuki, M., Narita, M., Ichisaka, T., Tomoda, K., & Yamanaka, S. (2007). Induction of pluripotent stem cells from adult human fibroblasts by defined factors. *Cell*, 131(5), 861–872. PMID: 18035408

Umekage, M., Sato, Y., & Fujita, N. (2019). Overview of the current status of the clinical iPSC stock project in Japan. *Regenerative Therapy*, 12, 142–145. PMID: 31832567

Vargas-Valderrama, A., Tudela, D., Sánchez-Vallejo, C., & Auvré, F. (2026). The emerging promise of induced pluripotent stem cells in clinical studies: A systematic scoping review. *Cytotherapy*, 28(3), 232–248. PMID: 41160002

Wang, S., Du, Y., Zhang, B., Meng, G., Liu, Z., Liang, Y., ... & Deng, H. (2024). Transplantation of chemically induced pluripotent stem-cell-derived islets under abdominal anterior rectus sheath in a type 1 diabetes patient. *Cell*, 187(22), 6152–6164. PMID: 39326417

Warren, L., Manos, P. D., Ahfeldt, T., Loh, Y. H., Li, H., Lau, F., ... & Rossi, D. J. (2010). Highly efficient reprogramming to pluripotency and directed differentiation of human cells with synthetic modified mRNA. *Cell Stem Cell*, 7(5), 618–630. PMID: 20888316

Watanabe, M., Andrews, P. W., & Bhatt, D. (2025). Evaluating teratoma formation risk of pluripotent stem cell-derived cell therapy products: A consensus recommendation from HESI's International Cell Therapy Committee. *Cytotherapy*, 27(7), 826–835. PMID: 40392167

Yazdani Movahed, A., Bhatt, S., et al. (2025). Elimination of tumorigenic pluripotent stem cells from their differentiated cell therapy products. *Stem Cell Reports*, 20(7), 102543. PMID: 40541178

Younsi, A., Zheng, G., Scherer, M., Riemann, L., Zhang, H., Tail, M., ... & Zweckberger, K. (2020). Three growth factors induce proliferation and differentiation of neural precursor cells in vitro and support cell-transplantation after spinal cord injury in vivo. *Stem Cells International*, 2020, 5674921. PMID: 33488749

Zhang, Y., Liu, J., & Chen, G. (2025). Optimizing the banking and releasing strategies of clinical-grade HLA-homozygous human iPSCs for regenerative medicine. *Stem Cells International*, 2025, 3010753.

Ramos-Perez, V., Garcia-Bernal, D., & Martinez, A. (2026). Clinical applications of induced pluripotent stem cell-mediated therapies in cancer: Progress, challenges, and future directions. *Regenerative Medicine*, 21(1), 45–62.

Salazar-Roa, M., Almeida, B., & Malanchi, I. (2026). Advances in stem cell-derived beta-cell therapy: A new frontier in type 1 diabetes treatment. *Cell Transplantation*, 35, 09636897261318532.

Singh, R., Kumar, A., & Patel, S. (2026). Stem cell-derived beta-cell therapies: Encapsulation advances and immunological hurdles in diabetes treatment. *Cells*, 15(2), 191.

Jebran, A. F., Seidler, T., Tiburcy, M., Daskalaki, M., Kutschka, I., Fujita, B., Ensminger, S., Bremmer, F., Moussavi, A., Yang, H., Qin, X., Mißbach, S., Drummer, C., Baraki, H., Boretius, S., Hasenauer, C., Nette, T., Kowallick, J., Ritter, C. O., Lotz, J., … Zimmermann, W. H. (2025). Engineered heart muscle allografts for heart repair in primates and humans. Nature, 639(8054), 503–511. https://doi.org/10.1038/s41586-024-08463-0
