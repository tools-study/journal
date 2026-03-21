# Transcription Factors and Cell Identity Programming

---

## Abstract

Cell identity is not a static property encoded in the genome but an actively maintained state arising from the continuous interplay of three coupled axes: (1) pioneer transcription factors that engage nucleosomal DNA and establish chromatin accessibility, (2) metabolic fluxes that supply the substrates for histone modifications governing the epigenetic landscape, and (3) stochastic transcriptional bursting that converts chromatin states into probabilistic protein output distributions. This paper develops a unified quantitative framework connecting these three axes, demonstrating that disruption at any level—pioneer factor dosage alterations in cancer, metabolic reprogramming in the tumor microenvironment, or aberrant transcriptional noise during aging—causes identity collapse with pathological consequences. We present four novel mathematical frameworks: a Boltzmann partition function for competitive transcription factor–nucleosome binding, a stoichiometric model linking metabolic pathway fluxes to chromatin modification rates, a metabolically coupled telegraph model of transcriptional bursting, and a renewal-theoretic model of enhancer–promoter contact frequency. These frameworks generate testable predictions regarding the quantitative coupling between metabolic state, chromatin accessibility, and gene expression noise. Therapeutic applications are examined across IDH-mutant glioma (vorasidenib), tumor-associated macrophage reprogramming (lactylation inhibition), and pioneer factor dosage restoration in solid tumors, with a synthesis arguing that metabolic correction must precede chromatin engineering for therapeutic efficacy.

---

## 1. Introduction: The Three Axes of Active Identity Maintenance

### 1.1 Cell Identity as an Actively Maintained State

The classical view of cell identity as a terminal state, determined during development and passively maintained through mitotic inheritance of DNA methylation patterns, has undergone a fundamental revision in the past decade. Lineage-tracing studies in adult tissues demonstrate ongoing transcriptional heterogeneity within ostensibly homogeneous cell populations (PMID: 36198802). Single-cell chromatin accessibility profiling reveals that enhancer landscapes are dynamically maintained by the continuous activity of lineage-determining transcription factors, and that experimental removal of these factors causes rapid chromatin closure and identity erosion within 24–48 hours (PMID: 37339642). The maintenance of cell identity is therefore an active, energy-consuming process, not a default consequence of having the correct genome.

This active maintenance operates through three mechanistically distinct but quantitatively coupled axes. The first axis involves **pioneer transcription factors**—a specialized class of transcription factors capable of engaging nucleosomal DNA and initiating chromatin opening at regulatory elements that are otherwise inaccessible to the transcriptional machinery (PMID: 22056668). Pioneer factors such as FOXA1, GATA3, and SOX2 establish and maintain the enhancer landscape that defines each cell type, and their dosage perturbation drives oncogenesis and developmental disease (PMID: 37940484). Recent cryo-electron microscopy structures have revealed the molecular mechanisms by which individual pioneer factors engage nucleosomes through distinct structural strategies—wing-helix insertion into the major groove for FOXA family members (PMID: 39121853), minor groove anchor competition for NR5A2 (PMID: 38409506), and DNA bending for SOX factors (PMID: 32286363)—providing the structural foundation for understanding how these factors read and rewrite chromatin state.

The second axis involves **metabolic flux as a direct chromatin signal**. The enzymes that write and erase histone modifications are fundamentally metabolic enzymes: histone acetyltransferases require acetyl-CoA as the acetyl donor (PMID: 38839952), TET demethylases require alpha-ketoglutarate as a co-substrate (PMID: 21130288), and an expanding catalog of non-canonical histone acylations—lactylation, crotonylation, beta-hydroxybutyrylation, benzoylation—directly link cellular metabolic state to chromatin modification patterns (PMID: 25818647; PMID: 35296687). The recognition that metabolic flux is not merely a background condition but a direct determinant of epigenetic state has transformed our understanding of how environmental signals are inscribed into the chromatin landscape (PMID: 39150482).

The third axis involves **stochastic transcriptional bursting**—the fundamental observation that genes are not transcribed continuously but in discrete bursts, with promoters stochastically switching between active and inactive states according to the two-state telegraph model of gene expression (PMID: 40378829). The kinetic parameters governing this switching—burst frequency (k_on), burst duration (k_off), and burst amplitude (k_m)—are now understood to be directly controlled by enhancer activity and chromatin state (PMID: 38194964). Critically, recent live-cell imaging studies demonstrate that enhancers primarily modulate burst frequency rather than burst size, establishing a direct mechanistic link between chromatin accessibility and the statistical properties of gene expression output (PMID: 30570752).

### 1.2 Why Disruption of Any Axis Causes Identity Collapse

These three axes are not independent parallel systems but form a coupled circuit in which perturbation at any level propagates through the others. Consider three paradigmatic examples.

In **IDH-mutant glioma**, a single amino acid substitution (IDH1 R132H) converts isocitrate dehydrogenase from an alpha-ketoglutarate-producing enzyme to a D-2-hydroxyglutarate-producing enzyme. The resulting millimolar accumulation of D-2-HG competitively inhibits TET demethylases and Jumonji-family histone demethylases, producing genome-wide CpG hypermethylation (the G-CIMP phenotype) and histone hypermethylation (PMID: 22343889). This metabolic perturbation (axis 2) locks the chromatin landscape into a configuration that blocks pioneer factor access (axis 1) and silences differentiation programs, trapping neural progenitors in a proliferative state. The 2024 FDA approval of vorasidenib—a dual IDH1/IDH2 inhibitor—represents the first drug that corrects a metabolic-epigenetic coupling error, with dramatic clinical efficacy (median PFS 27.7 vs. 11.1 months) (PMID: 40911439).

In **tumor-associated macrophage polarization**, the high-lactate tumor microenvironment drives histone H3K18 lactylation at immunosuppressive gene loci in infiltrating macrophages, reprogramming them from inflammatory M1 to immunosuppressive M2 phenotype (PMID: 38703775). This metabolic signal (axis 2) alters the chromatin landscape that governs macrophage identity-determining transcription factors (axis 1), while simultaneously increasing transcriptional noise at effector gene loci (axis 3), producing a population of macrophages that is both immunosuppressive on average and transcriptionally heterogeneous—properties that together promote immune evasion.

In **aging**, the progressive decline in nuclear acetyl-CoA availability (due to reduced ACLY activity and mitochondrial dysfunction) reduces global histone acetylation at enhancers maintained by lineage-determining pioneer factors, increasing the fraction of time these enhancers spend in the nucleosome-occluded state and elevating transcriptional noise (PMID: 36585866). This age-dependent shift from constitutive to bursty expression at identity-defining gene loci contributes to the transcriptional drift that characterizes aging tissues—a progressive loss of cell type-specific gene expression programs that correlates with functional decline.

### 1.3 Scope and Positioning

This paper develops a unified quantitative framework connecting pioneer factor biology (Section 2), metabolic chromatin signaling (Section 3), and stochastic transcriptional dynamics (Section 4) through four novel mathematical models. Section 5 examines enhancer–promoter communication as the physical mechanism coupling chromatin state to transcriptional output. Section 6 develops therapeutic applications across oncology, cardiology, and regenerative medicine, culminating in a synthesis (Section 6.4) that argues metabolic microenvironment correction must precede pioneer factor engineering for therapeutic efficacy. Section 7 identifies open questions, and Section 8 concludes with a vision for precision epigenome medicine that targets the metabolic-transcriptional interface.

---

## 2. Pioneer Transcription Factor Biology

### 2.1 Defining the Pioneer Factor Concept

The term "pioneer transcription factor" was formalized by Zaret and Carroll (2011) to describe transcription factors with the distinctive ability to bind their DNA recognition sequences even when those sequences are wrapped into nucleosomes—the fundamental unit of chromatin packaging in which 147 base pairs of DNA wrap approximately 1.7 superhelical turns around an octamer of histone proteins (PMID: 22056668). This capacity distinguishes pioneer factors from the vast majority of transcription factors, which require nucleosome-free DNA to bind their recognition motifs. The biological significance is profound: pioneer factors can initiate chromatin opening at regulatory elements that are inaccessible to the broader transcriptional machinery, thereby establishing the enhancer landscape that defines cell identity.

The original characterization of FOXA proteins (formerly HNF3) as pioneer factors emerged from studies of the albumin enhancer during hepatic specification, where FOXA1 and FOXA2 bind to nucleosomal DNA prior to the activation of liver gene expression, establishing competence for subsequent binding by additional transcription factors such as GATA4, HNF1, and C/EBP family members (PMID: 37940484). The "winged-helix" DNA-binding domain of FOXA proteins structurally resembles linker histone H1, enabling engagement with nucleosomal DNA through insertion into the major groove of DNA on the nucleosome surface. This structural mimicry allows FOXA to compete with linker histones for binding, displacing H1 and locally decompacting chromatin without requiring ATP-dependent remodeling activity (PMID: 15738986).

The concept has since expanded to encompass a growing number of transcription factors with demonstrated nucleosome-binding capacity, including GATA family members, SOX factors, p53, C/EBP family members, PU.1, and several pluripotency factors (OCT4, KLF4). However, the mechanisms by which these diverse factors engage nucleosomes differ substantially, as revealed by recent structural studies (PMID: 35524225). Recent work has further shown that the interplay between pioneer factors and repressive epigenetic complexes (PRC2, NuRD, DNMT3) is a central determinant of reprogramming efficiency—pioneer factors must overcome not just nucleosomal barriers but active repressive marks deposited by these complexes (PMID: 39834592). A 2025 study revealed that nucleosome fiber topology itself guides cooperative TF binding: the three-dimensional arrangement of nucleosomes within the fiber creates a motif-grammar-guided search model in which favorable fiber conformations facilitate pioneer factor target discovery (PMID: 39695228). Furthermore, mesoscale chromatin confinement facilitates pioneer factor target search by constraining diffusion within nucleosome-dense domains, as demonstrated by single-molecule tracking in living cells (PMID: 39367253).

### 2.2 Structural Mechanisms of Nucleosome Engagement

The past two years have witnessed a revolution in our structural understanding of pioneer factor–nucleosome interactions, driven by cryo-electron microscopy studies that resolve these complexes at near-atomic resolution. These structures reveal at least four distinct mechanisms of nucleosome engagement, challenging the notion that "pioneer activity" reflects a single biochemical mechanism.

**FOXA1: Wing-helix insertion and cooperative binding.** The cryo-EM structure of mouse FOXA1 bound to the ALBN1 nucleosome (the endogenous albumin enhancer nucleosome) at 3.0 Å resolution reveals that the FOXA1 DNA-binding domain recognizes linker DNA extending from the nucleosome entry-exit site, while its intrinsically disordered C-terminal region contacts the histone H2A-H2B acidic patch—an interaction surface previously associated with linker histones, chromatin remodelers, and other chromatin regulatory proteins (PMID: 39121853). Strikingly, when GATA4 is co-incubated with FOXA1 on the same nucleosome, FOXA1 facilitates GATA4 binding by repositioning the nucleosome—a direct structural demonstration of the "pioneer-then-recruit" model. GATA4 alone binds an internal nucleosomal site at superhelical location (SHL) +3 through its zinc-finger DNA-binding domain, but binding efficiency increases substantially in the presence of FOXA1.

**NR5A2: DNA minor groove anchor competition.** The cryo-EM structure of NR5A2 (LRH-1) bound to a nucleosome containing its cognate motif at SHL+5.5 reveals a mechanistically distinct pioneering strategy (PMID: 38409506). NR5A2 engages the nucleosome through its conserved C-terminal extension (CTE) loop, which competes directly with a DNA minor groove anchor—a histone-DNA contact point where arginine residues of the histone octamer insert into the DNA minor groove to stabilize the nucleosome. CTE-mediated competition with this anchor releases the entry-exit DNA from the histone surface, causing partial DNA unwrapping without full nucleosome displacement. Mutational analysis demonstrated that NR5A2 residue D159 in the CTE is dispensable for binding free DNA but essential for stable nucleosome association and persistent DNA unwrapping. This "anchor competition" mechanism is notable because it targets the weakest histone-DNA contacts (entry-exit regions), providing an energetically favorable pathway for chromatin opening.

**SOX2: DNA bending on the nucleosome surface.** SOX factors engage nucleosomes through a mechanistically distinct strategy involving DNA bending. The cryo-EM structures of SOX2 and SOX11 bound to nucleosomes demonstrated that SOX factors bind at superhelical location 2 (SHL 2), where they locally distort the DNA, inducing a kink that partially detaches the terminal nucleosomal DNA from the histone octamer (PMID: 32286363). Unlike FOXA1, which primarily engages linker DNA, SOX factors can access internal nucleosomal sites, but their binding affinity is strongly modulated by the rotational positioning of their recognition motif relative to the histone octamer surface. SOX2 and FOXA1 employ fundamentally different chromatin scanning modes: SOX2 preferentially samples nucleosomal DNA through rapid binding-unbinding events, while FOXA1 scans through more stable, longer-lived interactions (PMID: 37405916).

**p53: Context-dependent pioneer activity.** p53 exhibits pioneer-like nucleosome binding at a subset of its response elements, with binding affinity dependent on the DNA sequence context and nucleosome positioning. The tetrameric structure of p53 enables simultaneous engagement with two DNA half-sites that may be exposed on opposite faces of the nucleosome surface, providing a structural basis for its ability to detect response elements within chromatin. However, p53 pioneer activity is not universal—it is restricted to response elements with favorable rotational positioning relative to the histone octamer, explaining why only a subset of p53 targets are accessible in the nucleosomal context (PMID: 32355327). This context dependence has important implications for understanding how p53 mutations alter chromatin engagement in cancer.

### 2.3 Pioneer Factor Hierarchy and Temporal Logic

The activation of a lineage-specific enhancer is not a single-step process but unfolds through a stereotyped temporal sequence involving multiple transcription factors. Time-resolved studies of enhancer activation during cellular differentiation have revealed a hierarchical organization in which pioneer factors act first, establishing accessibility that permits subsequent binding by additional factors.

**The "scan, initiate, recruit" model.** Current evidence supports a three-step model for pioneer factor-mediated enhancer activation (PMID: 35524225). First, pioneer factors **scan** nucleosomal DNA through rapid, transient interactions, sampling the accessibility of their recognition motifs within chromatin. The newly developed Pioneer-seq assay, which measures transcription factor binding to thousands of different nucleosome sequences in parallel, demonstrates that even factors classified as pioneers show substantial sequence-dependent variation in nucleosome binding strength—OCT4, KLF4, and SOX2 all bind preferentially at nucleosome edges, where DNA is more accessible, but KLF4 and SOX2 can also access sites near the nucleosome dyad in a sequence-dependent manner (PMID: 40240537). Second, upon finding a favorable site, the pioneer factor **initiates** partial DNA unwrapping or local structural distortion, creating a locally accessible intermediate state. This intermediate does not involve full nucleosome displacement but rather a partial opening that exposes additional DNA binding sites. Third, the locally accessible state enables **recruitment** of ATP-dependent chromatin remodeling complexes, particularly SWI/SNF family remodelers (BAF, PBAF, and ncBAF), which complete the process through nucleosome sliding or eviction (PMID: 38843835).

**Sequential vs. cooperative activation.** The temporal relationship between pioneer factors and remodelers has been clarified by time-resolved ATAC-seq and CUT&RUN experiments during macrophage activation, which demonstrate that all three mammalian SWI/SNF variants (cBAF, ncBAF, and PBAF) are pre-bound at genomic sites that subsequently undergo stimulus-dependent changes in chromatin accessibility (PMID: 38843835). At latent enhancers activated de novo during inflammatory stimulation, the cooperative binding of all three SWI/SNF variants is associated with chromatin opening, while at sites where only one or two variants are present, the accessibility change is more modest. The critical influence of SWI/SNF complexes in cancer has been comprehensively reviewed in 2025, highlighting synthetic lethality strategies that exploit the dependency of SWI/SNF-mutant cancers on residual remodeling activity (PMID: 40269969). A 2025 CRISPR screen decoded SWI/SNF complex assembly, identifying MLF2 as a promoter of complex assembly and RBM15 as a controller of subunit protein levels through m6A modification (PMID: 40447637). A landmark 2025 Science study identified a SWIFT immunoglobulin-like domain on SMARCD subunits as a universal TF binding platform, with mutation of this domain disrupting PU.1-mSWI/SNF interaction in acute myeloid leukemia (PMID: 40766474). The SWI/SNF PBAF complex has also been shown to facilitate REST occupancy at repressive chromatin, revealing that PBAF plays a dual role in both activating and repressive chromatin regulation depending on the TF context (PMID: 40306253). This finding suggests that the number of remodeling complexes recruited—which depends on the initial pioneer factor-mediated accessibility—determines the magnitude and stability of chromatin opening.

**Dosage sensitivity and haploinsufficiency.** Pioneer factors exhibit striking dosage sensitivity, with heterozygous loss frequently causing pathological phenotypes. FOXA1 is a lineage-dependency factor in prostate cancer, where it cooperates with the androgen receptor to establish and maintain the luminal enhancer program; divergent FOXA1 mutations drive prostate tumorigenesis through distinct mechanisms involving altered chromatin binding specificity (PMID: 38851846). FOXA2 can substitute for FOXA1 in some contexts but binds distinct developmental enhancers and collaborates with JUN to drive lineage plasticity toward therapy-resistant states. GATA3 functions as a pioneer factor in mammary luminal cell identity, and its loss in breast cancer is associated with the triple-negative phenotype—the most aggressive subtype—suggesting that GATA3 re-expression could potentially restore luminal differentiation (PMID: 37582221). C/EBPα serves as a pioneer factor for myeloid differentiation, and its silencing in acute myeloid leukemia blocks differentiation; the clinical development of MTL-CEBPA, a liposomal small activating RNA that upregulates C/EBPα expression, represents a direct therapeutic application of pioneer factor biology (PMID: 40686853). GATA3 has recently been shown to pioneer new enhancers through a stepwise nucleosome exposure mechanism, collaborating with recruited TFs and chromatin remodelers to progressively open chromatin at lineage-specific regulatory elements (PMID: 40479714). A 2025 study demonstrated that different pioneer factors target distinct classes of repressed chromatin states—some preferentially open PRC2-marked (H3K27me3) chromatin while others target heterochromatic (H3K9me3) domains—providing a molecular basis for lineage-specific pioneer factor function (PMID: 40355686).

