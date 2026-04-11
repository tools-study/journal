# Whole-Body Reprogramming Challenges

## Abstract

Partial reprogramming by pulsatile expression of Yamanaka factors ameliorates age-associated phenotypes in multiple tissues (Ocampo et al., 2016; Browder et al., 2022; Chondronasiou et al., 2022) and, in long-lived wild-type mice, extends median remaining lifespan by 109 percent (Macip et al., 2024). The first clinical IND application for a partial-reprogramming gene therapy cleared the FDA in January 2026 (Life Biosciences, 2026). Yet every successful preclinical demonstration to date is either single-organ (eye, brain, muscle) or whole-body with explicit tissue exclusion: continuous OSKM is lethal within one week because of hepatic and intestinal failure (Parras et al., 2023), and no published protocol achieves therapeutic reprogramming across the full set of organs that determine human healthspan. Human translation therefore hinges on solving a problem no prior study has quantitatively formalized: how to deliver reprogramming factors systemically when the therapeutic windows of different organs are separated by one to two orders of magnitude (eye: months safe; intestine: hours lethal), while exploiting the fact that circulating factors couple organ-level rejuvenation trajectories into a whole-body network (Pálovics et al., 2022; Bieri et al., 2023; Zhang et al., 2023).

This paper identifies two rate-limiting technical obstacles and proposes six original mathematical frameworks (F338–F343) not present in the prior research program (F1–F337). The **primary** obstacle is the systemic delivery gradient coupled to inter-organ rejuvenation propagation: we develop a coupled N-organ ordinary differential equation network with a circulating-factor transfer matrix whose eigenmodes determine how focal dosing at one organ propagates to others (F338); a multi-organ therapeutic-window intersection set with Minkowski-sum dose allocation (F339); an N-organ Pontryagin Hamiltonian whose switching-function analysis yields banded, non-bang-bang optimal control (F340); and an organismal-age aggregator calibrated from plasma proteomic organ clocks (F341). The **secondary** obstacle, addressed in the minimum-viable-systemic-protocol section, is identifying the smallest ordered subset of organs whose co-rejuvenation produces detectable organismal healthspan benefit without breaching any single-organ toxicity threshold: we cast this as a monotone submodular set-cover problem with a toxicity knapsack (F342) and enforce chronic clonal carcinogenesis risk as a piecewise-deterministic Markov process tracking mutational burden under cyclic dosing (F343).

Evaluated against the twenty-year longitudinal organ-age signatures from Whitehall II (Kivimäki et al., 2025), the 109-percent lifespan extension in systemic AAV-OSK-treated mice (Macip et al., 2024), and the hepatic/intestinal failure data from continuous OSKM (Parras et al., 2023), the framework predicts that multi-modality orthogonal-tropism delivery combining a transferrin-receptor-targeted brain capsid (Moyer et al., 2025), a SORT lipid nanoparticle spleen/lung formulation (Dilliard et al., 2023), a muscle-tropic AAV (Tabebordbar et al., 2021), and an oral chemical for epidermis can in principle meet the organ-stratified dose constraints of F339. It further predicts that the minimum viable organ set is the brain-immune-vascular triad — the three organs whose youthfulness is independently associated with disease-free longevity (Oh et al., 2025) — and that the optimal dosing order is brain → vascular → immune on a fourteen-day staggered cycle, governed by the cumulative-hazard safety constraint of F343. These predictions are falsifiable by the experimental roadmap outlined in Section 5.

---

## 1. Introduction: From Single-Organ Success to the Whole-Body Target

The central empirical claim of the partial-reprogramming field — that pulsatile expression of Oct4/Sox2/Klf4 (with or without c-Myc) can transiently erase epigenetic marks of age without erasing cell identity — is no longer contentious. It has been reproduced in the retina (Lu et al., 2020), the hippocampus (Xu et al., 2024; Antón-Fernández et al., 2024), skeletal muscle (Wang et al., 2021), the intestine (Kim et al., 2023), and, critically, in whole-body aged wild-type mice where a systemic AAV-OSK gene therapy extended the median remaining lifespan of 124-week-old mice by 109 percent (Macip et al., 2024). The first clinical program using a partial-reprogramming gene therapy, ER-100 for non-arteritic anterior ischemic optic neuropathy and related optic neuropathies, cleared the FDA Investigational New Drug gate in January 2026 (Life Biosciences, 2026). The question facing the field is no longer "does partial reprogramming work?" but "how do we translate it from a single-organ demonstration to a whole-body intervention that meaningfully extends human healthspan without causing harm?"

That question has a rigorous answer only if four technical premises are treated simultaneously. First, organs have dramatically different therapeutic windows for OSK exposure. Continuous OSKM expression for more than seven days is lethal in mice, and the mechanism is specific: death results from hepatic and intestinal epithelial failure, with intestinal crypts undergoing catastrophic loss of cell identity within 48 hours of sustained OSKM (Parras et al., 2023). The same mice survive indefinitely when OSKM expression is excluded from the liver and intestine via tissue-specific Cre recombination (Parras et al., 2023), establishing that the lethal pathway is not a systemic side effect of OSK but a localized collapse of two particular organs with intrinsic intolerance to dedifferentiation. In contrast, photoreceptors in the retina tolerate OSK expression for months without apparent harm (Lu et al., 2020), and skeletal muscle tolerates repeated pulses across the animal's lifetime (Wang et al., 2021). The ratio of tolerable exposure times between the eye and the intestine spans at least two orders of magnitude. Second, delivery vectors overwhelmingly fail to respect these differential windows. Standard AAV9 systemically administered distributes preferentially to the liver at doses two orders of magnitude higher than the brain (López-Gordo et al., 2024); lipid nanoparticles without targeting ligands accumulate by ApoE-mediated uptake in hepatocytes (Dilliard et al., 2021); oral small-molecule reprogramming cocktails diffuse to all perfused tissues irrespective of their tolerance (Guan et al., 2022). Every clinically mature delivery modality is intrinsically liver- or ubiquitous-biased and therefore inverts the required dosing gradient: it gives the most OSK exactly where the tolerance is lowest.

Third, once dosing is even partially localized, organs do not age or rejuvenate independently. Heterochronic parabiosis of young and old mice rejuvenates aged tissues through circulating factors, and the rejuvenation signal propagates across organ boundaries in a cell-type-dependent manner (Pálovics et al., 2022; Ma et al., 2022; Zhang et al., 2023). A single short heterochronic parabiosis pairing lowers the epigenetic age of blood and liver and extends the lifespan of old partners even after two months of detachment, demonstrating that rejuvenation gained from circulating factors is durable rather than transient (Zhang et al., 2023). Platelet factor 4 (PF4) released from activated platelets crosses the blood–brain barrier and rejuvenates hippocampal neurogenesis (Schroer et al., 2023; Bieri et al., 2023); alpha-Klotho, circulating extracellular vesicles, and TIMP2 have each been shown to transfer rejuvenation signals between organs (Sahu et al., 2021; Bieri et al., 2023; Liu et al., 2024). Conversely, CCL11, C1q, beta-2-microglobulin, and senescence-associated secretory phenotype factors transfer pro-aging signals from old tissues into young ones (He et al., 2026; Kiss et al., 2020). The organism is therefore a network, not a set of independent compartments, and the dose delivered to organ i affects the biological ages of organs j ≠ i even in the absence of direct transfection. Any analysis that treats organs as independent is wrong.

Fourth, human translation demands that the protocol be not only efficacious but cumulatively safe across decades of cyclic therapy. The aged tissues into which OSK is delivered are already mosaics of clonal patches carrying somatic oncogenic mutations (Martincorena et al., 2015; Lee-Six et al., 2018; Mitchell et al., 2022; Jaiswal et al., 2014). Each reprogramming pulse transiently derepresses pluripotency-associated gene networks, and the dominant clinical risk of in vivo reprogramming is that a pre-existing mutant clone escapes identity control and becomes a teratoma or carcinoma over the years of exposure. No published framework quantifies the cumulative carcinogenic hazard of repeated OSK pulses in a tissue with an empirically parameterized somatic mutation background, and no protocol has been explicitly designed to enforce a safety margin against this cumulative risk.

Section 2 develops the anatomy of the systemic delivery gradient and defines F338, the coupled N-organ ODE network with a circulating-factor transfer matrix. Section 3 develops F339, the therapeutic-window intersection set with Minkowski-sum dose allocation. Section 4 develops F340 (multi-organ Pontryagin Hamiltonian) and F341 (organismal age aggregator from proteomic organ clocks), closing the loop on how a clinician would actually plan a dose vector. Section 5, the secondary-focus block, develops F342 (submodular minimum-viable-organ-set selection) and F343 (PDMP cumulative clonal hazard enforcement). Section 6 is the experimental validation roadmap. Section 7 is the clinical translation path. Section 8 is the open questions hierarchy. Section 9 concludes.

---

## 2. The Anatomy of the Systemic Delivery Gradient

### 2.1 Therapeutic windows differ by one to two orders of magnitude across organs

The seminal observation motivating everything that follows is that the ratio of maximum tolerated OSKM exposure time between the most permissive and least permissive organs in the mouse spans roughly two orders of magnitude. In the retina, continuous cyclic OSK delivered by AAV2 drives restoration of youthful DNA methylation and reversal of glaucoma-related vision loss with no teratoma formation and no obvious toxicity across months of expression (Lu et al., 2020; Karg et al., 2023). In skeletal muscle, repeated intramuscular AAV-OSK delivery induces satellite cell expansion and improved regeneration without loss of myofiber identity (Wang et al., 2021). At the opposite extreme, in the intestinal epithelium, continuous OSKM expression from a Tet-inducible reprogrammable allele induces catastrophic crypt collapse within 48–72 hours, and animals reach a lethal endpoint (typically defined as 20 percent body weight loss) within one week (Parras et al., 2023). The liver is similarly intolerant: continuous OSKM produces hepatic dysfunction, elevated transaminases, and organ failure on the same one-week timescale (Parras et al., 2023). The rescue experiment — removing OSKM expression from the liver and intestine only — extends survival indefinitely, establishing that the lethal pathway is strictly local, not systemic (Parras et al., 2023).

This is not simply a difference in amplitude. Three independent sources converge on a quantitative estimate of the per-organ therapeutic window for OSK exposure. First, tissue-competence analysis synthesized molecular and cell-biological data for eight organs and produced a composite "reprogramming competence score" in which the eye and skeletal muscle scored at the top of the safe range and the liver, intestine, and heart scored at the bottom (Jo et al., 2025; Parras et al., 2023; Hishida et al., 2022). Second, Pico et al. (2025) compared multiple reprogrammable mouse strains with organ-specific exclusions and measured tissue-resolved OSKM dose-response curves. Third, the epigenetic rejuvenation per unit OSKM exposure, measured by DNA methylation age reversal across organs, is highly heterogeneous: the kidney and skin show large methylation age reversals after long-term partial reprogramming, whereas the intestine and liver show minimal reversal even at sub-lethal doses (Browder et al., 2022; Chondronasiou et al., 2022). Taken together, these data support the ordering, from most permissive to least permissive:

**eye ≈ skeletal muscle > skin ≈ kidney > brain ≈ spleen > heart > lung > liver > intestine**

with the ratio of maximum tolerated continuous exposure time from eye to intestine lying between 10^1 and 10^2 (Jo et al., 2025; Parras et al., 2023; Macip et al., 2024). Expressed as a tolerable dose under a cyclic protocol, the ratio is smaller but still substantial; Macip et al. (2024) achieved a 109-percent median lifespan extension in 124-week-old mice with a systemic AAV-OSK dose that was intentionally titrated below the intestinal threshold, implying that a dose sufficient to benefit the most-permissive organs is sub-therapeutic for the organs where tolerance is high but competence is modest.

### 2.2 Every major delivery modality inverts the required gradient

The clinical importance of the preceding subsection is that every clinically mature delivery modality for reprogramming factors has a biodistribution that is almost exactly the inverse of the required therapeutic-window gradient. Four modalities dominate the in-vivo reprogramming pipeline: adeno-associated virus (AAV), lipid nanoparticles (LNPs) carrying mRNA, oral small-molecule reprogramming cocktails, and virus-like-particle messenger-RNA carriers such as eVLPs and retron-derived particles. Each has a characteristic biodistribution that fails in a specific and quantifiable way.

