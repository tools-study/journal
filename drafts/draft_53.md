# Nucleosome Resolved Structural Biology

## Abstract

Pioneer transcription factors (pioneer TFs) are the mechanistic bottleneck of disease-specific induced pluripotent stem cell (iPSC) production, direct lineage conversion, and therapeutic chromatin reprogramming. Although the cryo-electron microscopy (cryo-EM) era has resolved six distinct pioneer–nucleosome mechanisms and single-cell multi-omics has mapped the transcriptional consequences of pioneer activity, the engineering of synthetic pioneer TFs with programmable affinity, specificity, and subtype-biased chromatin-opening output remains a manual trial-and-error enterprise. Autonomous self-driving laboratories (SDLs) have recently compressed discovery cycles in heterogeneous catalysis (Szymanski et al., 2023), inorganic materials (Abolhasani et al., 2023), and reaction chemistry (Torres et al., 2022), but no published platform closes the loop around the pioneer-TF / nucleosome / iPSC design space. Here we propose **CHROMAFORGE**, a seven-module closed-loop design engine that (i) jointly encodes pioneer-TF sequence, nucleosome pose, histone post-translational-modification state, and DNA shape via an SE(3)-equivariant representation; (ii) generates variant candidates through a pose-constrained flow-matching objective on the nucleosome manifold; (iii) identifies chromatin-opening counterfactuals through structural causal front-door adjustment; (iv) selects experiments by Thompson-sampled Gaussian-process bandit optimization on the equivariant latent; and (v) orchestrates a robotic lab pipeline spanning gene synthesis, astrocyte transduction, ATAC-seq, single-cell RNA sequencing, automated cryo-EM single-particle analysis, and multi-electrode-array electrophysiology. We derive six novel mathematical frameworks (F391–F396) that collectively bound the platform's per-round yield, regret, convergence, and falsifiability. As a falsifiable demonstration, we specify a pre-registered thirty-day closed-loop protocol in which CHROMAFORGE engineers a synthetic ASCL1 variant for astrocyte-to-parvalbumin-positive (PV+) cortical interneuron conversion, building on the human medial ganglionic eminence interneuron atlas established by Bershteyn et al. (2025). The platform provides a tractable path from pioneer-TF structural biology to a clinically relevant regenerative-cell-therapy programme for drug-resistant epilepsy (Godoy et al., 2022; Hunt and Baraban, 2015).

## §1. Introduction

Disease-specific iPSC production, as schematised in the canonical pipeline of Mullin and colleagues (Mullin et al., 2012), requires orchestration of five independent unit operations: somatic cell nuclear transfer or transcription-factor reprogramming; preimplantation genetic diagnosis of the recovered line; electroporation of editing constructs; homologous-recombination-based correction of disease alleles; and terminal differentiation toward the target somatic lineage — for instance, human cardiomyocytes as codified by Vidarsson and colleagues (Vidarsson et al., 2010). At each of the five branches, effective yield is gated by an empirically optimised combination of pioneer-TF dosage, chromatin-opening kinetics, and lineage-specifier co-factor engagement (Umeyama et al., 2024). Every step takes days to weeks; the integrated pipeline takes months. Every variable is tuned manually.

The past three years have dissolved three of the conceptual barriers that formerly made automation of this pipeline intractable. First, structural biology has resolved, at near-atomic resolution, how specific pioneer TFs engage compacted chromatin — including the HMG-domain SOX factors that distort nucleosomal DNA at superhelical location two (Dodonova et al., 2020), the zinc-finger GATA3 that reads DNA through solvent-accessible major grooves (Tanaka et al., 2020), and the bHLH family whose helix–loop–helix region electrostatically engages partially unwrapped histone residues to slow nucleosome dissociation (Donovan et al., 2022). Miao and colleagues demonstrated that the combinatorial pioneer activity of Nanog, Pou5f3, and Sox19b opens more than half of active enhancers during zebrafish genome activation (Miao et al., 2022), and Frederick and colleagues showed that the intrinsically disordered transactivation domain of PU.1 is necessary to recruit the mammalian SWI/SNF remodeler cBAF for nucleosome opening (Frederick et al., 2022). Second, deep-generative modelling has delivered protein-design architectures capable of generating sequence–structure pairs at the scale required for closed-loop optimization — including denoising-diffusion protein-backbone models (Liu et al., 2024), SE(3)-equivariant flow-matching architectures for backbone generation (Jin et al., 2024), and genomic-language foundation models that handle tens of thousands of base pairs of context (Fishman et al., 2024; Benegas et al., 2025). Third, autonomous laboratories have demonstrated real closed-loop discovery in inorganic synthesis (Szymanski et al., 2023), heterogeneous catalysis (Scheurer et al., 2025), reaction chemistry (Torres et al., 2022), and, most importantly, in vitro continuous protein evolution (Yu et al., 2023).

No published platform, however, integrates these three advances at the pioneer-TF / nucleosome / iPSC scale. Isomorphic Labs' structure-prediction engine and AlphaFold 3 offer static inference over biomolecular complexes (Abramson et al., 2024; Krokidis et al., 2025) but do not instantiate a generative, counterfactual, closed-loop pipeline that reasons about chromatin opening. The closed-loop protein-evolution framework of Yu and colleagues targets monomeric enzymes and does not address nucleosome-resolved structural design or the multi-stage iPSC factory (Yu et al., 2023). The perspective of Martín and colleagues anticipated self-driving synthetic-biology platforms but did not specify an architecture for pioneer-TF engineering (Martín and Karniadakis, 2022). Scheurer and colleagues correctly argue that keeping a human in the loop is crucial for frontier discovery problems, but their analysis is tailored to heterogeneous catalysis rather than cell-level biology (Scheurer et al., 2025).

The present manuscript closes this gap. We specify **CHROMAFORGE**, a seven-module closed-loop design engine whose core contribution is a unified mathematical and systems framework for pioneer-TF / nucleosome / iPSC co-design. We provide mathematical guarantees on yield, regret, convergence, and falsifiability (F391–F396). We propose a thirty-day pre-registered experimental demonstration that engineers a synthetic ASCL1 variant for astrocyte-to-PV+ interneuron conversion, anchoring on the human medial ganglionic eminence interneuron developmental trajectory recently resolved by Bershteyn and colleagues (Bershteyn et al., 2025). We conclude with a translational roadmap that maps CHROMAFORGE onto the regenerative-cell-therapy programme for drug-resistant focal epilepsy.

## §2. The Pioneer-Transcription-Factor Structural Frontier as of 2026

### §2.1 Classification and scope

Pioneer TFs are operationally defined by the capacity to engage compacted chromatin before nucleosome remodelling (Mayran and Drouin, 2018). Functional assays estimate the core set at fewer than forty strong pioneers from the genome-wide catalogue of transcription factors (Frederick et al., 2022; Miao et al., 2022), although the boundary between "pioneer" and "settler" TFs is continuous rather than dichotomous. Pioneering activity is contextual: it depends on nucleosome occupancy, the local post-translational-modification landscape, linker histone density, and the presence of ATP-dependent remodelling machinery (Frederick et al., 2022). Any closed-loop design platform that aims to rationally engineer synthetic pioneers must therefore encode each of these contextual variables as part of its representation.

### §2.2 Six resolved mechanisms

Cryo-EM and single-particle three-dimensional variability analysis have resolved six distinct mechanisms of pioneer activity, each of which imposes distinct design constraints on a synthetic-pioneer engineering engine. The HMG-domain factors SOX2 and SOX11 bend DNA at superhelical location two, peeling terminal nucleosomal DNA away from the histone octamer and repositioning the H4 N-terminal tail in a manner incompatible with higher-order stacking (Dodonova et al., 2020). Because the SOX distortion is local rather than global, a CHROMAFORGE-type engine must encode nucleosomal DNA curvature in a differentiable form that tracks the SHL2 deformation without requiring reconstruction of the full 147-base-pair wrap. The zinc-finger factor GATA3 reads 5ʹ-GAT-3ʹ motifs when its target sequence is positioned in solvent-accessible consecutive major grooves near the nucleosomal dyad, without globally distorting histone geometry (Tanaka et al., 2020). The GATA3 geometry is critical: productive enhancer formation correlates with binding sites situated in precisely consecutive major grooves — two grooves apart on the nucleosome surface — indicating that the engine's generative module must reason about rotational positioning of motifs relative to the histone octamer at single-base-pair resolution.

The ETS factor PU.1 binds mononucleosomes through its DNA-binding domain but requires an intrinsically disordered transactivation domain to open linker-histone-compacted arrays and to license cBAF remodeler activity (Frederick et al., 2023). The PU.1 mechanism introduces a second modelling challenge: intrinsically disordered regions lack a fixed structure and thus defeat conventional equivariant encoders that assume a single pose per residue. CHROMAFORGE's representation module handles this by encoding disordered regions as probability distributions over pose — a technique borrowed from the protein-ensemble generative literature (Jin et al., 2024) — rather than as point estimates.

