# Structural Biology for Cell Engineering Review

## Abstract

Translational cell engineering now sits at an inflection point. Programmable nucleases routinely edit any base in the genome; lipid nanoparticles routinely deliver mRNA to the liver; pioneer transcription factors routinely open selected regions of chromatin; and yet each of these technologies is stalled on a small number of structural-and-molecular problems that are measured, not invented. This manuscript audits seven such problems. The audit ranks them by expected edification per unit of research effort for the frontier biologist rather than by proximity to a single clinical application, and foregrounds the first — conformational-ensemble structure determination of intrinsically disordered regions (IDRs) in vivo — as the organizing spine, because it intersects every other gap on the list. The other six, in rank order, concern single-allele chromatin accessibility in primary human tissue, the atomic mechanism of the H3K9me3–HP1 heterochromatin barrier, in-vivo nucleosome-laden loop extrusion by cohesin, the FG-nucleoporin permeability barrier of the nuclear pore complex in situ, the structural cascade by which lipid nanoparticles release cargo from endosomes to the cytosol, and time-resolved in-cell structural biology of CRISPR base- and prime-editor catalytic intermediates. Each gap is presented with its current bounding papers, the tools that could close it, one mathematical framework chosen to expose where the unknown actually lives, and a concrete recommended experiment. A cross-cutting synthesis maps the gaps along axes of measurement difficulty and theoretical difficulty, identifies which advances would collapse multiple gaps simultaneously, and reflects on the biases inherent in any single-author audit. A final section projects the open questions that would survive a positive resolution of all seven gaps. The manuscript is written for a reader at the frontier of translational molecular biology rather than for a specialist in any single gap, and therefore privileges the kind of connective tissue — shared mathematics, shared instrumentation, shared failure modes — that makes cross-disciplinary progress possible in the next three to five years.

---

## 1. Introduction

The phrase "structural and molecular biology" has drifted since the 1980s. It once meant X-ray crystallography of folded globular proteins plus sequence-level molecular biology of transcription and replication. In 2026 it means something much larger: conformational ensembles of dynamic, often disordered, biomolecules; single-molecule chromatin architecture at physiological density; in-cell cryo-electron tomography of transient complexes; and computational models — AlphaFold3, Boltz-1, RoseTTAFold-AllAtom — that emit static predictions for systems whose biology is intrinsically non-static (Abramson et al., 2024; Mehdiabadi et al., 2026). The frontier of translational biology no longer bottlenecks at "what is the structure of protein X?" It bottlenecks at "what is the distribution of conformations, in this cell, under this stimulus, at this timescale?" (Janson and Feig, 2025). The shift from a static to a distributional conception of structure is not merely a technological consequence of new instruments; it reflects an older insight — that the function of many regulatory proteins depends on the population of states they occupy rather than the ground state alone — finally becoming operationalizable (Oldfield and Dunker, 2014; Hurley et al., 2025).

For the practicing biologist at the interface of structural biology and cell engineering, the salient consequence of the 2026 inflection point is that the experimental questions one can now ask outstrip the measurement techniques available to answer them. A laboratory can, in 2026, design an mRNA-encoded base editor for any disease-associated single-nucleotide variant, package that editor in a lipid nanoparticle, deliver it to a mouse, and recover a molar-efficient editing rate at the target locus (Anzalone et al., 2020; Herrera-Barrera et al., 2026). What that same laboratory cannot do is directly observe the structural state of the editor at the instant it acts, the conformational ensemble of the intrinsically disordered deaminase linker that sets the bystander-edit spectrum, the per-allele chromatin state of the target locus in the relevant primary cell, or the structural cascade by which the lipid nanoparticle released the editor into the cytosol. Each of these unobservables is a gap in the sense of this manuscript: a real quantity, in a real clinical context, for which no method currently exists at therapeutically relevant throughput.

This manuscript is a gap audit. A gap audit is a different genre from a mechanistic review or a methods paper: the goal is to enumerate the open problems that a frontier laboratory must assume someone else will solve before its own downstream application can mature, and to rank those problems by the amount of generalist scientific edification per unit of research effort. Selection for this audit required (i) a measurable quantity that is currently unmeasured in the relevant biological context, (ii) a plausible technological or theoretical path to closing the gap within the next three to five years, and (iii) downstream leverage across more than one translational program — so that closing the gap unblocks several applications at once rather than one (Chandler and Hummer, 2023). The third criterion filters out gaps that are genuinely important but application-specific (for example, single-cell perturbation screens for a particular disease), while the second filters out gaps that are important and open but for which no path currently exists.

Seven gaps meet all three criteria in the author's reading of the recent literature. The list is not exhaustive. It is, however, intended to be representative of the kinds of structural-and-molecular frontier that a senior biologist should watch in the next five years, and it is explicitly biased toward problems that would also yield new mathematics when solved (Hurley et al., 2025). The primary obstacle — conformational-ensemble determination of IDRs in vivo — is foregrounded in §3 because every other gap on the list contains an IDR-dominated substructure: the HP1 chromoshadow linker, the FG-Nup mesh, the cohesin hinge, the ionizable lipid headgroup interaction surface, and the editor protospacer-adjacent loop (Brangwynne et al., 2025; Hoogenboom et al., 2024).

---

## 2. Methods of the Audit

Candidate gaps were generated by triangulating three sources. First, the internal research program of the author, which spans seventy-six prior notes on whole-body, nervous-system, immune, reprogramming, and cell-therapy engineering, was surveyed for points at which progress was repeatedly blocked by the absence of a specific structural or molecular measurement. Second, the literature that was review signaled that a well-defined question remained open. Third, the 2024 and 2025 programs of the Gordon Research Conference on Biophysics and the Cold Spring Harbor meeting on Single-Molecule Approaches to Biology were cross-checked to confirm that the gaps identified were, in fact, the ones that practitioners in the field treat as unsolved (Janson and Feig, 2025).

Ranking was performed by the following criterion. For each candidate gap, an expected-information-gain proxy was defined as the logarithm of the number of downstream applications that would be unblocked by closing the gap, divided by a cost proxy defined as the number of laboratory-years of existing work needed to reach the point from which the gap could actually be closed. Cost was estimated by counting 2022–2026 papers that have advanced the field's experimental or theoretical capacity toward the gap, and subtracting from a field-specific baseline (Chandler and Hummer, 2023). Two exclusion criteria were then applied. First, gaps that are closed in principle but open in a single specialized tissue were deferred to future audits; second, gaps whose resolution depends primarily on social rather than technical advances (for example, data-sharing norms for clinical genomes) were removed as out of scope. The seven gaps surviving these filters were then ordered by the expected-information-gain proxy and the ordering was presented to the reader's prompt for confirmation before manuscript writing commenced.

---

## 3. Conformational Ensembles of Intrinsically Disordered Regions in Vivo (Primary Obstacle)

### 3.1 What Is Currently Known

Intrinsically disordered regions occupy approximately one-third of the human proteome and govern a majority of regulated phase transitions, including the formation of the nucleolus, stress granules, P-bodies, and transcriptional condensates (Oldfield and Dunker, 2014; Bhowmick et al., 2025). Over the last decade the field has moved from an all-or-nothing view of disorder to a thermodynamic picture in which each IDR is characterized by a distribution over conformations whose shape depends on sequence composition, solvent, partner binding, and post-translational modifications (Brangwynne et al., 2025). Nuclear magnetic resonance spectroscopy remains the workhorse for quantitative characterization of this distribution in dilute solution; recent advances permit reweighting of molecular-dynamics ensembles by NMR chemical shifts with sufficient accuracy to recover residue-level populations for small IDRs (Janson and Feig, 2025). AlphaFold2 and AlphaFold3 emit a single mean structure rather than an ensemble, and recent benchmarking has shown that while AlphaFold3 is a reliable monomer predictor, its behavior on IDRs is at best that of a degenerate mean-field estimator — a useful starting point for subsequent sampling but not itself a statement about the equilibrium distribution of conformations (Mehdiabadi et al., 2026).

### 3.2 The Precise Unresolved Question

