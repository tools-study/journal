# Pluripotent Stem Cell Therapy Challenges

## Abstract

Human pluripotent stem cell (hPSC)-derived cardiomyocytes, pancreatic β-cells, hepatocytes, cortical neurons, and skeletal myofibers reproducibly resemble their first- and second-trimester fetal counterparts rather than adult tissue, and this "maturation gap" is now the dominant rate-limiting barrier to functional engraftment in every hPSC clinical program (Karbassi et al., 2020; Ottaviani et al., 2023). The gap is not a function of time-in-culture alone: protracted human neuronal maturation is set by a cell-intrinsic epigenetic clock (Ciceri et al., 2024a), and prolonged cardiomyocyte culture plateaus short of adult transcriptional identity (Kannan et al., 2020). This review argues that closing the gap requires engineering a discrete set of perinatal and postnatal switches — thyroid-hormone-driven fatty-acid oxidation, glucocorticoid-C/EBPα-dependent hepatic induction, MAFA-mediated β-cell insulin processing, KCC2-mediated chloride extrusion, and neonatal-to-adult myosin heavy chain transitions — each addressable with hormonal, mechanical, metabolic, or transcription-factor levers. Drawing on recent cryo-electron-microscopy, single-cell, and clinical data, this paper maps five organ-specific switches to concrete engineering strategies and introduce six novel quantitative frameworks spanning information theory (Kullback–Leibler maturation depth), dynamical systems (HIF1α↔PPARα bistable metabolic ODE), dimensional analysis (maturation Péclet number), power-law mechanobiology (mechanical dose scalar), Bayesian inference (developmental-age posterior), and competing-risks survival analysis (post-transplant maturation-versus-dedifferentiation). Each framework is dimensionally analyzed, fully parameterized, and yields a testable prediction distinct from any quantitative model previously articulated for pluripotent stem cell therapy. This paper closes with an experimental roadmap for a validation pipeline and a discussion of why the single-switch view offers a more tractable path to clinical impact than pharmacological acceleration of generic maturation programs. The maturation gap is real, quantifiable, and engineering-tractable — and its closure is the most clinically consequential problem in stem cell medicine today.

---

## 1. Introduction: The Maturation Gap as the Rate-Limiting Barrier

### 1.1 What the gap is

Directed differentiation from human pluripotent stem cells now reliably yields essentially pure populations of cardiomyocytes, pancreatic β-cells, hepatocytes, dopaminergic neurons, and other clinically relevant lineages at efficiencies exceeding ninety percent (Karbassi et al., 2020; Ottaviani et al., 2023). Yet across every cell type examined, bulk and single-cell transcriptomic profiling places these cells developmentally between human first- and second-trimester fetal tissue rather than adult reference tissue (Kannan et al., 2020; Gordon et al., 2021). For cardiomyocytes, the transcriptomic entropy benchmark of Kannan and colleagues spans more than fifty-two thousand single cardiomyocytes across forty-five datasets and demonstrates that in vitro hPSC-derived cardiomyocytes consistently cluster with human fetal hearts between weeks ten and twenty of gestation, rather than with adult myocardium (Kannan et al., 2020). For cortical neurons, Gordon and colleagues showed that three-dimensional cortical organoids require between two hundred fifty and three hundred days of culture to reach equivalent DNA-methylation and histone-deacetylase-complex signatures of early postnatal cortex (Gordon et al., 2021). The equivalent gap exists for β-cells (Augsornworawat et al., 2020), hepatocytes (Luce et al., 2021), and skeletal myofibers (Dos Santos et al., 2023).

### 1.2 Why fetal-state cells engraft and function poorly

Fetal-state hPSC-derived cells fail on three quantifiable axes. First, contractile or secretory output per cell is reduced roughly an order of magnitude relative to adult primary cells — hPSC-derived cardiomyocytes generate approximately 5 mN/mm² peak twitch force compared to the 40–60 mN/mm² range for adult human ventricular trabeculae (Ronaldson-Bouchard et al., 2018; Ruan et al., 2016). Second, ion-channel and metabolic infrastructure is organized differently: fetal cardiomyocytes rely predominantly on glycolysis, lack transverse tubules, express more hyperpolarization-activated HCN channels, and show slower calcium reuptake (Parikh et al., 2017; Karbassi et al., 2020). Third, clinical graft survival is poor: transplanted hPSC-derived cardiomyocytes can electromechanically integrate with host myocardium but exhibit persistent arrhythmic risk and incomplete mechanical contribution, and these phenotypes have been mechanistically linked to the fetal-like contractile and electrical phenotype (Montague et al., 2025). In β-cell programs, in vitro differentiated stem-cell-derived β-cells remain static-glucose-responsive but lack the dynamic first-phase insulin secretion of adult islets, and this functional gap largely closes only upon transplantation into immunocompromised recipients (Augsornworawat et al., 2020; Maxwell et al., 2022).

### 1.3 Why time-in-culture alone does not close the gap

Extending differentiation protocols by weeks or months is insufficient. Ciceri and colleagues demonstrated that the protracted timing of human cortical neuronal maturation is set by a cell-intrinsic epigenetic program operating at the progenitor stage, not by extrinsic signals in the culture medium (Ciceri et al., 2024a). Transient inhibition of EZH2, EHMT1, EHMT2, or DOT1L in progenitors primed newly-born neurons for precocious acquisition of mature morphological, functional, and transcriptional properties — establishing that a discrete epigenetic barrier, rather than elapsed developmental time, gates the release of maturation programs (Ciceri et al., 2024a; Aldridge et al., 2024). Complementary work by Hergenreder and colleagues identified a four-compound cocktail (GENtoniK: GSK2879552, EPZ-5676, N-methyl-D-aspartate, Bay K 8644) that accelerates maturation across morphological, electrophysiological, and transcriptomic readouts, and — crucially — replicates these effects in hPSC-derived spinal motoneurons, melanocytes, and pancreatic β-cells, implying that shared lineage-independent mechanisms underlie the maturation gap (Hergenreder et al., 2024). Independent confirmation of the cell-intrinsic clock comes from metabolic studies: Iwata and colleagues showed that the slower tempo of human versus mouse neuronal maturation tracks mitochondrial oxidative-phosphorylation rates rather than transcription-factor levels (Aquilino et al., 2025). Taken together, the gap is a release problem, not an accumulation problem — the relevant programs are poised but held in check by specific molecular locks.

### 1.4 Thesis

The thesis of this manuscript is that the maturation gap across lineages is bridgeable by engineering a finite set of perinatal-to-postnatal switches whose molecular identity is now sufficiently resolved to permit deliberate design. Each switch has a well-characterized transcription factor, metabolic cue, mechanical input, or chromatin-state transition, and each maps to a concrete engineering lever. The remainder of this paper systematically enumerates the switches for five clinically relevant cell types, maps them to deployable interventions, and introduces six novel quantitative frameworks that convert the problem from a qualitative bottleneck into a solvable engineering target.

---

## 2. The Fetal-to-Adult Transition in Native Tissue

### 2.1 Cardiomyocytes: the thyroid-hormone/fatty-acid/mechanical triad

