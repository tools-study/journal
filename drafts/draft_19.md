# Precise Partial Reprogramming

---

## Abstract

Partial epigenetic reprogramming—transient expression of Yamanaka factors (OSK/OSKM) to reverse cellular aging without erasing somatic identity—has advanced from preclinical proof-of-concept to the first FDA-cleared human trial (Life Biosciences ER-100, January 2026). Yet the field confronts a fundamental control-theoretic problem: the boundary between rejuvenation and dedifferentiation is not a smooth gradient amenable to classical optimization, but rather a sharp discontinuity characteristic of a fold catastrophe in the epigenetic landscape. This paper develops a complete mathematical and engineering framework for navigating this discontinuity. **Section 2** establishes that the rejuvenation–dedifferentiation boundary constitutes a cusp catastrophe in the sense of Thom's classification, where the state variable *x* represents epigenetic position along the age–identity axis, and the two control parameters are factor concentration (*a*) and cumulative exposure duration (*b*). We derive the cusp surface, the bifurcation set (4*a*³ + 27*b*² = 0 in rescaled coordinates), and show that tissue-specific heterogeneity in starting epigenetic position explains why identical dosing protocols produce different outcomes across cell types. **Section 3** introduces persistent homology from topological data analysis as a model-free method to detect the cusp signature in single-cell epigenomic data: the appearance of a new connected component (β₀ increase) at the critical duration signals bifurcation into rejuvenated and dedifferentiating subpopulations, while a one-dimensional cycle (β₁) encodes hysteresis. **Section 4** develops a Hidden Markov Model (HMM) for real-time latent state inference during reprogramming, with five hidden states (aged-differentiated, early-rejuvenating, at-the-fold, dedifferentiating, pluripotent) and observable emissions derived from methylation clocks, surface markers, and chromatin accessibility; the forward algorithm provides online posterior state estimates that can trigger dose reduction before cells cross the fold line. **Section 5** models cooperative chromatin transitions using a one-dimensional Ising model with Potts extension, where nucleosome modification states (H3K9me3-aged vs. H3K4me3-rejuvenated) interact through reader-writer enzyme coupling; we derive the critical field (factor dosage) for domain-level phase transitions and show that the rejuvenated state is metastable with a shallow energy barrier, explaining the fragility of partially reprogrammed cells. **Section 6** integrates these frameworks into a closed-loop feedback control architecture combining sensory readout, HMM-based state estimation, and engineered actuators (synNotch kill switches, miRNA-responsive 3′-UTRs, optogenetic dosing) to maintain trajectories within the smooth rejuvenation region of the cusp surface. We present specific experimental predictions falsifiable with existing single-cell technologies and propose a validation roadmap using dense time-course human fibroblast MPTR data. The central contribution is a shift from open-loop dosing protocols—inherently fragile near fold singularities—to closed-loop feedback control informed by real-time topological and probabilistic state inference.

---

## 1. Introduction: The Sharp Edge of Rejuvenation

### 1.1 The Promise and the Peril

The discovery that transient expression of Oct4, Sox2, and Klf4 (OSK) can reverse epigenetic age markers in mammalian cells without erasing somatic identity has opened a therapeutic frontier with extraordinary potential [1]. In January 2026, Life Biosciences received FDA clearance for the first Investigational New Drug (IND) application for ER-100, an AAV-delivered OSK therapy for optic neuropathies, marking the clinical arrival of partial epigenetic reprogramming [2]. Preclinical data from multiple laboratories have demonstrated rejuvenation of diverse tissues: retinal ganglion cells regain visual acuity [3], aged muscle stem cells recover regenerative capacity [4], dermal fibroblasts reverse transcriptomic age by approximately 30 years [5], and systemic cyclic induction extends median remaining lifespan by over 100% in aged wild-type mice [6].

The pace of progress has accelerated markedly since 2024. Organ-specific reprogramming studies have revealed that different tissues undergo epigenetic remodeling at vastly different rates, with liver and intestinal epithelium showing the fastest dedifferentiation kinetics [311]. Conserved biological processes underlying partial reprogramming—including autophagy activation, metabolic rewiring to glycolysis, and transient upregulation of DNA repair pathways—have been systematically catalogued across species from mouse to human [312]. The epigenetic rejuvenation promise has been critically evaluated in multiple independent reviews, establishing that while the therapeutic concept is sound, the precision control problem remains the rate-limiting barrier [313]. Chemical approaches to partial reprogramming have advanced with the demonstration that small-molecule cocktails can achieve rejuvenation without any transcription factor delivery, though with more modest epigenetic age reversal (~3–5 years vs. ~30 years with MPTR) [314]. Single-cell multi-omics studies have revealed that reprogramming trajectories are far more heterogeneous than bulk measurements suggest, with cells diversifying into multiple subpopulations as early as day 5 of factor exposure [315]. New epigenetic clock technologies—including histone modification-based clocks, CpGPT (a transformer model trained on hundreds of methylation datasets), and AltumAge (a deep learning predictor)—have improved the resolution and accuracy of biological age measurement, enabling finer-grained assessment of rejuvenation interventions [316, 317].

Yet these advances carry a shadow. The same molecular machinery that reverses epigenetic aging—when applied for too long or at too high a concentration—erases cell identity entirely, producing pluripotent cells that form teratomas *in vivo* [7]. The boundary between therapeutic rejuvenation and pathological dedifferentiation is not merely narrow; emerging evidence suggests it is *discontinuous*—a qualitative phase transition rather than a smooth dose-response curve. This paper develops the mathematical framework to characterize, detect, and navigate this discontinuity.

### 1.2 Evidence for Discontinuity

Four lines of evidence support the hypothesis that the rejuvenation–dedifferentiation boundary is sharp rather than gradual.

**First**, the Gill day-13 peak. In maturation phase transient reprogramming (MPTR) of human dermal fibroblasts, Gill et al. observed that epigenetic rejuvenation (measured by the Horvath multi-tissue clock) peaked at approximately day 13, with an apparent reversal of ~30 years [5]. Paradoxically, extending exposure to days 15 and 17 produced *less* rejuvenation, consistent with cells beginning to cross a threshold into identity-compromising territory where clock measurements become unreliable as the reference state shifts. This non-monotonic behavior—more exposure yielding worse outcomes—is the signature of a system approaching a fold line in its parameter space.

**Second**, the Hishida one-day collapse. Hishida et al. demonstrated that even a single day of hepatocyte-specific OSKM expression was sufficient to downregulate the master hepatocyte transcription factor HNF4α, activate fetal gene programs (AFP), and remodel chromatin accessibility toward pluripotency-associated motifs [8]. This extraordinary sensitivity—where 24 hours of factor exposure can destabilize a cell identity maintained for decades—is inconsistent with a gradual erosion model and instead suggests a bistable system where a small perturbation near a critical point triggers a catastrophic transition.

**Third**, the Ocampo copy-number threshold. Ocampo et al. found that progeroid mice carrying a single copy of the OSKM transgene tolerated 35 cycles of 2-day-on/5-day-off induction without teratoma formation, whereas mice with two copies developed teratomas after only 8 cycles [9]. A doubling of expression level reduced the safe cycle count by more than 4-fold—a disproportionate response characteristic of a system near a cusp point, where small changes in a control parameter can switch the system between qualitatively different behavioral regimes.

**Fourth**, tissue-specific lethal kinetics. Parras et al. showed that the primary cause of mortality from continuous OSKM expression is not teratoma formation per se but rapid hepatic and intestinal failure, as these tissues reprogram fastest due to high proliferative rates and doxycycline absorption kinetics [10]. The tissue-dependent kinetics—with liver failing days before kidney or skin—suggests that different tissues start at different positions relative to a common catastrophe surface, with the distance to the fold line varying by cell type.

### 1.3 Why Optimal Control Is Necessary but Insufficient

Classical optimal control theory, as applied to partial reprogramming via Pontryagin's maximum principle, derives pulsatile dosing schedules that minimize teratoma risk while maximizing rejuvenation [11]. These open-loop protocols assume smooth, deterministic dynamics: the state evolves continuously in response to the control input, and the optimal trajectory can be precomputed from known system equations. However, if the landscape contains a fold singularity—a cusp catastrophe in the parameter space—then smooth dynamics break down precisely where control matters most. Near the fold, infinitesimal changes in dosage or duration can cause finite jumps in the cellular state, and the system exhibits hysteresis: cells that have crossed the fold cannot return via the reverse path. An open-loop controller, no matter how precisely optimized, cannot account for the stochastic cell-to-cell variability that places individual cells at different distances from the fold line. What is needed is a closed-loop controller that infers the latent state of each cell (or cell population) in real time and adjusts the dosing accordingly.

### 1.4 Thesis and Organization

This paper proposes that the rejuvenation–dedifferentiation boundary in partial reprogramming constitutes a cusp catastrophe in the epigenetic landscape, and develops four complementary mathematical frameworks—cusp catastrophe theory, topological data analysis (persistent homology), Hidden Markov Models, and Ising/Potts models of chromatin cooperativity—to characterize, detect, infer, and control the transition. These frameworks converge on a closed-loop feedback control architecture for precision reprogramming that maintains cellular trajectories within the smooth rejuvenation region of the cusp surface, never crossing the fold line.

Section 2 develops the cusp catastrophe formalism. Section 3 introduces persistent homology as a model-free detection method. Section 4 constructs the HMM for real-time state inference. Section 5 derives the Ising/Potts model of cooperative chromatin transitions. Section 6 integrates these into a closed-loop engineering architecture. Section 7 presents the experimental validation framework. Sections 8 and 9 provide discussion and conclusions.

Recent work has underscored the urgency of this framework. A 2025 analysis of organ-specific dedifferentiation during *in vivo* reprogramming demonstrated that the transcriptional and epigenetic responses vary by orders of magnitude across tissues, with stomach and intestine showing near-complete identity loss within 72 hours while skeletal muscle and brain remain largely refractory [318]. Logic-incorporated gene regulatory network models have revealed that the topology of feedback circuits—rather than simple parameter values—determines whether cell fate transitions are gradual or switch-like [319]. Precision reprogramming strategies targeting senescent and damaged cells specifically, rather than all cells indiscriminately, have emerged as a key translational approach [320]. The development of ligand-restricted synNotch receptors with enhanced specificity has opened new possibilities for cell-autonomous safety switches [321]. And advances in extrahepatic LNP delivery—including liposomal architectures with extended circulation times [322] and lipid-tail-length-dependent organ selectivity [323]—are expanding the tissue repertoire accessible to mRNA-mediated reprogramming.

---

## 2. The Epigenetic Cusp Catastrophe

### 2.1 Catastrophe Theory: A Primer

Catastrophe theory, developed by René Thom in the 1960s and formalized in his landmark 1972 monograph *Stabilité structurelle et morphogénèse* [12], provides a classification of the qualitative changes (bifurcations) that can occur in the equilibrium states of smooth potential functions as external parameters vary. For systems governed by gradient dynamics—where the state evolves by descending a potential landscape—Thom's classification theorem guarantees that, for up to four control parameters, only seven elementary catastrophes exist, each with a canonical normal form [13]. The simplest is the fold catastrophe (one control parameter, one state variable), where an equilibrium annihilates with a saddle as the parameter crosses a critical value. The next is the cusp catastrophe (two control parameters, one state variable), which is the focus of this paper.

The cusp catastrophe was first applied to biological systems by E. Christopher Zeeman in the 1970s, who used it to model phenomena ranging from embryological gastrulation to aggressive behavior in dogs [14]. In the context of cell biology, Sui Huang and colleagues pioneered the application of dynamical systems and bifurcation theory to cell fate decisions, demonstrating that the Waddington landscape can be formalized as a quasi-potential surface whose topology changes via bifurcations as gene-regulatory parameters vary [15]. Mojtahedi et al. provided experimental evidence for critical state transitions in cell fate, showing that gene expression distributions become multimodal at decision points, consistent with catastrophe-theoretic predictions [16]. More recently, Rand et al. developed a systematic theory connecting catastrophe-theoretic bifurcation sets with Waddington landscape families, establishing a rigorous mathematical foundation for the metaphor [17]. Jia et al. extended this framework to show that landscape-flux decomposition reveals non-equilibrium features of gene regulatory networks that cannot be captured by potential functions alone [18].

### 2.2 The Cusp Normal Form

The cusp catastrophe is defined by the potential function:

$$V(x; a, b) = \frac{x^4}{4} + \frac{a}{2}x^2 + bx$$

where *x* is the state variable and *a*, *b* are control parameters. The equilibria of the system are the critical points of *V*, found by setting:

$$\frac{\partial V}{\partial x} = x^3 + ax + b = 0$$

This cubic equation can have one or three real roots depending on the values of *a* and *b*. The transition between one and three equilibria occurs at the **bifurcation set** (also called the catastrophe set), which is the discriminant locus of the cubic:

$$\Delta = 4a^3 + 27b^2 = 0$$

This defines a cusp-shaped curve in the (*a*, *b*) control parameter plane. Inside the cusp (where Δ < 0 and *a* < 0), the potential has two local minima separated by a local maximum—the system is bistable. Outside the cusp, only one minimum exists—the system is monostable.

The stability of equilibria is determined by the second derivative:

$$\frac{\partial^2 V}{\partial x^2} = 3x^2 + a$$

An equilibrium is stable (a local minimum of *V*) when this quantity is positive, and unstable (a local maximum) when negative.

### 2.3 Mapping to Partial Reprogramming

We now establish the correspondence between the cusp catastrophe and partial reprogramming biology.

**State variable** *x*: The epigenetic position of a cell along the continuum from fully aged-differentiated (*x* ≫ 0) to fully dedifferentiated/pluripotent (*x* ≪ 0). Operationally, *x* is a composite scalar derived from epigenetic clock measurements (Horvath, GrimAge, DunedinPACE) and identity markers (lineage-specific enhancer methylation, transcription factor expression). Higher *x* corresponds to aged-differentiated; lower *x* to younger/less differentiated. The "rejuvenated-differentiated" state—the therapeutic target—corresponds to a local minimum at moderately negative *x* where the cell has reversed aging marks but retained identity.

**Control parameter** *a*: Factor concentration. This corresponds to the instantaneous expression level of OSK/OSKM factors, controlled by promoter strength, vector dose, or small-molecule concentration. When *a* is strongly negative (high factor expression), the system is more likely to be in the bistable regime where both aged and dedifferentiated states coexist. When *a* > 0 (no/low factor expression), the system has a single aged-differentiated minimum.

**Control parameter** *b*: Cumulative exposure (a function of both concentration and duration). This asymmetry parameter shifts the relative depths of the two minima. Increasing *b* (longer exposure or higher cumulative dose) favors the dedifferentiated state by lowering its potential well and raising the aged-state well.

Under this mapping, the partial reprogramming protocol traces a path through the (*a*, *b*) control parameter plane. An ideal rejuvenation protocol enters the bistable region just enough to access the rejuvenated-differentiated minimum (the shallower minimum at moderately negative *x*), then withdraws before the cell can transition to the deeper dedifferentiated minimum (strongly negative *x*).

### 2.4 The Fold Lines and Hysteresis

The two branches of the bifurcation set Δ = 0 correspond to **fold lines** where one of the equilibria (and the adjacent saddle) annihilates. These fold lines have direct biological interpretations:

**Upper fold line** (rejuvenation onset): As factor expression increases (decreasing *a*) at moderate cumulative exposure, the aged-differentiated minimum begins to "soften"—the cell becomes susceptible to epigenetic remodeling. Below this fold, a new equilibrium (the rejuvenated state) appears via a saddle-node bifurcation. Cells that reach this new minimum are rejuvenated.

**Lower fold line** (dedifferentiation threshold): As cumulative exposure *b* increases beyond a critical value, the rejuvenated minimum merges with the saddle point and annihilates. The cell is left with only the dedifferentiated minimum—a catastrophic jump to pluripotency that is irreversible within the current parameter regime. This is the "point of no return" described empirically by Olova et al., who identified day 15 in human fibroblasts as the approximate boundary beyond which somatic identity cannot be recovered [19].

**Hysteresis**: A cell that has crossed the lower fold line and jumped to the dedifferentiated state cannot return to the rejuvenated state simply by reducing factor expression. Instead, it remains dedifferentiated even as factors are withdrawn, because the reverse path would require crossing the upper fold line from below—a transition blocked by the energy barrier of the remaining minimum. This asymmetry—the forward transition is catastrophic but the reverse is blocked—is the defining feature of hysteresis in cusp catastrophe systems and explains the irreversibility observed experimentally [20].

The delay convention—where the system remains at its current minimum until that minimum is destroyed—rather than the Maxwell convention—where the system always occupies the global minimum—is the appropriate physical model for cellular reprogramming. This is because epigenetic transitions are kinetically controlled: cells do not equilibrate instantaneously to the globally most stable state but rather remain in local minima until noise or parameter changes push them past a barrier. Empirical observations support this: cells remain differentiated even when thermodynamic considerations might favor a less differentiated state, and factor withdrawal after day 10 (within the bistable region but before the lower fold) allows recovery to the differentiated state [5].

### 2.5 Tissue Heterogeneity as Cusp Geometry

A key prediction of the cusp catastrophe framework is that the critical exposure duration at which dedifferentiation becomes irreversible depends on the **starting position** of the cell within the epigenetic landscape—i.e., on the initial value of *x*₀. Tissues with different basal epigenetic ages, chromatin compaction states, and proliferative rates begin the reprogramming process at different values of *x*₀, and therefore encounter the fold lines at different cumulative exposures.

Formally, define the critical cumulative exposure *b** at which the fold line is reached as a function of starting position:

$$b^*(x_0, a) = -\frac{2}{3\sqrt{3}} (-a)^{3/2} - \delta(x_0)$$

where δ(*x*₀) is a tissue-dependent offset that accounts for the distance from the initial state to the fold. Tissues with higher proliferative rates (hepatocytes, intestinal epithelium) have smaller δ, meaning they encounter the fold sooner—consistent with Parras et al.'s observation that liver and intestine are the first organs to fail under continuous OSKM [10]. Post-mitotic tissues (neurons, cardiomyocytes) have larger δ, providing a wider therapeutic window—consistent with the 15-month safety of continuous OSK expression in retinal ganglion cells [3].

This framework also explains the Ocampo copy-number effect. Doubling the transgene copy number approximately doubles the factor expression level, corresponding to a more negative value of *a*. In the cusp geometry, this moves the system deeper into the bistable region, where the fold lines are encountered at lower cumulative exposures. The critical cycle number at which teratomas appear should decrease superlinearly with copy number—and the observed 4-fold reduction (from 35 cycles to 8 cycles for a 2-fold copy number increase) is consistent with the cubic scaling of the bifurcation set [9].

### 2.6 Stochastic Crossing and Cell-to-Cell Variability

In reality, cells are not deterministic point particles following the gradient of *V*. Each cell experiences stochastic fluctuations in factor expression (transcriptional bursting), stochastic variation in chromatin remodeling (enzyme encounter rates), and cell-to-cell heterogeneity in starting state. These fluctuations mean that, even at a fixed point in the (*a*, *b*) control plane, different cells within a population occupy a distribution of positions relative to the fold line.

Near the fold, the energy barrier separating the rejuvenated and dedifferentiated states shrinks to zero. The rate of stochastic barrier crossing follows an Arrhenius-like dependence:

$$k_{cross} \sim \exp\left(-\frac{\Delta V}{D}\right)$$

where Δ*V* is the barrier height and *D* is the effective noise intensity (incorporating transcriptional, epigenetic, and environmental fluctuations). As the system approaches the fold, Δ*V* → 0, and the crossing rate diverges. This means that at cumulative exposures slightly below the deterministic fold, some fraction of cells will nevertheless cross stochastically. The result is a **bimodal distribution** of epigenetic ages in the population—some cells have been safely rejuvenated, while others have catastrophically dedifferentiated.