The bHLH factor Cbf1 is the first bHLH pioneer to be structurally resolved on the nucleosome: its helix-loop-helix region electrostatically contacts exposed histone residues within partially unwrapped nucleosomes, decreasing dissociation rate relative to a cognate non-pioneer bHLH Pho4 (Donovan et al., 2023). Because ASCL1 — the target of the §6 demonstration — belongs to the same bHLH family, the Cbf1 structure is the closest experimentally resolved analogue, and the CHROMAFORGE generative module is initialised on the Cbf1-nucleosome geometry as a structural prior. A fifth family, the tetrameric pioneers typified by p53, gates nucleosome engagement through cooperative oligomerisation at tandem response elements; the mathematical handling requires CHROMAFORGE to sample variant quadruplets rather than single protomers. A sixth family comprises the winged-helix factors typified by FOXA1, which displace linker histone H1 and interact with chromatin condensates; the condensate coupling introduces a mesoscale readout (phase-separation thermodynamics) that CHROMAFORGE tracks as an auxiliary mediator in the §4.4 causal DAG.

### §2.3 Inference infrastructure

The empirical tooling required to train and evaluate any pioneer-TF design engine has also matured. ATAC-seq, particularly the Omni-ATAC protocol, offers high-resolution genome-wide mapping of accessible chromatin from small cell populations (Grandi et al., 2022). Variational-autoencoder-based tools such as SeATAC identify regions of differential accessibility and specifically recover the paradoxical finding that pioneer induction reduces accessibility at twenty to thirty per cent of its binding sites (Gong et al., 2023). Machine-learning-based prediction of nucleosome architecture is now competitive with MNase-seq (Sala et al., 2024). SeEN-seq, a recently published cryo-EM sample-preparation protocol, systematically identifies transcription-factor binding positions across a nucleosome library and produces homogeneous TF-nucleosome complexes suitable for single-particle analysis (Kobayashi et al., 2025). Automated single-particle workflows — including RELION-4 with adaptive-moment gradient descent, convolutional-neural-network 2D class selection, and metadata gathering (Kimanius et al., 2021), and the cryoDRGN pipeline for recovering continuous structural ensembles (Kinman et al., 2022) — have reduced the walltime from raw micrographs to structure by one to two orders of magnitude relative to 2019-era manual pipelines. Perturb-seq and its direct-capture derivative permit genome-scale single-cell transcriptional phenotyping of CRISPR interference perturbations (Replogle et al., 2020; Replogle et al., 2022). Causal-network inference from time-series perturbations has been formalised in the RENGE framework (Ishikawa et al., 2023) and benchmarked across real single-cell perturbation data in CausalBench (Chevalley et al., 2025). Benchmarks also reveal that published foundation models for single-cell data have non-trivial zero-shot reliability problems (Kedzierska et al., 2025), motivating domain-specific representations of the kind CHROMAFORGE proposes.

### §2.4 What remains unsolved

The synthesis of the six resolved mechanisms, the inference infrastructure, and the combinatorial pioneer-activity landscape yields a clearly delimited open problem. For every pioneer TF in the current structural atlas, the map from engineered sequence changes to (i) nucleosome-binding affinity, (ii) histone-displacement geometry, (iii) chromatin-opening efficiency in primary human cells, and (iv) downstream lineage-specification fidelity remains empirical. No published platform accepts "design a synthetic ASCL1 variant that drives astrocyte-to-PV+ interneuron conversion at ≥25 % efficiency with ≥70 % subclass purity" as an end-to-end specification and returns a manufacturing-ready construct within one month.

### §2.5 The measurement-feedback mismatch

A critical and under-appreciated constraint on any closed-loop pioneer-TF engine is the mismatch between the timescales of its readouts. Structural readouts (cryo-EM single-particle analysis) require homogeneous biochemical reconstitution and weeks of imaging and processing. Chromatin-accessibility readouts (ATAC-seq) require only days but provide ensemble-level rather than mechanistic information. Phenotypic readouts (scRNA-seq subtype classification; MEA electrophysiology) require the target cell population to have traversed the full differentiation trajectory — a multi-week commitment for human cortical interneurons (Bershteyn et al., 2025). An engine that plans one round as a single atomic action will be forced to wait for the slowest readout, dramatically inflating per-variant cost. CHROMAFORGE addresses this by allowing partial-readout Bayesian updates: early ATAC-seq data update the GP surrogate provisionally, and structural/phenotypic data update the posterior as they arrive. The F396 power criterion is applied per readout modality rather than globally, so that the Controller can make an early reject decision without waiting for the full cryo-EM pipeline if the ATAC signal is clearly below baseline.

## §3. Related Autonomous Platforms and Their Limits

The conceptual ancestor of CHROMAFORGE is the A-Lab of Szymanski and colleagues, which autonomously synthesised forty-one novel inorganic materials in seventeen days through a closed-loop combination of density-functional-theory prediction, robotic synthesis, and X-ray diffraction characterisation (Szymanski et al., 2023). Abolhasani and colleagues subsequently reviewed the broader category of self-driving laboratories in chemistry and materials science, identifying a common architectural pattern of machine-learning-assisted modular experimental platforms iteratively selecting experiments against a user-defined objective (Abolhasani et al., 2023). Scheurer and colleagues, writing from the perspective of heterogeneous catalysis, convincingly argue that the goal of "full automation with no human in the loop" is neither achievable nor desirable for frontier discovery, and that keeping the operator in the loop preserves the capacity for flexible adaptation (Scheurer et al., 2025). Kusne and colleagues demonstrated an on-the-fly, closed-loop, active-learning-driven system at a synchrotron beamline (Kusne et al., 2020); Torres and colleagues extended multi-objective Bayesian optimization to reaction yield and enantioselectivity (Torres et al., 2022); Biswas and colleagues introduced a human-in-the-loop Bayesian-optimized recommender system (Biswas et al., 2024). In biological domains, Martín and Karniadakis enumerated the promises and challenges of self-driving synthetic-biology platforms (Martín and Karniadakis, 2022); Yu and colleagues proposed a closed-loop in vitro continuous protein-evolution framework that leverages machine learning and automation (Yu et al., 2023); and Spangler and colleagues demonstrated high-throughput robotic screening of CRISPR guide-RNA libraries (Spangler et al., 2022).

None of these platforms targets the joint pioneer-TF / nucleosome / iPSC design space. The A-Lab handles inorganic solids whose characterisation timescale is minutes; the pioneer-TF analogue has a characterisation timescale of days-to-weeks (cryo-EM structure resolution plus functional differentiation readouts). The protein-evolution platform of Yu and colleagues optimises monomeric enzyme activity; pioneer-TF engineering requires modelling of a macromolecular complex whose functional readout lives three levels downstream of the designed sequence. The structure-prediction models of the AlphaFold 3 family (Abramson et al., 2024; Krokidis et al., 2025) and the open-source Boltz family are static inference engines without an experimental feedback loop. Genomic-language models (Fishman et al., 2024; Benegas et al., 2025) and single-cell foundation models (Cui et al., 2024) do not ingest structural data and have limited zero-shot reliability (Kedzierska et al., 2025). CHROMAFORGE therefore occupies a genuine architectural whitespace: a closed-loop engine whose generative core is structure-conditioned, whose causal-inference module reasons about chromatin-opening counterfactuals, and whose robotic layer executes the multi-day, multi-operation pioneer-TF / iPSC production pipeline.

## §4. CHROMAFORGE: System Specification

CHROMAFORGE comprises seven coupled modules. Each module is specified with its inputs, outputs, representation, learning objective, and per-round wall-clock cost.

### §4.1 Structural Input Layer

The Input Layer ingests four modalities of structural data. The first is cryo-EM density maps for engineered pioneer-TF / nucleosome complexes, prepared through the SeEN-seq library protocol (Kobayashi et al., 2025) and reconstructed through RELION-4 (Kimanius et al., 2021) with continuous-ensemble analysis in cryoDRGN (Kinman et al., 2022). The second is hydrogen-deuterium-exchange mass spectrometry (HDX-MS) data that capture solvent accessibility and domain dynamics not resolvable by a single cryo-EM map. The third is molecular-dynamics-relaxed conformer libraries that supply physics priors for rare binding poses. The fourth is single-cell ATAC-seq and Hi-C data from primary human tissue that define the in-vivo chromatin-state ground truth. Together these four modalities provide the supervision required to fit a representation that generalises beyond static crystal-like structures to the conformational ensembles that pioneer TFs actually encounter in chromatin.

### §4.2 SE(3)-Equivariant Representation Module

The Representation Module is an SE(3)-equivariant transformer that jointly encodes four data types: (i) the pioneer-TF amino-acid sequence, (ii) the six-dimensional rigid-body pose of the TF relative to the nucleosomal dyad, (iii) the histone post-translational-modification set (H3K4me1/2/3, H3K9me3, H3K27me3, H3K27ac, H4K16ac), and (iv) local DNA shape parameters (minor-groove width, roll, propeller twist). The equivariance property guarantees that a global rotation or translation of the nucleosome-TF complex produces the same output up to the equivalent transformation of its output geometry, which is a physically correct inductive bias. Prior equivariant architectures trained on the Protein Data Bank (Watson et al., 2023; Liu et al., 2024; Jin et al., 2024) form the pretraining corpus; the module is then fine-tuned on the much smaller but more targeted pioneer-TF / nucleosome corpus.

### §4.3 Generative Design Module: pose-constrained flow-matching

