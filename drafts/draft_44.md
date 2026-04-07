# Precision Partial Reprogramming Review

---

## Abstract

Partial cellular reprogramming — the transient expression of Oct4, Sox2, and Klf4 (OSK) to reverse epigenetic age without erasing cell identity — has emerged as the first therapeutic modality capable of reversing biological aging at the molecular level. In progeroid mouse models, cyclic OSKM expression extends lifespan by 33% (Ocampo et al., 2016); in aged wild-type mice, systemic AAV-OSK delivery extends median remaining lifespan by 109% and reverses frailty (Macip et al., 2024); and in human fibroblasts, maturation phase transient reprogramming (MPTR) reverses the transcriptomic and epigenomic age by approximately 30 years while preserving cellular identity (Gill et al., 2022). The U.S. Food and Drug Administration cleared the first Investigational New Drug application for a partial epigenetic reprogramming therapy — ER-100, an AAV-delivered doxycycline-inducible OSK for optic neuropathies — in January 2026. This review provides a comprehensive analysis of six interconnected frontiers in precision partial reprogramming: (1) the molecular mechanisms by which transient Yamanaka factor expression dissociates age reversal from dedifferentiation; (2) the H3K9me3 heterochromatin barrier that defines the rejuvenation ceiling; (3) control strategies — temporal, genetic, chemical, and cell-type-targeted — that constrain reprogramming within the therapeutic window; (4) delivery platforms optimized for transient in vivo expression; (5) epigenetic clocks and multi-omic biomarker panels as pharmacodynamic endpoints; and (6) tissue-specific reprogramming biology, including the landmark discovery that mesenchymal drift is a universal age-associated transcriptomic signature reversible by partial reprogramming. Novel mathematical frameworks  formalize the quantitative principles governing reprogramming dose-response pharmacology, the stochastic dynamics of the rejuvenation–dedifferentiation boundary, clock-based pharmacodynamic modeling, and tissue-level reprogramming heterogeneity. Together, these advances define a translational path from preclinical proof-of-concept to precision rejuvenation medicine.

---

## 1. Introduction: The Reprogramming–Rejuvenation Dissociation

### 1.1 From iPSCs to Age Reversal

The discovery that four transcription factors — Oct4, Sox2, Klf4, and c-Myc (OSKM) — can reprogram somatic cells to a pluripotent state fundamentally altered our understanding of cell fate plasticity (Takahashi & Yamanaka, 2006). This Nobel Prize-winning advance (2012) demonstrated that the epigenetic information encoding cellular identity is rewritable, but it also created a conceptual barrier: if reprogramming erases identity, how could it serve as a therapy for aging tissues that must retain their function?

The critical insight — that epigenetic age reversal and identity erasure are separable processes occurring on different timescales — emerged from two landmark studies. Ocampo et al. (2016) demonstrated that cyclic expression of OSKM (2 days on, 5 days off) in a progeroid mouse model ameliorated multiple hallmarks of aging — DNA methylation age, cellular senescence, DNA damage, and mitochondrial dysfunction — while preserving tissue architecture, extending median lifespan by 33%. Lu et al. (2020) showed that ectopic expression of OSK alone (excluding the oncogene c-Myc) in mouse retinal ganglion cells restored youthful DNA methylation patterns, promoted axon regeneration after injury, and reversed glaucoma-induced vision loss — the first demonstration that post-mitotic neurons could be functionally rejuvenated by epigenetic reprogramming.

These studies established the foundational principle: aging is not a one-way process. The epigenetic information lost during aging can, in principle, be recovered — provided the reprogramming stimulus is precisely calibrated to reverse age without triggering dedifferentiation.

### 1.2 The Clinical Inflection Point

The field has now reached a historic inflection point. In January 2026, the U.S. FDA cleared the first Investigational New Drug (IND) application for a partial epigenetic reprogramming therapy: ER-100, developed by Life Biosciences, an AAV-delivered doxycycline-inducible OSK construct for the treatment of open-angle glaucoma and non-arteritic anterior ischemic optic neuropathy (Life Biosciences, 2026). This Phase 1 first-in-human study (NCT07290244) represents the transition of partial reprogramming from a preclinical curiosity to a regulated therapeutic modality.

Simultaneously, the preclinical evidence base has deepened. Macip et al. (2024) demonstrated that systemically delivered AAV-OSK in 124-week-old wild-type mice extended median remaining lifespan by 109% over controls, with significant improvements in frailty scores and multiple organ systems — the most dramatic lifespan extension reported for any partial reprogramming intervention in physiologically aged animals. Chemical reprogramming has advanced from proof-of-concept to a rapid 10-day system capable of generating human chemically induced pluripotent stem cells (hCiPSCs) with 100% success across 15 donors, with key epigenetic obstacles (KAT3A/B, KAT6A) identified as rate-limiting barriers (Guan et al., 2025). And the first direct demonstration that partial reprogramming rejuvenates memory-encoding neurons — restoring learning and memory in aged mice and Alzheimer's disease models to the level of healthy young animals — has extended the therapeutic applicability from retinal neurons to central cognitive circuits (Berdugo-Vega et al., 2026).

### 1.3 Scope of This Review

Recent comprehensive reviews have mapped the field's trajectory and open challenges (Roux et al., 2024; Paine et al., 2024; Adams et al., 2025), yet no prior work has systematically addressed the pharmacological framework required for clinical dosing. This review synthesizes the molecular, pharmacological, and translational science required to move partial reprogramming from preclinical promise to clinical reality. We focus on three questions that prior reviews have not systematically addressed: (1) How should reprogramming be dosed — what are the pharmacodynamic biomarkers, the dose-response relationships, and the therapeutic windows? (2) How should reprogramming be delivered — what platform (AAV, LNP-mRNA, small molecules) best matches the kinetic requirements of transient factor expression? (3) How should reprogramming be monitored — what biomarker panels can distinguish rejuvenation from dedifferentiation in real time?

---

## 2. Molecular Mechanisms of Partial Reprogramming

### 2.1 The Phased Reprogramming Trajectory

Reprogramming is not a single event but a multi-phase trajectory through epigenetic space. Comprehensive single-cell and multi-omic analyses have defined at least three distinct phases (Polo et al., 2012; Schiebinger et al., 2019).

**Phase I: Mesenchymal-to-epithelial transition (MET) and early chromatin remodeling (days 0–5).** The immediate response to OSKM/OSK expression involves downregulation of mesenchymal genes (e.g., SNAI1/2, ZEB1) and upregulation of epithelial markers (e.g., CDH1), accompanied by global changes in chromatin accessibility at reprogramming factor binding sites (Li et al., 2010). This phase is characterized by stochastic gene activation — most cells initiate MET, but only a minority progress to later stages — establishing the first "quality control checkpoint" in the reprogramming trajectory.

**Phase II: Chromatin decompaction and epigenetic erosion (days 5–15).** Oct4 and Sox2 function as pioneer transcription factors that engage nucleosomal DNA, cooperatively destabilizing histone-DNA contacts and recruiting chromatin remodeling complexes (Soufi et al., 2015). During this phase, DNA methylation at aging-associated CpG sites begins to decline — this is the phase exploited by maturation phase transient reprogramming (MPTR), which interrupts factor expression at day 13 to capture the rejuvenation benefit before identity loss occurs (Gill et al., 2022).

**Phase III: Endogenous pluripotency network activation (days 15+).** If factor expression continues, the endogenous pluripotency circuitry (NANOG, endogenous Oct4/Sox2) activates, committing the cell to the pluripotent state. This represents the "point of no return" — the boundary between partial and complete reprogramming, and the critical safety threshold that must not be crossed in therapeutic applications.

The therapeutic window for partial reprogramming thus lies within Phase II: long enough to reverse epigenetic age marks, short enough to avoid activating the pluripotency network. The precise duration of this window varies by cell type, species, and delivery modality — quantifying it for each clinical context is the central pharmacological challenge.

### 2.2 What Partial Reprogramming Reverses

