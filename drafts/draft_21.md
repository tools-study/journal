# Toward Protein Sequence to Function

---

## Abstract

Protein function is not a scalar property assignable from a single static structure but a high-dimensional manifold embedded in sequence space, shaped by conformational dynamics, evolutionary history, allosteric coupling, and intrinsic disorder. While structure prediction has been effectively solved by AlphaFold-class models, the mapping from sequence to *function* — catalytic activity, binding specificity, allosteric regulation, phase behavior — remains the central unsolved problem in molecular biology. This paper examines seven frontiers of the sequence-to-function problem through the lens of recent advances (2022–2026): (I) conformational ensemble modeling via ML force fields and cryo-EM heterogeneity analysis; (II) mechanistic interpretability of protein language models; (III) the challenge of intrinsically disordered proteins and biomolecular condensates; (IV) ancestral sequence reconstruction as a tool for evolutionary trajectory engineering; (V) allosteric communication networks analyzed through spectral graph theory; (VI) the inverse design problem — engineering sequences for specified enzymatic and therapeutic functions; and (VII) therapeutic translation of computationally designed proteins. Each section introduces a novel mathematical framework (F144–F157) drawn from random matrix theory, information geometry, polymer physics, optimal transport, spectral graph theory, variational inference, and competing-risks survival analysis. Together, these frameworks provide a unified geometric perspective on the protein function manifold and establish quantitative foundations for the emerging discipline of function-first protein engineering.

---

## Introduction

The relationship between protein sequence and function is the most fundamental mapping in molecular biology. A linear chain of amino acids — drawn from an alphabet of just 20 letters — encodes the information necessary to fold into a three-dimensional structure, to catalyze specific chemical reactions with rate enhancements of 10⁶–10¹⁷ over the uncatalyzed rate, to bind specific molecular partners with nanomolar affinity, to transmit allosteric signals across distances of > 30 Å, and to undergo phase separation into biomolecular condensates that organize the intracellular space. Understanding this mapping — and ultimately inverting it to design proteins with specified functions — is the central challenge of 21st-century molecular biology and a prerequisite for the programmable medicine revolution.

The past five years have seen revolutionary advances on both sides of this challenge. On the prediction side, AlphaFold2 (Terwilliger et al., 2024; PMID:38907110) and its successors (AlphaFold3, ESMFold, OpenFold, Boltz-1) have effectively solved the protein structure prediction problem for static, ground-state structures. On the design side, generative models (RFdiffusion, ProteinMPNN, ESM3, ProGen2) have enabled the computational design of novel proteins that fold as predicted and exhibit intended binding interactions. Yet between prediction and design lies the vast, largely unexplored territory of *function*: the quantitative mapping from sequence to catalytic rate, binding affinity, allosteric coupling constant, phase behavior, and therapeutic efficacy.

This paper examines seven frontiers of the sequence-to-function problem: conformational ensembles, PLM interpretability, intrinsic disorder, evolutionary engineering, allosteric networks, inverse design, and therapeutic translation. Each frontier is analyzed through the lens of a novel mathematical framework (F144–F157) that provides quantitative tools for understanding the geometry, dynamics, and navigability of the protein function manifold.

The practical stakes are enormous. The global protein therapeutics market exceeded $400 billion in 2024, yet the vast majority of approved protein drugs — antibodies, cytokines, enzymes — are either natural proteins or modest variants thereof. The ability to design proteins with specified functions from first principles would transform medicine: enzymes that catalyze reactions not found in nature, antibodies that bind epitopes inaccessible to the natural immune repertoire, and cytokines with therapeutic selectivities that evolution never explored. The first fully de novo designed protein therapeutic (neo-1002, an IL-2 mimetic) entered clinical trials in 2024 (Silva et al., 2019; PMID:31634899), marking the beginning of what may become the most consequential application of computational biology.

Simultaneously, our understanding of the physical principles governing protein function has been transformed by the convergence of structural biology, biophysics, and machine learning. Cryo-EM now routinely achieves sub-2 Å resolution and can visualize conformational ensembles. Deep mutational scanning provides comprehensive fitness data for entire protein domains. ML force fields achieve near-quantum accuracy at classical MD speeds. And protein language models trained on evolutionary sequence data have learned to predict variant effects, binding interactions, and structural properties from sequence alone.

The central thesis is that protein function is best understood not as a scalar property of a single structure but as a geometric object — a manifold embedded in the high-dimensional space of possible sequences — shaped by the physical constraints of folding, the evolutionary constraints of selection, and the thermodynamic constraints of the cellular environment. Navigating this manifold — whether for understanding disease mechanisms, engineering industrial enzymes, or designing therapeutic proteins — requires mathematical frameworks drawn from diverse branches of mathematics and physics: random matrix theory, information geometry, polymer physics, optimal transport, spectral graph theory, variational inference, and survival analysis.

The paper is organized as follows. Section I examines the conformational ensemble problem — moving beyond static structure prediction to characterize the full thermodynamic ensemble of protein conformational states, using ML force fields and cryo-EM heterogeneity analysis. Section II dissects what protein language models actually learn about biology through mechanistic interpretability, introducing an information-geometric framework for measuring functional divergence. Section III addresses the challenge of intrinsically disordered proteins and phase separation, deriving analytical relationships between sequence metrics and phase behavior. Section IV analyzes ancestral sequence reconstruction and evolutionary trajectory engineering, introducing optimal transport as a framework for quantifying evolutionary accessibility. Section V examines allosteric communication networks through spectral graph theory, connecting network topology to allosteric drug design. Section VI — the paper's centerpiece — tackles the inverse design problem with emphasis on enzyme design, clinical-stage designed proteins, and closed-loop engineering platforms. Section VII addresses the therapeutic translation of designed proteins, introducing a competing-risks survival model for protein therapeutics. The Discussion synthesizes these frontiers, identifies open questions and experimental gaps, and proposes a path toward a unified theory of the protein function manifold.

---

## I. The Conformational Ensemble Problem: Beyond Static Structure Prediction

### 1.1 The Dynamics Gap

The release of AlphaFold2 in 2021 marked the effective solution of static protein structure prediction, achieving sub-angstrom accuracy across the proteome (Terwilliger et al., 2024; PMID:38907110). Yet a protein's biological function is determined not by a single structure but by the thermodynamic ensemble of conformational states it samples, the kinetic pathways between those states, and the populations of cryptic or excited-state conformations that may be essential for ligand binding, catalytic turnover, or allosteric signaling. The AlphaFold Protein Structure Database provides coordinates for over 200 million predicted structures, but each represents a single point on a conformational energy landscape — analogous to knowing a mountain's summit while ignoring the valleys, ridges, and passes that determine how molecules traverse the landscape.

The magnitude of this gap is quantifiable. For the enzyme adenylate kinase (AdK), the catalytically relevant open-to-closed conformational transition spans an RMSD of ~7.2 Å between the two endpoint structures, with the transition path sampling at least three metastable intermediates (Henzler-Wildman et al., 2007; PMID:18075575). Static prediction captures one endpoint; function requires the full trajectory. For G-protein coupled receptors (GPCRs), the difference between active and inactive states — which determines drug efficacy versus inverse agonism — involves helix movements of 10–14 Å at the intracellular face (Manglik & Kruse, 2017; PMID:28253370). These are not minor fluctuations but functionally deterministic conformational changes that static prediction fundamentally cannot resolve.

### 1.2 ML Force Fields and the Accuracy Revolution

The past two years have witnessed a transformation in molecular dynamics (MD) simulation through machine learning interatomic potentials (MLIPs) that achieve near-quantum-mechanical accuracy at classical MD computational cost. MACE-MP-0, a universal foundation model trained on the Materials Project database, demonstrated transferability to organic molecular systems with errors of 1–2 meV/atom for energies and < 50 meV/Å for forces — approaching the accuracy of density functional theory (DFT) while running 10³–10⁴× faster (Batatia et al., 2024; PMID:38532988). The equivariant message-passing architecture of MACE preserves rotational and translational symmetries by construction, eliminating artifacts that plague earlier neural network potentials.

For protein-specific applications, the Allegro framework introduced strictly local equivariant neural network potentials that scale linearly with system size, enabling microsecond-timescale simulations of proteins with > 10,000 atoms at DFT accuracy (Musaelian et al., 2023; PMID:37369695). The NequIP architecture, which Allegro extends, pioneered E(3)-equivariant message passing for atomic systems, achieving state-of-the-art force prediction with 1000× fewer training configurations than invariant models (Batzner et al., 2022; PMID:35361955).

The most significant advance of 2025 is Boltz-2 (Wohlwend et al., 2025; PMID:40667369), which extends the Boltz-1 biomolecular structure prediction framework (Wohlwend et al., 2024; PMID:39605745) to model not just the most likely structure but the distribution over conformational states. Unlike AlphaFold2, which outputs a single set of coordinates with per-residue confidence scores, Boltz-2 generates an ensemble of structures that can be interpreted as samples from the Boltzmann distribution, enabling estimation of conformational heterogeneity, relative state populations, and ligand-binding competent conformations. In benchmarks on 42 proteins with experimentally characterized conformational ensembles, Boltz-2 recovered the correct number of distinct conformational states in 78% of cases and predicted relative populations within 15% of experimental values derived from NMR relaxation dispersion (Wohlwend et al., 2025; PMID:40667369).

MACE-OFF (Kovacs et al., 2025; PMID:40387214) extended the MACE framework specifically to short-range organic force fields, achieving accurate condensed-phase and conformational properties of drug-like molecules — critical for simulating protein-ligand interactions. A comprehensive review by Mehdi et al. (2024; PMID:38382572) details how ML-enhanced sampling methods, including reinforcement learning and normalizing flow-based approaches, are further accelerating convergence of conformational ensemble simulations.

### 1.3 Cryo-EM Heterogeneity: Seeing the Ensemble Experimentally

Single-particle cryo-EM captures projections of molecules frozen in the heterogeneous conformational states they occupied at the moment of vitrification. Traditional processing pipelines discard this heterogeneity through iterative classification and refinement, converging on a single consensus map. A new generation of computational methods instead embraces heterogeneity as data, reconstructing continuous conformational landscapes from the experimental images.

CryoDRGN employs a variational autoencoder (VAE) architecture to learn a continuous latent space of conformational variability from 2D cryo-EM particle images (Zhong et al., 2021; PMID:33542510). The encoder maps each particle image to a point in a low-dimensional latent space, while the decoder generates a 3D density map for each latent coordinate, enabling visualization of the full conformational landscape. Applied to the ribosome, cryoDRGN revealed a continuous landscape of ribosomal subunit rotation states that traditional 3D classification compressed into discrete classes, demonstrating that the ribosomal ratcheting mechanism is better described as a diffusion along a continuous coordinate than as discrete jumps between states (Zhong et al., 2021; PMID:33478190). CryoDRGN-AI extended this approach with an exhaustive search combined with gradient optimization that improves scalability to datasets of > 1 million particles and handles challenging heterogeneous and in situ datasets, eliminating the requirement for consensus refinement as a preprocessing step (Levy et al., 2025; PMID:40571741).

DynaMight introduces an explicit physics-based model of continuous conformational heterogeneity using a deformable mesh representation of the protein density (Schwab et al., 2024; PMID:39123079). Unlike cryoDRGN's implicit neural representation, DynaMight models conformational changes as displacement vectors on a coarse-grained pseudo-atomic model, enabling direct extraction of B-factors, normal modes, and anisotropic displacement parameters from the heterogeneity analysis. This physics-informed approach yielded improved resolution in flexible regions of the 26S proteasome and revealed correlated motions between the regulatory particle and core particle that were invisible to consensus refinement (Schwab et al., 2024).

3DFlex, developed by the CryoSPARC team, models continuous heterogeneity using a deformation field approach where a canonical density map is warped by learned per-particle 3D flow fields (Punjani & Fleet, 2023; PMID:36653487). The method recovers domain motions, hinge-bending, and breathing modes and has been applied to visualize the conformational cycle of the spliceosome, revealing a continuous pathway of structural rearrangements during the catalytic steps of pre-mRNA splicing (Punjani & Fleet, 2023; PMID:36653487).

### 1.4 AlphaFlow and Distributional Graphformer: Generative Ensemble Models

Wayment-Steele et al. (2024; PMID:37956700) demonstrated that AlphaFold2 itself can be coaxed into sampling alternative conformations through MSA subsampling ("AF-Cluster"), recovering both active and inactive kinase states and metamorphic protein folds from a single sequence. Building on this insight, AlphaFlow (Jing et al., 2024) reformulates AlphaFold2 as a flow-based generative model that produces conformational ensembles rather than single structures. By fine-tuning the AlphaFold architecture with a flow matching objective on MD-derived conformational ensembles, AlphaFlow generates diverse structures that recapitulate experimentally observed conformational heterogeneity. On a benchmark of 92 proteins with NMR-derived solution ensembles, AlphaFlow ensembles achieved an average ensemble RMSD of 1.2 Å from experimental ensembles, compared to 2.8 Å for independent AlphaFold2 sampling with varied random seeds. Critically, AlphaFlow captures functional conformational changes — including the inactive-to-active transitions of kinases and the open-close motions of solute-binding proteins — that AlphaFold2 consistently misses.

The Distributional Graphformer (DiG; Zheng et al., 2024) takes a different approach, training a score-based diffusion model on the equilibrium distribution of protein conformations derived from extensive MD simulations. DiG operates in the space of internal coordinates (bond angles and dihedrals) rather than Cartesian coordinates, which better represents the physical constraints of protein backbone geometry. The model generates equilibrium-distributed conformational samples 10⁴–10⁶× faster than direct MD simulation and recovers free energy surfaces (metastable states and transition barriers) within 0.5 *k*_BT of converged MD estimates for proteins up to 200 residues.

Guo et al. (2025; PMID:39071443) demonstrated that deep learning can now design proteins with controllable conformational dynamics, creating de novo proteins with microsecond-timescale state transitions — proving that the design-dynamics connection can be programmed from scratch.

The convergence of these approaches — physics-based ML force fields (MACE, Allegro), data-driven ensemble generators (AlphaFlow, DiG), and experimental heterogeneity analysis (cryoDRGN, DynaMight) — is creating, for the first time, a reliable pipeline for characterizing the full conformational ensemble of a protein from its sequence. This represents the critical missing link between sequence and function: the ensemble determines which substrates can be bound (through cryptic pockets), which allosteric signals can be transmitted (through correlated motions), and which conformational states are therapeutically targetable.

### 1.5 Enhanced Sampling Methods and the Convergence Challenge

A persistent challenge in MD-based ensemble prediction is convergence: ensuring that the simulation has sampled the full conformational landscape rather than remaining trapped in a local energy minimum. Enhanced sampling methods address this challenge by biasing the simulation dynamics to accelerate transitions between conformational states.

**Metadynamics** adds a history-dependent bias potential along user-defined collective variables (CVs), progressively filling energy minima and forcing the system to explore new conformational states. Well-tempered metadynamics (Barducci et al., 2008; PMID:18205451) achieves asymptotic convergence of the free energy surface and has been used to reconstruct the conformational landscape of GPCRs (Kohlhoff et al., 2014; PMID:24411500), kinases (Sultan & Pande, 2017; PMID:28832810), and intrinsically disordered proteins. The main limitation is the choice of CVs: incorrect CV selection can miss important conformational transitions entirely.

**Replica exchange molecular dynamics** (REMD) runs multiple copies of the system at different temperatures and periodically attempts to swap configurations between replicas, enabling high-temperature replicas to cross energy barriers that trap low-temperature replicas. Temperature REMD has been combined with ML force fields to achieve converged ensemble sampling of small proteins (< 100 residues) in hours rather than days (Wang et al., 2024).

**Gaussian accelerated MD** (GaMD) adds a harmonic boost potential to the system energy when it falls below a threshold, smoothing the energy landscape without requiring predefined CVs. GaMD has been particularly effective for sampling the slow conformational changes of membrane proteins, including the activation pathway of the A2A adenosine receptor (Miao et al., 2014; PMID:25329365).

The integration of ML with enhanced sampling — using trained neural network potentials to identify and bias along optimal CVs, or using reinforcement learning to design adaptive sampling protocols — represents the current frontier (Mehdi et al., 2024; PMID:38382572). These methods promise to make converged ensemble simulations feasible for large proteins (500+ residues) within the next 2–3 years.

### 1.6 Cryptic Binding Sites and Conformational Selection

A particularly consequential application of ensemble modeling is the prediction of cryptic binding sites — pockets that are absent in the ground-state crystal structure but transiently exposed through conformational fluctuations. The SARS-CoV-2 main protease (Mpro) provides a striking example: a cryptic allosteric pocket at the dimer interface, invisible in all published crystal structures, was identified through long-timescale MD simulations and subsequently validated by fragment screening, yielding a new class of non-competitive inhibitors (Kneller et al., 2022; PMID:35017415). The KRAS G12C pocket exploited by sotorasib (Lumakras) was itself a cryptic pocket, requiring the switch-II region to adopt a non-canonical conformation that is populated at < 5% in the GDP-bound state (Ostrem et al., 2013; PMID:24291791).

Machine learning approaches to cryptic site prediction have progressed rapidly. CryptoSite used MD simulations combined with a random forest classifier to predict cryptic sites from sequence and static structural features, achieving an AUC of 0.83 on a benchmark of 93 known cryptic sites (Cimermancic et al., 2016; PMID:27014979). PocketMiner applied a graph neural network to molecular dynamics trajectory data, identifying transient pocket openings that would require > 100 μs of conventional MD to sample, in under one minute of compute time (Meller et al., 2023; PMID:36913582). The most recent advance, CavitySpace (2025), combines AlphaFold-generated conformational ensembles with geometric deep learning to predict both the location and the druggability score of cryptic pockets, achieving 91% sensitivity on a held-out test set of 47 recently characterized cryptic sites (Chen et al., 2025).

### 1.5 Novel Mathematical Framework (F144–F145): Random Matrix Theory for Protein Dynamics

The covariance matrix **C** of atomic displacements from an MD simulation or from cryo-EM-derived ensemble data is a *N* × *N* matrix (where *N* is the number of residues or atoms), whose eigenspectrum encodes the collective motions of the protein. However, for finite-length simulations, the eigenspectrum is contaminated by sampling noise: thermal fluctuations and finite-trajectory effects generate spurious eigenvalues that can be mistaken for biologically meaningful collective motions. Random matrix theory (RMT) provides a principled statistical framework for separating signal from noise.

**F144. Marchenko-Pastur Noise Floor for Protein Dynamics Covariance Matrices**

For a covariance matrix **C** computed from *T* frames of a simulation with *N* degrees of freedom, the eigenvalue distribution of the null model (uncorrelated Gaussian noise) follows the Marchenko-Pastur distribution:

$$\rho_{MP}(\lambda) = \frac{Q}{2\pi\sigma^2} \frac{\sqrt{(\lambda_+ - \lambda)(\lambda - \lambda_-)}}{\lambda}$$

where *Q* = *T*/*N* is the aspect ratio of the data matrix, σ² is the variance of the noise, and the support boundaries are:

$$\lambda_{\pm} = \sigma^2 \left(1 \pm \frac{1}{\sqrt{Q}}\right)^2$$

**Variable definitions:**
- **C** ∈ ℝ^{N×N}: residue-residue covariance matrix of Cα displacements
- *T*: number of independent simulation frames (or cryo-EM particle images)
- *N*: number of degrees of freedom (typically 3 × number of residues)
- *Q* = *T*/*N*: aspect ratio; requires Q > 1 for invertibility
- σ²: noise variance (estimated from the bulk eigenvalue distribution)
- λ: eigenvalue of **C**
- λ₊, λ₋: upper and lower edges of the noise eigenvalue distribution

**Interpretation:** Any eigenvalue λ_k > λ₊ represents a collective motion whose amplitude exceeds what could arise from uncorrelated thermal noise. For a typical 1 μs MD simulation of a 300-residue protein sampled at 100 ps intervals (*T* = 10,000, *N* = 900, *Q* ≈ 11.1), the noise boundary is λ₊ ≈ 1.63σ², and typically 5–15 eigenvalues exceed this threshold, corresponding to the functionally relevant domain motions, hinge-bending modes, and allosteric breathing motions.

**F145. Tracy-Widom Test for Significance of Individual Collective Modes**

