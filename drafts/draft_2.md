# Structural and Molecular Biology

## Abstract

The period from 2020 to 2026 has witnessed a convergence of technological breakthroughs—atomic-resolution cryo-electron microscopy, AI-driven structure prediction, and advanced chemical biology—that has rendered previously intractable problems in structural and molecular biology experimentally accessible for the first time. This document provides a comprehensive, mathematically rigorous analysis of five distinct research frontiers that have emerged at this intersection: (1) the structural enzymology of LINE-1 retrotransposons, where the first atomic-resolution structures of the ORF2 protein have revealed the mechanistic basis of target-primed reverse transcription; (2) the prediction of protein conformational ensembles and dynamics by artificial intelligence, where the completion of the static structure prediction problem has exposed the grand challenge of predicting Boltzmann-weighted conformational distributions from sequence; (3) the cryo-EM structural biology of functional RNAs, where scaffold-based approaches have broken through the resolution barrier for protein-free RNA structures; (4) metabolite-derived histone modifications and the lactylation frontier, where the identification of writer enzymes has transformed an epigenetic observation into a structurally tractable field; and (5) liquid-to-solid transitions in biomolecular condensates, where NMR and cryo-electron tomography have achieved the sensitivity to detect pathological structural transitions within condensed phases. For each frontier, we present the foundational discoveries, derive the relevant biophysical and mathematical frameworks, critically evaluate the open questions, and assess the experimental strategies most likely to yield high-impact advances. We demonstrate that these five directions, while scientifically distinct, share a common enabling principle: the resolution revolution in structural tools has opened biological questions that were unanswerable at the molecular level even five years ago.

---

## 1. Introduction

### 1.1 The Resolution Revolution in Structural Biology

The central goal of structural biology is to determine the three-dimensional arrangement of atoms within biological macromolecules and to infer functional mechanism from this arrangement. For the better part of six decades following Kendrew's determination of the myoglobin structure at 6 Å resolution by X-ray crystallography (Kendrew et al., 1958), and the subsequent atomic-resolution structures of hemoglobin (Perutz et al., 1960), the field advanced incrementally—each new structure requiring months to years of crystallization optimization, synchrotron data collection, and computational phasing.

The period 2013–2025 witnessed a transformation of the field so rapid and so comprehensive that it has been termed the "resolution revolution" (Kühlbrandt, 2014). This revolution was driven by three convergent advances:

**Cryo-electron microscopy (cryo-EM).** The development of direct electron detectors (McMullan et al., 2009; Li et al., 2013), motion correction algorithms (Zheng et al., 2017), and iterative refinement software (Scheres, 2012; Punjani et al., 2017) elevated single-particle cryo-EM from a low-resolution technique capable of resolving only the gross morphology of large complexes to a method routinely achieving atomic resolution (< 2 Å) on favorable specimens (Yip et al., 2020; Nakane et al., 2020). The 2017 Nobel Prize in Chemistry recognized this transformation. By 2025, cryo-EM had surpassed X-ray crystallography as the dominant method for macromolecular structure determination in the Protein Data Bank, accounting for approximately 30% of new depositions.

**AI-driven structure prediction.** AlphaFold2 (Jumper et al., 2021) solved the protein structure prediction problem for single-chain, static structures, achieving experimental accuracy (median GDT-TS > 92) at CASP14. This was extended to protein–protein, protein–nucleic acid, and protein–ligand complexes by AlphaFold3 (Abramson et al., 2024), which introduced a diffusion-based generative architecture. The Isomorphic Labs Drug Design Engine (IsoDDE) subsequently more than doubled AlphaFold3's accuracy on challenging out-of-distribution benchmarks (Isomorphic Labs, 2026), demonstrating that the frontier of AI-driven structural biology has shifted from static structure prediction to generalization across novel chemical space, conformational dynamics, and binding affinity estimation.

**Chemical biology and metabolomics.** Advances in quantitative mass spectrometry, metabolite tracing with stable isotopes, and genetic code expansion have enabled the identification and structural characterization of novel post-translational modifications—including histone lactylation, serotonylation, and dopaminylation—that directly link cellular metabolism to epigenetic regulation (Zhang et al., 2019; Farrelly et al., 2019).

### 1.2 Scope and Organization

This document examines five research frontiers, selected on the basis of three criteria: (i) each represents a genuine open frontier with abundant publishable questions; (ii) each has a strong funding trajectory and the potential for high-impact discoveries; and (iii) each has become tractable only within the 2020–2026 period due to the convergence of the tools described above. All five are distinct from one another and from the topic of whole-body biological reprogramming.

The five frontiers are:

1. **Structural enzymology of LINE-1 retrotransposons** (Section 2)
2. **AI prediction of protein conformational ensembles and dynamics** (Section 3)
3. **Cryo-EM structural biology of functional RNAs** (Section 4)
4. **Metabolite-derived histone modifications and the lactylation frontier** (Section 5)
5. **Liquid-to-solid transitions in biomolecular condensates and disease** (Section 6)

For each frontier, we present the foundational discoveries with full citation context, derive the relevant biophysical and mathematical frameworks, evaluate the critical open questions, and assess the experimental strategies most likely to yield transformative results. Section 7 synthesizes the connections among these five directions and evaluates their collective significance for the future of structural and molecular biology.

### 1.3 Fundamental Principles: From the Central Dogma to Structural Mechanism

The central dogma of molecular biology, as articulated by Crick (1958, 1970), describes the directional flow of sequence information: DNA → RNA → Protein. This framework, while foundational, describes only the informational transfer of nucleotide and amino acid sequences. The functional behavior of biological macromolecules—their catalytic activity, binding specificity, allosteric regulation, and participation in higher-order assemblies—is determined by their three-dimensional structures and, critically, by the conformational dynamics through which they sample multiple structural states.

The thermodynamic stability of a folded protein is governed by the free energy difference between the native and unfolded states:

$$\Delta G_{fold} = \Delta H_{fold} - T\Delta S_{fold}$$

where $\Delta H_{fold}$ reflects the enthalpic contributions of hydrogen bonds, van der Waals contacts, and electrostatic interactions within the folded state, and $\Delta S_{fold}$ captures the conformational entropy loss upon folding. For a typical globular protein, $\Delta G_{fold} \approx -5$ to $-15$ kcal/mol—a remarkably small margin of stability that permits the conformational fluctuations essential for function (Privalov and Gill, 1988).

The relationship between sequence, structure, and function constitutes the foundational paradigm of structural biology. Each of the five frontiers examined in this document extends this paradigm in a distinct direction: LINE-1 enzymology reveals the structural basis of genome rewriting by endogenous retroelements; conformational ensemble prediction seeks to capture the full thermodynamic distribution of protein states from sequence alone; RNA structural biology extends the structure-function paradigm to the second major class of biological polymers; metabolite-derived modifications reveal a direct structural link between cellular metabolism and chromatin regulation; and condensate biology reveals how the material properties of protein-RNA assemblies—liquid, gel, or solid—determine the boundary between function and disease.

---

## 2. Structural Enzymology of LINE-1 Retrotransposons

### 2.1 Biological Significance: LINE-1 as a Genomic Architect

Long Interspersed Nuclear Element-1 (LINE-1, or L1) retrotransposons constitute approximately 17% of the human genome by mass, and L1-derived sequences—including processed pseudogenes, Alu elements (which parasitize the L1 machinery), and SVA elements—account for approximately one-third of the total genomic sequence (Lander et al., 2001; de Koning et al., 2011). LINE-1 elements are the only autonomously active transposable elements in the modern human genome, encoding the complete enzymatic machinery required for their own retrotransposition through a "copy-and-paste" mechanism termed target-primed reverse transcription (TPRT).

The biological significance of LINE-1 extends far beyond its role as a "selfish genetic element." L1 retrotransposition is implicated in:

- **Somatic mosaicism and cancer genomics.** De novo L1 insertions occur in approximately 1 in 20 live births (Kazazian et al., 1988; Ewing and Kazazian, 2010), and somatic retrotransposition is a hallmark of epithelial cancers, with tumor-specific insertions identified in colorectal, lung, prostate, and ovarian carcinomas (Tubio et al., 2014; Rodriguez-Martin et al., 2020). The Pan-Cancer Analysis of Whole Genomes (PCAWG) consortium identified 19,166 somatic L1 insertions across 2,954 cancer genomes (Rodriguez-Martin et al., 2020), establishing L1 as a major source of oncogenic structural variation.

- **Aging-associated sterile inflammation.** Cytoplasmic accumulation of L1 cDNA in senescent cells activates the cGAS-STING innate immune sensing pathway, triggering type I interferon production and chronic sterile inflammation (De Cecco et al., 2019). This L1-cGAS-STING axis represents a direct molecular link between transposon biology and the chronic low-grade inflammation ("inflammaging") that characterizes organismal aging.

- **Neuronal diversity.** L1 retrotransposition occurs at elevated frequency in neural progenitor cells, generating somatic mosaicism in the developing brain that may contribute to neuronal diversity and individuality (Muotri et al., 2005; Coufal et al., 2009).

### 2.2 The L1 Retrotransposition Machinery: ORF1p and ORF2p

A full-length human L1 element (L1Hs) is approximately 6 kilobases and encodes two open reading frames:

**ORF1p** is a ~40 kDa RNA-binding protein that forms homotrimers through a coiled-coil domain and possesses nucleic acid chaperone activity. The crystal structure of the ORF1p trimer was determined by Khazina et al. (2011), revealing the coiled-coil trimerization interface and the C-terminal domain (CTD) responsible for RNA binding. ORF1p coats the L1 mRNA to form the ribonucleoprotein particle (RNP) that is the functional unit of retrotransposition.