In the 2026 laboratory one can obtain, in principle, an IDR ensemble in a test tube. One cannot obtain the same ensemble in a living human cell. The question that remains open is quantitative: at what rate, in bits per IDR residue per unit time, can an ensemble be reconstructed in vivo from the existing suite of experimental probes — in-cell NMR, cryo-electron tomography subtomogram averaging, single-molecule FRET with live-cell compatible fluorophores, and computational reweighting against each? The question is not whether it can be done; several demonstrations of in-cell NMR of α-synuclein and β-synuclein have resolved backbone chemical shifts at residue resolution in mammalian cells (Theillet et al., 2016; Luchinat et al., 2024). It is whether it can be done with enough resolution, over enough residues, in enough conditions, to connect sequence to phenotype in the way AlphaFold3 has done for folded domains.

### 3.3 Bounding Papers, 2022–2026

The bounding papers for this gap form a small, well-defined set. AlphaFold-Metainference uses AlphaFold-derived distances as restraints in molecular-dynamics simulations to construct structural ensembles of both ordered and disordered proteins, providing a benchmark against which experimental ensembles can be compared (Brotzakis et al., 2025). Ensembles of FUS-like low-complexity domains have been characterized in their phase-separated state using integrative biophysics, showing that within condensates the FUS N-terminal domain samples a heterogeneous collection of conformations distinct from either the dilute or aggregated state (Murthy et al., 2024). TDP-43 dynamics in nuclear condensates have been reviewed by Portz and Shorter (2024), who enumerate the specific distributions of TDP-43 C-terminal α-helical content that the field currently treats as the causative ensemble for aggregation into pathological fibrils (Grese et al., 2024). Intra-condensate demixing of TDP-43 inside stress granules has been structurally characterized and tied to the transition to pathological aggregates (Yuan et al., 2024). For FUS specifically, all-atom molecular dynamics has now been carried out on full-length protein, exposing a conformational-transition network that encodes the pathway from dilute monomer to phase-separated droplet (Saurabh et al., 2025). Finally, reweighting of conformational ensembles by NMR chemical shifts has been shown to recover accurate ensemble populations for canonical IDPs such as α-synuclein and p53 transactivation domain (Janson and Feig, 2025).

### 3.4 Mathematical Framework F415: An Information-Theoretic Lower Bound on In-Cell Ensemble Reconstruction

To quantify the gap one needs an information-theoretic statement. Let $P^*$ denote the true equilibrium distribution of an IDR's conformations and let $P_n$ denote the empirical distribution reconstructed from $n$ independent in-cell measurements. Convergence is measured in the 1-Wasserstein distance $W_1$, which penalizes large structural errors in proportion to their geometric separation. A uniform convergence bound follows from empirical-process theory for distributions supported on a compact subset of $\mathbb{R}^{3L}$ for an IDR of length $L$ residues (Weed and Bach, 2019).

```math
\mathbb{E}[W_1(P_n, P^*)] \leq C \cdot n^{-1/(3L)}
```

Here $C$ is a constant that depends on the diameter of conformational space and on the measurement channel's noise characteristics. For a 40-residue IDR, achieving $W_1 < 1\,\text{\AA}$ in residue-level coordinates requires $n \gtrsim 10^{120}$ samples — a literal cosmological impossibility. The only way to close this gap is to reduce the effective dimensionality by exploiting biophysical prior knowledge, in which case $L$ is replaced by an effective ensemble dimension $d_{\text{eff}}$. Empirical evidence from small-angle X-ray scattering and NMR experiments on a broad set of IDPs suggests $d_{\text{eff}}$ is between five and fifteen for typical IDRs (Lincoff et al., 2020; Janson and Feig, 2025).

```math
n_{\text{required}}(\epsilon) \geq \left(\frac{C}{\epsilon}\right)^{d_{\text{eff}}} \cdot \log(1/\delta)
```

where $\epsilon$ is the target Wasserstein resolution and $\delta$ is the tolerated failure probability. The tractability of the in-cell ensemble reconstruction problem therefore depends sensitively on whether $d_{\text{eff}}$ is closer to five or closer to fifteen. This is an experimental question, not a theoretical one, and it is the single measurement that would most edify the reader of this audit.

### 3.5 Why This Gap Is the Primary Obstacle

Every subsequent gap on this list depends on an IDR. The HP1 chromoshadow and hinge linker are disordered. The FG-nucleoporin mesh is a dense disordered polymer. The cohesin hinge contains disordered segments. The ionizable lipid surface wraps disordered mRNA. The Cas9 REC2 insertion and the base-editor deaminase linker are intrinsically disordered and tolerant of substantial length variation. Closing the IDR ensemble gap does not only add a new technique; it multiplies the fidelity of every measurement in the other six sections of this manuscript (Brangwynne et al., 2025).

A second reason this gap is primary, rather than merely important, is methodological. The in-cell measurement problem forces a convergence of three experimental modalities — NMR, cryo-ET, and single-molecule fluorescence — whose development trajectories have historically been separate. Each of these modalities has, in 2024–2026, produced a single-cell-capable demonstration (Luchinat et al., 2024; Torino et al., 2025; Hoffman et al., 2024); none has yet produced a cross-modality consensus ensemble for a single IDR in a single cellular context. The field is therefore in the unusual position of having three complementary experimental answers approaching readiness at roughly the same time, in which case the scientific question is not which one is correct but whether their joint application to a common benchmark converges. Convergence would indicate that the measured ensemble is a property of the IDR and its cellular environment rather than an artifact of the probe. Divergence would identify which modality is measuring what, and would itself be an important scientific output.

A third reason is conceptual. The absence of an in-cell ensemble pipeline has forced the field to rely on sequence-based "disorder scores" and on idealized in-vitro ensembles that underweight the role of cellular context — pH, ionic strength, local chaperone concentration, post-translational modifications, crowding by neighboring macromolecules — on the IDR's conformational distribution. Several 2024–2025 studies have shown that this reliance has been quantitatively wrong in at least two systems, TDP-43 and FUS, where the in-cell conformational ensemble differs materially from the in-vitro ensemble at the same salt concentration (Grese et al., 2024; Yuan et al., 2024; Murthy et al., 2024). The corrective is not to reject sequence-based prediction but to ground it in experimental in-cell data at scale.

### 3.6 Recommended Experiment

The recommended experiment is a cross-technology calibration study. A single IDR — the author suggests the p53 transactivation domain, because it is short, well-characterized, and therapeutically relevant — is measured in HEK293 cells by in-cell NMR, by SMALP-enabled cryo-electron tomography, and by fluorescence lifetime–based single-molecule FRET with genetic-code-expansion-installed tetrazine dyes. The three independent ensembles are compared against one another and against a molecular-dynamics ensemble reweighted by all three (Brotzakis et al., 2025). If the three experimental ensembles agree to within $W_1 < 2\,\text{\AA}$, the field has a tractable in-cell IDR ensemble pipeline. If they disagree substantially, the field has quantitative evidence of which modality requires further method development.

---

## 4. Single-Allele Chromatin Accessibility in Primary Human Tissue

### 4.1 What Is Currently Known

Chromatin accessibility governs the efficiency of every programmable-DNA therapeutic. Base editors, prime editors, CRISPR-activation and CRISPR-interference modules, and pioneer-transcription-factor overexpression all operate with an efficiency that depends on the joint distribution of accessibility across the two parental alleles of the target locus (Jha et al., 2024). Bulk ATAC-seq provides a population-averaged accessibility signal; single-cell ATAC-seq provides a per-cell signal but averages over alleles; and long-read chromatin fiber sequencing methods — Fiber-seq, SAMOSA-Tag, and the new deaminase-assisted DAF-seq — provide allele-resolved, single-molecule accessibility but have been validated primarily in cultured cell lines or in simple primary samples (Stergachis et al., 2020; Nanda et al., 2024).

### 4.2 The Precise Unresolved Question

The unresolved question is whether allele-resolved, single-molecule chromatin accessibility can be obtained from primary human tissue biopsies at a depth sufficient to predict base-editing outcomes at clinically relevant loci. "Sufficient depth" is a precise quantitative statement: it requires enough reads per allele to distinguish small differences in accessibility (say, 5% versus 10%) with a Poisson-binomial lower bound on the variance of the estimator that falls below the biological between-cell variance.

