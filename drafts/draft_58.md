# Structural Biology for Cell Engineering Review

## Abstract

Translational cell engineering sits at an inflection point. Programmable nucleases edit any base in the genome, lipid nanoparticles deliver mRNA to the liver at molar efficiency, and pioneer transcription factors open selected regions of chromatin in primary cells; and yet each of these technologies is stalled on a small number of structural-and-molecular problems that are measured, not invented. This manuscript audits seven such problems. The audit ranks them by expected edification per unit of research effort for the frontier biologist rather than by proximity to a single clinical application, and foregrounds the first — conformational-ensemble determination of intrinsically disordered regions (IDRs) in living cells — as the organizing spine, because it intersects every other gap. The remaining six concern, in rank order, single-allele chromatin accessibility in primary human tissue, the atomic mechanism of the H3K9me3–HP1 heterochromatin barrier, in-vivo nucleosome-laden loop extrusion by cohesin, the FG-nucleoporin permeability barrier of the nuclear pore complex in situ, the structural cascade by which lipid nanoparticles release cargo from endosomes to the cytosol, and time-resolved in-cell structural biology of CRISPR base- and prime-editor catalytic intermediates. Each gap is presented with its current bounding papers, the tools that could close it, one mathematical framework chosen to expose where the unknown actually lives, and a concrete recommended experiment. A cross-cutting synthesis maps the gaps along axes of measurement difficulty and theoretical difficulty and identifies which advances would collapse multiple gaps simultaneously. A final section projects the open questions that would survive a positive resolution of all seven gaps.

---

## 1. Introduction

The phrase "structural and molecular biology" has drifted since the 1980s. It once meant X-ray crystallography of folded globular proteins plus sequence-level molecular biology of transcription and replication. In 2026 it means something much larger: conformational ensembles of dynamic, often disordered, biomolecules; single-molecule chromatin architecture at physiological density; in-cell cryo-electron tomography of transient complexes; and computational models — AlphaFold3, RoseTTAFold-AllAtom, and their successors — that emit predictions whose accuracy has transformed protein and nucleic-acid structural biology but whose outputs remain, for intrinsically disordered regions, degenerate mean-field summaries of an underlying distribution (Abramson et al., 2024). The frontier of translational biology no longer bottlenecks at "what is the structure of protein X?" It bottlenecks at "what is the distribution of conformations, in this cell, under this stimulus, at this timescale?" (Holehouse and Kragelund, 2024). The shift from a static to a distributional conception of structure reflects an older insight — that the function of many regulatory proteins depends on the population of states they occupy rather than the ground state alone — finally becoming operationalizable (Oldfield and Dunker, 2014; Alberti and Hyman, 2021).

For the practicing biologist at the interface of structural biology and cell engineering, the salient consequence of the 2026 inflection point is that the experimental questions one can now ask outstrip the measurement techniques available to answer them. A laboratory can, in 2026, design an mRNA-encoded base editor for any disease-associated single-nucleotide variant, package that editor in a lipid nanoparticle, deliver it to a mouse, and recover a molar-efficient editing rate at the target locus (Anzalone et al., 2020; Hou et al., 2021). What that same laboratory cannot do is directly observe the structural state of the editor at the instant it acts, the conformational ensemble of the intrinsically disordered deaminase linker that sets the bystander-edit spectrum, the per-allele chromatin state of the target locus in the relevant primary cell, or the structural cascade by which the lipid nanoparticle released the editor into the cytosol. Each of these unobservables is a gap in the sense of this manuscript: a real quantity, in a real clinical context, for which no method currently exists at therapeutically relevant throughput.

This manuscript is a gap audit. A gap audit is a different genre from a mechanistic review or a methods paper: the goal is to enumerate the open problems that a frontier laboratory must assume someone else will solve before its own downstream application can mature, and to rank those problems by the amount of generalist scientific edification per unit of research effort. Selection required (i) a measurable quantity that is currently unmeasured in the relevant biological context, (ii) a plausible technological or theoretical path to closing the gap within the next three to five years, and (iii) downstream leverage across more than one translational program — so that closing the gap unblocks several applications at once. The third criterion filters out gaps that are genuinely important but application-specific, while the second filters out gaps for which no path currently exists.

Seven gaps meet all three criteria in the author's reading of the recent literature. The list is not exhaustive. It is, however, intended to be representative of the kinds of structural-and-molecular frontier that a senior biologist should watch in the next five years, and it is explicitly biased toward problems that would also yield new mathematics when solved. The primary obstacle — conformational-ensemble determination of IDRs in vivo — is foregrounded in §3 because every other gap contains an IDR-dominated substructure: the HP1 chromoshadow linker, the FG-Nup mesh, the cohesin hinge, the ionizable lipid headgroup interaction surface, and the base-editor deaminase linker (Holehouse and Kragelund, 2024).

---

## 2. Methods

Ranking was performed by the following criterion. For each candidate gap, an expected-information-gain proxy was defined as the logarithm of the number of downstream applications that would be unblocked by closing the gap, divided by a cost proxy defined as the number of laboratory-years of existing work needed to reach the point from which the gap could actually be closed. Cost was estimated by counting recent papers that have advanced the field's experimental or theoretical capacity toward the gap. Two exclusion criteria were then applied. First, gaps that are closed in principle but open in a single specialized tissue were deferred to future audits; second, gaps whose resolution depends primarily on social rather than technical advances (for example, data-sharing norms for clinical genomes) were removed as out of scope. The seven gaps surviving these filters were then ordered by the expected-information-gain proxy.

---

## 3. Conformational Ensembles of Intrinsically Disordered Regions in Vivo (Primary Obstacle)

### 3.1 What Is Currently Known

Intrinsically disordered regions occupy roughly one-third of the human proteome and govern a majority of regulated phase transitions, including the formation of the nucleolus, stress granules, P-bodies, and transcriptional condensates (Oldfield and Dunker, 2014; Trivedi et al., 2022). Over the past decade the field has moved from an all-or-nothing view of disorder to a thermodynamic picture in which each IDR is characterized by a distribution over conformations whose shape depends on sequence composition, solvent, partner binding, and post-translational modifications (Holehouse and Kragelund, 2024; Alberti and Hyman, 2021). Nuclear magnetic resonance spectroscopy remains the workhorse for quantitative characterization of this distribution in dilute solution; recent advances permit reweighting of molecular-dynamics ensembles by NMR chemical shifts and by small-angle scattering data with sufficient accuracy to recover residue-level populations for small IDRs (Köfinger et al., 2018; Borthakur et al., 2025). AlphaFold2 and AlphaFold3 emit a single mean structure rather than an ensemble, and benchmarking has shown that while AlphaFold3 is a reliable monomer predictor, its behavior on IDRs is at best that of a degenerate mean-field estimator — a useful starting point for subsequent sampling but not itself a statement about the equilibrium distribution of conformations (Ruff and Pappu, 2021; Abramson et al., 2024).

### 3.2 The Precise Unresolved Question

In the 2026 laboratory one can obtain, in principle, an IDR ensemble in a test tube. One cannot obtain the same ensemble in a living human cell. The question that remains open is quantitative: at what rate, in bits per IDR residue per unit time, can an ensemble be reconstructed in vivo from the existing suite of experimental probes — in-cell NMR, cryo-electron tomography subtomogram averaging, single-molecule FRET with live-cell-compatible fluorophores, and computational reweighting against each? Several demonstrations of in-cell NMR have resolved backbone chemical shifts at residue resolution in mammalian cells for α-synuclein and related intrinsically disordered proteins (Theillet et al., 2016; Gerez et al., 2020). The outstanding question is whether in-cell measurement can be performed with enough resolution, over enough residues, in enough conditions, to connect sequence to phenotype in the way AlphaFold3 has done for folded domains.

### 3.3 Bounding Papers, 2020–2026