**ORF2p** is a ~150 kDa multidomain enzyme that encodes both an N-terminal apurinic/apyrimidinic endonuclease (EN) domain and a central reverse transcriptase (RT) domain—the two catalytic activities required for TPRT. Despite its centrality to genome biology, the structure of full-length ORF2p remained unknown until 2024, owing to the extreme difficulty of producing soluble, active recombinant protein and the conformational heterogeneity of the multi-domain architecture.

### 2.3 The 2024 Structural Breakthrough: Atomic-Resolution ORF2p Structures

Two landmark companion papers published in Nature in February 2024 simultaneously solved this decades-old problem:

**Baldwin, van de Plassche et al. (Nature 626: 194–206, 2024)** from Jef Boeke's laboratory at NYU Langone Health determined X-ray crystallographic and cryo-EM structures of the ORF2p core, spanning the EN domain, RT domain, and two previously unrecognized folded domains termed the "wrist" and "tower" domains. The tower domain makes extensive contacts with the RNA template and is essential for processivity. The structure revealed that ORF2p adopts a closed, ring-like architecture in which the EN and RT active sites are positioned on opposite faces of the enzyme, connected by a flexible linker that enables sequential catalytic steps during TPRT.

**Thawani, Ariza, Nogales & Collins (Nature 626: 186–193, 2024)** from UC Berkeley captured cryo-EM structures of full-length ORF2p bound to template RNA during cDNA synthesis initiation, resolving five distinct domains: EN, RT, wrist, tower, and a C-terminal cysteine-rich domain (CRD). This study revealed how the poly(A) tract at the 3' end of L1 mRNA is specifically recognized by a positively charged channel formed between the tower and CRD domains—a structural feature that explains the strong preference of L1 for poly(A)-tailed substrates.

### 2.4 The TPRT Mechanism: From Structure to Catalytic Cycle

Target-primed reverse transcription is the mechanism by which LINE-1 copies itself into new genomic locations. The catalytic cycle, as inferred from the 2024–2025 structural data, proceeds through the following steps:

**Step 1: Target site recognition and first-strand nicking.** The ORF2p EN domain, a member of the APE1 family of apurinic/apyrimidinic endonucleases, recognizes and cleaves the bottom strand of a degenerate consensus target sequence (5'-TTTT/AA-3') in genomic DNA, generating a free 3'-OH at the nick site.

**Step 2: Target-primed reverse transcription.** The free 3'-OH generated by the EN nick serves as the primer for reverse transcription of the L1 mRNA template by the ORF2p RT domain. The poly(A) tail of the L1 mRNA anneals to the T-rich sequence at the target site, positioning the template for cDNA synthesis.

**Step 3: Second-strand cleavage and synthesis.** The top strand of the target site is cleaved (the mechanism and responsible enzyme remain structurally uncharacterized), and second-strand DNA synthesis generates the target site duplication (TSD) flanking the new insertion.

In 2025, Ghanim et al. (Science, 2025) provided a transformative advance by solving four cryo-EM structures of the complete TPRT complex, capturing LINE-1 in the act of genome insertion for the first time. These structures revealed the spatial relationship between the EN domain engaged with the target DNA, the RT domain synthesizing cDNA from the RNA template, and the structural rearrangements that coordinate the transition between endonuclease and reverse transcriptase activities.

### 2.5 Mathematical Framework: Kinetics of Retrotransposition and Host Suppression

The dynamics of L1 retrotransposition within a cellular genome can be modeled as a stochastic birth-death process. Let $N(t)$ denote the number of retrotransposition-competent L1 copies at time $t$. The rate of new insertions depends on the copy number, expression level, and the efficacy of host suppression mechanisms:

$$\frac{dN}{dt} = r \cdot N \cdot f_{expr}(N) \cdot [1 - s_{host}(N)] - \mu \cdot N$$

where $r$ is the intrinsic retrotransposition rate per active element per cell division, $f_{expr}(N)$ is a function describing the expression probability of each element (which decreases with increasing copy number due to epigenetic silencing by the KRAB-ZFP/KAP1/SETDB1 pathway), $s_{host}(N)$ represents the aggregate host suppression efficiency (including APOBEC3-mediated cytidine deamination, piRNA-directed silencing, and DNA methylation), and $\mu$ is the rate of inactivation by truncation, inversion, or point mutation.

For the modern human genome, $N \approx 80–100$ retrotransposition-competent L1Hs elements (Brouha et al., 2003), with the majority of retrotransposition activity driven by a small number of highly active "hot" L1 elements. The retrotransposition rate in the human germline has been estimated at $r_{eff} \approx 1/20$ to $1/270$ births (Kazazian et al., 1988; Ewing and Kazazian, 2010), implying that host suppression mechanisms reduce the intrinsic rate by several orders of magnitude. The equilibrium between retrotransposition and host suppression can be formalized as a steady-state condition. This equilibrium is dynamically maintained: too little host suppression leads to genomic instability and cancer; too much suppression would eliminate the retrotransposition that has, over evolutionary time, contributed essential regulatory sequences, including approximately 25% of human promoter elements (Faulkner et al., 2009).

### 2.6 In Situ Structural Biology: Cryo-ET of Retrotransposon Particles

A complementary methodological advance came from in situ structural biology. A Cell paper (March 2025) used cryo-focused ion beam (cryo-FIB) milling combined with cryo-electron tomography (cryo-ET) to image retrotransposon virus-like particles (VLPs) within intact *Drosophila* tissue at 7.7 Å resolution. This represented the first visualization of a retrotransposon RNP in its native cellular context, revealing a packed arrangement of the capsid-like ORF1 protein shell surrounding the RNA-ORF2p catalytic core. The VLP architecture places constraints on models of how the L1 RNP accesses genomic DNA: the particle must either disassemble or undergo a conformational rearrangement to expose the ORF2p catalytic domains to their chromosomal substrate.

### 2.7 Open Questions and Research Directions

The foundational structural work is now in place, but major questions remain:

1. **Complete L1 RNP structure.** The full ribonucleoprotein particle—including ORF1p trimers in complex with ORF2p and the full-length L1 mRNA—has never been structurally resolved. Reconstitution of this complex from purified components and cryo-EM structure determination would reveal the stoichiometry, architecture, and functional organization of the retrotransposition machinery.

2. **Second-strand synthesis mechanism.** The enzyme responsible for second-strand cleavage and the mechanism of insertion resolution remain unknown. Whether ORF2p itself performs second-strand cleavage or whether host DNA repair factors (PCNA, FEN1, ligases) are recruited is a critical open question.

3. **Host factor recruitment.** AlphaFold-predicted interactions between ORF2p and host factors (PCNA, PABPC1, DNA repair machinery) have not been experimentally validated structurally. Cryo-EM of ORF2p–host factor complexes would illuminate the interface between the retrotransposon machinery and the host DNA repair system.

4. **Structure-guided ORF2p inhibitor design.** The 2024 structures enable rational design of selective ORF2p inhibitors targeting the unique structural features of the L1 RT active site—distinct from repurposed HIV RT inhibitors like lamivudine. The tower domain's RNA-binding channel and the EN domain's catalytic site are druggable surfaces with no current therapeutics.

5. **Somatic retrotransposition in aging.** Quantifying the rate of somatic L1 insertions as a function of age and tissue type, and correlating these rates with cGAS-STING activation and inflammaging markers, would establish the causal relationship between L1 activity and age-associated pathology.

---

## 3. AI Prediction of Protein Conformational Ensembles and Dynamics

### 3.1 The Completion of the Static Structure Prediction Problem

The protein structure prediction problem—determining the three-dimensional coordinates of a protein's atoms from its amino acid sequence alone—was one of the grand challenges of computational biology for over 50 years. AlphaFold2 (Jumper et al., 2021) solved this problem for single-chain proteins with static structures, achieving a median Global Distance Test (GDT-TS) score exceeding 92 at CASP14, comparable to the accuracy of experimental methods. This achievement was recognized with the 2024 Nobel Prize in Chemistry.

AlphaFold3 (Abramson et al., 2024) extended this to multi-chain protein complexes, protein–nucleic acid complexes, and protein–ligand systems using a diffusion-based generative architecture. IsoDDE (Isomorphic Labs, 2026) further advanced the state of the art, more than doubling AlphaFold3's accuracy on the most challenging out-of-distribution benchmarks (the [0–20] similarity bin of the Runs N' Poses benchmark) and achieving a 2.3× improvement in antibody-antigen interface prediction accuracy.

With static structure prediction effectively solved, the field's central unsolved problem has shifted to a far more challenging target: **the prediction of Boltzmann-weighted conformational ensembles from sequence alone.**

### 3.2 The Conformational Ensemble Problem: Thermodynamic Foundation

Proteins are not static objects. They exist as thermodynamic ensembles of conformational states, with the population of each state $i$ determined by the Boltzmann distribution:

$$p_i = \frac{e^{-G_i / k_B T}}{Z}$$

where $G_i$ is the free energy of state $i$, $k_B$ is the Boltzmann constant, $T$ is the absolute temperature, and $Z = \sum_j e^{-G_j / k_B T}$ is the partition function. The functional behavior of a protein—its catalytic rate, allosteric response, binding affinity, and susceptibility to post-translational regulation—is determined not by any single structure but by the full ensemble $\{p_i, \mathbf{x}_i\}$ of populated states and their interconversion kinetics.

The free energy landscape of a protein can be decomposed as:

$$G(\mathbf{x}) = H(\mathbf{x}) - TS(\mathbf{x})$$