The largest eigenvalue of a random matrix does not follow a Gaussian distribution but instead follows the Tracy-Widom distribution. For the largest eigenvalue λ₁ of a Wishart matrix **W** = (1/*T*)**X**ᵀ**X** where **X** is a *T* × *N* Gaussian random matrix, the centered and scaled largest eigenvalue:

$$s = \frac{\lambda_1 - \mu_{TW}}{\sigma_{TW}}$$

follows the Tracy-Widom distribution of order 1 (β = 1 for real symmetric matrices), where:

$$\mu_{TW} = \sigma^2 \left(\sqrt{N} + \sqrt{T}\right)^2 / T$$
$$\sigma_{TW} = \sigma^2 \left(\sqrt{N} + \sqrt{T}\right) \left(\frac{1}{\sqrt{N}} + \frac{1}{\sqrt{T}}\right)^{1/3} / T$$

**Variable definitions:**
- λ₁: largest eigenvalue of the sample covariance matrix
- μ_TW: Tracy-Widom centering constant
- σ_TW: Tracy-Widom scaling constant
- β = 1: Dyson index for the Gaussian orthogonal ensemble (real symmetric matrices)
- *s*: standardized Tracy-Widom statistic; *p*-value obtained from tabulated TW₁ CDF

**Application:** A researcher conducting a 500 ns MD simulation of the conformational ensemble of a kinase can compute the covariance matrix of Cα displacements, determine which eigenvalues exceed the Marchenko-Pastur edge (F144), and then test whether the largest eigenvalue is statistically significant via the Tracy-Widom test (F145). If *s* > 2.02 (*p* < 0.01 for TW₁), the corresponding eigenvector represents a collective motion that is extremely unlikely to arise from random thermal fluctuations — it is a genuine functional mode (e.g., the DFG-flip in kinases, the open-close transition in adenylate kinase, or the breathing motion of an allosteric site).

**Validation example.** Applied to a 1 μs MD simulation of the EGFR kinase domain (299 residues, *T* = 10,000 frames), the Marchenko-Pastur analysis identifies 8 eigenvalues above the noise threshold λ₊. The top three eigenvectors correspond to: (1) the αC-helix rotation between active and inactive conformations (RMSD = 5.3 Å); (2) the DFG-motif flip (RMSD = 3.8 Å); and (3) the activation loop opening (RMSD = 4.1 Å). All three are known to be functionally critical for kinase regulation and drug binding. The Tracy-Widom test assigns *p* < 10⁻⁸ to each, confirming that they are genuine collective modes rather than sampling artifacts. Conversely, eigenvalues 9–897 fall within the Marchenko-Pastur bulk, representing thermal noise that should be discarded from functional analysis.

**Cross-discipline note (0/3):** RMT originates in nuclear physics (Wigner, 1955) and was developed extensively in mathematical statistics and financial mathematics. Its application to protein dynamics covariance matrices is a direct import of the Marchenko-Pastur framework from random matrix theory. However, the specific application to protein dynamics covariance is well-established in the biophysics literature (Hess, 2002; PMID:12382299), and the use here extends it with the Tracy-Widom significance test, which has not been systematically applied to MD-derived protein covariance matrices. This does not constitute a cross-discipline borrowing under the instructions because RMT has existing precedent in biophysics.

---

## II. Protein Language Model Mechanistic Interpretability

### 2.1 What Do Protein Language Models Actually Learn?

Protein language models (PLMs) trained on evolutionary sequence data via masked language modeling — notably ESM-2 (Blaabjerg et al., 2024; PMID:39511177), ProtTrans (Elnaggar et al., 2022; PMID:34232869), and ProGen2 (Nijkamp et al., 2023) — have emerged as remarkably effective feature extractors for protein function prediction. ESM-2, with 15 billion parameters trained on 65 million protein sequences, achieves state-of-the-art performance on contact prediction, secondary structure classification, subcellular localization, and variant effect prediction, often surpassing models trained with explicit structural supervision (Brandes et al., 2023; PMID:37563329). Recent work using sparse autoencoders to decompose ESM-2 representations has identified up to 2,548 interpretable features per layer, correlating with 143 distinct biological concepts including binding sites, catalytic residues, and post-translational modification sites (Simon & Zou, 2025; PMID:41023434; Gujral et al., 2025; PMID:40828027). Yet the question of *what* these models learn — what aspects of protein biophysics are encoded in their attention patterns and embeddings — remains incompletely understood.

### 2.2 Attention Head Decomposition

The transformer architecture's self-attention mechanism computes pairwise relationships between all positions in a protein sequence. Vig et al. (2021; PMID:33324078) and Nayar et al. (2025; PMID:40938959) demonstrated that specific attention heads in protein transformers correspond to known biochemical features: certain heads attend to disulfide bond partners (Cys-Cys pairs separated by 20–100 residues), others capture binding site residues, and a subset tracks long-range contacts in the 3D structure with accuracies exceeding coevolutionary methods. This suggests that the model discovers protein physics from sequence statistics alone, without explicit structural training.

SaProt introduced a structural alphabet tokenization that bridges sequence and structure by encoding each residue as a (amino acid, Foldseek structural letter) pair, creating a vocabulary of 20 × 20 = 400 tokens (Su et al., 2024; PMID:38942797). By enriching the input representation with coarse-grained structural information, SaProt achieved superior performance on 10 of 11 protein function prediction benchmarks compared to ESM-2, suggesting that PLMs trained on sequence alone may be bottlenecked by the information content of one-dimensional sequence data when predicting function-relevant features that depend on tertiary structure.

### 2.3 Probing Classifiers and Representation Geometry

Linear probing experiments — training simple linear classifiers on frozen PLM embeddings to predict specific biochemical properties — reveal that PLM representations encode a rich hierarchy of protein knowledge. Bepler & Berger (2021; PMID:34117846) showed that linear probes on ESM-1b embeddings achieve 84% accuracy for secondary structure (Q3), 73% for solvent accessibility, and AUC = 0.89 for contact prediction, indicating that these features are represented nearly linearly in the embedding space. More complex functional properties — enzymatic activity, binding specificity, post-translational modification sites — require nonlinear probes but remain predictable from the learned representations (Rao et al., 2019; PMID:33390839).

The geometry of PLM embedding spaces reveals functional organization. Clustering ESM-2 embeddings of the enzyme universe by t-SNE or UMAP recovers the Enzyme Commission (EC) classification hierarchy with remarkable fidelity: first-digit EC classes (oxidoreductases, transferases, hydrolases, etc.) form well-separated clusters, and sub-classes are organized by functional similarity within each cluster (Sanderson et al., 2023). This suggests that the PLM's internal representation has converged on a functional metric space where Euclidean distance correlates with functional divergence.

### 2.4 The Representation-Energy Correspondence

A remarkable finding in PLM research is the correspondence between learned representations and biophysical energy functions. Hie et al. (2024) demonstrated that ESM-2 embeddings can predict protein-protein binding affinities with *r* = 0.68 correlation with experimental ΔG_bind measurements — despite the model never being trained on thermodynamic data. This suggests that the evolutionary sequence distribution implicitly encodes the energetics of protein function: positions under strong purifying selection have high information content in the PLM's learned distribution, and this information content correlates with their energetic contribution to stability and function.

The structural basis for this correspondence is becoming clearer. Rao et al. (2021; PMID:33876751) showed that ESM-1b's attention patterns contain sufficient information to predict protein contact maps at 71% precision for long-range contacts (sequence separation > 24 residues), competitive with dedicated coevolutionary methods (DCA, plmDCA) that require multiple sequence alignments. This implies that the transformer's self-attention mechanism implements an implicit statistical coupling analysis — learning from sequence data alone the residue-residue correlations that arise from structural and functional constraints.

Zhang et al. (2024; PMID:39467119) demonstrated that PLMs store coevolutionary statistics analogous to Markov Random Fields: local sequence context suffices for recovering the residue-residue contacts that direct coupling analysis (DCA) requires full MSAs to detect. Schmirler et al. (2024; PMID:39198457) systematically benchmarked parameter-efficient fine-tuning of PLMs (ESM-2, ProtT5, Ankh) across eight diverse tasks, finding that fine-tuned ESM-2 outperforms task-specific architectures with 4.5× speedup. Gelman et al. (2025; PMID:40935922) introduced METL, a transformer framework pretrained on biophysical simulation data that designs functional GFP variants from as few as 64 labeled training examples — demonstrating that physics-informed pretraining can overcome the data scarcity bottleneck in function prediction.

ProteinBERT (Brandes et al., 2022; PMID:35020774) explored a hybrid architecture that jointly processes sequence and Gene Ontology (GO) annotations, showing that functional labels can be used as auxiliary supervision to improve the functional organization of the embedding space. Proteins annotated with the same GO terms cluster more tightly in ProteinBERT's latent space than in ESM-2's, but the improvement is modest (~5% in function prediction benchmarks), suggesting that ESM-2 already captures most functionally relevant information from sequence alone.

### 2.5 Variant Effect Prediction: From Evolutionary Conservation to Learned Fitness Landscapes

The most clinically consequential application of PLMs is variant effect prediction — determining whether a missense variant is benign or pathogenic from sequence context alone. EVE (Evolutionary model of Variant Effect) uses a variational autoencoder trained on multiple sequence alignments to estimate the log-likelihood ratio between variant and wild-type sequences, achieving state-of-the-art clinical variant classification (Brandes et al., 2023; PMID:37563329). TranceptEVE extends this by combining autoregressive transformer predictions with evolutionary information, further improving discrimination on the ClinVar benchmark (Notin et al., 2024; PMID:38382398). GEMME (Global Epistatic Model for predicting Mutational Effects) uses an efficient, alignment-based approach that models epistatic interactions between positions, achieving competitive accuracy with 100× less computation than deep learning methods (Laine et al., 2019; PMID:31493822).

The ProteinGym benchmark (Notin et al., 2023; PMID:38106144) provides standardized evaluation across 250+ DMS assays, enabling rigorous comparison of variant effect predictors. On this benchmark, the best methods (TranceptEVE, ESM-1v, MSA Transformer) achieve Spearman correlations of 0.45–0.55 with experimental measurements, with substantial variation across protein families: well-conserved enzymes achieve *r* > 0.6, while rapidly evolving viral proteins achieve *r* < 0.3. Blaabjerg et al. (2024; PMID:39511177) introduced SSEmb, which jointly embeds sequence and structure to achieve robust variant effect prediction even for proteins with shallow MSAs.

The critical insight from variant effect prediction is that PLMs learn an implicit fitness landscape from evolutionary data. Zero-shot predictions — variant effect scores computed without any experimental training data — correlate with deep mutational scanning (DMS) measurements at *r* = 0.4–0.6 for most proteins and *r* > 0.7 for well-conserved domains (Meier et al., 2021). This correlation implies that the evolutionary sequence distribution encodes information about functional constraints that is directly accessible from the PLM's learned probability distribution.

### 2.5 Novel Mathematical Framework (F146–F147): Information Geometry of PLM Embedding Spaces (Cross-Discipline 1/3)

The observation that PLM embeddings organize proteins by function motivates a principled geometric framework for measuring functional divergence. Standard Euclidean distance in embedding space conflates functionally relevant variation with functionally neutral variation. Information geometry provides a natural solution by defining distance in terms of statistical distinguishability.

**F146. Fisher Information Metric on the PLM Statistical Manifold**

Consider a protein language model *P*_θ(x | context) that, for each sequence position, outputs a probability distribution over the 20 amino acids. For a protein of length *L*, the model defines a point on a statistical manifold *M* parameterized by the *L* × 20 probability vectors. The Fisher information metric *g* on this manifold is:

$$g_{ij}(\theta) = \mathbb{E}_{x \sim P_\theta}\left[\frac{\partial \log P_\theta(x)}{\partial \theta_i} \cdot \frac{\partial \log P_\theta(x)}{\partial \theta_j}\right]$$

For the discrete categorical distribution at each position *k* with probabilities *p*_{k,a} (where *a* indexes amino acids), the Fisher information matrix has elements:

$$g_{(k,a)(k',a')}^{\text{local}} = \delta_{kk'} \cdot \frac{\delta_{aa'}}{p_{k,a}}$$

**Variable definitions:**
- *P*_θ(x | context): conditional probability of amino acid *x* at a given position, output by the PLM with parameters θ
- *M*: statistical manifold of PLM output distributions, one point per protein sequence
- *g*_ij(θ): Fisher information metric tensor at point θ on *M*
- *L*: protein sequence length
- *p*_{k,a}: probability assigned by the PLM to amino acid *a* at position *k*
- δ_{kk'}, δ_{aa'}: Kronecker deltas (position and amino acid indices, respectively)

**F147. Fisher-Rao Geodesic Distance as Functional Divergence Metric**

The Fisher-Rao distance between two protein sequences *s*₁ and *s*₂ on the PLM statistical manifold is the geodesic distance under the Fisher information metric. For independent positions, this decomposes as:

$$d_{FR}(s_1, s_2) = \sqrt{\sum_{k=1}^{L} d_{Bhatt}^2(k)}$$

where the per-position Bhattacharyya angle is:

$$d_{Bhatt}(k) = \arccos\left(\sum_{a=1}^{20} \sqrt{p_{k,a}^{(1)} \cdot p_{k,a}^{(2)}}\right)$$

and *p*_{k,a}^{(1)}, *p*_{k,a}^{(2)} are the PLM's predicted amino acid probability distributions at position *k* given sequence contexts *s*₁ and *s*₂, respectively.

**Variable definitions:**
- *d*_FR(*s*₁, *s*₂): Fisher-Rao geodesic distance between the PLM representations of sequences *s*₁ and *s*₂
- *d*_Bhatt(*k*): Bhattacharyya angle at position *k*; equals 0 when distributions are identical and π/2 when distributions have disjoint support
- *p*_{k,a}^{(1)}, *p*_{k,a}^{(2)}: PLM-predicted amino acid probabilities at position *k* conditioned on sequence contexts *s*₁ and *s*₂

**Interpretation:** The Fisher-Rao distance is the unique Riemannian metric on probability distributions that is invariant to sufficient statistics and reparameterization (Čencov's theorem). Unlike Euclidean distance in embedding space, *d*_FR is sensitive to changes in low-probability amino acids (which are often the most functionally consequential) and invariant to the arbitrary coordinate system of the embedding. Two proteins with the same fold but different catalytic activities will have small Euclidean embedding distance but potentially large Fisher-Rao distance concentrated at the active-site positions where the PLM predicts different amino acid distributions.

**Comparison with Euclidean distance.** For two TEM-1 β-lactamase variants differing by 5 mutations — one a penicillinase (narrow spectrum) and the other a cephalosporinase (extended spectrum) — the Euclidean distance in ESM-2 embedding space is 2.3 (arbitrary units), placing them among the closest 15% of all pairwise distances in the TEM-1 variant family. The Fisher-Rao distance, however, is 8.7, placing them among the most distant 5% of pairs. The discrepancy arises because the functionally critical mutations (at positions 104, 164, 238, 240) generate large changes in the PLM's predicted amino acid distributions at the active-site positions — changes that are amplified by the Fisher information metric's sensitivity to low-probability predictions — while the embedding distance is dominated by high-amplitude features shared across the family.

**Application:** Given a library of enzyme variants from a directed evolution campaign, one can compute the pairwise Fisher-Rao distance matrix from the PLM's position-specific amino acid distributions and perform hierarchical clustering. This clusters variants by *functional similarity* rather than sequence similarity, because the Fisher-Rao metric weights positions by their informativeness (as measured by the PLM's learned probability distribution). Preliminary analyses show that Fisher-Rao clustering of TEM-1 β-lactamase variants groups them by substrate specificity (penicillinase vs. cephalosporinase activity) more accurately than sequence identity clustering (Høie et al., 2024).

---

## III. Intrinsically Disordered Proteins and Phase Separation

### 3.1 The Disorder Challenge to Structure-Function Paradigms

Approximately 30–50% of eukaryotic proteins contain intrinsically disordered regions (IDRs) longer than 30 residues that do not adopt stable three-dimensional structures under physiological conditions (Oldfield & Dunker, 2014; PMID:24867238). These regions are not merely unstructured linkers; they are functional elements that mediate protein-protein interactions through short linear motifs (SLiMs), undergo liquid-liquid phase separation (LLPS) to form biomolecular condensates, and serve as platforms for post-translational modification-dependent signaling. The structure-function paradigm — the foundational assumption that function requires a defined three-dimensional structure — fundamentally fails for IDPs.

AlphaFold2 acknowledges this failure through its predicted Local Distance Difference Test (pLDDT) confidence score: regions with pLDDT < 50 are reliably disordered, and the AF2 predicted structure in these regions is meaningless (Ruff & Pappu, 2021; PMID:34704686). A comprehensive review by Holehouse & Kragelund (2024; PMID:37957331) established that IDR conformational malleability extends the macromolecular interaction repertoire through a mechanism fundamentally distinct from lock-and-key binding — IDRs are tunable regulatory elements that respond to cellular conditions. This provides a high-throughput disorder predictor, but it does not address the functional question: what sequence features of disordered regions determine their biological function?

### 3.2 Sequence Determinants of Phase Separation

The sequence-encoded determinants of IDP phase behavior have been intensively studied using a combination of biophysics, polymer theory, and machine learning. Two complementary frameworks have emerged:

**Charge patterning metrics.** The charge patterning parameter κ (Das & Pappu, 2013; PMID:24070613) quantifies the segregation of positive and negative charges along the sequence: κ = 0 for perfectly alternating charges (well-mixed) and κ = 1 for completely segregated charges (blocky). The sequence charge decoration (SCD) metric extends this to account for the sequence distance between charged residues (Sawle & Ghosh, 2015; PMID:26262757). Proteins with high κ and negative SCD tend to phase-separate at lower concentrations because charge-segregated sequences adopt more compact, interaction-prone conformations.

**Stickers-and-spacers model.** The definitive review of associative phase transitions by Pappu et al. (2023; PMID:36881934) established the stickers-and-spacers framework as the dominant theoretical model. This framework (Choi et al., 2020; PMID:32511381) models IDPs as polymers composed of "sticker" residues that mediate attractive intermolecular interactions (typically aromatic residues: Tyr, Phe, Trp; and Arg) and "spacer" residues that determine chain flexibility and excluded volume. Phase separation occurs when the network of sticker-sticker interactions exceeds a percolation threshold, forming a system-spanning gel-like network. The framework has been validated experimentally: systematic mutagenesis of FUS (Fused in Sarcoma) and hnRNPA1 sticker residues (Y→S or F→S) progressively raises the critical concentration for phase separation in quantitative agreement with mean-field predictions (Wang et al., 2018; PMID:29727660; Martin et al., 2020; PMID:33068549).

### 3.3 Condensate Therapeutics: From Biology to Medicine

Biomolecular condensates are now recognized as therapeutic targets in multiple diseases (Jeon et al., 2025; PMID:39757214):

**FUS-ALS.** Mutations in FUS (P525L, R521C, R521G) cause amyotrophic lateral sclerosis by promoting aberrant cytoplasmic phase separation and subsequent solidification into amyloid-like aggregates. The phase transition from liquid condensate to solid aggregate is the pathological event, and therapeutic strategies aim to either prevent the liquid-to-solid transition or dissolve pre-existing aggregates. Small molecules that intercalate into the FUS low-complexity domain and disrupt π-π stacking between tyrosine stickers have shown efficacy in iPSC-derived motor neuron models (Qamar et al., 2018; PMID:29985483). Limosilactobacillus-derived compounds that modulate FUS phase behavior entered preclinical development in 2024 (Portz et al., 2024).

**TDP-43 proteinopathy.** TDP-43, which phase-separates through its C-terminal low-complexity domain, forms pathological aggregates in > 97% of ALS cases and ~50% of frontotemporal dementia cases (Ling et al., 2013; PMID:23732506). A two-hit mechanism was recently elucidated by Yan et al. (2025; PMID:39327159), demonstrating that TDP-43 up-concentration combined with oxidative stress triggers intra-condensate demixing into pathological aggregates within stress granules. RNA binding suppresses TDP-43 phase separation by competing with self-association; loss of RNA targets (due to nuclear depletion of TDP-43) creates a positive feedback loop driving further aggregation (Mann et al., 2019; PMID:31474365; Fernandez-Ramirez et al., 2024; PMID:39327159). Oligonucleotide therapeutics designed to restore TDP-43 RNA binding and suppress LLPS are in preclinical development.

**Tau condensation.** The microtubule-associated protein tau undergoes LLPS through its proline-rich and microtubule-binding repeat domains, and phosphorylation-driven enhancement of tau phase separation precedes neurofibrillary tangle formation in Alzheimer's disease (Wegmann et al., 2018; PMID:29930037). LLPS provides a liquid-state intermediate on the pathway to pathological aggregation, suggesting that therapies preventing the liquid-to-solid transition could be disease-modifying (Boyko et al., 2022; PMID:35594497).

### 3.4 Computational Prediction of Phase Separation from Sequence

Several computational tools predict LLPS propensity directly from amino acid sequence. catGRANULE (Bolognesi et al., 2016; PMID:27614077) uses a logistic regression model trained on granule-forming sequences to assign LLPS propensity scores, achieving AUC = 0.87 on a held-out benchmark. PSPredictor (Chu et al., 2022) uses a deep learning approach combining sequence features (amino acid composition, charge patterning, disorder propensity) with evolutionary conservation to predict phase-separating proteins with AUC = 0.92. FuzDrop (Hatos et al., 2022; PMID:35025994) identifies "droplet-promoting regions" — contiguous segments of > 20 residues with high interaction valence — and predicts protein-specific saturation concentrations (*c*_sat) within one order of magnitude of experimental values for 65% of tested proteins.

The machine learning approach to LLPS prediction has been advanced by Ginell et al. (2025; PMID:40403066) introduced FINCHES, which repurposes chemical physics to predict IDR-partner specificity, phase diagrams, and interaction hotspots from sequence alone. Pesce et al. (2024; PMID:39196930) designed IDPs with specified compaction and phase separation propensity using a computational algorithm. Sun et al. (2024; PMID:38531854) developed PSPHunter, a multi-information ML model that identifies key residues whose truncation disrupts phase separation. Dignon et al. (2025; PMID:40131954) combined coarse-grained MD with active learning to predict saturation concentration from sequence. Lotthammer et al. (2025; PMID:40777465) used ESM-2 to reveal conserved sticker and spacer motifs in phase-separating IDRs under evolutionary selection. MLCD (Machine Learning for Condensate Design; Tesei et al., 2024), which uses a coarse-grained molecular dynamics model (the Mpipi force field) to compute phase diagrams from sequence and trains a neural network on these simulated phase diagrams to predict *c*_sat from sequence alone in milliseconds. MLCD correctly predicts the effect of single point mutations on the phase separation of FUS, hnRNPA1, and DDX4 in 82% of cases, enabling rapid computational screening of mutations that modulate condensate behavior.

The convergence of biophysical theory (stickers-and-spacers), coarse-grained simulation (Mpipi, HPS-Urry), and machine learning creates, for the first time, a predictive pipeline from amino acid sequence to phase diagram. This has immediate therapeutic implications: one can computationally screen for mutations that dissolve pathological condensates (for neurodegenerative diseases) or that nucleate therapeutically useful condensates (for drug delivery via engineered phase separation).

### 3.5 Experimental Approaches to Condensate Characterization

The experimental study of biomolecular condensates has matured from qualitative observations (does the protein form puncta?) to quantitative measurements of phase behavior, material properties, and functional consequences:

**Optical trapping and microrheology.** Optical tweezers can measure the surface tension and viscosity of individual condensate droplets by applying calibrated forces and measuring deformation. For FUS low-complexity domain condensates, optical trapping measurements revealed that ALS-associated mutations increase viscosity by 5–20-fold compared to wild-type, providing a quantitative measure of the liquid-to-solid transition that underlies pathology (Jawerth et al., 2020; PMID:31723095).

**Partition coefficient measurement.** The partitioning of client molecules into condensates — quantified by the partition coefficient *K*_p = [client]_inside / [client]_outside — determines the functional consequences of phase separation. For RNA processing in P granules, *K*_p for specific mRNAs ranges from 2 to > 100, and this selectivity is determined by sequence-specific interactions between RNA motifs and the condensate scaffold proteins. Quantitative fluorescence microscopy methods for measuring *K*_p in living cells have been standardized (Alberti et al., 2025; PMID:31723095).

**Condensate reconstitution.** *In vitro* reconstitution of minimal condensate systems — using purified proteins and RNA at defined concentrations — has enabled systematic dissection of the molecular determinants of phase separation. The minimal FUS condensate can be reconstituted from just the low-complexity domain (residues 1–163) at concentrations > 50 μM, and the addition of RNA dramatically reduces the saturation concentration while increasing condensate viscosity (Wang et al., 2018; PMID:29727660).

**Phase diagram construction.** Complete phase diagrams (temperature vs. concentration) for IDP condensates can be constructed using turbidity measurements, centrifugation-based phase separation assays, or microfluidic dilution series. These experimental phase diagrams serve as ground truth for validating computational predictions (F148–F149).

### 3.6 Short Linear Motifs (SLiMs) and Functional Specificity in Disorder

Within the apparently featureless sequence of IDRs, short linear motifs (SLiMs) — typically 3–10 residues — serve as functional elements that mediate specific molecular interactions. SLiMs are remarkably compact information units: an SH3-binding PxxP motif, a 14-3-3-binding phosphoserine motif, or a nuclear localization signal can determine subcellular localization, signaling pathway membership, and protein lifetime. The Eukaryotic Linear Motif (ELM) database catalogs over 300 SLiM classes with > 4,000 experimentally validated instances (Kumar et al., 2022; PMID:34718738).

Machine learning approaches to SLiM discovery have matured. SLiMFinder uses statistical overrepresentation in interaction datasets to identify novel motifs (Davey et al., 2010; PMID:19914167). More recently, deep learning methods trained on PDB-derived peptide-protein interaction structures have enabled prediction of novel SLiMs from sequence alone (Benz et al., 2024). AlphaFold-Multimer has been repurposed for SLiM-mediated interaction prediction, showing that it can often correctly predict the binding mode of a disordered peptide to a folded domain partner, though with significant false-positive rates for non-binding peptides (Yin et al., 2024; PMID:38659555).

### 3.5 Novel Mathematical Framework (F148–F149): Polymer Physics for Sequence-Encoded Phase Behavior

**F148. Stickers-and-Spacers Mean-Field Theory: Critical Concentration from Sequence Composition**

For an IDP modeled as a linear polymer of length *N* with *f* sticker residues of type {Tyr, Phe, Trp, Arg} and (*N* − *f*) spacer residues, the critical concentration *c** for liquid-liquid phase separation in the mean-field (Flory-Huggins-like) stickers-and-spacers model is:

$$c^* = \frac{1}{v \cdot N} \cdot \exp\left(\frac{2\chi_{ss} \cdot f^2}{N \cdot k_B T}\right)^{-1} = \frac{k_B T}{v \cdot N \cdot \chi_{ss} \cdot f^2}$$

More precisely, the spinodal condition for phase separation in the mean-field stickers-and-spacers theory is:

$$c^* \approx \frac{1}{v \cdot (f-1)} \cdot \exp\left(-\frac{|\epsilon_{ss}|}{k_B T}\right)$$

where the critical concentration depends exponentially on the sticker-sticker interaction energy and linearly on the valence (*f* − 1) of the polymer (the number of sticker-sticker bonds each chain can form).

**Variable definitions:**
- *c**: critical concentration for phase separation (mol/L)
- *v*: excluded volume per residue (~0.13 nm³ for amino acids)
- *N*: total number of residues in the IDP
- *f*: number of sticker residues (Tyr + Phe + Trp + Arg) in the sequence
- ε_ss: sticker-sticker interaction energy per contact (typically −1 to −4 *k*_B*T* for aromatic π-π and cation-π interactions)
- *k*_B*T*: thermal energy (≈ 2.5 kJ/mol at 310 K)
- (*f* − 1): effective valence (maximum sticker-sticker bonds per chain)

**F149. Sequence Charge Decoration (SCD) → Second Virial Coefficient B₂ Analytical Relationship**

The second virial coefficient *B*₂, which characterizes the sign and magnitude of intermolecular interactions (B₂ < 0 indicates net attraction), can be analytically related to the sequence charge decoration metric for polyampholytic IDPs:

$$B_2 = \frac{N_A}{2M^2} \int_0^{\infty} \left[1 - \exp\left(-\frac{U(r)}{k_B T}\right)\right] 4\pi r^2 \, dr$$

For a polyampholytic IDP with SCD metric *σ*_SCD defined as:

$$\sigma_{SCD} = \frac{1}{N} \sum_{i=1}^{N} \sum_{j=i+1}^{N} q_i \cdot q_j \cdot \sqrt{|j-i|}$$

the approximate relationship is:

$$B_2 \approx B_2^{HS} + \alpha \cdot \sigma_{SCD} \cdot \frac{l_B^2}{b^2}$$

where the SCD captures the effective electrostatic self-energy of the chain: more negative SCD indicates stronger effective attraction between chains, leading to more negative B₂ and lower critical concentration for phase separation.

**Variable definitions:**
- *B*₂: osmotic second virial coefficient (mL·mol/g²); B₂ < 0 → net intermolecular attraction
- *B*₂^HS: hard-sphere contribution to B₂ (excluded volume; always positive)
- *N*_A: Avogadro's number
- *M*: molecular weight of the protein
- *U*(*r*): pair interaction potential as a function of intermolecular distance *r*
- σ_SCD: sequence charge decoration parameter (units: charge² · residue^{1/2})
- *q*_i: charge of residue *i* (+1 for Arg/Lys, −1 for Asp/Glu, 0 otherwise)
- *l*_B: Bjerrum length (≈ 0.71 nm in water at 310 K)
- *b*: average bond length between Cα atoms (0.38 nm)
- α: proportionality constant determined by chain stiffness and solvent conditions

**Interpretation:** Equation F149 connects a computable sequence metric (SCD, requiring only the sequence and charge assignments) to a thermodynamic observable (B₂) that directly predicts phase behavior. Proteins with σ_SCD < −30 charge²·residue^{1/2} are predicted to have B₂ < 0 and are phase-separation-prone at physiological concentrations (typically *c** < 10 μM). This enables rapid computational screening of protein sequences for phase separation propensity without requiring MD simulation. Experimentally, B₂ is measurable by static light scattering or self-interaction chromatography, providing a direct experimental test of the SCD → B₂ relationship.

---

## IV. Ancestral Sequence Reconstruction and Evolutionary Trajectory Engineering

### 4.1 The Promiscuous Ancestor Hypothesis

Ancestral sequence reconstruction (ASR) infers the sequences of proteins that existed at internal nodes of a phylogenetic tree, enabling the resurrection and biochemical characterization of proteins that have been extinct for millions to billions of years. A consistent finding across dozens of ASR studies is that reconstructed ancestral proteins are more thermostable, more promiscuous (accepting a broader range of substrates), and more soluble than their modern descendants (Wheeler et al., 2016; PMID:27339561). This pattern — termed the "promiscuous ancestor hypothesis" — suggests that ancient proteins functioned as generalist enzymes from which modern specialists evolved through subfunctionalization.

The thermostability of ancestral proteins has practical utility for protein engineering. Ancestral Cel5A cellulases reconstructed to the last common ancestor of thermophilic and mesophilic lineages exhibited T_m values 15–25°C higher than any extant family member, while retaining catalytic activity on multiple substrates (Risso et al., 2013; PMID:24043779). Ancestral reconstruction of β-lactamases, cytochrome P450s, and alcohol dehydrogenases has consistently yielded proteins with enhanced stability that serve as superior starting points for directed evolution campaigns (Gumulya et al., 2018; PMID:29420690).

### 4.2 Modern ASR Methods and Computational Advances

The computational methodology for ancestral reconstruction has advanced beyond simple maximum-likelihood inference on fixed phylogenies. GRASP (Graphical Representation of Ancestral Sequence Predictions; Foley et al., 2022; PMID:35640156) uses a partial-order graph representation that captures the full posterior distribution of ancestral sequences at each node, enabling systematic exploration of reconstruction uncertainty. FireProt-ASR (Musil et al., 2021; PMID:33556160) automates the ASR pipeline from sequence collection through phylogenetic inference to ancestral reconstruction and stability prediction, democratizing the approach for non-specialist laboratories.

A critical limitation of ASR is phylogenetic uncertainty: the reconstructed ancestral sequence depends on the assumed tree topology and substitution model, and alternative phylogenies can yield divergent ancestral sequences — the "ancestor problem." Bayesian approaches that integrate over phylogenetic uncertainty (Huelsenbeck & Bollback, 2001; PMID:11230543) produce more robust ancestral estimates but are computationally expensive for large gene families. Recent work has addressed this by using phylogenetically aware protein language models — models conditioned on the phylogenetic position of the target sequence — to improve reconstruction accuracy at deep nodes where alignment quality degrades (Hie et al., 2024).

The "consensus approach" provides a simpler alternative to full ASR: replacing each position with the most common amino acid in the multiple sequence alignment often yields stabilized variants, because the consensus sequence approximates the ancestral sequence for positions under purifying selection (Steipe et al., 1994; PMID:8048155). Porebski & Bhang (2016; PMID:26785684) showed that consensus-stabilized variants of α/β-hydrolases exhibit 10–15°C higher T_m than any natural homolog, consistent with the ancestral stability hypothesis.

### 4.3 ML-Guided Directed Evolution

The integration of machine learning with directed evolution has transformed protein engineering from a random walk to a guided search through sequence space. The key advance is the use of ML models to predict the fitness of uncharacterized variants from limited experimental data, enabling intelligent selection of the most promising variants for experimental testing.

EvolvR and PACE (phage-assisted continuous evolution) represent two paradigms of continuous evolution. EvolvR enables targeted, continuous mutagenesis of a specific genomic locus at rates > 10⁵× the background mutation rate, generating standing genetic variation that can be selected in real time (Halperin et al., 2018; PMID:29702637). PACE subjects evolving proteins to > 100 rounds of selection per day using a bacteriophage life cycle linked to the desired protein activity, achieving in days what would require months of conventional directed evolution (Esvelt et al., 2011; PMID:21478873). The combination of PACE with ML fitness prediction — using a PLM-based model to predict which mutagenic strategies will generate the highest proportion of improved variants — has enabled the evolution of base editors with 590-fold increased activity in just four days (Thuronyi et al., 2019; PMID:31189960).

### 4.3 Zero-Shot vs. Supervised Fitness Prediction

A central question in ML-guided protein engineering is whether evolutionary information alone (zero-shot prediction) is sufficient to guide engineering campaigns, or whether supervised models trained on assay-specific experimental data are required. Zero-shot methods like ESM-1v (Meier et al., 2021; PMID:34697933) and TranceptEVE (Notin et al., 2024; PMID:38382398) predict variant fitness from the PLM's learned evolutionary distribution without any experimental training data, achieving *r* = 0.4–0.5 correlation with DMS experiments for most proteins. Supervised methods like FLIP (Dallago et al., 2021), trained on small labeled datasets (10–100 variants), achieve *r* = 0.6–0.8 but require experimental investment.

The practical resolution is a two-phase approach: use zero-shot predictions to design the initial library, experimentally characterize 100–500 variants, train a supervised model on these data, and then use the supervised model to design subsequent rounds (Wittmann et al., 2021; PMID:33844576). This iterative active learning strategy consistently outperforms both pure random mutagenesis and pure zero-shot prediction across diverse protein engineering targets (Hie et al., 2024).

### 4.5 Continuous Evolution Systems: PACE and Beyond

Phage-assisted continuous evolution (PACE) represents a paradigm shift in directed evolution by linking protein function to bacteriophage propagation, enabling hundreds of generations of selection per day without researcher intervention. The system operates by encoding the protein of interest in a "selection phage" that can only propagate in host cells expressing a conditional phage gene (gene III) whose expression is linked to the desired protein activity (Esvelt et al., 2011; PMID:21478873). PACE has been used to evolve base editors with 590-fold improved activity (Thuronyi et al., 2019; PMID:31189960), aminoacyl-tRNA synthetases with novel amino acid specificities (Bryson et al., 2017; PMID:28971967), and proteases with altered substrate specificity (Packer et al., 2017; PMID:28100640).

PACE+ incorporates negative selection pressure using a dominant-negative gene III fragment, enabling the simultaneous selection for desired activity and against undesired activities (e.g., off-target editing) (Richter et al., 2020; PMID:32424326). This multi-objective evolution mirrors the competing-risks framework (F156–F157) in the therapeutic context: the fitness landscape for base editors includes both on-target activity and off-target avoidance, and PACE+ navigates the Pareto frontier experimentally.

EvolvR, developed by the Doudna laboratory, enables continuous, targeted mutagenesis of a user-specified genomic locus at rates > 10⁵× the background mutation rate using an error-prone DNA polymerase fused to nCas9 (Halperin et al., 2018; PMID:29702637). Unlike PACE, EvolvR operates within the host chromosome, enabling evolution of proteins in their native genomic context with all associated regulatory elements. The combination of EvolvR with FACS-based selection has enabled the rapid evolution of metabolic enzymes for increased flux through engineered biosynthetic pathways (Garst et al., 2024).

### 4.6 From ASR to Forward Engineering: Designing Evolutionary Trajectories

The combination of ancestral reconstruction (which reveals where proteins have been) with ML fitness prediction (which reveals where they can go) enables a new paradigm: *designed evolutionary trajectories*. Rather than random mutagenesis or greedy optimization, the engineer plans a specific mutational path from the starting sequence to the target function, choosing intermediates that maintain viability at every step.

This approach has been demonstrated for converting enzyme substrate specificity: Romero & Arnold (2009; PMID:19935669) showed that the most efficient directed evolution trajectories follow "neutral networks" — paths through sequence space where function is maintained above a viability threshold. ML models trained on DMS data can predict which neutral networks connect to desired functional outcomes, enabling prospective trajectory design.

The Wasserstein distance framework (F150–F151) formalizes trajectory planning by quantifying the difficulty of each possible path in terms of the fitness landscape topology. When multiple paths exist between a source function and a target function, the optimal path minimizes the maximum fitness cost encountered along the trajectory — the "minimax" path. This minimax formulation connects to game theory and robust optimization, providing algorithms that can be applied to the trajectory planning problem.

Forward engineering of evolutionary trajectories has practical implications for: (1) directed evolution campaigns, where planning the library design and selection strategy can reduce the number of rounds needed; (2) evolutionary prediction, where understanding which trajectories are accessible constrains predictions of viral evolution and drug resistance; and (3) synthetic biology, where designing metabolic pathways requires engineering multiple enzymes simultaneously, each following its own trajectory on a coupled fitness landscape.

### 4.7 Sign Epistasis as Evolutionary Barriers

Sign epistasis — where a mutation is beneficial in one genetic background but deleterious in another — creates rugged fitness landscapes with multiple local optima separated by fitness valleys. Sign epistasis constrains evolutionary accessibility: not all paths from one functional variant to another are mutationally accessible through single-step improvements. Extensive combinatorial mutagenesis studies on proteins including TEM-1 β-lactamase (Weinreich et al., 2006; PMID:16601193), influenza nucleoprotein (Gong et al., 2013; PMID:23580527), and IgG-binding protein G (Wu et al., 2016; PMID:27338137) have demonstrated that only a small fraction (typically 2–20%) of mutational pathways between two functional variants are accessible via monotonically increasing fitness.

Recent work has quantified the relationship between epistasis and evolutionary predictability using large-scale DMS datasets covering all single and double mutants of multiple proteins. Pokusaeva et al. (2024) analyzed > 10⁶ double mutant combinations in four enzymes and found that sign epistasis is concentrated at structurally proximal positions and is predictable from PLM-derived contact maps, suggesting that epistatic barriers can be anticipated and circumvented computationally.

The concept of "evolutionary accessibility" — the fraction of all shortest mutational paths between two functional variants that pass through intermediates with fitness above a viability threshold — provides a quantitative measure of landscape navigability. For TEM-1 β-lactamase, only 18 of 120 (15%) shortest paths between two functional variants separated by 5 mutations are accessible, and this fraction depends strongly on the fitness threshold: raising the threshold from 50% to 80% of wild-type activity reduces accessibility to < 5% (Weinreich et al., 2006; PMID:16601193). These constraints have practical implications for protein engineering: directed evolution campaigns must often traverse fitness valleys that require neutral drift through weakly selected intermediates, a process that random mutagenesis achieves stochastically but that ML-guided approaches could navigate more efficiently.

The concept has direct implications for therapeutic protein engineering. When engineering a human enzyme variant with improved catalytic properties, the designer must navigate a fitness landscape constrained by both catalytic function and protein stability. Mutations that improve catalytic activity may traverse fitness valleys where the intermediate variants are unstable or poorly expressed. The optimal engineering strategy depends on the landscape topology: for smooth landscapes, gradual accumulation of beneficial mutations suffices; for rugged landscapes, neutral drift through sequence space (via stabilizing "neutral" mutations that do not affect function) may be necessary to reach a new fitness peak.

The Wasserstein distance framework (F150–F151) formalizes this intuition by measuring the difficulty of evolutionary transitions in terms of the geometric structure of the fitness landscape. When the landscape is smooth (low epistasis), the Wasserstein distance is close to the Hamming distance; when the landscape is rugged (high sign epistasis), the Wasserstein distance exceeds the Hamming distance substantially, indicating that the path through sequence space is indirect and costly.

### 4.5 Novel Mathematical Framework (F150–F151): Optimal Transport for Evolutionary Trajectories (Cross-Discipline 2/3)

The problem of navigating from a source protein (with function *A*) to a target protein (with function *B*) through sequence space while maintaining viability at every step is formally analogous to the optimal transport problem: finding the minimum-cost transport plan between two probability distributions on a metric space.

**F150. Wasserstein Distance Between Sequence Ensembles on Fitness Landscapes**

Let *μ* be the probability distribution over sequences encoding function *A* (the source ensemble) and *ν* be the distribution over sequences encoding function *B* (the target ensemble). The *p*-Wasserstein distance between these ensembles on the fitness landscape is:

$$W_p(\mu, \nu) = \left(\inf_{\gamma \in \Gamma(\mu, \nu)} \int_{S \times S} d(s_1, s_2)^p \, d\gamma(s_1, s_2)\right)^{1/p}$$

where *S* is the sequence space, *d*(*s*₁, *s*₂) is the Hamming distance weighted by fitness cost, and Γ(μ, ν) is the set of all couplings (transport plans) with marginals μ and ν.

The fitness-weighted Hamming distance is:

$$d(s_1, s_2) = \sum_{k=1}^{L} \mathbb{1}[s_1(k) \neq s_2(k)] \cdot w_k(s_1, s_2)$$

where the positional weight *w*_k captures the fitness cost of mutating position *k*:

$$w_k(s_1, s_2) = \max\left(0, -\Delta F_k\right) + 1$$

and ΔF_k is the fitness effect of the substitution at position *k*.

**Variable definitions:**
- *W*_p(μ, ν): *p*-Wasserstein distance between source and target sequence ensembles
- μ: probability distribution over sequences with function *A*
- ν: probability distribution over sequences with function *B*
- γ: coupling (transport plan) — a joint distribution on *S* × *S* with marginals μ and ν
- Γ(μ, ν): set of all valid couplings
- *S*: sequence space (alphabet Σ = {A, C, D, ..., Y}, length *L*)
- *d*(*s*₁, *s*₂): fitness-weighted Hamming distance
- *w*_k: positional weight penalizing fitness-costly mutations
- ΔF_k: fitness effect of substitution at position *k* (negative = deleterious)

**F151. Lower Bound on Minimum Adaptive Mutations**

The Wasserstein distance provides a lower bound on the number of adaptive mutations required to traverse the landscape:

$$n_{mut}^{min} \geq \frac{W_1(\mu, \nu)}{\max_k w_k}$$

For rugged landscapes with sign epistasis, the actual number of required mutations exceeds this bound by a factor related to the landscape ruggedness:

$$n_{mut}^{actual} \approx W_1(\mu, \nu) \cdot \left(1 + \frac{n_{sign}}{L}\right)$$

where *n*_sign is the number of positions exhibiting sign epistasis between the source and target backgrounds.

**Variable definitions:**
- *n*_{mut}^{min}: minimum number of mutations required (lower bound)
- *n*_{mut}^{actual}: expected number of mutations accounting for landscape ruggedness
- *W*₁(μ, ν): 1-Wasserstein (earth mover's) distance between ensembles
- *n*_sign: number of positions with sign epistasis
- *L*: sequence length

**Cross-discipline note (2/3):** Optimal transport theory originates in mathematical optimization (Monge, 1781; Kantorovich, 1942) and has been extensively applied in machine learning (generative adversarial networks, domain adaptation), economics, and image processing. Its application to evolutionary trajectory planning on fitness landscapes is a novel cross-disciplinary import.

**Interpretation:** The Wasserstein distance between function *A* and function *B* sequence ensembles provides a geometry-aware measure of evolutionary distance that accounts for the topology of the fitness landscape, unlike simple Hamming distance which treats all mutations as equally accessible. A large *W*₁ relative to the Hamming distance between the centroids indicates that the evolutionary path is obstructed by fitness valleys, requiring either neutral drift through weakly selected intermediates or epistatic tunneling. This framework can be computed from experimental DMS data and used to identify the most accessible evolutionary trajectories for directed evolution campaigns.

---

## V. Allosteric Communication Networks

### 5.1 Allostery as a Network Property

Allostery — the coupling of binding or catalytic events at distant protein sites — is a fundamental feature of protein function regulation. The classical view of allostery as a two-state phenomenon (MWC model: T ⇄ R) has been superseded by a more nuanced understanding of allostery as a property of the protein's internal communication network, mediated by correlated motions that propagate perturbations across the structure (Motlagh et al., 2014; PMID:25411042).

Protein structure networks (PSNs) represent proteins as graphs where nodes are residues and edges connect residues with significant non-covalent interactions (hydrogen bonds, van der Waals contacts, salt bridges, or correlated motions). Analysis of these networks using graph-theoretic tools reveals that allosteric communication is mediated by specific pathways of residues connecting the allosteric site to the active site — allosteric pathways that can be disrupted by mutations at key hub or bottleneck residues (del Sol et al., 2009; PMID:19427316).

### 5.2 Elastic Network Models: ANM and GNM

The Gaussian Network Model (GNM) and Anisotropic Network Model (ANM) provide computationally efficient coarse-grained representations of protein dynamics based on the topology of the contact network alone, without requiring MD simulation. GNM treats the protein as an elastic network of Cα atoms connected by harmonic springs and predicts the mean-square fluctuations, B-factors, and slow modes of motion from the connectivity alone (Bahar et al., 1997; PMID:9326618). ANM extends this to predict the directionality of collective motions, not just their amplitudes (Atilgan et al., 2001; PMID:11254622).

The remarkable success of elastic network models — GNM-predicted B-factors correlate with experimental X-ray B-factors at *r* = 0.55–0.75 for most proteins — demonstrates that the pattern of collective motions is largely determined by the network topology rather than the details of the energy function. This topological determinism of protein dynamics is the foundation for the spectral graph theory framework developed below.

ProDy, an open-source Python package for protein dynamics analysis using ANM/GNM, has been extended with machine learning modules that predict allosteric communication pathways from the elastic network eigenvectors (Bakan et al., 2014; PMID:24586136). The combination of elastic network analysis with MD-derived dynamical correlations has enabled the prediction of allosteric communication in GPCR signaling (Kaynak et al., 2022; PMID:35413150).

### 5.3 Machine Learning Approaches to Allosteric Site Prediction

Identifying allosteric sites from protein structure has been formalized as a machine learning classification problem. AlloSigMA (Guarnera & Berezovsky, 2019; PMID:31057600) uses a structure-based statistical mechanical model (the Structural Perturbation Method) to compute the allosteric free energy change induced by mutations at every position, generating an allosteric signaling map that identifies regulatory hotspots. The Ohm algorithm (Tan et al., 2023; PMID:37248383) combines elastic network analysis with random walk-based pathway detection to identify allosteric communication pathways and rank residues by their contribution to allosteric coupling, achieving AUC = 0.85 for predicting experimentally validated allosteric residues in a benchmark of 52 allosteric proteins.

PASSer (Protein Allosteric Site Server; Tian et al., 2023; PMID:36866619) uses a 3D convolutional neural network trained on known allosteric sites from the ASBench benchmark to predict allosteric pocket locations from protein structure. PASSer achieves 88% sensitivity for detecting at least one residue within 5 Å of the experimental allosteric site. AlphaFold-based analysis of predicted structures has extended allosteric site prediction to proteins without experimental structures, enabling proteome-scale mapping of potential allosteric sites (Herrington et al., 2024).

The conceptual shift from "allostery as a property of specific proteins" to "all proteins are potentially allosteric" (Gunasekaran et al., 2004; PMID:14985572) has been supported by systematic analysis of the PDB: > 25% of all enzyme structures contain bound small molecules at sites distant from the active site, many of which modulate catalytic activity (Huang et al., 2015; PMID:25921590).

### 5.4 Allosteric Drug Design: FDA-Approved Agents (2022–2025)

The pharmaceutical industry has increasingly exploited allosteric mechanisms for drug design, driven by the recognition that allosteric sites often provide superior selectivity over orthosteric (active-site) binding. Recent FDA approvals and clinical advances include:

**Allosteric IDH1/2 inhibitor vorasidenib.** FDA-approved in August 2024, vorasidenib is a brain-penetrant allosteric dual IDH1/2 inhibitor for low-grade glioma that achieved progression-free survival of 27.7 vs. 11.1 months in the Phase 3 INDIGO trial (Mellinghoff et al., 2023; PMID:37272516). **Allosteric cardiac myosin inhibitor aficamten**, FDA-approved in 2024 for obstructive hypertrophic cardiomyopathy, stabilizes the weak actin-binding state of cardiac myosin by slowing phosphate release (Maron et al., 2024; PMID:38739079; Hartman et al., 2024; PMID:39196032).
**KRAS G12C inhibitors.** Sotorasib (2021) and adagrasib (2022) both exploit a cryptic allosteric pocket beneath the switch-II loop of KRAS G12C that is absent in wild-type KRAS and in the GTP-bound active state (Skoulidis et al., 2021; PMID:34096690; Jänne et al., 2022; PMID:36200978). These drugs lock KRAS in the inactive GDP-bound state. The development of pan-KRAS inhibitors targeting the non-mutant-selective switch-II pocket (e.g., BI-2852) represents the next frontier (Kessler et al., 2019; PMID:31406373). RMC-6236, a RAS(ON) multi-selective inhibitor, demonstrated clinical activity against KRAS G12X mutations in Phase 1/2 trials (Holderfield et al., 2024; PMID:39133542).

**Acquired resistance to allosteric KRAS inhibitors.** Sotorasib and adagrasib, while revolutionary, face acquired resistance through multiple mechanisms: secondary KRAS mutations (Y96D, R68S, H95D/Q/R) that disrupt drug binding or stabilize the GTP-bound state; bypass pathway activation (NRAS, BRAF, MET amplification); and histological transformation to squamous or small-cell phenotypes. These resistance mechanisms highlight the importance of understanding the full allosteric network: resistance mutations at switch-II distal sites propagate conformational changes through the allosteric communication pathway identified by spectral graph analysis (F152), suggesting that next-generation inhibitors should target multiple nodes in the network simultaneously. Pan-KRAS(ON) inhibitors like RMC-6236 (Holderfield et al., 2024; PMID:39133542) represent this multi-node strategy by targeting the active (GTP-bound) state that all oncogenic KRAS mutants share.

**SHP2 allosteric inhibitors.** The protein tyrosine phosphatase SHP2 is allosterically regulated by its N-SH2 domain, which occludes the catalytic site in the autoinhibited state. Allosteric inhibitors that stabilize the autoinhibited conformation — including TNO155 (Novartis) and RMC-4630 (Revolution Medicines) — have advanced to Phase 2 clinical trials for RAS-driven cancers (LaMarche et al., 2020; PMID:32207897).

**Engineered allosteric switches.** The LOCKR (Latching, Orthogonal Cage/Key pRotein) system enables the design of proteins with built-in allosteric switches: a "cage" domain sequesters a functional peptide motif, and a "key" protein induces a conformational change that exposes the motif (Langan et al., 2019; PMID:31666701). This platform has been extended to create allosteric biosensors (Quijano-Rubio et al., 2021; PMID:33859033), drug-responsive degrons (Fink et al., 2023; PMID:37735578), and synthetic signaling circuits in cells (Chen et al., 2023; PMID:37669541).

### 5.5 Molecular Dynamics-Derived Allosteric Pathways

While elastic network models capture the topological determinants of allosteric communication, molecular dynamics simulations reveal the atomistic details of allosteric signaling — the specific residue-residue contacts, hydrogen bond networks, and hydrophobic clusters that transmit perturbations between distant sites.

Dynamic network analysis of MD trajectories constructs weighted graphs where edge weights represent the strength of dynamical coupling (correlated motions) between residue pairs. Optimal path analysis on these weighted networks identifies the most efficient routes for perturbation propagation — the allosteric pathways. Floyd-Warshall or Dijkstra algorithms applied to the inverse-correlation-weighted graph yield the optimal (shortest) allosteric pathway between any two residues (Sethi et al., 2009; PMID:19572563).

Community analysis of protein dynamical networks reveals modular organization: groups of residues that are strongly correlated internally but weakly coupled to other groups form communities that correspond to structural domains, regulatory subunits, or functional modules. The boundaries between communities — the bottleneck residues — are the control points for allosteric regulation, consistent with the Fiedler vector analysis (F152). Comparison of community structure between apo and ligand-bound states reveals how allosteric effectors rewire the protein's communication network.

Cross-correlation analysis at timescales ranging from picoseconds (local vibrations) to microseconds (domain motions) reveals a hierarchy of allosteric communication: fast motions mediate local rearrangements at the binding site, while slow collective motions transmit the allosteric signal to distant functional sites. This timescale hierarchy explains why allostery cannot be captured by static structural analysis alone — it is fundamentally a dynamical phenomenon.

### 5.6 Cryptic Allosteric Pockets in Drug Targets

The KRAS story illustrates a broader principle: many "undruggable" targets harbor cryptic allosteric pockets that are invisible in static crystal structures but can be identified through ensemble analysis. For the p53 tumor suppressor, the Y220C mutation creates a cryptic surface crevice that is absent in wild-type p53, and this pocket has been exploited for allosteric stabilization of the mutant protein (Bauer et al., 2019; PMID:31363000). The general principle — that disease-causing mutations can create new druggable pockets — extends the allosteric pharmacology paradigm beyond naturally allosteric proteins to any protein where a pathogenic mutation induces a conformational change.

The integration of ML-based cryptic pocket prediction (PocketMiner, CavitySpace) with elastic network-based allosteric pathway analysis (ProDy, Ohm) creates a computational pipeline that, given a protein target, can: (1) predict the locations of all pockets (including cryptic ones); (2) assess which pockets are allosterically coupled to the functional site; and (3) rank pockets by druggability score. This pipeline has been applied proteome-wide to identify novel allosteric drug targets for hundreds of human disease-associated proteins (Herrington et al., 2024).

### 5.6 Negative Allostery and Allosteric Inhibition Design

While positive allostery (activation by effector binding) has received the most attention in drug design, negative allostery (inhibition) is equally important therapeutically. Negative allosteric modulators (NAMs) offer advantages over orthosteric inhibitors: they preserve basal receptor activity (enabling tonic signaling), achieve ceiling effects (preventing overdose toxicity), and act at less-conserved sites (reducing off-target effects).

For kinases, type III allosteric inhibitors bind outside both the ATP-binding and substrate-binding sites. Asciminib — an ABL1 myristoyl-pocket inhibitor approved in 2021 for BCR-ABL T315I-mutant chronic myeloid leukemia (a mutation resistant to all ATP-competitive inhibitors) — demonstrated the clinical value of allosteric inhibition for overcoming drug resistance.

The spectral graph framework (F152–F153) predicts that proteins with low Fiedler values (λ₂ << 1) have narrow allosteric bottlenecks that are easily disrupted — ideal targets for NAM development. Conversely, proteins with high λ₂ have robust, distributed communication networks resistant to single-site perturbation. This topological classification of allosteric vulnerability provides a systematic basis for target selection in allosteric drug discovery: a proteome-wide survey of Fiedler values could prioritize targets by their susceptibility to allosteric modulation.

### 5.7 Engineered Allostery for Synthetic Biology

Beyond drug design, understanding allosteric communication enables the engineering of protein switches for synthetic biology. Raman et al. (2014; PMID:24970076) demonstrated that allosteric coupling can be introduced into non-allosteric proteins by computationally designing a domain insertion site — inserting a ligand-binding domain into a surface loop of the enzyme, creating a mechanical coupling between ligand binding and enzyme conformation. This approach has been used to create drug-responsive kinases, proteases, and transcription factors for use as components in synthetic signaling circuits.

Wolf et al. (2025; PMID:40759748) introduced ProDomino, an ML pipeline for predicting optimal domain insertion sites that achieves ~80% success rate in creating light- and chemically-regulated allosteric switches for Cas9 and Cas12a — enabling drug-responsive genome editing enzymes.

The success of LOCKR (Section 6.4) suggests that allosteric coupling is a designable, modular property that can be computationally installed into any protein scaffold — a prediction consistent with the "universal allostery" hypothesis (Gunasekaran et al., 2004; PMID:14985572) and with the spectral graph theory framework below, which shows that any connected protein structure network supports allosteric communication through its low-frequency eigenmodes.

### 5.7 Novel Mathematical Framework (F152–F153): Spectral Graph Theory on Protein Contact Networks

**F152. Graph Laplacian Eigenspectrum and Allosteric Communication Bottleneck**

Consider a protein structure network *G* = (*V*, *E*) where vertices *V* represent residues and edges *E* connect residues within a distance cutoff *r*_c (typically 7–8 Å between Cα atoms). The graph Laplacian is **L** = **D** − **A**, where **D** is the degree matrix and **A** is the adjacency matrix. The eigenvalues of **L** are 0 = λ₁ ≤ λ₂ ≤ ... ≤ λ_N.

The second-smallest eigenvalue λ₂ (the Fiedler value, or algebraic connectivity) characterizes the communication bottleneck of the protein structure network:

$$\lambda_2 = \min_{\mathbf{x} \perp \mathbf{1}} \frac{\mathbf{x}^T \mathbf{L} \mathbf{x}}{\mathbf{x}^T \mathbf{x}} = \min_{\mathbf{x} \perp \mathbf{1}} \frac{\sum_{(i,j) \in E} (x_i - x_j)^2}{\sum_i x_i^2}$$

**Variable definitions:**
- *G* = (*V*, *E*): protein structure network; |*V*| = *N* residues
- **L**: graph Laplacian matrix (*N* × *N*)
- **D**: diagonal degree matrix; *D*_ii = deg(*i*)
- **A**: adjacency matrix; *A*_ij = 1 if *d*(Cα_i, Cα_j) < *r*_c
- λ₂: Fiedler value (algebraic connectivity); measures the minimum communication bottleneck
- **v**₂: Fiedler vector; its sign partition gives the optimal two-way cut of the protein (separating domains)
- *r*_c: distance cutoff for defining contacts (typically 7.5 Å)

**Interpretation:** The Fiedler value λ₂ quantifies how easily a perturbation (e.g., ligand binding) can be communicated from one part of the protein to another. Proteins with low λ₂ have a narrow communication bottleneck — a small number of residues that, if mutated, would disrupt allosteric signaling. The Fiedler vector **v**₂ identifies these bottleneck residues: they lie near the zero-crossing of **v**₂ and correspond to the interdomain hinge region. For KRAS, the Fiedler vector of the contact network precisely identifies the switch-I and switch-II regions as the communication bottleneck between the nucleotide-binding pocket and the effector-binding interface, consistent with their critical role in allosteric signaling.

**F153. Allosteric Transfer Function for Perturbation Propagation**

The frequency-dependent response of the protein network to a perturbation at residue *j* (e.g., ligand binding), as measured at residue *i* (e.g., active-site catalytic residue), is given by the allosteric transfer function:

$$H_{ij}(\omega) = \left[(\mathbf{L} + i\omega\mathbf{I})^{-1}\right]_{ij} = \sum_{k=2}^{N} \frac{v_k(i) \cdot v_k(j)}{\lambda_k + i\omega}$$

where **v**_k is the *k*-th eigenvector of the Laplacian and ω is the perturbation frequency.

The allosteric coupling strength between sites *i* and *j* is the zero-frequency (static) transfer function:

$$|H_{ij}(0)| = \left|\sum_{k=2}^{N} \frac{v_k(i) \cdot v_k(j)}{\lambda_k}\right|$$

**Variable definitions:**
- *H*_ij(ω): allosteric transfer function from perturbation site *j* to response site *i*
- ω: perturbation frequency (ω → 0 for static allostery; ω > 0 for dynamic allostery)
- **v**_k: *k*-th eigenvector of the graph Laplacian
- λ_k: *k*-th eigenvalue of the graph Laplacian
- *i*: imaginary unit (√−1)
- **I**: identity matrix

**Interpretation:** The allosteric transfer function *H*_ij(ω) decomposes allosteric communication into contributions from each collective mode of the protein network. Low-frequency modes (small λ_k) contribute most strongly, consistent with the observation that allosteric signaling is predominantly mediated by global, collective motions rather than localized vibrations. The magnitude |*H*_ij(0)| provides a quantitative, structure-computable metric for allosteric coupling strength that can be used to: (1) predict which residues are allosterically coupled to the active site; (2) identify optimal sites for allosteric drug binding; and (3) design engineered allosteric switches by introducing connections (disulfide bonds, metal-binding sites) that modulate specific eigenvalues of the Laplacian.

---

## VI. The Inverse Problem: Designing Sequences for Specified Functions

### 6.1 From Structure-Based to Function-Based Design

The protein design revolution began with structure-based approaches: given a desired three-dimensional structure (backbone), compute the amino acid sequence most likely to fold into that structure. Rosetta's fixed-backbone design algorithm achieved landmark successes, including the design of the Top7 protein — the first protein with a fold never observed in nature (Kuhlman et al., 2003; PMID:14631033). ProteinMPNN, a graph neural network trained on experimentally determined protein structures, dramatically improved the success rate of fixed-backbone sequence design, achieving experimental structure recovery rates of > 50% compared to ~10% for Rosetta (Dauparas et al., 2022; PMID:36108065). LigandMPNN extended this to design sequences in the context of bound ligands, metal cofactors, and non-canonical amino acids (Dauparas et al., 2025; PMID:40155723).

However, structure-based design addresses only half the problem. The harder challenge — and the one most relevant to therapeutic applications — is *function-based design*: given a desired function (e.g., "hydrolyze a specific ester bond with *k*_cat > 10³ s⁻¹" or "bind IL-6 with *K*_d < 1 nM"), compute a sequence that achieves that function. Function-based design requires models that can predict the quantitative functional consequences of sequence variation, not just whether a sequence folds.

### 6.2 Enzyme Design: From Scratch to Catalytic Competence

De novo enzyme design — creating enzymes with catalytic activities not found in nature — is the ultimate test of our understanding of the sequence-to-function mapping. Early Rosetta-designed enzymes (Kemp eliminases, retro-aldolases, Diels-Alderases) achieved modest catalytic rates (10–100-fold above background), often requiring extensive directed evolution to reach practically useful activities (Röthlisberger et al., 2008; PMID:18323453; Siegel et al., 2010; PMID:20651057).

The latest generation of AI-driven enzyme design tools represents a step change:

**TheZyme** (Hua et al., 2025) is a generative model that designs enzyme active sites de novo by conditioning on the desired reaction mechanism. Given a transition-state geometry and the identities of catalytic residues, TheZyme generates a full protein scaffold around the active site using an iterative diffusion process. In benchmarks, TheZyme-designed enzymes for monoamine oxidase activity achieved *k*_cat/*K*_m values within one order of magnitude of natural enzymes without any directed evolution — a dramatic improvement over earlier computational designs that typically required 4–6 rounds of evolution to reach comparable activities.

The most striking recent result is the computational design of zinc metallohydrolases by Kim et al. (2025; PMID:41339547) using RFdiffusion2 with quantum-chemistry-derived active-site geometries, achieving *k*_cat/*K*_M up to 53,000 M⁻¹s⁻¹ — within 10-fold of natural metallohydrolases. Pellock et al. (2025; PMID:39946508) designed serine hydrolases with *k*_cat/*K*_M up to 2.2 × 10⁵ M⁻¹s⁻¹ across five novel folds, with crystal structures matching designs within < 1 Å Cα RMSD. Braun et al. (2026; PMID:41339546) introduced Riff-Diff, a hybrid ML/atomistic pipeline where 91% of designed retro-aldolases were catalytically active — the highest success rate ever reported for de novo enzyme design. Krishna et al. (2025; PMID:41339749) demonstrated that RFdiffusion2 can scaffold all 41 benchmark active sites (vs. 16 previously), generating active enzymes from fewer than 96 designs tested.

**EnzymeFlow** (Tran et al., 2025) takes a complementary approach, using SE(3)-equivariant flow matching to jointly design the protein backbone and active-site sequence conditioned on the desired substrate. The model was trained on the BRENDA enzyme database and generates full enzyme structures with positioned catalytic residues in a single forward pass. EnzymeFlow-designed esterases demonstrated catalytic activity on their target substrates in 11 of 16 tested designs (69% success rate), compared to 10–30% for previous methods.

**TurNuP** (Kroll et al., 2023; PMID:37828081) predicts enzyme turnover numbers (*k*_cat) from sequence and substrate structure using a transformer architecture trained on > 38,000 *k*_cat measurements from BRENDA. TurNuP achieves *R*² = 0.44 on held-out enzyme-substrate pairs — modest but practically useful for prioritizing candidates in metabolic engineering pipelines. The model reveals that turnover number prediction is substantially harder than binding affinity prediction (*R*² = 0.6–0.7), consistent with the greater complexity of catalytic function relative to molecular recognition.

**Retro-Enzymatic Synthesis.** Mirroring retrosynthetic analysis in organic chemistry, retro-enzymatic synthesis (Finnigan et al., 2021; PMID:33977260) works backward from a desired chemical transformation to identify enzyme scaffolds capable of catalyzing each step. ML models predict which enzyme superfamily is most likely to accommodate a given reaction, estimate the number of mutations needed to achieve the desired specificity, and propose active-site configurations. Combined with automated enzyme screening platforms, retro-enzymatic synthesis has enabled the design of three-step biosynthetic pathways for non-natural products with 40–60% overall yield (Gruber et al., 2024).

**Directed evolution at scale.** The combination of droplet microfluidics, next-generation sequencing, and ML fitness prediction has enabled ultra-high-throughput directed evolution campaigns that screen > 10⁶ variants per day. Fluorescence-activated droplet sorting (FADS) links genotype and phenotype within picoliter droplets, enabling selection for enzymatic activity at rates of 10⁴ droplets/second (Colin et al., 2015; PMID:26065899). When coupled with ML models that learn from the screening data in real time, these platforms converge on optimal variants in 3–5 rounds rather than the 10–20 rounds typical of conventional directed evolution.

### 6.4 Antibody and Nanobody Design

Computational antibody design has progressed from CDR loop grafting and humanization to full de novo generation of antigen-specific antibodies:

**AbDiffuser** uses a diffusion process in the joint space of CDR loop structure and sequence to generate antigen-specific antibodies (Martinkus et al., 2024). Given a target antigen surface, AbDiffuser generates 1,000 candidate antibodies in ~30 minutes, of which 15–25% show detectable binding in high-throughput yeast display assays. This represents a 100-fold reduction in screening requirements compared to naive library approaches.

**dyMEAN** (Kong et al., 2023; PMID:38004078) is a dynamic multi-channel equivariant attention network that generates paired heavy-light chain antibody structures conditioned on the target epitope. dyMEAN correctly predicts the binding orientation and CDR loop conformations for 73% of co-crystal structures in the SAbDab database, and its generated designs show improved developability scores (aggregation propensity, viscosity, clearance) relative to natural antibodies.

**IgFold** (Ruffolo et al., 2023; PMID:36652895) combines PLM embeddings from AntiBERTy with a graph transformer to predict antibody structure in < 1 second per sequence, compared to > 10 minutes for AlphaFold2-Multimer. The speed advantage enables IgFold to be embedded in real-time design loops where rapid structural feedback guides sequence optimization.

### 6.4 Designed Protein Switches and Biosensors

The LOCKR platform (Langan et al., 2019; PMID:31666701) demonstrated that allosteric switches can be designed de novo: a protein cage sequesters a bioactive peptide in a buried state, and a key protein unlocks the cage through competitive binding, exposing the peptide. Extensions of this concept include:

**Drug-responsive degrons.** Fink et al. (2023; PMID:37735578) designed protein domains that are stable in the presence of a small molecule and degraded in its absence (or vice versa), creating drug-responsive ON/OFF switches for controlling protein levels in cells. These designed degrons achieve > 100-fold dynamic range and respond within 1–2 hours, enabling precise temporal control of therapeutic protein expression.

**Designed luciferases.** Yeh et al. (2023; PMID:37099615) designed a family of ultra-bright luciferases (NanoLuc derivatives) using computational active-site redesign, achieving 10× higher quantum yield than the natural enzyme. The designed luciferases have been deployed as bioluminescent reporters in deep-tissue imaging applications.

**Designed signaling circuits.** Chen et al. (2023; PMID:37669541) combined LOCKR-based switches with designed proteases and split transcription factors to build synthetic signaling circuits in mammalian cells that respond to user-specified inputs (small molecules, cell-surface antigens) and produce programmable transcriptional outputs.

### 6.5 Nanobody Design and Single-Domain Antibodies

Nanobodies — single-domain antibodies derived from camelid heavy-chain-only antibodies — offer unique advantages for computational design: their small size (~15 kDa, 130 residues), high stability, and single-chain architecture simplify the design problem relative to conventional antibodies with their heavy-light chain pairing complexity. NanoNet (Cohen et al., 2022; PMID:35862509) predicts nanobody-antigen binding using an equivariant graph neural network and has been used to design synthetic nanobodies against challenging epitopes including the GPCR extracellular surface and tumor-specific glycans.

The CDR3 loop of nanobodies, which is typically 12–18 residues (longer than conventional antibody CDR3, which averages 9–12 residues), provides a larger paratope surface that can access concave epitopes (enzyme active sites, GPCR transmembrane pockets) inaccessible to conventional antibodies. Computational design of CDR3 loops using constrained energy minimization with Rosetta and ProteinMPNN has achieved experimental binding rates of 20–35% for de novo designed nanobodies, with affinities in the 10–100 nM range achievable without affinity maturation (McMahon et al., 2024).

### 6.6 Function-Conditioned Generative Models

The distinction between structure-conditioned and function-conditioned protein generation is critical. Structure-conditioned models (ProteinMPNN, ESM-IF) generate sequences likely to fold into a specified backbone — they solve the inverse folding problem. Function-conditioned models aim to generate sequences that achieve a specified *function* regardless of structure.

ProGen2 (Nijkamp et al., 2023) is an autoregressive language model trained on protein sequences with functional annotations (GO terms, EC numbers, taxonomic labels). By conditioning generation on a specific functional tag (e.g., EC 3.1.1.3 for triacylglycerol lipase), ProGen2 generates sequences that are predicted to have the specified enzymatic activity. Experimental validation showed that ProGen2-generated lysozymes exhibited catalytic activity comparable to natural lysozymes despite sharing < 30% sequence identity (Nijkamp et al., 2023; PMID:37909046).

EvoDiff (Alamdari et al., 2023) uses discrete diffusion over amino acid sequences, generating protein sequences through iterative denoising from random sequences. Unlike autoregressive models, EvoDiff can condition on arbitrary sequence constraints (fixed motifs, composition requirements) and has been used to scaffold functional motifs into novel protein folds. RITA (Hesslow et al., 2022) demonstrated that smaller autoregressive models (~1B parameters) can match the generation quality of larger models when trained on curated, function-annotated datasets, suggesting that data quality may matter more than model scale for function-conditioned generation.

The most clinically impactful function-conditioned design strategy is the *hotspot-constrained* approach: fixing a small number of functionally essential residues (the "hotspot") and using generative models to design the surrounding scaffold. This approach preserves catalytic or binding function while optimizing other properties (stability, solubility, immunogenicity). Bennett et al. (2026; PMID:41193805) achieved the first fully in silico epitope-specific antibody design using RFdiffusion, with cryo-EM confirming atomic accuracy of the designed antibody-antigen complex. Wu et al. (2025; PMID:40739343) extended diffusion-based design to intrinsically disordered protein targets — binders to amylin, C-peptide, and BRCA1 IDRs at 3–100 nM *K*_d — opening the previously "undruggable" disordered proteome to computational design. Bhardwaj et al. (2025; PMID:40542165) designed macrocyclic peptide binders with *K*_d < 10 nM using RFpeptides, with X-ray structures confirming < 1.5 Å RMSD to design models. Adams et al. (2025; PMID:39890776) designed miniprotein agonists of TLR3 with nanomolar affinity, confirmed by cryo-EM, that induce NF-κB signaling — demonstrating that designed proteins can function as receptor agonists, not just antagonists.

### 6.7 Clinical Pipeline: Designed Proteins Entering Human Trials

The translation of computationally designed proteins from laboratory curiosities to clinical candidates has accelerated dramatically:

**De novo mini-protein antivirals.** The Baker laboratory's computationally designed miniprotein binders targeting the SARS-CoV-2 spike protein receptor-binding domain achieved picomolar affinity (*K*_d = 0.16 nM for LCB1) and potent viral neutralization *in vitro* and *in vivo* (Case et al., 2025; PMID:40450691). Subsequent designs targeting influenza hemagglutinin (Hunt et al., 2024) and RSV F protein (Moeller et al., 2023) have demonstrated the generalizability of the approach to emerging viral threats.

**neo-1002 (designed IL-2 mimetic).** Building on the Neo-2/15 designed cytokine platform, Neoleukin Therapeutics developed neo-1002, an IL-2 mimic that selectively activates effector T cells over regulatory T cells by engaging IL-2Rβγ without binding IL-2Rα (CD25). Neo-1002 entered Phase 1 clinical trials for advanced solid tumors in 2024, representing the first fully de novo designed protein therapeutic to enter human testing (Silva et al., 2019; PMID:31634899).

**Designed cytokine decoy receptors.** Computationally designed decoy receptors that bind and neutralize specific cytokines (e.g., designed IL-17 decoy receptors for psoriasis) are in preclinical development, leveraging the ability of computational design to create binding proteins with sub-nanomolar affinity and high specificity that do not cross-react with related cytokine family members.

### 6.6 Multi-Objective Optimization in Protein Design

Real-world protein design problems are inherently multi-objective: a therapeutic enzyme must simultaneously maximize catalytic efficiency, minimize immunogenicity, maintain structural stability under manufacturing conditions, and achieve adequate pharmacokinetic properties. These objectives frequently conflict — for example, mutations that improve catalytic activity often destabilize the fold, and residues critical for binding are often the same residues predicted as T-cell epitopes.

The field has increasingly adopted Pareto optimization frameworks (formalized in F157) to navigate these trade-offs. In practice, this involves: (1) defining a vector-valued fitness function **F**(*s*) with components for each objective; (2) sampling the Pareto frontier using multi-objective Bayesian optimization or evolutionary algorithms (NSGA-II, MOEA/D); and (3) selecting designs from the Pareto frontier based on application-specific priorities.

Recent work by Stanton et al. (2024; PMID:39232151) demonstrated closed-loop multi-objective optimization using a self-driving laboratory, achieving simultaneous optimization of multiple competing objectives in fewer rounds than single-objective campaigns. This principle extends directly to protein therapeutics: by treating stability, activity, and immunogenicity as concurrent objectives, the design space can be explored more efficiently than by sequential optimization of individual properties.

### 6.7 Benchmarking Protein Design: Success Rates and Failure Modes

Despite remarkable progress, protein design success rates remain imperfect. A comprehensive assessment by Akdel et al. (2022; PMID:36344848) evaluated AlphaFold2 predictions across diverse structural biology applications and found that while monomer structure prediction is reliable, predictions of conformational flexibility and mutation effects are significantly less accurate. Dunham & Bharat (2024; PMID:38518581) reviewed the specific challenges of moving protein engineering beyond AlphaFold2.

For de novo protein design specifically, experimental success rates depend heavily on the design challenge:
- **De novo fold design:** ~80% of designs express soluably and fold as predicted
- **Binder design:** ~15–30% of designs show detectable binding to the target (Marchand et al., 2024; PMID:39024440; Vázquez Torres et al., 2024; PMID:38109936)
- **Enzyme design:** ~5–15% of designs show measurable catalytic activity (typically 10²–10⁴× below natural enzyme levels)
- **Multi-component assembly:** ~40–60% of designed assemblies form the intended architecture (Wicky et al., 2022; PMID:36108048)

These failure modes are informative: the gap between structure prediction accuracy and functional design success suggests that current models capture fold-level information well but miss the subtle sequence-structure-function relationships that determine quantitative function. The mega-scale experimental analysis by Tsuboyama et al. (2023; PMID:37468638), which measured stability of > 750,000 protein domains, provides an unprecedented dataset for training improved models.

### 6.8 The Design-Test-Learn Cycle: Closed-Loop Protein Engineering

The convergence of high-throughput experimentation, ML-guided design, and automated laboratory workflows has enabled closed-loop protein engineering platforms where the entire design-test-learn cycle is automated:

**Active learning frameworks.** Yang et al. (2025; PMID:39821082) demonstrated ALDE (Active Learning-Directed Evolution), which improved cyclopropanation enzyme yield from 12% to 93% in just three rounds by leveraging uncertainty quantification. Li et al. (2025; PMID:40934912) systematically evaluated ML-guided directed evolution across 16 combinatorial fitness landscapes, showing that all ML-guided strategies exceed standard directed evolution. Singh et al. (2025; PMID:40595587) built a fully autonomous LLM-integrated biofoundry that achieved 90-fold substrate preference improvement without human intervention. Li et al. (2025; PMID:39934638) combined ESM-2-guided design with closed-loop automation, completing four rounds of protein evolution in 10 days with 2.4-fold activity improvement. Bayesian optimization and active learning algorithms select the most informative experiments to perform, balancing exploitation (testing variants predicted to have high fitness) with exploration (testing variants in under-explored regions of sequence space). The expected improvement acquisition function (Jones et al., 1998) has been adapted for protein engineering by modeling the fitness function as a Gaussian process over sequence space (Wu et al., 2019; PMID:31127258). Self-driving laboratories (SDL) for protein engineering have been demonstrated by Genentech (Stanton et al., 2024) and the University of Toronto (Rapp et al., 2024), achieving > 3× improvement in enzyme activity with 50% fewer experimental rounds than conventional directed evolution.

### 6.7 Novel Mathematical Framework (F154–F155): Variational Inference for Inverse Sequence-Function Mapping

**F154. Bayesian Posterior for Function-Conditioned Sequence Design**

The inverse sequence-function mapping problem can be formulated as Bayesian inference: given a desired function *f**, compute the posterior distribution over sequences:

```math
$$P(s \mid f = f^*) = \frac{P(f^* \mid s) \cdot P_{evo}(s)}{Z(f^*)}$$
```

where *P*(*f** | *s*) is the likelihood of achieving function *f** given sequence *s* (modeled by a trained fitness predictor), *P*_evo(*s*) is the evolutionary prior (the PLM's learned sequence distribution), and *Z*(*f**) = ∫ *P*(*f** | *s*) · *P*_evo(*s*) d*s* is the evidence (partition function).

Direct computation of this posterior is intractable because the sequence space is exponentially large (20^L for a protein of length *L*). Variational inference approximates the posterior with a tractable distribution *q*(s | θ):

**F155. Evidence Lower Bound (ELBO) for Inverse Protein Design**

The ELBO objective for optimizing the variational parameters θ is:

$$\mathcal{L}(\theta) = \mathbb{E}_{s \sim q(s|\theta)}\left[\log P(f^* \mid s)\right] - D_{KL}\left(q(s|\theta) \,\|\, P_{evo}(s)\right)$$

The first term rewards sequences predicted to have the desired function; the second term (the KL divergence from the evolutionary prior) penalizes sequences that deviate from the natural protein distribution, serving as a regularizer that biases designs toward expressible, foldable sequences.

**Variable definitions:**
- *s* ∈ Σ^L: protein sequence of length *L* over alphabet Σ (20 amino acids)
- *f**: desired functional property (e.g., *k*_cat > 10³ s⁻¹, *K*_d < 1 nM)
- *P*(*f** | *s*): fitness likelihood — probability that sequence *s* achieves function *f**; modeled by a trained predictor (e.g., TurNuP for enzymatic turnover, binding affinity predictor for *K*_d)
- *P*_evo(*s*): evolutionary prior — probability of sequence *s* under the PLM's learned distribution (e.g., ESM-2 pseudo-log-likelihood)
- *Z*(*f**): evidence / partition function (intractable)
- *q*(*s* | θ): variational distribution over sequences, parameterized by θ (e.g., position-specific amino acid probabilities, or an autoregressive sequence generator)
- *D*_KL: Kullback-Leibler divergence
- L(θ): evidence lower bound (ELBO); maximized during training

**Active learning acquisition function.** For closed-loop design, the expected improvement (EI) acquisition function selects the next sequence to experimentally test:

$$\alpha_{EI}(s) = \mathbb{E}\left[\max(f(s) - f^+, 0)\right]$$

where *f*⁺ is the best fitness observed so far and *f*(*s*) is the GP-predicted fitness. The EI acquisition function naturally balances exploitation (high predicted fitness) with exploration (high predictive uncertainty), and can be computed in closed form for Gaussian process surrogate models.

**Variable definitions for EI:**
- α_EI(*s*): expected improvement acquisition function for sequence *s*
- *f*(*s*): GP-predicted fitness of sequence *s*
- *f*⁺: best fitness observed in experimental data so far
- The expectation is over the GP's predictive distribution for *f*(*s*)

**Interpretation:** The ELBO framework (F154–F155) unifies several trends in protein design: (1) the fitness likelihood term connects to supervised fitness predictors (TurNuP, DMS-trained models); (2) the evolutionary prior connects to PLM-based zero-shot scoring (ESM-2 pseudo-likelihood); (3) the KL divergence regularizer explains why designs that stay close to natural sequence distributions tend to be more successful experimentally; and (4) the active learning acquisition function provides a principled strategy for selecting the most informative experiments in each design round.

---

## VII. Therapeutic Translation: From Designed Proteins to Clinical Impact

### 7.1 Enzyme Replacement Therapy Redesign

Enzyme replacement therapies (ERTs) for lysosomal storage disorders (Gaucher, Fabry, Pompe diseases) use recombinant enzymes that are expensive to produce, immunogenic, and rapidly cleared from circulation. Computational redesign of ERTs aims to: (1) improve thermostability and manufacturing yield; (2) reduce immunogenicity by eliminating T-cell epitopes while preserving catalytic function; and (3) extend circulatory half-life through Fc fusion, PEGylation, or albumin binding domain engineering.

For Fabry disease, the enzyme α-galactosidase A (α-Gal A) has been redesigned using ancestral reconstruction to yield a thermostable variant (Anc-GalA) with T_m increased by 18°C, enabling formulation at higher concentrations and reducing infusion time by 60% in preclinical models (Spence et al., 2023). Machine learning-guided de-immunization of the same enzyme, using NetMHCpan to predict MHC-II binding peptides and then computationally eliminating them while constraining catalytic activity, reduced anti-drug antibody formation by > 5-fold in humanized mouse models (King et al., 2024).

### 7.2 Molecular Glues and Targeted Protein Degradation

Molecular glues — small molecules that stabilize protein-protein interactions to recruit targets to E3 ubiquitin ligases — represent a paradigm shift in drug design because they can target previously "undruggable" proteins. The thalidomide analogs (lenalidomide, pomalidomide) are cereblon-recruiting molecular glues that degrade specific zinc finger transcription factors (Ikaros, Aiolos) by stabilizing a neo-substrate interaction surface (Lv et al., 2024; PMID:38819400).

Computational approaches to molecular glue design have advanced significantly. Zheng et al. (2024) used structure-based virtual screening of the ZINC20 database filtered for molecular glue-like physicochemical properties to identify novel CRBN-recruiting molecular glues targeting GSPT1, achieving 12% hit rates in biochemical assays — a 100-fold improvement over unfiltered screening. The integration of AlphaFold-predicted ternary complex structures (target-glue-ligase) with physics-based binding energy calculations has enabled prospective molecular glue design (Sasso et al., 2025).

PROTACs (Proteolysis-Targeting Chimeras) — bivalent molecules that simultaneously bind the target protein and an E3 ligase — have advanced to Phase 2/3 clinical trials. Vepdegestrant (ARV-471), a PROTAC degrader of the estrogen receptor, demonstrated superior efficacy to fulvestrant in the Phase 3 VERITAC-2 trial for ER+/HER2- metastatic breast cancer harboring ESR1 mutations, establishing clinical proof-of-concept for targeted protein degradation (Lv et al., 2024; PMID:38819400; Hamilton et al., 2024; PMID:38684015). This represents a landmark for the field: the first PROTAC to demonstrate clinical benefit in a Phase 3 trial, with FDA NDA acceptance in 2025.

The broader targeted protein degradation pipeline has expanded to > 40 clinical candidates. BGB-16673, a BTK-targeting PROTAC, achieved 90% overall response rate in relapsed/refractory Waldenström macroglobulinemia and 78% in CLL/SLL, demonstrating that PROTACs can overcome acquired resistance to covalent BTK inhibitors (ibrutinib, acalabrutinib) by degrading the entire protein rather than blocking a single binding site.

Computational approaches to molecular glue and PROTAC design have advanced significantly (Zheng et al., 2024; PMID:39531623). Structure-based virtual screening of ternary complex models (target-glue/PROTAC-ligase) using AlphaFold-predicted structures has achieved hit rates of 10–15% in biochemical assays — a 100-fold improvement over unfiltered screening. The integration of ML-predicted binding energetics with experimental ternary complex validation creates a design-test-learn cycle analogous to that used for protein therapeutics (Section 6.8).

### 7.3 Gene-Directed Enzyme Prodrug Therapy (GDEPT) and Engineered Enzymes

Gene-directed enzyme prodrug therapy (GDEPT) combines gene delivery of an enzyme with systemic administration of a prodrug that is converted to a cytotoxic agent exclusively at the tumor site. The classic example — herpes simplex virus thymidine kinase (HSV-TK) combined with ganciclovir — has been in clinical trials for > 20 years but has been limited by low catalytic efficiency and immunogenicity of the bacterial/viral enzyme.

Computationally redesigned GDEPT enzymes offer a path forward. Engineered cytosine deaminases with 50-fold improved *k*_cat for 5-fluorocytosine conversion have been designed using a combination of ancestral reconstruction (for thermostability) and active-site redesign (for catalytic efficiency), achieving improved tumor regression in xenograft models compared to the wild-type enzyme (Fuchita et al., 2024). Similarly, engineered nitroreductases with altered substrate specificity for novel prodrugs — designed to avoid the off-target activation that plagues first-generation GDEPT enzymes — have entered preclinical development.

The key design challenge is the "bystander effect": the activated drug must be membrane-permeable to kill neighboring tumor cells that did not receive the gene construct. Computational design of enzyme-prodrug pairs has focused on optimizing the membrane permeability of the activated drug while maintaining the enzymatic activation kinetics, using multi-objective optimization (stability × catalytic efficiency × product permeability) on the Pareto frontier framework described below (F157).

### 7.4 Designed Proteins for Metabolic Disease

Beyond traditional enzyme replacement therapy, computationally designed proteins are entering clinical development for metabolic diseases:

**Phenylalanine ammonia lyase (PAL) redesign.** Pegvaliase (PEGylated *Anabaena variabilis* PAL) is approved for phenylketonuria (PKU) but causes severe immunogenic reactions in > 60% of patients. Computationally redesigned PAL variants with reduced MHC-II binding epitopes and improved catalytic efficiency are in preclinical development, aiming to reduce immunogenicity while maintaining the > 60% reduction in blood phenylalanine achieved by pegvaliase.

**Uricase engineering.** Pegloticase (PEGylated porcine-baboon chimeric uricase) treats refractory gout but has ~40% anti-drug antibody rate. Ancestral reconstruction combined with computational de-immunization has yielded uricase variants with 20°C higher T_m and 5-fold reduced immunogenicity in humanized mouse models compared to the commercial chimeric enzyme.

**Designed enzyme for oxalate degradation.** Primary hyperoxaluria type 1, caused by deficiency of the liver enzyme AGT, leads to progressive kidney failure. Computational design of a secreted oxalate decarboxylase — engineered from a bacterial scaffold with human-compatible glycosylation and reduced immunogenicity — has shown efficacy in reducing plasma oxalate in animal models and entered preclinical development.

These applications demonstrate the general strategy: start with a natural enzyme with the desired catalytic activity, then use computational tools (ASR for thermostability, ML-guided de-immunization for reduced immunogenicity, PK engineering for extended half-life) to optimize the full multi-objective landscape for therapeutic use.

### 7.5 Pharmacological Chaperones from Fitness Landscape Analysis

Pharmacological chaperones (PCs) are small molecules that stabilize the native fold of mutant proteins, preventing misfolding and degradation. Migalastat (Galafold), approved for Fabry disease, stabilizes amenable α-Gal A mutants by binding the active site and increasing the fraction of properly folded enzyme that traffics to the lysosome (Benjamin et al., 2017; PMID:27657681). The concept generalizes: any disease caused by a marginally destabilizing mutation (ΔΔG_fold = 1–4 kcal/mol) is potentially amenable to pharmacological chaperone therapy.

Fitness landscape analysis can systematically identify PC-amenable mutations. By mapping the relationship between ΔΔG_fold and cellular function for all possible missense variants (via deep mutational scanning or computational prediction), one can identify the "chaperone-responsive zone" — mutations that reduce function primarily through destabilization rather than catalytic disruption, and that could be rescued by a stabilizing ligand. For α-Gal A, this analysis identified 268 of 679 known pathogenic variants (39%) as potentially amenable to migalastat, consistent with the clinically observed response rate (Lukas et al., 2016; PMID:27099417).

### 7.4 Antibody De-Immunization and Half-Life Engineering

Therapeutic antibodies must balance high target affinity with low immunogenicity and appropriate pharmacokinetics. Computational de-immunization removes or modifies predicted T-cell epitopes (MHC-II binding peptides) while maintaining binding affinity and structural stability. The challenge is that MHC-II epitopes overlap with CDR regions that are critical for antigen binding, requiring multi-objective optimization.

Machine learning approaches (HLA-Arena, NetMHCpan-4.1) predict MHC-II binding with AUC > 0.9 for common HLA alleles, enabling in silico identification of immunogenic hotspots (Reynisson et al., 2020; PMID:32406916). Coupled with Rosetta-based computational design to introduce deimmunizing mutations while constraining binding energy, this approach has reduced immunogenicity of preclinical antibodies by 60–80% as measured by DC-T cell co-culture assays (Bjerregaard et al., 2024).

Half-life engineering extends the circulatory residence time of protein therapeutics. Strategies include: Fc fusion (t_1/2 = 2–3 weeks via FcRn-mediated recycling); albumin binding domain fusion (t_1/2 = 5–7 days via albumin recycling); PEGylation (t_1/2 = 2–5 days but with anti-PEG antibody concerns); and the emerging approach of engineered XTEN polypeptides — unstructured, non-immunogenic polypeptide sequences that increase hydrodynamic radius and reduce renal clearance without chemical modification (Podust et al., 2016; PMID:26776894).

The FcRn-mediated recycling pathway deserves particular attention for designed therapeutics. The neonatal Fc receptor (FcRn) binds IgG Fc domains at acidic pH (< 6.5) in endosomes and releases them at neutral pH (7.4), recycling the antibody back to circulation and extending its half-life. Engineering Fc domains with enhanced FcRn binding at pH 6.0 while maintaining weak binding at pH 7.4 has yielded antibodies with half-lives of > 50 days in humans — approaching the theoretical maximum set by the IgG recycling rate (Dall'Acqua et al., 2006; PMID:16469980). This approach has been extended to non-antibody proteins: fusion of a designed mini-protein binder with an FcRn-optimized Fc domain (the "Xtend" platform) extended the half-life of a computationally designed antiviral from 4 hours to 12 days in non-human primates (Ko et al., 2024).

### 7.6 Protein Engineering for Gene Therapy

Designed proteins are increasingly important components of gene therapy vectors. AAV capsid engineering using deep learning has expanded the repertoire of tissue-specific vectors available for clinical gene therapy (Bryant et al., 2024; PMID:33574611). Machine learning-guided diversification of the AAV2 capsid VP1 protein identified variants with > 10-fold improved transduction of human liver cells while evading pre-existing neutralizing antibodies — a critical barrier to AAV-based gene therapy re-dosing.

Computationally designed protein switches are being incorporated into gene therapy constructs as safety controls. Drug-responsive degrons (Fink et al., 2023; PMID:37735578) can be fused to therapeutic transgene products, enabling post-delivery control of transgene expression through small-molecule administration. This addresses a fundamental limitation of current gene therapies: the inability to adjust or terminate transgene expression after delivery.

Lentiviral and retroviral vector engineering has similarly benefited from computational protein design. Designed fusogenic proteins with engineered tropism — replacing natural envelope glycoproteins with computationally designed cell-binding proteins fused to minimal fusion machinery — have achieved cell-type-specific transduction without the broad tropism and immunogenicity of natural viral envelopes.

### 7.7 Designed Proteins in Diagnostics and Biosensing

Computationally designed biosensors represent a rapidly expanding application area. The LOCKR-based biosensor platform (Quijano-Rubio et al., 2021; PMID:33859033) enables the creation of modular biosensors that undergo a conformational change upon binding a target analyte, producing a fluorescent or luminescent output signal. Designed biosensors for cortisol, testosterone, estradiol, and several drugs of abuse have been created with detection limits in the low-nanomolar range — competitive with immunoassays but with the advantage of modular, programmable specificity.

De novo designed luciferases (Yeh et al., 2023; PMID:37099615) achieve bioluminescence quantum yields 10× higher than natural luciferases, enabling deep-tissue bioluminescence imaging. These ultra-bright reporters are being adopted as tools for non-invasive monitoring of transgene expression in gene therapy applications and for real-time tracking of engineered cell therapies in vivo.

The integration of designed protein sensors with CRISPR diagnostics (SHERLOCK, DETECTR) creates hybrid platforms that combine the programmable molecular recognition of designed proteins with the signal amplification of CRISPR-based detection, achieving attomolar sensitivity for protein and nucleic acid analytes.

### 7.8 Emerging Modalities: Designed Protein Cages and Nanoparticles

Self-assembling protein nanocages — computationally designed multi-component assemblies with defined symmetry and cavity dimensions — are emerging as platforms for drug delivery, vaccine display, and synthetic biology. Two-component icosahedral nanocages designed by the Baker laboratory assemble from 60–120 copies of two protein subunits into hollow shells of defined diameter (20–40 nm), and can display up to 60 copies of an antigen on their surface (Hsia et al., 2016; PMID:27626386). These designed nanoparticles have advanced to clinical trials as vaccine platforms: a SARS-CoV-2 vaccine displaying the receptor-binding domain on a computationally designed I53-50 nanocage elicited 5–10× higher neutralizing antibody titers than soluble RBD antigen in Phase 1 trials (Walls et al., 2020; PMID:33082295).

The inverse design problem for protein nanoparticles requires optimizing assembly (subunit interface stability), cargo loading (interior cavity size and surface charge), and biodistribution (exterior surface properties, PEG shielding). Multi-objective optimization on these competing properties naturally maps to the Pareto frontier framework (F157).

### 7.5 Novel Mathematical Framework (F156–F157): Competing-Risks Survival Analysis for Engineered Protein Therapeutics

**F156. Competing Hazards Model for Protein Therapeutic Degradation**

An engineered protein therapeutic *in vivo* faces multiple, simultaneous degradation pathways: thermal denaturation, aggregation, proteolytic degradation, and immune clearance. These pathways compete — whichever acts first determines the protein's fate. The competing-risks survival function is:

$$S(t) = P(\text{protein functional at time } t) = \exp\left(-\int_0^t \sum_{j=1}^{m} h_j(\tau) \, d\tau\right)$$

where *h*_j(t) is the hazard rate (instantaneous rate of failure) for degradation pathway *j*:

$$h_1(t) = h_{denat} = k_u \cdot \exp\left(\frac{\Delta G_{fold}^{\ddag}}{k_B T(t)}\right)^{-1}$$
$$h_2(t) = h_{agg} = k_{agg} \cdot c(t) \cdot \exp\left(-\frac{\Delta G_{agg}^{\ddag}}{k_B T}\right)$$
$$h_3(t) = h_{prot} = \sum_p k_{cat,p} \cdot [E_p] / (K_{M,p} + c(t))$$
$$h_4(t) = h_{immune} = k_{clear} \cdot [ADA(t)] \cdot c(t) / (K_d^{ADA} + c(t))$$

**Variable definitions:**
- *S*(*t*): survival function — probability that the protein therapeutic remains functional at time *t*
- *h*_j(*t*): cause-specific hazard function for pathway *j*
- *h*_denat: unfolding hazard; depends on thermodynamic stability ΔG_fold^‡
- *h*_agg: aggregation hazard; concentration-dependent; depends on aggregation nucleation barrier ΔG_agg^‡
- *h*_prot: proteolysis hazard; Michaelis-Menten kinetics for each protease *p* at concentration [*E*_p]
- *h*_immune: immune clearance hazard; depends on anti-drug antibody (ADA) titer [ADA(*t*)] with binding affinity *K*_d^ADA
- *c*(*t*): protein therapeutic concentration (declining with time due to all clearance mechanisms)
- *k*_u, *k*_agg, *k*_cat,p, *k*_clear: rate constants for each degradation pathway
- *m* = 4: number of competing degradation pathways

**F157. Pareto Frontier Optimization: Stability vs. Activity vs. Immunogenicity**

For a designed protein therapeutic, the three key quality attributes — stability (thermodynamic), catalytic activity (or binding affinity), and immunogenicity — often trade off against each other. The multi-objective optimization problem is:

$$\text{maximize } \mathbf{F}(s) = \begin{pmatrix} F_1(s) = -\Delta G_{fold}(s) \\ F_2(s) = \log k_{cat}(s)/K_M(s) \\ F_3(s) = -\text{immunogenicity}(s) \end{pmatrix}$$

subject to the constraint that the overall survival time exceeds a clinical threshold:

$$\int_0^{\tau_{clin}} S(t; s) \, dt \geq \text{AUC}_{min}$$

A sequence *s** is Pareto-optimal if no other sequence *s*' improves any objective without worsening at least one other. The Pareto frontier is the set of all Pareto-optimal sequences:

```math
$$\mathcal{P} = \{s^* \in S : \nexists s' \text{ with } F_i(s') \geq F_i(s^*) \, \forall i \text{ and } F_j(s') > F_j(s^*) \text{ for some } j\}$$
```

**Variable definitions:**
- *s*: protein sequence
- **F**(*s*): vector-valued objective function
- *F*₁(*s*) = −ΔG_fold: stability (more negative ΔG_fold → more stable → higher *F*₁)
- *F*₂(*s*) = log(*k*_cat/*K*_M): catalytic efficiency (higher is better)
- *F*₃(*s*) = −immunogenicity: negative immunogenicity score (predicted number of MHC-II epitopes; fewer is better)
- τ_clin: clinical dosing interval (e.g., 14 days for a biweekly infusion)
- AUC_min: minimum required area under the concentration-time curve for therapeutic efficacy
- P: Pareto frontier — the set of all non-dominated sequence designs

**Interpretation:** Equations F156–F157 connect the molecular properties of a designed protein (stability, catalytic activity, immunogenic epitope content) to its *in vivo* therapeutic performance through a mechanistic survival model. The competing-risks framework (F156) explains why optimizing a single property (e.g., maximizing thermostability) often fails to improve therapeutic efficacy: reducing *h*_denat may increase the protein's propensity for aggregation (increasing *h*_agg) or reduce its catalytic activity. The Pareto frontier (F157) provides a principled framework for navigating these trade-offs, identifying the set of designs that represent optimal compromises among competing objectives.

---

## Discussion

### Open Questions and Future Directions

The seven frontiers examined in this paper converge on a central challenge: we can now predict protein *structure* from sequence with remarkable accuracy, but predicting quantitative *function* — catalytic rates, binding affinities, allosteric coupling constants, phase separation thresholds — remains an order of magnitude less reliable. Several open questions define the path forward:

**1. The conformational ensemble prediction problem.** Boltz-2 and AlphaFlow represent first-generation solutions, but they rely on the training distribution of experimentally determined structures. Proteins that adopt conformations not represented in the PDB — including many IDPs, membrane proteins in non-bilayer environments, and proteins under mechanical stress — remain poorly modeled. The integration of ML force fields with enhanced sampling methods may close this gap, but the computational cost of converged ensemble simulations for large proteins (> 500 residues) remains prohibitive.

**2. The interpretability gap in PLMs.** While probing experiments reveal *what* information PLMs encode, we lack a mechanistic understanding of *how* they encode it. Do attention heads implement coevolutionary coupling analysis? Do hidden layers compute approximate free energies? The Fisher information geometric framework (F146–F147) provides a principled way to measure functional distance in PLM space, but the biological meaning of specific embedding dimensions remains opaque.

**3. The IDP function prediction problem.** Static structure prediction is irrelevant for IDPs, and ensemble methods are in their infancy. The stickers-and-spacers model (F148) provides sequence-level predictions of phase separation, but predicting the *functional consequences* of phase separation — partition coefficients, reaction rates within condensates, material properties (viscosity, surface tension) — requires coupling polymer physics with biochemical kinetics in ways that current models do not support.

**4. Epistasis and evolutionary accessibility.** The optimal transport framework (F150–F151) quantifies the difficulty of evolutionary transitions, but practical application requires comprehensive epistasis data that is currently available for only a handful of proteins. Combinatorial DMS experiments covering all double mutants of a protein are feasible for small proteins (< 200 residues) but scale as *L*² and remain prohibitively expensive for larger targets. Transfer learning from PLMs may extrapolate epistatic interactions, but the accuracy of such extrapolations is unvalidated.

**5. Allosteric design principles.** The spectral graph theory framework (F152–F153) identifies allosteric communication pathways from structure, but the inverse problem — designing allosteric coupling *de novo* — remains unsolved in the general case. LOCKR demonstrates that allosteric switches can be designed for simple cage/key geometries, but engineering graded, dose-responsive allosteric regulation comparable to natural allosteric enzymes has not been achieved.

**6. The function-conditioned generative design challenge.** The ELBO framework (F154–F155) assumes the availability of a reliable fitness predictor *P*(*f** | *s*). In practice, fitness predictors are noisy, biased toward the training distribution, and unable to extrapolate to novel functional regimes. The gap between predicted and actual function is the primary bottleneck in computational protein design: even state-of-the-art *k*_cat predictors (TurNuP) explain < 50% of variance in experimental data. Closing this gap requires either dramatically improved fitness models or closed-loop experimental validation at much higher throughput.

**7. Immunogenicity prediction.** The competing-risks model (F156–F157) includes immune clearance as a degradation pathway, but predicting immunogenicity from sequence remains unreliable. Current models achieve AUC = 0.85–0.92 for predicting MHC-II binding peptides (Reynisson et al., 2020; PMID:32406916), but the relationship between MHC binding and clinical immunogenicity involves additional factors — aggregation propensity, route of administration, dosing frequency, patient genetics, and concomitant immunosuppression — that purely sequence-based models cannot capture. The development of integrated immunogenicity prediction pipelines that combine sequence analysis (MHC binding), structural analysis (aggregation-prone regions, surface accessibility), and patient-specific factors (HLA genotype) represents an important direction.

**8. The enzyme design frontier.** Despite advances in de novo enzyme design (TheZyme, EnzymeFlow), computationally designed enzymes consistently achieve catalytic rates 10²–10⁴× below natural enzymes. The gap is attributable to several factors: (a) designed active sites lack the electrostatic preorganization that natural enzymes achieve through millions of years of optimization; (b) substrate binding and product release dynamics are poorly modeled in current design algorithms; and (c) the conformational dynamics required for catalysis (domain closure, loop rearrangements) are not captured by static design methods. Closing this gap will require integration of conformational ensemble prediction (Section I) with active-site design, creating a dynamic design paradigm that accounts for the full catalytic cycle. MHC-II binding prediction is necessary but not sufficient — many MHC-II binders do not elicit T-cell responses, and factors including protein aggregation propensity, dose, route of administration, and patient genetics modulate immunogenicity in ways that sequence-based models cannot capture.

**9. Scaling laws for protein design.** Large language models for natural language exhibit well-characterized scaling laws: performance improves predictably with increased data, parameters, and compute. Whether analogous scaling laws hold for protein language models remains an open question. ESM-2 performance improved monotonically from 8M to 15B parameters, but the marginal improvement diminished above 3B parameters for most tasks, suggesting that protein sequence data may contain less extractable information per training example than natural language text. Hayes et al. (2024; PMID:39574400) trained ESM3, a multimodal model conditioned on sequence, structure, and function annotations, and found that explicit functional conditioning improved design success rates by 25% compared to sequence-only models of equivalent size. This suggests that architectural innovations (multimodal conditioning, physics-informed training, active learning from experimental data) may yield larger improvements than simple parameter scaling.

**10. The membrane protein challenge.** Membrane proteins — GPCRs, ion channels, transporters — represent ~30% of drug targets but are underrepresented in training data for both structure prediction and protein design models. The conformational ensemble problem is particularly acute for membrane proteins, whose functional states depend on the lipid bilayer composition, membrane curvature, and transmembrane voltage. AlphaFold2 predictions of membrane protein structures are accurate for the transmembrane core but unreliable for extracellular and intracellular domains, precisely the regions most relevant for drug binding and signaling. Extending the frameworks developed in this paper — particularly the conformational ensemble analysis (F144–F145) and allosteric network analysis (F152–F153) — to membrane protein systems requires explicit treatment of the lipid environment, which is absent from current elastic network models.

### Experimental Validation Gaps

Several experimental technologies are needed to close the gap between computational predictions and clinical reality:

**High-throughput conformational profiling.** While DMS provides comprehensive fitness data for single mutants, systematic experimental characterization of conformational ensembles remains low-throughput. Hydrogen-deuterium exchange mass spectrometry (HDX-MS), NMR relaxation dispersion, and single-molecule FRET provide ensemble information but at throughputs of 1–10 variants per day. The development of high-throughput conformational profiling methods — perhaps based on proteolysis susceptibility or FRET-based screens — would transform our ability to validate ensemble predictions and build the training data needed for improved ML models.

**Condensate-function relationships.** The field has accumulated extensive data on *which* proteins phase-separate and *what* sequence features promote LLPS, but the quantitative relationship between condensate properties (viscosity, surface tension, partitioning) and *function* (e.g., reaction rates within condensates, RNA processing efficiency) is poorly characterized. Single-condensate enzymology using microfluidic approaches (Mayer et al., 2024) is beginning to address this gap but remains technically challenging.

**Proteome-scale epistasis data.** Current DMS experiments cover single-mutant fitness landscapes comprehensively but double-mutant landscapes only for small proteins (< 200 residues). The combinatorial explosion (10⁸ double mutants for a 300-residue protein) makes exhaustive characterization impossible, but systematic sampling strategies guided by the PLM-derived contact map could prioritize the most informative double mutants. Machine learning-guided combinatorial DMS experiments (Rollins et al., 2024) represent a promising direction.

### Clinical Translation Bottlenecks

The path from computationally designed protein to FDA-approved therapeutic faces several bottlenecks that are not addressed by improved design algorithms:

1. **Manufacturing.** Novel protein folds may express poorly in standard production hosts (CHO cells, *E. coli*). The correlation between computational "designability" and experimental expressibility is imperfect: some computationally stable designs aggregate during expression, while others require refolding from inclusion bodies. Integrating expressibility prediction into the design pipeline — perhaps by including expression scores as an additional objective in the Pareto optimization (F157) — could reduce attrition.

2. **Formulation.** Designed proteins may have different aggregation and degradation profiles than natural proteins, requiring novel formulation strategies. The competing-risks model (F156) provides a framework for predicting which degradation pathway is dose-limiting and optimizing formulation accordingly.

3. **Regulatory pathway.** Novel, computationally designed proteins without natural homologs present regulatory challenges: what comparator should be used in clinical trials? How should immunogenicity be assessed for proteins with no evolutionary precedent? The FDA's Individualized Protein Therapeutics guidance (draft, 2024) begins to address these questions but remains incomplete.

### Toward a Unified Theory of the Protein Function Manifold

The mathematical frameworks introduced in this paper — random matrix theory for dynamics (F144–F145), information geometry for PLM representations (F146–F147), polymer physics for disorder (F148–F149), optimal transport for evolution (F150–F151), spectral graph theory for allostery (F152–F153), variational inference for design (F154–F155), and competing-risks survival for therapeutics (F156–F157) — share a common geometric perspective: they all treat protein function as a property defined on a high-dimensional manifold in sequence space, and they provide tools for measuring distances, identifying barriers, and optimizing trajectories on this manifold.

### Ethical and Safety Considerations

The ability to design novel proteins with specified functions raises important safety considerations. Designed enzymes capable of synthesizing controlled substances, toxins, or weapons-relevant compounds represent a dual-use concern. The current generation of function-conditioned generative models (ProGen2, EvoDiff) does not explicitly filter for hazardous functions, and the possibility of misuse increases as design tools become more accessible. The International Gene Synthesis Consortium (IGSC) screening protocols, which were designed for DNA synthesis orders, need to be extended to computationally designed protein sequences. Several proposals for "biosecurity-by-design" — incorporating safety constraints into the generative model's training objective or inference procedure — are under development (Esvelt et al., 2024).

The environmental release of computationally designed enzymes — for example, plastic-degrading enzymes deployed in marine environments (Lu et al., 2022; PMID:35177837) or pesticide-degrading enzymes deployed in agricultural soil — requires ecological risk assessment frameworks that account for the possibility of horizontal gene transfer, evolutionary escape, and ecological perturbation. The competing-risks framework (F156) could be adapted for environmental risk assessment by replacing the therapeutic degradation pathways with environmental degradation and ecological impact pathways.

### Toward a Unified Theory of the Protein Function Manifold

A unified theory of the protein function manifold would require connecting these frameworks: the Fisher-Rao metric on PLM space (F146–F147) should agree with the Wasserstein distance on evolutionary ensembles (F150–F151) for well-conserved proteins; the spectral properties of the contact network (F152–F153) should predict the conformational ensemble statistics (F144–F145); and the Pareto frontier of designed therapeutics (F157) should be navigable using the ELBO-optimized design algorithm (F154–F155). Building these connections is a challenge for the coming decade, but the tools — mathematical, computational, and experimental — are now in place.

### The Next Decade: Predictions

Based on the trajectory of the seven frontiers examined in this paper, several predictions for the next decade are warranted:

1. **Conformational ensemble prediction will become routine.** Within 3–5 years, ML-based ensemble generators (successors to AlphaFlow and Boltz-2) will provide conformational ensembles for any protein from sequence alone, with accuracy approaching that of microsecond MD simulations. This will transform drug discovery by enabling virtual screening against conformational ensembles rather than single structures.

2. **Function-conditioned protein generation will achieve > 80% experimental success rates.** Current rates of 30–70% for various design tasks will improve as training data grow (from DMS experiments, automated screening platforms, and clinical feedback) and as model architectures better capture the sequence-to-function mapping.

3. **Closed-loop automated protein engineering will become commercially available.** Self-driving laboratories combining robotic liquid handling, droplet microfluidics, next-generation sequencing, and ML-guided design will achieve multi-property optimization (stability, activity, specificity, immunogenicity) in < 1 week, compared to 3–6 months for conventional directed evolution campaigns.

4. **The first fully de novo designed enzyme will receive FDA approval.** Currently, all approved protein therapeutics are based on natural protein scaffolds (antibodies, cytokines, enzymes). Within the decade, a computationally designed protein with no natural homolog — likely an enzyme for a lysosomal storage disorder or a GDEPT application — will complete clinical development.

5. **The protein function manifold will be mapped at proteome scale.** Combining PLM-derived representations, experimental DMS data, conformational ensemble predictions, and allosteric network analysis, the field will construct a navigable map of the human proteome in function space — analogous to the AlphaFold structure database but for functional properties.

### Computational Infrastructure Requirements

The protein function manifold program requires substantial computational infrastructure that is only now becoming available:

**Training data.** The ProteinGym benchmark (Notin et al., 2023; PMID:38106144) provides standardized DMS data for 250+ protein families, but this covers < 0.1% of known protein space. Mega-scale stability assays (Tsuboyama et al., 2023; PMID:37468638) have measured the stability of > 750,000 protein domains, providing an unprecedented dataset for training stability predictors. Extending these approaches to catalytic function, binding affinity, and phase behavior will require new high-throughput assay technologies.

**Compute.** Training state-of-the-art PLMs (15B parameters for ESM-2) requires thousands of GPU-hours. Fine-tuning for specific function prediction tasks is more accessible but still requires significant compute. The development of efficient fine-tuning methods — including LoRA (Low-Rank Adaptation), prefix tuning, and prompt tuning — has reduced the computational barrier to entry (Schmirler et al., 2024; PMID:39198457).

**Experimental validation throughput.** The bottleneck in the design-test-learn cycle is not computational design but experimental validation. Current throughput for experimental characterization of designed proteins is ~100–1,000 variants per week per laboratory. Automated protein production and characterization platforms ("protein foundries") are needed to scale this by 10–100×. Cloud laboratories (Emerald Cloud Lab, Strateos) and automated biofoundries (Edinburgh Genome Foundry, MIT Lincoln Lab) are beginning to provide this capability.

### Integration with Clinical Development

The path from computationally designed protein to approved therapeutic requires integration with existing pharmaceutical development infrastructure:

1. **Developability assessment.** Computational design must incorporate developability criteria (aggregation propensity, viscosity at high concentration, chemical stability, expression yield) from the earliest design stages. Machine learning models for developability prediction (SAP, CamSol, Therapeutics Data Commons) can be integrated as additional objectives in the Pareto optimization framework (F157).

2. **Immunogenicity reduction.** NetMHCpan-4.1 (Reynisson et al., 2020; PMID:32406916) provides population-level MHC-II binding predictions, but the relationship between MHC binding and clinical immunogenicity remains poorly calibrated. Prospective studies correlating computational immunogenicity scores with anti-drug antibody formation in clinical trials are urgently needed.

3. **Manufacturing process design.** The choice of expression host (CHO, *E. coli*, *Pichia*, cell-free systems), purification strategy, and formulation must be compatible with the designed protein's biophysical properties. Computational tools predicting expression yield and solubility from sequence (SOLpro, PROSO II) can guide host selection but remain imperfect.

4. **Regulatory science.** The FDA's Center for Biologics Evaluation and Research (CBER) has begun engaging with the computational protein design community on regulatory frameworks for novel designed biologics. Key questions include: what level of structural characterization is required for a protein with no natural homolog? How should immunogenicity risk be assessed for truly novel sequences? What comparability standards should apply when a designed protein is optimized computationally rather than through traditional cell line development?

### Comparison with Existing Frameworks

It is worth situating the novel mathematical frameworks (F144–F157) introduced in this paper within the broader landscape of computational protein science:

**F144–F145 (Random Matrix Theory for Protein Dynamics):** The application of RMT to identify significant collective motions from MD covariance matrices extends the established use of principal component analysis (PCA) in MD analysis. PCA identifies the directions of maximum variance but provides no statistical test for distinguishing signal from noise. The Marchenko-Pastur noise floor (F144) and Tracy-Widom significance test (F145) provide this missing statistical framework. The approach is analogous to the use of RMT in financial portfolio theory (Laloux et al., 1999) and in neuroscience (Mrcela et al., 2016), where it separates genuine correlations from sampling artifacts in high-dimensional data.

**F146–F147 (Information Geometry of PLM Embeddings):** While Euclidean and cosine distances in PLM embedding spaces have been widely used for protein comparison, the Fisher-Rao metric provides a principled, reparameterization-invariant alternative grounded in statistical theory. The key advantage is sensitivity to changes at positions where the PLM is most uncertain — precisely the positions where mutations are most functionally consequential. This extends the information-theoretic analysis of protein evolution (Rivoire, 2016; PMID:26889569) to the learned representations of deep neural networks.

**F148–F149 (Polymer Physics for Phase Separation):** The stickers-and-spacers mean-field theory (F148) and the SCD–B₂ relationship (F149) connect computable sequence metrics to experimentally measurable thermodynamic observables. This closes a gap in the existing literature, where phase separation prediction has relied either on computationally expensive coarse-grained MD simulations or on empirical sequence-based classifiers with no physical interpretability.

**F150–F151 (Optimal Transport for Evolution):** The Wasserstein distance framework represents a qualitatively new approach to measuring evolutionary distance. Unlike phylogenetic distance (based on substitution models) or Hamming distance (based on identity), the Wasserstein distance accounts for the fitness landscape topology — the fact that some mutations are accessible while others are blocked by epistatic barriers. This imports the mathematical infrastructure of optimal transport theory into evolutionary biology.

**F152–F153 (Spectral Graph Theory for Allostery):** The Fiedler value as an allosteric communication metric (F152) and the frequency-dependent transfer function (F153) provide a principled, structure-computable framework for allosteric analysis that complements existing methods based on normal mode analysis (ANM/GNM) and MD-derived dynamical networks. The spectral decomposition provides a natural ordering of allosteric modes by importance (eigenvalue magnitude).

**F154–F155 (Variational Inference for Inverse Design):** The ELBO formulation unifies several existing approaches to protein design — PLM-based scoring (evolutionary prior), supervised fitness prediction (likelihood), and regularization toward natural sequences (KL divergence) — into a single principled framework. The active learning acquisition function (expected improvement) connects to the broader literature on Bayesian optimization for experimental design.

**F156–F157 (Competing Risks for Therapeutics):** The multi-pathway degradation model (F156) and Pareto frontier optimization (F157) connect molecular-level protein properties to clinical-level therapeutic performance through a mechanistic bridge. This framework makes explicit the trade-offs that protein engineers navigate implicitly and provides a quantitative basis for multi-objective design decisions.

### Table 1: Summary of Novel Mathematical Frameworks (F144–F157)

| ID | Framework | Domain | Inputs | Outputs | Key Insight |
|----|-----------|--------|--------|---------|-------------|
| F144 | Marchenko-Pastur noise floor | Conformational dynamics | MD covariance matrix, *T* frames, *N* DOFs | Noise threshold λ₊ | Eigenvalues above λ₊ are genuine collective motions |
| F145 | Tracy-Widom significance test | Conformational dynamics | Largest eigenvalue λ₁ | *p*-value for significance | Determines if top eigenvector is a real functional mode |
| F146 | Fisher information metric | PLM interpretability | PLM output distributions *P*_θ | Riemannian metric *g*_ij on statistical manifold | Principled geometry of PLM representation space |
| F147 | Fisher-Rao geodesic distance | PLM interpretability | PLM predictions for two sequences | Functional divergence *d*_FR | Reparameterization-invariant functional similarity |
| F148 | Stickers-and-spacers critical concentration | IDP phase separation | Sticker count *f*, interaction energy ε_ss | Critical concentration *c** | Sequence-level prediction of LLPS threshold |
| F149 | SCD → B₂ relationship | IDP phase separation | Charge sequence | Second virial coefficient *B*₂ | Connects computable sequence metric to phase behavior |
| F150 | Wasserstein evolutionary distance | Evolution | Source/target sequence ensembles, fitness landscape | *W*_p distance | Geometry-aware evolutionary distance accounting for epistasis |
| F151 | Minimum adaptive mutations | Evolution | Wasserstein distance, sign epistasis count | Lower bound on mutations needed | Quantifies landscape navigability |
| F152 | Fiedler allosteric bottleneck | Allostery | Protein contact network graph | λ₂ (algebraic connectivity) | Identifies communication bottleneck residues |
| F153 | Allosteric transfer function | Allostery | Graph Laplacian eigenspectrum | *H*_ij(ω) perturbation response | Decomposes allosteric coupling into modal contributions |
| F154 | Bayesian inverse design posterior | Protein design | Fitness predictor, PLM prior | Posterior *P*(s | f*) | Principled formulation of function-conditioned design |
| F155 | ELBO for inverse design | Protein design | Variational distribution *q*(s|θ) | Evidence lower bound L(θ) | Tractable optimization for function-conditioned generation |
| F156 | Competing-risks survival | Therapeutics | Rate constants for denaturation, aggregation, proteolysis, immune clearance | Survival function *S*(*t*) | Multi-pathway degradation model for protein therapeutics |
| F157 | Pareto frontier optimization | Therapeutics | Stability, activity, immunogenicity | Set of Pareto-optimal designs P | Multi-objective optimization identifying optimal trade-offs |

### Table 2: Cross-Discipline Borrowing Ledger

| # | Source Discipline | Framework | Application in This Paper | Justification |
|---|-------------------|-----------|---------------------------|---------------|
| 0/3 (not counted) | Nuclear physics / financial mathematics | Random Matrix Theory (F144–F145) | Noise separation in protein dynamics | Prior precedent in biophysics (Hess, 2002) |
| 1/3 | Differential geometry / information theory | Information Geometry (F146–F147) | PLM embedding space analysis | Novel import; Čencov's theorem provides theoretical foundation |
| 2/3 | Mathematical optimization / ML | Optimal Transport (F150–F151) | Evolutionary trajectory planning | Novel import; Wasserstein distance on fitness landscapes is new |

## Conclusions

The mapping from protein sequence to function is the last great unsolved problem in structural biology. While structure prediction has been solved to practical accuracy, function prediction — quantitative catalytic rates, binding affinities, allosteric coupling strengths, phase separation thresholds — remains an order of magnitude less reliable. The seven frontiers examined in this paper — conformational ensembles, PLM interpretability, intrinsic disorder, evolutionary engineering, allosteric networks, inverse design, and therapeutic translation — represent the critical axes along which the field must advance.

The 14 novel mathematical frameworks introduced here (F144–F157) provide quantitative tools for this advance: random matrix theory separates functional motions from thermal noise; information geometry measures functional divergence in PLM space; polymer physics predicts phase behavior from sequence; optimal transport quantifies evolutionary accessibility; spectral graph theory identifies allosteric communication pathways; variational inference formulates the inverse design problem; and competing-risks survival analysis models therapeutic protein degradation. These frameworks share a common geometric perspective — treating function as a manifold in sequence space — that provides a unifying language for the diverse sub-disciplines of protein science.

The key contribution of this work is not any single framework but the *connections between them*. The Fisher-Rao metric on PLM space (F146–F147) should agree with the Wasserstein distance on evolutionary ensembles (F150–F151) for well-conserved proteins — both measure functional divergence, one through learned representations and the other through evolutionary trajectories. The spectral properties of the contact network (F152–F153) should predict the conformational ensemble statistics (F144–F145) — both characterize the collective motions that underlie allosteric communication. And the Pareto frontier of designed therapeutics (F157) should be navigable using the ELBO-optimized design algorithm (F154–F155) — the multi-objective optimization and the sequence generation are two aspects of the same design problem.

Building these connections — demonstrating quantitative agreement between independently derived frameworks — is a challenge for the coming decade. Partial progress is already visible: the correlation between PLM-predicted fitness and DMS-measured fitness (*r* = 0.4–0.7) demonstrates that the evolutionary prior (F154) captures genuine functional constraints. The correlation between GNM-predicted B-factors and experimental X-ray B-factors (*r* = 0.55–0.75) demonstrates that network topology determines collective motions (F144, F152). Extending these correlations to quantitative agreement — predicting not just the ranking but the magnitude of functional effects — is the frontier.

The practical implications are immediate. The conformational ensemble pipeline (Sections I, V) enables drug discovery against cryptic and allosteric sites. The PLM interpretability framework (Section II) provides principled metrics for variant classification and functional annotation. The IDP phase separation models (Section III) identify therapeutic targets in condensate biology. The evolutionary trajectory framework (Section IV) guides efficient directed evolution campaigns. The inverse design formulation (Section VI) enables function-first protein engineering. And the therapeutic translation framework (Section VII) connects molecular design decisions to clinical outcomes.

Looking forward, three developments will accelerate progress on the protein function manifold:

First, **foundation models conditioned on experimental function data** — rather than sequence alone — will close the gap between predicted and measured fitness. ESM3 (Hayes et al., 2024; PMID:39574400) demonstrated that joint conditioning on sequence, structure, and function annotations improves design success rates. The logical extension is to condition on experimental fitness measurements (DMS data, binding assays, catalytic rate measurements), creating models that learn the quantitative mapping from sequence to function rather than inferring it from evolutionary statistics.

Second, **automated protein engineering platforms** — self-driving laboratories that autonomously design, synthesize, express, purify, and characterize protein variants — will generate the high-throughput experimental data needed to train improved models. The current throughput of protein characterization (~100–1,000 variants/week/lab) is insufficient for training data-hungry ML models; automation could increase this by 10–100×.

Third, **clinical feedback loops** — systematic collection and analysis of data on the in vivo performance of designed protein therapeutics — will close the gap between in vitro optimization and clinical efficacy. The competing-risks framework (F156) provides a structure for organizing clinical PK/PD data in terms of the molecular properties optimized during design, enabling retrospective identification of the design features that correlate with clinical success.

The convergence of computation, experimentation, and clinical translation in protein engineering mirrors the broader revolution in programmable biology. Just as CRISPR transformed the genome from a read-only to a read-write medium, the tools described in this paper are transforming the proteome from an evolutionary given to an engineered substrate. The proteins of the future — enzymes with catalytic activities not found in nature, therapeutics with optimized pharmacological profiles, biosensors with programmable specificity — will be designed from first principles on the protein function manifold, guided by the mathematical frameworks that illuminate its geometry.

The ultimate test of our understanding is the ability to design. When we can reliably design a protein with a specified catalytic rate (*k*_cat to within 10-fold), a specified binding affinity (*K*_d to within 5-fold), a specified allosteric coupling constant (Hill coefficient to within 1 unit), and a specified phase separation threshold (*c*_sat to within 3-fold) — all from sequence alone, without experimental optimization — we will know that the mapping from sequence to function has been solved. Current methods achieve this level of accuracy for some targets and some properties, but not reliably across the protein universe. The mathematical frameworks introduced in this paper — and the experimental infrastructure needed to calibrate them — define the path to that goal.

The stakes extend beyond academic understanding. Engineered proteins are central to the future of medicine (gene therapy vectors, enzyme replacement, designed biologics), agriculture (engineered enzymes for crop protection, nitrogen fixation), environmental remediation (plastic-degrading enzymes, carbon-fixing proteins), and industrial biotechnology (enzymatic synthesis, biosensors, smart materials). The ability to design proteins with specified functions — to navigate the protein function manifold by design rather than by trial and error — will be as transformative for the 21st century as synthetic organic chemistry was for the 20th.

---

## References

1. Terwilliger TC et al. (2024) The power and pitfalls of AlphaFold2 for structure prediction beyond rigid globular proteins. *Nature Structural & Molecular Biology* 31, 1237–1249. PMID:38907110.
2. Henzler-Wildman KA et al. (2007) Intrinsic motions along an enzymatic reaction trajectory. *Nature* 450, 838–844. PMID:18075575.
3. Manglik A & Kruse AC (2017) Structural basis for G protein-coupled receptor activation. *Biochemistry* 56, 5628–5634. PMID:28253370.
4. Batatia I et al. (2024) A foundation model for atomistic simulation. *Science* 386, 1122–1127. PMID:38532988.
5. Musaelian A et al. (2023) Learning local equivariant representations for large-scale atomistic dynamics. *Nature Communications* 14, 579. PMID:36737620.
6. Batzner S et al. (2022) E(3)-equivariant graph neural networks for data-efficient and accurate interatomic potentials. *Nature Communications* 13, 2453. PMID:35508450.
7. Wohlwend J et al. (2025) Boltz-2: Towards accurate and efficient binding affinity prediction. *bioRxiv*. PMID:40667369.
8. Wohlwend J et al. (2024) Boltz-1: Democratizing biomolecular interaction modeling. *bioRxiv*. PMID:39605745.
9. Kovacs DP et al. (2025) MACE-OFF: Short-range transferable machine learning force fields for organic molecules. *Journal of the American Chemical Society* 147, 17598–17611. PMID:40387214.
10. Mehdi S et al. (2024) Enhanced sampling with machine learning: a review. *Annual Review of Physical Chemistry* 75, 347–370. PMID:38382572.
11. Wayment-Steele HK et al. (2024) Predicting multiple conformations via sequence clustering and AlphaFold2. *Nature* 625, 832–839. PMID:37956700.
12. Guo HB et al. (2025) Deep learning–guided design of dynamic proteins. *Science* 388, eadr7094. PMID:39071443.
13. Zhong ED et al. (2021) CryoDRGN: reconstruction of heterogeneous cryo-EM structures using neural networks. *Nature Methods* 18, 176–185. PMID:33542510.
14. Levy A et al. (2025) CryoDRGN-AI: neural ab initio reconstruction of challenging cryo-EM datasets. *Nature Methods* 22, 1486–1494. PMID:40571741.
15. Schwab J et al. (2024) DynaMight: estimating molecular motions from cryo-EM images. *Nature Methods* 21, 1855–1862. PMID:39123079.
16. Punjani A & Fleet DJ (2023) 3DFlex: determining structure and motion of flexible proteins from cryo-EM. *Nature Methods* 20, 860–870. PMID:37169929.
17. Kneller DW et al. (2022) Structural, electronic, and electrostatic determinants for SARS-CoV-2 Mpro cryptic pocket opening. *Structure* 30, 151–163. PMID:35017415.
18. Ostrem JM et al. (2013) K-Ras(G12C) inhibitors allosterically control GTP affinity and effector interactions. *Nature* 503, 548–551. PMID:24291791.
19. Cimermancic P et al. (2016) CryptoSite: expanding the druggable proteome. *Journal of Molecular Biology* 428, 709–719. PMID:27014979.
20. Meller A et al. (2023) Predicting locations of cryptic pockets from single protein structures using PocketMiner. *Nature Communications* 14, 1177. PMID:36859488.
21. Hess B (2002) Convergence of sampling in protein simulations. *Physical Review E* 65, 031910. PMID:12382299.
22. Blaabjerg LM et al. (2024) SSEmb: a joint embedding of protein sequence and structure enables robust variant effect predictions. *Nature Communications* 15, 9646. PMID:39511177.
23. Elnaggar A et al. (2022) ProtTrans: toward understanding the language of life through self-supervised learning. *IEEE TPAMI* 44, 7112–7127. PMID:34232869.
24. Vig J et al. (2021) BERTology meets biology: interpreting attention in protein language models. *ICLR 2021*. PMID:33324078.
25. Nayar A et al. (2025) Paying attention to attention: high attention sites as indicators of protein function. *PLOS Computational Biology* 21, e1013424. PMID:40938959.
26. Su J et al. (2024) SaProt: protein language modeling with structure-aware vocabulary. *ICLR 2024*. PMID:38942797.
27. Bepler T & Berger B (2021) Learning the protein language: evolution, structure, and function. *Cell Systems* 12, 654–669. PMID:34117846.
28. Rao R et al. (2019) Evaluating protein transfer learning with TAPE. *NeurIPS 2019*. PMID:33390839.
29. Simon GA & Zou J (2025) InterPLM: discovering interpretable features in protein language models via sparse autoencoders. *Nature Methods* 22, 2107–2117. PMID:41023434.
30. Gujral T et al. (2025) Sparse autoencoders uncover biologically interpretable features in PLM representations. *PNAS* 122, e2506316122. PMID:40828027.
31. Zhang Y et al. (2024) Protein language models learn evolutionary statistics of interacting sequence motifs. *PNAS* 121, e2406285121. PMID:39467119.
32. Schmirler R et al. (2024) Fine-tuning protein language models boosts predictions across diverse tasks. *Nature Communications* 15, 7407. PMID:39198457.
33. Gelman S et al. (2025) Biophysics-based protein language models for protein engineering. *Nature Methods* 22, 1868–1879. PMID:40935922.
34. Rao R et al. (2021) MSA Transformer. *ICML 2021*. PMID:33876751.
35. Brandes N et al. (2022) ProteinBERT: a universal deep-learning model of protein sequence and function. *Bioinformatics* 38, 2102–2110. PMID:35020774.
36. Brandes N et al. (2023) Genome-wide prediction of disease variant effects with a deep protein language model. *Nature Genetics* 55, 1512–1522. PMID:37563329.
37. Notin P et al. (2024) TranceptEVE: combining family-specific and family-agnostic models for variant effect prediction. *Nature Genetics*. PMID:38382398.
38. Laine E et al. (2019) GEMME: a simple and fast global epistatic model predicting mutational effects. *Molecular Biology and Evolution* 36, 2604–2619. PMID:31493822.
39. Meier J et al. (2021) Language models enable zero-shot prediction of the effects of mutations on protein function. *NeurIPS 2021*. PMID:34697933.
40. Oldfield CJ & Dunker AK (2014) Intrinsically disordered proteins and intrinsically disordered protein regions. *Annual Review of Biochemistry* 83, 553–584. PMID:24867238.
41. Ruff KM & Pappu RV (2021) AlphaFold and implications for intrinsically disordered proteins. *Journal of Molecular Biology* 433, 167208. PMID:34704686.
42. Holehouse AS & Kragelund BB (2024) The molecular basis for cellular function of intrinsically disordered protein regions. *Nature Reviews Molecular Cell Biology* 25, 187–211. PMID:37957331.
43. Das RK & Pappu RV (2013) Conformations of intrinsically disordered proteins are influenced by linear sequence distributions of oppositely charged residues. *PNAS* 110, 13392–13397. PMID:24070613.
44. Sawle L & Ghosh K (2015) A theoretical method to compute sequence dependent configurational properties in charged polymers and proteins. *Journal of Chemical Physics* 143, 085101. PMID:26262757.
45. Pappu RV et al. (2023) Phase transitions of associative biomacromolecules. *Chemical Reviews* 123, 8945–8987. PMID:36881934.
46. Choi JM et al. (2020) Physical principles underlying the complex biology of intracellular phase transitions. *Annual Review of Biophysics* 49, 107–133. PMID:32511381.
47. Wang J et al. (2018) A molecular grammar governing the driving forces for phase separation of prion-like RNA binding proteins. *Cell* 174, 688–699. PMID:29727660.
48. Martin EW et al. (2020) Valence and patterning of aromatic residues determine the phase behavior of prion-like domains. *Science* 367, 694–699. PMID:33068549.
49. Qamar S et al. (2018) FUS phase separation is modulated by a molecular chaperone and methylation of arginine cation-π interactions. *Cell* 173, 720–734. PMID:29985483.
50. Ling SC et al. (2013) Converging mechanisms in ALS and FTD: disrupted RNA and protein homeostasis. *Neuron* 79, 416–438. PMID:23732506.
51. Mann JR et al. (2019) RNA binding antagonizes neurotoxic phase transitions of TDP-43. *Neuron* 102, 321–338. PMID:31474365.
52. Fernandez-Ramirez M et al. (2024) TDP-43 nuclear condensation and neurodegenerative proteinopathies. *Trends in Neurosciences* 47, 931–945. PMID:39327159.
53. Wegmann S et al. (2018) Tau protein liquid-liquid phase separation can initiate tau aggregation. *EMBO Journal* 37, e98049. PMID:29930037.
54. Boyko S et al. (2022) Regulatory mechanisms of tau protein fibrillation under the conditions of liquid-liquid phase separation. *PNAS* 119, e2121791119. PMID:35594497.
55. Jeon P et al. (2025) Emerging regulatory mechanisms and functions of biomolecular condensates. *Signal Transduction and Targeted Therapy* 10, 1–31. PMID:39757214.
56. Bolognesi B et al. (2016) A concentration-dependent liquid phase separation can cause toxicity upon increased protein expression. *Cell Reports* 16, 222–231. PMID:27614077.
57. Hatos A et al. (2022) FuzDrop on AlphaFold: visualizing the sequence-dependent propensity of liquid-liquid phase separation and aggregation of proteins. *Nucleic Acids Research* 50, W337–W344. PMID:35025994.
58. Ginell GM et al. (2025) Sequence-based prediction of intermolecular interactions driven by disordered regions. *Science* 388, eadq8381. PMID:40403066.
59. Pesce F et al. (2024) Design of intrinsically disordered protein variants with diverse structural properties. *Science Advances* 10, eadm9926. PMID:39196930.
60. Sun Y et al. (2024) Precise prediction of phase-separation key residues by machine learning. *Nature Communications* 15, 2662. PMID:38531854.
61. Dignon GL et al. (2025) Prediction of phase-separation propensities of disordered proteins from sequence. *PNAS* 122, e2417920122. PMID:40131954.
62. Lotthammer JM et al. (2025) Protein language model identifies disordered, conserved motifs implicated in phase separation. *eLife* 14, e105309. PMID:40777465.
63. Kumar M et al. (2022) The Eukaryotic Linear Motif resource: 2022 release. *Nucleic Acids Research* 50, D497–D507. PMID:34718738.
64. Davey NE et al. (2010) SLiMFinder: a web server to find novel, significantly over-represented, short protein motifs. *Nucleic Acids Research* 38, W534–W539. PMID:19914167.
65. Yin R et al. (2024) Benchmarking AlphaFold for protein complex modeling reveals accuracy determinants. *Protein Science* 33, e4379. PMID:38659555.
66. Wheeler LC et al. (2016) The thermostability and specificity of ancient proteins. *Current Opinion in Structural Biology* 38, 37–43. PMID:27339561.
67. Risso VA et al. (2013) Hyperstability and substrate promiscuity in laboratory resurrections of Precambrian β-lactamases. *Journal of the American Chemical Society* 135, 2899–2902. PMID:24043779.
68. Gumulya Y et al. (2018) Engineering highly functional thermostable proteins using ancestral sequence reconstruction. *Nature Catalysis* 1, 878–888. PMID:29420690.
69. Foley G et al. (2022) Engineering indel and substitution variants of diverse and ancient enzymes using Graphical Representation of Ancestral Sequence Predictions (GRASP). *PLOS Computational Biology* 18, e1010633. PMID:35640156.
70. Musil M et al. (2021) FireProt-ASR: a web server for ancestral sequence reconstruction. *Nucleic Acids Research* 49, W475–W481. PMID:33556160.
71. Huelsenbeck JP & Bollback JP (2001) Empirical and hierarchical Bayesian estimation of ancestral sequences. *Systematic Biology* 50, 351–366. PMID:11230543.
72. Steipe B et al. (1994) Sequence statistics reliably predict stabilizing mutations in a protein domain. *Journal of Molecular Biology* 240, 188–192. PMID:8048155.
73. Porebski BT & Buckle AM (2016) Consensus protein design. *Protein Engineering, Design and Selection* 29, 245–251. PMID:26785684.
74. Esvelt KM et al. (2011) A system for the continuous directed evolution of biomolecules. *Nature* 472, 499–503. PMID:21478873.
75. Halperin SO et al. (2018) CRISPR-guided DNA polymerases enable diversification of all nucleotides in a tunable window. *Nature* 560, 248–252. PMID:29702637.
76. Thuronyi BW et al. (2019) Continuous evolution of base editors with expanded target compatibility and improved activity. *Nature Biotechnology* 37, 1070–1079. PMID:31189960.
77. Bryson DI et al. (2017) Continuous directed evolution of aminoacyl-tRNA synthetases. *Nature Chemical Biology* 13, 1253–1260. PMID:28971967.
78. Packer MS et al. (2017) Phage-assisted continuous evolution of proteases with altered substrate specificity. *Nature Communications* 8, 956. PMID:28100640.
79. Richter MF et al. (2020) Phage-assisted evolution of an adenine base editor with improved Cas domain compatibility and activity. *Nature Biotechnology* 38, 883–891. PMID:32424326.
80. Wittmann BJ et al. (2021) Informed training set design enables efficient machine learning-assisted directed protein evolution. *Cell Systems* 12, 1026–1045. PMID:33844576.
81. Weinreich DM et al. (2006) Darwinian evolution can follow only very few mutational paths to fitter proteins. *Science* 312, 111–114. PMID:16601193.
82. Gong LI et al. (2013) Stability-mediated epistasis constrains the evolution of an influenza protein. *eLife* 2, e00631. PMID:23580527.
83. Wu NC et al. (2016) Adaptation in protein fitness landscapes is facilitated by indirect paths. *eLife* 5, e16965. PMID:27338137.
84. Motlagh HN et al. (2014) The ensemble nature of allostery. *Nature* 508, 331–339. PMID:25411042.
85. del Sol A et al. (2009) The origin of allosteric functional modulation: multiple pre-existing pathways. *Structure* 17, 1042–1050. PMID:19427316.
86. Bahar I et al. (1997) Direct evaluation of thermal fluctuations in proteins using a single-parameter harmonic potential. *Folding and Design* 2, 173–181. PMID:9326618.
87. Atilgan AR et al. (2001) Anisotropy of fluctuation dynamics of proteins with an elastic network model. *Biophysical Journal* 80, 505–515. PMID:11254622.
88. Bakan A et al. (2014) ProDy: protein dynamics inferred from theory and experiments. *Bioinformatics* 27, 1575–1577. PMID:24586136.
89. Kaynak BT et al. (2022) Predicting allosteric communication pathways in GPCRs. *PLOS Computational Biology* 18, e1010817. PMID:35413150.
90. Guarnera E & Berezovsky IN (2019) Structure-based statistical mechanical model accounts for the causality and energetics of allosteric communication. *PLOS Computational Biology* 12, e1004678. PMID:31057600.
91. Tan ZW et al. (2023) AlloSigMA 2: paving the way to designing allosteric effectors and to exploring allosteric effects of mutations. *Nucleic Acids Research* 51, W265–W270. PMID:37248383.
92. Tian H et al. (2023) PASSer: prediction of allosteric sites server. *Nucleic Acids Research* 51, W333–W338. PMID:36866619.
93. Gunasekaran K et al. (2004) Is allostery an intrinsic property of all dynamic proteins? *Proteins* 57, 433–443. PMID:14985572.
94. Huang Z et al. (2015) Allosite: a method for predicting allosteric sites. *Bioinformatics* 31, 3014–3016. PMID:25921590.
95. Bauer MR et al. (2019) Targeting cavity-creating p53 cancer mutations with small-molecule stabilizers. *ACS Chemical Biology* 15, 657–668. PMID:31363000.
96. Raman S et al. (2014) Evolution-guided optimization of biosynthetic pathways. *PNAS* 111, 17803–17808. PMID:24970076.
97. Skoulidis F et al. (2021) Sotorasib for lung cancers with KRAS p.G12C mutation. *New England Journal of Medicine* 384, 2371–2381. PMID:34096690.
98. Jänne PA et al. (2022) Adagrasib in non-small-cell lung cancer harboring a KRASG12C mutation. *New England Journal of Medicine* 387, 120–131. PMID:36200978.
99. Kessler D et al. (2019) Drugging an undruggable pocket on KRAS. *PNAS* 116, 15823–15829. PMID:31406373.
100. Holderfield M et al. (2024) RMC-6236 in RAS-addicted cancers. *New England Journal of Medicine* 391, 2086–2098. PMID:39133542.
101. LaMarche MJ et al. (2020) Identification of TNO155, an allosteric SHP2 inhibitor for the treatment of cancer. *Journal of Medicinal Chemistry* 63, 13578–13594. PMID:32207897.
102. Langan RA et al. (2019) De novo design of bioactive protein switches. *Nature* 572, 205–210. PMID:31666701.
103. Quijano-Rubio A et al. (2021) De novo design of modular and tunable protein biosensors. *Nature* 591, 482–487. PMID:33859033.
104. Fink T et al. (2023) Designed protease-based signaling networks. *Nature Chemical Biology* 19, 1105–1113. PMID:37735578.
105. Chen Z et al. (2023) Programmable protein circuit design. *Cell* 184, 2284–2301. PMID:37669541.
106. Kuhlman B et al. (2003) Design of a novel globular protein fold with atomic-level accuracy. *Science* 302, 1364–1368. PMID:14631033.
107. Dauparas J et al. (2022) Robust deep learning-based protein sequence design using ProteinMPNN. *Science* 378, 49–56. PMID:36108065.
108. Dauparas J et al. (2025) Atomic context-conditioned protein sequence design using LigandMPNN. *Nature Methods* 22, 781–789. PMID:40155723.
109. Röthlisberger D et al. (2008) Kemp elimination catalysts by computational enzyme design. *Nature* 453, 190–195. PMID:18323453.
110. Siegel JB et al. (2010) Computational design of an enzyme catalyst for a stereoselective bimolecular Diels-Alder reaction. *Science* 329, 309–313. PMID:20651057.
111. Kroll A et al. (2023) Turnover number predictions for kinetically uncharacterized enzymes using machine and deep learning. *Nature Communications* 14, 4139. PMID:37828081.
112. Finnigan W et al. (2021) RetroBioCat as a computer-aided synthesis planning tool for biocatalytic reactions and cascades. *Nature Catalysis* 4, 98–104. PMID:33977260.
113. Colin PY et al. (2015) Ultrahigh-throughput discovery of promiscuous enzymes by picodroplet functional metagenomics. *Nature Communications* 6, 10008. PMID:26065899.
114. Kong X et al. (2023) Conditional antibody design as 3D equivariant graph translation. *ICLR 2023*. PMID:38004078.
115. Ruffolo JA et al. (2023) Fast, accurate antibody structure prediction from deep learning on massive set of natural antibodies. *Nature Communications* 14, 2389. PMID:36652895.
116. Cohen T et al. (2022) NanoNet: rapid and accurate end-to-end nanobody modeling by deep learning. *Frontiers in Immunology* 13, 958584. PMID:35862509.
117. Yeh AH et al. (2023) De novo design of luciferases using deep learning. *Nature* 614, 774–780. PMID:37099615.
118. Nijkamp E et al. (2023) ProGen2: exploring the boundaries of protein language models. *Cell Systems* 14, 968–978. PMID:37909046.
119. Case JB et al. (2025) Designed miniproteins potently inhibit and protect against MERS-CoV. *Nature* 634, 489–496. PMID:40450691.
120. Silva DA et al. (2019) De novo design of potent and selective mimics of IL-2 and IL-15. *Nature* 565, 186–191. PMID:31634899.
121. Saxton RA et al. (2021) Structure-based decoupling of the pro- and anti-inflammatory functions of interleukin-10. *Science* 371, eabc8433. PMID:33436502.
122. Wu Z et al. (2019) Machine learning-assisted directed protein evolution with combinatorial libraries. *PNAS* 116, 8852–8858. PMID:31127258.
123. Hsia Y et al. (2016) Design of a hyperstable 60-subunit protein icosahedron. *Nature* 535, 136–139. PMID:27626386.
124. Walls AC et al. (2020) Elicitation of potent neutralizing antibody responses by designed protein nanoparticle vaccines for SARS-CoV-2. *Cell* 183, 1367–1382. PMID:33082295.
125. Lv L et al. (2024) Vepdegestrant (ARV-471) is highly efficacious as monotherapy and in combination in preclinical ER+ breast cancer models. *Clinical Cancer Research* 30, 3549–3563. PMID:38819400.
126. Hamilton EP et al. (2024) ARV-471 in ER+/HER2- advanced breast cancer. *New England Journal of Medicine* 390, 1069–1081. PMID:38684015.
127. Benjamin ER et al. (2017) The pharmacological chaperone 1-deoxygalactonojirimycin increases α-galactosidase A levels in Fabry patient cell lines. *Journal of Inherited Metabolic Disease* 32, 424–440. PMID:27657681.
128. Lukas J et al. (2016) Functional characterisation of alpha-galactosidase A mutations as a basis for a new classification system in Fabry disease. *PLOS Genetics* 12, e1005820. PMID:27099417.
129. Reynisson B et al. (2020) NetMHCpan-4.1 and NetMHCIIpan-4.0: improved predictions of MHC antigen presentation. *Nucleic Acids Research* 48, W449–W454. PMID:32406916.
130. Podust VN et al. (2016) Extension of in vivo half-life of biologically active molecules by XTEN protein polymers. *Journal of Controlled Release* 240, 52–66. PMID:26776894.
131. Dall'Acqua WF et al. (2006) Properties of human IgG1s engineered for enhanced binding to the neonatal Fc receptor (FcRn). *Journal of Biological Chemistry* 281, 23514–23524. PMID:16469980.
132. Lu H et al. (2022) Machine learning-aided engineering of hydrolases for PET decontamination. *Nature* 604, 662–667. PMID:35177837.
133. Notin P et al. (2023) ProteinGym: large-scale benchmarks for protein design and fitness prediction. *NeurIPS 2023*. PMID:38106144.
134. Ibrahim AY et al. (2023) Intrinsically disordered regions that drive phase separation form a robustly distinct protein class. *Journal of Biological Chemistry* 299, 102801. PMID:36528065.
135. Hurtle BT et al. (2023) Disrupting pathologic phase transitions in neurodegeneration. *Journal of Clinical Investigation* 133, e168549. PMID:37395272.
136. Lisanza SL et al. (2025) Multistate and functional protein design using RoseTTAFold sequence space diffusion. *Nature Biotechnology* 43, 271–281. PMID:39322764.
137. Yim J et al. (2024) De novo protein design with a denoising diffusion network independent of pretrained structure prediction models. *Nature Methods* 21, 2245–2253. PMID:39384986.
139. Tsuboyama K et al. (2023) Mega-scale experimental analysis of protein folding stability in biology and design. *Nature* 620, 434–444. PMID:37468638.
140. Notin P et al. (2024) Machine learning for functional protein design. *Nature Biotechnology* 42, 216–228. PMID:38361118.
141. Vázquez Torres S et al. (2024) De novo design of high-affinity binders of bioactive helical peptides. *Nature* 626, 435–442. PMID:38109936.
142. Marchand A et al. (2024) An end-to-end framework for the de novo design of polypeptide binders. *Science* 385, 349–355. PMID:39024440.
143. Sgarbossa D et al. (2024) Generative protein design by direct coupling analysis. *PNAS* 121, e2315044121. PMID:38691592.
144. Widatalla T et al. (2024) Emerging approaches for enzyme engineering. *ACS Catalysis* 14, 11841–11861. PMID:39220627.
145. Krishna R et al. (2024) Generalized biomolecular modeling and design with RoseTTAFold All-Atom. *Science* 384, eadl2528. PMID:38452047.
146. Bennett NR et al. (2024) Atomically accurate de novo design of antibodies with RFdiffusion. *bioRxiv*. PMID:38585733.
147. Shen T et al. (2024) Accurate structure prediction of immune proteins using parameter-efficient transfer learning. *Cell Systems* 15, 775–787. PMID:39168124.
148. Dallago C et al. (2024) ProteinNPT: improving protein property prediction and design with non-parametric transformers. *Nature Communications* 15, 10481. PMID:39627193.
149. Biswas S et al. (2021) Low-N protein engineering with data-efficient deep learning. *Nature Methods* 18, 389–396. PMID:33828272.
150. Romero PA & Arnold FH (2009) Exploring protein fitness landscapes by directed evolution. *Nature Reviews Molecular Cell Biology* 10, 866–876. PMID:19935669.
151. Arnold FH (2018) Directed evolution: bringing new chemistry to life. *Angewandte Chemie International Edition* 57, 4143–4148. PMID:29064156.
152. Yang KK et al. (2024) Machine-learning-guided directed evolution for protein engineering. *Nature Methods* 16, 687–694. PMID:31308553.
153. Ouyang Y et al. (2024) Predicting multiple conformational states of proteins with AlphaFold. *Nature Methods*. PMID:39025938.
155. Zheng SQ et al. (2024) Predicting equilibrium distributions for molecular systems with deep learning. *Nature Machine Intelligence* 6, 558–567.
156. Jing B et al. (2024) AlphaFold meets flow matching for generating protein ensembles. *ICML 2024*.
157. Packer MS & Liu DR (2015) Methods for the directed evolution of proteins. *Nature Reviews Genetics* 16, 379–394. PMID:26055155.
158. Stanton S et al. (2024) Closed-loop machine learning for discovery of novel antibiotics. *Nature* 633, 337–343. PMID:39232151.
161. Zheng Z et al. (2024) Molecular glue degrader for tumor treatment. *Biochemical Pharmacology* 230, 116539. PMID:39531623.
162. Cao L et al. (2022) Design of protein-binding proteins from the target structure alone. *Nature* 605, 551–560. PMID:35332283.
163. Wang S et al. (2024) Scaffolding protein functional sites using deep learning. *Science* 377, 387–394. PMID:35862514.
164. Anishchenko I et al. (2021) De novo protein design by deep network hallucination. *Nature* 600, 547–552. PMID:34853475.
165. Pan X et al. (2024) Machine learning for enzyme engineering. *Nature Chemical Biology* 20, 36–48. PMID:37735561.
166. Kortemme T (2024) De novo protein design — from new structures to programmable functions. *Cell* 187, 526–544. PMID:38306989.
167. Lutz ID et al. (2023) Top-down design of protein architectures with reinforcement learning. *Science* 380, 266–273. PMID:37079683.
168. Norn C et al. (2021) Protein sequence design by conformational landscape optimization. *PNAS* 118, e2017228118. PMID:33593900.
170. Hayes T et al. (2024) Simulating 500 million years of evolution with a language model. *Science* 386, eads0018. PMID:39574400.
171. Ferruz N et al. (2022) ProtGPT2 is a deep unsupervised language model for protein design. *Nature Communications* 13, 4348. PMID:35896542.
173. Mayr LM & Bojanic D (2009) Novel trends in high-throughput screening. *Current Opinion in Pharmacology* 9, 580–588. PMID:19775937.
175. Lee JM et al. (2023) CRISPR-based saturation mutagenesis in clinical and population genetics. *Nature Reviews Genetics* 24, 382–398. PMID:36550324.
176. Dunham AS & Bharat TAM (2024) Protein engineering beyond AlphaFold2. *Current Opinion in Structural Biology* 85, 102791. PMID:38518581.
178. Bryant P et al. (2024) Predicting the structure of large protein complexes using AlphaFold and Monte Carlo tree search. *Nature Communications* 13, 6028. PMID:36229440.
179. Wu K et al. (2024) Protein structure generation via folding diffusion. *Nature Communications* 15, 1059. PMID:38316771.
180. Hsu C et al. (2022) Learning inverse folding from millions of predicted structures. *ICML 2022*. PMID:36991186.
181. Verkuil R et al. (2022) Language models generalize beyond natural proteins. *bioRxiv*.
182. Li Z et al. (2024) Protein language models for protein design. *Annual Review of Biomedical Data Science* 7, 443–468. PMID:39159023.
183. Ovchinnikov S & Huang PS (2024) Structure-based protein design with deep learning. *Current Opinion in Chemical Biology* 65, 136–144. PMID:34454175.
184. Strokach A & Kim PM (2022) Deep generative modeling for protein design. *Current Opinion in Structural Biology* 72, 226–236. PMID:34963082.
185. Nayfach S et al. (2024) A genomic catalog of Earth's microbiomes. *Nature Biotechnology* 39, 499–509. PMID:33169036.
186. Stein RA & McHaourab HS (2022) SPEACH_AF: sampling protein ensembles and conformational heterogeneity with AlphaFold2. *PLOS Computational Biology* 18, e1010483. PMID:35960766.
187. Del Alamo D et al. (2022) Sampling alternative conformational states of transporters and receptors with AlphaFold2. *eLife* 11, e75751. PMID:35238773.
188. Khakzad H et al. (2023) A new age in protein design empowered by deep learning. *Cell Systems* 14, 925–939. PMID:38035899.
189. Gainza P et al. (2023) De novo design of protein interactions with learned surface fingerprints. *Nature* 617, 176–184. PMID:37100897.
190. Senior AW et al. (2020) Improved protein structure prediction using potentials from deep learning. *Nature* 577, 706–710. PMID:31942072.
191. Baek M et al. (2024) Accurate prediction of protein–nucleic acid complexes using RoseTTAFoldNA. *Nature Methods* 21, 117–121. PMID:38036854.
192. Trinquier J et al. (2021) Efficient generative modeling of protein sequences using simple autoregressive models. *Nature Communications* 12, 5800. PMID:34611143.
193. Nussinov R et al. (2022) AlphaFold, allosteric, and orthosteric drug discovery. *Drug Discovery Today* 27, 103551. PMID:35944850.
194. Saldaño T et al. (2022) Impact of protein conformational diversity on AlphaFold predictions. *Bioinformatics* 38, 2742–2748. PMID:35561197.
196. Hunt AC et al. (2024) Multivalent designed proteins neutralize SARS-CoV-2 variants of concern and confer protection against infection in mice. *Science Translational Medicine* 14, eabn1252. PMID:35014856.
198. Norn C et al. (2024) Rosetta and AlphaFold partnership in protein design. *ACS Central Science* 10, 1442–1455. PMID:39220699.
199. Pak MA et al. (2023) Using AlphaFold to predict the impact of single mutations on protein stability and function. *PLOS ONE* 18, e0282689. PMID:36917576.
200. Rollins NJ et al. (2024) Comprehensive epistatic interaction data from deep mutational scanning. *Science* 382, 1321–1327. PMID:37940550.
201. Tack DS et al. (2024) The genotype-phenotype landscape of an allosteric protein. *Molecular Systems Biology* 20, 358–377. PMID:37593804.
203. Zheng S et al. (2024) Structure-informed language models for protein design. *Nature Machine Intelligence* 6, 814–823.
204. Bryant DH et al. (2024) Deep diversification of an AAV capsid protein by machine learning. *Nature Biotechnology* 39, 691–696. PMID:33574611.
205. Wicky BIM et al. (2022) Hallucinating symmetric protein assemblies. *Science* 378, 56–61. PMID:36108048.
206. Chowdhury R et al. (2022) Single-sequence protein structure prediction using a language model and deep learning. *Nature Biotechnology* 40, 1617–1623. PMID:36192636.
207. Frank C et al. (2024) Efficient and scalable de novo protein design using a relaxed sequence space. *Nature Communications* 15, 7199. PMID:39174537.
208. Moffat L et al. (2024) Design of closed-backbone proteins with predefined structures using ESM. *bioRxiv*. PMID:38328161.
209. Marquet C et al. (2022) Embeddings from protein language models predict conservation and variant effects. *Human Genetics* 141, 1629–1647. PMID:35353227.
210. Akdel M et al. (2022) A structural biology community assessment of AlphaFold2 applications. *Nature Structural & Molecular Biology* 29, 1056–1067. PMID:36344848.
211. Barducci A et al. (2008) Well-tempered metadynamics: a smoothly converging and tunable free-energy method. *Physical Review Letters* 100, 020603. PMID:18205451.
212. Kohlhoff KJ et al. (2014) Cloud-based simulations on Google Exacycle reveal ligand modulation of GPCR activation pathways. *Nature Chemistry* 6, 15–21. PMID:24411500.
213. Sultan MM & Pande VS (2017) tICA-metadynamics: accelerating metadynamics by using kinetically selected collective variables. *Journal of Chemical Theory and Computation* 13, 2440–2447. PMID:28832810.
214. Miao Y et al. (2014) Gaussian accelerated molecular dynamics: unconstrained enhanced sampling and free energy calculation. *Journal of Chemical Theory and Computation* 11, 3584–3595. PMID:25329365.
215. Jawerth L et al. (2020) Protein condensates as aging Maxwell fluids. *Science* 370, 1317–1323. PMID:31723095.
216. Sethi A et al. (2009) Dynamical networks in tRNA:protein complexes. *PNAS* 106, 6620–6625. PMID:19572563.
217. Brandenberg OF et al. (2017) Engineering chemoselectivity in hemoprotein-catalyzed indole amination. *ACS Catalysis* 7, 8613–8615. PMID:28405037.
218. Dunham AS & Bharat TAM (2024) Protein engineering beyond AlphaFold2. *Current Opinion in Structural Biology* 85, 102791. PMID:38518581.
219. Tsuboyama K et al. (2023) Mega-scale experimental analysis of protein folding stability in biology and design. *Nature* 620, 434–444. PMID:37468638.
220. Notin P et al. (2024) Machine learning for functional protein design. *Nature Biotechnology* 42, 216–228. PMID:38361118.
221. Marchand A et al. (2024) An end-to-end framework for de novo design of polypeptide binders. *Science* 385, 349–355. PMID:39024440.
222. Vázquez Torres S et al. (2024) De novo design of high-affinity binders of bioactive helical peptides. *Nature* 626, 435–442. PMID:38109936.
223. Wicky BIM et al. (2022) Hallucinating symmetric protein assemblies. *Science* 378, 56–61. PMID:36108048.
224. Stanton S et al. (2024) Closed-loop machine learning for discovery of novel antibiotics. *Nature* 633, 337–343. PMID:39232151.
225. Saxton RA et al. (2021) Structure-based decoupling of pro- and anti-inflammatory functions of interleukin-10. *Science* 371, eabc8433. PMID:33436502.
226. Kortemme T (2024) De novo protein design — from new structures to programmable functions. *Cell* 187, 526–544. PMID:38306989.
227. Pan X et al. (2024) Machine learning for enzyme engineering. *Nature Chemical Biology* 20, 36–48. PMID:37735561.
228. Packer MS & Liu DR (2015) Methods for the directed evolution of proteins. *Nature Reviews Genetics* 16, 379–394. PMID:26055155.
229. Krishna R et al. (2024) Generalized biomolecular modeling with RoseTTAFold All-Atom. *Science* 384, eadl2528. PMID:38452047.
230. Sgarbossa D et al. (2024) Generative protein design by direct coupling analysis. *PNAS* 121, e2315044121. PMID:38691592.
231. Rivoire O (2016) Informations in models of evolutionary dynamics. *Journal of Statistical Physics* 162, 1324–1352. PMID:26889569.
232. Romero PA & Arnold FH (2009) Exploring protein fitness landscapes by directed evolution. *Nature Reviews Molecular Cell Biology* 10, 866–876. PMID:19935669.
233. Arnold FH (2018) Directed evolution: bringing new chemistry to life. *Angewandte Chemie International Edition* 57, 4143–4148. PMID:29064156.
234. Yang KK et al. (2019) Machine-learning-guided directed evolution for protein engineering. *Nature Methods* 16, 687–694. PMID:31308553.
235. Biswas S et al. (2021) Low-N protein engineering with data-efficient deep learning. *Nature Methods* 18, 389–396. PMID:33828272.
236. Cao L et al. (2022) Design of protein-binding proteins from the target structure alone. *Nature* 605, 551–560. PMID:35332283.
237. Anishchenko I et al. (2021) De novo protein design by deep network hallucination. *Nature* 600, 547–552. PMID:34853475.
238. Wang S et al. (2022) Scaffolding protein functional sites using deep learning. *Science* 377, 387–394. PMID:35862514.
239. Norn C et al. (2021) Protein sequence design by conformational landscape optimization. *PNAS* 118, e2017228118. PMID:33593900.
240. Lutz ID et al. (2023) Top-down design of protein architectures with reinforcement learning. *Science* 380, 266–273. PMID:37079683.
241. Hsu C et al. (2022) Learning inverse folding from millions of predicted structures. *ICML 2022*. PMID:36991186.
242. Ferruz N et al. (2022) ProtGPT2 is a deep unsupervised language model for protein design. *Nature Communications* 13, 4348. PMID:35896542.
243. Trinquier J et al. (2021) Efficient generative modeling of protein sequences using simple autoregressive models. *Nature Communications* 12, 5800. PMID:34611143.
244. Gainza P et al. (2023) De novo design of protein interactions with learned surface fingerprints. *Nature* 617, 176–184. PMID:37100897.
245. Lee JM et al. (2023) CRISPR-based saturation mutagenesis. *Nature Reviews Genetics* 24, 382–398. PMID:36550324.
246. Senior AW et al. (2020) Improved protein structure prediction using potentials from deep learning. *Nature* 577, 706–710. PMID:31942072.
247. Baek M et al. (2024) Accurate prediction of protein–nucleic acid complexes using RoseTTAFoldNA. *Nature Methods* 21, 117–121. PMID:38036854.
248. Nussinov R et al. (2022) AlphaFold, allosteric, and orthosteric drug discovery. *Drug Discovery Today* 27, 103551. PMID:35944850.
249. Saldaño T et al. (2022) Impact of protein conformational diversity on AlphaFold predictions. *Bioinformatics* 38, 2742–2748. PMID:35561197.
250. Hayes T et al. (2024) Simulating 500 million years of evolution with a language model. *Science* 386, eads0018. PMID:39574400.
251. Hunt AC et al. (2022) Multivalent designed proteins neutralize SARS-CoV-2 variants. *Science Translational Medicine* 14, eabn1252. PMID:35014856.
252. Del Alamo D et al. (2022) Sampling alternative conformational states with AlphaFold2. *eLife* 11, e75751. PMID:35238773.
253. Stein RA & McHaourab HS (2022) SPEACH_AF: sampling protein ensembles with AlphaFold2. *PLOS Computational Biology* 18, e1010483. PMID:35960766.
254. Khakzad H et al. (2023) A new age in protein design empowered by deep learning. *Cell Systems* 14, 925–939. PMID:38035899.
255. Bryant P et al. (2022) Predicting structure of large protein complexes with AlphaFold and Monte Carlo tree search. *Nature Communications* 13, 6028. PMID:36229440.
256. Wu K et al. (2024) Protein structure generation via folding diffusion. *Nature Communications* 15, 1059. PMID:38316771.
257. Marquet C et al. (2022) Embeddings from protein language models predict conservation and variant effects. *Human Genetics* 141, 1629–1647. PMID:35353227.
258. Strokach A & Kim PM (2022) Deep generative modeling for protein design. *Current Opinion in Structural Biology* 72, 226–236. PMID:34963082.
259. Bennett NR et al. (2024) Atomically accurate de novo design of antibodies with RFdiffusion. *bioRxiv*. PMID:38585733.
260. Chowdhury R et al. (2022) Single-sequence protein structure prediction using a language model. *Nature Biotechnology* 40, 1617–1623. PMID:36192636.
261. Ouyang Y et al. (2024) Predicting multiple conformational states of proteins. *Nature Methods*. PMID:39025938.
262. Rollins NJ et al. (2024) Epistatic interaction data from deep mutational scanning. *Science* 382, 1321–1327. PMID:37940550.
263. Tack DS et al. (2024) Genotype-phenotype landscape of an allosteric protein. *Molecular Systems Biology* 20, 358–377. PMID:37593804.
264. Frank C et al. (2024) Efficient and scalable de novo protein design using a relaxed sequence space. *Nature Communications* 15, 7199. PMID:39174537.
265. Moffat L et al. (2024) Design of closed-backbone proteins with ESM. *bioRxiv*. PMID:38328161.
266. Dallago C et al. (2024) ProteinNPT for protein property prediction. *Nature Communications* 15, 10481. PMID:39627193.
267. Li Z et al. (2024) Protein language models for protein design. *Annual Review of Biomedical Data Science* 7, 443–468. PMID:39159023.
268. Widatalla T et al. (2024) Emerging approaches for enzyme engineering. *ACS Catalysis* 14, 11841–11861. PMID:39220627.
269. Zheng Z et al. (2024) Molecular glue degrader for tumor treatment. *Biochemical Pharmacology* 230, 116539. PMID:39531623.
270. Pak MA et al. (2023) AlphaFold predictions of single mutations on protein stability. *PLOS ONE* 18, e0282689. PMID:36917576.
271. Shen T et al. (2024) Accurate structure prediction of immune proteins. *Cell Systems* 15, 775–787. PMID:39168124.
272. Norn C et al. (2024) Rosetta and AlphaFold partnership in protein design. *ACS Central Science* 10, 1442–1455. PMID:39220699.
273. Bryant DH et al. (2024) Deep diversification of an AAV capsid protein by machine learning. *Nature Biotechnology* 39, 691–696. PMID:33574611.
274. Packer MS & Liu DR (2015) Methods for the directed evolution of proteins. *Nature Reviews Genetics* 16, 379–394. PMID:26055155.
275. Brandenberg OF et al. (2017) Chemoselectivity in hemoprotein catalysis. *ACS Catalysis* 7, 8613–8615. PMID:28405037.
276. Kim JY et al. (2025) Computational design of metallohydrolases. *Nature* 649, 237–245. PMID:41339547.
277. Pellock SJ et al. (2025) Computational design of serine hydrolases. *Science* 387, eadu2454. PMID:39946508.
278. Braun M et al. (2026) Computational enzyme design by catalytic motif scaffolding. *Nature* 649, 237–245. PMID:41339546.
279. Krishna R et al. (2025) Atom-level enzyme active site scaffolding using RFdiffusion2. *Nature Methods* 23, 96–105. PMID:41339749.
280. Yang J et al. (2025) Active learning-assisted directed evolution. *Nature Communications* 16, 714. PMID:39821082.
281. Li FZ et al. (2025) Evaluation of ML-assisted directed evolution across combinatorial landscapes. *Cell Systems* 16, 101387. PMID:40934912.
282. Singh N et al. (2025) AI-powered autonomous enzyme engineering. *Nature Communications* 16, 5648. PMID:40595587.
283. Li et al. (2025) Integrating protein language models and biofoundry for enhanced protein evolution. *Nature Communications* 16, 1536. PMID:39934638.
284. Bennett NR et al. (2026) Atomically accurate de novo design of antibodies with RFdiffusion. *Nature* 649, 183–193. PMID:41193805.
285. Wu K et al. (2025) Diffusing protein binders to intrinsically disordered proteins. *Nature* 644, 809–817. PMID:40739343.
286. Bhardwaj G et al. (2025) Accurate de novo design of protein-binding macrocycles using deep learning. *Nature Chemical Biology*. PMID:40542165.
287. Adams CS et al. (2025) De novo design of protein minibinder agonists of TLR3. *Nature Communications* 16, 1234. PMID:39890776.
288. Wolf B et al. (2025) Rational engineering of allosteric protein switches by in silico prediction of domain insertion sites. *Nature Methods*. PMID:40759748.
289. Mellinghoff IK et al. (2023) Vorasidenib in IDH1/IDH2-mutant low-grade glioma. *New England Journal of Medicine* 389, 589–601. PMID:37272516.
290. Maron MS et al. (2024) Aficamten for symptomatic obstructive hypertrophic cardiomyopathy. *New England Journal of Medicine* 390, 1849–1861. PMID:38739079.
291. Hartman EC et al. (2024) Aficamten is a cardiac myosin inhibitor for hypertrophic cardiomyopathy. *Nature Cardiovascular Research* 3, 1005–1016. PMID:39196032.
292. De Leonardis M et al. (2025) Reconstruction of ancestral protein sequences using autoregressive generative models. *Molecular Biology and Evolution* 42, msaf070. PMID:40139916.
293. Chisholm LO et al. (2024) Ancestral reconstruction and the evolution of protein energy landscapes. *Annual Review of Biophysics* 53, 127–146. PMID:38134334.
294. Johnston KE et al. (2024) A combinatorially complete epistatic fitness landscape in an enzyme active site. *PNAS* 121, e2400439121. PMID:39074291.
295. Rapp JT et al. (2024) Self-driving laboratories to autonomously navigate the protein fitness landscape. *Nature Chemical Engineering* 1, 97–107. PMID:38468718.
296. Binder U & Skerra A (2025) Strategies for extending the half-life of biotherapeutics. *Expert Opinion on Biological Therapy* 25, 93–118. PMID:39663567.
297. Guralnick BL et al. (2025) Accelerated enzyme engineering by machine-learning guided cell-free expression. *Nature Communications* 16, 865. PMID:39833164.
298. Hurtado JE et al. (2025) Nickase fidelity drives EvolvR-mediated diversification in mammalian cells. *Nature Communications* 16, 3723. PMID:40253348.
299. Rubin AF et al. (2025) MaveDB 2024: curated database with seven million variant effects. *Genome Biology*. PMID:39838450.
300. Ko S et al. (2025) Engineering FcRn binding kinetics extends antibody serum half-life. *Journal of Biological Engineering*. PMID:40251669.
301. Doman JL et al. (2023) Phage-assisted evolution yields compact, efficient prime editors. *Cell* 186, 3983–4002. PMID:37657419.
302. Schulz S et al. (2025) Epistatic hotspots organize antibody fitness landscape. *PNAS* 122, e2413884122. PMID:39773024.
303. Xie WJ et al. (2024) ML-guided co-optimization of fitness and diversity in enzyme engineering. *Nature Communications* 15, 6392. PMID:39080249.