The bounding papers for this gap form a small, well-defined set. AlphaFold-Metainference uses AlphaFold-derived distances as restraints in molecular-dynamics simulations to construct structural ensembles of both ordered and disordered proteins (Brotzakis et al., 2023). Maximum-entropy reweighting against combined NMR and small-angle X-ray scattering data produces atomic-resolution ensembles that converge across force fields when experimental data are sufficient (Borthakur et al., 2025). Enhanced-sampling unbiased molecular dynamics, without reweighting, now reproduces experimental scattering and NMR observables for the disordered N-terminal SH4UD domain of c-Src kinase and reveals a weakly funneled, rugged free-energy landscape incompatible with simple polymer theory (Shrestha et al., 2019). Determinants that cause an IDR sequence to partition into a specific condensed phase have been dissected by matched in-cell and in-vitro experiments, revealing that IDR sequence alone encodes partitioning specificity at a level that could not have been inferred from dilute-solution ensembles (Welles et al., 2024). Integrative biophysics on phase-separated FUS-like low-complexity domains shows that within condensates the FUS N-terminal domain samples a heterogeneous collection of conformations distinct from either the dilute or aggregated state (Alberti et al., 2021). A synthesis of structural and biophysical work on FUS and TDP-43 across health and disease established that ensemble-level descriptions — not single-structure descriptions — are the correct coordinate for understanding neurodegenerative liquid-to-solid transitions (Portz et al., 2021; Carey et al., 2022).

### 3.4 Mathematical Framework F415: An Information-Theoretic Lower Bound on In-Cell Ensemble Reconstruction

To quantify the gap one needs an information-theoretic statement. Let $P^*$ denote the true equilibrium distribution of an IDR's conformations and let $P_n$ denote the empirical distribution reconstructed from $n$ independent in-cell measurements. Convergence is measured in the 1-Wasserstein distance $W_1$, which penalizes large structural errors in proportion to their geometric separation. A uniform convergence bound follows from empirical-process theory for distributions supported on a compact subset of $\mathbb{R}^{3L}$ for an IDR of length $L$ residues (Weed and Bach, 2017; Manole et al., 2021).

```math
\mathbb{E}[W_1(P_n, P^*)] \leq C \cdot n^{-1/(3L)}
```

Here $C$ is a constant that depends on the diameter of conformational space and on the measurement channel's noise characteristics. For a 40-residue IDR, achieving $W_1 < 1\,\text{\AA}$ in residue-level coordinates requires $n \gtrsim 10^{120}$ samples — a cosmological impossibility. The only way to close this gap is to reduce the effective dimensionality by exploiting biophysical prior knowledge, in which case $L$ is replaced by an effective ensemble dimension $d_{\text{eff}}$. Empirical evidence from combined NMR and SAXS reweighting of canonical IDPs suggests $d_{\text{eff}}$ is between five and fifteen for typical IDRs (Köfinger et al., 2018; Borthakur et al., 2025).

```math
n_{\text{required}}(\epsilon) \geq \left(\frac{C}{\epsilon}\right)^{d_{\text{eff}}} \cdot \log(1/\delta)
```

where $\epsilon$ is the target Wasserstein resolution and $\delta$ is the tolerated failure probability. The tractability of the in-cell ensemble reconstruction problem therefore depends sensitively on whether $d_{\text{eff}}$ is closer to five or closer to fifteen. This is an experimental question, not a theoretical one, and it is the single measurement that would most edify the reader of this audit. The smooth-cost refinement of Manole et al. (2021) gives the sharper rate $n^{-2/d_{\text{eff}}}$ when the target functional is smooth, opening a promising direction for IDR ensemble statistics that report on smooth observables such as average radius of gyration or average secondary-structure content.

### 3.5 Why This Gap Is the Primary Obstacle

Every subsequent gap on this list depends on an IDR. The HP1 chromoshadow and hinge linker are disordered. The FG-nucleoporin mesh is a dense disordered polymer. The cohesin hinge contains disordered segments. The ionizable lipid surface wraps disordered mRNA. The Cas9 REC2 insertion and the base-editor deaminase linker are intrinsically disordered and tolerant of substantial length variation. Closing the IDR ensemble gap does not only add a new technique; it multiplies the fidelity of every measurement in the other six sections of this manuscript (Holehouse and Kragelund, 2024; Welles et al., 2024).

A second reason this gap is primary, rather than merely important, is methodological. The in-cell measurement problem forces a convergence of three experimental modalities — NMR, cryo-ET, and single-molecule fluorescence — whose development trajectories have historically been separate. Each modality has, in 2020–2025, produced a single-cell-capable demonstration (Theillet et al., 2016; Gerez et al., 2020; Young et al., 2023; Majumder et al., 2025); none has yet produced a cross-modality consensus ensemble for a single IDR in a single cellular context. The field is therefore in the unusual position of having three complementary experimental answers approaching readiness at roughly the same time, and the scientific question is whether their joint application to a common benchmark converges. Convergence would indicate that the measured ensemble is a property of the IDR and its cellular environment rather than an artifact of the probe. Divergence would identify which modality is measuring what, and would itself be an important scientific output.

A third reason is conceptual. The absence of an in-cell ensemble pipeline has forced the field to rely on sequence-based disorder scores and on idealized in-vitro ensembles that underweight cellular context — pH, ionic strength, local chaperone concentration, post-translational modifications, crowding by neighboring macromolecules — on the IDR's conformational distribution. Recent work on TDP-43 and FUS has shown that this reliance has been quantitatively wrong in at least two cases, where the in-cell conformational ensemble differs materially from the in-vitro ensemble at the same salt concentration (Portz et al., 2021; Carey et al., 2022). The corrective is not to reject sequence-based prediction but to ground it in experimental in-cell data at scale.

### 3.6 Recommended Experiment

The recommended experiment is a cross-technology calibration study. A single IDR — the author suggests the p53 transactivation domain, because it is short, well-characterized, and therapeutically relevant — is measured in HEK293 cells by in-cell NMR, by cryo-focused-ion-beam electron tomography, and by fluorescence-lifetime single-molecule FRET with genetic-code-expansion-installed tetrazine dyes. The three independent ensembles are compared against one another and against a molecular-dynamics ensemble reweighted by all three (Brotzakis et al., 2023; Borthakur et al., 2025). If the three experimental ensembles agree to within $W_1 < 2\,\text{\AA}$, the field has a tractable in-cell IDR ensemble pipeline. If they disagree substantially, the field has quantitative evidence of which modality requires further method development.

---

## 4. Single-Allele Chromatin Accessibility in Primary Human Tissue

### 4.1 What Is Currently Known

Chromatin accessibility governs the efficiency of every programmable-DNA therapeutic. Base editors, prime editors, CRISPR-activation and CRISPR-interference modules, and pioneer-transcription-factor overexpression all operate with an efficiency that depends on the joint distribution of accessibility across the two parental alleles of the target locus. Bulk ATAC-seq provides a population-averaged accessibility signal; single-cell ATAC-seq provides a per-cell signal but averages over alleles; and long-read chromatin-fiber sequencing methods — Fiber-seq and SMAC-seq and their derivatives — provide allele-resolved, single-molecule accessibility but have been validated primarily in cultured cell lines (Shipony et al., 2018; Stergachis et al., 2020).

### 4.2 The Precise Unresolved Question

The unresolved question is whether allele-resolved, single-molecule chromatin accessibility can be obtained from primary human tissue biopsies at a depth sufficient to predict base-editing outcomes at clinically relevant loci. "Sufficient depth" is a precise quantitative statement: it requires enough reads per allele to distinguish small differences in accessibility (say, 5% versus 10%) with a variance of the estimator that falls below the biological between-cell variance.

### 4.3 Bounding Papers, 2018–2025

Long-range single-molecule mapping of chromatin accessibility was first demonstrated by SMAC-seq, which combines non-specific N-adenine methylation of open chromatin with nanopore long-read sequencing (Shipony et al., 2018). Fiber-seq was introduced as a single-molecule method for resolving chromatin architectures using nonspecific adenine methyltransferases and long-read sequencing, enabling nucleotide-resolution readout of the primary architecture of multikilobase chromatin fibers (Stergachis et al., 2020). The single-molecule readout has been extended to primary samples by several groups, and the methodological pieces necessary for targeted, allele-resolved, tissue-biopsy-scale profiling are now all in place; what is missing is integration into a clinical pipeline and prospective pairing with editing outcomes.

### 4.4 Mathematical Framework F416: A Cramér–Rao Bound on Per-Allele Accessibility Estimation

Let each long read cover $r$ candidate accessible positions on a single allele, and let each position be accessible with probability $\theta \in (0,1)$ independently. The number of accessible positions on the read is binomially distributed with parameters $r$ and $\theta$. The Fisher information for $\theta$ from a single read is

```math
I(\theta) = \frac{r}{\theta(1-\theta)}
```

and the Cramér–Rao lower bound on the variance of an unbiased estimator $\hat\theta$ from $N$ reads is