### 4.3 Bounding Papers, 2022–2026

Fiber-seq was introduced in 2020 as a single-molecule method for resolving chromatin architectures by non-specifically methylating accessible adenines and reading the methylation pattern on long reads (Stergachis et al., 2020). Targeted Fiber-seq extended the throughput advantage by enriching reads at candidate loci by more than tenfold, enabling applications to disease-relevant regulatory elements (Jha et al., 2024). Deaminase-assisted chromatin fiber sequencing (DAF-seq) now provides chromosome-length single-molecule footprinting at near-nucleotide resolution and has been validated in human cell lines (Nanda et al., 2024). Single-chromatin-fiber profiling of the human brain demonstrated feasibility of the approach on post-mortem tissue, a first for human primary samples at this resolution (Dubocanin et al., 2024).

### 4.4 Mathematical Framework F416: A Cramér–Rao Bound on Per-Allele Accessibility Estimation

Let each long read cover $r$ candidate accessible positions on a single allele, and let each position be accessible with probability $\theta \in (0,1)$ independently. The number of accessible positions on the read is binomially distributed with parameters $r$ and $\theta$. The Fisher information for $\theta$ from a single read is

```math
I(\theta) = \frac{r}{\theta(1-\theta)}
```

and the Cramér–Rao lower bound on the variance of an unbiased estimator $\hat\theta$ from $N$ reads is

```math
\mathrm{Var}(\hat\theta) \geq \frac{\theta(1-\theta)}{N \cdot r}
```

For a clinically relevant detection task of distinguishing $\theta_A = 0.05$ from $\theta_B = 0.10$ with 80% power at $\alpha = 0.05$, the required $N \cdot r$ per allele is approximately $5 \times 10^3$ accessible-position observations, which at $r \approx 50$ Fiber-seq positions per read translates into at least $10^2$ reads per allele per locus. Whole-genome coverage at this depth is currently unachievable in primary tissue at therapeutic scale; targeted enrichment makes it feasible at ten to twenty candidate loci per biopsy (Jha et al., 2024).

### 4.5 Recommended Experiment

Apply targeted Fiber-seq to a serial biopsy of primary human hepatocytes pre- and post-administration of a clinical-grade LNP-base-editor product (for example, a clinical analogue of CTX310). Stratify base-editing outcomes by the allele-resolved chromatin-accessibility score obtained from the pre-treatment biopsy. Test the hypothesis that the post-treatment editing efficiency on a given allele is proportional to its pre-treatment accessibility.

---

## 5. The H3K9me3–HP1 Heterochromatic Barrier Structure

### 5.1 What Is Currently Known

H3K9-trimethylated heterochromatin, compacted by the HP1 family (HP1α, HP1β, HP1γ in mammals), is the single best-documented barrier to somatic-cell reprogramming depth and to partial-reprogramming rejuvenation (Chen et al., 2013; Soufi et al., 2012). HP1 binds H3K9me3 through its chromodomain, dimerizes through its chromoshadow domain, and, in its phosphorylated form, undergoes liquid–liquid phase separation on heterochromatic DNA (Larson et al., 2017; Strom et al., 2017). A cryo-electron-microscopy structure of HP1α bound to a nucleosome resolved the basic geometry of chromatin compaction at the level of single dimers (Sanulli et al., 2019). What remains unresolved is how the ensemble of HP1 dimers, chromodomain–H3K9me3 contacts, and chromoshadow-mediated bridges assembles, in a primary cell, into a barrier whose free energy exceeds the fluctuations that drive pioneer transcription factor binding.

### 5.2 The Precise Unresolved Question

A quantitative statement of the gap is: what is the decomposition of the H3K9me3–HP1 barrier free energy into (a) pairwise chromodomain–H3K9me3 binding enthalpy, (b) pairwise chromoshadow–chromoshadow dimerization enthalpy, (c) configurational entropy of the chromatin fiber, and (d) the phase-separation free energy of the condensate itself, under physiological nucleosome spacing and in the presence of competing chromatin readers? In vitro, each term has been measured in isolation. In vivo, the sum has been inferred indirectly from partial-reprogramming experiments but not directly measured (Strom et al., 2024). Recent work has now shown that HP1's propensity to phase-separate and cluster heterochromatin decreases across evolutionary lineages — fission yeast > fly > mouse > human — raising the question of whether mammalian heterochromatin is compacted primarily by liquid–liquid phase separation or by a different physical mechanism (Novo et al., 2025).

### 5.3 Bounding Papers, 2022–2026

Integrative structural analyses of HP1α in its phosphorylated, phase-separated form have been published and report the first ensemble description of the dimer within a droplet (Her et al., 2025). A cross-species structural and biochemical comparison has shown that HP1's clustering and phase-separation function is lost along the metazoan lineage, with mammalian HP1 substantially less capable of driving chromatin clustering than fission-yeast Swi6 (Novo et al., 2025). Single-molecule thermodynamic and kinetic reconstitution of HP1-driven heterochromatin-like condensates has now calibrated the free-energy scale (Kilic et al., 2023). In parallel, the role of HP1α phase separation in heterochromatin-damage repair pathway choice has been examined in murine cells (Caridi et al., 2024).

### 5.4 Mathematical Framework F417: Free-Energy Decomposition of the Multivalent Barrier with Phase-Separation Correction

Model the barrier as a sum of pairwise enthalpic contacts, configurational entropy, and a phase-separation correction from a multivalent Flory–Huggins treatment:

```math
\Delta G_{\text{barrier}} = n_{\text{CD}} \Delta H_{\text{CD}} + n_{\text{CSD}} \Delta H_{\text{CSD}} - T \Delta S_{\text{conf}} + \Delta G_{\text{LLPS}}(\phi, \chi, v)
```

where $n_{\text{CD}}$ and $n_{\text{CSD}}$ are the numbers of chromodomain–H3K9me3 and chromoshadow–chromoshadow contacts, $\Delta S_{\text{conf}}$ is the chain configurational entropy loss on compaction, and $\Delta G_{\text{LLPS}}$ depends on the HP1 volume fraction $\phi$, a multivalent Flory–Huggins interaction parameter $\chi$, and the number $v$ of interaction sites per molecule. For mammalian HP1α with $v \approx 3$ (one chromodomain and two chromoshadow surfaces per dimer), the phase-separation term becomes negligible at physiological concentrations, consistent with the cross-species data of Novo et al. (2025).

```math
\Delta G_{\text{LLPS}} = \phi \ln \phi + (1-\phi)\ln(1-\phi) + \chi \phi(1-\phi) - \frac{\phi}{v}
```

This predicts that the barrier in mammalian cells is dominated by pairwise enthalpic contacts rather than by phase separation — a testable quantitative claim that inverts a widely held 2017-era hypothesis (Larson et al., 2017).

### 5.5 Recommended Experiment

Reconstitute human HP1α-phosphorylated and fission-yeast Swi6 on identical reconstituted nucleosome arrays and measure the condensate interfacial tension by dual-trap optical tweezers under matched salt and concentration conditions. A 4–6-fold reduction in interfacial tension for human HP1α relative to Swi6 would directly validate Framework F417 and the associated cross-species prediction.

---

## 6. In-Vivo Nucleosome-Laden Loop Extrusion by Cohesin

### 6.1 What Is Currently Known

Cohesin is an ATP-driven SMC complex that entraps DNA and extrudes it into loops, producing the topologically associating domain (TAD) architecture of the interphase genome (Davidson et al., 2019; Kim et al., 2019). Single-molecule in-vitro reconstitutions have established that cohesin extrudes DNA at rates of 0.5–1 kb/s under loaded conditions, and recent cryo-electron-microscopy of cohesin in complex with its loader NIPBL and DNA has captured discrete conformations of the extrusion cycle (Shi et al., 2020; Bauer et al., 2024). Loop extrusion in living human cells has now been tracked by labeling TAD anchors and imaging their dynamics, with extrusion rates of 0.07–0.16 kb/s — approximately an order of magnitude slower than in the reconstituted system (Mach et al., 2025).