Multi-omic characterization of partially reprogrammed cells has identified a consistent set of age-associated changes that are reversed (Paine et al., 2024; Adams et al., 2025):

**DNA methylation age.** The most robustly measured endpoint. Gill et al. (2022) demonstrated approximately 30 years of transcriptomic age reduction in MPTR-treated human fibroblasts, measured by multiple epigenetic clock algorithms. Importantly, clock age decreased steadily during factor expression before accelerating upon withdrawal — a "rejuvenation overshoot" phenomenon suggesting that factor withdrawal does not halt the age-reversal process immediately (Olova et al., 2019).

**Cellular senescence markers.** p16^INK4a, p21^CIP1, and senescence-associated β-galactosidase (SA-β-gal) are consistently reduced after partial reprogramming. The senescence-associated secretory phenotype (SASP) — a major driver of inflammaging — is attenuated, with reduced expression of IL-6, IL-8, and MMP3 (Sarkar et al., 2020; Browder et al., 2022).

**Mitochondrial function.** Reactive oxygen species (ROS) production decreases, mitochondrial membrane potential is restored, and oxidative phosphorylation (OXPHOS) complex expression increases. PINK1-dependent mitophagy, the selective clearance of damaged mitochondria, is upregulated — a process shown to be rate-limiting for reprogramming efficiency (Vazquez-Martin et al., 2016).

**Proteostasis.** Autophagic flux increases, and proteasomal activity is enhanced, consistent with the reactivation of quality control systems that decline with age (Vilchez et al., 2014).

**Chromatin architecture.** Heterochromatin marks, particularly H3K9me3, are dynamically remodeled during reprogramming, with implications for both the mechanism of rejuvenation and the definition of its limits (see Section 3).

### 2.3 TET-Mediated Demethylation as the Rejuvenation Mechanism

The age-reversal effect of partial reprogramming operates, at least in part, through the ten-eleven translocation (TET) family of dioxygenases, which catalyze the iterative oxidation of 5-methylcytosine (5mC) through 5-hydroxymethylcytosine (5hmC), 5-formylcytosine (5fC), and 5-carboxylcytosine (5caC), with subsequent removal by thymine DNA glycosylase (TDG) and base excision repair (Tahiliani et al., 2009). Lu et al. (2020) demonstrated that the rejuvenating effect of OSK in retinal ganglion cells is Tet1/Tet2-dependent: genetic ablation of both enzymes abolished the age-reversal and regenerative effects of OSK, establishing that active DNA demethylation — not merely passive dilution through replication — is required for epigenetic rejuvenation.

The kinetics of TET-mediated oxidation impose a natural timescale on rejuvenation. The initial oxidation of 5mC to 5hmC proceeds 5-7 fold faster than subsequent oxidation to 5fC and 5caC (Ito et al., 2011), suggesting that the early phase of rejuvenation (days 0–5) involves primarily the generation of 5hmC — which itself has been shown to be enriched at enhancers and gene bodies of actively transcribed genes — while complete demethylation at aging-associated CpGs requires longer exposure. This kinetic hierarchy provides a molecular rationale for the observation that longer factor expression produces deeper rejuvenation but also increases the risk of identity loss: the beneficial 5hmC-mediated effects precede the more destabilizing complete demethylation.

---

## 3. The H3K9me3 Barrier and the Rejuvenation Ceiling

### 3.1 The Dual Role of H3K9me3 in Aging and Reprogramming

Trimethylation of histone H3 at lysine 9 (H3K9me3) — the hallmark of constitutive heterochromatin — plays a paradoxical dual role in the intersection of aging and reprogramming. In the aging context, H3K9me3 declines globally with age, leading to heterochromatin loss, derepression of transposable elements, and genomic instability — one of the primary drivers of the aging phenotype (Villeponteau, 1997; Zhang et al., 2015). In the reprogramming context, H3K9me3 at specific loci constitutes the principal epigenetic barrier to factor binding, with H3K9me3-marked regions among the last to be remodeled during iPSC generation (Soufi et al., 2012).

This creates a fundamental paradox for partial reprogramming as a rejuvenation therapy: the goal is to *restore* the youthful heterochromatin landscape (increasing H3K9me3 at repetitive elements and transposon loci) while simultaneously *overcoming* H3K9me3 barriers at reprogramming-relevant loci to enable the epigenetic reset. The resolution of this paradox — whether it is achievable at all, and if so, how — defines the theoretical rejuvenation ceiling.

### 3.2 KDM4 Demethylases and Barrier Modulation

The H3K9me3 barrier can be modulated by KDM4 family demethylases (KDM4A-D), which catalyze the removal of H3K9me3 and H3K9me2. Supplementation of reprogramming cocktails with KDM4B or KDM4C overexpression, or treatment with small molecule inhibitors of the H3K9 methyltransferases SUV39H1/H2 and SETDB1, has been shown to improve reprogramming efficiency by reducing the barrier at recalcitrant loci (Chen et al., 2013; Becker et al., 2016). However, global H3K9me3 reduction carries risks: derepression of endogenous retroviruses and LINE-1 elements, activation of innate immune sensing pathways (cGAS-STING), and potential genomic instability.

The ideal therapeutic strategy would therefore involve *locus-specific* modulation of H3K9me3 — reducing it at reprogramming barrier loci while preserving or restoring it at repetitive element loci. This is, in principle, achievable through epigenome editing tools such as dCas9-KDM4B fusions targeted to specific barrier regions, but such approaches remain in early development for the reprogramming context.

### 3.3 Defining the Rejuvenation Ceiling

The maximum achievable rejuvenation depth — how many years of epigenetic age can be reversed before identity loss occurs — has not been precisely measured. Available data suggest it is tissue- and protocol-dependent. MPTR in human fibroblasts achieves approximately 30 years of reversal (Gill et al., 2022). OSK in mouse retinal ganglion cells appears to achieve complete functional rejuvenation of a post-mitotic neuron (Lu et al., 2020). Systemic AAV-OSK in aged mice produces multi-organ rejuvenation sufficient to more than double remaining lifespan (Macip et al., 2024). Whether these reflect the same or different rejuvenation ceilings remains unknown.

---

## 4. Control Strategies for Precision Reprogramming

### 4.1 Temporal Control: Cyclic vs. Continuous Protocols

Two temporal strategies have been validated in vivo. **Cyclic OSKM** (2 days on, 5 days off), pioneered by Ocampo et al. (2016) and extended by Browder et al. (2022), uses repeated pulses that allow cells to "recover" their differentiated identity between cycles, preventing cumulative reprogramming from crossing the dedifferentiation threshold. Long-term cyclic OSKM in wild-type mice (7 or 10 months of treatment starting at 12 or 15 months of age) produced significant rejuvenation of kidney, skin, and organismal-level phenotypes, with the duration of treatment determining the magnitude of benefit (Browder et al., 2022). **Continuous OSK** (excluding c-Myc), as used by Lu et al. (2020), relies on the inherent safety of the three-factor system: without c-Myc, the oncogenic drive is substantially reduced, and long-term OSK expression (up to 21 months in mice) has not produced tumors or adverse effects in retinal or systemic delivery contexts (Macip et al., 2024).

### 4.2 Factor Selection: OSK vs. OSKM vs. Chemical

The exclusion of c-Myc from the reprogramming cocktail represents the single most important safety modification for therapeutic applications. c-Myc is a potent oncogene whose inclusion dramatically increases the risk of teratoma formation in partially reprogrammed tissues (Abad et al., 2013). The OSK combination retains the core pioneer factor activity of Oct4 and Sox2 while using Klf4 as a cooperative partner, and is sufficient for both rejuvenation and functional regeneration across multiple tissue contexts (Lu et al., 2020; Macip et al., 2024; Berdugo-Vega et al., 2026).

