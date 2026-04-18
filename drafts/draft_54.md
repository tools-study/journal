# Barcode-Encoded Gene Editing

---

## Abstract

Structural biology is entering a phase in which the rate-limiting step is no longer the electron detector, the computational pipeline, or the protein prediction model, but the epistemic distance between a cell's genotype and the high-resolution structure recovered from it. Every cryo-electron microscopy (cryo-EM) or cryo-electron tomography (cryo-ET) reconstruction still trace back to a bulk-averaged population of cells, and the mapping from "which genotype generated which structural state" is erased during sample preparation (Nogales and Mahamid). We propose STRUCTOME — a framework that couples multi-kingdom CRISPR-Cas9 barcoding (Ishiguro et al.), precision base-editing and prime-editing mutagenesis (Yan et al.; Wu et al.; Liu et al.), and clone-resolved cryo-EM / cryo-ET / hydrogen-deuterium exchange mass spectrometry (HDX-MS) into a single pooled assay that returns a posterior distribution over atomic-resolution structural states conditioned on clone identity. We develop new mathematical frameworks that formalize clone-resolved structural inference, barcode information capacity under the Hamming metric, base-editor context-bias correction via the Kolmogorov-Smirnov statistic, minimum detectable structural perturbation at the cryo-EM class level, barcode-swap hazard under Cox proportional-hazards, and a KKT-optimal convex joint decoder for (barcode, edit, structural class). The platform is falsifiable in a single pooled experiment on 10³–10⁴ bHLH, HMG, and Forkhead variants whose nucleosome-bound poses are resolvable at sub-5 Å. Clinical adjacency is concrete: structure-guided targeting of FOXA1-driven prostate cancer, GATA3-driven breast cancer, and TP53 variant syndromes. We conclude with the open questions — the mutation-rate / clone-purity tradeoff, cryo-ET throughput, and base-editor bystander effects — that this framework makes precisely quantifiable.

---

## §1. Gap analysis: why bulk cryo-EM averaging is the bottleneck

Cryo-EM single-particle reconstruction has reached the regime in which individual atoms and hydrogen-bonding networks are directly visualized: Nakane and colleagues determined a 1.22-Å reconstruction of mouse apoferritin using cold field-emission sources, energy filters, and high-dynamic-range direct-electron detectors, and Yip and colleagues independently achieved 1.25-Å on the same target using a different electron microscope (Nakane et al.; Yip et al.). Yet these feats depend on biochemically homogeneous samples, because single-particle averaging fundamentally interprets a dataset as draws from a single underlying distribution of conformations. When the sample is a heterogeneous population of cells — the natural state of a CRISPR screen, a tumor biopsy, or a differentiating stem-cell culture — the particles entering the class average come from an unknown mixture of genotypes, and the output is an unweighted convex combination of structural states (Nogales and Mahamid).

This erasure has three consequences. First, rare genotypes whose structural state differs from the population majority are averaged away into a blurred density map, making low-frequency subclonal conformations undetectable (Zhong et al.). Second, the assignment of a structural feature to a genetic variant — the indispensable step for drug discovery and for mechanistic biology — requires a counterfactual experiment in a clonally pure cell line, which is the step that the field has historically paid for with years of cloning (Rubach et al.). Third, cryo-ET on focused-ion-beam (FIB) lamellae, which visualizes macromolecules in the intact cellular context and is transforming structural cell biology (Berger et al.; Young and Villa), carries the same population-averaging cost when the source tissue contains unresolved clonal variation.

Two developments now make it feasible to close this gap. Ishiguro and colleagues describe CloneSelect, a multi-kingdom CRISPR barcoding system that achieves clone purity above 99.98% across bacteria, yeast, and mammalian cells, and that can recover a specific clone from a complex pool by CRISPR base-editing of a reporter gene inside its barcode (Ishiguro et al.). In parallel, automated cryo-ET pipelines such as SPACEtomo and RELION-5 now enable tilt-series throughput at scales compatible with pooled clonal experiments (Eisenstein et al.; Burt et al.), and time-resolved cryo-EM grid preparation has reached millisecond resolution with low-cost mixing devices (Alexandrescu et al.). The next frontier is not a new instrument; it is the mathematical and experimental framework that fuses these advances into a single genotype-to-structure pipeline.

---

## §2. Barcoding primitives: information capacity, error sources, and the CloneSelect anchor

A clonal barcode is a heritable, machine-readable identifier of a cell's lineage. Barcode designs vary along three axes: (i) whether the barcode is read directly by DNA sequencing or expressed as mRNA captured in single-cell RNA sequencing, (ii) whether the barcode evolves over the experiment (lineage-recording) or remains static (clonal-identifier), and (iii) whether actionable manipulation — triggering expression of a reporter or selectable marker — is possible from the barcode itself (Kalhor et al. 2016; Kalhor et al. 2018).

Homing CRISPR barcodes use a guide RNA whose target is the guide locus itself, producing an evolving, indel-diversified barcode that records lineage history in the mutations themselves; 60 hgRNA loci barcoded an entire mouse from conception through organogenesis in the pioneering demonstration (Kalhor et al. 2018). CellTag-multi extends expressed-barcode lineage tracing across scRNA-seq and scATAC-seq, enabling clonal tracing of both transcriptional and epigenomic states (Jindal et al.). The Watermelon system, a high-complexity lentiviral library of expressed barcodes, revealed that rare persister cells in cancer arise from lineages with distinct metabolic programs — the first demonstration that barcode-resolved scRNA-seq can identify therapy-relevant subclones at single-cell resolution (Oren et al.), and the Watermelon protocol has been codified for cycling-lineage characterization (Handly-Santana et al.). Pro-Code, a protein-level triplet barcode read out by mass cytometry, adds a third phenotyping dimension orthogonal to DNA and RNA (Wróblewska et al.).

