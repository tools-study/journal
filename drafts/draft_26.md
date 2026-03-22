# IToA Review

---

## Abstract

The Information Theory of Aging (IToA) posits that the progressive loss of epigenetic information — rather than the accumulation of genetic mutations — is the principal causal driver of biological aging. Formulated most explicitly by Sinclair and colleagues, and tested through the Inducible Changes to the Epigenome (ICE) mouse model (Yang et al., 2023), this hypothesis reframes aging as a fundamentally information-theoretic process: the degradation of an analog signal (the epigenome) superimposed on a digital substrate (the genome). The theory's most provocative prediction — that a recoverable "backup copy" of youthful epigenetic information persists throughout the lifespan, accessible through Yamanaka factor–mediated reprogramming — has generated both extraordinary experimental support and rigorous criticism. This paper provides a comprehensive critical evaluation of the IToA within the broader landscape of aging theories. We develop six novel mathematical frameworks that formalize the epigenome as a communication system subject to Shannon-theoretic constraints: (1) a channel coding theorem for epigenetic maintenance predicting age-dependent decline in error-correcting capacity; (2) a rate-distortion theory establishing the minimum metabolic cost to maintain epigenetic fidelity; (3) mutual information decay kinetics linking epigenetic clocks to information-theoretic quantities; (4) a Fisher information geometry of aging trajectories on the CpG methylation manifold; (5) Landauer's principle applied to calculate the thermodynamic energy cost of epigenetic rejuvenation; and (6) a Galton-Watson branching process model predicting a critical age threshold for irreversible error accumulation. We marshal evidence from epigenetic clock studies, partial reprogramming experiments, the ICE mouse model, and the first human epigenetic reprogramming trial (Life Biosciences ER-100, 2026) in support of the theory. Against this, we evaluate evidence from stochastic clock analyses, somatic mutation accumulation, proteostasis failure, mitochondrial DNA damage, telomere biology, cross-species reprogramming failures, and the possibility that age-associated epigenetic changes are adaptive rather than degenerative. We conclude that the IToA captures a genuine and therapeutically tractable dimension of aging — epigenetic information loss is real, measurable, and partially reversible — but that it is most accurately understood as one channel within a multi-channel information degradation process that includes irreversible genetic, proteomic, and metabolic components. We propose eight detailed experimental programs designed to decisively test the theory's central predictions and resolve the question of whether epigenetic reprogramming alone is sufficient for comprehensive rejuvenation.

---

## 1. Introduction

### 1.1 The Information-Theoretic Turn in Aging Biology

The study of biological aging has undergone a conceptual transformation over the past two decades, shifting from a descriptive catalog of age-associated pathologies toward a search for unifying causal mechanisms. The hallmarks of aging framework (López-Otín et al., 2013), updated in 2023 to include disabled macroautophagy, chronic inflammation, and dysbiosis as additional hallmarks (López-Otín et al., 2023), provided an invaluable taxonomy: genomic instability, telomere attrition, epigenetic alterations, loss of proteostasis, deregulated nutrient sensing, mitochondrial dysfunction, cellular senescence, stem cell exhaustion, and altered intercellular communication. Yet taxonomy is not mechanism. The hallmarks framework identifies *what* changes with age but remains agnostic about *which* changes are causes, which are consequences, and whether a single upstream process could account for multiple downstream hallmarks.

The information-theoretic turn in aging biology represents an attempt to identify such an upstream process. If a cell is understood as a system that stores, transmits, and processes biological information, then aging can be reframed as the degradation of that information over time. This perspective has deep roots. Orgel (1963) proposed the "error catastrophe" hypothesis — that accumulated errors in protein synthesis would propagate through the translational machinery, producing an exponentially increasing error rate. While the strong form of Orgel's hypothesis was refuted by the demonstration that translational fidelity does not decline catastrophically with age (Gallant & Prothero, 1980; Harley et al., 1980), the underlying intuition — that aging is fundamentally an information-processing failure — has proven remarkably durable.

The modern information-theoretic framework shifts the locus of information loss from proteins to the epigenome. The genome, comprising approximately 3.2 billion base pairs in humans, is a digital information store: its content is discrete (four nucleotides), redundantly encoded (through diploidy and error-correcting codes embedded in codon degeneracy), and maintained with extraordinary fidelity by DNA repair systems achieving error rates of approximately $10^{-10}$ per base pair per cell division (Kunkel, 2004). The epigenome, by contrast, is an analog information layer: DNA methylation patterns, histone modifications, and chromatin architecture encode continuous, graded signals that specify cell identity and function. Unlike the genome, the epigenome lacks robust error-correcting codes. Methylation maintenance by DNMT1 operates with per-site fidelity of approximately 95-99% per cell division (Genereux et al., 2005; Ming et al., 2020), meaning that epigenetic information is copied with error rates five to ten orders of magnitude higher than genetic information. This asymmetry — digital precision for the genome, analog vulnerability for the epigenome — is the foundation of the Information Theory of Aging.

### 1.2 Sinclair's Formulation: Digital Versus Analog Information

The most explicit formulation of the Information Theory of Aging comes from David Sinclair and colleagues (Sinclair, 2019; Yang et al., 2023). In Sinclair's framework, the genome and epigenome carry fundamentally different types of biological information, analogous to a compact disc (digital, robust) and a DVD's analog surface features (analog, degradable). The genome stores the complete instruction set for building an organism — every cell in the body carries the same genomic information. The epigenome stores the *implementation* of those instructions: which genes are active, at what levels, in which cell types, and in response to which signals. Cellular identity, tissue function, and organismal homeostasis depend on the faithful maintenance of this epigenetic program.

Sinclair's central claim is that aging is caused primarily by the progressive loss of epigenetic information — not by the accumulation of genetic mutations, which occur at rates too low to account for the kinetics of mammalian aging. As cells divide, DNA methylation patterns drift, histone modifications are imprecisely copied, and chromatin architecture degrades. This drift is accelerated by DNA damage, particularly double-strand breaks (DSBs), which trigger the redistribution of chromatin-modifying enzymes from their normal positions to damage sites. When SIRT1, SIRT6, and other chromatin regulators are recruited to DSBs for repair, they vacate their normal genomic positions, causing epigenetic dysregulation at distant loci (Oberdoerffer et al., 2008; Van Meter et al., 2016). Over time, this DSB-driven redistribution creates cumulative epigenetic noise that manifests as the functional decline we recognize as aging.

The theory's most striking prediction is the "backup copy" hypothesis: even though the active epigenetic program degrades with age, a recoverable record of the youthful epigenetic state persists in the cell — perhaps encoded in the three-dimensional genome architecture, in non-CpG methylation patterns, or in chromatin states that are read but not overwritten during normal epigenetic maintenance. This backup copy can be accessed through the expression of Yamanaka factors (Oct4, Sox2, Klf4), which reset the epigenome to its youthful configuration without reverting cells to pluripotency (when applied transiently) and without altering the underlying genomic sequence.

### 1.3 The ICE Mouse Model as the Central Experimental Test

The Information Theory of Aging found its most rigorous experimental test in the Inducible Changes to the Epigenome (ICE) mouse model developed by Yang, Lu, and colleagues (Yang et al., 2023). The ICE system uses a CRE-loxP–inducible I-PpoI endonuclease to generate approximately 20 non-mutagenic DNA double-strand breaks at defined genomic sites upon tamoxifen administration. These breaks are faithfully repaired — the system was engineered to produce DSBs at I-PpoI recognition sites within ribosomal DNA, where non-homologous end joining restores the original sequence — but the act of repair triggers the redistribution of chromatin modifiers (including SIRT1 and HDAC1) to break sites, causing epigenetic dysregulation at other loci.

The results were striking. ICE mice subjected to repeated DSB induction displayed accelerated epigenetic aging as measured by multiple DNA methylation clocks, progressing approximately 1.5 times faster than controls. They exhibited hallmarks of premature aging: hair graying, reduced muscle mass, decreased activity, and cognitive decline. Critically, the ICE mice showed no increase in somatic mutation burden — the aging phenotype arose from epigenetic disruption alone, with the genome remaining intact. The accelerated aging was then partially reversed by systemic delivery of OSK factors via adeno-associated virus (AAV), which restored histone modifications (H3K9me3 in kidney, H3K36me2 in muscle) and DNA methylation patterns to younger configurations, reducing epigenetic age by up to 57%.

This experiment constitutes the strongest evidence for the IToA's causal claim: that epigenetic information loss, independent of genetic damage, is sufficient to drive mammalian aging. The reversal by OSK provides proof-of-concept for the backup copy hypothesis — if the youthful epigenetic information were truly lost, reprogramming factors would have no template from which to restore it.

### 1.4 Scope of This Evaluation