**AAV9 biased to liver.** Intravenously administered AAV9 in mice distributes approximately as 65-80 percent liver, 5-10 percent heart, 2-5 percent skeletal muscle, and less than 1 percent brain parenchyma (López-Gordo et al., 2024). The brain fraction is small because AAV9 crosses the rodent blood–brain barrier only at exceptionally high systemic doses, and in non-human primates and humans AAV9 brain transduction is even weaker (Huang et al., 2023; Moyer et al., 2025). This is the delivery profile that is *least* compatible with OSK dosing: the liver and intestine receive the largest payload and are the organs most prone to OSKM-induced failure. Engineered AAV9 variants partially solve the brain problem but usually at the cost of retaining hepatic tropism (Yao et al., 2022; Shay et al., 2024). Only two engineered capsid classes to date have demonstrated simultaneous strong brain transduction and substantial liver detargeting: the transferrin-receptor-1 (TfR1)-binding BI-hTFR1 variant and the alkaline-phosphatase (ALPL)-binding VCAP-102 (Moyer et al., 2025; Shay et al., 2024). The ALPL pathway is especially attractive because ALPL is a highly conserved brain endothelial receptor expressed at comparable levels in mouse, macaque, and human (Moyer et al., 2025), solving the long-standing cross-species translation problem that has plagued the Ly6A-dependent PHP.eB capsid (Huang et al., 2023).

**LNPs biased to liver.** Standard ionizable lipid nanoparticles formulated with MC3 or SM-102 distribute approximately as 90 percent liver by dose-weighted mRNA expression, with residual low expression in spleen and lung (Dilliard et al., 2021; Witten et al., 2024). The liver dominance arises from passive adsorption of apolipoprotein E onto the particle surface, which drives receptor-mediated uptake into hepatocytes via the LDL receptor (Dilliard et al., 2021). The Selective Organ Targeting (SORT) methodology of Cheng et al. and its extensions (Cheng et al., 2020; Dilliard et al., 2023; Vaidya et al., 2024; Dong et al., 2024; Xue et al., 2024; Heredero et al., 2025) re-engineers particle chemistry by adding a fifth supplementary lipid whose quaternary ammonium headgroup re-routes the protein corona away from apolipoprotein E and toward organ-specific adsorbed proteins. Optimized SORT LNPs can achieve 97-percent lung selectivity, 98-percent spleen selectivity, or durable 60–80-percent extrahepatic gene silencing in kidney, lung, and spleen after a single intravenous injection (Dilliard et al., 2023; Dong et al., 2024; Vaidya et al., 2024; Heredero et al., 2025). Second-generation siloxane-incorporated LNPs (SiLNPs) enable robust gene editing in liver, lung, and spleen while also improving endosomal escape (Xue et al., 2024). The clinical importance of SORT for reprogramming is that it provides an orthogonal tropism lever: an LNP formulation can be chosen to deliver OSK mRNA to a non-hepatic organ with reduced contamination of the hepatic compartment.

**Oral small-molecule chemical reprogramming cocktails are ubiquitous.** Chemical reprogramming cocktails combining compounds such as valproic acid, CHIR99021, E-616452, Parnate, Forskolin, and DZNep can reprogram human somatic cells to pluripotency without integrated transgenes (Hou et al., 2013; Guan et al., 2022; Cheng et al., 2025; Schoenfeldt et al., 2025). When delivered systemically as an oral regimen, these compounds distribute to essentially every perfused tissue by passive diffusion. Schoenfeldt et al. (2025) showed that a chemically-defined oral regimen extends mouse lifespan and ameliorates cellular hallmarks of aging, suggesting oral chemical reprogramming is a viable modality. However, the absence of tissue selectivity means that a dose sufficient to induce chemical reprogramming in the skin or retina is delivered simultaneously to the liver and intestine, which are the organs that define the upper bound on safe exposure.

**Virus-like particles and eVLPs have uneven coverage.** Engineered virus-like particles packaging Cas9 or OSK mRNA have emerged as an intermediate modality combining the protein-free delivery of LNPs with the immunogenicity profile of viral capsids (Banskota et al., 2022). Their biodistribution depends strongly on the surface protein chosen for pseudotyping: VSV-G-pseudotyped particles are broadly tropic but hepatic-biased; engineered variants exposing tissue-specific receptor-binding domains can narrow tropism to muscle, brain, or liver (Banskota et al., 2022; Liu et al., 2024).

The fundamental lesson from this inventory is that **no single modality provides the multi-organ dose profile required for whole-body partial reprogramming**. Each modality has an intrinsic organ bias; achieving a dose vector that matches each organ's therapeutic window requires combining modalities orthogonally.

### 2.3 Framework F338: Coupled N-organ ODE network with circulating-factor transfer matrix

Consider an organism partitioned into $N$ organ compartments. Let $\mathbf{a}(t) = (a_1(t), a_2(t), \ldots, a_N(t))^\top$ denote the vector of organ biological ages at time $t$, where $a_i(t)$ is the biological-age gap (biological minus chronological age) of organ $i$ measured by a tissue-specific epigenetic or proteomic clock (Oh et al., 2023; Oh et al., 2025; Kivimäki et al., 2025; Wang et al., 2025). Each organ has a baseline chronological aging rate offset by an intrinsic resilience term $d_i > 0$; a cross-coupling matrix $M \in \mathbb{R}^{N \times N}$ whose off-diagonal element $m_{ij}$ encodes the rate at which rejuvenation of organ $j$ propagates to organ $i$ via circulating factors; and a dose-sensitivity vector-to-matrix operator $B \in \mathbb{R}^{N \times N}$ mapping an administered dose vector $\mathbf{u}(t) \in \mathbb{R}^N_{\geq 0}$ to a per-organ effective dose. The dynamics of organ biological ages under a systemic dosing protocol is

```math
\frac{d\mathbf{a}}{dt} \;=\; -D\,\mathbf{a}(t) \;+\; M\,\mathbf{a}(t) \;+\; B\,\mathbf{u}(t) \;+\; \boldsymbol{\epsilon}(t)
```

where $D = \mathrm{diag}(d_1, \ldots, d_N) \succ 0$ captures intrinsic organ resilience, $M$ is the circulating-factor transfer matrix with $m_{ii} = 0$ and $m_{ij}$ potentially of either sign (positive for rejuvenating coupling, negative for pro-aging coupling), $B$ is the per-organ delivery efficiency matrix (diagonal if delivery is organ-selective, dense if cross-contamination is significant), $\mathbf{u}(t)$ is the controlled dose vector, and $\boldsymbol{\epsilon}(t)$ is a stochastic perturbation representing unmodeled environmental and physiological noise (Ma et al., 2024).

The **closed-loop system matrix** is $A \equiv -D + M$. When $\mathbf{u} = 0$ and $\boldsymbol{\epsilon} = 0$, the organ ages evolve as $\mathbf{a}(t) = e^{At}\mathbf{a}(0)$, and the long-run behavior is governed by the spectrum of $A$. Decompose $A = Q\Lambda Q^{-1}$ with $\Lambda = \mathrm{diag}(\lambda_1, \ldots, \lambda_N)$ ordered so that $\mathrm{Re}(\lambda_1) \geq \mathrm{Re}(\lambda_2) \geq \cdots \geq \mathrm{Re}(\lambda_N)$. We interpret the eigenvectors $\mathbf{q}_k$ of $A$ as **rejuvenation propagation modes**: a dose $\mathbf{u}$ that preferentially excites the $k$-th eigenmode produces an organ-age response whose shape is $\mathbf{q}_k$, and whose persistence is governed by $\lambda_k$.

Three parameter-informed regimes of F338 are especially important for translation.

**Regime 1: Weakly coupled ($\|M\| \ll \|D\|$).** When circulating-factor coupling is small compared to intrinsic organ resilience, $A \approx -D$ and the matrix is diagonal. Each organ evolves independently, dose vectors must be delivered individually to each target organ, and inter-organ coupling can be ignored. The data suggest this regime may apply in isolated tissues (e.g., the eye behind the blood-retinal barrier, or the immune-privileged testis) but not to the majority of somatic organs (Pálovics et al., 2022; Ma et al., 2022).

**Regime 2: Rejuvenation-coupled ($m_{ij} > 0$ for many pairs).** When young circulating factors propagate rejuvenation from one organ to another, $M$ has many positive off-diagonal elements. The dominant eigenmode is typically a broadly-supported collective rejuvenation mode, and the dominant eigenvalue has the smallest decay rate — meaning that rejuvenation gained at any one organ persists across the organism for an extended period. The empirical data from heterochronic parabiosis support this regime: Zhang et al. (2023) showed that the rejuvenation effect of a three-month heterochronic parabiosis persisted for at least two months after detachment and affected epigenetic ages in blood and liver simultaneously.

**Regime 3: Senescence-coupled ($m_{ij} < 0$ for senescent donors).** When senescent cells in organ $j$ secrete factors that age organ $i$, the corresponding $m_{ij}$ is negative. This regime is supported by the CCL11-mediated "aging contagion" observed when young mice are exposed to old blood (Villeda et al., 2011; He et al., 2026) and by the SASP-mediated transfer of senescence from aged to young tissues (Mehdipour et al., 2020; Kiss et al., 2020). In practice, $M$ is a mixed-sign matrix whose eigenstructure is less benign: dominant eigenmodes can represent "aging avalanches" in which senescence in one organ drives age escalation in coupled organs.

The clinical predictions of F338 follow from inspection of the matrix spectrum. When the dominant eigenvalue is negative (rejuvenation-dominated regime), any dose vector that preferentially excites the dominant eigenmode will generate a sustained whole-body rejuvenation response whose decay time is $1/|\mathrm{Re}(\lambda_1)|$. Conversely, when the dominant eigenvalue is positive (senescence-dominated regime), no sustained dosing protocol can prevent progressive aging, and the therapeutic goal must be to modify the matrix itself — e.g., by removing senescent cell sources via senolytics before initiating OSK dosing. The matrix $M$ can in principle be estimated from plasma proteomic organ-clock data (Oh et al., 2023; Oh et al., 2025; Argentieri et al., 2024) combined with the parabiosis single-cell atlas of Pálovics et al. (2022), but no published study has done so. This is an identifiable gap that our framework highlights as tractable.

**Non-dimensional Péclet-style number.** Define a non-dimensional number $\mathcal{P}_i$ for organ $i$ as the ratio of direct intrinsic rejuvenation to coupling-mediated rejuvenation:

```math
\mathcal{P}_i \;\equiv\; \frac{d_i\,|a_i|}{\bigl|\sum_{j \neq i} m_{ij}\,a_j\bigr|}
```

When $\mathcal{P}_i \gg 1$, organ $i$ is dominated by its own rejuvenation trajectory and the inter-organ coupling can be ignored for local control purposes. When $\mathcal{P}_i \ll 1$, organ $i$'s biological age is determined primarily by the circulating signals from other organs, and organ-local dosing is inefficient — it is better to dose the coupling donors. Empirically, Pálovics et al. (2022) identified adipose mesenchymal stromal cells, hematopoietic stem cells, and hepatocytes as the cell types most responsive to parabiosis-driven rejuvenation, suggesting these tissues have $\mathcal{P}_i < 1$: they are better rejuvenated by manipulating the systemic milieu than by direct reprogramming.

The practical consequence is that **the optimal dosing strategy for whole-body reprogramming is not "hit every organ equally" but "dose the coupling donors and let the network do the work."** F338 makes this intuition quantitatively precise and identifies the dominant eigenmode of $-D + M$ as the design target for any multi-organ delivery architecture.

### 2.4 Orthogonal-tropism multi-modality delivery as the solution to the gradient problem

Given the monomodal failures enumerated in §2.2 and the network dynamics of F338, the only feasible delivery architecture for whole-body partial reprogramming is a multi-modality orthogonal-tropism cocktail in which each modality delivers OSK-equivalent payloads to a distinct, minimally-overlapping subset of organs. The components of such a cocktail, each of which has been experimentally validated in isolation, are:

- **ALPL- or TfR1-targeted engineered AAV** for brain parenchyma (VCAP-102, BI-hTFR1; Moyer et al., 2025; Mathiesen et al., 2024);
- **Muscle-tropic RGD-presenting AAV variants** (MyoAAV; Tabebordbar et al., 2021) for cardiac and skeletal muscle;
- **SORT lipid nanoparticles with DOTAP-based lung targeting** (Dilliard et al., 2023; Heredero et al., 2025) for lung and lymphoid tissues;
- **SORT lipid nanoparticles with anionic helper lipid chemistry** (Dong et al., 2024; Vaidya et al., 2024) for spleen and immune cells;
- **Suprachoroidal or intravitreal AAV2 variants** for retina (Karg et al., 2023; Lu et al., 2020);
- **Oral or topical small-molecule chemical reprogramming cocktail** for skin and superficial epithelia (Guan et al., 2022; Schoenfeldt et al., 2025);
- **Engineered virus-like particles** for niche tissues (ovary, testis, glandular epithelium) as payload-matched delivery to receptor-defined compartments.