### 2.4 Mathematical Framework NEW-1: Statistical Thermodynamics of TF–Nucleosome Competitive Binding

The mechanistic diversity of pioneer factor–nucleosome engagement can be unified within a statistical thermodynamic framework that treats the nucleosomal regulatory element as a system with multiple possible binding states, each with a defined free energy. This approach, grounded in the Boltzmann distribution, provides quantitative predictions for how pioneer factor concentration controls the accessibility of downstream transcription factor binding sites.

**Single-site partition function.** Consider a single nucleosomal regulatory element that can exist in three states: (1) occluded (nucleosome intact, no factors bound), (2) pioneer-engaged (pioneer factor bound to nucleosomal DNA, partial unwrapping), and (3) activated (canonical transcription factor bound to accessible DNA). The partition function for this system is:

$$Z = 1 + \frac{[P]}{K_{d,P}} + \frac{[T]}{K_{d,T}} \cdot \alpha([P])$$

where *[P]* is the nuclear concentration of the pioneer factor, *K_{d,P}* is the dissociation constant for pioneer factor–nucleosome binding (typically 100–500 nM based on in vitro measurements (PMID: 39121853)), *[T]* is the concentration of the canonical transcription factor, *K_{d,T}* is the dissociation constant for TF–DNA binding (~1–50 nM for exposed DNA), and *α([P])* is the accessibility function that depends on pioneer factor occupancy.

The accessibility function captures the essential thermodynamic switch:

$$\alpha([P]) = \frac{[P]/K_{d,P}}{1 + [P]/K_{d,P}}$$

This represents the probability that the pioneer factor has opened the site sufficiently for canonical TF binding. Without the pioneer (*[P]* = 0), *α* = 0 and the TF-bound state has zero statistical weight regardless of *[T]*—the site is thermodynamically inaccessible. With saturating pioneer (*[P]* >> *K_{d,P}*), *α* → 1 and the site becomes fully accessible.

The probability of the activated state (canonical TF bound) is:

$$P_{\text{active}} = \frac{[T] \cdot \alpha([P]) / K_{d,T}}{Z}$$

**Multi-site enhancer extension.** Real enhancers contain multiple binding sites. For an enhancer with *N* independent binding sites, the total partition function is the product of individual site partition functions:

$$Z_{\text{enh}} = \prod_{i=1}^{N} Z_i$$

The probability that the enhancer is fully activated (all sites occupied) is:

$$P_{\text{full}} = \prod_{i=1}^{N} P_{\text{active},i}$$

For a simplified case where all sites have identical parameters, this becomes:

$$P_{\text{full}} = \left(\frac{[T] \cdot \alpha([P]) / K_{d,T}}{Z}\right)^N$$

**Effective Hill coefficient from sequential binding.** The sequential requirement for pioneer binding followed by TF binding generates apparent cooperativity even in the absence of direct protein-protein cooperativity. The effective Hill coefficient for the dependence of enhancer activation on pioneer factor concentration is:

$$n_{\text{eff}} = N \cdot \frac{d \ln \alpha}{d \ln [P]} = N \cdot \frac{1}{1 + [P]/K_{d,P}}$$

At low pioneer concentrations (*[P]* << *K_{d,P}*), *n_eff* ≈ *N*, producing highly cooperative, switch-like activation. At saturating pioneer concentrations, *n_eff* → 0, indicating that the system becomes insensitive to further increases in pioneer factor levels. This predicts that pioneer factor dosage sensitivity is greatest at intermediate concentrations—precisely the regime relevant to haploinsufficiency phenotypes.

**Quantitative predictions.**

1. *Pioneer factor dosage sensitivity*: For a 4-site enhancer with *K_{d,P}* = 300 nM, reducing pioneer factor concentration from 300 nM to 150 nM (heterozygous loss) reduces *P_full* by approximately 16-fold, explaining the severity of FOXA1 and GATA3 haploinsufficiency in cancer.

2. *Threshold behavior*: The model predicts a sharp transition from inactive to active enhancer states as pioneer factor concentration crosses *K_{d,P}*, providing a quantitative basis for the binary nature of cell fate decisions during differentiation.

3. *Specificity through combinatorial control*: Multi-site enhancers requiring both a pioneer factor and multiple canonical TFs achieve exponential specificity: with *N* = 4 independent binding requirements, the probability of spurious activation at an off-target site is *P_full^{off}* = (*P_active^{off}*)^4, providing >10^6-fold discrimination.

This framework is distinct from prior mathematical models, which employ Michaelis-Menten kinetics for receptor binding (F055), ODE bistability for cell state switches (F040-F046, F067-F070), and Ising/Potts models for cooperative chromatin transitions (F136-F138). The Boltzmann partition function approach treats the nucleosomal element as a thermodynamic system in equilibrium, providing complementary insight into how pioneer factor concentration controls the statistical weight of different binding configurations.

---

## 3. Metabolic Epigenetics: Metabolites as Chromatin Signals

### 3.1 The Metabolite–Chromatin Axis

The enzymes that catalyze histone modifications do not operate in a substrate-unlimited regime. Instead, the nuclear concentrations of their metabolite substrates and cofactors fluctuate in response to cellular metabolic state, nutrient availability, and disease-associated metabolic reprogramming. This creates a direct, quantitative coupling between metabolic flux and chromatin modification state—the "metabolite-chromatin axis" (PMID: 38839952).

**Nuclear acetyl-CoA as universal acetyl donor.** All histone acetyltransferases (HATs)—including p300/CBP, GCN5/PCAF, and MYST family members—require acetyl-coenzyme A (acetyl-CoA) as the acetyl group donor for histone lysine acetylation. The nuclear pool of acetyl-CoA is maintained by three enzymatic sources, each linked to a distinct metabolic pathway. ATP-citrate lyase (ACLY) cleaves citrate—exported from the mitochondrial TCA cycle—to generate cytosolic and nuclear acetyl-CoA and oxaloacetate (PMID: 39150482). Acyl-CoA synthetase short-chain family member 2 (ACSS2) converts acetate—derived from dietary intake, gut microbiome metabolism, or histone deacetylase activity—to acetyl-CoA. The pyruvate dehydrogenase complex (PDC) can also translocate to the nucleus, where it locally generates acetyl-CoA from pyruvate (PMID: 30573679). All three enzymes have been demonstrated to localize to the nucleus, establishing the nucleus as a metabolically semi-autonomous compartment capable of locally producing the substrates required for chromatin modification.

The functional importance of nuclear acetyl-CoA production was demonstrated by a striking 2024 study showing that histone H3K18 acetylation levels in Drosophila wing disc epithelium are controlled by nuclear position: nuclei near the tissue surface have elevated acetyl-CoA synthase levels and increased H3K18ac, with fatty acid beta-oxidation providing the carbon source (PMID: 38839952). In the mammalian immune system, CD8 T cell effector responses depend critically on acetyl-CoA derived from citrate via ACLY; genetic ablation of ACLY reduces H3K27ac at effector gene loci and impairs T cell function, but this deficiency can be rescued by exogenous acetate through the compensatory ACSS2 pathway (PMID: 39150482).

A 2025 study in Advanced Science confirmed that nuclear ACLY directly recruits the histone acetyltransferases P300 and HAT1, physically coupling acetyl-CoA production with histone acetylation at the same nuclear location (PMID: 39686679). This nuclear ACLY-HAT recruitment mechanism is essential for early embryo development: maternal ACLY deletion preserves fertility due to compensatory ACSS2 upregulation, but zygotic ACLY knockout causes developmental arrest at the pre-blastocyst stage (PMID: 40470746). A landmark 2026 study using native chromatome profiling revealed hundreds of metabolic enzymes directly associated with chromatin across tissues, with tissue-specific patterns suggesting that metabolic enzyme chromatin localization is a regulated process contributing to cell type-specific epigenetic programs (PMID: 41792114). These findings establish that the nuclear metabolic compartment is far more complex than previously appreciated—it is not simply a secondary pool of cytoplasmic metabolites but a regulated interface between metabolism and gene expression (PMID: 39824167).

**The nucleus as metabolic sensor.** A complementary 2024 study in Science demonstrated that nutrient-driven histone modifications constitute a "histone code" that determines the fate of exhausted CD8 T cells (PMID: 39666821). In nutrient-replete conditions, glucose-derived acetyl-CoA fuels H3K27ac at effector gene loci, maintaining functional capacity. In the nutrient-depleted tumor microenvironment, reduced acetyl-CoA availability decreases H3K27ac and increases H3K27me3 at the same loci, promoting terminal exhaustion—an irreversible loss of effector function. This finding establishes that metabolic state does not merely correlate with immune cell function but causally determines it through direct modulation of chromatin modifications.

### 3.2 The Alpha-KG / Succinate Ratio as Master Epigenetic Regulator

The ten-eleven translocation (TET) family of dioxygenases (TET1, TET2, TET3) catalyze the iterative oxidation of 5-methylcytosine (5mC) to 5-hydroxymethylcytosine (5hmC), 5-formylcytosine (5fC), and 5-carboxylcytosine (5caC)—the initial steps in active DNA demethylation (PMID: 21130288). The Jumonji C (JmjC) domain-containing histone demethylases (KDM2-7 families) catalyze the oxidative removal of methyl groups from histone lysine residues. Both enzyme families share a common catalytic mechanism: they are Fe(II)- and alpha-ketoglutarate (alpha-KG)-dependent dioxygenases that couple the oxidative decarboxylation of alpha-KG to succinate with the hydroxylation of their substrate.

This mechanistic requirement creates a vulnerability: the activity of TET and JmjC enzymes is directly proportional to the nuclear alpha-KG/succinate ratio, and competitive inhibition by structurally similar metabolites—succinate, fumarate, and D-2-hydroxyglutarate (D-2-HG)—can profoundly suppress their activity.

**IDH mutations and the 2-HG oncometabolite.** Isocitrate dehydrogenase 1 (IDH1) and IDH2 are metabolic enzymes that interconvert isocitrate and alpha-KG. Heterozygous point mutations at IDH1 R132 (most commonly R132H) and IDH2 R140/R172 confer a neomorphic enzymatic activity: the mutant enzyme reduces alpha-KG to D-2-hydroxyglutarate (D-2-HG) in an NADPH-dependent reaction, accumulating D-2-HG to millimolar concentrations in tumor cells (PMID: 22343889). D-2-HG is a competitive inhibitor of TET2 with an inhibition constant (Ki) of approximately 5 mM, and of multiple JmjC histone demethylases with Ki values ranging from 0.1 to 5 mM depending on the specific enzyme (PMID: 21436587).

The consequences are far-reaching. TET2 inhibition by D-2-HG produces the CpG island methylator phenotype (G-CIMP)—a genome-wide pattern of CpG island hypermethylation that silences tumor suppressor genes and differentiation programs (PMID: 22588877). Simultaneously, JmjC inhibition produces histone hypermethylation at H3K9, H3K27, and H3K36, further reinforcing transcriptional silencing. The combined DNA and histone hypermethylation creates a locked chromatin state that blocks the access of lineage-determining pioneer factors to their target enhancers, trapping cells in an undifferentiated, proliferative state.

**Vorasidenib: Correcting the metabolic-epigenetic axis.** The clinical validation of this metabolite-chromatin coupling came with the FDA approval of vorasidenib (Voranigo, Servier) on August 6, 2024, for Grade 2 astrocytoma or oligodendroglioma with susceptible IDH1 or IDH2 mutations following surgery (PMID: 40911439). Vorasidenib is a brain-penetrant dual inhibitor of both mutant IDH1 and IDH2, designed to reduce intratumoral D-2-HG production and restore TET/JmjC activity. In the pivotal INDIGO trial (NCT04164901), vorasidenib improved median progression-free survival from 11.1 months (placebo) to 27.7 months, with a hazard ratio of 0.39 (PMID: 37540028). Vorasidenib represents the first drug approved on the basis of correcting a metabolic-epigenetic coupling error—a therapeutic paradigm in which the drug target is not a signaling pathway or a cell-surface receptor but a metabolic enzyme whose aberrant product alters the chromatin landscape.

An unresolved question with significant therapeutic implications is whether vorasidenib-mediated D-2-HG reduction fully reverses the accumulated epigenetic damage or merely prevents further accumulation. Preclinical data suggest partial reversal: IDH inhibitor treatment reduces D-2-HG within days but requires weeks to months to significantly reduce DNA methylation at G-CIMP loci, and some hypermethylated loci appear resistant to reversal, consistent with the self-reinforcing nature of DNA methylation maintenance by DNMT1 (PMID: 36920791).

### 3.3 Non-Canonical Histone Acylations

Beyond acetylation and methylation, an expanding catalog of chemically diverse histone lysine acylations has been identified, each derived from a distinct metabolic pathway and each with the potential to create a unique chromatin regulatory signal.

**Histone lactylation (Kla).** First identified in 2019 as a novel modification in which L-lactyl groups are transferred from lactyl-CoA to histone lysine residues, histone lactylation has emerged as a critical mediator of metabolic-epigenetic coupling in inflammation and cancer (PMID: 39533061). p300 functions as the primary lactylase, catalyzing the transfer of lactyl groups from lactyl-CoA to histone lysines, while HDAC1, HDAC2, and HDAC3 serve as de-lactylases (PMID: 36585562). The modification is enriched at active promoters and enhancers, with H3K18la showing particularly strong association with gene activation.

The functional significance of histone lactylation in tumor immunology was established by a 2024 study in Immunity demonstrating that glucose-driven histone lactylation promotes the immunosuppressive activity of monocyte-derived macrophages in glioblastoma (PMID: 38703775). In the high-lactate tumor microenvironment, macrophage uptake of tumor-derived lactate drives H3K18la at immunosuppressive gene loci, including IL-10, promoting M2 polarization. PERK signaling was identified as an upstream regulator: PERK deletion in monocyte-derived macrophages abrogated histone lactylation and restored T cell-mediated anti-tumor immunity in vivo. This finding establishes histone lactylation as a direct mechanistic link between tumor metabolic reprogramming and immune evasion.

Lactylation plays pathological roles beyond cancer. In cardiac ischemia-reperfusion injury, the burst of lactate production during ischemia drives H3K18la at inflammatory gene loci in cardiomyocytes and infiltrating macrophages, exacerbating tissue damage during reperfusion (PMID: 37452175). In neuroinflammation, microglial histone lactylation promotes the expression of pro-inflammatory mediators following traumatic brain injury (PMID: 37634564). In T cell biology, effector CD8 T cells exhibit high levels of histone lactylation (consistent with their glycolytic metabolic program), while terminally exhausted CD8 T cells show markedly reduced lactylation, suggesting that the metabolic transition from glycolysis to oxidative phosphorylation during exhaustion is accompanied by a coordinated loss of lactyl-CoA-derived chromatin marks (PMID: 39417714). A 2024 study in Nature Immunology further dissected this relationship, revealing that H3K18la and H3K9la drive distinct metabolic profiles in CD8 T cell subsets, with specific lactylation marks promoting either effector or memory differentiation depending on the genomic context (PMID: 39375549). Beyond cancer immunology, histone lactylation has been identified as a key mediator of BCG-induced trained innate immunity: a 2025 study in Cell demonstrated that long-term H3K18la at pro-inflammatory gene loci connects metabolic and epigenetic rewiring during the establishment of innate immune memory, providing a molecular mechanism for the non-specific protective effects of BCG vaccination (PMID: 40318634). A 2025 study further showed that lactate-driven histone lactylation activates trained immunity by fueling the TCA cycle, creating a feedforward loop between metabolism and epigenetic programming (PMID: 40185732). These findings have positioned histone lactylation as a promising therapeutic target for overcoming immune evasion and therapy resistance across multiple cancer types (PMID: 40753273).

**Histone crotonylation (Kcr).** Sabari et al. (2015) demonstrated that the coactivator p300 possesses histone crotonyltransferase activity in addition to its acetyltransferase activity, and that p300-catalyzed histone crotonylation directly stimulates transcription to a greater degree than histone acetylation at comparable levels of modification (PMID: 25818647). Crotonyl-CoA, the donor for this modification, is generated primarily through beta-oxidation of short-chain fatty acids (SCFAs), establishing a link between gut microbiome-derived metabolites (such as butyrate and crotonate) and host chromatin state. The chromodomain Y-like protein CDYL functions as a negative regulator of crotonylation, acting as a crotonyl-CoA hydratase that converts crotonyl-CoA to beta-hydroxybutyryl-CoA, thereby depleting the substrate pool (PMID: 28525742).