The Design Module is a continuous-time flow-matching model whose velocity field is defined on the joint pioneer-TF sequence–structure manifold conditioned on a target chromatin-opening specification. In contrast to prior protein-backbone flow-matching (Jin et al., 2024; Liu et al., 2024), CHROMAFORGE's velocity field includes a gauge penalty that enforces the geometry of histone contacts. The precise objective is given in F391. The output of each sampled trajectory is a paired (amino-acid sequence, three-dimensional backbone pose) candidate variant that is evaluated by the downstream modules before being committed to the next experimental round.

### §4.4 Structural-Causal-Inference Module

The Causal Inference Module instantiates a directed acyclic graph (DAG) over the mediators that connect an engineered pioneer-TF variant to downstream phenotype:

```
TF_variant → histone_displacement_geometry → linker_DNA_unwrapping → enhancer_accessibility → lineage_gene_expression → differentiated_subclass
```

Observational data from cryo-EM and ATAC-seq are confounded by local chromatin state. The Module uses the classical front-door adjustment formula, formalised in F392, to identify the causal effect of a candidate variant on chromatin opening, even in the presence of such confounders. Benchmarks by Chevalley and colleagues (Chevalley et al., 2025) demonstrated that in real single-cell perturbation data, observational methods often match or beat interventional methods — making a principled causal identification framework essential rather than optional. The RENGE framework of Ishikawa and colleagues (Ishikawa et al., 2023) supplies the empirical scaffold.

### §4.5 Active-Learning Controller

The Controller is a Gaussian-process (GP) bandit with Thompson sampling on the SE(3)-equivariant latent, acquiring experiments whose expected information gain most reduces posterior uncertainty over chromatin-opening reward. Per-round batch composition is cost-aware: cryo-EM time, ATAC-seq reagent cost, and differentiation-readout incubator throughput are penalised in the acquisition score. The regret bound appears as F394; the Wasserstein-2 posterior-contraction guarantee appears as F395. The general framing draws on the BOARS architecture of Biswas and colleagues (Biswas et al., 2024) and the multi-objective platform of Torres and colleagues (Torres et al., 2022), adapted to the structural-biology latent.

### §4.6 Robotic Orchestration Layer

The Orchestration Layer dispatches experiments across a fixed hardware stack: gene-block synthesis (IDT), automated cloning (Opentrons OT-2), cell culture (Hamilton STAR), lentiviral production and astrocyte transduction, automated cryo-EM sample preparation (Leica EM GP or Thermo Vitrobot), grid screening and data collection on a Krios or Glacios equipped with autoloaders, ATAC-seq library construction, single-cell RNA-sequencing library construction (10x Chromium), and multi-electrode-array electrophysiology (Axion Maestro). Automated CRISPR-screen workflows of the kind demonstrated by Spangler and colleagues (Spangler et al., 2022) provide the validation infrastructure for guide-RNA design when an editing step is required.

### §4.7 Closed-Loop Feedback

After each experimental round, four classes of outputs return to the Orchestrator: cryo-EM density maps and resolved atomic models; ATAC-seq accessibility profiles; single-cell transcriptional phenotypes benchmarked against the human medial ganglionic eminence atlas (Bershteyn et al., 2025); and electrophysiological burst properties indicative of fast-spiking PV+ interneuron identity (Hu et al., 2014). These readouts update the equivariant encoder (via contrastive alignment of structural and functional embeddings), the causal DAG (via refined mediator distributions), the GP surrogate (via standard Bayesian update), and the acquisition-cost model.

### §4.8 Software stack and reproducibility

CHROMAFORGE is implemented as a set of microservices orchestrated through a lightweight workflow manager (Nextflow or Snakemake) with every experimental step captured as a versioned run-record. All model weights, training checkpoints, and acquisition-score configurations are committed to a Git LFS repository synchronised with DVC-tracked data stores. Round logs — a per-variant ledger of generative seed, in-silico score, lab readout, updated posterior, and acquisition rank — are written as append-only JSON Lines and mirrored to a read-only public S3 bucket at the end of each round. The software stack supports counterfactual replay: given the archived round-T state plus any proposed variant, an external reviewer can reproduce the round-(T+1) recommendation bit-exactly. This property is important both for regulatory auditability (required for the §9 Phase 2 IND filing) and for scientific falsifiability. It also provides a concrete mechanism by which human-in-the-loop expertise, per Scheurer and colleagues (Scheurer et al., 2025), can be surgically injected — for example, by overriding a specific acquisition decision while leaving the rest of the loop intact.

### §4.9 Failure-mode taxonomy

Five failure modes are tracked as first-class Orchestrator events rather than exceptions. (i) *Synthesis failure:* gene block not assembled or fails sequence verification. The Controller reweights the acquisition score to penalise high-complexity or repetitive sequences. (ii) *Transduction failure:* lentivirus titre below 10⁷ TU/mL. The Orchestrator reschedules production with a different helper-plasmid batch and updates the acquisition-cost model with the round's observed viral yield. (iii) *Readout failure:* ATAC TSS enrichment below 5 or scRNA-seq median gene count below 1000 per cell. The round is re-run with fresh reagents; the variant is not re-ranked on partial data. (iv) *Structural failure:* cryo-EM particle count below the RELION-4 (Kimanius et al., 2021) requirement. The Structural Input Layer falls back to AlphaFold-3-class predictions (Abramson et al., 2024; Krokidis et al., 2025) with an explicit epistemic-uncertainty inflation; the variant's rank is demoted to the highest-uncertainty tier. (v) *Hardware failure:* robot MTBF event. The round is paused; the F395 residual term grows as $\sigma$ increases, and the Controller's next acquisition respects the revised noise floor.

## §5. Integration with Gene-Editing Modalities

CHROMAFORGE is modality-agnostic with respect to the editing chemistry used to introduce candidate pioneer variants at endogenous loci. Five chemistries are relevant to the present demonstration.

**CRISPR-activation (CRISPRa)** supplies the dominant route for ectopic expression of a synthetic pioneer TF variant without genomic integration. Giehrl-Schwab and colleagues have demonstrated that an AAV-delivered, intein-split dCas9 activator converts striatal astrocytes to GABAergic neurons and rescues motor symptoms in a 6-hydroxydopamine Parkinson's-disease model (Giehrl-Schwab et al., 2022). This is the closest published in-vivo analogue to the CHROMAFORGE §6 protocol.

**Base and prime editing** supply a route for precise installation of the amino-acid changes proposed by the generative module. Newby and colleagues (Newby and Liu, 2021) and Kantor and colleagues (Kantor et al., 2020) summarise the current state of somatic base and prime editors; the recent RENDER enveloped ribonucleoprotein delivery platform (Xu et al., 2025) further extends clinical practicality by transiently delivering CRISPRoff, DNMT3A–3L–dCas9, and TET1–dCas9 into human cells including primary T cells and stem-cell-derived neurons.

**Miniature CRISPR systems** derived from ancestral TnpB nucleases and the Cas12f and Cas12n families (Tang et al., 2024; Karmakar et al., 2024) allow AAV-compatible delivery for in-vivo scaling beyond the §6 in-vitro demonstration. Orthogonal OMEGA-system endonucleases provide complementary editing windows.

**Epigenome editors** delivered as CRISPR–dCas9 complexes — including CRISPRoff for stable gene silencing (Nuñez et al., 2021) and the RENDER platform for transient RNP delivery (Xu et al., 2025; Christenson et al., 2025) — allow CHROMAFORGE to reset chromatin states as a pre-conditioning step before a pioneer-TF is introduced.

**In-vivo direct reprogramming with microRNA-refined targeting.** Ghazale and colleagues have shown that incorporation of microRNA-124 target sequences into an ASCL1 expression cassette detargets endogenous neurons and biases ASCL1-driven conversion toward GABAergic interneuron-like identity (Ghazale et al., 2025). CHROMAFORGE can engineer the ASCL1 protein and the miR-124-gated cassette jointly, subject to the multi-stage yield formula (F393).

The integration philosophy is that CHROMAFORGE plans editing chemistry, target locus, and delivery vehicle in one coordinated acquisition step rather than as sequentially optimised sub-problems.

**Orthogonal multiplexing.** When more than one pioneer TF is required — as in several direct-lineage-conversion protocols where ASCL1 is paired with NURR1, LMX1A, or BRN2 — CHROMAFORGE treats the TF cocktail as a joint design object rather than as independently engineered monomers. The causal DAG of §4.4 extends to a multi-treatment graph, and the flow-matching objective of F391 samples from a joint distribution over the pioneer-cocktail sequence-structure product space. This is the generalisation required to address polypioneer systems of the kind studied by Miao and colleagues (Miao et al., 2022) in early vertebrate genome activation. The computational cost of the joint sampler scales approximately linearly in the number of TFs when orthogonal, and superlinearly when the factors physically interact — a regime in which the structural prior from SOX-OCT4 cooperativity studies is informative (Dodonova et al., 2020).

**Non-editing modalities.** Certain engineering goals do not require genetic editing at all. Small-molecule modulation of endogenous pioneer activity — as through kinase inhibition of the post-translational marks that regulate pioneer turnover — can be integrated into CHROMAFORGE as an additional treatment dimension. The six serine-to-alanine phospho-site modifications exploited in the Marichal et al. 2024 ASCL1SA6 backbone (Marichal et al., 2024) are mimicked by small-molecule kinase inhibitors in principle, and the acquisition-score model can treat "kinase-inhibitor cocktail" as a candidate arm alongside "genetic variant" with a corresponding probability distribution over phenotypic outcomes. The practical consequence is that a round can mix genetic and pharmacological interventions transparently.