where $H(\mathbf{x})$ includes bonded interactions (bond stretches, angle bends, torsions), non-bonded interactions (van der Waals, electrostatics, hydrogen bonds), and solvent effects (hydrophobic effect, solvent entropy), and $S(\mathbf{x})$ captures the conformational entropy at configuration $\mathbf{x}$.

For a protein of $N$ residues, the conformational space has approximately $3N$ relevant degrees of freedom (backbone and sidechain torsion angles), yielding a free energy landscape of dimension $\sim 3N$. For a typical 300-residue protein, this landscape has $\sim 900$ relevant dimensions—a space that cannot be exhaustively sampled by molecular dynamics simulation on any foreseeable timescale. This is the fundamental computational challenge that makes conformational ensemble prediction far harder than static structure prediction.

### 3.3 The AlphaFold-Cluster Approach: Coevolutionary Signal for Alternative States

Wayment-Steele, Kern et al. (Nature 625: 832–839, 2024) demonstrated that AlphaFold2 can be coaxed into predicting alternative conformational states by clustering the input multiple sequence alignment (MSA) and running predictions on each cluster independently (the "AF-Cluster" method). The key insight is that different evolutionary lineages within a protein family may have accumulated substitutions that stabilize different conformational states, and that MSA clustering can separate these lineages.

The method was validated on the metamorphic protein KaiB, which adopts two completely different folds (a thioredoxin-like fold and a novel fold) depending on its functional context. AF-Cluster successfully predicted both folds from the same input sequence, and the predictions were validated against experimental NMR data.

However, a critical challenge to this approach emerged from Schafer et al. (Nature, 2025), who demonstrated that AF-Cluster may exploit memorization of the training set rather than genuine coevolutionary signal. The authors showed that AF-Cluster's performance degrades sharply when training-set homologs are removed, raising the fundamental question: **do current AI models learn the physics of protein conformational change, or do they memorize correlations between sequence features and structures deposited in the PDB?**

### 3.4 Systematic Failures: Fold-Switching Proteins and Intrinsically Disordered Regions

Two classes of proteins expose the fundamental limitations of current AI structure prediction:

**Fold-switching proteins.** These are proteins that adopt completely different secondary and tertiary structures under different conditions (e.g., different binding partners, pH, redox state, or oligomeric context). Chakravarty and Porter (Protein Science, 2022) systematically catalogued fold-switching proteins and showed that AlphaFold2 fails to predict the alternative fold in virtually all cases, instead predicting only the dominant PDB conformation. This failure is expected from a model trained to minimize the distance to a single deposited structure, but it highlights the inadequacy of single-structure prediction for understanding proteins that function through conformational switching.

**Intrinsically disordered proteins (IDPs) and regions (IDRs).** Approximately 30% of the human proteome is predicted to contain significant disordered regions (Dunker et al., 2001; Ward et al., 2004), and many functional proteins (e.g., p53 transactivation domain, α-synuclein, tau) are entirely or predominantly disordered. These proteins do not adopt a single well-defined structure but instead sample a broad ensemble of rapidly interconverting conformations. AlphaFold2 and AlphaFold3 produce low-confidence predictions for disordered regions (reflected in low pLDDT scores), effectively acknowledging their inability to model these systems. No current AI method generates physically meaningful conformational ensembles for IDPs.

### 3.5 Mathematical Framework: The Conformational Free Energy Landscape

The conformational ensemble of a protein can be rigorously described by the potential of mean force (PMF) over a reduced set of collective variables (CVs) $\boldsymbol{\xi} = (\xi_1, \xi_2, \ldots, \xi_d)$:

$$F(\boldsymbol{\xi}) = -k_B T \ln P(\boldsymbol{\xi}) + C$$

where $P(\boldsymbol{\xi})$ is the equilibrium probability density over the CVs. The challenge is twofold: (i) identifying the appropriate CVs that capture the functionally relevant motions, and (ii) sampling the PMF with sufficient accuracy to resolve the populations and interconversion barriers of the relevant states.

For a two-state protein with conformations A and B separated by a transition state ‡, the interconversion rate is given by transition state theory:

$$k_{A \to B} = \frac{k_B T}{h} \cdot \kappa \cdot e^{-\Delta G^{\ddagger}_{A \to B} / k_B T}$$

where $h$ is Planck's constant, $\kappa$ is the transmission coefficient (accounting for recrossing and friction), and $\Delta G^{\ddagger}_{A \to B} = G^{\ddagger} - G_A$ is the activation free energy. For typical allosteric transitions, $\Delta G^{\ddagger} \approx 10–20$ kcal/mol, corresponding to millisecond-to-second timescales—far beyond the reach of conventional molecular dynamics.

### 3.6 Emerging Computational Approaches

Several complementary approaches are under development:

**Boltzmann generators (Noé et al., 2019).** These are normalizing flow models trained to sample from the Boltzmann distribution of a molecular system. The model learns an invertible transformation from a simple prior distribution (e.g., Gaussian) to the Boltzmann distribution in Cartesian coordinates. The loss function enforces:

$$\mathcal{L} = D_{KL}\left(q_\theta(\mathbf{x}) \| p_{Boltz}(\mathbf{x})\right) = \mathbb{E}_{q_\theta}\left[\ln q_\theta(\mathbf{x}) - \ln p_{Boltz}(\mathbf{x})\right]$$

where $q_\theta$ is the learned distribution and $p_{Boltz}(\mathbf{x}) \propto e^{-U(\mathbf{x})/k_BT}$ is the Boltzmann distribution with energy function $U(\mathbf{x})$. When converged, the generator produces independent, uncorrelated samples from the equilibrium ensemble—circumventing the time-correlation problem of molecular dynamics.

**Flow matching and diffusion models.** Building on the success of diffusion-based architectures in AlphaFold3, several groups are developing generative models that learn to sample from conformational distributions conditioned on sequence. These approaches use score-based generative modeling:

$$\nabla_{\mathbf{x}} \ln p(\mathbf{x}) \approx s_\theta(\mathbf{x}, t)$$

where the score network $s_\theta$ is trained to approximate the gradient of the log-probability density at each noise level $t$. By running a reverse-time stochastic differential equation guided by the learned score, the model generates new conformational samples.

**idpGAN (Ramaswamy et al., Nature Communications 14: 774, 2023).** A generative adversarial network specifically designed for intrinsically disordered protein ensembles, trained on molecular dynamics trajectories to produce conformational distributions consistent with experimental NMR and SAXS data.

**AlphaMissense and mutation effects (Cheng et al., Science 381, 2023).** While AlphaMissense successfully classifies missense variants as pathogenic or benign, it operates on a classification level and does not predict how mutations shift conformational equilibria. Extending pathogenicity prediction to quantitative $\Delta\Delta G$ and conformational ensemble perturbation remains an open challenge.

### 3.7 Integrating AI Predictions with Experimental Data

A particularly promising direction is the integration of AI-generated structural hypotheses with heterogeneous experimental data:

**CryoDRGN (Zhong et al., 2021).** This neural network-based approach models continuous conformational heterogeneity from cryo-EM particle images, representing each particle as a point in a learned latent space. The combination of AlphaFold-predicted starting structures with cryoDRGN-derived continuous heterogeneity maps enables the construction of conformational movies from single-particle cryo-EM data.