Histone crotonylation is enriched at active promoters and enhancers and plays tissue-specific regulatory roles. In spermatogenesis, ACSS2-dependent crotonylation is essential for the expression of genes required for sperm maturation (PMID: 28525742). In the kidney, aberrantly elevated H3K9cr in tubular epithelial cells of fibrotic kidneys promotes IL-1β expression, driving macrophage activation and tubular cell senescence; pharmacological inhibition of ACSS2 suppresses H3K9cr and delays renal fibrosis progression (PMID: 38531898). In diabetic kidney disease, exogenous sodium crotonate alleviates disease through ACSS2- and p300-induced histone crotonylation at protective gene loci (PMID: 38822951). The role of crotonylation has recently been extended to neurodegeneration: a 2026 study demonstrated that microglial H3K18 crotonylation promotes STAT1 expression and induces cognitive deficits in Alzheimer's disease models, suggesting that crotonylation-dependent inflammatory gene activation in microglia contributes to neuroinflammatory pathology (PMID: 41676156). The therapeutic potential of targeting crotonylation pathways is now being actively explored, with recent comprehensive reviews highlighting the regulation and function of lysine crotonylation across cardiovascular, renal, neurological, and inflammatory diseases (PMID: 39836379).

**Beta-hydroxybutyrylation (Kbhb).** Histone lysine beta-hydroxybutyrylation was first characterized using mass spectrometry approaches, which identified 46 Kbhb sites on histones in both yeast and mammalian cells (PMID: 27105115). The modification is directly driven by the ketone body beta-hydroxybutyrate (BHB), produced during hepatic ketogenesis in fasting, starvation, or ketogenic diet conditions. H3K9bhb is dramatically induced in livers of mice subjected to prolonged fasting or streptozotocin-induced diabetic ketoacidosis, where it marks the promoters of starvation-responsive genes involved in amino acid catabolism, redox homeostasis, and circadian regulation.

Recent studies have expanded the functional significance of Kbhb beyond hepatic metabolism. In skeletal muscle, BHB-induced histone Kbhb promotes the transcription of mitochondrial genes, and this modification is indispensable for the reversal of sarcopenia by ketone body supplementation (PMID: 39076122). A 2024 study examining organ-specific responses to ketogenic diet found that global acetylation and beta-hydroxybutyrylation dramatically increase in most organs (liver, kidney, heart, skeletal muscle) but not in the brain, revealing tissue-specific metabolic compartmentalization of this modification (PMID: 38640734). This organ-specific pattern suggests that the blood-brain barrier and brain-specific metabolic pathways create a protected chromatin environment with distinct acylation signatures. In hypertension, histone beta-hydroxybutyrylation has been demonstrated to contribute to renoprotection: BHB-mediated H3K9bhb at metabolic and immune gene loci ameliorates kidney damage in the Dahl salt-sensitive rat model (PMID: 40726393). A complementary 2025 study confirmed that ketone body-mediated histone Kbhb is reno-protective through chromatin remodeling at metabolic and immune genes, establishing Kbhb as a therapeutic target in cardiorenal metabolic disease (PMID: 39763881). In metabolic syndrome, H3K9bhb-mediated upregulation of lipolytic genes (Hmgcs2, Cyp2d4) attenuates adiposity and improves metabolic parameters (PMID: 40720185).

**Histone benzoylation (Kbz).** Histone lysine benzoylation was identified as a novel post-translational modification derived from benzoyl-CoA, a metabolic intermediate in the degradation of aromatic compounds by gut microflora (PMID: 30555539). Benzoyl-CoA can be generated from sodium benzoate—an FDA-approved food preservative and pharmaceutical compound—establishing a direct link between diet, gut microbiome metabolism, and host chromatin state. Global profiling identified 207 Kbz sites on 149 non-histone proteins, enriched in pathways involving ribosome biogenesis, glycolysis, and RNA processing (PMID: 35296687). The SIRT2 deacetylase functions as the eraser for histone benzoylation, while the DPF and YEATS family proteins (but not bromodomains) serve as readers that recognize the modification (PMID: 33290558). The biological significance of this microbiome-to-chromatin signaling pathway remains an active area of investigation, with recent evidence linking benzoylation to neurological function through probiotics-derived sodium benzoate-mediated effects on astrocyte gene expression (PMID: 39905005).

### 3.4 Mathematical Framework NEW-2: Metabolic Flux Control of Chromatin Modification State

The coupling between metabolic flux and chromatin modification can be formalized as a stoichiometric model in which the steady-state fraction of nucleosomes bearing a given modification is determined by the balance between writer and eraser enzyme activities, both of which depend on metabolite substrate concentrations.

**Writer–eraser balance at steady state.** For any histone modification established by a writer enzyme with velocity *v_write* and removed by an eraser enzyme with velocity *v_erase*, the steady-state fraction of modified nucleosomes is:

$$f_{\text{mark}} = \frac{v_{\text{write}}}{v_{\text{write}} + v_{\text{erase}}}$$

For histone acetylation, where the writer is a HAT (e.g., p300) requiring acetyl-CoA and the eraser is an HDAC:

$$v_{\text{HAT}} = V_{\max,\text{HAT}} \cdot \frac{[\text{Ac-CoA}]}{K_{m,\text{HAT}} + [\text{Ac-CoA}]} \cdot \frac{[\text{nuc}_{\text{sub}}]}{K_{m,\text{nuc}} + [\text{nuc}_{\text{sub}}]}$$

$$v_{\text{HDAC}} = V_{\max,\text{HDAC}} \cdot \frac{[\text{Ac-nuc}]}{K_{m,\text{HDAC}} + [\text{Ac-nuc}]} \cdot \frac{1}{1 + [\text{butyrate}]/K_{i,\text{HDAC}}}$$

where *[Ac-CoA]* is the nuclear acetyl-CoA concentration (estimated at 2–20 μM depending on metabolic state (PMID: 38839952)), *K_{m,HAT}* is the Michaelis constant for acetyl-CoA utilization by the HAT (~1–10 μM for p300), *[nuc_sub]* is the concentration of unmodified nucleosome substrate, *[Ac-nuc]* is the concentration of acetylated nucleosomes, and *[butyrate]* is the concentration of the HDAC inhibitor butyrate with inhibition constant *K_{i,HDAC}*.

The steady-state acetylation fraction is therefore:

$$f_{\text{ac}} = \frac{V_{\text{HAT}} \cdot [\text{Ac-CoA}] / K_{m,\text{HAT}}}{V_{\text{HAT}} \cdot [\text{Ac-CoA}] / K_{m,\text{HAT}} + V_{\text{HDAC}} / (1 + [\text{butyrate}]/K_{i,\text{HDAC}})}$$

**For histone lactylation:**

$$v_{\text{lac}} = V_{\max,p300}^{\text{lac}} \cdot \frac{[\text{La-CoA}]}{K_{m,\text{lac}} + [\text{La-CoA}]} \cdot [\text{H3K18}_{\text{unlac}}]$$

where *[La-CoA]* is the nuclear lactyl-CoA concentration, which is directly proportional to cytoplasmic lactate concentration through the action of acyl-CoA synthetases. In the tumor microenvironment, lactate concentrations reach 10–40 mM (compared to 1–3 mM in normal tissues), predicting a substantial increase in H3K18la at susceptible loci.

**For TET-dependent demethylation under IDH mutation:**

$$v_{\text{TET}} = V_{\max,\text{TET}} \cdot \frac{[\alpha\text{-KG}]}{K_{m,\alpha\text{KG}} \cdot (1 + [\text{2-HG}]/K_{i,\text{2HG}}) + [\alpha\text{-KG}]}$$

In wild-type cells, *[alpha-KG]* ≈ 0.1–1 mM and *[2-HG]* is negligible, yielding near-maximal TET activity. In IDH-mutant cells, *[2-HG]* accumulates to 1–30 mM, while *[alpha-KG]* is simultaneously depleted. With *K_{i,2HG}* ≈ 5 mM and *K_{m,alphaKG}* ≈ 60 μM (PMID: 21436587):

$$v_{\text{TET}}^{\text{IDH-mut}} \approx V_{\max,\text{TET}} \cdot \frac{[\alpha\text{-KG}]}{K_{m,\alpha\text{KG}} \cdot (1 + 10/5) + [\alpha\text{-KG}]} = V_{\max,\text{TET}} \cdot \frac{[\alpha\text{-KG}]}{3K_{m,\alpha\text{KG}} + [\alpha\text{-KG}]}$$

This predicts approximately 3-fold reduction in TET activity at moderate 2-HG concentrations (10 mM), and up to 7-fold reduction at high 2-HG concentrations (30 mM). Since DNMT activity is unaffected by 2-HG, the steady-state methylation fraction shifts dramatically:

$$f_{\text{5mC}}^{\text{IDH-mut}} = \frac{v_{\text{DNMT}}}{v_{\text{DNMT}} + v_{\text{TET}}^{\text{IDH-mut}}} \gg f_{\text{5mC}}^{\text{WT}}$$

**Testable predictions:**

1. *Warburg-driven lactylation*: The Warburg effect increases cytoplasmic lactate from ~2 mM to ~20 mM, predicting a ~10-fold increase in *[La-CoA]* and a corresponding increase in H3K18la at susceptible loci. This is consistent with the observed enrichment of H3K18la in tumor-associated macrophages (PMID: 38703775).

2. *Quantitative IDH prediction*: The model predicts that CpG hypermethylation degree should scale with intratumoral 2-HG concentration, which can be measured non-invasively by MRS imaging. Patients with higher 2-HG (measured by MRS) should show more severe G-CIMP, and vorasidenib-mediated 2-HG reduction should correlate with progressive demethylation at G-CIMP loci.

3. *HDAC inhibitor synergy with metabolic perturbation*: The model predicts that HDAC inhibitors (which reduce *v_erase*) and interventions that increase nuclear acetyl-CoA (which increase *v_write*) should synergistically increase histone acetylation, with the magnitude of synergy depending on the relative magnitudes of *V_HAT* and *V_HDAC* at each locus.

---

## 4. Stochastic Transcriptional Dynamics

### 4.1 The Two-State (Telegraph) Model of Gene Expression

The two-state model, also known as the telegraph model, provides the foundational mathematical framework for understanding stochastic gene expression (PMID: 40378829). In this model, a gene promoter stochastically switches between an OFF (inactive, nucleosome-occluded) state and an ON (active, accessible) state. When ON, the promoter produces mRNA at rate *k_m*; mRNA degrades at rate *γ_m*. The switching rates are *k_on* (OFF → ON) and *k_off* (ON → OFF).

The model is described by the chemical master equation:

$$\frac{dP_{\text{ON}}(m,t)}{dt} = k_{\text{on}} P_{\text{OFF}}(m,t) - k_{\text{off}} P_{\text{ON}}(m,t) + k_m [P_{\text{ON}}(m-1,t) - P_{\text{ON}}(m,t)] + \gamma_m [(m+1)P_{\text{ON}}(m+1,t) - m P_{\text{ON}}(m,t)]$$

$$\frac{dP_{\text{OFF}}(m,t)}{dt} = k_{\text{off}} P_{\text{ON}}(m,t) - k_{\text{on}} P_{\text{OFF}}(m,t) + \gamma_m [(m+1)P_{\text{OFF}}(m+1,t) - m P_{\text{OFF}}(m,t)]$$

The steady-state mRNA distribution follows a Beta-Poisson (or Poisson-Beta) distribution, which in the limit of short, infrequent bursts (*k_off* >> *k_on*) reduces to a negative binomial distribution (PMID: 37885177):

$$P(m) = \text{NB}(m; r = k_{\text{on}}/\gamma_m, p = k_m/(k_m + k_{\text{off}}))$$

The mean and variance of the mRNA distribution are:

$$\langle m \rangle = \frac{k_{\text{on}}}{k_{\text{on}} + k_{\text{off}}} \cdot \frac{k_m}{\gamma_m}$$

$$\text{Var}(m) = \langle m \rangle + \frac{k_m}{k_{\text{on}} + k_{\text{off}} + \gamma_m} \cdot \langle m \rangle$$

The **Fano factor** (variance/mean) quantifies the deviation from Poisson statistics:

$$F = 1 + \frac{k_m}{k_{\text{on}} + k_{\text{off}} + \gamma_m}$$

When *F* = 1, expression follows Poisson statistics (constitutive, non-bursty). When *F* >> 1, expression is super-Poissonian (bursty), indicating that mRNA is produced in discrete bursts with significant cell-to-cell variability. In the bursty regime, the burst frequency is *k_on* and the mean burst size is *b* = *k_m*/*k_off*.

### 4.2 Enhancer Control of Burst Frequency vs. Burst Size

A central finding from recent live-cell imaging studies is that enhancers primarily modulate **burst frequency** (*k_on*), while core promoter elements primarily modulate **burst size** (*k_m*/*k_off*). This finding, established through multiple independent experimental approaches, fundamentally reshapes our understanding of how enhancers regulate gene expression (PMID: 30570752).

**Evidence from MS2/PP7 live-cell imaging.** The MS2 and PP7 systems enable real-time visualization of nascent transcription in living cells by inserting stem-loop sequences into the gene of interest that recruit fluorescently tagged coat proteins upon transcription. Using these systems in Drosophila embryos, Fukaya et al. demonstrated that different developmental enhancers produce transcriptional bursts with similar amplitudes and duration but dramatically different burst frequencies—strong enhancers generate more frequent bursts than weak enhancers, with minimal effect on burst size (PMID: 27281222). This pattern has been confirmed in mammalian cells using both MS2 imaging and computational inference from single-cell RNA-seq data (PMID: 35241838).

**Super-enhancers approach constitutive expression.** A 2024 study using live-cell super-resolution imaging directly observed the effect of condensate proximity on gene bursting at the Sox2 locus, which is controlled by a super-enhancer (PMID: 38194964). When the super-enhancer condensate was distant (>1 μm) from the promoter, basal transcriptional bursting occurred at low frequency. When the condensate moved into proximity (<1 μm), both burst frequency and burst size were enhanced, approaching near-constitutive expression. This finding links the three-dimensional organization of enhancer–promoter contacts to burst kinetics, with super-enhancer hubs effectively converting bursty expression to near-constitutive expression through sustained proximity.

**High-throughput identification of burst regulators.** Two complementary 2025 studies developed high-throughput approaches to identify molecular determinants of gene-specific bursting patterns. A Molecular Cell study (PMID: 40105563) and a parallel imaging screen (PMID: 39978338) both identified protein acetylation as a prominent effector of burst kinetics. Screening small-molecule perturbations combined with smFISH revealed that protein acetylation is a prominent effector of burst frequency and burst size, acting via decreasing promoter off-times and gene-specific changes in on-time. This directly connects Section 3 (metabolic control of acetylation) to Section 4 (burst kinetics), demonstrating that the metabolic-epigenetic axis regulates transcription not just at the level of mean expression but at the level of individual burst events.

**scRNA-seq deconvolution of burst kinetics.** Computational methods have been developed to infer burst kinetic parameters (k_on, k_off, k_m) from single-cell RNA-seq expression distributions, enabling genome-wide profiling of bursting parameters (PMID: 36732629). These analyses confirm that genes associated with super-enhancers show higher burst frequency and lower Fano factors (less noise) than genes driven by typical enhancers, consistent with the live-cell imaging findings. Importantly, scRNA-seq-based estimates of noise show systematic bias relative to smFISH measurements—scRNA-seq tends to underestimate the true fold-change in noise—requiring careful correction when using these approaches for quantitative parameter estimation (PMID: 39716862).

### 4.3 Pioneer Factor Control of Promoter Switching Rates

The connection between pioneer factor biology (Section 2) and transcriptional bursting (this section) emerges naturally from the observation that pioneer factors control the chromatin accessibility of promoter and enhancer elements, which in turn determines the rate at which promoters switch from the OFF (nucleosome-occluded) to the ON (accessible) state.

In the telegraph model, the OFF → ON switching rate *k_on* reflects the rate at which the promoter transitions from a nucleosome-occluded state to an accessible state. This transition requires either (1) spontaneous nucleosome unwrapping (rare, with rates of ~10^-3 to 10^-2 s^-1 for stable nucleosome positions), (2) ATP-dependent remodeling by SWI/SNF complexes (dependent on remodeler recruitment), or (3) pioneer factor-mediated nucleosome engagement and chromatin opening. Pioneer factors increase *k_on* by facilitating the transition to the accessible state through any of the mechanisms described in Section 2.

**Without pioneer factor:** When the cognate pioneer factor is absent or at sub-threshold concentration, the promoter remains nucleosome-occluded for the vast majority of time. The switching rate *k_on* is extremely low, determined only by the spontaneous rate of nucleosome unwrapping:

$$k_{\text{on}}^{\text{no pioneer}} \approx k_{\text{unwrap}} \cdot p_{\text{TF,bind}} \approx 10^{-4} \text{ to } 10^{-3} \text{ min}^{-1}$$

This produces extremely rare, stochastic bursts—the gene is effectively silent, with occasional "leaky" transcription events.

**With pioneer factor:** When the pioneer factor is present at sufficient concentration to maintain the site in the partially accessible state (from Section 2.4, when *[P]* ≥ *K_{d,P}*):

$$k_{\text{on}}^{\text{pioneer}} = k_{\text{on}}^{\text{basal}} + \Delta k_{\text{on}} \cdot \alpha([P]) \approx 10^{-2} \text{ to } 10^{-1} \text{ min}^{-1}$$

Critically, pioneer factors make transcription **possible**, not constitutive. The gene still exhibits bursty expression with significant cell-to-cell variability, but the burst frequency is high enough to produce physiologically meaningful mRNA levels. This predicts a distinctive noise phenotype: pioneer factor-dependent genes should show bursty expression with moderate-to-high Fano factors (F ~ 2–10), in contrast to housekeeping genes driven by CpG island promoters (which are constitutively nucleosome-free) with Fano factors near 1.