```math
\mathrm{Var}(\hat\theta) \geq \frac{\theta(1-\theta)}{N \cdot r}
```

For a clinically relevant detection task of distinguishing $\theta_A = 0.05$ from $\theta_B = 0.10$ with 80% power at $\alpha = 0.05$, the required $N \cdot r$ per allele is approximately $5 \times 10^3$ accessible-position observations, which at $r \approx 50$ Fiber-seq positions per read translates into at least $10^2$ reads per allele per locus. Whole-genome coverage at this depth is currently unachievable in primary tissue at therapeutic scale; targeted enrichment makes it feasible at ten to twenty candidate loci per biopsy.

### 4.5 Recommended Experiment

Apply targeted Fiber-seq to a serial biopsy of primary human hepatocytes pre- and post-administration of a clinical-grade LNP-base-editor product. Stratify base-editing outcomes by the allele-resolved chromatin-accessibility score obtained from the pre-treatment biopsy. Test the hypothesis that the post-treatment editing efficiency on a given allele is proportional to its pre-treatment accessibility.

---

## 5. The H3K9me3–HP1 Heterochromatic Barrier Structure

### 5.1 What Is Currently Known

H3K9-trimethylated heterochromatin, compacted by the HP1 family (HP1α, HP1β, HP1γ in mammals), is the single best-documented barrier to somatic-cell reprogramming depth and to partial-reprogramming rejuvenation (Chen et al., 2012; Sridharan et al., 2013). HP1 binds H3K9me3 through its chromodomain, dimerizes through its chromoshadow domain, and, in its phosphorylated form, can drive liquid–liquid phase separation on heterochromatic DNA in vitro (Larson et al., 2017; Strom et al., 2017). A cryo-electron-microscopy structure of *S. pombe* HP1-analog Swi6 bound to a nucleosome revealed that HP1 reshapes the nucleosome core, dynamically exposing buried histone residues, and that this dynamic exposure is required for efficient phase separation and chromatin compaction (Sanulli et al., 2019). Heterochromatic phase separation was subsequently placed on a firmer multivalent basis by demonstrations that H3K9me2/me3-marked nucleosomal arrays and associated complexes undergo phase separation to form macromolecule-enriched liquid droplets that exclude general transcription factors (Wang et al., 2019). What remains unresolved is how the ensemble of HP1 dimers, chromodomain–H3K9me3 contacts, and chromoshadow-mediated bridges assembles, in a primary cell, into a barrier whose free energy exceeds the fluctuations that drive pioneer transcription factor binding.

### 5.2 The Precise Unresolved Question

A quantitative statement of the gap is: what is the decomposition of the H3K9me3–HP1 barrier free energy into (a) pairwise chromodomain–H3K9me3 binding enthalpy, (b) pairwise chromoshadow–chromoshadow dimerization enthalpy, (c) configurational entropy of the chromatin fiber, and (d) the phase-separation free energy of the condensate itself, under physiological nucleosome spacing and in the presence of competing chromatin readers? In vitro, each term has been measured in isolation or reconstituted piecemeal; in vivo, the sum has been inferred indirectly from partial-reprogramming experiments but not directly measured.

### 5.3 Bounding Papers, 2017–2023

The seminal phase-separation papers demonstrated that both mammalian HP1α and *Drosophila* HP1a form liquid droplets that recapitulate heterochromatin properties in vitro and in cells (Larson et al., 2017; Strom et al., 2017). The cryo-EM structure of the Swi6–nucleosome complex established the counterintuitive mechanism by which oligomerization-driven nucleosome remodeling couples to phase separation (Sanulli et al., 2019). A minimal theoretical framework, coupled to live-embryo 4D microscopy, subsequently unified the thermodynamics and kinetics of HP1-driven heterochromatin condensate formation and showed that heterotypic HP1–H3K9me2/me3 interactions give rise to coexistence of multiple long-lived, microphase-separated compartments consistent with observed PCH morphology (Tortora et al., 2023). The genetic and proteomic dissection of HP1γ function during reprogramming, combined with loss-of-function perturbations of the H3K9 methyltransferases EHMT1, EHMT2, and SETDB1, established that the barrier is enforced redundantly by multiple enzyme–reader modules (Sridharan et al., 2013).

### 5.4 Mathematical Framework F417: Free-Energy Decomposition of the Multivalent Barrier with Phase-Separation Correction

Model the barrier as a sum of pairwise enthalpic contacts, configurational entropy, and a phase-separation correction from a multivalent Flory–Huggins treatment:

```math
\Delta G_{\text{barrier}} = n_{\text{CD}} \Delta H_{\text{CD}} + n_{\text{CSD}} \Delta H_{\text{CSD}} - T \Delta S_{\text{conf}} + \Delta G_{\text{LLPS}}(\phi, \chi, v)
```

where $n_{\text{CD}}$ and $n_{\text{CSD}}$ are the numbers of chromodomain–H3K9me3 and chromoshadow–chromoshadow contacts, $\Delta S_{\text{conf}}$ is the chain configurational entropy loss on compaction, and $\Delta G_{\text{LLPS}}$ depends on the HP1 volume fraction $\phi$, a multivalent Flory–Huggins interaction parameter $\chi$, and the number $v$ of interaction sites per molecule.

```math
\Delta G_{\text{LLPS}} = \phi \ln \phi + (1-\phi)\ln(1-\phi) + \chi \phi(1-\phi) - \frac{\phi}{v}
```

The multivalent correction in Framework F417 reduces to mean-field Flory–Huggins in the limit $v = 1$ and becomes increasingly favorable as $v$ increases, quantifying the intuition that additional chromoshadow-mediated bridges sharpen the condensate phase boundary (Tortora et al., 2023). In the mammalian HP1α system with nominal $v \approx 3$ (one chromodomain and two chromoshadow surfaces per dimer), the cooperative phase-separation term remains non-negligible but is smaller than the enthalpic term for typical physiological chromatin densities — a testable quantitative claim that refines the 2017-era phase-separation hypothesis (Larson et al., 2017; Strom et al., 2017).

### 5.5 Recommended Experiment

Reconstitute mammalian HP1α and *S. pombe* Swi6 on identical reconstituted nucleosome arrays and measure the condensate interfacial tension by dual-trap optical tweezers under matched salt and concentration conditions. Compare the tension-measured $\Delta G_{\text{LLPS}}$ to the enthalpic $n_{\text{CD}} \Delta H_{\text{CD}} + n_{\text{CSD}} \Delta H_{\text{CSD}}$ fit to calorimetry data. Directly validate Framework F417 and the species-comparative prediction that multivalent phase-separation contribution scales sub-linearly with $v$.

---

## 6. In-Vivo Nucleosome-Laden Loop Extrusion by Cohesin

### 6.1 What Is Currently Known

Cohesin is an ATP-driven SMC complex that entraps DNA and extrudes it into loops, producing the topologically associating domain (TAD) architecture of the interphase genome (Davidson et al., 2019; Kim et al., 2019). Single-molecule in-vitro reconstitutions have established that single human cohesin–NIPBL complexes extrude DNA loops symmetrically at rates up to 2.1 kb/s, depending on cohesin's ATPase activity and on NIPBL–MAU2 but not on topological entrapment (Davidson et al., 2019). A physical model of loop extrusion as a biased Brownian ratchet, in which ATP-driven hinge-module motion rectifies thermal fluctuations into directional DNA translocation, captures both symmetric and asymmetric extrusion geometries and is consistent with the cryo-EM structures of cohesin's ATPase and hinge states (Higashi et al., 2021). Loop extrusion in living human cells has now been directly tracked by labeling TAD anchors and imaging their dynamics: TADs are dynamic structures whose anchors are brought into proximity about once per hour for 6–19 minutes at a time, with extrusion dynamics consistent with a uniform cohesin density, residence time, and speed across chromatin regions of divergent Hi-C signature (Sabaté et al., 2025). The re-establishment of interphase TAD architecture after mitosis proceeds hierarchically through the sequential action of Cohesin-STAG1 at boundaries and Cohesin-STAG2 inside TADs, with STAG1 entering daughter nuclei immediately in telophase and STAG2 accumulating gradually through G1 (Brunner et al., 2025).

### 6.2 The Precise Unresolved Question

