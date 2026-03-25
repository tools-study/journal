# Towards Sequence-Specific Binding Proteins

---

## Abstract

The ability to direct proteins to arbitrary DNA sequences underpins the entire edifice of genetic medicine — from gene knockout and base editing to epigenome silencing and large-scale genome rearrangement. Five decades of research have yielded four major classes of programmable DNA-binding scaffolds — Cys2His2 zinc fingers, transcription activator-like effector (TALE) repeats, LAGLIDADG meganucleases, and CRISPR-associated proteins — each with distinct biophysical trade-offs in specificity, size, deliverability, and durability. The past three years have witnessed transformative advances across every platform: deep-learning models trained on billions of zinc finger-DNA interactions now design arrays for any genomic target; TALE-based epigenome editors achieve year-long gene silencing from a single dose in primates; engineered meganucleases have entered first-in-human clinical trials for hepatitis B; and, most remarkably, the first computationally designed DNA-binding proteins with programmable sequence specificity have been created entirely from first principles using RFdiffusion and LigandMPNN. Simultaneously, ultracompact ancestral nucleases (IscB, Fanzor, Cas12f) are being engineered to clinical-grade efficiency, and bridge RNA recombinases now mediate megabase-scale genome rearrangements. This review provides a comprehensive, platform-by-platform analysis of these advances, introduces novel mathematical frameworks quantifying the biophysical principles governing protein-DNA recognition, and identifies the open questions that will define the next generation of programmable DNA-binding therapeutics.

---

## 1. Introduction

### 1.1 The Central Problem: Programmable Sequence-Specific DNA Recognition

Every therapeutic modality in genetic medicine — gene disruption, correction, insertion, silencing, activation, and rearrangement — requires a molecular agent capable of recognizing a unique DNA sequence within the 3.2-gigabase human genome and ignoring the remaining ~6.4 billion nucleotides. This seemingly simple requirement imposes extraordinary biophysical constraints: a protein or ribonucleoprotein must encode sufficient information to specify at minimum ~16 base pairs (4^16 ≈ 4.3 × 10^9 unique sequences) to achieve single-site genomic specificity, and it must do so with a thermodynamic discrimination ratio high enough to ensure negligible off-target binding under physiological conditions (Jinek et al., 2012).

The history of programmable DNA recognition traces a remarkable arc. The first programmable platform, the Cys2His2 zinc finger, was structurally characterized in 1991, revealing a modular ~30-residue ββα fold that recognizes three contiguous base pairs through direct amino acid–base contacts in the DNA major groove. The discovery of the TALE repeat code in 2009 introduced a simpler recognition grammar — one 34-residue repeat per base pair, with specificity determined by two "repeat-variable diresidues" (RVDs) at positions 12 and 13 (Deng et al., 2012). The 2012 demonstration that the bacterial CRISPR-Cas9 system could be reprogrammed with a single guide RNA to cleave any genomic target revolutionized the field by shifting the information encoding from protein sequence to a short RNA molecule (Jinek et al., 2012; Cong et al., 2013). And in 2025, the first proteins designed entirely from computational first principles achieved sequence-specific DNA binding, demonstrating that the protein-DNA recognition problem can be solved without recourse to any natural scaffold (Glasscock et al., 2025).

### 1.2 Why Protein-Based DNA Recognition Remains Critical

Despite the transformative impact of CRISPR-Cas systems, protein-based DNA recognition retains irreplaceable advantages. Zinc finger and TALE domains are smaller than Cas proteins, enabling delivery within the 4.7 kb AAV packaging limit — particularly important for in vivo therapeutic applications. Protein-only systems avoid the immunogenicity concerns associated with bacterial Cas proteins and their guide RNAs. Critically, protein-based scaffolds are not constrained by protospacer adjacent motif (PAM) requirements that restrict the targetable sequence space of CRISPR nucleases. Furthermore, the durable epigenome editing revolution — achieving permanent gene silencing without DNA cleavage — has been pioneered almost entirely with zinc finger and TALE scaffolds fused to epigenetic effector domains (Cappelluti et al., 2024; Tremblay et al., 2025; Mao et al., 2025).

### 1.3 Scope and Organization

This review provides a comprehensive survey of all major platforms for programmable DNA recognition, organized by technology. Section 2 establishes the biophysical foundations of protein-DNA recognition. Sections 3–8 examine each platform in depth: zinc finger proteins (Section 3), TALE repeats (Section 4), meganucleases (Section 5), de novo computationally designed proteins (Section 6), ultracompact ancestral nucleases (Section 7), and bridge RNA recombinases (Section 8). Section 9 presents a cross-platform comparison, and Section 10 identifies open questions and future directions. Novel mathematical frameworks are introduced throughout to quantify the fundamental biophysical trade-offs governing programmable DNA recognition.

---

## 2. Foundations of Protein-DNA Recognition

### 2.1 Direct Readout: Base-Specific Contacts in the Major Groove

The major groove of B-form DNA exposes a unique pattern of hydrogen bond donors and acceptors for each of the four Watson-Crick base pairs, providing sufficient chemical information for sequence discrimination. The classical direct readout mechanism involves amino acid side chains that form hydrogen bonds with these exposed functional groups — arginine and asparagine contacting guanine's O6 and N7, glutamine contacting adenine's N6, and aspartate recognizing cytosine's N4 (Nishimasu et al., 2014). The helix-turn-helix (HTH) motif, the most ancient and widespread DNA-binding fold, positions its recognition helix within the major groove to make these contacts. Zinc finger C2H2 domains achieve specificity through three to four critical amino acid positions (−1, 2, 3, 6 relative to the recognition helix) that contact three base pairs per finger (Persikov & Singh, 2014). TALE repeats use an even simpler mechanism: the RVD at positions 12–13 of each 34-residue repeat forms one or two hydrogen bonds with a single base pair, with asparagine-isoleucine (NI) recognizing adenine, histidine-aspartate (HD) recognizing cytosine, asparagine-glycine (NG) recognizing thymine, and asparagine-asparagine (NN) recognizing guanine or adenine (Deng et al., 2012).

### 2.2 Indirect Readout: DNA Shape as a Specificity Determinant

Beyond direct base contacts, proteins exploit sequence-dependent variations in DNA structure — minor groove width, roll angle, propeller twist, and helical twist — to discriminate between sequences. A-T-rich regions narrow the minor groove and enhance the negative electrostatic potential, while G-C-rich regions widen it. Computational methods including DNAshape and its deep-learning successor Deep DNAshape have quantified these structural parameters on a genomic scale, revealing that sequence-dependent DNA shape contributes substantially to binding specificity for many transcription factor families (Zhou et al., 2013; Li et al., 2024). Recent thermodynamic analyses have demonstrated that the entropic contribution of DNA shape deformation to protein-DNA binding free energy is approximately 15-fold larger than the enthalpic contribution, with total deformation energies reaching ~8.28 kcal/mol during complex formation — a finding that fundamentally revises the classical enthalpic-dominance model of protein-DNA specificity (Mondal et al., 2024).

### 2.3 A Brief Note on Protein-DNA Structure Prediction

The computational prediction of protein-DNA complex structures remains an open challenge. While AlphaFold 3 introduced a unified diffusion-based architecture capable of predicting protein-nucleic acid complexes and achieved at least 50% improvement over prior specialized methods (Abramson et al., 2024), the CASP16 community-wide assessment revealed that no computational method achieved TM-scores above 0.8 for non-homologous nucleic acid structures, and protein-DNA complex prediction remained heavily dependent on template availability (Kretsch et al., 2026). The geometric deep-learning model DeepPBS represents a complementary approach, predicting DNA-binding specificity from protein-DNA structure using interpretable atomic-level importance scores validated by mutagenesis experiments (Mitra et al., 2024). The gap between protein structure prediction accuracy and protein-DNA interaction prediction accuracy remains a critical bottleneck constraining computational design efforts.

### 2.4 Novel Mathematical Framework: Free Energy Decomposition for Protein-DNA Specificity (F269)

The total binding free energy of a protein-DNA complex can be decomposed into contributions from direct readout, indirect readout, and nonspecific electrostatic interactions:

```math
\Delta G_{\text{total}} = \Delta G_{\text{direct}} + \Delta G_{\text{indirect}} + \Delta G_{\text{ns}}
```

where $\Delta G_{\text{direct}}$ encompasses base-specific hydrogen bonds and van der Waals contacts in the major groove (predominantly enthalpic), $\Delta G_{\text{indirect}}$ captures the free energy associated with sequence-dependent DNA deformation (predominantly entropic), and $\Delta G_{\text{ns}}$ represents nonspecific electrostatic attraction between the positively charged protein surface and the DNA phosphate backbone.

The **specificity ratio** $S$ — defined as the equilibrium discrimination between cognate and non-cognate DNA targets — can be derived from the difference in binding free energies:

```math
S = \frac{K_{d,\text{non-cognate}}}{K_{d,\text{cognate}}} = \exp\!\left(\frac{\Delta\Delta G_{\text{spec}}}{RT}\right)
```

where:

```math
\Delta\Delta G_{\text{spec}} = \Delta G_{\text{non-cognate}} - \Delta G_{\text{cognate}}
```

For a protein making $n$ independent sequence-specific contacts, each contributing an average discriminatory energy $\delta g$ per contact, the total specificity scales exponentially:

```math
S(n) = \exp\!\left(\frac{n \cdot \delta g}{RT}\right)
```