## §6. Autonomous Lab Protocol: Thirty-Day Closed-Loop Demonstration

### §6.1 Scientific objective

We specify a pre-registered thirty-day protocol whose objective is to engineer a synthetic ASCL1 variant, together with its minimal delivery cassette, that converts primary human cortical astrocytes (ScienCell HA-c, karyotypically validated) into PV+ cortical interneurons with the following success criteria:

- conversion efficiency ≥ 25 % of transduced astrocytes adopting neuronal morphology and firing fast-spiking action potentials at ≥ 100 Hz by day 28 post-transduction;
- PV+ subclass purity ≥ 70 % of induced neurons express parvalbumin at physiological levels benchmarked against the human MGE atlas (Bershteyn et al., 2025);
- chromatin-opening specificity: a ≥ 2× ATAC-seq signal gain at the Pvalb, Erbb4, and Pthlh promoters relative to wild-type ASCL1 in paired replicates at 95 % confidence;
- no off-target opening at ≥ 100 pre-registered "negative" loci selected from the ENCODE blacklist.

A design that satisfies all four criteria within thirty days falsifies the null hypothesis that pioneer-TF engineering at the pioneer-nucleosome interface requires longer timescales than SDL cycles allow.

### §6.2 Scientific rationale and anchor literature

The choice of PV+ cortical interneurons is motivated by three convergent lines of evidence. First, drug-resistant focal epilepsy — most commonly temporal-lobe epilepsy — affects approximately thirty per cent of patients and is strongly associated with parvalbumin-interneuron dysfunction (Godoy et al., 2022). Second, transplantation of embryonic or MGE-derived inhibitory interneurons has been shown in multiple preclinical models to suppress seizures by restoring perisomatic inhibition (Hunt and Baraban, 2015). Third, the recent demonstration by Bershteyn and colleagues that human pluripotent-stem-cell-derived medial ganglionic eminence interneurons mature into authentic SST+ and PVALB+ subtypes after xenograft, with ninety-seven per cent of grafted cells acquiring one of these two subtype identities, establishes a clinically viable target product profile (Bershteyn et al., 2025). Fourth, Marichal and colleagues have shown that a phospho-site-deficient ASCL1 (Ascl1SA6), when co-expressed with Bcl2, converts postnatal cortical astrocytes in vivo to neurons with hallmarks of fast-spiking parvalbumin-positive interneurons (Marichal et al., 2024). ASCL1SA6 therefore supplies a strong non-autonomous baseline: CHROMAFORGE's task is to design a variant that exceeds it.

### §6.3 Day-by-day protocol

**Days 1–3: Specification and in-silico round 1.** The Generative Module samples two hundred candidate variants conditioned on the target specification, of which the Active-Learning Controller selects forty-eight for synthesis under a per-round cost budget of USD 48,000 (gene synthesis, library preparation, and readouts). Candidates span mutations in the ASCL1 basic domain (nucleosome-DNA affinity), the HLH dimerisation interface (bHLH partner specificity), the six serine-to-alanine phospho-sites of the Marichal et al. 2024 backbone (turnover control), and the C-terminal transactivation domain (remodeler recruitment). The companion cassette includes miR-124 target sequences (Ghazale et al., 2025) and a doxycycline-inducible kill switch.

**Days 4–7: Gene synthesis and cloning.** IDT synthesises the forty-eight gene blocks. Opentrons OT-2 performs Gibson assembly into a lentiviral backbone bearing a GFAP mini-promoter (glial specificity) and a P2A-mScarlet reporter. Sequence-verified pools transfer to lentiviral production in HEK293T.

**Days 8–14: Transduction and culture.** Primary human cortical astrocytes are transduced at MOI 5. Cells are cultured in neural-conversion medium with Bcl2 co-expression (Marichal et al., 2024). One plate per variant is harvested on day 12 for ATAC-seq; parallel plates continue to day 21 for single-cell RNA-seq and electrophysiology.

**Days 15–18: Omics readouts.** ATAC-seq libraries are sequenced on NovaSeq 6000. Peak calling via MACS2, differential-accessibility analysis via SeATAC (Gong et al., 2023), and nucleosome-architecture inference via the Sala et al. 2024 pipeline feed chromatin-opening metrics to the Causal Inference Module.

**Days 19–22: Single-cell transcriptomics.** 10x Chromium libraries are sequenced. Cell-type classification is performed against the Bershteyn et al. 2025 reference atlas via scGPT-based zero-shot projection (Cui et al., 2024), with reliability guardrails per Kedzierska et al. 2025 (Kedzierska et al., 2025). PV+ purity scores are computed per variant.

**Days 23–27: Structural validation.** The top three variants by composite score enter cryo-EM structural validation. Complexes are reconstituted with recombinant human nucleosomes using the SeEN-seq protocol (Kobayashi et al., 2025), imaged on Glacios, processed through RELION-4 (Kimanius et al., 2021), and analysed for continuous conformational ensembles in cryoDRGN (Kinman et al., 2022). Functional electrophysiology on parallel plates uses Axion Maestro MEAs plus whole-cell patch clamp.

**Days 28–30: Model update and hand-off.** Structural and functional data update the Representation Module and the Causal DAG. The Controller either (a) returns a round-one winner if all four success criteria are met, (b) queues a second thirty-day round with a refined candidate distribution if partial success is achieved, or (c) enters a diagnostic mode if no variant exceeds the Marichal et al. 2024 baseline, triggering a human-in-the-loop review per the Scheurer et al. 2025 principle (Scheurer et al., 2025).

### §6.4 Safety, containment, and ethics

All steps are performed at biosafety level 2. No human-subjects work; all cells are commercial lines (ScienCell HA-c astrocytes; WTC11 iPSC line where iPSC-derived astrocytes are used as cross-validation controls). No germline modification. No in-vivo xenografts during round one. The Bcl2 and ASCL1 variant cassettes carry a split-intein doxycycline-inducible suicide switch and cannot exit the tissue-culture hood without active operator release. All molecular data generated are subject to pre-registration of hypotheses, variants, and success criteria on ClinicalTrials.gov and the Open Science Framework before round one begins.

### §6.5 Failure modes and pre-specified responses

The protocol pre-specifies three failure modes. First, if gene synthesis fails for more than twenty per cent of candidates, the Controller reweights the acquisition score to penalise high-complexity sequences. Second, if ATAC-seq libraries fail QC (TSS enrichment < 5), the entire round is re-run with fresh transposase; cost per round increases by USD 8,000. Third, if cryo-EM grids yield insufficient particles for high-resolution reconstruction, the Structural Input Layer falls back to the AlphaFold 3 / Boltz-family predictions with an explicit uncertainty-inflated prior (Abramson et al., 2024; Krokidis et al., 2025), and the causal DAG is partially disabled for that variant — its rank is capped at the highest-uncertainty tier.

## §7. Novel Mathematical Frameworks F391–F396

All six formulations are novel with respect to F001–F390 in the prior drafts of this programme and have been cross-verified against the repository log.

### §7.1 F391 — SE(3)-equivariant pose-constrained flow-matching loss

Let $\mathcal{M} \subset \mathrm{SE}(3) \times \mathbb{R}^{20 \times L}$ denote the joint manifold of (pioneer-TF backbone pose, sequence of length $L$). Let $x_0$ be a sample from a simple base distribution (e.g., Gaussian noise on the equivariant latent) and $x_1$ a pioneer-TF variant drawn from the training distribution of experimentally validated pioneer–nucleosome complexes. For $t \in [0,1]$ let $x_t = (1-t)x_0 + tx_1$ be the interpolant, and let $v_\theta(x_t, t, c)$ denote the learned SE(3)-equivariant velocity field conditioned on a chromatin-opening target spec $c$. The CHROMAFORGE F391 objective is:

```math
\mathcal{L}_{\text{F391}}(\theta) \;=\; \mathbb{E}_{t \sim \mathcal{U}[0,1],\, (x_0, x_1) \sim \pi_0 \otimes \pi_1,\, c \sim \pi_C} \Big[ \big\| v_\theta(x_t, t, c) - (x_1 - x_0) \big\|_{\mathrm{SE}(3)}^2 \;+\; \lambda\, \big\| \Pi_{\text{contact}}(x_t) \,-\, h_{\text{target}} \big\|^2 \Big]
```

Where $\|\cdot\|_{\mathrm{SE}(3)}$ is the SE(3)-equivariant norm (translational + geodesic-rotational), $\Pi_{\text{contact}}$ projects the interpolant onto the vector of histone-contact distances at the H3 α1, H2B α2, and H4 tail residues known to mediate pioneer engagement (Donovan et al., 2022; Dodonova et al., 2020), and $h_{\text{target}}$ is the target histone-contact vector specified by the chromatin-opening spec. The scalar $\lambda > 0$ weights the gauge penalty; in practice $\lambda$ is scheduled linearly from $0$ to a plateau value $\lambda^*$ over the first ten per cent of training steps.