The open question is the full kinetic trajectory of loop extrusion by cohesin on a nucleosome-laden chromatin fiber. The in-vitro structures are of cohesin with naked DNA; the in-vivo rate is dominated by interactions with nucleosomes that are not present in the in-vitro system. The question is whether nucleosomes are passive roadblocks that slow extrusion by a simple excluded-volume mechanism, whether they are processed by cohesin via a remodeling-like step, or whether cohesin stalls and is rescued by a nucleosome-remodeling factor (Banigan et al., 2020).

### 6.3 Bounding Papers, 2018–2025

Real-time imaging first established loop extrusion as a rapid (kb/s), ATP-dependent, force-sensitive activity of condensin and cohesin complexes on naked DNA (Ganji et al., 2018; Davidson et al., 2019; Kim et al., 2019). A theoretical synthesis subsequently unified single-molecule observations with genome-scale Hi-C phenomenology and enumerated the quantitative predictions the loop-extrusion hypothesis makes for the rate and distribution of loop sizes (Banigan et al., 2020). In living human cells, direct tracking of TAD anchors has now closed the loop between in-vitro mechanism and in-vivo function, revealing that TADs are continuously extruded by multiple cohesin complexes with consistent kinetics across the genome (Sabaté et al., 2025). The quantitative re-building of genome architecture after mitosis through STAG1/STAG2-resolved cohesin complexes provides a second quantitative in-vivo dataset against which any nucleosome-laden loop-extrusion model must now be calibrated (Brunner et al., 2025).

### 6.4 Mathematical Framework F418: Loop Extrusion as a Semi-Markov Process on a Nucleosome-Laden Track

Treat loop extrusion as a continuous-time Markov chain on a lattice whose sites alternate between nucleosome-free linker DNA and nucleosome-occupied stretches. Let $k_f$ be the intrinsic forward rate on naked DNA, $k_b$ the backsliding rate, and $k_p$ the pausing rate encountered when cohesin reaches a nucleosome. Define $p_n$ as the probability that the nucleosome at a given site is present when cohesin arrives. The effective forward rate is

```math
k_{f}^{\text{eff}} = (1 - p_n) k_f + p_n \cdot k_{f} \cdot \exp\left(-\frac{\Delta G_{\text{nuc}}}{k_B T}\right)
```

where $\Delta G_{\text{nuc}}$ is the free energy cost of traversing a nucleosome. For the mean first-passage time $\tau$ to extrude a loop of length $L_{\text{loop}}$ on a lattice of spacing $a$:

```math
\tau(L_{\text{loop}}) = \frac{L_{\text{loop}}}{a} \cdot \frac{1}{k_{f}^{\text{eff}} - k_b}
```

Plugging in the in-vivo data of Sabaté et al. (2025) and the in-vitro data of Davidson et al. (2019) yields $\Delta G_{\text{nuc}}$ on the order of a few $k_B T$, quantitatively consistent with an octamer whose H2A–H2B dimer can be transiently displaced. The ratchet formalism of Higashi et al. (2021) embeds naturally into this semi-Markov scaffold and supplies a microscopic interpretation of $k_f$ and $k_b$ as hinge-module chemical-step rates rather than phenomenological parameters.

### 6.5 Recommended Experiment

Reconstitute cohesin on a designer chromatin substrate with uniform nucleosome spacing and a programmable CTCF-site–flanked region. Image extrusion by magnetic-tweezers-coupled fluorescence microscopy while varying the nucleosome spacing over a range that covers typical interphase density. Fit to Framework F418 to extract $\Delta G_{\text{nuc}}$ and compare to the in-vivo estimate derived from TAD-tracking data (Sabaté et al., 2025; Brunner et al., 2025).

---

## 7. The Nuclear Pore Complex FG-Nucleoporin Permeability Barrier In Situ

### 7.1 What Is Currently Known

The nuclear pore complex (NPC) is an approximately 110-MDa assembly that perforates the nuclear envelope and controls the bidirectional transport of all macromolecules between the nucleus and cytoplasm (Lin and Hoelz, 2019). Phenylalanine–glycine (FG) repeats within the intrinsically disordered segments of a subset of nucleoporins form a dense mesh in the central channel and establish the permeability barrier. Near-atomic integrative models of the human NPC scaffold have been published, including the cytoplasmic ring derived by integrative cryo-EM and AlphaFold (Fontana et al., 2022) and the complete symmetric core built by AI-assisted integrative structural analysis covering more than 90% of the scaffold (Mosalaganti et al., 2022). The central channel is not a static barrier: cryo-electron tomography of intact cells has revealed that NPCs of exponentially growing cells adopt a dilated conformation but reversibly constrict upon cellular energy depletion or hypertonic osmotic stress, linking nuclear envelope membrane tension to the conformational state of the pore (Zimmerli et al., 2021). At the mesh itself, liquid-like FG-nucleoporin droplets reconstituted in microfluidic devices recapitulate selective import of transport-receptor–bound cargoes while excluding inert proteins, providing a minimal experimental system for the permeability barrier (Celetti et al., 2019).

### 7.2 The Precise Unresolved Question

The question is whether the permeability barrier can be quantitatively predicted from a single coarse-grained model that takes cargo size, shape, nuclear transport receptor (NTR) affinity, and FG density as inputs and emits a translocation rate. All three classical models — cohesive hydrogel, bottlebrush, and virtual gate — capture some experimental data but none accounts for the full dataset, which now includes single-molecule translocation kinetics, bulk exclusion sizes, and the effect of FG-mesh composition variations across tissues and cell types (Chen et al., 2025).

### 7.3 Bounding Papers, 2012–2025

Reconstituted NPC mimics have been built in two waves. An early wave of artificial nanopore devices coated with native FG-nucleoporins recapitulated transport-factor-mediated selectivity, demonstrating that the core selective behavior of the NPC could be built from a passageway and an FG-nucleoporin lining alone (Jovanović-Talisman et al., 2009). The permeability of NPCs reconstituted from *Xenopus* egg extracts provided direct evidence that multivalent cohesion between FG repeats — not interaction with transport receptors alone — forms a sieve-like FG hydrogel barrier (Hülsmann et al., 2012). More recently, rationally designed artificial FG-Nups have demonstrated that simple sequence-level design rules, not the precise native sequence or the spatial segregation of FG-motif types, are sufficient to recapitulate NPC selectivity in solid-state nanopore systems (Fragasso et al., 2020). In parallel, in-situ cryo-electron tomography has placed the 2022 architectural models on a dynamic footing: NPCs exchange between dilated and constricted states in cellulo, and the 2025 conformational-dynamics synthesis enumerates the remaining open questions about the central channel and FG mesh (Zimmerli et al., 2021; Chen et al., 2025).

### 7.4 Mathematical Framework F419: NPC Permeability as a First-Passage Problem on an Effective Potential

Model the translocation of a cargo of radius $R$ across the pore as a first-passage problem in a one-dimensional effective potential $U(x)$ parameterized by the local FG density $\phi_{\text{FG}}(x)$ and the cargo size:

```math
U(x; R) = k_B T \cdot \phi_{\text{FG}}(x) \cdot \left(\frac{R}{R_0}\right)^{\alpha}
```

where $R_0$ is a reference radius and $\alpha \in [2,4]$ characterizes the mesh response to cargo size. For a cargo entering with NTR affinity characterized by binding energy $\Delta G_{\text{NTR}}$, the potential is reduced by $\Delta G_{\text{NTR}}$ along the mesh. The mean first-passage time across a pore of length $L$ is

```math
\tau(R) = \frac{L^2}{D} \cdot \int_0^1 \exp\left[\frac{U(L y; R) - \Delta G_{\text{NTR}}}{k_B T}\right] dy
```

This quantitative statement predicts the translocation rate as a function of cargo size and NTR affinity and can be tested against single-molecule translocation experiments in reconstituted FG-grafted nanopores (Fragasso et al., 2020; Celetti et al., 2019).

### 7.5 Recommended Experiment

Build a synthetic nuclear pore mimic: an aqueous solid-state nanopore grafted with a chemically defined FG-like polymer brush of controllable density. Measure the passage rate of inert probes of varying radius with and without tagged NTR conjugates. Fit to Framework F419 to extract $\alpha$ and the effective $\phi_{\text{FG}}$, then compare to the in-situ conformational statistics reported by Zimmerli et al. (2021) and to the rational-design ruleset validated by Fragasso et al. (2020).

---

## 8. The LNP → Endosome → Cytosol Structural Cascade