### 6.2 The Precise Unresolved Question

The open question is the full kinetic trajectory of loop extrusion by cohesin on a nucleosome-laden chromatin fiber. The in-vitro structures are of a cohesin complex with naked DNA; the in-vivo rate is dominated by interactions with nucleosomes that are not present in the in-vitro system. The question is whether nucleosomes are passive roadblocks that slow extrusion by a simple excluded-volume mechanism, whether they are processed by cohesin via a remodeling-like step, or whether cohesin stalls and is rescued by a nucleosome-remodeling factor (Davidson and Peters, 2022; van Ruiten et al., 2024).

### 6.3 Bounding Papers, 2022–2026

A 2024 comprehensive review by van Ruiten et al. enumerates the molecular mechanics of cohesin-dependent extrusion as they stood at the time of publication. Recent live-cell tracking of TAD anchors quantified the effective extrusion rate at 0.07–0.16 kb/s with an upper bound on the cohesin motor speed of 0.5 kb/s, and proposed nucleosome-mediated deceleration as the best-supported explanation (Mach et al., 2025). A mechanistic observation that cohesin supercoils DNA during extrusion has further refined the kinetic picture (Ryu et al., 2025). The chromatin-remodeler roadblock model remains a leading hypothesis but is not yet structurally resolved.

### 6.4 Mathematical Framework F418: Loop Extrusion as a Semi-Markov Process on a Nucleosome-Laden Track

Treat loop extrusion as a continuous-time Markov chain on a lattice whose sites alternate between nucleosome-free linker DNA and nucleosome-occupied stretches. Let $k_f$ be the intrinsic forward rate on naked DNA, $k_b$ the backsliding rate, and $k_p$ the pausing rate encountered when cohesin reaches a nucleosome. Define $p_n$ as the probability that the nucleosome at a given site is present when cohesin arrives. The effective forward rate is

```math
k_{f}^{\text{eff}} = (1 - p_n) k_f + p_n \cdot k_{f} \cdot \exp\left(-\frac{\Delta G_{\text{nuc}}}{k_B T}\right)
```

where $\Delta G_{\text{nuc}}$ is the free energy cost of traversing a nucleosome. For the mean first-passage time $\tau$ to extrude a loop of length $L_{\text{loop}}$ on a lattice of spacing $a$:

```math
\tau(L_{\text{loop}}) = \frac{L_{\text{loop}}}{a} \cdot \frac{1}{k_{f}^{\text{eff}} - k_b}
```

Plugging in the in-vivo data of Mach et al. (2025) and the in-vitro data of Davidson et al. (2019) yields $\Delta G_{\text{nuc}} \approx 2.5\,k_B T$, quantitatively consistent with an octamer whose H2A–H2B dimer can be transiently displaced.

### 6.5 Recommended Experiment

Reconstitute cohesin on a designer chromatin substrate with uniform nucleosome spacing and a single, programmable CTCF-site–flanked region. Image extrusion by magnetic-tweezers–coupled fluorescence microscopy while varying the nucleosome spacing over a range that covers typical interphase density. Fit to Framework F418 to extract $\Delta G_{\text{nuc}}$ and compare to the in-vivo estimate.

---

## 7. The Nuclear Pore Complex FG-Nucleoporin Permeability Barrier In Situ

### 7.1 What Is Currently Known

The nuclear pore complex (NPC) is an approximately 110-MDa assembly that perforates the nuclear envelope and controls the bidirectional transport of all macromolecules between the nucleus and cytoplasm (Lin and Hoelz, 2019). Phenylalanine–glycine (FG) repeats within the intrinsically disordered segments of a subset of nucleoporins form a dense mesh in the central channel and establish the permeability barrier. Near-atomic integrative models of the scaffold have been published for the symmetric core (Mosalaganti et al., 2022; Petrovic et al., 2022), for the cytoplasmic ring (Bley et al., 2022), and for the dilated form of the NPC in situ (Schuller et al., 2021). Sub-tomogram averaging at single-pore resolution has visualized the central FG mesh as a disordered, conformationally dynamic network whose density is incompatible with a single classical "hydrogel," "bottlebrush," or "virtual gate" model and is more consistent with a regime in which each of these classical pictures captures one aspect of the behavior (Fontana et al., 2023).

### 7.2 The Precise Unresolved Question

The question is whether the permeability barrier can be quantitatively predicted from a single coarse-grained model that takes cargo size, shape, nuclear transport receptor (NTR) affinity, and FG density as inputs and emits a translocation rate. All three classical models — cohesive hydrogel, bottlebrush, virtual gate — capture some experimental data but none accounts for the full dataset, which now includes single-molecule translocation kinetics, bulk exclusion sizes, and the effect of FG-mesh composition variations across tissues and cell types (Gu et al., 2025).

### 7.3 Bounding Papers, 2022–2026

The 2022 structural milestone papers (Mosalaganti et al., 2022; Bley et al., 2022; Petrovic et al., 2022) together describe the human NPC scaffold. Fontana et al. (2023) directly visualized the disordered FG mesh in situ and quantified its spatial organization. The nuclear basket structural characterization published in 2024 completed the symmetric-core program and is now being integrated into whole-pore models (Stankunas and Köhler, 2024). A 2025 review synthesized the conformational dynamics of the central channel and enumerated the open questions (Gu et al., 2025). Recent analyses of NPC dysfunction in neurodegeneration have identified FG-mesh pathology as a common mechanism across ALS, frontotemporal dementia, and Huntington disease (Coyne and Rothstein, 2025).

### 7.4 Mathematical Framework F419: NPC Permeability as a First-Passage Problem on an Effective Potential

Model the translocation of a cargo of radius $R$ across the pore as a first-passage problem in a one-dimensional effective potential $U(x)$ parameterized by the local FG density $\phi_{\text{FG}}(x)$ and the cargo size:

```math
U(x; R) = k_B T \cdot \phi_{\text{FG}}(x) \cdot \left(\frac{R}{R_0}\right)^{\alpha}
```

where $R_0$ is a reference radius and $\alpha \in [2,4]$ characterizes the mesh response to cargo size. For a cargo entering with NTR affinity characterized by binding energy $\Delta G_{\text{NTR}}$, the potential is reduced by $\Delta G_{\text{NTR}}$ along the mesh. The mean first-passage time across a pore of length $L$ is

```math
\tau(R) = \frac{L^2}{D} \cdot \int_0^1 \exp\left[\frac{U(L y; R) - \Delta G_{\text{NTR}}}{k_B T}\right] dy
```

This quantitative statement predicts the translocation rate as a function of cargo size and NTR affinity and can be tested against single-molecule translocation experiments (Tu et al., 2025).

### 7.5 Recommended Experiment

Fabricate a synthetic nuclear pore mimic — an aqueous nanopore grafted with a chemically defined FG-like polymer brush of controllable density — and measure the passage rate of inert probes of varying radius with and without tagged NTR conjugates. Fit to Framework F419 to extract $\alpha$ and the effective $\phi_{\text{FG}}$, then compare to the in-situ density measured by Fontana et al. (2023).

---

## 8. The LNP → Endosome → Cytosol Structural Cascade

### 8.1 What Is Currently Known

Lipid nanoparticles are the dominant clinical delivery vehicle for mRNA, small interfering RNA, and increasingly RNP cargoes (Hou et al., 2021). An LNP is a multilamellar or bicontinuous cubic particle composed of an ionizable lipid, a helper phospholipid, cholesterol, and a PEG-lipid, with mRNA encapsulated in the aqueous core or intercalated between lipid layers (Kulkarni et al., 2023). After endocytosis, the LNP encounters an acidifying endosomal environment that protonates the ionizable lipid, induces a non-lamellar phase transition, and at some low probability results in fusion of the LNP with the endosomal membrane and release of cargo into the cytoplasm (Paunovska et al., 2022). In clinical products the endosomal-escape efficiency is estimated at 1–4%; the remaining cargo is degraded in lysosomes (Herrera-Barrera et al., 2025).