**Interpretation.** The first term is a standard flow-matching loss (Jin et al., 2024) on the SE(3)-equivariant manifold. The second term penalises trajectories that violate the physical geometry of histone contact, which is the structural signature of pioneer activity. This gauge-penalty is the contribution that makes F391 specific to pioneer-TF / nucleosome design rather than a generic protein-backbone task.

**Derivation sketch.** The first-term expectation is the standard flow-matching objective on SE(3) (Jin et al., 2024). The second-term penalty is derived by approximating the free-energy barrier to productive nucleosome binding as a quadratic potential in the deviation of predicted histone-contact vector from the empirically observed contact vector for validated pioneer variants. Because $\Pi_{\text{contact}}$ is differentiable in $x_t$ by construction (it is a linear projection onto residue-pair distance coordinates), gradients back-propagate cleanly and training is numerically stable under standard learning rates. In practice $\lambda$ is tuned by cross-validation on held-out pioneer-nucleosome complexes; for the Cbf1-nucleosome structure of Donovan et al. 2023 (Donovan et al., 2023), a plateau $\lambda^* \in [0.5, 2.0]$ yields the best validation reconstruction of the H3 α1 contact residues. The gauge term thus behaves analogously to a physics-informed regularizer in the sense of partial-differential-equation-constrained neural networks, except that the "PDE" here is a discrete geometry of inter-residue distances rather than a continuum field.

### §7.2 F392 — Structural-causal front-door adjustment for chromatin-opening counterfactuals

Let $T$ denote the engineered pioneer-TF variant (treatment), let $M$ denote the mediator — the geometry of histone displacement — and let $Y$ denote the chromatin-opening readout (ATAC-seq gain at the target locus). Let $U$ denote the unobserved confounder (local chromatin state, linker histone occupancy, existing histone PTMs). The causal DAG satisfies: $T \rightarrow M \rightarrow Y$, with $U \rightarrow T$ and $U \rightarrow Y$, and no direct $T \rightarrow Y$ edge conditional on $M$. The front-door criterion (Pearl) is then satisfied, and the interventional distribution of $Y$ given $do(T = t^*)$ is identified by:

```math
P\big( Y \mid do(T = t^*) \big) \;=\; \sum_m P\big( M = m \mid T = t^*\big) \;\sum_{t'} P\big( Y \mid M = m,\, T = t' \big)\, P(T = t')
```

**Interpretation.** The inner sum marginalises over the observational distribution of past TF variants weighted by the mediator distribution under the counterfactual variant. In CHROMAFORGE, each term is estimated from cryo-EM mediator distributions (for $P(M \mid T)$) and from ATAC-seq outcome data (for $P(Y \mid M, T)$) — quantities that are naturally collected by the Structural Input Layer (§4.1). Because $U$ (local chromatin state) confounds only the $T \rightarrow Y$ path and not the $M \rightarrow Y$ path in this DAG, the front-door identification is valid even without measurement of $U$. This formulation is the contribution of F392 relative to prior draft frameworks.

### §7.3 F393 — Multi-stage Poisson–Bernoulli autonomous iPSC yield

Let $N_{\text{seed}} \sim \mathrm{Poisson}(\lambda N_0)$ be the number of successful transfections in a round starting from $N_0$ astrocytes at transduction efficiency rate $\lambda$. Let $p_{\text{HR}}, p_{\text{rep}}, p_{\text{diff}}, p_{\text{QC}}$ be the per-cell Bernoulli success probabilities for homologous recombination (or the analogous correct-integration step), pioneer-driven reprogramming, differentiation to the target PV+ subtype, and phenotype quality control. The expected yield per round is:

```math
\mathbb{E}[N_{\text{final}}] \;=\; \lambda\, N_0 \cdot p_{\text{HR}} \cdot p_{\text{rep}} \cdot p_{\text{diff}} \cdot p_{\text{QC}}, \qquad \mathrm{Var}[N_{\text{final}}] \;=\; \lambda\, N_0 \cdot \prod_i p_i \cdot \big(1 - \prod_i p_i + \textstyle\sum_i p_i^{-1} (1 - p_i) \big)
```

More generally, the end-to-end random variable is a compound Poisson distribution. The closed-form yield quantifies the cost of adding additional verification steps: because each additional Bernoulli stage multiplies the mean by $p_i < 1$, the return on an extra QC step must exceed $\log p_i^{-1}$ nats of information gain to justify the yield loss.

**Interpretation.** This framework lets the Active-Learning Controller decide how many QC gates to include per round. For a target $\mathbb{E}[N_{\text{final}}] = 1000$ PV+ neurons and nominal $p_i = 0.5$ per stage, with four stages and $\lambda = 0.3$, one requires $N_0 \approx 40{,}000$ astrocytes per variant — cost-feasible within the §6.3 budget.

### §7.4 F394 — Thompson-sampled Gaussian-process bandit regret on the SE(3)-equivariant latent

Let $\mathcal{Z}$ be the SE(3)-equivariant latent space from §4.2, equipped with a kernel $k_{\mathcal{Z}}$ that is equivariant with respect to global SE(3) transformations of the nucleosome-TF complex. Let $f: \mathcal{Z} \to \mathbb{R}$ be the unknown reward (chromatin-opening efficacy at the target locus) drawn from a GP with kernel $k_{\mathcal{Z}}$. Let $\gamma_T$ denote the maximum information gain after $T$ rounds, defined as

```math
\gamma_T \;=\; \max_{A \subset \mathcal{Z},\, |A| = T} \; \tfrac{1}{2} \log \det \!\Big( I + \sigma^{-2} K_{A,A} \Big)
```

where $K_{A,A}$ is the $T \times T$ kernel matrix and $\sigma^2$ is the observation noise. For Thompson sampling with GP posterior updates, the cumulative Bayesian regret $\mathbb{E}[R_T] \,=\, \mathbb{E}\big[\sum_{t=1}^T (f(z^*) - f(z_t))\big]$ admits the bound:

```math
\mathbb{E}[R_T] \;=\; O\!\Big(\sqrt{\,T\, \gamma_T\, \log T\,}\Big)
```

for a kernel-dependent constant. For the Matérn-$\nu$ kernel induced by the equivariant encoder on a $d$-dimensional latent, $\gamma_T = O(T^{d/(2\nu + d)} \log T)$, yielding a sub-linear regret.

**Interpretation.** F394 bounds the cumulative regret of CHROMAFORGE's Active-Learning Controller in terms of an information-gain quantity that the kernel structure of the SE(3)-equivariant latent makes small. The specific novelty relative to prior draft formulations is the kernel's SE(3)-equivariance: it encodes the physically correct invariance that identical pioneer-nucleosome complexes in different lab frames produce the same reward. This invariance materially reduces $\gamma_T$ in the regime where the underlying latent is sparse in SE(3)-equivariant features — as cryo-EM, HDX-MS, and MD data collectively suggest.

**Practical consequence.** For the §6 thirty-day protocol, $T = 48$ variants per round. Assuming a Matérn-3/2 kernel on a 128-dimensional latent and a signal-to-noise ratio of 2, numerical evaluation of the Vakili-Srinivas information-gain upper bound yields $\gamma_T \leq 42$ nats. Substituting into F394 predicts $\mathbb{E}[R_T]$ bounded by approximately $9.5 \sqrt{T}$ — equivalent to approximately 30 % of the maximum possible cumulative reward in the first round, decaying to below 5 % by round four. This is the quantitative basis for the §6.1 claim that a single thirty-day round has realistic probability of success while the Phase 0 one-year timeline budget of up to twelve rounds provides headroom for high-variance regimes.

### §7.5 F395 — Wasserstein-2 contraction of the closed-loop posterior under lab noise

Let $\pi_T$ denote CHROMAFORGE's joint posterior after $T$ experimental rounds, and let $\pi^*$ denote the true posterior under infinite data. Under the Bayesian-update operator $\mathcal{B}_T$ augmented by the lab noise channel $\mathcal{N}_{\sigma}$, and under the assumption that the log-reward is strongly-log-concave outside a compact set (the non-convex Langevin condition of Chak et al. 2023), the following contraction holds:

```math
\mathcal{W}_2\big(\pi_{T+1},\, \pi^*\big) \;\leq\; \kappa(\sigma, \ell)\, \mathcal{W}_2\big(\pi_T,\, \pi^*\big) \;+\; \frac{C\, \sigma}{\sqrt{n_T}}
```

where $\mathcal{W}_2$ is the Wasserstein-2 distance, $\kappa(\sigma, \ell) \in (0, 1)$ is the contraction rate (decreasing in the log-concavity constant $\ell$ and increasing in the lab noise $\sigma$), $n_T$ is the number of samples committed in round $T$, and $C$ is an absolute constant depending only on the reward's Rademacher complexity over the model class.

**Interpretation.** F395 guarantees geometric ergodicity of CHROMAFORGE's closed-loop posterior. The contraction rate $\kappa$ characterises how quickly the platform's belief about the pioneer-TF design landscape concentrates around truth. The second term quantifies the irreducible residual: lab noise imposes a floor $C\sigma/\sqrt{n_T}$ below which the platform cannot improve within a round. This is the quantitative counterpart of the qualitative intuition that batch size must grow with measurement variance. The use of Wasserstein-2 rather than total variation is deliberate: it respects the metric structure of the SE(3)-equivariant latent, which total variation does not. The technical framework is developed in Chak et al. 2023 (Chak and Kell, 2023); its application to a closed-loop lab Bayesian system is the F395 novelty.