Chemical reprogramming offers an alternative that eliminates the need for genetic factors entirely. Small molecule cocktails can drive somatic cells to pluripotency through sequential modulation of signaling pathways (WNT, TGF-β, Hippo) and epigenetic modifiers (HDAC inhibitors, DOT1L inhibitors) (Liuyang et al., 2023). A rapid chemical reprogramming system developed in 2025 achieves human CiPSC generation in as few as 10 days, with identification of KAT3A/B and KAT6A as key epigenetic barriers (Guan et al., 2025). For partial rejuvenation applications, chemical cocktails could be dose-titrated to achieve epigenetic resetting without full pluripotency — an approach with inherent advantages for systemic delivery (oral or intravenous) and precise temporal control. Schoenfeldt et al. (2025) demonstrated that a seven-compound chemical cocktail reversed multiple aging hallmarks in human dermal fibroblasts and extended lifespan in *C. elegans*, providing proof-of-concept for chemical partial rejuvenation.

### 4.3 Cell-Type-Targeted Reprogramming

A transformative advance is the use of cell-type-specific promoters to restrict reprogramming factor expression to defined populations. Sahu et al. (2024) demonstrated that driving OSK expression from the Cdkn2a (p16^INK4a) promoter — which is selectively active in senescent and aged cells — extended lifespan in both progeroid and naturally aged wild-type mice without increasing tumor incidence. This approach achieves two objectives simultaneously: it targets reprogramming to the cells that need it most (aged and damaged cells with high p16 expression), and it provides a natural safety mechanism (expression automatically attenuates as cells rejuvenate and p16 levels decline).

Berdugo-Vega et al. (2026) extended this concept to the nervous system, targeting OSK specifically to engram neurons — the memory-encoding cells active during learning — using activity-dependent labeling (Fos-CreERT2). Reprogramming of dentate gyrus engrams improved learning strategies, while reprogramming of prefrontal cortex engrams restored long-term spatial memory in Alzheimer's disease models, demonstrating that cell-type-specific reprogramming can achieve functional rejuvenation of specific neural circuits.

### 4.4 Framework F318: Reprogramming Dose-Response Pharmacology

The relationship between reprogramming factor dose (cumulative exposure) and biological outcome can be formalized as a modified sigmoid dose-response with a therapeutic window bounded by a minimum effective dose (MED) and a maximum tolerated dose (MTD).

Let $D$ denote the cumulative reprogramming dose, defined as:

```math
D = \int_0^T c(t) \, dt
```

where $c(t)$ is the intracellular concentration of active reprogramming factors at time $t$, and $T$ is the treatment duration. The rejuvenation response $R(D)$ — measured as the reduction in epigenetic age (years reversed) — follows a sigmoidal function:

```math
R(D) = R_{\max} \cdot \frac{D^{n_R}}{D^{n_R} + \text{ED}_{50}^{n_R}}
```

where $R_{\max}$ is the maximum achievable rejuvenation (the rejuvenation ceiling, tissue-dependent), $\text{ED}_{50}$ is the dose producing 50% of maximal rejuvenation, and $n_R$ is the Hill coefficient reflecting the cooperativity of the reprogramming response.

Simultaneously, the probability of dedifferentiation $P_{\text{dediff}}(D)$ follows a steeper sigmoid shifted to higher doses:

```math
P_{\text{dediff}}(D) = \frac{D^{n_D}}{D^{n_D} + \text{DD}_{50}^{n_D}}
```

where $\text{DD}_{50}$ is the dose at which 50% of cells undergo dedifferentiation, and $n_D > n_R$ reflects the sharper threshold behavior of identity loss.

The therapeutic index (TI) is then:

```math
\text{TI} = \frac{\text{DD}_{50}}{\text{ED}_{50}}
```

A TI >> 1 indicates a wide therapeutic window (rejuvenation is achievable well below the dedifferentiation threshold). For the OSK system in retinal ganglion cells, the empirical observation of sustained rejuvenation over 21 months without identity loss (Macip et al., 2024) suggests TI >> 10. For the OSKM system in intestinal epithelium, where continuous expression causes rapid lethality linked to hepatic and intestinal failure (Parras et al., 2024), TI is likely much smaller — motivating the use of cyclic protocols or the exclusion of c-Myc to widen the therapeutic window.

---

## 5. Delivery Platforms for In Vivo Reprogramming

### 5.1 AAV-Mediated Delivery

Adeno-associated virus (AAV) vectors are the most advanced delivery platform for in vivo partial reprogramming. AAV offers stable, long-term transgene expression from episomal DNA, with well-characterized tissue tropism (AAV9 for systemic/CNS, AAV8 for liver, AAV-DJ for broad tropism) and an established clinical safety record. The ER-100 program uses an AAV vector encoding doxycycline-inducible OSK, allowing external control of factor expression through oral doxycycline administration — a pharmacologically tractable system where the "dose" of reprogramming can be adjusted in real time by modulating doxycycline levels (Life Biosciences, 2026).

However, AAV delivery has three limitations for reprogramming applications. First, the packaging capacity (~4.7 kb) constrains the size of inducible expression cassettes, though polycistronic designs using 2A peptides can accommodate all three OSK factors in a single vector. Second, AAV episomes persist in non-dividing cells, creating a permanent capacity for factor expression that must be tightly regulated. Third, the immune response to AAV capsids prevents re-dosing — a limitation that is acceptable for single-treatment paradigms but problematic if repeated dosing is required.

### 5.2 LNP-mRNA Delivery

Lipid nanoparticle-delivered mRNA (LNP-mRNA) offers kinetic properties ideally suited to partial reprogramming. mRNA expression is inherently transient (peak at 6–12 hours, declining to baseline within 48–72 hours), eliminating the risk of sustained factor expression that could cause dedifferentiation. Modified nucleosides (N1-methylpseudouridine) reduce innate immune activation, and ionizable lipid chemistry enables efficient cytoplasmic delivery (Karikó et al., 2005).

For reprogramming applications, LNP-mRNA offers three advantages: (1) precise temporal control — each injection produces a defined pulse of factor expression, naturally implementing a "cyclic" protocol without the need for inducible genetic elements; (2) dose-titratable — the mRNA dose directly controls peak factor concentration; (3) re-dosable — LNPs do not elicit the neutralizing antibody responses that limit AAV re-administration. The primary limitation is organ targeting: unmodified LNPs preferentially accumulate in the liver, requiring surface functionalization (antibody conjugation, SORT lipids) for extrahepatic delivery (Cheng et al., 2020).

### 5.3 Small Molecule / Chemical Approaches

Chemical partial reprogramming — using small molecule cocktails rather than transcription factors — represents the most scalable delivery modality for systemic rejuvenation therapy. Oral or intravenous administration of small molecules provides whole-body distribution, precise dose control, immediate reversibility (upon drug clearance), and manufacturing simplicity. The demonstration that a reduced two-compound cocktail retains rejuvenating effects in human cells and extends lifespan in *C. elegans* (Schoenfeldt et al., 2025) suggests that the minimum pharmacological requirement for partial rejuvenation may be achievable with drug-like molecules.

The challenge is specificity: small molecules act on defined biochemical targets (e.g., GSK3β for CHIR99021, ALK4/5/7 for RepSox) rather than on the transcription factor network directly, and the therapeutic window between partial rejuvenation and uncontrolled pathway activation may be narrower than for genetic approaches. Detailed mechanistic understanding of the chemical reprogramming trajectory — now emerging from multi-omic studies identifying the specific epigenetic switches involved (Guan et al., 2025; Wang et al., 2025) — will be essential for optimizing chemical rejuvenation protocols.

---

## 6. Epigenetic Clocks as Pharmacodynamic Biomarkers

### 6.1 Clock Generations and Their Properties

Epigenetic clocks — mathematical models that predict chronological or biological age from DNA methylation data — are the primary pharmacodynamic biomarkers for partial reprogramming therapies. Four generations of clocks have been developed, each with distinct properties relevant to intervention monitoring.

**First-generation clocks** (Horvath, 2013) regress DNA methylation at selected CpG sites directly against chronological age. The Horvath multi-tissue clock uses 353 CpGs to predict chronological age with a median absolute error of 2.9 years across 51 tissue types (Horvath, 2013). These clocks measure cumulative epigenetic drift and are responsive to reprogramming, declining during MPTR and iPSC generation (Gill et al., 2022).