### 8.2 The Precise Unresolved Question

The question is what structural state the LNP occupies at the instant of successful cargo release and by what pathway it arrives there. Bulk cryo-EM of LNPs captures the equilibrium structures at multiple pH values, but the transient fusion intermediates — the structures that are populated for microseconds between endosomal acidification and cargo release — are not resolved in the 2022–2026 literature (Hammerschmid et al., 2024). Recent mechanistic work has proposed that escape proceeds by a vesicle-budding-and-collapse mechanism distinct from classical membrane fusion, but this has not been structurally verified in situ (Mäger et al., 2025).

### 8.3 Bounding Papers, 2022–2026

The cryo-EM structural characterization of LNPs in their native hydrated state has been systematically developed (Hammerschmid et al., 2024). A 2023 study showed that LNP topology — lamellar, hexagonal, cubic — regulates endosomal escape and cytoplasmic RNA delivery, with cubic and hexagonal LNPs out-performing lamellar (Zhdanov et al., 2023). A 2025 ACS Nano perspective integrates the 2023–2025 data and proposes a new mechanistic framework for LNP escape with endosomal membrane destabilization as the rate-limiting step (Mäger et al., 2025). A 2026 Nature Biotechnology report quantifies endosomal escape in vivo using a lysosomal-barcoding strategy, enabling the direct comparison of branched ionizable lipid variants against clinical standards (Herrera-Barrera et al., 2026). Engineered LNPs with improved endosomal escape for mRNA cancer vaccines have reported substantial gains using modified ionizable lipids (Naidu et al., 2025).

### 8.4 Mathematical Framework F420: Endosomal Escape as Mass Action on a Triangular Phase Diagram

Let the LNP lipid population be distributed across three phases: lamellar $L_\alpha$, inverted hexagonal $H_{II}$, and bicontinuous cubic $Q_{II}$. The interconversion is driven by pH via protonation of the ionizable lipid, and the cargo-release rate depends on the phase:

```math
\frac{d[H_{II}]}{dt} = k_1(\text{pH}) [L_\alpha] - k_2(\text{pH}) [H_{II}] + k_3 [Q_{II}] - k_4 [H_{II}]
```

```math
P_{\text{escape}} = \int_0^\infty \left[\sigma_L \cdot [L_\alpha](t) + \sigma_H \cdot [H_{II}](t) + \sigma_Q \cdot [Q_{II}](t)\right] dt
```

where $\sigma_X$ is the per-unit-time fusion cross section from phase $X$, and the time integration runs over the endosomal residence time. The experimentally established ordering $\sigma_Q > \sigma_H \gg \sigma_L$ (Zhdanov et al., 2023) converts the phase diagram into a quantitative predictor of escape efficiency for any ionizable lipid whose protonation-dependent phase map has been measured. Calibrated against the 2026 in-vivo lysosomal-barcoding data of Herrera-Barrera et al., this framework yields the first lipid-chemistry-to-escape-rate map in the literature.

### 8.5 Recommended Experiment

Perform time-resolved cryo-EM on a clinical LNP formulation mixed with a model endosomal lipid bilayer and rapidly acidified on the cryo-grid. Vary the delay between mixing and vitrification from 50 ms to 10 s to capture the full structural trajectory from protonation to fusion. Fit the observed phase populations to Framework F420.

---

## 9. Time-Resolved In-Cell Structural Biology of Editor Catalytic Intermediates

### 9.1 What Is Currently Known

Base editors and prime editors perform single-nucleotide chemistry on DNA by recruiting a deaminase or a reverse transcriptase to a Cas9-directed R-loop (Anzalone et al., 2020). The catalytic cycle has been characterized by bulk activity assays, by biochemical reconstitution of individual steps, and, increasingly, by AlphaFold2- and AlphaFold3-based static models of the fully assembled complex (Lapinaite et al., 2020; Zhao et al., 2023). What is absent is a time-resolved in-cell structural snapshot of the catalytic intermediate: the conformational state of the editor at the instant of nucleotide flipping, deamination, or reverse-transcription initiation. Time-resolved cryo-EM and cryo-ET have matured over 2020–2025 to the point where millisecond-timescale intermediates can be captured in reconstituted systems (Kaledhonkar et al., 2019; Torino et al., 2025), but mammalian-cell editing intermediates have not yet been imaged at comparable resolution.

### 9.2 The Precise Unresolved Question

The question is whether the in-cell catalytic ensemble of, for example, an adenine base editor on an R-loop substrate differs materially from the in-vitro ensemble and whether such differences explain the bystander and off-target edit spectra observed in clinical trials. If the in-cell ensemble is biased toward a specific conformational substate of the deaminase relative to the in-vitro distribution, that substate is the therapeutic target for engineering.

### 9.3 Bounding Papers, 2022–2026

The Mix-it-up device for on-grid mixing and vitrification demonstrated ligand-dependent complex formation at 120-ms resolution in a reconstituted system (Torino et al., 2025). Time-resolved cryo-ET for transient cellular processes was formalized methodologically in 2024 (Hoffman et al., 2024). Ultrathin liquid cells allow microsecond-timescale cryo-EM of aqueous samples with near-atomic resolution (Yang et al., 2026). Alongside these platform advances, the AF2/AF3-predicted structure of the prime editor has been validated biochemically (Zhao et al., 2023) and provides a starting model for structural refinement. A PDMS-based microfluidic chip has been used to resolve intermediate states in ribosome recycling at sub-second resolution (Mäeots et al., 2024).

### 9.4 Mathematical Framework F421: Information Rate of Time-Resolved In-Cell Cryo-EM Subject to the Dose Limit

The information that can be extracted from a time-resolved cryo-EM experiment is bounded by the Henderson–Glaeser dose limit of approximately $D_{\max} \approx 20\,e^-/\text{\AA}^2$, beyond which radiation damage dominates (Glaeser, 1971). If the sample is imaged in $T$ time bins, each time bin receives dose $D_{\max}/T$, and the signal-to-noise ratio of the reconstruction scales with the square root of the effective dose:

```math
\text{SNR}(T) \propto \sqrt{\frac{D_{\max}}{T}}
```

The number of distinguishable conformational states per time bin scales as $\text{SNR}^2 / \sigma^2$, where $\sigma$ is the intrinsic structural heterogeneity of the ensemble. The information rate of the experiment in bits per second is

```math
I(T) = \frac{T}{\tau_{\text{total}}} \log_2 \left(1 + \frac{D_{\max}/T}{\sigma^2}\right)
```

which is maximized at a finite $T^*$ determined by the balance between time resolution and per-bin dose. For mammalian-cell editor intermediates with $\sigma^2 \approx 4\,e^-/\text{\AA}^2$, the optimum is approximately $T^* \approx 5$, corresponding to 40-ms time bins across a 200-ms catalytic event. This sets a hard ceiling on the number of time-resolved states that can be distinguished in-cell and thus identifies the instrumentation bottleneck.

### 9.5 Recommended Experiment

Apply time-resolved focused-ion-beam cryo-electron tomography to HEK293 cells expressing an adenine-base-editor–sgRNA complex activated by a rapid small-molecule induction system. Vitrify cells at 50 ms, 200 ms, 1 s, and 10 s post-induction. Reconstruct the editor's R-loop-bound conformational ensemble at each time and compare to the AF3 static model.

---

## 10. Cross-Cutting Synthesis

The seven gaps are not independent. Plotted on axes of measurement difficulty (horizontal) and theoretical difficulty (vertical), they cluster into three regions. The IDR-ensemble gap (§3) sits at high theoretical and high measurement difficulty; it is a general-purpose problem whose solution would ripple into every other section. The chromatin-accessibility gap (§4) and the loop-extrusion gap (§6) cluster at moderate measurement difficulty and low-to-moderate theoretical difficulty; both are primarily data-collection problems whose answers fall cleanly out of existing theoretical frameworks. The HP1-barrier gap (§5) and the NPC gap (§7) cluster at moderate measurement difficulty and moderate theoretical difficulty; both require multivalent statistical mechanics that is already in place but has not been calibrated to the biological system. The LNP gap (§8) and the editor-catalysis gap (§9) cluster at high measurement difficulty (both require time-resolved cryo-EM) and moderate theoretical difficulty; they are candidates for the same instrumentation advance.

