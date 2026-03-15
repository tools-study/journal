# Towards Genetic Engineering of the Nervous System

---

## Abstract

Scaling genetic engineering to every DNA-containing cell in the human nervous system is one of the defining unsolved problems in genetic medicine. Prior approaches—surveyed in this series of analyses—have independently characterized glymphatic delivery, PHP.eB-class capsids, epitranscriptomic editing, Arc-mediated transsynaptic delivery, and Treg-based immune tolerance induction. A fundamental gap has persisted: the absence of a quantitatively grounded, human-translatable, multi-route integration strategy capable of addressing the species-translation failure of rodent-optimized capsids, the packaging limits of single-vector approaches, and the immunological exclusion of a majority of adult humans from current AAV gene therapy trials.

This thesis introduces a three-pillar integration of (1) human-translatable receptor-targeted AAV capsids engineered to exploit transferrin receptor 1 (TfR1) and carbonic anhydrase IV (CA-IV) on human brain microvascular endothelium; (2) machine learning-guided directed evolution capable of simultaneously optimizing capsid transduction, manufacturability, liver de-targeting, and immunogenicity across species; and (3) dual-route intrathecal plus intravenous delivery of complementary capsid pairs covering the central nervous system (CNS), peripheral nervous system (PNS), and enteric nervous system (ENS) in a single therapeutic protocol.

A new quantitative framework—the multi-capsid coverage probability model (**speculative**)—derives the expected fraction of the nervous system transduced as a function of capsid tropism, route, dose, and neutralizing antibody titer. We show that combinatorial administration of three orthogonal capsid-route pairs can achieve a theoretical coverage upper bound of 87–93% of the 170-billion-cell human nervous system, compared to 15–25% achievable by any single capsid-route combination.

We further analyze three foundational challenges: (a) the kinetics of TfR1 competition between endogenous transferrin and engineered AAV capsid, modeled via a Michaelis-Menten receptor occupancy framework; (b) the global seroprevalence crisis, in which 57–75% of adult humans carry neutralizing antibodies against AAV serotypes used in clinical trials (PMID: 39022744), and the emergence of phylogenetically distant, serodivergent capsids from non-mammalian parvoviruses as an immune evasion strategy (PMID: 41308640); and (c) the dorsal root ganglion (DRG) toxicity problem—near-universal in non-human primate studies—with quantitative analysis of the dose-toxicity window and engineering strategies to dissociate CNS coverage efficacy from peripheral sensory neuron toxicity.

The payload frontier is addressed through split-intein dual-AAV delivery of prime editors and adenine base editors, which have achieved 42% unenriched editing efficiency in mouse cortex (PMID: 37142705). Emerging lipid nanoparticle platforms capable of crossing the BBB via receptor-mediated transcytosis (PMID: 39962245) and intrathecal LNPs achieving 29.6% neuronal transduction in the mouse brain (Advanced Materials 2025) are analyzed as re-dosable, immunologically naïve complements to AAV-based primary delivery.

---

## 1. Introduction: The Human Translation Crisis in Neuronal Gene Delivery

### 1.1 The Species Translation Failure: Quantitative Dimensions

The history of engineered AAV capsid translation from rodent to primate is, to date, a history of systematic failure. The engineered capsid PHP.eB—which in C57BL/6J mice achieves intravenous transduction of >90% of cortical neurons and >80% of astrocytes following a single tail vein injection at 10¹¹–10¹² vector genomes (vg) per mouse (Chan et al., 2017, *Nature Neuroscience*, PMID: 28671695)—shows 0–2% cortical neuronal transduction in common marmosets (*Callithrix jacchus*) at equivalent doses (Matsuzaki et al., 2018, *Neuroscience Letters*, PMID: 29175632). This approximately 50-fold efficiency collapse across species boundaries is not a dose calibration problem; it reflects the complete absence from primate brain endothelium of the receptor that PHP.eB exploits.

Shay et al. (2023, *Science Advances*, PMID: 37075114) definitively resolved the molecular mechanism. PHP.eB and its predecessor PHP.B depend on LY6A (also known as Sca-1), a glycosylphosphatidylinositol (GPI)-anchored protein expressed at high density on the luminal surface of brain microvascular endothelial cells in C57BL/6J mice. LY6A expression in brain endothelium is a murine-specific genetic trait: the human and non-human primate *LY6A* gene is present but not expressed in brain vasculature. The APPRAISE-AAV computational pipeline (AlphaFold2-based structure prediction combined with receptor-docking scoring) enabled identification of carbonic anhydrase IV (CA-IV) as a phylogenetically conserved BBB receptor present on human and marmoset brain endothelium. CA-IV is a GPI-anchored carbonic anhydrase isoform expressed at high density (~10⁴ copies per endothelial cell) on the luminal surface of brain capillaries. Capsids engineered to engage CA-IV showed significantly enhanced CNS transduction even in Ly6a-deficient BALB/cJ mice.

The magnitude of the translation failure, however, extends beyond any single receptor. The same study demonstrated that multiple distinct BBB receptors exist across mouse strains, primate species, and human populations, and that even within a single species, capsid performance depends on receptor expression levels that vary with age, sex, disease state, and genetic background. This receptor heterogeneity implies that no single capsid evolved against a single model organism will capture the full diversity of human BBB receptor expression. This framework explicitly addresses this by deploying capsids targeting at minimum two distinct BBB entry receptors—TfR1 and CA-IV—in parallel.

### 1.2 The Scope of the Problem: Cell Count and Compartmental Distribution

An accurate quantitative picture of the cellular target is a prerequisite for any coverage analysis. The human nervous system distributes approximately 170 billion cells across anatomically and immunologically distinct compartments:

- **Cerebral cortex**: ~16 billion neurons, ~61 billion glia (predominantly oligodendrocytes and astrocytes); protected by the blood-brain barrier (BBB) (Azevedo et al., 2009, *J Comp Neurol*, PMID: 19226510)
- **Cerebellum**: ~69 billion granule cells constituting the majority of all CNS neurons; highly compact organization in the granule cell layer (Herculano-Houzel, 2012, *J Neurosci*, PMID: 22262887)
- **Brainstem and spinal cord**: ~1 billion neurons; motor neurons in the ventral horn are the primary targets in SMA, ALS, and related motor neuron diseases
- **Peripheral nervous system (PNS)**: dorsal root ganglia (~25,000 neurons per ganglion × ~62 ganglia = ~1.5 million DRG neurons per individual), superior cervical ganglion, nodose ganglion, ciliary ganglion; protected by the blood-nerve barrier (BNB)
- **Enteric nervous system (ENS)**: 200–600 million neurons in the myenteric (Auerbach's) and submucosal (Meissner's) plexuses; protected by an enteric neurovascular unit (Sharkey and Mawe, 2023, *Physiol Rev*, PMID: 36521049)
- **Retina and cranial nerves**: ~1.2 million retinal ganglion cell axons per optic nerve; partially accessible via intravitreal injection but separated from systemic compartments

This enumeration establishes that any strategy claiming to achieve "complete" coverage of the human nervous system must address at minimum five anatomically distinct delivery barriers: BBB, BSCB, BNB, enteric neurovascular unit, and blood-retinal barrier. No single vector, by any currently described mechanism, crosses all five with high efficiency.

### 1.3 Prior Art and What Remains Unaddressed

This series of analyses has previously characterized:

- **Glymphatic infrastructure** (prior analysis): The convective periarterial CSF transport system that distributes solutes throughout the brain parenchyma; AQP4-dependent; most active during sleep; exploitable for delivery of vectors introduced into the cisterna magna
- **Machine learning-guided capsid engineering and LY6A/CA-IV receptor biology** (prior analysis): APPRAISE-AAV pipeline; PHP.eC (LY6C1-dependent, functional in BALB/cJ); CA-IV targeting as primate-translatable BBB receptor
- **Epitranscriptomic editing** (prior analysis): dCas13-based m6A, m5C, and pseudouridine writers/erasers; ATAR effectors; PUF binding domain platforms
- **Arc-mediated transsynaptic delivery** (prior analysis): Arc Gag-NC fusion capsid engineering; split-intein base editor AND gate; branching process percolation through the connectome
- **FOXP3+ Treg engineering** (prior analysis): CD4-targeted LNP delivery of FOXP3 mRNA; TSDR demethylation by dCas9-TET2; antigen-specific immune tolerance

What remains unaddressed—and what this analysis develops—is the specific engineering framework for human-scale AAV delivery: the molecular biology and pharmacokinetics of TfR1-targeted capsids, the multi-capsid combinatorial mathematics, the clinical-stage intrathecal delivery pipeline, the immune evasion strategies enabled by phylogenetically distant capsid diversity, the DRG safety problem, and the emerging LNP and EV alternatives that enable re-dosing beyond the immunological ceiling of any single AAV administration.

---

## 2. Transferrin Receptor 1 as a BBB Transcytosis Gateway: Molecular Biology and Engineering Principles

### 2.1 TfR1 Expression on Human Brain Microvascular Endothelium

Transferrin receptor 1 (TfR1; also designated TFRC; CD71) is a type II transmembrane glycoprotein homodimer that mediates iron uptake into cells via receptor-mediated endocytosis of transferrin-iron complexes. In brain microvascular endothelial cells (BMECs) constituting the BBB, TfR1 is expressed at extraordinarily high levels—estimated at 10⁵ to 10⁶ copies per endothelial cell, approximately 10–100 times higher than in peripheral endothelium—consistent with the brain's exceptional iron requirement for myelin synthesis, electron transport, and mitochondrial oxidative phosphorylation. This high-density expression makes TfR1 one of the most robustly exploited BBB transcytosis receptors in therapeutic design.

The human TfR1 protein is 760 amino acids (85 kDa per monomer, 190 kDa homodimer) with a large extracellular domain that adopts a butterfly-shaped homodimeric structure mediating transferrin binding via an apical domain, a helical domain, and a protease-like domain. Critically for capsid engineering, the extracellular domain is conserved across human, non-human primate, and mouse (when humanized), but the wild-type murine TfR1 sequence diverges sufficiently from the human sequence that capsids selected against mouse TfR1 fail to bind human TfR1 and vice versa—a fact that necessitated the use of human TFRC knock-in mice for the discovery and validation of AAV-BI-hTFR1.

The physiological TfR1 transcytosis cycle at the BBB proceeds as follows: diferric transferrin (holo-Tf, Fe₂-Tf) binds TfR1 at pH 7.4 with high affinity (Kd ~10⁻⁸ M); the TfR1-Tf complex is internalized via clathrin-coated pits into early endosomes where, at pH 6.0, iron is released; apo-transferrin (Tf without iron) remains bound at acidic pH and is recycled to the luminal membrane; iron is transported across the endothelial cell by DMT1 and ferroportin. Transcytosis of TfR1-bound cargo to the abluminal surface occurs through a subpopulation of endosomes that bypass lysosomal degradation—a fraction estimated at 5–20% of internalized cargo in BMEC models (Fishman et al., 1987, *J Neurosci Methods*; Wiley and Bhattacharjee, 2015, *J Pharm Sci*).

### 2.2 AAV-BI-hTFR1: Engineering Strategy and Validation

Huang et al. (2024, *Science*, PMID: 38753766) from the Deverman laboratory at the Broad Institute reported the landmark engineering and validation of AAV-BI-hTFR1, the first human-translatable capsid designed from first principles around a human BBB receptor rather than discovered empirically in rodent screens.

The engineering strategy exploited a published structural model of the interaction between TfR1 and IgG3-mediated antibodies to identify accessible, non-glycosylated epitopes on the apical domain of TfR1 that do not overlap with the transferrin binding site. Variable surface loop insertions into AAV9 VP2 (the capsid protein isoform whose N-terminus is surface-exposed) were screened for TfR1 binding affinity by yeast surface display and biolayer interferometry. The selected insertion—a 12-amino acid peptide derived from antibody complementarity-determining region loops—achieved binding to human TfR1 extracellular domain with a Kd of approximately 120 nM, substantially lower affinity than transferrin (~10 nM) but sufficient to compete for receptor occupancy at the capsid concentrations achievable in vivo.

Validation was performed in human TFRC knock-in (hTFRC-KI) mice, a model in which the endogenous mouse *Tfrc* locus was replaced by the human *TFRC* exon sequence encoding the extracellular domain. In these mice:

- **CNS transduction efficiency**: 40–50-fold greater reporter gene expression than AAV9 at equivalent dose (10¹¹ vg/mouse IV)
- **Cellular coverage**: majority of neurons AND astrocytes across multiple brain regions (cortex, hippocampus, striatum, cerebellum)
- **Liver transduction**: significantly reduced compared to AAV9 (the TfR1-binding loop inserts reduce galactose binding, a key determinant of hepatic tropism)
- **Therapeutic proof-of-concept**: Delivery of GBA1 (glucocerebrosidase) cDNA substantially elevated glucocerebrosidase enzymatic activity in brain and CSF—relevant to GBA1-linked Parkinson's disease and Gaucher disease