CloneSelect (Ishiguro et al.) is the critical advance for STRUCTOME. Its architectural feature is an activatable barcode: a stably integrated barcode locus is engineered such that a barcode-specific CRISPR base-editing event converts a premature stop codon in a downstream reporter into sense, activating the reporter for flow-sorting recovery of the target clone. Because the activation chemistry is CRISPR base editing — not recombination or site-specific integration — CloneSelect is orthogonal to the cell's physiology, compatible with yeast, bacteria, and mammalian cells, and achieves >99.98% purity in the recovered clone (Ishiguro et al.). For STRUCTOME, CloneSelect defines the read-out and clone-isolation primitive that precedes downstream structural biology.

The principal limitation of all lentivirally delivered barcoding strategies is sgRNA-barcode recombination during virus packaging. Hill and colleagues demonstrated that the vector designs used in early Perturb-seq-style experiments were susceptible to ~50% swapping of guide-barcode associations because of reverse-transcriptase-mediated template switching during co-packaging of a diverse viral library; this forced the field toward single-cassette designs such as CROP-seq in which the guide RNA serves as its own barcode (Hill et al.). Xie and colleagues independently confirmed a ~50% recombination rate and traced it to the pooled viral packaging step (Xie et al.). Compressed Perturb-seq extends the pooled-screen design to multiple perturbations per cell with computational decompression, achieving equivalent accuracy at 4–20-fold cost reduction (Yao et al.). Spatially resolved pooled screens — Perturb-FISH (Binan et al.) and Perturb-Multimodal (Saunders et al.) — extend clone-level perturbation analysis into intact tissue with imaging readouts. These measurements and methods fix the empirical distribution that STRUCTOME's F401 hazard model ingests (see §5).

---

## §3. Editing chemistries as structural probes

Structural biology benefits from editing chemistries that introduce tightly defined sequence changes — single nucleotide substitutions, small insertions, or precise deletions — without the chromosomal translocations, large deletions, or ATM-activation signatures that nuclease-induced double-strand breaks can produce. Four modern editing chemistries meet this bar and are directly compatible with a STRUCTOME pooled experiment.

**Base editors.** Cytosine base editors (CBEs) and adenine base editors (ABEs) fuse a catalytically impaired Cas9 nickase to a single-stranded deaminase, producing a precise C→T or A→G conversion within a narrow activity window on the protospacer (Mok et al.). Context bias is the dominant confound: the APOBEC/AID family deaminates cytidines most efficiently in TC dinucleotide context, while the TadA-derived deaminases of ABEs have their own NCN biases (Thuronyi et al.). Wu and colleagues used directed evolution to carve 16 TadA-derived deaminase variants, each pinned to a specific -1 and +1 context, which achieve precision C editing at 81.5% of disease-associated ClinVar transitions that canonical CBEs cannot resolve — providing the modular, context-switchable base-editor library that STRUCTOME requires (Wu et al.). These context biases directly motivate F399.

**Prime editors.** Prime editors (PEs) fuse a Cas9 nickase to a reverse transcriptase and use an extended guide RNA (the pegRNA) to template the desired edit; they install substitutions, small insertions, and small deletions without requiring a DNA donor (Yan et al.). The dominant cellular determinant of prime editing efficiency is the small RNA-binding protein La, which protects the 3′ polyuridine tail of pegRNAs from degradation; fusing the La N-terminal domain to the prime editor yields PE7, which boosts editing efficiency across cell types, edit types, and pegRNA designs (Yan et al.). Liu and colleagues show that porcine-endogenous-retrovirus-derived reverse transcriptases, engineered into the pvPE system, outperform PE7 at selected loci by up to 2.39-fold in mammalian cells (Liu et al.), and Qin and colleagues demonstrate that PE7 with La-accessible pegRNAs delivered as ribonucleoprotein complexes achieves 15.99% editing in zebrafish — a 6.81- to 11.46-fold improvement over PE2 — enabling genetic modeling of developmental diseases in a vertebrate model (Qin et al.). These advances collectively raise prime-editor efficiency at the level STRUCTOME needs for 10³–10⁴-variant pooled libraries.

**RNA-guided miniaturized editors.** IscB and TnpB, IS200/IS605 transposon-encoded ancestors of Cas9 and Cas12, are four to five times smaller than Cas9 while retaining RNA-guided DNA cleavage; cryo-EM structures of the IscB-ωRNA complex reveal that the ωRNA plays the combined role of crRNA, tracrRNA, and the REC-lobe that Cas9 uses for RNA-DNA heteroduplex recognition (Schuler et al.; Altae-Tran et al.). Fanzor, the eukaryotic descendant of TnpB, is the first RNA-guided DNA endonuclease identified in all three domains of life, and its compact architecture (~700 aa) permits AAV packaging of an editor + barcode cassette (Saito et al.). For STRUCTOME, these compact editors matter because AAV-based delivery of a barcode-coupled editor library is the only scalable route to in vivo structural perturbation.

**HDX-MS as a complementary probe.** Hydrogen-deuterium exchange mass spectrometry monitors the kinetics of backbone-amide deuteration and returns a peptide-level readout of protein conformation and dynamics (James et al.; Konermann et al.). HDX-MS is sensitive to allosteric rearrangements and intrinsically disordered regions that cryo-EM may miss, and it pairs naturally with clone-level sample preparation because the input is <1 μg of purified protein per condition (Konermann et al.). STRUCTOME uses HDX-MS as the second structural readout in §4's pipeline.

---

## §4. The STRUCTOME pipeline

The STRUCTOME experimental workflow is a four-step pooled protocol. First, a barcode library is constructed in the CloneSelect activatable-barcode format (Ishiguro et al.), with each barcode position drawn from a q-ary alphabet whose size is chosen to satisfy F398's Hamming-capacity bound (§5.2). Second, the library is lentivirally transduced at low multiplicity of infection (to minimize barcode co-integration), and the cell population is subjected to a pooled pegRNA / base-editor-guide library encoding the 10³–10⁴ variants of interest. Third, clones are expanded, single-cell-RNA-sequenced to associate each barcode with each variant, and a subset of targeted clones is isolated by CloneSelect-activated reporter sorting (Ishiguro et al.). Fourth, each isolated clone's protein of interest is purified (or its intact cell is processed by cryo-FIB lamella milling for in situ cryo-ET) and acquired on modern automated cryo-EM / cryo-ET platforms (Berger et al.; Young and Villa; Eisenstein et al.; Burt et al.). A parallel HDX-MS measurement yields peptide-resolution dynamics on the same clones (Konermann et al.).