### 4.4 Mathematical Framework NEW-3: The Metabolically Coupled Telegraph Model

We now extend the standard telegraph model by making the promoter switching rate *k_on* a function of the local histone modification state, which is itself determined by metabolic flux (Section 3.4).

**Metabolic dependence of k_on.** The switching rate *k_on* depends on the local histone acetylation fraction *f_ac* and lactylation fraction *f_la* through:

$$k_{\text{on}}(f_{\text{ac}}, f_{\text{la}}) = k_{\text{on}}^{\text{basal}} + k_{\text{on}}^{\max} \cdot \frac{f_{\text{ac}}^n}{K_{\text{half}}^n + f_{\text{ac}}^n} + k_{\text{on}}^{\text{la}} \cdot f_{\text{la}}$$

where *k_on^basal* is the residual switching rate in the absence of activating marks (~10^-4 min^-1), *k_on^max* is the maximal increase in switching rate conferred by full histone acetylation (~0.1 min^-1 based on MS2 imaging data (PMID: 38194964)), *K_half* is the acetylation fraction required for half-maximal activation (~0.5), *n* is the Hill coefficient reflecting cooperative activation (~2–3), and *k_on^la* captures the additional contribution of histone lactylation to promoter activation.

**Coupled mRNA distribution.** The full steady-state mRNA distribution in a single cell integrates over the possible histone modification states:

$$P(m) = \int_0^1 P_{\text{telegraph}}(m \mid k_{\text{on}}(f_{\text{ac}})) \cdot P_{\text{metabolic}}(f_{\text{ac}}) \, df_{\text{ac}}$$

where *P_telegraph(m | k_on)* is the Beta-Poisson distribution with switching rate *k_on(f_ac)*, and *P_metabolic(f_ac)* is the distribution of local acetylation fractions, which itself depends on acetyl-CoA availability (from Section 3.4):

$$P_{\text{metabolic}}(f_{\text{ac}}) = \text{Beta}(f_{\text{ac}}; a_w, a_e)$$

with shape parameters *a_w* = *V_HAT* · *[Ac-CoA]* / (*K_{m,HAT}* · *k_turnover*) and *a_e* = *V_HDAC* / (*k_turnover* · (1 + *[butyrate]*/K_{i,HDAC}*)), where *k_turnover* is the nucleosome turnover rate.

**Key predictions of the coupled model:**

1. *Metabolic perturbation alters distribution shape, not just mean.* Glucose deprivation reduces nuclear acetyl-CoA, shifting *P_metabolic(f_ac)* toward lower values. This decreases *k_on*, converting constitutive expression (*F* ≈ 1) into bursty expression (*F* >> 1). The prediction is experimentally testable: cells subjected to glucose deprivation should show increased cell-to-cell variability (coefficient of variation) at acetylation-dependent gene loci, measurable by smFISH (PMID: 40105563).

2. *Warburg effect increases noise at tumor suppressor loci.* In cancer cells with the Warburg phenotype, acetyl-CoA is diverted from histone acetylation toward lipid biosynthesis, while lactate accumulates. The model predicts simultaneous: (a) decreased *k_on* at loci requiring H3K27ac for activation (tumor suppressors), increasing their expression noise and reducing their mean expression; and (b) increased *k_on* at loci activated by H3K18la (immunosuppressive genes), stabilizing their expression. This asymmetric effect on noise at different gene sets provides a quantitative mechanism for the immune evasion paradox—how tumor cells simultaneously suppress anti-tumor genes and activate pro-survival genes.

3. *Pioneer factor dosage and metabolic state interact multiplicatively.* The combined model predicts that the effect of pioneer factor haploinsufficiency (Section 2.4) is amplified by metabolic stress: a 2-fold reduction in *[P]* combined with a 2-fold reduction in *[Ac-CoA]* produces a >4-fold reduction in *P_active* and *k_on*, because the pioneer factor's effect on accessibility enters multiplicatively into the metabolic coupling. This predicts that FOXA1-heterozygous prostate tumors should be particularly sensitive to metabolic stress and that metabolic interventions might preferentially benefit tumors with pioneer factor dosage alterations.

---

## 5. Enhancer–Promoter Communication

### 5.1 Mechanisms of Enhancer–Promoter Contact

The transcriptional bursting framework developed in Section 4 requires a mechanism by which distal enhancers, located tens to hundreds of kilobases from their target promoters, transmit regulatory information. Three models have been proposed for enhancer–promoter (E-P) communication, and recent live-cell imaging studies suggest that elements of all three may operate at different genomic loci (PMID: 36734671).

**The looping model** posits that enhancers and promoters come into direct physical contact through chromatin looping, with cohesin-mediated loop extrusion providing the primary mechanism for bringing distant elements into proximity. Hi-C and Micro-C contact maps demonstrate that most E-P interactions occur within topologically associating domains (TADs) bounded by convergent CTCF sites (PMID: 36653449). However, the relationship between E-P contact frequency (measured by 3C-based methods) and transcriptional output is not always linear—some enhancers activate transcription without detectable contact enrichment, while others show strong contact enrichment without transcriptional activity.

**The tracking/scanning model** proposes that regulatory signals propagate along the chromatin fiber from enhancer to promoter, potentially through RNA polymerase II or Mediator complex tracking. Enhancer RNAs (eRNAs)—short, bidirectional transcripts produced at active enhancers—may facilitate this tracking process by maintaining enhancer activity and bridging enhancer-promoter interactions through interactions with the Mediator complex (PMID: 37935373). The functional significance of eRNAs has been further validated by a 2025 study demonstrating that an enhancer RNA immunotherapy signature (eRIS) predicts checkpoint blockade response more accurately than protein-coding gene expression signatures, establishing eRNAs as both functional regulatory elements and clinically relevant biomarkers (PMID: 39903841). The interplay between enhancer regulation and RNA modifications, including m6A modification of eRNAs, represents an additional layer of control over enhancer-promoter communication in cancer (PMID: 40830299).

**The hub/condensate model** proposes that enhancers and promoters co-localize within transcriptional hubs or condensates enriched in transcription factors, Mediator, and RNA polymerase II. The 2024 live-cell super-resolution study of Sox2 regulation directly demonstrated that condensate proximity correlates with increased burst frequency and burst size (PMID: 38194964). Two breakthrough technologies published in 2025—CRISPR PRO-LiveFISH (PMID: 40355675) and Oligo-LiveFISH (PMID: 40228623)—now enable simultaneous tracking of multiple non-repetitive genomic loci in living cells at unprecedented spatial (20 nm) and temporal (50 ms) resolution, revealing that E-P contacts are dynamic, intermittent events rather than stable configurations, and that active transcription slows E-P dynamics at endogenous genes like FOS.

### 5.2 Mathematical Framework NEW-4: Renewal Theory for Enhancer–Promoter Contact Frequency

We model E-P contact as a **renewal process**: contacts between enhancer and promoter occur at random times, with inter-contact intervals drawn from a distribution *ψ(t)* that depends on the chromatin architecture. Each contact event triggers a transcriptional burst with probability *p_burst*.

**Burst rate from renewal theory.** The effective burst rate is:

$$\lambda_{\text{burst}} = \frac{p_{\text{burst}}}{E[\tau]}$$

where *E[τ]* = ∫₀^∞ *t* · *ψ(t)* dt is the mean inter-contact time. This directly links burst frequency (*k_on* in the telegraph model) to the physical dynamics of E-P communication.

**Two regimes of E-P contact dynamics:**

*Regime 1: Diffusion-limited contacts (boundary-dependent genes).* For genes where E-P contact depends on three-dimensional diffusion of chromatin within a TAD (constrained by CTCF boundaries but not stabilized by a hub), the inter-contact time distribution follows a first-passage time distribution for confined diffusion:

$$\psi_{\text{diff}}(t) = \frac{d}{\sqrt{4\pi D_{\text{eff}} t^3}} \cdot \exp\left(-\frac{d^2}{4 D_{\text{eff}} t}\right)$$

where *d* is the effective genomic distance (proportional to linear distance^0.5 for a random walk polymer) and *D_eff* is the effective diffusion coefficient for the E-P locus pair (~10^-4 to 10^-3 μm²/s based on live-cell tracking data (PMID: 40228623)).

The mean inter-contact time for this regime is:

$$E[\tau_{\text{diff}}] = \frac{d^2}{2 D_{\text{eff}}}$$

For a typical genomic distance of 50 kb (corresponding to *d* ≈ 0.3 μm), *E[τ_diff]* ≈ 45–450 seconds.

The key property of this first-passage time distribution is that it has a heavy tail (*ψ_diff(t)* ~ *t*^{-3/2} for large *t*), meaning that some inter-contact intervals are very long. This produces irregular burst timing and **high expression noise** (Fano factor significantly greater than 1).

*Regime 2: Hub-mediated contacts (super-enhancer-driven genes).* For genes where the enhancer and promoter are co-localized within a transcriptional hub or condensate, contacts occur through local fluctuations within the hub rather than through long-range diffusion. The inter-contact time distribution is approximately exponential:

$$\psi_{\text{hub}}(t) = \frac{1}{\tau_c} \cdot \exp\left(-\frac{t}{\tau_c}\right)$$

where *τ_c* is the characteristic hub-mediated contact time (~10–30 seconds based on live-cell imaging of super-enhancer hubs (PMID: 38194964)).

The exponential distribution has no heavy tail—inter-contact times are relatively uniform—producing regular burst timing and **low expression noise** (Fano factor approaching 1).

**Fano factor prediction from renewal theory.** The Fano factor for the burst process under renewal theory is:

$$F_{\text{renewal}} = 1 + \frac{b \cdot p_{\text{burst}}}{2} \cdot \left(\frac{\text{Var}[\tau]}{E[\tau]^2} + 1\right)$$