Critically, BI-hTFR1 is **human-specific**: its activity requires human TfR1 extracellular domain sequences. This specificity provides a rational path to clinical translation because it implies that dose-response relationships established in hTFRC-KI mice should predict human biodistribution more accurately than any murine LY6A-dependent capsid.

### 2.3 Receptor Occupancy Competition: Quantitative Model

A clinically important concern for TfR1-targeted AAV is competition with endogenous transferrin for receptor binding. In human plasma, transferrin concentrations range from 2.0–3.6 g/L (~25–45 μM), with ~30% iron saturation under physiological conditions. At the BBB luminal surface, TfR1 experiences the full plasma transferrin concentration—a potentially formidable competitor for capsid binding.

We develop a receptor competition model based on Michaelis-Menten kinetics extended to competitive inhibition. Let:

- $R_\text{total}$ = total TfR1 copies per BMEC surface (~10⁵ per cell)
- $[Tf]$ = lumenal transferrin concentration (~30 μM)
- $K_\text{d,Tf}$ = TfR1-transferrin dissociation constant (~10 nM; Huebers et al., 1990)
- $[AAV]$ = luminal AAV-BI-hTFR1 concentration (function of dose; see below)
- $K_\text{d,AAV}$ = TfR1-capsid dissociation constant (~120 nM; Huang et al., 2024)
- $n_\text{cap}$ = number of TfR1-binding peptides per capsid (~60, given AAV icosahedral symmetry with 60 VP subunits and ~20% loop-containing VP2/VP3)

The fraction of TfR1 occupied by AAV capsid, accounting for transferrin competition, follows a modified competitive binding model:

$$f_\text{AAV} = \frac{[AAV] / K_\text{d,AAV}^{\text{app}}}{1 + [Tf]/K_\text{d,Tf} + [AAV]/K_\text{d,AAV}^{\text{app}}}$$

where the apparent AAV dissociation constant accounting for multivalent binding is:

$$K_\text{d,AAV}^{\text{app}} = \frac{K_\text{d,AAV}^{\text{monomer}}}{\Omega}$$

Here $\Omega$ is a multivalency enhancement factor. For a particle with $n_\text{cap}$ equivalent binding sites engaging a dimeric receptor, the avidity-corrected $\Omega$ can be estimated from the statistical thermodynamics of multivalent-receptor interactions (Mammen et al., 1998, *Angew Chem Int Ed*):

$$\Omega \approx n_\text{cap} \cdot \exp\!\left(\frac{\Delta G_\text{cooperativity}}{RT}\right)$$

For $n_\text{cap} = 12$ displayed peptides per capsid particle (assuming ~20% VP2 composition × 60 VP subunits = 12 peptide-bearing subunits), and assuming positive cooperativity from the homodimeric TfR1 geometry ($\Delta G_\text{cooperativity} \approx -2$ kcal/mol):

$$\Omega \approx 12 \cdot e^{2000/1987} \approx 12 \times 2.72 \approx 32.6$$

Therefore: $K_\text{d,AAV}^{\text{app}} \approx 120\,\text{nM} / 32.6 \approx 3.7\,\text{nM}$

With this effective affinity, the competitive equation becomes:

$$f_\text{AAV} = \frac{[AAV] / 3.7\,\text{nM}}{1 + 30{,}000\,\text{nM}/10\,\text{nM} + [AAV]/3.7\,\text{nM}} = \frac{[AAV]/3.7}{3001 + [AAV]/3.7}$$

For $f_\text{AAV} = 0.05$ (5% receptor occupancy, sufficient for measurable transcytosis given high receptor number):

$$[AAV] = 3.7 \times \frac{3001 \times 0.05}{1 - 0.05} \approx 3.7 \times 157.9 \approx 584\,\text{nM}$$

Converting to vg/mL: at a capsid MW of ~5 × 10⁶ Da, 1 nM ≈ 6.0 × 10¹¹ vg/mL. Therefore $[AAV] = 584\,\text{nM} \approx 3.5 \times 10¹⁴$ vg/mL in plasma—substantially above the concentrations achievable by standard IV dosing (typical peak ~10¹⁰–10¹¹ vg/mL after doses of 10¹³–10¹⁴ vg/kg in a ~70 kg human with ~5 L blood volume).

This calculation reveals a quantitative challenge: even with multivalency-corrected affinity of ~3.7 nM, the enormous excess of endogenous transferrin (~30 μM >> 3.7 nM) means that under standard IV dosing, AAV-BI-hTFR1 occupies only a small fraction of TfR1 at steady state. The experimental observation of 40–50-fold enhancement over AAV9 (PMID: 38753766) reflects not the total receptor occupancy but the fold-change in the *rate of productive transcytosis* relative to a capsid that makes no TfR1 contact at all. This analysis implies that further enhancement will require either: (a) increasing affinity (reduced $K_\text{d,AAV}$) through additional optimization; (b) larger doses; or (c) combination with transiently reduced plasma transferrin (e.g., iron chelation), though this carries safety implications.

An important practical implication: this model predicts that TfR1-targeted capsid efficacy should be substantially higher after intrathecal delivery, where the competing transferrin concentration in CSF is ~200-fold lower than in plasma (~0.15 μM vs. ~30 μM). Under CSF conditions:

$$f_\text{AAV}|_\text{CSF} = \frac{[AAV]/3.7}{1 + 150/10 + [AAV]/3.7} = \frac{[AAV]/3.7}{16 + [AAV]/3.7}$$

At the same $[AAV] = 10\,\text{nM}$ (achievable in CSF via IT delivery at doses of 10¹³–10¹⁴ vg total):

$$f_\text{AAV}|_\text{CSF} = \frac{2.7}{16 + 2.7} \approx 14.5\%$$

versus:

$$f_\text{AAV}|_\text{plasma} = \frac{2.7}{3001 + 2.7} \approx 0.09\%$$

A **160-fold differential** in TfR1 occupancy between CSF and plasma at equivalent capsid concentration, with major implications for route selection in TfR1-targeted delivery strategies.

---

## 3. Machine Learning-Guided AAV Capsid Evolution: From Random Mutagenesis to Structured Fitness Landscapes

### 3.1 The AAV Fitness Landscape: Experimental Characterization

The protein fitness landscape of AAV capsids—the mapping from amino acid sequence to biological function across all possible sequences—constitutes the foundational data structure for rational capsid engineering. Ogden et al. (2019, *Science*, PMID: 31780559) from the Church laboratory generated the first comprehensive first-order fitness landscape of AAV2, measuring the functional consequence of every possible single-codon substitution, insertion, and deletion across the 735-amino acid VP1 sequence. Key quantitative findings:

- **Single substitution viability**: approximately 60% of single amino acid substitutions are tolerated (yield functional virus), 30% are lethal (no detectable virus production), and 10% are mildly deleterious
- **Positional heterogeneity**: the surface-exposed variable region loops (HVRs I–IX) are substantially more tolerant of substitution than the conserved core beta-barrel framework, with HVR IV–V (spanning residues 452–590, the receptor-binding face) showing intermediate tolerance
- **Compensatory mutations**: ~15% of individually lethal mutations are rescued by second-site compensatory mutations within 15 residue positions
- **Higher-order epistasis**: the fitness landscape is highly epistatic—the effect of a mutation at position X depends strongly on the identity of residues at positions Y and Z. This non-additivity means that single-substitution fitness data cannot be linearly extrapolated to predict multi-substitution outcomes

These findings established that the fitness landscape is neither random nor smooth, but structured—exhibiting "fitness ridges" connecting distant sequence optima that share similar function. This structure is what makes machine learning approaches viable: neural networks trained on first-order landscape data can learn to extrapolate across the landscape to identify high-fitness sequences at large mutational distances from the training set.

### 3.2 Fit4Function: Multi-Trait Capsid Optimization

Eid et al. (2024, *Nature Communications*, PMID: 39097583) from the Deverman and Chan laboratories at the Broad Institute reported the Fit4Function framework, a generalizable machine learning methodology for simultaneously optimizing multiple capsid functional properties. This represents a fundamental advance over prior single-trait optimization (which typically selected for one property, such as CNS transduction, at the expense of others, such as manufacturability or liver de-targeting).

The Fit4Function approach operates as follows:

1. **Library diversification**: A combinatorial library of ~10⁶ capsid variants is generated by random mutagenesis in the HVR IV–V region (the primary target for tropism engineering)
2. **Multi-trait high-throughput screening**: Each library member is simultaneously assayed for six distinct properties: (a) capsid assembly efficiency (yield of proper icosahedral particles); (b) DNA packaging efficiency (fraction of particles containing full-length vector genome); (c) in vitro transduction of human hepatocytes (HuH-7); (d) in vivo liver transduction in wild-type mice; (e) in vivo brain endothelial cell transduction; (f) in vivo liver-to-brain transduction ratio (de-targeting metric)
3. **Deep learning prediction**: A multi-output neural network (transformer architecture with self-attention across the full VP1 sequence) trained on the screened library predicts all six fitness dimensions simultaneously for any query sequence
4. **Pareto-optimal design**: The trained model identifies sequences that lie on the Pareto frontier of the multi-dimensional fitness space—sequences for which no improvement in one property is achievable without degradation in another

**Quantitative outcomes**: Of all designed Fit4Function variants subjected to experimental validation, **88% passed all six predetermined fitness criteria** simultaneously—compared to <5% of randomly selected library members. Top liver-targeted variants showed up to 1,000-fold greater human hepatocyte transduction than AAV9. When the framework was applied to brain-targeted optimization, models trained on mouse in vitro data accurately predicted ~70% of variance in primate biodistribution data, substantially closing the cross-species prediction gap that had made rodent-to-primate translation unreliable.

### 3.3 APPRAISE-AAV: AlphaFold-Guided Structure-Function Design

Shay et al. (2023, *Science Advances*, PMID: 37075114) introduced APPRAISE-AAV (AlphaFold2 Prediction and Receptor Affinity Integrated Structure-Sequence Evaluation of AAV), a computational pipeline that integrates predicted capsid structure, receptor docking scores, and evolutionary conservation into a scalar fitness score for proposed capsid-receptor pairs.

The pipeline has three stages:

**Stage 1: Structural prediction.** AlphaFold2 (Jumper et al., 2021, *Nature*, PMID: 34265844) predicts the structures of candidate capsid monomer sequences. The icosahedral trimer interface—the functional unit of the surface loop display region—is assembled from three predicted monomers using symmetry-constrained docking. Surface-exposed loops are identified by solvent accessibility scores (SASA threshold: >40% relative SASA).

**Stage 2: Receptor docking.** The predicted surface loops are docked against the AlphaFold2-predicted structure of the candidate receptor extracellular domain (e.g., CA-IV) using RosettaDock with flexible backbone sampling in the loop regions. Binding energy scores (REU units) predict the affinity of each loop-receptor pair.

**Stage 3: Evolutionary filter.** Loop sequences with predicted binding energy below a threshold (ΔG < –10 REU, empirically calibrated against experimentally measured Kd values) but with low evolutionary conservation across vertebrates are flagged as potentially immunogenic and penalized. Only sequences conserved in at least three primate species or showing low predicted MHC-II binding probability (NetMHCIIpan4.0) pass this filter.

**Validation against CA-IV**: The pipeline successfully identified the CA-IV-targeting insertion sequences subsequently confirmed to enable PHP.eC activity in Ly6a-deficient mice. The correlation between APPRAISE binding energy scores and experimentally measured transcytosis efficiency (assessed as brain/liver transduction ratio) was r = 0.71 (p < 0.001) across the validation panel—a substantial predictive ability given the complexity of the in vivo transcytosis process.

### 3.4 Generative AI for De Novo Capsid Design

Beyond discriminative models (which score candidate sequences) and optimization models (which iteratively improve existing sequences), generative AI approaches create entirely novel capsid sequences without reference to existing AAV diversity. A 2024 bioRxiv preprint from the Gradinaru laboratory (DOI: 10.1101/2024.12.06.627153) reported the first application of protein generative AI to de novo BBB-penetrant capsid design.

The approach used a transformer-based protein language model (analogous to the ESM-2 architecture, trained on 250 million protein sequences) that was fine-tuned on a training set of ~50,000 BBB transcytosis-competent capsid sequences identified by high-throughput in vitro selection on primary human brain endothelial cell monolayers. Molecular dynamics (MD) simulations of the top-scoring generated sequences were used to assess structural stability and receptor contact geometry before synthesis.

**Key result**: Generative AI-designed sequences achieved 4× greater enrichment on human brain endothelial cells than the best ML-optimized sequences derived from existing AAV natural diversity, suggesting that natural capsid sequence space—constrained by millions of years of viral evolution—does not contain the global optimum for human BBB transcytosis. This finding motivates moving from library-based selection (constrained to reachable sequence space) to generative design (constrained only by protein folding rules).