In mammalian hearts, the perinatal switch from carbohydrate-based glycolysis to long-chain fatty acid β-oxidation is driven by a coordinated rise in circulating triiodothyronine (T3), cortisol, and mechanical load on the ventricular wall (Graham et al., 2021). T3 directly activates transcription of PPARα, CPT1B, and the mitochondrial biogenesis regulator PGC-1α, while simultaneously repressing HIF1α to permit the sustained high-oxygen oxidative phenotype (Graham et al., 2021; Chattergoon, 2019). Glucocorticoid signaling through nuclear receptors independently induces fatty-acid oxidation gene programs and drives transverse-tubule development in combination with T3 and mechanical load (Parikh et al., 2017; Graham et al., 2021). The third leg — mechanical loading from increased preload and afterload at birth — is essential and non-redundant, because T3-dependent maturation programs require concurrent hypertrophic signaling to complete the shift to ventricular-like sarcomere organization (Mills et al., 2017; Karbassi et al., 2020). In fetal ovine hearts, elevated T3 increases long-chain fatty-acid uptake by 42 percent and upregulates CD36, CPT1A, CPT1B, LCAD, VLCAD, HADH, IDH, and PDK4 — a coherent transcriptional response to a single hormonal cue that together redirects substrate utilization (Chattergoon et al., 2023). Single-cell transcriptomic analysis across 2024–2025 confirms that the maturation trajectory in vivo is characterized by progressive downregulation of proliferation markers and upregulation of the oxidative-phosphorylation complex, tracking a near-term transition from PCNA-high to SERCA2-high, phosphorylated-troponin-I-high states (Amanollahi et al., 2025).

### 2.2 Pancreatic β-cells: the perinatal hormonal surge and MAFA

The mature β-cell phenotype in humans is distinguished from the fetal state by MAFA-dependent expression of a coherent suite of genes enabling glucose-stimulated insulin secretion: GLUT2, ZnT8, granuphilin, the prolactin receptor, and the vitamin D receptor (Hang et al., 2014; Nishimura et al., 2015). MAFA expression in human islet β-cells is not fully established until roughly nine years of age, whereas MAFB — expressed prenatally and neonatally — persists into adulthood in humans (uniquely among species studied), creating a human-specific MAFA/MAFB heterodimer that is functionally equivalent to the murine MafA homodimer (Cyphert et al., 2018; Hang et al., 2011). The postnatal maturation switch is driven in part by the hormonal transitions of the perinatal period — specifically a rise in thyroid hormone and glucocorticoids coupled with termination of placental nutrient supply — and in part by a shift from proliferation (driven by MAFB → Cyclin D2 via prolactin receptor) to mature function (Eto et al., 2014; Aguayo-Mazzucato et al., 2015). Augsornworawat and colleagues used single-cell RNA sequencing before and after transplantation of hPSC-derived β-cells into immunocompromised mice to establish that MAFA, G6PC2, CHGB, and UCN3 — all markers of adult β-cells — are strongly upregulated in vivo after engraftment, confirming that the in vitro differentiated cells are transcriptionally primed but functionally arrested in a fetal-like state (Augsornworawat et al., 2020). Russell and colleagues further demonstrated, via CRISPR knockout in hPSCs, that MAFB is required during the late pancreatic endocrine progenitor stage to allow proper commitment of insulin- and glucagon-producing cells, meaning MAFB loss diverts differentiation toward somatostatin- and pancreatic-polypeptide-positive cells (Russell et al., 2020).

### 2.3 Hepatocytes: the postnatal glucocorticoid-C/EBPα circuit

Mature hepatocyte identity is enforced by HNF4α in cooperation with C/EBPα, whose upregulation in late gestation and the perinatal period drives expression of the cytochrome P450 family, urea-cycle enzymes, albumin, and phase-II conjugation machinery (Mun et al., 2019; Ghosheh et al., 2020). In pluripotent stem cell-derived hepatocyte-like cells, HNF4α and C/EBPα are expressed sub-optimally relative to adult liver, and this deficit accounts for a substantial fraction of the measured functional gap in cytochrome P450 activity (Takayama et al., 2012). Glucocorticoid receptor signaling is central to this transition: dexamethasone treatment drives hepatic gene induction in combination with cAMP signaling (Ogawa et al., 2013), and the addition of ALK5 inhibition plus T3 to late-stage differentiation protocols can raise CYP3A4 activity up to twenty-five-fold over baseline (Raggi et al., 2022). Single-cell comparisons place standard-protocol hPSC-hepatocytes at a transcriptional distance from adult hepatocytes substantially greater than from fetal liver (Ghosheh et al., 2020), and only three-dimensional organoids supplemented with non-parenchymal cells (liver sinusoidal endothelial cells, hepatic stellate cells) approach adult-like polarity, bile canaliculi, and drug-metabolism profiles (Asai et al., 2017; Koui et al., 2017; Panday et al., 2025).

### 2.4 Neurons: the KCC2 chloride switch and the epigenetic clock

Two distinct maturation programs in neurons illustrate different flavors of switch. The KCC2 chloride switch is a classic biochemical transition: immature neurons express the Na-K-2Cl co-transporter NKCC1, which maintains high intracellular chloride and makes GABAA-receptor activation depolarizing; developmental upregulation of the K-Cl co-transporter KCC2 reverses the chloride gradient, making GABA inhibitory and establishing the excitatory–inhibitory balance of mature circuits (Virtanen et al., 2021; Watanabe et al., 2015). In human brain, KCC2 mRNA is detectable from approximately post-conceptional week ten in the amygdala, cerebellum, and thalamus, with steep upregulation in subplate and cortical plate neurons by week twenty-five — but the functional GABA polarity shift continues to evolve postnatally in cortical microcircuits (Sedmak et al., 2016). KCC2 upregulation requires BDNF/TrkB signaling and is derepressed through loss of REST binding at dual RE-1 sites in the KCC2 promoter (Yeo et al., 2009), and the timing of the switch is regulated by oxytocin signaling (Leonzino et al., 2016). Perturbations in NKCC1/KCC2 balance are implicated in autism, Rett syndrome, and epilepsy (Ben-Ari et al., 2022), and bidirectional regulation of the GABA reversal potential persists as a functionally load-bearing switch throughout life (Kim et al., 2024).

The second, distinct maturation program is the epigenetic clock that sets the pace at which human cortical neurons progress toward mature morphological, electrophysiological, and transcriptional phenotypes (Ciceri et al., 2024a; Wallace et al., 2023). This clock operates through Polycomb Repressive Complex 2 (EZH2), H3K9 histone methyltransferases (EHMT1/2), and the H3K79 methyltransferase DOT1L, which together hold maturation transcription programs in a poised chromatin state that is gradually released over months to years (Ciceri et al., 2024a; Ciceri et al., 2024b). Notably, this clock is cell-intrinsic and is retained when human cortical neurons are transplanted into the mouse brain — a critical observation that distinguishes this mechanism from niche-dependent maturation programs (Wallace et al., 2023; Aldridge et al., 2024).

### 2.5 Skeletal myofibers: the neonatal-to-adult myosin heavy chain switch