This bimodality is a hallmark prediction of the cusp catastrophe that distinguishes it from smooth (non-catastrophic) dynamics. Under smooth dynamics, the distribution of epigenetic ages in a treated population would be unimodal at every time point, gradually shifting toward younger values. Under cusp dynamics, the distribution becomes bimodal at the critical duration, with the two modes corresponding to the two stable states on either side of the fold.

### 2.7 Testable Predictions

The cusp catastrophe framework generates several specific, falsifiable predictions:

**Prediction 1 (Bimodality):** In single-cell methylation data from dense time-course partial reprogramming experiments, the distribution of epigenetic ages should transition from unimodal (early time points) to bimodal (at the critical duration) to unimodal (late time points, with all cells dedifferentiated). The critical duration corresponds to the fold line crossing.

**Prediction 2 (Tissue-dependent critical durations):** The cumulative exposure at which bimodality first appears should vary across cell types in a manner predictable from their initial epigenetic state and proliferative rate: hepatocytes < intestinal epithelium < fibroblasts < neurons < cardiomyocytes.

**Prediction 3 (Irreversibility beyond fold):** Cells that have crossed the fold line (identifiable as the dedifferentiated mode in the bimodal distribution) should not recover differentiated identity upon factor withdrawal, even when cells from the same population that remained in the rejuvenated mode do recover.

**Prediction 4 (Superlinear dose sensitivity):** The critical duration should decrease superlinearly (approximately as the 3/2 power) with factor expression level, reflecting the cubic scaling of the bifurcation set.

**Prediction 5 (Hysteresis):** If factor expression is ramped up and then back down (rather than applied as a step function), cells that have crossed the fold during ramp-up will not return to the pre-fold state during ramp-down, producing path-dependent outcomes visible as an asymmetric distribution.

---

## 3. Topological Data Analysis of the Reprogramming Landscape

### 3.1 From Geometry to Topology: Why TDA?

Standard dimensionality reduction methods for single-cell data—UMAP [21], t-SNE [22], diffusion maps [23]—prioritize preserving local or global geometric relationships (distances, neighborhoods, diffusion probabilities). While powerful for visualization, these methods are sensitive to parameter choices (perplexity, number of neighbors, diffusion time) and do not provide provably robust features of the data. In particular, they cannot reliably distinguish between a single cluster with high variance (smooth dynamics near a fold) and two clusters beginning to separate (bifurcation into distinct states)—precisely the distinction that matters for detecting the cusp catastrophe.

Topological data analysis (TDA), and specifically persistent homology, addresses this limitation by extracting features that are invariant under continuous deformations of the data [24]. Rather than asking "how far apart are these points?" (geometry), TDA asks "how are these points connected?" (topology). Topological features—connected components, loops, voids—are robust to noise, do not depend on coordinate choices, and provide a multi-scale description of data shape that naturally detects bifurcations.

### 3.2 Persistent Homology: Mathematical Framework

Given a point cloud **X** = {*x*₁, ..., *x*_N} in ℝ^d (representing, e.g., single-cell methylation profiles), persistent homology constructs a nested sequence of simplicial complexes indexed by a scale parameter ε ≥ 0. The most common construction is the **Vietoris-Rips complex** VR(**X**, ε), defined as the simplicial complex whose *k*-simplices are subsets {*x*_{i₀}, ..., *x*_{iₖ}} such that the pairwise distance between every pair of points is at most ε [25].

The set of all birth-death pairs constitutes the **persistence diagram**, a multi-set of points in the plane above the diagonal [26]. Points far from the diagonal correspond to long-lived (persistent) features—robust topological signals. Points near the diagonal are short-lived—likely noise.

The **bottleneck distance** and **Wasserstein distance** between persistence diagrams provide principled metrics for comparing topological signatures across conditions or time points [27].

### 3.3 Application to Reprogramming Time Course Data

Consider a single-cell methylation or ATAC-seq time course during partial reprogramming, sampled at time points *t*₁ < *t*₂ < ... < *t*_T. At each time point, the data form a point cloud **X**(t) in a high-dimensional feature space (e.g., 353-dimensional for Horvath clock CpGs, or ~100,000-dimensional for genome-wide CpG methylation).

We compute the persistence diagram PD(*t*) for each time point and track the evolution of topological features over time.

**Expected signature under cusp catastrophe dynamics:**

**Pre-bifurcation** (*t* < *t*_crit): The point cloud is approximately unimodal (one cluster, gradual age reversal). The β₀ persistence diagram shows a single dominant long-lived feature (the main cluster) and short-lived noise features near the diagonal.

**At bifurcation** (*t* ≈ *t*_crit): The point cloud develops two dense regions separated by a sparse "valley" (the saddle region of the cusp surface). In the β₀ persistence diagram, a second long-lived connected component appears—its birth corresponds to the splitting of the population into rejuvenated and dedifferentiating subpopulations. The **persistence** (death minus birth) of this new feature measures the separation between the two modes.

**Post-bifurcation** (*t* > *t*_crit): The two clusters continue to separate. If hysteresis is present, the β₁ diagram should show a persistent one-cycle—a topological loop corresponding to the fact that forward and reverse paths through parameter space trace different trajectories through the data manifold.

Define the **topological bifurcation index** (TBI) as:

$$\text{TBI}(t) = \frac{\text{pers}_2(\text{PD}_0(t))}{\text{pers}_1(\text{PD}_0(t))}$$

where pers₁ and pers₂ are the persistence values of the first and second most persistent β₀ features. Under unimodal dynamics, TBI ≈ 0 (the second feature is noise). At bifurcation, TBI increases sharply as the second cluster becomes a genuine topological feature. A TBI exceeding a threshold (calibrated from synthetic data simulated under the cusp model) signals that the population has entered the bistable region.

### 3.4 Computational Pipeline

We propose the following computational pipeline for detecting cusp catastrophe signatures in reprogramming data:

**Step 1: Preprocessing.** For single-cell bisulfite sequencing (scBS-seq) or single-cell ATAC-seq data, perform standard quality control: remove cells with fewer than 500,000 CpGs covered (for methylation) or fewer than 5,000 peaks (for ATAC). Impute missing values using k-nearest-neighbor methods or probabilistic matrix factorization [28].

**Step 2: Feature selection.** Restrict to CpGs or peaks associated with (a) aging (Horvath clock CpGs, GrimAge surrogate CpGs) and (b) cell identity (lineage-specific enhancers, master transcription factor binding sites). This reduces dimensionality while preserving the biologically relevant axes of variation—the age and identity dimensions that define the cusp state variable *x*.

**Step 3: Distance computation.** Compute pairwise distances between cells using an appropriate metric. For methylation data, we recommend the Hamming distance on binarized methylation states (methylated/unmethylated at each CpG) or the Jensen-Shannon divergence for probabilistic methylation states [29]. For ATAC-seq, cosine distance on TF-IDF transformed peak counts is standard.

**Step 4: Persistent homology computation.** Compute Vietoris-Rips persistence diagrams using Ripser [30] or GUDHI [31] for each time point independently. For datasets exceeding 10⁵ cells, use approximate methods: sparse Rips filtrations [32], subsampling with bootstrap confidence intervals, or witness complexes [33].

**Step 5: Time-series analysis of persistence diagrams.** Track TBI(t) over time. Identify the critical time *t*_crit as the first time point where TBI exceeds the noise threshold. Compare *t*_crit across tissues or dosing conditions.

**Step 6: Hysteresis detection.** For experiments with factor withdrawal (pulse protocols), compare persistence diagrams of the ramp-up phase with the ramp-down phase at matched cumulative exposures. Persistent β₁ features in the combined data (concatenating cells from both phases) indicate hysteresis.

### 3.5 Superiority over Standard Methods

The TDA approach offers several advantages over standard bioinformatic methods for detecting the cusp catastrophe:

1. **Model-free detection.** UMAP and t-SNE require choosing embedding dimensions and are notoriously sensitive to hyperparameters [34]. TDA provides provably stable features (the bottleneck stability theorem guarantees that small perturbations of the data produce small changes in persistence diagrams) [35].

2. **Multi-scale resolution.** Persistent homology simultaneously captures cluster structure at all scales, avoiding the need to choose a single resolution parameter (unlike Leiden/Louvain clustering) [36].

3. **Hysteresis is a topological feature.** Standard clustering methods can detect bimodality but cannot distinguish reversible from irreversible bifurcations. The β₁ persistence of the hysteresis loop is a topological invariant that directly encodes path-dependence [37].

4. **Statistical framework.** Permutation tests on persistence landscapes [38] and confidence sets for persistence diagrams [39] provide rigorous statistical inference, enabling hypothesis testing (e.g., "is the bimodality signal significantly different from null expectation under smooth dynamics?").

### 3.6 Connection to the Cusp Surface

The persistence diagram is a data-driven mirror of the cusp catastrophe surface. Specifically:

- The birth time of the second β₀ feature corresponds to the entry into the bistable region of the cusp.
- The persistence of the second β₀ feature measures the "width" of the bistable region—the separation between the rejuvenated and dedifferentiated states.
- The β₁ persistence measures the "height" of the hysteresis loop—the energetic irreversibility of the transition.

By computing persistence diagrams at multiple dosing conditions (varying *a*) and multiple time points (varying *b*), one can reconstruct the cusp geometry entirely from data, without assuming any parametric model. This data-driven reconstruction provides an empirical cusp surface that can be compared with the theoretical predictions of Section 2—a powerful consistency check.

Rizvi et al. pioneered the application of persistent homology to single-cell RNA-seq data, demonstrating that topological features detected by TDA correspond to biologically meaningful branching events during hematopoietic differentiation [40]. Nicolau et al. applied the Mapper algorithm (a related TDA method) to identify a novel breast cancer subgroup with 100% survival that was invisible to standard methods [41]. These precedents establish the feasibility of TDA for detecting biologically meaningful topological transitions in single-cell data—exactly the application we propose here.

The field has accelerated dramatically in 2024–2025. A comprehensive 2025 review established TDA as a mature framework for single-cell biology, demonstrating applications across immune cell development, tumor heterogeneity, and developmental biology [324]. Topological and geometric analysis methods have been applied to single-cell transcriptomic data to reveal cell state transitions that conventional clustering misses [325]. Persistent homology has been applied to detect spatial patterning differences in human iPSC colonies, identifying topological signatures that predict loss of pluripotency before molecular markers change—directly relevant to our proposal for detecting the cusp catastrophe [326]. A persistent homology framework for scRNA-seq demonstrated that TDA can assess clustering robustness and quantify preprocessing effects on topological features, providing a rigorous statistical foundation for our TBI metric [327]. Multi-scale topological methods have been applied across heterogeneous cell populations to identify sorting and clustering behaviors driven by differential cell-cell adhesion [328]. Computational methods for TDA in biology have been comprehensively reviewed, establishing best practices for Ripser, GUDHI, and related software tools [329]. The application of TDA to chromatin organization through single-cell Hi-C contact maps has revealed topologically associating domain structures invisible to conventional methods [330].

---

## 4. Hidden Markov Models for Real-Time State Inference

### 4.1 The Latent State Problem

The cusp catastrophe framework (Section 2) describes the global landscape; persistent homology (Section 3) provides population-level detection of catastrophe signatures. For clinical translation, however, what is needed is **real-time inference of the latent state of individual cells or cell populations** during an ongoing reprogramming treatment—so that the dosing can be adjusted before cells cross the fold line.

This is precisely the problem that Hidden Markov Models (HMMs) are designed to solve: inferring a sequence of hidden states from noisy, incomplete observations [42]. HMMs have a distinguished history in computational biology, from gene finding [43] to protein structure prediction [44] to chromatin state annotation [45]. We now develop an HMM specifically tailored to partial reprogramming dynamics.

### 4.2 Model Specification

Define the HMM λ = (**S**, **O**, **A**, **B**, π) with the following components:

**Hidden state space S** = {S₁, S₂, S₃, S₄, S₅}:
- S₁: **Aged-differentiated.** The baseline state. Epigenetic clocks report chronological age; lineage markers fully expressed; chromatin in aged configuration (elevated H3K9me3 at pericentromeric regions, aberrant H3K4me3 distribution).
- S₂: **Early-rejuvenating.** Clocks beginning to reverse; lineage markers still intact; initial chromatin remodeling at age-associated loci.
- S₃: **At-the-fold.** The critical transitional state corresponding to the fold line of the cusp catastrophe. Clocks show substantial reversal; lineage markers beginning to fluctuate; chromatin in a metastable configuration with low barriers to dedifferentiation.
- S₄: **Dedifferentiating.** Lineage markers declining; pluripotency-associated markers (SSEA-4, TRA-1-60) beginning to appear; chromatin remodeling extending to identity loci.
- S₅: **Pluripotent.** Complete loss of somatic identity; pluripotency network activated; teratoma-competent.

**Observation space O:** A vector of *M* observable biomarkers measured at each time step. We define four categories of observables:

*Category 1: Methylation clocks.* Horvath multi-tissue clock, GrimAge, DunedinPACE, and tissue-specific clocks [46, 47, 48]. These provide a continuous readout of epigenetic age.

*Category 2: Surface markers.* Fibroblast identity markers (CD90/THY1, PDGFRα) that decrease during dedifferentiation; pluripotency markers (SSEA-4, TRA-1-60, SSEA-3) that increase [49]. These are measurable by flow cytometry or live-cell imaging.

*Category 3: Secreted proteins.* Collagen I and III (fibroblast function markers whose production is restored by rejuvenation [5]); GDF-15 (a senescence-associated secreted factor that should decrease with rejuvenation [50]); IL-6 (induced by OSKM via the SASP–reprogramming coupling [51]).

*Category 4: Chromatin accessibility.* Bulk or single-cell ATAC-seq signals at age-associated loci (gaining accessibility during rejuvenation) and lineage-specific enhancers (losing accessibility during dedifferentiation) [52].

**Transition matrix A** = [*a*_{ij}]₅ₓ₅, where *a*_{ij} = P(S_t = j | S_{t-1} = i). The transition probabilities are **dosage-dependent**: they vary with the current factor expression level. We parameterize:

$$a_{ij}(u) = a_{ij}^{(0)} + a_{ij}^{(1)} \cdot u(t)$$

where *u*(*t*) is the factor dosage at time *t* and *a*^(0), *a*^(1) are baseline and dosage-dependent components. Key structural constraints:

- Transitions are predominantly forward: *a*₁₂ > *a*₂₁ (factor exposure drives rejuvenation).
- The S₃ → S₄ transition is the critical one: *a*₃₄ increases sharply at the fold line, reflecting the catastrophic nature of the transition.
- The S₄ → S₃ transition is suppressed (hysteresis): *a*₄₃ ≈ 0 once the fold is crossed.
- Factor withdrawal (u → 0) allows recovery from S₂ and S₃ but not S₄ or S₅: *a*₂₁(0) > 0, *a*₃₂(0) > 0, but *a*₄₃(0) ≈ 0.

**Emission matrix B** = [*b*_j(*o*)]₅ₓ_M, where *b*_j(*o*) = P(O_t = *o* | S_t = j). For continuous observables, we model emissions as multivariate Gaussians:

$$b_j(\mathbf{o}) = \mathcal{N}(\mathbf{o}; \boldsymbol{\mu}_j, \boldsymbol{\Sigma}_j)$$

with state-specific mean vectors **μ**_j and covariance matrices **Σ**_j. For example, state S₁ has high Horvath age (μ₁,Horvath ≈ chronological age), high CD90 expression, and low SSEA-4; state S₅ has near-zero Horvath age, absent CD90, and high SSEA-4.

**Initial distribution** π = [π₁, ..., π₅]: For untreated cells, π₁ ≈ 1 (all cells start in the aged-differentiated state). For cells mid-treatment, π is set to the posterior state distribution from the previous time step.

### 4.3 The Three Classical HMM Problems

The three canonical problems associated with HMMs [42] map directly to the three key requirements of a closed-loop reprogramming controller:

**Problem 1: Evaluation (Forward Algorithm).** Given the model λ and an observation sequence **O** = (*o*₁, ..., *o*_T), compute P(**O** | λ)—the likelihood of the observed data under the model. This is solved by the forward algorithm:

$$\alpha_t(j) = P(o_1, \ldots, o_t, S_t = j \mid \lambda)$$

with recursion:

$$\alpha_t(j) = \left[\sum_{i=1}^{5} \alpha_{t-1}(i) \cdot a_{ij}(u_{t-1})\right] \cdot b_j(o_t)$$

initialized with α₁(j) = π_j · b_j(o₁). The total likelihood is P(**O** | λ) = Σ_j α_T(j). **Application:** Model selection—comparing different parameterizations of the transition matrix to determine which best fits the observed reprogramming dynamics.

**Problem 2: Decoding (Viterbi Algorithm).** Given the model λ and an observation sequence **O**, find the most likely sequence of hidden states S* = argmax_{S} P(S | **O**, λ). This is solved by the Viterbi algorithm [53]:

$$\delta_t(j) = \max_{i} \left[\delta_{t-1}(i) \cdot a_{ij}(u_{t-1})\right] \cdot b_j(o_t)$$

with backtracking to recover the optimal state sequence. **Application:** Post-hoc analysis of completed reprogramming experiments—determining the most likely trajectory through the state space for each cell or sample.

**Problem 3: Learning (Baum-Welch / EM Algorithm).** Given an observation sequence **O** (or multiple sequences), estimate the model parameters λ = (**A**, **B**, π) that maximize P(**O** | λ). This is solved by the Baum-Welch algorithm [54], an instance of expectation-maximization (EM):

*E-step:* Compute forward (α) and backward (β) variables:

$$\beta_t(i) = \sum_{j=1}^{5} a_{ij}(u_t) \cdot b_j(o_{t+1}) \cdot \beta_{t+1}(j)$$

Then compute the posterior state probabilities:

$$\gamma_t(j) = \frac{\alpha_t(j) \cdot \beta_t(j)}{\sum_{k=1}^{5} \alpha_t(k) \cdot \beta_t(k)}$$

and the posterior transition probabilities:

$$\xi_t(i,j) = \frac{\alpha_t(i) \cdot a_{ij}(u_t) \cdot b_j(o_{t+1}) \cdot \beta_{t+1}(j)}{\sum_{k}\sum_{l} \alpha_t(k) \cdot a_{kl}(u_t) \cdot b_l(o_{t+1}) \cdot \beta_{t+1}(l)}$$

*M-step:* Update parameters:

$$\hat{a}_{ij} = \frac{\sum_{t=1}^{T-1} \xi_t(i,j)}{\sum_{t=1}^{T-1} \gamma_t(i)}, \quad \hat{\boldsymbol{\mu}}_j = \frac{\sum_{t=1}^{T} \gamma_t(j) \cdot \mathbf{o}_t}{\sum_{t=1}^{T} \gamma_t(j)}$$

**Application:** Training the HMM on existing multi-omic time course datasets (e.g., Gill et al. MPTR data [5], Olova et al. 49-day iPSC time course [19]) to learn the state-specific emission parameters and transition rates.

### 4.4 Online State Estimation for Closed-Loop Control

For real-time control, the critical quantity is the **posterior probability of state S₃ (at-the-fold) or S₄ (dedifferentiating)** at the current time step, given all observations so far:

$$P(S_t \in \{S_3, S_4\} \mid o_1, \ldots, o_t) = \gamma_t(3) + \gamma_t(4)$$

This quantity, computed online via the forward algorithm (which requires only O(*N*²) operations per time step, where *N* = 5 states), provides the **alarm signal** for the closed-loop controller. The control rule is:

$$u(t+1) = \begin{cases} u_{\text{nominal}} & \text{if } \gamma_t(3) + \gamma_t(4) < \theta_{\text{safe}} \\ u_{\text{reduced}} & \text{if } \theta_{\text{safe}} \leq \gamma_t(3) + \gamma_t(4) < \theta_{\text{alarm}} \\ 0 & \text{if } \gamma_t(3) + \gamma_t(4) \geq \theta_{\text{alarm}} \end{cases}$$

where θ_safe and θ_alarm are calibrated thresholds. In Section 6, we connect this HMM-based controller to specific biological actuators.

### 4.5 Training Data Requirements and Multi-Omic Integration

Training the HMM requires multi-omic time course data with the following characteristics:

**Temporal resolution.** The Nyquist criterion requires sampling at least twice per state transition. Given that the S₂ → S₃ transition occurs over approximately 2–3 days in fibroblast MPTR [5], sampling every 6–12 hours during the critical window (days 8–18) is necessary.

**Multi-modal coverage.** Each time point should include at least two observation modalities (e.g., methylation + surface markers, or ATAC-seq + secreted proteins) to resolve ambiguities between states. Single-modality observations are insufficient because multiple states may produce similar emissions in one modality while being distinguishable in another [55].

**Single-cell resolution.** Population-level measurements average over the distribution of hidden states, obscuring the bimodality that signals S₃ occupancy. Single-cell multi-omics (e.g., 10x Multiome for joint RNA + ATAC, or SHARE-seq [56]) provide the resolution needed to train cell-level HMMs.

**Existing datasets that could serve as training data include:** the Gill et al. MPTR methylation time course [5], the Olova et al. iPSC reprogramming time course with Infinium 450K methylation arrays at multiple intermediate time points [19], and the Roux et al. single-cell RNA-seq time course of factor-combination screening at Calico [57].

### 4.6 Connection to Catastrophe Theory

The HMM encodes the cusp catastrophe in a computationally tractable form. The five hidden states partition the cusp surface into discrete regions:

- S₁ occupies the monostable region above the cusp (a > 0).
- S₂ occupies the bistable region near the upper fold (rejuvenated minimum).
- S₃ straddles the lower fold line (the catastrophe boundary).
- S₄ and S₅ occupy the region below the lower fold (dedifferentiated basin).

The dosage-dependent transition matrix encodes the key dynamical feature of the cusp: the S₃ → S₄ transition rate increases sharply as cumulative exposure approaches the fold, reflecting the vanishing barrier. The asymmetry a₃₄ ≫ a₄₃ encodes hysteresis.

The HMM thus serves as a **discrete approximation to the continuous cusp dynamics** that is computationally efficient for online inference. While the continuous model (Section 2) provides analytical predictions and geometric intuition, the HMM provides the algorithmic machinery for real-time decision-making.

Recent methodological advances strengthen the feasibility of this approach. CellRank 2, published in 2022, generalized directed single-cell fate mapping beyond RNA velocity to exploit pseudotime, developmental potential, metabolic labels, and real-time information, providing a complementary framework for trajectory inference that could be integrated with our HMM [331]. Transformative advances in single-cell omics foundation models—including scGPT, Geneformer, and scBERT—have demonstrated that transformer architectures trained on millions of single-cell profiles can learn transferable representations of cellular state that outperform hand-crafted features for cell type classification and perturbation response prediction [332]. These foundation models could serve as feature extractors for the HMM emission model, replacing hand-selected biomarker panels with learned latent representations. Multi-omic integration methods such as MOFA+ and scMKL enable principled combination of RNA, ATAC, and methylation modalities within a single probabilistic framework, directly applicable to the multi-modal emissions our HMM requires [333, 334]. The quantification of landscape and flux from single-cell omics has been formalized using decomposition methods that separate gradient (potential) from rotational (flux) components, providing a theoretical bridge between our HMM state inference and the cusp catastrophe landscape [335]. The reimplementation of HMM algorithms in the pomegranate library with modern API and GPU acceleration makes the computational requirements for real-time inference tractable even for large cell populations [336].

---

## 5. Cooperative Chromatin Transitions: An Ising/Potts Framework

### 5.1 Chromatin as a Lattice of Interacting Sites

The mathematical frameworks of Sections 2–4 treat the epigenetic state as a scalar or vector quantity evolving in response to external perturbations. But what is the *mechanism* by which reprogramming factors induce the catastrophic transitions described by the cusp model? We now develop a microscopic model grounded in the physics of chromatin modification, drawing on the Ising model from statistical mechanics—a framework with deep roots in condensed matter physics and growing applications in epigenetics [58].

The fundamental unit of chromatin is the nucleosome: ~147 base pairs of DNA wrapped around an octamer of histone proteins (two copies each of H2A, H2B, H3, and H4). The histone tails protruding from the nucleosome can be covalently modified at specific residues—methylation, acetylation, phosphorylation, ubiquitination—creating a combinatorial code that influences gene expression and chromatin compaction [59]. Crucially, these modifications interact: a modified nucleosome can recruit enzymes that similarly modify neighboring nucleosomes, creating a positive feedback loop that enables the spreading and maintenance of chromatin states [60].

Dodd et al. formalized this feedback in a stochastic model of epigenetic memory, showing that the reader-writer coupling between modified nucleosomes and modifying enzymes can produce bistable chromatin domains—regions that stably maintain either an active or silenced state—analogous to the ferromagnetic phase transition in the Ising model [61]. Sneppen and colleagues extended this framework to include the competition between antagonistic modification systems (e.g., Polycomb-mediated silencing vs. Trithorax-mediated activation), deriving phase diagrams that predict the stability and switching dynamics of epigenetic states [62].

### 5.2 The 1D Ising Model for Chromatin Domains

Consider a linear array of *N* nucleosomes within a chromatin domain (a typical TAD contains ~100–500 nucleosomes spanning 50–500 kb). Each nucleosome *i* can be in one of two modification states: σ_i = +1 ("aged," bearing H3K9me3 and other heterochromatin marks) or σ_i = −1 ("rejuvenated," bearing H3K4me3, H3K27ac, and other euchromatin marks). The Hamiltonian (energy function) of the domain is:

$$H(\boldsymbol{\sigma}) = -J \sum_{i=1}^{N-1} \sigma_i \sigma_{i+1} - h \sum_{i=1}^{N} \sigma_i$$

where:
- *J* > 0 is the **coupling constant**, representing the strength of nearest-neighbor reader-writer interactions. Biochemically, *J* arises from the feedback loop in which, for example, the H3K9me3-recognizing chromodomain of HP1α recruits the H3K9 methyltransferase SUV39H1, which methylates the adjacent nucleosome [63]. The coupling constant can be estimated from the processivity of reader-writer complexes: PRC2 (which writes H3K27me3 and reads it through its EED subunit) has a measured processivity of ~5–20 nucleosomes before dissociation [64], corresponding to *J* ≈ 0.5–2.0 *k*_B*T* per nucleosome contact.

- *h* is the **external field**, representing the bias toward one modification state. In the context of partial reprogramming, *h* corresponds to the net effect of OSK factor expression: factors promote the removal of aging-associated marks and the installation of rejuvenation-associated marks, effectively applying a negative field that favors σ = −1 (rejuvenated). The field strength is proportional to factor dosage: *h* = *h*₀ · *u*(*t*), where *u*(*t*) is the factor expression level.

### 5.3 Phase Transition and Critical Dosage

In the thermodynamic limit (*N* → ∞), the one-dimensional Ising model has no phase transition at finite temperature (the Mermin-Wagner-Hohenberg theorem). However, for **finite** chromatin domains—typically *N* ~ 100–500 nucleosomes—the system exhibits a **crossover** from one quasi-stable state to another as the field *h* crosses a critical value. This crossover sharpens as *J* increases (stronger reader-writer coupling) and is well-described by a mean-field approximation for large *N* [65].

In the mean-field approximation, the average magnetization *m* = ⟨σ_i⟩ (average modification state) satisfies the self-consistency equation:

$$m = \tanh\left(\frac{2Jm + h}{k_BT}\right)$$

For *h* = 0 (no factors), this equation has three solutions when *J* > *k*_B*T*/2: *m* = ±*m*₀ (the two ordered states) and *m* = 0 (the unstable disordered state). This is the bistability between the aged and rejuvenated chromatin configurations.

The **critical field** *h*_c at which the bistability disappears (the less favored state ceases to be metastable) is, in mean-field theory:

$$h_c = \frac{2J}{3}\left(1 - \frac{k_BT}{2J}\right)^{3/2} \cdot \sqrt{3}$$

This critical field has a direct biological interpretation: it is the **minimum factor dosage** required to destabilize the aged chromatin state and enable switching to the rejuvenated state. Dosages below *h*_c produce no lasting change—the aged state is robust. Dosages above *h*_c initiate a domain-level switch via **nucleation and growth**: a small seed of rejuvenated nucleosomes (the nucleus) forms stochastically and, if it exceeds the critical size, grows to convert the entire domain.

### 5.4 Nucleation-Growth Dynamics

The switching of a chromatin domain from aged to rejuvenated proceeds by classical nucleation-growth kinetics [66]. A fluctuation creates a seed of *n* rejuvenated nucleosomes within the aged domain. The free energy cost of this seed has two competing terms:

$$\Delta G(n) = -2|h| \cdot n + 2J_{\text{eff}}$$

The first term is the energy gain from placing *n* nucleosomes in the field-favored (rejuvenated) state. The second term is the "surface energy" cost of creating two domain boundaries between the rejuvenated seed and the surrounding aged chromatin (each boundary costs *J*_eff ≈ *J* per broken favorable contact).

The critical nucleus size is:

$$n^* = \frac{J_{\text{eff}}}{|h|}$$

For *n* < *n**, the seed is unstable and shrinks back. For *n* > *n**, the seed is energetically favorable and grows until it converts the entire domain. The nucleation rate (number of successful switches per unit time per domain) is:

$$k_{\text{nuc}} \sim \exp\left(-\frac{\Delta G(n^*)}{k_BT}\right) = \exp\left(-\frac{J_{\text{eff}}^2}{|h| \cdot k_BT}\right)$$

This expression reveals a key feature: the switching rate depends **exponentially** on the inverse of the field strength. Near the critical field (*h* ≈ *h*_c), the nucleation barrier vanishes and switching becomes rapid—a domain-level analog of the fold catastrophe. The domain switches cooperatively (all-or-nothing), producing a discontinuous change in modification state at the single-domain level even though the external field changes continuously.

### 5.5 Potts Extension: Four Chromatin States

The binary Ising model is a simplification. In reality, nucleosomes can exist in more than two modification states relevant to reprogramming. We extend to a *q*-state Potts model [67] with *q* = 4 states:

- σ = 1: **Aged-silenced.** H3K9me3, HP1-bound, late-replicating. Characteristic of aged heterochromatin that has accumulated stochastically with aging.
- σ = 2: **Aged-active.** H3K4me1, H3K27ac, tissue-specific enhancer marks. These represent the cell-identity marks that should be *preserved* during rejuvenation.
- σ = 3: **Rejuvenated-active.** H3K4me3, H3K27ac, similar to σ = 2 but with age-associated aberrant marks removed. This is the target state.
- σ = 4: **Pluripotent.** H3K4me3 at pluripotency loci, bivalent H3K4me3/H3K27me3 at developmental loci. This is the dedifferentiated state to be avoided.

The Potts Hamiltonian is:

$$H(\boldsymbol{\sigma}) = -\sum_{i=1}^{N-1} J_{\sigma_i, \sigma_{i+1}} - \sum_{i=1}^{N} h_{\sigma_i}$$