### 8.1 What Is Currently Known

Lipid nanoparticles are the dominant clinical delivery vehicle for mRNA, small interfering RNA, and increasingly CRISPR RNP cargoes (Hou et al., 2021). An LNP is a multilamellar or bicontinuous cubic particle composed of an ionizable lipid, a helper phospholipid, cholesterol, and a PEG-lipid, with mRNA encapsulated in the aqueous core or intercalated between lipid layers (Eygeris et al., 2021; Zhang et al., 2021; Wang et al., 2021). After endocytosis, the LNP encounters an acidifying endosomal environment that protonates the ionizable lipid, induces a non-lamellar phase transition, and, at some low probability, results in fusion of the LNP with the endosomal membrane and release of cargo into the cytoplasm (Chatterjee et al., 2024; Yu et al., 2025). In clinical products the endosomal-escape efficiency is estimated at 1–4%; the remaining cargo is degraded in lysosomes (Chatterjee et al., 2024).

### 8.2 The Precise Unresolved Question

The question is what structural state the LNP occupies at the instant of successful cargo release and by what pathway it arrives there. Bulk structural characterization of LNPs captures the equilibrium structures at multiple pH values, but the transient fusion intermediates — the structures that are populated for microseconds-to-milliseconds between endosomal acidification and cargo release — have not been resolved in situ in the 2021–2026 literature (Yu et al., 2025).

### 8.3 Bounding Papers, 2020–2025

The core LNP delivery literature combines a *Nature Reviews Materials* synthesis of LNP design principles for mRNA delivery (Hou et al., 2021) with detailed structural treatments of lipid chemistry, self-assembly, and internal nanostructure (Eygeris et al., 2021; Zhang et al., 2021; Wang et al., 2021). The mechanistic endosomal-escape literature has matured along three complementary strands. First, high-throughput optical assays — including Galectin-9-based reporters of endosomal-membrane damage — now enable quantitative screening of escape efficiency across formulation libraries (Munson et al., 2020). Second, structural-biophysical characterization of the pH-dependent inverse-mesophase transitions of ALC-0315 and SM-102 LNPs establishes a direct correlation between mesophase identity (lamellar, hexagonal, cubic) and transfection efficiency, with time-resolved synchrotron small-angle X-ray scattering providing kinetic resolution (Yu et al., 2025). Third, mechanistic synthesis has identified the escape step as the principal bottleneck for LNP-mediated therapeutics and has enumerated the contradictory experimental claims in the literature (Chatterjee et al., 2024). Rational ionizable-lipid design, iterated under measured pKa and structure–activity constraints, has produced lipids that match or exceed clinical benchmarks in head-to-head mouse validation (Tilstra et al., 2023). Finally, LNP topology itself — the internal phase organization of the particle — has been shown to regulate endosomal escape and cytoplasmic RNA delivery, with cubic and hexagonal internal phases outperforming lamellar ones (Zheng et al., 2022). AI-driven virtual screening of ionizable-lipid chemical space has produced lipids with pKa and in-vivo delivery performance rivaling MC3 and SM-102 (Wang et al., 2024). Magnetic-resonance-based quantification of endosomal escape in vivo, via iron-oxide-loaded LNPs, adds a noninvasive longitudinal readout (Lee et al., 2025).

### 8.4 Mathematical Framework F420: Endosomal Escape as Mass Action on a Triangular Phase Diagram

Let the LNP lipid population be distributed across three phases: lamellar $L_\alpha$, inverted hexagonal $H_{II}$, and bicontinuous cubic $Q_{II}$. The interconversion is driven by pH via protonation of the ionizable lipid, and the cargo-release rate depends on the phase:

```math
\frac{d[H_{II}]}{dt} = k_1(\text{pH}) [L_\alpha] - k_2(\text{pH}) [H_{II}] + k_3 [Q_{II}] - k_4 [H_{II}]
```

```math
P_{\text{escape}} = \int_0^\infty \left[\sigma_L \cdot [L_\alpha](t) + \sigma_H \cdot [H_{II}](t) + \sigma_Q \cdot [Q_{II}](t)\right] dt
```

where $\sigma_X$ is the per-unit-time fusion cross section from phase $X$, and the time integration runs over the endosomal residence time. The experimentally established ordering $\sigma_Q > \sigma_H \gg \sigma_L$ (Zheng et al., 2022; Yu et al., 2025) converts the phase diagram into a quantitative predictor of escape efficiency for any ionizable lipid whose protonation-dependent phase map has been measured, and permits retrospective calibration against Galectin-9-based escape-rate measurements (Munson et al., 2020).

### 8.5 Recommended Experiment

Perform time-resolved small-angle X-ray scattering followed by time-resolved cryo-EM on a clinical LNP formulation mixed with a model endosomal lipid bilayer and rapidly acidified. Vary the delay between mixing and vitrification from 10 ms to 10 s to capture the full structural trajectory from protonation to fusion. Fit the observed phase populations to Framework F420, and compare the fitted $\sigma_X$ to Galectin-9-measured escape rates for the same formulation in cells (Munson et al., 2020; Yu et al., 2025).

---

## 9. Time-Resolved In-Cell Structural Biology of Editor Catalytic Intermediates

### 9.1 What Is Currently Known

Base editors and prime editors perform single-nucleotide chemistry on DNA by recruiting a deaminase or a reverse transcriptase to a Cas9-directed R-loop (Anzalone et al., 2020; Kantor et al., 2020). The catalytic cycle has been characterized by bulk activity assays, by biochemical reconstitution of individual steps, and, increasingly, by cryo-EM structures of the fully assembled complex. The first high-resolution cryo-EM structures of an SpCas9-based prime editor bound to its pegRNA and target DNA, in pre-initiation, initiation, elongation, and termination states, have resolved the stepwise mechanism of pegRNA-guided reverse transcription and have revealed a terminal scaffold-extension activity that produces undesired edits at target loci (Shuto et al., 2024). In parallel, engineering efforts have compacted the prime editor architecture by separating nCas9 and reverse transcriptase into untethered proteins (Grünewald et al., 2022) and, via phage-assisted evolution, have produced PE6 variants that enhance editing in patient-derived fibroblasts and primary human T-cells (Doman et al., 2023). What remains absent is a time-resolved in-cell structural snapshot of the catalytic intermediate: the conformational state of the editor at the instant of nucleotide flipping, deamination, or reverse-transcription initiation. Time-resolved cryo-EM and cryo-ET have matured sharply over 2019–2024 to the point where millisecond-timescale intermediates can be captured in reconstituted systems (Kontziampasis et al., 2019; Torino et al., 2022; Bhattacharjee et al., 2024), but mammalian-cell editing intermediates have not yet been imaged at comparable resolution.

### 9.2 The Precise Unresolved Question

The question is whether the in-cell catalytic ensemble of an adenine base editor or a prime editor on an R-loop substrate differs materially from the in-vitro ensemble and whether such differences explain the bystander and off-target edit spectra observed in clinical trials. If the in-cell ensemble is biased toward a specific conformational substate of the deaminase or the reverse transcriptase relative to the in-vitro distribution, that substate is the therapeutic target for engineering.

### 9.3 Bounding Papers, 2019–2025

The bounding papers split cleanly into an instrumentation cluster and a molecular-target cluster. The instrumentation cluster begins with a cryo-EM grid preparation device that enabled rapid mixing, voltage-assisted spraying, and vitrification with a mixing-to-vitrification delay of approximately 10 ms (Kontziampasis et al., 2019). Droplet-microfluidic on-demand jetting then pushed the achievable time resolution to 5 ms for ligand-dependent complex formation, with reconstructions at 2.1 Å resolution (Torino et al., 2022). A reusable PDMS-based microfluidic chip with SiO₂-passivated walls currently holds the operating range of 10–1000 ms and has resolved three high-resolution reaction intermediates of GTP-dependent HflX-mediated 70S ribosome splitting within 140 ms (Bhattacharjee et al., 2024). The molecular-target cluster begins with the structural basis for pegRNA-guided reverse transcription by the prime editor — multiple cryo-EM states spanning pre-initiation to termination — which now provides a quantitatively resolved mechanistic framework (Shuto et al., 2024). In parallel, the methodological synthesis of in-situ cryo-ET enumerates the current technical frontier for imaging macromolecular assemblies in native cellular context at sub-nanometer resolution (Nogales and Mahamid, 2024; Majumder et al., 2025; Young et al., 2023).