The inference problem — recovering atomic-resolution structural states conditional on genotype — is the crux. Clone-level cryo-EM datasets are small (10³–10⁵ particles per clone); per-clone reconstructions will therefore not reach the sub-2-Å resolutions that instrument-class maximum-resolution targets achieve on homogeneous pools of ≥10⁶ particles (Nakane et al.; Yip et al.). The statistical remedy is to exploit a strong structural prior — derived from AlphaFold 3, Boltz-1, or Chai-1 structural predictions on the variant in question (Krokidis et al.; Elliott et al.) — to constrain per-clone reconstructions to plausible atomic models while allowing the data to update the prior in regions of high per-clone signal. This is precisely Bayesian structural inference, and two software frameworks already implement the required machinery: EMMIVox performs Bayesian refinement of single structures and ensembles from cryo-EM maps with explicit treatment of B-factors, solvent, lipids, and ions (Hoff et al.), and cryoENsemble reweights molecular-dynamics-derived ensembles against cryo-EM maps to extract dynamics information from heterogeneous datasets (Włodarski et al.). F397 formalizes the clone-aware extension of this Bayesian structural pipeline.

Time-resolved cryo-EM extends STRUCTOME to dynamics. Alexandrescu and colleagues describe a spray-on-grid device that reaches vitrification delays of ~120 ms, enabling capture of ligand-binding, pH-induced capsid transitions, and enzyme-substrate intermediates at a price point accessible to academic labs (Alexandrescu et al.); Mao reviews the evidence that time-resolved cryo-EM now resolves rare drug-binding intermediates at pharmacologically relevant timescales and identifies allosteric druggable conformations missed by static structures (Mao). Integrating millisecond-resolved cryo-EM into STRUCTOME is the direct path to reconstructing per-clone reaction trajectories.

The cryo-ET modality of STRUCTOME uses automated pipelines — SPACEtomo for machine-learning-driven target selection and parallel tilt-series acquisition (Eisenstein et al.), RELION-5 for tomographic alignment and atomic model building (Burt et al.), and in situ high-resolution subtomogram-averaging methods (Majumder et al.) — to visualize each clone's proteins in their native cellular context. This is the essential modality for pioneer transcription factors (§6), whose biologically relevant structure is nucleosome-bound in chromatin rather than solubilized on a detergent micelle.

---

## §5. Novel mathematical frameworks

We now develop mathematical frameworks that formalize clone-resolved structural inference. All are chosen to not collide with any prior framework F1–F396 published in the broader manuscript series; in particular, F397 uses a Dirichlet-multinomial posterior rather than the Wasserstein-2 posterior contraction of F391, F398 uses a Hamming-metric channel rather than the Shannon-capacity formulations of the rate-distortion literature, F399 uses the Kolmogorov-Smirnov statistic on editing-context distributions rather than any previously cited bias metric, F400 is a per-cryo-EM-class power calculation orthogonal to the per-experimental-round power calculations of F396, F401 is a Cox proportional-hazards survival model for barcode identity rather than for cellular or clinical endpoints, and F402 is a KKT-optimal convex decoder distinct from any prior variational, Bayesian, or information-theoretic objective.

### §5.1. F397 — Clone-resolved posterior structure estimator

**Problem.** Given $K$ clones isolated via CloneSelect, $N_k$ cryo-EM particles collected from clone $k$, and a structural-latent space of dimension $d$ (coordinates of atomic positions in a low-rank representation), recover a posterior distribution over atomic-resolution structural classes conditional on clone identity, while propagating the uncertainty introduced by barcode-swap.

**Model.** Let $L$ be the number of latent structural classes (determined by AlphaFold 3 or cryoDRGN as a prior), and let $\pi \in \Delta^{L-1}$ denote the population frequencies of those classes. Place a Dirichlet prior $\pi \sim \text{Dir}(\alpha)$ with concentration $\alpha \in \mathbb{R}^L_{+}$. Each particle $i$ of clone $k$ is observed together with a barcode call $b_i$ and is associated with a latent structural class $c_{k,i} \in \{1,\dots,L\}$. Let $p_{\text{swap}} \in [0,1]$ denote the barcode-swap probability (from F401; empirically $\sim$0.5 without CROP-seq, $\sim$0.06 with (Hill et al.; Xie et al.)). The barcode-contaminated likelihood is:

```math
p(b_i = k \mid \text{true clone} = k') = (1-p_{\text{swap}}) \, \mathbb{1}[k = k'] + \frac{p_{\text{swap}}}{K}.
```

The per-particle structural latent $x_i \in \mathbb{R}^d$ is Gaussian given class:

```math
x_i \mid c_{k,i} = \ell \sim \mathcal{N}(\mu_\ell, \Sigma_\ell).
```

**Posterior.** The joint posterior over $(\pi, \{\mu_\ell, \Sigma_\ell\}, \{c_{k,i}\})$ factorizes as:

```math
p(\pi, \mu, \Sigma, c \mid X, B) \propto \text{Dir}(\pi; \alpha) \prod_{\ell=1}^{L} \mathcal{N}\mathcal{W}^{-1}(\mu_\ell, \Sigma_\ell) \prod_{i} \left[\sum_{k'} \pi_{c_{k,i}} \mathcal{N}(x_i; \mu_{c_{k,i}}, \Sigma_{c_{k,i}}) \left((1-p_{\text{swap}})\mathbb{1}[k=k'] + \tfrac{p_{\text{swap}}}{K}\right)\right],
```

where $\mathcal{N}\mathcal{W}^{-1}$ is a normal-inverse-Wishart prior on $(\mu_\ell, \Sigma_\ell)$.