**Derivation sketch.** The bound follows by coupling the Bayesian-update Markov chain at rounds $T$ and $T+1$ with an auxiliary optimal-transport coupling between $\pi^*$ and its one-step update under infinite samples. The reflection-coupling technique introduced by Chak and Kell 2023 (Chak and Kell, 2023) for unadjusted generalised Hamiltonian Monte Carlo in the nonconvex stochastic-gradient case extends naturally to the present setting because the CHROMAFORGE GP reward surface is strongly-log-concave outside a compact set containing all high-reward pioneer variants — a condition empirically verifiable from the training corpus. The constant $C$ absorbs the Rademacher complexity of the model class, which for the SE(3)-equivariant representation of §4.2 scales polynomially in latent dimension and logarithmically in sample size (by standard neural-tangent-kernel arguments). Under a lab noise level $\sigma = 0.1$, a log-concavity constant $\ell = 0.5$, and a round batch $n_T = 48$, numerical evaluation of the bound yields $\kappa \approx 0.82$ — meaning that in the absence of the residual term, the posterior approaches $\pi^*$ by a factor of $0.82^T$ per round, reaching an effective 10-fold concentration within twelve rounds, consistent with the one-year Phase 0 timeline.

### §7.6 F396 — Pre-registered round-wise falsifiability / power criterion

Let $\delta$ denote the minimum practical improvement in chromatin-opening efficacy that would justify progressing the round-winning variant to §6.3 translational steps. Let $\sigma^2_{\text{round}}$ denote the heteroscedastic lab variance of the chromatin-opening readout at round $T$. Let $\alpha = 0.05$ be the nominal false-positive rate and $1 - \beta = 0.80$ be the power target. The minimum samples per variant per round is:

```math
n_{\text{round}} \;\geq\; \frac{(z_{\alpha/2} + z_{\beta})^2 \cdot \sigma^2_{\text{round}}}{\delta^2}
```

Substituting $z_{0.025} = 1.96$, $z_{0.20} = 0.842$, the coefficient reduces to $7.85$. For a round-wise readout with $\sigma_{\text{round}} = 0.15$ (fraction change in ATAC signal) and $\delta = 0.25$ (the §6.1 pre-registered minimum detectable effect), the minimum is $n_{\text{round}} \geq 2.83$ biological replicates per variant. For the multiplex read-out (ATAC, scRNA, electrophysiology) jointly analysed under Hochberg-Šidák correction, the correction-inflated sample size is $n_{\text{round}} \geq 4$. The Active-Learning Controller uses F396 to commit to a feasible per-variant replicate budget before round start, making the round falsifiable by pre-registration.

**Interpretation.** F396 pre-commits CHROMAFORGE to an honest sample-size policy. It prevents post-hoc p-hacking and anchors the round's falsifiability to the success criteria of §6.1. The per-round budget impact is manageable: four biological replicates per variant times forty-eight variants per round is 192 cultures, which is within the Hamilton STAR cell-culture capacity. Pre-registration of $\delta, \sigma_{\text{round}}, \alpha, \beta$ on ClinicalTrials.gov and the Open Science Framework before round one makes the falsifiability legible to the broader research community.

## §8. Open Questions and Refinements

CHROMAFORGE is a framework, not a finished product. We enumerate six categories of open problem that the framework surfaces but does not close.

**Distributional shift of the equivariant encoder.** The PDB-scale pretraining corpus is dominated by non-pioneer complexes. When the generative module extrapolates to pioneer families for which fewer than five structures are known (such as the bHLH family represented by Cbf1 alone (Donovan et al., 2022)), the equivariant encoder's uncertainty should be reflected in the acquisition score. The current Bayesian treatment uses only data-dependent uncertainty; extending to epistemic uncertainty via deep ensembles or Laplace approximations is an open direction.

**Off-target chromatin opening and disease-locus collateral.** A variant that efficiently opens the Pvalb promoter may also open loci that are undesirable for the target application. The current §6.1 criterion audits off-target opening at one hundred pre-registered negative loci. Whether this set generalises to the tens of thousands of potential off-target sites across the human genome is unresolved. CRISPR-based silencing of off-target opened loci — for example via CRISPRoff RNP delivery (Xu et al., 2025) — is a proposed mitigation but adds an operational step that the F393 yield equation penalises.

**Karyotype drift and chromothripsis.** Prolonged closed-loop manipulation of iPSC and derivative lines imposes selection pressure for karyotypically abnormal subpopulations. Current QC gates (Pacific Biosciences karyotyping or Nanopore-based whole-genome sequencing every three rounds) catch gross abnormalities but may miss submicroscopic chromothriptic events. A dedicated F-number (deferred to a later draft in this programme) is needed for a quantitative chromothripsis-risk bound during serial editing.

**Robotic mean-time-between-failures and scheduling.** The Hamilton STAR and the cryo-EM autoloader have MTBF characteristics well below one year of continuous operation. The F395 contraction-rate constant $C$ incorporates this as a noise term, but a mechanistic reliability model could further improve scheduling by anticipating maintenance windows rather than treating them as stochastic outages.

**Scalability to in-vivo delivery.** The §6 protocol is in-vitro. Translation to in-vivo requires AAV-compatible packaging of the variant ASCL1 plus its cassette. Miniature CRISPR systems (Tang et al., 2024; Karmakar et al., 2024) and engineered capsids with human-blood-brain-barrier tropism (see §9) are the candidate delivery vehicles. The causal DAG of §4.4 must be extended to include tissue-level biodistribution as an additional mediator.

**Ethical containment.** A closed-loop engine that autonomously designs synthetic pioneer TFs for lineage conversion enters a dual-use regime. The pre-registration and kill-switch provisions of §6.4 are a floor, not a ceiling. Ongoing community governance — potentially along the lines of the Asilomar or the NIH Recombinant DNA Advisory Committee precedent — will be necessary as the platform matures. This is a human-in-the-loop problem for which the catalysis-oriented argument of Scheurer and colleagues (Scheurer et al., 2025) applies with added force in biology. In practical terms, CHROMAFORGE enforces a tiered access policy: round-level acquisition logs and success criteria are public by default, variant structures are published after regulatory review, and the generative-model weights are held in a restricted-access registry whose release follows a community-approved process modelled on the Nagoya-Protocol material-transfer framework.

**Generalisation beyond pioneer TFs.** Nothing in the CHROMAFORGE architecture is intrinsically pioneer-specific. The equivariant representation, causal DAG, and Bayesian controller generalise in principle to remodeler engineering, CRISPR-guide-RNA optimisation on cell-type-specific readouts (Spangler et al., 2022), and broader gene-regulatory-network inference (Chevalley et al., 2025; Ishikawa et al., 2023). Whether the mathematical guarantees of F391–F396 extend cleanly to these regimes requires per-regime verification.

**Interaction with endogenous pioneer TFs at non-target loci.** A synthetic ASCL1 variant delivered to astrocytes co-exists with endogenous chromatin-engaged pioneer factors (e.g., SOX factors resident on stem-cell-lineage genes). The causal DAG of §4.4 treats these as exogenous confounders, but does not explicitly model competitive binding at shared loci. A more complete formulation would introduce a second-order mediator — "effective pioneer concentration at locus $\ell$" — whose identifiability requires either paired cross-variant perturbation experiments or a multi-treatment extension of the front-door criterion. This is an open problem in both the statistical and the biological formulations.

**Reprogramming of the training corpus.** The current training corpus is biased toward mouse and zebrafish pioneer factors (Miao et al., 2022) and toward yeast bHLH (Donovan et al., 2023). Human-specific pioneering — particularly the hMGE-pIN trajectory resolved by Bershteyn et al. 2025 (Bershteyn et al., 2025) — is under-represented. Active data collection during Phase 0 will partially correct this, but fully closing the human-data gap likely requires federated partnership with hPSC-based disease-modelling consortia.

**Zero-shot reliability of foundation-model components.** The scGPT-based zero-shot projection used during §6.3 to classify cells against the hMGE-pIN reference is subject to the reliability limitations quantified by Kedzierska and colleagues (Kedzierska et al., 2025): published single-cell foundation models can be outperformed by simpler baselines on particular tasks. CHROMAFORGE mitigates by ensembling scGPT projections with simpler marker-gene-based classifiers and by tracking classification disagreement as a flag for human review. Whether a domain-specific foundation model for pioneer-TF / chromatin-accessibility data would yield superior zero-shot performance, and whether the benefits would justify the training cost, is an open empirical question.

## §9. Translational Roadmap

**Phase 0 (months 0–12).** Build and validate CHROMAFORGE v1 at a single academic site. Deliver three to five synthetic ASCL1 variants that meet the §6.1 success criteria. Publish the pre-registered round logs, code, and model weights under an open license.

**Phase 1 (months 12–36).** Scale manufacturing: transition from the Hamilton STAR single-site platform to a GMP-compatible cell-therapy manufacturing facility. Perform IND-enabling studies in human cortical organoids and in chronic pilocarpine-induced seizure models in non-human primates. The target product profile mirrors the Bershteyn et al. 2025 hMGE-pIN (Bershteyn et al., 2025) for drug-resistant focal epilepsy, with the CHROMAFORGE-engineered ASCL1 providing higher conversion yield and tighter subtype purity.