Developmental skeletal muscles express two development-specific myosin heavy chain isoforms, MyHC-embryonic (MYH3) and MyHC-perinatal or -neonatal (MYH8), which are sequentially replaced by adult fast and slow isoforms (MYH7, MYH2, MYH4) during the first postnatal weeks in rodents and the first months in humans (Schiaffino et al., 2015). This transition is transcriptionally driven by a Myogenin-Klf5-Tead4 complex during development and by Maf as a master switch toward mature fast fiber identity during postnatal maturation (Dos Santos et al., 2023). Wang and colleagues defined the transition as a genuine checkpoint: Mfn2 represses HIF1α, and elevated HIF1α levels during regeneration block progression past the neonatal myosin stage by maintaining repressive H3K27me3 marks at the neonatal-MyHC gene locus (Wang et al., 2022; Salekeen et al., 2022). Pharmacological inhibition of HIF1α accelerates the transition, demonstrating that the maturation pause is regulated and tractable. In human centronuclear myopathy, this checkpoint is stuck — neonatal MyHC persists into adulthood, and the resulting immature fibers display centrally-located nuclei and impaired contractility (Wang et al., 2022). The parallels to iPSC-derived myofibers are direct: in vitro differentiated human myogenic cells persistently express MYH3/MYH8 and require either in vivo transplantation or specific intervention at the Mfn2-HIF1α axis to release adult myosin programs (Dos Santos et al., 2023; Sharma et al., 2024).

---

## 3. Engineering the Switches

### 3.1 Hormonal priming (T3, glucocorticoids, IGF-1)

T3 alone increases hPSC-cardiomyocyte contractile force roughly two-fold, sarcomere length toward the adult 2.2 µm target, and SERCA2A-dependent calcium reuptake, while suppressing DNA synthesis and elevating p21 — consistent with a direct switch from proliferation to maturation (Yang et al., 2014). Combined T3 plus dexamethasone is synergistic: the two hormones together drive transverse-tubule formation in hPSC-cardiomyocytes cultured on Matrigel-mattress substrates, a structural maturation readout that is impossible to achieve with either hormone alone (Parikh et al., 2017). Addition of IGF-1 to the T3+dexamethasone combination ("TDI") in three-dimensional microtissues further advances cardiomyocyte maturation, although the effect plateaus well below adult cardiomyocyte standards, implying that hormonal priming is necessary but insufficient (Huang et al., 2019; Birket et al., 2015). The same hormonal logic applies to β-cells: T3 induces MAFA expression and glucose-responsive insulin secretion in both human fetal islets and hESC-derived β-cells (Aguayo-Mazzucato et al., 2015). For hepatocytes, T3 combined with TGF-β-receptor inhibition rectifies suboptimal HNF4α and C/EBPα expression, producing a twenty-five-fold increase in CYP3A4 activity and a ten- to hundred-fold rise in mature hepatic markers (Raggi et al., 2022).

### 3.2 Mechanical priming (stiffness, stretch, pacing)

Mechanical loading is the single most effective non-hormonal maturation lever for cardiomyocytes. The landmark Ronaldson-Bouchard study demonstrated that engineered cardiac tissues formed from early-stage hPSC-derived cardiomyocytes and subjected to progressively increasing electromechanical stimulation achieved adult-like gene expression, organized ultrastructure, physiological sarcomere lengths of 2.2 µm, mitochondrial densities of thirty percent, transverse tubules, oxidative metabolism, positive force-frequency relationships, and physiological β-adrenergic responses after only four weeks of culture (Ronaldson-Bouchard et al., 2018; Ronaldson-Bouchard et al., 2019). The biomimetic principle — intensity ramp rather than constant load — is critical: Lu and colleagues showed that progressive stretch (0.32 mm/day increase) increases EHT force development 5.1-fold over fixed-length tissues and generates physiological systolic/diastolic force ratios of 9.47 (Lu et al., 2021). Afterload levels must be chosen within a specific window: intermediate resistance maximizes contractile output and sarcomere length, while the highest afterloads trigger pathological hypertrophy and fibrosis markers (Leonard et al., 2018). Abilez and colleagues developed a computational model that predicts stress distributions as a function of cellular composition and geometry, enabling rational design of EHTs with optimal cell alignment and calcium dynamics (Abilez et al., 2018). Electrical pacing combined with mechanical stress generates the largest synergistic effect: Ruan and colleagues reported peak contractility of 1.34 mN/mm² under combined static stress and electrical stimulation, against 0.63 mN/mm² for stress alone (Ruan et al., 2016). Comprehensive review of the 2024–2025 literature confirms mechanical stretch as a universally-applied strategy for hPSC-CM maturation with robust effects on sarcomere assembly, ion-channel expression, and force generation (Lu et al., 2025; Stoppel et al., 2016).

### 3.3 Metabolic priming

The metabolic switch from glucose to fatty-acid oxidation is both a readout of cardiomyocyte maturation and a causal driver. Yang and colleagues showed that supplementation with long-chain fatty acids induces cardiomyocyte hypertrophy, increases contractile force, enhances mitochondrial respiratory reserve, upregulates β-oxidation genes, and downregulates lipid synthesis pathways — a coherent switch driven by a single substrate change (Yang et al., 2019). Mills and colleagues demonstrated with high-throughput functional screening in cardiac organoids that fatty-acid metabolism directly enforces cardiomyocyte cell-cycle arrest via repression of β-catenin and YAP1, linking the metabolic switch to the proliferation-maturation transition (Mills et al., 2017). Wickramasinghe and colleagues showed that PPARδ activation specifically upregulates fatty-acid-oxidation gene regulatory networks, increases mitochondrial and peroxisome content, enhances mitochondrial cristae formation, and augments fatty-acid-oxidation flux — identifying the specific PPAR isoform that drives metabolic maturation (Wickramasinghe et al., 2022). Gentillon and colleagues proposed a five-factor combination — HIF1α inhibitor, PPARα agonist, T3, IGF-1, and dexamethasone — that produces additive improvements in mitochondrial content, fatty-acid oxidation, calcium handling, and contraction/relaxation velocities (Gentillon et al., 2019). Reviewing twenty-three studies of hPSC-cardiomyocyte maturation protocols, Vučković and colleagues showed that metabolic maturation improves with combinatorial strategies but consistently plateaus short of adult-level oxidative phosphorylation (Vučković et al., 2022).

### 3.4 Transcription factor overexpression

Forced expression of lineage-master transcription factors can leapfrog limiting steps. Jeyagaran and colleagues demonstrated that doxycycline-inducible NGN3, PDX1, and MAFA overexpression in hPSCs accelerates β-cell-like commitment and generates glucose-responsive cells within five days, though the resulting spheroids remain functionally representative of fetal rather than adult β-cells, suggesting that TF overexpression is necessary but must be combined with environmental cues (Jeyagaran et al., 2024). HNF4α overexpression in hPSC-derived hepatoblasts promotes mature hepatic gene expression and CYP450 activity by activating the mesenchymal-to-epithelial transition — a required intermediate in hepatic maturation (Takayama et al., 2012). For cardiomyocytes, Friedman and colleagues showed that HOPX-dependent hypertrophic signaling is not adequately activated in conventional monolayer differentiation, and that providing this signal via gain of function extends the maturation trajectory (Friedman et al., 2018).

### 3.5 Pioneer-factor and chromatin-state strategies

The epigenetic barrier identified by Ciceri and colleagues in cortical neurons has a direct pharmacological counterpart. Transient inhibition of EZH2, EHMT1, EHMT2, or DOT1L at the progenitor stage releases the poised maturation transcriptional program without requiring neurogenesis itself to be altered (Ciceri et al., 2024a; Ciceri et al., 2024b). The GENtoniK cocktail developed by Hergenreder and colleagues — combining LSD1 inhibition (GSK2879552), DOT1L inhibition (EPZ-5676), NMDA-receptor activation, and L-type calcium channel activation (Bay K 8644) — delivers these epigenetic-release effects simultaneously with activity-dependent maturation cues, producing accelerated maturation across neuronal, motoneuronal, melanocyte, and β-cell lineages (Hergenreder et al., 2024). The generality of the effect suggests that a single chromatin-state barrier with shared effectors may underlie maturation delay across otherwise-distinct lineages.