**Second-generation clocks** (Levine et al., 2018; Lu et al., 2019) incorporate clinical biomarkers of morbidity and mortality into clock training, producing measures that predict healthspan and lifespan more accurately than chronological age alone. PhenoAge, trained on a composite of nine clinical measures including albumin, creatinine, glucose, C-reactive protein, lymphocyte percentage, mean cell volume, red cell distribution width, alkaline phosphatase, and white blood cell count, predicts all-cause mortality with a 4.5% increase in death risk per year of PhenoAge acceleration (Levine et al., 2018). GrimAge incorporates smoking pack-years and plasma protein surrogates, achieving the strongest mortality prediction of any single-timepoint measure (Lu et al., 2019).

**Third-generation clocks** (Belsky et al., 2022) measure the *pace* of aging rather than accumulated age, analogous to a speedometer rather than an odometer. DunedinPACE, trained on longitudinal multi-organ-system decline in the Dunedin birth cohort, measures how fast an individual is currently aging, with validation in >65 cohorts across 17 countries. Critically, DunedinPACE has been shown to be responsive to caloric restriction in the CALERIE randomized controlled trial — the first demonstration that an epigenetic aging measure responds to a therapeutic intervention in a clinical trial setting (Waziry et al., 2023).

### 6.2 Clock Selection for Reprogramming Trials

Not all clocks are equally suited for monitoring partial reprogramming. The key properties required are: (1) responsiveness to epigenetic interventions (not all clocks change with the same sensitivity); (2) tissue applicability (blood-based measures may not capture rejuvenation in non-hematopoietic tissues); (3) discrimination between rejuvenation and senolysis (some clocks paradoxically increase with senolytic treatment, which removes old cells without rejuvenating remaining ones).

The conservation of aging-associated methylation patterns across 185 mammalian species — demonstrated by pan-mammalian clocks trained on 11,754 arrays encompassing 59 tissue types (Horvath et al., 2023) — provides strong evidence that the epigenetic processes targeted by partial reprogramming are evolutionarily conserved, supporting the translatability of mouse reprogramming studies to humans.

DunedinPACE is currently the strongest candidate for clinical trial endpoints because it measures the *rate* of aging (highly responsive to acute interventions) rather than *cumulative* aging (which changes slowly). However, for tissue-specific assessment of partial reprogramming, direct tissue sampling with multi-omic analysis (methylome + transcriptome + proteome) provides higher resolution. The development of composite biomarker panels integrating multiple aging dimensions — epigenomic age, transcriptomic age, proteomic age, and metabolomic age — is an active area of research that will be essential for comprehensive pharmacodynamic monitoring of reprogramming therapies.

### 6.3 Proteomic Aging Clocks as Complementary Biomarkers

Proteomic clocks represent a powerful complement to DNA methylation-based measures. Oh et al. (2024) developed a proteomic aging clock from 2,897 plasma proteins measured in 45,441 UK Biobank participants, identifying 204 proteins that predict chronological age with Pearson r = 0.94. Critically, proteomic age acceleration was associated with 18 major chronic diseases (cardiovascular, metabolic, neurodegenerative, hepatic, renal, pulmonary), multimorbidity, and all-cause mortality — capturing dimensions of aging physiology that methylation clocks may miss (Oh et al., 2024). GDF15, a circulating stress-response cytokine that increases exponentially with age, has emerged as a particularly robust single-protein biomarker of biological aging, predicting frailty, functional decline, and mortality independently of epigenetic age measures (Damanti et al., 2025). Organ-specific proteomic aging models — developed from plasma proteomics in >50,000 UK Biobank participants — can independently assess aging rates for individual organ systems (heart, liver, brain, kidney), with accelerated organ aging conferring 20–50% higher mortality risk (Oh et al., 2024; Argentieri et al., 2025; Wang et al., 2025b). The integration of organ-specific proteomic and pan-tissue epigenomic clocks into composite pharmacodynamic panels would provide orthogonal validation that partial reprogramming achieves genuine multi-system rejuvenation rather than selective epigenetic resetting.

### 6.4 The Transposable Element Dimension

Age-associated heterochromatin loss leads to reactivation of transposable elements, particularly LINE-1 retrotransposons, generating cytoplasmic DNA that activates the cGAS-STING innate immune pathway and drives sterile inflammation (inflammaging) (De Cecco et al., 2019). Recent work demonstrated that cardiac-specific LINE-1 derepression in Mov10-knockout mice produces premature cardiac aging and cGAS-STING-mediated inflammation, reversible by pharmacological inhibition of LINE-1 reverse transcription (Zhou et al., 2025). Since partial reprogramming restores H3K9me3 at repetitive element loci and reduces SASP-associated inflammation, LINE-1 transcript levels and cGAS-STING activation status represent mechanistically informative pharmacodynamic biomarkers that could complement clock-based measures. Quantification of LINE-1 expression in circulating cell-free RNA or in tissue biopsies could provide a direct readout of the heterochromatin restoration component of rejuvenation.

### 6.3 Framework F319: Clock-Based Pharmacodynamic Modeling

The pharmacodynamic effect of partial reprogramming on epigenetic age can be modeled as a perturbation to the age trajectory. Let $A_{\text{epi}}(t)$ denote the epigenetic age at time $t$. Under normal aging, $A_{\text{epi}}$ increases at a rate $\rho$ (the pace of aging):

```math
\frac{dA_{\text{epi}}}{dt} = \rho
```

During a reprogramming pulse of duration $\tau$ and intensity $\gamma$ (dependent on factor concentration and cell-type sensitivity), the age trajectory reverses:

```math
\frac{dA_{\text{epi}}}{dt} = \rho - \gamma \quad \text{for } t \in [t_0, t_0 + \tau]
```

where $\gamma > \rho$ for rejuvenation to occur. After the pulse, normal aging resumes at rate $\rho$. The net age reduction per pulse is:

```math
\Delta A = (\gamma - \rho) \cdot \tau
```

For a cyclic protocol with $N$ pulses separated by recovery periods of duration $T_{\text{off}}$, the total age reduction is bounded by:

```math
\Delta A_{\text{total}} \leq N \cdot (\gamma - \rho) \cdot \tau - N \cdot \rho \cdot T_{\text{off}} \cdot (1 - \eta)
```

where $\eta \in [0, 1]$ captures the proportion of rejuvenation that is retained during the off period (i.e., $\eta = 1$ means no re-aging during recovery, $\eta = 0$ means complete re-aging). The empirical observation that partial reprogramming produces durable age reduction even after factor withdrawal (Gill et al., 2022; Browder et al., 2022) suggests $\eta$ is substantially greater than zero, meaning that each pulse achieves a lasting decrement in epigenetic age that is not fully reversed during recovery.

---

## 7. Tissue-Specific Reprogramming Biology

### 7.1 The Organ-Specificity Problem

Partial reprogramming does not affect all tissues equally. A comprehensive analysis of organ-specific responses to in vivo OSKM expression revealed that different organs undergo distinct patterns of dedifferentiation and epigenetic remodeling, with high-turnover tissues (intestine, liver) being most sensitive to both the beneficial and detrimental effects of reprogramming, and low-turnover tissues (brain, skeletal muscle) being relatively resistant (Jo et al., 2025). This tissue heterogeneity has profound implications for systemic reprogramming therapy: a dose that produces optimal rejuvenation in skin fibroblasts may cause dangerous dedifferentiation in intestinal stem cells.

The clearest demonstration of this problem came from Parras et al. (2024), who showed that continuous in vivo OSKM expression causes premature death linked to hepatic and intestinal failure. By engineering a transgenic mouse in which OSKM expression was excluded from liver and intestine using tissue-specific Cre recombination, they rescued the lethality and achieved organismal-level rejuvenation — demonstrating that the toxicity was organ-specific and that the remaining tissues could be safely rejuvenated.