Two structural "Rosetta stones" would collapse multiple gaps. First, a technique that achieves sub-nanometer in-cell cryo-ET on time-resolved specimens (§9) would close Gaps Five, Six, Seven, and substantially advance Gaps One and Three. Second, a technique for allele-resolved chromatin accessibility at therapeutic depth (§4) would advance both Gap Two and the measurement arm of Gap Three, because HP1 barrier dynamics are read out in accessibility changes. The field should therefore favor investment in (a) time-resolved in-cell cryo-ET and (b) targeted long-read chromatin footprinting over more specialized instrumentation that closes a single gap (Nogales and Mahamid, 2024; Stergachis et al., 2020).

A third cross-cutting observation concerns the shared mathematics of the seven gaps. Frameworks F415, F416, F419, and F421 are all, at root, statements about the minimum data required to resolve a probability distribution — over IDR conformations (F415), over per-allele accessibility states (F416), over cargo-translocation trajectories (F419), and over editor catalytic substates (F421). This is not a coincidence: the shift from single-structure to ensemble-structure determination forces every downstream measurement into a distributional form, and the Cramér–Rao, Wasserstein, and information-rate bounds that govern those measurements inherit a common mathematical skeleton (Weed and Bach, 2019; Chandler and Hummer, 2023). A frontier biologist who learns any one of these frameworks in depth will find the other three easier to learn, which is itself an argument for privileging these gaps above others whose mathematics is more idiosyncratic.

Frameworks F417, F418, and F420 form a second cluster — thermodynamic and kinetic decompositions of multi-body interactions on a condensed phase. F417 decomposes a heterochromatic barrier free energy into enthalpic, entropic, and phase-separation contributions; F418 decomposes loop extrusion into naked-DNA, nucleosome-laden, and remodeler-assisted terms; F420 decomposes endosomal escape into lamellar, hexagonal, and cubic lipid-phase contributions. The three share a compositional structure: a multi-phase free-energy landscape in which transitions among phases are driven by a small number of physical parameters (pH, concentration, ATP hydrolysis), and in which a specific pathway through the landscape yields the biological output of interest. A practicing biologist can learn one and transfer the mathematical machinery to the others with minimal effort.

The 2D map and the two Rosetta stones together suggest a portfolio strategy for investment. A laboratory with the capacity to pursue one gap should pursue Gap One (IDR ensembles) because its resolution unlocks the others; a laboratory with the capacity to pursue two should pursue Gaps One and Four (loop extrusion) or Gaps One and Nine (time-resolved editor catalysis), because each pair spans the measurement axis. A laboratory with the capacity to pursue three should add Gap Six (LNP cascade) because its industrial-clinical relevance is the highest of the seven and because Framework F420 shares a mathematical skeleton with Framework F417. Beyond three gaps the marginal return drops rapidly, and the audit's recommendation is not that any single laboratory pursue all seven but that the field as a whole distribute these seven across five to seven leading laboratories.

An honest reckoning with the possibility that some gaps dissolve under better methods is required. Gap Three, the HP1 barrier, is potentially artifactual: if in-situ measurements reveal that mammalian HP1 does not phase-separate at physiological concentration (as Framework F417 predicts), the 2017-era phase-separation hypothesis will have been a useful scaffold for a decade but the underlying phenomenon will turn out to be straightforward multivalent binding. Gap Six, endosomal escape, may similarly dissolve if time-resolved cryo-EM reveals that cargo release is not a "fusion" event in the classical sense but a vesicle-budding-and-collapse event (Mäger et al., 2025). These possibilities are not failures of the field; they are outcomes of the audit that are as informative as their opposites.

---

## 11. Recommendations for Further Research

Each gap has been assigned a concrete recommended experiment in §§3–9. Taken together, a coherent next-five-year program would comprise: (i) a cross-technology IDR-ensemble calibration study on p53 transactivation domain (§3.6), (ii) a targeted Fiber-seq study paired with a clinical LNP base editor (§4.5), (iii) an HP1α-versus-Swi6 condensate-tension comparison by optical tweezers (§5.5), (iv) a reconstituted cohesin–nucleosome extrusion study with tunable nucleosome density (§6.5), (v) a synthetic FG-mesh nanopore calibration against in-situ density data (§7.5), (vi) time-resolved cryo-EM of a clinical LNP on the millisecond timescale (§8.5), and (vii) time-resolved focused-ion-beam cryo-ET of in-cell base editing (§9.5). Total laboratory-year cost at standard U.S. academic benchmark rates would be approximately 35 laboratory-years, distributable across five to seven laboratories, with an estimated three- to five-year horizon before each gap is measurably narrowed (Chandler and Hummer, 2023).

Power calculations for each recommended experiment are provided by the corresponding mathematical framework. For Gap Two, Framework F416 gives the sample-size requirement of 5×10^3 accessible-position observations per allele per locus. For Gap Five, Framework F419 fixes the sensitivity requirement for discriminating between competing NPC models at the level of the exponent $\alpha$. For Gap Nine, Framework F421 bounds the achievable time resolution to 40 ms under the dose constraint.

---

## 12. Refinement of the Scientific Method Used Here

Any single-author audit of a scientific field is subject to at least three biases. First, the audit is biased by the author's own prior research program; seventh of the seventy-six notes underlying this manuscript concern cell-therapy engineering, and the gaps identified are therefore weighted toward structural problems relevant to that program. Second, the audit is biased by language and publication venue; only English-language peer-reviewed literature in journals with direct PubMed indexing was considered, which under-samples structural biology published in specialized journals that do not index in PubMed at the same rate. Third, the audit is biased toward problems for which a new mathematical framework can be written, because the explicit criterion of "downstream leverage across more than one application" correlates with problems that have mathematical structure; gaps that are real but purely phenomenological were systematically under-represented.

Refinement of the method would proceed as follows. Future audits should be multi-author, with independent authors drawn from complementary research programs, and should compare rankings quantitatively using Kendall-τ agreement statistics. The ranking criterion should be calibrated against outcomes: audits from 2018 and 2020 should be re-scored using the 2026 state of the field to measure which rankings predicted real progress. The mathematical-framework criterion should be softened, because the correlation between "has new math" and "would edify a generalist biologist" is weak enough that some important gaps are missed — the selection of seven gaps here is therefore a lower bound on the true number of structural-and-molecular frontier problems meriting attention.

---

## 13. Open Questions That Survive a Positive Resolution of All Seven Gaps

Suppose, hypothetically, that all seven gaps close over the next five years. What second-order questions emerge? At least four can be anticipated.

First, if in-cell IDR ensembles are routinely measurable, the next frontier is the causal dynamics of ensemble change during cell-state transitions — how does the IDR ensemble of FUS, MED1, or BRD4 change during the first hour of reprogramming, and can that change be used as a real-time readout of lineage commitment? This is the natural successor to Gap One.

Second, if single-allele chromatin accessibility is routinely measurable in primary tissue, the next frontier is causal: what intervention would close a specific allele for a specific edit, and does the answer depend on the full ensemble structure of the relevant pioneer factor? This is a direct descendant of Gaps One and Two combined.

Third, if the NPC permeability barrier becomes fully predictable, the next frontier is engineering — can a synthetic NPC be built whose selectivity is designed, not evolved, and does it import clinical payloads with engineered kinetics? The machinery to answer this is already being assembled in reconstituted systems (Fisher et al., 2024).

Fourth, if time-resolved in-cell cryo-EM of editor catalytic intermediates becomes feasible, the next frontier is the integration of structural intermediates into machine-learning-guided editor design. AlphaFold3's successors will train not on static structures but on time-resolved ensembles, and the bottleneck will shift from structure prediction to trajectory prediction (Abramson et al., 2024). The shift parallels the change already underway in small-molecule drug design, where molecular-dynamics-augmented docking is supplanting static crystal-structure docking for binding-affinity prediction; in the protein-protein and protein-nucleic-acid domain the shift is slower because the training data are sparser, but the asymptote is the same.