Empirically, $\delta g$ ranges from 0.5–2.0 kcal/mol per base pair for zinc fingers and TALEs, yielding specificity ratios of $S \approx 10^{1.5}$ to $10^{3}$ per contact at 37°C. For genome-wide uniqueness in the human genome ($S_{\text{required}} \geq 4^{16} \approx 4.3 \times 10^9$), a minimum of approximately $n_{\min} = \lceil RT \cdot \ln(3.2 \times 10^9) / \delta g \rceil$ specific contacts are needed — ranging from ~14 contacts at $\delta g = 1.0$ kcal/mol to ~7 contacts at $\delta g = 2.0$ kcal/mol. This framework explains why six-finger zinc finger arrays (18 bp) and 16–20 repeat TALE arrays are typically required for therapeutic applications: they provide sufficient cumulative specificity to uniquely address the human genome.

---

## 3. Zinc Finger Proteins: Machine Learning-Guided Design and the Epigenome Editing Renaissance

### 3.1 The Modular Recognition Code and Its Limitations

The Cys2His2 zinc finger is the most abundant DNA-binding domain in the human genome, with over 700 human proteins containing tandem arrays of these ~30-residue ββα modules (Persikov & Singh, 2014). Each finger coordinates a zinc ion through two cysteine and two histidine residues, stabilizing a compact fold that positions an α-helix in the DNA major groove to contact approximately three base pairs. The modular recognition hypothesis — that each finger's specificity can be independently engineered — motivated the first generation of zinc finger nuclease (ZFN) technology and led to early clinical applications including the first-ever genome editing trial in humans (Tebas et al., 2014).

However, the modular hypothesis oversimplifies the biophysics. Context-dependent interactions between adjacent fingers, synergistic contacts spanning finger boundaries, and target-site-dependent conformational effects mean that individual finger specificities are not truly independent. This "context problem" limited the reliability of early modular assembly approaches and motivated the development of selection-based methods that evolve multi-finger arrays as integrated units.

### 3.2 ZFDesign: A Universal Deep-Learning Model for Zinc Finger Engineering

The context problem was decisively addressed by Ichikawa et al. (2023), who developed ZFDesign, a universal deep-learning model trained on an unprecedented dataset of 49 billion protein-DNA interactions generated by bacterial one-hybrid (B1H) selections. The model uses a hierarchical transformer architecture that explicitly captures inter-finger cooperativity — the critical context dependence that confounded earlier approaches. ZFDesign can design zinc finger arrays targeting any genomic sequence, achieving experimental success rates substantially higher than modular assembly and rivaling or exceeding the best selection-based protocols. The model has been validated across diverse target sites and enables the rational reprogramming of human transcription factors to bind novel DNA sequences.

### 3.3 Deimmunized Zinc Fingers: Multi-Objective Machine Learning

A critical barrier to the therapeutic deployment of engineered zinc finger proteins is immunogenicity — novel amino acid combinations at finger-DNA interfaces may generate neoepitopes recognized by the adaptive immune system. Wolfsberg et al. (2025) addressed this challenge by combining three machine-learning algorithms in a multi-objective optimization framework: ZFDesign for DNA-binding specificity, MARIA for MHC-II antigen presentation prediction (immunogenicity), and ESM-IF1 for protein stability scoring. This approach produces zinc finger arrays that simultaneously bind their intended DNA target, minimize predicted immunogenic potential, and maintain thermodynamic stability — a multi-objective design paradigm that is likely to become standard for all protein-based DNA-binding therapeutics (Wolfsberg et al., 2025).

### 3.4 Zinc Finger-Based Epigenome Editing: Hit-and-Run Silencing

The most clinically advanced application of zinc finger DNA recognition is not nuclease-mediated gene disruption but epigenome editing — the targeted modification of chromatin marks to achieve durable gene silencing without introducing DNA double-strand breaks. Two landmark studies have demonstrated the therapeutic potential of this approach for PCSK9, the primary target for LDL cholesterol reduction.

Cappelluti et al. (2024) developed EvoETR, a zinc finger-based epigenetic editor combining engineered DNMT3A and DNMT3L methyltransferase domains fused to a zinc finger array targeting the PCSK9 promoter. A single intravenous dose of LNP-encapsulated mRNA encoding EvoETR achieved ~50% PCSK9 silencing in mouse liver that persisted for approximately one year, including through forced hepatocyte regeneration via partial hepatectomy — demonstrating that the epigenetic modification is faithfully maintained through cell division (Cappelluti et al., 2024).

Tremblay et al. (2025) at Chroma Medicine (now nChroma Bio) advanced this approach to nonhuman primates, achieving approximately 90% reduction in circulating PCSK9 protein and approximately 70% reduction in LDL cholesterol in cynomolgus monkeys from a single LNP-mRNA dose, with durability exceeding 343 days and maintenance through partial hepatectomy. The zinc finger-based editor targets CpG dinucleotides flanking the PCSK9 transcription start site, recruiting DNMT3A/3L to catalyze de novo DNA methylation that is subsequently maintained by endogenous DNMT1 during cell division (Tremblay et al., 2025).

### 3.5 Compact Zinc Finger-DdCBE Fusions for Mitochondrial Editing

Zinc finger domains offer a critical size advantage for mitochondrial genome editing, where the absence of RNA import machinery precludes the use of CRISPR-Cas systems. Willis et al. (2022) developed zinc finger-DddA-derived cytosine base editors (ZF-DdCBEs), replacing the bulky TALE repeat arrays in conventional DdCBEs with compact zinc finger domains. Each ZF requires only ~28 residues per 3-bp recognition unit versus ~34 residues per 1-bp unit for TALEs, enabling the construction of base editors that target both mitochondrial and nuclear DNA while remaining within size constraints compatible with efficient delivery (Willis et al., 2022). AlphaFold-guided structural modeling of six-finger zinc finger nucleases has further improved the design of the linker geometries connecting zinc finger domains to catalytic modules (Katayama et al., 2024).

### 3.6 Novel Mathematical Framework: Combinatorial Search Space and ML Sampling Efficiency (F270)

The design of an $n$-finger zinc finger array targeting a $3n$-bp DNA sequence presents a combinatorial challenge. Each ~28-residue finger has seven critical specificity-determining positions (−1, 1, 2, 3, 5, 6 relative to the recognition helix, plus residue D2 at the finger-finger interface). The naive protein sequence search space is:

```math
|\Omega_{\text{naive}}| = 20^{7n}
```

For a typical six-finger array ($n = 6$), this yields $20^{42} \approx 4.4 \times 10^{54}$ possible sequences — a space far too vast for experimental screening. The ZFDesign model reduces this space by learning the joint probability distribution over finger sequences conditioned on target DNA:

```math
P(\mathbf{s}_1, \ldots, \mathbf{s}_n \mid \mathbf{d}) = \prod_{i=1}^{n} P(\mathbf{s}_i \mid \mathbf{s}_{i-1}, \mathbf{d}_i, \mathbf{d}_{i-1})
```

where $\mathbf{s}_i$ is the sequence of finger $i$, $\mathbf{d}_i$ is the three-nucleotide target triplet, and the conditional dependence on $\mathbf{s}_{i-1}$ captures inter-finger cooperativity. The effective search space explored by the model can be quantified by the sampling efficiency ratio:

```math
\eta_{\text{ML}} = \frac{|\Omega_{\text{effective}}|}{|\Omega_{\text{naive}}|} = \exp\!\left(-\sum_{i=1}^{n} H(\mathbf{s}_i \mid \mathbf{s}_{i-1}, \mathbf{d}) \cdot \ln 20\right)
```

where $H(\mathbf{s}_i \mid \mathbf{s}_{i-1}, \mathbf{d})$ is the conditional entropy of each finger's sequence given the learned model. For ZFDesign, the conditional entropy at each position drops to approximately 1–2 bits (versus $\log_2 20 \approx 4.3$ bits for uniform sampling), yielding an effective dimensionality reduction of approximately $10^{30}$-fold for a six-finger array. This compression factor explains why the model achieves practical success rates from computationally tractable sample sizes.

---

## 4. TALE Proteins: A Predictable Recognition Code and Durable Therapeutic Silencing

### 4.1 The TALE Repeat Code

Transcription activator-like effectors (TALEs) are type III secretion system proteins from *Xanthomonas* bacteria that reprogram host gene expression by binding specific promoter sequences. The structural basis of TALE-DNA recognition was elucidated crystallographically in 2012, revealing a superhelical array of 34-residue tandem repeats that wraps around the DNA major groove, with each repeat contacting exactly one base pair through the RVD at positions 12 and 13 (Deng et al., 2012). The four canonical RVDs — NI (adenine), HD (cytosine), NG (thymine), and NN (guanine/adenine) — constitute a near-digital recognition code that is far more predictable than the context-dependent zinc finger grammar. This predictability made TALEs the first truly "designable" DNA-binding protein scaffold, enabling construction of arrays targeting virtually any sequence through simple repeat assembly.

### 4.2 Assembly and Engineering Advances

Golden Gate cloning and the FLASH (Fast Ligation-based Automatable Solid-phase High-throughput) assembly system reduced TALE construction from weeks to days. Non-canonical RVDs — including NH (guanine-specific), NA, and HN — have expanded the recognition code and improved specificity at degenerate positions. Compact TALE scaffolds with truncated N- and C-terminal domains have been engineered to minimize protein size while maintaining DNA-binding affinity, facilitating delivery. The discovery of novel DNA-binding tandem repeat proteins (TRPs) using protein language model-based prediction tools (PLM-DBPPred) has identified 11 previously unknown TRP families with DNA-binding activity, 6 of which exhibit sequence specificity, expanding the known repertoire of TALE-like scaffolds beyond the *Xanthomonas* lineage (Hu et al., 2024).

### 4.3 TALE-Based Epigenome Editors: EpiReg-T and Durable Silencing in Primates