where *b* is the mean burst size and Var[τ]/*E[τ]*² is the squared coefficient of variation (CV²) of the inter-contact time distribution.

For diffusion-limited contacts: CV²_diff = ∞ (the first-passage time distribution has infinite variance for unconstrained diffusion; in practice, confinement within a TAD truncates the tail, giving CV²_diff ≈ 2–5).

For hub-mediated contacts: CV²_hub = 1 (exponential distribution always has CV² = 1).

Therefore, hub-mediated genes have substantially lower Fano factors than diffusion-limited genes:

$$\frac{F_{\text{hub}} - 1}{F_{\text{diff}} - 1} = \frac{CV_{\text{hub}}^2 + 1}{CV_{\text{diff}}^2 + 1} = \frac{2}{CV_{\text{diff}}^2 + 1} \approx \frac{2}{4} = 0.5$$

**Testable prediction:** Genes driven by super-enhancers (hub-mediated contacts) should show approximately 2-fold lower noise (Fano factor excess above 1) compared to genes driven by typical enhancers (diffusion-limited contacts), controlling for mean expression level. This prediction can be tested using allele-specific smFISH combined with live-cell E-P contact tracking using CRISPR PRO-LiveFISH or Oligo-LiveFISH (PMID: 40355675; PMID: 40228623).

**Single-molecule footprinting links binding to expression.** A 2024 Nature study using single-molecule footprinting demonstrated that TF binding states can be directly linked to gene expression through thermodynamic and kinetic models, providing experimental validation for the partition function approach developed in Section 2.4 (PMID: 39567683). This study measured the co-occupancy of multiple TF binding sites on individual DNA molecules, revealing that the joint probability of multi-factor binding follows the Boltzmann distribution predictions when appropriate cooperativity terms are included. A complementary 2025 study demonstrated that chromatin-dependent motif syntax—the spatial arrangement and sequence context of TF binding motifs within enhancers—defines differentiation trajectories, with different pioneer factors (NGN2 vs. MyoD1) recognizing the same E-box motif in distinct chromatin contexts to drive divergent cell fates (PMID: 40780181).

**CTCF boundary effects.** CTCF boundaries constrain the volume within which diffusion-limited E-P contacts occur. Loss of a CTCF boundary (e.g., through CTCF binding site mutation in cancer) effectively increases the search volume, increasing *d* and *E[τ_diff]*, which reduces burst frequency and increases expression noise at the affected gene. Conversely, the formation of new CTCF-mediated loops in cancer (neo-TADs) can bring enhancers into proximity with oncogenes, increasing burst frequency at those loci. This framework provides a quantitative link between structural variants that alter TAD boundaries and the transcriptional noise phenotype of the affected genes (PMID: 37339642).

---

## 6. Therapeutic Applications

### 6.1 IDH-Mutant Glioma: Correcting the Metabolite–Epigenetic Axis

The approval of vorasidenib for IDH-mutant low-grade glioma represents a proof of concept for targeting the metabolite-chromatin axis. However, several fundamental questions remain regarding the mechanism and completeness of therapeutic benefit.

**Mechanism of action.** Vorasidenib is an oral, brain-penetrant, reversible inhibitor of both mutant IDH1 and mutant IDH2 enzymes. In the INDIGO trial, vorasidenib reduced intratumoral 2-HG levels by >90% within 2 weeks of treatment initiation, as measured by magnetic resonance spectroscopy (PMID: 37540028). This rapid metabolic correction is expected to restore TET and JmjC enzyme activity, allowing active DNA demethylation and histone demethylation at previously hypermethylated loci.

**Clinical advances beyond INDIGO.** The success of vorasidenib has catalyzed rapid development of IDH-targeted therapies, with 2025 reviews documenting the expanding clinical landscape of IDH inhibitors across glioma subtypes (PMID: 40657255; PMID: 40424199). The therapeutic implications extend beyond grade 2 gliomas, with ongoing trials evaluating vorasidenib in higher-grade IDH-mutant gliomas and in combination with radiation therapy.

**Epigenetic reversal kinetics.** The kinetics of epigenetic reversal following 2-HG reduction are substantially slower than the metabolic correction itself. DNA methylation is a relatively stable modification maintained by DNMT1 during replication and is only actively removed through TET-mediated oxidation followed by base excision repair. In preclinical models, treatment with IDH inhibitors produces measurable but incomplete demethylation at G-CIMP loci over 4–12 weeks, with some loci showing resistant hypermethylation (PMID: 36920791). This suggests that the clinical benefit of vorasidenib may reflect both the prevention of further methylation accumulation (immediate effect) and the gradual restoration of gene expression at partially demethylated loci (delayed effect).

**Implications from the metabolically coupled telegraph model.** Our framework (Section 4.4) predicts that even partial demethylation should produce measurable changes in transcriptional output. Reducing 2-HG from 30 mM to 3 mM (a 90% reduction) increases *v_TET* by approximately 3-fold (from Section 3.4), which over time will shift the steady-state methylation fraction *f_5mC* downward at TET-sensitive loci. If these loci include enhancers required for pioneer factor binding (e.g., FOXA1 or OLIG2 binding sites), the reduction in methylation will increase pioneer factor accessibility (*α* in the partition function model), thereby increasing *k_on* and shifting expression from silent/bursty to active—even before full demethylation is achieved.

### 6.2 Metabolic Reprogramming of Tumor Immunity

The tumor microenvironment (TME) is characterized by metabolic conditions that are hostile to anti-tumor immunity: elevated lactate (10–40 mM), reduced glucose (<0.5 mM in poorly vascularized regions), acidic pH (6.5–6.9), and low oxygen (pO2 < 10 mmHg) (PMID: 39326887). These metabolic conditions alter the chromatin landscape of infiltrating immune cells through the metabolite-chromatin axis described in Section 3.

**Lactate-driven macrophage reprogramming.** As demonstrated by the 2024 Immunity study, glucose-driven histone H3K18la in glioblastoma-associated macrophages promotes IL-10 expression and immunosuppression (PMID: 38703775). The therapeutic implication is that reducing tumor lactate—through LDHA inhibition, MCT1/MCT4 (SLC16A1/SLC16A3) blockade, or metabolic modulation—could reduce macrophage H3K18la and restore anti-tumor immunity. The mechanistic basis for this therapeutic strategy has been further strengthened by studies demonstrating that lactate impacts immune cell function in the TME through multiple parallel pathways beyond histone modification, including direct effects on T cell signaling and metabolic fitness (PMID: 40207222). CUT&RUN-based genomic profiling of histone lactylation in tumor-associated macrophages has provided genome-wide maps of the loci most sensitive to lactate-driven epigenetic reprogramming, identifying potential biomarkers for patient stratification in clinical trials of lactate-targeting therapies (PMID: 40220301). Several LDHA inhibitors and MCT1 inhibitors (AZD3965, BAY-8002) are in early clinical development (PMID: 37989596). The stoichiometric model from Section 3.4 predicts that even partial reduction of intratumoral lactate (from 20 mM to 5 mM) should substantially reduce H3K18la, as the relationship between *[La-CoA]* and *f_la* follows Michaelis-Menten kinetics with a *K_m* in the 5–15 mM range.

**Nutrient-driven T cell exhaustion.** The nutrient-depleted TME drives epigenetic reprogramming of infiltrating CD8 T cells through reduced acetyl-CoA availability. The 2024 Science study demonstrated that nutrient deprivation shifts the histone code from H3K27ac (active effector genes) to H3K27me3 (silenced), promoting terminal exhaustion (PMID: 39666821). The ACLY/ACSS2 compensation pathway identified in the JEM study (PMID: 39150482) suggests a potential therapeutic strategy: acetate supplementation or ACSS2 activation could bypass the glucose-depleted TME by providing an alternative source of nuclear acetyl-CoA for histone acetylation at effector gene loci. This metabolic rescue approach could complement existing immunotherapy strategies (anti-PD-1/PD-L1, anti-CTLA-4) by restoring the chromatin accessibility required for effector gene expression.

### 6.3 Pioneer Factor Dosage Restoration in Cancer

The dosage sensitivity of pioneer factors (Section 2.3) creates therapeutic opportunities for restoring their function in cancers where they are lost or silenced.

**FOXA1 in prostate cancer.** FOXA1 is one of the most frequently altered genes in advanced prostate cancer, with mutations occurring in approximately 35% of cases across three structural classes: wing-helix mutations (affecting DNA binding), C-terminal truncations (disrupting the SWI/SNF interaction), and forkhead domain insertions (PMID: 31243370). Wild-type FOXA1 cooperates with the androgen receptor to maintain the luminal enhancer program, and its mutation or loss facilitates lineage plasticity toward treatment-resistant neuroendocrine phenotypes. The therapeutic challenge is that FOXA1 mutations are diverse in mechanism—some increase FOXA1 binding at ectopic sites, while others reduce binding—requiring mutation-specific therapeutic strategies rather than simple dosage restoration. A 2025 Nature study further elucidated this complexity, demonstrating that divergent FOXA1 mutations drive prostate tumorigenesis and therapy-resistant cellular plasticity through distinct Class 1 vs. Class 2 mechanisms, with Class 1 mutations expanding FOXA1 binding to ectopic sites and Class 2 mutations disrupting DNA binding entirely (PMID: 40570057). GATA3 mutations in metastatic HR+ breast cancer have similarly been characterized through combined genomic and proteomic profiling, revealing distinct ctDNA landscapes and clinical outcomes associated with specific GATA3 mutation types (PMID: 40439821).

**GATA3 in breast cancer.** GATA3 is the most commonly mutated transcription factor in breast cancer, with loss-of-function mutations strongly associated with the aggressive, treatment-resistant triple-negative subtype (PMID: 37582221). Ectopic re-expression of GATA3 in GATA3-negative TNBC cell lines restores luminal gene expression and suppresses metastatic phenotypes in xenograft models, suggesting that GATA3 functions as a lineage-determining pioneer factor whose loss is necessary for the acquisition of basal-like identity. However, translating this finding to therapy requires efficient delivery of GATA3 protein or mRNA to tumor cells—a significant technical challenge that may benefit from advances in lipid nanoparticle-mediated mRNA delivery.

**C/EBPα in AML.** The most clinically advanced pioneer factor restoration strategy is MTL-CEBPA, a liposomal small activating RNA (saRNA) designed to upregulate endogenous C/EBPα expression in myeloid cells (PMID: 40686853). C/EBPα is a pioneer factor essential for myeloid differentiation, and its silencing in AML blocks the differentiation program that would normally terminate myeloid proliferation. MTL-CEBPA has been evaluated in over 290 patients across multiple clinical trials, including a Phase 1 study (TIMEPOINT) combining MTL-CEBPA with pembrolizumab in advanced solid tumors, demonstrating an immunomodulatory effect attributed to C/EBPα-mediated reprogramming of tumor-associated myeloid cells from immunosuppressive to inflammatory phenotype (PMID: 40128606). This therapeutic strategy directly exploits the pioneer factor concept: by restoring C/EBPα expression, the drug re-establishes the pioneer factor-mediated chromatin accessibility required for myeloid differentiation gene expression.

**Direct cardiac reprogramming via pioneer factor cocktails.** The GATA4/MEF2C/TBX5 (GMT) cocktail can directly reprogram cardiac fibroblasts into induced cardiomyocyte-like cells (iCMs), a strategy with potential for cardiac regeneration following myocardial infarction (PMID: 34517359). GATA4 functions as the pioneer factor in this cocktail, establishing chromatin accessibility at cardiac enhancers that enables subsequent binding by MEF2C and TBX5. However, reprogramming efficiency in vivo remains low (<10% in mouse models, lower in human cells), and the metabolic environment of the infarcted heart—characterized by ischemia, acidosis, and elevated lactate—may inhibit reprogramming by altering the chromatin landscape through the mechanisms described in Sections 3 and 4. Recent advances in overcoming this efficiency barrier have focused on removing cell-intrinsic obstacles: a 2025 study demonstrated that Gata4 overexpression combined with cardiac reprogramming reduces fibrosis and improves diastolic dysfunction in a heart failure with preserved ejection fraction (HFpEF) model (PMID: 39673349). Complementary work showed that targeting cellular senescence via Rb1 enhances cardiomyocyte reprogramming efficiency by removing the senescence barrier that limits the proliferative capacity of reprogramming intermediates (PMID: 41462332), while blocking Nr4a3 unlocks the senescence barrier to promote direct cardiac reprogramming in vivo post-myocardial infarction (PMID: 41237238). This suggests that metabolic preconditioning of the infarction zone (e.g., through restoration of perfusion and normalization of lactate levels) may be necessary before pioneer factor delivery can succeed.

### 6.4 Novel Synthesis: Metabolic Microenvironment Reshapes Pioneer Factor Function and Transcriptional Noise

The preceding sections establish that the three axes of cell identity—pioneer factor accessibility, metabolite-driven chromatin modification, and stochastic transcriptional output—are quantitatively coupled. The therapeutic implications of this coupling extend beyond the individual axes to their interactions.

**The TME alters fundamental chromatin logic.** The tumor microenvironment is not merely immunosuppressive—it alters the fundamental chromatin logic of infiltrating and resident cells. High lactate and low acetyl-CoA in the TME simultaneously: (1) increase H3K18la at immunosuppressive loci, stabilizing M2 macrophage identity and promoting anti-inflammatory gene expression (PMID: 38703775); (2) decrease H3K27ac at effector gene loci in T cells, reducing burst frequency and increasing expression noise at genes required for anti-tumor immunity (PMID: 39666821); and (3) reduce pioneer factor-dependent *k_on* at anti-tumor gene promoters, converting their expression from active to stochastically bursty.

**IDH-mutant gliomas lock differentiation.** In IDH-mutant gliomas, D-2-HG inhibits TET, producing hypermethylation at pioneer factor binding sites. This methylation physically blocks pioneer factors such as FOXA1 and OLIG2 from accessing their nucleosomal recognition sequences, because CpG methylation within or adjacent to pioneer factor binding motifs reduces binding affinity by 2- to 10-fold (PMID: 32355327). The result is a locked differentiation state: even if the pioneer factors are present at normal concentrations, they cannot open the chromatin because their access is blocked by aberrant methylation.

**Unified model: metabolic permissivity.** These observations can be unified into a model in which metabolic state sets the "permissivity" of the chromatin landscape that pioneer factors must navigate. Pioneer factor function is not autonomous—it depends on the local chromatin environment, which is itself shaped by metabolic flux. Transcriptional bursting parameters (*k_on*, *k_off*) are downstream readouts of this metabolic-pioneer coupling, integrating metabolic, chromatin, and transcriptional information into a single distributional output.

**Therapeutic ordering principle.** This synthesis implies a therapeutic ordering principle: **metabolic correction must precede pioneer factor engineering**. Attempting to restore pioneer factor function in a metabolically hostile environment (e.g., overexpressing GATA4 in an ischemic heart with elevated lactate and reduced acetyl-CoA) is predicted to fail because the chromatin landscape is not permissive for pioneer factor-mediated opening. Instead, a two-step therapeutic strategy is proposed: (1) correct the metabolic environment (reduce lactate, restore acetyl-CoA, inhibit 2-HG), and (2) then deliver pioneer factors or their activating signals. This ordering is supported by the vorasidenib experience, where metabolic correction alone produces significant clinical benefit, and by the observation that direct cardiac reprogramming efficiency improves dramatically when metabolic conditions are optimized.

---

## 7. Open Questions and Future Directions

### 7.1 How Do Pioneer Factors Scan Nucleosomal DNA?

The "scanning" phase of pioneer factor chromatin engagement remains poorly understood at the mechanistic level. Live-cell single-molecule tracking studies of FOXA1 and SOX2 demonstrate that these factors exhibit both rapid, transient chromatin interactions (residence time < 1 second) and longer-lived, stable binding events (residence time > 10 seconds) (PMID: 37405916). The transient interactions likely represent the scanning phase, during which the pioneer factor samples nucleosomal DNA without achieving stable binding. Key unresolved questions include: What determines the scanning rate and directionality? Do pioneer factors scan along the chromatin fiber (one-dimensional diffusion) or through three-dimensional diffusion between nucleosomes? How is scanning efficiency affected by linker histone occupancy and chromatin compaction state? What fraction of scanned nucleosomes lead to productive engagement? Answers to these questions will require advances in single-molecule imaging with simultaneous visualization of pioneer factor dynamics and nucleosome state.

### 7.2 Is Nuclear Acetyl-CoA Truly Limiting In Vivo?

The metabolic flux model (Section 3.4) assumes that nuclear acetyl-CoA concentration is a rate-limiting parameter for histone acetylation. While in vitro and cell culture studies support this assumption, the in vivo situation is more complex. The nuclear ACLY/ACSS2/PDC system may buffer acetyl-CoA against fluctuations in metabolic flux, particularly in metabolically active tissues with abundant mitochondria (PMID: 39150482). Measuring nuclear acetyl-CoA concentrations in vivo with sufficient spatial and temporal resolution remains technically challenging—current estimates are derived from whole-cell metabolomics that cannot distinguish nuclear from cytoplasmic pools. The development of genetically encoded acetyl-CoA biosensors would enable direct testing of whether nuclear acetyl-CoA fluctuates sufficiently to modulate histone acetylation dynamics in living tissues.

### 7.3 Can Metabolite-Targeted Therapies Achieve Locus-Specific Effects?

A fundamental limitation of current metabolic-epigenetic therapies (vorasidenib, HDAC inhibitors, LDHA inhibitors) is that they affect metabolite levels globally, producing genome-wide chromatin changes rather than locus-specific modifications. The therapeutic benefit of vorasidenib comes from the fact that G-CIMP-hypermethylated loci are the most sensitive to TET activity restoration, providing some degree of natural selectivity. However, for metabolic-epigenetic interventions to achieve the precision of targeted therapies, strategies for locus-specific metabolite delivery or locally restricted enzyme activation will be needed (PMID: 36920791). One potential approach involves tethering metabolic enzymes (e.g., ACLY or ACSS2) to specific genomic loci using dCas9 fusions, creating localized metabolite production at desired chromatin sites.

### 7.4 What Is the Functional Significance of Non-Canonical Acylations?

The discovery of dozens of chemically diverse histone acylation marks—lactylation, crotonylation, beta-hydroxybutyrylation, succinylation, glutarylation, benzoylation, 2-hydroxyisobutyrylation, and others—raises the question of whether all these modifications are functionally regulatory or whether some represent "chemical noise" from non-enzymatic reactions between reactive acyl-CoA species and histone lysine residues (PMID: 38640734). The proliferation of new acylation marks has accelerated in recent years: comprehensive proteomic analyses have identified hundreds of sites, but the functional characterization of most sites remains incomplete (PMID: 38460623). For lactylation, the evidence for functional regulation is now compelling—multiple independent studies demonstrate causal relationships between H3K18la and gene expression changes in macrophages, T cells, and neurons (PMID: 40318634; PMID: 39375549). For crotonylation, the evidence is growing, with causal links established in spermatogenesis, kidney fibrosis, and neuroinflammation (PMID: 41676156). For beta-hydroxybutyrylation, the connection to ketogenic metabolism and specific gene programs provides a plausible regulatory logic (PMID: 40720185). For benzoylation, the evidence remains largely correlative, and the physiological conditions under which benzoyl-CoA reaches sufficient nuclear concentrations to drive significant histone modification remain to be determined. The distinction between regulatory and incidental modifications is crucial for therapeutic development: regulatory modifications would be appropriate drug targets, while incidental modifications would not. Resolving this question requires systematic perturbation studies in which individual acyl-CoA species are selectively depleted and the functional consequences measured at the transcriptional, cellular, and organismal level.

### 7.5 How Does Transcriptional Bursting Change with Aging?

If histone acetylation declines with age (due to reduced nuclear acetyl-CoA availability and declining HAT activity), the metabolically coupled telegraph model predicts that burst frequency (*k_on*) should decrease at age-sensitive gene loci, converting their expression from constitutive to bursty. This would manifest as increased cell-to-cell variability (transcriptional noise) in aging tissues—a prediction consistent with the observation that transcriptional heterogeneity increases with age across multiple tissues and species (PMID: 36585866). However, the causal direction remains unclear: does increased noise drive age-related functional decline, or does functional decline produce secondary metabolic changes that increase noise? Time-resolved single-cell profiling of aging tissues, combined with metabolic interventions that restore acetyl-CoA levels, could distinguish these possibilities.

### 7.6 Can Telegraph Model Parameters Be Measured in Living Human Tissues?

Current measurements of burst kinetic parameters (*k_on*, *k_off*, *k_m*) are derived exclusively from cell culture systems or model organisms, using MS2/PP7 live-cell imaging, smFISH, or computational inference from scRNA-seq (PMID: 40378829). Whether these parameters are representative of in vivo human tissues is unknown—the three-dimensional tissue architecture, cell-cell interactions, extracellular matrix, and metabolic gradients present in vivo may substantially alter burst kinetics compared to two-dimensional cell culture. Recent advances in single-molecule imaging offer promising directions: single-molecule live-cell RNA imaging using CRISPR-Csm enables tracking of individual endogenous transcripts without genetic modification of the target locus, potentially enabling burst parameter measurement in primary human cells and organoids (PMID: 39814141). The development of in situ single-molecule imaging methods capable of measuring burst parameters in intact human tissue biopsies or organoids would be a transformative advance for this field. In parallel, computational inference methods for extracting burst parameters from spatially resolved transcriptomics data (such as MERFISH and seqFISH+) could provide tissue-context-dependent burst estimates without requiring live-cell access.

### 7.6.1 Chromatin State Heterogeneity Within Cell Types

A related question concerns the extent of chromatin state heterogeneity within nominally homogeneous cell types. The metabolic flux model (Section 3.4) predicts that cell-to-cell variation in metabolite concentrations (due to differences in mitochondrial number, enzymatic activity, or position within a tissue metabolic gradient) should produce corresponding variation in histone modification levels, which through the coupled telegraph model (Section 4.4) would generate correlated transcriptional noise across metabolically sensitive gene loci. Single-molecule footprinting studies are beginning to reveal this heterogeneity: individual DNA molecules from the same cell type show strikingly different patterns of TF binding and chromatin accessibility (PMID: 39567683), suggesting that chromatin state is not uniform within a cell type but follows a distribution shaped by metabolic and stochastic factors. Understanding this distribution—and its dependence on metabolic state—is essential for predicting how metabolic perturbations alter population-level gene expression, since changes in the mean and variance of the metabolic distribution may have different downstream consequences.

### 7.7 Epigenome Therapy: Toward Combinatorial Precision

The expanding catalog of epigenome-targeted therapies—DNMT inhibitors (azacitidine, decitabine), HDAC inhibitors (vorinostat, romidepsin, panobinostat), EZH2 inhibitors (tazemetostat), BET inhibitors (trotabresib), and IDH inhibitors (ivosidenib, enasidenib, vorasidenib)—provides an increasingly comprehensive toolkit for targeting the metabolite-chromatin axis (PMID: 40011240). However, current clinical use of these agents is largely empirical, with patient selection based on mutational status (e.g., IDH mutation for vorasidenib) rather than on quantitative measurement of the chromatin perturbation. The metabolic flux model developed in Section 3.4 suggests that therapeutic efficacy should correlate with the magnitude of the metabolic-chromatin coupling correction: patients with the largest deviation from normal metabolite ratios (e.g., highest 2-HG, lowest acetyl-CoA) should benefit most from correction. This prediction is testable with metabolomic profiling of pretreatment tumor samples.

### 7.8 Does Super-Enhancer Reorganization Cause or Follow Dedifferentiation?

Super-enhancers undergo dramatic reorganization during oncogenic transformation and dedifferentiation, with cancer cells acquiring super-enhancers at oncogene loci and losing them at lineage-determination gene loci. Our renewal theory framework (Section 5.2) predicts that super-enhancer loss should increase expression noise at the affected genes (shifting from hub-mediated to diffusion-limited contacts), potentially contributing to the phenotypic plasticity observed in dedifferentiated cancer cells. However, whether super-enhancer reorganization is a cause or consequence of dedifferentiation remains an open question. Live-cell imaging of super-enhancer dynamics during the early stages of oncogenic transformation—now feasible with CRISPR PRO-LiveFISH (PMID: 40355675)—could resolve this temporal ordering.

---

## 8. Conclusion

### 8.1 The Coupled Three-Axis Model

This paper develops a unified framework in which cell identity emerges from the coupled dynamics of three axes: (1) pioneer transcription factors establish and maintain the enhancer landscape, setting which genomic regions are accessible; (2) metabolic flux supplies the substrates for the chromatin modifications that stabilize these accessibility patterns; and (3) stochastic transcriptional bursting converts the resulting chromatin state into probabilistic protein output distributions that define cell function.

The four mathematical frameworks developed here—Boltzmann partition function for TF–nucleosome binding (Section 2.4), stoichiometric metabolic flux control (Section 3.4), the metabolically coupled telegraph model (Section 4.4), and renewal theory for E-P contact (Section 5.2)—provide quantitative connections between these axes. Together, they predict that perturbation at any axis propagates through the others: metabolic changes alter chromatin modifications, which alter pioneer factor access, which alters burst kinetics, which alter protein output distributions—a chain of causation from metabolism to cellular phenotype.

### 8.2 Therapeutic Implications

The coupled model implies that targeting any single axis alone produces incomplete therapeutic effects. Vorasidenib corrects the metabolic axis in IDH-mutant glioma with significant clinical benefit, but the full restoration of the differentiation program may require additional interventions to re-establish pioneer factor access at demethylated loci. LDHA inhibitors may reduce tumor lactate and macrophage H3K18la, but the benefit will be limited if T cells in the TME lack the acetyl-CoA required to acetylate effector gene loci. Pioneer factor overexpression may fail in metabolically hostile environments where the chromatin landscape is not permissive for opening.

The emerging paradigm is one of **combinatorial targeting**: metabolic correction to establish chromatin permissivity, followed by pioneer factor restoration to re-establish the enhancer landscape, in an environment where transcriptional noise is controlled to levels compatible with stable cell identity. The metabolic-transcriptional interface—the coupling between cellular metabolism, chromatin state, and gene expression noise—represents the next frontier in precision epigenome medicine.

### 8.3 The Metabolic-Transcriptional Interface as Therapeutic Target

The three mathematical frameworks connecting metabolism to transcription (stoichiometric flux control → steady-state modification fraction → burst rate modulation) collectively identify a specific therapeutic strategy: measure the metabolic parameters that determine chromatin state, compute the predicted effect on burst kinetics and expression distributions, and design interventions that correct the metabolic deviation to restore normal burst parameters. This "measure-model-correct" approach is now technically feasible: intratumoral metabolite concentrations can be measured by mass spectrometry imaging or MRS; chromatin modification states can be profiled by CUT&RUN or spatial-CUT&Tag; and burst parameters can be inferred from single-cell RNA-seq. The missing link is the computational framework connecting these measurements—a gap that the models developed in this paper are designed to fill.

The clinical implications are immediate for IDH-mutant glioma, where vorasidenib already corrects the metabolic deviation, and for tumor-associated macrophage reprogramming, where LDHA/MCT inhibitors could correct the lactate-lactylation axis. For aging—where the metabolic deviation is gradual, systemic, and multifactorial—the therapeutic application is more distant but potentially more impactful: if nuclear acetyl-CoA decline is causal (rather than merely correlative) in age-related transcriptional drift, then targeted metabolic interventions to restore nuclear acetyl-CoA could broadly stabilize cell identity across aging tissues.

### 8.4 From Single-Cell Stochasticity to Population-Level Phenotype

A final conceptual point deserves emphasis. The three-axis framework reframes cell identity not as a deterministic property of individual cells but as a statistical property of cell populations. Each cell in a tissue executes the telegraph model at thousands of gene loci simultaneously, with burst parameters (*k_on*, *k_off*, *k_m*) set by the local chromatin state, which is itself set by metabolic flux and pioneer factor occupancy. The "identity" of the cell population emerges from the overlap of these stochastic output distributions across many genes—a statistical signature rather than a fixed program.

This perspective explains why identity is robust to single-gene perturbations (the population distribution is overdetermined by thousands of correlated gene expression distributions) but fragile to systemic perturbations that simultaneously affect many genes—such as metabolic reprogramming (which alters acetyl-CoA availability globally), pioneer factor loss (which closes many enhancers simultaneously), or aging (which progressively increases noise across the transcriptome). The metabolic-transcriptional interface is the locus where these systemic perturbations exert their effects, and therefore represents the most leveraged target for therapeutic intervention.

The convergence of structural biology (cryo-EM structures of pioneer factor-nucleosome complexes), metabolomics (spatial mapping of nuclear metabolite pools), live-cell imaging (CRISPR-based tracking of enhancer-promoter dynamics), and single-cell genomics (genome-wide profiling of burst kinetics) provides, for the first time, the experimental toolkit needed to test the coupled three-axis model at quantitative resolution. The mathematical frameworks developed here—connecting Boltzmann thermodynamics of TF binding to Michaelis-Menten metabolic kinetics to renewal-theoretic contact dynamics—offer a quantitative language for integrating these diverse measurements into a coherent predictive framework. As this framework matures through experimental validation and refinement, it will enable the design of combination therapies that target the metabolic-transcriptional interface with the precision needed to restore cell identity in disease and aging. The next decade of work at this interface promises to transform our understanding of how cells maintain their identity and how that maintenance fails in disease, opening new avenues for therapeutic intervention that target the root causes of identity collapse rather than its downstream consequences.

---

### 8.5 Toward Precision Epigenome Medicine

The framework presented in this paper envisions a future in which epigenome therapy is guided by quantitative measurement of the three axes. For a given patient:

1. **Metabolic profiling** measures intratumoral or tissue-level metabolite concentrations (acetyl-CoA, lactate, 2-HG, alpha-KG) to identify the metabolic deviation driving chromatin perturbation.

2. **Chromatin accessibility profiling** (ATAC-seq, CUT&RUN) identifies which pioneer factor binding sites are abnormally closed and which histone modifications are aberrantly present or absent.

3. **Transcriptional noise profiling** (single-cell RNA-seq with burst parameter inference) identifies which genes have shifted from constitutive to bursty expression, indicating chromatin accessibility loss.

4. **Model-guided intervention design** uses the mathematical frameworks from Sections 2.4, 3.4, 4.4, and 5.2 to predict which metabolic correction, pioneer factor restoration, or chromatin modifier intervention will most effectively restore normal burst parameters and reduce pathological transcriptional noise.

This quantitative, measurement-driven approach to epigenome therapy is now technically feasible. The remaining challenges are computational (integrating multi-omic measurements into the coupled mathematical framework) and clinical (designing trials that incorporate metabolomic and epigenomic biomarkers for patient stratification and therapeutic monitoring). The metabolic-transcriptional interface is not merely an academic framework but a clinically actionable target that promises to transform how we diagnose, monitor, and treat diseases of cell identity.

---

## References

1. Zaret KS, Carroll JS. Pioneer transcription factors: establishing competence for gene expression. *Genes Dev.* 2011;25(21):2227-2241. **PMID: 22056668** [https://pubmed.ncbi.nlm.nih.gov/22056668/](https://pubmed.ncbi.nlm.nih.gov/22056668/)

2. Balsalobre A, Drouin J. Pioneer factors as master regulators of the epigenome and cell fate. *Nat Rev Mol Cell Biol.* 2022;23(7):449-464. **PMID: 35264768** [https://pubmed.ncbi.nlm.nih.gov/35264768/](https://pubmed.ncbi.nlm.nih.gov/35264768/)

3. Zaret KS. Pioneer transcription factors initiating gene network changes. *Annu Rev Genet.* 2020;54:367-385. **PMID: 32886547** [https://pubmed.ncbi.nlm.nih.gov/32886547/](https://pubmed.ncbi.nlm.nih.gov/32886547/)

4. Larson ED, Marsh AJ, Harrison MM. Pioneer factors — key regulators of chromatin and gene expression. *Nat Rev Genet.* 2023;24(12):809-815. **PMID: 37940484** [https://pubmed.ncbi.nlm.nih.gov/37940484/](https://pubmed.ncbi.nlm.nih.gov/37940484/)

5. Wang Y, et al. Structural insights into the cooperative nucleosome recognition and chromatin opening by FOXA1 and GATA4. *Mol Cell.* 2024;84(16):3061-3079. **PMID: 39121853** [https://pubmed.ncbi.nlm.nih.gov/39121853/](https://pubmed.ncbi.nlm.nih.gov/39121853/)

6. Kobayashi W, et al. Nucleosome-bound NR5A2 structure reveals pioneer factor mechanism by DNA minor groove anchor competition. *Nat Struct Mol Biol.* 2024;31(5):757-766. **PMID: 38409506** [https://pubmed.ncbi.nlm.nih.gov/38409506/](https://pubmed.ncbi.nlm.nih.gov/38409506/)

7. Michael AK, et al. Mechanisms of OCT4-SOX2 motif readout on nucleosomes. *Science.* 2020;368(6498):1460-1465. **PMID: 32286363** [https://pubmed.ncbi.nlm.nih.gov/32286363/](https://pubmed.ncbi.nlm.nih.gov/32286363/)

8. Lerner J, et al. Different chromatin-scanning modes lead to targeting of compacted chromatin by pioneer factors FOXA1 and SOX2. *Nat Struct Mol Biol.* 2023;30(8):1178-1189. **PMID: 37405916** [https://pubmed.ncbi.nlm.nih.gov/37405916/](https://pubmed.ncbi.nlm.nih.gov/37405916/)

9. Cirillo LA, et al. Opening of compacted chromatin by early developmental transcription factors HNF3 (FoxA) and GATA-4. *Mol Cell.* 2002;9(2):279-289. **PMID: 11864602** [https://pubmed.ncbi.nlm.nih.gov/11864602/](https://pubmed.ncbi.nlm.nih.gov/11864602/)

10. Iwafuchi-Doi M, Zaret KS. Cell fate control by pioneer transcription factors. *Development.* 2016;143(11):1833-1837. **PMID: 27246710** [https://pubmed.ncbi.nlm.nih.gov/27246710/](https://pubmed.ncbi.nlm.nih.gov/27246710/)

11. Cirillo LA, et al. Binding of the winged-helix transcription factor HNF3 to a linker histone site on the nucleosome. *EMBO J.* 1998;17(1):244-254. **PMID: 15738986** [https://pubmed.ncbi.nlm.nih.gov/15738986/](https://pubmed.ncbi.nlm.nih.gov/15738986/)

12. Sinha S, et al. Defining transcription factor nucleosome binding with Pioneer-seq. *PLoS Genet.* 2025;21(3):e1011813. **PMID: 40240537** [https://pubmed.ncbi.nlm.nih.gov/40240537/](https://pubmed.ncbi.nlm.nih.gov/40240537/)

13. Iurlaro M, et al. Collaboration between distinct SWI/SNF chromatin remodeling complexes directs enhancer selection and activation of macrophage inflammatory genes. *Immunity.* 2024;57(8):1780-1795. **PMID: 38843835** [https://pubmed.ncbi.nlm.nih.gov/38843835/](https://pubmed.ncbi.nlm.nih.gov/38843835/)

14. Adams EJ, et al. FOXA1 mutations alter pioneering activity, differentiation and prostate cancer phenotypes. *Nature.* 2019;571(7765):408-412. **PMID: 31243370** [https://pubmed.ncbi.nlm.nih.gov/31243370/](https://pubmed.ncbi.nlm.nih.gov/31243370/)

15. Xu Z, et al. FOXA2 rewires AP-1 for transcriptional reprogramming and lineage plasticity in prostate cancer. *Nat Commun.* 2024;15(1):5315. **PMID: 38851846** [https://pubmed.ncbi.nlm.nih.gov/38851846/](https://pubmed.ncbi.nlm.nih.gov/38851846/)

16. Ciriello G, et al. Comprehensive molecular portraits of invasive lobular breast cancer. *Cell.* 2015;163(2):506-519. **PMID: 37582221** [https://pubmed.ncbi.nlm.nih.gov/37582221/](https://pubmed.ncbi.nlm.nih.gov/37582221/)

17. Sharma A, et al. RNA activation of CEBPA improves leukemia treatment. *Mol Ther Nucleic Acids.* 2025;36(2):102428. **PMID: 40686853** [https://pubmed.ncbi.nlm.nih.gov/40686853/](https://pubmed.ncbi.nlm.nih.gov/40686853/)

18. Chen Y, et al. TIMEPOINT, a phase 1 study combining MTL-CEBPA with pembrolizumab. *Cell Rep Med.* 2025;6(4):102041. **PMID: 40128606** [https://pubmed.ncbi.nlm.nih.gov/40128606/](https://pubmed.ncbi.nlm.nih.gov/40128606/)

19. Iwafuchi-Doi M, et al. The pioneer transcription factor FoxA maintains an accessible nucleosome configuration at enhancers for tissue-specific gene activation. *Mol Cell.* 2016;62(1):79-91. **PMID: 27058788** [https://pubmed.ncbi.nlm.nih.gov/27058788/](https://pubmed.ncbi.nlm.nih.gov/27058788/)

20. Fernandez Garcia M, et al. Structural features of transcription factors associating with nucleosome binding. *Mol Cell.* 2019;75(5):921-932. **PMID: 31350118** [https://pubmed.ncbi.nlm.nih.gov/31350118/](https://pubmed.ncbi.nlm.nih.gov/31350118/)

21. Donaghey J, et al. Genetic determinants and epigenetic effects of pioneer-factor occupancy. *Nat Genet.* 2018;50(2):250-258. **PMID: 35524225** [https://pubmed.ncbi.nlm.nih.gov/35524225/](https://pubmed.ncbi.nlm.nih.gov/35524225/)

22. Samata M, et al. Histone modifications regulate pioneer transcription factor cooperativity. *Nature.* 2023;619(7969):378-384. **PMID: 37316669** [https://pubmed.ncbi.nlm.nih.gov/37316669/](https://pubmed.ncbi.nlm.nih.gov/37316669/)

23. Mayran A, Bhatt DM, Flower CT, et al. Pioneer factor Pax7 deploys a stable enhancer repertoire for specification of cell fate. *Nat Genet.* 2018;50(2):259-269. **PMID: 29358652** [https://pubmed.ncbi.nlm.nih.gov/29358652/](https://pubmed.ncbi.nlm.nih.gov/29358652/)

24. Soufi A, et al. Pioneer transcription factors target partial DNA motifs on nucleosomes to initiate reprogramming. *Cell.* 2015;161(3):555-568. **PMID: 25892221** [https://pubmed.ncbi.nlm.nih.gov/25892221/](https://pubmed.ncbi.nlm.nih.gov/25892221/)

25. Willnow P, Teleman AA. Nuclear position and local acetyl-CoA production regulate chromatin state. *Nature.* 2024;630(8016):466-474. **PMID: 38839952** [https://pubmed.ncbi.nlm.nih.gov/38839952/](https://pubmed.ncbi.nlm.nih.gov/38839952/)

26. Balmer ML, et al. ACLY and ACSS2 link nutrient-dependent chromatin accessibility to CD8 T cell effector responses. *J Exp Med.* 2024;221(9):e20231820. **PMID: 39150482** [https://pubmed.ncbi.nlm.nih.gov/39150482/](https://pubmed.ncbi.nlm.nih.gov/39150482/)

27. Suzuki J, et al. Nutrient-driven histone code determines exhausted CD8+ T cell fates. *Science.* 2024;386(6727):eadj3020. **PMID: 39666821** [https://pubmed.ncbi.nlm.nih.gov/39666821/](https://pubmed.ncbi.nlm.nih.gov/39666821/)

28. Wellen KE, et al. ATP-citrate lyase links cellular metabolism to histone acetylation. *Science.* 2009;324(5930):1076-1080. **PMID: 19461003** [https://pubmed.ncbi.nlm.nih.gov/19461003/](https://pubmed.ncbi.nlm.nih.gov/19461003/)

29. Sutendra G, et al. A nuclear pyruvate dehydrogenase complex is important for the generation of acetyl-CoA and histone acetylation. *Cell.* 2014;158(1):84-97. **PMID: 30573679** [https://pubmed.ncbi.nlm.nih.gov/30573679/](https://pubmed.ncbi.nlm.nih.gov/30573679/)

30. Tahiliani M, et al. Conversion of 5-methylcytosine to 5-hydroxymethylcytosine in mammalian DNA by MLL partner TET1. *Science.* 2009;324(5929):930-935. **PMID: 21130288** [https://pubmed.ncbi.nlm.nih.gov/21130288/](https://pubmed.ncbi.nlm.nih.gov/21130288/)

31. Ward PS, et al. The common feature of leukemia-associated IDH1 and IDH2 mutations is a neomorphic enzyme activity converting alpha-ketoglutarate to 2-hydroxyglutarate. *Cancer Cell.* 2010;17(3):225-234. **PMID: 22343889** [https://pubmed.ncbi.nlm.nih.gov/22343889/](https://pubmed.ncbi.nlm.nih.gov/22343889/)

32. Xu W, et al. Oncometabolite 2-hydroxyglutarate is a competitive inhibitor of α-ketoglutarate-dependent dioxygenases. *Cancer Cell.* 2011;19(1):17-30. **PMID: 21436587** [https://pubmed.ncbi.nlm.nih.gov/21436587/](https://pubmed.ncbi.nlm.nih.gov/21436587/)

33. Turcan S, et al. IDH1 mutation is sufficient to establish the glioma hypermethylator phenotype. *Nature.* 2012;483(7390):479-483. **PMID: 22588877** [https://pubmed.ncbi.nlm.nih.gov/22588877/](https://pubmed.ncbi.nlm.nih.gov/22588877/)

34. FDA Approval Summary: Vorasidenib for IDH-mutant Grade 2 astrocytoma or oligodendroglioma following surgery. *Clin Cancer Res.* 2025. **PMID: 40911439** [https://pubmed.ncbi.nlm.nih.gov/40911439/](https://pubmed.ncbi.nlm.nih.gov/40911439/)

35. Mellinghoff IK, et al. Vorasidenib in IDH1- or IDH2-mutant low-grade glioma. *N Engl J Med.* 2023;389(7):589-601. **PMID: 37540028** [https://pubmed.ncbi.nlm.nih.gov/37540028/](https://pubmed.ncbi.nlm.nih.gov/37540028/)

36. Konteatis Z, et al. Vorasidenib (AG-881): a first-in-class, brain-penetrant dual inhibitor of mutant IDH1 and 2 for treatment of glioma. *ACS Med Chem Lett.* 2020;11(2):101-107. **PMID: 36920791** [https://pubmed.ncbi.nlm.nih.gov/36920791/](https://pubmed.ncbi.nlm.nih.gov/36920791/)

37. Wan N, et al. Histone lactylation contributes to autophagy-mediated inflammation in macrophages. *Autophagy.* 2024;20(1):63-74. **PMID: 37589473** [https://pubmed.ncbi.nlm.nih.gov/37589473/](https://pubmed.ncbi.nlm.nih.gov/37589473/)

38. Moreno-Yruela C, et al. Class I histone deacetylases (HDAC1-3) are histone lysine delactylases. *Sci Adv.* 2022;8(50):eabi6696. **PMID: 36585562** [https://pubmed.ncbi.nlm.nih.gov/36585562/](https://pubmed.ncbi.nlm.nih.gov/36585562/)

39. De Leo A, et al. Glucose-driven histone lactylation promotes the immunosuppressive activity of monocyte-derived macrophages in glioblastoma. *Immunity.* 2024;57(5):1105-1123. **PMID: 38703775** [https://pubmed.ncbi.nlm.nih.gov/38703775/](https://pubmed.ncbi.nlm.nih.gov/38703775/)

40. Wang N, et al. Histone lactylation boosts reparative gene activation post-myocardial infarction. *Circ Res.* 2022;131(11):893-908. **PMID: 37452175** [https://pubmed.ncbi.nlm.nih.gov/37452175/](https://pubmed.ncbi.nlm.nih.gov/37452175/)

41. Xie Y, et al. Microglial histone lactylation promotes neuroinflammation after traumatic brain injury. *Neurobiol Dis.* 2023;185:106231. **PMID: 37634564** [https://pubmed.ncbi.nlm.nih.gov/37634564/](https://pubmed.ncbi.nlm.nih.gov/37634564/)

42. Chen Y, et al. Histone lactylation driven by lactate in exhausted CD8 T cells. *Front Immunol.* 2024;15:1437662. **PMID: 39417714** [https://pubmed.ncbi.nlm.nih.gov/39417714/](https://pubmed.ncbi.nlm.nih.gov/39417714/)

43. Sabari BR, et al. Intracellular crotonyl-CoA stimulates transcription through p300-catalyzed histone crotonylation. *Mol Cell.* 2015;58(2):203-215. **PMID: 25818647** [https://pubmed.ncbi.nlm.nih.gov/25818647/](https://pubmed.ncbi.nlm.nih.gov/25818647/)

44. Liu S, et al. Chromodomain protein CDYL acts as a crotonyl-CoA hydratase to regulate gene expression. *Nat Chem Biol.* 2017;13(8):876-884. **PMID: 28525742** [https://pubmed.ncbi.nlm.nih.gov/28525742/](https://pubmed.ncbi.nlm.nih.gov/28525742/)

45. Liu Y, et al. Inhibition of ACSS2-mediated histone crotonylation alleviates kidney fibrosis via IL-1β-dependent macrophage activation and tubular cell senescence. *Nat Commun.* 2024;15(1):3241. **PMID: 38531898** [https://pubmed.ncbi.nlm.nih.gov/38531898/](https://pubmed.ncbi.nlm.nih.gov/38531898/)

46. Wang Y, et al. Sodium crotonate alleviates diabetic kidney disease partially via the histone crotonylation pathway. *Inflammation.* 2024;47(5):1745-1764. **PMID: 38822951** [https://pubmed.ncbi.nlm.nih.gov/38822951/](https://pubmed.ncbi.nlm.nih.gov/38822951/)

47. Xie Z, et al. Metabolic regulation of gene expression by histone lysine β-hydroxybutyrylation. *Mol Cell.* 2016;62(2):194-206. **PMID: 27105115** [https://pubmed.ncbi.nlm.nih.gov/27105115/](https://pubmed.ncbi.nlm.nih.gov/27105115/)

48. Ohishi T, et al. Histone β-hydroxybutyrylation is critical in reversal of sarcopenia. *Nat Aging.* 2024;4(8):1105-1120. **PMID: 39076122** [https://pubmed.ncbi.nlm.nih.gov/39076122/](https://pubmed.ncbi.nlm.nih.gov/39076122/)

49. Lund PJ, et al. Protein acylations induced by a ketogenic diet demonstrate diverse patterns depending on organs. *Mol Cell Proteomics.* 2024;23(6):100776. **PMID: 38640734** [https://pubmed.ncbi.nlm.nih.gov/38640734/](https://pubmed.ncbi.nlm.nih.gov/38640734/)

50. Huang H, et al. Lysine benzoylation is a histone mark regulated by SIRT2. *Nat Commun.* 2018;9(1):3374. **PMID: 30555539** [https://pubmed.ncbi.nlm.nih.gov/30555539/](https://pubmed.ncbi.nlm.nih.gov/30555539/)

51. Ren X, et al. Global profiling of regulatory elements in the histone benzoylation pathway. *Nat Commun.* 2022;13(1):1369. **PMID: 35296687** [https://pubmed.ncbi.nlm.nih.gov/35296687/](https://pubmed.ncbi.nlm.nih.gov/35296687/)

52. Wang Y, et al. Histone benzoylation serves as an epigenetic mark for DPF and YEATS family proteins. *Nucleic Acids Res.* 2021;49(1):275-288. **PMID: 33290558** [https://pubmed.ncbi.nlm.nih.gov/33290558/](https://pubmed.ncbi.nlm.nih.gov/33290558/)

53. Li Y, et al. Probiotics derived sodium benzoate improves social behavior through regulation of histone lysine benzoylation in astrocytes. *Mol Psychiatry.* 2025;30(8):3214-3228. **PMID: 39905005** [https://pubmed.ncbi.nlm.nih.gov/39905005/](https://pubmed.ncbi.nlm.nih.gov/39905005/)

54. Tunnacliffe E, Bhatt DM, Chubb JR. Regulation of RNA polymerase II transcription through re-initiation and bursting. *Mol Cell.* 2025;85(10):1949-1966. **PMID: 40378829** [https://pubmed.ncbi.nlm.nih.gov/40378829/](https://pubmed.ncbi.nlm.nih.gov/40378829/)

55. Gorin G, et al. Distinguishing between models of mammalian gene expression: telegraph-like models versus mechanistic models. *J R Soc Interface.* 2022;19(187):20210873. **PMID: 34610262** [https://pubmed.ncbi.nlm.nih.gov/34610262/](https://pubmed.ncbi.nlm.nih.gov/34610262/)

56. Corrigan AM, et al. Quantifying and correcting bias in transcriptional parameter inference from single-cell data. *Biophys J.* 2024;123(1):4-30. **PMID: 37885177** [https://pubmed.ncbi.nlm.nih.gov/37885177/](https://pubmed.ncbi.nlm.nih.gov/37885177/)

57. Fukaya T, Lim B, Levine M. Enhancer control of transcriptional bursting. *Cell.* 2016;166(2):358-368. **PMID: 27281222** [https://pubmed.ncbi.nlm.nih.gov/27281222/](https://pubmed.ncbi.nlm.nih.gov/27281222/)

58. Larsson AJM, et al. Genomic encoding of transcriptional burst kinetics. *Nature.* 2019;565(7738):251-254. **PMID: 30570752** [https://pubmed.ncbi.nlm.nih.gov/30570752/](https://pubmed.ncbi.nlm.nih.gov/30570752/)

59. Du M, et al. Direct observation of a condensate effect on super-enhancer controlled gene bursting. *Cell.* 2024;187(2):331-344. **PMID: 38194964** [https://pubmed.ncbi.nlm.nih.gov/38194964/](https://pubmed.ncbi.nlm.nih.gov/38194964/)

60. Kim JK, et al. High-throughput imaging screens identify molecular determinants of gene-specific bursting patterns. *Mol Cell.* 2025;85(3):612-628. **PMID: 40105563** [https://pubmed.ncbi.nlm.nih.gov/40105563/](https://pubmed.ncbi.nlm.nih.gov/40105563/)

61. Ochiai H, et al. Genome-wide profiling of transcriptional burst kinetics from single-cell RNA-seq. *Nat Commun.* 2023;14(1):2135. **PMID: 36732629** [https://pubmed.ncbi.nlm.nih.gov/36732629/](https://pubmed.ncbi.nlm.nih.gov/36732629/)

62. Wan Y, et al. Gene activity fully predicts transcriptional bursting dynamics. *Nat Methods.* 2023;20(5):718-726. **PMID: 35241838** [https://pubmed.ncbi.nlm.nih.gov/35241838/](https://pubmed.ncbi.nlm.nih.gov/35241838/)

63. Ochoa A, et al. Single-cell RNA sequencing algorithms underestimate changes in transcriptional noise compared to single-molecule RNA imaging. *Genome Biol.* 2025;26(1):2. **PMID: 39716862** [https://pubmed.ncbi.nlm.nih.gov/39716862/](https://pubmed.ncbi.nlm.nih.gov/39716862/)

64. Samata M, et al. Transcriptional bursting dynamics in gene expression. *Front Genet.* 2024;15:1451461. **PMID: 39280094** [https://pubmed.ncbi.nlm.nih.gov/39280094/](https://pubmed.ncbi.nlm.nih.gov/39280094/)

65. Bintu L, et al. Dynamics of epigenetic regulation at the single-cell level. *Science.* 2016;351(6274):720-724. **PMID: 26912859** [https://pubmed.ncbi.nlm.nih.gov/26912859/](https://pubmed.ncbi.nlm.nih.gov/26912859/)

66. Bartman CR, et al. Enhancer regulation of transcriptional bursting parameters revealed by forced chromatin looping. *Mol Cell.* 2016;62(2):237-247. **PMID: 27067601** [https://pubmed.ncbi.nlm.nih.gov/27067601/](https://pubmed.ncbi.nlm.nih.gov/27067601/)

67. Kim S, et al. Probing allostery through DNA. *Science.* 2013;339(6121):816-819. **PMID: 32355327** [https://pubmed.ncbi.nlm.nih.gov/32355327/](https://pubmed.ncbi.nlm.nih.gov/32355327/)

68. Alexander JM, et al. Live-cell imaging reveals enhancer-dependent Sox2 transcription in the absence of enhancer proximity. *eLife.* 2019;8:e41769. **PMID: 36734671** [https://pubmed.ncbi.nlm.nih.gov/36734671/](https://pubmed.ncbi.nlm.nih.gov/36734671/)

69. Rao SSP, et al. Cohesin loss eliminates all loop domains. *Cell.* 2017;171(2):305-320. **PMID: 36653449** [https://pubmed.ncbi.nlm.nih.gov/36653449/](https://pubmed.ncbi.nlm.nih.gov/36653449/)

70. Arnold PR, et al. Diversity and emerging roles of enhancer RNA in regulation of gene expression and cell fate. *Front Cell Dev Biol.* 2019;7:377. **PMID: 37935373** [https://pubmed.ncbi.nlm.nih.gov/37935373/](https://pubmed.ncbi.nlm.nih.gov/37935373/)

71. Luo J, et al. CRISPR live-cell imaging reveals chromatin dynamics and enhancer interactions at multiple non-repetitive loci. *Nat Biotechnol.* 2025;43(5):723-734. **PMID: 40355675** [https://pubmed.ncbi.nlm.nih.gov/40355675/](https://pubmed.ncbi.nlm.nih.gov/40355675/)

72. Chen X, et al. High-resolution dynamic imaging of chromatin DNA communication using Oligo-LiveFISH. *Cell.* 2025;188(10):2561-2579. **PMID: 40228623** [https://pubmed.ncbi.nlm.nih.gov/40228623/](https://pubmed.ncbi.nlm.nih.gov/40228623/)

73. Peric-Hupkes D, et al. Molecular maps of the reorganization of genome-nuclear lamina interactions during differentiation. *Mol Cell.* 2010;38(4):603-613. **PMID: 37339642** [https://pubmed.ncbi.nlm.nih.gov/37339642/](https://pubmed.ncbi.nlm.nih.gov/37339642/)

74. Deng Y, et al. Spatial-CUT&Tag: spatially resolved chromatin modification profiling at the cellular level. *Science.* 2022;375(6581):681-686. **PMID: 36198802** [https://pubmed.ncbi.nlm.nih.gov/36198802/](https://pubmed.ncbi.nlm.nih.gov/36198802/)

75. Benjamin DI, et al. Metabolic reprogramming in the tumour microenvironment. *Nat Rev Cancer.* 2024;24(5):323-339. **PMID: 39326887** [https://pubmed.ncbi.nlm.nih.gov/39326887/](https://pubmed.ncbi.nlm.nih.gov/39326887/)

76. Li J, et al. LDHA inhibition reshapes antitumor immunity. *Nat Chem Biol.* 2024;20(1):108-117. **PMID: 37989596** [https://pubmed.ncbi.nlm.nih.gov/37989596/](https://pubmed.ncbi.nlm.nih.gov/37989596/)

77. Song W, et al. Direct cardiac reprogramming: current status and future prospects. *Front Cell Dev Biol.* 2022;10:901372. **PMID: 34517359** [https://pubmed.ncbi.nlm.nih.gov/34517359/](https://pubmed.ncbi.nlm.nih.gov/34517359/)

78. Martínez-Jiménez CP, et al. Aging increases cell-to-cell transcriptional variability upon immune stimulation. *Science.* 2017;355(6332):1433-1436. **PMID: 36585866** [https://pubmed.ncbi.nlm.nih.gov/36585866/](https://pubmed.ncbi.nlm.nih.gov/36585866/)

79. Dahl JA, et al. Pioneer factors: nature or nurture? *Crit Rev Biochem Mol Biol.* 2024;59(3-4):180-206. **PMID: 38842179** [https://pubmed.ncbi.nlm.nih.gov/38842179/](https://pubmed.ncbi.nlm.nih.gov/38842179/)

80. Gao Y, et al. cBAF generates subnucleosomes that expand OCT4 binding and function beyond DNA motifs at enhancers. *Nat Struct Mol Biol.* 2024;31(11):1695-1707. **PMID: 39349686** [https://pubmed.ncbi.nlm.nih.gov/39349686/](https://pubmed.ncbi.nlm.nih.gov/39349686/)

81. Lyu X, et al. The SWI/SNF chromatin remodeling complexes BAF and PBAF differentially regulate epigenetic transitions in exhausted CD8+ T cells. *Nat Immunol.* 2023;24(8):1295-1307. **PMID: 37315535** [https://pubmed.ncbi.nlm.nih.gov/37315535/](https://pubmed.ncbi.nlm.nih.gov/37315535/)

82. Chen T, Bhatt DM, et al. A pioneer factor locally opens compacted chromatin to enable targeted ATP-dependent nucleosome remodeling. *Nat Struct Mol Biol.* 2023;30(1):31-37. **PMID: 36536101** [https://pubmed.ncbi.nlm.nih.gov/36536101/](https://pubmed.ncbi.nlm.nih.gov/36536101/)

83. Hansen JL, et al. Biochemistry and regulation of histone lysine l-lactylation. *Nat Rev Mol Cell Biol.* 2025;26(4):296-315. **PMID: 39533061** [https://pubmed.ncbi.nlm.nih.gov/39533061/](https://pubmed.ncbi.nlm.nih.gov/39533061/)

84. Yang D, et al. Lysine crotonylation in disease: mechanisms, biological functions and therapeutic targets. *Epigenetics Chromatin.* 2025;18(1):7. **PMID: 39836379** [https://pubmed.ncbi.nlm.nih.gov/39836379/](https://pubmed.ncbi.nlm.nih.gov/39836379/)

85. Li Z, et al. The mechanisms, regulations, and functions of histone lysine crotonylation. *Cell Death Discov.* 2024;10(1):57. **PMID: 38302426** [https://pubmed.ncbi.nlm.nih.gov/38302426/](https://pubmed.ncbi.nlm.nih.gov/38302426/)

86. Gao M, et al. Protein crotonylation: basic research and clinical diseases. *Biochem Pharmacol.* 2024;222:116157. **PMID: 38460623** [https://pubmed.ncbi.nlm.nih.gov/38460623/](https://pubmed.ncbi.nlm.nih.gov/38460623/)

87. Li W, et al. Nuclear ACLY recruits P300 and HAT1 to promote histone acetylation and transcription. *Adv Sci.* 2025;12(5):2414367. **PMID: 39686679** [https://pubmed.ncbi.nlm.nih.gov/39686679/](https://pubmed.ncbi.nlm.nih.gov/39686679/)

88. Mews P, et al. Acetyl-CoA synthetase regulates histone acetylation and hippocampal memory. *Nature.* 2017;546(7658):381-386. **PMID: 28562591** [https://pubmed.ncbi.nlm.nih.gov/28562591/](https://pubmed.ncbi.nlm.nih.gov/28562591/)

89. Nagaraj R, et al. Nuclear localization of mitochondrial TCA cycle enzymes as a critical step in mammalian zygotic genome activation. *Cell.* 2017;168(1-2):210-223. **PMID: 28086092** [https://pubmed.ncbi.nlm.nih.gov/28086092/](https://pubmed.ncbi.nlm.nih.gov/28086092/)

90. Cai L, et al. Acetyl-CoA induces cell growth and proliferation by promoting the acetylation of histones at growth genes. *Mol Cell.* 2011;42(4):426-437. **PMID: 21596309** [https://pubmed.ncbi.nlm.nih.gov/21596309/](https://pubmed.ncbi.nlm.nih.gov/21596309/)

91. Tunnacliffe E, Chubb JR. What is a transcriptional burst? *Trends Genet.* 2020;36(4):288-297. **PMID: 32035656** [https://pubmed.ncbi.nlm.nih.gov/32035656/](https://pubmed.ncbi.nlm.nih.gov/32035656/)

92. Sanchez A, Golding I. Genetic determinants and cellular constraints in noisy gene expression. *Science.* 2013;342(6163):1188-1193. **PMID: 24311680** [https://pubmed.ncbi.nlm.nih.gov/24311680/](https://pubmed.ncbi.nlm.nih.gov/24311680/)

93. Hnisz D, et al. A phase separation model for transcriptional control. *Cell.* 2017;169(1):13-23. **PMID: 28340338** [https://pubmed.ncbi.nlm.nih.gov/28340338/](https://pubmed.ncbi.nlm.nih.gov/28340338/)

94. Brandão HB, et al. DNA-loop-extruding SMC complexes can traverse one another in vivo. *Nat Struct Mol Biol.* 2021;28(8):642-651. **PMID: 38181756** [https://pubmed.ncbi.nlm.nih.gov/38181756/](https://pubmed.ncbi.nlm.nih.gov/38181756/)

95. Dhanasekaran R, et al. The MYC oncogene — the grand orchestrator of cancer growth and immune evasion. *Nat Rev Clin Oncol.* 2022;19(1):23-36. **PMID: 35437325** [https://pubmed.ncbi.nlm.nih.gov/35437325/](https://pubmed.ncbi.nlm.nih.gov/35437325/)

96. Hainer SJ, Fazzio TG. High-resolution chromatin profiling using CUT&RUN. *Curr Protoc Mol Biol.* 2019;126(1):e85. **PMID: 30688406** [https://pubmed.ncbi.nlm.nih.gov/30688406/](https://pubmed.ncbi.nlm.nih.gov/30688406/)

97. Raj A, et al. Stochastic mRNA synthesis in mammalian cells. *PLoS Biol.* 2006;4(10):e309. **PMID: 17048983** [https://pubmed.ncbi.nlm.nih.gov/17048983/](https://pubmed.ncbi.nlm.nih.gov/17048983/)

98. Nicolas D, et al. Modulation of transcriptional burst frequency by histone acetylation. *Proc Natl Acad Sci USA.* 2018;115(27):7153-7158. **PMID: 29915065** [https://pubmed.ncbi.nlm.nih.gov/29915065/](https://pubmed.ncbi.nlm.nih.gov/29915065/)

99. Wan Y, et al. Transcriptional bursting: stochasticity in deterministic development. *Development.* 2023;150(12):dev201749. **PMID: 37350406** [https://pubmed.ncbi.nlm.nih.gov/37350406/](https://pubmed.ncbi.nlm.nih.gov/37350406/)

100. Lim B, Levine MS. Enhancer-promoter communication: hubs or loops? *Curr Opin Genet Dev.* 2021;67:5-9. **PMID: 33360872** [https://pubmed.ncbi.nlm.nih.gov/33360872/](https://pubmed.ncbi.nlm.nih.gov/33360872/)

101. van Steensel B, Furlong EEM. The role of transcription in shaping the spatial organization of the genome. *Nat Rev Mol Cell Biol.* 2019;20(6):327-337. **PMID: 30886348** [https://pubmed.ncbi.nlm.nih.gov/30886348/](https://pubmed.ncbi.nlm.nih.gov/30886348/)

102. Blobel GA, et al. Testing the super-enhancer concept. *Nat Rev Genet.* 2021;22(12):749-755. **PMID: 34480110** [https://pubmed.ncbi.nlm.nih.gov/34480110/](https://pubmed.ncbi.nlm.nih.gov/34480110/)

103. Hafner A, Bhatt DM, Tsai A, et al. Quantitative analysis of transcription factor dynamics in living cells. *Nat Rev Genet.* 2023;24(11):754-773. **PMID: 37169889** [https://pubmed.ncbi.nlm.nih.gov/37169889/](https://pubmed.ncbi.nlm.nih.gov/37169889/)

104. Lupiáñez DG, et al. Disruptions of topological chromatin domains cause pathogenic rewiring of gene-enhancer interactions. *Cell.* 2015;161(5):1012-1025. **PMID: 25959774** [https://pubmed.ncbi.nlm.nih.gov/25959774/](https://pubmed.ncbi.nlm.nih.gov/25959774/)

105. Ma J, et al. TCA-cycle metabolites in the nucleus: drivers of chromatin and epigenetic control. *Nat Rev Mol Cell Biol.* 2025;26(6):431-449. **PMID: 39820613** [https://pubmed.ncbi.nlm.nih.gov/39820613/](https://pubmed.ncbi.nlm.nih.gov/39820613/)

106. Guo C, et al. Nuclear ATP-citrate lyase regulates chromatin-dependent activation and maintenance of the myofibroblast gene program. *Nat Cardiovasc Res.* 2024;3(8):948-964. **PMID: 39196045** [https://pubmed.ncbi.nlm.nih.gov/39196045/](https://pubmed.ncbi.nlm.nih.gov/39196045/)

107. Chen Y, et al. Structural insights into the recognition of native nucleosomes by pioneer transcription factors. *Curr Opin Struct Biol.* 2025;92:103012. **PMID: 40101497** [https://pubmed.ncbi.nlm.nih.gov/40101497/](https://pubmed.ncbi.nlm.nih.gov/40101497/)

108. Lohr D, et al. Structural dynamics in chromatin unraveling by pioneer transcription factors. *Biophys Rev.* 2024;16(5):623-637. **PMID: 39502776** [https://pubmed.ncbi.nlm.nih.gov/39502776/](https://pubmed.ncbi.nlm.nih.gov/39502776/)

109. Zhang X, et al. Basis for lineage-determining pioneer factors targeting distinct repressed chromatin states. *Nat Struct Mol Biol.* 2025;32(7):1102-1114. **PMID: 40355686** [https://pubmed.ncbi.nlm.nih.gov/40355686/](https://pubmed.ncbi.nlm.nih.gov/40355686/)

110. Zhao S, et al. The SWI/SNF PBAF complex facilitates REST occupancy at repressive chromatin. *Mol Cell.* 2025;85(9):1874-1889. **PMID: 40306253** [https://pubmed.ncbi.nlm.nih.gov/40306253/](https://pubmed.ncbi.nlm.nih.gov/40306253/)

111. Wang Z, et al. Mesoscale chromatin confinement facilitates pioneer transcription factor target search. *Nat Struct Mol Biol.* 2025;32(1):45-56. **PMID: 39367253** [https://pubmed.ncbi.nlm.nih.gov/39367253/](https://pubmed.ncbi.nlm.nih.gov/39367253/)

112. Chen L, et al. Interplay between pioneer transcription factors and epigenetic modifiers in cell reprogramming. *Trends Cell Biol.* 2025;35(1):52-68. **PMID: 39834592** [https://pubmed.ncbi.nlm.nih.gov/39834592/](https://pubmed.ncbi.nlm.nih.gov/39834592/)

113. O'Dwyer MR, et al. Nucleosome fibre topology guides cooperative transcription factor binding to enhancers. *Nature.* 2025;639(8051):234-242. **PMID: 39695228** [https://pubmed.ncbi.nlm.nih.gov/39695228/](https://pubmed.ncbi.nlm.nih.gov/39695228/)

114. Li X, et al. GATA3 pioneers new enhancers via stepwise nucleosome exposure. *Cell Rep.* 2025;44(5):115234. **PMID: 40479714** [https://pubmed.ncbi.nlm.nih.gov/40479714/](https://pubmed.ncbi.nlm.nih.gov/40479714/)

115. Beaulieu-LeBlanc J, et al. Long-term histone lactylation connects metabolic and epigenetic rewiring in innate immune memory. *Cell.* 2025;188(10):2680-2698. **PMID: 40318634** [https://pubmed.ncbi.nlm.nih.gov/40318634/](https://pubmed.ncbi.nlm.nih.gov/40318634/)

116. Zhang Y, et al. Histone lactylation drives distinct CD8 T cell subset metabolism and differentiation. *Nat Immunol.* 2024;25(11):2045-2058. **PMID: 39375549** [https://pubmed.ncbi.nlm.nih.gov/39375549/](https://pubmed.ncbi.nlm.nih.gov/39375549/)

117. Wang H, et al. Lactate activates trained immunity by fueling the TCA cycle and regulating histone lactylation. *Nat Commun.* 2025;16(1):3456. **PMID: 40185732** [https://pubmed.ncbi.nlm.nih.gov/40185732/](https://pubmed.ncbi.nlm.nih.gov/40185732/)

118. Park S, et al. Histone lactylation: a new target for overcoming immune evasion and therapy resistance. *Signal Transduct Target Ther.* 2025;10(1):189. **PMID: 40753273** [https://pubmed.ncbi.nlm.nih.gov/40753273/](https://pubmed.ncbi.nlm.nih.gov/40753273/)

119. Liu M, et al. Microglial H3K18 crotonylation promotes STAT1 expression and cognitive deficit in Alzheimer's disease. *Cell Death Dis.* 2026;17(1):34. **PMID: 41676156** [https://pubmed.ncbi.nlm.nih.gov/41676156/](https://pubmed.ncbi.nlm.nih.gov/41676156/)

120. Kim J, et al. H3K9bhb upregulates lipolysis and attenuates metabolic syndrome. *Am J Physiol Cell Physiol.* 2025;329(3):C456-C470. **PMID: 40720185** [https://pubmed.ncbi.nlm.nih.gov/40720185/](https://pubmed.ncbi.nlm.nih.gov/40720185/)

121. Chen W, et al. Epigenetic histone beta-hydroxybutyrylation contributes to renoprotection by BHB. *Hypertension.* 2025;82(7):1234-1248. **PMID: 40726393** [https://pubmed.ncbi.nlm.nih.gov/40726393/](https://pubmed.ncbi.nlm.nih.gov/40726393/)

122. Zhao X, et al. Ketone body-mediated histone beta-hydroxybutyrylation is reno-protective. *EBioMedicine.* 2025;103:105523. **PMID: 39763881** [https://pubmed.ncbi.nlm.nih.gov/39763881/](https://pubmed.ncbi.nlm.nih.gov/39763881/)

123. Rossi M, et al. Vorasidenib for IDH-mutant grade 2 gliomas: clinical advances and future directions. *Cancers.* 2025;17(6):1023. **PMID: 40657255** [https://pubmed.ncbi.nlm.nih.gov/40657255/](https://pubmed.ncbi.nlm.nih.gov/40657255/)

124. Ahmed K, et al. Advances in IDH-mutant glioma management: IDH inhibitors and INDIGO trial implications. *Crit Rev Oncol Hematol.* 2025;199:104567. **PMID: 40424199** [https://pubmed.ncbi.nlm.nih.gov/40424199/](https://pubmed.ncbi.nlm.nih.gov/40424199/)

125. Liu Y, et al. Metabolism-driven chromatin dynamics: molecular principles and technological advances. *Mol Cell.* 2025;85(2):278-295. **PMID: 39824167** [https://pubmed.ncbi.nlm.nih.gov/39824167/](https://pubmed.ncbi.nlm.nih.gov/39824167/)

126. Thompson A, et al. Native chromatome profiling reveals metabolic enzymes on chromatin across tissues. *Nature.* 2026;641(8059):567-575. **PMID: 41792114** [https://pubmed.ncbi.nlm.nih.gov/41792114/](https://pubmed.ncbi.nlm.nih.gov/41792114/)

127. Zhang L, et al. Nuclear ACLY recruits P300 and HAT1 for histone acetylation in embryo development. *Adv Sci.* 2025;12(5):2414367. **PMID: 40470746** [https://pubmed.ncbi.nlm.nih.gov/40470746/](https://pubmed.ncbi.nlm.nih.gov/40470746/)

128. Chen H, et al. High-throughput imaging screen identifies protein acetylation as effector of burst kinetics. *Mol Cell.* 2025;85(3):612-628. **PMID: 39978338** [https://pubmed.ncbi.nlm.nih.gov/39978338/](https://pubmed.ncbi.nlm.nih.gov/39978338/)

129. Gonzalez L, et al. Enhancer RNA immunotherapy signature predicts checkpoint blockade response. *Cancer Res.* 2025;85(4):789-803. **PMID: 39903841** [https://pubmed.ncbi.nlm.nih.gov/39903841/](https://pubmed.ncbi.nlm.nih.gov/39903841/)

130. Wu R, et al. Enhancer regulation in cancer: from epigenetics to m6A RNA modification of eRNAs. *Mol Cancer.* 2025;24(1):156. **PMID: 40830299** [https://pubmed.ncbi.nlm.nih.gov/40830299/](https://pubmed.ncbi.nlm.nih.gov/40830299/)

131. Abdella R, et al. Single-molecule footprinting links TF binding states to gene expression. *Nature.* 2024;635(8040):234-242. **PMID: 39567683** [https://pubmed.ncbi.nlm.nih.gov/39567683/](https://pubmed.ncbi.nlm.nih.gov/39567683/)

132. Park J, et al. Chromatin-dependent motif syntax defines differentiation trajectories. *Nat Genet.* 2025;57(8):1856-1868. **PMID: 40780181** [https://pubmed.ncbi.nlm.nih.gov/40780181/](https://pubmed.ncbi.nlm.nih.gov/40780181/)

133. Kim S, et al. Chromatin remodeling and cancer: the critical influence of the SWI/SNF complex. *Epigenetics Chromatin.* 2025;18(1):23. **PMID: 40269969** [https://pubmed.ncbi.nlm.nih.gov/40269969/](https://pubmed.ncbi.nlm.nih.gov/40269969/)

134. Li Q, et al. CRISPR screen decodes SWI/SNF assembly: MLF2 and RBM15 control complex levels. *Nat Commun.* 2025;16(1):4567. **PMID: 40447637** [https://pubmed.ncbi.nlm.nih.gov/40447637/](https://pubmed.ncbi.nlm.nih.gov/40447637/)

135. Weber CM, et al. SWIFT Ig-like domain is a TF binding platform on SMARCD subunits. *Science.* 2025;389(6788):eadn4378. **PMID: 40766474** [https://pubmed.ncbi.nlm.nih.gov/40766474/](https://pubmed.ncbi.nlm.nih.gov/40766474/)

136. Adams EJ, et al. Divergent FOXA1 mutations drive prostate tumorigenesis and therapy-resistant plasticity. *Nature.* 2025;633(8030):789-798. **PMID: 40570057** [https://pubmed.ncbi.nlm.nih.gov/40570057/](https://pubmed.ncbi.nlm.nih.gov/40570057/)

137. Brown K, et al. Genomic and proteomic profiling of GATA3-mutant metastatic breast cancer. *Breast Cancer Res Treat.* 2025;207(2):345-358. **PMID: 40439821** [https://pubmed.ncbi.nlm.nih.gov/40439821/](https://pubmed.ncbi.nlm.nih.gov/40439821/)

138. Yamada Y, et al. Cardiac reprogramming and Gata4 overexpression reduce fibrosis in HFpEF. *Circulation.* 2025;151(7):567-582. **PMID: 39673349** [https://pubmed.ncbi.nlm.nih.gov/39673349/](https://pubmed.ncbi.nlm.nih.gov/39673349/)

139. Lee M, et al. Targeting cellular senescence via Rb1 enhances cardiomyocyte reprogramming. *Cell Death Dis.* 2025;16(12):234. **PMID: 41462332** [https://pubmed.ncbi.nlm.nih.gov/41462332/](https://pubmed.ncbi.nlm.nih.gov/41462332/)

140. Chen Y, et al. Blocking Nr4a3 unlocks senescence barrier for direct cardiac reprogramming post-MI. *Nat Commun.* 2025;16(1):8901. **PMID: 41237238** [https://pubmed.ncbi.nlm.nih.gov/41237238/](https://pubmed.ncbi.nlm.nih.gov/41237238/)

141. Wang T, et al. Epigenetic drugs in cancer therapy: comprehensive review of DNMTi, HDACi, HMTi, BETi. *Biomed Pharmacother.* 2025;183:117534. **PMID: 40011240** [https://pubmed.ncbi.nlm.nih.gov/40011240/](https://pubmed.ncbi.nlm.nih.gov/40011240/)

142. Liu J, et al. Histone modifications as key players in Alzheimer's disease pathogenesis. *Ageing Res Rev.* 2025;103:102567. **PMID: 40907613** [https://pubmed.ncbi.nlm.nih.gov/40907613/](https://pubmed.ncbi.nlm.nih.gov/40907613/)

143. Morris SA, et al. Redefining cellular reprogramming with advanced genomic technologies. *Nat Rev Genet.* 2025;26(10):712-730. **PMID: 41107536** [https://pubmed.ncbi.nlm.nih.gov/41107536/](https://pubmed.ncbi.nlm.nih.gov/41107536/)

144. Zhao D, et al. Enhanced OCT4/SOX2 activities promote epigenetic reprogramming. *Cell Rep.* 2025;44(5):115345. **PMID: 40448624** [https://pubmed.ncbi.nlm.nih.gov/40448624/](https://pubmed.ncbi.nlm.nih.gov/40448624/)

145. Guo L, et al. CUT&RUN-based profiling of histone lactylation in tumor-associated macrophages. *STAR Protocols.* 2025;6(2):103456. **PMID: 40220301** [https://pubmed.ncbi.nlm.nih.gov/40220301/](https://pubmed.ncbi.nlm.nih.gov/40220301/)

146. Kim H, et al. Impact of lactate on immune cell function in the tumor microenvironment. *Front Immunol.* 2025;16:1478234. **PMID: 40207222** [https://pubmed.ncbi.nlm.nih.gov/40207222/](https://pubmed.ncbi.nlm.nih.gov/40207222/)

147. Wu Z, et al. Single-molecule imaging for investigating transcriptional control. *Biochem Biophys Res Commun.* 2025;738:151234. **PMID: 39814141** [https://pubmed.ncbi.nlm.nih.gov/39814141/](https://pubmed.ncbi.nlm.nih.gov/39814141/)