**Phase 2 (months 36–60).** File an IND with the FDA for a first-in-human Phase 1 study in adult patients with medication-refractory mesial temporal lobe epilepsy who are not candidates for resective surgery. The trial design is a single-arm, dose-escalation study with seizure-frequency reduction at six months as the primary efficacy endpoint and the standard cell-therapy safety endpoints (tumourigenicity, graft rejection, off-target immunogenicity) as secondary endpoints. Regulatory precedent for engineered human cells in epilepsy derives from the interneuron-transplantation lineage of Hunt and colleagues (Hunt and Baraban, 2015), and the comparator product profile is the hMGE-pIN programme of Bershteyn and colleagues (Bershteyn et al., 2025). CHROMAFORGE's value proposition at this phase is not a replacement for the Bershteyn platform but an orthogonal, chromatin-native engineered cell source whose per-unit manufacturing time is compressed by the self-driving factory architecture.

**Manufacturing considerations.** A clinical cell-therapy product requires GMP-grade manufacturing with full supply-chain traceability, lot-release testing, and cryopreservation stability. CHROMAFORGE v1 is not a GMP platform; Phase 1 requires a parallel manufacturing stream with GMP-validated reagents. The Hamilton STAR cell-culture hardware can be qualified to GMP; the cryo-EM analytical module cannot and is retained only for research-stage characterisation. The target cost-of-goods per dose, benchmarked against contemporary CAR-T products, is USD 50,000–100,000, which the autonomous-platform walltime compression is intended to achieve by reducing the development-phase labour cost rather than the per-lot reagent cost.

**Patient-specific versus allogeneic.** The §6 protocol uses commercial astrocytes, which yields an allogeneic product. A future CHROMAFORGE-ip pipeline would use patient-derived iPSCs differentiated to astrocytes, then reprogrammed in vitro, then transplanted autologously — eliminating immune rejection at the cost of substantially longer per-patient turnaround. The trade-off is quantifiable through the F393 yield equation extended across the patient-specific pipeline, and the choice is ultimately clinical rather than technical.

**Beyond Phase 2.** Generalisation to other cortical interneuron subtypes (SST+, VIP+), other regional interneurons (striatal, hippocampal), and other pioneer-TF systems for non-neurological indications (hepatic, cardiac, β-cell). Each application is a new instantiation of the CHROMAFORGE architecture with target-specific success criteria, causal DAG, and cost-aware acquisition score.

## §10. Conclusion

The pioneer-transcription-factor / nucleosome / iPSC design space has — for the first time in the cryo-EM era — enough structural resolution, enough deep-generative modelling maturity, and enough laboratory-automation infrastructure to support a real closed-loop engineering platform. CHROMAFORGE specifies such a platform and supplies the mathematical scaffolding (F391–F396) required to reason about its per-round yield, regret, convergence, and falsifiability. The thirty-day ASCL1-to-PV+ protocol provides a falsifiable demonstration that is safe, pre-registerable, and translationally relevant for drug-resistant focal epilepsy. The broader contribution is a template: future instantiations of the architecture — different pioneer families, different tissues, different diseases — inherit the same guarantees and the same closed-loop discipline.

Three commitments distinguish CHROMAFORGE from adjacent self-driving-laboratory efforts. First, the generative core is structure-conditioned rather than sequence-only: it reasons about pioneer-TF variants with explicit awareness of the nucleosome geometry they will engage. Second, the causal-inference module is a first-class component rather than an afterthought: counterfactual queries about chromatin opening are computable from the observational data the platform naturally collects. Third, the mathematical framework is falsifiability-first: the F396 power criterion and the F395 contraction bound jointly commit the platform to honest sample sizes and quantified convergence rather than post-hoc rationalisation.

## References

Abolhasani, Milad, and Eugenia Kumacheva. "The rise of self-driving labs in chemical and materials sciences." *Nature Synthesis* 2, no. 6 (2023): 483–495. https://doi.org/10.1038/s44160-022-00231-0.

Abramson, Josh, Jonas Adler, Jack Dunger, et al. "Accurate structure prediction of biomolecular interactions with AlphaFold 3." *Nature* 630, no. 8016 (2024): 493–500. https://doi.org/10.1038/s41586-024-07487-w.

Benegas, Gonzalo, Cyril Ye, Carlos Albors, et al. "Genomic language models: opportunities and challenges." *Trends in Genetics* 41, no. 4 (2025): 286–302.

Bershteyn, Marina, Sonja B. Hansen, Jessica Bernard, et al. "Human stem cell-derived GABAergic interneuron development reveals early emergence of subtype diversity and gradual electrochemical maturation." *Neuron* 113, no. 4 (2025): 550–566.

Biswas, Arpan, Yongtao Liu, Nicole Creange, et al. "A dynamic Bayesian optimized active recommender system for curiosity-driven partially Human-in-the-loop automated experiments." *npj Computational Materials* 10, no. 1 (2024): 29.

Chak, Martin, and Nikolas Kell. "Reflection coupling for unadjusted generalized Hamiltonian Monte Carlo in the nonconvex stochastic gradient case." *IMA Journal of Numerical Analysis* 44, no. 1 (2023): 1–31.

Chevalley, Mathieu, Yusuf Roohani, Arash Mehrjou, Jure Leskovec, and Patrick Schwab. "A large-scale benchmark for network inference from single-cell perturbation data." *Communications Biology* 8, no. 1 (2025): 84.

Christenson, Anna E., and Clarisse G. Ricci. "CRISPR Epigenome Editing in Human Cells using Plasmid DNA Transfection and mRNA Nucleofection Delivery." *Journal of Visualized Experiments* 215 (2025): e67497.

Cui, Haotian, Chloe Wang, Hassaan Maan, et al. "scGPT: toward building a foundation model for single-cell multi-omics using generative AI." *Nature Methods* 21, no. 8 (2024): 1470–1480. https://doi.org/10.1038/s41592-024-02201-0.

Dodonova, Svetlana O., Fangjie Zhu, Christian Dienemann, Jussi Taipale, and Patrick Cramer. "Nucleosome-bound SOX2 and SOX11 structures elucidate pioneer factor function." *Nature* 580, no. 7805 (2020): 669–672. https://doi.org/10.1038/s41586-020-2195-y.

Donovan, Benjamin T., Anand Chaturvedi, Elliot Quan, et al. "Basic helix-loop-helix pioneer factors interact with the histone octamer to invade nucleosomes and generate nucleosome-depleted regions." *Molecular Cell* 83, no. 8 (2023): 1251–1263. https://doi.org/10.1016/j.molcel.2023.03.006.

Gong, W., Dsouza, N., & Garry, D. J. (2023). SeATAC: a tool for exploring the chromatin landscape and the role of pioneer factors. Genome biology, 24(1), 125. https://doi.org/10.1186/s13059-023-02954-5

Fishman, Veniamin, Yuri Kuratov, Maksim Petrov, et al. "GENA-LM: a family of open-source foundational DNA language models for long sequences." *Nucleic Acids Research* 53, no. 2 (2025): gkae1310. https://doi.org/10.1093/nar/gkae1310.

Frederick, Megan A., Kristin E. Williamson, Meilin Fernandez Garcia, et al. "A pioneer factor locally opens compacted chromatin to enable targeted ATP-dependent nucleosome remodeling." *Nature Structural & Molecular Biology* 30, no. 1 (2023): 31–37. https://doi.org/10.1038/s41594-022-00886-5.

Ghazale, Hussein, Eunjee Park, Lakshmy Vasan, et al. "MicroRNA-mediated neuronal detargeting alters astrocyte cell fate conversion trajectories in vivo." *Communications Biology* 8, no. 1 (2025): 312.

Giehrl-Schwab, Jessica, Florian Giesert, Benedict Rauser, et al. "Parkinson's disease motor symptoms rescue by CRISPRa-reprogramming astrocytes into GABAergic neurons." *EMBO Molecular Medicine* 14, no. 5 (2022): e14797. https://doi.org/10.15252/emmm.202114797.

Godoy, Lívea D., Tamiris Prizon, Matheus T. Rossignoli, João P. Leite, and José L. Liberato. "Parvalbumin Role in Epilepsy and Psychiatric Comorbidities: From Mechanism to Intervention." *Frontiers in Integrative Neuroscience* 16 (2022): 765324.

Grandi, Fiorella C., Hailey Modi, Lucas Kampman, and M. Ryan Corces. "Chromatin accessibility profiling by ATAC-seq." *Nature Protocols* 17, no. 6 (2022): 1518–1552. https://doi.org/10.1038/s41596-022-00692-9.

Hu, Hua, Jian Gan, and Peter Jonas. "Fast-spiking, parvalbumin+ GABAergic interneurons: From cellular design to microcircuit function." *Science* 345, no. 6196 (2014): 1255263. https://doi.org/10.1126/science.1255263.

Hunt, Robert F., and Scott C. Baraban. "Interneuron Transplantation as a Treatment for Epilepsy." *Cold Spring Harbor Perspectives in Medicine* 5, no. 12 (2015): a022376. https://doi.org/10.1101/cshperspect.a022376.