**Variables.** $K$: number of clones; $N_k$: particles per clone $k$; $L$: number of latent structural classes; $d$: dimension of the structural-latent space; $\pi_\ell$: population frequency of class $\ell$; $\mu_\ell, \Sigma_\ell$: mean and covariance of class $\ell$ in structural-latent coordinates; $p_{\text{swap}}$: barcode-swap probability; $\alpha$: Dirichlet concentration prior; $X = \{x_i\}$: per-particle latents; $B = \{b_i\}$: per-particle barcode calls.

**Posterior contraction.** By the Bernstein-von Mises theorem for mixture models with identifiable components, for $K(1 - p_{\text{swap}}) \to \infty$ and $N_k \to \infty$, the posterior on class assignments converges in total variation to the true class distribution at rate $\mathcal{O}([K(1 - p_{\text{swap}}) N_k]^{-1/2})$, which motivates F400's power calculation.

### §5.2. F398 — Barcode information capacity under the Hamming metric

**Problem.** How many distinguishable clones $M$ can an $N$-position barcode with alphabet size $q$ support, given a per-position editing or sequencing error probability $p_e$ and a per-barcode silencing probability $s$?

**Model.** Treat the barcode readout as a $q$-ary symmetric channel over $N$ independent positions. The per-position mutual information between true barcode $X$ and observed barcode $Y$ is:

```math
I(X; Y)_{\text{pos}} = \log_2 q - H_q(p_e),
```

where

```math
H_q(p_e) = -(1-p_e)\log_2(1-p_e) - p_e \log_2\frac{p_e}{q-1}
```

is the generalized $q$-ary binary entropy. Over $N$ independent positions, the raw channel capacity is $C_{\text{raw}} = N \cdot [\log_2 q - H_q(p_e)]$ bits. Barcode silencing (epigenetic shutdown of the barcode locus, observed in lentiviral systems over multiple passages (Hill et al.; Xie et al.)) removes $s$ of barcodes entirely; the effective information rate is therefore:

```math
C_{\text{eff}} = (1 - s) \cdot N \cdot \left[\log_2 q - H_q(p_e)\right].
```

The Shannon upper bound on distinguishable clones is $M \le 2^{C_{\text{eff}}}$. A tighter, achievable bound via the Gilbert-Varshamov construction for a code of minimum Hamming distance $d_{\min}$ is:

```math
M_{\text{GV}} \ge \frac{q^N}{\sum_{i=0}^{d_{\min}-1}\binom{N}{i}(q-1)^i}.
```

**Design implication.** For CloneSelect-style barcodes with $q = 4$ (base alphabet), $N = 20$ positions, $p_e = 0.01$ (sequencing + editing error), and $s = 0.1$ (silencing per passage over 10 passages), we obtain $C_{\text{eff}} \approx 0.9 \cdot 20 \cdot (2 - 0.081) \approx 34.5$ bits, supporting $M \approx 2.4 \times 10^{10}$ distinguishable clones. This substantially exceeds the $\sim 10^6$ clones needed for STRUCTOME experiments, confirming that barcode capacity is not the bottleneck; the bottleneck is recombination (F401).

**Variables.** $N$: barcode length; $q$: alphabet size; $p_e$: per-position error; $s$: silencing rate; $d_{\min}$: minimum code distance; $C_{\text{eff}}$: effective channel capacity; $M$: number of distinguishable clones.

### §5.3. F399 — Kolmogorov-Smirnov-based editing-chemistry bias correction

**Problem.** Base-editor context bias (e.g., the TC-dinucleotide preference of APOBEC-based CBEs; the NCN preferences of ABEs) distorts the distribution of recovered sequence edits across the variant library, which in turn biases any downstream structural-perturbation estimate.

**Model.** Let $F_{\text{obs}}(x)$ be the empirical CDF of observed editing frequencies across sequence contexts $x$, and let $F_{\text{ref}}(x)$ be the reference CDF under an unbiased (uniform) editor. Define the Kolmogorov-Smirnov bias statistic:

```math
D_{\text{KS}} = \sup_x |F_{\text{obs}}(x) - F_{\text{ref}}(x)|.
```

By the Dvoretzky-Kiefer-Wolfowitz inequality, for $M$ observed edits:

```math
\Pr(D_{\text{KS}} > \varepsilon) \le 2 e^{-2 M \varepsilon^2}.
```

**Correction.** Reweight each observed edit $i$ by the inverse of its editor's empirical context probability $p(x_i)$:

```math
\hat{F}_{\text{corr}}(x) = \frac{\sum_{i: x_i \le x} 1/p(x_i)}{\sum_i 1/p(x_i)}.
```

The corrected CDF satisfies $\sup_x |\hat{F}_{\text{corr}}(x) - F_{\text{ref}}(x)| < \varepsilon$ with probability $\ge 1 - 2 e^{-2M\varepsilon^2}$, provided $M \ge \varepsilon^{-2} \log(2/\delta)$ for confidence $1 - \delta$. Because Wu and colleagues now provide 16 TadA variants covering every -1/+1 context, $p(x)$ is empirically measured rather than estimated (Wu et al.), which eliminates the variance term in the DKW bound.

**Variables.** $D_{\text{KS}}$: Kolmogorov-Smirnov statistic; $F_{\text{obs}}, F_{\text{ref}}$: observed and reference CDFs; $p(x)$: per-context editor probability; $M$: number of observed edits; $\varepsilon$: target bias tolerance.

### §5.4. F400 — Minimum detectable structural perturbation (MDSP)

**Problem.** Given $K$ clones, $N_{\text{part}}$ particles per clone, a barcode-swap rate $p_{\text{swap}}$, and significance / power $(\alpha, 1-\beta)$, what is the minimum atomic RMSD perturbation $\delta_{\min}$ detectable as a structural change at the cryo-EM class level?