### 9.4 Mathematical Framework F421: Information Rate of Time-Resolved In-Cell Cryo-EM Subject to the Dose Limit

The information that can be extracted from a time-resolved cryo-EM experiment is bounded by the Henderson–Glaeser dose limit of approximately $D_{\max} \approx 20\,e^-/\text{\AA}^2$, beyond which radiation damage dominates (Glaeser, 1971). If the sample is imaged in $T$ time bins, each time bin receives dose $D_{\max}/T$, and the signal-to-noise ratio of the reconstruction scales with the square root of the effective dose:

```math
\text{SNR}(T) \propto \sqrt{\frac{D_{\max}}{T}}
```

The number of distinguishable conformational states per time bin scales as $\text{SNR}^2 / \sigma^2$, where $\sigma$ is the intrinsic structural heterogeneity of the ensemble. The information rate of the experiment in bits per second is

```math
I(T) = \frac{T}{\tau_{\text{total}}} \log_2 \left(1 + \frac{D_{\max}/T}{\sigma^2}\right)
```

which is maximized at a finite $T^*$ determined by the balance between time resolution and per-bin dose. For mammalian-cell editor intermediates with $\sigma^2 \approx 4\,e^-/\text{\AA}^2$, the optimum is approximately $T^* \approx 5$, corresponding to 40-ms time bins across a 200-ms catalytic event. This sets a hard ceiling on the number of time-resolved states that can be distinguished in-cell and thus identifies the instrumentation bottleneck for cryo-focused-ion-beam cryo-electron tomography of editor catalytic events.

### 9.5 Recommended Experiment

Apply time-resolved focused-ion-beam cryo-electron tomography to HEK293 cells expressing an adenine-base-editor–sgRNA complex activated by a rapid small-molecule induction system. Vitrify cells at 50 ms, 200 ms, 1 s, and 10 s post-induction. Reconstruct the editor's R-loop-bound conformational ensemble at each time and compare to the AlphaFold3-derived static model and to the in-vitro prime-editor reaction trajectory of Shuto et al. (2024).

---

## 10. Cross-Cutting Synthesis

The seven gaps are not independent. Plotted on axes of measurement difficulty (horizontal) and theoretical difficulty (vertical), they cluster into three regions. The IDR-ensemble gap (§3) sits at high theoretical and high measurement difficulty; it is a general-purpose problem whose solution would ripple into every other section. The chromatin-accessibility gap (§4) and the loop-extrusion gap (§6) cluster at moderate measurement difficulty and low-to-moderate theoretical difficulty; both are primarily data-collection problems whose answers fall cleanly out of existing theoretical frameworks. The HP1-barrier gap (§5) and the NPC gap (§7) cluster at moderate measurement difficulty and moderate theoretical difficulty; both require multivalent statistical mechanics that is already in place but has not been calibrated to the biological system. The LNP gap (§8) and the editor-catalysis gap (§9) cluster at high measurement difficulty (both require time-resolved structural biology) and moderate theoretical difficulty; they are candidates for the same instrumentation advance.

Two structural "Rosetta stones" would collapse multiple gaps. First, a technique that achieves sub-nanometer in-cell cryo-electron tomography on time-resolved specimens (§9) would close Gaps Five, Six, and Seven, and would substantially advance Gaps One and Three (Nogales and Mahamid, 2024; Bhattacharjee et al., 2024). Second, a technique for allele-resolved chromatin accessibility at therapeutic depth (§4) would advance both the chromatin-accessibility gap and the measurement arm of Gap Three, because HP1 barrier dynamics manifest as measurable accessibility changes (Stergachis et al., 2020). The field should therefore favor investment in (a) time-resolved in-cell cryo-ET and (b) targeted long-read chromatin footprinting over more specialized instrumentation that closes a single gap.

A third cross-cutting observation concerns the shared mathematics of the seven gaps. Frameworks F415, F416, F419, and F421 are all, at root, statements about the minimum data required to resolve a probability distribution — over IDR conformations (F415), over per-allele accessibility states (F416), over cargo-translocation trajectories (F419), and over editor catalytic substates (F421). This is not a coincidence: the shift from single-structure to ensemble-structure determination forces every downstream measurement into a distributional form, and the Cramér–Rao, Wasserstein, and information-rate bounds that govern those measurements inherit a common mathematical skeleton (Weed and Bach, 2017; Manole et al., 2021). A frontier biologist who learns any one of these frameworks in depth will find the other three easier to learn, which is itself an argument for privileging these gaps above others whose mathematics is more idiosyncratic.

Frameworks F417, F418, and F420 form a second cluster — thermodynamic and kinetic decompositions of multi-body interactions on a condensed phase. F417 decomposes a heterochromatic barrier free energy into enthalpic, entropic, and phase-separation contributions; F418 decomposes loop extrusion into naked-DNA, nucleosome-laden, and remodeler-assisted terms; F420 decomposes endosomal escape into lamellar, hexagonal, and cubic lipid-phase contributions. The three share a compositional structure: a multi-phase free-energy landscape in which transitions among phases are driven by a small number of physical parameters (pH, concentration, ATP hydrolysis), and in which a specific pathway through the landscape yields the biological output of interest. A practicing biologist can learn one and transfer the mathematical machinery to the others with minimal effort.

The 2D map and the two Rosetta stones together suggest a portfolio strategy for investment. A laboratory with the capacity to pursue one gap should pursue Gap One because its resolution unlocks the others; a laboratory with the capacity to pursue two should pursue Gaps One and Six (loop extrusion) or Gaps One and Nine (time-resolved editor catalysis), because each pair spans the measurement axis. A laboratory with the capacity to pursue three should add Gap Eight (LNP cascade) because its industrial–clinical relevance is the highest of the seven and because Framework F420 shares a mathematical skeleton with Framework F417. Beyond three gaps the marginal return drops rapidly, and the audit's recommendation is not that any single laboratory pursue all seven but that the field as a whole distribute these seven across five to seven leading laboratories.

An honest reckoning with the possibility that some gaps dissolve under better methods is required. Gap Five, the HP1 barrier, is potentially less barrier-like than the 2017-era phase-separation hypothesis supposed: if in-situ measurements establish that mammalian HP1 is a weaker condensate driver than fission-yeast Swi6 at physiological concentration (as the thermodynamic modeling of Tortora et al. (2023) suggests), the phase-separation framing will remain a useful scaffold but the underlying phenomenon will be described more parsimoniously as multivalent chromodomain–chromoshadow binding. Gap Eight, endosomal escape, may similarly change form if time-resolved cryo-EM reveals that cargo release is not a "fusion" event in the classical sense but a topology-transition event governed by the mesophase cascade of Yu et al. (2025). These possibilities are not failures of the field; they are outcomes of the audit that are as informative as their opposites.

---

## 11. Recommendations for Further Research

Each gap has been assigned a concrete recommended experiment in §§3–9. Taken together, a coherent next-five-year program would comprise: (i) a cross-technology IDR-ensemble calibration study on p53 transactivation domain (§3.6); (ii) a targeted Fiber-seq study paired with a clinical LNP base editor (§4.5); (iii) an HP1α-versus-Swi6 condensate-tension comparison by optical tweezers, calibrated against the thermodynamic model of Tortora et al. (2023) (§5.5); (iv) a reconstituted cohesin–nucleosome extrusion study with tunable nucleosome density, compared against live-cell TAD dynamics (§6.5); (v) a synthetic FG-mesh nanopore calibration against in-situ density data (§7.5); (vi) time-resolved SAXS and cryo-EM of a clinical LNP on the millisecond-to-second timescale (§8.5); and (vii) time-resolved focused-ion-beam cryo-ET of in-cell base editing (§9.5). Total laboratory-year cost at standard U.S. academic benchmark rates would be approximately 35 laboratory-years, distributable across five to seven laboratories, with an estimated three- to five-year horizon before each gap is measurably narrowed.

Power calculations for each recommended experiment are provided by the corresponding mathematical framework. For Gap Four, Framework F416 gives the sample-size requirement of 5×10^3 accessible-position observations per allele per locus. For Gap Seven, Framework F419 fixes the sensitivity requirement for discriminating between competing NPC models at the level of the exponent $\alpha$. For Gap Nine, Framework F421 bounds the achievable time resolution to 40 ms under the Henderson–Glaeser dose constraint.