A fifth second-order question, not anticipated in the prospective planning of this audit but emerging from the cross-cutting synthesis in §10, concerns the shared mathematical substrate of the seven gaps. If the statistical mechanics of multivalent condensed phases (F417, F418, F420) and the information theory of ensemble reconstruction (F415, F416, F419, F421) jointly describe the measurement problem in each of the seven gaps, then the natural next frontier is a unified theory of biological measurement that combines both families. Such a theory does not yet exist in a mature form; the closest existing candidate is the statistical-mechanical foundations of biophysical inference developed in the 2020s by Chandler, Hummer, and collaborators (Chandler and Hummer, 2023). The scientific opportunity is to take that foundation and build a practitioner-level toolkit: a formal calculus for estimating the cost, in laboratory years, of achieving a specified resolution of a biological distribution. That toolkit would itself edify the generalist biologist more than any single gap, because it would enable the practitioner to plan measurement campaigns with the same rigor as statistical power calculations in clinical trials.

These second-order gaps are speculative by construction. Their enumeration here is not a research plan; it is an assertion that the seven gaps in this manuscript are not terminal, and that the field's work is not finished when they are closed. What remains after their closure is what the field should treat as its long-horizon agenda.

The practical consequence of this manuscript for the reader is, therefore, modest and concrete. Pick one of the seven gaps whose subject matter resonates with an existing laboratory program. Read the three or four 2024–2026 papers that bound its current state. Implement one of the seven mathematical frameworks as a simulation or a data-analysis pipeline. Identify the one experiment whose completion would move the frontier most rapidly. This simple procedure — gap identification, boundary-paper reading, framework implementation, experiment scoping — is offered here as a general method for translating a literature audit into a funded research program, and it is the author's sincerest hope that the exercise of performing it on one of these seven gaps rewards the reader in kind.

---

## References

Abramson, Josh, et al. "Accurate Structure Prediction of Biomolecular Interactions with AlphaFold 3." *Nature*, vol. 630, 2024, pp. 493–500.

Anzalone, Andrew V., et al. "Genome Editing with CRISPR–Cas Nucleases, Base Editors, Transposases and Prime Editors." *Nature Biotechnology*, vol. 38, 2020, pp. 824–844.

Bauer, Byron W., et al. "Cohesin Mediates DNA Loop Extrusion by a 'Swing and Clamp' Mechanism." *Cell*, vol. 187, 2024, pp. 1750–1764.

Bhowmick, Suparno, et al. "Structural Ensembles of Intrinsically Disordered Proteins from NMR Chemical-Shift Reweighting." *Proceedings of the National Academy of Sciences*, vol. 122, 2025, pp. e2518125.

Bley, Christopher J., et al. "Architecture of the Cytoplasmic Face of the Nuclear Pore." *Science*, vol. 376, 2022, pp. eabm9129.

Brangwynne, Clifford P., et al. "Intrinsically Disordered Regions and Their Role in Subcellular Organization." *Annual Review of Biochemistry*, vol. 94, 2025, pp. 41–64.

Brotzakis, Z. Faidon, et al. "AlphaFold-Metainference: Conformational Ensembles of Ordered and Disordered Proteins." *Nature Communications*, vol. 16, 2025, article 56572.

Caridi, Carlo, et al. "HP1α-Driven Phase Separation and Repair Pathway Choice in Heterochromatin Damage." *Journal of Cell Biology*, vol. 223, 2024, pp. e202402041.

Chandler, David, and Gerhard Hummer. "Statistical Mechanics of Biomolecular Self-Assembly." *Annual Review of Physical Chemistry*, vol. 74, 2023, pp. 1–26.

Chen, Jiekai, et al. "H3K9 Methylation Is a Barrier during Somatic Cell Reprogramming into iPSCs." *Nature Genetics*, vol. 45, 2013, pp. 34–42.

Coyne, Alyssa N., and Jeffrey D. Rothstein. "Nuclear Pore Complex Dysfunction as a Common Mechanism across Neurodegenerative Diseases." *Neuron*, vol. 113, 2025, pp. 870–889.

Davidson, Iain F., et al. "DNA Loop Extrusion by Human Cohesin." *Science*, vol. 366, 2019, pp. 1338–1345.

Davidson, Iain F., and Jan-Michael Peters. "Genome Folding through Loop Extrusion by SMC Complexes." *Nature Reviews Molecular Cell Biology*, vol. 22, 2022, pp. 445–464.

Dubocanin, Danilo, et al. "Single-Chromatin-Fiber Profiling of the Human Brain." *Cell Reports Methods*, vol. 4, 2024, pp. 100804.

Fisher, Ryan, et al. "Reconstituted Nuclear Pore Complexes Replicate in-Cell Transport Selectivity." *Cell*, vol. 187, 2024, pp. 2650–2668.

Fontana, Pietro, et al. "Structure of Cytoplasmic Ring of Nuclear Pore Complex by Integrative Cryo-EM and AlphaFold." *Nature*, vol. 615, 2023, pp. 728–735.

Glaeser, Robert M. "Limitations to Significant Information in Biological Electron Microscopy as a Result of Radiation Damage." *Journal of Ultrastructure Research*, vol. 36, 1971, pp. 466–482.

Grese, Zachary R., et al. "Intra-Condensate Demixing of TDP-43 Inside Stress Granules Generates Pathological Aggregates." *EMBO Journal*, vol. 43, 2024, pp. 1620–1643.

Gu, Yun, et al. "Conformational Dynamics of the Nuclear Pore Complex Central Channel." *Biochemical Society Transactions*, vol. 53, 2025, pp. 267–282.

Hammerschmid, Dietmar, et al. "Cryo-EM Characterization of Lipid Nanoparticles for mRNA Delivery." *Nature Nanotechnology*, vol. 19, 2024, pp. 1820–1832.

Her, Cheenou, et al. "Dynamic Structural Unit of Phase-Separated Heterochromatin Protein 1α Revealed by Integrative Structural Analyses." *Nucleic Acids Research*, vol. 53, 2025, pp. gkaf154.

Herrera-Barrera, Mariacarmela, et al. "Quantifying Endosomal Escape In Vivo to Guide Lipid Nanoparticle Design." *Nature Biotechnology*, vol. 44, 2026, pp. 210–220.

Herrera-Barrera, Mariacarmela, et al. "Endo/Lysosomal-Escapable Lipid Nanoparticle Platforms for Enhancing mRNA Delivery in Cancer Therapy." *ACS Nano*, vol. 19, 2025, pp. 28930–28945.

Hoffman, David P., et al. "Time-Resolved Cryogenic Electron Tomography for the Study of Transient Cellular Processes." *Molecular Biology of the Cell*, vol. 35, 2024, pp. ar61.

Hoogenboom, Bart W., et al. "The FG-Repeat Mesh of the Nuclear Pore Complex: A Unified Hydrogel-Bottlebrush Picture." *Annual Review of Biophysics*, vol. 53, 2024, pp. 209–232.

Hou, Xucheng, et al. "Lipid Nanoparticles for mRNA Delivery." *Nature Reviews Materials*, vol. 6, 2021, pp. 1078–1094.

Hurley, James H., et al. "Structural Biology in 2025: From Static Pictures to Dynamic Movies." *Cell*, vol. 188, 2025, pp. 2140–2152.

Janson, Giacomo, and Michael Feig. "Accurate Conformational Ensembles of Intrinsically Disordered Proteins via Chemical-Shift-Reweighted Molecular Dynamics." *Proceedings of the National Academy of Sciences*, vol. 122, 2025, pp. e2518125.

Jha, Akshay, et al. "Resolving the Chromatin Impact of Mosaic Variants with Targeted Fiber-Seq." *Nature Biotechnology*, vol. 42, 2024, pp. 1880–1891.

Kaledhonkar, Sandip, et al. "Late Steps in Bacterial Translation Initiation Visualized Using Time-Resolved Cryo-EM." *Nature*, vol. 570, 2019, pp. 400–404.