**NMR chemical shift-guided refinement.** NMR backbone chemical shifts (${}^{13}C_\alpha$, ${}^{13}C_\beta$, ${}^{13}C'$, ${}^{15}N$, ${}^{1}H_N$) are exquisitely sensitive to local conformation and can be predicted from structure with sub-ppm accuracy by programs like SPARTA+ and ShiftX2. AI-generated ensembles can be validated and refined by computing predicted chemical shifts and comparing them to experimental values, using the $\chi^2$ metric:

$$\chi^2 = \sum_{i,\alpha} \frac{(\delta_{i,\alpha}^{pred} - \delta_{i,\alpha}^{exp})^2}{\sigma_\alpha^2}$$

where $\delta_{i,\alpha}$ is the chemical shift of nucleus $\alpha$ at residue $i$ and $\sigma_\alpha$ is the expected prediction error. This approach provides an orthogonal validation metric that is independent of the PDB training data.

### 3.8 Open Questions

1. Can any AI method reliably predict allosteric transition states and kinetic rates from sequence alone?
2. Can generative models produce physically meaningful ensembles for the ~30% of the human proteome that is intrinsically disordered?
3. How can the memorization problem identified by Schafer et al. be addressed—what architectural or training innovations would enable genuine learning of conformational physics?
4. Can AI predictions of mutation effects on conformational landscapes be validated experimentally and extended to quantitative $\Delta\Delta G$ prediction?
5. What is the minimal set of experimental data (NMR, cryo-EM, SAXS) needed to calibrate and validate AI-generated conformational ensembles?

---

## 4. Cryo-EM Structural Biology of Functional RNAs

### 4.1 The RNA Structure Problem

RNA molecules perform a remarkable diversity of biological functions—catalysis (ribozymes), gene regulation (riboswitches, microRNAs), structural scaffolding (rRNA, lncRNAs), and information transfer (mRNA)—yet the structural biology of RNA has lagged far behind that of proteins. As of 2020, fewer than 200 unique RNA structures had been deposited in the PDB at resolutions better than 4 Å, compared to over 150,000 protein structures at equivalent resolution.

This disparity has structural and physicochemical origins. RNA molecules are flexible, sampling multiple conformational states that frustrate crystallization. RNA lacks the diversity of hydrophobic amino acid side chains that drive protein folding into compact, well-defined cores; instead, RNA structure is stabilized primarily by base pairing (Watson-Crick and non-canonical), base stacking, metal ion coordination (especially Mg²⁺), and tertiary interactions (A-minor motifs, ribose zippers, pseudoknots). The result is that most functional RNAs adopt structures with fewer long-range contacts and greater conformational heterogeneity than typical protein structures.

For cryo-EM, RNA poses additional challenges: small size (most riboswitches are 50–200 nucleotides, corresponding to molecular weights of 15–65 kDa—below the typical resolution limit of single-particle cryo-EM), lack of recognizable features for particle alignment, and a tendency to adopt preferred orientations on the cryo-EM grid.

### 4.2 The Scaffold-Based Cryo-EM Breakthrough

The breakthrough that enabled high-resolution cryo-EM of small, flexible RNAs was the development of scaffold strategies that embed the RNA of interest within a larger, rigid RNA framework that provides mass, distinct features for alignment, and protection from conformational collapse.

**The Ribosolve pipeline (Kappel, Zhang, Su et al., Nature Methods 17: 699–707, 2020)** combined cryo-EM with M2-seq biochemical mapping and Rosetta molecular modeling to determine 11 RNA-only structures in a single study, including the SAM-IV riboswitch and glycine riboswitch. The pipeline uses a three-step approach: (1) cryo-EM density map determination at moderate resolution (4–7 Å); (2) M2-seq chemical mapping to constrain secondary structure; (3) Rosetta-based modeling and refinement into the cryo-EM density.

**The Tetrahymena group I ribozyme (Su et al., Nature 596: 603–607, 2021)** represented the landmark achievement of RNA cryo-EM. The complete 414-nucleotide ribozyme was solved at 3.1 Å resolution—the first high-resolution structure of the first ribozyme ever discovered (Cech, 1982). The structure revealed two previously unforeseen tertiary interactions and substrate-induced conformational changes that explain the catalytic mechanism of self-splicing.

**The group II intron scaffold (Langeberg, Kieft et al., Nature Communications, 2025)** achieved 2.5 Å resolution structures of a TPP riboswitch and a novel bacterial non-coding RNA (raiA), using a group II intron RNA as a scaffold to provide mass and alignment features. This study directly visualized ligand-induced conformational switching in the TPP riboswitch, capturing both the apo (ligand-free) and holo (TPP-bound) states at near-atomic resolution.

### 4.3 The RNA Free Energy Landscape

The thermodynamics of RNA folding can be described using the nearest-neighbor model, which decomposes the folding free energy into contributions from individual base pairs and their stacking interactions:

$$\Delta G_{fold}^{RNA} = \sum_{i} \Delta G_{stack}(bp_i, bp_{i+1}) + \sum_{j} \Delta G_{loop}(loop_j) + \sum_{k} \Delta G_{tertiary}(contact_k)$$

where $\Delta G_{stack}$ represents the stacking free energy of consecutive base pairs (the dominant stabilizing force in RNA, contributing $\approx -1.5$ to $-3.5$ kcal/mol per stacking interaction), $\Delta G_{loop}$ represents the entropic penalty for loop formation, and $\Delta G_{tertiary}$ captures the contribution of long-range tertiary contacts.

For a riboswitch that switches between two conformations (ON and OFF) in response to ligand binding, the thermodynamic framework is:

$$K_{switch} = \frac{[RNA_{OFF}]}{[RNA_{ON}]} = e^{-\Delta G_{switch}/k_BT}$$

and the ligand response curve follows:

$$f_{OFF}([L]) = \frac{1}{1 + \frac{1}{K_{switch}} \cdot \frac{K_d}{[L]}}$$

where $[L]$ is the ligand concentration and $K_d$ is the dissociation constant for ligand binding to the ON state. The sharpness of the switching response is determined by the ratio $\Delta G_{switch} / k_B T$, and cooperative ligand binding (as in tandem riboswitch architectures) can produce ultrasensitive responses.

### 4.4 AI Meets RNA Structure Prediction

AlphaFold3 represents the first AI system capable of predicting RNA three-dimensional structures with meaningful accuracy, though performance on RNA remains substantially below the level achieved for proteins. The key challenges are:

- **Sparse training data.** The PDB contains approximately 5,000 RNA-containing structures compared to >200,000 protein structures, providing a much smaller training set.
- **Non-canonical base pairs.** RNA structures contain a rich repertoire of non-Watson-Crick base pairs (Hoogsteen, sugar-edge, wobble) that are critical for tertiary structure but poorly represented in training data.
- **Metal ion coordination.** Mg²⁺ ions are essential for RNA folding and catalysis, but their positions are often ambiguous in experimental structures and challenging for AI models to predict.
- **Conformational dynamics.** Many functional RNAs adopt multiple conformations (e.g., riboswitch ligand-free and ligand-bound states), and current models predict only a single structure.

The combination of AI-predicted RNA structures with experimental cryo-EM density maps offers a hybrid approach: AI provides an initial structural hypothesis, which is then refined against experimental density to produce a high-confidence model. This approach is particularly valuable for large, multi-domain RNA structures where neither method alone achieves atomic resolution.

### 4.5 Riboswitch Structural Diversity and Drug Targeting

Riboswitches are structured RNA elements typically located in the 5' untranslated regions of bacterial mRNAs that bind small molecule metabolites (e.g., TPP, SAM, FMN, lysine, glycine, adenine, guanine) and regulate gene expression through conformational switching. Over 40 classes of riboswitches have been experimentally validated, and computational analysis by Narunsky and Breaker (Nucleic Acids Research 52: 5152–5165, 2024) identified at least 44 additional riboswitch candidates, suggesting that the true diversity of riboswitch-mediated regulation is far larger than currently appreciated.

Riboswitches are absent from mammalian genomes but widespread in pathogenic bacteria, making them attractive antibiotic targets. Structural knowledge of the ligand-binding pocket enables the design of riboswitch-targeting antibiotics that exploit the conformational switch:

$$IC_{50} \propto K_d^{analog} \cdot \frac{1}{k_{switch}}$$

where $K_d^{analog}$ is the binding affinity of the antibiotic analog for the riboswitch pocket and $k_{switch}$ is the rate of the conformational change induced by binding. Tight-binding analogs that trap the riboswitch in its OFF state (gene repression) would selectively kill bacteria that depend on the regulated gene product.

### 4.6 Non-Canonical RNA Structures: R-loops and G-Quadruplexes

Beyond riboswitches and ribozymes, two non-canonical RNA structures have emerged as critical players in genome stability:

**R-loops** are three-stranded nucleic acid structures consisting of an RNA:DNA hybrid and a displaced single-stranded DNA. They form co-transcriptionally when nascent RNA anneals to the template DNA strand, and they regulate processes including class-switch recombination, transcription termination, and DNA repair. Aberrant R-loop accumulation is associated with genome instability and neurodegenerative disease. Sato et al. (Science, 2025) provided new structural insights into how R-loops interact with the DNA repair machinery.

**G-quadruplexes (G4s)** are four-stranded structures formed by guanine-rich sequences through Hoogsteen base pairing around a central cation channel. RNA G4s (rG4s) form in mRNAs and non-coding RNAs, regulating translation, splicing, and telomere biology. Wulfridge and Sarma (Nature Cell Biology 26: 1025–1036, 2024) demonstrated that R-loops and G4s co-occur at specific genomic loci and cooperatively regulate DNA repair, adding a new dimension to the structural biology of non-canonical nucleic acid structures.

### 4.7 Open Questions

1. **Systematic structure determination of disease-relevant RNA elements.** Viral RNA regulatory elements (frameshifting pseudoknots, IRES elements), bacterial riboswitch variants, and human lncRNA functional domains remain largely uncharacterized structurally.
2. **Long non-coding RNA architecture.** The functional domains of lncRNAs that interact with chromatin-modifying complexes (e.g., XIST, HOTAIR, NEAT1) have never been structurally resolved at high resolution.
3. **AI-experimental hybrid methods.** Development of integrative frameworks that combine AlphaFold3 RNA predictions with cryo-EM density maps and chemical probing data.
4. **Riboswitch-based antibiotics.** Structure-guided design of ligand analogs targeting essential bacterial riboswitches.
5. **Co-transcriptional RNA folding.** How do RNA structures form during transcription, and how does the kinetics of folding determine the functional conformation?

---

## 5. Metabolite-Derived Histone Modifications and the Lactylation Frontier

### 5.1 The Expanding Universe of Histone Post-Translational Modifications

The nucleosome—the fundamental unit of eukaryotic chromatin—consists of 147 base pairs of DNA wrapped 1.67 turns around an octamer of histone proteins (two copies each of H2A, H2B, H3, and H4). The histone tails, which extend from the nucleosome core, serve as substrates for an extraordinarily diverse array of post-translational modifications (PTMs) that collectively regulate chromatin accessibility, gene expression, DNA repair, and cell fate specification.

The classical histone code, as conceptualized by Strahl and Allis (2000) and refined by Jenuwein and Allis (2001), initially focused on acetylation (lysine, by histone acetyltransferases/HATs), methylation (lysine and arginine, by histone methyltransferases/HMTs), phosphorylation (serine and threonine, by kinases), and ubiquitination (lysine, by E3 ligases). Each modification was understood to recruit specific "reader" domains—bromodomains for acetylation, chromodomains and PHD fingers for methylation, 14-3-3 domains for phosphorylation—that translate the modification pattern into a transcriptional output.

The period 2019–2025 revealed that the histone code is far more complex than initially conceived. A new class of metabolite-derived modifications—in which intermediary metabolites of cellular metabolism are covalently attached to histone residues—has established a direct mechanistic link between metabolic state and epigenetic regulation. These modifications include:

- **Lactylation (Kla)**: L-lactate attached to lysine residues (Zhang et al., 2019)
- **Serotonylation (H3Q5ser)**: Serotonin attached to glutamine residues (Farrelly et al., 2019)
- **Succinylation (Ksucc)**: Succinate attached to lysine residues
- **Crotonylation (Kcr)**: Crotonate attached to lysine residues (Tan et al., 2011)
- **β-Hydroxybutyrylation (Kbhb)**: β-Hydroxybutyrate attached to lysine residues (Xie et al., 2016)
- **Benzoylation (Kbz)**: Benzoate attached to lysine residues
- **Dopaminylation (H3Q5dop)**: Dopamine attached to glutamine residues (Lepack et al., 2020)

### 5.2 The Discovery of Histone Lactylation

Zhang, Zhao et al. (Nature 574: 575–580, 2019) identified 28 histone lysine lactylation (Kla) sites on core histones in human and mouse cells. Key findings included:

1. Lactylation is stimulated by conditions that elevate intracellular lactate—hypoxia, the Warburg effect in cancer cells, and bacterial lipopolysaccharide (LPS) challenge in macrophages.
2. Lactylation and acetylation have distinct temporal dynamics: following LPS stimulation of macrophages, acetylation increases rapidly (peaking at 6–12 hours) and drives pro-inflammatory gene expression (M1 polarization), while lactylation increases with a delay (peaking at 16–24 hours) and drives anti-inflammatory, homeostatic gene expression (M2-like polarization).
3. H3K18la is enriched at the promoters of homeostatic genes including *Arg1*, establishing lactylation as a transcriptional activator with functional specificity distinct from acetylation.

The thermodynamic rationale for metabolite-derived histone modifications can be formalized as follows. The modification reaction requires an activated metabolite donor (e.g., lactyl-CoA for enzymatic lactylation):

$$\Delta G_{rxn} = \Delta G_f^{products} - \Delta G_f^{reactants}$$

For the lactylation reaction catalyzed by a histone acyltransferase:

$$\text{Histone-Lys-NH}_2 + \text{Lactyl-CoA} \xrightarrow{KAT} \text{Histone-Lys-NH-CO-CHOH-CH}_3 + \text{CoA-SH}$$

The equilibrium is driven toward modification by the high-energy thioester bond of lactyl-CoA ($\Delta G_{hydrolysis} \approx -31.4$ kJ/mol), analogous to the energetics of acetyl-CoA-dependent acetylation.

### 5.3 The Enzymology of Lactylation: Two Mechanistically Distinct Pathways

The period 2024–2025 brought the mechanistic breakthroughs that transformed lactylation from an observation into a structurally tractable field:

**The CoA-dependent pathway (Zhu, Lu et al., Cell Metabolism 37: 361–376, 2025).** This study identified ACSS2 (Acyl-CoA Synthetase Short-chain family member 2) as the first mammalian lactyl-CoA synthetase—the enzyme that converts free L-lactate to lactyl-CoA, the activated donor for enzymatic lactylation:

$$\text{L-Lactate} + \text{CoA-SH} + \text{ATP} \xrightarrow{ACSS2} \text{L-Lactyl-CoA} + \text{AMP} + \text{PP}_i$$

Critically, the study solved the co-crystal structure of KAT2A (also known as GCN5) bound to lactyl-CoA at 2.37 Å resolution—the first structural view of any lactyltransferase with its acyl-CoA substrate. The structure revealed that lactyl-CoA is accommodated in the KAT2A active site through a hydrogen bond between the lactyl hydroxyl group and an asparagine residue that is not utilized during acetylation, providing a structural basis for the enzyme's dual acetyl/lactyl transferase activity.

Furthermore, the study demonstrated that EGFR-ERK signaling phosphorylates ACSS2, promoting its nuclear translocation and thereby coupling growth factor signaling to lactylation. In glioblastoma, this EGFR→ERK→ACSS2→KAT2A→H3K14la/H3K18la axis drives immune evasion through upregulation of immunosuppressive gene programs.

**The non-CoA-dependent pathway (Zong et al., Cell 187: 2375–2392, 2024).** In a parallel and entirely unexpected discovery, Zong et al. identified AARS1—alanyl-tRNA synthetase, an essential enzyme of the translation machinery—as responsible for approximately 80% of global cellular lactylation through a mechanism that does not require CoA intermediates:

$$\text{AARS1} + \text{L-Lactate} + \text{ATP} \xrightarrow{} \text{AARS1-Lactyl-AMP} \xrightarrow{transfer} \text{Histone-Kla} + \text{AMP}$$

AARS1 senses intracellular lactate concentration, activates it via an ATP-dependent adenylation reaction (analogous to aminoacyl-tRNA synthesis), and transfers the lactyl group directly to histone lysine residues. This moonlighting function was entirely unexpected—aminoacyl-tRNA synthetases were not previously known to modify histones—and it establishes a direct link between the translational apparatus and the epigenetic code.

### 5.4 Structural Analysis: Comparing the Two Lactylation Pathways

The coexistence of two mechanistically distinct lactylation pathways raises the question of their relative contributions and functional specialization. A quantitative comparison:

| Property | CoA-dependent (ACSS2/KAT2A) | Non-CoA (AARS1) |
|---|---|---|
| Fraction of cellular lactylation | ~20% | ~80% |
| Activated intermediate | Lactyl-CoA | Lactyl-AMP |
| ATP cost per modification | 2 ATP equivalents | 1 ATP |
| Subcellular regulation | ACSS2 nuclear translocation | Constitutive nuclear presence |
| Signaling input | EGFR-ERK phosphorylation | Lactate concentration sensing |
| Structural data | KAT2A:Lactyl-CoA co-crystal (2.37 Å) | None (AARS1 lactyltransferase structure unknown) |

The relative contributions of these pathways likely vary by tissue, metabolic state, and disease context. In tumors with high glycolytic flux (Warburg effect), the AARS1 pathway may dominate due to elevated lactate concentrations, while in tissues with active growth factor signaling, the ACSS2/KAT2A pathway may be more important.

### 5.5 The Reader Problem: Does a Dedicated Lactylation Reader Exist?

The functional readout of histone modifications depends on "reader" proteins that specifically recognize the modified residue and recruit downstream effectors. For acetylation, bromodomains serve this function; for methylation, chromodomains, Tudor domains, and PHD fingers. **No dedicated lactylation reader domain has been identified.**

This represents one of the most important open questions in the field. The structural difference between acetyl-lysine and lactyl-lysine is the addition of a hydroxyl group:

- Acetyl-lysine: Lys-NH-CO-CH₃
- Lactyl-lysine: Lys-NH-CO-CHOH-CH₃

The hydroxyl group provides a potential hydrogen bond donor/acceptor that could, in principle, be recognized by a modified bromodomain or a novel reader domain. Candidate identification approaches include:

1. **Chemical proteomics.** Synthesis of histone peptides bearing site-specific Kla marks, followed by affinity pulldown and mass spectrometry-based identification of binding partners.
2. **Structural screening.** Systematic co-crystallization of bromodomain family members with Kla-containing peptides to identify any that bind lactyl-lysine with specificity over acetyl-lysine.
3. **Bioinformatic prediction.** AlphaFold-based modeling of bromodomain:Kla peptide complexes to predict binding modes and identify candidate readers computationally.

### 5.6 Serotonylation and the Neurotransmitter-Chromatin Axis

Farrelly, Muir, Maze et al. (Nature 567: 535–539, 2019) discovered that serotonin (5-hydroxytryptamine, 5-HT) is covalently attached to histone H3 at glutamine 5 (H3Q5ser) by tissue transglutaminase 2 (TGM2). The reaction mechanism involves:

$$\text{H3-Q5-CONH}_2 + \text{5-HT-NH}_2 \xrightarrow{TGM2} \text{H3-Q5-CO-NH-5-HT} + \text{NH}_3$$

H3Q5ser co-occurs with H3K4me3 in serotonergic neurons and potentiates gene expression at loci critical for serotonin neurotransmission. This modification establishes that neurotransmitters—molecules classically associated with synaptic signaling—can directly write the epigenetic code, creating a molecular feedback loop between neuronal activity and gene expression.

The subsequent discovery of histone dopaminylation (H3Q5dop) by Lepack et al. (Science 368: 645–649, 2020) extended this principle to the dopaminergic system, demonstrating that cocaine exposure increases H3Q5dop at reward-related gene loci in the ventral tegmental area—providing a direct chromatin-level mechanism for drug-induced transcriptional plasticity.

### 5.7 Phase Separation and Histone Modification: The Condensate Connection

Gallego et al. (Nature 579: 592–597, 2020) demonstrated that phase separation directs the ubiquitination of gene-body nucleosomes through a core-shell condensate mechanism, linking histone PTM biology directly to the biomolecular condensate field discussed in Section 6. In this system, the ubiquitin ligase RING1B concentrates within transcriptional condensates and preferentially modifies nucleosomes within the condensate interior, creating a spatial coupling between condensate formation and chromatin modification.

This condensate-PTM connection has profound implications: if the material properties of nuclear condensates determine which histone modifications are deposited and where, then the interplay between metabolic state (which determines modification supply), condensate physics (which determines spatial organization), and reader/writer/eraser enzymology (which determines modification dynamics) constitutes a three-way regulatory circuit of extraordinary complexity.

### 5.8 Open Questions

1. **Lactylation reader identification.** Is there a dedicated reader domain for Kla, or is lactylation read by promiscuous bromodomains with altered affinity?
2. **AARS1 lactyltransferase structure.** The structure of AARS1 in its lactyltransferase mode (bound to histone substrate and lactyl-AMP) is unknown and would reveal the structural basis of this unexpected moonlighting function.
3. **L- vs. D-lactylation.** Distinguishing enzymatic L-lactylation from non-enzymatic D-lactylation (via the lactoylglutathione pathway) requires chemical tools (e.g., stereospecific antibodies, chiral mass spectrometry reporters) that are still under development.
4. **Therapeutic targeting.** Structure-guided design of inhibitors targeting the ACSS2-KAT2A interaction or the AARS1 lactyltransferase activity for cancer immunotherapy.
5. **Metabolite-to-PTM flux quantification.** Using ¹³C-labeled metabolite tracing to quantify the kinetic flux from metabolite pool to histone modification at specific genomic loci.

---

## 6. Liquid-to-Solid Transitions in Biomolecular Condensates and Disease

### 6.1 Biomolecular Condensates: Phase Separation as an Organizing Principle

Biomolecular condensates are membrane-less compartments formed through liquid-liquid phase separation (LLPS) of proteins and nucleic acids. They concentrate specific macromolecules and catalytic activities while excluding others, functioning as reaction crucibles, signaling hubs, and organizational platforms. Major cellular condensates include:

- **Nucleolus**: ribosome biogenesis (NPM1, FBL, rRNA)
- **Stress granules**: mRNA triage during cellular stress (G3BP1, TIA-1)
- **P-bodies**: mRNA decay and storage (DCP1/2, EDC3)
- **Cajal bodies**: snRNP maturation (coilin, SMN)
- **Transcriptional condensates**: gene activation (Mediator, RNA Pol II CTD)

The physical basis of condensate formation is liquid-liquid phase separation, governed by the Flory-Huggins theory of polymer solutions. For a binary solution of macromolecule (volume fraction $\phi$) and solvent, the free energy of mixing per lattice site is:

$$\frac{\Delta G_{mix}}{k_BT} = \frac{\phi}{N} \ln \phi + (1-\phi) \ln(1-\phi) + \chi \phi (1-\phi)$$

where $N$ is the degree of polymerization and $\chi$ is the Flory-Huggins interaction parameter capturing the net interaction energy between polymer segments and solvent. Phase separation occurs when $\chi > \chi_c = \frac{1}{2}\left(1 + \frac{1}{\sqrt{N}}\right)^2$, at which point the solution demixes into a dense phase (the condensate) and a dilute phase (the surrounding cytoplasm or nucleoplasm).

For intrinsically disordered proteins (IDPs) with multivalent interaction motifs—the primary drivers of biological phase separation—the interaction parameter $\chi$ depends on the amino acid composition, charge patterning, and aromatic content of the IDP. The Cation-π, π-π stacking, and electrostatic interactions between charged residues and aromatic amino acids (particularly tyrosine and phenylalanine in low-complexity domains) are the dominant driving forces.

### 6.2 The Liquid-to-Solid Transition: Physical Framework

The specific frontier most relevant to structural biology is the **liquid-to-solid transition (LST)**: the process by which functional liquid condensates transform into pathological solid aggregates. This transition drives the protein aggregation diseases that collectively represent the largest unmet medical need in neurology—ALS (TDP-43, FUS, SOD1), frontotemporal dementia (tau, TDP-43), Alzheimer's disease (tau, Aβ), and Parkinson's disease (α-synuclein).

Jawerth et al. (Science 370: 1317–1323, 2020) established the quantitative physical framework by showing that protein condensates behave as **aging Maxwell fluids**. A Maxwell fluid is characterized by a viscosity $\eta$ and an elastic modulus $E$, with a relaxation time $\tau_R = \eta / E$. Jawerth et al. demonstrated that the relaxation time of protein condensates increases exponentially with time:

$$\tau_R(t) = \tau_0 \exp\left(\frac{t}{\tau_{aging}}\right)$$

where $\tau_0$ is the initial relaxation time and $\tau_{aging}$ is the aging time constant. This exponential aging drives the condensate from a liquid state ($\tau_R \ll t_{observation}$, droplets are round and fuse rapidly) to a solid-like state ($\tau_R \gg t_{observation}$, droplets are irregular and do not fuse).

The physical origin of this aging is the progressive formation of intermolecular β-sheet contacts within the condensate, which act as cross-links that arrest the dynamics of the polymer network. The cross-link density $\rho_{cross}(t)$ grows with time as:

$$\frac{d\rho_{cross}}{dt} = k_{form} \cdot c_{local}^2 \cdot (1 - \rho_{cross} / \rho_{max}) - k_{break} \cdot \rho_{cross}$$

where $k_{form}$ is the rate of β-sheet contact formation, $c_{local}$ is the local protein concentration within the condensate (which is much higher than the bulk concentration), $\rho_{max}$ is the maximum cross-link density, and $k_{break}$ is the rate of cross-link dissolution. The condensate interior provides both the high local concentration ($c_{local} \sim 100-300$ mg/mL) and the conformational confinement that accelerate cross-link formation relative to the dilute phase.

### 6.3 Atomic-Level View of the LST: NMR of FUS Droplet Aging

Emmanouilidis et al. (Nature Chemical Biology 20: 1044–1052, 2024) achieved the first atomic-level structural view of the liquid-to-solid transition in a disease-relevant RNA-binding protein. Using solution-state and solid-state NMR spectroscopy applied to FUS (Fused in Sarcoma) protein condensates, they detected β-sheet structures forming at the surface of FUS droplets during aging.

Key findings:

1. Fresh FUS condensates exhibit NMR spectra consistent with a disordered, dynamic interior—the low-complexity domain (LCD) of FUS remains largely disordered even within the condensed phase.
2. Over hours to days, new NMR peaks emerge that are characteristic of β-sheet secondary structure, specifically at the **surface** of the condensate rather than uniformly throughout.
3. ALS-causing FUS mutations (e.g., G156E, R244C) accelerate the rate of β-sheet formation at the condensate surface, providing a direct structural mechanism linking genetic mutations to disease pathology.
4. The surface-nucleated β-sheet formation is consistent with a heterogeneous nucleation model in which the liquid-air (or liquid-cytoplasm) interface provides a catalytic surface for amyloid-like cross-β structure formation.

### 6.4 Mathematical Framework: Nucleation Theory of the LST

The kinetics of the liquid-to-solid transition can be described by classical nucleation theory adapted for intracondensate β-sheet formation. The free energy barrier for nucleation of a β-sheet aggregate of $n$ monomers within the condensate is:

$$\Delta G_{nuc}(n) = -n \cdot \Delta g_{bulk} + n^{2/3} \cdot \gamma \cdot A_0$$

where $\Delta g_{bulk} < 0$ is the free energy gain per monomer incorporated into the β-sheet (reflecting the favorable hydrogen bonding and van der Waals contacts in the cross-β structure), $\gamma$ is the surface tension of the β-sheet nucleus, and $A_0$ is a geometric factor relating the surface area to the number of monomers.

The critical nucleus size $n^*$ is obtained by setting $d\Delta G_{nuc}/dn = 0$:

$$n^* = \left(\frac{2 \gamma A_0}{3 \Delta g_{bulk}}\right)^3$$

and the nucleation rate is:

$$J = J_0 \exp\left(-\frac{\Delta G^*}{k_BT}\right)$$

where $\Delta G^* = \Delta G_{nuc}(n^*)$ is the barrier height. The observation that β-sheet formation initiates at the condensate surface is explained by the reduction of $\gamma$ at the interface: the liquid-air interface provides a pre-organized surface where protein chains are partially constrained, lowering the effective surface tension and reducing the nucleation barrier.

### 6.5 Disease-Relevant Condensate Proteins

**TDP-43 (TAR DNA-binding protein 43).** TDP-43 is a nuclear RNA-binding protein whose cytoplasmic aggregation is the pathological hallmark of ALS and frontotemporal lobar degeneration (FTLD). In its native state, TDP-43 partitions into nuclear condensates involved in RNA splicing and processing. Disease mutations in the low-complexity C-terminal domain (e.g., A315T, M337V, Q331K) increase the protein's propensity for phase separation and accelerate the liquid-to-solid transition.

**Tau.** Tau is a microtubule-associated protein that forms neurofibrillary tangles in Alzheimer's disease and other tauopathies. Tau undergoes LLPS in the presence of RNA or crowding agents, and phosphorylation at disease-relevant sites (e.g., AT8 epitope: pS202/pT205) promotes phase separation and subsequent gelation.

**α-Synuclein.** The protein whose aggregation drives Parkinson's disease undergoes LLPS under conditions of elevated concentration, and Lewy body formation may proceed through a condensate intermediate.

**FUS.** ALS-causing mutations in the FUS low-complexity domain accelerate the liquid-to-solid transition, as demonstrated by the NMR studies of Emmanouilidis et al. (2024).

### 6.6 Condensate-Modifying Therapeutics (c-mods)

The therapeutic targeting of biomolecular condensates represents a new pharmacological paradigm. Mitrea et al. (Nature Reviews Drug Discovery 21: 841–862, 2022) formalized the "condensate-modifying therapeutics" (c-mods) framework, defining three classes of intervention:

1. **Condensate dissolvers**: Small molecules that disrupt the multivalent interactions driving phase separation (e.g., 1,6-hexanediol, though this is a non-specific tool compound).
2. **Condensate hardeners**: Molecules that stabilize the solid state, trapping pathogens or aberrant assemblies. Risso-Ballester et al. (Nature 595: 596–599, 2021) demonstrated that a small molecule (SLR14) that hardens RSV viral condensates blocks viral replication in vivo—the first proof-of-concept for a c-mod therapy.
3. **Partition modulators**: Molecules that alter the partitioning of client proteins or drugs into specific condensates. Klein et al. (Science 368: 1386–1392, 2020) showed that anticancer drugs like cisplatin preferentially partition into transcriptional condensates (Mediator condensates), fundamentally altering our understanding of drug pharmacokinetics.

The partition coefficient of a drug into a condensate is:

$$K_{partition} = \frac{c_{drug}^{condensate}}{c_{drug}^{dilute}} = \exp\left(-\frac{\Delta G_{transfer}}{k_BT}\right)$$

where $\Delta G_{transfer}$ is the free energy of transferring the drug from the dilute phase to the condensate interior. Drugs with favorable interactions with condensate components (π-π stacking with aromatic residues, electrostatic interactions with charged IDRs) will have $K_{partition} \gg 1$ and concentrate within condensates. This condensate-mediated drug concentration creates an effective local drug concentration far higher than the bulk concentration, with profound implications for drug efficacy, toxicity, and resistance.

### 6.7 Single-Molecule and In-Cell Structural Methods

**Single-molecule FRET (smFRET).** Galvanetto et al. (Nature 619: 876–883, 2023) used single-molecule FRET within condensates to measure sub-microsecond dynamics, revealing that the condensate interior is far more dynamic than expected. The measured reconfiguration times ($\tau_r \sim 50-200$ ns) for disordered proteins within condensates are only 2-3× slower than in dilute solution, challenging the assumption that the dense phase represents a "frozen" or gel-like state. This extreme dynamism coexists with the slow aging process described by Jawerth et al., suggesting that the liquid-to-solid transition involves a gradual increase in the fraction of time spent in cross-linked states rather than a sudden arrest of all dynamics.

**Cryo-electron tomography (cryo-ET).** Cryo-FIB milling combined with cryo-ET enables the visualization of condensate ultrastructure within intact cells at nanometer resolution. This approach can resolve the spatial organization of condensate components—protein, RNA, and nucleic acid—and detect the onset of structural ordering (fibrillar or crystalline regions) that marks the liquid-to-solid transition.

### 6.8 Open Questions

1. **Atomic-resolution LST intermediates.** What are the precise intermediate structures during the liquid-to-solid transition for disease proteins TDP-43, tau, and α-synuclein? Can NMR and cryo-ET be combined to resolve condensate nanoarchitecture in situ at atomic resolution?
2. **PTM switches.** How do specific post-translational modifications (phosphorylation, methylation, acetylation, ubiquitination) act as molecular switches that trigger or prevent pathological solidification?
3. **RNA determinants.** How do RNA sequence, structure, and modifications determine condensate material properties? Building on Roden and Gladfelter (Nature Reviews Molecular Cell Biology 22: 183–195, 2021), the role of RNA as both a structural scaffold and a regulator of condensate viscosity is poorly understood.
4. **Selective c-mods.** Can engineered RNA aptamers or small molecules selectively reverse pathological phase transitions without disrupting functional condensates?
5. **Quantitative condensate biophysics.** What are the measurable biophysical parameters (viscosity, surface tension, elastic modulus, mesh size) that distinguish functional from pathological condensates, and can these be used as diagnostic biomarkers?

---

## 7. Synthesis: How Five Frontiers Connect

### 7.1 The Unifying Thread: The Resolution Revolution

These five research directions share a unifying principle: the revolution in structural tools—cryo-EM, AI prediction, NMR, chemical biology—has opened biological questions that were previously inaccessible at the molecular level. The connections are specific and mechanistic:

**LINE-1 enzymology** became tractable because cryo-EM reached the resolution needed for flexible, multi-domain enzymes that resisted crystallization for decades. The ORF2p structures solved in 2024 required both the direct electron detectors and the advanced particle classification algorithms developed during the resolution revolution.

**Conformational ensemble prediction** became the next grand challenge precisely because static structure prediction was solved. The AlphaFold revolution defined the boundary of what AI can currently achieve—and exposed the conformational ensemble problem as the frontier that lies beyond.

**RNA structural biology** emerged as a tractable field because scaffold strategies overcame the size and flexibility barriers that defeated earlier crystallographic and cryo-EM approaches. The Ribosolve pipeline and group II intron scaffolds represent methodological innovations specifically enabled by the improved signal-to-noise ratio of modern cryo-EM.

**Metabolite-derived modifications** became a structural biology problem once writer enzymes were identified and crystallized. The ACSS2/KAT2A co-crystal structure was determined by conventional X-ray crystallography, but the broader characterization of the lactylation machinery—including the AARS1 pathway and the search for reader domains—requires the integrative structural biology approaches (cryo-EM, HDX-MS, cross-linking mass spectrometry) that have matured in the current era.

**Condensate pathology** crossed from cell biology into structural biology when NMR and cryo-ET achieved the sensitivity to detect structural transitions within the heterogeneous, dynamic condensed phases that had previously been "black boxes" to structural methods.

### 7.2 Cross-Frontier Connections

Beyond their shared dependence on the resolution revolution, these five frontiers exhibit specific mechanistic connections:

- **LINE-1 and condensates.** LINE-1 ORF1p forms condensate-like granules in the cytoplasm, and recent evidence suggests that phase separation plays a role in organizing the L1 RNP for retrotransposition. The material properties of these L1 granules—liquid vs. solid—may determine whether the RNP is competent for nuclear import and genome insertion.

- **Lactylation and condensates.** The metabolic regulation of histone lactylation (Section 5) intersects with condensate biology (Section 6) through the observation that transcriptional condensates concentrate histone-modifying enzymes at specific genomic loci. Whether lactylation is preferentially deposited at loci within transcriptional condensates, and whether condensate material properties influence lactylation dynamics, are open questions.

- **RNA structure and condensates.** RNA is a critical determinant of condensate material properties: the sequence, structure, and modifications of RNA molecules within a condensate influence its viscosity, dynamics, and propensity for solidification. The structural biology of RNA within condensates (Section 4) is directly relevant to understanding the RNA-dependent aspects of the LST (Section 6).

- **AI prediction and all four experimental frontiers.** AlphaFold3 and its successors provide starting structural models for LINE-1 complexes, RNA structures, histone-modifying enzyme complexes, and condensate protein conformations. The integration of AI-predicted structures with experimental cryo-EM density maps is becoming standard practice across all four experimental frontiers.

### 7.3 The Mathematical Unity of Structural Biology

A deeper mathematical unity connects these five frontiers through the shared framework of free energy landscapes and statistical mechanics:

1. **Protein folding** (Section 3): The Boltzmann distribution over conformational states, with barriers determined by the potential of mean force.
2. **RNA folding** (Section 4): The nearest-neighbor free energy model, with conformational switching governed by ligand-binding thermodynamics.
3. **Enzymatic catalysis** (Sections 2, 5): Transition state theory, with catalytic rates determined by activation free energies.
4. **Phase separation** (Section 6): Flory-Huggins theory, with the liquid-to-solid transition governed by nucleation thermodynamics.

In each case, the structural biology question reduces to characterizing the free energy landscape—its minima (stable states), saddle points (transition states), and the kinetic pathways connecting them. The revolution in structural tools has given us the ability to directly observe the molecular configurations corresponding to these thermodynamic states, transforming abstract energy landscapes into atomically detailed structural movies.

### 7.4 Future Prospects

The convergence of cryo-EM, AI structure prediction, NMR spectroscopy, and chemical biology has created a unique moment in the history of structural and molecular biology. For the first time, it is possible to:

1. Determine the structures of biological machines that were previously inaccessible (L1 RNP, riboswitch conformational states, condensate intermediates).
2. Predict structures computationally with experimental accuracy, enabling hypothesis-driven experimental design at a pace that was previously impossible.
3. Visualize biological processes in situ—within intact cells and tissues—at nanometer to atomic resolution using cryo-ET and correlative methods.
4. Link molecular structure directly to cellular metabolism through the discovery of metabolite-derived modifications that write the epigenetic code.

Each of the five frontiers examined in this document sits at the intersection of these capabilities, and each offers abundant opportunities for transformative discoveries over the next decade. The structural enzymology of LINE-1 will yield new therapeutic targets for cancer and aging. Conformational ensemble prediction will revolutionize drug design by enabling the targeting of dynamic, allosteric, and disordered protein states. RNA structural biology will unlock new classes of antibiotics targeting essential bacterial riboswitches. The lactylation frontier will reveal how cellular metabolism instructs gene expression at the chromatin level. And condensate biology will provide the structural basis for understanding—and ultimately treating—the neurodegenerative diseases that represent the greatest unmet medical challenge of the 21st century.

---

## References

[1] Abramson, J., et al. (2024). Accurate structure prediction of biomolecular interactions with AlphaFold 3. *Nature* 630, 493–500.

[2] Baldwin, E.T., van de Plassche, M., et al. (2024). Structures of LINE-1 ORF2 protein. *Nature* 626, 194–206.

[3] Brouha, B., et al. (2003). Hot L1s account for the bulk of retrotransposition in the human population. *Proc. Natl. Acad. Sci. USA* 100, 5280–5285.

[4] Cech, T.R. (1982). Self-splicing of group I introns. *Annu. Rev. Biochem.* 59, 543–568.

[5] Chakravarty, D., and Porter, L.L. (2022). AlphaFold2 fails to predict protein fold switching. *Protein Science* 31, e4353.

[6] Cheng, J., et al. (2023). Accurate proteome-wide missense variant effect prediction with AlphaMissense. *Science* 381, eadg7492.

[7] Coufal, N.G., et al. (2009). L1 retrotransposition in human neural progenitor cells. *Nature* 460, 1127–1131.

[8] Crick, F.H.C. (1958). On protein synthesis. *Symp. Soc. Exp. Biol.* 12, 138–163.

[9] Crick, F.H.C. (1970). Central dogma of molecular biology. *Nature* 227, 561–563.

[10] De Cecco, M., et al. (2019). L1 drives IFN in senescent cells and promotes age-associated inflammation. *Nature* 566, 73–78.

[11] de Koning, A.P.J., et al. (2011). Repetitive elements may comprise over two-thirds of the human genome. *PLoS Genet.* 7, e1002384.

[12] Dunker, A.K., et al. (2001). Intrinsically disordered protein. *J. Mol. Graph. Model.* 19, 26–59.

[13] Emmanouilidis, L., et al. (2024). NMR reveals surface β-sheet formation during FUS droplet aging. *Nat. Chem. Biol.* 20, 1044–1052.

[14] Ewing, A.D., and Kazazian, H.H. (2010). High-throughput sequencing reveals extensive variation in human-specific L1 content in individual human genomes. *Genome Res.* 20, 1262–1270.

[15] Farrelly, L.A., et al. (2019). Histone serotonylation is a permissive modification that enhances TFIID binding to H3K4me3. *Nature* 567, 535–539.

[16] Faulkner, G.J., et al. (2009). The regulated retrotransposon transcriptome of mammalian cells. *Nat. Genet.* 41, 563–571.

[17] Gallego, L.D., et al. (2020). Phase separation directs ubiquitination of gene-body nucleosomes. *Nature* 579, 592–597.

[18] Galvanetto, N., et al. (2023). Extreme dynamics in a biomolecular condensate. *Nature* 619, 876–883.

[19] Ghanim, G.E., et al. (2025). Structural basis of target-primed reverse transcription by LINE-1. *Science* (2025).

[20] Isomorphic Labs Team (2026). Accurate predictions of novel biomolecular interactions with IsoDDE. Preprint.

[21] Jawerth, L., et al. (2020). Protein condensates as aging Maxwell fluids. *Science* 370, 1317–1323.

[22] Jenuwein, T., and Allis, C.D. (2001). Translating the histone code. *Science* 293, 1074–1080.

[23] Jumper, J., et al. (2021). Highly accurate protein structure prediction with AlphaFold. *Nature* 596, 583–589.

[24] Kappel, K., Zhang, K., Su, Z., et al. (2020). Accelerated cryo-EM-guided determination of RNA structures. *Nat. Methods* 17, 699–707.

[25] Kazazian, H.H., et al. (1988). Haemophilia A resulting from de novo insertion of L1 sequences represents a novel mechanism for mutation in man. *Nature* 332, 164–166.

[26] Kendrew, J.C., et al. (1958). A three-dimensional model of the myoglobin molecule obtained by X-ray analysis. *Nature* 181, 662–666.

[27] Khazina, E., et al. (2011). Trimeric structure and flexibility of the L1ORF1 protein in human L1 retrotransposition. *Nat. Struct. Mol. Biol.* 18, 1006–1014.

[28] Klein, I.A., et al. (2020). Partitioning of cancer therapeutics in nuclear condensates. *Science* 368, 1386–1392.

[29] Kühlbrandt, W. (2014). The resolution revolution. *Science* 343, 1443–1444.

[30] Lander, E.S., et al. (2001). Initial sequencing and analysis of the human genome. *Nature* 409, 860–921.

[31] Langeberg, C.J., Kieft, J.S., et al. (2025). Scaffold-based cryo-EM structures of riboswitches. *Nat. Commun.* (2025).

[32] Lepack, A.E., et al. (2020). Dopaminylation of histone H3 in ventral tegmental area regulates cocaine seeking. *Science* 368, 645–649.

[33] Li, X., et al. (2013). Electron counting and beam-induced motion correction enable near-atomic-resolution single-particle cryo-EM. *Nat. Methods* 10, 584–590.

[34] McRae, E.K.S., et al. (2024). Cryo-EM structure of a triplet polymerase ribozyme. *Proc. Natl. Acad. Sci. USA* 121, e2313332121.

[35] Mitrea, D.M., et al. (2022). Modulating biomolecular condensates: a novel approach to drug discovery. *Nat. Rev. Drug Discov.* 21, 841–862.

[36] Muotri, A.R., et al. (2005). Somatic mosaicism in neuronal precursor cells mediated by L1 retrotransposition. *Nature* 435, 903–910.

[37] Nakane, T., et al. (2020). Single-particle cryo-EM at atomic resolution. *Nature* 587, 152–156.

[38] Narunsky, A., and Breaker, R.R. (2024). Computational identification of novel riboswitch candidates. *Nucleic Acids Res.* 52, 5152–5165.

[39] Noé, F., et al. (2019). Boltzmann generators: sampling equilibrium states of many-body systems with deep learning. *Science* 365, eaaw1147.

[40] Perutz, M.F., et al. (1960). Structure of haemoglobin. *Nature* 185, 416–422.

[41] Privalov, P.L., and Gill, S.J. (1988). Stability of protein structure and hydrophobic interaction. *Adv. Protein Chem.* 39, 191–234.

[42] Punjani, A., et al. (2017). cryoSPARC: algorithms for rapid unsupervised cryo-EM structure determination. *Nat. Methods* 14, 290–296.

[43] Ramaswamy, V.K., et al. (2023). Deep learning generates disordered protein ensembles. *Nat. Commun.* 14, 774.

[44] Risso-Ballester, J., et al. (2021). A condensate-hardening drug blocks RSV replication in vivo. *Nature* 595, 596–599.

[45] Roden, C., and Gladfelter, A.S. (2021). RNA contributions to the form and function of biomolecular condensates. *Nat. Rev. Mol. Cell Biol.* 22, 183–195.

[46] Rodriguez-Martin, B., et al. (2020). Pan-cancer analysis of whole genomes identifies driver rearrangements promoted by LINE-1 retrotransposition. *Nat. Genet.* 52, 306–319.

[47] Sato, K., et al. (2025). R-loop structures and genome stability. *Science* (2025).

[48] Schafer, J.W., et al. (2025). AF-Cluster exploits training set memorization. *Nature* (2025).

[49] Scheres, S.H.W. (2012). RELION: implementation of a Bayesian approach to cryo-EM structure determination. *J. Struct. Biol.* 180, 519–530.

[50] Strahl, B.D., and Allis, C.D. (2000). The language of covalent histone modifications. *Nature* 403, 41–45.

[51] Su, Z., et al. (2021). Cryo-EM structure of the Tetrahymena group I ribozyme at 3.1 Å. *Nature* 596, 603–607.

[52] Tan, M., et al. (2011). Identification of 67 histone marks and histone lysine crotonylation as a new type of histone modification. *Cell* 146, 1016–1028.

[53] Thawani, A., Ariza, A.J.F., Nogales, E., and Collins, K. (2024). Cryo-EM structure of LINE-1 ORF2p during cDNA synthesis. *Nature* 626, 186–193.

[54] Tubio, J.M.C., et al. (2014). Extensive transduction of nonrepetitive DNA mediated by L1 retrotransposition in cancer genomes. *Science* 345, 1251343.

[55] Ward, J.J., et al. (2004). Prediction and functional analysis of native disorder in proteins from the three kingdoms of life. *J. Mol. Biol.* 337, 635–645.

[56] Wayment-Steele, H.K., Kern, D., et al. (2024). Predicting multiple conformations via sequence clustering and AlphaFold2. *Nature* 625, 832–839.

[57] Wulfridge, P., and Sarma, K. (2024). R-loops and G-quadruplexes in genome stability. *Nat. Cell Biol.* 26, 1025–1036.

[58] Xie, Z., et al. (2016). Metabolic regulation of gene expression by histone lysine β-hydroxybutyrylation. *Mol. Cell* 62, 194–206.

[59] Yip, K.M., et al. (2020). Atomic-resolution protein structure determination by cryo-EM. *Nature* 587, 157–161.

[60] Zhang, D., Tang, Z., Huang, H., Zhou, G., Cui, C., Weng, Y., Liu, W., Kim, S., Lee, S., Perez-Neut, M., et al. (2019). Metabolic regulation of gene expression by histone lactylation. *Nature* 574, 575–580.

[61] Zheng, S.Q., et al. (2017). MotionCor2: anisotropic correction of beam-induced motion for improved cryo-electron microscopy. *Nat. Methods* 14, 331–332.

[62] Zhong, E.D., et al. (2021). CryoDRGN: reconstruction of heterogeneous cryo-EM structures using neural networks. *Nat. Methods* 18, 176–185.

[63] Zhu, Z., Lu, Z., et al. (2025). ACSS2 is a lactyl-CoA synthetase and KAT2A is a lactyltransferase. *Cell Metab.* 37, 361–376.

[64] Zong, Z., et al. (2024). AARS1 senses and transfers lactate to histones. *Cell* 187, 2375–2392.

[65] Alberti, S., and Hyman, A.A. (2021). Biomolecular condensates at the nexus of cellular stress, protein aggregation disease, and ageing. *Nat. Rev. Mol. Cell Biol.* 22, 196–213.

[66] Mittag, T., and Pappu, R.V. (2022). A conceptual framework for understanding phase separation and addressing open questions and challenges. *Mol. Cell* 82, 2201–2214.

[67] Narunsky, A., and Breaker, R.R. (2024). Identification of novel riboswitch candidates. *Nucleic Acids Res.* 52, 5152–5165.

[68] Brixi, G., et al. (2025). Genome modeling and design across all domains of life with Evo 2. BioRxiv, 2025-02.