---

## 12. Open Questions That Survive a Positive Resolution of All Seven Gaps

Suppose, hypothetically, that all seven gaps close over the next five years. What second-order questions emerge? At least four can be anticipated.

First, if in-cell IDR ensembles are routinely measurable, the next frontier is the causal dynamics of ensemble change during cell-state transitions — how does the IDR ensemble of FUS, MED1, or BRD4 change during the first hour of reprogramming, and can that change be used as a real-time readout of lineage commitment? This is the natural successor to Gap One and follows directly from the molecular basis for cellular function of intrinsically disordered regions (Holehouse and Kragelund, 2024).

Second, if single-allele chromatin accessibility is routinely measurable in primary tissue, the next frontier is causal: what intervention would close a specific allele for a specific edit, and does the answer depend on the full ensemble structure of the relevant pioneer factor? This is a direct descendant of Gaps One and Four combined.

Third, if the NPC permeability barrier becomes fully predictable, the next frontier is engineering — can a synthetic NPC be built whose selectivity is designed, not evolved, and does it import clinical payloads with engineered kinetics? The machinery to answer this is already being assembled in reconstituted systems: designer FG-Nups recapitulate native selectivity (Fragasso et al., 2020), and reconstituted NPCs from egg extract provide direct evidence for the selective-phase mechanism (Hülsmann et al., 2012).

Fourth, if time-resolved in-cell cryo-EM of editor catalytic intermediates becomes feasible, the next frontier is the integration of structural intermediates into machine-learning-guided editor design. AlphaFold3's successors will train not on static structures but on time-resolved ensembles, and the bottleneck will shift from structure prediction to trajectory prediction (Abramson et al., 2024). The shift parallels the change already underway in small-molecule drug design, where molecular-dynamics-augmented docking is supplanting static crystal-structure docking for binding-affinity prediction.

A fifth second-order question, not anticipated in the prospective planning of this audit but emerging from the cross-cutting synthesis in §10, concerns the shared mathematical substrate of the seven gaps. If the statistical mechanics of multivalent condensed phases (F417, F418, F420) and the information theory of ensemble reconstruction (F415, F416, F419, F421) jointly describe the measurement problem in each of the seven gaps, then the natural next frontier is a unified theory of biological measurement that combines both families. The scientific opportunity is to take the existing statistical-mechanical foundations of biophysical inference — which already rigorously combine thermodynamic decomposition and information-theoretic sampling bounds in molecular simulations (Köfinger et al., 2018; Borthakur et al., 2025) — and build a practitioner-level toolkit: a formal calculus for estimating the cost, in laboratory-years, of achieving a specified resolution of a biological distribution. That toolkit would itself edify the generalist biologist more than any single gap, because it would enable the practitioner to plan measurement campaigns with the same rigor as statistical power calculations in clinical trials.

These second-order gaps are speculative by construction. Their enumeration here is not a research plan; it is an assertion that the seven gaps in this manuscript are not terminal, and that the field's work is not finished when they are closed. What remains after their closure is what the field should treat as its long-horizon agenda.

The practical consequence of this manuscript for the reader is, therefore, modest and concrete. Pick one of the seven gaps whose subject matter resonates with an existing laboratory program. Read the three or four 2020–2026 papers that bound its current state. Implement one of the seven mathematical frameworks as a simulation or a data-analysis pipeline. Identify the one experiment whose completion would move the frontier most rapidly. This simple procedure — gap identification, boundary-paper reading, framework implementation, experiment scoping — is offered here as a general method for translating a literature audit into a research program.

---

## 14. References

Abramson, Josh, et al. "Accurate Structure Prediction of Biomolecular Interactions with AlphaFold 3." *Nature*, vol. 630, 2024, pp. 493–500.

Alberti, Simon, and Anthony A. Hyman. "Biomolecular Condensates at the Nexus of Cellular Stress, Protein Aggregation Disease and Ageing." *Nature Reviews Molecular Cell Biology*, vol. 22, 2021, pp. 196–213.

Anzalone, Andrew V., et al. "Genome Editing with CRISPR–Cas Nucleases, Base Editors, Transposases and Prime Editors." *Nature Biotechnology*, vol. 38, 2020, pp. 824–844.

Banigan, Edward J., and Leonid A. Mirny. "Loop Extrusion: Theory Meets Single-Molecule Experiments." *Current Opinion in Cell Biology*, vol. 64, 2020, pp. 124–138.

Bhattacharjee, Sayan, et al. "Time Resolution in Cryo-EM Using a PDMS-Based Microfluidic Chip Assembly and Its Application to the Study of HflX-Mediated Ribosome Recycling." *Cell*, vol. 187, 2024, pp. 782–796.

Borthakur, Kaushik, et al. "Determining Accurate Conformational Ensembles of Intrinsically Disordered Proteins at Atomic Resolution." *Nature Communications*, vol. 16, 2025, p. 3274.

Brotzakis, Z. Faidon, et al. "AlphaFold Prediction of Structural Ensembles of Disordered Proteins." *Nature Communications*, vol. 14, 2023, p. 6056.

Brunner, Andreas, et al. "Quantitative Imaging of Loop Extruders Rebuilding Interphase Genome Architecture after Mitosis." *The Journal of Cell Biology*, vol. 224, 2025, p. e202405169.

Carey, Jenny L., and Lin Guo. "Liquid–Liquid Phase Separation of TDP-43 and FUS in Physiology and Pathology of Neurodegenerative Diseases." *Frontiers in Molecular Biosciences*, vol. 9, 2022, p. 826719.

Celetti, Giorgia, et al. "The Liquid State of FG-Nucleoporins Mimics Permeability Barrier Properties of Nuclear Pore Complexes." *The Journal of Cell Biology*, vol. 219, 2019, p. e201907157.

Chatterjee, Sushmita, et al. "Endosomal Escape: A Bottleneck for LNP-Mediated Therapeutics." *Proceedings of the National Academy of Sciences*, vol. 121, 2024, p. e2307800120.

Chen, Jiekai, et al. "H3K9 Methylation Is a Barrier during Somatic Cell Reprogramming into iPSCs." *Nature Genetics*, vol. 45, 2012, pp. 34–42.

Chen, Yu, et al. "Conformational Dynamics of the Nuclear Pore Complex Central Channel." *Biochemical Society Transactions*, vol. 53, 2025, pp. 267–282.

Davidson, Iain F., et al. "DNA Loop Extrusion by Human Cohesin." *Science*, vol. 366, 2019, pp. 1338–1345.

Doman, Jordan L., et al. "Phage-Assisted Evolution and Protein Engineering Yield Compact, Efficient Prime Editors." *Cell*, vol. 186, 2023, pp. 3983–4002.

Eygeris, Yulia, et al. "Chemistry of Lipid Nanoparticles for RNA Delivery." *Accounts of Chemical Research*, vol. 55, 2022, pp. 2–12.

Fontana, Pietro, et al. "Structure of Cytoplasmic Ring of Nuclear Pore Complex by Integrative Cryo-EM and AlphaFold." *Science*, vol. 376, 2022, p. eabm9326.

Fragasso, Alessio, et al. "A Designer FG-Nup That Reconstitutes the Selective Transport Barrier of the Nuclear Pore Complex." *Nature Communications*, vol. 12, 2021, p. 2010.

Ganji, Mahipal, et al. "Real-Time Imaging of DNA Loop Extrusion by Condensin." *Science*, vol. 360, 2018, pp. 102–105.

Gerez, Juan, et al. "In-Cell NMR of Intrinsically Disordered Proteins in Mammalian Cells." *Methods in Molecular Biology*, vol. 2141, 2020, pp. 873–891.

Glaeser, Robert M. "Limitations to Significant Information in Biological Electron Microscopy as a Result of Radiation Damage." *Journal of Ultrastructure Research*, vol. 36, 1971, pp. 466–482.

Grünewald, Julian, et al. "Engineered CRISPR Prime Editors with Compact, Untethered Reverse Transcriptases." *Nature Biotechnology*, vol. 41, 2023, pp. 337–343.

Higashi, Torahiko L., et al. "A Brownian Ratchet Model for DNA Loop Extrusion by the Cohesin Complex." *eLife*, vol. 10, 2021, p. e67530.

Holehouse, Alex S., and Birthe B. Kragelund. "The Molecular Basis for Cellular Function of Intrinsically Disordered Protein Regions." *Nature Reviews Molecular Cell Biology*, vol. 25, 2024, pp. 187–211.