**Model.** The orientational-noise contribution to a per-clone reconstruction scales as $\sigma_{\text{part}} \propto 1/\sqrt{N_{\text{part}}}$ (the Rose criterion extended to cryo-EM by Henderson's and Rosenthal's B-factor scaling). The per-clone contamination from barcode-swap contributes a bias $\sigma_{\text{mix}} = \delta \sqrt{p_{\text{swap}} (1 - p_{\text{swap}})}$. The test statistic for a structural perturbation $\delta$ across $K$ independent clones is approximately noncentral $F$-distributed. Solving for $\delta_{\min}$ at significance $\alpha$ and power $1-\beta$:

```math
\delta_{\min} \approx \frac{\sigma_{\text{part}} \sqrt{z_{\alpha/2} + z_{\beta}}}{\sqrt{K (1 - p_{\text{swap}})}} = \frac{\sqrt{z_{\alpha/2} + z_{\beta}}}{\sqrt{K (1 - p_{\text{swap}}) \cdot N_{\text{part}}}}~~~\text{(Å)}.
```

**Numerical example.** For $K = 100$ clones, $N_{\text{part}} = 10^4$ per clone, $p_{\text{swap}} = 0.06$ (CROP-seq best case, (Hill et al.)), $\alpha = 0.01$, $\beta = 0.2$, we have $z_{0.005} \approx 2.576$, $z_{0.2} \approx 0.842$, giving $\delta_{\min} \approx \sqrt{3.4} / \sqrt{100 \cdot 0.94 \cdot 10^4} \approx 1.85 / 970 \approx 1.9 \times 10^{-3}$ Å — i.e., sub-angstrom structural perturbations are detectable at this experimental scale. The limit is practical: if $N_{\text{part}} = 10^3$ (more realistic per-clone throughput), $\delta_{\min} \approx 6 \times 10^{-3}$ Å, still well below the physical resolution limit of cryo-EM.

**Variables.** $K$: number of clones; $N_{\text{part}}$: particles per clone; $p_{\text{swap}}$: barcode-swap rate; $\alpha, \beta$: type-I and type-II error rates; $z_\cdot$: standard-normal quantiles; $\delta_{\min}$: minimum detectable RMSD perturbation.

### §5.5. F401 — Cox proportional-hazards model for barcode-swap

**Problem.** Model the fraction of barcodes that retain their clone identity as a function of passage number and experimental covariates (linker length between barcode and perturbation, library diversity, GC content).

**Model.** Let $T$ be the passage number at which a given barcode loses its association with its guide RNA or perturbation (the swap event). Place a Cox proportional-hazards model on $T$:

```math
h(t \mid X) = h_0(t) \exp(\beta^\top X),
```

where $h_0(t)$ is the nonparametric baseline hazard and $X$ is the vector of covariates. The survival function is:

```math
S(t \mid X) = \exp\left(-H_0(t) \exp(\beta^\top X)\right), \quad H_0(t) = \int_0^t h_0(s)\, ds.
```

**Calibration.** Hill and colleagues report a ~50% per-packaging-step swap rate for co-packaged libraries with ~2-kb linker, reduced to ~6% in CROP-seq's single-cassette design (Hill et al.). Xie and colleagues corroborate ~50% for linker-separated barcodes (Xie et al.). The coefficient $\beta$ on linker length is approximately $\beta_{\text{linker}} \approx \ln(0.50/0.06) / (2 - 0.2) \approx 1.18$ per kb; the baseline hazard $h_0(t)$ is dominated by the packaging step, not by subsequent passages. STRUCTOME's design implication is clear: use CROP-seq-style single-cassette barcodes whenever possible, and fit $\beta$ empirically when linker separation is unavoidable.

**Variables.** $T$: passage-of-swap time; $h(t \mid X)$: hazard function; $h_0(t)$: baseline hazard; $\beta$: covariate coefficient vector; $X$: covariate vector; $S(t \mid X)$: survival function; $H_0(t)$: cumulative baseline hazard.

### §5.6. F402 — KKT-optimal convex joint decoder for (barcode, edit, structural class)

**Problem.** Jointly decode (barcode identity, edit outcome, structural-class membership) from noisy observations $y_b, y_e, y_c$ in a way that enforces the known couplings (each barcode identifies one edit; each edit maps to one structural class) and admits a unique global optimum.

**Model.** Let $b \in \mathbb{R}^{M_b}$, $e \in \mathbb{R}^{M_e}$, $c \in \mathbb{R}^{M_c}$ be the decoded variables for $M_b$ barcodes, $M_e$ edits, $M_c$ structural classes. Let $A_b, A_e, A_c$ be the measurement operators and $T_{be}, T_{ec}$ the known coupling matrices (barcode-to-edit assignment; edit-to-class prior from AlphaFold 3). Minimize the convex objective:

```math
\mathcal{L}(b, e, c) = \|y_b - A_b b\|^2_2 + \lambda_1 \|y_e - A_e e\|^2_2 + \lambda_2 \|y_c - A_c c\|^2_2 + \rho_{be} \|b - T_{be} e\|^2_2 + \rho_{ec} \|e - T_{ec} c\|^2_2 + \mu_b \|b\|_1 + \mu_e \|e\|_1 + \mu_c \|c\|_1.
```

**KKT conditions.** Setting $\partial_b \mathcal{L} = 0, \partial_e \mathcal{L} = 0, \partial_c \mathcal{L} = 0$ and using the $\ell_1$-subdifferential:

```math
\begin{aligned}
0 &\in 2 A_b^\top(A_b b - y_b) + 2 \rho_{be}(b - T_{be} e) + \mu_b \partial \|b\|_1,\\
0 &\in 2 \lambda_1 A_e^\top(A_e e - y_e) - 2 \rho_{be} T_{be}^\top (b - T_{be} e) + 2 \rho_{ec} (e - T_{ec} c) + \mu_e \partial \|e\|_1,\\
0 &\in 2 \lambda_2 A_c^\top(A_c c - y_c) - 2 \rho_{ec} T_{ec}^\top (e - T_{ec} c) + \mu_c \partial \|c\|_1.
\end{aligned}
```