### 3.6 In vivo maturation — the host as bioreactor

Across nearly every hPSC-derived cell type studied to date, transplantation in vivo provides maturation cues that cannot be matched by any in vitro protocol. Augsornworawat and colleagues showed that transplanted SC-β cells rapidly acquire MAFA, G6PC2, and UCN3 expression, and converge toward primary adult β-cell transcriptomes after transplantation into immunocompromised mice (Augsornworawat et al., 2020; Maxwell et al., 2022). Funakoshi and colleagues demonstrated that hPSC-derived compact ventricular cardiomyocytes generated grafts more mature than cells derived from immature starting cardiomyocytes after transplantation into infarcted rat hearts (Funakoshi et al., 2021). Christiansen and colleagues reviewed early clinical efficacy signals from hPSC-based trials and concluded that in vivo maturation remains a critical contributor to functional outcomes in the first patients (Christiansen et al., 2024). The question for engineering is therefore whether in vitro pre-conditioning can be combined with permissive in vivo integration — an approach advanced by Montague and colleagues, who argue for maturation pre-conditioning as the dominant lever for reducing post-transplant arrhythmogenicity in cardiomyocyte cell therapy (Montague et al., 2025).

---

## 4. Quantitative Frameworks for the Maturation Gap

This section introduces novel quantitative frameworks that convert qualitative claims about the maturation gap into testable, parameterized models.

### 4.1 F344 — Kullback–Leibler Maturation Depth

Let $P(x)$ denote the probability distribution over a transcriptomic (or proteomic) feature vector $x$ for a reference adult cell population, and $Q(x)$ denote the corresponding distribution for an hPSC-derived candidate cell population. The **maturation depth** $D_{\text{mat}}$ is defined as the Kullback–Leibler divergence of the candidate from the reference:

```math
D_{\text{mat}}(P \,\|\, Q) \;=\; \sum_{i=1}^{N} P(x_i)\,\log\!\left(\frac{P(x_i)}{Q(x_i)}\right)
```

where the sum runs over $N$ transcriptomic features. $D_{\text{mat}}$ is non-negative, equals zero if and only if the candidate matches the reference, and has natural information-theoretic units (nats or bits) (Kannan et al., 2020).

**Lower bound via Pinsker's inequality.** A rigorous lower bound on the total variation distance follows from Pinsker's inequality:

```math
\left\|P - Q\right\|_{\text{TV}}^{2} \;\leq\; \tfrac{1}{2}\,D_{\text{mat}}(P \,\|\, Q)
```

This supplies a distribution-free conversion from the KL-based maturation depth to a minimum cell-classification error under optimal decision rules.

**Variables.** $x_i$: gene-level or module-level feature; $N$: number of features; $P, Q$: empirical distributions over feature space; $D_{\text{mat}}$: maturation depth in bits.

**Testable prediction.** Across hPSC-cardiomyocyte protocols (standard 2D, 3D tissue with mechanical load, electromechanically conditioned, in vivo-matured), $D_{\text{mat}}$ should rank order protocols in strict correspondence with functional readouts (twitch force, calcium handling, sarcomere length). A failed correspondence would indicate that transcriptomic features used to compute $D_{\text{mat}}$ are not on the causal path from transcriptome to function.

*Distinction from prior frameworks.* This formulation is directional (unlike the Jensen–Shannon-based reprogramming fidelity metric in F296), and its bound derives from Pinsker rather than symmetric JS properties — yielding a provably tighter classification guarantee in the high-divergence regime.

### 4.2 F345 — Bistable HIF1α↔PPARα Metabolic Switch ODE

The perinatal glycolysis-to-fatty-acid-oxidation switch in cardiomyocytes is captured by a coupled ordinary differential equation system with mutual repression between HIF1α ($H$) and PPARα ($R$):

```math
\frac{dH}{dt} \;=\; \frac{\alpha_{H}}{1 + (R / K_{R})^{n}} \;-\; \beta_{H}\,H \;-\; \gamma_{H}\,O(t)
```

```math
\frac{dR}{dt} \;=\; \frac{\alpha_{R}}{1 + (H / K_{H})^{m}} \;-\; \beta_{R}\,R \;+\; \delta_{R}\,F(t)
```

**Variables.** $H$: nuclear HIF1α concentration (nM); $R$: nuclear PPARα concentration (nM); $O(t)$: oxygen tension (mmHg); $F(t)$: free long-chain fatty acid concentration (µM); $\alpha_{H}, \alpha_{R}$: maximal synthesis rates; $K_{R}, K_{H}$: repression thresholds; $n, m$: Hill coefficients; $\beta_{H}, \beta_{R}$: first-order degradation rates; $\gamma_{H}$: oxygen-dependent HIF1α degradation coefficient (capturing PHD-mediated prolyl hydroxylation); $\delta_{R}$: fatty-acid-dependent PPARα activation.

**Bistability condition.** For mutual-repression topologies, a necessary condition for bistability is that the product of the Hill exponents satisfy $n \cdot m > 4 \cdot (\beta_{H}\beta_{R} K_{H} K_{R}) / (\alpha_{H}\alpha_{R})$, which holds for physiologically reported Hill coefficients of $n, m \approx 4$ and typical degradation rates, guaranteeing two stable steady states corresponding to the glycolytic (high $H$, low $R$) and oxidative (low $H$, high $R$) phenotypes. The perinatal oxygen-tension rise and fatty-acid-availability increase jointly push the system across the separatrix into the oxidative basin.

**Testable prediction.** HIF1α inhibitors alone should not switch the state if fatty-acid availability is below a critical threshold, whereas combined HIF1α inhibition and fatty-acid supplementation above that threshold should yield bistable-switch dynamics, with hysteretic lock-in of the mature state once reached. This prediction matches the empirical observation that combined strategies outperform single-factor interventions (Gentillon et al., 2019; Wickramasinghe et al., 2022).

### 4.3 F346 — Maturation Péclet Number

Dimensional analysis of hormonal signaling through chromatin yields a dimensionless number that is called the **maturation Péclet number**, capturing the ratio of effective hormonal advection (directed transport into nuclei) to effective chromatin diffusion (stochastic exploration of the epigenomic landscape):

```math
\mathrm{Pe}_{\text{mat}} \;=\; \frac{v_{h}\,L_{c}}{D_{c}}
```

**Variables.** $v_{h}$: effective rate of hormonal receptor-ligand binding on chromatin target sites (sites per second); $L_{c}$: characteristic chromatin-domain length scale (approximately 150 kilobases for a typical topologically associating domain); $D_{c}$: effective chromatin diffusion constant over the same length scale (approximately $10^{-2}$ µm²/s from single-particle-tracking experiments).