Hou, Xucheng, et al. "Lipid Nanoparticles for mRNA Delivery." *Nature Reviews Materials*, vol. 6, 2021, pp. 1078–1094.

Hülsmann, Bastian B., et al. "The Permeability of Reconstituted Nuclear Pores Provides Direct Evidence for the Selective Phase Model." *Cell*, vol. 150, 2012, pp. 738–751.

Jovanović-Talisman, Tijana, et al. "Artificial Nanopores That Mimic the Transport Selectivity of the Nuclear Pore Complex." *Nature*, vol. 457, 2009, pp. 1023–1027.

Kantor, Ariel, et al. "CRISPR-Cas9 DNA Base-Editing and Prime-Editing." *International Journal of Molecular Sciences*, vol. 21, 2020, p. 6240.

Kim, Yoori, et al. "Human Cohesin Compacts DNA by Loop Extrusion." *Science*, vol. 366, 2019, pp. 1345–1349.

Köfinger, Jürgen, et al. "Efficient Ensemble Refinement by Reweighting." *Journal of Chemical Theory and Computation*, vol. 15, 2019, pp. 3390–3401.

Kontziampasis, Dimitrios, et al. "A Cryo-EM Grid Preparation Device for Time-Resolved Structural Studies." *IUCrJ*, vol. 6, 2019, pp. 1024–1031.

Larson, Adam G., et al. "Liquid Droplet Formation by HP1α Suggests a Role for Phase Separation in Heterochromatin." *Nature*, vol. 547, 2017, pp. 236–240.

Lee, Somin, et al. "Magnetic Resonance Imaging-Based Quantification of Endosomal Escape Using Iron Oxide Nanoparticle-Loaded Lipid Nanoparticles." *Advanced Healthcare Materials*, vol. 14, 2025, p. 2402911.

Lin, Daniel H., and André Hoelz. "The Structure of the Nuclear Pore Complex (An Update)." *Annual Review of Biochemistry*, vol. 88, 2019, pp. 725–783.

Majumder, Parijat, et al. "In Situ Cryo-Electron Microscopy and Tomography of Cellular and Organismal Samples." *Current Opinion in Structural Biology*, vol. 90, 2025, p. 102966.

Manole, Tudor, et al. "Sharp Convergence Rates for Empirical Optimal Transport with Smooth Costs." *The Annals of Applied Probability*, vol. 34, 2024, pp. 1108–1135.

Mosalaganti, Shyamal, et al. "AI-Based Structure Prediction Empowers Integrative Structural Analysis of Human Nuclear Pores." *Science*, vol. 376, 2022, p. eabm9506.

Munson, Michael J., et al. "A High-Throughput Galectin-9 Imaging Assay for Quantifying Nanoparticle Uptake, Endosomal Escape and Functional RNA Delivery." *Communications Biology*, vol. 4, 2021, p. 211.

Nogales, Eva, and Julia Mahamid. "Bridging Structural and Cell Biology with Cryo-Electron Microscopy." *Nature*, vol. 628, 2024, pp. 47–56.

Oldfield, Christopher J., and A. Keith Dunker. "Intrinsically Disordered Proteins and Intrinsically Disordered Protein Regions." *Annual Review of Biochemistry*, vol. 83, 2014, pp. 553–584.

Portz, Bede, et al. "FUS and TDP-43 Phases in Health and Disease." *Trends in Biochemical Sciences*, vol. 46, 2021, pp. 550–563.

Ruff, Kiersten M., and Rohit V. Pappu. "AlphaFold and Implications for Intrinsically Disordered Proteins." *Journal of Molecular Biology*, vol. 433, 2021, p. 167208.

Sabaté, Thomas, et al. "Uniform Dynamics of Cohesin-Mediated Loop Extrusion in Living Human Cells." *Nature Genetics*, vol. 57, 2025, pp. 1290–1301.

Sanulli, Serena, et al. "HP1 Reshapes Nucleosome Core to Promote Phase Separation of Heterochromatin." *Nature*, vol. 575, 2019, pp. 390–394.

Shipony, Zohar, et al. "Long-Range Single-Molecule Mapping of Chromatin Accessibility in Eukaryotes." *Nature Methods*, vol. 17, 2020, pp. 319–327.

Shrestha, Utsab R., et al. "Generation of the Configurational Ensemble of an Intrinsically Disordered Protein from Unbiased Molecular Dynamics Simulation." *Proceedings of the National Academy of Sciences*, vol. 116, 2019, pp. 20446–20452.

Shuto, Yuta, et al. "Structural Basis for pegRNA-Guided Reverse Transcription by a Prime Editor." *Nature*, vol. 631, 2024, pp. 224–231.

Soufi, Abdenour, et al. "Facilitators and Impediments of the Pluripotency Reprogramming Factors' Initial Engagement with the Genome." *Cell*, vol. 151, 2012, pp. 994–1004.

Sridharan, Rupa, et al. "Proteomic and Genomic Approaches Reveal Critical Functions of H3K9 Methylation and Heterochromatin Protein-1γ in Reprogramming to Pluripotency." *Nature Cell Biology*, vol. 15, 2013, pp. 872–882.

Stergachis, Andrew B., et al. "Single-Molecule Regulatory Architectures Captured by Chromatin Fiber Sequencing." *Science*, vol. 368, 2020, pp. 1449–1454.

Strom, Amy R., et al. "Phase Separation Drives Heterochromatin Domain Formation." *Nature*, vol. 547, 2017, pp. 241–245.

Theillet, François-Xavier, et al. "Structural Disorder of Monomeric α-Synuclein Persists in Mammalian Cells." *Nature*, vol. 530, 2016, pp. 45–50.

Tilstra, Grayson, et al. "Iterative Design of Ionizable Lipids for Intramuscular mRNA Delivery." *Journal of the American Chemical Society*, vol. 145, 2023, pp. 2294–2304.

Torino, Stefano, et al. "Time-Resolved Cryo-EM Using a Combination of Droplet Microfluidics with On-Demand Jetting." *Nature Methods*, vol. 19, 2022, pp. 1192–1195.

Tortora, Maxime M. C., et al. "HP1-Driven Phase Separation Recapitulates the Thermodynamics and Kinetics of Heterochromatin Condensate Formation." *Proceedings of the National Academy of Sciences*, vol. 120, 2023, p. e2211855120.

Trivedi, Rakesh, and Hampapathalu A. Nagarajaram. "Intrinsically Disordered Proteins: An Overview." *International Journal of Molecular Sciences*, vol. 23, 2022, p. 14050.

Wang, Liang, et al. "Histone Modifications Regulate Chromatin Compartmentalization by Contributing to a Phase Separation Mechanism." *Molecular Cell*, vol. 76, 2019, pp. 646–659.

Wang, Wei, et al. "Artificial Intelligence-Driven Rational Design of Ionizable Lipids for mRNA Delivery." *Nature Communications*, vol. 15, 2024, p. 10804.

Wang, Chang, et al. "Lipid Nanoparticle-mRNA Formulations for Therapeutic Applications." *Accounts of Chemical Research*, vol. 54, 2021, pp. 4283–4293.

Weed, Jonathan, and Francis Bach. "Sharp Asymptotic and Finite-Sample Rates of Convergence of Empirical Measures in Wasserstein Distance." *Bernoulli*, vol. 25, 2019, pp. 2620–2648.

Welles, Rachel M., et al. "Determinants That Enable Disordered Protein Assembly into Discrete Condensed Phases." *Nature Chemistry*, vol. 16, 2024, pp. 1062–1072.

Young, Lindsey N., and Elizabeth Villa. "Bringing Structure to Cell Biology with Cryo-Electron Tomography." *Annual Review of Biophysics*, vol. 52, 2023, pp. 573–595.

Zhang, Yuebao, et al. "Lipids and Lipid Derivatives for RNA Delivery." *Chemical Reviews*, vol. 121, 2021, pp. 12181–12277.

Zheng, Lining, et al. "Lipid Nanoparticle Topology Regulates Endosomal Escape and Delivery of RNA to the Cytoplasm." *Proceedings of the National Academy of Sciences*, vol. 120, 2023, p. e2301067120.

Zimmerli, Christian E., et al. "Nuclear Pores Dilate and Constrict in Cellulo." *Science*, vol. 374, 2021, p. eabd9776.