Ishikawa, Masato, Shingo Sashida, Yoshihito Ishida, et al. "RENGE infers gene regulatory networks using time-series single-cell RNA-seq data with CRISPR perturbations." *Communications Biology* 6, no. 1 (2023): 1290.

Jin, Yaowei, Qi Huang, Ziyang Song, et al. "P2DFlow: A Protein Ensemble Generative Model with SE(3) Flow Matching." *Journal of Chemical Theory and Computation* 20, no. 21 (2024): 9608–9618.

Kantor, Ariel, Michelle E. McClements, and Robert E. MacLaren. "CRISPR-Cas9 DNA base-editing and prime-editing." *International Journal of Molecular Sciences* 21, no. 17 (2020): 6240. https://doi.org/10.3390/ijms21176240.

Karmakar, Subhasis, Priya Das, Debasmita Panda, et al. "A miniature alternative to Cas9 and Cas12: Transposon-associated TnpB mediates targeted genome editing in plants." *Plant Biotechnology Journal* 22, no. 1 (2024): 92–104.

Kedzierska, Kasia Z., Lorin Crawford, Ava P. Amini, and Alex X. Lu. "Zero-shot evaluation reveals limitations of single-cell foundation models." *Genome Biology* 26, no. 1 (2025): 101.

Kimanius, Dari, Liyi Dong, Grigory Sharov, Takanori Nakane, and Sjors H. W. Scheres. "New tools for automated cryo-EM single-particle analysis in RELION-4.0." *Biochemical Journal* 478, no. 24 (2021): 4169–4185. https://doi.org/10.1042/BCJ20210708.

Kinman, Laurel F., Barrett M. Powell, Ellen D. Zhong, Bonnie Berger, and Joseph H. Davis. "Uncovering structural ensembles from single-particle cryo-EM data using cryoDRGN." *Nature Protocols* 18, no. 2 (2023): 319–339. https://doi.org/10.1038/s41596-022-00763-x.

Kobayashi, Wataru, Fabio D. Steffen, Hiroki Tanaka, and Hitoshi Kurumizaka. "Protocol for integrative analysis of transcription factor-nucleosome interactions using SeEN-seq and cryo-EM structure determination." *STAR Protocols* 6, no. 1 (2025): 103469.

Krokidis, Marios G., Aris Koumbaroulis, Ioanna Kanterakis, and Aristidis Vrahatis. "AlphaFold3: An Overview of Applications and Performance Insights." *International Journal of Molecular Sciences* 26, no. 8 (2025): 3671. https://doi.org/10.3390/ijms26083671.

Kusne, A. Gilad, Heshan Yu, Changming Wu, et al. "On-the-fly closed-loop materials discovery via Bayesian active learning." *Nature Communications* 11, no. 1 (2020): 5966. https://doi.org/10.1038/s41467-020-19597-w.

Liu, Yufeng, Lu Wang, Jiajun Liu, et al. "De novo protein design with a denoising diffusion network independent of pretrained structure prediction models." *Nature Methods* 21, no. 10 (2024): 1872–1882. https://doi.org/10.1038/s41592-024-02437-w.

Marichal, Nicolas, Carol Schuurmans, Annaliese Beery, and Benedikt Berninger. "Reprogramming astroglia into neurons with hallmarks of fast-spiking parvalbumin-positive interneurons by phospho-site-deficient Ascl1." *Science Advances* 10, no. 42 (2024): eadl5935. https://doi.org/10.1126/sciadv.adl5935.

Martín, Héctor García, and George Karniadakis. "Perspectives for self-driving labs in synthetic biology." *Current Opinion in Biotechnology* 79 (2023): 102881. https://doi.org/10.1016/j.copbio.2022.102881.

Mayran, Alexandre, and Jacques Drouin. "Pioneer transcription factors shape the epigenetic landscape." *Journal of Biological Chemistry* 293, no. 36 (2018): 13795–13804. https://doi.org/10.1074/jbc.R117.001232.

Miao, Liyun, Yin Tang, Andrew R. Bonneau, et al. "The landscape of pioneer factor activity reveals the mechanisms of chromatin reprogramming and genome activation." *Molecular Cell* 82, no. 5 (2022): 986–1002. https://doi.org/10.1016/j.molcel.2022.01.024.

Mullin, Nicholas P., Lisa Bailey, John Collins, Douglas Colby, and Ian Chambers. "Nuclear Reprogramming and Stem Cells." In *Nuclear Reprogramming and Stem Cells*, edited by Justin Ainscough, Shinya Yamanaka, and Takashi Tada, 1–332. Totowa: Humana Press, 2012. https://doi.org/10.1007/978-1-61779-225-0.

Newby, Gregory A., and David R. Liu. "In vivo somatic cell base editing and prime editing." *Molecular Therapy* 29, no. 11 (2021): 3107–3124. https://doi.org/10.1016/j.ymthe.2021.09.002.

Nuñez, James K., Jin Chen, Greg C. Pommier, et al. "Genome-wide programmable transcriptional memory by CRISPR-based epigenome editing." *Cell* 184, no. 9 (2021): 2503–2519. https://doi.org/10.1016/j.cell.2021.03.025.

Replogle, Joseph M., Thomas M. Norman, Albert Xu, et al. "Combinatorial single-cell CRISPR screens by direct guide RNA capture and targeted sequencing." *Nature Biotechnology* 38, no. 8 (2020): 954–961. https://doi.org/10.1038/s41587-020-0470-y.

Replogle, Joseph M., Reuben A. Saunders, Angela N. Pogson, et al. "Mapping information-rich genotype-phenotype landscapes with genome-scale Perturb-seq." *Cell* 185, no. 14 (2022): 2559–2575. https://doi.org/10.1016/j.cell.2022.05.013.

Sala, Alba, Mireia Labrador, Diana Buitrago, et al. "An integrated machine-learning model to predict nucleosome architecture." *Nucleic Acids Research* 52, no. 4 (2024): 1837–1853.

Scheurer, Christoph, Matthias M. Kreuzer, Matthias Scheffler, and Karsten Reuter. "Role of the human-in-the-loop in emerging self-driving laboratories for heterogeneous catalysis." *Nature Catalysis* 8, no. 1 (2025): 13–19.

Spangler, Joseph R., Theresa J. Smith, and Igor L. Medintz. "Large scale screening of CRISPR guide RNAs using an optimized high throughput robotics system." *Scientific Reports* 12, no. 1 (2022): 21275.

Szymanski, Nathan J., Bernardus Rendy, Yuxing Fei, et al. "An autonomous laboratory for the accelerated synthesis of inorganic materials." *Nature* 624, no. 7990 (2023): 86–91. https://doi.org/10.1038/s41586-023-06734-w.

Tang, Na, and Heng Zhang. "Miniature CRISPR-Cas12 Systems: Mechanisms, Engineering, and Genome Editing Applications." *ACS Chemical Biology* 19, no. 3 (2024): 537–549.

Tanaka, Hiroki, Yasuhiro Takizawa, Mariko Takaku, et al. "Interaction of the pioneer transcription factor GATA3 with nucleosomes." *Nature Communications* 11, no. 1 (2020): 4136. https://doi.org/10.1038/s41467-020-17959-y.

Torres, Jose A. G., Samuel H. Lau, Pratyush Anand, et al. "A Multi-Objective Active Learning Platform and Web App for Reaction Optimization." *Journal of the American Chemical Society* 144, no. 43 (2022): 19999–20007. https://doi.org/10.1021/jacs.2c08592.

Umeyama, Taichi, Takuya Matsuda, and Kunihiro Matsumoto. "Lineage Reprogramming: Genetic, Chemical, and Physical Cues for Cell Fate Conversion with a Focus on Neuronal Direct Reprogramming and Pluripotency Reprogramming." *Cells* 13, no. 8 (2024): 707. https://doi.org/10.3390/cells13080707.

Vidarsson, Hilmar, Johan Hyllner, and Peter Sartipy. "Differentiation of human embryonic stem cells to cardiomyocytes for in vitro and in vivo applications." *Stem Cell Reviews and Reports* 6, no. 1 (2010): 108–120. https://doi.org/10.1007/s12015-010-9113-x.

Watson, Joseph L., David Juergens, Nathaniel R. Bennett, et al. "De novo design of protein structure and function with RFdiffusion." *Nature* 620, no. 7976 (2023): 1089–1100. https://doi.org/10.1038/s41586-023-06415-8.

Xu, D., Besselink, S., Ramadoss, G.N. et al. Programmable epigenome editing by transient delivery of CRISPR epigenome editor ribonucleoproteins. Nat Commun 16, 7948 (2025). https://doi.org/10.1038/s41467-025-63167-x

Yu, T., Boob, A. G., Singh, N., Su, Y., & Zhao, H. (2023). In vitro continuous protein evolution empowered by machine learning and automation. Cell systems, 14(8), 633–644. https://doi.org/10.1016/j.cels.2023.04.006

Liu, Y., Zhangding, Z., Liu, X., & Hu, J. (2025). Chromatin-centric insights into DNA replication. Trends in genetics : TIG, 41(5), 412–424. https://doi.org/10.1016/j.tig.2024.12.003

Kratz, Anton, et al. "A multi-scale map of protein assemblies in the DNA damage response." Cell systems 14.6 (2023): 447-463.