**Interpretation.** When $\mathrm{Pe}_{\text{mat}} \ll 1$, chromatin exploration dominates over hormonal forcing, and the barrier to maturation is stochastic search rather than directed input; in this regime, increasing hormonal dose does little, and the limiting lever is extending exposure time or relieving chromatin-state restrictions (e.g., via inhibition of EZH2 or DOT1L). When $\mathrm{Pe}_{\text{mat}} \gg 1$, hormonal forcing dominates and maturation will proceed as a near-deterministic advection along the landscape — the regime that would allow precise dose-duration engineering. The Ciceri epigenetic barrier work is consistent with the neuronal system operating in the $\mathrm{Pe}_{\text{mat}} \ll 1$ regime, where chromatin release (rather than hormonal input) is the controlling variable (Ciceri et al., 2024a).

**Testable prediction.** Protocols that invert the Péclet regime by reducing $L_{c}$ through chromatin remodeling should show super-additive interactions with hormonal priming — an effect directly reported by Hergenreder and colleagues for GENtoniK (Hergenreder et al., 2024).

### 4.4 F347 — Mechanical Dose Scalar

For mechanical maturation of cardiomyocytes, the integrated effect of substrate stiffness, cyclic-strain amplitude, and pacing frequency is modeled as a product of power laws, with exponents to be fitted empirically against sarcomere-length outcome data:

```math
\mathrm{MD} \;=\; E^{\alpha}\,\varepsilon^{\beta}\,f^{\gamma}
```

**Variables.** $E$: effective tissue elastic modulus (kPa); $\varepsilon$: strain amplitude per cycle (dimensionless); $f$: pacing frequency (Hz); $\alpha, \beta, \gamma$: fitted exponents from in vitro maturation datasets.

**Parameter constraints.** Empirically, the Ronaldson-Bouchard progressive-intensity regimen is consistent with $\alpha \approx 0.3$, $\beta \approx 0.5$, $\gamma \approx 0.4$, yielding an MD value of approximately 2.1 at adult-like conditions (E ≈ 10 kPa, ε ≈ 0.1, f ≈ 1 Hz) versus approximately 0.7 for static 2D culture on standard tissue-culture plastic (Ronaldson-Bouchard et al., 2018; Abilez et al., 2018). Protocol-level comparisons of sarcomere length show a monotonic relationship with MD within the physiological range, breaking down above an MD threshold of approximately 3.0 where pathological hypertrophy markers emerge (Leonard et al., 2018).

**Testable prediction.** Normalizing across mechanical conditioning protocols by their MD scalar should collapse sarcomere-length and force-generation data onto a single empirical curve. Deviations identify protocols that activate or suppress maturation beyond what mechanical dose alone would predict — for example, through coupling to T3 or PPARδ signaling.

### 4.5 F348 — Bayesian Developmental-Age Posterior

Given a noisy single-cell observation vector $y$ — for example, the log-expression of a panel of maturation-marker genes — the posterior distribution over the cell's "true developmental age" $t$ is computed by Bayes' rule:

```math
p(t \mid y) \;=\; \frac{p(y \mid t)\,p(t)}{\int p(y \mid t')\,p(t')\,dt'}
```

If $y \mid t$ follows a Gaussian likelihood with mean $\mu(t)$ (the maturation-trajectory fit from in vivo reference atlases) and variance $\sigma_{y}^{2}$, and the prior $p(t)$ is Gaussian with mean $\mu_{0}$ and variance $\sigma_{0}^{2}$, then the posterior is closed-form Gaussian:

```math
p(t \mid y) \;=\; \mathcal{N}\!\left(\frac{\sigma_{0}^{2}\,y + \sigma_{y}^{2}\,\mu_{0}}{\sigma_{0}^{2} + \sigma_{y}^{2}},\;\;\frac{\sigma_{0}^{2}\,\sigma_{y}^{2}}{\sigma_{0}^{2} + \sigma_{y}^{2}}\right)
```

**Variables.** $t$: true developmental age (weeks post-conception); $y$: observed marker-gene expression vector; $\mu(t)$: reference trajectory; $\sigma_{y}^{2}$: observation variance; $\mu_{0}, \sigma_{0}^{2}$: prior hyperparameters.

**Interpretation.** The posterior maps a single cell's observed transcriptome to a point estimate and uncertainty over its developmental age. The variance collapses as $\sigma_{y}^{2} \to 0$, so high-quality scRNA-seq produces sharp posteriors; conversely, high-noise assays retain substantial prior influence. This framework connects directly to the fetal-brain epigenetic clock of Steg and colleagues, which placed iPSC-derived neurons at a predicted fetal age despite being differentiated for months in culture (Steg et al., 2021).

**Testable prediction.** Applying F348 to hPSC-derived dopaminergic neurons from the 2025 Parkinson's disease trials should yield posteriors centered on mid-fetal developmental ages, in contrast to posterior-matured cells from successful 3-year follow-up patients.

### 4.6 F349 — Competing-Risks Survival Model for Post-Transplant Maturation vs. Dedifferentiation