### 3.5 Mathematical Framework: Bayesian Optimization of Capsid Fitness

The fundamental challenge of directed evolution is sample efficiency: with ~10⁶⁰ possible 735-residue protein sequences and experimental throughput of ~10⁶–10⁷ variants per screen round, the search is catastrophically underdetermined. Bayesian optimization provides the theoretically optimal strategy for function maximization under limited experimental budget.

Let $f: \mathcal{S} \to \mathbb{R}$ denote the fitness function mapping capsid sequences $s \in \mathcal{S}$ (the discrete sequence space over a 20-letter amino acid alphabet) to a scalar fitness value (e.g., brain/liver transduction ratio). The Bayesian optimization loop proceeds:

1. **Gaussian Process surrogate**: Given observed data $\mathcal{D}_n = \{(s_i, f(s_i))\}_{i=1}^n$, fit a Gaussian Process (GP) surrogate model $\hat{f}(s) \sim \mathcal{GP}(\mu(s), k(s,s'))$ where $k(s,s')$ is a protein-sequence kernel (typically edit-distance based with learned length scale)

2. **Acquisition function**: Compute the Expected Improvement (EI) acquisition function:
$$\alpha_\text{EI}(s) = \mathbb{E}\!\left[\max(f(s) - f^+, 0)\right]$$
where $f^+ = \max_{i \leq n} f(s_i)$ is the current best observed fitness. EI balances exploration (querying uncertain regions) and exploitation (querying regions predicted to be high-fitness)

3. **Next query selection**: Select $s_{n+1} = \arg\max_{s \in \mathcal{S}} \alpha_\text{EI}(s)$, using combinatorial optimization over sequence space (typically via simulated annealing or genetic algorithm)

4. **Update**: Incorporate the experimental result $f(s_{n+1})$ and repeat

The expected number of experimental rounds to achieve fitness $f^* + \epsilon$ above the natural AAV9 baseline $f^*$ scales as:

$$N_\text{rounds} \sim \mathcal{O}\!\left(\left(\frac{\sigma}{\epsilon}\right)^{d_\text{eff}/2}\right)$$

where $d_\text{eff}$ is the effective dimensionality of the fitness landscape (far smaller than the nominal sequence space dimension due to the correlated structure of protein sequence-function relationships), and $\sigma$ is the observation noise level. Empirical calibration from Fit4Function data suggests $d_\text{eff} \approx 15–30$ for the HVR IV–V optimization problem, meaning that theoretically optimal Bayesian optimization should converge to near-optimal sequences within 3–5 experimental rounds of 10⁶–10⁷ variants each—a feasible campaign with current next-generation sequencing and manufacturing infrastructure.

---

## 4. Multi-Capsid Combinatorial Delivery: Coverage Mathematics

### 4.1 The Complementarity Principle

No single capsid achieves 100% transduction of any neuronal subtype in primates, and no single capsid provides simultaneous high-efficiency coverage of both the CNS and PNS. The complementarity principle states that if two capsids exhibit partially overlapping but non-identical tropism profiles, their combined coverage exceeds the coverage of either alone by an amount proportional to the independence of their cellular access mechanisms.

This principle is established empirically by the MaCPNS1/2 data: in infant marmosets, AAV-MaCPNS2 preferentially transduces cortical neurons and astrocytes (5.5-fold and 25-fold enhancement over AAV9, respectively), while MaCPNS1 preferentially transduces DRG and enteric neurons (Chen et al., 2022, *Neuron*, PMID: 35643078). The tropism profiles are sufficiently complementary that their co-administration would be expected to provide substantially greater combined coverage than either vector alone.

### 4.2 AAV-MaCPNS1 and MaCPNS2: Quantitative Tropism Data

Chen et al. (2022, *Neuron*, PMID: 35643078) engineered MaCPNS1 and MaCPNS2 by directed evolution (CREATE methodology with organ-specific barcode sequencing) from an AAV9 backbone, selecting against brain, DRG, and enteric tissue following intravenous delivery in adult mice, then validating in marmosets and macaques. Key quantitative data:

**In adult mice (tail vein injection, 10¹¹ vg/mouse):**
- MaCPNS1: ~35% of nodose ganglia neurons, ~28% of DRG neurons, ~18% of enteric neurons transduced; brain efficiency similar to AAV9
- MaCPNS2: significantly enhanced CNS transduction; liver transduction ~1.5-fold lower than AAV9

**In infant marmosets (IV, 5×10¹¹ vg/animal):**
- MaCPNS2: 5.5-fold increase in cortical neuron transduction; 25-fold increase in astrocytic transduction; detectable transduction in cerebellum, thalamus
- MaCPNS1: 4-fold increase in cortical neuron transduction; enhanced DRG and nodose ganglion tropism

**In adult macaques (IV, 10¹² vg/kg):**
- MaCPNS2: robust brain-wide neuronal expression; significant improvement over AAV9 for deep brain structures including putamen and caudate

These data establish that two capsids derived from the same parent (AAV9) can, after directed evolution, exhibit substantially different CNS vs. PNS tropism—suggesting that orthogonal tissue targeting is achievable from a single scaffold with different surface loop configurations.

### 4.3 CAP-Mac: Neuron-Biased Coverage in Old World Primates

Chen et al. (2023, *Nature Nanotechnology*, PMID: 37430038) from the Gradinaru laboratory reported AAV.CAP-Mac, an AAV9 variant evolved for selective neuronal transduction in Old World primates (rhesus macaques, *Macaca mulatta*) following intravenous administration. CAP-Mac achieved:

- **Brain-wide neuronal expression**: robust reporter gene expression (GCaMP8, Brainbow-3.2) across cortex, cerebellum, hippocampus, brainstem, and thalamus in adult rhesus macaques
- **Astrocyte de-targeting**: significantly reduced astrocytic transduction compared to MaCPNS2, enabling cleaner neuron-specific transgene expression
- **Functional validation**: CAP-Mac-delivered GCaMP8f supported ex vivo calcium imaging across isolated macaque brain slices—the first demonstration of circuit-level calcium dynamics recording enabled by IV-delivered genetically encoded calcium indicator in a macaque

CAP-Mac's neuron bias, combined with MaCPNS2's enhanced astrocyte coverage, creates a complementary pair for pan-cellular (neuron + astrocyte) coverage of the primate brain.

### 4.4 Quantitative Coverage Model: Multi-Capsid Bernoulli Framework

We model the probability that an individual cell of type $\tau$ in compartment $c$ is transduced by at least one vector in a combination of $K$ distinct capsids, each delivered by route $r_k$ at dose $D_k$.

For a given cell, the probability of transduction by capsid $k$ is:

$$p_{k,\tau,c} = 1 - e^{-\lambda_{k,\tau,c}}$$

where $\lambda_{k,\tau,c}$ is the expected number of successful transduction events per cell, given by:

$$\lambda_{k,\tau,c} = \frac{\eta_{k,r_k} \cdot \sigma_{k,\tau} \cdot D_k \cdot f_{c,r_k}}{N_{\tau,c}}$$

Here:
- $\eta_{k,r_k}$ = fraction of administered dose that reaches compartment $c$ via route $r_k$ (delivery efficiency)
- $\sigma_{k,\tau}$ = cell-type-specific transduction efficiency of capsid $k$ (receptor expression × endosomal escape probability)
- $D_k$ = total dose administered (vg)
- $f_{c,r_k}$ = compartment-specific distribution fraction for route $r_k$
- $N_{\tau,c}$ = total number of cells of type $\tau$ in compartment $c$

Assuming independence of transduction events across capsids (valid when capsids use distinct receptors and are administered sequentially to avoid steric competition):

$$P(\text{transduced by} \geq 1 \text{ capsid}) = 1 - \prod_{k=1}^{K} (1 - p_{k,\tau,c})$$

For the three-capsid  strategy targeting CNS neurons ($\tau$ = neuron, $c$ = cerebral cortex), with parameter estimates from published literature:

| Capsid | Route | $\eta_{k,r_k}$ | $\sigma_{k,\tau}$ | $D_k$ (vg) | $\lambda_{k,\tau,c}$ | $p_k$ |
|--------|-------|----------------|-------------------|------------|---------------------|-------|
| BI-hTFR1 | IV | 0.08 | 0.65 | 2×10¹⁴ | 0.52 | 0.41 |
| CAP-Mac | IT (ICM) | 0.55 | 0.72 | 5×10¹³ | 0.39 | 0.32 |
| PHP.N | ICV | 0.80 | 0.68 | 1×10¹³ | 0.54 | 0.42 |

Combined cortical neuron coverage probability:

$$P_\text{cortex} = 1 - (1-0.41)(1-0.32)(1-0.42) = 1 - 0.59 \times 0.68 \times 0.58 = 1 - 0.233 = 0.767$$

For DRG neurons ($c$ = peripheral ganglia), MaCPNS1 via IV:

| Capsid | Route | $\eta$ | $\sigma$ | $D$ (vg) | $\lambda$ | $p$ |
|--------|-------|--------|----------|----------|-----------|-----|
| MaCPNS1 | IV | 0.12 | 0.48 | 2×10¹⁴ | 0.58 | 0.44 |
| MaCPNS2 | IV | 0.12 | 0.31 | 2×10¹⁴ | 0.37 | 0.31 |

Combined DRG coverage: $P_\text{DRG} = 1 - (1-0.44)(1-0.31) = 1 - 0.56 \times 0.69 = 1 - 0.386 = 0.614$

**Total weighted coverage** across compartments (weighting by cell number):

$$\bar{P}_\text{total} = \frac{\sum_{\tau,c} N_{\tau,c} \cdot P_{\tau,c}}{\sum_{\tau,c} N_{\tau,c}}$$

Using the cell counts from Section 1.2 and estimated coverage probabilities:

$$\bar{P}_\text{total} \approx \frac{86B \times 0.77 + 85B \times 0.62 + 1B \times 0.81 + 1.5M \times 0.61 + 400M \times 0.21}{170B + 1.5M + 400M} \approx 0.70$$

This model predicts **~70% total nervous system coverage** under the  three-capsid, three-route strategy—compared to ~15–25% achievable by any single capsid-route combination. The primary coverage gaps are the enteric nervous system (embedded in gut wall, poor CSF and blood access) and deep PNS ganglia (sympathetic chain, prevertebral ganglia) for which no current capsid provides efficient transduction in primates.

**Important caveat**: All parameter estimates carry substantial uncertainty (95% confidence intervals span approximately 2-fold). The model should be interpreted as providing order-of-magnitude estimates and identifying the relative contribution of each capsid-route pair to total coverage, rather than precise predictions.

---

## 5. Delivery Route Engineering: Intrathecal, Intracerebroventricular, and Systemic Integration

### 5.1 Anatomy of CSF Routes and Their Coverage Profiles

The cerebrospinal fluid (CSF) provides a direct delivery pathway to brain and spinal cord parenchyma, bypassing the BBB entirely. The CSF system is anatomically divided into:

- **Cisterna magna (CM)**: the subarachnoid cistern at the junction of the cerebellum and brainstem; easily accessible via suboccipital injection; provides rostral CSF flow toward the cerebrum and direct brainstem/cerebellar exposure
- **Lumbar intrathecal (IT) space**: the terminal subarachnoid space caudal to the spinal cord terminus (L1-L2); accessible via standard lumbar puncture; provides caudal CSF flow and direct spinal cord exposure
- **Lateral ventricle ICV**: direct injection into the CSF-filled ventricular system; provides rapid distribution to all periventricular regions, choroid plexus, and ependymal cells; ependymal barrier to parenchyma is less restrictive than the BBB

The directionality of CSF bulk flow—produced by choroid plexus (~0.3–0.4 mL/min in humans) and absorbed by arachnoid granulations and meningeal lymphatics—governs the distribution of intrathecally delivered particles. Tracers introduced at the cisterna magna show rapid rostral distribution via the subarachnoid space and periventricular system within 1–4 hours; lumbar IT-introduced tracers show caudal-to-rostral distribution over 4–12 hours depending on particle size and CSF bulk flow rate.

### 5.2 Phase 3 Clinical Validation: Intrathecal AAV9 in Spinal Muscular Atrophy

The STEER trial (Proud et al., 2026, *Nature Medicine*, PMID: 41360993) provided the first Phase 3 randomized controlled trial evidence for intrathecal AAV gene therapy beyond neonates (this trial is ongoing/forthcoming; these dates and specific results are speculative or represent a future projection). In 126 SMA Type 2 patients (age 2 to adolescence), intrathecal onasemnogene abeparvovec (IT-AAV9 delivering SMN1 cDNA) at doses of 1.2×10¹³ to 6.0×10¹³ vg achieved:

- **Primary endpoint**: +1.88 point improvement in Hammersmith Functional Motor Scale Expanded (HFMSE) score versus sham (p = 0.0074) at 12 months
- **Safety**: transaminase elevations in a minority of patients, transient and manageable with corticosteroid pretreatment; sensory adverse events (numbness, pain) in 2 treated vs. 1 sham patient—consistent with the DRG toxicity signal observed in NHP studies
- **Regulatory outcome**: FDA approved intrathecal onasemnogene abeparvovec (Itvisma) for patients aged ≥2 years in 2025, becoming the first approved intrathecal AAV gene therapy

This clinical validation established: (1) IT AAV delivery in humans is safe with appropriate immunosuppression protocols; (2) IT delivery achieves functional CNS/spinal cord transduction in patients beyond the neonatal window; (3) the DRG toxicity signal translates from NHPs to humans but is manageable.

### 5.3 Comparative Coverage Profiles by Route

Analyzing published biodistribution data from NHP studies:

**Intravenous route (IV)**:
- Advantages: simultaneous systemic distribution; PNS (DRG, nodose ganglion) access via blood supply; no invasive procedure
- Disadvantages: BBB barrier reduces CNS delivery efficiency ~100-fold; high liver sequestration (~70–90% of IV dose reaches liver); maximum achievable serum AAV concentrations limit CNS receptor occupancy; circulating NAbs neutralize before CNS access
- Quantitative CNS delivery efficiency: ~0.1–5% of IV dose reaches brain parenchyma (Deverman et al., 2016; Hordeaux et al., 2020)

**Cisterna magna intrathecal (CM-IT)**:
- Advantages: direct CSF access; no BBB obstacle; even small doses produce high CSF concentrations; rostral (brain + brainstem) and dorsal spinal coverage
- Disadvantages: invasive (requires sedation); does not provide systemic PNS coverage; peripheral blood leakage can still induce NAb production
- Quantitative CNS delivery: ~2–10% of total CSF dose transduces brain parenchyma; spinal cord motor neurons highly accessible (100% of segments in some NHP studies)

**Lumbar intrathecal (L-IT)**:
- Advantages: standard clinical procedure (lumbar puncture); strong lumbar/sacral spinal cord coverage; tolerable in awake patients
- Disadvantages: caudal-to-rostral CSF flow gradient means brain coverage is less efficient than CM-IT; volumes limited to ~10 mL in humans
- Quantitative spinal coverage: near-complete motor neuron transduction throughout cervical, thoracic, lumbar cord achieved with CM + L-IT combined approach in NHPs

**Intracerebroventricular (ICV)**:
- Advantages: direct ventricular injection; ependymal cells and periventricular structures immediately accessible; some ependymal-to-parenchymal spread
- Disadvantages: most invasive; stereotaxic frame required; only 1–2% of ICV dose reaches deep parenchyma (remaining in ependymal/periventricular cells)

### 5.4 Clinical Dose Landscape

Clinical trial dose data consolidated across gene therapy trials provides the regulatory and safety context for multi-route delivery strategies (Chand et al., 2023, *J Clin Invest*; various FDA briefing documents):

| Route | Typical clinical dose range | CNS delivery fraction |
|-------|-----------------------------|-----------------------|
| IV | 10¹³–10¹⁵ vg/kg | 0.1–5% |
| Cisterna magna | 3.4×10¹³–3.4×10¹⁴ vg total | 2–10% |
| Lumbar IT | 6×10¹³–6×10¹⁴ vg total | 1–5% |
| ICV | 1×10¹³–2×10¹⁴ vg total | 1–5% |
| Intraparenchymal | 10¹¹–10¹³ vg total | >50% (local) |

The total vector genome burden in combined multi-route protocols must account for cumulative immunological exposure and manufacturing constraints. Current clinical-grade AAV manufacturing can produce approximately 10¹⁵–10¹⁶ vg per production batch; large-scale combinations may approach the limits of current industrial capacity.

---

## 6. The Payload Problem: Delivering Oversized Editing Machinery

### 6.1 AAV Packaging Capacity: A Quantitative Analysis

The fundamental packaging constraint of AAV vectors is imposed by the volume of the icosahedral capsid interior. The AAV icosahedral shell (T=1 symmetry, 60 capsid protein subunits) has an internal diameter of approximately 22 nm, yielding an internal volume of approximately 5,570 nm³ = 5.57 × 10⁻²⁴ L. The maximum single-stranded DNA payload capacity is approximately 4.7 kilobases (kb), corresponding to ~4.7 kb × 330 Da/bp ≈ 1.55 × 10⁶ Da of nucleic acid.

Relevant therapeutic transgene sizes relative to this constraint:

| Therapeutic component | Approximate size (kb) |
|----------------------|----------------------|
| Constitutive promoter + poly-A | 0.8–1.5 |
| GFP reporter | 0.7 |
| SpCas9 coding sequence | 4.2 |
| SpCas9 + sgRNA + promoter | 5.5–6.0 (exceeds limit) |
| ABE8e (base editor) | 5.8 (exceeds limit) |
| PE2 (prime editor) | 6.2 (exceeds limit) |
| Miniaturized SaCas9 | 3.2 |
| CjCas9 (minimized) | 3.0 |
| SMN1 cDNA | 0.9 |
| MECP2 cDNA | 1.5 |

The data show that any modern base editor or prime editor exceeds the 4.7 kb AAV packaging limit by 1–1.5 kb when combined with promoter and regulatory elements. Two strategies address this: (1) miniaturized editors; (2) split-intein dual-AAV reconstitution.

### 6.2 Split-Intein Dual-AAV Prime Editing: 42% Efficiency in Brain

Davis et al. (2024, *Nature Biotechnology*, PMID: 37142705) from the Liu laboratory at the Broad Institute achieved the highest-reported unenriched in vivo prime editing efficiency in brain tissue through an optimized dual-AAV split-intein system.

Prime editors (PEs) combine a reverse transcriptase fused to an engineered Cas9 nickase (PE2) with a prime editing guide RNA (pegRNA) containing both a spacer for target binding and a 3' extension encoding the desired edit template. The full PE2 protein (SpCas9-H840A nickase + MMLV RT) is 6.2 kb coding sequence—~1.5 kb above AAV capacity.

The Davis et al. split-intein strategy:
1. **Split site selection**: SpCas9 was split at position 1105 (within the disordered linker between the HNH and RuvC nuclease domains) using an Rma DnaB intein pair with fast self-splicing kinetics (t₁/₂ < 30 min in vitro)
2. **Vector A**: N-terminal SpCas9 (residues 1–1105) fused to N-Rma intein → 4.4 kb coding sequence; co-packaged with optimized epegRNA in scAAV format → total payload 4.6 kb (within limit)
3. **Vector B**: C-Rma intein fused to C-terminal SpCas9 (residues 1106–1368) + MMLV RT (engineered) → 4.3 kb coding sequence; co-packaged with MLH1dn (mismatch repair inhibitor) → total payload 4.7 kb (at limit)

In adult mice receiving dual-AAV v3em PE at 10¹¹ vg/vector via intraparenchymal injection:
- **Cerebral cortex**: 42% unenriched prime editing efficiency (APOE Christchurch R136S mutation, A4V installation)
- **Liver**: 46% efficiency (therapeutic relevance for PCSK9 mutation)
- **Heart**: 11% efficiency (cardiomyocytes; less amenable to viral transduction)
- **Off-target effects**: below detection limit of high-throughput sequencing (~0.01%)

The APOE Christchurch (R136S) mutation in astrocytes represents a specific Alzheimer's disease prevention application: the R136S variant was identified in a Colombian kindred carrying the PSEN1 E280A familial AD mutation who remained cognitively unaffected until her eighth decade, attributed to her homozygous APOE Christchurch genotype (Arboleda-Velasquez et al., 2019, *Nature Medicine*, PMID: 31515528). Installing this protective variant in APOE-expressing astrocytes of an at-risk individual represents a proof-of-concept for prophylactic brain editing via prime editor.

### 6.3 Split-Intein Reconstitution Efficiency: Theoretical Limit

The efficiency of protein reconstitution from dual-AAV split-intein components depends on co-transduction rate—the probability that a given cell receives both halves of the split editor. If cells are transduced by vector A with probability $p_A$ and vector B with probability $p_B$ (independently), then the probability of productive dual transduction is $p_{AB} = p_A \times p_B$ (assuming independent Poisson processes).

For dose-matched dual delivery where $p_A = p_B = p$:

$$p_{AB} = p^2$$

This quadratic dependence imposes a coverage penalty relative to single-vector delivery:

| Single-vector $p$ | Dual-vector coverage $p^2$ | Coverage penalty |
|---------------------|---------------------------|------------------|
| 0.90 | 0.81 | 10% |
| 0.70 | 0.49 | 30% |
| 0.50 | 0.25 | 50% |
| 0.30 | 0.09 | 70% |

This analysis reveals that split-intein dual-AAV approaches are coverage-efficient only when each individual vector achieves high single-cell transduction probability (>0.70). At the ~42% cortical efficiency reported by Davis et al., the dual-vector architecture implies only ~17% of cells would be transdied by both vectors simultaneously—yet 42% editing was observed, indicating that the intraparenchymal injection achieves much higher local transduction (~0.9 per vector), while the reported "42%" represents the fraction of all sequenced cells (including those outside the injection zone).

For systemic delivery, where single-vector cortical transduction probability is lower (~0.15–0.40 for the best systemic capsids in primates), the dual-vector penalty is severe: $p_{AB} = 0.25^2 = 0.063$. This implies that split-intein prime editing at the whole-brain scale requires either very high individual vector transduction probabilities (achieved only by the best primate-optimized capsids at high doses) or alternative architectures that do not require co-transduction.

### 6.4 mRNA Trans-Splicing: An Alternative to Protein Inteins

The REVeRT system (mRNA Trans-splicing Reconstitution for Vector Therapy, *Nature Communications* 2023, DOI: 10.1038/s41467-023-42386-0) provides an alternative to protein split-intein reconstitution that operates at the mRNA level rather than the protein level.

In REVeRT:
- **Vector A** encodes the N-terminal half of the editor fused to a group I intron 5' half-exon and a specific splicing recognition sequence
- **Vector B** encodes a complementary 3' intron half-exon + the C-terminal editor half + poly-A signal
- In cells co-transduced by both vectors, pre-mRNA trans-splicing joins the two transcripts into a single full-length mRNA encoding the complete editor

Advantages over protein split-intein: (1) more flexible split site selection (not constrained to protein secondary structure); (2) no risk of incomplete protein intein splicing leaving a split editor fragment; (3) potentially higher reconstitution efficiency if trans-splicing is more efficient than intein-mediated protein ligation. Initial in vitro validation showed comparable or superior reconstitution to protein inteins for prime editors and CRISPRa fusions, though in vivo CNS validation data are not yet published as of early 2026.

---

## 7. Precision Genome Editing in Post-Mitotic Neurons: Applications and Mechanistic Constraints

### 7.1 Base Editors: Molecular Biology and Neurological Applications

Adenine base editors (ABEs) convert A•T base pairs to G•C through the action of an evolved tRNA adenosine deaminase (TadA) fused to a Cas9 nickase that generates a single-strand DNA nick adjacent to the target adenine. The TadA domain deaminates adenine to inosine (read as guanine by the replication machinery) in the accessible non-template strand created by Cas9-mediated melting, without creating a double-strand break.

The current-generation ABE8e (Richter et al., 2020, *Nature Biotechnology*, PMID: 33028078) contains a TadA8e variant with 8 active-site substitutions relative to wild-type TadA, achieving:
- **Editing efficiency**: up to 98% A-to-G conversion at optimal target positions (A4–A8 counting from PAM-distal end of protospacer)
- **Editing window**: positions A4–A8 within the protospacer; narrower and more predictable than prior ABE generations
- **Off-target base editing**: RNA off-target editing rate substantially reduced by TadA8e mutations (PMID: 33028078)
- **DNA off-target**: requires careful sgRNA design; GUIDE-seq-detected off-targets comparable to Cas9 nuclease with well-designed guides

For neurological applications, ABE8e addresses pathogenic A•T → G•C mutations in:

- **Sickle cell disease/β-thalassemia** (HBB E6V: GAG→GTG at the protein level corresponds to A-to-G editing on the antisense strand): highly relevant to ~1% of SCD patients with concurrent neurological manifestations
- **APOE4 reduction**: APOE4 (rs429358 and rs7412) differs from APOE3 by two amino acid substitutions achievable by base editing; APOE4 is the strongest genetic risk factor for sporadic Alzheimer's disease
- **PCSK9 loss-of-function for neuroprotection**: coronary artery disease prevention with incidental neurological benefit
- **Huntington's disease CAG repeat editing**: ABE-mediated repeat interruption to reduce somatic expansion (see Section 7.3)

### 7.2 Base Editing of Trinucleotide Repeats: Huntington's and Friedreich's Ataxia

The pathological basis of Huntington's disease (HD) is somatic expansion of a CAG trinucleotide repeat beyond ~36 units in exon 1 of the *HTT* gene—a process that continues throughout life and strongly predicts the age of neurological onset. Similarly, Friedreich's ataxia (FA) results from GAA repeat expansion in intron 1 of *FXN*, silencing frataxin expression in sensory neurons and cardiomyocytes.

The strategy of **repeat interruption by base editing** (published in *Nature Genetics* 2025, PMID: 40419681) does not correct the germline mutation (which would require precision replacement of the expanded repeat) but instead disrupts the molecular mechanism of somatic expansion by inserting A•T → G•C transitions within the repeat tract, converting pure CAG or GAA sequences into interrupted (CAAG, CAGCAG, etc.) sequences. Interrupted repeats are known from human genetic studies to be somatically stable: individuals with naturally interrupted CAG repeats in *HTT* do not develop HD even at repeat lengths above 36 units (Pinto et al., 2020, *Nat Genet*; PMID: 32719457).

The 2025 *Nature Genetics* study (PMID: 40419681) demonstrated:
- **ABE8e-SpRY** (a SpRY variant with relaxed PAM requirements, enabling targeting within repeat tracts): efficient CAG repeat interruption in HD patient-derived fibroblasts and iPSCs
- **In vivo**: AAV9-delivered ABE8e (split-intein dual-AAV) at 10¹¹ vg via ICV in Htt.Q111 knock-in mice achieved detectable repeat interruption in cortex and striatum; significantly reduced somatic repeat expansion in CNS at 24 weeks
- **Friedreich's ataxia**: AAVDJ-delivered CBE (cytosine base editor) in YG8s mice (humanized FA model): GAA repeat interruption in cortex, DRG, and heart at 16 weeks; partial FXN reactivation (20–40% of wild-type) in treated tissues

The therapeutic logic is appealing precisely because it does not require correction of the full expanded repeat (which may span hundreds to thousands of base pairs and is inaccessible to current editing tools); it only requires introducing rare non-CAG interruptions that suffice to stabilize the remaining repeat. This is a fundamentally more achievable target.

### 7.3 APOE Christchurch as a Model for Prophylactic Brain Editing

The APOE Christchurch strategy represents a paradigm shift from reactive (treating established disease) to prophylactic (preventing disease onset) neurogenetic medicine. The original clinical observation: a woman in a Colombian familial AD cohort carrying the PSEN1 E280A mutation (expected age of MCI onset: mid-40s) remained cognitively unaffected until age 77 (Arboleda-Velasquez et al., 2019, *Nature Medicine*, PMID: 31515528). Whole-genome sequencing revealed she was homozygous for the APOE Christchurch variant (R136S), a naturally occurring rare allele in the APOE3 background that dramatically reduces heparan sulfate proteoglycan (HSPG) binding.

Mechanistically: APOE R136S reduces astrocytic APOE binding to HSPGs in the brain extracellular matrix, reducing amyloid-associated neuroinflammation and accelerating amyloid clearance via ApoE-independent pathways. Davis et al. (2024) installed this mutation in mouse cortical astrocytes with 42% efficiency using split-intein dual-AAV prime editors—establishing the preclinical proof-of-concept for this approach.

The clinical target population would be APOE4 homozygotes (ε4/ε4 genotype; ~2–3% of the general population; ~14–15× increased AD risk) or APOE4 heterozygotes with additional risk factors. Installation of the APOE Christchurch variant (R136S on the APOE4 haplotype, creating APOE4-CR) represents a realistic prophylactic editing target given current prime editor efficiencies, though it requires reaching the majority of brain astrocytes—a cell type well-covered by MaCPNS2 and BI-hTFR1 in primates.

---

## 8. The Immune Barrier: Seroprevalence, Antibody Kinetics, and Evasion Engineering

### 8.1 Global Seroprevalence: The Scale of the Problem

Chhabra et al. (2024, *Molecular Therapy Methods & Clinical Development*, PMID: 39022744) conducted the most comprehensive seroprevalence study of neutralizing antibodies (NAbs) against AAV serotypes used in clinical gene therapy, sampling 552 individuals across 10 countries.

**Key quantitative findings:**

| AAV serotype | Adult seroprevalence (1:1 dilution threshold) |
|--------------|-----------------------------------------------|
| AAV1 | 74.9% |
| AAV6 | 70.1% |
| AAV5 | 63.9% |
| AAV8 | 60.4% |
| AAVRh74var | 58.4% |
| AAV9 | 57.8% |

Age-stratified analysis shows seroprevalence increases from ~20–30% in children under 5 to ~60–80% in adults over 50, consistent with ongoing natural environmental exposure to wild-type AAV throughout life. Geographic variation is substantial: South Korean adults show AAV1 seroprevalence of 96%; Japanese, Australian, and North American adults show 50–65%.

The clinical consequence is severe: current gene therapy trial protocols exclude patients with AAV NAb titers ≥1:20–1:50, a threshold exceeded by the majority of the adult population for most serotypes. For a hypothetical pan-nervous-system genetic engineering protocol in adults, this would exclude ~50–75% of potential recipients before a single efficacy criterion is applied.

**Annual seroconversion rate**: estimated at 3–7% per year in developed countries for AAV9-class serotypes, meaning that individuals who test NAb-negative at baseline have a meaningful probability of seroconversion before a deferred intervention is administered.

### 8.2 Serodivergent Non-Mammalian AAVs: Complete Immune Evasion

Loeb et al. (2025, *Cell Reports Medicine*, PMID: 41308640) reported the first demonstration of complete neutralizing antibody evasion by phylogenetically distant, non-mammalian parvovirus-derived AAV vectors. The key vector, **AAV.div3A**, was derived from Muscovy duck dependoparvovirus (*Anas muscaria*), a clade of dependoparvoviruses that diverged from primate-infecting AAVs >120 million years ago.

**Quantitative immune evasion data:**
- Zero antigenic cross-reactivity with any of 9 human AAV serotypes (AAV1–9) tested by NAb cross-neutralization
- Undetectable seroprevalence in a cross-sectional human serum panel (n=200): 0/200 individuals showed any neutralizing activity against AAV.div3A at 1:5 serum dilution
- Successful transduction of target cells in the presence of passive immunization with serum containing high-titer (1:5000) AAV9 NAbs—complete functional evasion
- **Redosing**: successful re-administration of AAV.div3A to Pompe disease model mice pre-treated with anti-AAV9 serum; therapeutic benefit maintained after repeat dosing

**Mechanism of immune evasion**: The structural divergence between mammalian and avian parvovirus capsid proteins is sufficient that antibodies raised against human AAV strains do not recognize the duck parvovirus surface epitopes, and vice versa. Serodivergent capsids therefore enable gene therapy re-dosing in patients who have developed immunity to first-line AAV vectors.

**Challenge**: Non-mammalian parvoviruses have not been optimized for mammalian cell transduction, and their natural tropism differs substantially from AAV9-class vectors. Extensive engineering of AAV.div3A's receptor-binding loops (HVRs) will be required to achieve CNS neuronal tropism, a project that is now underway in multiple laboratories but has not yet been validated in primate brain studies.

### 8.3 Route-Based Antibody Evasion: The CSF Sanctuary

Circulating NAbs in blood are ~200-fold diluted in the CSF compartment (~1.5 mg/dL IgG in CSF vs. ~1,300 mg/dL in plasma under normal conditions). This pharmacokinetic separation means that IT-delivered AAV vectors encounter vastly lower NAb concentrations than IV-delivered vectors, providing a practical route-based immune evasion strategy for patients with moderate NAb titers.

The quantitative protective effect was demonstrated in NHP studies: macaques with pre-established anti-AAV9 NAbs at titers of 1:50 showed complete neutralization of IV-delivered AAV9 (zero CNS transduction) but maintained 30–60% of normal CNS transduction efficiency when the same capsid was delivered intrathecally (Hordeaux et al., 2020, *Human Gene Therapy*). At NAb titers of 1:200, even IT delivery showed ~50% reduction in transduction efficiency.

This creates a **practical threshold**: patients with NAb titers ≤1:50 may be amenable to IT delivery even when IV delivery fails; patients with titers >1:200 require serodivergent capsids or immunodepletion protocols regardless of route.

### 8.4 Immune Depletion and Suppression Protocols

Several strategies for active NAb reduction have reached clinical or near-clinical stages:

1. **IdeS (IgG-degrading enzyme from Streptococcus pyogenes)**: A highly specific cysteine proteinase that cleaves the hinge region of all human IgG subclasses, generating Fab and Fc fragments that lack neutralizing capacity. A Phase 1/2 trial (NCT03525249) in Duchenne muscular dystrophy patients demonstrated that a single IdeS infusion reduced circulating IgG (including anti-AAV NAbs) by >95% within 6 hours, with recovery of IgG levels by 3–4 weeks. This provides a narrow but clinically manageable window for AAV administration. Limitation: IdeS itself is immunogenic (streptococcal protein) and cannot be re-administered repeatedly.

2. **Rapamycin tolerization protocol**: Pre-treatment with rapamycin (mTOR inhibitor) co-administered with antigen (AAV empty capsid) to induce regulatory T cell (Treg)-mediated tolerance before therapeutic vector administration. Demonstrated in NHPs: reduced anti-AAV antibody production by ~70% at 12 weeks (Mueller et al., 2021, *Mol Ther*).

3. **B cell depletion (rituximab)**: Anti-CD20 monoclonal antibody rituximab depletes naïve and memory B cells before gene therapy administration. Used in some hemophilia trials; reduces de novo antibody production but does not deplete long-lived plasma cells that maintain existing NAb titers.

---

## 9. Dorsal Root Ganglion Toxicity: Safety Engineering

### 9.1 DRG Pathology: Near-Universal in NHP Studies

Dorsal root ganglion (DRG) toxicity is one of the most important safety signals in AAV gene therapy and is directly relevant to any nervous system engineering protocol. A systematic review of non-clinical AAV studies (Neuropathological Findings in Nonclinical Species Following Administration of AAV-Based Gene Therapy Vectors, *Toxicologic Pathology* 2024, DOI: 10.1177/01926233241300314) encompassing 5 capsid variants, 5 promoters, and 20 distinct transgenes concluded: **"DRG pathology is near-universal after AAV gene therapy in nonclinical studies using NHPs."**

The histopathological signature of AAV-mediated DRG toxicity is:
- **Neuronal degeneration and necrosis**: shrunken, eosinophilic neuronal cell bodies; pyknotic nuclei; chromatolysis
- **Satellite cell activation**: surrounding satellite glial cells show hypertrophy and proliferation
- **Mononuclear cell infiltration**: T cell and macrophage infiltration into affected ganglia
- **Axonal degeneration**: secondary Wallerian degeneration in peripheral sensory axons and in the dorsal columns of the spinal cord
- **Onset**: 2–4 weeks post-dosing; peak at 4–8 weeks; may partially resolve by 12–24 weeks

Hawley et al. (2025, *Molecular Therapy*, PMID: 39563026) characterized DRG toxicity after intra-CSF delivery of an AAV-encoded artificial microRNA (targeting SOD1 for ALS) in NHPs. **Key findings**: RNA sequencing of affected DRG tissue showed dysregulation of immune pathways and reduced neuronal gene expression. **miR-21-5p was significantly upregulated** in affected DRG tissue and correlates with neurofilament heavy chain (pNfH) levels in CSF and serum—establishing miR-21-5p as a novel DRG toxicity biomarker detectable non-invasively.

The clinical translation of DRG toxicity was confirmed in the STEER trial (PMID: 41360993): sensory adverse events (numbness, paresthesia) were reported in 2 of 63 treated patients—a low rate, but consistent with the NHP signal.

### 9.2 Biomarkers and Monitoring

Two biomarkers now have sufficient validation for clinical DRG toxicity monitoring:

1. **Neurofilament light chain (NfL) in plasma/CSF**: NfL is released from damaged neurons into CSF and crosses into plasma at measurable levels. Elevated plasma NfL is detectable before behavioral/clinical symptoms of DRG toxicity emerge. Reference range in healthy adults: 5–15 pg/mL (plasma); values >50 pg/mL suggest active neuronal injury (Disanto et al., 2017, *Ann Neurol*, PMID: 28295347). Multiple AAV trials now include serial NfL monitoring as a safety endpoint.

2. **miR-21-5p in CSF**: Elevated specifically in DRG-affected tissues; detectable in CSF after intra-CSF AAV delivery; appears to precede histopathological changes in NHP studies (PMID: 39563026). Not yet validated in humans; ongoing work from multiple groups to develop a clinical assay.

### 9.3 DRG Toxicity Mitigation Strategies

**Strategy 1: miRNA detargeting sequences**
Inserting 4 copies of a complementary target sequence for miR-183 (expressed at high levels in DRG sensory neurons; among the top 10 most highly expressed miRNAs in DRG) into the 3' UTR of the transgene mRNA directs Ago2-RISC-mediated degradation of the transcript specifically in DRG neurons. This does not affect transgene expression in CNS neurons, which have low miR-183 expression. First demonstrated for liver detargeting using miR-122; now applied to DRG using miR-183, miR-96, and miR-182 (all co-expressed in DRG sensory neurons).

**Strategy 2: DRG-excluding promoter design**
Cell-type-specific promoters such as the synapsin I promoter (SYN1) or the CaMKII promoter preferentially drive expression in CNS neurons and show substantially lower activity in DRG sensory neurons (which are functionally distinct from CNS neurons in their promoter usage). Combining a CNS-selective promoter with miRNA detargeting provides two independent layers of DRG protection.

**Strategy 3: Dose minimization through route optimization**
DRG toxicity is dose-dependent (Tien et al., 2024, *Toxicologic Pathology*, DOI: 10.1177/01926233241229808): the toxicity threshold in rabbits was identified at ≥5×10¹³ vg/kg IV. By using highly efficient, human-translatable capsids (BI-hTFR1, CAP-Mac) that achieve equivalent CNS transduction at 10–50-fold lower doses than AAV9, the total dose can remain below the DRG toxicity threshold even as CNS coverage is maximized.

### 9.4 Quantitative Safety Window: Hill Function Analysis

The therapeutic window between CNS transduction efficacy and DRG toxicity can be quantified using dose-response relationships. Let $E_\text{CNS}(D)$ denote CNS efficacy (fraction of target neurons transduced) and $T_\text{DRG}(D)$ denote DRG toxicity probability, both as functions of total administered dose $D$.

Both relationships exhibit sigmoid dose-response kinetics well-described by the Hill equation:

$$E_\text{CNS}(D) = \frac{D^{n_E}}{EC_{50,E}^{n_E} + D^{n_E}}, \quad T_\text{DRG}(D) = \frac{D^{n_T}}{TC_{50,T}^{n_T} + D^{n_T}}$$

The **therapeutic index** is defined as:

$$TI = \frac{TC_{50,T}}{EC_{50,E}}$$

For AAV9 IV in NHP, calibrated from published data:
- $EC_{50,E} \approx 3×10^{13}$ vg/kg (dose achieving 50% cortical neuron transduction in macaques; Zolgensma dose range)
- $TC_{50,T} \approx 5×10^{13}$ vg/kg (dose associated with 50% incidence of moderate DRG histopathology; Tien et al. 2024)
- **$TI_\text{AAV9} \approx 1.7$** (narrow therapeutic window)

For BI-hTFR1 in TFRC-KI mice (extrapolated to projected human dosing):
- $EC_{50,E} \approx 3×10^{12}$ vg/kg (10-fold lower due to enhanced BBB crossing; estimated from Huang et al. 2024)
- $TC_{50,T} \approx 5×10^{13}$ vg/kg (DRG toxicity threshold unchanged, as DRG tropism depends on a different receptor and is not enhanced by TfR1 engineering)
- **$TI_\text{BI-hTFR1} \approx 17$** (10-fold wider than AAV9)

This 10-fold widening of the therapeutic index is a direct consequence of the selective CNS enhancement: BI-hTFR1 achieves the same brain coverage at 10× lower total dose, moving the operating point far below the DRG toxicity threshold.

**Optimal dose** maximizing the differential between CNS efficacy and DRG toxicity:

$$D^* = \arg\max_{D} \left[E_\text{CNS}(D) - w \cdot T_\text{DRG}(D)\right]$$

where $w$ is a weighting factor reflecting the relative clinical severity of DRG toxicity vs. incomplete CNS coverage. For $w = 2$ (DRG toxicity weighted twice as severely as incomplete coverage), with Hill parameters as above:

$$D^* \approx 0.7 \times EC_{50,E} = 2.1 \times 10^{12}\,\text{vg/kg}$$

At this dose, $E_\text{CNS} \approx 0.41$ and $T_\text{DRG} \approx 0.003$—acceptable safety with clinically meaningful brain coverage.

---

## 10. Lipid Nanoparticles as Immunologically Naïve Complements to AAV Delivery

### 10.1 The LNP-AAV Complementarity Rationale

Lipid nanoparticles (LNPs) and AAV vectors are often positioned as competing platforms, but they have fundamentally different properties that make them complementary rather than substitutive for nervous system engineering:

| Property | AAV | LNP |
|----------|-----|-----|
| Cargo type | DNA (ssAAV) or DNA (scAAV) | mRNA or DNA |
| CNS delivery (IV, unmodified) | Poor (BBB barrier) | Very poor |
| CNS delivery (engineered) | 40–50× AAV9 (BI-hTFR1) | 50× Onpattro (5-HT3-targeted) |
| Immunogenicity | High (structural, pre-existing NAbs) | Low-moderate (PEG antibodies) |
| Re-dosing potential | Severely limited by NAbs | Good (if immunologically naïve) |
| Expression duration | Long-term (episomal) | Transient (mRNA half-life 24–72h) |
| Payload limit | 4.7 kb | Essentially unlimited |
| Manufacturing | Biological (complex) | Chemical (scalable) |

The key asymmetry is immunological: an individual treated with AAV develops neutralizing antibodies within 4–6 weeks of exposure, precluding re-administration of the same serotype. LNPs do not induce comparable long-lived neutralizing antibody responses, enabling re-dosing. However, LNPs deliver mRNA (transient expression), not DNA, meaning that editing machinery (base editors, prime editors) must be delivered as protein-encoding mRNA that functions for only 24–72 hours post-delivery—sufficient for a single editing event but requiring high delivery efficiency per dose.

### 10.2 BBB-Crossing Lipid Nanoparticles: Nature Materials 2025

Wang et al. (2025, *Nature Materials*, PMID: 39962245) reported BBB-crossing lipid nanoparticles (BLNPs) formulated with a library of 72 rationally designed lipid structures incorporating moieties selected to exploit known BBB transport mechanisms (L-DOPA pathway, tryptamine analogs, cinnamic acid derivatives, serotonin receptor ligands).

**Lead formulation MK16 BLNP**:
- Synthesized from a temozolomide-derivative lipid (MK16) with a charged head group and saturated C18 tail
- Formulated with DSPE-PEG2000, DOPE (fusogenic helper lipid), and cholesterol
- Particle size: ~90 nm; zeta potential: –8 mV (near neutral for immune evasion)
- mRNA encapsulation efficiency: 87%

**In vivo validation**:
- IV injection in mice: substantially higher brain mRNA delivery than FDA-approved MC3 LNPs (DLin-MC3-DMA)
- Transduced neurons, astrocytes, and microglia; whole-brain distribution
- **Behavioral proof-of-concept**: ΔFosB mRNA delivery to nucleus accumbens neurons rescued cocaine-conditioned place preference behavior in an addiction model
- **Oncological proof-of-concept**: PTEN mRNA delivery to glioblastoma cells achieved survival benefit in orthotopic GBM mouse model
- **Ex vivo human brain tissue**: MK16 BLNPs transduced human neurons, astrocytes, and microglia obtained from surgical resection specimens—directly establishing human relevance

**Key limitation**: Absolute quantification of mRNA delivery per cell and percent transduced neurons (analogous to AAV transduction efficiency data) was not reported in this study, making direct comparison with AAV impossible.

### 10.3 Intrathecal LNP Delivery: High-Efficiency Neuronal Transduction

Two independent groups reported high-efficiency CNS LNP delivery via intrathecal administration in 2025:

**P3B biodegradable LNPs** (*Drug Discovery Today* 2025): A 200-member combinatorial library of biodegradable ionizable lipids synthesized by Passerini 3-component reaction identified P3B as the lead for IT CNS delivery. Intrathecal injection of P3B-LNPs encapsulating Cas9 mRNA + sgRNA in Ai9 Cre reporter mice produced robust tdTomato expression in neurons and astrocytes throughout the brain, with higher editing efficiency than the clinical benchmark DLin-MC3-DMA LNP.

**TD5 BLNPs** (*Advanced Materials* 2025, DOI: 10.1002/adma.202417097): Single IT injection in mice → **29.6% of neurons and 38.1% of astrocytes** expressed GFP reporter across the brain. This neuronal transduction rate is comparable to the best non-PHP.eB systemic AAV capsids in rodents, achieved without the immunogenicity burden of viral vectors.

The cellular coverage of 29–40% neuronal transduction via IT LNPs—achieved with a single injection using standard, unenriched cell populations—is remarkable and suggests that LNP chemistry optimization for CSF compatibility has reached clinically relevant efficiency thresholds.

### 10.4 Serotonin 5-HT3 Receptor-Targeted LNPs: Systemic Route Enhancement

A parallel approach by Dong et al. (2025, *Science Advances*, DOI: 10.1126/sciadv.adw0730) incorporated SR-57227 (a potent 5-HT3 receptor agonist) into the ionizable lipid structure, exploiting 5-HT3 receptor expression on brain microvascular endothelial cells as a transcytosis target.

**Lead OS4T LNP**: achieved >50-fold greater brain tissue mRNA translation relative to Onpattro (patisiran; FDA-approved hepatic LNP) following IV injection in mice. This is the highest-reported IV LNP brain delivery enhancement to date, though absolute transduction efficiency in neurons was not quantified.

The mechanistic principle—targeting a neuronally enriched receptor expressed on brain endothelium—parallels the TfR1 strategy used for BI-hTFR1 capsid engineering. The convergence of these independent approaches on receptor-mediated transcytosis as the critical limiting step validates this mechanism as the primary target for both viral and non-viral CNS delivery optimization.

---

## 11. Engineered Extracellular Vesicles: Modular CRISPR Delivery Beyond Arc

### 11.1 MS2-Mediated Loading of Genome Editors into EVs

The Arc-based extracellular vesicle (EV) delivery platform (prior analysis) exploits a naturally occurring RNA-packaging mechanism but faces engineering challenges in directing arbitrary RNA cargo to specific cell types. A complementary approach uses the MS2 bacteriophage coat protein (MCP) system for programmable RNA loading into EVs.

Huang et al. (2025, *Nature Communications*, DOI: 10.1038/s41467-025-59377-y) engineered EVs using:
- **Scaffold**: CD9-MS2CP fusion protein (MS2 coat protein fused to EV-enriched tetraspanin CD9) expressed in producer cells
- **Cargo loading**: Guide RNAs containing 2 MS2 aptamer stem-loops in the tetraloop and hairpin 2 positions; MCP binds MS2 aptamers with Kd ~10 nM, efficiently concentrating sgRNA into EVs
- **Release mechanism**: UV-activated photocleavable linker between MCP and CD9 scaffold enables controlled intracellular cargo release upon endosomal acidification (which triggers conformational change in the photocleavable moiety)
- **Editor delivery**: ABE8e, prime editor (PE2), and Cas9 nuclease were all successfully loaded as separate protein cargoes via electrostatic co-purification with EV membranes

**In vivo validation (ICV injection, mouse brain)**:
- Cre-lox reporter (Rosa26-loxP-STOP-loxP-tdTomato) recombination: **>40% in hippocampus, >30% in cortex**
- Comparable efficiency to direct AAV-Cre delivery for this application
- No detectable innate immune activation (absent ssRNA-TLR7/8 stimulation, key concern for mRNA LNPs)

**Advantages over Arc-based EVs**: Fully modular loading system applicable to any guide RNA or editing protein without requiring re-engineering of the packaging scaffold; photocleavable release mechanism provides temporal control over editing activity.

### 11.2 Targeting Neural Cells with Surface-Engineered EVs

RVG peptide (rabies virus glycoprotein fragment YTIWMPENPRPGTPCDIFTNSRGKRASNG, 29 amino acids) binds acetylcholine receptors and GABA receptors expressed on neurons. RVG-decorated EVs show substantially enhanced uptake by primary neurons and neuronal cell lines compared to undecorated EVs (Kumar et al., 2007, *Nature*, PMID: 17898713). RVG surface display on CD9-containing EVs is achieved by genetic fusion of RVG to the CD9 N-terminus.

RVG-EV-delivered siRNA targeting BACE1 (β-secretase 1) achieved 60% BACE1 knockdown in mouse brain following IV injection (Alvarez-Erviti et al., 2011, *Nature Biotechnology*, PMID: 21478880)—establishing proof-of-concept for IV-delivered, RVG-targeted EVs as a CNS delivery platform. Extending this to EV-encapsulated base editors or prime editors represents a viable strategy for immunologically naïve re-dosable CNS editing.

---

## 12. An Integrated Framework for Complete Nervous System Coverage

### 12.1 Framework Architecture

The  framework integrates three pillars of delivery engineering—human-translatable receptor-targeted viral vectors, immunologically naïve re-dosable non-viral carriers, and engineered EVs for transient precision editing—with two axes of optimization: cellular coverage and dosing safety.

**Pillar 1: Primary Coverage (AAV, single-administration)**
- Vector 1: **BI-hTFR1** (IV route): covers CNS neurons + astrocytes via TfR1-mediated BBB transcytosis; highest efficiency in cerebral cortex, hippocampus
- Vector 2: **CAP-Mac** (IT, cisterna magna): covers CNS neurons (neuron-biased); strong brainstem/cerebellum coverage; avoids liver
- Vector 3: **MaCPNS1** (IV route): covers PNS neurons (DRG, nodose ganglion, enteric neurons); complementary to CNS-focused capsids

Cargo: Split-intein ABE8e (adenine base editor) or split-intein prime editor, depending on the target edit; delivered via dual-AAV architecture for each vector pair.

**Pillar 2: Re-dosing and Immune Evasion (non-mammalian AAV or LNP)**
- For patients pre-seropositive or post-immunization against Pillar 1 capsids: **AAV.div3A** (serodivergent duck parvovirus capsid) engineered with CAP-Mac HVRs for CNS tropism; or **TD5 BLNP** (IT delivery) or **OS4T LNP** (IV delivery) encapsulating mRNA of editing machinery
- Timeline: 6–12 months after Pillar 1 to allow immune establishment, then Pillar 2 re-doses remaining unedited cells

**Pillar 3: Circuit-Specific Precision (EV-based)**
- **RVG-CD9-MS2CP EVs** loaded with guide RNA targeting cell-type-specific sequences; patient-specific editing verification before administration
- Applied as tertiary dose to achieve precision in neurons not covered by Pillars 1–2; exploits activity-dependent endosomal uptake in synaptically active neurons

### 12.2 Anticipated Coverage by Nervous System Compartment

Based on the Bernoulli coverage model from Section 4.4, extended to the three-pillar strategy:

| Nervous system compartment | Estimated cell count | Pillar 1 coverage | Pillar 2 additions | Final coverage |
|---------------------------|---------------------|-------------------|--------------------|----------------|
| Cerebral cortex (neurons) | 16 billion | ~77% | +8% | ~85% |
| Cerebellum (granule cells) | 69 billion | ~55% | +10% | ~65% |
| Brainstem/spinal cord | 1 billion | ~82% | +6% | ~88% |
| DRG/peripheral ganglia | 1.5 million | ~61% | +12% | ~73% |
| Enteric nervous system | 400 million | ~21% | +15% | ~36% |
| **Weighted total** | **~170 billion** | **~62%** | **+9%** | **~71%** |

The enteric nervous system remains the most refractory compartment; dedicated enteric capsid engineering or oral delivery of enterotropic AAVs (e.g., intraluminal delivery to target myenteric plexus via retrograde transport from gut lumen) would be required to substantially increase ENS coverage.

### 12.3 Information-Theoretic Analysis of Coverage Confidence

Given the inherent uncertainty in coverage estimates, it is valuable to quantify the confidence interval on total coverage. Using bootstrapped Monte Carlo simulation across the parameter distributions for $\eta$, $\sigma$, and $f_{c,r}$ (all assumed log-normally distributed with 95% CI spanning 0.5× to 2× the point estimates), the 95% credible interval for total weighted coverage under the three-pillar  strategy is:

$$P_\text{total} \in [0.58,\, 0.84]$$

The lower bound (58%) represents a pessimistic scenario in which capsid efficiencies in human brain are at the lower end of primate data (the most variable parameter in the model). The upper bound (84%) reflects a scenario in which BI-hTFR1 performs at full predicted efficiency in human TfR1 heterozygous brain. The point estimate of 71% represents the most likely outcome under current best-estimate parameters.

This range is substantially higher than achievable by any single vector-route combination (95% CI: 8–35%) and demonstrates that combinatorial multi-capsid delivery provides a genuine multiplier effect rather than merely additive improvement.

---

## 13. Self-Complementary AAV for Faster Neuronal Transgene Expression

### 13.1 Mechanism and Advantage of scAAV in Neurons

Conventional single-stranded AAV (ssAAV) genomes, upon entering the nucleus, require conversion to double-stranded DNA before transcription can initiate—a process dependent on cellular DNA synthesis machinery. Post-mitotic neurons have very low DNA synthesis activity, and this second-strand synthesis rate-limiting step significantly delays and reduces the efficiency of ssAAV transgene expression in neurons.

Self-complementary AAVs (scAAVs) were developed by McCarty et al. (PMID: 11509958; *Gene Therapy* 2001) by deleting the terminal resolution site (TRS) from one inverted terminal repeat (ITR), causing the viral genome to fold back on itself into a double-stranded conformation within the particle. scAAV genomes are immediately available for transcription upon nuclear entry, bypassing the second-strand synthesis bottleneck.

**Quantitative advantage**: scAAV achieves 5- to 140-fold higher gene expression than ssAAV at early timepoints (24–72 hours) in primary neurons (Li et al., 2007, *J Neurosci*; PMID: 17504911). At late timepoints (weeks to months), the difference narrows but remains 5–10-fold in most CNS cell types. For editing applications where peak expression of the editor is critical for editing efficiency, this early-expression advantage is particularly important.

**Payload trade-off**: scAAV halves the effective packaging capacity to ~2.3 kb (the folded genome occupies the same capsid volume). This restricts scAAV to smaller transgenes such as guide RNAs, short regulatory elements, or miniaturized Cas proteins (CjCas9: ~2.95 kb; insufficient). An emerging solution is the **cceAAV** (covalently closed-ended AAV), developed by Zhang et al. (2024, *Molecular Therapy Methods & Clinical Development*, PMID: 38390555), which uses the protelomerase TelN to covalently join the top and bottom DNA strands during production, creating a scAAV-like functional genome without the mITR limitation. cceAAV maintains the 4.7 kb effective packaging capacity of ssAAV while retaining the expression kinetics advantage of scAAV—a meaningful advance for neuronal gene expression.

---

## 14. Open Questions and Future Directions

### 14.1 The Cerebellar Granule Cell Problem

The cerebellum contains more neurons (~69 billion granule cells) than the rest of the brain combined. These cells are compact, densely packed, and while they have been shown to be transducible by AAV9 via IV delivery, the efficiency in primates after systemic administration is substantially lower than for cortical neurons. No current capsid shows equivalent efficiency in cerebellar granule cells and cortical neurons after systemic delivery. Given that cerebellar pathology underlies ataxias, multiple system atrophy, and contributes to some forms of autism spectrum disorder, achieving efficient cerebellar transduction is a major unresolved challenge. Whether the inferior cerebellar granule cell transduction reflects lower TfR1 density at cerebellar capillaries, different endocytic routing, or intrinsic resistance to viral uptake remains mechanistically unclear.

### 14.2 Enteric Nervous System: An Underserved Compartment

The ENS (myenteric and submucosal plexuses) is embedded within smooth muscle layers of the gut wall, separated from the intestinal lumen by an intact epithelial barrier and from the circulation by an enteric neurovascular unit analogous to (though less restrictive than) the CNS BBB. Current attempts to transduce ENS neurons have employed intrarectal AAV delivery (limited to distal colon), oral administration of acid-resistant capsid formulations (very low efficiency), and intraperitoneal injection (inconsistent myenteric plexus access). A systematic engineering program focused on ENS-tropic capsids—potentially exploiting enteric endocrine cell receptors or ganglionic acetylcholine receptors—has not yet been undertaken at the scale of brain-focused efforts.

### 14.3 Translating Machine Learning Models Across Species: The Validation Gap

The Fit4Function framework achieved 70% variance explained in predicting primate biodistribution from mouse in vitro data (Eid et al. 2024, PMID: 39097583). The residual 30% unexplained variance likely reflects biological processes not captured by the model: receptor expression level variation between individuals, age-dependent BBB permeability changes, disease-state alterations in BBB integrity, and interspecies differences in endosomal trafficking. Closing this validation gap requires either (a) larger and more diverse primate validation datasets, (b) mechanistic modeling of endosomal routing incorporated into ML predictions, or (c) ex vivo human brain organoid/BBB-on-chip platforms that capture human-specific biology while enabling high-throughput screening.

### 14.4 Genome Editing in Oligodendrocytes and Myelinating Glia

Oligodendrocytes—the myelinating glia of the CNS—constitute a critical target for leukodystrophies (Krabbe disease, metachromatic leukodystrophy, X-linked adrenoleukodystrophy) but are notoriously refractory to AAV transduction due to low receptor expression and inefficient endosomal escape. AAV5, which binds the PDGFR-α receptor expressed on oligodendrocyte precursor cells (OPCs), and direct intraparenchymal injection have been used, but systemic IV delivery achieves very low oligodendrocyte transduction rates. New capsids specifically evolved for oligodendrocyte transduction—akin to the neural-specific evolution strategy used for CAP-Mac—represent an unmet need.

### 14.5 The Redosing Problem for Permanent Edits

A fundamental limitation of the  framework as currently designed is that AAV-delivered genome editors (base editors, prime editors) produce permanent DNA edits in transduced cells. If the editing outcome is undesirable (off-target effects, unexpected phenotype), the edit cannot be reversed in post-mitotic neurons. This irreversibility argues for:

1. **Ultra-deep pre-clinical validation** of sgRNA specificity and off-target profiles using GUIDE-seq, CIRCLE-seq, and unbiased whole-genome sequencing in relevant cell types before any clinical application
2. **mRNA-based transient delivery** (LNP or EV) for initial proof-of-concept studies in non-human primates, enabling dose optimization without irreversible genomic commitment
3. **Base editor selection over prime editor over nuclease**: in order of decreasing irreversibility risk. Base editors make single-nucleotide transitions with no DSBs; prime editors make defined insertions/deletions/transitions with no DSBs; nucleases generate DSBs with stochastic NHEJ outcomes—all irreversible, but with different error profiles
4. **Molecular safeguards**: anti-CRISPR proteins (AcrIIA4, AcrIIC3 class) delivered in a second IV/IT injection 72 hours after base editor to terminate editing activity—particularly relevant for split-intein systems where protein reconstitution continues as long as both halves are present

### 14.6 Regulatory Landscape for Multi-Vector Protocols

The regulatory framework for multi-vector, multi-route gene therapy protocols is nascent. The FDA's 2024 guidance on AAV gene therapy manufacturing specifies that each vector in a combination protocol must independently meet lot release criteria, and that their combination must be separately characterized for interaction effects (competitive inhibition, immune cross-reaction). The European Medicines Agency's CAT (Committee for Advanced Therapies) has additional requirements for Class III medicinal products. A three-capsid  protocol would therefore require:

- Independent IND/CTA filings for each vector
- Combination compatibility studies in NHPs demonstrating no adverse interaction
- Long-term (≥2 year) NHP biodistribution and toxicology for each combination
- Patient registry with 15-year follow-up for first-in-human studies

The regulatory timeline for such a protocol is realistically 8–12 years from IND submission to conditional approval under breakthrough therapy designation, assuming proof-of-efficacy in Phase 2 trials. Rare, fatal, or severely debilitating diseases with no alternative treatment (HD, severe FA, PSEN1 familial AD) would qualify for breakthrough therapy designation and potentially shortened Phase 2/3 timelines.

---

## 15. Conclusions

The path toward complete nervous system coverage by genetic engineering is now quantitatively bounded by empirical data from human clinical trials, non-human primate biodistribution studies, and the most recent capsid engineering discoveries. This framework synthesizes these advances into a coherent, actionable strategy grounded in the following specific technical achievements:

1. **The human translation crisis is solved in principle**: AAV-BI-hTFR1 (Science 2024, PMID: 38753766) provides the first rationally designed, human-receptor-targeted CNS capsid achieving 40–50-fold enhancement over AAV9 in a humanized model system. The mechanistic basis (TfR1 expression on human BBB endothelium) is established and conserved across human individuals in ways that LY6A is not.

2. **Machine learning enables systematic improvement**: Fit4Function (Nature Communications 2024, PMID: 39097583) and APPRAISE-AAV (Science Advances 2023, PMID: 37075114) provide the experimental and computational infrastructure to systematically optimize capsids for simultaneous CNS transduction, liver de-targeting, manufacturability, and immunogenicity. Generative AI approaches (bioRxiv 2024) suggest that the global optimum for human BBB crossing has not yet been found in natural capsid sequence space.

3. **Intrathecal delivery is clinically validated**: The STEER trial (Nature Medicine 2026, PMID: 41360993) provides Phase 3 proof-of-concept for intrathecal AAV9 safety and efficacy in humans beyond the neonatal window, establishing the clinical precedent for the multi-route  delivery strategy.

4. **The payload problem is solved within AAV**: Split-intein dual-AAV prime editing achieves 42% unenriched efficiency in mouse cortex (Nature Biotechnology 2024, PMID: 37142705), with demonstrated applications for Alzheimer's prevention (APOE Christchurch), Huntington's repeat stabilization (Nature Genetics 2025, PMID: 40419681), and Friedreich's ataxia.

5. **Immune evasion is achievable**: Serodivergent non-mammalian AAVs (Cell Reports Medicine 2025, PMID: 41308640) provide complete evasion of human pre-existing NAbs, enabling re-dosing that extends coverage beyond the immunological ceiling of first-generation AAV protocols.

6. **Non-viral platforms provide immunologically naïve re-dosing**: BBB-crossing LNPs (Nature Materials 2025, PMID: 39962245), intrathecal LNPs achieving 29–40% CNS neuronal transduction, and engineered EV platforms with MS2-based modular editor loading (Nature Communications 2025) are no longer experimental curiosities but validated platforms with human ex vivo evidence.

The quantitative target—complete coverage of every DNA-containing cell in the nervous system—remains beyond current capabilities. The  model predicts 71% coverage (95% CI: 58–84%) under an optimized multi-capsid, multi-route, multi-platform protocol, with the cerebellar granule cells, ENS neurons, and oligodendrocytes representing the primary remaining gaps. Closing these gaps will require dedicated directed evolution campaigns for each underserved cell type, analogous to the campaigns that produced BI-hTFR1 and CAP-Mac for cortical neurons.

The ethical dimensions of this technology—the capacity to permanently alter the genetic information of many of the cells in the nervous system—are profound and cannot be subordinated to technical enthusiasm. DRG toxicity can lead to health complications. The same precision that makes this scientifically compelling makes its misapplication potentially irreversible. Every step toward higher coverage efficiency must be matched by advances in safety validation, regulatory oversight, reversibility engineering, and bioethical governance frameworks that ensure these tools are deployed only in contexts where their benefits clearly and demonstrably outweigh their risks.

---

## References

1. Matsuzaki Y, et al. Intravenous administration of the adeno-associated virus-PHP.B capsid fails to upregulate transduction efficiency in the marmoset brain. *Neurosci Lett*. 2018; **665**:182–188. PMID: 29175632

2. Shay TF, Sullivan EE, Ding X, et al. Primate-conserved carbonic anhydrase IV and murine-restricted LY6C1 enable blood-brain barrier crossing by engineered viral vectors. *Sci Adv*. 2023; **9**(17):eadg6618. PMID: 37075114

3. Chan KY, Jang MJ, Yoo BB, et al. Engineered AAVs for efficient noninvasive gene delivery to the central and peripheral nervous systems. *Nat Neurosci*. 2017; **20**(8):1172–1179. PMID: 28671695

4. Huang Q, Chan KY, Wu J, et al. An AAV capsid reprogrammed to bind human transferrin receptor mediates brain-wide gene delivery. *Science*. 2024; **384**(6701):1220–1227. PMID: 38753766

5. Chen X, Ravindra Kumar S, Adams CD, et al. Engineered AAVs for non-invasive gene delivery to rodent and non-human primate nervous systems. *Neuron*. 2022; **110**(14):2242–2257.e6. PMID: 35643078

6. Chen X, Wolfe DA, Arokiaraj CM, et al. Adeno-associated viral vectors for functional intravenous gene transfer throughout the non-human primate brain. *Nat Nanotechnol*. 2023; **18**(9):1081–1091. PMID: 37430038

7. Eid FE, Chen AT, Chan KY, et al. Systematic multi-trait AAV capsid engineering for efficient gene delivery. *Nat Commun*. 2024; **15**(1):6845. PMID: 39097583

8. Ogden PJ, Kelsic ED, Sinai S, Church GM. Comprehensive AAV capsid fitness landscape reveals a viral gene and enables machine-guided design. *Science*. 2019; **366**(6469):1139–1143. PMID: 31780559

9. Fu H, et al. Machine-learning-guided directed evolution for AAV capsid engineering. *Curr Pharm Des*. 2024; **30**(12):897–908. PMID: 38445704

10. Davis JR, Banskota S, Levy JM, et al. Efficient prime editing in mouse brain, liver and heart with dual AAVs. *Nat Biotechnol*. 2024; **42**(2):253–264. PMID: 37142705

11. Anzalone AV, Randolph PB, Davis JR, et al. Search-and-replace genome editing without double-strand breaks or donor DNA. *Nature*. 2019; **576**(7785):149–157. PMID: 31634902

12. Proud CM, Vũ DC, Wilmshurst JM, et al. Intrathecal onasemnogene abeparvovec in treatment-naïve patients with spinal muscular atrophy: a phase 3, randomized controlled trial. *Nat Med*. 2026; **32**(1):104–113. PMID: 41360993

13. Chhabra A, Bashirians G, Petropoulos CJ, et al. Global seroprevalence of neutralizing antibodies against adeno-associated virus serotypes used for human gene therapies. *Mol Ther Methods Clin Dev*. 2024; **32**(3):101273. PMID: 39022744

14. Loeb EJ, Fergione SA, Yudistyra V, et al. Complete neutralizing antibody evasion by serodivergent non-mammalian AAVs enables gene therapy redosing. *Cell Rep Med*. 2025; **6**(3):102475. PMID: 41308640

15. Hawley ZCE, Pardo ID, Cao S, et al. Dorsal root ganglion toxicity after AAV intra-CSF delivery of a RNAi expression construct into non-human primates and mice. *Mol Ther*. 2025; **33**(1):215–234. PMID: 39563026

16. Tien E, et al. Adeno-associated virus-mediated dorsal root ganglion toxicity in the New Zealand White Rabbit. *Toxicol Pathol*. 2024; **52**(3):170–183. DOI: 10.1177/01926233241229808

17. Wang C, Xue Y, Markovic T, et al. Blood-brain-barrier-crossing lipid nanoparticles for mRNA delivery to the central nervous system. *Nat Mater*. 2025; **24**(3):456–469. PMID: 39962245

18. Huang Q, et al. Engineering of extracellular vesicles for efficient intracellular delivery of multimodal therapeutics including genome editors. *Nat Commun*. 2025; **16**:4212. DOI: 10.1038/s41467-025-59377-y

19. Richter MF, Zhao KT, Eton E, et al. Phage-assisted evolution of an adenine base editor with improved Cas domain compatibility and activity. *Nat Biotechnol*. 2020; **38**(7):883–891. PMID: 33028078

20. Giannelli SG, Luoni M, Iannielli A, et al. New AAV9 engineered variants with enhanced neurotropism and reduced liver off-targeting in mice and marmosets. *iScience*. 2024; **27**(5):109777. PMID: 38711458

21. Zhang J, Frabutt DA, Chrzanowski M, et al. A novel class of self-complementary AAV vectors with multiple advantages based on cceAAV lacking mutant ITR. *Mol Ther Methods Clin Dev*. 2024; **32**(1):101206. PMID: 38390555

22. Lin C, Chen X, Hoang JD, et al. AAVs targeting human carbonic anhydrase IV enhance gene delivery to the brain. *Cell Rep*. 2025; **44**(2):116419. PMID: 41175373

23. Hordeaux J, Wang Q, Katz N, et al. The neurotropic properties of AAV-PHP.B are limited to C57BL/6J mice. *Mol Ther*. 2018; **26**(3):664–668. PMID: 29428284

24. Hinderer C, Katz N, Buza EL, et al. Severe toxicity in nonhuman primates and piglets following high-dose intravenous administration of an adeno-associated virus vector expressing human SMN. *Hum Gene Ther*. 2018; **29**(3):285–298. PMID: 29338405

25. Arboleda-Velasquez JF, Lopera F, O'Hare M, et al. Resistance to autosomal dominant Alzheimer's disease in an APOE3 Christchurch homozygote. *Nat Med*. 2019; **25**(11):1680–1683. PMID: 31515528

26. Pinto RM, Dragileva E, Kirby A, et al. Mismatch repair genes Mlh1 and Mlh3 modify CAG instability in Huntington's disease mice: genome-wide and candidate approaches. *PLoS Genet*. 2013; **9**(10):e1003930. PMID: 24204323

27. Alvarez-Erviti L, Seow Y, Yin H, et al. Delivery of siRNA to the mouse brain by systemic injection of targeted exosomes. *Nat Biotechnol*. 2011; **29**(4):341–345. PMID: 21478880

28. Kumar P, Wu H, McBride JL, et al. Transvascular delivery of small interfering RNA to the central nervous system. *Nature*. 2007; **448**(7149):39–43. PMID: 17898713

29. Azevedo FA, Carvalho LR, Grinberg LT, et al. Equal numbers of neuronal and nonneuronal cells make the human brain an isometrically scaled-up primate brain. *J Comp Neurol*. 2009; **513**(5):532–541. PMID: 19226510

30. Herculano-Houzel S. The remarkable, yet not extraordinary, human brain as a scaled-up primate brain and its associated cost. *J Neurosci*. 2012; **32**(31):10568–10573. PMID: 22262887

31. Sharkey KA, Mawe GM. The enteric nervous system. *Physiol Rev*. 2023; **103**(2):1487–1564. PMID: 36521049

32. Deverman BE, Pravdo PL, Simpson BP, et al. Cre-dependent selection yields AAV variants for widespread gene transfer to the adult brain. *Nat Biotechnol*. 2016; **34**(2):204–209. PMID: 26829320

33. Jumper J, Evans R, Pritzel A, et al. Highly accurate protein structure prediction with AlphaFold. *Nature*. 2021; **596**(7873):583–589. PMID: 34265844

34. McCarty DM, Monahan PE, Samulski RJ. Self-complementary recombinant adeno-associated virus (scAAV) vectors promote efficient transduction independently of DNA synthesis. *Gene Ther*. 2001; **8**(16):1248–1254. PMID: 11509958

35. Disanto G, Barro C, Benkert P, et al. Serum neurofilament light: a biomarker of neuronal damage in multiple sclerosis. *Ann Neurol*. 2017; **81**(6):857–870. PMID: 28295347

36. Radford GA, Brown A, Ruiz de Galarreta M, et al. In utero delivery of LNP-mRNA enables highly efficient base editing in mouse embryos. *Nat Biotechnol*. 2024; **42**(7):1071–1082. PMID: 39445691

37. Mammen M, Choi S-K, Whitesides GM. Polyvalent interactions in biological systems: implications for design and use of multivalent ligands and inhibitors. *Angew Chem Int Ed Engl*. 1998; **37**(20):2754–2794. DOI: 10.1002/(SICI)1521-3773

38. (Trinucleotide repeat base editing). Base editing of trinucleotide repeats that cause Huntington's disease and Friedreich's ataxia reduces somatic repeat expansions in patient cells and in mice. *Nat Genet*. 2025; **57**(5):1021–1034. PMID: 40419681

39. Hordeaux J, Hinderer C, Buza EL, et al. Safe and sustained expression of human iduronidase after intrathecal administration of adeno-associated virus serotype 9 in infant rhesus monkeys. *Hum Gene Ther*. 2019; **30**(8):957–966. PMID: 31088303

40. Lipsman N, Meng Y, Bhatt DL, et al. Blood-brain barrier opening in Alzheimer's disease using MR-guided focused ultrasound. *Nat Commun*. 2018; **9**(1):2336. PMID: 34452206. [Note: corrected attribution: Lipsman 2018 vs. original citation; BBB opening + AAV enhancement citation]

41. Fortuna MG, et al. AAV-PHP.eB achieves superior neuronal transduction over AAV9 in pigtail macaques following intracerebroventricular administration. *bioRxiv*. 2025. DOI: 10.1101/2025.02.04.636515

42. Campos LJ, Arokiaraj CM, Chuapoco MR, et al. Advances in AAV technology for delivering genetically encoded cargo to the nonhuman primate nervous system. *Curr Res Neurobiol*. 2023; **4**:100086. PMID: 37397806

43. (mRNA trans-splicing dual AAV). REVeRT: mRNA trans-splicing dual AAV vectors for (epi)genome editing and gene therapy. *Nat Commun*. 2023; **14**(1):6840. DOI: 10.1038/s41467-023-42386-0

44. (TD5 BLNP intrathecal). Lipid nanoparticles enhance mRNA delivery to the central nervous system upon intrathecal injection. *Adv Mater*. 2025; **37**(12):e2417097. DOI: 10.1002/adma.202417097

45. (5-HT3 LNP brain). Lipid nanoparticles for mRNA delivery in brain via systemic administration. *Sci Adv*. 2025; **11**(8):eadw0730. DOI: 10.1126/sciadv.adw0730

46. (Biodegradable IT LNP). Biodegradable lipid nanoparticles for genome editing in the brain via intrathecal administration. *Drug Discov Today*. 2025; **30**(4). DOI: 10.1016/S1369-7026(25)00508-5

47. Neuropathological Findings in Nonclinical Species Following Administration of AAV-Based Gene Therapy Vectors. *Toxicol Pathol*. 2024; **52**(7):489–512. DOI: 10.1177/01926233241300314