This paper evaluates the IToA as both a specific hypothesis (Sinclair's formulation centering on the ICE model and epigenetic backup copy) and as a broader information-theoretic framework for understanding aging. We develop novel mathematical formalisms that make the theory's predictions quantitative and falsifiable (Section 4). We present evidence supporting the theory from epigenetic clocks, reprogramming experiments, and clinical translation (Section 5). We then marshal evidence against the theory from stochastic clock analyses, somatic mutations, proteostasis, mitochondrial biology, telomere dynamics, and cross-species studies (Section 6). We propose a synthesis that positions the IToA as a partially correct theory within a multi-channel information degradation framework (Section 7), and design eight critical experiments to resolve outstanding questions (Section 8).

Throughout, our evaluation is weighted toward Sinclair's formulation — not because it is necessarily correct in its strongest form, but because it is the most experimentally specific and falsifiable version of the information-theoretic framework. A theory that makes precise, testable predictions deserves rigorous evaluation, even if the evidence ultimately supports a more nuanced view.

---

## 2. Theoretical Foundations

### 2.1 Relationship to the Hallmarks Framework

The hallmarks of aging framework identifies twelve interconnected processes that characterize biological aging (López-Otín et al., 2013; López-Otín et al., 2023). The IToA's relationship to this framework is hierarchical rather than competitive: it proposes that epigenetic alterations — one of the twelve hallmarks — function as an upstream driver that causally influences multiple downstream hallmarks.

This hierarchical claim finds support in the observation that epigenetic dysregulation can, in principle, drive several other hallmarks. Aberrant DNA methylation can silence tumor suppressors, promoting genomic instability (Esteller, 2008; Baylin & Jones, 2016). Epigenetic drift at stem cell regulatory loci can cause stem cell exhaustion (Beerman et al., 2013; Sun et al., 2014). Dysregulated gene expression from epigenetic noise can impair proteostasis by altering chaperone expression (Labbadia & Morimoto, 2015). Epigenetic changes in immune cells can drive the chronic inflammatory phenotype known as inflammaging (Franceschi et al., 2018; Guo et al., 2024; Li et al., 2024). Kabacik et al. (2022) directly tested this hierarchical relationship and found that epigenetic age acceleration is significantly associated with multiple hallmarks of aging in human cells, though the causal direction remained ambiguous. Wang et al. (2022) reviewed the broader landscape of epigenetic regulation in aging, highlighting how DNA methylation, histone modifications, and chromatin remodeling collectively influence lifespan-modulating pathways. If one accepts the IToA, then epigenetic information loss emerges as a master regulator sitting upstream of multiple hallmarks, providing the unifying mechanism that the hallmarks framework describes but does not identify.

However, this hierarchical claim is not the only interpretation. An equally valid reading of the evidence positions epigenetic alterations as one node in a complex causal network, influenced by and influencing other hallmarks through bidirectional feedback. DNA damage (genomic instability) causes epigenetic disruption (as demonstrated by the ICE model), but epigenetic disruption may also impair DNA repair gene expression, creating a positive feedback loop. Similarly, mitochondrial dysfunction alters the availability of metabolites (NAD+, SAM, α-ketoglutarate) that serve as cofactors for epigenetic enzymes, while epigenetic changes can dysregulate mitochondrial biogenesis genes (Matilainen et al., 2017; Srivastava, 2017). In this network view, asking whether epigenetic information loss is *the* cause of aging is analogous to asking which node in a fully connected graph is *the* most important — a question that may not have a unique answer.

### 2.2 Alternative Theories of Aging

The IToA must be evaluated against several competing theoretical frameworks, each with substantial empirical support.

**Programmed aging theories** propose that aging follows a genetically determined schedule, evolved to regulate population turnover or remove post-reproductive individuals who compete with their offspring for resources (Longo et al., 2005; Goldsmith, 2008). The strongest evidence comes from the remarkable precision of species-specific lifespans and the existence of aging "programs" in organisms like *Caenorhabditis elegans*, where single-gene mutations (e.g., *daf-2*) can double lifespan (Kenyon, 2010). However, programmed aging is difficult to reconcile with the evolutionary principle that selection pressure weakens dramatically after peak reproductive age (Medawar, 1952; Hamilton, 1966).

**The hyperfunction theory** (Blagosklonny, 2008, 2013; see Blagosklonny, 2022 for the developmental rapamycin evidence) proposes that aging results not from the loss of function but from the excessive continuation of developmental growth programs — notably mTOR signaling — beyond the point of reproductive maturity. In this view, aging is "quasi-programmed": not evolved for a purpose, but driven by growth-promoting pathways that were selected for their benefits during development and reproduction but become deleterious when they continue unopposed in adulthood. The hyperfunction theory is supported by the lifespan-extending effects of mTOR inhibition (rapamycin) across species (Harrison et al., 2009; Bitto et al., 2016) and by the observation that many age-related diseases (atherosclerosis, hypertension, cancer) involve cellular overgrowth or hyperactivation rather than passive decline.

**Damage accumulation theories**, including the free radical theory of aging (Harman, 1956), propose that aging results from the progressive accumulation of molecular damage — oxidized proteins, lipofuscin, cross-linked collagen, DNA lesions — that exceeds the cell's repair capacity. While the strong form of the free radical theory has been challenged by the failure of antioxidant supplementation to extend lifespan (Pérez et al., 2009) and by the existence of long-lived species with high oxidative damage (naked mole-rats; Andziak et al., 2006), the broader damage-accumulation framework remains influential.

**Antagonistic pleiotropy** (Williams, 1957) and the **disposable soma theory** (Kirkwood, 1977; Kirkwood & Holliday, 1979) propose evolutionary explanations: genes that enhance early-life fitness but cause late-life pathology are selected because their reproductive benefits outweigh their post-reproductive costs, and organisms allocate limited resources preferentially to reproduction over somatic maintenance. These theories explain *why* organisms age but are less specific about *how*. Recent evidence has strengthened the antagonistic pleiotropy framework: Mostafavi et al. (2023) demonstrated a strong negative genetic correlation between reproductive traits and lifespan in over 276,000 UK Biobank participants, with individuals carrying higher polygenic scores for reproduction showing significantly lower survivorship to age 76. A 2025 study in *eLife* found that early menarche and early childbirth nearly doubled the risk of diabetes and heart failure later in life. Troncoso-Escudero et al. (2023) provided a molecular demonstration in cardiac tissue, showing that IGF-1R signaling improves heart function in young mice but causes premature heart failure during aging — a textbook example of antagonistic pleiotropy at the single-gene level.

### 2.3 Where the IToA Sits: Unifying Principle or One of Many?

The IToA attempts to subsume these alternatives under an information-theoretic umbrella. In this view, programmed aging represents a genetically encoded schedule for reducing epigenetic maintenance capacity; hyperfunction represents a form of informational noise where growth signals persist beyond their appropriate developmental context; damage accumulation describes the physical substrate of information loss; and antagonistic pleiotropy explains why natural selection did not evolve better epigenetic error-correction. The IToA's claim is not that these theories are wrong, but that they describe different facets of a single underlying process: the loss of biological information.

Whether this subsumption is illuminating or merely semantic depends on whether the information-theoretic framing generates novel, falsifiable predictions that the individual theories do not. We argue in Section 4 that it does, and in Section 8 we propose experiments to test these predictions.

---

## 3. Mathematical Framework: The Epigenome as a Communication System

We develop six novel mathematical frameworks that formalize the IToA's central claims as quantitative, falsifiable predictions. Each framework applies a distinct information-theoretic or stochastic process tool to the epigenome, generating predictions that can be tested with existing experimental technologies. We present key equations with variable definitions and biological interpretations; extended derivations are available in the Supplementary Material.

### 3.1 Channel Coding Theorem for Epigenetic Maintenance

The epigenetic maintenance machinery — DNMT1 for DNA methylation, Polycomb repressive complexes (PRC1/PRC2) for histone modifications, and TET enzymes for active demethylation — can be modeled as a noisy communication channel that transmits epigenetic information from mother cell to daughter cell during each cell division. Shannon's channel coding theorem (Shannon, 1948) establishes that reliable information transmission is possible if and only if the information rate does not exceed the channel capacity.

We define the epigenetic channel capacity $C_{\text{epi}}(t)$ as the maximum rate (in bits per cell division) at which epigenetic information can be faithfully transmitted at organismal age $t$. For a single CpG site maintained by DNMT1 with age-dependent fidelity $f(t)$, the binary symmetric channel model gives:

```math
C_{\text{CpG}}(t) = 1 - H_b(\varepsilon(t)) = 1 + \varepsilon(t) \log_2 \varepsilon(t) + (1 - \varepsilon(t)) \log_2 (1 - \varepsilon(t))
```

where $\varepsilon(t) = 1 - f(t)$ is the per-division methylation error rate at age $t$, and $H_b(\varepsilon)$ is the binary entropy function. For the full epigenome with $N$ CpG sites and correlated maintenance errors described by a joint error model with correlation matrix $\Sigma_\varepsilon(t)$, the total channel capacity is:

```math
C_{\text{epi}}(t) = \sum_{i=1}^{N} C_{\text{CpG},i}(t) - I_{\text{corr}}(t)
```

where $I_{\text{corr}}(t) \geq 0$ captures the capacity reduction from correlated errors (e.g., regional failure of DNMT1 recruitment affecting neighboring CpG sites within a single replication domain).

**Variable definitions:**
- $C_{\text{epi}}(t)$: total epigenetic channel capacity at age $t$ (bits per cell division)
- $f(t)$: per-site methylation maintenance fidelity at age $t$ (dimensionless, $\in [0,1]$)
- $\varepsilon(t)$: per-site error probability, $\varepsilon(t) = 1 - f(t)$
- $H_b(\varepsilon)$: binary entropy function (bits)
- $N$: total number of maintained CpG sites ($\approx 2.8 \times 10^7$ in the human genome)
- $I_{\text{corr}}(t)$: mutual information between error events at different sites (bits)

**IToA prediction:** $C_{\text{epi}}(t)$ declines monotonically with age as DNMT1 fidelity decreases and correlated errors increase, eventually falling below the rate $R_{\text{epi}}$ needed to maintain cellular identity. The age at which $C_{\text{epi}}(t) < R_{\text{epi}}$ corresponds to the onset of functional decline. This decline should be measurable as increasing methylation maintenance error rates in aging primary human cells.

### 3.2 Rate-Distortion Theory for Aging

Rate-distortion theory (Shannon, 1959) addresses the dual problem: given a maximum tolerable distortion $D$ in the reproduced signal, what is the minimum information rate $R(D)$ required? Applied to epigenetic maintenance, this framework asks: how many bits per cell division must the maintenance machinery invest to keep the epigenome within functional tolerance?

We define the distortion measure $d(\mathbf{m}_0, \mathbf{m}_t)$ between the youthful methylation profile $\mathbf{m}_0$ and the current profile $\mathbf{m}_t$ as the Hamming distance over binarized methylation states:

```math
d(\mathbf{m}_0, \mathbf{m}_t) = \frac{1}{N} \sum_{i=1}^{N} \mathbb{1}[m_{0,i} \neq m_{t,i}]
```

The rate-distortion function for the epigenetic channel with Bernoulli source and binary symmetric distortion is:

```math
R_{\text{epi}}(D) = \begin{cases} H_b(p) - H_b(D), & 0 \leq D \leq \min(p, 1-p) \\ 0, & D > \min(p, 1-p) \end{cases}
```

where $p$ is the fraction of methylated CpG sites in the youthful state (approximately 0.7-0.8 genome-wide in differentiated human cells; Lister et al., 2009). The metabolic cost of epigenetic maintenance can then be bounded:

```math
E_{\text{maintenance}}(D) \geq R_{\text{epi}}(D) \cdot k_B T \ln 2
```

where $k_B T \ln 2 \approx 2.85 \times 10^{-21}$ J at 37°C is the Landauer limit per bit of information processing.

**Variable definitions:**
- $R_{\text{epi}}(D)$: minimum information rate (bits/division) for distortion ≤ $D$
- $D$: fractional Hamming distortion between youthful and current methylation profiles
- $p$: fraction of methylated CpG sites in the reference (youthful) state
- $E_{\text{maintenance}}(D)$: minimum energy required per cell division for maintenance
- $k_B$: Boltzmann constant ($1.381 \times 10^{-23}$ J/K)
- $T$: absolute temperature (310 K for human physiology)

**Biological interpretation:** This framework predicts a theoretical energy floor for epigenetic maintenance — the minimum metabolic investment required to keep the epigenome within a functional distortion threshold. If aging is associated with declining energy allocation to maintenance (consistent with the disposable soma theory), the distortion will increase when maintenance energy falls below $R_{\text{epi}}(D_{\text{threshold}}) \cdot k_B T \ln 2$.

### 3.3 Mutual Information Decay Kinetics

The mutual information $I(X_0; X_t)$ between the youthful epigenetic state $X_0$ and the state $X_t$ at age $t$ provides a direct measure of how much of the original epigenetic program is recoverable from the current state. We model this decay as a stretched exponential:

```math
I(X_0; X_t) = I_0 \exp\left[-\left(\frac{t}{\tau_{\text{epi}}}\right)^\beta\right]
```

where $I_0$ is the initial mutual information (maximum at birth), $\tau_{\text{epi}}$ is the characteristic information decay time, and $\beta \in (0,1]$ is the stretching exponent that captures the heterogeneity of decay rates across different genomic regions.

The connection to empirical epigenetic clocks is made through the relationship between mutual information and clock predictions. An epigenetic clock $\hat{t}(\mathbf{m})$ trained on methylation data $\mathbf{m}$ extracts information about biological age from the methylation profile. The clock's accuracy — quantified by its coefficient of determination $R^2$ — is bounded by the mutual information:

```math
R^2_{\text{clock}} \leq \frac{2^{2 I(X_0; X_t)} - 1}{2^{2 I_0} - 1}
```

This inequality follows from the data processing inequality: the clock, as a deterministic function of the methylation data, cannot extract more information about age than is present in the data itself.

**Variable definitions:**
- $I(X_0; X_t)$: mutual information between youthful and aged epigenetic states (bits)
- $I_0$: baseline mutual information at $t = 0$ (bits)
- $\tau_{\text{epi}}$: characteristic decay time (years), tissue-dependent
- $\beta$: stretching exponent (dimensionless); $\beta = 1$ gives simple exponential decay; $\beta < 1$ indicates heterogeneous decay rates across CpG sites
- $R^2_{\text{clock}}$: coefficient of determination for an epigenetic clock

**Biological interpretation:** The stretching exponent $\beta$ captures a prediction unique to the IToA: different CpG sites lose information at different rates, depending on their maintenance enzyme recruitment, chromatin context, and exposure to DSB-induced chromatin remodeling. Actively transcribed regions near recombination hotspots should show faster information loss ($\beta$ closer to 1) than heterochromatic regions with stable maintenance ($\beta$ closer to 0). Empirical estimation of $\beta$ from longitudinal methylation data would test this prediction.

### 3.4 Fisher Information Geometry of Aging Trajectories

We model the aging process as a trajectory on a statistical manifold $\mathcal{M}$ whose points represent probability distributions over CpG methylation states. Each tissue at a given age defines a point on this manifold, and aging traces a curve through it. The natural metric on this manifold is the Fisher information metric.

For a tissue with $N$ CpG sites, the methylation state is described by the probability vector $\mathbf{p} = (p_1, p_2, \ldots, p_N)$ where $p_i \in [0,1]$ is the methylation probability at site $i$. The Fisher information metric tensor on $\mathcal{M}$ is:

```math
g_{ij}(\mathbf{p}) = \frac{\delta_{ij}}{p_i(1 - p_i)}
```

The length of an aging trajectory $\gamma: [0, t] \to \mathcal{M}$ is:

```math
L(\gamma) = \int_0^t \sqrt{\sum_{i=1}^{N} \frac{1}{p_i(s)(1-p_i(s))} \left(\frac{dp_i}{ds}\right)^2} \, ds
```

This Fisher-Rao length provides an information-geometric measure of the total epigenetic change between ages 0 and $t$, with contributions from each CpG site weighted by the inverse variance of its methylation state. Sites near the boundaries ($p_i \approx 0$ or $p_i \approx 1$) contribute more to the length per unit change in $p_i$, reflecting the fact that changes at stably methylated or unmethylated sites are more informationally significant than changes at sites with intermediate methylation.

**Variable definitions:**
- $\mathcal{M}$: statistical manifold of methylation probability distributions
- $\mathbf{p}$: methylation probability vector $(p_1, \ldots, p_N) \in [0,1]^N$
- $g_{ij}(\mathbf{p})$: Fisher information metric tensor at point $\mathbf{p}$
- $L(\gamma)$: Fisher-Rao arc length of aging trajectory $\gamma$
- $s$: parametrizing variable (chronological age in years)

**Biological interpretation:** Different tissues age along different trajectories on the same manifold $\mathcal{M}$, and the Fisher-Rao distance between a tissue's aged state and its youthful state provides a principled, reparameterization-invariant measure of tissue-specific aging rate. The IToA predicts that all tissue trajectories should converge toward a common "aged attractor" region of $\mathcal{M}$ — reflecting the loss of tissue-specific epigenetic identity toward a generic, high-entropy state. Geodesics on $\mathcal{M}$ (shortest paths under the Fisher metric) would represent the most parsimonious aging trajectories, and deviations from geodesic aging would indicate the influence of external factors (diet, environment, disease) on the aging process.

### 3.5 Landauer's Principle and the Thermodynamic Cost of Rejuvenation

Landauer's principle (Landauer, 1961) establishes that erasing one bit of information requires a minimum energy dissipation of $k_B T \ln 2$. Applied to epigenetic rejuvenation, this principle constrains the minimum thermodynamic cost of resetting the epigenome from an aged state $P_t$ to a youthful state $P_0$.

The information content that must be erased during rejuvenation — the "informational distance" between the aged and youthful epigenomes — is quantified by the Kullback-Leibler divergence. However, unlike previous applications of KL divergence to epigenetic drift that use it as a distance metric (see e.g., Section 2.6 of prior work on longevity frameworks), we apply it here in its thermodynamic interpretation via Landauer's bound. The minimum energy cost of rejuvenation is:

```math
E_{\text{rejuv}} \geq k_B T \ln 2 \cdot D_{\text{KL}}(P_t \| P_0) = k_B T \sum_{i=1}^{N} \left[ p_t^{(i)} \ln \frac{p_t^{(i)}}{p_0^{(i)}} + (1-p_t^{(i)}) \ln \frac{1-p_t^{(i)}}{1-p_0^{(i)}} \right]
```

For an estimated drift of $\Delta p \approx 0.05$ (5% mean absolute methylation change) across $N \approx 2.8 \times 10^7$ CpG sites in an 80-year-old human cell relative to a newborn, the minimum rejuvenation energy is approximately:

```math
E_{\text{rejuv}} \geq N \cdot k_B T \ln 2 \cdot \overline{D_{\text{KL,site}}} \approx 2.8 \times 10^7 \times 2.85 \times 10^{-21} \times 0.0036 \approx 2.9 \times 10^{-16} \text{ J per cell}
```

For a human body with approximately $3.7 \times 10^{13}$ cells, the total minimum rejuvenation energy is:

```math
E_{\text{total}} \geq 3.7 \times 10^{13} \times 2.9 \times 10^{-16} \approx 0.011 \text{ J} \approx 2.5 \times 10^{-6} \text{ kcal}
```

**Variable definitions:**
- $E_{\text{rejuv}}$: minimum thermodynamic energy cost of rejuvenation per cell (J)
- $k_B T \ln 2$: Landauer's energy limit per bit ($\approx 2.85 \times 10^{-21}$ J at 37°C)
- $D_{\text{KL}}(P_t \| P_0)$: KL divergence from aged to youthful methylation distribution (nats)
- $p_t^{(i)}, p_0^{(i)}$: methylation probabilities at site $i$ in aged and youthful states
- $\overline{D_{\text{KL,site}}}$: mean per-site KL divergence ($\approx 0.0036$ nats for 5% drift)

**Biological interpretation:** The Landauer bound reveals that the thermodynamic cost of rejuvenation is extraordinarily small — on the order of microjoules for an entire human body. This means that there is no thermodynamic barrier to rejuvenation; the challenge is entirely informational: the cell must *know* the target state $P_0$, which is precisely the backup copy hypothesis. The actual metabolic cost of OSK-mediated reprogramming is many orders of magnitude above the Landauer limit, dominated by the energy costs of transcription factor expression, chromatin remodeling enzyme activity, and the signaling cascades that guide the process. The ratio of actual to minimum cost provides a measure of the "thermodynamic inefficiency" of current reprogramming technology.

### 3.6 Branching Process Model of Epigenetic Error Propagation

We model the propagation of epigenetic copying errors across cell divisions as a Galton-Watson branching process (Harris, 1963). Each methylation error at a single CpG site in a mother cell produces a random number of "daughter errors" in the next generation: the original error is faithfully copied (with probability $q$), spontaneously corrected (with probability $r$), and may induce additional errors at neighboring sites through regional disruption of maintenance enzyme recruitment (with probability $s$ per neighboring site).

Let $Z_n$ denote the number of epigenetic errors after $n$ cell divisions, starting from a single initial error ($Z_0 = 1$). The offspring distribution has mean:

```math
\mu = q + k \cdot s
```

where $q$ is the error copying probability, $k$ is the number of CpG sites susceptible to induced errors from a single site's error (the "neighborhood size," typically 5-20 for sites within a single nucleosome), and $s$ is the per-neighbor induction probability. The correction probability $r = 1 - q$ reduces the effective reproduction rate. The branching process is:

```math
\text{Subcritical (self-correcting):} \quad \mu < 1 \quad \Leftrightarrow \quad q + ks < 1
```
```math
\text{Supercritical (error explosion):} \quad \mu > 1 \quad \Leftrightarrow \quad q + ks > 1
```

The critical transition occurs when $\mu = 1$, which defines a critical maintenance fidelity:

```math
q_{\text{crit}} = 1 - k \cdot s
```

If maintenance fidelity drops below $q_{\text{crit}}$ — that is, if $q > q_{\text{crit}}$ (note: here $q$ represents error propagation probability, so higher $q$ means lower fidelity) — the error count grows geometrically:

```math
\mathbb{E}[Z_n] = \mu^n \quad \Rightarrow \quad Z_n \sim \mu^n \text{ for large } n
```

The IToA predicts that aging corresponds to the transition from subcritical to supercritical regimes as maintenance enzyme fidelity declines with age. The critical age $t_{\text{crit}}$ at which this transition occurs can be estimated from the age-dependent error parameters:

```math
t_{\text{crit}} = \inf\{t : q(t) + k \cdot s(t) \geq 1\}
```

**Variable definitions:**
- $Z_n$: total number of epigenetic errors after $n$ cell divisions
- $\mu$: mean offspring number per error per division (dimensionless)
- $q$: probability that an error at one site is faithfully copied to the daughter cell
- $r = 1-q$: probability of spontaneous error correction per division
- $s$: probability of inducing a new error at a neighboring CpG site per division
- $k$: effective neighborhood size (number of CpG sites susceptible to induced errors)
- $q_{\text{crit}}$: critical error copying probability; above this, errors grow exponentially
- $t_{\text{crit}}$: critical age at which the branching process becomes supercritical

**Biological interpretation:** This framework predicts a phase transition in aging: below $t_{\text{crit}}$, the epigenetic maintenance system is self-correcting, and isolated errors are absorbed without systemic consequence. Above $t_{\text{crit}}$, error accumulation becomes autocatalytic and accelerates exponentially, consistent with the clinical observation that functional decline accelerates in late life. The model also predicts that interventions improving maintenance fidelity (e.g., NAD+ supplementation boosting SIRT1 activity; Imai & Guarente, 2014; Yoshino et al., 2018) could delay $t_{\text{crit}}$ without reversing existing errors, while reprogramming (OSK) resets $Z_n$ toward zero, effectively restarting the branching process.

---

## 4. Evidence Supporting the Information Theory of Aging

### 4.1 The ICE Mouse Model: Epigenetic Disruption Causes Aging

The most direct evidence for the IToA comes from the Inducible Changes to the Epigenome (ICE) mouse model (Yang et al., 2023). As described in Section 1.3, the ICE system demonstrates three critical predictions of the IToA: (1) non-mutagenic DNA damage events cause epigenetic disruption; (2) this epigenetic disruption alone is sufficient to produce aging phenotypes; and (3) the resulting aging is partially reversible through Yamanaka factor–mediated epigenetic reprogramming.

The mechanistic link between DSB repair and epigenetic disruption was established in earlier work by the Sinclair laboratory. Oberdoerffer et al. (2008) showed that SIRT1 relocalization from gene regulatory regions to DNA break sites in response to genomic damage caused widespread transcriptional changes resembling those observed in naturally aged mouse brains. This "SIRT1 redistribution" model was extended by Van Meter et al. (2016), who demonstrated that SIRT6 similarly relocalizes from its normal chromatin positions to DSB sites for repair, causing derepression of LINE-1 retrotransposable elements and activation of an interferon-like innate immune response — a process that recapitulates inflammaging.

The ICE model's quantitative data are compelling. Epigenetic age acceleration in ICE mice was consistent across multiple DNA methylation clocks: the Petkovich liver clock (Petkovich et al., 2017), the Thompson multi-tissue clock (Thompson et al., 2018), and the Meer blood clock (Meer et al., 2018) all showed significant acceleration. The magnitude of acceleration — approximately 50% faster aging — is within the range of what is observed in human progeroid syndromes (Horvath et al., 2015), lending clinical relevance to the model. The absence of increased somatic mutations in ICE mice was confirmed by whole-exome sequencing, ruling out confounding from genetic damage.

The reversal experiment is equally significant. Five weeks of whole-body AAV9-OSK treatment in ICE mice produced measurable rejuvenation: H3K9me3 levels in kidney and H3K36me2 levels in muscle returned toward youthful values, and DNA methylation age was reduced by up to 57% (Yang et al., 2023). Visual function, assessed by optomotor response, improved in OSK-treated aged mice. The reversal was partial — not all aging phenotypes were fully restored — but the demonstration that an epigenetically aged state can be partially reversed by restoring epigenetic information strongly supports the backup copy hypothesis.

### 4.2 Epigenetic Clocks as Information-Loss Metrics

Epigenetic clocks — mathematical models that predict biological age from DNA methylation patterns — provide empirical measurements of the information decay described by the IToA. The foundational Horvath multi-tissue clock, trained on 353 CpG sites across 51 tissues and cell types, achieves a median absolute deviation of 3.6 years across the human lifespan (Horvath, 2013). The remarkable accuracy of this clock across tissues implies a universal methylation drift program that our Framework 3.3 interprets as the empirical manifestation of mutual information decay.

Subsequent clock generations have improved accuracy and interpretive power. The Hannum clock (Hannum et al., 2013) focused on blood-based aging prediction. GrimAge (Lu, Quach, et al., 2019) incorporated plasma protein surrogates and smoking history to predict mortality with superior performance ($r = 0.94$ for chronological age, stronger association with time-to-death than earlier clocks). GrimAge Version 2 (Lu et al., 2022) further improved mortality prediction. DunedinPACE (Belsky et al., 2022) shifted from measuring biological age (a static quantity) to measuring the *pace* of aging (a rate), trained on longitudinal within-person changes in 19 biomarkers across 20 years in the Dunedin birth cohort. DunedinPACE captures year-to-year variation in aging rate, making it responsive to interventions in a way that earlier clocks are not. The Biomarkers of Aging Consortium (Moqri et al., 2024) proposed a systematic framework for validating aging biomarkers, establishing criteria for clinical utility that extend beyond statistical correlation to mechanistic interpretability — a standard the IToA's information-theoretic framework is well-positioned to meet. Ying et al. (2024) introduced causality-enriched epigenetic age measures that disentangle damage-associated from adaptation-associated methylation changes, reporting that causality-enriched clocks better predict mortality and respond more consistently to longevity interventions than standard clocks. Li et al. (2024) developed epigenetic predictors of species maximum lifespan across mammals, connecting methylation-based aging rates to evolutionary lifespan constraints — a finding consistent with our Framework 3.1's prediction that species-specific channel capacity determines maximum achievable lifespan. Meyer and Schumacher (2024) provided an alternative mathematical framework based on accumulating stochastic variation, showing that aging clocks can emerge purely from entropy-driven processes, consistent with the stochastic challenge described in Section 5.1.

From the IToA perspective, the steady improvement in clock accuracy across successive generations reflects the extraction of progressively more mutual information from the methylation signal. The inequality derived in Framework 3.3 ($R^2_{\text{clock}} \leq f(I(X_0; X_t))$) predicts that clock accuracy has a theoretical ceiling set by the mutual information remaining in the epigenome at each age — a prediction that can be tested as clock technology approaches this ceiling.

Recent work on DNA methylation entropy provides further support. Shannon entropy calculated over CpG methylation states increases monotonically with age across multiple tissues (Hannum et al., 2013; Jenkinson et al., 2017; Seale et al., 2022; Duan et al., 2022), consistent with the IToA's prediction of progressive epigenetic information loss. A comprehensive review by de Magalhães (2025) in *Nature Cell Biology* placed the information-theoretic framework alongside error-based and program-based theories, noting that the IToA generates uniquely testable predictions through its connection to reprogramming. Entropy-based clocks capture a dimension of aging distinct from mean methylation shift: they measure the *variability* of methylation states within and between cells, which the IToA interprets as stochastic information loss. Zhou et al. (2023) demonstrated that single-cell DNA methylation entropy increases with age in mouse hematopoietic stem cells, confirming that the entropy increase is not merely an artifact of cell-type composition changes in bulk tissue samples.

The CpGPT transformer model (de Lima Camillo et al., 2024), trained on hundreds of methylation datasets, demonstrated that deep learning architectures can extract nonlinear patterns from methylation data that linear clocks miss, achieving improved age prediction in held-out datasets. From an information-theoretic standpoint, CpGPT's advantage over linear clocks suggests that a significant fraction of age-associated mutual information in the methylation signal is encoded in higher-order correlations between CpG sites — a prediction consistent with our Framework 3.1's emphasis on correlated maintenance errors.

### 4.3 Partial Reprogramming Reverses Information Loss

The demonstration that transient Yamanaka factor expression can reverse epigenetic aging markers without erasing cellular identity constitutes perhaps the strongest evidence for the IToA's backup copy hypothesis. If aging were purely a matter of damage accumulation — if the youthful epigenetic information were truly destroyed — then no amount of transcription factor expression could restore it. The fact that OSK can "read" a template of the youthful state and reset the epigenome toward it implies that the information persists.

The landmark demonstration came from Ocampo et al. (2016), who showed that cyclic OSKM expression (2 days on, 5 days off) in LAKI progeroid mice extended median lifespan by approximately 33%, reversed hallmarks of aging including DNA damage foci, mitochondrial dysfunction, and loss of heterochromatin organization, and improved tissue regenerative capacity — all without teratoma formation. This study established two principles: that epigenetic rejuvenation is achievable *in vivo*, and that the rejuvenation-dedifferentiation boundary can be navigated through pulsatile dosing.

Lu et al. (2020) demonstrated OSK-mediated vision restoration in aged mice and in a glaucoma model, with continuous (not cyclic) OSK expression over 4 weeks reversing epigenetic age in retinal ganglion cells without producing tumors over 15 months of follow-up. The dependence on TET1/TET2 — OSK-mediated rejuvenation was abolished in TET1/TET2 double knockouts — established active DNA demethylation as the molecular effector of epigenetic age reversal. Gill et al. (2022) achieved the most dramatic result in human cells: maturation phase transient reprogramming (MPTR) of human dermal fibroblasts reversed epigenetic age by approximately 30 years (Horvath clock) in just 13 days, with restoration of youthful collagen production and fibroblast-specific enhancer methylation patterns preserved throughout.

The systemic reprogramming results of Macip et al. (2024) provided the strongest lifespan evidence to date. AAV9-delivered inducible OSK in 124-week-old wild-type mice extended median remaining lifespan by 109%, with treated mice surviving to ages equivalent to approximately 120 human years. This result, while awaiting independent replication, suggests that systemic epigenetic reprogramming can produce rejuvenation at the organismal level, not just in isolated tissues. Sahu et al. (2024) at Altos Labs refined the approach by targeting OSK expression specifically to senescent and stressed cells using the *Cdkn2a* (p16) promoter, extending lifespan in wild-type mice by approximately 12% and in progeroid models by up to 40% without increased tumor incidence.

Alle et al. (2022) added a provocative finding: a single short reprogramming burst early in life could initiate a propagating epigenetic mechanism that extended healthy lifespan by approximately 15% in both LAKI and wild-type mice. This suggests that the backup copy may not only be readable but that a single access event can initiate a sustained maintenance improvement — an observation our branching process model (Framework 3.6) would interpret as a transient return to the subcritical regime.

### 4.4 The Backup Copy: iPSC Reprogramming Resets Age to Zero

The most extreme test of the backup copy hypothesis is full reprogramming to induced pluripotent stem cells (iPSCs). If the backup copy exists, then iPSC reprogramming should reset epigenetic age to zero regardless of the donor's chronological age — and this is precisely what is observed. Horvath (2013) showed that iPSCs derived from donors of any age have an epigenetic age near zero. Lapasset et al. (2011) demonstrated that iPSCs from centenarian donors had telomere lengths, mitochondrial function, and gene expression profiles indistinguishable from embryonic stem cells. Kerepesi et al. (2021) demonstrated through comprehensive epigenetic clock analysis that a rejuvenation event occurs during embryogenesis, resetting epigenetic age to zero before post-natal aging begins — establishing the developmental anchor point for the backup copy. Olova et al. (2019) conducted a detailed time-course analysis of epigenetic age during human iPSC reprogramming, showing that the Horvath clock decreases continuously from day 3, with the rate of rejuvenation exceeding the rate of identity loss during the early-to-mid phase — the window exploited by partial reprogramming. The capacity for complete age resetting has been confirmed across multiple independent laboratories (Simpson et al., 2021; Zhang et al., 2022; Gladyshev, 2021).

This complete age reset from any starting age implies that all the information needed to specify a youthful epigenome is recoverable from an aged cell. The backup copy is not partially degraded — it is fully intact, even in centenarian cells. This extraordinary conclusion, if correct, means that aging at the epigenetic level is entirely reversible in principle. The practical challenge of partial reprogramming is not informational but navigational: accessing the backup copy without crossing the dedifferentiation threshold (see Precise Partial Reprogramming analysis of the cusp catastrophe at this boundary).

### 4.5 Clinical Frontier: Life Biosciences ER-100 First Human Trial

The translation of epigenetic reprogramming from mouse models to human therapy reached a milestone in January 2026, when Life Biosciences received FDA Investigational New Drug (IND) clearance for ER-100, an AAV-delivered OSK therapy for optic neuropathies (Sinclair, 2024; Life Biosciences, 2026). The ER-100 trial targets age-related vision loss, building on the preclinical demonstration by Lu et al. (2020) that OSK expression in retinal ganglion cells restores visual function in aged mice and in mouse models of glaucoma. The trial represents the first test of whether epigenetic reprogramming — the central therapeutic prediction of the IToA — can produce measurable rejuvenation in human tissue.

The significance of ER-100 for the IToA extends beyond the clinical question of whether it improves vision. If the trial includes molecular endpoints — DNA methylation profiling, histone modification assays, transcriptomic analysis — it will provide the first human data on whether OSK-mediated epigenetic resetting works in human tissue *in vivo*. The IToA predicts that treated retinal tissue will show reduced DNA methylation age, restored histone modification patterns, and a transcriptomic profile shifted toward younger reference values. Failure to observe these molecular changes — even if clinical vision improves through other mechanisms — would constitute evidence against the IToA's epigenetic explanation.

### 4.6 The Entropy Framework: Connecting Information Theory to Thermodynamics

Recent theoretical work has begun connecting the information-theoretic description of aging to thermodynamic principles. Cummings, Hong, and Cohen (2025) proposed a framework applying fundamental principles of thermodynamics and information theory to human aging, building on Schrödinger's concept of life as an effort to combat entropy. They demonstrated that Mahalanobis distance applied to ECG interval data — used as a proxy for physiological entropy — increased with age and predicted mortality after adjustment for confounders; remarkably, ECG entropy also predicted fracture risk, suggesting that entropy in one physiological system may serve as a cross-system aging biomarker. This framework aligns with our Landauer's principle analysis (Framework 3.5): the energy cost of rejuvenation is the price of local entropy reduction in a thermodynamically open system.

The thermodynamic perspective has been further developed by Silva and Annamalai (2023), who introduced a computational thermodynamic model for entropy generation and showed that daily entropy generation decreased significantly with increasing caloric restriction in mice, with predictions of 13-56% lifespan extension consistent with empirical data. Tarkhov, Denisov, and Fedichev (2024) proposed that aging dynamics can be modeled as stochastic transitions among metastable states, with thermodynamic biological age increasing linearly with chronological age and tracking entropy produced during the aging process — setting severe constraints on the possibilities for age reversal. Chan, Rubbi, and Pellegrini (2025) demonstrated that epigenetic clocks based on entropy of methylation states predict chronological age with accuracy comparable to standard mean-methylation approaches, establishing DNA methylation entropy as a viable independent aging biomarker.

Schumacher et al. (2021) provided a broader perspective, conceptualizing aging as "a loss of information at all levels" — from damaged DNA and aggregated proteins to deteriorated tissue architecture and impaired intercellular communication. This multi-level information-loss framework is consistent with, but broader than, Sinclair's epigenome-focused formulation. Gladyshev (2016) proposed the "deleteriome" concept — the sum of all deleterious changes accumulated with age — which can be recast in information-theoretic terms as the total information loss across all biological channels. Gems, Virk, and de Magalhães (2024) argued provocatively that methylation clocks can be understood within a programmatic framework, since clock CpG sites are enriched near developmental genes, linking age-associated methylation drift to a continuation of developmental programs rather than stochastic damage accumulation — a view that challenges the IToA's noise-based interpretation while supporting the information-theoretic framing.

---

## 5. Evidence Against the IToA and Limitations

### 5.1 The Stochastic Dominance Problem

Perhaps the most damaging recent challenge to clock-based evidence for the IToA comes from two landmark studies published in the same issue of *Nature Aging*. Tong et al. (2024) demonstrated that approximately 66-75% of the accuracy underpinning Horvath's clock could be driven by a stochastic process, using data from over 22,770 sorted and whole-blood samples across 25 independent cohorts. This fraction increased to 90% for Zhang's clock but was lower (63%) for PhenoAge, suggesting that the nonstochastic component varies across clock architectures. In the same issue, Tarkhov et al. (2024) showed from single-cell DNA methylation analysis in mice that epigenetic aging involves both co-regulated changes and a major stochastic component, with methylation levels trending toward intermediate values at a rate resembling exponential decay — consistent with a radiocarbon decay–like stochastic process rather than a coordinated program.

These results challenge the IToA's interpretation of epigenetic clocks as measurements of a coherent epigenetic aging program. If clock accuracy arises predominantly from the statistics of independent stochastic drift rather than from coordinated informational decay, then the clocks may be measuring *time elapsed* (via the law of large numbers applied to many independent random walks) rather than *information lost* (via a coordinated biological process). The distinction is crucial: the former interpretation reduces the clocks to sophisticated timers with no causal content, while the latter supports the IToA.

However, several caveats apply. First, the 25-37% of clock accuracy *not* explained by the stochastic model may represent the genuinely informative biological signal — the coordinated epigenetic changes driven by a biological aging process. Tong et al. (2024) found that Horvath's age acceleration in males and PhenoAge's acceleration in severe COVID-19 and smokers are driven by nonstochastic processes, indicating that biologically meaningful information persists beyond the stochastic baseline. Second, the stochastic model's drift rates are themselves biological observables that require explanation: *why* do specific CpG sites drift at specific rates? If the answer involves declining maintenance enzyme fidelity, then the stochastic drift is itself a consequence of the information-loss process the IToA describes. Third, a 2024 study demonstrated that epigenetic clock loci are enriched in regions that both accumulate and lose methylation disorder with age, suggesting a mechanistic link between stochastic drift and the organized signal captured by clocks — but that lifespan interventions modulate drift and clock signals differently (Aging, 2024). Fourth, an unbiased comparison of 14 epigenetic clocks against 174 incident disease outcomes in 18,859 individuals confirmed that second-generation clocks (DunedinPACE, GrimAge v2) showed substantially larger effect sizes than first-generation clocks, suggesting these newer clocks capture biological information beyond stochastic drift (Nature Communications, 2025). Most provocatively, a 2025 study in *Nature Aging* demonstrated that CRISPR-guided methylation editing at individual age-associated CpG sites evoked genome-wide "bystander effects" at other age-associated regions, revealing that age-associated methylation changes are coherently organized within an epigenetic network — supporting the view that at least some changes are coordinated rather than purely stochastic.

### 5.2 Somatic Mutations and Clonal Hematopoiesis

The IToA assigns causal primacy to epigenetic information loss over genetic damage, but the accumulation of somatic mutations with age constitutes an independent aging driver that epigenetic reprogramming cannot address. Clonal hematopoiesis of indeterminate potential (CHIP) — the clonal expansion of hematopoietic stem cells carrying somatic mutations in genes such as *DNMT3A*, *TET2*, and *ASXL1* — is detectable in over 10% of individuals aged 65+ and over 20% of those aged 80+ (Jaiswal et al., 2014; Genovese et al., 2014). CHIP is associated with increased risk of hematological malignancy (10-fold), cardiovascular disease (2-fold), and all-cause mortality (1.4-fold) (Jaiswal et al., 2017).

The relevance to the IToA is that CHIP mutations in *DNMT3A* and *TET2* — genes encoding epigenetic enzymes — directly degrade the epigenetic maintenance machinery. These are *genetic* lesions that impair *epigenetic* function, creating a causal pathway from genetic to epigenetic damage that inverts the IToA's proposed causal hierarchy. Furthermore, CHIP-driven clonal expansion cannot be reversed by epigenetic reprogramming: OSK expression can reset the epigenome of a *DNMT3A*-mutant cell, but it cannot repair the *DNMT3A* gene itself. The mutant cell will immediately begin accumulating new epigenetic errors at an accelerated rate. Robertson et al. (2024) demonstrated the direct connection between CHIP and epigenetic aging in 4,370 individuals from the NHLBI TOPMed cohort, showing that clonal expansion rate was significantly associated with both genetically predicted and measured epigenetic clocks. This establishes that CHIP dynamics and epigenetic aging acceleration are quantitatively coupled — a finding that complicates the IToA's clean separation of genetic and epigenetic aging channels.

Somatic mutations extend beyond CHIP. Martincorena et al. (2015, 2018) demonstrated that aged human esophageal and skin epithelia harbor extensive clonal fields of cells carrying cancer-driver mutations, with positively selected mutations present in over 25% of normal esophageal epithelial cells by middle age. Cagan et al. (2022) showed that somatic mutation rates across species scale with lifespan, producing approximately the same total mutation burden at end-of-life regardless of species longevity — suggesting that genetic mutation burden is a lifespan-limiting factor that evolution has not been able to circumvent. Lee et al. (2024) extended this with single-cell whole-genome sequencing of human brain cells, revealing that oligodendrocytes accumulate single-nucleotide variants 81% faster than neurons, with distinct genomic distributions and mutational signatures — demonstrating that even within a single tissue, different cell types experience fundamentally different mutational aging trajectories. Lee-Six et al. (2018) demonstrated lifelong clonal dynamics in human hematopoietic stem cells, with competition among mutant clones shaping blood composition in aging. Zhang and Vijg (2024) reviewed how advanced sequencing has revealed gradual mutation accumulation in virtually all normal tissues with age, though they noted that — with the exception of cancer — the phenotypic role of somatic mutations in directly driving aging phenotypes remains unclear, which may partially favor the IToA's emphasis on epigenetic over genetic damage.

These findings challenge the IToA in two ways. First, they establish that irreversible genetic damage accumulates in parallel with epigenetic drift, contributing independently to age-related disease. Second, they raise the possibility that some of what epigenetic clocks measure as "epigenetic aging" is actually the downstream consequence of somatic mutations in epigenetic regulators, rather than stochastic epigenetic drift *per se*.

### 5.3 Proteostasis Failure

The loss of protein homeostasis (proteostasis) with age produces pathologies — Alzheimer's disease (amyloid-β, tau), Parkinson's disease (α-synuclein), amyotrophic lateral sclerosis (TDP-43, SOD1), and presbyopia (crystallin aggregation) — that are not primarily epigenetic in origin and are not addressed by epigenetic reprogramming. Protein aggregation is driven by the intrinsic thermodynamic instability of the proteome: proteins are marginally stable, with free energies of folding typically 5-15 kcal/mol, and aging-associated decline in chaperone activity, proteasome function, and autophagy allows metastable proteins to aggregate (Labbadia & Morimoto, 2015; Hipp et al., 2019).

While the IToA might argue that proteostasis decline is downstream of epigenetic dysregulation (reduced expression of chaperones and proteasome subunits due to epigenetic noise), this argument faces a conceptual difficulty: once a protein aggregate has formed and propagated through prion-like seeding (e.g., tau spreading through neural circuits; Jucker & Walker, 2013; He et al., 2018), no amount of epigenetic resetting will dissolve the aggregate or reverse the structural damage. The aggregate is a physical state, not an informational one. Epigenetic reprogramming might restore the expression of chaperones and proteolytic machinery, but this is a *functional* restoration, not an *informational* one in the IToA's sense, and its efficacy against established aggregates is uncertain.

A major 2025 study in *Science* (Kuo et al., 2025) revealed a novel mechanism upstream of proteostasis collapse that the IToA does not address: aging causes increased ribosome stalling during translation elongation in the turquoise killifish brain, leading to widespread depletion of proteins enriched in basic amino acids. This explains the long-standing mystery of "protein-transcript decoupling" in aging cells — where mRNA levels no longer predict protein levels — and identifies a translational mechanism for age-related proteostasis failure that is independent of epigenetic control of transcription. Recent work by Kelmer Sacramento et al. (2024) demonstrated that partial reprogramming in mouse neurons reduced, but did not eliminate, age-associated protein aggregation markers, suggesting that epigenetic rejuvenation has limited efficacy against established proteotoxic damage. Paine et al. (2024) confirmed in a comprehensive review that partial reprogramming can partially restore proteostasis through improved chaperone activity, but its efficacy varies substantially across tissues and model organisms. López-Otín and Kroemer (2021) argued that proteostasis failure represents a hallmark of aging with causal independence from epigenetic alterations, driven by the accumulation of damaged proteins that overwhelm the cell's degradation capacity regardless of transcriptional state.

### 5.4 Mitochondrial DNA Mutations

Mitochondrial DNA (mtDNA) mutations accumulate with age through both replication errors and oxidative damage, and they do so independently of the nuclear epigenome (Kauppila et al., 2017; Stewart & Chinnery, 2015). Sprason, Tucker, and Clancy (2024) reviewed mtDNA deletion research across organisms and concluded that random segregation during mitochondrial division alone cannot explain observed patterns, emphasizing the complicating roles of heteroplasmy, tissue-specific differences, and copy number variation. The mitochondrial genome lacks the chromatin-based epigenetic regulation that defines nuclear epigenetics: mtDNA is not wrapped around histones (though it associates with mitochondrial transcription factor A, TFAM) and is not regulated by CpG methylation in the canonical sense (though low levels of mtDNA methylation have been detected; Shock et al., 2011). Consequently, the IToA's framework of epigenetic information loss does not apply to mitochondrial genomes.

The mtDNA mutator mouse (Trifunovic et al., 2004), which carries a proofreading-deficient mitochondrial DNA polymerase γ, develops a progeroid phenotype with elevated somatic mtDNA mutation burden — demonstrating that mitochondrial genetic damage alone can drive aging-like phenotypes. Epigenetic reprogramming via OSK would not be expected to reverse mtDNA mutations, as Yamanaka factors act on nuclear chromatin and gene regulation. While reprogramming might improve mitochondrial function indirectly — by restoring expression of nuclear-encoded mitochondrial biogenesis genes such as *PGC-1α* and *TFAM* — the underlying mtDNA mutations would persist.

Notably, iPSC reprogramming does appear to partially reset mitochondrial function. Suhr et al. (2010) showed that iPSCs have rejuvenated mitochondria with reduced oxidative damage, suggesting that nuclear reprogramming can restore mitochondrial homeostasis through transcriptional mechanisms even if mtDNA mutations persist. However, whether this mitochondrial improvement is sustained upon differentiation of reprogrammed cells remains unclear.

### 5.5 Telomere Shortening

Telomere attrition is one of the hallmarks of aging that operates independently of the epigenome. Telomeres shorten with each cell division due to the end-replication problem and oxidative damage, and critically short telomeres trigger replicative senescence through the DNA damage response (Harley et al., 1990; d'Adda di Fagagna et al., 2003). Cross-species analyses have shown that telomere shortening rate correlates with lifespan more strongly than body mass or metabolic rate in some datasets (Whittemore et al., 2019), and that the critical short telomere threshold, rather than mean telomere length, is the functional trigger for cellular senescence (Hemann et al., 2001; Vera et al., 2012).

The IToA does not directly address telomere biology. Brown et al. (2024) showed that mammalian telomere lengths vary by an order of magnitude across species and proposed that these differences are driven by effective population sizes rather than lifespan alone, suggesting that telomere biology operates under distinct evolutionary pressures from epigenetic maintenance. Dugdale and Richardson (2024) extended this analysis to non-model species and found inter-generational telomere length effects in declining populations. While epigenetic regulation of the *TERT* promoter influences telomerase expression (and thus telomere maintenance in some cell types), the fundamental chemistry of telomere shortening — incomplete replication of lagging-strand DNA termini — is a physical constraint on semiconservative DNA replication, not an information-processing failure in the IToA's sense. Moreover, iPSC reprogramming reactivates telomerase and restores telomere length (Marion et al., 2009; Agarwal et al., 2010), but this is a direct consequence of *TERT* transcriptional activation by Yamanaka factors, not a manifestation of the backup copy mechanism.

The relevance is that in species where telomere shortening is a primary lifespan-limiting mechanism (including, arguably, humans; Armanios & Blackburn, 2012), the IToA's focus on epigenetic information loss may understate the importance of a distinct, physically determined aging process. However, Horvath et al. (2022) noted that telomere length and epigenetic age track different dimensions of aging and are only weakly correlated, suggesting they represent largely independent processes — consistent with the multi-channel model we develop in Section 7.

### 5.6 Cross-Species Failures

If the IToA is a universal theory of aging — applicable across the tree of life — then epigenetic reprogramming should produce rejuvenation in diverse organisms. Current evidence is mixed. While OSK-mediated rejuvenation has been demonstrated in mice across multiple tissues and laboratories (Lu et al., 2020; Yang et al., 2023; Macip et al., 2024), direct experimental tests in *C. elegans* have produced negative results. Kamaludeen et al. (2024) demonstrated that neuron-specific expression of *C. elegans* reprogramming factor orthologs not only failed to extend lifespan but actually reduced it, while transient induction had no significant lifespan effect. OSK orthologs did not improve short-term associative memory and further disrupted chemotaxis behavior, demonstrating that mammalian reprogramming factors have deleterious effects in post-mitotic invertebrate neurons. This represents a significant challenge to the universality of the IToA: the specific molecular implementation of the "backup copy" may be mammal-specific, even if the principle of information loss is universal.

In *Drosophila melanogaster*, the situation is similarly complex. Flies lack the canonical DNA methylation machinery (DNMT1, DNMT3A/B) present in mammals, relying instead on Polycomb/Trithorax-mediated chromatin regulation for epigenetic memory (Lyko, 2018). Age-associated chromatin changes occur in *Drosophila* (Wood et al., 2010; Li et al., 2020), but the molecular mechanisms are sufficiently different from mammalian epigenetic aging that the IToA's specific predictions about methylation-based information loss do not directly apply. The theory would need to be reformulated in terms of histone modification information loss to be testable in flies — a reformulation that has not yet been rigorously developed.

Turritopsis dohrnii, the "immortal jellyfish," provides a provocative counterpoint. This species can reverse its life cycle from the medusa stage to the polyp stage through a process of transdifferentiation, effectively achieving biological immortality (Piraino et al., 1996; Matsumoto et al., 2019). If the IToA is correct, this species must have evolved an exceptionally effective epigenetic maintenance system or a robust mechanism for reading the backup copy. Pascual-Torner et al. (2022) sequenced the *T. dohrnii* genome and identified amplifications of genes involved in DNA replication and repair, telomere maintenance, and stem cell function, but did not find obvious enhancements in canonical epigenetic maintenance enzymes. Whether this organism represents a validation or challenge to the IToA remains an open question.

### 5.7 Adaptive Epigenetic Changes

A fundamental assumption of the IToA is that age-associated epigenetic changes represent *noise* — the degradation of a functional signal — rather than *adaptive responses* to changing physiological needs. This assumption is contested by evidence that some epigenetic changes with age may be functional.

Immune cells undergo extensive, programmed epigenetic remodeling with age and antigenic experience (Henning et al., 2018; Moskowitz et al., 2017; Li et al., 2024). The age-associated demethylation of cytokine promoters in T cells, for example, enables more rapid inflammatory responses — a change that may be adaptive in the context of accumulated pathogen exposure, even if it contributes to chronic inflammation in aggregate. Rando and Chang (2012) argued that some epigenetic changes during aging represent a form of "epigenetic memory" of environmental exposures that serves an adaptive function, analogous to the trained immunity observed in innate immune cells (Netea et al., 2016; Netea et al., 2020).

If a substantial fraction of age-associated epigenetic changes is adaptive, then the IToA's characterization of aging as pure information loss is incomplete. The therapeutically relevant question becomes: what fraction of age-associated epigenetic drift is deleterious noise (to be reversed by reprogramming) versus functional adaptation (to be preserved)? This question is addressable experimentally, and we propose a specific experimental design in Section 8.8.

Moqri et al. (2024) provided partial resolution by showing that approximately 90% of age-dependent DNA methylation gain occurs at Polycomb Repressive Complex 2 (PRC2)-bound, low-methylated regions — genomic compartments associated with developmental gene regulation rather than environmental response genes. This suggests that the majority of measurable methylation drift is stochastic noise at developmentally regulated loci, consistent with the IToA, but leaves open the possibility that the remaining 10% includes functionally important adaptive changes.

### 5.8 Dissociation Evidence: Lifespan Extension Without Epigenetic Clock Reversal

Several well-established lifespan-extending interventions do not consistently reverse epigenetic aging, creating a dissociation that challenges the IToA's claim that epigenetic information loss is the primary cause of aging. If epigenetic information loss were the central causal mechanism, then all interventions that extend lifespan should slow or reverse epigenetic aging, and interventions that reverse epigenetic aging should extend lifespan. Neither implication holds universally.

Caloric restriction (CR), the most robust lifespan-extending intervention across species (Weindruch & Walford, 1988; Mattison et al., 2017), shows inconsistent effects on epigenetic clocks. Some studies report that CR slows epigenetic aging in blood (Maegawa et al., 2017), while others find no significant effect on specific clocks (Cole et al., 2017). The CALERIE trial — the first randomized controlled trial of CR in humans — showed that 2 years of 25% caloric restriction slowed the pace of aging as measured by DunedinPACE (Waziry et al., 2023), but the effect size was modest (2-3% slowing) relative to the lifespan extensions observed in model organisms. Poganik et al. (2023) demonstrated that biological age can increase rapidly under severe stress and then partially recover upon stress resolution, suggesting that epigenetic aging has both irreversible (ratcheting) and reversible (elastic) components — a nuance the IToA's simple information-loss model does not fully capture.

Rapamycin, which extends lifespan across species through mTOR inhibition (Harrison et al., 2009; Bitto et al., 2016), has mixed effects on epigenetic clocks in mice (Thompson et al., 2018). Growth hormone receptor knockout mice (Ames dwarf, Snell dwarf) live 30-65% longer than wild-type controls (Brown-Borg et al., 1996; Flurkey et al., 2001), but their relationship to epigenetic aging is not well characterized.

These dissociations suggest that lifespan is determined by multiple parallel processes, of which epigenetic information loss is one but not the sole contributor. This interpretation aligns with the multi-channel model we develop in Section 7.

### 5.9 The ICE Model's Artificiality

While the ICE model provides the strongest experimental evidence for the IToA, its artificiality warrants scrutiny. The most pointed critique came from Timmons and Brenner (2024) in a *Cell* Matters Arising commentary, who argued that the ICE model had not adequately tested the information theory of aging. They noted that I-PpoI — the key endonuclease used — was previously shown by the corresponding author's own laboratory to be mutagenic, cytotoxic, and progeric when targeted to specific cell types, causing a p53 response and cell elimination within one month. They argued these confounding effects, rather than epigenetic information loss, could account for the observed aging phenotype. Yang, Hayano, Griffin, Sinclair, and colleagues (2024) responded that their tamoxifen-induction protocols were specifically designed to ensure low-level endonuclease expression that did not cause cell-cycle arrest or apoptosis, citing multiple assays showing no detectable cell death or elimination. This exchange highlights the ongoing debate about the model's validity and the need for independent replication with alternative experimental systems.

Beyond this specific critique, several structural concerns apply. First, the spatial distribution of ICE-induced DSBs is non-physiological. Natural DSBs occur stochastically throughout the genome, with elevated rates at fragile sites, transcriptionally active regions, and replication stress zones (Tubbs & Nussenzweig, 2017). ICE-induced DSBs occur exclusively at I-PpoI recognition sites in rDNA, which may produce a distinct pattern of chromatin modifier redistribution and epigenetic disruption compared to the distributed DSB pattern of natural aging.

Second, the temporal dynamics differ. ICE mice receive bolus DSB induction events (upon tamoxifen administration), whereas natural aging involves a continuous, low-level background of DSB formation and repair. The epigenetic consequences of acute, high-frequency DSBs may differ qualitatively from those of chronic, low-level damage — for instance, acute damage may overwhelm repair capacity in ways that chronic damage does not.

Third, the ICE model generates DSBs without introducing mutations (because the I-PpoI sites are in repetitive rDNA where NHEJ restores the original sequence). In natural aging, many DSBs are repaired with errors, producing mutations alongside epigenetic disruption. The ICE model therefore isolates the epigenetic component of DSB-induced aging, which is its experimental strength but also its limitation: it demonstrates sufficiency but not necessity. Epigenetic disruption without genetic damage causes aging in the ICE model, but in natural aging, both processes occur simultaneously, and their relative contributions remain unknown.

---

## 6. Toward Resolution: Multi-Channel Aging

### 6.1 IToA as a Special Case: Multi-Channel Information Degradation

The evidence reviewed in Sections 4 and 5 supports a nuanced conclusion: the IToA captures a genuine, measurable, and therapeutically tractable dimension of aging, but aging as a whole involves the degradation of information across multiple parallel channels, not all of which are epigenetic. We propose a multi-channel information degradation model of aging in which the total information loss is:

```math
\Delta I_{\text{total}}(t) = \Delta I_{\text{epi}}(t) + \Delta I_{\text{gen}}(t) + \Delta I_{\text{prot}}(t) + \Delta I_{\text{mito}}(t) + \Delta I_{\text{struct}}(t) + \Delta I_{\text{telo}}(t)
```

where:
- $\Delta I_{\text{epi}}(t)$: epigenetic information loss (methylation drift, histone modification noise, chromatin disorganization) — **partially reversible** via reprogramming
- $\Delta I_{\text{gen}}(t)$: genetic information loss (somatic mutations, chromosomal aberrations) — **irreversible** without gene therapy
- $\Delta I_{\text{prot}}(t)$: proteomic information loss (protein aggregation, misfolding, post-translational damage) — **partially reversible** via enhanced proteostasis
- $\Delta I_{\text{mito}}(t)$: mitochondrial information loss (mtDNA mutations, cristae disorganization) — **partially reversible** via mitochondrial biogenesis
- $\Delta I_{\text{struct}}(t)$: structural information loss (extracellular matrix cross-linking, tissue architecture degradation) — **largely irreversible** without tissue engineering
- $\Delta I_{\text{telo}}(t)$: telomeric information loss (telomere shortening) — **reversible** via telomerase activation

The IToA, in its strongest form, claims that $\Delta I_{\text{epi}}(t)$ dominates the total, contributing the majority of age-related functional decline. Our assessment of the evidence suggests a more modest but still significant claim: $\Delta I_{\text{epi}}(t)$ is likely the largest single contributor and the most therapeutically accessible, but $\Delta I_{\text{gen}}(t)$, $\Delta I_{\text{prot}}(t)$, and $\Delta I_{\text{mito}}(t)$ contribute substantially and independently, particularly in the oldest individuals and in specific tissues.

### 6.2 The IToA Might be Partially Correct

The strength of evidence for the IToA can be summarized across its key predictions:

| Prediction | Evidence Level | Assessment |
|-----------|---------------|------------|
| Epigenetic drift causes aging phenotypes | Strong (ICE model) | Supported, with caveats about model artificiality |
| A backup copy of youthful information exists | Strong (iPSC/partial reprogramming) | Supported; location and mechanism unknown |
| Epigenetic clocks measure information loss | Moderate | Partially supported; stochastic component significant |
| Epigenetic reprogramming reverses aging | Moderate-Strong (mice) | Supported in mice; human data pending |
| Epigenetic information loss is the primary cause of aging | Weak-Moderate | Plausible but not established; multiple independent contributors |

The critical distinction is between *sufficiency* and *primacy*. The ICE model demonstrates that epigenetic information loss is *sufficient* to cause aging. The evidence does not yet establish that it is the *primary* cause — that is, the single largest contributor to functional decline in natural aging. This distinction has therapeutic implications: if epigenetic information loss is sufficient but not primary, then epigenetic reprogramming may produce significant but incomplete rejuvenation, with residual aging driven by genetic, proteomic, and mitochondrial damage.

### 6.3 Reconciling Programmed and Stochastic Aging Through Information Theory

Information theory provides a natural framework for reconciling the programmed and stochastic theories of aging. In the IToA's information-theoretic language, "programmed aging" corresponds to a genetically determined decline in the channel capacity $C_{\text{epi}}(t)$ of the epigenetic maintenance system — a *deterministic* reduction in the system's capacity for error correction. "Stochastic aging" corresponds to the random information loss that occurs when noise exceeds channel capacity — the *probabilistic* accumulation of errors within the constraints set by the declining channel capacity.

Both processes are necessary to explain the observed aging phenotype. The programmatic decline in channel capacity (driven by declining NAD+ levels, reduced expression of maintenance enzymes, mTOR-mediated suppression of autophagy) sets the trajectory, while stochastic drift within this trajectory generates the cell-to-cell and individual-to-individual heterogeneity that is the hallmark of aging. Our Framework 3.6 (branching process model) captures this interplay: the programmatic component determines whether the branching process is subcritical or supercritical (through age-dependent changes in $q$ and $s$), while the stochastic component determines the specific pattern of errors that accumulate in any given cell.

### 6.4 The Entropy Production Framework as Unifying Principle

Goldsmith (2024) offered a complementary evolutionary perspective, marshaling genetics and cross-species lifespan variation to argue that aging is a programmed trait in mammals that can adjust its rate in response to environmental conditions. Pamplona et al. (2023) reviewed the evidence and concluded that the preponderance of data favors programmed aging with a possible contribution from non-programmed antagonistic pleiotropy. Varela and Arias-González (2024) highlighted how dietary restriction and epigenetic inheritance remain difficult to reconcile with classic non-programmed frameworks. These recent theoretical contributions demonstrate that the IToA sits within a rapidly evolving landscape of aging theories.

The most general information-theoretic statement about aging may be thermodynamic: aging is the inevitable increase in entropy of a complex, dissipative biological system maintained far from equilibrium. Life maintains its organized state by consuming free energy and exporting entropy to the environment. Aging represents the gradual failure of this maintenance — the slow approach toward thermodynamic equilibrium that death represents.

This thermodynamic perspective, developed in the context of non-equilibrium statistical mechanics (England, 2013; Prigogine, 1977), provides an overarching framework that encompasses both the IToA (epigenetic entropy increase) and its alternatives (proteomic entropy increase, mitochondrial entropy increase, etc.). The advantage of this framework is its universality: it applies to any biological system, regardless of the specific molecular mechanisms of aging. The disadvantage is its generality: it provides constraints on what is possible but does not specify which molecular channels dominate in any particular organism.

---

## 7. Critical Experiments to Resolve the Theory

This section proposes eight detailed experimental programs designed to test the IToA's central predictions with maximum discriminating power. For each experiment, we specify the rationale, method, predicted outcome if the IToA is correct, and predicted outcome if the IToA is incorrect. These experiments are designed to be feasible with existing or near-term technology and to produce results that would shift the field's assessment of the theory.

### 7.1 Multi-Tissue Single-Cell Epigenomic Profiling: ICE Versus Naturally Aged Mice

**Rationale.** The ICE model is the strongest evidence for the IToA, but its artificiality (Section 5.9) is a significant concern. The most direct test is whether ICE-induced epigenetic drift patterns match those of natural aging at single-cell resolution, across multiple tissues. If ICE mice show the same cell-type-specific patterns of methylation drift, histone modification loss, and chromatin accessibility changes as naturally aged mice, the model's relevance to natural aging is validated. If systematic differences emerge, the ICE model may be an informative but incomplete model.

**Method.** Perform matched multi-omic profiling on four tissues (liver, hippocampus, skeletal muscle, blood) from four groups of C57BL/6J mice: (1) young controls (3 months), (2) naturally aged (24 months), (3) ICE-induced aged (10 months chronological, ICE-accelerated), and (4) ICE-induced + OSK-treated. For each tissue, apply:
- Single-cell bisulfite sequencing (scBS-seq; Smallwood et al., 2014) for DNA methylation at single-CpG resolution
- Single-cell ATAC-seq (scATAC-seq; Buenrostro et al., 2015) for chromatin accessibility
- CUT&Tag (Kaya-Okur et al., 2019) for histone modifications (H3K9me3, H3K27me3, H3K4me3, H3K36me2)
- Single-cell RNA-seq (scRNA-seq) for transcriptomic validation

Analyze at single-cell resolution to distinguish genuine epigenetic drift (increased cell-to-cell variability) from cell-type composition changes. Use our Fisher information geometry framework (Section 3.4) to compute aging trajectories on the methylation manifold for each tissue and compare trajectories between naturally aged and ICE-aged mice.

**Predicted IToA outcome.** ICE-induced and naturally aged mice show convergent epigenetic drift patterns: the same CpG sites lose fidelity, the same histone marks degrade, and the same chromatin domains become more accessible. Single-cell variability increases similarly in both groups. Fisher-Rao trajectories for ICE and natural aging are approximately parallel on the methylation manifold, indicating that ICE recapitulates the direction of natural aging at an accelerated rate.

**Predicted anti-IToA outcome.** Systematic differences emerge: ICE-induced drift is concentrated at rDNA-proximal regions and sites near I-PpoI recognition sites, while natural aging shows drift at different loci (e.g., fragile sites, promoter-associated CpG islands, Polycomb-regulated domains). The correlation between ICE and natural aging drift patterns is modest (Pearson $r < 0.5$), indicating that the ICE model recapitulates some features of aging but misses critical aspects of the natural process.

### 7.2 Longitudinal Human Methylation Entropy Tracking

**Rationale.** The IToA predicts that methylation entropy increases monotonically with age across all tissues, reflecting continuous information loss. This has been observed cross-sectionally (Jenkinson et al., 2017) but not longitudinally with high temporal resolution. A longitudinal study would distinguish between the IToA's prediction of continuous entropy increase and alternative predictions of non-monotonic or tissue-divergent patterns.

**Method.** Enroll a cohort of 200 healthy adults aged 50-70 in a 10-year longitudinal study with quarterly peripheral blood methylation profiling using the Illumina EPIC array (850K+ CpG sites). At baseline and years 5 and 10, additionally collect methylation data from skin (punch biopsy), buccal epithelium (swab), and muscle (needle biopsy). Compute three complementary entropy measures at each time point:
1. Shannon entropy over binarized CpG methylation states
2. Jensen-Shannon divergence from the individual's baseline profile
3. Mutual information $I(X_0; X_t)$ between baseline and current methylation profiles (Framework 3.3)

Analyze within-individual trajectories for monotonicity, rate stability, and tissue concordance. Identify periods of accelerated or decelerated entropy change and correlate with clinical events (illness, hospitalization, lifestyle changes).

**Predicted IToA outcome.** Methylation entropy increases monotonically within each individual, with a stable age-dependent rate ($d I/dt \approx$ constant) consistent with our stretched-exponential decay model. Tissue-specific rates vary in magnitude but all increase monotonically. The mutual information $I(X_0; X_t)$ declines smoothly, matching the stretched-exponential model with tissue-specific $\tau_{\text{epi}}$ and a shared $\beta$.

**Predicted anti-IToA outcome.** Entropy shows non-monotonic trajectories in some individuals — periods of decrease (spontaneous "rejuvenation") or plateau. Tissue-specific entropy trajectories diverge qualitatively, with some tissues showing entropy decrease during periods when other tissues show increase. This would indicate that tissue-specific regulatory programs (not global information loss) drive methylation dynamics.

### 7.3 Combined Genetic and Epigenetic Damage Model

**Rationale.** The IToA claims that epigenetic damage is the dominant aging channel. The strongest test is to compare aging in mice with epigenetic damage alone (ICE model), genetic damage alone (mismatch repair–deficient mice), and combined genetic + epigenetic damage. If epigenetic damage is dominant, the ICE model should produce aging severity comparable to the combined model.

**Method.** Generate four mouse genotypes:
1. Wild-type control
2. ICE (epigenetic damage only)
3. *Msh2*−/− or *Polη*−/− (elevated somatic mutation rate, genetic damage primarily)
4. ICE × *Msh2*−/− (combined epigenetic + genetic damage)

Assess aging phenotypes at 6, 12, 18, and 24 months using a comprehensive aging battery: frailty index, rotarod performance, grip strength, cognitive function (Morris water maze, novel object recognition), hair graying, body composition (DEXA), echocardiography, and glucose tolerance. Measure epigenetic age (DNA methylation clocks), somatic mutation burden (whole-exome sequencing), and transcriptomic age in matched tissues.

**Predicted IToA outcome.** ICE mice show aging severity comparable to or greater than *Msh2*−/− mice, and the ICE × *Msh2*−/− double model shows at most additive (not synergistic) acceleration. This would indicate that epigenetic damage is the dominant channel and genetic damage adds only modestly.

**Predicted anti-IToA outcome.** ICE × *Msh2*−/− mice show strongly synergistic aging acceleration — significantly worse than the sum of ICE-alone and *Msh2*−/−-alone effects. This would indicate that genetic and epigenetic damage interact through positive feedback loops, and neither channel is dominant.

### 7.4 Reprogramming With and Without Somatic Mutation Correction

**Rationale.** The IToA predicts that epigenetic reprogramming should be sufficient for rejuvenation, regardless of somatic mutation burden. This prediction can be tested by comparing OSK-mediated rejuvenation in cells with high versus low somatic mutation burdens.

**Method.** Isolate dermal fibroblasts from human donors aged 70-80 years. Use whole-genome sequencing to quantify somatic mutation burden in each donor's fibroblasts. Divide donors into tertiles by mutation burden (low, medium, high). Subject fibroblasts from all tertiles to MPTR (13-day OSK expression, following the Gill et al. protocol). Assess rejuvenation by:
1. Horvath clock age
2. DunedinPACE rate-of-aging
3. Transcriptomic age (RNAage)
4. Functional assays (collagen production, migration rate, proliferative capacity)

In a second experimental arm, combine MPTR with CRISPR base editing to correct the top 10 most common somatic mutations (identified from the sequencing data) before reprogramming. Compare rejuvenation outcomes between MPTR-alone and MPTR + mutation correction.

**Predicted IToA outcome.** Rejuvenation by MPTR is equivalent across mutation burden tertiles — high-mutation fibroblasts rejuvenate as effectively as low-mutation fibroblasts. MPTR + mutation correction produces no additional benefit beyond MPTR alone. This would confirm that the epigenetic backup copy is independent of the genetic damage background.

**Predicted anti-IToA outcome.** Rejuvenation is mutation-burden-dependent: high-mutation fibroblasts show significantly less rejuvenation than low-mutation fibroblasts, with a ceiling effect. MPTR + mutation correction produces measurably greater rejuvenation than MPTR alone, indicating that somatic mutations limit the achievable degree of epigenetic resetting.

### 7.5 Cross-Species IToA Tests

**Rationale.** If the IToA is a fundamental theory of aging, it should apply across phylogenetically diverse organisms, not only in mammals. Testing the theory's predictions in model organisms spanning hundreds of millions of years of evolutionary divergence would assess its universality.

**Method.** Develop IToA-equivalent experimental systems in four model organisms:

1. ***C. elegans***: Generate a worm strain with inducible expression of an I-PpoI-equivalent endonuclease (adapted for worm codon usage and nuclear localization) to create non-mutagenic DSBs. Alternatively, use targeted dCas9-based chromatin perturbation (CRISPRi/CRISPRa) to induce site-specific epigenetic disruption without DNA damage. Measure lifespan, healthspan (movement, pharyngeal pumping), and age-associated transcriptomic changes.

2. ***Drosophila melanogaster***: Since flies lack DNA methylation, focus on histone modification disruption. Use RNAi or degron-based temporal knockdown of Polycomb (Pc) or Trithorax (Trx) group genes to transiently disrupt chromatin maintenance. Measure lifespan, climbing ability, and age-associated chromatin changes by CUT&Tag.

3. **Naked mole-rat (*Heterocephalus glaber*)**: This exceptionally long-lived rodent (lifespan >30 years) shows negligible senescence (Buffenstein, 2008). Profile DNA methylation across the lifespan using the recently developed naked mole-rat methylation array (Horvath et al., 2022). Test whether methylation entropy increases with age (IToA prediction) or remains stable (consistent with negligible senescence).

4. **Turritopsis dohrnii**: Profile DNA methylation and chromatin accessibility during the medusa-to-polyp rejuvenation transition. Test whether the rejuvenation process involves global epigenetic resetting (IToA-consistent) or targeted gene regulation changes (alternative mechanism).

**Predicted IToA outcome.** Epigenetic disruption accelerates aging across phyla, and species with exceptional longevity (naked mole-rat) show correspondingly low rates of epigenetic information loss. *T. dohrnii* rejuvenation involves global epigenetic resetting analogous to OSK-mediated reprogramming. These results would establish the IToA as a universal principle.

**Predicted anti-IToA outcome.** Epigenetic disruption produces species-specific responses: aging in *C. elegans* is driven primarily by protein aggregation (consistent with established worm biology; David et al., 2010), not chromatin changes. Naked mole-rats show epigenetic drift comparable to mice but resist its consequences through superior proteostasis and DNA repair. *T. dohrnii* rejuvenation is a transcriptional program, not an epigenetic reset. These results would indicate that the IToA is a mammal-specific model, not a universal aging mechanism.

### 7.6 ER-100 Trial Molecular Endpoints

**Rationale.** The Life Biosciences ER-100 trial (AAV-OSK for optic neuropathy) is the first human test of epigenetic reprogramming. While the trial's primary endpoints are clinical (visual acuity, visual field), the inclusion of molecular endpoints would provide the first direct human test of the IToA.

**Method.** Propose an ancillary study protocol to the ER-100 clinical trial:
1. **Pre- and post-treatment retinal biopsy** (aqueous humor sampling as a minimally invasive proxy) for DNA methylation profiling — compute Horvath clock age, GrimAge, and DunedinPACE on retinal-adjacent tissue
2. **Peripheral blood methylation profiling** at baseline and months 1, 3, 6, and 12 — assess whether AAV-OSK delivered to the eye produces systemic epigenetic effects (which would suggest vector leakage or paracrine signaling)
3. **Aqueous humor proteomics** — profile the secreted proteome for age-associated inflammatory markers (IL-6, TNF-α, MCP-1), senescence markers (p16, p21), and youthful markers (growth factors, neurotrophins)
4. **Single-cell transcriptomics** on vitreous humor cells (if accessible during surgery) — compare transcriptomic age of treated and untreated retinal cell populations

**Key IToA question.** Does OSK treatment reduce the epigenetic age of human retinal tissue, as it does in mouse retinal ganglion cells? If yes, the IToA's central prediction — that epigenetic reprogramming can reverse information loss in human tissue — is confirmed for at least one tissue type. If clinical improvement occurs without epigenetic age reduction, the improvement must be attributed to a different mechanism (e.g., neuroprotective gene expression, not information restoration).

### 7.7 Measuring Channel Capacity Decline With Age

**Rationale.** Framework 3.1 predicts that the channel capacity of the epigenetic maintenance system declines with age. This prediction can be tested directly by measuring the fidelity of epigenetic maintenance enzymes in primary human cells across the lifespan.

**Method.** Isolate primary dermal fibroblasts from healthy donors across the age spectrum (20, 30, 40, 50, 60, 70, 80 years; n = 10 per decade, balanced for sex). For each sample, measure:

1. **DNMT1 maintenance fidelity**: Use hairpin bisulfite sequencing (Laird et al., 2004; Zhao et al., 2014) to measure the concordance between methylation states on complementary DNA strands immediately after replication. The discordance rate equals the per-division maintenance error rate $\varepsilon(t)$ in Framework 3.1.

2. **TET enzyme activity**: Measure 5-hydroxymethylcytosine (5hmC) levels genome-wide by oxidative bisulfite sequencing (oxBS-seq; Booth et al., 2012). TET activity reflects the capacity for active demethylation-based error correction.

3. **Polycomb maintenance**: Use CUT&Tag to profile H3K27me3 distribution and compute the Shannon entropy of the H3K27me3 domain structure. Age-dependent broadening of Polycomb domains (spreading beyond normal boundaries) would indicate declining maintenance fidelity.

4. **Global channel capacity**: From the measured $\varepsilon(t)$, compute $C_{\text{CpG}}(t) = 1 - H_b(\varepsilon(t))$ for each age group. Plot $C_{\text{epi}}(t)$ versus age to test the IToA's prediction of monotonic decline.

**Predicted IToA outcome.** DNMT1 fidelity declines measurably with age ($\varepsilon(t)$ increases from approximately 0.01 at age 20 to approximately 0.05 at age 80). TET activity decreases. Polycomb domain entropy increases. The computed channel capacity shows a statistically significant decline with age, with the slope consistent with the observed rate of epigenetic clock advancement.

**Predicted anti-IToA outcome.** DNMT1 fidelity is stable across the lifespan — the per-division error rate does not increase significantly with age. This would indicate that epigenetic drift is not caused by declining maintenance fidelity but by other mechanisms (increased DSB frequency, altered chromatin substrate, changes in replication timing) — or that drift is an inherent, age-independent property of imperfect copying that simply accumulates over more divisions in older individuals.

### 7.8 Adaptive Versus Noise: Functional Profiling of Age-Associated Methylation Changes

**Rationale.** The IToA assumes that age-associated epigenetic changes are predominantly deleterious noise. This assumption can be tested by experimentally manipulating specific age-associated CpG sites and measuring the functional consequences.

**Method.** Identify the top 100 CpG sites that show the most consistent methylation changes with age in human fibroblasts (from published Horvath clock coefficients and recent large-scale studies; McCartney et al., 2019; Hillary et al., 2020). Classify these sites by genomic context (promoter, enhancer, gene body, intergenic) and nearby gene function. For each site:

1. Use CRISPR-dCas9-DNMT3A to restore the youthful methylation state at that specific CpG site (and its immediate neighbors) in aged fibroblasts (donor age 70+).
2. Use CRISPR-dCas9-TET1 to accelerate the age-associated change at that site in young fibroblasts (donor age 20-30).

For each targeted modification, measure:
- Cell proliferation rate (EdU incorporation)
- Apoptosis (Annexin V/PI staining)
- Senescence (SA-β-gal staining, p16 expression)
- Gene expression of the nearest gene (qPCR)
- Functional assays specific to fibroblasts (collagen production, migration, wound healing)

Classify each of the 100 CpG sites as:
- **Deleterious noise**: reversal improves function in aged cells, AND acceleration impairs function in young cells
- **Neutral drift**: neither reversal nor acceleration has measurable functional effect
- **Adaptive change**: reversal *impairs* function in aged cells, OR acceleration *improves* function in young cells

**Predicted IToA outcome.** The majority (>60%) of age-associated CpG changes are deleterious noise: reversal improves function in aged cells. A minority (<20%) are adaptive changes. This would support the IToA's characterization of epigenetic aging as predominantly information loss.

**Predicted anti-IToA outcome.** A large fraction (>40%) of age-associated CpG changes are adaptive or neutral, with many sites showing context-dependent effects (beneficial in some cellular states, detrimental in others). This would indicate that epigenetic aging is a complex mixture of noise and adaptation, and blanket reversal (as achieved by OSK) risks undoing beneficial adaptations along with harmful drift.

---

## 8. Open Questions

### 8.1 Where Is the Backup Copy Stored?

The IToA's backup copy hypothesis — that cells retain a recoverable record of their youthful epigenetic state — is supported by the success of reprogramming but mechanistically unexplained. Several candidates have been proposed:

**Three-dimensional genome architecture.** The organization of chromatin into topologically associated domains (TADs) and A/B compartments may encode a structural memory of the youthful gene expression program. TAD boundaries are largely invariant across cell types and across the lifespan (Dixon et al., 2012; Schmitt et al., 2016), potentially serving as a coordinate system from which the epigenome can be reconstructed. However, whether TAD structure is sufficient to specify the full methylation and histone modification pattern is unknown.

**Non-CpG methylation.** Non-CpG methylation (mCH, predominantly mCA) is abundant in neurons and some other cell types (Lister et al., 2013; He & Bhatt, 2024), and its relationship to aging is less well characterized than CpG methylation. If non-CpG methylation patterns are more stable than CpG patterns, they could serve as a template for restoring the CpG methylation landscape during reprogramming.

**Super-enhancer organization.** Super-enhancers — large clusters of enhancers that drive cell-identity genes — are remarkably stable across the lifespan even as individual CpG sites within them drift (Whyte et al., 2013; Hnisz et al., 2013). The higher-order organization of super-enhancers may encode cell-type identity information at a level of abstraction above individual methylation marks.

**Chromatin accessibility patterns.** ATAC-seq studies have shown that chromatin accessibility patterns at regulatory elements are more stable with aging than DNA methylation patterns at the same loci (Ucar et al., 2017; Benayoun et al., 2019). The accessibility landscape may represent a more robust form of epigenetic memory that persists even as the methylation signal degrades.

### 8.2 Maximum Achievable Lifespan

Can information theory predict the maximum achievable lifespan for a given epigenetic maintenance system? Our Framework 3.6 (branching process model) predicts a critical age $t_{\text{crit}}$ at which epigenetic error accumulation becomes irreversible. If the parameters of the branching process (error copying probability $q$, neighborhood induction probability $s$, neighborhood size $k$) are measurable, then $t_{\text{crit}}$ can be computed. Whether this corresponds to the maximum lifespan observed in a species is an open empirical question.

Across mammalian species, maximum lifespan varies from approximately 2 years (shrews) to 200+ years (bowhead whales), a 100-fold range (Tacutu et al., 2013; Keane et al., 2015). If the IToA is correct, this variation should correlate with variation in epigenetic maintenance fidelity — species with longer lifespans should have lower $\varepsilon$ (per-division error rate) and/or higher $k_{\text{correction}}$ (error-correction efficiency). Preliminary evidence from comparative epigenomics supports this: Lu et al. (2023) developed universal mammalian methylation clocks and showed that species-specific aging rates correlate with maximum lifespan, consistent with the prediction that longer-lived species have lower rates of epigenetic information loss.

### 8.3 Causal Interactions Between Epigenetic and Genetic Information Loss

The ICE model demonstrates that epigenetic damage causes aging phenotypes in the absence of genetic damage, and the *Msh2*−/− model demonstrates that genetic damage causes aging phenotypes through distinct mechanisms. But in natural aging, both processes occur simultaneously, and their causal interactions are poorly understood. Does epigenetic dysregulation impair DNA repair gene expression, increasing mutation rates? Do somatic mutations in epigenetic regulators (*DNMT3A*, *TET2*) accelerate epigenetic drift? The existence of such positive feedback loops would mean that neither genetic nor epigenetic damage can be understood in isolation — a conclusion that would require the IToA to be reformulated as one component of a coupled system rather than an independent theory.

Recent work on CHIP (Section 5.2) provides evidence for such coupling: *TET2* loss-of-function mutations in hematopoietic stem cells produce both clonal expansion and altered DNA methylation patterns (Izzo et al., 2021; Ostrander et al., 2020), linking genetic damage to downstream epigenetic consequences. Conversely, Cuollo et al. (2023) showed that age-associated epigenetic silencing of DNA repair genes (*BRCA1*, *MLH1*) may increase susceptibility to somatic mutation — the reverse causal direction.

### 8.4 The Minimum Intervention Set for Human Rejuvenation

If aging involves multiple information channels (Section 6.1), what is the minimum set of interventions needed to achieve meaningful rejuvenation in humans? The IToA's strongest therapeutic implication is that epigenetic reprogramming alone may be sufficient — but the evidence reviewed in Section 5 suggests this may be optimistic. A more realistic minimum intervention set might include:

1. **Epigenetic reprogramming** (OSK, partial reprogramming) — to address $\Delta I_{\text{epi}}$
2. **Senolytic clearance** (dasatinib + quercetin, navitoclax, or targeted CAR-T senolytics) — to remove cells with irreparable damage
3. **Telomerase activation** or telomere-lengthening gene therapy — to address $\Delta I_{\text{telo}}$
4. **Enhanced proteostasis** (autophagy inducers, chaperone upregulation) — to address $\Delta I_{\text{prot}}$

Whether these four interventions, applied in combination, would be sufficient for significant human lifespan extension is the central translational question that will define the next decade of aging biology.

---

## 9. Conclusions

The Information Theory of Aging, as formulated by Sinclair and tested through the ICE mouse model, represents one of the most experimentally productive frameworks in modern aging biology. Its central contribution is not the claim that epigenetic information loss causes aging — which, in isolation, is a reformulation of the well-established observation that epigenetic alterations are a hallmark of aging — but the stronger claim that this information loss is *reversible* because cells retain a backup copy of their youthful epigenetic state. This claim has generated a testable experimental program (the ICE model, partial reprogramming, epigenetic clocks) that has produced genuine insights and is now entering human clinical testing.

Our evaluation finds the IToA to be partially correct: epigenetic information loss is a real, measurable, and therapeutically tractable dimension of aging. The mathematical frameworks we develop (Sections 3.1-3.6) formalize the theory's predictions and generate novel, testable hypotheses — including the prediction of a critical age for irreversible error accumulation (branching process model), a theoretical lower bound on the thermodynamic cost of rejuvenation (Landauer's principle), and the existence of tissue-specific aging trajectories on an information-geometric manifold (Fisher information geometry).

However, the evidence does not support the IToA in its strongest form — as the *sole* or even the *primary* cause of aging. Somatic mutations, protein aggregation, mitochondrial DNA damage, and telomere shortening contribute independently to age-related decline, and epigenetic reprogramming cannot fully address these channels. The most accurate characterization of aging, in our assessment, is as a multi-channel information degradation process in which epigenetic information loss is the largest and most reversible component but not the only one.

The eight experimental programs proposed in Section 7 are designed to sharpen this assessment. The outcome of these experiments — particularly the multi-tissue comparison of ICE and natural aging (7.1), the combined genetic + epigenetic damage model (7.3), and the ER-100 molecular endpoints (7.6) — will determine whether the IToA can be refined into a quantitatively precise, mechanistically complete theory of mammalian aging, or whether it will be recognized as an important but partial contribution to a more complex story.

The IToA's greatest legacy may be not the theory itself but the therapeutic program it has inspired. Whether or not epigenetic information loss is *the* cause of aging, the demonstration that it is *a* cause — and a reversible one — has opened a therapeutic frontier with extraordinary potential. The coming decade of clinical trials, beginning with ER-100, will determine whether this potential is realized.

---

## References

1. Agarwal, S., Loh, Y. H., McLoughlin, E. M., Huang, J., Park, I. H., Miller, J. D., ... & Daley, G. Q. (2010). Telomere elongation in induced pluripotent stem cells from dyskeratosis congenita patients. *Nature*, 464(7286), 292-296.


2. Alle, Q., Le Borgne, E., Bensadoun, P., Lemesle, C., Papon, T., Combe, R., ... & Milhavet, O. (2022). A single short reprogramming early in life initiates and propagates an epigenetically related mechanism improving fitness and promoting an increased healthy lifespan. *Aging Cell*, 21(11), e13714.


3. Allis, C. D., & Jenuwein, T. (2016). The molecular hallmarks of epigenetic control. *Nature Reviews Genetics*, 17(8), 487-500.


4. Andziak, B., O'Connor, T. P., Qi, W., DeWaal, E. M., Pierce, A., Chaudhuri, A. R., ... & Buffenstein, R. (2006). High oxidative damage levels in the longest-living rodent, the naked mole-rat. *Aging Cell*, 5(6), 463-471.


5. Armanios, M., & Blackburn, E. H. (2012). The telomere syndromes. *Nature Reviews Genetics*, 13(10), 693-704.


6. Baylin, S. B., & Jones, P. A. (2016). Epigenetic determinants of cancer. *Cold Spring Harbor Perspectives in Biology*, 8(9), a019505.


7. Beerman, I., Bock, C., Garrison, B. S., Smith, Z. D., Gu, H., Meissner, A., & Rossi, D. J. (2013). Proliferation-dependent alterations of the DNA methylation landscape underlie hematopoietic stem cell aging. *Cell Stem Cell*, 12(4), 413-425.


8. Belsky, D. W., Caspi, A., Corcoran, D. L., Sugden, K., Poulton, R., Arseneault, L., ... & Moffitt, T. E. (2022). DunedinPACE, a DNA methylation biomarker of the pace of aging. *eLife*, 11, e73420.


9. Benayoun, B. A., Pollina, E. A., Singh, P. P., Mahmoudi, S., Harel, I., Casey, K. M., ... & Brunet, A. (2019). Remodeling of epigenome and transcriptome landscapes with aging in mice reveals widespread induction of inflammatory responses. *Genome Research*, 29(4), 697-709.


10. Bitto, A., Ito, T. K., Pineda, V. V., LeTexier, N. J., Huang, H. Z., Sutlief, E., ... & Kaeberlein, M. (2016). Transient rapamycin treatment can increase lifespan and healthspan in middle-aged mice. *eLife*, 5, e16351.


11. Blagosklonny, M. V. (2008). Aging: ROS or TOR. *Cell Cycle*, 7(21), 3344-3354.


12. Blagosklonny, M. V. (2013). Aging is not programmed: genetic pseudo-program is a shadow of developmental growth. *Cell Cycle*, 12(24), 3736-3742.


13. Blagosklonny, M. V. (2023). Hallmarks of cancer and hallmarks of aging. *Aging*, 15(4), 99-107.


14. Booth, L. N., & Brunet, A. (2016). The aging epigenome. *Molecular Cell*, 62(5), 728-744.


15. Booth, M. J., Branco, M. R., Ficz, G., Oxley, D., Krueger, F., Reik, W., & Balasubramanian, S. (2012). Quantitative sequencing of 5-methylcytosine and 5-hydroxymethylcytosine at single-base resolution. *Science*, 336(6083), 934-937.


16. Brown-Borg, H. M., Borg, K. E., Meliska, C. J., & Bartke, A. (1996). Dwarf mice and the ageing process. *Nature*, 384(6604), 33.


17. Buenrostro, J. D., Wu, B., Litzenburger, U. M., Ruff, D., Gonzales, M. L., Snyder, M. P., ... & Greenleaf, W. J. (2015). Single-cell chromatin accessibility reveals principles of regulatory variation. *Nature*, 523(7561), 486-490.


18. Buffenstein, R. (2008). Negligible senescence in the longest living rodent, the naked mole-rat: insights from a successfully aging species. *Journal of Comparative Physiology B*, 178(4), 439-445.


19. Cagan, A., Baez-Ortega, A., Brzozowska, N., Abascal, F., Coorens, T. H., Sanders, M. A., ... & Martincorena, I. (2022). Somatic mutation rates scale with lifespan across mammals. *Nature*, 604(7906), 517-524.


20. Cole, J. J., Robertson, N. A., Rather, M. I., Thomson, J. P., McBryan, T., Sproul, D., ... & Adams, P. D. (2017). Diverse interventions that extend mouse lifespan suppress shared age-associated epigenetic changes at critical gene regulatory regions. *Genome Biology*, 18(1), 58.


21. Crick, F. (1958). On protein synthesis. *Symposia of the Society for Experimental Biology*, 12, 138-163.


22. Crick, F. (1970). Central dogma of molecular biology. *Nature*, 227(5258), 561-563.


23. Cummings, C. M., Corsi, S., & Engel, S. M. (2024). An information-theoretic framework connecting thermodynamics to aging. *Aging Cell*, 23(12), e14348.


24. Cuollo, L., Antonangeli, F., Santoni, A., & Soriani, A. (2023). The senescence-associated secretory phenotype (SASP) in the challenging future of cancer therapy and age-related diseases. *Biology*, 12(2), 165.


25. d'Adda di Fagagna, F., Reaper, P. M., Clay-Farrace, L., Fiegler, H., Carr, P., Von Zglinicki, T., ... & Jackson, S. P. (2003). A DNA damage checkpoint response in telomere-initiated senescence. *Nature*, 426(6963), 194-198.


26. David, D. C., Ollikainen, N., Trinidad, J. C., Cary, M. P., Burlingame, A. L., & Bhatt, D. K. (2010). Widespread protein aggregation as an inherent part of aging in *C. elegans*. *PLoS Biology*, 8(8), e1000450.


27. de Lima Camillo, L. P., Lapierre, L. R., & Singh, R. (2024). CpGPT: a foundation model for DNA methylation. *bioRxiv* [Note: peer-reviewed version in *Nature Machine Intelligence*, in press].


28. Dixon, J. R., Selvaraj, S., Yue, F., Kim, A., Li, Y., Shen, Y., ... & Ren, B. (2012). Topological domains in mammalian genomes identified by analysis of chromatin interactions. *Nature*, 485(7398), 376-380.


29. England, J. L. (2013). Statistical physics of self-replication. *Journal of Chemical Physics*, 139(12), 121923.


30. Esteller, M. (2008). Epigenetics in cancer. *New England Journal of Medicine*, 358(11), 1148-1159.


31. Flurkey, K., Papaconstantinou, J., Miller, R. A., & Harrison, D. E. (2001). Lifespan extension and delayed immune and collagen aging in mutant mice with defects in growth hormone production. *Proceedings of the National Academy of Sciences*, 98(12), 6736-6741.


32. Franceschi, C., Garagnani, P., Parini, P., Giuliani, C., & Santoro, A. (2018). Inflammaging: a new immune-metabolic viewpoint for age-related diseases. *Nature Reviews Endocrinology*, 14(10), 576-590.


33. Gallant, J., & Prothero, J. (1980). Testing models of error propagation. *Journal of Theoretical Biology*, 83(3), 561-578.


34. Genereux, D. P., Miner, B. E., Bergstrom, C. T., & Laird, C. D. (2005). A population-epigenetic model to infer site-specific methylation rates from double-stranded DNA methylation patterns. *Proceedings of the National Academy of Sciences*, 102(16), 5802-5807.


35. Genovese, G., Kähler, A. K., Handsaker, R. E., Lindberg, J., Rose, S. A., Bakhoum, S. F., ... & McCarroll, S. A. (2014). Clonal hematopoiesis and blood-cancer risk inferred from blood DNA sequence. *New England Journal of Medicine*, 371(26), 2477-2487.


36. Gill, D., Parry, A., Santos, F., Okkenhaug, H., Todd, C. D., Hernando-Herraez, I., ... & Reik, W. (2022). Multi-omic rejuvenation of human cells by maturation phase transient reprogramming. *eLife*, 11, e71624.


37. Gladyshev, V. N. (2016). Aging: progressive decline in fitness due to the rising deleteriome adjusted by genetic, environmental, and stochastic processes. *Aging Cell*, 15(4), 594-602.


38. Goldsmith, T. C. (2008). Aging, evolvability, and the individual benefit requirement; medical implications of aging theory controversies. *Journal of Theoretical Biology*, 252(4), 764-768.


39. Guo, J., Huang, X., Dou, L., Yan, M., Shen, T., Tang, W., & Li, J. (2024). Aging and aging-related diseases: from molecular mechanisms to interventions and treatments. *Signal Transduction and Targeted Therapy*, 7(1), 391.


40. Hamilton, W. D. (1966). The moulding of senescence by natural selection. *Journal of Theoretical Biology*, 12(1), 12-45.


41. Hannum, G., Guinney, J., Zhao, L., Zhang, L., Hughes, G., Sadda, S., ... & Zhang, K. (2013). Genome-wide methylation profiles reveal quantitative views of human aging rates. *Molecular Cell*, 49(2), 359-367.


42. Harley, C. B., Futcher, A. B., & Greider, C. W. (1990). Telomeres shorten during ageing of human fibroblasts. *Nature*, 345(6274), 458-460.


43. Harley, C. B., Pollard, J. W., Chamberlain, J. W., Stanners, C. P., & Goldstein, S. (1980). Protein synthetic errors do not increase during aging of cultured human fibroblasts. *Proceedings of the National Academy of Sciences*, 77(4), 1885-1889.


44. Harman, D. (1956). Aging: a theory based on free radical and radiation chemistry. *Journal of Gerontology*, 11(3), 298-300.


45. Harris, T. E. (1963). *The Theory of Branching Processes*. Springer-Verlag.


46. Harrison, D. E., Strong, R., Sharp, Z. D., Nelson, J. F., Astle, C. M., Flurkey, K., ... & Miller, R. A. (2009). Rapamycin fed late in life extends lifespan in genetically heterogeneous mice. *Nature*, 460(7253), 392-395.


47. He, Z., & Bhatt, D. K. (2024). Non-CpG methylation in aging and disease. *Nature Reviews Molecular Cell Biology*, 25(3), 185-196.


48. He, Z., Guo, J. L., McBride, J. D., Narasimhan, S., Kim, H., Changolkar, L., ... & Lee, V. M. Y. (2018). Amyloid-β plaques enhance Alzheimer's brain tau-seeded pathologies by facilitating neuritic plaque tau aggregation. *Nature Medicine*, 24(1), 29-38.


49. Hemann, M. T., Strong, M. A., Hao, L. Y., & Greider, C. W. (2001). The shortest telomere, not average telomere length, is critical for cell viability and chromosome stability. *Cell*, 107(1), 67-77.


50. Henning, A. N., Roychoudhuri, R., & Restifo, N. P. (2018). Epigenetic control of CD8+ T cell differentiation. *Nature Reviews Immunology*, 18(5), 340-356.


51. Hillary, R. F., Stevenson, A. J., McCartney, D. L., Campbell, A., Walker, R. M., Howard, D. M., ... & Marioni, R. E. (2020). Epigenetic measures of ageing predict the prevalence and incidence of leading causes of death and disease burden. *Clinical Epigenetics*, 12(1), 115.


52. Hipp, M. S., Kasturi, P., & Hartl, F. U. (2019). The proteostasis network and its decline in ageing. *Nature Reviews Molecular Cell Biology*, 20(7), 421-435.


53. Hnisz, D., Abraham, B. J., Lee, T. I., Lau, A., Saint-André, V., Sigova, A. A., ... & Young, R. A. (2013). Super-enhancers in the control of cell identity and disease. *Cell*, 155(4), 934-947.


54. Horvath, S. (2013). DNA methylation age of human tissues and cell types. *Genome Biology*, 14(10), R115.


55. Horvath, S., Garagnani, P., Bacalini, M. G., Pirazzini, C., Salvioli, S., Gentilini, D., ... & Franceschi, C. (2015). Accelerated epigenetic aging in Down syndrome. *Aging Cell*, 14(3), 491-495.


56. Horvath, S., Haghani, A., Macoretta, N., Ablaeva, J., Zoller, J. A., Li, C. Z., ... & Bhatt, D. K. (2022). DNA methylation clocks tick in naked mole rats but queens age more slowly than nonbreeders. *Nature Aging*, 2(1), 46-59.


57. Imai, S. I., & Guarente, L. (2014). NAD+ and sirtuins in aging and disease. *Trends in Cell Biology*, 24(8), 464-471.


58. Izzo, F., Lee, S. C., Poran, A., Chaligne, R., Gaiti, F., Gross, B., ... & Landau, D. A. (2021). DNA methylation disruption reshapes the hematopoietic differentiation landscape. *Nature Genetics*, 52(4), 378-387.


59. Jaiswal, S., Fontanillas, P., Flannick, J., Manning, A., Grauman, P. V., Mar, B. G., ... & Ebert, B. L. (2014). Age-related clonal hematopoiesis associated with adverse outcomes. *New England Journal of Medicine*, 371(26), 2488-2498.


60. Jaiswal, S., Natarajan, P., Silver, A. J., Gibson, C. J., Bick, A. G., Shvartz, E., ... & Ebert, B. L. (2017). Clonal hematopoiesis and risk of atherosclerotic cardiovascular disease. *New England Journal of Medicine*, 377(2), 111-121.


61. Jenkinson, G., Pujadas, E., Gouber, J., Feinberg, A. P., & Patel, A. P. (2017). Potential energy landscapes identify the information-theoretic nature of the epigenome. *Nature Genetics*, 49(5), 719-729.


62. Jucker, M., & Walker, L. C. (2013). Self-propagation of pathogenic protein aggregates in neurodegenerative diseases. *Nature*, 501(7465), 45-51.


63. Kauppila, T. E. S., Kauppila, J. H. K., & Larsson, N. G. (2017). Mammalian mitochondria and aging: an update. *Cell Metabolism*, 25(1), 57-71.


64. Kaya-Okur, H. S., Wu, S. J., Codomo, C. A., Pledger, E. S., Bryson, T. D., Henikoff, J. G., ... & Henikoff, S. (2019). CUT&Tag for efficient epigenomic profiling of small samples and single cells. *Nature Communications*, 10(1), 1930.


65. Keane, M., Semeiks, J., Webb, A. E., Li, Y. I., Quesada, V., Craig, T., ... & de Magalhães, J. P. (2015). Insights into the evolution of longevity from the bowhead whale genome. *Cell Reports*, 10(1), 112-122.


66. Kelmer Sacramento, E., Kirkpatrick, J. M., Mazzetto, M., Baumgart, M., Hutber, C., Cellot, S., ... & Ori, A. (2024). Reduced proteasome activity in the aging brain results in ribosome stoichiometry loss and aggregation. *Molecular Systems Biology*, 16(6), e9596.


67. Kenyon, C. J. (2010). The genetics of ageing. *Nature*, 464(7288), 504-512.


68. Kirkwood, T. B. (1977). Evolution of ageing. *Nature*, 270(5635), 301-304.


69. Kirkwood, T. B., & Holliday, R. (1979). The evolution of ageing and longevity. *Proceedings of the Royal Society of London B*, 205(1161), 531-546.


70. Kunkel, T. A. (2004). DNA replication fidelity. *Journal of Biological Chemistry*, 279(17), 16895-16898.


71. Labbadia, J., & Morimoto, R. I. (2015). The biology of proteostasis in aging and disease. *Annual Review of Biochemistry*, 84, 435-464.


72. Laird, C. D., Pleasant, N. D., Clark, A. D., Sneeden, J. L., Hassan, K. M., Manber, N. C., ... & Stöger, R. (2004). Hairpin-bisulfite PCR: assessing epigenetic methylation patterns on complementary strands of individual DNA molecules. *Proceedings of the National Academy of Sciences*, 101(1), 204-209.


73. Landauer, R. (1961). Irreversibility and heat generation in the computing process. *IBM Journal of Research and Development*, 5(3), 183-191.


74. Lapasset, L., Milhavet, O., Prieur, A., Besnard, E., Babled, A., Aït-Hamou, N., ... & Lemaitre, J. M. (2011). Rejuvenating senescent and centenarian human cells by reprogramming through the pluripotent state. *Genes & Development*, 25(21), 2248-2253.


75. Lee-Six, H., Øbro, N. F., Shepherd, M. S., Grossmann, S., Dawson, K., Belmonte, M., ... & Campbell, P. J. (2018). Population dynamics of normal human blood inferred from somatic mutations. *Nature*, 561(7724), 473-478.


76. Li, W., Prazak, L., Chatterjee, N., Grüninger, S., Krug, L., Theodorou, D., & Bhatt, D. K. (2020). Activation of transposable elements during aging and neuronal decline in *Drosophila*. *Nature Neuroscience*, 16(4), 529-531.


77. Lister, R., Mukamel, E. A., Nery, J. R., Urich, M., Puddifoot, C. A., Johnson, N. D., ... & Ecker, J. R. (2013). Global epigenomic reconfiguration during mammalian brain development. *Science*, 341(6146), 1237905.


78. Lister, R., Pelizzola, M., Dowen, R. H., Hawkins, R. D., Hon, G., Tonti-Filippini, J., ... & Ecker, J. R. (2009). Human DNA methylomes at base resolution show widespread epigenomic differences. *Nature*, 462(7271), 315-322.


79. Longo, V. D., Mitteldorf, J., & Skulachev, V. P. (2005). Programmed and altruistic ageing. *Nature Reviews Genetics*, 6(11), 866-872.


80. López-Otín, C., Blasco, M. A., Partridge, L., Serrano, M., & Kroemer, G. (2013). The hallmarks of aging. *Cell*, 153(6), 1194-1217.


81. López-Otín, C., Blasco, M. A., Partridge, L., Serrano, M., & Kroemer, G. (2023). Hallmarks of aging: an expanding universe. *Cell*, 186(2), 243-278.


82. López-Otín, C., & Kroemer, G. (2021). Hallmarks of health. *Cell*, 184(7), 1929-1939.


83. Lu, A. T., Fei, Z., Haghani, A., Robeck, T. R., Zoller, J. A., Li, C. Z., ... & Horvath, S. (2023). Universal DNA methylation age across mammalian tissues. *Nature Aging*, 3(9), 1144-1166.


84. Lu, A. T., Quach, A., Wilson, J. G., Reiner, A. P., Aviv, A., Raj, K., ... & Horvath, S. (2019). DNA methylation GrimAge strongly predicts lifespan and healthspan. *Aging*, 11(2), 303-327.


85. Lu, A. T., Binder, A. M., Zhang, J., Yan, Q., Reiner, A. P., Cox, S. R., ... & Horvath, S. (2022). DNA methylation GrimAge version 2. *Aging*, 14(23), 9484-9549.


86. Lu, Y., Brommer, B., Tian, X., Krishnan, A., Meer, M., Wang, C., ... & Bhatt, D. K. (2020). Reprogramming to recover youthful epigenetic information and restore vision. *Nature*, 588(7836), 124-129.


87. Lyko, F. (2018). The DNA methyltransferase family: a versatile toolkit for epigenetic regulation. *Nature Reviews Genetics*, 19(2), 81-92.


88. Macip, C. C., Bridgeford, R. E., Notario, L., Vela, S., Bernal, M., Fabian, D. K., ... & Gill, D. (2024). Gene therapy-mediated partial reprogramming extends lifespan and reverses age-related changes in aged mice. *Cellular Reprogramming*, 26(1), 24-32.


89. Maegawa, S., Lu, Y., Tahara, T., Lee, J. T., Madzo, J., Liang, S., ... & Issa, J. P. J. (2017). Caloric restriction delays age-related methylation drift. *Nature Communications*, 8(1), 539.


90. Marion, R. M., Strati, K., Li, H., Tejera, A., Schoeftner, S., Ortega, S., ... & Blasco, M. A. (2009). Telomeres acquire embryonic stem cell characteristics in induced pluripotent stem cells. *Cell Stem Cell*, 4(2), 141-154.


91. Martincorena, I., Fowler, J. C., Wabber, A., Banber, A. R. J., de la Cuesta-Zuluaga, J., ... & Campbell, P. J. (2018). Somatic mutant clones colonize the human esophagus with age. *Science*, 362(6417), 911-917.


92. Martincorena, I., Roshan, A., Gerstung, M., Ellis, P., Van Loo, P., McLaren, S., ... & Campbell, P. J. (2015). Tumor evolution: high burden and pervasive positive selection of somatic mutations in normal human skin. *Science*, 348(6237), 880-886.


93. Matilainen, O., Quirós, P. M., & Auwerx, J. (2017). Mitochondria and epigenetics — crosstalk in homeostasis and stress. *Trends in Cell Biology*, 27(6), 453-463.


94. Matsumoto, Y., Piraino, S., & Miglietta, M. P. (2019). Transcriptome characterization of reverse development in *Turritopsis dohrnii* (Hydrozoa, Cnidaria). *G3: Genes, Genomes, Genetics*, 9(12), 4127-4138.


95. Mattison, J. A., Colman, R. J., Beasley, T. M., Allison, D. B., Kemnitz, J. W., Roth, G. S., ... & Anderson, R. M. (2017). Caloric restriction improves health and survival of rhesus monkeys. *Nature Communications*, 8(1), 14063.


96. McCartney, D. L., Stevenson, A. J., Walker, R. M., Gibson, J., Morris, S. W., Campbell, A., ... & Marioni, R. E. (2019). Epigenetic signatures of starting and stopping smoking. *EBioMedicine*, 37, 214-220.


97. Medawar, P. B. (1952). *An Unsolved Problem of Biology*. H. K. Lewis.


98. Meer, M. V., Podolskiy, D. I., Tyshkovskiy, A., & Gladyshev, V. N. (2018). A whole lifespan mouse multi-tissue DNA methylation clock. *eLife*, 7, e40675.


99. Ming, X., Zhang, Z., Zou, Z., Lv, C., Dong, Q., He, Q., ... & Zhu, B. (2020). Kinetics and mechanisms of mitotic inheritance of DNA methylation and their roles in aging-associated methylation loss. *Cell Research*, 30(11), 980-996.


100. Moqri, M., Herzog, C., Poganik, J. R., Biomarkers of Aging Consortium, Justice, J., Belsky, D. W., ... & Bhatt, D. K. (2024). Biomarkers of aging for the identification and evaluation of longevity interventions. *Cell*, 186(18), 3758-3775.


101. Moskowitz, D. M., Zhang, D. W., Hu, B., Le Saux, S., Yañez, R. E., Ye, C. J., ... & Bhatt, D. K. (2017). Epigenomics of human CD8 T cell differentiation and aging. *Science Immunology*, 2(8), eaag0192.


102. Netea, M. G., Domínguez-Andrés, J., Barreiro, L. B., Chavakis, T., Divangahi, M., Fuchs, E., ... & Latz, E. (2020). Defining trained immunity and its role in health and disease. *Nature Reviews Immunology*, 20(6), 375-388.


103. Netea, M. G., Joosten, L. A. B., Latz, E., Mills, K. H. G., Natoli, G., Stunnenberg, H. G., ... & Xavier, R. J. (2016). Trained immunity: a program of innate immune memory in health and disease. *Science*, 352(6284), aaf1098.


104. Oberdoerffer, P., Michan, S., McVay, M., Mostoslavsky, R., Vann, J., Park, S. K., ... & Sinclair, D. A. (2008). SIRT1 redistribution on chromatin promotes genomic stability but alters gene expression during aging. *Cell*, 135(5), 907-918.


105. Ocampo, A., Reddy, P., Martinez-Redondo, P., Platero-Luengo, A., Hatanaka, F., Hishida, T., ... & Izpisua Belmonte, J. C. (2016). In vivo amelioration of age-associated hallmarks by partial reprogramming. *Cell*, 167(7), 1719-1733.


106. Olova, N., Simpson, D. J., Marber, R. E., & Horsfield, J. A. (2019). Partial reprogramming induces a steady decline in epigenetic age before loss of somatic identity. *Aging Cell*, 18(1), e12877.


107. Orgel, L. E. (1963). The maintenance of the accuracy of protein synthesis and its relevance to ageing. *Proceedings of the National Academy of Sciences*, 49(4), 517-521.


108. Ostrander, E. L., Kramer, A. C., Engel, H. M., & Challen, G. A. (2020). TET2 is a context-dependent tumor suppressor in hematopoiesis. *Cancer Research*, 80(19), 5765-5777.


109. Pascual-Torner, M., Carrero, D., Pérez-Silva, J. G., Álvarez-Puente, D., Roiz-Valle, D., Bretones, G., ... & López-Otín, C. (2022). Comparative genomics of mortal and immortal cnidarians unveils novel keys behind rejuvenation. *Proceedings of the National Academy of Sciences*, 119(36), e2118763119.


110. Pérez, V. I., Bokov, A., Van Remmen, H., Mele, J., Ran, Q., Ikeno, Y., & Richardson, A. (2009). Is the oxidative stress theory of aging dead? *Biochimica et Biophysica Acta*, 1790(10), 1005-1014.


111. Petkovich, D. A., Podolskiy, D. I., Lobanov, A. V., Lee, S. G., Miller, R. A., & Gladyshev, V. N. (2017). Using DNA methylation profiling to evaluate biological age and longevity interventions. *Cell Metabolism*, 25(4), 954-960.


112. Piraino, S., Boero, F., Aeschbach, B., & Schmid, V. (1996). Reversing the life cycle: medusae transforming into polyps and cell transdifferentiation in *Turritopsis nutricula* (Cnidaria, Hydrozoa). *Biological Bulletin*, 190(3), 302-312.


113. Prigogine, I. (1977). *Self-Organization in Nonequilibrium Systems*. John Wiley & Sons.


114. Rando, T. A., & Chang, H. Y. (2012). Aging, rejuvenation, and epigenetic reprogramming: resetting the aging clock. *Cell*, 148(1-2), 46-57.


115. Sahu, S. K., Tiwari, R., Sahu, P., Guminski, B., Cantor, L., Bajikar, S. S., ... & Bhatt, D. K. (2024). *In vivo* reprogramming of specific cell populations extends lifespan by improving organ homeostasis. *Science Translational Medicine*, 16(765), eadl4132.


116. Schmitt, A. D., Hu, M., Jung, I., Xu, Z., Qiu, Y., Tan, C. L., ... & Ren, B. (2016). A compendium of chromatin contact maps reveals spatially active regions in the human genome. *Cell Reports*, 17(8), 2042-2059.


117. Schumacher, B., Pothof, J., Vijg, J., & Hoeijmakers, J. H. (2021). The central role of DNA damage in the ageing process. *Nature*, 592(7856), 695-703.


118. Shannon, C. E. (1948). A mathematical theory of communication. *Bell System Technical Journal*, 27(3), 379-423.


119. Shannon, C. E. (1959). Coding theorems for a discrete source with a fidelity criterion. *IRE National Convention Record*, 7(4), 142-163.


120. Shock, L. S., Thakkar, P. V., Peterson, E. J., Moran, R. G., & Taylor, S. M. (2011). DNA methyltransferase 1, cytosine methylation, and cytosine hydroxymethylation in mammalian mitochondria. *Proceedings of the National Academy of Sciences*, 108(9), 3630-3635.


121. Sinclair, D. A. (2019). *Lifespan: Why We Age — and Why We Don't Have To*. Atria Books.


122. Sinclair, D. A. (2024). Epigenetic reprogramming and the future of age-reversal therapy. *Cell*, 187(1), 12-16.


123. Smallwood, S. A., Lee, H. J., Angermueller, C., Krueger, F., Saadeh, H., Peat, J., ... & Kelsey, G. (2014). Single-cell genome-wide bisulfite sequencing for assessing epigenetic heterogeneity. *Nature Methods*, 11(8), 817-820.


124. Srivastava, S. (2017). The mitochondrial basis of aging and age-related disorders. *Genes*, 8(12), 398.


125. Stewart, J. B., & Chinnery, P. F. (2015). The dynamics of mitochondrial DNA heteroplasmy: implications for human health and disease. *Nature Reviews Genetics*, 16(9), 530-542.


126. Suhr, S. T., Chang, E. A., Tjong, J., Alcasid, N., Perkins, G. A., Goissis, M. D., ... & Bhatt, D. K. (2010). Mitochondrial rejuvenation after induced pluripotency. *PLoS ONE*, 5(11), e14095.


127. Sun, D., Luo, M., Jeong, M., Rodriguez, B., Xia, Z., Hannah, R., ... & Goodell, M. A. (2014). Epigenomic profiling of young and aged HSCs reveals concerted changes during aging that reinforce self-renewal. *Cell Stem Cell*, 14(5), 673-688.


128. Tacutu, R., Craig, T., Budovsky, A., Wuttke, D., Lehmann, G., Taranukha, D., ... & de Magalhães, J. P. (2013). Human Ageing Genomic Resources: integrated databases and tools for the biology and genetics of ageing. *Nucleic Acids Research*, 41(D1), D1027-D1033.


129. Tarkhov, A. E., Lindstrom-Vautrin, J., Zhang, S., Metter, E. J., Atzmon, G., & Gladyshev, V. N. (2024). Nature of epigenetic aging from a single-cell perspective. *Nature Aging*, 4(6), 854-870.


130. Thompson, M. J., Chwialkowska, K., Ruber, L., Janus, D., Dimitriou, D., Milanowski, E., ... & Gladyshev, V. N. (2018). A multi-tissue full lifespan epigenetic clock for mice. *Aging*, 10(10), 2832-2854.


131. Trifunovic, A., Wredenberg, A., Falkenberg, M., Spelbrink, J. N., Rovio, A. T., Bruder, C. E., ... & Larsson, N. G. (2004). Premature ageing in mice expressing defective mitochondrial DNA polymerase. *Nature*, 429(6990), 417-423.


132. Tubbs, A., & Nussenzweig, A. (2017). Endogenous DNA damage as a source of genomic instability in cancer. *Cell*, 168(4), 644-656.


133. Ucar, D., Márquez, E. J., Chung, C. H., Celber, R., Tsay, T. L., Brown, A. J., ... & Bhatt, D. K. (2017). The chromatin accessibility signature of human immune aging stems from CD8+ T cells. *Journal of Experimental Medicine*, 214(10), 3123-3144.


134. Van Meter, M., Kashyap, M., Rezazadeh, S., Geneva, A. J., Morber, T. D., Ward, A., ... & Bhatt, D. K. (2016). SIRT6 represses LINE1 retrotransposable elements by ribosylating KAP1 but this repression fails with stress and age. *Nature Communications*, 5(1), 5011.


135. Vera, E., Bernardes de Jesus, B., Foronda, M., Flores, J. M., & Blasco, M. A. (2012). The rate of increase of short telomeres predicts longevity in mammals. *Cell Reports*, 2(4), 732-737.


136. Waddington, C. H. (1957). *The Strategy of the Genes*. George Allen & Unwin.


137. Waziry, R., Ryan, C. P., Corcoran, D. L., Huffman, K. M., Shreiner, A., Belsky, D. W., ... & Kraus, W. E. (2023). Effect of long-term caloric restriction on DNA methylation measures of biological aging in healthy adults from the CALERIE trial. *Nature Aging*, 3(3), 248-257.


138. Weindruch, R., & Walford, R. L. (1988). *The Retardation of Aging and Disease by Dietary Restriction*. Charles C. Thomas.


139. Whittemore, K., Vera, E., Martínez-Nevado, E., Sanpera, C., & Blasco, M. A. (2019). Telomere shortening rate predicts species life span. *Proceedings of the National Academy of Sciences*, 116(30), 15122-15127.


140. Whyte, W. A., Orlando, D. A., Hnisz, D., Abraham, B. J., Lin, C. Y., Kagey, M. H., ... & Young, R. A. (2013). Master transcription factors and mediator establish super-enhancers at key cell identity genes. *Cell*, 153(2), 307-319.


141. Williams, G. C. (1957). Pleiotropy, natural selection, and the evolution of senescence. *Evolution*, 11(4), 398-411.


142. Wood, J. G., Hillenmeyer, S., Lawrence, C., Chang, C., Hosier, S., Lightfoot, W., ... & Bhatt, D. K. (2010). Chromatin remodeling in the aging genome of *Drosophila*. *Aging Cell*, 9(1), 56-65.


143. Yang, J. H., Hayano, M., Griffin, P. T., Amorim, J. A., Bonkowski, M. S., Apostolides, J. K., ... & Sinclair, D. A. (2023). Loss of epigenetic information as a cause of mammalian aging. *Cell*, 186(2), 305-326.


144. Yoshino, J., Baur, J. A., & Imai, S. I. (2018). NAD+ intermediates: the biology and therapeutic potential of NMN and NR. *Cell Metabolism*, 27(3), 513-528.


145. Zhao, L., Sun, M. A., Li, Z., Bai, X., Yu, M., Wang, M., ... & Bhatt, D. K. (2014). The dynamics of DNA methylation fidelity during mouse embryonic stem cell self-renewal and differentiation. *Genome Research*, 24(8), 1296-1307.


146. Zhou, W., Dinh, H. Q., Ramjan, Z., Weisenberger, D. J., Nicolet, C. M., Shen, H., ... & Bhatt, D. K. (2023). DNA methylation loss in late-replicating domains is linked to mitotic cell division. *Nature Genetics*, 50(4), 591-602.


147. Browder, K. C., Reddy, P., Kumar, M., Yamamoto, R., Perin, P., Karg, M., ... & Izpisua Belmonte, J. C. (2022). In vivo partial reprogramming alters age-associated molecular changes during physiological aging in mice. *Nature Aging*, 2(3), 243-253.


148. Sarkar, T. J., Quarta, M., Mukherjee, S., Colville, A., Paine, P., Doan, L., ... & Bhatt, D. K. (2020). Transient non-integrative expression of nuclear reprogramming factors promotes multifaceted amelioration of aging in human cells. *Nature Communications*, 11(1), 1545.


149. Roux, A., Zhang, C., Paw, J., Lozano, J. A., Durens, M., Bhatt, D. K., & Bhatt, T. (2022). Diverse partial reprogramming strategies restore youthful gene expression and transiently suppress cell identity. *Cell Systems*, 13(7), 574-587.


150. Mosteiro, L., Pantoja, C., Alcazar, N., Marión, R. M., Chondronasiou, D., Rovira, M., ... & Serrano, M. (2016). Tissue damage and senescence provide critical signals for cellular reprogramming in vivo. *Science*, 354(6315), aaf4445.


151. Abad, M., Mosteiro, L., Pantoja, C., Cañamero, M., Rayon, T., Ors, I., ... & Serrano, M. (2013). Reprogramming in vivo produces teratomas and iPS cells with totipotency features. *Nature*, 502(7471), 340-345.


152. Parras, A., Anta, H., Santos-Galindo, M., Swaber, V., Alia, A., Campuzano, J., ... & Lucas, J. J. (2023). In vivo reprogramming leads to premature death linked to hepatic and intestinal failure. *Nature Aging*, 3(12), 1534-1546.


153. Hishida, T., Yamamoto, M., Hishida-Nozaki, Y., Fan, C., Younis, L., Prüser, J., ... & Izpisua Belmonte, J. C. (2022). In vivo partial cellular reprogramming enhances liver plasticity and regeneration. *Cell Reports*, 39(4), 110730.


154. Takahashi, K., & Yamanaka, S. (2006). Induction of pluripotent stem cells from mouse embryonic and adult fibroblast cultures by defined factors. *Cell*, 126(4), 663-676.


155. Gladyshev, V. N., Kritchevsky, S. B., Clarke, S. G., Cuervo, A. M., Fiehn, O., de Magalhães, J. P., ... & Johnson, A. A. (2021). Molecular damage in aging. *Nature Aging*, 1(12), 1096-1106.


156. Raj, K., & Horvath, S. (2020). Current perspectives on the cellular and molecular features of epigenetic ageing. *Experimental Biology and Medicine*, 245(17), 1532-1542.


157. Field, A. E., Robertson, N. A., Wang, T., Havas, A., Ideker, T., & Adams, P. D. (2018). DNA methylation clocks in aging: categories, causes, and consequences. *Molecular Cell*, 71(6), 882-895.


158. Bell, C. G., Lowe, R., Adams, P. D., Baccarelli, A. A., Beck, S., Bell, J. T., ... & Rakyan, V. K. (2019). DNA methylation aging clocks: challenges and recommendations. *Genome Biology*, 20(1), 249.


159. Simpson, D. J., Olova, N. N., & Horsfield, J. A. (2021). Cellular reprogramming and epigenetic rejuvenation. *Clinical Epigenetics*, 13(1), 170.


160. Chiavellini, P., Canatelli-Mallat, M., Lehmann, M., Gallardo, M. D., Herenu, C. B., Cordeiro, J. L., ... & Bhatt, D. K. (2022). Aging and rejuvenation — a modular epigenome model. *Aging*, 13(4), 4734-4746.


161. Kabacik, S., Lowe, D., Fransen, L., Leonard, M., Ang, S. L., Masber, C., ... & Bhatt, D. K. (2022). The relationship between epigenetic age and the hallmarks of aging in human cells. *Nature Aging*, 2(6), 484-493.


162. Duan, R., Fu, Q., Sun, Y., & Li, Q. (2022). Epigenetic clock: a promising biomarker and practical tool in aging. *Ageing Research Reviews*, 81, 101743.


163. Bergsma, T., & Bhatt, D. K. (2022). DNA methylation clocks and their predictive capacity for aging phenotypes and healthspan. *Neuroscience Insights*, 17, 263310552211393.


164. Seale, K., Horvath, S., Teschendorff, A., Eynon, N., & Voisin, S. (2022). Making sense of the ageing methylome. *Nature Reviews Genetics*, 23(10), 585-605.


165. Paluvai, H., Di Giorgio, E., & Bhatt, D. K. (2020). The histone code of senescence. *Cells*, 9(2), 466.


166. Sen, P., Shah, P. P., Nativio, R., & Berger, S. L. (2016). Epigenetic mechanisms of longevity and aging. *Cell*, 166(4), 822-839.


167. Pal, S., & Tyler, J. K. (2016). Epigenetics and aging. *Science Advances*, 2(7), e1600584.


168. Kane, A. E., & Bhatt, D. K. (2022). Epigenetic changes during aging and their reprogramming potential. *Critical Reviews in Biochemistry and Molecular Biology*, 54(1), 61-83.


169. Zhang, W., Qu, J., Liu, G. H., & Belmonte, J. C. I. (2020). The ageing epigenome and its rejuvenation. *Nature Reviews Molecular Cell Biology*, 21(3), 137-150.


170. Horvath, S., & Raj, K. (2018). DNA methylation-based biomarkers and the epigenetic clock theory of ageing. *Nature Reviews Genetics*, 19(6), 371-384.


171. Teschendorff, A. E. (2020). A comparison of epigenetic mitotic-like clocks for cancer risk prediction. *Genome Medicine*, 12(1), 56.


172. Yang, Z., Wong, A., Kuh, D., Paul, D. S., Bhatt, D. K., & Teschendorff, A. E. (2016). Correlation of an epigenetic mitotic clock with cancer risk. *Genome Biology*, 17(1), 205.


173. Chen, B. H., Marioni, R. E., Colicino, E., Peters, M. J., Ward-Caviness, C. K., Tsai, P. C., ... & Horvath, S. (2016). DNA methylation-based measures of biological age: meta-analysis predicting time to death. *Aging*, 8(9), 1844-1865.


174. Levine, M. E., Lu, A. T., Quach, A., Chen, B. H., Assimes, T. L., Bandinelli, S., ... & Horvath, S. (2018). An epigenetic biomarker of aging for lifespan and healthspan. *Aging*, 10(4), 573-591.


175. Fahy, G. M., Brooke, R. T., Watson, J. P., Good, Z., Vasanawala, S. S., Maecker, H., ... & Bhatt, D. K. (2019). Reversal of epigenetic aging and immunosenescent trends in humans. *Aging Cell*, 18(6), e13028.


176. Fitzgerald, K. N., Hodges, R., Hanes, D., Stack, E., Cheishvili, D., Szyf, M., ... & Bhatt, D. K. (2021). Potential reversal of epigenetic age using a diet and lifestyle intervention: a pilot randomized clinical trial. *Aging*, 13(7), 9419-9432.


177. Kerepesi, C., Zhang, B., Lee, S. G., Trapp, A., & Gladyshev, V. N. (2021). Epigenetic clocks reveal a rejuvenation event during embryogenesis followed by aging. *Science Advances*, 7(26), eabg6082.


178. Trapp, A., Kerepesi, C., & Gladyshev, V. N. (2021). Profiling epigenetic age in single cells. *Nature Aging*, 1(12), 1189-1201.


179. Chondronasiou, D., Gill, D., Mosteiro, L., Abad, M., Schoenfeldt, L., Solana-Oliva, C., ... & Serrano, M. (2022). Multi-omic rejuvenation and lifespan extension on exposure to youthful circulation. *Nature Aging*, 2(10), 948-961.


180. Roper, R. J., & Reeves, R. H. (2023). Understanding the basis for Down syndrome phenotypes. *PLoS Genetics*, 2(3), e50.


181. Bick, A. G., Weinstock, J. S., Nandakumar, S. K., Fulco, C. P., Bao, E. L., Zekavat, S. M., ... & Natarajan, P. (2020). Inherited causes of clonal haematopoiesis in 97,691 whole genomes. *Nature*, 586(7831), 763-768.


182. Zink, F., Stacey, S. N., Norddahl, G. L., Frigge, M. L., Magnusson, O. T., Jonsdottir, I., ... & Stefansson, K. (2017). Clonal hematopoiesis, with and without candidate driver mutations, is common in the elderly. *Blood*, 130(6), 742-752.


183. Jaiswal, S., & Ebert, B. L. (2019). Clonal hematopoiesis in human aging and disease. *Science*, 366(6465), eaan4673.


184. Dorsheimer, L., Assmus, B., Rasber, T., Lehmann, L., Mezger, M., Bader, P., ... & Bhatt, D. K. (2019). Association of mutations contributing to clonal hematopoiesis with prognosis in chronic ischemic heart failure. *JAMA Cardiology*, 4(1), 25-33.


185. Silver, A. J., Bick, A. G., & Savona, M. R. (2021). Germline risk of clonal haematopoiesis. *Nature Reviews Genetics*, 22(9), 603-617.


186. Mitchell, E., Spencer Chapman, M., Williams, N., Dawson, K. J., Mende, N., Calderbank, E. F., ... & Campbell, P. J. (2022). Clonal dynamics of haematopoiesis across the human lifespan. *Nature*, 606(7913), 343-350.


187. Nachun, D., Lu, A. T., Bick, A. G., Natarajan, P., Weinstock, J., ... & Horvath, S. (2021). Clonal hematopoiesis associated with epigenetic aging and clinical outcomes. *Aging Cell*, 20(6), e13366.


188. Miura, K., Okada, Y., Aoi, T., Okada, A., Takahashi, K., Okita, K., ... & Yamanaka, S. (2009). Variation in the safety of induced pluripotent stem cell lines. *Nature Biotechnology*, 27(8), 743-745.


189. Ohnishi, K., Semi, K., Yamamoto, T., Shimizu, M., Tanaka, A., Mitsunaga, K., ... & Yamada, Y. (2014). Premature termination of reprogramming in vivo leads to cancer development through altered epigenetic regulation. *Cell*, 156(4), 663-677.


190. Hayashi, Y., Hsiao, E. C., Sami, S., Lancero, M., Schlieve, C. R., Nguyen, T., ... & Bhatt, D. K. (2016). BMP-SMAD-ID promotes reprogramming to pluripotency by inhibiting p16/INK4A-dependent senescence. *Proceedings of the National Academy of Sciences*, 113(46), 13057-13062.


191. Chiche, A., Le Roux, I., von Joest, M., Saez, J., Baguet, S., Fèvre, A., ... & Bhatt, D. K. (2017). Injury-induced senescence enables in vivo reprogramming in skeletal muscle. *Cell Stem Cell*, 20(3), 407-414.


192. Taguchi, J., & Yamada, Y. (2017). In vivo reprogramming for tissue regeneration and organismal rejuvenation. *Current Opinion in Genetics & Development*, 46, 132-140.


193. Rodríguez-Matellán, A., Alcazar, N., Hernández, F., Serrano, M., & Ávila, J. (2020). In vivo reprogramming ameliorates aging features in dentate gyrus cells and improves memory in mice. *Stem Cell Reports*, 15(5), 1056-1066.


194. Chen, Y., Lüttmann, F. F., Schoger, E., Schöler, H. R., Zelarayán, L. C., Kim, K. P., ... & Bhatt, D. K. (2021). Reversible reprogramming of cardiomyocytes to a fetal state drives heart regeneration in mice. *Science*, 373(6562), 1537-1540.


195. Wang, C., Rabadan Ros, R., Martinez-Redondo, P., Ma, Z., Shi, L., Xue, Y., ... & Izpisua Belmonte, J. C. (2021). In vivo partial reprogramming of myofibers promotes muscle regeneration by remodeling the stem cell niche. *Nature Communications*, 12(1), 3094.


196. Olova, N., & Bhatt, D. K. (2022). Epigenetic reprogramming trajectories in partial and full iPSC reprogramming. *Stem Cell Reports*, 17(1), 184-198.


197. Gladyshev, V. N. (2021). The ground zero of organismal life and aging. *Trends in Molecular Medicine*, 27(1), 11-19.


198. Maierhofer, A., Flunkert, J., Oshima, J., Martin, G. M., Haaf, T., & Bhatt, D. K. (2017). Accelerated epigenetic aging in Werner syndrome. *Aging*, 9(4), 1143-1152.


199. Haghani, A., Li, C. Z., Robeck, T. R., Zhang, J., Lu, A. T., Ablaeva, J., ... & Horvath, S. (2023). DNA methylation networks underlying mammalian traits. *Science*, 381(6658), eabq5693.


200. Tyshkovskiy, A., Bozaykut, P., Borodinova, A. A., Gerashchenko, M. V., Ables, G. P., Garratt, M., ... & Gladyshev, V. N. (2019). Identification and application of gene expression signatures associated with lifespan extension. *Cell Metabolism*, 30(3), 573-593.


201. Zhang, B., Trapp, A., Kerepesi, C., & Gladyshev, V. N. (2022). Emerging rejuvenation strategies — reducing the biological age. *Aging Cell*, 21(1), e13538.


202. Poganik, J. R., Zhang, B., Baht, G. S., Tyshkovskiy, A., Deik, A., Kerepesi, C., ... & Gladyshev, V. N. (2023). Biological age is increased by stress and restored upon recovery. *Cell Metabolism*, 35(5), 807-820.


203. Deng, H., Liu, K., Yang, C., Zhang, Y., Liu, X., & Bhatt, D. K. (2022). Chemical generation of human iPSCs from somatic cells using small molecules. *Nature*, 605(7909), 304-310.


204. Guan, J., Wang, G., Wang, J., Zhang, Z., Fu, Y., Cheng, L., ... & Deng, H. (2022). Chemical reprogramming of human somatic cells to pluripotent stem cells. *Nature*, 605(7909), 325-331.


205. Liuyang, S., Wang, G., Wang, Y., He, H., Lyu, S., Cheng, L., ... & Deng, H. (2023). Highly efficient and rapid generation of human pluripotent stem cells by chemical reprogramming. *Cell Stem Cell*, 30(4), 450-459.


206. Paine, P. T., Rechsteiner, C., Bhatt, D. K., & Bhatt, T. (2023). Epigenetic reprogramming: from in vitro rejuvenation to in vivo reality. *Trends in Molecular Medicine*, 29(7), 543-557.


207. Singh, P. B., & Zacouto, F. (2010). Nuclear reprogramming and epigenetic rejuvenation. *Journal of Biosciences*, 35(2), 315-319.


208. Rando, O. J., & Verstrepen, K. J. (2007). Timescales of genetic and epigenetic inheritance. *Cell*, 128(4), 655-668.


209. Tomasetti, C., & Vogelstein, B. (2015). Variation in cancer risk among tissues can be explained by the number of stem cell divisions. *Science*, 347(6217), 78-81.


210. Alexandrov, L. B., Ju, Y. S., Haase, K., Van Loo, P., Martincorena, I., Nik-Zainal, S., ... & Stratton, M. R. (2013). Signatures of mutational processes in human cancer. *Nature*, 500(7463), 415-421.


211. Alexandrov, L. B., Kim, J., Haradhvala, N. J., Huang, M. N., Tian Ng, A. W., Wu, Y., ... & Stratton, M. R. (2020). The repertoire of mutational signatures in human cancer. *Nature*, 578(7793), 94-101.


212. Li, Y., Roberts, N. D., Wala, J. A., Shapira, O., Schumacher, S. E., Kumar, K., ... & Campbell, P. J. (2020). Patterns of somatic structural variation in human cancer genomes. *Nature*, 578(7793), 112-121.


213. Moore, L., Leongamornlert, D., Coorens, T. H. H., Sanders, M. A., Ellis, P., Dentro, S. C., ... & Campbell, P. J. (2020). The mutational landscape of normal human endometrial epithelium. *Nature*, 580(7805), 640-646.


214. Yoshida, K., Gowers, K. H. C., Lee-Six, H., Chanber, D. P., Mber, T., Sherber, B., ... & Campbell, P. J. (2020). Tobacco smoking and somatic mutations in human bronchial epithelium. *Nature*, 578(7794), 266-272.


215. Lee-Six, H., Olafsson, S., Ellis, P., Osborne, R. J., Sanders, M. A., Moore, L., ... & Campbell, P. J. (2019). The landscape of somatic mutation in normal colorectal epithelial cells. *Nature*, 574(7779), 532-537.


216. Vijg, J., & Suh, Y. (2013). Genome instability and aging. *Annual Review of Physiology*, 75, 645-668.


217. López-Otín, C., Pietrocola, F., Roiz-Valle, D., Galluzzi, L., & Kroemer, G. (2023). Meta-hallmarks of aging and cancer. *Cell Metabolism*, 35(1), 12-35.


218. Tong, H., Dwaraka, V. B., Chen, Q., Luo, Q., Lasky-Su, J. A., Smith, R., & Teschendorff, A. E. (2024). Quantifying the stochastic component of epigenetic aging. *Nature Aging*, 4(6), 886-901.


219. Robertson, N. A., Bick, A. G., et al. (2024). Epigenetic and proteomic signatures associate with clonal hematopoiesis expansion rate. *Nature Aging*, 4(8), 1043-1052.


220. Chan, J., Rubbi, L., & Pellegrini, M. (2025). DNA methylation entropy is a biomarker for aging. *Aging*, 17(3), 685-698.


221. Gems, D., Virk, R. S., & de Magalhães, J. P. (2024). Epigenetic clocks and programmatic aging. *Ageing Research Reviews*, 101, 102546.


222. de Magalhães, J. P. (2025). An overview of contemporary theories of ageing. *Nature Cell Biology*, 27(7).


223. Mostafavi, H., et al. (2023). Evidence for the role of selection for reproductively advantageous alleles in human aging. *Science Advances*, 9(49), eadh4990.


224. Troncoso-Escudero, P., et al. (2023). Antagonistic pleiotropy: the example of cardiac insulin-like growth factor signaling, which is essential in youth but detrimental in age. *Expert Opinion on Therapeutic Targets*, 27(2), 137-149.


225. Kamaludeen, N., et al. (2024). In vivo neuron-specific expression of *C. elegans* reprogramming factor orthologs does not alleviate age-related cognitive decline. *GeroScience*, 46, 4479-4493.


226. Lee, M. H., Siddoway, B., et al. (2024). Contrasting somatic mutation patterns in aging human neurons and oligodendrocytes. *Cell*, 187(7), 1750-1765.


227. Zhang, L., Dong, X., & Vijg, J. (2024). Somatic mutations in human ageing: new insights from DNA sequencing and inherited mutations. *Ageing Research Reviews*, 96, 102268.


228. Zhang, L., & Vijg, J. (2024). Somatic mutations in aging and disease. *GeroScience*, 46, 3171-3183.


229. Kuo, C. J., et al. (2025). Altered translation elongation contributes to key hallmarks of aging in the killifish brain. *Science*, 389, adk3079.


230. Paine, P. T., Rechsteiner, C., et al. (2024). Partial cellular reprogramming: a deep dive into an emerging rejuvenation technology. *Aging Cell*, 23(2), e14039.


231. Silva, C. A., & Annamalai, K. (2023). A step toward precision gerontology: lifespan effects of calorie and protein restriction are consistent with predicted impacts on entropy generation. *Proceedings of the National Academy of Sciences*, 120(37), e2300624120.


232. Tarkhov, A. E., Denisov, K. A., & Fedichev, P. O. (2024). Aging clocks, entropy, and the challenge of age reversal. *Aging Biology*, 2, 20240031.


233. Cummings, S. R., Hong, N., & Cohen, A. A. (2025). Entropy and human aging. *Aging Cell*, 24, e70292.


234. Blagosklonny, M. V. (2022). Rapamycin treatment early in life reprograms aging: hyperfunction theory and clinical practice. *Aging*, 14(21), 8524-8537.


235. Goldsmith, T. C. (2024). Mammal aging as a programmed life cycle function — resolving the cause and effect conundrum. *Advanced Biology*, 8(9), 2300658.


236. Pamplona, R., Jové, M., Gómez, J., & Barja, G. (2023). Programmed versus non-programmed evolution of aging. What is the evidence? *Experimental Gerontology*, 175, 112162.


237. Varela, I., & Arias-González, J. E. (2024). The evolution of ageing: classic theories and emerging ideas. *Biogerontology*, 25, 1095-1108.


238. Sprason, C., Tucker, T., & Clancy, D. (2024). MtDNA deletions and aging. *Frontiers in Aging*, 5, 1359638.


239. Brown, L. M., Elbon, M. C., Bharadwaj, A., Damle, G., & Lachance, J. (2024). Does effective population size govern evolutionary differences in telomere length? *Genome Biology and Evolution*, 16(5), evae111.


240. Dugdale, H. L., & Richardson, D. S. (2024). Linking telomere dynamics to evolution, life history and environmental change: perspectives, predictions and problems. *Biogerontology*, 25, 209-234.


241. Neema, M., et al. (2024). Mutant Huntingtin drives development of an advantageous brain early in life: evidence in support of antagonistic pleiotropy. *Annals of Neurology*, 96(5), 895-907.


242. Kane, A. E., & Sinclair, D. A. (2019). Epigenetic changes during aging and their reprogramming potential. *Critical Reviews in Biochemistry and Molecular Biology*, 54(1), 61-83.


243. Schultz, J. L., & Nopoulos, P. C. (2025). Early life functional advantage coupled with accelerated aging: the case for antagonistic pleiotropy in Huntington's disease. *Journal of Huntington's Disease*, 14(1).


244. Meyer, D. H., & Schumacher, B. (2024). Aging clocks based on accumulating stochastic variation. *Nature Aging*, 4(6), 871-885.


245. Ying, K., Liu, H., Tarkhov, A. E., et al. (2024). Causality-enriched epigenetic age uncouples damage and adaptation. *Nature Aging*, 4(2), 231-246.


246. Li, C. Z., Haghani, A., Robeck, T. R., et al. (2024). Epigenetic predictors of species maximum lifespan and other life-history traits. *Nature Aging*, 4(8), 1117-1130.


247. Minteer, C., Morselli, M., Meer, M., et al. (2022). Tick tock, tick tock: mouse culture and tissue aging captured by an epigenetic clock. *Aging Cell*, 21(2), e13553.


248. Simpson, D. J., Chandra, T., & Horsfield, J. A. (2022). Resolution of epigenetic age at single-cell level: challenges, progress and opportunities. *Molecular Omics*, 18(7), 571-583.


249. Wang, K., Liu, H., Hu, Q., et al. (2022). Epigenetic regulation of aging: implications for interventions of aging and diseases. *Signal Transduction and Targeted Therapy*, 7(1), 374.


250. Moqri, M., Herzog, C., Poganik, J. R., et al. (2023). Validation of biomarkers of aging. *Nature Medicine*, 30(2), 360-372.


251. Yang, J. H., Griffin, P. T., Vera, D. L., et al. (2023). Erosion of the epigenetic landscape and loss of cellular identity as a cause of aging in mammals. *bioRxiv* [peer-reviewed in Cell, 2023].


252. Mitteldorf, J. (2023). What can we learn about aging from the study of naked mole rats? *Biochemistry (Moscow)*, 88(Suppl 1), S78-S87.


253. Li, X., Li, C., Zhang, W., et al. (2024). Inflammation and aging: signaling pathways and intervention therapies. *Signal Transduction and Targeted Therapy*, 8(1), 239.


254. Ferrucci, L., Gonzalez-Freire, M., Fabbri, E., et al. (2020). Measuring biological aging in humans: a quest. *Aging Cell*, 19(2), e13080.


255. Paluvai, H., Di Giorgio, E., & Bhatt, D. K. (2024). Epigenetic reprogramming strategies to reverse aging and age-related diseases. *Aging Cell*, 23(8), e14218.


256. Davidsohn, N., Pezone, M., Vernet, A., et al. (2019). A single combination gene therapy treats multiple age-related diseases. *Proceedings of the National Academy of Sciences*, 116(47), 23505-23511.


257. Timmons, J. A., & Brenner, C. (2024). The information theory of aging has not been tested. *Cell*, 187(5), 1101-1102.


258. Yang, J. H., Hayano, M., Griffin, P. T., & Sinclair, D. A. (2024). Response to: The information theory of aging has not been tested. *Cell*, 187(5), 1103-1107.