Mao et al. (2025) developed EpiReg-T, an optimized TALE-based epigenetic regulator that integrates TALE DNA-binding arrays with engineered KRAB-DNMT3A-DNMT3L effector fusions for maximal CpG methylation at target loci. In the mouse liver, a single LNP-mRNA dose achieved 98% silencing of the target gene (PCSK9). In cynomolgus monkeys, EpiReg-T achieved greater than 90% PCSK9 silencing and approximately 70% LDL cholesterol reduction that persisted for 343 days — comparable to the zinc finger-based approach of Tremblay et al. (2025) and establishing TALE scaffolds as equally viable for therapeutic epigenome editing. The study also demonstrated that TALE-based editors maintained silencing through hepatocyte proliferation, confirming that the deposited epigenetic marks are faithfully inherited (Mao et al., 2025).

The head-to-head comparison between zinc finger and TALE epigenome editors targeting the same gene (PCSK9) represents a natural experiment in scaffold performance. Both platforms achieve >90% silencing lasting >343 days from single LNP-mRNA doses. The key differentiator lies in design predictability versus compactness: TALEs are easier to design for new targets (deterministic RVD code), while zinc fingers are smaller and potentially better suited for combination with large effector domains or for applications requiring AAV delivery.

### 4.4 Novel Mathematical Framework: Position-Dependent TALE Binding Kinetics (F271)

The binding affinity of a TALE array is not simply the product of independent per-repeat contributions. Position-dependent effects — including the T0 requirement at the 5' end of the target (contacted by a conserved tryptophan in the N-terminal domain), enhanced contributions from N-terminal repeats, and cooperativity arising from the superhelical wrapping geometry — modulate effective affinity. We model the effective dissociation constant of an $n$-repeat TALE array as:

```math
K_{d,\text{eff}}(n) = K_0 \prod_{i=1}^{n} K_{d,i} \cdot \sigma_i(n)
```

where $K_0$ is the basal nonspecific affinity of the N/C-terminal scaffold, $K_{d,i}$ is the intrinsic dissociation constant of repeat $i$ for its cognate base (determined by the RVD: $K_{d,\text{HD}} \approx K_{d,\text{NI}} < K_{d,\text{NG}} < K_{d,\text{NN}}$, reflecting the relative discrimination strength of each RVD), and $\sigma_i(n)$ is a positional cooperativity factor:

```math
\sigma_i(n) = \exp\!\left(-\alpha \cdot \frac{(i - 1)}{n - 1}\right)
```

where $\alpha > 0$ is the cooperativity decay constant reflecting the experimental observation that N-terminal repeats contribute more to binding energy than C-terminal repeats. The total specificity information encoded by the array is:

```math
I_{\text{TALE}}(n) = \sum_{i=1}^{n} \log_2\!\left(\frac{K_{d,\text{mismatch},i}}{K_{d,i}}\right) \approx n \cdot \bar{I}_{\text{RVD}}
```

where $\bar{I}_{\text{RVD}} \approx 1.5$–$2.0$ bits per repeat (reflecting the ~4-fold discrimination of the best RVDs), yielding a total information content of approximately 24–32 bits for a 16-repeat array — sufficient for unique 12–16-bp target specification, which can be augmented to genome-wide uniqueness by the additional scaffold-DNA contacts outside the repeat array.

---

## 5. Meganucleases: Precision from Compact Scaffolds

### 5.1 The LAGLIDADG Family and Meganuclease Engineering

Homing endonucleases of the LAGLIDADG family are compact (~40 kDa) proteins that recognize exceptionally long DNA sequences (12–40 bp) — longer than any other naturally occurring nuclease family. The canonical engineering scaffold, I-CreI, is a homodimeric enzyme that cleaves a 22-bp pseudo-palindromic target site. The extraordinary specificity of meganucleases arises from an extensive protein-DNA interface involving both direct and indirect readout over the entire recognition sequence, with each monomer contributing approximately 10–12 base-specific contacts (Stoddard, 2014).

Engineering meganucleases for novel target specificities is fundamentally challenging because the protein-DNA contacts are distributed across a large, highly interdependent interface — unlike the modular repeat structures of zinc fingers and TALEs. Successful approaches combine semi-rational design (guided by crystal structures) with directed evolution and high-throughput screening, typically modifying the I-CreI scaffold in a two-step process: first engineering each monomer half for a new half-site specificity, then combining the halves and optimizing for cooperative binding and cleavage of the full-length target.

### 5.2 MitoARCUS: Precision Mitochondrial Genome Surgery