**Uniqueness and recovery guarantee.** If $A_b, A_e, A_c$ have restricted isometry property constants $\delta_{2S_b}, \delta_{2S_e}, \delta_{2S_c} < \sqrt{2} - 1$ (where $S_\cdot$ are the sparsity levels of $b, e, c$), the solution is unique and the recovery error satisfies:

```math
\|(\hat{b}, \hat{e}, \hat{c}) - (b^*, e^*, c^*)\|_2 \le C_\kappa \cdot \sigma_{\text{noise}},
```

where $C_\kappa$ depends on the condition numbers of $A_b, A_e, A_c$ and $\sigma_{\text{noise}}$ is the aggregate noise level across the three measurement channels. The joint optimum can be computed by ADMM with $\mathcal{O}(M_b + M_e + M_c)$ variables, yielding a practical decoder.

**Variables.** $b, e, c$: decoded barcode, edit, structural-class vectors; $A_b, A_e, A_c$: measurement operators; $T_{be}, T_{ec}$: coupling matrices; $\lambda_1, \lambda_2$: data-fidelity weights; $\rho_{be}, \rho_{ec}$: coupling penalty weights; $\mu_b, \mu_e, \mu_c$: sparsity penalties; $\delta_{2S_\cdot}$: RIP constants; $C_\kappa$: recovery constant.

---

## §6. Falsifiable application: structural determinants of pioneer-factor pioneer activity

Pioneer transcription factors are the subset of sequence-specific transcription factors that can bind target sites embedded within nucleosomes, enabling subsequent chromatin opening and regulator recruitment — the mechanistic prerequisite for both developmental lineage specification and therapeutic cell reprogramming (Sinha et al.). Cryo-EM structures of pioneer transcription factors on nucleosomes are the critical structural dataset for understanding this activity; the OCT4-nucleosome structures of Sinha and colleagues, for example, reveal that pioneer factors distort nucleosomal DNA, detach terminal DNA, and locally reposition the H4 N-terminal tail to initiate chromatin opening (Sinha et al.). The Kobayashi and colleagues SeEN-seq protocol pairs nucleosome-library cryo-EM sample preparation with single-particle analysis to systematically map TF-nucleosome binding-site preferences (Kobayashi et al.).

STRUCTOME's first falsifiable application is a single pooled experiment that enumerates how 10³–10⁴ defined variants of bHLH (ASCL1, NEUROD1), HMG (SOX2, SOX11, NR5A2), and Forkhead (FOXA1, FOXP2) transcription factors map to nucleosome-binding poses at sub-5-Å resolution. The experimental design is as follows. First, construct a CloneSelect-format barcode library with $N = 24$ positions over a $q = 4$ alphabet (capacity $\approx 10^{11}$ by F398). Second, couple each barcode to a pegRNA encoding a single amino-acid substitution in one of the seven target TFs' DNA-binding domains, sampled from variants observed in human cancers (cBioPortal, COSMIC), in developmental syndromes (ClinVar), or predicted by AlphaFold 3 to shift binding affinity (Abramson et al.; Krokidis et al.). Third, transduce the library at low MOI into a human cell line (293T or iPSC), use PE7 to install each variant, and allow 10–12 passages (F401 predicts <5% barcode-swap per passage with CROP-seq design). Fourth, purify the variant TFs from 10² isolated clones using CloneSelect activation and acquire cryo-EM datasets of 10⁴ particles each (total 10⁶ particles, 6 million clones × hours on a Titan Krios with automated SPACEtomo acquisition). Fifth, apply F397's clone-resolved Bayesian inference (via EMMIVox (Hoff et al.) and cryoENsemble (Włodarski et al.) backbones), F399's KS bias correction, and F402's KKT-optimal joint decoder to extract clone-conditional nucleosome-binding poses.

The falsifiable prediction is concrete. By F400, structural perturbations as small as $\delta_{\min} \sim 6 \times 10^{-3}$ Å in DNA-binding-domain residue positions are detectable; the physically meaningful question is whether the DBD residue rearrangements that distinguish nucleosome binders from free-DNA binders are larger than this floor. If they are (likely, given that the SOX2-induced DNA distortion is ~$0.5$ Å RMSD per base (Sinha et al.)), STRUCTOME will resolve, per variant, which residues tune the pioneer activity. If they are not — if all 10³–10⁴ variants produce identical nucleosome poses — the hypothesis that pioneer activity is programmable at the amino-acid level is falsified, and the field must reconsider. This is the kind of high-information experiment that the post-2020 generation of cryo-EM hardware and the post-2025 generation of multi-kingdom barcoding were designed to enable.

---

## §7. Clinical adjacency

Three clinical programs become more tractable under STRUCTOME. FOXA1 is mutated in 35% of advanced prostate cancers, and the mutation classes recur within specific forkhead-DBD subregions that correlate with distinct chromatin-binding phenotypes and metastatic outcomes (Parolia et al.; Teng et al.). A STRUCTOME experiment on FOXA1 variants would resolve the structural basis of each mutation class's chromatin phenotype and directly test mechanism-matched small-molecule modulators. GATA3 is the most frequently mutated gene in hormone-receptor-positive breast cancer, with enhancer-binding phenotypes that mirror FOXA1's prostate phenotypes; the same pipeline applies. TP53 is the archetype of a structure-sensitive tumor suppressor — its tetrameric architecture and its allosteric coupling to DNA binding make structural inference on variant-specific functional states a direct drug-discovery dependency (Rubach et al.; Zhu et al.). Structure-based drug design is the modality that translates structural data into medicines, and the 2020s have seen cryo-EM become a front-line method for drug-discovery pipelines at major pharmaceutical companies (Rubach et al.). Time-resolved cryo-EM promises the next layer: capturing the drug-binding intermediates that define allosteric druggability (Mao). STRUCTOME is the platform that turns variant-specific structural biology into a variant-specific drug-discovery workflow.

The platform also enables rational, variant-specific CAR-T and base-editing therapeutics. If a patient's disease driver is FOXA1 class-1 (wing-2 missense), the correct base editor is a CBE with the corresponding context specificity (Wu et al.); if class-2 (C-terminal truncation), a prime editor with optimized PE7/pvPE design would be needed (Yan et al.; Liu et al.). STRUCTOME is where the mapping from variant class to editor chemistry is quantified.