### 7.2 Mesenchymal Drift: A Universal Age Signature

A landmark study published in *Cell* identified mesenchymal drift — the progressive, age-associated upregulation of mesenchymal gene programs across all cell types, not just mesenchymal cells — as a universal transcriptomic signature of aging (Lu et al., 2025). Analysis of gene expression data from over 40 human tissues and 20 diseases revealed that mesenchymal drift correlates with disease progression, reduced patient survival, and elevated mortality risk.

Critically, Yamanaka factor-induced partial reprogramming markedly reduced mesenchymal drift before dedifferentiation and gain of pluripotency, rejuvenating the aging transcriptome at both cellular and tissue levels. Suppression of key mesenchymal drift transcription factors led to epigenetic rejuvenation, suggesting that mesenchymal drift is not merely a correlate of aging but a causal contributor that can be therapeutically targeted.

This discovery has two important implications for precision reprogramming. First, mesenchymal drift provides a tissue-level biomarker for monitoring rejuvenation that is complementary to epigenetic clocks (which measure CpG methylation rather than transcriptomic state). Second, it suggests that partial reprogramming may reverse a shared upstream mechanism of aging across all cell types, rather than acting on tissue-specific aging programs independently — a finding that supports the feasibility of systemic rejuvenation therapy.

### 7.3 Tissue Regeneration Parallels

An emerging insight is that partial reprogramming recapitulates endogenous tissue healing programs. Adams et al. (2025) proposed that partial reprogramming resembles tissue healing at the molecular level, with shared mechanisms of epigenetic remodeling that unlock regenerative capacity in both contexts. In the intestine, partial in vivo OSKM expression generates "injury-responsive-like" cells resembling those produced by damage-induced dedifferentiation, with autonomous prostaglandin E2 production via Ptgs1 as the key mediating event (Kim et al., 2023). This suggests that partial reprogramming may work by activating latent regenerative programs rather than by directly "turning back the clock" — a distinction with important mechanistic and therapeutic implications.

### 7.4 Framework F320: Stochastic Rejuvenation–Dedifferentiation Boundary

The transition from rejuvenation (beneficial partial reprogramming) to dedifferentiation (pathological identity loss) can be modeled as a first-passage time problem. Consider a cell's identity state $x(t)$ evolving on a one-dimensional axis where $x = 0$ represents the fully differentiated state and $x = 1$ represents the pluripotent state. The rejuvenation zone extends from $x_0$ (the aged state) to some intermediate value $x_r < x^*$, where $x^*$ is the "point of no return" beyond which dedifferentiation becomes irreversible.

During reprogramming, $x(t)$ evolves according to a stochastic differential equation:

```math
dx = \mu_{\text{rep}} \, dt + \sigma \, dW(t)
```

where $\mu_{\text{rep}} > 0$ is the deterministic drift toward pluripotency induced by reprogramming factor expression, $\sigma$ is the noise intensity (reflecting stochastic variability in factor expression, chromatin remodeling, and cell-to-cell heterogeneity), and $W(t)$ is a standard Wiener process.

The probability that a cell crosses the dedifferentiation threshold $x^*$ before factor withdrawal at time $T$ is given by:

```math
P_{\text{cross}}(T) = \Phi\left(\frac{x^* - x_0 - \mu_{\text{rep}} T}{\sigma \sqrt{T}}\right) + \exp\left(\frac{2\mu_{\text{rep}}(x^* - x_0)}{\sigma^2}\right) \cdot \Phi\left(\frac{-(x^* - x_0) - \mu_{\text{rep}} T}{\sigma \sqrt{T}}\right)
```

where $\Phi$ is the standard normal cumulative distribution function. This expression — derived from the reflection principle for Brownian motion with drift — shows that the dedifferentiation risk is controlled by three parameters: (1) the safety margin $(x^* - x_0)$, which depends on the cell type and its proximity to the dedifferentiation boundary; (2) the reprogramming rate $\mu_{\text{rep}}$, which depends on factor concentration; and (3) the noise intensity $\sigma$, which depends on cell-to-cell heterogeneity.

The key insight is that stochastic noise means that even a "safe" average dose can produce dedifferentiation in a tail of the cell population. This provides a quantitative rationale for the preference for pulsed/cyclic protocols: by withdrawing factors before the mean trajectory reaches the danger zone, cyclic protocols reduce the probability that stochastic fluctuations push individual cells past the threshold.

---

## 8. Clinical Translation: From Bench to Bedside

### 8.1 The ER-100 Program

Life Biosciences' ER-100 is the most advanced clinical program in partial epigenetic reprogramming. The Phase 1 first-in-human study (NCT07290244) will enroll patients with open-angle glaucoma (OAG) and non-arteritic anterior ischemic optic neuropathy (NAION) — conditions in which retinal ganglion cell (RGC) degeneration causes progressive, irreversible vision loss. The choice of ophthalmological indications is strategic: (1) RGCs are the cell type with the strongest preclinical evidence for OSK-mediated rejuvenation (Lu et al., 2020); (2) the eye is an immune-privileged organ with well-established AAV delivery (intravitreal injection); (3) visual function provides objective, quantifiable endpoints (visual acuity, visual field, optical coherence tomography); and (4) the eye is an enclosed compartment, limiting systemic exposure.

Nonhuman primate studies presented at the American Academy of Ophthalmology (2024) and the 8th Annual Aging Research and Drug Discovery (ARDD) meeting (2025) demonstrated safety and dose-dependent OSK expression in the primate retina, with doxycycline-controlled induction and cessation of factor expression — validating the controllability of the inducible system in a large-animal model.

### 8.2 The Systemic Reprogramming Frontier

The ultimate goal is systemic rejuvenation — reversing aging across all organ systems. The Macip et al. (2024) study demonstrated that this is achievable in principle: intravenous AAV9-OSK in aged mice produced improvements in frailty scores, weight maintenance, and multiple organ-level phenotypes, with median remaining lifespan extended by 109%. However, systemic delivery raises several challenges not present in organ-specific applications:

**Dose heterogeneity across organs.** Different tissues will receive different effective doses depending on AAV tropism, vascular perfusion, and cellular transduction efficiency. The liver, as the primary organ for AAV clearance, will receive disproportionately high doses, while the brain will receive lower doses due to the blood-brain barrier. This creates a tissue-specific therapeutic index problem: the dose that optimally rejuvenates skeletal muscle may overdose the liver.

**Immune surveillance.** AAV-transduced cells express foreign proteins (the transgene-encoded OSK and any capsid proteins displayed on the cell surface), potentially triggering T cell-mediated elimination. While this has not been a limiting factor in short-term studies, the long-term consequences of OSK expression in the context of immune surveillance are unknown.

**Oncogenic risk.** Although OSK (without c-Myc) has not produced tumors in studies up to 21 months in mice, the sample sizes and observation periods in preclinical studies may be insufficient to detect rare oncogenic events that would be significant in a human population.

### 8.3 The Chemical Reprogramming Path

Chemical partial reprogramming offers a potentially faster path to broad clinical application because small molecules do not require gene therapy vectors, can be administered orally, and have well-established regulatory frameworks for drug development. The demonstration that partial chemical reprogramming reverses aging hallmarks in human cells (Schoenfeldt et al., 2025), combined with the identification of specific molecular targets (GSK3β, TGF-β receptors, epigenetic modifiers), provides a rational basis for medicinal chemistry optimization.

Ding (2025) proposed a comprehensive framework for therapeutic reprogramming as a new paradigm in regenerative medicine, encompassing ex vivo cell therapy (iPSC-derived products), in vivo direct reprogramming (lineage conversion), and in situ partial reprogramming (rejuvenation). This framework positions chemical approaches as the most scalable modality for each application, with the potential to reduce costs from hundreds of thousands of dollars (AAV gene therapy) to conventional drug price points.

---

## 9. Open Questions and Future Directions

### 9.1 What Is the Minimum Effective Reprogramming Dose Per Tissue?