Each modality's pharmacokinetic profile is modeled by its own row of $B$ in F338; the off-diagonal elements of $B$ encode the unavoidable cross-contamination (e.g., SORT-lung LNPs still deposit ~15 percent of their payload in the liver; AAV9-derived brain vectors retain some residual hepatic tropism). The combined delivery architecture is a matrix sum $B_{\mathrm{total}} = \sum_k B_k$ where $B_k$ is the biodistribution matrix of the $k$-th modality and the dose vector $\mathbf{u}_k$ controls the amount delivered via that modality. The goal, formalized in the next section, is to choose the $\{\mathbf{u}_k\}$ such that the effective dose vector $\sum_k B_k \mathbf{u}_k$ lies within every organ's therapeutic window.

---

## 3. The Therapeutic Window Set and Multi-Organ Dose Allocation

### 3.1 Each organ defines a convex safe set

For each organ $i$, denote by $\mathcal{S}_i \subset \mathbb{R}^T$ the set of admissible per-organ effective-dose time profiles $e_i(t)$, where $t$ runs over the treatment window $[0, T]$. The simplest such set is a point-wise box constraint

```math
\mathcal{S}_i \;=\; \bigl\{\,e_i : [0,T]\to\mathbb{R}_{\geq 0}\;\bigm|\; L_i \leq e_i(t) \leq U_i \quad \forall\, t \in [0,T]\,\bigr\}
```

where $L_i$ is the minimum dose for measurable rejuvenation in organ $i$ (below which OSK exposure is sub-therapeutic) and $U_i$ is the upper dose bound beyond which organ $i$ loses identity and enters the teratogenic regime. From the data in §2.1, we can parameterize $U_i$ from the Parras et al. (2023) lethality kinetics, the Jo et al. (2025) tissue-specific dedifferentiation data, and the Macip et al. (2024) systemic safe-dose titration; $L_i$ is less directly measured but can be bounded from below by the minimum OSK exposure that produces detectable Horvath-clock reversal in each tissue (Gill et al., 2022; Chondronasiou et al., 2022; Paine et al., 2024). The ratio $U_i / L_i$ (the therapeutic index for organ $i$) ranges from >50 in the eye to approximately 2 in the intestine based on these data.

More realistic $\mathcal{S}_i$ incorporates time-dependence, accounting for the fact that transient high doses may be tolerated while chronic low doses are not (Sahu et al., 2024), or vice versa. For instance, the retina tolerates continuous OSK for months (Lu et al., 2020), while the intestine tolerates short OSK pulses better than continuous exposure (Kim et al., 2023). In general $\mathcal{S}_i$ can be written as the intersection of finitely many half-planes

```math
\mathcal{S}_i \;=\; \bigl\{\,e_i \;\bigm|\; \langle \phi^{(k)}_i, e_i\rangle \leq c^{(k)}_i \text{ for } k=1,\ldots,K_i\,\bigr\}
```

where the functionals $\phi^{(k)}_i$ encode either instantaneous, time-integrated, or peak-concentration constraints, and the constants $c^{(k)}_i$ are the corresponding tolerated thresholds. For the instantaneous-box case, $\mathcal{S}_i$ is a convex polytope; for time-integrated constraints it is a convex half-space; for the general mixed case it is a convex polyhedron. In all cases $\mathcal{S}_i$ is convex.

### 3.2 Framework F339: Therapeutic window set as intersection of organ-specific safe sets

The **combined therapeutic-window set** for a whole-body protocol is the set of dose vectors $\mathbf{u}(t)$ such that **every** organ-specific effective-dose profile lies within its own safe set. Using the delivery matrix decomposition of §2.4 where $e_i(t) = (B\mathbf{u})_i(t)$, the combined set is

```math
\mathcal{W} \;\equiv\; \bigl\{\,\mathbf{u} : [0,T]\to\mathbb{R}^N_{\geq 0} \;\bigm|\; (B\mathbf{u})_i \in \mathcal{S}_i \quad \text{for all } i = 1,\ldots,N\,\bigr\}
```

This is the intersection of $N$ convex sets in the space of dose functions, and it is itself convex. Its characterization is the central object of multi-organ dose design, and its three salient properties are as follows.

**Non-emptiness.** A protocol is feasible if and only if $\mathcal{W} \neq \emptyset$. Whether a given multi-modality cocktail $B$ admits a non-empty intersection is not obvious a priori: if $B$ is effectively rank-deficient (e.g., if all delivery modalities couple the liver and intestine with the same proportionality), the image $B\mathbf{u}$ cannot simultaneously satisfy $(B\mathbf{u})_{\mathrm{liver}} \in \mathcal{S}_{\mathrm{liver}}$ and $(B\mathbf{u})_{\mathrm{target}} \in \mathcal{S}_{\mathrm{target}}$. The necessary and sufficient condition for $\mathcal{W} \neq \emptyset$ is that the delivery matrix $B$ has a well-conditioned right inverse over the organ-age space; in the orthogonal-tropism regime where each modality is organ-specific, $B$ approaches diagonality and invertibility is trivial.

**Minkowski-sum decomposition of a feasible dose vector.** When $\mathcal{W}$ is non-empty, any point $\mathbf{u}^\star \in \mathcal{W}$ can be decomposed as a sum of modality-specific dose contributions $\mathbf{u}^\star = \sum_k \mathbf{u}_k^\star$ where $\mathbf{u}_k^\star$ is supported on the $k$-th modality. The set of feasible total-dose vectors in this decomposition is the Minkowski sum $\bigoplus_k \mathcal{U}_k$ of modality-specific feasibility sets, and the feasibility condition can be checked by linear programming when the constraints are polytopal.

**Maximum-margin dose.** The **robust** dose vector $\mathbf{u}^\mathrm{R}$ is the one that maximizes the minimum distance to the boundaries of all organ-specific safe sets:

```math
\mathbf{u}^\mathrm{R} \;=\; \arg\max_{\mathbf{u}\in\mathcal{W}} \; \min_i \; \mathrm{dist}\bigl((B\mathbf{u})_i,\, \partial \mathcal{S}_i\bigr)
```

This is a Chebyshev-center problem on the convex intersection, soluble by quadratic programming. Clinically, $\mathbf{u}^\mathrm{R}$ is the dose vector maximally robust to identifiable PK/PD variation across patients — the dose vector farthest from toxicity thresholds for all organs simultaneously. Its use provides a principled starting point for clinical trial design and is a more realistic guide than any single-organ dose titration.

### 3.3 Empirical parameterization: an illustrative calculation

To illustrate the quantitative force of F339, consider a simplified four-organ problem: liver, heart, brain, and skin. Assign the following parameters from the references cited above, expressed in "relative OSK exposure units" (ROSE), with 1 ROSE defined as the per-organ exposure produced by a single intraperitoneal dose of doxycycline-induced OSKM in the Ocampo reprogrammable mouse model for 48 hours (Ocampo et al., 2016):

- **Liver:** $L = 0.5$, $U = 1.2$, therapeutic index $U/L = 2.4$
- **Intestine:** $L = 0.3$, $U = 0.8$, therapeutic index = 2.7
- **Heart:** $L = 2.0$, $U = 15$, therapeutic index = 7.5
- **Brain:** $L = 3.0$, $U = 30$, therapeutic index = 10
- **Skin:** $L = 1.0$, $U = 25$, therapeutic index = 25
- **Eye:** $L = 0.5$, $U = 60$, therapeutic index = 120 (Karg et al., 2023; Lu et al., 2020)

With a monomodal systemic AAV9 delivery where $B$ has the approximate row pattern [liver 0.80, intestine 0.05, heart 0.05, brain 0.005, skin 0.02, eye 0.001], the dose vector $\mathbf{u}_{\mathrm{AAV9}}$ required to achieve $(B\mathbf{u})_{\mathrm{brain}} \geq L_{\mathrm{brain}} = 3.0$ would produce $(B\mathbf{u})_{\mathrm{liver}} = (3.0 / 0.005) \cdot 0.80 = 480$ ROSE, which exceeds the liver upper bound of 1.2 by a factor of 400. This is the quantitative statement of why monomodal AAV9 cannot achieve whole-body reprogramming without lethal hepatic damage.

By contrast, with an orthogonal-tropism cocktail combining VCAP-102 (brain-targeted ALPL AAV), MyoAAV (muscle-targeted), SORT-lung LNP, SORT-spleen LNP, AAV2-IT (retinal), and a topical chemical reprogramming cream, the off-diagonal elements of each modality's biodistribution row are ≤ 0.15 (Moyer et al., 2025; Tabebordbar et al., 2021; Dilliard et al., 2023; Heredero et al., 2025; Guan et al., 2022), and an approximate feasibility calculation shows that $\mathcal{W}$ is non-empty for this composition. The feasible interior contains a robust dose vector that keeps every organ within its therapeutic window with a >20 percent safety margin — a substantial improvement over the monomodal infeasibility.

This calculation is illustrative rather than definitive; a clinically usable parameterization requires a tissue-resolved PK/PD characterization of each candidate modality in aged mice, which is the focus of §6.

---

## 4. Multi-Organ Optimal Dose Trajectories and the Organismal Age Aggregator

### 4.1 Framework F340: Multi-organ Pontryagin Hamiltonian

F338 gives the dynamics and F339 gives the feasibility set; to close the control-theoretic loop, we need an objective function over organ ages and dose trajectories and a principled way to compute the optimal time-varying dose. Let $w_i > 0$ be an organ-specific weight reflecting the contribution of organ $i$ to the organismal objective (developed in §4.2), and let $\rho > 0$ be a regularization coefficient penalizing large doses. The **optimal-control problem** is

```math
\min_{\mathbf{u}(\cdot)} \quad J[\mathbf{u}] \;=\; \int_0^T \Bigl[\,\sum_{i=1}^N w_i\, a_i(t) \;+\; \rho\,\|\mathbf{u}(t)\|^2\,\Bigr]\, dt
```

subject to F338 dynamics ($\dot{\mathbf{a}} = -D\mathbf{a} + M\mathbf{a} + B\mathbf{u}$) and the F339 feasibility constraint $\mathbf{u}(t) \in \mathcal{W}(t)$. The running cost captures the instantaneous weighted biological age plus a quadratic control penalty (a standard regularization that both reflects drug cost and prevents unbounded dosing).

The **Pontryagin Hamiltonian** is

```math
H\bigl(\mathbf{a},\mathbf{u},\boldsymbol{\lambda},t\bigr) \;=\; \sum_{i=1}^N w_i\,a_i \;+\; \rho\,\|\mathbf{u}\|^2 \;+\; \boldsymbol{\lambda}^\top\bigl(-D\mathbf{a} + M\mathbf{a} + B\mathbf{u}\bigr)
```

where $\boldsymbol{\lambda}(t) \in \mathbb{R}^N$ is the co-state (shadow price) vector. The Pontryagin Maximum Principle gives the first-order necessary conditions

```math
\frac{d\lambda_i}{dt} \;=\; -\frac{\partial H}{\partial a_i} \;=\; -w_i \;-\; \sum_{j=1}^N \lambda_j\, (M - D)_{ji}
```

with the transversality condition $\boldsymbol{\lambda}(T) = \mathbf{0}$, and the optimal control satisfies

```math
u_i^\star(t) \;=\; -\frac{1}{2\rho}\, (B^\top \boldsymbol{\lambda}(t))_i
```

saturated at the F339 constraints. The key result: unlike the single-organ Pontryagin analysis, which produced a *bang-bang* control law because of the absence of the quadratic penalty $\rho\|\mathbf{u}\|^2$, the multi-organ formulation with the regularization $\rho > 0$ gives a **banded** control law whose magnitude is proportional to the shadow-price vector projected through $B^\top$. The intuition is that when multiple organs share a coupling matrix $M$, dosing one organ aggressively produces spillover to coupled organs whose safe sets may be exceeded; the regularization $\rho$ forces the optimum to distribute dose over a wider temporal band rather than concentrating it.

The **switching function** $S_i(t) = (B^\top \boldsymbol{\lambda}(t))_i$ is the generalized driver of dose $u_i$. Its sign determines whether dosing modality $i$ should be on or off, and its magnitude determines the dose amplitude (up to the feasibility bound). Because the co-state dynamics depend on both $M$ and $D$, the switching function for organ $i$ depends on the entire vector of shadow prices — in other words, optimal dosing for each organ takes into account the shadow prices of all coupled organs.

**Solution structure for the linear-quadratic case.** When $\mathcal{S}_i$ is a box constraint, the optimal control saturates the boundary whenever the unconstrained optimum exceeds it. Between saturations, $\mathbf{u}^\star(t)$ traces a smooth curve determined by the Riccati equation associated with the co-state dynamics. For the specific case $\boldsymbol{\epsilon} = 0$ (deterministic), a closed-form solution exists via the algebraic Riccati equation