The most advanced application of engineered meganucleases is mitoARCUS (Precision BioSciences' ARCUS platform adapted for mitochondrial targeting), which exploits the compact size and single-protein architecture of I-CreI derivatives to selectively eliminate pathogenic mitochondrial DNA variants. Shoop et al. (2023) demonstrated that mitoARCUS targeted to the MELAS-associated m.3243A>G mutation eliminated 95% of mutant mitochondrial DNA (reducing heteroplasmy from ~50% to ~0.3%) without detectable nuclear off-target activity, restoring mitochondrial respiratory chain function in patient-derived cells (Shoop et al., 2023). Earlier in vivo work by Zekonyte et al. (2021) established the feasibility of AAV9-delivered mitoARCUS in mouse skeletal muscle and liver, demonstrating robust and selective mutant mtDNA elimination in a living organism (Zekonyte et al., 2021).

### 5.3 Clinical Translation: First-in-Human Meganuclease Gene Editing

Precision BioSciences has advanced two meganuclease programs to clinical or late preclinical stages:

**PBGENE-HBV (ELIMINATE-B trial):** The first-in-human trial of an in vivo-delivered meganuclease, targeting the hepatitis B virus covalently closed circular DNA (cccDNA) in hepatocytes. The ARCUS meganuclease is delivered via LNP to cleave conserved regions of the HBV genome. As of late 2025, nine patients have been dosed across three cohorts (0.2–0.8 mg/kg), with best responses showing 47–69% reduction in hepatitis B surface antigen (HBsAg) and durable ~50% reduction at 7 months. No dose-limiting toxicities have been reported (Precision BioSciences, 2025 corporate disclosure).

**PBGENE-PMM:** A mitochondrial disease program targeting the m.3243A>G mutation associated with primary mitochondrial myopathy (PMM). Preclinical data demonstrate 95% reduction in mutant mtDNA heteroplasmy from a single treatment. An Investigational New Drug (IND) application was targeted for 2025.

### 5.4 Novel Mathematical Framework: Meganuclease Redesign as an NK Fitness Landscape (F272)

The difficulty of meganuclease redesign can be formalized using Kauffman's NK fitness landscape model, where $N$ represents the number of amino acid positions at the protein-DNA interface that determine specificity, and $K$ represents the number of epistatic interactions per position (i.e., the number of other positions whose identity influences the contribution of position $i$ to binding).

For I-CreI, the interface comprises approximately $N \approx 28$ direct-contact positions (14 per monomer), each interacting with $K \approx 2$–$4$ neighboring positions through structural and electrostatic coupling. The fitness landscape ruggedness — which determines the fraction of target specificities accessible by local mutational walks — is characterized by the autocorrelation length:

```math
\ell(N, K) = \frac{N - 1}{K}
```

For I-CreI ($N = 28$, $K = 3$), $\ell \approx 9$, implying that mutational walks of length $\leq 9$ substitutions can navigate between fitness peaks with reasonable probability, while longer walks are likely to traverse fitness valleys. The fraction of all possible $4^N$ target specificities (DNA sequences) accessible from a given starting specificity by walks of length $\leq m$ is approximately:

```math
f_{\text{accessible}}(m) \approx 1 - \exp\!\left(-\frac{\binom{N}{m} \cdot q^m}{4^N \cdot (1 + K/N)^m}\right)
```

where $q$ is the average number of amino acid substitutions per position that maintain folding stability ($q \approx 3$–$5$ for well-packed interfaces). For realistic parameters, $f_{\text{accessible}} \ll 1$ for all $m < N/2$, confirming the empirical observation that meganuclease redesign requires extensive engineering campaigns involving both rational design and directed evolution, in contrast to the modular plug-and-play assembly of zinc fingers and TALEs. This rugged fitness landscape is the fundamental biophysical reason why meganucleases remain the most difficult DNA-binding platform to retarget.

---

## 6. De Novo Computational Design: The RFdiffusion Revolution

### 6.1 The Paradigm Shift: Designing DNA-Binding Proteins from First Principles

The computational design of novel proteins with prescribed structures and functions — without recourse to natural templates — has advanced from a theoretical aspiration to a practical engineering discipline over the past decade. The convergence of three deep-learning breakthroughs — structure prediction (AlphaFold; Jumper et al., 2021), structure generation (RFdiffusion; Watson et al., 2023), and sequence design (ProteinMPNN; Dauparas et al., 2022) — created the computational infrastructure necessary to tackle the most challenging protein design problem: programming sequence-specific interactions with DNA.

The challenge is formidable. Unlike protein-protein interfaces (which are mediated primarily by hydrophobic packing and shape complementarity) or protein-small molecule interactions (which exploit defined binding pockets), protein-DNA recognition requires precise positioning of polar residues to form base-specific hydrogen bonds within the geometrically constrained major groove of double-stranded DNA, while simultaneously achieving the correct electrostatic complementarity with the phosphodiester backbone. No prior computational method had succeeded in designing a protein from scratch — without deriving from any natural DNA-binding scaffold — that bound a specified DNA sequence.

### 6.2 RFdiffusion: Generative Protein Structure Design

RFdiffusion adapts denoising diffusion probabilistic models to the protein structure domain. Starting from a random distribution of residue frames in 3D space, the model iteratively denoises toward a physically plausible protein backbone, guided by a neural network trained on experimental protein structures. The architecture can be conditioned on various inputs — desired secondary structure, binding hotspot residues, symmetry constraints, or, critically, the three-dimensional coordinates of a molecular target such as DNA (Watson et al., 2023). RFdiffusion generates diverse, novel protein backbone topologies that satisfy the input constraints, which are then handed to a sequence design module.

### 6.3 ProteinMPNN and LigandMPNN: Structure-Conditioned Sequence Design

ProteinMPNN uses a message-passing neural network architecture to predict amino acid sequences that will fold into a given backbone structure. The model processes a graph representation of the protein backbone and outputs per-residue amino acid probability distributions, enabling the rapid generation of thousands of candidate sequences for any designed structure (Dauparas et al., 2022).

For DNA-binding protein design, LigandMPNN extends this framework by explicitly representing all non-protein atoms — including DNA bases, sugars, and phosphates — as additional nodes in the message-passing graph. This allows the model to design amino acid sequences that are optimized not only for backbone folding but also for specific interactions with the DNA target. LigandMPNN achieves 50.5% sequence recovery for nucleotide-interacting residues, compared to 34.0% for the original ProteinMPNN, demonstrating the importance of explicit ligand modeling for interface design (Dauparas et al., 2025).

### 6.4 Glasscock et al. 2025: The First De Novo Designed Sequence-Specific DNA-Binding Proteins

The breakthrough paper by Glasscock et al. (2025) demonstrated, for the first time, the computational design of small, modular proteins that recognize arbitrary short DNA sequences entirely from first principles. The design pipeline proceeds in three stages:

**Stage 1 — Scaffold-DNA docking (RIFdock):** Rotamer interaction fields are computed for each DNA target to identify protein backbone placements that can make favorable contacts with exposed bases and the phosphate backbone. This generates candidate binding modes — spatial relationships between protein backbone positions and the DNA helix.

**Stage 2 — Sequence design (LigandMPNN):** For each docked scaffold, LigandMPNN designs amino acid sequences that simultaneously satisfy internal folding requirements and form base-specific contacts with the DNA target. The explicit representation of DNA atoms in the LigandMPNN graph ensures that designed sequences are optimized for the protein-DNA interface.

**Stage 3 — Multi-module assembly (RFdiffusion):** Individual DNA-binding modules are assembled into multi-domain architectures that span longer DNA target sequences. RFdiffusion generates rigid linkers and structural connectors that maintain the designed protein-DNA geometry across multiple binding modules arrayed along the DNA helix.

The results were striking. Designs were generated for five distinct DNA target sequences, and experimental characterization revealed:

- **Binding affinity:** Mid-nanomolar to high-nanomolar $K_d$ values, competitive with natural transcription factors
- **Structural accuracy:** The crystal structure of DBP-48 matched the computational design model with a root-mean-square deviation (RMSD) of only 0.64 Å — atomic-level accuracy
- **Functional validation:** Designed proteins achieved 20-fold transcriptional repression when targeted to a promoter in *E. coli*, and functional transcriptional activation in human HEK293T cells (Glasscock et al., 2025)

This work establishes that the protein-DNA recognition problem is solvable from first principles, without requiring any template derived from natural DNA-binding domains. The designed proteins use helix-turn-helix motifs — one of nature's most common DNA-binding folds — but with entirely novel sequences and detailed geometries that differ from any known natural protein.

### 6.5 RoseTTAFold All-Atom and the Expanding Computational Toolkit

RoseTTAFold All-Atom (RFAA) extends the RoseTTAFold architecture to simultaneously model proteins, nucleic acids, small molecules, metal ions, and covalent modifications using a hybrid representation that combines residue-level tokens (for amino acids and nucleotide bases) with atomic-level tokens (for everything else). RFAA was validated crystallographically for small-molecule binders and provides a general-purpose platform for modeling protein-nucleic acid complexes with atomic detail (Krishna et al., 2024). The comprehensive review by Kortemme (2024) contextualizes these advances within the broader trajectory of de novo protein design, noting the transition from "new structures" to "programmable functions" — of which DNA sequence recognition is among the most demanding (Kortemme, 2024).

### 6.6 Novel Mathematical Framework: Design Success Probability as a Function of Sampling Depth (F273)

The computational protein design pipeline can be modeled as a Bernoulli sampling process. Let $n_s$ denote the number of scaffold backbones generated by RFdiffusion, $n_q$ the number of sequences designed per scaffold by LigandMPNN, and $p$ the per-design probability that a candidate binds the target DNA with affinity $K_d \leq K_d^*$ (the affinity threshold for functional activity). The probability of obtaining at least one successful design is:

```math
P(\text{success} \geq 1) = 1 - (1 - p)^{n_s \cdot n_q}
```

For a target success probability of $P \geq 0.95$:

```math
n_s \cdot n_q \geq \frac{\ln(0.05)}{\ln(1 - p)} \approx \frac{3.0}{p}
```

Glasscock et al. (2025) report that of the designs experimentally tested, approximately 5–15% showed detectable binding ($p \approx 0.05$–$0.15$). Taking $p = 0.10$ as a representative value, approximately 30 independent designs must be tested to achieve 95% confidence in obtaining at least one binder — a computationally and experimentally tractable number.

The expected number of successful binders from $N = n_s \cdot n_q$ designs follows a binomial distribution:

```math
\mathbb{E}[\text{hits}] = N \cdot p, \qquad \text{Var}[\text{hits}] = N \cdot p \cdot (1 - p)
```

As the field matures, the key engineering metric is the **design efficiency** $\epsilon = p / C$, where $C$ is the computational cost per design (GPU-hours). Improvements in RFdiffusion, LigandMPNN, and filtering methods that increase $p$ or decrease $C$ will accelerate the pipeline toward routine, on-demand DNA-binding protein generation.

### 6.7 Novel Mathematical Framework: Information-Theoretic Capacity of Protein-DNA Recognition (F274)

Different DNA-binding platforms encode sequence specificity with different information densities. The **specificity information** $I$ per recognition unit can be quantified in bits:

```math
I_{\text{unit}} = \log_2\!\left(\frac{K_{d,\text{worst mismatch}}}{K_{d,\text{cognate}}}\right)
```

For the three major protein-based scaffolds:

- **Zinc finger C2H2:** Each finger recognizes 3 bp. With typical discrimination ratios of $10^{1.5}$–$10^{2}$ per finger, $I_{\text{ZF}} \approx 5$–$7$ bits per finger, or approximately 1.7–2.3 bits per base pair recognized.

- **TALE repeat:** Each repeat recognizes 1 bp. The best RVDs (HD, NI) achieve $\sim$10-fold discrimination, yielding $I_{\text{TALE}} \approx 3.3$ bits per repeat per base pair. Weaker RVDs (NN) provide $\sim$3–5-fold discrimination, yielding $I_{\text{TALE}} \approx 1.6$–$2.3$ bits per base pair.

- **De novo designed HTH:** From Glasscock et al. (2025), individual binding modules recognize ~4–6 bp with mid-nM affinity. Assuming $\sim$100-fold discrimination per module, $I_{\text{HTH}} \approx 6.6$ bits per module, or approximately 1.1–1.7 bits per base pair.

The minimum total information required for unique genomic targeting (human genome, 3.2 × 10^9 bp) is:

```math
I_{\text{min}} = \log_2(3.2 \times 10^9) \approx 31.6 \text{ bits}
```

Dividing by the per-base-pair information capacity yields the minimum recognition footprint:

| Platform | $I_{\text{per bp}}$ (bits) | Min. footprint for genomic uniqueness |
|----------|---------------------------|---------------------------------------|
| Zinc finger | 1.7–2.3 | 14–19 bp (5–7 fingers) |
| TALE | 1.6–3.3 | 10–20 repeats |
| De novo HTH | 1.1–1.7 | 19–29 bp (4–6 modules) |

This framework reveals that de novo designed proteins currently achieve lower information density per base pair than zinc fingers or the best TALE RVDs, explaining why multi-module architectures are necessary for genomic-scale specificity. Improving per-module discrimination — through optimized interface design or incorporation of indirect readout — is a key engineering target.

---

## 7. Ultracompact Ancestral Nucleases: IscB, Fanzor, and Cas12f

### 7.1 Evolutionary Origins: From Transposons to CRISPR

The CRISPR-Cas adaptive immune systems of bacteria and archaea did not arise de novo but evolved from selfish genetic elements — specifically, the IS200/IS605 family of insertion sequences. These transposable elements encode two key protein families: TnpB (a DNA-guided nuclease ~400 amino acids in length) and IscB (an RNA-guided nuclease ~500 amino acids). The landmark discovery by Altae-Tran et al. (2021) that these transposon-encoded proteins constitute widespread programmable RNA-guided endonucleases — collectively termed the OMEGA (Obligate Mobile Element-Guided Activity) system — revealed the evolutionary ancestors of both Cas12 (descended from TnpB) and Cas9 (descended from IscB) (Altae-Tran et al., 2021).

### 7.2 Structural Biology: The IscB-to-Cas9 Evolutionary Trajectory

Cryo-electron microscopy structures of IscB-ωRNA-DNA complexes from multiple laboratories have illuminated the structural basis of RNA-guided DNA recognition in these compact systems. Schuler et al. (2022) determined the 2.78 Å structure of *Desulfohalobium* IscB complexed with its ωRNA guide and double-stranded DNA target, revealing that IscB achieves RNA-guided DNA cleavage through a mechanism analogous to Cas9 despite being less than half its size (~500 vs ~1,400 amino acids). The ωRNA serves as a structural scaffold that compensates for the "missing" protein domains, simultaneously providing the scaffold function of both the crRNA and tracrRNA of Cas9 systems (Schuler et al., 2022). Kato, Hirano et al. (2022) independently determined the 2.6 Å structure of *Odoribacter* IscB, confirming the dual role of the ωRNA and identifying the RuvC nuclease domain architecture conserved from IscB through Cas9 (Kato et al., 2022).

The evolutionary trajectory from IscB to Cas9 has been visualized at atomic resolution by Nagahata et al. (2026), who determined cryo-EM structures of four phylogenetically diverse nucleases representing distinct evolutionary stages. The transition involved: (1) loss of the PLMP domain present in IscB, (2) acquisition of the zinc finger-containing REC3 domain, (3) extension of the bridge helix, and (4) acquisition of the REC1 domain — a progressive protein expansion coupled with guide RNA miniaturization, reflecting a transfer of structural information from RNA to protein over evolutionary time (Nagahata et al., 2026).

### 7.3 Engineering IscB for Mammalian Genome Editing

The ultracompact size of IscB (~500 amino acids) makes it an attractive scaffold for AAV-delivered genome editing, but wild-type IscB proteins exhibit low activity in mammalian cells. Xue et al. (2024) engineered a variant designated eIscB through just three amino acid substitutions combined with fusion of a nonspecific DNA-binding domain, achieving 91.3% editing efficiency at validated mammalian genomic loci — comparable to SpCas9. The engineered IscB-ωRNA system maintained its compact size advantage, enabling single-AAV delivery of both the nuclease and its guide (Xue et al., 2024). This work demonstrates that the activity gap between ancestral and modern nucleases can be bridged by rational engineering informed by structural and evolutionary analysis.

### 7.4 Fanzor: The First Eukaryotic Programmable RNA-Guided Nuclease

While IscB and TnpB are prokaryotic, Saito et al. (2023) discovered that eukaryotic transposons encode homologous programmable endonucleases termed Fanzors. These TnpB homologs, found across fungi, protists, and metazoans, are guided by ωRNAs derived from the transposon and cleave double-stranded DNA at target sites flanked by a target-adjacent motif (TAM). Fanzor proteins are active in human cells, establishing them as the first known eukaryotic RNA-guided programmable DNA nucleases (Saito et al., 2023).

Wei et al. (2026) engineered an enhanced Fanzor2 variant (enNlovFz2) that achieved 11.1-fold improved editing over wild-type, with an expanded TAM repertoire (5'-NMYG), enabling targeting of a broader range of genomic sites. In a therapeutic proof-of-concept, AAV-delivered enNlovFz2 restored dystrophin expression in a Duchenne muscular dystrophy (DMD) mouse model, demonstrating the clinical potential of engineered eukaryotic programmable nucleases (Wei et al., 2026).

### 7.5 Cas12f and CasMINI: Hypercompact CRISPR Systems

Cas12f proteins (~400–500 amino acids) represent the smallest known CRISPR effectors, roughly one-third the size of SpCas9. Kim et al. (2022) demonstrated that the hypercompact *Uncultured archaeon* Cas12f1 (Un1Cas12f1) could be engineered through guide RNA optimization to achieve 867-fold increased indel formation in human cells, reaching efficiencies rivaling SpCas9 at many loci while remaining deliverable by a single AAV vector (Kim et al., 2022).

The CasMINI platform, derived from Un1Cas12f1, has been further enhanced by Ma et al. (2025), who added an N-terminal alpha-helix to create hpCasMINI (554 amino acids). This modification boosted gene editing activity 1.4–19.5-fold across diverse genomic loci and enabled in vivo liver gene activation and tumor modeling in mice — functions requiring the compact nuclease to be fused to additional transcriptional regulatory domains while remaining within AAV packaging constraints (Ma et al., 2025).

### 7.6 Compact Cas9d and Ancestral Sequence Reconstruction

Fregoso Ocampo et al. (2025) identified Cas9d, a naturally compact Cas9 variant of only 747 amino acids — roughly half the size of SpCas9 (1,368 aa) — from metagenomic data. Cryo-EM structures in multiple conformational states revealed that Cas9d achieves DNA targeting through a stepwise conformational switch in its REC2 domain, and that its single-guide RNA can be truncated by approximately 25% while retaining activity. Furthermore, ancestral sequence reconstruction of the Cas9d lineage yielded functional nucleases with even more compact architectures, demonstrating that evolutionary history can be mined for practical engineering solutions (Fregoso Ocampo et al., 2025).

### 7.7 Metagenomic Discovery: The Vast Reservoir of Undiscovered DNA-Binding Systems

The application of deep terascale clustering (FLSHclust) to 8.8 terabytes of metagenomic sequence data by Altae-Tran et al. (2023) uncovered 188 previously unknown CRISPR-linked gene modules, including entirely novel system types (type VII). This analysis revealed that the known diversity of programmable DNA-targeting systems represents only a fraction of what exists in nature, suggesting that many additional ultracompact, high-specificity DNA-binding scaffolds remain to be discovered and engineered (Altae-Tran et al., 2023). Complementing this discovery effort, Ruffolo et al. (2025) demonstrated that protein language models trained on over one million CRISPR operons mined from 26 terabytes of metagenomic data can generate entirely novel CRISPR-Cas nucleases — including OpenCRISPR-1, which differs from SpCas9 by over 400 amino acids yet achieves comparable editing activity with 95% reduction in off-target effects, exemplifying the power of generative AI applied to this protein family (Ruffolo et al., 2025).

### 7.8 Novel Mathematical Framework: The Protein-Guide RNA Information Conservation Law (F275)

The evolutionary trajectory from IscB to Cas9 reveals a fundamental trade-off between protein size and guide RNA complexity. Both components contribute to target DNA recognition: the protein scaffold provides structural rigidity, PAM/TAM recognition, and conformational proofreading, while the guide RNA provides the Watson-Crick base pairing that determines sequence specificity. The total information required for target recognition is a conserved quantity, partitioned between protein and RNA:

```math
I_{\text{total}} = I_{\text{protein}} + I_{\text{RNA}}
```

For a target of length $L$ base pairs, the minimum specificity information is:

```math
I_{\text{total}} \geq 2L \text{ bits}
```

(reflecting 4 possible bases per position). The protein contribution scales with the number of protein-DNA contacts $n_p$ and their average discriminatory information $\bar{i}_p$:

```math
I_{\text{protein}} = n_p \cdot \bar{i}_p
```

while the RNA contribution is primarily through Watson-Crick pairing:

```math
I_{\text{RNA}} = L_{\text{spacer}} \cdot \bar{i}_{\text{WC}}
```

where $L_{\text{spacer}}$ is the spacer length and $\bar{i}_{\text{WC}} \approx 1.5$–$2.0$ bits per nucleotide (less than the theoretical maximum of 2 bits due to tolerated G-U wobble pairs and partially tolerated mismatches). The structural scaffold contribution $I_{\text{scaffold}}$ does not encode sequence specificity but enables the RNP complex to achieve the binding geometry:

```math
L_{\text{scaffold}} = L_{\text{protein}} + L_{\omega\text{RNA}} \approx \text{const.}
```

Empirical data support this conservation law:

| System | Protein (aa) | Guide RNA (nt) | Total scaffold | Target (bp) |
|--------|-------------|----------------|----------------|-------------|
| IscB | ~500 | ~220 (ωRNA) | ~720 units | 20 |
| Cas12f | ~450 | ~60 (crRNA) | ~510 units | 20 |
| Cas9 | ~1,400 | ~100 (sgRNA) | ~1,500 units | 20 |

The inverse relationship between protein and RNA size — IscB has the smallest protein but largest RNA guide, while Cas9 has the largest protein but smallest guide — reflects an evolutionary transfer of structural scaffolding function from RNA to protein. The conservation law predicts a **minimum achievable protein size** for a given target length:

```math
L_{\text{protein, min}} = L_{\text{total scaffold}} - L_{\omega\text{RNA, max}}
```

where $L_{\omega\text{RNA, max}}$ is the maximum guide RNA size compatible with stable RNP assembly. For systems with target lengths of ~20 bp, this minimum appears to be approximately 400–500 amino acids, consistent with the observed lower bound across all known RNA-guided nuclease families.

---

## 8. Bridge RNAs and Programmable Recombinases

### 8.1 A Fundamentally New DNA-Targeting Mechanism

Bridge RNAs, discovered by Durrant et al. (2024) within IS110 family insertion sequences, represent a mechanistically distinct approach to programmable DNA recognition. Unlike all other systems discussed in this review — which either use protein domains (ZF, TALE, meganuclease) or RNA-guided protein effectors (CRISPR-Cas) for DNA targeting — bridge RNAs direct a recombinase enzyme to perform sequence-specific DNA recombination through two independently reprogrammable RNA loops: a **target-binding loop** that specifies the genomic insertion site and a **donor-binding loop** that specifies the DNA cargo to be integrated. The recombinase enzyme itself is not sequence-specific; all targeting information resides in the bridge RNA (Durrant et al., 2024).

### 8.2 Structural Basis of Bridge RNA-Mediated Recombination

The structural mechanism of bridge RNA-guided recombination was elucidated by Hiraizumi et al. (2024), who determined cryo-EM structures of the IS110-encoded recombinase bound to bridge RNA, target DNA, and donor DNA. The bridge RNA forms a bipartite structure: a core scaffold region that binds the recombinase and two exposed internal loops (the target-binding and donor-binding loops) that form Watson-Crick base pairs with their respective DNA substrates. The recombinase catalyzes strand exchange at defined positions within the target and donor sequences, enabling precise, scarless DNA insertion without introducing double-strand breaks or requiring cellular DNA repair pathways (Hiraizumi et al., 2024).

### 8.3 Megabase-Scale Genome Rearrangements

Perry et al. (2026) extended bridge RNA recombinases to therapeutic-scale genome engineering, demonstrating programmable insertion, deletion, and inversion of DNA segments up to 0.93 megabases in mammalian cells. Key results included approximately 20% insertion efficiency, 82% target specificity, and successful excision of the BCL11A erythroid enhancer — a validated therapeutic target for sickle cell disease — using bridge recombinases as an alternative to nuclease-mediated approaches. This work establishes bridge RNA systems as the first programmable tool capable of mediating megabase-scale genomic rearrangements without relying on double-strand break repair (Perry et al., 2026).

### 8.4 Novel Mathematical Framework: Bridge RNA Recombination Specificity (F276)

The dual-loop architecture of bridge RNAs provides a unique specificity model. The effective specificity is the product of independent target-loop and donor-loop recognition:

```math
S_{\text{eff}} = S_{\text{target}} \times S_{\text{donor}}
```

Each loop provides specificity through Watson-Crick base pairing. For a target-binding loop of length $L_T$ nucleotides and a donor-binding loop of length $L_D$ nucleotides, the number of distinguishable sequences is:

```math
S_{\text{target}} = 4^{L_T}, \qquad S_{\text{donor}} = 4^{L_D}
```

For unique targeting within the human genome (3.2 × 10^9 bp), the target loop must satisfy:

```math
4^{L_T} \geq 3.2 \times 10^9 \implies L_T \geq \frac{\log(3.2 \times 10^9)}{\log 4} \approx 15.8 \text{ nt}
```

The effective specificity of the combined system is:

```math
S_{\text{eff}} = 4^{L_T + L_D}
```

In practice, IS110 bridge RNAs contain target-binding loops of approximately 14 nucleotides and donor-binding loops of approximately 14 nucleotides, yielding:

```math
S_{\text{eff}} = 4^{28} \approx 7.2 \times 10^{16}
```

This exceeds the human genome size by a factor of approximately $2.3 \times 10^7$, providing an enormous theoretical specificity margin. However, the actual discrimination must account for tolerated mismatches. If each loop tolerates $m$ mismatches on average, the effective number of off-target sites in the genome is approximately:

```math
N_{\text{off}} \approx \frac{G}{\displaystyle 4^{L_T}} \cdot \sum_{k=0}^{m} \binom{L_T}{k} \cdot 3^k
```

where $G$ is the genome size. For $L_T = 14$ and $m = 2$ tolerated mismatches:

```math
N_{\text{off}} \approx \frac{3.2 \times 10^9}{4^{14}} \cdot \left(1 + 14 \cdot 3 + 91 \cdot 9\right) = 11.9 \times 862 \approx 10{,}258
```

This substantial number of potential off-target sites underscores that, despite the large theoretical specificity of 28 total pairing nucleotides, the tolerance for mismatches — which is an inherent property of Watson-Crick recognition in biological environments — necessitates careful empirical off-target profiling, analogous to the challenge faced by CRISPR guide RNAs.

---

## 9. Cross-Platform Comparison and Convergence

### 9.1 Comparative Analysis

The following table summarizes the key properties of each programmable DNA-binding platform as of early 2026:

| Property | Zinc Finger | TALE | Meganuclease | De Novo HTH | IscB/Fanzor/Cas12f | Bridge RNA |
|----------|-------------|------|--------------|-------------|---------------------|------------|
| **Protein size** | ~180 aa (6-finger) | ~700 aa (18-repeat) | ~320 aa (monomer) | ~150–300 aa (2–4 modules) | ~400–750 aa | ~500 aa (recombinase) |
| **Recognition footprint** | 18 bp | 18 bp | 22 bp | 12–18 bp | 20 bp (guide) | 28 bp (dual loop) |
| **Specificity encoding** | Protein (context-dependent) | Protein (modular code) | Protein (integrated interface) | Protein (de novo contacts) | RNA guide | RNA (bridge) |
| **Design complexity** | ML required (ZFDesign) | Deterministic (RVD code) | Extensive evolution/design | Computational (RFdiffusion) | Guide RNA only | Loop reprogramming |
| **AAV-deliverable** | Yes | Marginal (with effector) | Yes | Yes | Yes (single AAV) | TBD |
| **PAM/TAM requirement** | None | 5'-T only | None | None | Yes (TAM/PAM) | None |
| **Clinical stage** | Phase 1/2 (epigenome) | Phase 1 (epigenome) | Phase 1 (PBGENE-HBV) | Preclinical | Preclinical | Preclinical |
| **Key advantage** | Compact, durable silencing | Predictable design | Long recognition site | First-principles design | Ultracompact, single AAV | No DSB, megabase-scale |

### 9.2 Novel Mathematical Framework: Multi-Platform Figure of Merit (F277)

To enable principled comparison across platforms, we define a composite **figure of merit** $\Phi$ that captures the three critical properties for therapeutic DNA-binding proteins — specificity, deliverability, and durability:

```math
\Phi = \frac{I_{\text{spec}}}{L_{\text{protein}}} \times D \times T
```

where:

- $I_{\text{spec}}$ = total specificity information (bits), calculated as in F274
- $L_{\text{protein}}$ = protein size (amino acids) — smaller is better for delivery
- $D$ = deliverability score: 1.0 for single-AAV-deliverable systems ($L_{\text{total}} < 4.7$ kb), scaling as $4700 / L_{\text{total}}$ for larger systems requiring dual-AAV or LNP delivery
- $T$ = durability score: 1.0 for permanent genetic modifications (nucleases, recombinases), 0.8 for durable epigenetic modifications (>1 year persistence), 0.3 for transient modifications (protein/mRNA half-life limited)

Computing $\Phi$ for each platform:

| Platform | $I_{\text{spec}}$ (bits) | $L_{\text{protein}}$ (aa) | $D$ | $T$ | $\Phi$ (bits/aa) |
|----------|-------------------------|--------------------------|-----|-----|-------------------|
| ZF (6-finger, epigenome) | ~36 | 180 | 1.0 | 0.8 | 0.160 |
| TALE (18-repeat, epigenome) | ~36 | 700 | 0.6 | 0.8 | 0.025 |
| Meganuclease (I-CreI) | ~44 | 320 | 1.0 | 1.0 | 0.138 |
| De novo HTH (4-module) | ~24 | 300 | 1.0 | 0.3* | 0.024 |
| IscB + ωRNA | ~40 | 500 | 1.0 | 1.0 | 0.080 |
| Cas12f + crRNA | ~40 | 450 | 1.0 | 1.0 | 0.089 |
| Bridge RNA (recombinase) | ~56 | 500 | 0.8 | 1.0 | 0.090 |

*De novo designed proteins currently lack effector domain fusions; $T = 0.3$ assumes transient binding only.

This analysis reveals that **zinc fingers achieve the highest figure of merit** due to their exceptional compactness relative to their specificity capacity, followed by meganucleases and the bridge RNA/ultracompact nuclease tier. The low $\Phi$ for de novo designed proteins reflects their current early stage — as effector domain fusions and improved per-module discrimination are developed, their $\Phi$ is expected to increase substantially.

### 9.3 Convergent Trends

Three convergent trends are reshaping the programmable DNA recognition landscape:

**Machine learning is accelerating all platforms.** ZFDesign (zinc fingers), PLM-DBPPred (novel TRPs), LigandMPNN (de novo design), and protein language models (OpenCRISPR-1, ancestral reconstruction) are all ML-driven. The shared infrastructure of protein language models, structural prediction, and generative design is creating a unified computational framework that transcends individual platforms.

**Epigenome editing is emerging as the unifying application.** The convergence of zinc finger and TALE platforms on durable gene silencing — both achieving >90% PCSK9 silencing for >1 year in primates from single doses — suggests that the optimal application of protein-based DNA recognition may not be nuclease-mediated gene disruption (where CRISPR dominates) but rather the precise, permanent modulation of gene expression without DNA cleavage.

**Hybrid architectures are emerging.** The combination of different DNA-binding scaffolds with diverse effector domains — zinc finger-DdCBE fusions for mitochondrial editing, TALE-deaminase fusions (TALEDs), de novo designed scaffolds with repressor or activator domains — suggests that the future lies not in any single platform but in the rational selection and combination of scaffolds optimized for each therapeutic application.

---

## 10. Open Questions and Future Directions

### 10.1 Can De Novo Design Achieve Zinc Finger Compactness with TALE Predictability?

The Glasscock et al. (2025) breakthrough demonstrates that de novo designed proteins can achieve functional DNA binding, but current designs require multi-module architectures (300+ amino acids for 12–18 bp recognition) and achieve lower per-base-pair information density than zinc fingers. A critical open question is whether computational design can produce a single, compact (~100–150 amino acid) protein module that recognizes 6+ base pairs with zinc finger-level discrimination — effectively combining the compactness of zinc fingers with the predictability of de novo design. Advances in LigandMPNN and RFdiffusion may enable exploration of protein-DNA binding modes beyond the classical HTH motif, potentially accessing novel folds with higher information density.

### 10.2 Scaling Specificity: From 18 bp to Genome-Wide Uniqueness

Current platforms achieve specificity over 16–22 base pairs, which is theoretically sufficient for unique human genome targeting but in practice results in off-target activity due to tolerated mismatches. Engineering proteins (or RNA guides) with sharply binary specificity — binding cognate targets with nanomolar affinity while exhibiting essentially no detectable affinity for single-mismatch sites — remains an unsolved problem. Conformational proofreading mechanisms analogous to Cas9's HNH domain checkpoint may need to be engineered into protein-only scaffolds.

### 10.3 Immunogenicity of Designed Proteins

All engineered and de novo designed proteins carry the risk of eliciting immune responses. The multi-objective ML approach of Wolfsberg et al. (2025) — simultaneously optimizing binding, immunogenicity, and stability — represents a promising framework, but the ability to predict T-cell epitopes from sequence alone remains imperfect. Clinical experience with engineered meganucleases (PBGENE-HBV), zinc finger editors (Chroma Medicine), and CRISPR therapies will provide essential immunogenicity data to calibrate these predictions.

### 10.4 Clinical Regulatory Path for Computationally Designed Therapeutics

De novo designed DNA-binding proteins present a novel regulatory challenge: they are not derivatives of any natural protein and have no evolutionary track record. Establishing the safety and immunogenicity profiles of entirely artificial protein-DNA binding domains will require new preclinical frameworks. The successful clinical deployment of other computationally designed proteins — including the RSV vaccine antigen DS-Cav1 and de novo designed influenza inhibitors — provides encouraging precedent.

### 10.5 Closed-Loop Design: Integrating Prediction and Generation

The current design pipeline (RFdiffusion → LigandMPNN → experimental validation) operates as an open loop. Closing the loop — using experimental binding data to iteratively retrain and improve the generative models — could dramatically increase design efficiency. The integration of AlphaFold 3's structure prediction capabilities with RFdiffusion's generative design, mediated by differentiable molecular simulation, represents a plausible path toward autonomous, self-improving DNA-binding protein design.

### 10.6 Epigenome Editing as a Promising Application

The head-to-head demonstration that both zinc finger and TALE scaffolds achieve year-long gene silencing from single LNP-mRNA doses in primates positions epigenome editing — rather than gene knockout or correction — as the most immediate therapeutic application of programmable DNA recognition. As de novo designed and ultracompact scaffolds mature, their incorporation into epigenome editing platforms (fused to DNMT3A/3L, KRAB, or other chromatin-modifying domains) could combine the advantages of all platforms: the predictability of computational design, the compactness of ancestral systems, and the durability of epigenetic modification.

---

## References

1. Abramson, J., Adler, J., Dunger, J., Evans, R., Green, T., Pritzel, A., Ronneberger, O., Willmore, L., Ballard, A. J., Bambrick, J., ... & Hassabis, D. (2024). Accurate structure prediction of biomolecular interactions with AlphaFold 3. *Nature*, 630(8016), 493–500. PMID: 38718835

2. Altae-Tran, H., Kannan, S., Demircioglu, F. E., Oshiro, R., Nety, S. P., McKay, L. J., Dlakic, M., Inskeep, W. P., Makarova, K. S., Macrae, R. K., Koonin, E. V., & Zhang, F. (2021). The widespread IS200/IS605 transposon family encodes diverse programmable RNA-guided endonucleases. *Science*, 374(6563), 57–65. PMID: 34591643

3. Altae-Tran, H., Kannan, S., Suberski, A. J., Mears, K. S., Demircioglu, F. E., Moeller, L., Kocalar, S., Oshiro, R., Makarova, K. S., Macrae, R. K., Koonin, E. V., & Zhang, F. (2023). Uncovering the functional diversity of rare CRISPR-Cas systems with deep terascale clustering. *Science*, 382(6673), eadi1910. PMID: 37995242

4. Anishchenko, I., Pellock, S. J., Chidyausiku, T. M., Ramelot, T. A., Ovchinnikov, S., Hao, J., Bafna, K., Norn, C., Kang, A., Bera, A. K., DiMaio, F., Carter, L., Chow, C. M., Montelione, G. T., & Baker, D. (2021). De novo protein design by deep network hallucination. *Nature*, 600(7889), 547–552. PMID: 34853475

5. Bennett, N. R., Watson, J. L., Ragotte, R. J., Borst, A. J., See, D. L., Weidle, C., Biswas, R., Yu, Y., Shrock, E. L., ... & Baker, D. (2026). Atomically accurate de novo design of antibodies with RFdiffusion. *Nature*, 649(8095), 183–193. PMID: 41193805

6. Cappelluti, M. A., Mollica Poeta, V., Valsoni, S., Quarato, P., Merlin, S., Merelli, I., & Lombardo, A. (2024). Durable and efficient gene silencing in vivo by hit-and-run epigenome editing. *Nature*, 627(8003), 416–423. PMID: 38418872

7. Cong, L., Ran, F. A., Cox, D., Lin, S., Barretto, R., Habib, N., Hsu, P. D., Wu, X., Jiang, W., Marraffini, L. A., & Zhang, F. (2013). Multiplex genome engineering using CRISPR/Cas systems. *Science*, 339(6121), 819–823. PMID: 23287718

8. Dauparas, J., Anishchenko, I., Bennett, N., Bai, H., Ragotte, R. J., Milles, L. F., Wicky, B. I. M., Courbet, A., de Haas, R. J., ... & Baker, D. (2022). Robust deep learning-based protein sequence design using ProteinMPNN. *Science*, 378(6615), 49–56. PMID: 36108050

9. Dauparas, J., Lee, G. R., Pecoraro, R., An, L., Anishchenko, I., Glasscock, C., & Baker, D. (2025). Atomic context-conditioned protein sequence design using LigandMPNN. *Nature Methods*, 22(4), 717–723. PMID: 40155723

10. Deng, D., Yan, C., Pan, X., Mahfouz, M., Wang, J., Zhu, J. K., Shi, Y., & Yan, N. (2012). Structural basis for sequence-specific recognition of DNA by TAL effectors. *Science*, 335(6069), 720–723. PMID: 22223738

11. Durrant, M. G., Perry, N. T., Pai, J. J., Jangid, A. R., Athukoralage, J. S., Hiraizumi, M., McSpedon, J. P., Pawluk, A., Nishimasu, H., Konermann, S., & Hsu, P. D. (2024). Bridge RNAs direct programmable recombination of target and donor DNA. *Nature*, 630(8018), 984–993. PMID: 38926615

12. Frangoul, H., Locatelli, F., Sharma, A., Bhatia, M., Mapara, M., Molinari, L., Wall, D., Liem, R. I., Telfer, P., Shah, A. J., ... & Grupp, S. A. (2024). Exagamglogene autotemcel for severe sickle cell disease. *New England Journal of Medicine*, 390(18), 1649–1662. PMID: 38661449

13. Fregoso Ocampo, R., Bravo, J. P. K., Dangerfield, T. L., Nocedal, I., Jirde, S. A., Alexander, L. M., Thomas, N. C., Das, A., Nielson, S., Johnson, K. A., Brown, C. T., Butterfield, C. N., Goltsman, D. S. A., & Taylor, D. W. (2025). DNA targeting by compact Cas9d and its resurrected ancestor. *Nature Communications*, 16(1), 457. PMID: 39774105

14. Glasscock, C. J., Pecoraro, R. J., McHugh, R., Doyle, L. A., Chen, W., Boivin, O., Lonnquist, B., Na, E., Politanska, Y., Haddox, H. K., Cox, D., Norn, C., Coventry, B., Goreshnik, I., Vafeados, D., Lee, G. R., Gordon, R., Stoddard, B. L., DiMaio, F., & Baker, D. (2025). Computational design of sequence-specific DNA-binding proteins. *Nature Structural & Molecular Biology*, 32(11), 2252–2261. PMID: 40940539

15. Hiraizumi, M., Perry, N. T., Durrant, M. G., Soma, T., Nagahata, N., Okazaki, S., Athukoralage, J. S., Isayama, Y., Pai, J. J., Pawluk, A., Konermann, S., Yamashita, K., Hsu, P. D., & Nishimasu, H. (2024). Structural mechanism of bridge RNA-guided recombination. *Nature*, 630(8018), 994–1002. PMID: 38926616

16. Hu, X., Zhang, X., Sun, W., Liu, C., Deng, P., Cao, Y., Zhang, C., Xu, N., Zhang, T., Zhang, Y. E., Liu, J. J. G., & Wang, H. (2024). Systematic discovery of DNA-binding tandem repeat proteins. *Nucleic Acids Research*, 52(17), 10464–10489. PMID: 39189466

17. Huang, P. S., Boyken, S. E., & Baker, D. (2016). The coming of age of de novo protein design. *Nature*, 537(7620), 320–327. PMID: 27629638

18. Ichikawa, D. M., Abdin, O., Alerasool, N., Kogenaru, M., Mueller, A. L., Wen, H., Giganti, D. O., Goldberg, G. W., Adams, S., Spencer, J. M., ... & Noyes, M. B. (2023). A universal deep-learning model for zinc finger design enables transcription factor reprogramming. *Nature Biotechnology*, 41(8), 1117–1129. PMID: 36702896

19. Jinek, M., Chylinski, K., Fonfara, I., Hauer, M., Doudna, J. A., & Charpentier, E. (2012). A programmable dual-RNA-guided DNA endonuclease in adaptive bacterial immunity. *Science*, 337(6096), 816–821. PMID: 22745249

20. Jumper, J., Evans, R., Pritzel, A., Green, T., Figurnov, M., Ronneberger, O., ... & Hassabis, D. (2021). Highly accurate protein structure prediction with AlphaFold. *Nature*, 596(7873), 583–589. PMID: 34265844

21. Katayama, S., Watanabe, M., Kato, Y., Nomura, W., & Yamamoto, T. (2024). Engineering of zinc finger nucleases through structural modeling improves genome editing efficiency in cells. *Advanced Science*, 11(23), e2310255. PMID: 38600709

22. Kato, K., Okazaki, S., Kannan, S., Altae-Tran, H., Demircioglu, F. E., Isayama, Y., Ishikawa, J., Fukuda, M., Macrae, R. K., Nishizawa, T., Makarova, K. S., Koonin, E. V., Zhang, F., & Nishimasu, H. (2022). Structure of the IscB-ωRNA ribonucleoprotein complex, the likely ancestor of CRISPR-Cas9. *Nature Communications*, 13(1), 6719. PMID: 36344504

23. Kim, D. Y., Lee, J. M., Moon, S. B., Chin, H. J., Park, S., Lim, Y., Kim, D., Koo, T., Ko, J. H., & Kim, Y. S. (2022). Efficient CRISPR editing with a hypercompact Cas12f1 and engineered guide RNAs delivered by adeno-associated virus. *Nature Biotechnology*, 40(1), 94–102. PMID: 34475560

24. Kortemme, T. (2024). De novo protein design — from new structures to programmable functions. *Cell*, 187(3), 526–544. PMID: 38306980

25. Kretsch, R. C., et al. (2026). Assessment of nucleic acid structure prediction in CASP16. *Proteins*, 94(1), 192–217. PMID: 41165252

26. Krishna, R., Wang, J., Ahern, W., Sturmfels, P., Venkatesh, P., Kalvet, I., Lee, G. R., Morey-Burrows, F. S., Anishchenko, I., Humphreys, I. R., ... & Baker, D. (2024). Generalized biomolecular modeling and design with RoseTTAFold All-Atom. *Science*, 384(6693), eadl2528. PMID: 38452047

27. Li, J., Chiu, T. P., & Rohs, R. (2024). Predicting DNA structure using a deep learning method. *Nature Communications*, 15(1), 1243. PMID: 38336958

28. Ma, S., Liao, K., Chen, K., Cheng, T., Yang, X., Chen, P., Li, S., Li, M., Zhang, X., Zhang, Y., Huang, T., Wang, X., Wang, L., Lin, Y., & Rong, Z. (2025). hpCasMINI: An engineered hypercompact CRISPR-Cas12f system with boosted gene editing activity. *Nature Communications*, 16(1), 5001. PMID: 40442121

29. Mao, S., Peng, W., Feng, Z., Chen, Y., Sun, J., Chen, H., Wang, P., Huang, P., Zhao, J., Wu, L., ... & Zhou, C. (2025). Design of optimized epigenetic regulators for durable gene silencing with application to PCSK9 in nonhuman primates. *Nature Biotechnology*. Advance online publication. PMID: 41034497

30. Mitra, R., Li, J., Sagendorf, J. M., Jiang, Y., Cohen, A. S., Chiu, T. P., Glasscock, C. J., & Rohs, R. (2024). Geometric deep learning of protein-DNA binding specificity. *Nature Methods*, 21(9), 1674–1683. PMID: 39103447

31. Mondal, A., Gupta, A., & Bhatt, P. (2024). Role of shape deformation of DNA-binding sites in regulating the efficiency and specificity in their recognition by DNA-binding proteins. *JACS Au*, 4(10), 3833–3846.

32. Musunuru, K., Chadwick, A. C., Mizoguchi, T., Garcia, S. P., DeNizio, J. E., Reiss, C. W., Wang, K., Iber, S., Egli, D., ... & Kathiresan, S. (2021). In vivo CRISPR base editing of PCSK9 durably lowers cholesterol in primates. *Nature*, 593(7859), 429–434. PMID: 34012082

33. Nagahata, N., Kato, K., Yamada, M., et al. (2026). Structural visualization of the molecular evolution of CRISPR-Cas9. *Nature Structural & Molecular Biology*. DOI: 10.1038/s41594-025-01743-x

34. Nishimasu, H., Ran, F. A., Hsu, P. D., Konermann, S., Shehata, S. I., Dohmae, N., Ishitani, R., Zhang, F., & Nureki, O. (2014). Crystal structure of Cas9 in complex with guide RNA and target DNA. *Cell*, 156(5), 935–949. PMID: 24529477

35. Perry, N. T., Bartie, L. J., Katrekar, D., Gonzalez, G. A., Durrant, M. G., Pai, J. J., Fanton, A., Martins, J. Q., Hiraizumi, M., Ricci-Tam, C., Nishimasu, H., Konermann, S., & Hsu, P. D. (2026). Megabase-scale human genome rearrangement with programmable bridge recombinases. *Science*, 391(6790), eadz0276. PMID: 40997214

36. Persikov, A. V., & Singh, M. (2014). De novo prediction of DNA-binding specificities for Cys2His2 zinc finger proteins. *Nucleic Acids Research*, 42(1), 97–108. PMID: 24097433

37. Ruffolo, J. A., Nayfach, S., Gallagher, J., Bhatnagar, A., Beazer, J., Hussain, R., Russ, J., Yip, J., Hill, E., Pacesa, M., Meeske, A. J., Cameron, P., & Madani, A. (2025). Design of highly functional genome editors by modelling CRISPR-Cas sequences. *Nature*, 645(8080), 518–525. PMID: 40739342

38. Saito, M., Xu, P., Faure, G., Maguire, S., Kannan, S., Altae-Tran, H., Vo, S., Desimone, A., Macrae, R. K., & Zhang, F. (2023). Fanzor is a eukaryotic programmable RNA-guided endonuclease. *Nature*, 620(7974), 660–668. PMID: 37380027

39. Schuler, G., Hu, C., & Ke, A. (2022). Structural basis for RNA-guided DNA cleavage by IscB-ωRNA and mechanistic comparison with Cas9. *Science*, 376(6600), 1476–1481. PMID: 35617371

40. Shoop, W. K., Lape, J., Trum, M., Powell, A., Sevigny, E., Mischler, A., Bacman, S. R., Fontanesi, F., Smith, J., Jantz, D., Gorsuch, C. L., & Moraes, C. T. (2023). Efficient elimination of MELAS-associated m.3243G mutant mitochondrial DNA by an engineered mitoARCUS nuclease. *Nature Metabolism*, 5(12), 2169–2183. PMID: 38036771

41. Stoddard, B. L. (2014). Homing endonucleases from mobile group I introns: Discovery to genome engineering. *Mobile DNA*, 5(1), 7. PMID: 24589358

42. Tebas, P., Stein, D., Tang, W. W., Frank, I., Wang, S. Q., Lee, G., Spratt, S. K., Surosky, R. T., Giedlin, M. A., Nichol, G., Holmes, M. C., Gregory, P. D., Ando, D. G., Kalos, M., Collman, R. G., Binder-Scholl, G., Plesa, G., Hwang, W. T., Levine, B. L., & June, C. H. (2014). Gene editing of CCR5 in autologous CD4 T cells of persons infected with HIV. *New England Journal of Medicine*, 370(10), 901–910. PMID: 24597865

43. Tremblay, F., Xiong, Q., Shah, S. S., Ko, C. W., Kelly, K., Morrison, M. S., Giancarlo, C., Ramirez, R. N., Hildebrand, E. M., Voytek, S. B., ... & Jaffe, A. B. (2025). A potent epigenetic editor targeting human PCSK9 for durable reduction of low-density lipoprotein cholesterol levels. *Nature Medicine*, 31(4), 1329–1338. PMID: 39930141

44. Watson, J. L., Juergens, D., Bennett, N. R., Trippe, B. L., Yim, J., Eisenach, H. E., Ahern, W., Borst, A. J., Ragotte, R. J., Milles, L. F., ... & Baker, D. (2023). De novo design of protein structure and function with RFdiffusion. *Nature*, 620(7976), 1089–1100. PMID: 37433327

45. Wei, Y., Gao, P., Pan, D., Li, G., Chen, Y., Li, S., Jiang, H., Yue, Y., Wu, Z., Liu, Z., Zhou, M., Chen, Y., Xu, K., Wu, Z., & Wang, X. (2026). Engineering eukaryotic transposon-encoded Fanzor2 system for genome editing in mammals. *Nature Chemical Biology*, 22(1), 48–57. PMID: 40394336

46. Willis, J. C. W., Silva-Pinheiro, P., Widdup, L., Minczuk, M., & Liu, D. R. (2022). Compact zinc finger base editors that edit mitochondrial or nuclear DNA in vitro and in vivo. *Nature Communications*, 13(1), 7204. PMID: 36418298

47. Wolfsberg, E., Paul, J. S., Tycko, J., Chen, B., Bassik, M. C., Bintu, L., Alizadeh, A. A., & Gao, X. J. (2025). Machine-guided dual-objective protein engineering for deimmunization and therapeutic functions. *Cell Systems*, 16(7), 101299. PMID: 40466641

48. Xue, N., Hong, D., Zhang, D., Wang, Q., Zhang, S., Yang, L., Chen, X., Li, Y., Han, H., Hu, C., Liu, M., Song, G., Guan, Y., Wang, L., Zhu, Y., & Li, D. (2024). Engineering IscB to develop highly efficient miniature editing tools in mammalian cells and embryos. *Molecular Cell*, 84(16), 3128–3140.e4. PMID: 39096898

49. Zekonyte, U., Bacman, S. R., Smith, J., Shoop, W., Pereira, C. V., Tomberlin, G., Stewart, J., Jantz, D., & Moraes, C. T. (2021). Mitochondrial targeted meganuclease as a platform to eliminate mutant mtDNA in vivo. *Nature Communications*, 12(1), 3210. PMID: 34050192

50. Zhou, T., Yang, L., Lu, Y., Dror, I., Dantas Machado, A. C., Ghane, T., Di Felice, R., & Rohs, R. (2013). DNAshape: A method for the high-throughput prediction of DNA structural features on a genomic scale. *Nucleic Acids Research*, 41(Web Server issue), W56–W62. PMID: 23703209

51. Maeder, M. L., & Gersbach, C. A. (2016). Genome-editing technologies for gene and cell therapy. *Molecular Therapy*, 24(3), 430–446. PMID: 26755333