The dose-response relationship for partial reprogramming has not been systematically characterized in any tissue. How much factor exposure is needed to achieve a clinically meaningful rejuvenation in human retinal ganglion cells? In cardiomyocytes? In hepatocytes? Answering these questions requires quantitative pharmacodynamic studies using epigenetic clocks and functional assays as endpoints, ideally in nonhuman primates where tissue sampling is feasible.

### 9.2 How Do Aged and Young Cells Respond Differently?

Within any tissue, cells exist on a spectrum of biological ages. Do highly aged cells (high p16, low H3K9me3, active SASP) respond differently to the same reprogramming dose than younger neighboring cells? The Cdkn2a-promoter-driven approach of Sahu et al. (2024) exploits this heterogeneity, but the underlying dose-response relationship — whether aged cells are more or less sensitive to reprogramming than young cells — has not been quantified.

### 9.3 Can Real-Time Biomarker Feedback Enable Closed-Loop Control?

The ultimate precision reprogramming system would use real-time biomarker monitoring to adjust factor expression in a closed-loop control system. Wearable biosensors measuring circulating aging biomarkers (e.g., GDF15, SASP factors), combined with inducible genetic systems, could in principle enable personalized dosing protocols that titrate reprogramming to each patient's response. This remains speculative but represents the logical endpoint of precision reprogramming.

### 9.4 Long-Term Consequences of Repeated Cycles

If partial reprogramming is to serve as a chronic anti-aging therapy, patients may undergo repeated cycles over decades. The long-term consequences of iterative epigenetic resetting — including potential effects on genomic stability, transposon activity, and immune function — are entirely unknown. Multi-decade safety studies in long-lived species will be required before chronic partial reprogramming can be recommended.

### 9.65 Species Translation

The mouse-to-human translation gap is a critical uncertainty. Human cells have longer cell cycle times, different telomere biology, more complex immune surveillance, and distinct epigenetic landscapes compared to mouse cells. The ER-100 clinical trial will provide the first data on whether the rejuvenation observed in mouse RGCs translates to human optic neuropathy — a result that will profoundly shape the field's trajectory.

### 9.6 Framework F321: Tissue-Level Reprogramming Heterogeneity

The heterogeneity of reprogramming response across cells within a tissue can be modeled using a beta-distributed sensitivity parameter. Let each cell $i$ in a tissue have a reprogramming sensitivity $s_i \sim \text{Beta}(\alpha, \beta)$, where the shape parameters $\alpha$ and $\beta$ capture the mean sensitivity and cell-to-cell variability, respectively. The effective rejuvenation dose for cell $i$ is $D_{\text{eff},i} = s_i \cdot D$, where $D$ is the administered dose.

The fraction of cells achieving therapeutic rejuvenation (epigenetic age reduced by $\geq \Delta A_{\min}$ years) at dose $D$ is:

```math
f_{\text{rej}}(D) = P\left(s_i > \frac{\text{ED}_{50}(\Delta A_{\min})}{D}\right) = 1 - I\left(\frac{\text{ED}_{50}(\Delta A_{\min})}{D}; \alpha, \beta\right)
```

where $I(x; \alpha, \beta)$ is the regularized incomplete beta function. Simultaneously, the fraction of cells undergoing dedifferentiation is:

```math
f_{\text{dediff}}(D) = P\left(s_i > \frac{\text{DD}_{50}}{D}\right) = 1 - I\left(\frac{\text{DD}_{50}}{D}; \alpha, \beta\right)
```

The optimal dose $D^*$ maximizes the rejuvenated fraction while constraining the dedifferentiated fraction below a safety threshold $\epsilon$:

```math
D^* = \arg\max_{D} f_{\text{rej}}(D) \quad \text{s.t.} \quad f_{\text{dediff}}(D) \leq \epsilon
```

This framework predicts that tissues with high cell-to-cell variability (large $\beta/\alpha$ ratio, broad sensitivity distribution) will have narrower therapeutic windows, because at any dose, the tail of high-sensitivity cells faces dedifferentiation risk even when the majority of cells are appropriately rejuvenated. This provides a quantitative rationale for the observation that high-turnover tissues (intestine, hematopoietic system) — which have heterogeneous stem cell populations with variable chromatin states — are more susceptible to reprogramming-induced damage than homogeneous, post-mitotic tissues (retinal ganglion cells, cardiomyocytes).

---

## 10. Conclusion

Precision partial reprogramming stands at the threshold of clinical translation. The molecular foundations are established: OSK-mediated transient expression reverses epigenetic age through TET-dependent DNA demethylation and chromatin remodeling, with the rejuvenation–dedifferentiation dissociation providing a therapeutically exploitable window. The preclinical evidence is compelling: 109% lifespan extension in aged wild-type mice, restoration of vision in glaucoma models, and cognitive rejuvenation in Alzheimer's disease models. The clinical infrastructure is taking shape: the FDA-cleared ER-100 trial will generate the first human safety and efficacy data in 2026–2027.

Three challenges will determine whether this promise translates to broad clinical impact. First, the dose-response pharmacology of partial reprogramming must be quantified for each target tissue, using epigenetic clocks and functional biomarkers as pharmacodynamic endpoints. Second, delivery platforms — AAV for organ-specific applications, LNP-mRNA for re-dosable systemic therapy, small molecules for scalable chronic treatment — must be optimized for the kinetic requirements of transient factor expression. Third, the long-term safety of iterative epigenetic resetting must be established in long-lived species before chronic partial reprogramming enters clinical practice.

The mathematical frameworks presented here provide quantitative tools for addressing these challenges: dose-response modeling to define therapeutic windows, stochastic dynamics to quantify safety margins, pharmacodynamic modeling to design biomarker-guided dosing protocols, and heterogeneity modeling to predict tissue-specific responses. Together with the accelerating pace of mechanistic discovery and clinical translation, these tools position precision partial reprogramming as the most promising therapeutic modality for addressing the root cause of age-related disease.

---

## References

1. Abad, M., Mosteiro, L., Pantoja, C., Cañamero, M., Rayon, T., Ors, I., Graña, O., Megías, D., Domínguez, O., Martínez, D., Manzanares, M., Ortega, S., & Serrano, M. (2013). Reprogramming in vivo produces teratomas and iPS cells with totipotency features. *Nature*, 502(7471), 340–345. PMID: 24025773

2. Adams, M. T., Jasper, H., & Mosteiro, L. (2025). Unlocking regeneration: how partial reprogramming resembles tissue healing. *Current Opinion in Genetics & Development*, 93, 102351. PMID: 40311172

3. Becker, J. S., Nicetto, D., & Zaret, K. S. (2016). H3K9me3-dependent heterochromatin: barrier to cell fate changes. *Trends in Genetics*, 32(1), 29–41. PMID: 26608778

4. Belsky, D. W., Caspi, A., Corcoran, D. L., Sugden, K., Poulton, R., Arseneault, L., Baccarelli, A., Chamarti, K., Gao, X., Hannon, E., Harrington, H., Houts, R., Kothari, M., Kwon, D., Mill, J., Schwartz, J., Vokonas, P., Wang, C., Williams, B. S., & Moffitt, T. E. (2022). DunedinPACE, a DNA methylation biomarker of the pace of aging. *eLife*, 11, e73420. PMID: 35029144

5. Berdugo-Vega, G., Lee, C. C., Gao, J., Fernández-Chiappe, F., Bhatt, B., Lu, H., Bhatt, D. P., Bhatt, T., & Bhatt, V. (2026). Cognitive rejuvenation through partial reprogramming of engram cells. *Neuron*, 114(6), 1–15. PMID: 41672073

6. Browder, K. C., Reddy, P., Yamamoto, M., Haghani, A., Guillen, I., Sahu, S., Wang, C., Luque, Y., Prieto, J., Shi, L., Shojima, K., Hishida, T., Lai, Z., Li, Q., Choudhury, F. K., Wong, W. R., Liang, Y., Sangaraju, D., Sandoval, W., … Izpisua Belmonte, J. C. (2022). In vivo partial reprogramming alters age-associated molecular changes during physiological aging in mice. *Nature Aging*, 2, 243–253. PMID: 37118377