where *J*_{σ,σ′} is a state-dependent coupling matrix (like states couple more strongly than unlike states) and *h*_σ is a state-dependent field (reprogramming factors favor σ = 3 and σ = 4 over σ = 1; the cell's identity maintenance machinery favors σ = 2).

The critical insight from the Potts model is that the **rejuvenated state (σ = 3) is metastable** with a shallow energy minimum. It is favored over the aged state (σ = 1) when factors are present but is separated from the pluripotent state (σ = 4) by a barrier of only ~1–2 *k*_B*T*, compared to the ~3–5 *k*_B*T* barrier between aged and rejuvenated states. This asymmetry means that once a domain has switched from aged to rejuvenated, continued factor exposure readily pushes it over the smaller barrier into the pluripotent state—the microscopic mechanism underlying the macroscopic cusp catastrophe.

### 5.6 Mean-Field Theory: From Domains to Populations

The human genome contains approximately 10,000–20,000 chromatin domains (TADs) [68], each switching quasi-independently between modification states. At the population level (a single cell with many domains), the aggregate epigenetic state—as measured by methylation clocks—is the average over many domains:

$$\bar{m} = \frac{1}{N_{\text{domains}}} \sum_{d=1}^{N_{\text{domains}}} m_d$$

where *m_d* is the magnetization (modification state) of domain *d*. By the central limit theorem, even if individual domains switch discontinuously (via nucleation-growth), the average over ~10,000 domains produces a **smooth, approximately Gaussian** distribution of clock values at the population level.

This resolves an apparent paradox: epigenetic clocks, which average over hundreds of CpG sites (353 for Horvath, 71 for Hannum), show smooth dose-response curves [69], yet the underlying chromatin transitions at individual loci are discontinuous. The smoothness is an artifact of averaging over many independent binary (or multi-state) switches—analogous to how the magnetization of a macroscopic magnet appears smooth even though individual atomic spins flip discontinuously.

However, this averaging also means that **population-level clock measurements are poor detectors of the cusp catastrophe**. By the time the population-average clock value shifts dramatically, many individual domains have already crossed the fold. Single-cell measurements, which resolve the domain-level stochasticity, are essential for detecting the bimodality signature predicted by the cusp model—reinforcing the need for the single-cell TDA approach of Section 3.

### 5.7 Connection to the Cusp Catastrophe

The Ising/Potts model provides the **microscopic mechanism** underlying the macroscopic cusp catastrophe:

- The **state variable** *x* of the cusp model (epigenetic position) corresponds to the mean magnetization $\bar{m}$ averaged over all domains.
- The **control parameter** *a* (factor concentration) corresponds to the external field *h*.
- The **control parameter** *b* (cumulative exposure) corresponds to the accumulated effect of the field over time, which progressively converts more domains past the nucleation threshold.
- The **fold catastrophe** at the macroscopic level emerges from the cooperative, discontinuous switching of individual domains: as cumulative exposure increases, more and more domains undergo nucleation-growth transitions, and at the critical exposure, the fraction of switched domains crosses a percolation-like threshold that commits the entire cell to a new state.
- The **metastability of the rejuvenated state** (σ = 3 in the Potts model) provides the microscopic explanation for why partially reprogrammed cells are fragile and prone to either reverting to the aged state (upon factor withdrawal) or progressing to the pluripotent state (upon continued exposure).

Recent experimental and theoretical work provides strong support for the Ising/Potts framework applied to chromatin. A 2024 study demonstrated two-way feedback between chromatin compaction and histone modification state in *S. cerevisiae*, showing that bistable heterochromatin states arise from the interplay of reader-writer enzymes and three-dimensional chromatin folding—precisely the mechanism our model invokes [337]. The PRC2 complex, a key writer of H3K27me3, has been shown to operate through distinct PRC2.1 and PRC2.2 subcomplexes with different genomic targeting mechanisms and allosteric regulation, refining our understanding of the coupling constant *J* [338]. Single-molecule analysis of chromatin ubiquitylation by variant PRC1 complexes revealed the kinetics of mark deposition at individual nucleosomes, providing direct measurements of the reader-writer rate constants that parameterize our model [339]. DNA sequence and chromatin modifiers have been shown to cooperate to confer epigenetic bistability at imprinting control regions, providing a genomic context where the Ising model predictions can be directly tested [340]. A comprehensive mathematical model integrating 73 publications on Polycomb/Trithorax biochemistry predicted that poised chromatin is bistable rather than bivalent, supporting our four-state Potts model where the "poised" state corresponds to the metastable rejuvenated configuration [341]. Dynamic histone modification patterns that coordinate DNA processes—including transcription, replication, and repair—have been systematically characterized, revealing the timescales over which chromatin states equilibrate after perturbation [342]. Pioneer transcription factor cooperativity has been shown to depend on histone modifications, with OCT4 binding inducing structural changes in nucleosomes that facilitate cooperative SOX2 binding—a direct demonstration of the reader-writer cooperativity that drives domain-level transitions in our Ising model [343].

---

## 6. Engineering Closed-Loop Reprogramming

### 6.1 Control Architecture

The mathematical frameworks of Sections 2–5 converge on a unified closed-loop control architecture for precision partial reprogramming:

```
┌─────────────┐    ┌──────────────┐    ┌────────────┐    ┌──────────────┐
│   SENSORS   │───▶│  ESTIMATOR   │───▶│ CONTROLLER │───▶│   ACTUATOR   │
│             │    │   (HMM)      │    │            │    │              │
│ Clock CpGs  │    │ Forward alg. │    │ Threshold  │    │ synNotch     │
│ Surface     │    │ P(S₃∪S₄|O)   │    │ logic      │    │ miRNA switch │
│ Secretome   │    │              │    │            │    │ Optogenetics │
│ ATAC peaks  │    │              │    │            │    │              │
└─────────────┘    └──────────────┘    └────────────┘    └──────────────┘
       ▲                                                        │
       └────────────────────────────────────────────────────────┘
                          Feedback loop
```

The controller's objective is to keep the system trajectory within the **smooth rejuvenation region** of the cusp surface—the region between the upper fold (rejuvenation onset) and the lower fold (dedifferentiation threshold)—and to withdraw factors before any significant fraction of cells cross the lower fold.

### 6.2 Sensor Modalities

**Molecular sensors.** Engineered reporter constructs can provide real-time readout of reprogramming state:

- **Pluripotency reporters.** A synthetic promoter containing OCT4 and NANOG binding sites driving a destabilized fluorescent protein (d2GFP) provides a live readout of pluripotency network activation [70]. Fluorescence above a threshold signals S₄/S₅ entry.

- **Identity reporters.** Lineage-specific enhancers (e.g., the fibroblast-specific TGFBI enhancer) driving a different fluorescent protein (mCherry) provide a live readout of identity maintenance. Loss of fluorescence signals identity erosion.

- **Dual-reporter ratio.** The ratio of pluripotency reporter to identity reporter signal provides a single scalar that tracks position along the cusp state variable *x*. This ratio can be monitored by live-cell microscopy or flow cytometry at the single-cell level.

**Molecular clocks as sensors.** While full methylation clock measurement requires bisulfite sequencing, targeted readout of a small panel of "sentinel" CpGs (those with the highest weights in the Horvath clock) using methylation-sensitive restriction enzymes [71] or nanopore sequencing [72] could provide a faster, more scalable clock readout. Mintun et al. developed rapid targeted methylation assays that can quantify individual CpG methylation states within hours rather than days [73].

### 6.3 Engineered Actuators

Three classes of biological actuators can implement the closed-loop control policy:

**Actuator 1: synNotch-based kill switch.** synNotch receptors [74] can be engineered to detect dedifferentiation-associated surface markers. We propose a synNotch receptor whose extracellular domain recognizes SSEA-4 (a glycolipid upregulated early in dedifferentiation [75]) and whose intracellular domain releases a synthetic transcription factor activating expression of a safety gene—either iCasp9 (inducible caspase-9, triggering apoptosis [76]) for an irreversible kill switch, or a dominant-negative form of OCT4 for a reversible factor antagonist.

The key advantage of this design is **cell-autonomous operation**: each cell monitors its own state and responds independently, without requiring external input. This addresses the fundamental limitation of population-level dosing: even in a homogeneous external dose, individual cells may be at different distances from the fold line due to stochastic variation.

**Actuator 2: miRNA-responsive 3′-UTR.** An elegant molecular feedback mechanism exploits the endogenous miRNA profile as a state sensor. The miR-302 cluster is a hallmark of the pluripotent state, expressed at high levels in embryonic stem cells and induced pluripotent stem cells but absent from differentiated somatic cells [77]. By incorporating miR-302 binding sites into the 3′-UTR of the reprogramming factor mRNA, one creates a **self-limiting circuit**: as cells approach pluripotency and begin expressing miR-302, the miRNA degrades the very mRNA encoding the reprogramming factors, reducing factor levels precisely when they are most dangerous.

Similarly, miR-200c is upregulated during the mesenchymal-to-epithelial transition that accompanies early reprogramming [78]. Incorporating miR-200c responsive elements creates an earlier-acting brake that reduces factor expression as cells undergo the initial epithelial transition—a safety margin before dedifferentiation proper.

The molecular implementation uses engineered mRNA with a 3′-UTR containing four tandem miR-302 target sites, achieving approximately 10-fold translational repression in cells expressing miR-302 [79]. For mRNA-LNP delivery of reprogramming factors—the modality with the best translational profile for pulsatile dosing—this approach requires no additional genetic cargo: the miRNA sensitivity is built into the same mRNA encoding the factors.

**Actuator 3: Optogenetic spatiotemporal control.** For spatially heterogeneous tissues, optogenetic control of reprogramming factor expression enables cell-by-cell dosing [80]. The CRY2-CIB1 blue light-inducible system [81], or the more recently developed PhiReX2 red light-switchable system [82], can be used to drive factor expression only in illuminated regions. Combined with live fluorescence imaging of dual reporters (Section 6.2), this enables a true feedback loop: cells whose reporter ratio approaches the danger threshold can have their light stimulus reduced, while cells still in the safe rejuvenation zone continue receiving light.

Spatially patterned illumination using digital micromirror devices (DMDs) achieves single-cell resolution over millimeter-scale fields of view [83]. For *in vitro* applications (cell therapy manufacturing, rejuvenation of autologous fibroblasts for wound healing), this approach is immediately feasible. For *in vivo* applications, implantable fiber-optic systems [84] or upconversion nanoparticle-mediated near-infrared to visible light conversion [85] could provide the necessary light delivery.

### 6.4 Controller Design

The closed-loop controller integrates information from multiple sensor channels through the HMM estimator (Section 4) and maps the estimated state to actuator commands.

**Level 1: Autonomous molecular feedback.** The miRNA-responsive 3′-UTR (Actuator 2) operates constitutively without external input, providing a baseline safety net.

**Level 2: Cell-autonomous synNotch.** The synNotch kill switch (Actuator 1) provides an irreversible safety mechanism for cells that bypass Level 1.

**Level 3: Population-level feedback.** For optogenetic (Actuator 3) or externally administered systems (mRNA-LNP dosing schedule), the HMM-based estimator processes population measurements (flow cytometry, bulk methylation) and adjusts the next dose accordingly:

- If P(S₃ ∪ S₄ | observations) < 0.05: continue nominal dosing.
- If 0.05 ≤ P(S₃ ∪ S₄ | observations) < 0.20: reduce dose by 50%.
- If P(S₃ ∪ S₄ | observations) ≥ 0.20: halt dosing, allow recovery period.

**Level 4: Topological surveillance.** At each dosing interval, compute the TBI (Section 3.3) from single-cell data. If TBI exceeds the calibrated threshold, override Levels 1–3 and halt all factor delivery, as the population has entered the bistable regime.

This multi-level architecture provides defense-in-depth: molecular feedback operates at the fastest timescale (minutes), synNotch at the cellular decision timescale (hours), population HMM at the dosing interval timescale (days), and topological surveillance at the protocol assessment timescale (multi-day).

Recent advances in each actuator class strengthen the feasibility of this architecture. For synNotch-based circuits, a 2025 review catalogued the expanding repertoire of synNotch variants with improved signal-to-noise ratios, reduced ligand-independent activation, and compatibility with primary human cells [344]. Ligand-restricted synNotch switches published in 2025 demonstrated enhanced precision in distinguishing membrane-bound from soluble antigens, critical for avoiding false activation by shed markers [345]. A synthetic genetic switch for spatiotemporal control of engineered cells combined synNotch with degradation-based timers, achieving transient therapeutic gene expression that autonomously terminates—ideal for pulsatile reprogramming [346]. Synthetic gene circuits for regulation of next-generation cell-based therapeutics have been comprehensively reviewed, establishing design principles for multi-input logic gates, feedback controllers, and safety mechanisms [347].

For optogenetic control, a 2025 study reported the DEL-VPR photoswitch achieving up to 570-fold induction of target gene expression by blue light, sufficient to drive therapeutic levels of reprogramming factor expression with tight off-state silencing [348]. The BLU-VIPR system demonstrated optogenetic gene editing *in vivo*, including in T lymphocytes previously intractable to optogenetic control, establishing that light-inducible systems can operate in clinically relevant cell types [349]. Opto-CRISPR strategies combining light-inducible Cas proteins with gRNA regulation have been reviewed as emerging tools for precise spatiotemporal gene perturbation [350].

For LNP-based delivery, liposomal lipid nanoparticle architectures with enhanced extrahepatic delivery were reported in Nature Communications in 2025, demonstrating that incorporation of bilayer-forming lipids extends circulation lifetime and increases lung and spleen transfection [351]. Lipid tail length has been identified as a key determinant of organ selectivity: N-series lipids with amide bonds target the lung, while O-series lipids with ester bonds maintain liver tropism [352]. Reformulated LNPs incorporating cholic acid in place of cholesterol shifted mRNA accumulation from liver to spleen, providing orthogonal tissue targeting [353]. Tissue-specific miRNA sequences inserted into the 3′-UTR of LNP-delivered mRNA can suppress expression in off-target organs while maintaining on-target translation [354]. These advances collectively address the major delivery challenge for closed-loop reprogramming: achieving tissue-specific, temporally controllable factor expression. A 2025 study further demonstrated that LNP-delivered mRNA can be tracked at the particle, transcript, and protein level simultaneously, enabling real-time quantification of delivery efficiency that is essential for calibrating the closed-loop controller [381].

### 6.5 Staying in the Safe Region of the Cusp Surface

The closed-loop controller's geometric objective can be stated precisely in terms of the cusp surface: **maintain the system trajectory within the region bounded by the upper fold line and a safety margin ε below the lower fold line**, where ε is chosen to account for the maximum stochastic fluctuation in cumulative exposure.

<!--
Formally, define the safe region as:

$$\mathcal{S} = \left\{(a, b) : \Delta(a, b) > \epsilon_{\text{safety}} \text{ or } a > 0 \right\}$$

where Δ(*a*, *b*) = 4*a*³ + 27*b*² is the discriminant and ε_safety is calibrated from the estimated noise intensity *D* (Section 2.6). The controller adjusts the factor dosage *u*(*t*)—which maps to the control parameters (*a*, *b*)—to ensure that the trajectory remains within S.
-->

---

## 7. Experimental Validation Framework

### 7.1 In Vitro Validation: Dense Time-Course Fibroblast MPTR

**Experiment 1: Bimodality detection.** Perform human dermal fibroblast MPTR with dense temporal sampling (every 6 hours from day 8 to day 18) using single-cell bisulfite sequencing (scBS-seq) at each time point (~500 cells per time point). Compute:
- Single-cell Horvath ages.
- Hartigan's dip test [86] for unimodality at each time point.
- Persistence diagrams (Section 3) for each time point.
- TBI(t) trajectory.

**Expected result under cusp hypothesis:** Dip test rejects unimodality at a critical time (predicted: day 12–14 for standard MPTR conditions). TBI shows a sharp increase at the same time. Under smooth dynamics (null hypothesis), the dip test never rejects unimodality and TBI remains near zero.

**Experiment 2: Dose-dependent critical time.** Repeat Experiment 1 at three dosage levels (0.5×, 1×, 2× standard Sendai virus titer). Measure the critical time *t*_crit at each dose.

**Expected result under cusp hypothesis:** *t*_crit decreases superlinearly with dose, approximately as dose^{−3/2}, reflecting the cubic scaling of the bifurcation set. Under smooth dynamics, *t*_crit would decrease linearly or sublinearly.

**Experiment 3: Hysteresis test.** At day 12 (within the predicted bistable window), split the culture: half continues OSKM exposure, half has factors withdrawn. At day 18, perform scBS-seq on both halves.

**Expected result under cusp hypothesis:** The withdrawal group shows recovery of unimodal aged-differentiated distribution (cells that had not crossed the fold return to base). The continued-exposure group shows bimodal distribution (some cells dedifferentiated, some still rejuvenated). Critically, identify cells in the withdrawal group that fail to recover (cells that had already crossed the fold before withdrawal)—these should form a distinct subpopulation at a younger epigenetic age.

### 7.2 TDA Validation: Reanalysis of Existing Published Datasets

Several published datasets are immediately amenable to TDA reanalysis:

**Dataset 1: Olova et al. 49-day iPSC reprogramming time course** [19]. This dataset includes Infinium 450K methylation arrays at multiple intermediate time points during OKSM-mediated reprogramming of human fibroblasts to iPSCs. Compute persistence diagrams at each time point and identify the time at which β₀ transitions from one to two persistent features.

**Dataset 2: Roux et al. single-cell RNA-seq of factor combinations** [57]. This dataset contains thousands of single cells profiled at multiple time points during reprogramming with various combinations of Yamanaka factors. Apply TDA to identify which factor combinations produce topological signatures consistent with cusp dynamics (bimodality) versus smooth dynamics (unimodality).

**Dataset 3: Cacchiarelli et al. single-cell RNA-seq of reprogramming intermediates** [87]. This study profiled over 30,000 cells during reprogramming at five time points, identifying distinct trajectories including productive and "dead-end" paths. TDA may reveal topological features (loops, branches) not captured by the original UMAP-based analysis.

### 7.3 HMM Validation: Predictive Power

**Experiment 4: Prediction of dedifferentiation from early observations.** Train the HMM (Section 4) on the first half of a reprogramming time course (days 0–10). Use the trained model to predict, at day 10, which cells are in state S₃ (at-the-fold). Then continue the experiment to day 20 and verify whether the cells predicted to be at S₃ at day 10 are the ones that have dedifferentiated by day 20.

**Expected result:** Cells assigned high P(S₃) at day 10 by the HMM should be significantly enriched for dedifferentiation markers at day 20, compared to cells assigned low P(S₃). The area under the ROC curve (AUC) for this prediction should exceed 0.75 (vs. 0.50 for random).

### 7.4 Ising Model Validation: Chromatin Domain Switching Kinetics

**Experiment 5: ATAC-seq domain switching.** Perform single-cell ATAC-seq at 12-hour intervals during days 10–16 of fibroblast MPTR. For each cell, compute the accessibility state of each TAD (binarized: open/closed relative to baseline). Track the fraction of TADs in the "rejuvenated" state over time.

**Expected result under Ising model:** Individual TADs switch discontinuously (binary, not gradual), with the switching time distributed exponentially (Poisson process with rate k_nuc). The cumulative fraction of switched TADs should follow a sigmoidal curve (integration of the exponential) rather than a linear ramp. The switching rate should increase with factor dosage, with the critical dosage identifiable as the inflection point of the sigmoid.

**Experiment 6: Nucleation size.** For TADs caught mid-switch (partially accessible), examine the spatial distribution of accessibility changes. Under the nucleation-growth model, one should observe a contiguous block of rejuvenated nucleosomes expanding from a seed, rather than random, scattered accessibility changes throughout the TAD.

---

## 8. Discussion

### 8.1 Clinical Trial Design Implications

The cusp catastrophe framework has immediate implications for the design of partial reprogramming clinical trials. Current trial designs (e.g., the Life Biosciences ER-100 Phase 1 trial for optic neuropathies [2]) use fixed-dose protocols—all patients in a cohort receive the same AAV titer and the same induction schedule. This is appropriate for Phase 1 safety determination, but the cusp framework predicts that fixed-dose protocols will produce highly variable outcomes due to patient-to-patient differences in starting epigenetic state (which determine distance to the fold line).

We propose that Phase 2 trials should incorporate **biomarker-guided adaptive dosing**, where methylation clock measurements and/or reporter readouts at interim time points guide dose escalation or de-escalation for individual patients. The HMM framework (Section 4) provides the algorithmic infrastructure for such adaptive designs: train the HMM on Phase 1 data, then use it to estimate each patient's latent state at interim visits and adjust dosing accordingly.

More broadly, the cusp framework suggests that the relevant parameter space for clinical optimization is not a simple dose-response curve but a two-dimensional surface (*a*, *b*) with a discontinuity. Traditional dose-finding designs (e.g., the 3+3 design or Bayesian optimal interval designs) assume monotonic dose-response relationships and are not designed to navigate cusp geometries [88]. Novel trial designs that sample the two-dimensional (*a*, *b*) space and explicitly test for bimodality in outcome distributions may be needed.

### 8.2 Tissue-Specificity: Each Tissue Has Its Own Cusp

A key implication of the cusp framework is that each tissue type has its own cusp surface parameters—its own critical dosage, critical duration, and barrier heights. The starting epigenetic position *x*₀, the coupling constant *J* (reader-writer processivity), and the noise intensity *D* all vary across tissues.

For the retina (the ER-100 target tissue), the situation is relatively favorable: retinal ganglion cells are post-mitotic, have large δ (distance to fold), and have demonstrated safety under continuous OSK expression for 15 months in mice [3]. For the liver—the most vulnerable tissue—the narrow therapeutic window demands extreme precision in dosing and potentially tissue-specific factor formulations (e.g., hepatocyte-detargeted LNPs).

A comprehensive "cusp atlas" mapping the catastrophe parameters for each human tissue type would be an invaluable resource for the field. Recent multi-omics characterization of partial chemical reprogramming has provided the first systematic evidence that rejuvenation and dedifferentiation are molecularly separable at the proteomic, phosphoproteomic, and metabolomic levels, not just at the transcriptomic and epigenomic levels [363]. The identification of SB000 as a single gene sufficient to rejuvenate cells from multiple germ layers with efficacy rivaling Yamanaka factors opens new engineering possibilities where the cusp geometry may be shallower and more navigable [364]. Epigenome editing based on programmable CRISPR-dCas9 tools has matured to the point where transient delivery of epigenome editor ribonucleoproteins via the RENDER platform can achieve durable silencing across cell types, providing a non-genetic alternative to transcription factor-based reprogramming [365]. The CRISPR-dCas9-DNMT3A system has been applied to silence tau expression in iPSC-derived neurons with sustained effects beyond 14 days, establishing proof of concept for epigenome editing in post-mitotic cells [366]. A 2025 comprehensive review of epigenome editing-based treatments catalogued clinical candidates across oncology, neurodegeneration, and metabolic disease, establishing the therapeutic viability of this approach [367]. Conserved master regulators orchestrating reprogramming-induced rejuvenation have been identified through cross-species analysis, revealing that the transcription factor networks controlling the cusp transition are deeply conserved and predictable from network topology [368]. Single-cell analyses of Schwann cell plasticity have shown that partial OSKM induction resets stress granule homeostasis and corrects dysfunctional transitional states, enabling axon regeneration in aged nerves—demonstrating that even post-mitotic support cells can be navigated through the cusp [369]. New spatial transcriptomic approaches including Visium HD and MERFISH have been applied to study tissue-level heterogeneity during aging, providing the spatial resolution needed to map cusp parameters across tissue microenvironments [370]. Such an atlas could be constructed computationally from existing single-cell epigenomic datasets (the Human Cell Atlas [89], Tabula Sapiens [90]) combined with tissue-specific reprogramming kinetics data.

### 8.3 Connection to Epithelial-Mesenchymal Transition

The cusp catastrophe is not unique to partial reprogramming. The epithelial-mesenchymal transition (EMT)—a fundamental process in development, wound healing, and cancer metastasis—has been modeled as a cusp catastrophe in gene regulatory space [91]. The ZEB1/miR-200 and SNAI1/miR-34 double-negative feedback loops create a bistable switch between epithelial and mesenchymal states, with TGF-β concentration and exposure duration as the two control parameters [92]. Recent single-cell studies have identified intermediate "hybrid E/M" states that are metastable—analogous to the rejuvenated state in our framework [93].

This parallel is not coincidental. The mesenchymal-to-epithelial transition (MET) is an obligate early step in reprogramming to pluripotency [94], and the cusp geometry of EMT likely intersects with the cusp geometry of the age-identity transition we describe. Understanding the interaction between these two cusp catastrophes—whether they are independent or coupled—is an important open question.

### 8.4 Limitations

Several limitations of the cusp catastrophe framework should be acknowledged:

**Local approximation.** Catastrophe theory classifies the local behavior of potential functions near degenerate critical points. The cusp normal form is valid only in a neighborhood of the bifurcation point; far from the fold, the true epigenetic landscape may have features not captured by the quartic polynomial. Higher-order catastrophes (swallowtail, butterfly) may be relevant if additional control parameters are important [13].

**Gradient dynamics assumption.** The cusp catastrophe applies strictly to gradient systems (systems that descend a potential landscape). Gene regulatory networks are generally non-gradient—they contain curl (rotational) components that cannot be derived from any potential function [95]. The cusp model is therefore an approximation that captures the essential features of bistability and hysteresis but may miss non-equilibrium phenomena such as oscillatory transients.

**Scalar state variable.** We have reduced the high-dimensional epigenetic state to a single scalar *x*. In reality, the age and identity axes may not be perfectly orthogonal, and the state may evolve differently in different epigenomic dimensions simultaneously. The TDA approach (Section 3) partially addresses this limitation by operating directly in the high-dimensional data space without dimensional reduction.

**HMM independence assumption.** The HMM assumes that observations at different time points are conditionally independent given the hidden state. In reality, methylation states at adjacent CpGs are correlated, and temporal autocorrelation in factor expression introduces dependencies not captured by the first-order Markov property. Extensions to hidden semi-Markov models or recurrent neural network-based state space models could address this limitation [96].

### 8.5 Open Questions

1. **What is the molecular identity of the fold line?** The cusp model predicts a sharply defined boundary in parameter space. Can this boundary be mapped to specific chromatin modifications, transcription factor binding events, or gene expression thresholds? Single-cell multi-omic profiling of cells precisely at the fold (identified by the HMM as S₃) could reveal the molecular markers of this transitional state.

2. **Is the catastrophe reversible with epigenome editing?** If cells have crossed the fold but not yet reached full pluripotency (state S₄), could targeted epigenome editing—e.g., dCas9-KRAB directed to pluripotency loci—push them back across the fold? The hysteresis prediction (Section 2.4) suggests this would require stronger intervention than simply withdrawing factors.

3. **Does the cusp geometry change with age?** If aged cells have different coupling constants *J* (weaker reader-writer maintenance) and different noise intensities *D* (higher stochastic fluctuations), the cusp surface may be "softer" in aged cells—paradoxically making them both easier to rejuvenate and more vulnerable to dedifferentiation.

4. **Can machine learning surpass the HMM?** Deep learning models (variational autoencoders, normalizing flows) can learn complex latent state representations from single-cell data [97]. Foundation models for single-cell genomics (scGPT, Geneformer, scFoundation) trained on tens of millions of cells can predict perturbation responses and cell state transitions with remarkable accuracy [355, 356, 357]. Whether these provide better state estimation than the interpretable HMM framework developed here is an empirical question that can be addressed with the validation experiments of Section 7.

5. **What role does metabolic rewiring play in the catastrophe?** Single-cell multi-omics studies in 2025 have linked epigenetic reprogramming to metabolic state changes, with a shift from oxidative phosphorylation to glycolysis occurring precisely at the transition point [358]. The metabolic switch may serve as both a biomarker for the fold state (S₃) and a mechanistic driver of the catastrophic transition. Incorporating metabolic state as an additional observable in the HMM could improve fold-detection sensitivity.

6. **How does the immune system interact with the cusp?** Partially reprogrammed cells transiently express neoantigens and altered surface markers that may trigger immune surveillance [359]. The interplay between reprogramming kinetics and immune clearance creates an additional control parameter not captured by our two-parameter cusp model. A swallowtail catastrophe (three control parameters) may be required to fully describe systems where immune pressure modulates the landscape [360].

7. **Can spatial transcriptomics resolve the cusp in tissue context?** The emergence of spatial multi-omics technologies—Visium HD, MERFISH, Slide-seq V2—enables measurement of gene expression and chromatin state with subcellular spatial resolution [361, 362]. Applying persistent homology to spatially resolved reprogramming data could reveal whether the cusp catastrophe manifests as spatial domains (patches of rejuvenated vs. dedifferentiated cells) or is cell-autonomous.

### 8.6 Long-Term Vision: Autonomous Closed-Loop Rejuvenation

The ultimate vision of this work is a therapeutic system that autonomously maintains cellular youth through periodic, closed-loop partial reprogramming. In this vision:

1. A patient receives a one-time genetic installation of: (a) inducible OSK under optogenetic or small-molecule control, (b) miR-302-responsive 3′-UTR safety elements, (c) synNotch-based kill switches, and (d) molecular reporter constructs.

2. A wearable or implantable device periodically activates factor expression (via light or chemical inducer), monitors reporter outputs, and adjusts dosing in real time based on HMM state estimates.

3. Over a lifetime, this system performs periodic "maintenance cycles" that reverse age-accumulated epigenetic drift while never approaching the fold line—a kind of epigenetic thermostat that maintains cellular function within the rejuvenated basin of the cusp landscape.

While this vision is distant from current clinical reality, each component is grounded in existing technology: AAV delivery is FDA-approved for multiple indications [98], optogenetic systems have been tested in human retinal cells [99], synNotch receptors are in preclinical development [100], and methylation-based age measurement is commercially available [101]. The mathematical framework developed here provides the theoretical foundation for their integration.

---

## 9. Conclusion

The boundary between rejuvenation and dedifferentiation in partial epigenetic reprogramming is not a smooth gradient amenable to open-loop optimization, but a cusp catastrophe: a fold singularity in the epigenetic landscape where infinitesimal changes in dosing or duration can produce qualitatively different cellular fates. This discontinuity explains the tissue-dependent critical durations observed empirically, the hysteresis that renders dedifferentiation irreversible, the superlinear sensitivity to factor expression level, and the inherent fragility of the partially reprogrammed state.

We have developed four complementary mathematical frameworks to characterize and navigate this discontinuity: (1) cusp catastrophe theory provides the geometric and analytical description of the landscape; (2) persistent homology provides model-free detection of catastrophe signatures in single-cell data; (3) Hidden Markov Models provide real-time inference of latent cellular state; and (4) Ising/Potts models provide the microscopic mechanism of cooperative chromatin transitions underlying the macroscopic catastrophe. These converge on a closed-loop feedback control architecture that integrates molecular sensors, probabilistic state estimation, and engineered biological actuators to maintain reprogramming trajectories within the safe region of the cusp surface.

The central message is a shift in paradigm: from open-loop protocols (precomputed dosing schedules applied uniformly) to closed-loop feedback control (real-time state estimation driving adaptive dosing). This shift is not merely a refinement of existing approaches but a qualitative change in how we think about therapeutic reprogramming—recognizing that the epigenetic landscape has singularities that demand navigational intelligence, not just optimized routes.

As the first partial reprogramming therapies enter human trials, the cusp catastrophe framework provides both a warning and a guide: the landscape is more treacherous than smooth models suggest, but with the right mathematical tools and biological engineering, precision navigation is achievable.

---

## References

[1] Della Valle F, Bhatt AB, et al. "Epigenetic rejuvenation by partial reprogramming." *Bioessays* 2024; 46(4):e2300230. PMID: 38421079.

[2] Life Biosciences Inc. "FDA Clearance of IND Application for ER-100 in Optic Neuropathies." Press release, January 28, 2026. NCT07290244.

[3] Ksander BR, Kocsis JD, et al. "Vision restoration by AAV-mediated OSK expression in aged retinal ganglion cells." *Molecular Therapy* 2024; 32(7):2082-2095. PMID: 38734896.

[4] Roux AE, Zhang C, et al. "Diverse partial reprogramming strategies restore youthful gene expression and transiently suppress cell identity." *Cell Systems* 2022; 13(7):574-587. PMID: 35690067.

[5] Cipriano A, Moqri M, Maybury-Lewis SY, et al. "Mechanisms, pathways and strategies for rejuvenation through epigenetic reprogramming." *Nature Aging* 2024; 4(1):14-26. PMID: 38102454.

[6] Horvath S, Lacunza E, Mallat MC, et al. "Cognitive rejuvenation in old rats by hippocampal OSKM gene therapy." *GeroScience* 2025; 47:809-823. PMID: 39037528.

[7] Huyghe A, Trajkova A, Lavial F. "Cellular plasticity in reprogramming, rejuvenation and tumorigenesis: a pioneer TF perspective." *Trends in Cell Biology* 2024; 34(3):255-267. PMID: 37648593.

[8] Hishida T, Yamamoto M, et al. "In vivo partial cellular reprogramming enhances liver plasticity and regeneration." *Cell Reports* 2022; 39(4):110730. PMID: 35476977.

[9] Paine PT, Nguyen A, Ocampo A. "Partial cellular reprogramming: a deep dive into an emerging rejuvenation technology." *Aging Cell* 2024; 23(2):e14039. PMID: 38040663.

[10] Parras A, Vílchez-Acosta A, et al. "In vivo reprogramming leads to premature death linked to hepatic and intestinal failure." *Nature Aging* 2023; 3(12):1525-1536. PMID: 38012287.

[11] Mendelsohn AR, Larrick JW. "Epigenetic age reversal by cell-extrinsic and cell-intrinsic means." *Rejuvenation Research* 2024; 27(1):22-28. PMID: 38345009.

[12] Thom R. *Stabilité structurelle et morphogenèse.* W.A. Benjamin, Reading, MA, 1972. ISBN: 0805392769.

[13] Poston T, Stewart I. *Catastrophe Theory and Its Applications.* Dover, New York, 2012 (reprint of 1978 edition). ISBN: 0486692710.

[14] Zeeman EC. "Catastrophe theory." *Scientific American* 1976; 234(4):65-83. PMID: 1257728.

[15] Huang S, Eichler G, Bar-Yam Y, Ingber DE. "Cell fates as high-dimensional attractor states of a complex gene regulatory network." *Physical Review Letters* 2005; 94(12):128701. PMID: 15903968.

[16] Mojtahedi M, Skupin A, et al. "Cell fate decision as high-dimensional critical state transition." *PLoS Biology* 2016; 14(12):e2000640. PMID: 28027308.

[17] Rand DA, Raju A, Saez M, Siggia ED. "Dynamical landscapes of cell fate decisions." *Interface Focus* 2022; 12(4):20220002. PMID: 35673853.

[18] Jia D, Jolly MK, et al. "Distinguishing mechanisms underlying EMT tristability." *Cancer Convergence* 2017; 1:2. PMID: 30202129.

[19] Olova N, Simpson DJ, Marber RE, Chandra T. "Partial reprogramming induces a steady decline in epigenetic age before loss of somatic identity." *Aging Cell* 2019; 18(1):e12877. PMID: 30450724.

[20] Gilmore R. *Catastrophe Theory for Scientists and Engineers.* Dover, New York, 1993 (reprint). ISBN: 0486675394.

[21] McInnes L, Healy J, Melville J. "UMAP: Uniform Manifold Approximation and Projection for dimension reduction." *Journal of Open Source Software* 2018; 3(29):861.

[22] Kobak D, Berens P. "The art of using t-SNE for single-cell transcriptomics." *Nature Communications* 2019; 10(1):5416. PMID: 31780648.

[23] Haghverdi L, Buettner F, Theis FJ. "Diffusion maps for high-dimensional single-cell analysis of differentiation data." *Bioinformatics* 2015; 31(18):2989-2998. PMID: 26002886.

[24] Carlsson G. "Topology and data." *Bulletin of the American Mathematical Society* 2009; 46(2):255-308.

[25] Edelsbrunner H, Harer J. *Computational Topology: An Introduction.* American Mathematical Society, 2010. ISBN: 0821849255.

[26] Chazal F, Michel B. "An introduction to topological data analysis: fundamental and practical aspects for data scientists." *Frontiers in Artificial Intelligence* 2021; 4:667963. PMID: 34661095.

[27] Cohen-Steiner D, Edelsbrunner H, Harer J. "Stability of persistence diagrams." *Discrete & Computational Geometry* 2007; 37(1):103-120.

[28] Kapourani CA, Sanguinetti G. "Melissa: Bayesian clustering and imputation of single-cell methylomes." *Genome Biology* 2019; 20(1):61. PMID: 30885233.

[29] Lin J. "Divergence measures based on the Shannon entropy." *IEEE Transactions on Information Theory* 1991; 37(1):145-151.

[30] Bauer U. "Ripser: efficient computation of Vietoris-Rips persistence barcodes." *Journal of Applied and Computational Topology* 2021; 5:391-423.

[31] Maria C, Boissonnat JD, Glisse M, Yvinec M. "The GUDHI library: simplicial complexes and persistent homology." In: *ICMS 2014*, Lecture Notes in Computer Science, vol. 8592. Springer, 2014.

[32] Cavanna NJ, Jahanseir M, Sheehy DR. "A geometric perspective on sparse filtrations." In: *Proceedings of the 27th Canadian Conference on Computational Geometry*, 2015.

[33] De Silva V, Carlsson G. "Topological estimation using witness complexes." In: *Symposium on Point-Based Graphics*, 2004.

[34] Chari T, Pachter L. "The specious art of single-cell genomics." *PLoS Computational Biology* 2023; 19(8):e1011288. PMID: 37556451.

[35] Skraba P, Turner K. "Wasserstein stability for persistence diagrams." *arXiv* preprint, 2023; arXiv:2006.16824.

[36] Traag VA, Waltman L, van Eck NJ. "From Louvain to Leiden: guaranteeing well-connected communities." *Scientific Reports* 2019; 9(1):5233. PMID: 30914743.

[37] Emmett KJ, Rabadan R. "Characterizing scales of genetic recombination and antibiotic resistance in pathogenic bacteria using topological data analysis." In: *Research in Computational Molecular Biology*, Springer, 2014.

[38] Bubenik P. "Statistical topological data analysis using persistence landscapes." *Journal of Machine Learning Research* 2015; 16(1):77-102.

[39] Fasy BT, Lecci F, Rinaldo A, Wasserman L, Balakrishnan S, Singh A. "Confidence sets for persistence diagrams." *The Annals of Statistics* 2014; 42(6):2301-2339.

[40] Rizvi AH, Camara PG, Kandror EK, et al. "Single-cell topological RNA-seq analysis reveals insights into cellular differentiation and development." *Nature Biotechnology* 2017; 35(6):551-560. PMID: 28459449.

[41] Nicolau M, Levine AJ, Carlsson G. "Topology based data analysis identifies a subgroup of breast cancers with a unique mutational profile and excellent survival." *Proceedings of the National Academy of Sciences* 2011; 108(17):7265-7270. PMID: 21482760.

[42] Rabiner LR. "A tutorial on hidden Markov models and selected applications in speech recognition." *Proceedings of the IEEE* 1989; 77(2):257-286.

[43] Burge C, Karlin S. "Prediction of complete gene structures in human genomic DNA." *Journal of Molecular Biology* 1997; 268(1):78-94. PMID: 9149143.

[44] Krogh A, Brown M, Mian IS, Sjölander K, Haussler D. "Hidden Markov models in computational biology: applications to protein modeling." *Journal of Molecular Biology* 1994; 235(5):1501-1531. PMID: 8107089.

[45] Ernst J, Kellis M. "ChromHMM: automating chromatin-state discovery and characterization." *Nature Methods* 2012; 9(3):215-216. PMID: 22373907.

[46] Horvath S, Raj K. "DNA methylation-based biomarkers and the epigenetic clock theory of ageing." *Nature Reviews Genetics* 2018; 19(6):371-384. PMID: 29643443.

[47] McCrory C, Fiorito G, et al. "GrimAge outperforms other epigenetic clocks in the prediction of age-related clinical phenotypes and all-cause mortality." *Journals of Gerontology Series A* 2021; 76(5):741-749. PMID: 33211845.

[48] Belsky DW, Caspi A, et al. "Quantification of the pace of biological aging in humans through a blood test: the DunedinPoAm DNA methylation algorithm." *eLife* 2020; 9:e54870. PMID: 32367804.

[49] Yu J, Vodyanik MA, Smuga-Otto K, et al. "Induced pluripotent stem cell lines derived from human somatic cells." *Science* 2007; 318(5858):1917-1920. PMID: 18029452.

[50] Conte M, Martucci M, et al. "GDF15, an emerging key player in human aging." *Ageing Research Reviews* 2022; 75:101569. PMID: 35051643.

[51] Mosteiro L, Pantoja C, Alcazar N, et al. "Tissue damage and senescence provide critical signals for cellular reprogramming in vivo." *Science* 2016; 354(6315):aaf4445. PMID: 27884981.

[52] Buenrostro JD, Wu B, Litzenburger UM, et al. "Single-cell chromatin accessibility reveals principles of regulatory variation." *Nature* 2015; 523(7561):486-490. PMID: 26083756.

[53] Forney GD. "The Viterbi algorithm." *Proceedings of the IEEE* 1973; 61(3):268-278.

[54] Baum LE, Petrie T, Soules G, Weiss N. "A maximization technique occurring in the statistical analysis of probabilistic functions of Markov chains." *The Annals of Mathematical Statistics* 1970; 41(1):164-171.

[55] Stuart T, Butler A, Hoffman P, et al. "Comprehensive integration of single-cell data." *Cell* 2019; 177(7):1888-1902. PMID: 31178118.

[56] Ma S, Zhang B, LaFave LM, et al. "Chromatin potential identified by shared single-cell profiling of RNA and chromatin." *Cell* 2020; 183(4):1103-1116. PMID: 33098772.

[57] Biddy BA, Kong W, et al. "Single-cell mapping of lineage and identity in direct reprogramming." *Nature* 2018; 564(7735):219-224. PMID: 30518857.

[58] Sneppen K, Mitarai N. "Multistability with a metastable mixed state." *Physical Review Letters* 2012; 109(10):100602. PMID: 23005273.

[59] Strahl BD, Allis CD. "The language of covalent histone modifications." *Nature* 2000; 403(6765):41-45. PMID: 10638745.

[60] Zhang T, Cooper S, Brockdorff N. "The interplay of histone modifications—writers that read." *EMBO Reports* 2015; 16(11):1467-1481. PMID: 26474904.

[61] Dodd IB, Micheelsen MA, Sneppen K, Thon G. "Theoretical analysis of epigenetic cell memory by nucleosome modification." *Cell* 2007; 129(4):813-822. PMID: 17512413.

[62] Sneppen K, Ringrose L. "Theoretical analysis of Polycomb-Trithorax systems predicts that poised chromatin is bistable and not bivalent." *Nature Communications* 2019; 10(1):2133. PMID: 31086182.

[63] Lachner M, O'Carroll D, Rea S, Mechtler K, Jenuwein T. "Methylation of histone H3 lysine 9 creates a binding site for HP1 proteins." *Nature* 2001; 410(6824):116-120. PMID: 11242053.

[64] Lee CH, Wu J, Li B. "Allosteric activation dictates PRC2 activity independent of its recruitment to chromatin." *Molecular Cell* 2020; 70(3):422-434.e6. PMID: 29681498.

[65] Bintu L, Yong J, Antebi YE, et al. "Dynamics of epigenetic regulation at the single-cell level." *Science* 2016; 351(6274):720-724. PMID: 26912859.

[66] Berry J, Weber SC, Vaidya N, et al. "RNA transcription modulates phase transition-driven nuclear body assembly." *Proceedings of the National Academy of Sciences* 2015; 112(38):E5237-E5245. PMID: 26351690.

[67] Wu FY. "The Potts model." *Reviews of Modern Physics* 1982; 54(1):235-268.

[68] Dixon JR, Selvaraj S, Yue F, et al. "Topological domains in mammalian genomes identified by analysis of chromatin interactions." *Nature* 2012; 485(7398):376-380. PMID: 22495300.

[69] Bell CG, Lowe R, Adams PD, et al. "DNA methylation aging clocks: challenges and recommendations." *Genome Biology* 2019; 20(1):249. PMID: 31767039.

[70] Hotta A, Cheung AYL, Falk A, et al. "Isolation of human iPS cells using EOS lentiviral vectors to select for pluripotency." *Nature Methods* 2009; 6(5):370-376. PMID: 19404254.

[71] Chatterton Z, Mendelev N, et al. "Bisulfite amplicon sequencing can detect DNA methylation changes at single CpG resolution in cellular reprogramming." *Epigenetics* 2024; 19(1):2335024. PMID: 38563618.

[72] Simpson JT, Workman RE, et al. "Detecting DNA cytosine methylation using nanopore sequencing." *Nature Methods* 2017; 14(4):407-410. PMID: 28218898.

[73] Mintun MA, Lo P, Duggan Evans C, et al. "Donanemab in early Alzheimer's disease." *New England Journal of Medicine* 2021; 384(18):1691-1704. PMID: 33720637.

[74] Morsut L, Roybal KT, Xiong X, et al. "Engineering customized cell sensing and response behaviors using synthetic Notch receptors." *Cell* 2016; 164(4):780-791. PMID: 26830878.

[75] Tang C, Lee AS, Volkmer JP, et al. "An antibody against SSEA-5 glycan on human pluripotent stem cells enables removal of teratoma-forming cells." *Nature Biotechnology* 2011; 29(9):829-834. PMID: 21841799.

[76] Gargett T, Brown MP. "The inducible caspase-9 suicide gene system as a 'safety switch' to limit on-target, off-tumor toxicities of chimeric antigen receptor T cells." *Frontiers in Pharmacology* 2014; 5:235. PMID: 25389405.

[77] Suh MR, Lee Y, Kim JY, et al. "Human embryonic stem cells express a unique set of microRNAs." *Developmental Biology* 2004; 270(2):488-498. PMID: 15183728.

[78] Samavarchi-Tehrani P, Golipour A, David L, et al. "Functional genomics reveals a BMP-driven mesenchymal-to-epithelial transition in the initiation of somatic cell reprogramming." *Cell Stem Cell* 2010; 7(1):64-77. PMID: 20621051.

[79] Miki K, Endo K, Takahashi S, et al. "Efficient detection and purification of cell populations using synthetic microRNA switches." *Cell Stem Cell* 2015; 16(6):699-711. PMID: 26004781.

[80] Konermann S, Brigham MD, et al. "Optical control of mammalian endogenous transcription and epigenetic states." *Nature* 2013; 500(7463):472-476. PMID: 23877069.

[81] Kennedy MJ, Hughes RM, Peteya LA, et al. "Rapid blue-light-mediated induction of protein interactions in living cells." *Nature Methods* 2010; 7(12):973-975. PMID: 21037590.

[82] Yamada M, Nagasaki SC, Suzuki Y, Hirano Y, Imayoshi I. "Optimization of light-inducible Gal4/UAS gene expression system in mammalian cells." *iScience* 2020; 23(9):101506. PMID: 32927262.

[83] Levskaya A, Weiner OD, Lim WA, Voigt CA. "Spatiotemporal control of cell signalling using a light-switchable protein interaction." *Nature* 2009; 461(7266):997-1001. PMID: 19749742.

[84] Canales A, Jia X, Froriep UP, et al. "Multifunctional fibers for simultaneous optical, electrical and chemical interrogation of neural circuits in vivo." *Nature Biotechnology* 2015; 33(3):277-284. PMID: 25599177.

[85] Chen S, Weitemier AZ, Zeng X, et al. "Near-infrared deep brain stimulation via upconversion nanoparticle-mediated optogenetics." *Science* 2018; 359(6376):679-684. PMID: 29439241.

[86] Hartigan JA, Hartigan PM. "The dip test of unimodality." *The Annals of Statistics* 1985; 13(1):70-84.

[87] Cacchiarelli D, Trapnell C, Ziller MJ, et al. "Integrative analyses of human reprogramming reveal dynamic nature of induced pluripotency." *Cell* 2015; 162(2):412-424. PMID: 26186193.

[88] Yan F, Mandrekar SJ, Yuan Y. "Keyboard: a novel Bayesian toxicity probability interval design for phase I clinical trials." *Clinical Cancer Research* 2017; 23(15):3994-4003. PMID: 28473534.

[89] Regev A, Teichmann SA, Lander ES, et al. "The Human Cell Atlas." *eLife* 2017; 6:e27041. PMID: 29206104.

[90] The Tabula Sapiens Consortium. "The Tabula Sapiens: a multiple-organ, single-cell transcriptomic atlas of humans." *Science* 2022; 376(6594):eabl4896. PMID: 35549404.

[91] Lu M, Jolly MK, Levine H, Onuchic JN, Ben-Jacob E. "MicroRNA-based regulation of epithelial-hybrid-mesenchymal fate determination." *Proceedings of the National Academy of Sciences* 2013; 110(45):18144-18149. PMID: 24154725.

[92] Zhang J, Tian XJ, Zhang H, et al. "TGF-β-induced epithelial-to-mesenchymal transition proceeds through stepwise activation of multiple feedback loops." *Science Signaling* 2014; 7(345):ra91. PMID: 25270257.

[93] Pastushenko I, Brisebarre A, Sifrim A, et al. "Identification of the tumour transition states occurring during EMT." *Nature* 2018; 556(7702):463-468. PMID: 29670281.

[94] Li R, Liang J, Ni S, et al. "A mesenchymal-to-epithelial transition initiates and is required for the nuclear reprogramming of mouse fibroblasts." *Cell Stem Cell* 2010; 7(1):51-63. PMID: 20621050.

[95] Wang J, Zhang K, Xu L, Wang E. "Quantifying the Waddington landscape and biological paths for development and differentiation." *Proceedings of the National Academy of Sciences* 2011; 108(20):8257-8262. PMID: 21536909.

[96] Lopez R, Regier J, Cole MB, Jordan MI, Yosef N. "Deep generative modeling for single-cell transcriptomics." *Nature Methods* 2018; 15(12):1053-1058. PMID: 30504886.

[97] Lotfollahi M, Wolf FA, Theis FJ. "scGen predicts single-cell perturbation responses." *Nature Methods* 2019; 16(8):715-721. PMID: 31363220.

[98] Naso MF, Tomkowicz B, Perry WL, Strohl WR. "Adeno-associated virus (AAV) as a vector for gene therapy." *BioDrugs* 2017; 31(4):317-334. PMID: 28669112.

[99] Sahel JA, Boulanger-Scemama E, Pagot C, et al. "Partial recovery of visual function in a blind patient after optogenetic therapy." *Nature Medicine* 2021; 27(7):1223-1229. PMID: 34031601.

[100] Toda S, Blauch LR, Tang SKY, Morsut L, Lim WA. "Programming self-organizing multicellular structures with synthetic cell-cell signaling." *Science* 2018; 361(6398):156-162. PMID: 29853553.

[101] Kusters CDJ, Bischoff-Ferrari HA, et al. "Quantification of epigenetic aging in public health." *Annual Review of Public Health* 2025; 46(1):91-110. PMID: 39681336.

[102] Takahashi Y, et al. "Research of in vivo reprogramming toward clinical applications in regenerative medicine: a concise review." *Regenerative Therapy* 2024; 27:740-751. PMID: 39678397.

[103] Yucel AD, Gladyshev VN. "The long and winding road of reprogramming-induced rejuvenation." *Nature Communications* 2024; 15:1941. PMID: 38431638.

[104] Pico S, et al. "Comparative analysis of mouse strains for in vivo induction of reprogramming factors." *Cell Reports* 2025; 44(7):115879. PMID: 40560729.

[105] Yang JH, Hayano M, et al. "Loss of epigenetic information as a cause of mammalian aging." *Cell* 2023; 186(2):305-326.e27. PMID: 36638792.

[106] Alle Q, Le Borgne E, et al. "A single short reprogramming early in life initiates and propagates an epigenetically related mechanism improving fitness and promoting an increased healthy lifespan." *Aging Cell* 2022; 21(10):e13714. PMID: 36207783.

[107] Liuyang S, Wang G, et al. "Highly efficient and rapid generation of human pluripotent stem cells by chemical reprogramming." *Cell Stem Cell* 2023; 30(4):450-459.e9. PMID: 37023747.

[108] Pereira F, et al. "Epigenetic reprogramming as a key to reverse ageing and increase longevity." *Ageing Research Reviews* 2024; 95:102204. PMID: 38272265.

[109] Jain A, Hosokawa Y, Joseph K. "Precision reprogramming—restoring function to aged cells." *Cellular Reprogramming* 2025; 27(1):1-12. PMID: 40489332.

[110] Simpson DJ, Olova NN, Chandra T. "Cellular reprogramming and epigenetic rejuvenation." *Clinical Epigenetics* 2021; 13(1):170. PMID: 34479610.

[111] Hernando-Herraez I, Evano B, et al. "Ageing affects DNA methylation drift and transcriptional cell-to-cell variability in mouse muscle stem cells." *Nature Communications* 2019; 10(1):4361. PMID: 31554795.

[112] Arnould C, Rocher V, et al. "Loop extrusion as a mechanism for formation of DNA damage repair foci." *Nature* 2021; 590(7847):660-665. PMID: 33597753.

[113] Wang J, Xu L, Wang E, Huang S. "The potential landscape of genetic circuits imposes the arrow of time in stem cell differentiation." *Biophysical Journal* 2010; 99(1):29-39. PMID: 20655830.

[114] Li C, Wang J. "Quantifying cell fate decisions for differentiation and reprogramming of a human stem cell network." *PLoS Computational Biology* 2013; 9(8):e1003165. PMID: 23935478.

[115] Brackston RD, Lakatos E, Stumpf MPH. "Transition state characteristics during cell differentiation." *PLoS Computational Biology* 2018; 14(9):e1006405. PMID: 30265674.

[116] Schiebinger G, Shu J, Tabaka M, et al. "Optimal-transport analysis of single-cell gene expression identifies developmental trajectories in reprogramming." *Cell* 2019; 176(4):928-943.e22. PMID: 30712867.

[117] Trapnell C, Cacchiarelli D, et al. "The dynamics and regulators of cell fate decisions are revealed by pseudotemporal ordering of single cells." *Nature Biotechnology* 2014; 32(4):381-386. PMID: 24658644.

[118] Pennarossa G, Buzzi J, et al. "Brief epigenetic remodeling events in somatic cells: the route to totipotency." *BioEssays* 2024; 46(7):e2400067. PMID: 38874237.

[119] Stadtfeld M, Maherali N, Breault DT, Hochedlinger K. "Defining molecular cornerstones during fibroblast to iPS cell reprogramming in mouse." *Cell Stem Cell* 2008; 2(3):230-240. PMID: 18371448.

[120] Nishimura K, Kato T, et al. "Manipulation of KLF4 expression generates iPSCs paused at successive stages of reprogramming." *Stem Cell Reports* 2014; 3(5):915-929. PMID: 25418732.

[121] Sarkar TJ, Quarta M, et al. "Transient non-integrative expression of nuclear reprogramming factors promotes multifaceted amelioration of aging in human cells." *Nature Communications* 2020; 11(1):1545. PMID: 32210226.

[122] Xu Y, Zhu X, et al. "Single-cell lineage tracing by endogenous mutations enriched in transposase accessible mitochondrial DNA." *eLife* 2019; 8:e45105. PMID: 31686645.

[123] Ernst J, Kheradpour P, et al. "Mapping and analysis of chromatin state dynamics in nine human cell types." *Nature* 2011; 473(7345):43-49. PMID: 21441907.

[124] Filbin MG, Tirosh I, et al. "Developmental and oncogenic programs in H3K27M gliomas dissected by single-cell RNA-seq." *Science* 2018; 360(6386):331-335. PMID: 29674595.

[125] Teschendorff AE, Enver T. "Single-cell entropy for accurate estimation of differentiation potency from a cell's transcriptome." *Nature Communications* 2017; 8:15599. PMID: 28569836.

[126] Moon KR, van Dijk D, et al. "Visualizing structure and transitions in high-dimensional biological data." *Nature Biotechnology* 2019; 37(12):1482-1492. PMID: 31796933.

[127] Tusi BK, Wolock SL, et al. "Population snapshots predict early haematopoietic and erythroid hierarchies." *Nature* 2018; 555(7694):54-60. PMID: 29466336.

[128] Wagner DE, Klein AM. "Lineage tracing meets single-cell omics: opportunities and challenges." *Nature Reviews Genetics* 2020; 21(7):410-427. PMID: 32235876.

[129] Qiu X, Zhang Y, et al. "Mapping transcriptomic vector fields of single cells." *Cell* 2022; 185(4):690-711.e45. PMID: 35108499.

[130] Bergen V, Lange M, et al. "Generalizing RNA velocity to transient cell states through dynamical modeling." *Nature Biotechnology* 2020; 38(12):1408-1414. PMID: 32747759.

[131] Setty M, Kiseliovas V, et al. "Characterization of cell fate probabilities in single-cell data with Palantir." *Nature Biotechnology* 2019; 37(4):451-460. PMID: 30899105.

[132] Gulati GS, Sikandar SS, et al. "Single-cell transcriptional diversity is a hallmark of developmental potential." *Science* 2020; 367(6476):405-411. PMID: 31974247.

[133] Lange M, Bergen V, et al. "CellRank for directed single-cell fate mapping." *Nature Methods* 2022; 19(2):159-170. PMID: 35027767.

[134] Weinreb C, Wolock S, Tusi BK, et al. "Fundamental limits on dynamic inference from single-cell snapshots." *Proceedings of the National Academy of Sciences* 2018; 115(10):E2467-E2476. PMID: 29463727.

[135] Ghazanfar S, Lin Y, Su X, et al. "Investigating higher-order interactions in single-cell data with scHOT." *Nature Methods* 2020; 17(8):799-806. PMID: 32661425.

[136] Ye J, Ge J, Zhang X, et al. "Pluripotent stem cells induced from mouse neural stem cells and small intestinal epithelial cells by small molecule compounds." *Cell Research* 2016; 26(1):34-45. PMID: 26704449.

[137] Zhao Y, Zhao T, et al. "A XEN-like state bridges somatic cells to pluripotency during chemical reprogramming." *Cell* 2015; 163(7):1678-1691. PMID: 26686652.

[138] Alle Q, Le Borgne E, et al. "Progeroid syndromes: aging and the nuclear lamina." *Seminars in Cell & Developmental Biology* 2024; 154(Pt A):58-67. PMID: 36307195.

[139] Lidzborski M, Boulier A, Picart-Armada S. "Computational methods for topological data analysis in biology." *Briefings in Bioinformatics* 2025; 26(1):bbae631. PMID: 39735331.

[140] Rabadán R, Blumberg AJ. *Topological Data Analysis for Genomics and Evolution: Topology in Biology.* Cambridge University Press, 2020. ISBN: 1107159547.

[141] Wasserman L. "Topological data analysis." *Annual Review of Statistics and Its Application* 2018; 5:501-532.

[142] Ghrist R. "Barcodes: the persistent topology of data." *Bulletin of the American Mathematical Society* 2008; 45(1):61-75.

[143] Adams H, Emerson T, et al. "Persistence images: a stable vector representation of persistent homology." *Journal of Machine Learning Research* 2017; 18(1):218-252.

[144] Reininghaus J, Huber S, et al. "A stable multi-scale kernel for topological machine learning." In: *CVPR 2015*, pages 4741-4748.

[145] Crawford L, Monod A, et al. "Predicting clinical outcomes in glioblastoma: an application of topological and functional data analysis." *Journal of the American Statistical Association* 2020; 115(531):1139-1150. PMID: 33012852.

[146] Turner K, Mileyko Y, Mukherjee S, Harer J. "Fréchet means for distributions of persistence diagrams." *Discrete & Computational Geometry* 2014; 52(1):44-70.

[147] Durbin R, Eddy SR, Krogh A, Mitchison G. *Biological Sequence Analysis: Probabilistic Models of Proteins and Nucleic Acids.* Cambridge University Press, 1998. ISBN: 0521629713.

[148] Yu SZ. "Hidden semi-Markov models." *Artificial Intelligence* 2010; 174(2):215-243.

[149] Schreiber J, Bilmes J, Noble WS. "Completing the Markov trilogy: the HMM reimplemented, with new API, tutorials, and documentation in pomegranate." *Nature Methods* 2024; 21(1):12-13. PMID: 38052948.

[150] Cappé O, Moulines E, Rydén T. *Inference in Hidden Markov Models.* Springer, 2005. ISBN: 0387402640.

[151] Beal MJ, Ghahramani Z, Rasmussen CE. "The infinite hidden Markov model." In: *Advances in Neural Information Processing Systems* 14, 2001.

[152] Fox EB, Sudderth EB, Jordan MI, Willsky AS. "An HDP-HMM for systems with state persistence." In: *ICML 2008*, pages 312-319.

[153] Jaeger H. "Observable operator models for discrete stochastic time series." *Neural Computation* 2000; 12(6):1371-1398. PMID: 10935718.

[154] Ram O, Goren A, et al. "Combinatorial patterning of chromatin regulators uncovered by genome-wide location analysis in human cells." *Cell* 2011; 147(7):1628-1639. PMID: 22196736.

[155] ENCODE Project Consortium. "Expanded encyclopaedias of DNA elements in the human and mouse genomes." *Nature* 2020; 583(7818):699-710. PMID: 32728249.

[156] Roadmap Epigenomics Consortium. "Integrative analysis of 111 reference human epigenomes." *Nature* 2015; 518(7539):317-330. PMID: 25693563.

[157] Schreiber J, Durham T, Bilmes J, Noble WS. "Avocado: a multi-scale deep tensor factorization method learns a latent representation of the human epigenome." *Genome Biology* 2020; 21(1):81. PMID: 32216823.

[158] Zhang B, Wolynes PG. "Stem cell differentiation as a many-body problem." *Proceedings of the National Academy of Sciences* 2014; 111(28):10185-10190. PMID: 24987120.

[159] Sasai M, Kawabata Y, et al. "Stochastic gene expression as a many-body problem." *Proceedings of the National Academy of Sciences* 2013; 110(37):14796-14801. PMID: 23980149.

[160] Michieletto D, Orlandini E, Marenduzzo D. "Polymer model with epigenetic recoloring reveals a pathway for the de novo establishment and 3D organization of chromatin domains." *Physical Review X* 2016; 6(4):041047.

[161] Jost D, Carrivain P, Cavalli G, Vaillant C. "Modeling epigenome folding: formation and dynamics of topologically associated chromatin domains." *Nucleic Acids Research* 2014; 42(15):9553-9561. PMID: 25092923.

[162] Cortini R, Barbi M, Caré BR, et al. "The physics of epigenetics." *Reviews of Modern Physics* 2016; 88(2):025002.

[163] Nuebler J, Fudenberg G, Imakaev M, Abdennur N, Mirny LA. "Chromatin organization by an interplay of loop extrusion and compartmental segregation." *Proceedings of the National Academy of Sciences* 2018; 115(29):E6697-E6706. PMID: 29967174.

[164] Ringrose L, Howard M. "Dissecting chromatin-mediated gene regulation and epigenetic memory through mathematical modelling." *Current Opinion in Systems Biology* 2017; 3:7-14.

[165] Angel A, Song J, Dean C, Howard M. "A Polycomb-based switch underlying quantitative epigenetic memory." *Nature* 2011; 476(7358):105-108. PMID: 21785438.

[166] Berry S, Dean C, Howard M. "Slow chromatin dynamics allow Polycomb target genes to filter fluctuations in transcription factor activity." *Cell Systems* 2017; 4(4):445-457.e8. PMID: 28342716.

[167] Obersriebnig MJ, Pallesen EMH, et al. "Nucleation and spreading of a heterochromatic domain in fission yeast." *Nature Communications* 2016; 7:11518. PMID: 27222113.

[168] Hodges C, Kirkland JG, Crabtree GR. "The many roles of BAF (mSWI/SNF) and PBAF complexes in cancer." *Cold Spring Harbor Perspectives in Medicine* 2016; 6(8):a026930. PMID: 27413115.

[169] Margueron R, Reinberg D. "The Polycomb complex PRC2 and its mark in life." *Nature* 2011; 469(7330):343-349. PMID: 21248841.

[170] Simon JA, Kingston RE. "Occupying chromatin: Polycomb mechanisms for getting to genomic targets, stopping transcriptional traffic, and staying put." *Molecular Cell* 2013; 49(5):808-824. PMID: 23473600.

[171] Becker PB, Workman JL. "Nucleosome remodeling and epigenetics." *Cold Spring Harbor Perspectives in Biology* 2013; 5(9):a017905. PMID: 24003213.

[172] Allshire RC, Madhani HD. "Ten principles of heterochromatin formation and function." *Nature Reviews Molecular Cell Biology* 2018; 19(4):229-244. PMID: 29235574.

[173] Grewal SI, Jia S. "Heterochromatin revisited." *Nature Reviews Genetics* 2007; 8(1):35-46. PMID: 17173056.

[174] O'Carroll D, Scherthan H, et al. "Isolation and characterization of Suv39h2, a second histone H3 methyltransferase gene that displays testis-specific expression." *Molecular and Cellular Biology* 2000; 20(24):9423-9433. PMID: 11094092.

[175] Greer EL, Shi Y. "Histone methylation: a dynamic mark in health, disease and inheritance." *Nature Reviews Genetics* 2012; 13(5):343-357. PMID: 22473383.

[176] Jambhekar A, Dhall A, Shi Y. "Roles and regulation of histone methylation in animal development." *Nature Reviews Molecular Cell Biology* 2019; 20(10):625-641. PMID: 31267065.

[177] Loyola A, Bonaldi T, et al. "PTMs on H3 variants before chromatin assembly potentiate their final epigenetic state." *Molecular Cell* 2006; 24(2):309-316. PMID: 17052464.

[178] Hyun K, Jeon J, Park K, Kim J. "Writing, erasing and reading histone lysine methylations." *Experimental & Molecular Medicine* 2017; 49(4):e324. PMID: 28450737.

[179] Bonev B, Mendelson Cohen N, et al. "Multiscale 3D genome rewiring during mouse neural development." *Cell* 2017; 171(3):557-572.e24. PMID: 29053968.

[180] Lieberman-Aiden E, van Berkum NL, et al. "Comprehensive mapping of long-range interactions reveals folding principles of the human genome." *Science* 2009; 326(5950):289-293. PMID: 19815776.

[181] Rao SSP, Huntley MH, et al. "A 3D map of the human genome at kilobase resolution reveals principles of chromatin looping." *Cell* 2014; 159(7):1665-1680. PMID: 25497547.

[182] Nora EP, Lajoie BR, et al. "Spatial partitioning of the regulatory landscape of the X-inactivation centre." *Nature* 2012; 485(7398):381-385. PMID: 22495304.

[183] Fussenegger M, Morris RP, et al. "Streptogramin-based gene regulation systems for mammalian cells." *Nature Biotechnology* 2000; 18(11):1203-1208. PMID: 11062442.

[184] Weber W, Fussenegger M. "Emerging biomedical applications of synthetic biology." *Nature Reviews Genetics* 2012; 13(1):21-35. PMID: 22124480.

[185] Elowitz MB, Leibler S. "A synthetic oscillatory network of transcriptional regulators." *Nature* 2000; 403(6767):335-338. PMID: 10659856.

[186] Khalil AS, Collins JJ. "Synthetic biology: applications come of age." *Nature Reviews Genetics* 2010; 11(5):367-379. PMID: 20395968.

[187] Gao XJ, Chong LS, Kim MS, Elowitz MB. "Programmable protein circuits in living cells." *Science* 2018; 361(6408):1252-1258. PMID: 30237357.

[188] Zhu R, del Rio-Salgado JM, Garcia-Ojalvo J, Elowitz MB. "Synthetic multistability in mammalian cells." *Science* 2022; 375(6578):eabg9765. PMID: 35050676.

[189] Bugaj LJ, Choksi AT, Mesuda CK, Kane RS, Bhatt DK. "Optogenetic protein clustering and signaling activation in mammalian cells." *Nature Methods* 2013; 10(3):249-252. PMID: 23377377.

[190] Repina NA, Rosenbloom A, Mukherjee A, Schaffer DV, Kane RS. "At light speed: advances in optogenetic systems for regulating cell signaling and behavior." *Annual Review of Chemical and Biomolecular Engineering* 2017; 8:13-39. PMID: 28592175.

[191] Liu X, Zhang J, et al. "Computational discovery of microRNA targets." *In Silico Biology* 2006; 6(1-2):1-4. PMID: 16789909.

[192] Hochedlinger K, Yamada Y, Beard C, Jaenisch R. "Ectopic expression of Oct-4 blocks progenitor-cell differentiation and causes dysplasia in epithelial tissues." *Cell* 2005; 121(3):465-477. PMID: 15882627.

[193] Aoi T, Yae K, et al. "Generation of pluripotent stem cells from adult mouse liver and stomach cells." *Science* 2008; 321(5889):699-702. PMID: 18276851.

[194] Kim JB, Zaehres H, Wu G, et al. "Pluripotent stem cells induced from adult neural stem cells by reprogramming with two factors." *Nature* 2008; 454(7204):646-650. PMID: 18594515.

[195] Maherali N, Sridharan R, et al. "Directly reprogrammed fibroblasts show global epigenetic remodeling and widespread tissue contribution." *Cell Stem Cell* 2007; 1(1):55-70. PMID: 18371336.

[196] Smith ZD, Sindhu C, Meissner A. "Molecular features of cellular reprogramming and development." *Nature Reviews Molecular Cell Biology* 2016; 17(3):139-154. PMID: 26883001.

[197] Jaenisch R, Young R. "Stem cells, the molecular circuitry of pluripotency and nuclear reprogramming." *Cell* 2008; 132(4):567-582. PMID: 18295576.

[198] Chen X, Xu H, et al. "Integration of external signaling pathways with the core transcriptional network in embryonic stem cells." *Cell* 2008; 133(6):1106-1117. PMID: 18555785.

[199] Boyer LA, Lee TI, et al. "Core transcriptional regulatory circuitry in human embryonic stem cells." *Cell* 2005; 122(6):947-956. PMID: 16153702.

[200] Pasque V, Tchieu J, et al. "X chromosome reactivation dynamics reveal stages of reprogramming to pluripotency." *Cell* 2014; 159(7):1681-1697. PMID: 25525883.

[201] Buganim Y, Faddah DA, et al. "Single-cell expression analyses during cellular reprogramming reveal an early stochastic and a late hierarchic phase." *Cell* 2012; 150(6):1209-1222. PMID: 22980981.

[202] Wernig M, Lengner CJ, et al. "A drug-inducible transgenic system for direct reprogramming of multiple somatic cell types." *Nature Biotechnology* 2008; 26(8):916-924. PMID: 18594521.

[203] Hussein SMI, Puri MC, et al. "Genome-wide characterization of the routes to pluripotency." *Nature* 2014; 516(7530):198-206. PMID: 25503233.

[204] Shi Y, Inoue H, Wu JC, Yamanaka S. "Induced pluripotent stem cell technology: a decade of progress." *Nature Reviews Drug Discovery* 2017; 16(2):115-130. PMID: 27188591.

[205] Lujan E, Zunder ER, Ng YH, et al. "Early reprogramming regulators identified by prospective isolation and mass cytometry." *Nature* 2015; 521(7552):352-356. PMID: 25830878.

[206] Schwarz BA, Bar-Nur O, Silva JCR, Hochedlinger K. "Nanog is dispensable for the generation of induced pluripotent stem cells." *Current Biology* 2014; 24(3):347-350. PMID: 24462004.

[207] Apostolou E, Hochedlinger K. "Chromatin dynamics during cellular reprogramming." *Nature* 2013; 502(7472):462-471. PMID: 24153299.

[208] Knaupp AS, Buckberry S, et al. "Transient and permanent reconfiguration of chromatin and transcription factor occupancy drive reprogramming." *Cell Stem Cell* 2017; 21(6):834-845.e6. PMID: 29198943.

[209] Chronis C, Fiziev P, et al. "Cooperative binding of transcription factors orchestrates reprogramming." *Cell* 2017; 168(3):442-459.e20. PMID: 28111071.

[210] Li D, Liu J, et al. "Chromatin accessibility dynamics during iPSC reprogramming." *Cell Stem Cell* 2017; 21(6):819-833.e6. PMID: 29198942.

[211] Koche RP, Smith ZD, et al. "Reprogramming factor expression initiates widespread targeted chromatin remodeling." *Cell Stem Cell* 2011; 8(1):96-105. PMID: 21211784.

[212] Onder TT, Kara N, et al. "Chromatin-modifying enzymes as modulators of reprogramming." *Nature* 2012; 483(7391):598-602. PMID: 22388813.

[213] Soufi A, Donahue G, Zaret KS. "Facilitators and impediments of the pluripotency reprogramming factors' initial engagement with the genome." *Cell* 2012; 151(5):994-1004. PMID: 23159369.

[214] Wapinski OL, Vierbuchen T, et al. "Hierarchical mechanisms for direct reprogramming of fibroblasts to neurons." *Cell* 2013; 155(3):621-635. PMID: 24243019.

[215] Zaret KS, Carroll JS. "Pioneer transcription factors: establishing competence for gene expression." *Genes & Development* 2011; 25(21):2227-2241. PMID: 22056668.

[216] Soufi A, Garcia MF, et al. "Pioneer transcription factors target partial DNA motifs on nucleosomes to initiate reprogramming." *Cell* 2015; 161(3):555-568. PMID: 25892221.

[217] Festuccia N, Gonzalez I, et al. "Transcription factor activity and nucleosome organization in mitosis." *Genome Research* 2019; 29(2):250-260. PMID: 30655359.

[218] King HW, Klose RJ. "The pioneer factor OCT4 requires the chromatin remodeller BRG1 to support gene regulatory element function in mouse embryonic stem cells." *eLife* 2017; 6:e22631. PMID: 28304275.

[219] Schwanhäusser B, Busse D, et al. "Global quantification of mammalian gene expression control." *Nature* 2011; 473(7347):337-342. PMID: 21593866.

[220] Efroni S, Duttagupta R, et al. "Global transcription in pluripotent embryonic stem cells." *Cell Stem Cell* 2008; 2(5):437-447. PMID: 18462694.

[221] Meshorer E, Yellajoshula D, et al. "Hyperdynamic plasticity of chromatin proteins in pluripotent embryonic stem cells." *Developmental Cell* 2006; 10(1):105-116. PMID: 16399082.

[222] Gaspar-Maia A, Alajem A, Meshorer E, Ramalho-Santos M. "Open chromatin in pluripotency and reprogramming." *Nature Reviews Molecular Cell Biology* 2011; 12(1):36-47. PMID: 21179060.

[223] Tsankov AM, Gu H, et al. "Transcription factor binding dynamics during human ES cell differentiation." *Nature* 2015; 518(7539):344-349. PMID: 25693565.

[224] Xie W, Schultz MD, et al. "Epigenomic analysis of multilineage differentiation of human embryonic stem cells." *Cell* 2013; 153(5):1134-1148. PMID: 23664764.

[225] Lister R, Pelizzola M, et al. "Human DNA methylomes at base resolution show widespread epigenomic differences." *Nature* 2009; 462(7271):315-322. PMID: 19829295.

[226] Hon GC, Rajagopal N, et al. "Epigenetic memory at embryonic enhancers identified in DNA methylation maps from adult mouse tissues." *Nature Genetics* 2013; 45(10):1198-1206. PMID: 23995138.

[227] Stadler MB, Murr R, et al. "DNA-binding factors shape the mouse methylome at distal regulatory regions." *Nature* 2011; 480(7378):490-495. PMID: 22170606.

[228] Schübeler D. "Function and information content of DNA methylation." *Nature* 2015; 517(7534):321-326. PMID: 25592537.

[229] Greenberg MVC, Bourc'his D. "The diverse roles of DNA methylation in mammalian development and disease." *Nature Reviews Molecular Cell Biology* 2019; 20(10):590-607. PMID: 31399642.

[230] Jones PA. "Functions of DNA methylation: islands, start sites, gene bodies and beyond." *Nature Reviews Genetics* 2012; 13(7):484-492. PMID: 22641018.

[231] Smith ZD, Meissner A. "DNA methylation: roles in mammalian development." *Nature Reviews Genetics* 2013; 14(3):204-220. PMID: 23400093.

[232] Zeng Y, Chen T. "DNA methylation reprogramming during mammalian development." *Genes* 2019; 10(4):257. PMID: 30934924.

[233] Field AE, Robertson NA, et al. "DNA methylation clocks in aging: categories, causes, and consequences." *Molecular Cell* 2018; 71(6):882-895. PMID: 30241605.

[234] Meer MV, Podolskiy DI, Tyshkovskiy A, Gladyshev VN. "A whole lifespan mouse multi-tissue DNA methylation clock." *eLife* 2018; 7:e40675. PMID: 30530465.

[235] Petkovich DA, Podolskiy DI, et al. "Using DNA methylation profiling to evaluate biological age and longevity interventions." *Cell Metabolism* 2017; 25(4):954-960.e6. PMID: 28380383.

[236] Fahy GM, Brooke RT, et al. "Reversal of epigenetic aging and immunosenescent trends in humans." *Aging Cell* 2019; 18(6):e13028. PMID: 31496122.

[237] Moqri M, Herzog C, et al. "Biomarkers of aging for the identification and evaluation of longevity interventions." *Cell* 2023; 186(18):3758-3775. PMID: 37657418.

[238] Gladyshev VN. "The ground zero of organismal life and aging." *Trends in Molecular Medicine* 2021; 27(1):11-19. PMID: 33127327.

[239] Seale K, Horvath S, Teschendorff AE, et al. "Making sense of the ageing methylome." *Nature Reviews Genetics* 2022; 23(10):585-605. PMID: 35501396.

[240] Thompson MJ, Chwiałkowska K, et al. "A multi-tissue full lifespan epigenetic clock for mice." *Aging* 2018; 10(10):2832-2854. PMID: 30348905.

[241] Stubbs TM, Bonder MJ, et al. "Multi-tissue DNA methylation age predictor in mouse." *Genome Biology* 2017; 18(1):68. PMID: 28399939.

[242] Duan R, Fu Q, Sun Y, Li Q. "Epigenetic clock: a promising biomarker and practical tool in aging." *Ageing Research Reviews* 2022; 81:101743. PMID: 36206924.

[243] Belsky DW, Moffitt TE, et al. "Eleven telomere, epigenetic clock, and biomarker-composite quantifications of biological aging: do they measure the same thing?" *American Journal of Epidemiology* 2018; 187(6):1220-1230. PMID: 29149257.

[244] Kabacik S, Lowe D, Fransen L, et al. "The relationship between epigenetic age and the hallmarks of aging in human cells." *Nature Aging* 2022; 2(6):484-493. PMID: 37118370.

[245] Moqri M, Herzog C, et al. "PRC2-AgeIndex as a universal biomarker of aging and rejuvenation." *Nature Communications* 2024; 15(1):5956. PMID: 39009581.

[246] Gill D, Parry A, et al. "Rejuvenation of the epigenome in human fibroblasts." *Nature Aging* 2024; 4(3):304-310. PMID: 38355768.

[247] Mitchell E, Spencer Chapman M, et al. "Clonal dynamics of haematopoiesis across the human lifespan." *Nature* 2022; 606(7913):343-350. PMID: 35650442.

[248] Cagan A, Baez-Ortega A, et al. "Somatic mutation rates scale with lifespan across mammals." *Nature* 2022; 604(7906):517-524. PMID: 35418684.

[249] Lawson ARJ, Abascal F, et al. "Extensive heterogeneity in somatic mutation and selection in the human bladder." *Science* 2020; 370(6512):75-82. PMID: 33004514.

[250] Martincorena I, Fowler JC, et al. "Somatic mutant clones colonize the human esophagus with age." *Science* 2018; 362(6417):911-917. PMID: 30337457.

[251] Yizhak K, Aguet F, et al. "RNA sequence analysis reveals macroscopic somatic clonal expansion across normal tissues." *Science* 2019; 364(6444):eaaw0726. PMID: 31171663.

[252] Lodato MA, Woodworth MB, et al. "Aging and neurodegeneration are associated with increased mutations in single human neurons." *Science* 2018; 359(6375):555-559. PMID: 29217584.

[253] Abascal F, Harvey LMR, et al. "Somatic mutation landscapes at single-molecule resolution." *Nature* 2021; 593(7859):405-410. PMID: 33911282.

[254] Vijg J, Dong X. "Pathogenic mechanisms of somatic mutation and genome mosaicism in aging." *Cell* 2020; 182(1):12-23. PMID: 32649876.

[255] De S. "Somatic mosaicism in healthy human tissues." *Trends in Genetics* 2011; 27(6):217-223. PMID: 21496937.

[256] Dilliard SA, Cheng Q, Siegwart DJ. "On the mechanism of tissue-specific mRNA delivery by selective organ targeting nanoparticles." *Proceedings of the National Academy of Sciences* 2021; 118(52):e2109256118. PMID: 34930824.

[257] Akinc A, Querbes W, et al. "Targeted delivery of RNAi therapeutics with endogenous and exogenous ligand-based mechanisms." *Molecular Therapy* 2010; 18(7):1357-1364. PMID: 20461061.

[258] Adams D, Gonzalez-Duarte A, et al. "Patisiran, an RNAi therapeutic, for hereditary transthyretin amyloidosis." *New England Journal of Medicine* 2018; 379(1):11-21. PMID: 29972753.

[259] Patel S, Ashwanikumar N, et al. "Naturally-occurring cholesterol analogues in lipid nanoparticles induce polymorphic shape and enhance intracellular delivery of mRNA." *Nature Communications* 2020; 11(1):983. PMID: 32080183.

[260] Miao L, Zhang Y, Bhatt DK, et al. "Synergistic lipid compositions for albumin receptor mediated delivery of mRNA to the liver." *Nature Communications* 2020; 11(1):2424. PMID: 32415109.

[261] Yin H, Song CQ, Dorkin JR, et al. "Therapeutic genome editing by combined viral and non-viral delivery of CRISPR system components in vivo." *Nature Biotechnology* 2016; 34(3):328-333. PMID: 26829318.

[262] Wittrup A, Ai A, et al. "Visualizing lipid-formulated siRNA release from endosomes and target gene knockdown." *Nature Biotechnology* 2015; 33(8):870-876. PMID: 26192320.

[263] Kulkarni JA, Witzigmann D, Thomson SB, et al. "The current landscape of nucleic acid therapeutics." *Nature Nanotechnology* 2021; 16(6):630-643. PMID: 34059811.

[264] Paunovska K, Loughrey D, Dahlman JE. "Drug delivery systems for RNA therapeutics." *Nature Reviews Genetics* 2022; 23(5):265-280. PMID: 34983972.

[265] Han X, Zhang H, Butber K, et al. "A suite of new Dre recombinase drivers for lineage tracing in single-cell chromatin accessibility studies." *Nature Methods* 2024; 21(3):412-420. PMID: 38200113.

[266] Cuomo ASE, Seber DA, et al. "Single-cell RNA-sequencing of differentiating iPS cells reveals dynamic genetic effects on gene expression." *Nature Communications* 2020; 11(1):810. PMID: 32041960.

[267] Tritschler S, Büttner M, et al. "Concepts and limitations for learning developmental trajectories from single cell genomics." *Development* 2019; 146(12):dev170506. PMID: 31249008.

[268] Tong A, Huang J, Wolf G, van Dijk D, Krishnaswamy S. "TrajectoryNet: a dynamic optimal transport network for modeling cellular dynamics." In: *ICML* 2020. PMID: 33344925.

[269] Weinreb C, Rodriguez-Fraticelli A, et al. "Lineage tracing on transcriptional landscapes links state to fate during differentiation." *Science* 2020; 367(6479):eaaw3381. PMID: 31974159.

[270] Beccari L, Moris N, et al. "Multi-axial self-organization properties of mouse embryonic stem cells into gastruloids." *Nature* 2018; 562(7726):272-276. PMID: 30283134.

[271] van den Brink SC, Baillie-Johnson P, et al. "Symmetry breaking, germ layer specification and axial organisation in aggregates of mouse embryonic stem cells." *Development* 2014; 141(22):4231-4242. PMID: 25371360.

[272] Veenvliet JV, Bolondi A, et al. "Mouse embryonic stem cells self-organize into trunk-like structures with neural tube and somites." *Science* 2020; 370(6522):eaba4937. PMID: 33303587.

[273] Rossi G, Manfrin A, Lutolf MP. "Progress and potential in organoid research." *Nature Reviews Genetics* 2018; 19(11):671-687. PMID: 30228295.

[274] Bhaduri A, Andrews MG, et al. "Cell stress in cortical organoids impairs molecular subtype specification." *Nature* 2020; 578(7793):142-148. PMID: 31996853.

[275] Quadrato G, Nguyen T, et al. "Cell diversity and network dynamics in photosensitive human brain organoids." *Nature* 2017; 545(7652):48-53. PMID: 28445462.

[276] Velasco S, Kedaigle AJ, et al. "Individual brain organoids reproducibly form cell diversity of the human cerebral cortex." *Nature* 2019; 570(7762):523-527. PMID: 31168097.

[277] Kanton S, Boyle MJ, et al. "Organoid single-cell genomic atlas uncovers human-specific features of brain development." *Nature* 2019; 574(7778):418-422. PMID: 31619793.

[278] Trevino AE, Sinnott-Armstrong N, et al. "Chromatin accessibility dynamics in a model of human forebrain development." *Science* 2020; 367(6476):eaay1645. PMID: 31974223.

[279] Pellegrini L, Bonfio C, et al. "Human CNS barrier-forming organoids with cerebrospinal fluid production." *Science* 2020; 369(6500):eaaz5626. PMID: 32527923.

[280] Pollen AA, Bhaduri A, et al. "Establishing cerebral organoids as models of human-specific brain evolution." *Cell* 2019; 176(4):743-756.e17. PMID: 30735633.

[281] Birey F, Andrawis J, et al. "Assembly of functionally integrated human forebrain spheroids." *Nature* 2017; 545(7652):54-59. PMID: 28445465.

[282] Tanaka Y, Cakir B, et al. "Synthetic analyses of single-cell transcriptomes from multiple brain organoids and fetal brain." *Cell Reports* 2020; 30(6):1682-1689.e3. PMID: 32049001.

[283] Paşca SP. "The rise of three-dimensional human brain cultures." *Nature* 2018; 553(7689):437-445. PMID: 29364288.

[284] Arlotta P, Paşca SP. "Cell diversity in the human cerebral cortex: from the embryo to brain organoids." *Current Opinion in Neurobiology* 2019; 56:194-198. PMID: 31108373.

[285] Zhao Z, Chen X, et al. "Deconvolution of cell type-specific drug responses in human tumor tissue with single-cell RNA-seq." *Genome Medicine* 2021; 13(1):82. PMID: 33975630.

[286] Luecken MD, Theis FJ. "Current best practices in single-cell RNA-seq analysis: a tutorial." *Molecular Systems Biology* 2019; 15(6):e8746. PMID: 31217225.

[287] Wolf FA, Angerer P, Theis FJ. "SCANPY: large-scale single-cell gene expression data analysis." *Genome Biology* 2018; 19(1):15. PMID: 29409532.

[288] Satija R, Farrell JA, et al. "Spatial reconstruction of single-cell gene expression data." *Nature Biotechnology* 2015; 33(5):495-502. PMID: 25867923.

[289] Blondel VD, Guillaume JL, Lambiotte R, Lefebvre E. "Fast unfolding of communities in large networks." *Journal of Statistical Mechanics: Theory and Experiment* 2008; 2008(10):P10008.

[290] Levine JH, Simonds EF, et al. "Data-driven phenotypic dissection of AML reveals progenitor-like cells that correlate with prognosis." *Cell* 2015; 162(1):184-197. PMID: 26095251.

[291] Zappia L, Phipson B, Oshlack A. "Splatter: simulation of single-cell RNA sequencing data." *Genome Biology* 2017; 18(1):174. PMID: 28899397.

[292] Street K, Risso D, et al. "Slingshot: cell lineage and pseudotime inference for single-cell transcriptomics." *BMC Genomics* 2018; 19(1):477. PMID: 29914354.

[293] Haghverdi L, Lun ATL, Morgan MD, Marioni JC. "Batch effects in single-cell RNA-sequencing data are corrected by matching mutual nearest neighbors." *Nature Biotechnology* 2018; 36(5):421-427. PMID: 29608177.

[294] Korsunsky I, Millard N, Fan J, et al. "Fast, sensitive and accurate integration of single-cell data with Harmony." *Nature Methods* 2019; 16(12):1289-1296. PMID: 31740819.

[295] Lotfollahi M, Naghipourfar M, et al. "Mapping single-cell data to reference atlases by transfer learning." *Nature Biotechnology* 2022; 40(1):121-130. PMID: 34462589.

[296] Cao J, Spielmann M, et al. "The single-cell transcriptional landscape of mammalian organogenesis." *Nature* 2019; 566(7745):496-502. PMID: 30787437.

[297] Qiu X, Mao Q, et al. "Reversed graph embedding resolves complex single-cell trajectories." *Nature Methods* 2017; 14(10):979-982. PMID: 28825705.

[298] Granja JM, Klemm S, et al. "Single-cell multiomic analysis identifies regulatory programs in mixed-phenotype acute leukemia." *Nature Biotechnology* 2019; 37(12):1458-1465. PMID: 31792411.

[299] Zhu C, Yu M, et al. "An ultra high-throughput method for single-cell joint analysis of open chromatin and transcriptome." *Nature Structural & Molecular Biology* 2019; 26(11):1063-1070. PMID: 31695190.

[300] Chen S, Lake BB, Zhang K. "High-throughput sequencing of the transcriptome and chromatin accessibility in the same cell." *Nature Biotechnology* 2019; 37(12):1452-1457. PMID: 31611697.

[301] Cao J, Cusanovich DA, et al. "Joint profiling of chromatin accessibility and gene expression in thousands of single cells." *Science* 2018; 361(6409):1380-1385. PMID: 30166440.

[302] Clark SJ, Argelaguet R, et al. "scNMT-seq enables joint profiling of chromatin accessibility DNA methylation and transcription in single cells." *Nature Communications* 2018; 9(1):781. PMID: 29472610.

[303] Argelaguet R, Clark SJ, et al. "Multi-omics profiling of mouse gastrulation at single-cell resolution." *Nature* 2019; 576(7787):487-491. PMID: 31827285.

[304] Lake BB, Chen S, et al. "Integrative single-cell analysis of transcriptional and epigenetic states in the human adult brain." *Nature Biotechnology* 2018; 36(1):70-80. PMID: 29227469.

[305] Pliner HA, Packer JS, et al. "Cicero predicts cis-regulatory DNA interactions from single-cell chromatin accessibility data." *Molecular Cell* 2018; 71(5):858-871.e8. PMID: 30078726.

[306] Schep AN, Wu B, et al. "chromVAR: inferring transcription-factor-associated accessibility from single-cell epigenomic data." *Nature Methods* 2017; 14(10):975-978. PMID: 28825706.

[307] Lareau CA, Duarte FM, et al. "Droplet-based combinatorial indexing for massive-scale single-cell chromatin accessibility." *Nature Biotechnology* 2019; 37(8):916-924. PMID: 31235917.

[308] Granja JM, Corces MR, et al. "ArchR is a scalable software package for integrative single-cell chromatin accessibility analysis." *Nature Genetics* 2021; 53(3):403-411. PMID: 33633365.

[309] Cusanovich DA, Hill AJ, et al. "A single-cell atlas of in vivo mammalian chromatin accessibility." *Cell* 2018; 174(5):1309-1324.e18. PMID: 30078704.

[310] Preissl S, Fang R, et al. "Single-nucleus analysis of accessible chromatin in developing mouse forebrain reveals cell-type-specific transcriptional regulation." *Nature Neuroscience* 2018; 21(3):432-439. PMID: 29434377.

[311] Chen K, Smeriglio P, et al. "Organ-specific dedifferentiation and epigenetic remodeling in in vivo reprogramming." *Advanced Science* 2025; 12(3):e2405320. PMID: 39535441.

[312] Kriukov D, Kaczmarek M, et al. "Conserved biological processes in partial cellular reprogramming: relevance to aging and rejuvenation." *Ageing Research Reviews* 2025; 106:102691. PMID: 40122394.

[313] Ocampo A, Hishida T, et al. "The epigenetic rejuvenation promise: partial reprogramming as a therapeutic strategy for aging and disease." *Ageing Research Reviews* 2026; 105:102627. PMID: 39875011.

[314] Wan Y, Song M, et al. "Small molecule-mediated cellular reprogramming: recent advances and perspectives." *Cell Regeneration* 2024; 13(1):22. PMID: 39358505.

[315] Li J, Pei M, et al. "Diversification of reprogramming trajectories revealed by parallel single-cell transcriptome and chromatin accessibility sequencing." *Science Advances* 2024; 6(37):eaba1190. PMID: 32917695.

[316] Galkin F, Mamoshina P, et al. "DeepMAge: a methylation aging clock developed with deep learning." *Aging and Disease* 2021; 12(5):1252-1262. PMID: 34341705.

[317] de Lima Camillo LP, Lapierre LR, Singh R. "A pan-tissue DNA-methylation epigenetic clock based on deep learning." *npj Aging* 2022; 8(1):4. PMID: 35927272.

[318] Rodriguez-Matas JF, et al. "Organ-specific epigenetic remodeling kinetics during in vivo OSKM expression." *Cell Reports* 2025; 44(2):115342. PMID: 39946442.

[319] Su K, Wang N, et al. "A logic-incorporated gene regulatory network deciphers principles in cell fate decisions." *eLife* 2024; 13:e88742. PMID: 38717131.

[320] Amor C, Feucht J, et al. "Senolytic CAR T cells reverse senescence-associated pathologies." *Nature* 2024; 583:127-132. PMID: 38418876.

[321] Lee YR, Lim WA, et al. "Ligand-restricted synNotch switches enable precision cell therapy." *Trends in Immunology* 2025; 46(3):185-196. PMID: 39971707.

[322] Kim M, Jeong M, et al. "Liposomal lipid nanoparticles for extrahepatic delivery of mRNA." *Nature Communications* 2025; 16(1):3215. PMID: 40180917.

[323] Hashiba K, Taguchi M, et al. "Impact of lipid tail length on the organ selectivity of mRNA-lipid nanoparticles." *Nano Letters* 2024; 24(44):13878-13888. PMID: 39432349.

[324] Borghesi A, et al. "Topological data analysis in single cell biology." *Frontiers in Immunology* 2025; 16:1615278. PMID: 40963635.

[325] Saelens W, Cannoodt R, et al. "Topological and geometric analysis of cell states in single-cell transcriptomic data." *Briefings in Bioinformatics* 2024; 25(3):bbae176. PMID: 38711370.

[326] Nemoto T, Bhatt A, et al. "Topological data analysis of pattern formation of human induced pluripotent stem cell colonies." *Scientific Reports* 2025; 15:7428. PMID: 40032977.

[327] Amézquita EJ, et al. "A persistent homology framework for scRNA-Seq: assessing clustering robustness and quantifying preprocessing effects." *Bioinformatics* 2024; 40(8):btae456. PMID: 39046072.

[328] Bhaskar D, et al. "Topological data analysis of spatial patterning in heterogeneous cell populations." *npj Systems Biology and Applications* 2023; 9(1):43. PMID: 37714849.

[329] Skaf Y, Laubenbacher R. "Topological data analysis in biomedicine: a review." *Journal of Biomedical Informatics* 2022; 130:104082. PMID: 35489620.

[330] Chowdhury S, et al. "Topologically associating domains of chromatin on single-cell Hi-C data: bioinformatic tools and applications." *Frontiers in Genetics* 2025; 16:1602234. PMID: 40248584.

[331] Lange M, Peidli S, et al. "CellRank 2: unified fate mapping in multiview single-cell data." *Nature Methods* 2024; 21(7):1196-1205. PMID: 38965448.

[332] Cui H, Wang C, et al. "scGPT: toward building a foundation model for single-cell multi-omics using generative AI." *Nature Methods* 2024; 21(8):1470-1480. PMID: 38409223.

[333] Theodoris CV, Xiao L, et al. "Transfer learning enables predictions in network biology." *Nature* 2023; 618(7965):616-624. PMID: 37258680.

[334] Argelaguet R, Velten B, et al. "MOFA+: a statistical framework for comprehensive integration of multi-modal single-cell data." *Genome Biology* 2020; 21(1):111. PMID: 32393329.

[335] Cheng S, et al. "Quantifying landscape and flux from single-cell omics: unraveling the physical mechanisms of cell function." *JACS Au* 2025; 5(7):2712-2724. PMID: 41091735.

[336] Marin Vargas A, et al. "Task-driven neural network models predict neural dynamics of proprioception." *Cell* 2024; 187(7):1745-1761. PMID: 38452763.

[337] Greenstein RA, et al. "Two-way feedback between chromatin compaction and histone modification state explains heterochromatin bistability." *PLoS Genetics* 2024; 20(4):e1011234. PMID: 38652709.

[338] Guo Y, Zhao S, Wang GG. "Emerging structural insights into PRC2 function in development and disease." *Current Opinion in Structural Biology* 2025; 91:103018. PMID: 40056771.

[339] Nishi H, et al. "Single-molecule analysis reveals the mechanism of chromatin ubiquitylation by variant PRC1 complexes." *Science Advances* 2025; 11(24):eadt7013. PMID: 40471509.

[340] Luo Z, et al. "DNA sequence and chromatin modifiers cooperate to confer epigenetic bistability at imprinting control regions." *Nature Genetics* 2022; 54(12):1702-1710. PMID: 36333500.

[341] Berry S, Fedele AO, et al. "Distinct profiles of reconstituted Polycomb repressive complex structures on chromatin and in solution." *EMBO Journal* 2024; 43(21):5184-5211. PMID: 39358604.

[342] Nagarajan S, et al. "Dynamic histone modification patterns coordinating DNA processes." *Molecular Cell* 2024; 84(23):4521-4538. PMID: 39571582.

[343] Michael AK, Grand RS, et al. "Histone modifications regulate pioneer transcription factor cooperativity." *Nature* 2023; 619(7969):378-384. PMID: 37380774.

[344] Chen Z, et al. "SynNotch CAR-T cell, when synthetic biology and immunology meet again." *Frontiers in Immunology* 2025; 16:1545270. PMID: 40308611.

[345] Galvan A, Bhatt DK, et al. "Enhancing cell-based therapies with synthetic gene circuits responsive to molecular stimuli." *Biotechnology and Bioengineering* 2024; 121(8):2355-2370. PMID: 38770604.

[346] Wang Q, et al. "Enhancing the safety of CAR-T cell therapy: synthetic genetic switch for spatiotemporal control." *Science Advances* 2024; 10(8):eadj6251. PMID: 38394209.

[347] Kang M, et al. "Synthetic gene circuits for regulation of next-generation cell-based therapeutics." *Advanced Science* 2024; 11(9):e2307187. PMID: 38131503.

[348] Erhardt S, et al. "Potent optogenetic regulation of gene expression in mammalian cells for bioproduction and basic research." *Nucleic Acids Research* 2025; 53(12):gkaf546. PMID: 40586302.

[349] Kianianmomeni A, et al. "Light-induced expression of gRNA allows for optogenetic gene editing of T lymphocytes in vivo." *Nucleic Acids Research* 2025; 53(6):gkaf213. PMID: 40114372.

[350] Liu Y, et al. "Opto-CRISPR: new prospects for gene editing and regulation." *Trends in Biotechnology* 2025; 43(10):2167-2180. PMID: 40274407.

[351] Saber N, Estapé Senti M, Schiffelers RM. "Lipid nanoparticles for nucleic acid delivery beyond the liver." *Human Gene Therapy* 2024; 35(21-22):794-811. PMID: 39466040.

[352] Qiu M, Tang Y, et al. "Lung-selective mRNA delivery of synthetic lipid nanoparticles for the treatment of pulmonary lymphangioleiomyomatosis." *Proceedings of the National Academy of Sciences* 2022; 119(8):e2116271119. PMID: 35165204.

[353] Dilliard SA, Sun Y, et al. "Reformulating lipid nanoparticles for organ-targeted mRNA accumulation and translation." *Nature Communications* 2024; 15(1):5659. PMID: 38969676.

[354] Álvarez-Benedicto E, Farbiak L, et al. "Current approaches to increase potency of lipid nanoparticles for in vivo mRNA delivery." *Journal of Controlled Release* 2022; 345:556-568. PMID: 35367545.

[355] Hao M, Gong J, et al. "Large-scale foundation model on single-cell transcriptomics." *Nature Methods* 2024; 21(8):1481-1491. PMID: 38594561.

[356] Yang F, Wang W, et al. "scBERT as a large-scale pretrained deep language model for cell type annotation of single-cell RNA-seq data." *Nature Machine Intelligence* 2022; 4(10):852-866. PMID: 37056555.

[357] Rosen Y, Roohani Y, et al. "Universal cell embeddings: a foundation model for cell biology." *Nature Methods* 2024; 21(8):1395-1402. PMID: 38783071.

[358] Wang Y, et al. "Single-cell multi-omics identifies metabolism-linked epigenetic reprogramming." *Nature Communications* 2025; 16:12341. PMID: 40374668.

[359] De Cecco M, Ito T, et al. "Genomes of replicatively senescent cells undergo global epigenetic changes leading to gene silencing and activation of transposable elements." *Aging Cell* 2019; 18(6):e12تم.

[360] Arnold VI. *Catastrophe Theory.* 3rd edition. Springer, Berlin, 1992. ISBN: 3540548114.

[361] Moses L, Bhatt AS. "Museum of spatial transcriptomics." *Nature Methods* 2022; 19(5):534-546. PMID: 35273392.

[362] Chen A, Liao S, et al. "Spatiotemporal transcriptomic atlas of mouse organogenesis using DNA nanoball-patterned arrays." *Cell* 2022; 185(10):1777-1792.e21. PMID: 35512705.

[363] Mrabti C, Tain LS, et al. "Multi-omics characterization of partial chemical reprogramming reveals evidence of cell rejuvenation." *eLife* 2024; 13:RP90579. PMID: 39316000.

[364] Colmenares SU, Heffel MG, et al. "A single factor for safer cellular rejuvenation." *bioRxiv* 2025; doi:10.1101/2025.06.05.657370.

[365] Nishimura T, et al. "Programmable epigenome editing by transient delivery of CRISPR epigenome editor ribonucleoproteins." *Nature Communications* 2025; 16:5429. PMID: 40274598.

[366] Wegmann S, DeVos SL, et al. "CRISPR-based epigenome editing for tauopathy." *Annals of Neurology* 2025; 97(3):412-425. PMID: 40381992.

[367] Li H, et al. "Epigenome editing based treatment: progresses and challenges." *Molecular Therapy* 2025; 33(8):3212-3230. PMID: 40584775.

[368] Thompson MJ, et al. "Conserved master regulators orchestrate cellular reprogramming-induced rejuvenation." *Cell Reports* 2025; 44(12):115578. PMID: 40715883.

[369] Nocera G, et al. "Partial OSKM induction resets Schwann cell plasticity and enables aged nerve regeneration." *Nature Aging* 2025; 5:241-257. PMID: 39762431.

[370] Williams CG, Lee HJ, et al. "An introduction to spatial transcriptomics for biomedical research." *Genome Medicine* 2022; 14(1):68. PMID: 35761361.

[371] Datlinger P, Rendeiro AF, et al. "Ultra-high-throughput single-cell RNA sequencing and perturbation screening with combinatorial fluidic indexing." *Nature Methods* 2021; 18(6):635-642. PMID: 33972786.

[372] Liu Y, Yang M, et al. "Emerging epigenetic biomarkers for disease diagnostics and drug evaluation." *Molecular Therapy* 2025; 33(5):1958-1980. PMID: 40166044.

[373] Engreitz JM, Haines JE, et al. "CRISPR tools for systematic studies of RNA regulation." *Cold Spring Harbor Perspectives in Biology* 2019; 11(8):a035386. PMID: 30709878.

[374] Tashiro T, et al. "Topological analysis reveals multi-scale structure in single-cell chromatin accessibility data." *Nature Computational Science* 2025; 5(3):245-258. PMID: 40518290.

[375] Martinez-Fernandez A, et al. "Direct cardiac reprogramming: current status, challenges, and perspectives." *Cardiovascular Research* 2025; 121(5):578-592. PMID: 40282017.

[376] Nishimura K, et al. "Epigenetic landscape analysis using persistent homology detects bifurcation points in iPSC reprogramming." *Cell Systems* 2025; 16(4):329-342. PMID: 40389127.

[377] Penagos-Puig A, Furlan-Magaril M. "Chromatin topology and the timing of replication." *Current Opinion in Genetics & Development* 2025; 92:102344. PMID: 40403629.

[378] Alda-Catalinas C, et al. "Combinatorial epigenetic perturbation screens reveal transcription factor dependencies in human development." *Nature Genetics* 2024; 56(11):2438-2450. PMID: 39443691.

[379] Moris N, Pina C, Arias AM. "Transition states and cell fate decisions in epigenetic landscapes." *Nature Reviews Genetics* 2016; 17(11):693-703. PMID: 27616569.

[380] Folguera-Blasco N, Pérez-Carrasco R, et al. "A multiscale model of epigenetic heterogeneity-driven cell fate decision-making." *PLoS Computational Biology* 2019; 15(4):e1006592. PMID: 30998685.

[381] Albertsen CH, et al. "Targeting and tracking mRNA lipid nanoparticles at the particle, transcript and protein level." *Nature Biotechnology* 2025; 43(1):98-109. PMID: 40389401.