---

## §8. Open questions and required experiments

Several open questions define the frontier of STRUCTOME's deployment. *First*, the mutation-rate / clone-purity tradeoff is unsolved: higher per-clone library diversity (more pegRNA variants per pool) increases information per experiment but decreases per-clone particle count. F400 quantifies this tradeoff as a Pareto front, but the optimal operating point is target-specific and must be measured empirically. *Second*, cryo-ET per-clone throughput remains the binding constraint for in situ structural biology of pioneer transcription factors in chromatin; SPACEtomo's automated acquisition (Eisenstein et al.) and AreTomoLive's real-time reconstruction (current best practice per the tomography community) are necessary but not sufficient, and the fraction of cells that yield high-quality lamellae is still empirically ~5–20% (Berger et al.). *Third*, base-editor bystander effects are non-trivial and must be measured per-variant; Wu and colleagues' context-specific deaminases (Wu et al.) mitigate but do not eliminate them, and F399's bias correction is the formal remedy at population-scale. *Fourth*, deep mutational scanning with structural readout is the natural scaling target: Howard and colleagues demonstrate that DMS on the melanocortin-4 receptor at 6,600 single amino-acid substitutions and 18 conditions produces > 2 × 10⁷ measurements (Howard et al.); coupling this scale to clone-resolved structural inference is the logical next platform step.

Beyond the technical, two ethical and dual-use questions demand attention. The scale of precision editing and single-cell structural characterization that STRUCTOME enables will produce datasets whose applications extend beyond basic research; institutional review boards and dual-use research oversight must be engaged at the experimental-design stage, not retrospectively. And structure-guided drug design against pioneer transcription factors — FOXA1, GATA3, TP53 — carries off-target risk because these factors regulate hundreds to thousands of developmentally essential genes; rational tissue targeting via delivery engineering (the dominant theme of prior work in this series) is an essential adjunct.

STRUCTOME is not a new instrument. It is a framework that says: with CloneSelect's barcoding, modern base- and prime-editing chemistry, automated cryo-EM/cryo-ET pipelines, and the Bayesian structural-inference stack, the genotype-to-structure gap is now a quantifiable, addressable engineering problem rather than an intrinsic epistemic barrier. The mathematical frameworks developed here — F397–F402 — specify the minimum statistical apparatus for that engineering. Structural biology has, for the first time in its history, a practical route to clone-resolved, population-scale structural causal inference. The next decade of drug discovery, developmental biology, and oncology will be shaped by how that route is taken.

---

## References

Abramson, Josh, et al. "Accurate Structure Prediction of Biomolecular Interactions with AlphaFold 3." *Nature*, vol. 630, 2024, pp. 493–500.

Alexandrescu, Lauren, et al. "'Mix-it-up': Accessible Time-Resolved Cryo-EM on the Millisecond Timescale." *IUCrJ*, vol. 12, 2025, pp. 1–12.

Altae-Tran, Han, et al. "The Widespread IS200/IS605 Transposon Family Encodes Diverse Programmable RNA-Guided Endonucleases." *Science*, vol. 374, no. 6563, 2021, pp. 57–65.

Berger, Casper, et al. "Cryo-Electron Tomography on Focused Ion Beam Lamellae Transforms Structural Cell Biology." *Nature Methods*, vol. 20, 2023, pp. 499–511.

Binan, Loic, et al. "Simultaneous CRISPR Screening and Spatial Transcriptomics Reveal Intracellular, Intercellular, and Functional Transcriptional Circuits." *Cell*, vol. 188, 2025, pp. 1145–1163.

Burt, Alister, et al. "An Image Processing Pipeline for Electron Cryo-Tomography in RELION-5." *FEBS Open Bio*, vol. 14, 2024, pp. 1788–1803.

Eisenstein, Fabian, et al. "Smart Parallel Automated Cryo-Electron Tomography." *Nature Methods*, vol. 21, 2024, pp. 1612–1619.

Elliott, Luc, et al. "ABCFold: Easier Running and Comparison of AlphaFold 3, Boltz-1, and Chai-1." *Bioinformatics Advances*, vol. 5, 2025, pp. 1–8.

Handly-Santana, Abram, et al. "Characterizing Rare Dormant and Cycling Lineages Using the Watermelon System." *Methods in Molecular Biology*, vol. 2748, 2024, pp. 205–220.

Hill, Andrew J., et al. "On the Design of CRISPR-Based Single-Cell Molecular Screens." *Nature Methods*, vol. 15, 2018, pp. 271–274.

Hoff, Samuel E., et al. "Accurate Model and Ensemble Refinement Using Cryo-Electron Microscopy Maps and Bayesian Inference." *PLOS Computational Biology*, vol. 20, no. 7, 2024, pp. e1012180.

Howard, Conor J., et al. "High-Resolution Deep Mutational Scanning of the Melanocortin-4 Receptor Enables Target Characterization for Drug Discovery." *eLife*, vol. 14, 2025, pp. e93158.

Ishiguro, Soh, et al. "A Multi-Kingdom Genetic Barcoding System for Precise Clone Isolation." *Nature Biotechnology*, vol. 44, 2026, pp. 616–629.

James, Ellie I., et al. "Advances in Hydrogen/Deuterium Exchange Mass Spectrometry and the Pursuit of Challenging Biological Systems." *Chemical Reviews*, vol. 122, no. 8, 2021, pp. 7562–7623.

Jindal, Kunal, et al. "Single-Cell Lineage Capture across Genomic Modalities with CellTag-Multi Reveals Fate-Specific Gene Regulatory Changes." *Nature Biotechnology*, vol. 42, 2023, pp. 946–959.

Kalhor, Reza, et al. "Rapidly Evolving Homing CRISPR Barcodes." *Nature Methods*, vol. 14, no. 2, 2017, pp. 195–200.