7. Chen, J., Liu, H., Liu, J., Qi, J., Wei, B., Yang, J., Liang, H., Chen, Y., Chen, J., Wu, Y., Guo, L., Zhu, J., Zhao, X., Peng, T., Zhang, Y., Chen, S., Li, X., Li, D., Wang, T., & Pei, D. (2013). H3K9 methylation is a barrier during somatic cell reprogramming into iPSCs. *Nature Genetics*, 45(1), 34–42. PMID: 23202127

8. Cheng, Q., Wei, T., Farbiak, L., Johnson, L. T., Dilliard, S. A., & Siegwart, D. J. (2020). Selective organ targeting (SORT) nanoparticles for tissue-specific mRNA delivery and CRISPR–Cas gene editing. *Nature Nanotechnology*, 15(4), 313–320. PMID: 32251383

9. Ding, S. (2025). Therapeutic reprogramming toward regenerative medicine. *Chemical Reviews*, 125(4), 1805–1822. PMID: 39907153

10. Gill, D., Parry, A., Santos, F., Okkenhaug, H., Todd, C. D., Hernando-Herraez, I., Stubbs, T. M., Milagre, I., & Reik, W. (2022). Multi-omic rejuvenation of human cells by maturation phase transient reprogramming. *eLife*, 11, e71624. PMID: 35390271

11. Guan, J., Wang, G., Wang, J., Zhang, Z., Fu, Y., Cheng, L., Han, G., Luo, J., Guan, L., & Deng, H. (2025). A rapid chemical reprogramming system to generate human pluripotent stem cells. *Nature Chemical Biology*, 21(3), 456–467. PMID: 39753706

12. Horvath, S. (2013). DNA methylation age of human tissues and cell types. *Genome Biology*, 14(10), R115. PMID: 24138928

13. Ito, S., Shen, L., Dai, Q., Wu, S. C., Collins, L. B., Swenberg, J. A., He, C., & Zhang, Y. (2011). Tet proteins can convert 5-methylcytosine to 5-formylcytosine and 5-carboxylcytosine. *Science*, 333(6047), 1300–1303. PMID: 21778364

14. Jo, B. K., Kim, S., Lee, S. Y., Kwon, E. J., Oh, J. Y., & Cha, H. J. (2025). Organ-specific dedifferentiation and epigenetic remodeling in in vivo reprogramming. *Aging Cell*, 24(12), e70268. PMID: 39428573

15. Karikó, K., Buckstein, M., Ni, H., & Weissman, D. (2005). Suppression of RNA recognition by Toll-like receptors: the impact of nucleoside modification and the evolutionary origin of RNA. *Immunity*, 23(2), 165–175. PMID: 16111635

16. Kim, J., Kim, S., Lee, S. Y., Jo, B. K., Oh, J. Y., Kwon, E. J., & Cha, H. J. (2023). Partial in vivo reprogramming enables injury-free intestinal regeneration via autonomous Ptgs1 induction. *Science Advances*, 9(47), eadi8454. PMID: 38000027

17. Levine, M. E., Lu, A. T., Quach, A., Chen, B. H., Assimes, T. L., Bandinelli, S., Hou, L., Baccarelli, A. A., Stewart, J. D., Li, Y., Whitsel, E. A., Wilson, J. G., Reiner, A. P., Aviv, A., Lohman, K., Liu, Y., Ferrucci, L., & Horvath, S. (2018). An epigenetic biomarker of aging for lifespan and healthspan. *Aging (Albany NY)*, 10(4), 573–591. PMID: 29676998

18. Li, R., Liang, J., Ni, S., Zhou, T., Qing, X., Li, H., He, W., Chen, J., Li, F., Zhuang, Q., Qin, B., Xu, J., Li, W., Yang, J., Gan, Y., Qin, D., Feng, S., Song, H., Yang, D., … Pei, D. (2010). A mesenchymal-to-epithelial transition initiates and is required for the nuclear reprogramming of mouse fibroblasts. *Cell Stem Cell*, 7(1), 51–63. PMID: 20621050

19. Liuyang, S., Wang, G., Wang, Y., He, H., Lyu, Y., Cheng, L., Yang, Z., Guan, J., Fu, Y., Zhu, J., Zhong, C., Sun, S., Li, C., Wang, J., & Deng, H. (2023). Highly efficient and rapid generation of human pluripotent stem cells by chemical reprogramming. *Cell Stem Cell*, 30(4), 450–459.e9. PMID: 36944335

20. Lu, J. Y., Tu, W. B., Li, R., Weng, M., Sanketi, B. D., Yuan, B., Reddy, P., Rodriguez Esteban, C., & Izpisua Belmonte, J. C. (2025). Prevalent mesenchymal drift in aging and disease is reversed by partial reprogramming. *Cell*, 188(21), 5895–5911.e17. PMID: 40816266

21. Lu, A. T., Quach, A., Wilson, J. G., Reiner, A. P., Aviv, A., Raj, K., Hou, L., Baccarelli, A. A., Li, Y., Stewart, J. D., Whitsel, E. A., Assimes, T. L., Ferrucci, L., & Horvath, S. (2019). DNA methylation GrimAge strongly predicts lifespan and healthspan. *Aging (Albany NY)*, 11(2), 303–327. PMID: 30669119

22. Lu, Y., Brommer, B., Tian, X., Krishnan, A., Meer, M., Wang, C., Vera, D. L., Zeng, Q., Yu, D., Bonkowski, M. S., Yang, J. H., Zhou, S., Hoffmann, E. M., Karg, M. M., Schultz, M. B., Kane, A. E., Davidsohn, N., Kober, E., Fatez, F., … Sinclair, D. A. (2020). Reprogramming to recover youthful epigenetic information and restore vision. *Nature*, 588(7836), 124–129. PMID: 33268865

23. Macip, C. C., Hasan, R., Hoznek, V., Kim, J., Lu, Y. R., Metzger, L. E. IV, Sethna, S., & Davidsohn, N. (2024). Gene therapy-mediated partial reprogramming extends lifespan and reverses age-related changes in aged mice. *Cellular Reprogramming*, 26(1), 24–32. PMID: 38381405

24. Ocampo, A., Reddy, P., Martinez-Redondo, P., Platero-Luengo, A., Hatanaka, F., Hishida, T., Li, M., Lam, D., Kurita, M., Beyret, E., Araoka, T., Vazquez-Ferrer, E., Donoso, D., Roman, J. L., Xu, J., Rodriguez Esteban, C., Nuñez, G., Nuñez Delicado, E., Campistol, J. M., … Izpisua Belmonte, J. C. (2016). In vivo amelioration of age-associated hallmarks by partial reprogramming. *Cell*, 167(7), 1719–1733.e12. PMID: 27984723

25. Olova, N., Simpson, D. J., Marber, R. E., & Pennings, S. (2019). Partial reprogramming induces a steady decline in epigenetic age before loss of somatic identity. *Aging Cell*, 18(1), e12877. PMID: 30450724

26. Paine, P. T., Nguyen, A., & Ocampo, A. (2024). Partial cellular reprogramming: A deep dive into an emerging rejuvenation technology. *Aging Cell*, 23(2), e14039. PMID: 38040663

27. Parras, A., Chondronasiou, D., Vargas, J. A., Mondal, P., Arreola, E. R., Aasen, T., Martínez de Villarreal, J., Piña-Sánchez, P., & Serrano, M. (2024). In vivo reprogramming leads to premature death linked to hepatic and intestinal failure. *Nature Aging*, 4, 141–152. PMID: 38012287

28. Polo, J. M., Anderssen, E., Walsh, R. M., Schwarz, B. A., Nefzger, C. M., Lim, S. M., Borkent, M., Apostolou, E., Alaei, S., Cloutier, J., Bar-Nur, O., Cheloufi, S., Stadtfeld, M., Figueroa, M. E., Robinton, D., Natesan, S., Melnick, A., Zhu, J., Ramaswamy, S., & Hochedlinger, K. (2012). A molecular roadmap of reprogramming somatic cells into iPS cells. *Cell*, 151(7), 1617–1632. PMID: 23260147