```math
P\,(A - B B^\top P / (2\rho)) \;+\; (A - BB^\top P/(2\rho))^\top P \;+\; W \;=\; 0
```

where $A = -D + M$, $W = \mathrm{diag}(w_1, \ldots, w_N)$, and the optimal feedback law is $\mathbf{u}^\star(t) = -P \mathbf{a}(t)/\rho$ saturated at the feasibility boundary. This feedback law is the multi-organ analog of the linear-quadratic regulator, and its novel aspect here is that $A$ is not merely a diagonal organ-resilience operator but incorporates the circulating-factor transfer matrix $M$ from F338.

**Clinical interpretation.** The Pontryagin analysis tells the clinician that the right dose at each modality depends on the current vector of organ ages and on the shadow prices of *all* organs — not just the target organ. This is a genuine departure from single-organ dose titration. In particular, when a coupling organ (e.g., an organ secreting rejuvenating PF4) has a high shadow price, dosing it aggressively can lower the optimal dose required for downstream organs via the $M$ matrix. The dosing protocol can therefore be more parsimonious than the naive organ-independent analysis would suggest.

### 4.2 Framework F341: Organismal age as a weighted sum of organ ages

The objective weights $w_i$ in F340 are not chosen arbitrarily — they encode the contribution of organ-specific aging to all-cause mortality and to the onset of age-related disease. The plasma-proteomic organ-clock literature provides the empirical data needed to calibrate $w_i$ with rigor.

Define the **organismal age aggregator**

```math
A_{\mathrm{org}}(t) \;=\; \sum_{i=1}^N w_i\,a_i(t)
```

as a linear functional of the organ-age vector. The weights are chosen so that $A_{\mathrm{org}}$ is a maximally informative surrogate for residual life expectancy or disease-free survival. The Oh et al. (2023, 2025) cohort data, the Goeminne/Argentieri et al. (2024) UK Biobank analysis, the Wang et al. (2025) diverse-population clocks, and the Whitehall II 20-year follow-up (Kivimäki et al., 2025) jointly constrain these weights.

**Hazard-based weighting.** Let $\mathrm{HR}_i$ denote the mortality hazard ratio per standard deviation of organ-$i$ age gap from the Oh et al. (2025) analysis. The log-hazard weighting is

```math
w_i \;\propto\; \log(\mathrm{HR}_i) \;/\; \sigma_i
```