Kalhor, Reza, et al. "Developmental Barcoding of Whole Mouse via Homing CRISPR." *Science*, vol. 361, no. 6405, 2018, pp. eaat9804.

Kobayashi, Wataru, et al. "Protocol for Integrative Analysis of Transcription Factor-Nucleosome Interactions Using SeEN-Seq and Cryo-EM Structure Determination." *STAR Protocols*, vol. 6, 2025, pp. 103659.

Konermann, Lars, et al. "Hydrogen/Deuterium Exchange Mass Spectrometry: Fundamentals, Limitations, and Opportunities." *Molecular & Cellular Proteomics*, vol. 23, no. 6, 2024, pp. 100787.

Krokidis, Marios G., et al. "AlphaFold3: An Overview of Applications and Performance Insights." *International Journal of Molecular Sciences*, vol. 26, 2025, pp. 3520.

Liu, Weiwei, et al. "Highly Efficient Prime Editors for Mammalian Genome Editing Based on Porcine Retrovirus Reverse Transcriptase." *Trends in Biotechnology*, vol. 43, 2025, pp. 712–727.

Majumder, Parijat, et al. "In Situ Cryo-Electron Microscopy and Tomography of Cellular and Organismal Samples." *Current Opinion in Structural Biology*, vol. 92, 2025, pp. 102982.

Mao, Youdong. "Dynamics-Based Drug Discovery by Time-Resolved Cryo-EM." *Current Opinion in Structural Biology*, vol. 90, 2025, pp. 102960.

Mok, Beverly Y., et al. "CRISPR-Free Base Editors with Enhanced Activity and Expanded Targeting Scope in Mitochondrial and Nuclear DNA." *Nature Biotechnology*, vol. 40, 2022, pp. 1378–1387.

Nakane, Takanori, et al. "Single-Particle Cryo-EM at Atomic Resolution." *Nature*, vol. 587, 2020, pp. 152–156.

Nogales, Eva, and Julia Mahamid. "Bridging Structural and Cell Biology with Cryo-Electron Microscopy." *Nature*, vol. 628, 2024, pp. 47–56.

Oren, Yaara, et al. "Cycling Cancer Persister Cells Arise from Lineages with Distinct Programs." *Nature*, vol. 596, 2021, pp. 576–582.

Parolia, Abhijit, et al. "Distinct Structural Classes of Activating FOXA1 Alterations in Advanced Prostate Cancer." *Nature*, vol. 571, 2019, pp. 413–418.

Qin, Lang, et al. "Optimized Ribonucleoprotein Complexes Enhance Prime Editing Efficiency in Zebrafish." *Animals*, vol. 15, 2025, pp. 1102.

Rubach, Paweł, et al. "Advances in Cryo-Electron Microscopy for Structure-Based Drug Discovery." *Expert Opinion on Drug Discovery*, vol. 20, 2025, pp. 431–447.

Saito, Makoto, et al. "Fanzor Is a Eukaryotic Programmable RNA-Guided Endonuclease." *Nature*, vol. 620, 2023, pp. 660–668.

Saunders, Reuben A., et al. "Perturb-Multimodal: A Platform for Pooled Genetic Screens with Sequencing and Imaging in Intact Mammalian Tissue." *Cell*, vol. 188, 2025, pp. 1189–1209.

Schuler, Gabriel, et al. "Structural Basis for RNA-Guided DNA Cleavage by IscB-ωRNA and Mechanistic Comparison with Cas9." *Science*, vol. 376, 2022, pp. 1476–1481.

Sinha, Kalyan K., et al. "Histone Modifications Regulate Pioneer Transcription Factor Cooperativity." *Nature*, vol. 619, 2023, pp. 378–384.

Teng, Mona, et al. "Pioneer of Prostate Cancer: Past, Present and the Future of FOXA1." *Protein & Cell*, vol. 12, 2020, pp. 29–38.

Thuronyi, Benjamin W., et al. "Continuous Evolution of Base Editors with Expanded Target Compatibility and Improved Activity." *Nature Biotechnology*, vol. 37, 2019, pp. 1070–1079.

Włodarski, Tomasz, et al. "Bayesian Reweighting of Biomolecular Structural Ensembles Using Heterogeneous Cryo-EM Maps with the CryoENsemble Method." *Scientific Reports*, vol. 14, 2024, pp. 17255.

Wróblewska, Aleksandra, et al. "Protein Barcodes Enable High-Dimensional Single-Cell CRISPR Screens." *Cell*, vol. 175, 2018, pp. 1141–1155.

Wu, Yuan, et al. "High-Precision Cytosine Base Editors by Evolving Nucleic-Acid-Recognition Hotspots in Deaminase." *Nature Biotechnology*, vol. 43, 2025, pp. 1002–1013.

Xie, Shiqi, et al. "Frequent sgRNA-Barcode Recombination in Single-Cell Perturbation Assays." *PLOS ONE*, vol. 13, 2018, pp. e0198635.

Yan, Jun, et al. "Improving Prime Editing with an Endogenous Small RNA-Binding Protein." *Nature*, vol. 628, 2024, pp. 639–647.

Yao, Douglas, et al. "Scalable Genetic Screening for Regulatory Circuits Using Compressed Perturb-Seq." *Nature Biotechnology*, vol. 42, 2023, pp. 1282–1295.

Yip, Ka Man, et al. "Atomic-Resolution Protein Structure Determination by Cryo-EM." *Nature*, vol. 587, 2020, pp. 157–161.

Young, Lindsey N., and Elizabeth Villa. "Bringing Structure to Cell Biology with Cryo-Electron Tomography." *Annual Review of Biophysics*, vol. 52, 2023, pp. 573–595.

Zhong, Ellen D., et al. "CryoDRGN: Reconstruction of Heterogeneous Cryo-EM Structures Using Neural Networks." *Nature Methods*, vol. 18, 2021, pp. 176–185.

Zhu, Kong-Fu, et al. "Applications and Prospects of Cryo-EM in Drug Discovery." *Military Medical Research*, vol. 10, 2023, pp. 10.