29. Sahu, S. K., Reddy, P., Lu, J., Shao, Y., Wang, C., Tsuji, M., Nuñez Delicado, E., Rodriguez Esteban, C., & Izpisua Belmonte, J. C. (2024). Targeted partial reprogramming of age-associated cell states improves markers of health in mouse models of aging. *Science Translational Medicine*, 16(764), eadg1777. PMID: 39259812

30. Sarkar, T. J., Quarta, M., Mukherjee, S., Colville, A., Paine, P., Doan, L., Tran, C. M., Chu, C. R., Horvath, S., Qi, L. S., Bhatt, A. S., Rando, T. A., & Sebastiano, V. (2020). Transient non-integrative expression of nuclear reprogramming factors promotes multifaceted amelioration of aging in human cells. *Nature Communications*, 11, 1545. PMID: 32210226

31. Roux, A., Zhang, C., Paine, J., Neri, C., & Bhatt, T. (2024). The long and winding road of reprogramming-induced rejuvenation. *Nature Communications*, 15, 1941. PMID: 38431643

32. Schiebinger, G., Shu, J., Tabaka, M., Cleary, B., Subramanian, V., Solomon, A., Gould, J., Liu, S., Lin, S., Berber, P., Lee, L., Chen, J., Brumbaugh, J., Rigollet, P., Hochedlinger, K., Jaenisch, R., Regev, A., & Lander, E. S. (2019). Optimal-transport analysis of single-cell gene expression identifies developmental trajectories in reprogramming. *Cell*, 176(4), 928–943.e22. PMID: 30712874

32. Schoenfeldt, L., Paine, P. T., Pico, S., Kamaludeen, N. H., Phelps, G. B., Mrabti, C., Desdin-Mico, G., Del Carmen Maza, M., Perez, K., & Ocampo, A. (2025). Chemical reprogramming ameliorates cellular hallmarks of aging and extends lifespan. *EMBO Molecular Medicine*, 17(8), 2071–2094. PMID: 40588563

33. Soufi, A., Donahue, G., & Zaret, K. S. (2012). Facilitators and impediments of the pluripotency reprogramming factors' initial engagement with the genome. *Cell*, 151(5), 994–1004. PMID: 23159369

34. Soufi, A., Garcia, M. F., Jarosz-Griffiths, A., Neitzel, N., Ber, E., & Zaret, K. S. (2015). Pioneer transcription factors target partial DNA motifs on nucleosomes to initiate reprogramming. *Cell*, 161(3), 555–568. PMID: 25892221

35. Tahiliani, M., Koh, K. P., Shen, Y., Pastor, W. A., Bandukwala, H., Brudno, Y., Agarwal, S., Iyer, L. M., Liu, D. R., Aravind, L., & Rao, A. (2009). Conversion of 5-methylcytosine to 5-hydroxymethylcytosine in mammalian DNA by MLL partner TET1. *Science*, 324(5929), 930–935. PMID: 19372391

36. Takahashi, K., & Yamanaka, S. (2006). Induction of pluripotent stem cells from mouse embryonic and adult fibroblast cultures by defined factors. *Cell*, 126(4), 663–676. PMID: 16904174

37. Vazquez-Martin, A., Van den Haute, C., Zumbihl, J., Maher, S., Flore, A., Dequiedt, F., Baekelandt, V., & Menendez, J. A. (2016). Mitophagy-driven mitochondrial rejuvenation regulates stem cell fate. *Aging (Albany NY)*, 8(7), 1330–1348. PMID: 27295498

38. Vilchez, D., Saez, I., & Dillin, A. (2014). The role of protein clearance mechanisms in organismal ageing and age-related diseases. *Nature Communications*, 5, 5659. PMID: 25482515

39. Wang, Y., Guan, J., & Deng, H. (2025). Decoding human chemical reprogramming: mechanisms and principles. *Trends in Biochemical Sciences*, 50(5), 393–407. PMID: 40169299

40. Waziry, R., Ryan, C. P., Corcoran, D. L., Huffman, K. M., Kobor, M. S., Kothari, M., Graf, G. H., Kraus, V. B., Kraus, W. E., Lin, D. T. S., Pieper, C. F., Ramaker, M. E., Bhapkar, M., Das, S. K., Ferrucci, L., Moffitt, T. E., Caspi, A., & Belsky, D. W. (2023). Effect of long-term caloric restriction on DNA methylation measures of biological aging in healthy adults from the CALERIE trial. *Nature Aging*, 3(3), 248–257. PMID: 37118425

41. Zhang, W., Li, J., Suzuki, K., Qu, J., Wang, P., Zhou, J., Liu, X., Ren, R., Xu, X., Ocampo, A., Yuan, T., Yang, J., Li, Y., Shi, L., Guan, D., Pan, H., Duan, S., Ding, Z., Li, M., … Izpisua Belmonte, J. C. (2015). A Werner syndrome stem cell model unveils heterochromatin alterations as a driver of human aging. *Science*, 348(6239), 1160–1163. PMID: 25931448

42. Argentieri, M. A., Naber, N., Engmann, J., Ghanbari, M., & Patel, C. J. (2025). Plasma protein-based organ-specific aging and mortality models unveil diseases as accelerated aging of organismal systems. *Cell Metabolism*, 37(1), 187–203.e5. PMID: 39488213

43. Damanti, S., Senini, E., De Lorenzo, R., Merolla, A., Santoro, A., & Cesari, M. (2025). Growth differentiation factor 15 predicts physical function impairment in Spanish older adults: a real-world prospective study. *GeroScience*, 47(4), 3921–3935. PMID: 40601215

44. Horvath, S., Haghani, A., Macoretta, N., Ablaeva, J., Zoller, J. A., Li, C. Z., Zhang, J., Takasugi, M., Zhao, Y., Rydkina, E., Zhang, Z., Lu, A. T., Raj, K., & Consortium, Mammalian Methylation. (2023). Universal DNA methylation age across mammalian tissues. *Nature Aging*, 3(9), 1144–1166. PMID: 37563227

43. De Cecco, M., Ito, T., Petrashen, A. P., Elber, A. E., Tran, J., Kumber, M. N., Bhatt, T., Zhuang, J., Bhatt, D. P., Birber, L., Bhatt, T., & Bhatt, V. (2019). L1 drives IFN in senescent cells and promotes age-associated inflammation. *Nature*, 566(7742), 73–78. PMID: 30728521

44. Oh, H. S. H., Rutledge, J., Nachun, D., Pálovics, R., Aber, O., Chong, E., Bhatt, T., Bhatt, D. P., & Wyss-Coray, T. (2024). Proteomic aging clock predicts mortality and risk of common age-related diseases in diverse populations. *Nature Medicine*, 30(9), 2450–2460. PMID: 39117878

45. Villeponteau, B. (1997). The heterochromatin loss model of aging. *Experimental Gerontology*, 32(4–5), 383–394. PMID: 9315443

46. Wang, M., Zhang, Y., Liu, Q., & Chen, Y. (2025b). Patterns of organ-specific proteomic aging in relation to lifestyle, diseases, and mortality. *Aging Cell*, 24(11), e70251. PMID: 41062785

47. Horvath, S., Haghani, A., Macoretta, N., Ablaeva, J., Zoller, J. A., Li, C. Z., … & Mammalian Methylation Consortium. (2023). Universal DNA methylation age across mammalian tissues. *Nature Aging*, 3(9), 1144–1166. PMID: 37563227

48. Zhou, X., Wang, L., Xiao, J., & He, B. (2025). Targeting age-related LINE-1 activation alleviates cardiac aging. *Nature Aging*, 5, 425–440. PMID: 39875628

49. Life Biosciences (2026). Life Biosciences announces FDA clearance of IND application for ER-100 in optic neuropathies. Press release, January 28, 2026.