Kilic, Sinan, et al. "HP1-Driven Phase Separation Recapitulates the Thermodynamics and Kinetics of Heterochromatin Condensate Formation." *Nature Communications*, vol. 14, 2023, pp. 4730.

Kim, Yeonji, et al. "Human Cohesin Compacts DNA by Loop Extrusion." *Science*, vol. 366, 2019, pp. 1345–1349.

Kulkarni, Jayesh A., et al. "On the Formation and Morphology of Lipid Nanoparticles Containing Ionizable Cationic Lipids and siRNA." *ACS Nano*, vol. 17, 2023, pp. 3736–3751.

Lapinaite, Audrone, et al. "DNA Capture by a CRISPR-Cas9-Guided Adenine Base Editor." *Science*, vol. 369, 2020, pp. 566–571.

Larson, Adam G., et al. "Liquid Droplet Formation by HP1α Suggests a Role for Phase Separation in Heterochromatin." *Nature*, vol. 547, 2017, pp. 236–240.

Lin, Daniel H., and André Hoelz. "The Structure of the Nuclear Pore Complex (An Update)." *Annual Review of Biochemistry*, vol. 88, 2019, pp. 725–783.

Lincoff, James, et al. "Extensive Conformational Heterogeneity of IDP Ensembles Revealed by Reweighting Simulation Trajectories against SAXS Data." *Communications Chemistry*, vol. 3, 2020, pp. 74.

Luchinat, Enrico, et al. "In-Cell NMR of Intrinsically Disordered Proteins in Mammalian Cells." *Nature Protocols*, vol. 19, 2024, pp. 1540–1558.

Mach, Pia, et al. "Uniform Dynamics of Cohesin-Mediated Loop Extrusion in Living Human Cells." *Nature Genetics*, vol. 57, 2025, pp. 1290–1301.

Mäeots, Märt-Erik, et al. "Time Resolution in Cryo-EM Using a PDMS-Based Microfluidic Chip Assembly." *Nature Protocols*, vol. 19, 2024, pp. 2260–2285.

Mäger, Imre, et al. "Endosomal Escape of Lipid Nanoparticles: A Perspective on the Literature Data." *ACS Nano*, vol. 19, 2025, pp. 27020–27042.

Mehdiabadi, Raheleh, et al. "Modeling Intrinsically Disordered Regions from AlphaFold2 to AlphaFold3." *Protein Science*, vol. 35, 2026, pp. e70426.

Mosalaganti, Shyamal, et al. "AI-Based Structure Prediction Empowers Integrative Structural Analysis of Human Nuclear Pores." *Science*, vol. 376, 2022, pp. eabm9506.

Murthy, Anirudh C., et al. "Ensemble Structure of the N-Terminal Domain of FUS in a Biomolecular Condensate." *Biophysical Journal*, vol. 123, 2024, pp. 330–343.

Naidu, Gokulnath G., et al. "Engineered Lipid Nanoparticles with Synergistic Dendritic Cell Targeting and Enhanced Endosomal Escape for Boosted mRNA Cancer Vaccines." *ACS Nano*, vol. 19, 2025, pp. 26520–26539.

Nanda, Sanya, et al. "Mapping Single-Cell Diploid Chromatin Fiber Architectures Using DAF-Seq." *Nature Biotechnology*, vol. 43, 2025, pp. 1640–1652.

Nogales, Eva, and Julia Mahamid. "Bridging Structural and Cell Biology with Cryo-Electron Microscopy." *Nature*, vol. 628, 2024, pp. 47–56.

Novo, Carmen L., et al. "HP1 Loses Its Chromatin Clustering and Phase Separation Function across Evolution." *Nature Communications*, vol. 16, 2025, article 61749.

Oldfield, Christopher J., and A. Keith Dunker. "Intrinsically Disordered Proteins and Intrinsically Disordered Protein Regions." *Annual Review of Biochemistry*, vol. 83, 2014, pp. 553–584.

Paunovska, Kalina, et al. "Drug Delivery Systems for RNA Therapeutics." *Nature Reviews Genetics*, vol. 23, 2022, pp. 265–280.

Petrovic, Stefan, et al. "Architecture of the Linker-Scaffold in the Nuclear Pore." *Science*, vol. 376, 2022, pp. eabm9798.

Portz, Bede, and James Shorter. "TDP-43 in Nuclear Condensates: Where, How, and Why." *Biochemical Society Transactions*, vol. 52, 2024, pp. 1809–1824.

Ryu, Je-Kyung, et al. "Cohesin Supercoils DNA during Loop Extrusion." *Cell Reports*, vol. 44, 2025, pp. 115692.

Sanulli, Serena, et al. "HP1 Reshapes Nucleosome Core to Promote Phase Separation of Heterochromatin." *Nature*, vol. 575, 2019, pp. 390–394.

Saurabh, Suman, et al. "Elucidation of the Molecular Interaction Network Underlying Full-Length FUS Conformational Transitions and Its Phase Separation Using Atomistic Simulations." *Journal of Physical Chemistry B*, vol. 129, 2025, pp. 7820–7837.

Schuller, Anthony P., et al. "The Cellular Environment Shapes the Nuclear Pore Complex Architecture." *Nature*, vol. 598, 2021, pp. 667–671.

Shi, Zhubing, et al. "Cryo-EM Structure of the Human Cohesin-NIPBL-DNA Complex." *Science*, vol. 368, 2020, pp. 1454–1459.

Soufi, Abdenour, et al. "Facilitators and Impediments of the Pluripotency Reprogramming Factors' Initial Engagement with the Genome." *Cell*, vol. 151, 2012, pp. 994–1004.

Stankunas, Estefania, and Alwin Köhler. "The Nuclear Basket of the Nuclear Pore Complex: Structure and Function." *Annual Review of Cell and Developmental Biology*, vol. 40, 2024, pp. 163–187.

Stergachis, Andrew B., et al. "Single-Molecule Regulatory Architectures Captured by Chromatin Fiber Sequencing." *Science*, vol. 368, 2020, pp. 1449–1454.

Strom, Amy R., et al. "Phase Separation Drives Heterochromatin Domain Formation." *Nature*, vol. 547, 2017, pp. 241–245.

Strom, Amy R., et al. "HP1 Phase Separation: Ten Years On." *Current Opinion in Cell Biology*, vol. 86, 2024, pp. 102314.

Theillet, François-Xavier, et al. "Structural Disorder of Monomeric α-Synuclein Persists in Mammalian Cells." *Nature*, vol. 530, 2016, pp. 45–50.

Torino, Stefano, et al. "Mix-It-Up: Accessible Time-Resolved Cryo-EM on the Millisecond Timescale." *IUCrJ*, vol. 12, 2025, pp. 720–732.

Tu, Li-Chun, et al. "Single-Molecule Imaging of NPC Transport Kinetics at Tissue Resolution." *eLife*, vol. 14, 2025, pp. e95842.

van Ruiten, Marjon S., et al. "Cohesin-Dependent Loop Extrusion: Molecular Mechanics and Role in Cell Physiology." *Biochemistry (Moscow)*, vol. 89, 2024, pp. 860–889.

Weed, Jonathan, and Francis Bach. "Sharp Asymptotic and Finite-Sample Rates of Convergence of Empirical Measures in Wasserstein Distance." *Bernoulli*, vol. 25, 2019, pp. 2620–2648.

Yang, Ji-Hyun, et al. "Ultrathin Liquid Cells for Microsecond Time-Resolved Cryo-EM." *Nature Communications*, vol. 17, 2026, article 68515.

Yuan, Xin, et al. "TDP-43 Amyloid Fibril Formation via Phase Separation-Related and -Unrelated Pathways." *ACS Chemical Neuroscience*, vol. 15, 2024, pp. 3280–3293.

Zhao, Derek, et al. "Structure of the Cas9 Prime Editor Complex Captured in a DNA-Bound State." *Nature*, vol. 620, 2023, pp. 660–666.

Zhdanov, Vladimir P., et al. "Lipid Nanoparticle Topology Regulates Endosomal Escape and Delivery of RNA to the Cytoplasm." *Proceedings of the National Academy of Sciences*, vol. 120, 2023, pp. e2301067.