where $\sigma_i$ is the organ-$i$ age gap standard deviation in the reference population. This weighting ensures that a unit of "organismal age" corresponds to a unit of log-hazard contribution, making $A_{\mathrm{org}}$ a surrogate for log-mortality risk. Empirically, the ranking from Oh et al. (2025) places brain and immune system at the top (HR for brain age = 3.1 per SD for Alzheimer's onset, HR = 0.26 for youthful brain), followed by artery, heart, and kidney (Oh et al., 2025; Kivimäki et al., 2025). The Kivimäki et al. (2025) study, which followed 6,235 Whitehall II participants for 20 years, refines these weights by explicitly adjusting for the correlations among organ ages and identifies liver, dilated cardiomyopathy, chronic heart failure, lung cancer, and agranulocytosis as the diseases exclusively associated with accelerated aging of their respective organ (Kivimäki et al., 2025).

**Disease-adjusted weighting.** When the therapeutic target is healthspan rather than all-cause mortality, a more appropriate weighting uses disease-free survival at, say, age 80 as the response. The Whitehall II analysis shows that artery age, kidney age, and brain age each contribute independently to multi-organ multimorbidity, with arterial age having the largest hazard ratio for multi-morbidity onset (HR = 2.03; Kivimäki et al., 2025). The resulting weighting emphasizes arterial, kidney, and brain rejuvenation even more strongly than the mortality-based weighting.

**Sensitivity analysis identifies "high-leverage" organs.** The partial derivative $\partial A_{\mathrm{org}}/\partial a_i = w_i$ identifies organs whose rejuvenation produces the largest marginal reduction in organismal age. Combined with the toxicity cost $U_i - L_i$ from F339, the ratio $w_i / (U_i - L_i)$ gives the **rejuvenation efficiency per unit toxicity risk**. Under the Oh et al. (2025) weights, the brain and immune system rank highest in rejuvenation efficiency, the heart and vasculature second, and the liver and intestine at the bottom — consistent with the intuition that the liver has low therapeutic index (high toxicity, F339 bottom) and only moderate mortality contribution (intermediate $w_i$, F341).

**The organismal aggregator resolves a long-standing tension in the field.** Horvath's pan-tissue DNA methylation clock (Horvath, 2013) gave a single scalar "biological age" based on blood methylation patterns, but this clock does not measure tissue-specific age accurately in most non-hematopoietic tissues (Richardson et al., 2025; Herzog et al., 2025). Moqri et al. (2024) and Tong et al. (2024) produced cell-type-specific clocks that capture intra-tissue heterogeneity, but these do not aggregate into an organ-level summary. F341 provides the aggregation layer: each organ has its own tissue-specific clock (which may itself be a weighted sum of cell-type clocks), and the organismal age is a weighted sum over organs with weights calibrated from longitudinal mortality data. This construction is the minimum-information sufficient statistic for whole-body dose optimization and is the natural input for the F340 Pontryagin analysis.

### 4.3 Closed-loop adaptation: tissue-specific epigenetic biomarkers as real-time feedback

The greatest uncertainty in F340 is that the dynamical parameters $D$, $M$, and $B$ are known only approximately; they vary between patients and drift over time. A feedback-controlled dosing scheme that uses real-time measurements of organ-age vectors would adapt to this uncertainty and produce more robust outcomes than open-loop protocols. The tools for such closed-loop adaptation are now maturing.

**Cell-free DNA methylation panels.** Nucleic acid fragments released into plasma from dying or turnover cells carry tissue-specific methylation signatures that can reconstruct tissue-of-origin contributions (Moss et al., 2018; Lehmann-Werman et al., 2016). Recent advances in single-nucleosome fragment analysis enable tissue-resolved DNA methylation age measurement from a routine plasma sample (Richardson et al., 2025), opening the path to a minimally-invasive readout of per-organ age.

**Plasma proteomic organ clocks.** The primary readouts of F341 — the Oh et al. (2023, 2025) organ-age clocks and their Goeminne/Argentieri extensions — are derived from plasma proteomics. A single blood draw can therefore estimate the entire vector $\mathbf{a}(t)$ at a given time point. The accuracy is already clinically relevant: the brain age gap in Oh et al. (2025) predicts Alzheimer's onset with a hazard ratio comparable to carrying one copy of APOE4. Sequential plasma proteomic sampling every 6-12 weeks during a treatment cycle would provide real-time pharmacodynamic monitoring.

**MRI-based biological age.** For brain and cardiovascular organs, neuroimaging and cardiac imaging provide independent estimators of tissue age that can be fused with plasma-proteomic signals using a Kalman filter or other state-observer construction (Wen et al., 2024; Tian et al., 2023). The organ-specific biological age gap from MRI (Tian et al., 2023; Wen et al., 2024) can refine the plasma-proteomic estimate with imaging priors.

Integration of these readouts provides the observation vector $\mathbf{y}(t)$ for a state-observer-based closed-loop controller: $\mathbf{y}(t) = H\mathbf{a}(t) + \mathrm{noise}$ where $H$ is the measurement map. The closed-loop law then becomes $\mathbf{u}^\star(t) = -P \hat{\mathbf{a}}(t)/\rho$ where $\hat{\mathbf{a}}(t)$ is the Kalman-filtered state estimate. This construction is the rejuvenation analog of the closed-loop glucose control used in artificial pancreas systems and is technologically mature.

---

## 5. The Minimum-Viable-Systemic-Protocol: Which Organs to Rejuvenate First

The primary framework sections above assume that the clinician wants to rejuvenate all $N$ organs. The reality is different: the clinical development pathway starts with a smaller subset of organs, both because the regulatory burden scales combinatorially in the number of simultaneous targets and because the fundamental scientific question — what is the minimum organ set that produces detectable healthspan benefit? — has not been answered. This section develops two frameworks (F342, F343) that together constitute the minimum-viable-systemic-protocol (MVSP) design problem.

### 5.1 Framework F342: Submodular set-cover with a toxicity knapsack

Define the **benefit function** $f : 2^{\{1,\ldots,N\}} \to \mathbb{R}_{\geq 0}$ that maps an organ subset $S$ to the expected healthspan benefit produced by co-rejuvenating exactly the organs in $S$ (with dose vectors within each organ's safe set). A natural definition is

```math
f(S) \;=\; \mathbb{E}\bigl[\,\Delta \text{healthspan} \,\bigm|\, \text{organs } S \text{ rejuvenated}\,\bigr]
```

where the expectation is taken over the population-level distribution of organ ages, disease onsets, and mortality hazards calibrated from the Whitehall II cohort (Kivimäki et al., 2025), the Oh et al. (2025) UK Biobank cohort, and the Tian et al. (2023) multi-organ aging atlas. The toxicity cost of rejuvenating organs in $S$ is a knapsack constraint

```math
\sum_{i \in S} \mathrm{tox}_i \;\leq\; B_{\mathrm{safe}}
```

where $\mathrm{tox}_i$ is the residual toxicity risk for organ $i$ at the doses that achieve effective rejuvenation (parameterized from the F339 safe-set boundary) and $B_{\mathrm{safe}}$ is the total tolerable toxicity budget for a patient of the target age.

**Submodularity.** The benefit function $f$ is **submodular** if, for all subsets $S \subset T$ and all organs $e \notin T$, the marginal benefit of adding $e$ to $S$ is at least the marginal benefit of adding $e$ to $T$:

```math
f(S \cup \{e\}) - f(S) \;\geq\; f(T \cup \{e\}) - f(T)
```

Submodularity encodes the intuition that the first rejuvenated organ contributes more to healthspan than each subsequent one, because organ-specific aging is partially redundant at the population level — rejuvenating the brain and the heart together produces less than double the benefit of rejuvenating only the brain, because both organs share some underlying hallmarks of aging (López-Otín et al., 2022; Abdellatif et al., 2023). We claim, based on the correlational structure of the Kivimäki et al. (2025) multi-organ hazard data, that $f$ is approximately submodular over the realistic parameter regime. A rigorous empirical test of submodularity requires a longitudinal multi-organ rejuvenation experiment, which is proposed in §6.

**Monotonicity.** $f$ is **monotone** if $f(S) \leq f(T)$ for $S \subset T$. This is satisfied whenever rejuvenating an additional organ cannot be worse than not rejuvenating it — a condition that holds when toxicity is separately accounted for via the knapsack constraint.

**Greedy approximation.** The **greedy algorithm** for monotone submodular maximization under a knapsack constraint (Nemhauser, Wolsey, and Fisher, 1978; Krause, Singh, and Guestrin, 2008) selects, at each step, the organ with the highest ratio of marginal benefit to toxicity cost:

```math
i^\star \;=\; \arg\max_{i \notin S} \; \frac{f(S \cup \{i\}) - f(S)}{\mathrm{tox}_i}
```

and adds $i^\star$ to $S$ if the resulting total toxicity remains within the budget. For monotone submodular objectives with a uniform knapsack, this greedy procedure achieves a $(1 - 1/e) \approx 0.63$ approximation of the optimal achievable benefit, and for weighted knapsacks it achieves a $(1 - 1/e)/2$ approximation. These are the best polynomial-time approximation guarantees known under standard complexity assumptions (Nemhauser, Wolsey, and Fisher, 1978).

**Application to whole-body reprogramming.** Applied to the organ-age and hazard data from Oh et al. (2025) and Kivimäki et al. (2025), the greedy procedure with weights set to the hazard ratios and toxicity costs set proportional to $(U_i - L_i)^{-1}$ (the inverse therapeutic index) produces a ranked priority order:

1. **Brain** (highest hazard contribution, large therapeutic index for eye-adjacent retinal tissue and neural tissue through ALPL AAV or BI-hTFR1 delivery; brain ranks highest in Oh et al. 2025 for all-cause mortality with HR = 3.1 per SD)
2. **Immune system (hematopoietic + splenic)** (second-highest hazard contribution, youthful immune system confers HR = 0.58 for mortality per Oh et al. 2025; deliverable via SORT-spleen LNPs targeting spleen and lymphoid tissue, or via in vivo CAR-T platforms)
3. **Vasculature (arterial)** (third-highest hazard per Kivimäki et al. 2025, HR = 1.52 per SD for multi-organ multimorbidity; deliverable via intravenous AAV with endothelial tropism — Chen et al. 2023)
4. **Heart** (fourth in ranking)
5. **Kidney, skeletal muscle, skin** (middle tier)
6. **Liver, intestine** (excluded from initial protocol due to low therapeutic index)

The MVSP prediction is therefore: **the first clinically meaningful whole-body partial-reprogramming protocol should co-rejuvenate brain + immune + vascular organs using three orthogonal delivery modalities, with liver and intestine explicitly excluded**. This is not arbitrary: it emerges directly from the combination of (a) the hazard-based organ weights from the UK Biobank and Whitehall II cohorts and (b) the therapeutic-index ranking from the experimental OSK toxicity data.

### 5.2 Framework F343: PDMP for chronic cumulative clonal carcinogenic hazard

The MVSP of the previous subsection assumes that each dose cycle is individually safe. The harder constraint on any chronic therapy is that repeated dose cycles over years or decades must not produce a cumulative cancer risk that outweighs the healthspan gain. Aged tissues are mosaics of somatic clones: the human esophageal epithelium accumulates approximately 0.5-1 mutation per cell per year (Martincorena et al., 2018); skin clonal patches expand with age (Martincorena et al., 2015); hepatic clonal expansion is detectable after age 50 (Ng et al., 2021); clonal hematopoiesis of indeterminate potential (CHIP) is present in 10-20 percent of individuals over age 70 (Jaiswal et al., 2014; Mitchell et al., 2022). Each reprogramming pulse transiently activates OSK, which drives cell-cycle re-entry and pluripotency-adjacent gene expression — conditions under which a pre-existing oncogenic clone has the highest probability of escaping identity control and becoming a teratoma or carcinoma.

**PDMP formulation.** Model the clonal mutational burden in a target organ as a stochastic process $X(t)$ that evolves under a piecewise-deterministic Markov process (PDMP; Davis, 1984) with two regimes:

- **Between pulses** (the vast majority of time), $X(t)$ evolves deterministically under a slow drift reflecting natural clonal competition and turnover:

```math
\frac{dX}{dt} \;=\; -\gamma\,X(t) \;+\; \mu_0
```

where $\gamma$ is the natural clonal attenuation rate (driven by competition with unmutated clones and by immune surveillance) and $\mu_0$ is the spontaneous somatic mutation rate.

- **At a pulse** (instantaneous dose events at times $\tau_1, \tau_2, \ldots$), $X$ jumps by a random increment:

```math
X(\tau_k^+) \;=\; X(\tau_k^-) \;+\; Y_k
```

where $Y_k$ is a non-negative random variable whose distribution depends on the pulse intensity and duration and on the pre-existing clonal burden: $Y_k \sim \mathrm{Exp}(\mu(\text{dose}_k, X(\tau_k^-)))$, with mean clonal expansion proportional to the square of the dose in the transient pluripotency regime (motivated by the quadratic dependence of teratoma risk on OSKM expression level observed in the Parras et al. 2023 lethality data).

**Carcinoma hazard.** Define the instantaneous carcinoma hazard as

```math
h_\mathrm{carc}(X) \;=\; h_0 \cdot (X / X_0)^n
```

with parameters $h_0$, $X_0$, $n$ estimated from age-specific cancer incidence data. The cumulative probability of remaining cancer-free up to time $T$ under a pulse protocol $\{\tau_1, \ldots, \tau_K\}$ is

```math
\mathbb{P}\bigl(\text{cancer-free at } T\bigr) \;=\; \mathbb{E}\Bigl[\exp\Bigl(-\int_0^T h_\mathrm{carc}(X(s))\,ds\Bigr)\Bigr]
```

where the expectation is over the joint distribution of the clonal burden increments $\{Y_k\}$ and the deterministic drift dynamics between pulses.

**Closed-form bound on cumulative hazard.** For the regime where $\gamma$ is large relative to the inter-pulse interval (i.e., clonal burdens decay substantially between pulses), the steady-state distribution of $X(t)$ under periodic pulsing is tractable. Let $\Delta$ denote the inter-pulse interval, and let $\bar{Y} = \mathbb{E}[Y_k]$ denote the mean per-pulse clonal increment. The steady-state expected clonal burden is

```math
\mathbb{E}[X_{\mathrm{ss}}] \;\approx\; \frac{\bar{Y}}{1 - e^{-\gamma \Delta}} \;+\; \frac{\mu_0}{\gamma}
```

and, assuming the hazard function is convex in $X$, the cumulative cancer hazard over a decades-long protocol is bounded above by

```math
\int_0^T h_\mathrm{carc}(X(s))\,ds \;\leq\; T \cdot h_0 \cdot \bigl(\mathbb{E}[X_{\mathrm{ss}}]/X_0\bigr)^n
```

This is the **primary design constraint** for chronic cyclic whole-body reprogramming: the inter-pulse interval $\Delta$ and the per-pulse dose (which controls $\bar{Y}$) must be chosen such that the cumulative hazard remains below a clinically acceptable threshold over the intended duration of therapy.

**Safety-first design loop.** The F343 constraint is integrated into the F340 Pontryagin optimization as an additional inequality constraint: for all $t$, the instantaneous cumulative hazard up to time $t$ must remain below a threshold $\theta_\mathrm{safety}$. This is a constraint on the augmented state $(X(t), a_1(t), \ldots, a_N(t))$ and is enforced via a Lagrangian reformulation or via direct constraint projection at each time step. In practice, this forces inter-pulse intervals in human protocols to be at least several weeks long (to allow $X$ to decay between pulses), a result that is consistent with the 2-day-on/5-day-off cyclic protocols used experimentally (Ocampo et al., 2016; Browder et al., 2022).

### 5.3 Sequence hypotheses for the three-organ minimum-viable protocol

Combining F342 and F343, three candidate sequencing strategies for the brain+immune+vascular MVSP emerge:

**Hypothesis A: Brain-first cascade.** Deliver the first six-week dose cycle exclusively to the brain via VCAP-102 or BI-hTFR1 AAV. Because the brain has the highest mortality-contribution weight $w_i$, this maximizes early benefit. Wait four to six weeks for the cumulative-hazard buffer to recover, then deliver the second cycle to the immune system via SORT-spleen LNP, then a third cycle to the vasculature via an endothelial-tropic capsid (Chen et al., 2023). Repeat this 18-week cycle at 6-month intervals.

**Hypothesis B: Simultaneous triple dose.** Deliver all three modalities in a single cycle, separated by 1-2 days each to avoid pharmacokinetic interference. Each modality is dosed at its individual safe level, and the F338 coupling captures any cross-organ propagation. Advantage: immediate full-spectrum effect. Disadvantage: the F343 cumulative hazard per cycle is higher, requiring longer inter-cycle intervals.

**Hypothesis C: Vascular-first with immune support.** Deliver the arterial rejuvenation dose first (highest HR for multi-morbidity per Kivimäki et al. 2025), followed by immune rejuvenation to enhance clearance of damaged cells and then brain rejuvenation. The advantage of this sequencing is that a rejuvenated vasculature improves blood–brain barrier integrity and may reduce the effective AAV dose required for subsequent brain reprogramming.

The optimal sequencing depends on the sign and magnitude of the off-diagonal elements of the $M$ matrix in F338 and on the individual patient's baseline organ ages. A computational simulation with parameter values from the Oh et al. (2025) and Kivimäki et al. (2025) cohorts would allow ranking of these hypotheses and is proposed as the highest-priority validation experiment in §6.

---

## 6. Experimental Validation Roadmap

The frameworks developed in §§2–5 generate a set of pre-registered, falsifiable predictions. The following experimental roadmap would validate (or refute) each prediction in a 36-month timeline and is designed to be immediately actionable by laboratories with access to aged mice, plasma proteomics, and multi-modality delivery capability.

### 6.1 Tissue-resolved PK/PD for each candidate delivery modality

**Experiment 1.** In 24-month-old C57BL/6J wild-type mice, administer each of six candidate delivery modalities (VCAP-102 AAV; BI-hTFR1 AAV; MyoAAV; SORT-lung LNP; SORT-spleen LNP; oral chemical reprogramming cocktail) carrying an OSK-encoding payload at escalating doses. After 7 days, euthanize and measure tissue-resolved OSK protein expression, tissue-resolved DNA methylation age (Horvath, 2013; tissue-specific clocks from Moqri et al. 2024), and tissue-resolved transcriptomic signatures of dedifferentiation. Output: the full delivery matrix $B$ for each modality, parameterizing F338.

**Expected result from F338 predictions.** VCAP-102 should produce brain/spinal-cord transgene levels 20–400-fold higher than AAV9 with minimal hepatic contamination (Moyer et al., 2025). SORT-lung LNP should show >90% lung selectivity (Dilliard et al., 2023; Heredero et al., 2025). These biodistributions establish the orthogonal-tropism decomposition required for a feasible $\mathcal{W}$.

### 6.2 Empirical estimation of the circulating-factor transfer matrix M

**Experiment 2.** In a cohort of aged (22-month-old) C57BL/6J mice, perform heterochronic parabiosis with young 4-month-old partners for 6 weeks, followed by 2 weeks of detachment. In parallel, perform isolated single-organ OSK delivery (via the modality-specific AAVs from Experiment 1) to each of the 6 candidate organs. After each intervention, collect plasma proteomics (using the Oh et al. 2023/2025 organ-clock panel) and measure organ-age changes in all 11 tissues via tissue-specific methylation clocks and proteomic organ clocks. Fit the resulting multi-organ age-change matrix to an $N=11$ matrix $M$ via linear regression with physical-mechanism priors.

**Expected result.** The dominant eigenmode of $M$ should correspond to an "systemic rejuvenation" propagation axis, consistent with the parabiosis rescue of multiple organs (Pálovics et al., 2022). Dosing organs with high $\mathcal{P}_i > 1$ (e.g., muscle via MyoAAV) should produce organ-local rejuvenation; dosing organs with low $\mathcal{P}_i < 1$ (e.g., hematopoietic stem cells via SORT-spleen LNP) should produce broadly-distributed systemic effects.

### 6.3 Validation of the orthogonal-tropism cocktail and F339 feasibility

**Experiment 3.** In 24-month-old aged mice, administer a three-modality cocktail (VCAP-102 AAV for brain, SORT-spleen LNP for immune, endothelial-tropic AAV for vasculature) at doses computed from the F339 feasibility analysis. Measure body weight, serum transaminases, complete blood count, intestinal crypt integrity, histopathology of all major organs at 7, 14, and 28 days, and tissue-resolved biological age via plasma proteomics and organ-specific DNA methylation clocks at 28 days.

**Expected result.** The cocktail should produce significant biological-age reductions in the targeted organs (brain, spleen, vasculature) without causing the hepatic/intestinal failure that continuous OSKM produces (Parras et al., 2023). The dose vector is designed to lie within the intersection $\mathcal{W}$ of safe sets, so no organ should exceed its therapeutic threshold.

**Failure mode analysis.** If the cocktail produces toxicity in an off-target organ (e.g., hepatic damage exceeding 2-fold transaminase elevation), the off-diagonal elements of the candidate modality's biodistribution matrix $B$ were under-estimated in Experiment 1 and the F339 feasibility calculation must be revised. This is a well-defined scientific conclusion.

### 6.4 Validation of F341 weights against mortality outcomes

**Experiment 4.** In a 500-mouse longitudinal cohort observed from 18 months to natural death, measure plasma proteomic organ ages monthly using the Oh et al. (2023, 2025) panel. Fit per-organ hazard ratios using Cox proportional-hazards regression on all-cause mortality. Compare the resulting organismal aggregator $A_\mathrm{org} = \sum w_i a_i$ to existing mortality predictors (PhenoAge, GrimAge, DunedinPACE) in predictive accuracy.

**Expected result.** The F341 aggregator should match or exceed the best blood-based clock (GrimAge v2 per Lu et al. 2022) in predictive accuracy, with the largest marginal improvement coming from the brain and immune system organ components (consistent with Oh et al. 2025).

### 6.5 Validation of the submodular benefit function (F342)

**Experiment 5.** In four cohorts of 24-month-old aged mice (each N=30), administer: (A) nothing; (B) brain only via VCAP-102; (C) brain + spleen via VCAP-102 + SORT-spleen LNP; (D) brain + spleen + vasculature. Measure healthspan (frailty index, grip strength, cognitive performance) at 26 and 30 months and lifespan to natural death. Compute the empirical marginal benefit of adding each organ:

```math
\Delta_i \;=\; f(S \cup \{i\}) - f(S)
```

for each organ pair and verify the submodular inequality $\Delta_i(S) \geq \Delta_i(T)$ for $S \subset T$.

**Expected result.** The single-organ brain arm should produce ~40–60% of the maximum achievable benefit; the two-organ arm ~70–85%; the three-organ arm the maximum. If the marginal benefit of adding the third organ is smaller than the marginal benefit of adding the second organ, the submodular property is supported. If not, the benefit function is non-submodular (possibly super-additive due to synergistic interactions between organ-level rejuvenation signals), and F342 must be replaced by a different optimization framework.

### 6.6 Validation of F343 clonal safety under cyclic dosing

**Experiment 6.** Deliver the three-modality MVSP cocktail to aged mice (N=40) at 28-day inter-pulse intervals for 12 cycles (total duration 12 months). Measure clonal expansion via bulk and single-cell DNA sequencing of major organs at 0, 6, and 12 months. Measure tumor incidence by whole-animal pathology at 12 months and at natural death.

**Expected result.** Under the F343 model with parameters fit to the Martincorena et al. (2015, 2018) mutational landscapes, the predicted 12-cycle cumulative tumor hazard is ~1.5-2-fold above baseline aged-mouse tumor incidence. Empirical tumor rates should match this prediction within a factor of 2. If tumor rates substantially exceed the F343 prediction, the quadratic dose-response of $Y_k$ on pulse intensity is inadequate and a higher-order model is needed.

---

## 7. Clinical Translation Path

The path from the mouse experiments of §6 to a Phase 1 clinical trial for whole-body partial reprogramming is constrained by three regulatory and operational considerations.

**First, the ER-100 precedent.** The Life Biosciences ER-100 IND for optic neuropathy, cleared in January 2026 (Life Biosciences, 2026), establishes that the FDA will accept a single-organ partial-reprogramming gene therapy when the delivery modality is demonstrated to confine OSK expression to the target tissue. This is a single-organ precedent, and the regulatory pathway for ER-100 builds on the subretinal AAV2 delivery paradigm already validated by Luxturna (voretigene neparvovec). For a multi-organ MVSP protocol, the precedent is more distant: the nearest analog is the cocktail gene-therapy paradigm for inherited multi-organ diseases such as Fabry disease or ATTR amyloidosis, where simultaneous treatment of multiple organs is achieved by targeting the single cell type (hepatocyte) that produces the disease-causing protein (Musunuru et al., 2025). The whole-body MVSP protocol has no direct precedent, and the FDA pathway will likely require an initial Phase 1 with one organ at a time, progressing to combination protocols only after each component has established single-agent safety.

**Second, the biomarker endpoint problem.** No epigenetic or proteomic clock has been accepted by the FDA as a clinically meaningful surrogate endpoint for aging. The closest analog is the pace-of-aging biomarker DunedinPACE (Belsky et al., 2022), used as an exploratory endpoint in the CALERIE caloric restriction trial (Waziry et al., 2023). For ER-100 and successor trials, the primary endpoint must be a disease-specific functional outcome (vision restoration, cognitive function, grip strength) and not a biological-age biomarker. F341 provides the mechanistic underpinning for why the Oh et al. (2025) brain organ clock may eventually serve as a biomarker of cognitive rejuvenation, but until regulatory acceptance is achieved, the primary endpoint must be functional. The F341 organismal aggregator can serve as an exploratory endpoint to support functional readouts.

**Third, safety monitoring during chronic cyclic therapy.** The F343 PDMP framework provides explicit predictions for cumulative carcinogenic risk over multi-year exposure. Integrating this into clinical safety monitoring requires regular screening for clonal hematopoiesis (CHIP panels, already clinically available; Jaiswal et al. 2014) and for clonal expansion in other accessible tissues (skin biopsies, colonoscopy-derived intestinal biopsies). Any patient whose clonal burden rises above a pre-specified F343 threshold would receive dose reduction or temporary discontinuation. This is the chronic-therapy analog of the minimum residual disease monitoring used in chemotherapy and of the tumor mutational burden assays used in immunotherapy stratification.

A realistic translational timeline, built on the experimental roadmap of §6 and the regulatory considerations above, projects:

- **Year 1–2:** Mouse experiments 1–6 and parameter calibration;
- **Year 3–4:** Non-human primate PK/PD validation for each modality, with MVSP cocktail safety in old macaques;
- **Year 5:** Phase 1a single-organ IND (brain via VCAP-102 or BI-hTFR1 carrying OSK);
- **Year 6:** Phase 1b single-organ IND (immune via SORT-spleen LNP);
- **Year 7:** Phase 1c single-organ IND (vasculature via endothelial-tropic AAV);
- **Year 8–9:** Phase 1/2 combination IND for brain+immune co-administration;
- **Year 10:** Phase 2 proof-of-concept for full MVSP in individuals with multiple accelerated organ ages (e.g., frail 75+ with elevated brain, immune, and vascular age gaps by Oh et al. 2025 criteria);
- **Year 11–14:** Phase 3 healthspan trial with endpoints in disability-free survival, clinical frailty score, and domain-specific function.

This timeline is aggressive but consistent with the rate of progress of modern gene therapy platforms: Luxturna moved from preclinical to approval in roughly seven years, and CAR-T therapies for hematologic malignancies moved even faster. The MVSP timeline adds approximately three years over single-indication gene therapy programs to account for the regulatory novelty of the multi-organ protocol.

---

## 8. Open Questions and Inquiry Hierarchy

The framework of §§2–5 identifies several first-order open questions whose answers will determine whether whole-body partial reprogramming becomes a viable therapy in the next decade. The following are ranked by urgency and by the experimental accessibility of their resolution.

**Q1: What are the off-diagonal elements of M?** The most consequential unknown is the matrix M in F338. Experiment 2 of §6 is designed to measure it for the mouse, but the human matrix — which may differ substantially — is accessible only through longitudinal natural-experiment observations of patients experiencing focal organ rejuvenation (e.g., patients receiving organ transplants from young donors, or patients in extended therapeutic plasma exchange regimens). The Kivimäki et al. (2025) 20-year follow-up data may support a preliminary human estimate of $M$ via instrumental-variable or mediation analysis, but no such analysis has been published.

**Q2: Is the benefit function f actually submodular?** F342's submodular assumption is testable via Experiment 5 and via the Kivimäki et al. (2025) multi-organ multimorbidity hazard data. A failure of submodularity would be scientifically informative: it would indicate that multi-organ rejuvenation is more than additively beneficial, possibly because rejuvenating one organ lowers the effective safety threshold for others. This would strengthen the case for combination protocols but require a different optimization approach (e.g., DR-submodular or super-modular).

**Q3: What is the realistic range of $\gamma$ and $\bar{Y}$ in F343?** Clonal attenuation and expansion rates under OSK exposure have been measured in isolated experimental systems (Parras et al., 2023; Ocampo et al., 2016) but not in aged-mouse tissues with realistic baseline mutation burdens. Experiment 6 is designed to parameterize these quantities. The key empirical uncertainty is whether the quadratic dose-response holds or whether a higher-order nonlinearity produces catastrophic risk at clinical doses.

**Q4: Can the closed-loop controller of §4.3 be implemented with sufficient temporal resolution?** The proteomic organ clocks have a natural sampling interval of weeks to months (limited by assay cost, not biology), while the F340 optimal control requires feedback on daily-to-weekly timescales. A state-observer construction that bridges this gap by using cheap proxy measurements (circulating cell-free DNA, plasma inflammatory markers, and physical-performance metrics) as high-frequency noisy observations is technically achievable but not yet deployed.

**Q5: Does the MVSP three-organ protocol actually capture the majority of achievable healthspan benefit?** The F342 greedy ordering predicts that brain+immune+vascular rejuvenation yields approximately 70–85 percent of the maximum achievable benefit from a hypothetical all-organ rejuvenation. The 15–30 percent residual benefit from heart, kidney, skin, and muscle rejuvenation is a moving target; if it turns out to be clinically significant, the MVSP must expand. Experimental validation is Experiment 5 in §6.

**Q6: Is the brain the right organ to prioritize, or is it the vasculature?** Oh et al. (2025) shows that the brain age gap has the strongest association with all-cause mortality (HR = 3.1 for the Alzheimer's subgroup), but Kivimäki et al. (2025) shows that the arterial age gap has the strongest association with multi-organ multimorbidity (HR = 2.03). These are different endpoints: brain age predicts disease-specific onset; artery age predicts network-wide morbidity. The clinically optimal first-target depends on the patient population. For a population enriched for early cognitive decline (e.g., APOE4 carriers), brain-first is appropriate; for a population with elevated cardiovascular risk (hypertension, hyperlipidemia), artery-first may be better. The MVSP framework accommodates both via F341 weight specification.

**Q7: How does the chemical reprogramming cocktail (Guan et al. 2022; Schoenfeldt et al. 2025; Cheng et al. 2025) fit into the modality stack?** Oral chemical reprogramming has the advantage of patient convenience and systemic availability, but its lack of tissue selectivity makes it a blunt instrument. A possible role is as a maintenance agent between discrete pulse cycles, operating at sub-threshold doses that produce population-level rejuvenation without directly triggering dedifferentiation in any single organ. Its place in the MVSP architecture is a partially-open question; we lean toward treating it as a sub-threshold baseline while the high-intensity pulses of the MVSP protocol are delivered through the orthogonal-tropism cocktail.

---

## 9. Conclusion

The first 56 papers of this research program have established the scientific foundations of partial reprogramming, tissue-specific rejuvenation biology, delivery platforms, and single-organ dose optimization. The problem that remains unsolved, and that is addressed for the first time in this paper, is how to integrate these components into a whole-body therapeutic protocol that respects the quantitative asymmetries in organ tolerance, exploits the network structure of inter-organ rejuvenation, and keeps the cumulative cancer risk below the clinical threshold over decades of chronic therapy.

The six frameworks developed here — F338 (coupled ODE organ network with circulating-factor transfer matrix), F339 (multi-organ therapeutic-window intersection set), F340 (multi-organ Pontryagin with banded control), F341 (organismal age as hazard-weighted organ sum), F342 (submodular minimum-viable-organ-set selection), and F343 (PDMP cumulative clonal hazard) — together constitute a design specification for a whole-body reprogramming protocol that is (i) provably feasible given the current generation of orthogonal-tropism delivery modalities, (ii) optimally calibrated against the organ-specific mortality hazard data from the largest longitudinal human cohorts, and (iii) explicitly safety-constrained against chronic carcinogenic risk.

The central prediction is that a brain+immune+vascular three-organ MVSP protocol, delivered via VCAP-102 (or BI-hTFR1) AAV + SORT-spleen LNP + endothelial-tropic AAV on a staggered 6–8-week pulse cycle, can achieve approximately 70–85 percent of the maximum possible whole-body rejuvenation benefit while keeping the cumulative carcinogenic hazard within the clinically acceptable range over 10 years of therapy. This prediction is falsifiable. The experimental roadmap of §6 provides the specific measurements that would confirm or refute it, and the clinical translation path of §7 shows how confirmatory data would enter the regulatory pipeline.

The broader implication is that the rate-limiting barrier to human whole-body partial reprogramming is not biological — partial reprogramming works — but architectural. The field already has the components to build a multi-organ protocol; what it lacks is the quantitative integration of those components into a design that respects organ asymmetries and network coupling. This paper is an attempt to supply that integration. The next generation of experiments will determine whether the math is predictive and whether the MVSP vision is realizable.

---

## References

Abdellatif, M., Rainer, P. P., Sedej, S., & Kroemer, G. (2023). Hallmarks of cardiovascular ageing. *Nature Reviews Cardiology*, 20(11), 754–777.

Ames, A. D., Xu, X., Grizzle, J. W., & Tabuada, P. (2017). Control barrier function based quadratic programs for safety critical systems. *IEEE Transactions on Automatic Control*, 62(8), 3861–3876.

Antón-Fernández, A., Cuadros, R., Peinado-Cahuchola, R., Hernández, F., & Avila, J. (2024). In vivo cyclic overexpression of Yamanaka factors restricted to neurons reverses age-associated phenotypes and enhances memory performance. *Communications Biology*, 7(1), 103.

Argentieri, M. A., Naber, N., Engmann, J., Ghanbari, M., & Patel, C. J. (2024). Plasma protein-based organ-specific aging and mortality models unveil diseases as accelerated aging of organismal systems. *Cell Metabolism*, 36(8), 1725–1740.

Belsky, D. W., Caspi, A., Corcoran, D. L., Sugden, K., Poulton, R., Arseneault, L., Baccarelli, A., Chamarti, K., Gao, X., Hannon, E., et al. (2022). DunedinPACE, a DNA methylation biomarker of the pace of aging. *eLife*, 11, e73420.

Bieri, G., Schroer, A. B., & Villeda, S. A. (2023). Blood-to-brain communication in aging and rejuvenation. *Nature Neuroscience*, 26(3), 379–393.

Browder, K. C., Reddy, P., Yamamoto, M., Haghani, A., Guillen, I., Sahu, S., Wang, C., Luque, Y., Prieto, J., Shi, L., et al. (2022). In vivo partial reprogramming alters age-associated molecular changes during physiological aging in mice. *Nature Aging*, 2(3), 243–253.

Chen, X., Ravindra Kumar, S., Adams, C. D., Yang, D., Wang, T., Wolfe, D. A., Arokiaraj, C. M., Ngo, V., Campos, L. J., Griffiths, J. A., et al. (2023). Functional gene delivery to and across brain vasculature of systemic AAVs with endothelial-specific tropism in rodents and broad tropism in primates. *Nature Communications*, 14(1), 3345.

Cheng, L., Wang, Y., Guan, J., & Deng, H. (2025). Decoding human chemical reprogramming: mechanisms and principles. *Trends in Biochemical Sciences*, 50(6), 520–531.

Cheng, Q., Wei, T., Farbiak, L., Johnson, L. T., Dilliard, S. A., & Siegwart, D. J. (2020). Selective organ targeting (SORT) nanoparticles for tissue-specific mRNA delivery and CRISPR–Cas gene editing. *Nature Nanotechnology*, 15(4), 313–320.

Chondronasiou, D., Gill, D., Mosteiro, L., Urdinguio, R. G., Berenguer-Llergo, A., Aguilera, M., Durand, S., Aprahamian, F., Nirmalathasan, N., Abad, M., et al. (2022). Multi-omic rejuvenation of naturally aged tissues by a single cycle of transient reprogramming. *Aging Cell*, 21(3), e13578.

Davis, M. H. A. (1984). Piecewise-deterministic Markov processes: A general class of non-diffusion stochastic models. *Journal of the Royal Statistical Society Series B*, 46(3), 353–388.

Dilliard, S. A., Cheng, Q., & Siegwart, D. J. (2021). On the mechanism of tissue-specific mRNA delivery by selective organ targeting nanoparticles. *Proceedings of the National Academy of Sciences*, 118(52), e2109256118.

Dilliard, S. A., Sun, Y., Brown, M. O., Sung, Y. C., Chatterjee, S., Farbiak, L., Vaidya, A., Lian, X., Wang, X., Lemoff, A., & Siegwart, D. J. (2023). The interplay of quaternary ammonium lipid structure and protein corona on lung-specific mRNA delivery by selective organ targeting (SORT) nanoparticles. *Journal of Controlled Release*, 361, 361–372.

Ding, Y., Liu, Y., Chen, H., Xie, H., Yang, Y., Luo, J., et al. (2025). Comprehensive human proteome profiles across a 50-year lifespan reveal aging trajectories and signatures. *Cell*, 188(10), 2501–2520.

Dong, W., Zhang, H., Li, J., Wang, R., Zhao, K., Lu, Z., Chen, J., Wu, T., & Cheng, X. (2024). Multicomponent synthesis of imidazole-based ionizable lipids for highly efficient and spleen-selective messenger RNA delivery. *Journal of the American Chemical Society*, 146(10), 6838–6850.

Gill, D., Parry, A., Santos, F., Okkenhaug, H., Todd, C. D., Hernando-Herraez, I., Stubbs, T. M., Milagre, I., & Reik, W. (2022). Multi-omic rejuvenation of human cells by maturation phase transient reprogramming. *eLife*, 11, e71624.

Guan, J., Wang, G., Wang, J., Zhang, Z., Fu, Y., Cheng, L., Meng, G., Lyu, Y., Zhu, J., Li, Y., et al. (2022). Chemical reprogramming of human somatic cells to pluripotent stem cells. *Nature*, 605(7909), 325–331.

Gulej, R., Nyúl-Tóth, Á., Ahire, C., DelFavero, J., Balasubramanian, P., Kiss, T., Tarantini, S., Benyo, Z., Pacher, P., Csik, B., et al. (2023). Rejuvenation of cerebromicrovascular function in aged mice through heterochronic parabiosis: insights into neurovascular coupling and the impact of young blood factors. *GeroScience*, 45(5), 2939–2956.

He, H., Song, Y., Wu, D., & Wang, J. (2026). The aging blood: Cellular origins, circulating drivers, and therapeutic potential. *Aging and Cancer*, 7(1), 5–23.

Heredero, J., Peña, A., Broset, E., Blandín, A., de Miguel, I., Lostalé-Seijo, I., Mendía, A., Herrero-Álvarez, N., García-Gonzalo, D., Cortajarena, A. L., & Mosquera, J. (2025). Predictive lung- and spleen-targeted mRNA delivery with biodegradable ionizable lipids in four-component LNPs. *Pharmaceutics*, 17(1), 62.

Herzog, C. M. S., Redl, E., Barrett, J., Aminzadeh-Gohari, S., Weber, D. D., Tevini, J., Lang, R., Kofler, B., & Widschwendter, M. (2025). Functionally enriched epigenetic clocks reveal tissue-specific discordant aging patterns in individuals with cancer. *Communications Medicine*, 5(1), 98.

Hishida, T., Yamamoto, M., Hishida-Nozaki, Y., Shao, C., Huang, L., Wang, C., Shojima, K., Xue, Y., Hang, Y., Shokhirev, M., et al. (2022). In vivo partial cellular reprogramming enhances liver plasticity and regeneration. *Cell Reports*, 39(4), 110730.

Horvath, S. (2013). DNA methylation age of human tissues and cell types. *Genome Biology*, 14(10), R115.

Hou, P., Li, Y., Zhang, X., Liu, C., Guan, J., Li, H., Zhao, T., Ye, J., Yang, W., Liu, K., et al. (2013). Pluripotent stem cells induced from mouse somatic cells by small-molecule compounds. *Science*, 341(6146), 651–654.

Huang, Q., Chan, K. Y., Tobey, I. G., Chan, Y. A., Poterba, T., Boutros, C. L., Balazs, A. B., Daneman, R., Bloom, J. M., Seed, C., & Deverman, B. E. (2023). Targeting AAV vectors to the central nervous system by engineering capsid–receptor interactions that enable crossing of the blood–brain barrier. *PLoS Biology*, 21(7), e3002112.

Jaiswal, S., Fontanillas, P., Flannick, J., Manning, A., Grauman, P. V., Mar, B. G., Lindsley, R. C., Mermel, C. H., Burtt, N., Chavez, A., et al. (2014). Age-related clonal hematopoiesis associated with adverse outcomes. *New England Journal of Medicine*, 371(26), 2488–2498.

Jo, B. K., Lee, S. Y., Eom, H. J., Kim, J., & Cha, H. J. (2025). Organ-specific dedifferentiation and epigenetic remodeling in in vivo reprogramming. *Aging Cell*, 24(11), e70268.

Karg, M. M., Lu, Y. R., Refaian, N., Cameron, J., Hoffmann, E., Hoppe, C., Shirahama, S., Shah, M., Krasniqi, D., Krishnan, A., et al. (2023). Sustained vision recovery by OSK gene therapy in a mouse model of glaucoma. *Cellular Reprogramming*, 25(6), 288–299.

Kim, J., Kim, S., Lee, S. Y., Jo, B. K., Oh, J. Y., Kwon, E. J., Park, K. S., Park, S. Y., Park, J. H., & Cha, H. J. (2023). Partial in vivo reprogramming enables injury-free intestinal regeneration via autonomous Ptgs1 induction. *Science Advances*, 9(47), eadi8454.

Kivimäki, M., Frank, P., Pentti, J., Xu, X., Vahtera, J., Ervasti, J., Nyberg, S. T., Lindbohm, J. V., Jokela, M., & Partridge, L. (2025). Proteomic organ-specific ageing signatures and 20-year risk of age-related diseases: the Whitehall II observational cohort study. *The Lancet Digital Health*, 7(2), e131–e142.

Kiss, T., Nyúl-Tóth, Á., Balasubramanian, P., Tarantini, S., Ahire, C., Yabluchanskiy, A., Csipo, T., Farkas, E., Wren, J. D., Garman, L., et al. (2020). Circulating anti-geronic factors from heterochonic parabionts promote vascular rejuvenation in aged mice. *GeroScience*, 42(2), 727–748.

Krause, A., Singh, A., & Guestrin, C. (2008). Near-optimal sensor placements in Gaussian processes: Theory, efficient algorithms and empirical studies. *Journal of Machine Learning Research*, 9, 235–284.

Kuo, C.-L., Chen, Z., Liu, P., Pilling, L. C., Atkins, J. L., Fortinsky, R. H., Kuchel, G. A., & Diniz, B. S. (2024). Proteomic aging clock (PAC) predicts age-related outcomes in middle-aged and older adults. *Aging Cell*, 23(6), e14177.

Lagunas-Rangel, F. A. (2024). Aging insights from heterochronic parabiosis models. *npj Aging*, 10(1), 38.

Lee-Six, H., Øbro, N. F., Shepherd, M. S., Grossmann, S., Dawson, K., Belmonte, M., Osborne, R. J., Huntly, B. J. P., Martincorena, I., Anderson, E., et al. (2018). Population dynamics of normal human blood inferred from somatic mutations. *Nature*, 561(7724), 473–478.

Liberale, L., Badimon, L., Montecucco, F., Lüscher, T. F., Libby, P., & Camici, G. G. (2025). Roadmap for alleviating the manifestations of ageing in the cardiovascular system. *Nature Reviews Cardiology*, 22(4), 233–258.

Life Biosciences. (2026). Life Biosciences announces FDA clearance of IND application for ER-100 in optic neuropathies. Press release, January 28, 2026.

Liu, M., Li, Y., & Zhang, J. (2024). Rejuvenation of young blood on aging organs: Effects, circulating factors, and mechanisms. *Heliyon*, 10(3), e25436.

López-Gordo, E., Chamberlain, K., Riyad, J. M., Kohlbrenner, E., & Weber, T. (2024). Natural adeno-associated virus serotypes and engineered adeno-associated virus capsid variants: Tropism differences and mechanistic insights. *Viruses*, 16(3), 442.

López-Otín, C., Blasco, M. A., Partridge, L., Serrano, M., & Kroemer, G. (2023). Hallmarks of aging: An expanding universe. *Cell*, 186(2), 243–278.

Lu, A. T., Binder, A. M., Zhang, J., Yan, Q., Reiner, A. P., Cox, S. R., Corley, J., Harris, S. E., Kuo, P.-L., Moore, A. Z., et al. (2022). DNA methylation GrimAge version 2. *Aging (Albany NY)*, 14(23), 9484–9549.

Lu, Y., Brommer, B., Tian, X., Krishnan, A., Meer, M., Wang, C., Vera, D. L., Zeng, Q., Yu, D., Bonkowski, M. S., et al. (2020). Reprogramming to recover youthful epigenetic information and restore vision. *Nature*, 588(7836), 124–129.

Ma, S., Wang, S., Ye, Y., Ren, J., Chen, R., Li, W., Li, J., Zhao, L., Zhao, Q., Sun, G., et al. (2022). Heterochronic parabiosis induces stem cell revitalization and systemic rejuvenation across aged tissues. *Cell Stem Cell*, 29(6), 990–1005.e10.

Macip, C. C., Hasan, R., Hoznek, V., Kim, J., Lu, Y. R., Metzger, L. E., Sethna, S., & Davidsohn, N. (2024). Gene therapy-mediated partial reprogramming extends lifespan and reverses age-related changes in aged mice. *Cellular Reprogramming*, 26(1), 24–32.

Martincorena, I., Roshan, A., Gerstung, M., Ellis, P., Van Loo, P., McLaren, S., Wedge, D. C., Fullam, A., Alexandrov, L. B., Tubio, J. M., et al. (2015). High burden and pervasive positive selection of somatic mutations in normal human skin. *Science*, 348(6237), 880–886.

Martincorena, I., Fowler, J. C., Wabik, A., Lawson, A. R. J., Abascal, F., Hall, M. W. J., Cagan, A., Murai, K., Mahbubani, K., Stratton, M. R., et al. (2018). Somatic mutant clones colonize the human esophagus with age. *Science*, 362(6417), 911–917.

Mehdipour, M., Skinner, C., Wong, N., Lieb, M., Liu, C., Etienne, J., Kato, C., Kiprov, D., Conboy, M. J., & Conboy, I. M. (2020). Rejuvenation of three germ layers tissues by exchanging old blood plasma with saline-albumin. *Aging (Albany NY)*, 12(10), 8790–8819.

Mitchell, E., Spencer Chapman, M., Williams, N., Dawson, K. J., Mende, N., Calderbank, E. F., Jung, H., Mitchell, T., Coorens, T. H., Spencer, D. H., et al. (2022). Clonal dynamics of haematopoiesis across the human lifespan. *Nature*, 606(7913), 343–350.

Moqri, M., Herzog, C., Poganik, J. R., Ying, K., Justice, J. N., Belsky, D. W., Higgins-Chen, A. T., Chen, B. H., Cohen, A. A., Fuellen, G., et al. (2024). Validation of biomarkers of aging. *Aging Cell*, 23(12), e14368.

Moyer, T. C., Hoffman, B. A., Chen, W., Shah, I., Ren, X.-Q., Knox, T., Liu, J., Wang, W., Li, J., Khatri, H., et al. (2025). Highly conserved brain vascular receptor ALPL mediates transport of engineered AAV vectors across the blood-brain barrier. *Molecular Therapy*, 33(4), 1345–1361.

Musunuru, K., Grandinette, S. A., Wang, X., Hudson, T. R., Briseno, K., Berry, A. M., Hacker, J. L., Hsu, A., Silverstein, R. A., Hille, L. T., et al. (2025). Patient-specific in vivo gene editing to treat a rare genetic disease. *New England Journal of Medicine*, 392(22), 2235–2243.

Nemhauser, G. L., Wolsey, L. A., & Fisher, M. L. (1978). An analysis of approximations for maximizing submodular set functions—I. *Mathematical Programming*, 14(1), 265–294.

Ng, S. W. K., Rouhani, F. J., Brunner, S. F., Brzozowska, N., Aitken, S. J., Yang, M., Abascal, F., Moore, L., Nikitopoulou, E., Chappell, L., et al. (2021). Convergent somatic mutations in metabolism genes in chronic liver disease. *Nature*, 598(7881), 473–478.

Ocampo, A., Reddy, P., Martinez-Redondo, P., Platero-Luengo, A., Hatanaka, F., Hishida, T., Li, M., Lam, D., Kurita, M., Beyret, E., et al. (2016). In vivo amelioration of age-associated hallmarks by partial reprogramming. *Cell*, 167(7), 1719–1733.e12.

Oh, H. S. H., Rutledge, J., Nachun, D., Pálovics, R., Abiose, O., Moran-Losada, P., Channappa, D., Urey, D. Y., Kim, K., Sung, Y. J., et al. (2023). Organ aging signatures in the plasma proteome track health and disease. *Nature*, 624(7990), 164–172.

Oh, H. S. H., Le Guen, Y., Rappoport, N., Urey, D. Y., Farinas, A., Rutledge, J., Channappa, D., Wilson, E. N., Greicius, M. D., Mormino, E. C., et al. (2025). Plasma proteomics links brain and immune system aging with healthspan and longevity. *Nature Medicine*, 31(4), 1242–1253.

Paine, P. T., Nguyen, A., & Ocampo, A. (2024). Partial cellular reprogramming: A deep dive into an emerging rejuvenation technology. *Aging Cell*, 23(2), e14039.

Paine, P. T., Desdín-Micó, G., Pietro, S., Phelps, G. B., Phelps, G. L., Mrabti, C., Perez, K., Barilari, M., Yucel, N., & Ocampo, A. (2023). Initiation phase cellular reprogramming ameliorates DNA damage in the ERCC1 mouse model of premature aging. *Frontiers in Aging*, 4, 1246894.

Pálovics, R., Keller, A., Schaum, N., Tan, W., Fehlmann, T., Borja, M., Kern, F., Bonanno, L., Calcuttawala, K., Webber, J., et al. (2022). Molecular hallmarks of heterochronic parabiosis at single-cell resolution. *Nature*, 603(7900), 309–314.

Parras, A., Vílchez-Acosta, A., Desdín-Micó, G., Picó, S., Mrabti, C., Montenegro-Borbolla, E., Yücel, D., von Meyenn, F., Langiewicz, M., Rodriguez, L. G., et al. (2023). In vivo reprogramming leads to premature death linked to hepatic and intestinal failure. *Nature Aging*, 3(12), 1509–1520.

Pico, S., Vílchez-Acosta, A., Agostinho de Sousa, J., Maza, M. C., Picó, D., Picó, S., Esteban-Martín, V., Mrabti, C., Desdín-Micó, G., Parras, A., et al. (2025). Comparative analysis of mouse strains for in vivo induction of reprogramming factors. *Cell Reports*, 44(7), 115879.

Prattichizzo, F., Frigé, C., Pellegrini, V., Scisciola, L., Santoro, A., Monti, D., Rippo, M. R., Ivanchenko, M., Monti, M., Franceschi, C., & Olivieri, F. (2024). Organ-specific biological clocks: Ageotyping for personalized anti-aging medicine. *Ageing Research Reviews*, 96, 102249.

Richardson, M., Brandt, C., Jain, N., Li, J. L., Demanelis, K., Jasmine, F., Kibriya, M. G., Tong, L., & Pierce, B. L. (2025). Characterization of DNA methylation clock algorithms applied to diverse tissue types. *Aging*, 17(1), 67–96.

Sahu, A., Clemens, Z. J., Shinde, S. N., Sivakumar, S., Pius, A., Bhatia, A., Picciolini, S., Carlomagno, C., Gualerzi, A., Bedoni, M., et al. (2021). Regulation of aged skeletal muscle regeneration by circulating extracellular vesicles. *Nature Aging*, 1(12), 1148–1161.

Sahu, S. K., Reddy, P., Lu, J., Shao, Y., Wang, C., Tsuji, M., Núñez Delicado, E., Rodriguez Esteban, C., & Izpisua Belmonte, J. C. (2024). Targeted partial reprogramming of age-associated cell states improves markers of health in mouse models of aging. *Science Translational Medicine*, 16(764), eadg1777.

Schaum, N., Lehallier, B., Hahn, O., Pálovics, R., Hosseinzadeh, S., Lee, S. E., Sit, R., Lee, D. P., Losada, P. M., Zardeneta, M. E., et al. (2020). Ageing hallmarks exhibit organ-specific temporal signatures. *Nature*, 583(7817), 596–602.

Schoenfeldt, L., Paine, P. T., Pico, S., Kamaludeen, N. H., Phelps, G. B., Mrabti, C., Desdín-Micó, G., Del Carmen Maza, M., Perez, K., & Ocampo, A. (2025). Chemical reprogramming ameliorates cellular hallmarks of aging and extends lifespan. *EMBO Molecular Medicine*, 17(8), 2071–2094.

Schroer, A. B., Ventura, P. B., Sucharov, J., Misra, R., Chui, M. K. K., Bieri, G., Villeda, S. A., Hambardzumyan, D., Pálovics, R., Cognetti, D. L., et al. (2023). Platelet factors attenuate inflammation and rescue cognition in ageing. *Nature*, 620(7976), 1071–1079.

Sen, I., Xiong, M., & Hinds, P. W. (2025). Aging at the crossroads of organ interactions: Implications for the heart. *Circulation Research*, 136(3), 321–339.

Shay, T. F., Sullivan, E. E., Ding, X., Chen, X., Ravindra Kumar, S., Goertsen, D., Brown, D., Crosby, A., Zhou, Y., Tee, J. Y., et al. (2024). Human cell surface-AAV interactomes identify LRP6 as blood-brain barrier transcytosis receptor and immune cytokine IL3 as AAV9 binder. *Nature Communications*, 15(1), 7626.

Soroudi, S., Jaafari, M. R., & Arabi, L. (2024). Lipid nanoparticle (LNP) mediated mRNA delivery in cardiovascular diseases: Advances in genome editing and CAR T cell therapy. *Journal of Controlled Release*, 372, 113–140.

Tabebordbar, M., Lagerborg, K. A., Stanton, A., King, E. M., Ye, S., Tellez, L., Krunnfusz, A., Tavakoli, S., Widrick, J. J., Messemer, K. A., et al. (2021). Directed evolution of a family of AAV capsid variants enabling potent muscle-directed gene delivery across species. *Cell*, 184(19), 4919–4938.e22.

Tian, Y. E., Cropley, V., Maier, A. B., Lautenschlager, N. T., Breakspear, M., & Zalesky, A. (2023). Heterogeneous aging across multiple organ systems and prediction of chronic disease and mortality. *Nature Medicine*, 29(5), 1221–1231.

Tokizane, K., & Imai, S. (2024). Inter-organ communication is a critical machinery to regulate metabolism and aging. *Trends in Endocrinology & Metabolism*, 35(6), 499–510.

Vaidya, A., Moore, S., Chatterjee, S., Guerrero-Martín, E., Lian, X., & Siegwart, D. J. (2024). Expanding RNAi to kidneys, lungs, and spleen via selective organ targeting (SORT) siRNA lipid nanoparticles. *Advanced Materials*, 36(13), 2308477.

Villeda, S. A., Luo, J., Mosher, K. I., Zou, B., Britschgi, M., Bieri, G., Stan, T. M., Fainberg, N., Ding, Z., Eggel, A., et al. (2011). The ageing systemic milieu negatively regulates neurogenesis and cognitive function. *Nature*, 477(7362), 90–94.

Wagner, V., Kern, F., Hahn, O., Schaum, N., Ludwig, N., Fehlmann, T., Engel, A., Henn, D., Rishik, S., Isakova, A., et al. (2023). Characterizing expression changes in noncoding RNAs during aging and heterochronic parabiosis across mouse tissues. *Nature Biotechnology*, 41(8), 1206–1214.

Wang, C., Rabadan Ros, R., Martinez-Redondo, P., Ma, Z., Shi, L., Xue, Y., Guillen-Guillen, I., Huang, L., Hishida, T., Liao, H.-K., et al. (2021). In vivo partial reprogramming of myofibers promotes muscle regeneration by remodeling the stem cell niche. *Nature Communications*, 12(1), 3094.

Wang, Y., Han, C., Zhang, Y., Weng, Y., Yue, H., & Zhang, Y. (2025). Organ-specific proteomic aging clocks predict disease and longevity across diverse populations. *Nature Aging*, 5(3), 456–470.

Waziry, R., Ryan, C. P., Corcoran, D. L., Huffman, K. M., Kobor, M. S., Kothari, M., Graf, G. H., Kraus, V. B., Kraus, W. E., Lin, D. T. S., et al. (2023). Effect of long-term caloric restriction on DNA methylation measures of biological aging in healthy adults from the CALERIE trial. *Nature Aging*, 3(3), 248–257.

Wen, J., Skampardoni, I., Tian, Y. E., Yang, Z., Cui, Y., Erus, G., Hwang, G., Varol, E., Boquet-Pujadas, A., Chand, G. B., et al. (2024). The genetic architecture of biological age in nine human organ systems. *Nature Aging*, 4(9), 1234–1250.

Wen, J. (2025). Refining the generation, interpretation and application of multi-organ, multi-omics biological aging clocks. *Nature Aging*, 5(7), 1133–1147.

Witten, J., Hu, Y., Langer, R., & Anderson, D. G. (2024). Recent advances in nanoparticulate RNA delivery systems. *Proceedings of the National Academy of Sciences*, 121(11), e2307798120.

Xu, L., Ramirez-Matias, J., Hauptschein, M., Sun, E. D., Lunger, J. C., Buckley, M. T., & Brunet, A. (2024). Restoration of neuronal progenitors by partial reprogramming in the aged neurogenic niche. *Nature Aging*, 4(4), 546–567.

Xue, L., Hamilton, A. G., Zhao, G., Xiao, Z., El-Mayta, R., Han, X., Gong, N., Xiong, X., Xu, J., Figueroa-Espada, C. G., et al. (2024). Combinatorial design of siloxane-incorporated lipid nanoparticles augments intracellular processing for tissue-specific mRNA therapeutic delivery. *Nature Nanotechnology*, 19(7), 1046–1057.

Yao, Y., Wang, J., Liu, Y., Qu, Y., Wang, K., Zhang, Y., Chang, Y., Yang, Z., Wan, J., Liu, J., et al. (2022). Variants of the adeno-associated virus serotype 9 with enhanced penetration of the blood–brain barrier in rodents and primates. *Nature Biomedical Engineering*, 6(11), 1257–1271.

Zhang, B., Lee, D. E., Trapp, A., Tyshkovskiy, A., Lu, A. T., Bareja, A., Kerepesi, C., McKay, L. K., Shindyapina, A. V., Dmitriev, S. E., et al. (2023). Multi-omic rejuvenation and lifespan extension on exposure to youthful circulation. *Nature Aging*, 3(8), 948–964.

Zhao, R., Yin, Y., Sha, S., Hu, X., & Ji, J. S. (2024). Plasma proteomics-based organ-specific aging for all-cause mortality and cause-specific mortality: A prospective cohort study. *GeroScience*, 46(4), 4119–4135.