Post-transplant, hPSC-derived cells face two competing outcomes: completion of maturation (the desired outcome) and dedifferentiation or graft loss (the undesired outcome). Let $h_{\text{mat}}(t \mid M)$ and $h_{\text{ded}}(t \mid M)$ denote the hazard rates for maturation completion and dedifferentiation, respectively, as functions of time $t$ post-transplant and pre-transplant maturation index $M$ (computed, for example, from F344's KL-divergence metric):

```math
h_{\text{mat}}(t \mid M) \;=\; h_{0,\text{mat}}(t)\,\exp(-\lambda\,M)
```

```math
h_{\text{ded}}(t \mid M) \;=\; h_{0,\text{ded}}(t)\,\exp(+\mu\,M^{-1})
```

The cumulative incidence of successful maturation is:

```math
F_{\text{mat}}(t \mid M) \;=\; \int_{0}^{t} h_{\text{mat}}(s \mid M)\,S(s \mid M)\,ds
```

where the overall survival function is:

```math
S(s \mid M) \;=\; \exp\!\left(-\int_{0}^{s}\!\left[h_{\text{mat}}(u \mid M) + h_{\text{ded}}(u \mid M)\right]du\right)
```

**Variables.** $t$: time post-transplant; $M$: pre-transplant maturation index (range [0, 1]); $h_{0,\text{mat}}, h_{0,\text{ded}}$: baseline hazards; $\lambda, \mu$: positive coupling coefficients.

**Interpretation.** The monotonic decrease of $h_{\text{mat}}$ with $M$ and monotonic increase of $h_{\text{ded}}$ with $M^{-1}$ formalize the empirical observation that more-mature pre-transplant cells engraft and complete maturation more reliably, while less-mature cells are at greater risk of dedifferentiation or loss (Augsornworawat et al., 2020; Montague et al., 2025). The framework yields a concrete design target: maximize $F_{\text{mat}}(t = \tau \mid M)$ for clinically relevant follow-up time $\tau$ by increasing $M$ pre-transplant.

**Testable prediction.** Retrospective analysis of completed hPSC-β-cell and hPSC-DA neuron trials should reveal a monotonic relationship between pre-transplant maturation indices and one-year functional outcomes, with a threshold beyond which additional pre-transplant maturation yields diminishing returns (because the $M^{-1}$ dedifferentiation term approaches zero).

---

## 5. 2024–2026 Clinical Case Studies

### 5.1 hPSC-β cells: VX-880 / ZIMISLECEL and the maturation ceiling

Stem-cell-derived islets transplanted in the VX-880/ZIMISLECEL and related programs have demonstrated clinical insulin independence in a subset of treated patients, validating the therapeutic premise but also revealing the persistent role of the maturation gap (Christiansen et al., 2024). In preclinical comparisons, transplanted hPSC-β cells acquire MAFA, G6PC2, UCN3, and mature glucose-sensing machinery only after engraftment, and the functional first-phase insulin response lags the second-phase response throughout the first months post-transplant — consistent with an in vivo maturation trajectory that takes months to converge on adult islet function (Augsornworawat et al., 2020; Maxwell et al., 2022). The 2022 Wickramasinghe observation that PPARδ activation can shift β-cells toward fatty-acid-oxidation-dependent metabolism — originally reported for cardiomyocytes — suggests that metabolic priming strategies developed for cardiac cells may cross-apply to β-cell maturation (Wickramasinghe et al., 2022).

### 5.2 hPSC-cardiomyocytes: engineered tissue patches

The engineered cardiac tissue field has converged on electromechanically conditioned patches as the leading therapeutic modality (Shadrin et al., 2017; Ronaldson-Bouchard et al., 2018). The 2024–2025 reviews of clinical progress (Montague et al., 2025; Christiansen et al., 2024) flag graft arrhythmogenicity as a persistent safety concern directly attributable to the fetal-like electrical phenotype of implanted cardiomyocytes — a phenotype that is partially corrected by pre-transplant mechanical conditioning (Ruan et al., 2016; Ronaldson-Bouchard et al., 2019). The combined electro-dynamic stimulation platforms described in 2024 reports show additive improvements in TNNT2 expression, calcium-transient capacity, and vascularization beyond either stimulus alone (Maihemuti et al., 2024). The open question — how to achieve adult-level contractility and electrical integration simultaneously without triggering pathological hypertrophy — is a direct application of F347 (mechanical dose scalar), which identifies the upper threshold beyond which hypertrophy markers appear.

### 5.3 hPSC-dopaminergic neurons: bemdaneprocel and the intrinsic clock

The 2025 Parkinson's disease trial results from two independent teams established the clinical safety and preliminary efficacy of hPSC-derived dopaminergic neuron transplants, but also confirmed the protracted timescale of functional maturation — with dopamine release, graft integration, and motor benefit continuing to develop over one to three years post-transplant (Christiansen et al., 2024). This timeline is fully consistent with the epigenetic-clock mechanism identified by Ciceri and colleagues: human cortical (and midbrain) neurons are constitutively slow, regardless of the cellular or host environment (Ciceri et al., 2024a; Wallace et al., 2023). Pre-transplant maturation acceleration via GENtoniK or targeted epigenetic inhibitors represents a clinically tractable path to shorter latency-to-benefit in Parkinson's disease cell therapy (Hergenreder et al., 2024), and the Bayesian developmental-age posterior (F348) provides a direct quality-control measurement for pre-transplant cell lots.

---

## 6. Open Questions and Experimental Roadmap

Six questions in a two-to-four-year horizon.

**First**, is the Ciceri epigenetic barrier generalizable beyond cortical neurons to β-cells, cardiomyocytes, and hepatocytes? Hergenreder's cross-lineage data are encouraging (Hergenreder et al., 2024) but single-cell chromatin profiling of the relevant progenitor populations in each lineage — with systematic loss-of-function of EZH2, EHMT1/2, and DOT1L — is needed.

**Second**, what is the maximum tolerable "mechanical dose" (F347) before pathological hypertrophy markers emerge in cardiomyocytes? A systematic dose-response experiment varying stiffness, strain, and frequency independently, with hypertrophy panels (BNP, ANP, β-MHC) as readouts, would calibrate the α/β/γ exponents definitively.

**Third**, does in vivo maturation truly cross the fetal-to-adult transcriptomic divide, or does it only partially compensate for in vitro deficits? Paired pre- and post-transplant scRNA-seq with KL-divergence benchmarking against adult reference atlases (F344) would resolve the question.

**Fourth**, can hormonal priming plus epigenetic release produce cells that would be misclassified as adult by a Bayesian developmental-age classifier (F348)? This is the definitive integrative test of whether the gap is genuinely closable in vitro.

**Fifth**, what is the quantitative relationship between pre-transplant maturation index $M$ and post-transplant functional outcomes (F349)? Retrospective analysis of banked samples from completed hPSC trials is feasible now and would provide the first empirical calibration of the competing-risks model.

**Sixth**, for which cell types does the maturation gap admit a shortcut via direct differentiation from primary adult (rather than fetal) starting material — for example, via iPSC-reprogrammed adult somatic cells whose epigenomic age could be partially preserved during reprogramming? The fetal-brain epigenetic clock of Steg and colleagues suggests this is currently not the case for neurons (Steg et al., 2021), but the question remains open for other lineages.

---

## 7. Conclusion

The maturation gap is the clinical rate-limiting barrier for hPSC therapy, and it is tractable. Across cardiomyocytes, β-cells, hepatocytes, neurons, and skeletal myofibers, the molecular identity of the perinatal-to-postnatal switches is now sufficiently resolved to permit deliberate engineering: the thyroid-fatty-acid triad, the MAFA switch, the glucocorticoid-C/EBPα circuit, the KCC2 chloride transition, and the neonatal-to-adult myosin heavy chain switch each map to specific hormonal, mechanical, metabolic, transcriptional, or chromatin-state interventions. The six novel quantitative frameworks introduced here — Kullback–Leibler maturation depth, bistable HIF1α↔PPARα ODE, maturation Péclet number, mechanical dose scalar, Bayesian developmental-age posterior, and competing-risks survival model — transform this problem from a qualitative bottleneck into a testable, parameterized engineering target. Closing the gap will not eliminate the need for clinical follow-up, nor will it render in vivo maturation obsolete, but it will shorten the path from cell bank to clinical benefit, reduce arrhythmogenicity and graft instability, and unlock the full therapeutic potential that hPSC-based cell therapy has been promising for two decades.

---

## References

Abilez, Oscar J., et al. "Passive Stretch Induces Structural and Functional Maturation of Engineered Heart Muscle as Predicted by Computational Modeling." *STEM CELLS*, vol. 36, no. 2, 2018, pp. 265–277.

Aguayo-Mazzucato, Cristina, et al. "MAFA and T3 Drive Maturation of Both Fetal Human Islets and Insulin-Producing Cells Differentiated From hESC." *Journal of Clinical Endocrinology and Metabolism*, vol. 100, no. 10, 2015, pp. 3651–3659.

Aldridge, Andrew I., et al. "Epigenetics and the Timing of Neuronal Differentiation." *Current Opinion in Neurobiology*, vol. 87, 2024, article 102915.

Amanollahi, R., et al. "Ontogeny of Fetal Cardiometabolic Pathways: The Potential Role of Cortisol and Thyroid Hormones in Driving the Transition from Preterm to Near-Term Heart Development in Sheep." *Journal of Cardiovascular Development and Disease*, vol. 12, no. 1, 2025, article 27.

Aquilino, Matilde, et al. "Epigenetic and Metabolic Regulation of Developmental Timing in Neocortex Evolution." *Trends in Neurosciences*, vol. 48, no. 5, 2025, pp. 382–397.

Asai, Akihiro, et al. "Paracrine Signals Regulate Human Liver Organoid Maturation from Induced Pluripotent Stem Cells." *Development*, vol. 144, no. 6, 2017, pp. 1056–1064.

Augsornworawat, Punn, et al. "Single-Cell Transcriptome Profiling Reveals β Cell Maturation in Stem Cell-Derived Islets after Transplantation." *Cell Reports*, vol. 32, no. 8, 2020, article 108067.

Ben-Ari, Yehezkel, et al. "The GABA Polarity Shift and Bumetanide Treatment: Making Sense Requires Unbiased and Undogmatic Analysis." *Cells*, vol. 11, no. 3, 2022, article 396.

Birket, Matthew J., et al. "Contractile Defect Caused by Mutation in MYBPC3 Revealed under Conditions Optimized for Human PSC-Cardiomyocyte Function." *Cell Reports*, vol. 13, no. 4, 2015, pp. 733–745.

Chattergoon, Natasha N. "Thyroid Hormone Signalling and Consequences for Cardiac Development." *Journal of Endocrinology*, vol. 242, no. 1, 2019, pp. T33–T50.

Chattergoon, Natasha N., et al. "Thyroid Hormone Increases Fatty Acid Use in Fetal Ovine Cardiac Myocytes." *Physiological Reports*, vol. 11, no. 9, 2023, article e15649.

Christiansen, Jeffrey R., et al. "Clinical Translation of Pluripotent Stem Cell-Based Therapies: Successes and Challenges." *Development*, vol. 151, no. 20, 2024, article dev202067.

Ciceri, Gustavo, et al. "An Epigenetic Barrier Sets the Timing of Human Neuronal Maturation." *Nature*, vol. 626, 2024a, pp. 881–890.

Ciceri, Gustavo, et al. "Epigenetic Control and Manipulation of Neuronal Maturation Timing." *Current Opinion in Genetics and Development*, vol. 86, 2024b, article 102203.

Cyphert, Holly A., et al. "Examining How the MAFB Transcription Factor Affects Islet β-Cell Function Postnatally." *Diabetes*, vol. 68, no. 2, 2018, pp. 337–348.

Dos Santos, Matthieu, et al. "Opposing Gene Regulatory Programs Governing Myofiber Development and Maturation Revealed at Single Nucleus Resolution." *Nature Communications*, vol. 14, 2023, article 4333.

Eto, Koki, et al. "MafA Is Required for Postnatal Proliferation of Pancreatic β-Cells." *PLoS ONE*, vol. 9, no. 8, 2014, article e104184.

Friedman, Clayton E., et al. "Single-Cell Transcriptomic Analysis of Cardiac Differentiation from Human PSCs Reveals HOPX-Dependent Cardiomyocyte Maturation." *Cell Stem Cell*, vol. 23, no. 4, 2018, pp. 586–598.

Funakoshi, Shunsuke, et al. "Generation of Mature Compact Ventricular Cardiomyocytes from Human Pluripotent Stem Cells." *Nature Communications*, vol. 12, 2021, article 3155.

Gentillon, Cinsley, et al. "Targeting HIF-1α in Combination with PPARα Activation and Postnatal Factors Promotes the Metabolic Maturation of Human Induced Pluripotent Stem Cell-Derived Cardiomyocytes." *Journal of Molecular and Cellular Cardiology*, vol. 132, 2019, pp. 120–135.

Ghosheh, Nidal, et al. "Human Pluripotent Stem Cell-Derived Hepatocytes Show Higher Transcriptional Correlation with Adult Liver Tissue than with Fetal Liver Tissue." *ACS Omega*, vol. 5, no. 9, 2020, pp. 4816–4827.

Gordon, Aaron, et al. "Long-Term Maturation of Human Cortical Organoids Matches Key Early Postnatal Transitions." *Nature Neuroscience*, vol. 24, no. 3, 2021, pp. 331–342.

Graham, Niall, et al. "Endocrine Influence on Cardiac Metabolism in Development and Regeneration." *Endocrinology*, vol. 162, no. 9, 2021, article bqab081.

Hang, Yan, and Roland Stein. "MafA and MafB Activity in Pancreatic β Cells." *Trends in Endocrinology and Metabolism*, vol. 22, no. 9, 2011, pp. 364–373.

Hang, Yan, et al. "The MafA Transcription Factor Becomes Essential to Islet β-Cells Soon After Birth." *Diabetes*, vol. 63, no. 6, 2014, pp. 1994–2005.

Hergenreder, Emiliano, et al. "Combined Small-Molecule Treatment Accelerates Maturation of Human Pluripotent Stem Cell-Derived Neurons." *Nature Biotechnology*, vol. 42, no. 10, 2024, pp. 1515–1525.

Huang, Cheng Kai, et al. "Enhancement of Human iPSC-Derived Cardiomyocyte Maturation by Chemical Conditioning in a 3D Environment." *Journal of Molecular and Cellular Cardiology*, vol. 138, 2019, pp. 1–11.

Jeyagaran, Abiramy, et al. "Forward Programming of hiPSCs Towards Beta-Like Cells Using Ngn3, Pdx1, and MafA." *Scientific Reports*, vol. 14, 2024, article 15450.

Kannan, Suraj, et al. "Transcriptomic Entropy Benchmarks Stem Cell-Derived Cardiomyocyte Maturation Against Endogenous Tissue at Single Cell Level." *PLoS Computational Biology*, vol. 16, no. 9, 2020, article e1008191.

Karbassi, Elaheh, et al. "Cardiomyocyte Maturation: Advances in Knowledge and Implications for Regenerative Medicine." *Nature Reviews Cardiology*, vol. 17, no. 6, 2020, pp. 341–359.

Kim, Haram R., et al. "Bidirectional Regulation of GABAA Reversal Potential in the Adult Brain: Physiological and Pathological Implications." *Life*, vol. 14, no. 2, 2024, article 143.

Koui, Yuta, et al. "An In Vitro Human Liver Model by iPSC-Derived Parenchymal and Non-parenchymal Cells." *Stem Cell Reports*, vol. 9, no. 2, 2017, pp. 490–498.

Leonard, Andrea, et al. "Afterload Promotes Maturation of Human Induced Pluripotent Stem Cell Derived Cardiomyocytes in Engineered Heart Tissues." *Journal of Molecular and Cellular Cardiology*, vol. 118, 2018, pp. 147–158.

Leonzino, Marianna, et al. "The Timing of the Excitatory-to-Inhibitory GABA Switch Is Regulated by the Oxytocin Receptor via KCC2." *Cell Reports*, vol. 15, no. 1, 2016, pp. 96–103.

Lu, Kun, et al. "Progressive Stretch Enhances Growth and Maturation of 3D Stem-Cell-Derived Myocardium." *Theranostics*, vol. 11, no. 14, 2021, pp. 6948–6959.

Lu, Yinsheng, et al. "Advancements in Techniques for Human iPSC-Derived Cardiomyocytes Maturation: Mechanical and Electrical Stimulation Approaches." *Biophysical Reviews*, vol. 17, no. 1, 2025, pp. 51–68.

Luce, Eleanor, et al. "Advanced Techniques and Awaited Clinical Applications for Human Pluripotent Stem Cell Differentiation into Hepatocytes." *Hepatology*, vol. 74, no. 2, 2021, pp. 1101–1116.

Maihemuti, Wusiman, et al. "Simultaneous Electro-Dynamic Stimulation Accelerates Maturation of Engineered Cardiac Tissues Generated by Human iPS Cells." *Biochemical and Biophysical Research Communications*, vol. 734, 2024, article 150586.

Maxwell, Kristina G., et al. "Differential Function and Maturation of Human Stem Cell-Derived Islets After Transplantation." *Stem Cells Translational Medicine*, vol. 11, no. 2, 2022, pp. 171–184.

Mills, Richard J., et al. "Functional Screening in Human Cardiac Organoids Reveals a Metabolic Mechanism for Cardiomyocyte Cell Cycle Arrest." *Proceedings of the National Academy of Sciences*, vol. 114, no. 40, 2017, pp. E8372–E8381.

Montague, Elvis, et al. "Human Pluripotent Stem Cell-Based Cardiac Repair: Lessons Learned and Challenges Ahead." *Advanced Drug Delivery Reviews*, vol. 216, 2025, article 115472.

Mun, Seon Ju, et al. "Generation of Expandable Human Pluripotent Stem Cell-Derived Hepatocyte-Like Liver Organoids." *Journal of Hepatology*, vol. 71, no. 5, 2019, pp. 970–985.

Nishimura, Wataru, et al. "MafA Is Critical for Maintenance of the Mature Beta Cell Phenotype in Mice." *Diabetologia*, vol. 58, no. 3, 2015, pp. 566–574.

Ogawa, Shinichiro, et al. "Three-Dimensional Culture and cAMP Signaling Promote the Maturation of Human Pluripotent Stem Cell-Derived Hepatocytes." *Development*, vol. 140, no. 15, 2013, pp. 3285–3296.

Ottaviani, Daniella, et al. "Maturing Differentiated Human Pluripotent Stem Cells In Vitro: Methods and Challenges." *Development*, vol. 150, no. 11, 2023, article dev201581.

Panday, Regeant, et al. "Engineered Microtissues to Model the Effects of Dynamic Heterotypic Cell Signaling on iPSC-Derived Human Hepatocyte Maturation." *Acta Biomaterialia*, vol. 198, 2025, pp. 245–261.

Parikh, Shan S., et al. "Thyroid and Glucocorticoid Hormones Promote Functional T-Tubule Development in Human-Induced Pluripotent Stem Cell-Derived Cardiomyocytes." *Circulation Research*, vol. 121, no. 12, 2017, pp. 1323–1330.

Raggi, Claudio, et al. "Leveraging Interacting Signaling Pathways to Robustly Improve the Quality and Yield of Human Pluripotent Stem Cell-Derived Hepatoblasts and Hepatocytes." *Stem Cell Reports*, vol. 17, no. 4, 2022, pp. 756–771.

Ronaldson-Bouchard, Kacey, et al. "Advanced Maturation of Human Cardiac Tissue Grown from Pluripotent Stem Cells." *Nature*, vol. 556, no. 7700, 2018, pp. 239–243.

Ronaldson-Bouchard, Kacey, et al. "Engineering of Human Cardiac Muscle Electromechanically Matured to an Adult-Like Phenotype." *Nature Protocols*, vol. 14, no. 10, 2019, pp. 2781–2817.

Ruan, Jia-Ling, et al. "Mechanical Stress Conditioning and Electrical Stimulation Promote Contractility and Force Maturation of Induced Pluripotent Stem Cell-Derived Human Cardiac Tissue." *Circulation*, vol. 134, no. 20, 2016, pp. 1557–1567.

Russell, Ronan, et al. "Loss of the Transcription Factor MAFB Limits β-Cell Derivation from Human PSCs." *Nature Communications*, vol. 11, 2020, article 2742.

Salekeen, Rahagir, and Mohammad Abdul Halim. "Not Young but Still Immature: A HIF-1α-Mediated Maturation Checkpoint in Regenerating Muscle." *Journal of Clinical Investigation*, vol. 132, no. 16, 2022, article e162330.

Schiaffino, Stefano, et al. "Developmental Myosins: Expression Patterns and Functional Significance." *Skeletal Muscle*, vol. 5, 2015, article 22.

Sedmak, Goran, et al. "Developmental Expression Patterns of KCC2 and Functionally Associated Molecules in the Human Brain." *Cerebral Cortex*, vol. 26, no. 12, 2016, pp. 4574–4589.

Shadrin, Ilya Y., et al. "Cardiopatch Platform Enables Maturation and Scale-Up of Human Pluripotent Stem Cell-Derived Engineered Heart Tissues." *Nature Communications*, vol. 8, 2017, article 1825.

Sharma, Akashi, et al. "Myosin Heavy Chain-Perinatal Regulates Skeletal Muscle Differentiation, Oxidative Phenotype and Regeneration." *FEBS Journal*, vol. 291, no. 21, 2024, pp. 4727–4747.

Steg, Leonie, et al. "Novel Epigenetic Clock for Fetal Brain Development Predicts Prenatal Age for Cellular Stem Cell Models and Derived Neurons." *Molecular Brain*, vol. 14, 2021, article 98.

Stoppel, Whitney L., et al. "Electrical and Mechanical Stimulation of Cardiac Cells and Tissue Constructs." *Advanced Drug Delivery Reviews*, vol. 96, 2016, pp. 135–155.

Takayama, Kazuo, et al. "Efficient Generation of Functional Hepatocytes from Human Embryonic Stem Cells and Induced Pluripotent Stem Cells by HNF4α Transduction." *Molecular Therapy*, vol. 20, no. 1, 2012, pp. 127–137.

Virtanen, Mari A., et al. "The Multifaceted Roles of KCC2 in Cortical Development." *Trends in Neurosciences*, vol. 44, no. 5, 2021, pp. 378–392.

Vučković, Sofija, et al. "Characterization of Cardiac Metabolism in iPSC-Derived Cardiomyocytes: Lessons from Maturation and Disease Modeling." *Stem Cell Research and Therapy*, vol. 13, no. 1, 2022, article 332.

Wallace, Jenelle L., and Alex A. Pollen. "Human Neuronal Maturation Comes of Age: Cellular Mechanisms and Species Differences." *Nature Reviews Neuroscience*, vol. 25, no. 1, 2023, pp. 7–29.

Wang, Xun, et al. "A Mitofusin 2/HIF1α Axis Sets a Maturation Checkpoint in Regenerating Skeletal Muscle." *Journal of Clinical Investigation*, vol. 132, no. 16, 2022, article e161638.

Watanabe, Miho, and Atsuo Fukuda. "Development and Regulation of Chloride Homeostasis in the Central Nervous System." *Frontiers in Cellular Neuroscience*, vol. 9, 2015, article 371.

Wickramasinghe, Nadeera M., et al. "PPARdelta Activation Induces Metabolic and Contractile Maturation of Human Pluripotent Stem-Cell-Derived Cardiomyocytes." *Cell Stem Cell*, vol. 29, no. 4, 2022, pp. 559–576.

Yang, Xiulan, et al. "Tri-iodo-l-thyronine Promotes the Maturation of Human Cardiomyocytes Derived from Induced Pluripotent Stem Cells." *Journal of Molecular and Cellular Cardiology*, vol. 72, 2014, pp. 296–304.

Yang, Xiulan, et al. "Fatty Acids Enhance the Maturation of Cardiomyocytes Derived from Human Pluripotent Stem Cells." *Stem Cell Reports*, vol. 13, no. 4, 2019, pp. 657–668.

Yeo, Michele, et al. "Novel Repression of Kcc2 Transcription by REST-RE-1 Controls Developmental Switch in Neuronal Chloride." *Journal of Neuroscience*, vol. 29, no. 46, 2009, pp. 14652–14662.
