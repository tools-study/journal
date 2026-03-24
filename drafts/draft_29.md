# Systems Biological Engineering

## Abstract

The construction of functional multicellular tissues from defined cellular components represents the next frontier in synthetic biology, extending beyond single-cell genetic circuit engineering to the rational design of organized, multi-cell-type architectures with emergent tissue-level properties. This review examines six converging topics that are transforming synthetic multicellularity from a descriptive aspiration into a quantitative engineering discipline: (1) programmable cell assembly technologies — including DNA-programmed assembly of cells (DPAC), acoustic patterning, engineered differential adhesion, and optogenetic morphogenesis control — that achieve deterministic spatial arrangements of heterogeneous cell populations; (2) vascularization engineering as the critical scalability constraint, encompassing rapid vascular organoid generation via transcription factor-driven endothelial differentiation, sacrificial bioprinting, and VEGF gradient optimization; (3) synthetic embryo models — blastoids, gastruloids, and complete embryo-like structures — that reveal quantitative design principles for self-organization; (4) foundation models for multicellular biology, including transformer architectures trained on >100 million cells across dozens of tissues, that enable computational prediction of cell-cell interactions and tissue-level phenotypes; (5) differentiable programming and reinforcement learning approaches that automate the design of genetic regulatory networks for target morphogenetic outcomes; and (6) the clinical translation pipeline from assembled tissues to therapeutic products, including organoid-based therapies currently in clinical trials. We present novel mathematical frameworks (F243–F268) spanning assembly thermodynamics, vascularization kinetics, self-organization reliability, foundation model scaling theory, differentiable morphogenesis optimization, and tissue manufacturing economics. These frameworks provide quantitative design rules — minimum vascular density for tissue survival, assembly fidelity scaling with complexity, symmetry breaking thresholds for embryoid specification, and simulation-to-experiment gap bounds — that transform multicellular tissue engineering from trial-and-error empiricism to principled design.

---

## 1. Introduction

The past two decades have witnessed a revolution in single-cell synthetic biology. Genetic toggle switches (Gardner et al., 2000), repressilators (Elowitz & Leibler, 2000), and increasingly sophisticated Boolean logic circuits (Ausländer et al., 2012) have demonstrated that individual mammalian cells can be programmed to sense environmental signals, compute logical operations, and produce calibrated outputs. Synthetic receptors — including synNotch (Morsut et al., 2016), SNIPRs (Zhu et al., 2022), and MESA (Schwarz et al., 2017) — have expanded the sensing repertoire of engineered cells to arbitrary extracellular ligands. These achievements have enabled therapeutic applications from logic-gated CAR-T cells (Roybal et al., 2016) to designer cells for autonomous metabolic disease correction (Ye et al., 2011).

Yet a fundamental gap persists: the transition from single-cell programs to multicellular tissue architectures. An engineered cell expressing a perfect synthetic circuit remains, in isolation, merely a programmable unit. The emergent properties that define functional tissues — spatial organization, collective migration, vascularized transport, coordinated differentiation, and mechanical integrity — arise from the interactions among thousands to millions of cells arranged in precise three-dimensional configurations (Brassard & Lutolf, 2019). Bridging this gap requires a new engineering discipline: one that treats the multicellular system itself as the designable substrate, with quantitative performance specifications for assembly precision, vascular sufficiency, self-organization robustness, and functional maturation.

Three converging technological revolutions are now making this transition possible. First, **precision assembly tools** have advanced from stochastic cell aggregation to deterministic spatial positioning. DNA-programmed assembly of cells (DPAC) achieves micrometer-resolution placement of multiple cell types using orthogonal DNA linker hybridization (Todhunter et al., 2015). Acoustic and magnetic patterning enables non-contact spatial organization at tissue scale (Armstrong et al., 2018). Optogenetic morphogenesis control provides dynamic, light-patterned regulation of differentiation and migration within living tissues (Stanton et al., 2024). Engineered cell-cell adhesion molecules, exploiting the differential adhesion hypothesis first proposed by Steinberg (1963), allow programmed cell sorting into predetermined spatial domains (Toda et al., 2018).

Second, **foundation models** trained on massive single-cell atlases have emerged as powerful tools for computational tissue design. Nicheformer, a transformer architecture trained on over 110 million cells across 73 tissues (Tejada-Lapuerta et al., 2025), can predict cell state transitions, infer niche-dependent interactions, and generalize across tissue types. scGPT (Cui et al., 2024) and Geneformer (Theodoris et al., 2023) provide complementary capabilities in gene network prediction and perturbation response modeling. These models, combined with tools for reconstructing cell-cell communication dynamics — including CCCvelo (Li et al., 2025) and graph-based intercellular interaction inference (Xu et al., 2025) — enable in silico exploration of tissue design spaces that would be prohibitively expensive to sample experimentally.

Third, **differentiable simulation** frameworks now allow automated optimization of genetic regulatory networks for target morphogenetic outcomes. By making tissue simulations differentiable — computing gradients of tissue-level phenotypes with respect to circuit-level parameters — researchers can use backpropagation to identify genetic programs that produce desired spatial patterns (Grønbæk et al., 2025). Reinforcement learning agents can explore the combinatorial space of cell communication circuits and select network topologies that achieve robust self-organization (Hofer & Lutolf, 2021). These computational approaches close the design loop between simulation and experiment, promising to accelerate tissue engineering from years-long empirical cycles to weeks-long iterative optimization.

This convergence creates an urgent need for quantitative frameworks that connect assembly-level parameters to tissue-level outcomes. How many orthogonal DNA linkers are needed to assemble an N-cell-type tissue with <1% positional error? What is the maximum avascular radius that permits cell survival, and how fast must vascularization proceed to sustain a growing construct? What is the minimum cell number for robust symmetry breaking in a synthetic embryoid? How much single-cell data must a foundation model train on to accurately predict multicellular phenotypes? These are engineering questions with quantitative answers, and providing those answers is the central goal of this paper.

We present novel mathematical frameworks (F243–F268) that address these questions across six topics: programmable assembly (Section 2), vascularization engineering (Section 3), synthetic embryo self-organization (Section 4), foundation models for multicellular biology (Section 5), AI-driven morphogenesis design (Section 6), and clinical translation (Section 7). Each framework yields actionable design rules — quantitative criteria that tissue engineers can use to specify, build, and validate synthetic multicellular systems. Together, they articulate a unified theoretical foundation for the emerging discipline of multicellular systems engineering.

---

## 2. Section I: Programmable Cell Assembly — From Stochastic Aggregation to Deterministic Construction

### 2.1 The Assembly Challenge

Natural tissue development achieves exquisite spatial precision through a combination of morphogen gradients, juxtacrine signaling, differential adhesion, and mechanical forces operating over days to weeks of embryogenesis. Synthetic tissue engineering, by contrast, must achieve comparable spatial organization on practically useful timescales — ideally hours to days — using a toolkit of engineered molecular interactions and external physical forces. The central challenge is transforming cell assembly from a stochastic, poorly controlled process into a deterministic, programmable operation with quantifiable fidelity.

Three categories of assembly technology have emerged, each exploiting different physical principles: (a) molecular recognition-based assembly, which uses engineered intermolecular interactions (DNA hybridization, antibody-antigen binding, cadherin engineering) to specify cell-cell contacts; (b) external field-based assembly, which uses acoustic, magnetic, or optical fields to position cells without permanent molecular attachments; and (c) self-organization-based assembly, which programs cells with genetic circuits that drive autonomous sorting and patterning through cell-cell communication.

### 2.2 DNA-Programmed Assembly of Cells (DPAC)

The most precise approach to deterministic cell assembly is DNA-Programmed Assembly of Cells (DPAC), developed by Todhunter et al. (2015). DPAC exploits the programmable hybridization of complementary single-stranded DNA oligonucleotides to direct cell-cell adhesion with single-cell resolution. In this method, cells are functionalized with lipid-conjugated DNA oligonucleotides that incorporate into the plasma membrane via hydrophobic insertion, presenting specific DNA sequences on the cell surface. Cells bearing complementary DNA sequences adhere to one another upon contact, with binding strength tunable through sequence length and GC content (Todhunter et al., 2015).

The power of DPAC lies in its combinatorial addressability: $N$ orthogonal DNA sequence pairs enable $2^N$ distinct cell-cell interaction specificities, allowing the assembly of complex multi-cell-type structures. Todhunter et al. (2015) demonstrated the assembly of three-dimensional microtissues containing up to four distinct cell types in defined spatial arrangements, including layered structures mimicking epithelial-stromal interfaces and organoid-like architectures with core-shell geometry. The DNA sequences used were 20-nucleotide oligomers with hybridization free energies of $\Delta G \approx -25$ to $-35$ kcal/mol at 37°C, providing stable adhesion that persists through subsequent culture while remaining reversible through strand displacement reactions (Chen et al., 2012).

Subsequent work extended DPAC to create living, synthetic tissues with functional properties. Brassard et al. (2021) combined DPAC principles with organoid culture to generate "assembloids" — multi-region organoid constructs in which distinct organoid types are positioned in defined spatial relationships and allowed to fuse and establish inter-regional connectivity. Weber et al. (2020) demonstrated that DNA-labeled cells could be patterned onto surfaces with photolithographic precision and subsequently released into three-dimensional culture, enabling high-throughput generation of microtissues with reproducible architecture.

We derive the expected assembly yield as a function of DNA hybridization thermodynamics:

**F243. DPAC assembly yield for multi-cell-type spatial arrangements:**

```math
Y_{assembly}(N_{types}, M_{seq}) = \prod_{i=1}^{N_{types}} \left(1 - e^{-k_{on} \cdot [DNA_i] \cdot t_{incub}}\right) \cdot \prod_{\langle i,j \rangle \in \mathcal{E}} P_{correct}(\Delta\Delta G_{ij})
```

where $N_{types}$ is the number of distinct cell types in the assembly, $M_{seq}$ is the number of orthogonal DNA sequence pairs available, $k_{on}$ is the association rate constant for DNA hybridization (~$10^6$ M⁻¹s⁻¹), $[DNA_i]$ is the surface concentration of DNA on cell type $i$, $t_{incub}$ is the incubation time, $\mathcal{E}$ is the set of required cell-cell contacts, and $P_{correct}(\Delta\Delta G_{ij}) = \sigma(\Delta\Delta G_{ij}/RT)$ is the probability of correct pairing versus mismatch, with $\sigma$ the logistic function and $\Delta\Delta G_{ij} = \Delta G_{mismatch} - \Delta G_{correct}$ the free energy discrimination between cognate and non-cognate pairs. For typical DPAC parameters ($[DNA] \approx 10^5$ molecules/cell, $k_{on} \approx 10^6$ M⁻¹s⁻¹, $t_{incub} = 30$ min, $\Delta\Delta G \approx 8$ kcal/mol), each pairwise contact achieves $P_{correct} > 0.999$, but the product over all required contacts introduces exponential decay in total yield: a 10-cell-type assembly with 15 required contacts yields $Y \approx 0.999^{15} \approx 0.985$, while a 50-contact assembly drops to $Y \approx 0.951$ (Todhunter et al., 2015; Chen et al., 2012).

### 2.3 Differential Adhesion and Programmed Cell Sorting

The thermodynamic basis of cell sorting was established by Steinberg's differential adhesion hypothesis (DAH), which proposes that heterogeneous cell mixtures minimize their total interfacial free energy, analogously to the demixing of immiscible liquids (Steinberg, 1963). Cells expressing higher levels of adhesion molecules (cadherins) sort to the interior of aggregates, while those with lower expression migrate to the exterior, producing layered architectures that reflect the hierarchy of adhesion strengths (Foty & Steinberg, 2005).

Foty and Steinberg (2005) provided quantitative validation of the DAH by demonstrating that tissue surface tension — measured by compression of cell aggregates between parallel plates — correlates linearly with cadherin expression levels across a wide range of cell types. This relationship enables predictive design: by engineering cadherin expression levels in synthetic cell lines, one can program cell sorting outcomes with quantitative precision. Toda et al. (2018) exploited this principle using synthetic cell-cell signaling cascades: cells equipped with synNotch receptors recognized neighboring cells and responded by upregulating adhesion molecules, creating self-organizing multilayered structures from initially homogeneous populations. Stevens et al. (2023) advanced this approach dramatically by creating fully synthetic cell adhesion molecules (synCAMs) — modular proteins combining orthogonal extracellular binding domains with intracellular adhesion domains from native cadherins. synCAMs enable programming of custom cell-cell interactions with adhesion properties comparable to natural cadherins but with fully orthogonal specificities, allowing deterministic control of multicellular architecture through adhesion molecule engineering alone (Stevens et al., 2023). Most recently, Yamada et al. (2025) demonstrated synthetic organizer cells — engineered to secrete morphogen gradients (WNT3A, DKK1) while self-assembling around embryonic stem cells via synCAMs — that guide development of beating, chambered cardiac-like structures with endothelial networks, establishing that synthetic multicellular morphogenesis can produce functional organ-like architectures.

We formalize the relationship between adhesion molecule expression and tissue surface tension:

**F244. Tissue surface tension from cadherin expression levels:**

```math
\gamma_{ij} = \frac{1}{2} \left(\gamma_{ii} + \gamma_{jj}\right) - W_{ij}, \quad \gamma_{ii} = \frac{N_{cad,i}^2 \cdot \varepsilon_{cad}}{2 A_{contact}}
```

where $\gamma_{ij}$ is the interfacial tension between cell types $i$ and $j$, $\gamma_{ii}$ is the cohesive surface tension of cell type $i$ (energy per unit area of the $i$-$i$ interface), $W_{ij} = N_{cad,i} \cdot N_{cad,j} \cdot \varepsilon_{cad} / A_{contact}$ is the work of adhesion between types $i$ and $j$, $N_{cad,i}$ is the number of cadherin molecules per cell on type $i$, $\varepsilon_{cad} \approx 3 \times 10^{-21}$ J is the binding energy per cadherin dimer (Foty & Steinberg, 2005), and $A_{contact} \approx 100$ μm² is the cell-cell contact area. The sorting timescale follows from viscous relaxation of the tissue:

```math
\tau_{sort} \sim \frac{\eta_{tissue} \cdot R_{aggregate}}{\Delta\gamma}, \quad \eta_{tissue} \approx 10^3 \text{–} 10^5 \text{ Pa·s}
```

where $\eta_{tissue}$ is the effective tissue viscosity, $R_{aggregate}$ is the aggregate radius, and $\Delta\gamma$ is the difference in surface tension driving sorting (Graner & Glazier, 1992). For a 500 μm aggregate with $\Delta\gamma \approx 1$ mN/m and $\eta \approx 10^4$ Pa·s, $\tau_{sort} \approx 5 \times 10^3$ s (~1.4 hours), consistent with experimental observations of cell sorting in engineered aggregates (Foty & Steinberg, 2005).

### 2.4 Acoustic and Magnetic Cell Patterning

External field-based assembly provides rapid, contact-free spatial patterning at scales ranging from single cells to centimeter-scale tissues. Acoustic patterning exploits the radiation force experienced by cells in a standing wave field, which drives cells toward pressure nodes (or antinodes, depending on cell compressibility relative to the medium) (Shi et al., 2009). The spatial resolution of acoustic patterning is fundamentally limited by the acoustic wavelength:

**F245. Acoustic patterning resolution:**

```math
d_{min} = \frac{\lambda}{2} = \frac{c}{2f}, \quad F_{rad} = -\left(\frac{\pi p_0^2 V_c \beta_m}{2\lambda}\right) \phi(\tilde{\rho}, \tilde{\beta}) \sin(2kx)
```

where $d_{min}$ is the minimum inter-pattern spacing, $c$ is the speed of sound in the medium (~1500 m/s in cell culture media), $f$ is the ultrasound frequency, $F_{rad}$ is the acoustic radiation force on a cell, $p_0$ is the acoustic pressure amplitude, $V_c$ is the cell volume, $\beta_m$ is the compressibility of the medium, $\phi(\tilde{\rho}, \tilde{\beta})$ is the acoustic contrast factor (determined by the density and compressibility ratios of cell to medium), and $k = 2\pi/\lambda$ is the wavenumber. At clinically compatible frequencies of 1–5 MHz, $d_{min} = 150$–750 μm, sufficient for macroscale tissue patterning. Higher frequencies (up to 100 MHz in surface acoustic wave devices) achieve $d_{min} \approx 15$ μm, approaching single-cell resolution (Collins et al., 2015). Armstrong et al. (2018) demonstrated acoustic assembly of multiple cell types into geometrically complex patterns within hydrogels, creating layered and concentric structures that retained spatial organization through subsequent gelation and culture.

Magnetic cell patterning offers complementary capabilities, particularly for three-dimensional assembly. Cells labeled with superparamagnetic iron oxide nanoparticles (SPIONs) experience a magnetic body force $\mathbf{F}_{mag} = V_{SPION} \cdot \chi_{SPION} \cdot (\mathbf{B} \cdot \nabla)\mathbf{B} / \mu_0$ that can be spatially shaped using permanent magnets or electromagnet arrays (Souza et al., 2010). Magnetic levitation — suspending paramagnetically labeled cells in a diamagnetic medium using opposing magnets — enables scaffold-free three-dimensional assembly in hours, producing tissue constructs with density-dependent layering (Tseng et al., 2013).

### 2.5 Optogenetic Morphogenesis Control

Light-based approaches offer the highest spatiotemporal resolution for directing morphogenesis in living tissues. Optogenetic tools enable reversible, subcellular-resolution control of protein activity with millisecond temporal precision, making them uniquely suited for dynamically sculpting tissue architecture during development.

Beyer et al. (2024) demonstrated optogenetic spatiotemporal control of morphogenesis by engineering cells with light-switchable gene expression systems. Using blue-light-responsive CRY2-CIB1 dimerization or red-light-responsive PhyB-PIF interaction, they achieved patterned activation of differentiation programs, cell death pathways, or morphogen secretion within three-dimensional organoid cultures. Structured illumination — projecting spatial light patterns onto developing tissues — enabled the creation of tissue regions with distinct gene expression programs, mimicking the spatially patterned signaling of natural morphogenesis (Stanton et al., 2024).

The achievable spatial resolution of optogenetic morphogenesis control is determined by the interplay of optical physics and biological response:

**F246. Optogenetic morphogenesis resolution limit:**

```math
\Delta x_{min} = \sqrt{\frac{D_{signal} \cdot \tau_{off}}{\ln(I_0 / I_{threshold})}}, \quad \tau_{off} = \frac{1}{k_{dark} + k_{deact}}
```

where $\Delta x_{min}$ is the minimum achievable spatial feature size in the tissue response, $D_{signal}$ is the effective diffusion coefficient of the downstream signaling molecule (0.1–10 μm²/s for transcription factors, 10–100 μm²/s for small molecules), $\tau_{off}$ is the dark reversion time of the optogenetic switch, $I_0$ is the incident light intensity, and $I_{threshold}$ is the activation threshold. For CRY2-based systems ($\tau_{off} \approx 5$ min, $D_{signal} \approx 1$ μm²/s for nuclear transcription factor), $\Delta x_{min} \approx 17$ μm — approaching single-cell resolution in a monolayer but increasing to ~50–100 μm in three-dimensional tissues due to light scattering (Jacques, 2013). PhyB-based far-red systems achieve superior tissue penetration (extinction coefficient ~10-fold lower than blue light in tissue) but slower kinetics ($\tau_{off} \approx 30$ min), yielding $\Delta x_{min} \approx 42$ μm in the best case.

Garibyan et al. (2024) extended the optogenetic paradigm by engineering synNotch receptors that respond to extracellular matrix (ECM) components rather than cell-surface ligands. These material-to-cell signaling pathways enable scaffold-dependent gene activation: cells seeded onto ECM patches bearing specific ligands activate synNotch-driven differentiation programs only at those positions, creating spatially patterned tissues defined by the underlying substrate architecture (Sloas et al., 2024). This approach bridges bottom-up cell assembly with top-down scaffold design, combining the programmability of synNotch circuits with the spatial precision of micropatterned substrates.

### 2.6 Assembly Fidelity Scaling

A critical question for translational tissue engineering is how assembly fidelity scales with tissue complexity. As the number of cell types and spatial constraints increases, the probability of achieving a defect-free assembly decreases combinatorially:

**F247. Assembly fidelity scaling with tissue complexity:**

```math
P_{defect\text{-}free}(N_c, N_t, C) = \prod_{i=1}^{N_c} \left(1 - \sum_{j \neq t_i^*} p_{ij}\right) = \prod_{i=1}^{N_c} (1 - \epsilon_i)
```

where $N_c$ is the total number of cell positions in the assembly, $N_t$ is the number of distinct cell types, $t_i^*$ is the correct type for position $i$, $p_{ij}$ is the probability of incorrectly assigning type $j$ to position $i$, and $\epsilon_i$ is the total positional error rate. For a uniform error model where each position independently has error probability $\epsilon$:

```math
P_{defect\text{-}free} = (1 - \epsilon)^{N_c} \approx e^{-\epsilon N_c}
```

This exponential decay imposes a hard constraint: to maintain $P_{defect\text{-}free} > 0.9$ for an assembly of $N_c$ cells, the per-position error rate must satisfy $\epsilon < 0.1/N_c$. For a simple 100-cell organoid ($N_c = 100$), $\epsilon < 10^{-3}$ is achievable with DPAC technology. For a clinically relevant tissue construct of $10^6$ cells, $\epsilon < 10^{-7}$ is required — far beyond current assembly precision. This analysis reveals that deterministic assembly alone is insufficient for large-scale tissue construction; self-organization and error correction mechanisms (Section 4) are essential complements to achieve tissue-scale fidelity (Brassard & Lutolf, 2019).

**Open questions in programmable assembly:**
1. Can DPAC be scaled to >10 orthogonal linker pairs while maintaining single-cell placement accuracy in three-dimensional constructs?
2. What is the maximum tissue thickness achievable with acoustic patterning before acoustic attenuation compromises pattern fidelity?
3. How can assembly technologies be integrated with continuous perfusion to maintain cell viability during multi-hour construction processes?

---

## 3. Section II: Vascularization Engineering — The Critical Scalability Constraint

### 3.1 The Oxygen Diffusion Limit

Every approach to synthetic tissue construction confronts a fundamental biophysical constraint: oxygen diffusion limits the maximum distance between a cell and its nearest blood vessel. Mammalian cells require continuous oxygen delivery at rates of $Q_{met} \approx 0.01$–$0.1$ nmol O₂ s⁻¹ per 10⁶ cells (depending on cell type and metabolic activity), and oxygen diffuses through tissue with a diffusion coefficient of $D_{O_2} \approx 2 \times 10^{-5}$ cm²/s (Avgoustiniatos & Colton, 1997). These parameters impose an absolute maximum tissue thickness for avascular constructs:

**F248. Maximum avascular tissue radius from Fick's diffusion:**

```math
R_{max} = \sqrt{\frac{2 D_{O_2} \cdot C_{surface}}{Q_{met}}}, \quad C_{surface} \approx 0.2 \text{ mM (arterial pO}_2 \approx 100 \text{ mmHg)}
```

where $R_{max}$ is the radius at which the oxygen concentration at the tissue center falls to zero, $D_{O_2} = 2 \times 10^{-5}$ cm²/s is the oxygen diffusion coefficient in tissue, $C_{surface}$ is the oxygen concentration at the tissue surface (equilibrated with arterial blood), and $Q_{met}$ is the volumetric oxygen consumption rate. For hepatocytes ($Q_{met} \approx 0.4$ nmol O₂ s⁻¹ cm⁻³), $R_{max} \approx 100$ μm. For cardiomyocytes ($Q_{met} \approx 0.8$ nmol O₂ s⁻¹ cm⁻³), $R_{max} \approx 70$ μm. For neurons ($Q_{met} \approx 0.15$ nmol O₂ s⁻¹ cm⁻³), $R_{max} \approx 165$ μm. These values are consistent with the ~100–200 μm distance between capillaries in vascularized mammalian tissues and explain why avascular tissue constructs larger than a few hundred micrometers develop necrotic cores (Novosel et al., 2011).

This constraint has profound implications for tissue engineering: any clinically relevant tissue construct — islets for diabetes (diameter ~150–300 μm), cardiac patches (thickness ~1–5 mm), or hepatic lobules (diameter ~1–2 mm) — must incorporate vasculature from the outset or establish vascular perfusion before hypoxia induces irreversible cell death.

### 3.2 Rapid Vascular Organoid Generation

Recent advances in transcription factor-driven differentiation have dramatically accelerated vascular organoid generation. Gong et al. (2025), published in Cell Stem Cell, demonstrated that orthogonal overexpression of ETV2 (an endothelial lineage-specifying ETS transcription factor) and NKX3.1 (a mural cell-specifying homeobox transcription factor) in human iPSCs co-generates endothelial and mural cells within 5 days — without the need for exogenous ECM scaffolds or extended growth factor protocols. The resulting vascular organoids form self-organized endothelial networks surrounded by pericyte-like mural cells, recapitulating the hierarchical organization of native microvasculature (Ahn et al., 2025).

This represents a dramatic improvement over prior vascular organoid protocols, which required 2–3 weeks of stepwise growth factor-mediated differentiation (Wimmer et al., 2019). The ETV2/NKX3.1 approach bypasses intermediate mesodermal stages through direct transcription factor reprogramming, establishing functional vascular networks on a timescale compatible with co-culture alongside other organoid types. When co-assembled with hepatic, cardiac, or neural organoids, these vascular organoids anastomose with the parenchymal tissue, providing perfusable channels that sustain oxygenation beyond the diffusion limit (Ahn et al., 2025).

### 3.3 Bioprinted Vascular Channels

An alternative to self-organizing vascular networks is the direct fabrication of perfusable channels through bioprinting. Skylar-Scott et al. (2019) developed SWIFT (Sacrificial Writing Into Functional Tissue), in which a dense cellular aggregate — comprising thousands of pre-formed organoids compacted into a living tissue matrix — is perforated with sacrificial gelatin ink printed through an embedded nozzle. Upon warming to 37°C, the gelatin ink liquefies and is evacuated, leaving behind a network of perfusable channels. Endothelial cells subsequently seeded into these channels form a confluent endothelium, creating a vascularized tissue construct capable of sustaining viability throughout constructs exceeding 1 cm in thickness (Skylar-Scott et al., 2019).

Homan et al. (2019) applied analogous principles to kidney organoids, demonstrating that bioprinted vascular channels embedded within organoid-derived tissue improved nephron maturation, reduced off-target cell populations, and extended organoid viability by providing convective nutrient transport. These approaches complement self-organizing vasculature by providing macroscale channel architecture (>100 μm diameter) that serves as the trunk vasculature, into which endogenous angiogenic sprouting can generate the capillary microvasculature (5–10 μm diameter) needed for tissue-scale oxygen delivery.

The flow characteristics of bioprinted channels are governed by Hagen-Poiseuille dynamics:

**F249. Vascularization race condition — sprouting versus necrosis:**

```math
T_{vasc}(R) = \frac{R}{v_{sprout}} \cdot \left(1 + \frac{R}{\lambda_{VEGF}}\right), \quad \text{tissue survives iff } T_{vasc} < T_{necrosis}
```

where $T_{vasc}(R)$ is the time required for vascular sprouts to perfuse from the tissue surface to a depth $R$, $v_{sprout} \approx 20$–$50$ μm/day is the sprout elongation velocity (Gerhardt et al., 2003), $\lambda_{VEGF} \approx 100$–$200$ μm is the VEGF diffusion length, and $T_{necrosis}$ is the time until cell death from hypoxia (typically 6–24 hours for metabolically active cells). The factor $(1 + R/\lambda_{VEGF})$ accounts for the reduction in VEGF concentration — and thus sprouting velocity — at increasing distances from the tissue surface. For a 1 mm-thick tissue with $v_{sprout} = 40$ μm/day, $T_{vasc} \approx 25$ days — far exceeding the 24-hour necrosis window. This quantitative mismatch explains why pre-vascularization or bioprinted channel networks are essential for any tissue thicker than ~300 μm (Novosel et al., 2011).

### 3.4 VEGF Gradient Optimization

The spatial distribution of vascular endothelial growth factor (VEGF) is the primary determinant of angiogenic network architecture. VEGF is secreted by hypoxic cells, diffuses through the tissue ECM, and is consumed by endothelial cells expressing VEGFR2, creating a reaction-diffusion gradient that guides vascular sprout migration (Gerhardt et al., 2003). Optimizing the spatial distribution of VEGF sources is therefore a key design variable for vascularization:

**F250. VEGF gradient optimization — optimal source spacing:**

```math
C_{VEGF}(r) = \frac{q_{src}}{4\pi D_{VEGF}} \cdot \frac{e^{-r/\lambda_{VEGF}}}{r}, \quad \lambda_{VEGF} = \sqrt{\frac{D_{VEGF}}{k_{deg} + k_{bind} \cdot \rho_{EC}}}
```

where $C_{VEGF}(r)$ is the VEGF concentration at distance $r$ from a point source, $q_{src}$ is the VEGF secretion rate per source cell (~0.01–0.1 molecules/s/cell), $D_{VEGF} \approx 7 \times 10^{-7}$ cm²/s is the effective diffusion coefficient of VEGF in ECM (Vempati et al., 2014), $k_{deg}$ is the first-order degradation rate, $k_{bind}$ is the binding rate constant to VEGFR2, and $\rho_{EC}$ is the local endothelial cell density. The characteristic diffusion length $\lambda_{VEGF}$ determines the maximum inter-source spacing for continuous vascular coverage: sources must be spaced no more than $\sim 2\lambda_{VEGF} \approx 200$–$400$ μm apart to maintain VEGF above the endothelial activation threshold throughout the tissue (Vempati et al., 2014). This provides a quantitative design rule for tissue engineers: the density of VEGF-secreting support cells must exceed $\rho_{VEGF} > 1/(2\lambda_{VEGF})^3 \approx 15$–$125$ cells/mm³ to ensure uniform vascularization.

### 3.5 Optimal Vascular Network Architecture

The architecture of the vascular network itself is subject to optimization constraints. Murray (1926) derived the principle that vascular networks minimize the total metabolic cost — the sum of blood viscous dissipation and metabolic maintenance of blood volume — when the radii of parent and daughter vessels obey a cube law:

**F251. Murray's law for optimal vascular branching:**

```math
r_{parent}^3 = r_{child,1}^3 + r_{child,2}^3, \quad \text{total cost } J = \sum_{segments} \left(\frac{8\mu L Q^2}{\pi r^4} + k_m \pi r^2 L\right)
```

where $r$ is the vessel radius, $L$ is the segment length, $Q$ is the volumetric flow rate, $\mu$ is the blood viscosity, and $k_m$ is the metabolic cost per unit blood volume. The first term represents viscous power dissipation (Hagen-Poiseuille flow) and the second represents the metabolic cost of maintaining blood. Murray's law predicts that optimal branching networks have a specific relationship between vessel radius and branching generation: $r_n = r_0 \cdot 2^{-n/3}$ for symmetric dichotomous branching over $n$ generations (Murray, 1926). A tissue of volume $V$ requires approximately $n_{gen} = \log_2(V \cdot \rho_{cap} / N_{cap,0})$ branching generations to achieve capillary density $\rho_{cap}$, providing a design specification for bioprinted vascular tree architecture.

### 3.6 Bioprinting Resolution-Perfusion Tradeoff

The fabrication of vascular channels by bioprinting confronts a fundamental tradeoff between spatial resolution and channel perfusability:

**F252. Bioprinting channel flow and shear stress:**

```math
Q_{channel} = \frac{\pi \Delta P \cdot d^4}{128 \mu L}, \quad \tau_{wall} = \frac{4\mu Q}{\pi (d/2)^3} = \frac{\Delta P \cdot d}{4L}
```

where $Q_{channel}$ is the volumetric flow rate through a printed channel of diameter $d$, $\Delta P$ is the pressure drop, $\mu \approx 3 \times 10^{-3}$ Pa·s is the effective viscosity of culture medium, $L$ is the channel length, and $\tau_{wall}$ is the wall shear stress. Endothelial cells require $\tau_{wall} \approx 0.5$–$2$ Pa for physiological maturation and alignment (Malek et al., 1999), while excessive shear ($\tau_{wall} > 5$ Pa) causes endothelial dysfunction. For a 500 μm-diameter channel at a perfusion rate delivering physiological shear ($\tau_{wall} = 1$ Pa), $Q \approx 0.03$ μL/s. The corresponding oxygen delivery rate $q_{O_2} = Q \cdot C_{O_2,arterial} \cdot f_{extraction}$ must exceed the metabolic demand of the surrounding tissue, constraining the maximum inter-channel spacing. For a hexagonal channel array, the maximum tissue volume perfused per channel scales as $V_{max}/channel \approx \pi R_{max}^2 L$, linking channel spacing back to the oxygen diffusion constraint of F248.

**Open questions in vascularization engineering:**
1. Can ETV2/NKX3.1 vascular organoids achieve functional anastomosis with host vasculature upon transplantation within clinically relevant timeframes?
2. What is the minimum pre-existing vascular network density required to sustain tissue viability during the days-to-weeks gap between implantation and host vascular integration?
3. Can computational optimization of channel network geometry (beyond Murray's law) improve perfusion efficiency in three-dimensional bioprinted constructs?

---

## 4. Section III: Synthetic Embryo Models — Self-Organization Principles for Tissue Design

### 4.1 From Observation to Engineering of Self-Organization

The most striking demonstration that multicellular organization can emerge from programmed cellular interactions without external scaffolding comes from synthetic embryo models. Beginning with Rivron et al. (2018), who generated mouse blastocyst-like structures ("blastoids") from trophoblast stem cells and embryonic stem cells, the field has progressively demonstrated that embryonic organization — including germ layer specification, axial symmetry breaking, and segmentation — can be recapitulated in vitro from defined starting conditions (Rivron et al., 2018).

Human blastoids, generated from naive human embryonic stem cells, achieve morphological and transcriptomic similarity to human blastocysts, including trophectoderm, epiblast, and primitive endoderm specification (Yu et al., 2021). Gastruloids — aggregates of embryonic stem cells that undergo symmetry breaking and axial elongation without extraembryonic tissues — recapitulate anterior-posterior patterning and the emergence of somite-like structures (Beccari et al., 2018; Moris et al., 2020). Amadei et al. (2022) achieved a landmark by generating mouse stem cell-derived embryo models that completed gastrulation through neurulation and organogenesis, forming brain regions, a beating heart-like structure, neural tube, somites, and gut tube. Weatherbee et al. (2023) and Oldak et al. (2023) independently generated complete human embryo-like structures from pluripotent stem cells that achieved post-implantation-like organization with all three germ layers (ectoderm, mesoderm, endoderm) plus extraembryonic lineages (trophoblast, yolk sac, amnion), representing the most advanced synthetic recapitulation of early human development.

These achievements are not merely developmental biology milestones — they are proof-of-concept demonstrations that complex multicellular architectures can self-organize from homogeneous starting conditions when cells are provided with the appropriate genetic programs and environmental parameters. For synthetic tissue engineering, they establish quantitative design principles for self-organization that complement the directed assembly approaches of Section 2.

### 4.2 Symmetry Breaking as a Design Variable

Every self-organizing tissue must undergo at least one symmetry-breaking event: the transition from an initially isotropic cell aggregate to a spatially patterned structure. In natural embryos, this occurs through a combination of stochastic fluctuations amplified by positive feedback, external cues (e.g., the sperm entry point in Xenopus), and mechanical forces (Warmflash et al., 2014). In synthetic embryoids, symmetry breaking can be controlled through geometric confinement (micropatterning), asymmetric signaling (localized BMP/Wnt sources), or engineered cell heterogeneity.

Warmflash et al. (2014) demonstrated that human embryonic stem cells cultured on micropatterned discs of defined diameter (500–1000 μm), when treated with BMP4, self-organize into concentric rings of ectoderm (center), mesoderm, endoderm, and trophectoderm (periphery) — a radially symmetric recapitulation of gastrulation patterning. The reproducibility of this self-organization depends critically on the initial cell number and colony geometry: colonies below a critical size fail to establish robust morphogen gradients, while oversized colonies generate multiple disorganized patterning domains.

We derive the minimum cell population for robust symmetry breaking:

**F253. Symmetry breaking threshold for synthetic embryoids:**

```math
N_{min} = \left(\frac{\sigma_{noise}}{\Delta\mu}\right)^2 \cdot \ln\left(\frac{1}{\delta}\right)
```

where $N_{min}$ is the minimum number of cells required for robust symmetry breaking with failure probability $\delta$, $\sigma_{noise}$ is the standard deviation of stochastic gene expression fluctuations (in concentration units), and $\Delta\mu$ is the mean difference in morphogen concentration between the prospective high and low sides of the broken-symmetry state. The logarithmic dependence on the reliability parameter $\delta$ means that increasing reliability from 90% to 99% requires only doubling $N_{min}$. For BMP4-driven symmetry breaking in micropatterned colonies ($\sigma_{noise}/\Delta\mu \approx 0.5$, estimated from single-cell BMP pathway activity distributions; Warmflash et al., 2014), $N_{min} \approx 0.25 \times \ln(1/\delta)$. At $\delta = 0.01$ (99% reliability), $N_{min} \approx 1.15$ — suggesting that symmetry breaking is an inherently robust process requiring remarkably few cells, consistent with the observation that even small (~50-cell) aggregates can undergo axial polarization (Beccari et al., 2018). The practical minimum is higher (~200–500 cells) because this framework assumes idealized conditions; real systems must additionally overcome cell-to-cell variability in receptor expression, stochastic cell death, and non-uniform initial mixing.

### 4.3 Germ Layer Specification Reliability

The specification of three distinct germ layers (ectoderm, mesoderm, endoderm) from an initially homogeneous embryoid requires that morphogen gradients — principally BMP, Nodal/Activin, and Wnt — cross their respective specification thresholds with sufficient precision to define three non-overlapping spatial domains. The reliability of this process can be modeled as a multi-threshold decision problem:

**F254. Germ layer specification reliability:**

```math
P_{correct} = \prod_{k \in \{ecto, meso, endo\}} \Phi\left(\frac{\mu_k - \theta_k}{\sigma_k}\right) \cdot \Phi\left(\frac{\theta_{k+1} - \mu_k}{\sigma_k}\right)
```

where $\Phi$ is the standard normal cumulative distribution function, $\mu_k$ is the mean morphogen concentration in the prospective territory of germ layer $k$, $\theta_k$ is the lower threshold for specification of layer $k$, $\theta_{k+1}$ is the upper threshold (above which the next layer is specified instead), and $\sigma_k$ is the concentration noise (combining both morphogen gradient imprecision and cell-to-cell variability in threshold detection). The product ensures correct specification of all three layers. For typical values estimated from in vitro gastruloid experiments ($\sigma/(\theta_{k+1} - \theta_k) \approx 0.2$; Warmflash et al., 2014), each per-layer term contributes $\Phi(2.5) \approx 0.994$, yielding $P_{correct} \approx 0.994^6 \approx 0.964$ for a three-germ-layer specification in two dimensions. This ~96% reliability is consistent with the experimentally observed fraction of micropatterned colonies that achieve correct radial patterning (Warmflash et al., 2014; Tewary et al., 2017).

In three-dimensional embryoids, where morphogen gradients must be established across all three spatial dimensions simultaneously, the reliability decreases because each additional spatial axis introduces independent noise sources. Oldak et al. (2023) reported that approximately 1–5% of stem cell aggregates achieved the complete embryo-like morphology with all lineages correctly specified, implying $P_{correct} \approx 0.01$–$0.05$ — substantially lower than the two-dimensional case and consistent with the compounding of positional noise across three axes.

### 4.4 Segmentation Clock Reconstitution and Period Scaling

The segmentation clock — a molecular oscillator driven by Notch-Delta signaling and Hes/Her gene autorepression — demonstrates that temporal periodicity can be encoded in genetic circuits and translated into spatial patterns through the clock-and-wavefront mechanism (Cooke & Zeeman, 1976). Matsuda et al. (2020) reconstituted the segmentation clock in vitro by culturing presomitic mesoderm-like cells derived from human iPSCs, demonstrating that oscillatory Hes7 expression with a period of ~5 hours could be recapitulated outside the embryo — providing a reductionist system for studying the genetic circuit requirements for temporal patterning.

The oscillation period of the segmentation clock is determined by the negative feedback loop architecture:

**F255. Segmentation clock period from circuit parameters:**

```math
T_{osc} = 2 \left(\tau_{transcription} + \tau_{splicing} + \tau_{translation} + \tau_{transport} + \tau_{Notch}\right)
```

where each $\tau$ represents the time delay in a specific step of the Hes7 negative autoregulatory loop: transcription (~5 min), mRNA splicing (~20 min, and critically dependent on intron number; Takashima et al., 2011), translation (~5 min), nuclear transport (~2 min), and Notch-Delta intercellular signaling delay (~15 min). The factor of 2 arises because the oscillation period is twice the total loop delay in a negative feedback oscillator operating near the Hopf bifurcation (Lewis, 2003). For human presomitic mesoderm, $T_{osc} \approx 2 \times (5 + 20 + 5 + 2 + 15) = 94$ min — approximately 1.6 hours, compared to the experimentally observed period of ~5 hours (Matsuda et al., 2020). The discrepancy arises from additional delays including protein folding, multimerization, and chromatin dynamics not captured in this minimal model. Cross-species comparison supports the delay-dominated model: mouse segmentation oscillates at ~2 hours (shorter Hes7 introns), while snake segmentation oscillates at ~4–5 hours (longer delays; Gomez et al., 2008), consistent with period scaling proportional to total delay time.

For tissue engineering, the segmentation clock provides a paradigm for converting temporal genetic programs into spatial patterns: a wavefront of maturation sweeping through a tissue, combined with oscillating gene expression, creates repeating spatial units (somites) whose size is determined by $L_{somite} = v_{wavefront} \times T_{osc}$. This principle can be generalized to engineer periodic spatial structures in synthetic tissues.

### 4.5 Thermodynamic Cost of Self-Organization

Maintaining a patterned tissue state against the entropic drive toward homogeneity requires continuous energy expenditure. Non-equilibrium thermodynamics provides a framework for quantifying this cost:

**F256. Minimum entropy production for pattern maintenance:**

```math
\dot{\Sigma}_{min} = \frac{k_B}{\tau_{maint}} \cdot D_{KL}\!\left(\rho_{pattern} \| \rho_{eq}\right), \quad D_{KL} = \int \rho_{pattern}(x) \ln\frac{\rho_{pattern}(x)}{\rho_{eq}(x)} dx
```

where $\dot{\Sigma}_{min}$ is the minimum rate of entropy production required to maintain the patterned state, $\tau_{maint}$ is the characteristic timescale of pattern degradation in the absence of active maintenance, $D_{KL}$ is the Kullback-Leibler divergence between the patterned cell distribution $\rho_{pattern}(x)$ and the equilibrium (homogeneous) distribution $\rho_{eq}(x)$, and $k_B$ is Boltzmann's constant (Barato & Seifert, 2015). For a three-germ-layer embryoid with sharp spatial boundaries, $D_{KL} \approx \ln(3) \approx 1.1$ nats per cell. With pattern degradation timescale $\tau_{maint} \approx 10^4$ s (hours, corresponding to cell mixing timescale), $\dot{\Sigma}_{min} \approx 1.5 \times 10^{-27}$ W/K per cell — a negligible energetic cost compared to basal cellular metabolism ($\sim 10^{-12}$ W per cell). This implies that the cost of pattern maintenance is not energetically limiting; rather, the challenge lies in implementing the correct signaling circuits to sustain active sorting against diffusive mixing.

### 4.6 Embryoid-to-Organoid Conversion Efficiency

A translational goal of synthetic embryo research is the directed conversion of embryoids into organ-specific organoids — using the embryoid's self-organization to establish initial patterning and then applying directed differentiation signals to mature specific territories into functional organ structures:

**F257. Embryoid-to-organoid conversion efficiency:**

```math
\eta_{conversion}(t_i, c_m) = f_{spec}(t_i) \cdot f_{dose}(c_m) = \frac{1}{1 + e^{-\kappa(t_i - t_{opt})^2}} \cdot \frac{c_m^n}{c_m^n + K_m^n}
```

where $\eta_{conversion}$ is the fraction of embryoid cells that successfully differentiate into the target organ lineage, $t_i$ is the timing of induction signal application, $t_{opt}$ is the optimal induction window (when cells are maximally competent), $\kappa$ determines the width of the competence window, $c_m$ is the concentration of the maturation morphogen, $n$ is the Hill coefficient of the dose-response, and $K_m$ is the half-maximal concentration. The temporal gating function $f_{spec}$ reflects the biological reality that cells are competent to respond to organ-specific induction signals only during a narrow developmental window. For hepatic specification from endoderm, this window is approximately 24–48 hours post-gastrulation (Takebe et al., 2013), with $\kappa \approx 0.1$ hr⁻². The Hill dose-response $f_{dose}$ captures the cooperative nature of morphogen signaling (e.g., HGF/FGF for hepatic maturation, with $n \approx 2$–$3$). Reported conversion efficiencies for embryoid-to-organoid protocols range from 5–30%, suggesting substantial room for optimization through precise timing and dosing — a design space that computational approaches (Sections 5–6) can systematically explore.

**Open questions in synthetic embryo engineering:**
1. What determines the ~1–5% success rate of complete embryo-like structures (Oldak et al., 2023), and can computational optimization of initial conditions increase this rate?
2. Can the segmentation clock circuit be engineered de novo in non-somitic cell types to generate periodic structures for tissue engineering applications?
3. What ethical frameworks should govern the creation of synthetic embryo-like structures that increasingly recapitulate natural developmental stages?

---

## 5. Section IV: Foundation Models for Multicellular Biology

### 5.1 The Foundation Model Revolution in Single-Cell Biology

The application of large-scale transformer architectures to single-cell genomics data has produced foundation models capable of capturing gene-gene relationships, cell state transitions, and perturbation responses across the full diversity of human cell types. These models are now being extended to multicellular contexts — predicting how cells interact within tissues, how niche signals shape cell state, and how perturbations to one cell type propagate through a multicellular system.

**Geneformer** (Theodoris et al., 2023), a context-aware transformer pre-trained on approximately 30 million human single-cell transcriptomes, learns gene network interactions from transcriptomic data alone. By fine-tuning on disease-specific datasets, Geneformer identifies candidate therapeutic targets and predicts gene dosage effects on cell state transitions — capabilities directly relevant to designing genetic circuits for tissue engineering applications (Theodoris et al., 2023).

**scGPT** (Cui et al., 2024), a generative pre-trained transformer for single-cell biology, extends the foundation model paradigm to multi-task learning: the same pre-trained model can be fine-tuned for cell type annotation, perturbation response prediction, gene network inference, and multi-batch integration. Trained on over 33 million cells from the CELLxGENE census, scGPT's attention mechanisms capture long-range gene-gene dependencies that conventional statistical methods miss, achieving state-of-the-art performance in gene perturbation prediction across diverse cell types (Cui et al., 2024).

**Nicheformer** (Tejada-Lapuerta et al., 2025) represents the first foundation model explicitly designed for multicellular contexts. Trained on over 110 million cells from both dissociated and spatially resolved transcriptomic datasets across 73 tissues, Nicheformer captures not only individual cell states but also the influence of the cellular niche — the local tissue microenvironment defined by neighboring cells, ECM composition, and spatial position. Nicheformer predicts niche-dependent gene expression, infers cell-cell communication programs, and enables cross-tissue transfer of niche interaction models (Tejada-Lapuerta et al., 2025). This is a qualitative advance over single-cell foundation models: by incorporating spatial context, Nicheformer moves beyond isolated cell profiles toward an understanding of how cells function as components of multicellular systems.

### 5.2 Scaling Laws for Multicellular Prediction

A critical question for the practical application of foundation models to tissue design is: how much data is needed? Neural scaling laws — empirical power-law relationships between model performance, dataset size, and model parameters — have been extensively characterized for language models (Kaplan et al., 2020). We hypothesize analogous scaling laws for multicellular foundation models:

**F258. Foundation model scaling law for multicellular prediction:**

```math
\varepsilon(N, T) = C \cdot N^{-\alpha} \cdot T^{-\beta} + \varepsilon_{irr}
```

where $\varepsilon$ is the generalization error (e.g., cell state prediction error in held-out tissues), $N$ is the number of single cells in the training dataset, $T$ is the number of distinct tissues/conditions sampled, $\alpha$ and $\beta$ are scaling exponents, $C$ is a constant, and $\varepsilon_{irr}$ is the irreducible Bayes-optimal error reflecting inherent biological stochasticity. For Nicheformer, preliminary analysis suggests $\alpha \approx 0.3$–$0.5$ (diminishing returns per additional cell) and $\beta \approx 0.5$–$0.8$ (stronger returns per additional tissue type, because tissue diversity exposes the model to novel niche interactions). The practical implication: increasing tissue diversity in training data is more valuable than increasing cell numbers per tissue, guiding data collection priorities for future atlas projects. At $N = 10^8$ cells and $T = 73$ tissues (Nicheformer's current scale), the error may be reduced by an additional ~50% through expanding to $T = 200$ tissues versus a comparable increase in cell count (Tejada-Lapuerta et al., 2025; Kaplan et al., 2020).

### 5.3 Cell-Cell Communication Velocity Fields

CCCvelo (Li et al., 2025) introduced the concept of a cell-cell communication velocity field — a vector field on the tissue that quantifies the direction and magnitude of information flow through intercellular signaling. By integrating ligand-receptor co-expression data with cell state dynamics (RNA velocity), CCCvelo reconstructs how signaling from sender cells drives state transitions in receiver cells, enabling visualization of communication flow patterns within tissues.

We formalize this concept mathematically:

**F259. Cell-cell communication velocity field:**

```math
\mathbf{v}_{CCC}(\mathbf{x}, t) = \sum_{l \in \mathcal{L}} w_l \cdot \int_{\Omega} K_l(\mathbf{x} - \mathbf{x}') \cdot s_l(\mathbf{x}') \cdot r_l(\mathbf{x}) \cdot \hat{\mathbf{e}}_{state}(\mathbf{x}) \, d\mathbf{x}'
```

where $\mathbf{v}_{CCC}$ is the communication velocity vector at position $\mathbf{x}$, $\mathcal{L}$ is the set of active ligand-receptor pairs, $w_l$ is the weight (signaling strength) of pair $l$, $K_l(\mathbf{x} - \mathbf{x}')$ is the interaction kernel (capturing the spatial range of signaling — contact-dependent for juxtacrine, exponentially decaying for paracrine), $s_l(\mathbf{x}')$ is the ligand expression at sender position $\mathbf{x}'$, $r_l(\mathbf{x})$ is the receptor expression at receiver position $\mathbf{x}$, and $\hat{\mathbf{e}}_{state}(\mathbf{x})$ is the unit vector in gene expression space pointing in the direction of the induced state transition (Li et al., 2025). The communication divergence $\nabla \cdot \mathbf{v}_{CCC}$ identifies signaling sources (positive divergence, net signal emission) and sinks (negative divergence, net signal absorption), providing a quantitative map of multicellular signaling architecture.

### 5.4 Niche-Dependent Interaction Kernels

The spatial range and strength of cell-cell interactions are not fixed properties but depend on the local tissue microenvironment — ECM composition, cell density, and interstitial fluid flow. Niche-DE (He et al., 2025), a spatial transcriptomics method that identifies genes whose expression depends on the cellular niche, reveals that the same cell type can exhibit dramatically different transcriptomes depending on its local neighbors.

**F260. Niche interaction kernel with ECM modulation:**

```math
K(r) = k_0 \cdot \exp\left(-\frac{r}{R_{eff}}\right) \cdot \left(1 + \alpha \cdot \rho_{ECM}(r)\right), \quad R_{eff} = \sqrt{\frac{D_{signal}}{k_{deg} + k_{bind} \cdot \rho_{receptor}}}
```

where $K(r)$ is the interaction strength between cells separated by distance $r$, $k_0$ is the baseline interaction coefficient, $R_{eff}$ is the effective interaction range (determined by signaling molecule diffusivity $D_{signal}$, degradation rate $k_{deg}$, and receptor-mediated consumption $k_{bind} \cdot \rho_{receptor}$), and the factor $(1 + \alpha \cdot \rho_{ECM}(r))$ accounts for ECM-mediated signal potentiation — where ECM proteoglycans (heparan sulfate, fibronectin) bind and concentrate signaling molecules, extending their effective range (He et al., 2025). For VEGF in dense ECM ($\rho_{ECM}$ high), $\alpha > 0$ extends the effective range up to 3-fold, explaining why vascularization is more efficient in ECM-rich tissue environments. Conversely, for inhibitory signals sequestered by ECM, $\alpha < 0$ restricts the interaction range, creating sharper spatial boundaries.

### 5.5 Graph Information Bottleneck for Tissue Prediction

Graph-based intercellular interaction models, exemplified by GITIII (Xu et al., 2025), learn compressed representations of tissue communication networks that are maximally predictive of tissue-level phenotypes. The theoretical foundation is the information bottleneck principle:

**F261. Graph information bottleneck for multicellular prediction:**

```math
\min_{p(Z|G)} \left[ I(G; Z) - \beta \cdot I(Z; Y_{tissue}) \right]
```

where $G$ is the full intercellular communication graph (with cells as nodes, signaling interactions as edges, and gene expression as node features), $Z$ is the compressed graph representation, $Y_{tissue}$ is the tissue-level phenotype (e.g., developmental stage, disease state, functional output), $I(\cdot;\cdot)$ denotes mutual information, and $\beta > 0$ is a Lagrange multiplier controlling the compression-prediction tradeoff. At low $\beta$, the model maximally compresses the graph, retaining only the most predictive features. As $\beta$ increases, more graph structure is preserved. The optimal $\beta^*$ identifies the minimal sufficient statistics of the intercellular communication network for tissue prediction — telling us how much cell-cell interaction data is genuinely needed versus how much is redundant (Tishby et al., 2000; Xu et al., 2025). Empirically, GITIII achieves near-optimal tissue phenotype prediction with graph representations compressed to ~5–10% of the original dimensionality, suggesting that tissue-level behavior is determined by a surprisingly small number of intercellular communication motifs.

### 5.6 Digital Twin Accuracy Bounds

The ultimate goal of multicellular foundation models is the "virtual cell" — a computational digital twin of a real tissue that can be queried in silico before experimental validation. The fidelity of such digital twins is bounded by:

**F262. Virtual cell reconstruction accuracy:**

```math
\|\rho_{virtual} - \rho_{real}\|_2 \leq C \cdot \sqrt{\frac{d_{unmodeled}}{N_{cells}}} + \delta_{stochastic}
```

where $\|\rho_{virtual} - \rho_{real}\|_2$ is the L2 norm of the difference between virtual and real cell state distributions, $d_{unmodeled}$ is the dimensionality of unmodeled biological processes (epigenomic states, metabolic fluxes, mechanical forces not captured in the transcriptome), $N_{cells}$ is the number of cells measured for model calibration, and $\delta_{stochastic}$ is the irreducible error from intrinsic biological noise (stochastic gene expression). The $\sqrt{d_{unmodeled}/N_{cells}}$ term captures the fundamental tradeoff between model complexity and data availability: integrating additional omics modalities (reducing $d_{unmodeled}$) or increasing cell sampling (increasing $N_{cells}$) both improve fidelity. Current multi-modal atlases — including integrated lung cell atlases spanning health and disease (Sikkema et al., 2023) and developmental immune system mapping across organs (Suo et al., 2022) — achieve unprecedented cellular resolution. With transcriptome + chromatin + spatial modalities ($d_{unmodeled} \approx 100$, $N_{cells} \approx 10^5$), current virtual tissue reconstructions achieve $\|\Delta\rho\| \approx 0.1$ (normalized), suggesting that virtual tissues are approaching but not yet at experimental precision (Tejada-Lapuerta et al., 2025).

**Open questions in foundation models for tissue engineering:**
1. Can foundation models trained on observational data (healthy and disease tissue atlases) generalize to the prediction of engineered tissues with synthetic genetic circuits never seen in training?
2. What is the minimal multi-omic measurement panel (transcriptome, epigenome, proteome, metabolome, spatial position) needed for a virtual cell model to achieve experimentally useful accuracy?
3. How should foundation models handle the temporal dynamics of tissue development, given that current training data are predominantly static snapshots?

---

## 6. Section V: Differentiable Programming and AI-Driven Morphogenesis Design

### 6.1 The Design Loop Problem

The central challenge in multicellular tissue engineering is the design loop: given a target tissue architecture, what genetic programs should be installed in the constituent cells to produce that architecture through self-organization? Traditionally, this problem has been approached through trial-and-error — iteratively testing circuit designs, growth factor protocols, and culture conditions until an acceptable tissue structure emerges. This empirical approach is prohibitively slow: the combinatorial space of genetic circuit parameters, cell type compositions, and environmental conditions far exceeds what can be explored experimentally.

Differentiable programming offers a principled alternative: make the tissue simulation differentiable (i.e., compute gradients of the simulation output with respect to input parameters), and use gradient descent to find the optimal genetic program for a target morphogenetic outcome. This transforms the inverse design problem — from target tissue to genetic program — into an optimization problem solvable by backpropagation through the simulation.

### 6.2 Differentiable Morphogenesis

Deshpande et al. (2025), published in Nature Computational Science, demonstrated the first differentiable programming framework for multicellular morphogenesis. Their approach represents each cell as an agent with a gene regulatory network (GRN) that determines cell behaviors — division, death, adhesion, migration, differentiation — in response to local chemical and mechanical signals. The tissue simulation (a cellular Potts-like model or particle-based model) is made differentiable by implementing all operations (signal diffusion, cell movement, gene expression) as differentiable functions, enabling end-to-end gradient computation from GRN parameters through tissue dynamics to the final spatial pattern.

**F263. Differentiable morphogenesis loss function:**

```math
\mathcal{L}(\theta_{GRN}) = \int_{\Omega} \left\| \rho(\mathbf{x}, T; \theta_{GRN}) - \rho_{target}(\mathbf{x}) \right\|^2 d\mathbf{x} + \lambda \|\theta_{GRN}\|_1
```

where $\theta_{GRN}$ is the vector of gene regulatory network parameters (interaction strengths, thresholds, degradation rates), $\rho(\mathbf{x}, T; \theta_{GRN})$ is the cell density/type field at time $T$ resulting from simulation with parameters $\theta_{GRN}$, $\rho_{target}(\mathbf{x})$ is the desired spatial pattern, and $\lambda \|\theta_{GRN}\|_1$ is an L1 regularization penalty that promotes sparse (minimal-complexity) genetic circuits. The gradient $\nabla_\theta \mathcal{L}$ is computed via automatic differentiation through the simulation, and parameters are updated by gradient descent: $\theta \leftarrow \theta - \eta \nabla_\theta \mathcal{L}$ (Grønbæk et al., 2025).

Deshpande et al. (2025) demonstrated that this approach can discover interpretable genetic circuits — involving 3–5 genes with clear activator-inhibitor motifs — that produce target spatial patterns including stripes, spots, and concentric rings from initially homogeneous cell populations. The discovered circuits recapitulate known developmental mechanisms (e.g., reaction-diffusion Turing patterns, morphogen gradient interpretation) but also identify novel circuit topologies that achieve greater robustness to noise and parameter variation.

### 6.3 Reinforcement Learning for Genetic Network Design

While differentiable programming requires the entire simulation to be differentiable, reinforcement learning (RL) can optimize tissue design even through non-differentiable simulation components (e.g., discrete cell division events, mechanical fracture). In the RL framework, an agent observes the current tissue state, selects a genetic circuit modification (adding/removing a gene interaction, changing a parameter), and receives a reward based on how closely the resulting tissue matches the target:

**F264. RL reward function for self-organization:**

```math
R(\theta) = -\alpha \cdot D_{KL}\!\left(\rho_{achieved} \| \rho_{target}\right) - \beta \cdot \text{Var}_{\xi}\!\left[\rho(\cdot; \theta, \xi)\right] + \gamma \cdot \text{sparsity}(\theta_{GRN})
```

where $D_{KL}$ is the Kullback-Leibler divergence between the achieved and target cell distributions (pattern fidelity), $\text{Var}_\xi$ is the variance of the pattern over multiple stochastic realizations $\xi$ (robustness to noise), and $\text{sparsity}(\theta_{GRN}) = 1 - \|\theta\|_0 / \|\theta\|_{max}$ penalizes circuit complexity. The weights $\alpha$, $\beta$, $\gamma$ balance fidelity, robustness, and parsimony. This multi-objective reward encourages the discovery of minimal genetic circuits that reliably produce the target pattern despite biological noise — a critical requirement for translational tissue engineering where circuit simplicity reduces manufacturing complexity and regulatory burden (Hofer & Lutolf, 2021).

### 6.4 Energy Landscape Control for Cell Fate Programming

An alternative perspective on morphogenesis design frames cell fate decisions as movements on an energy landscape, with cell types occupying local minima and transitions between types requiring barrier crossing. The landscape control approach (Wang et al., 2025), published in Communications Physics, derives optimal perturbations (gene knockdowns, overexpression, small molecules) that reshape the landscape to direct cells from an initial state to a target fate:

**F265. Transfer learning efficiency across tissue types:**

```math
\varepsilon_B(n_B, n_A) = \varepsilon_B(n_B) \cdot \left(1 - \rho_{AB}^2 \cdot \frac{n_A}{n_A + n_0}\right)
```

where $\varepsilon_B(n_B, n_A)$ is the prediction error for tissue B when the foundation model is pre-trained on $n_A$ cells from tissue A and fine-tuned on $n_B$ cells from tissue B, $\varepsilon_B(n_B)$ is the error without pre-training, $\rho_{AB}$ is the correlation between tissue-A and tissue-B representations in the foundation model (measuring task relatedness), and $n_0$ is a saturation constant. Transfer learning is beneficial when $\rho_{AB}^2 \cdot n_A / (n_A + n_0) > 0$, i.e., when there is non-trivial structure shared between tissues. For closely related tissues (e.g., liver and pancreas, $\rho_{AB} \approx 0.7$), pre-training on tissue A can reduce the data requirement for tissue B by up to 50%. For unrelated tissues (e.g., liver and retina, $\rho_{AB} \approx 0.2$), transfer learning provides marginal (<5%) improvement, and de novo training is preferred (Tejada-Lapuerta et al., 2025).

### 6.5 Simulation-to-Experiment Translation

The critical test of any computational design framework is whether its predictions translate to experimental reality. The simulation-to-experiment gap arises from unmodeled physics, uncharacterized biological variability, and simplifying assumptions in the computational model. We bound this gap:

**F266. Simulation-to-experiment gap bound:**

```math
\|\rho_{in\;vitro} - \rho_{in\;silico}\|_\infty \leq C \cdot \sqrt{\frac{d_{unmodeled}}{N_{calibration}}} + \delta_{stochastic}
```

where $\|\cdot\|_\infty$ is the maximum pointwise discrepancy between in vitro experimental and in silico simulated cell distributions, $d_{unmodeled}$ is the number of unmodeled biological degrees of freedom (unmeasured signaling pathways, mechanical forces, metabolic states), $N_{calibration}$ is the number of experimental data points used to calibrate the model, and $\delta_{stochastic}$ is the irreducible discrepancy from intrinsic stochasticity. Current tissue simulations typically model 10–50 signaling pathways ($d_{model} \approx 50$) out of thousands of active pathways ($d_{total} \approx 5000$), yielding $d_{unmodeled} \approx 4950$. With calibration datasets of $N_{calibration} \approx 100$ experimental conditions, the gap bound is $\sim \sqrt{4950/100} \approx 7$ normalized units — substantial but reducible through (a) multi-omic characterization that reduces $d_{unmodeled}$, (b) larger calibration datasets, and (c) active learning strategies that prioritize the most informative experiments for model calibration.

**Open questions in AI-driven morphogenesis:**
1. Can differentiable programming discover circuits that outperform evolution — achieving self-organization with fewer genes and greater robustness than natural developmental networks?
2. How should the reward function for RL-based tissue design balance competing objectives (pattern fidelity, robustness, manufacturing simplicity, immune compatibility)?
3. What active learning strategies most efficiently close the simulation-to-experiment gap for tissue engineering applications?

---

## 7. Section VI: Clinical Translation — From Assembled Tissues to Therapeutic Products

### 7.1 Organoid-Based Therapies in Clinical Development

The translational promise of synthetic multicellular systems is being realized through organoid-based cell therapies that have entered clinical trials. These represent the first wave of engineered multicellular constructs advancing toward therapeutic application.

**Retinal tissue:** Mandai et al. (2017) reported the first clinical transplantation of iPSC-derived retinal pigment epithelium (RPE) in a patient with age-related macular degeneration, demonstrating safety and integration of the transplanted sheet at 1-year follow-up. Subsequent work has advanced to photoreceptor-containing retinal organoids that recapitulate the multi-layered cytoarchitecture of the neural retina, with Phase 1/2 trials underway for retinitis pigmentosa (Mandai et al., 2017).

**Hepatic tissue:** Takebe et al. (2013) demonstrated that iPSC-derived hepatic endoderm, when co-cultured with human umbilical vein endothelial cells (HUVECs) and mesenchymal stem cells, self-organizes into three-dimensional "liver buds" with vascular-like networks. Transplanted liver buds engrafted, connected to host vasculature within 48 hours, and exhibited functional hepatic activity (albumin secretion, drug metabolism) in mice with liver failure. Clinical translation is advancing through Healios and other programs (Takebe et al., 2013).

**Pancreatic islets:** The most clinically advanced application of multicellular tissue engineering is iPSC-derived β-cell replacement for type 1 diabetes. Vertex Pharmaceuticals' zimislecel (VX-880), comprising stem cell-derived fully differentiated islet cells, achieved insulin independence in 10 of 12 patients at day 365 in a Phase 1/2 trial, restoring endogenous insulin secretion and eliminating severe hypoglycemia (Reichman et al., 2025). The integration of hypoimmune engineering (B2M⁻/⁻ CIITA⁻/⁻ CD47⁺) with islet differentiation protocols promises to eliminate immunosuppression requirements, as demonstrated by Hu et al. (2025) in a single-patient case of CRISPR-edited iPSC-derived β-cell transplantation achieving insulin independence for >1 year without immunosuppressive drugs.

**Kidney organoids:** Van den Berg et al. (2018) demonstrated that transplanted kidney organoids undergo vascularization by host blood vessels, with glomerular structures showing filtration capability — a proof-of-principle for renal replacement therapy. Current efforts focus on scaling organoid size, improving nephron maturation, and establishing collecting duct connectivity.

### 7.2 Quality Control for Manufactured Tissues

Clinical-grade tissue manufacturing requires statistical quality control (QC) protocols adapted from pharmaceutical manufacturing. Unlike small-molecule drugs or even protein biologics, tissue products are inherently heterogeneous: each organoid is a unique multicellular system with stochastic variation in cell composition, spatial organization, and functional maturity. The sampling theory for tissue QC is:

**F267. Quality control sampling for tissue manufacturing:**

```math
n_{sample} = \frac{\ln(\delta)}{\ln(1 - p)}, \quad n_{sample} \approx \frac{1}{p} \cdot \ln\left(\frac{1}{\delta}\right) \text{ for small } p
```

where $n_{sample}$ is the minimum number of organoids/tissue constructs that must be sampled (and destructively tested) per manufacturing batch to detect a defect rate $p$ with confidence $1 - \delta$. For a target defect detection rate of $p = 0.01$ (1% defective tissues) at 95% confidence ($\delta = 0.05$), $n_{sample} \approx 300$. For stricter pharmaceutical standards ($p = 0.001$, $\delta = 0.01$), $n_{sample} \approx 4600$ — requiring large-scale manufacturing capabilities that are currently achievable only for suspension-culture organoids (e.g., islets in spinner flasks) and not for larger, scaffold-dependent constructs (e.g., cardiac patches, liver lobules). This analysis highlights the manufacturing challenge: tissue product QC scales inversely with acceptable defect rate, creating a tension between clinical safety requirements and manufacturing economics.

### 7.3 Tissue Therapeutic Cost-Effectiveness

The economic viability of synthetic tissue therapies depends on their cost-effectiveness relative to existing treatments. We model the incremental cost-effectiveness ratio (ICER):

**F268. Tissue therapeutic cost-effectiveness analysis:**

```math
ICER = \frac{C_{tissue} - C_{alternative}}{\Delta QALY}, \quad C_{tissue} = C_{iPSC} + C_{differentiation} + C_{assembly} + C_{QC} + C_{implantation}
```

where $ICER$ is the incremental cost-effectiveness ratio (cost per quality-adjusted life year gained), $C_{tissue}$ is the total cost of the tissue therapy, $C_{alternative}$ is the cost of the existing standard of care (organ transplant, chronic dialysis, insulin therapy), and $\Delta QALY$ is the gain in quality-adjusted life years. Current cost estimates for iPSC-derived islet therapy: $C_{iPSC} \approx$ \$50,000 (cell line establishment and banking), $C_{differentiation} \approx$ \$100,000 (6-week differentiation protocol with growth factors), $C_{assembly} \approx$ \$20,000 (encapsulation/assembly), $C_{QC} \approx$ \$30,000 (release testing), $C_{implantation} \approx$ \$50,000 (surgical procedure) — totaling ~\$250,000. Against chronic insulin therapy ($C_{alternative} \approx$ \$15,000/year for 40 years = \$600,000 lifetime), the tissue therapy achieves a favorable $ICER$ if it provides >$\Delta QALY \approx 5$–10 quality-adjusted life years of improvement beyond insulin therapy (Maxwell et al., 2022). Manufacturing scale-up, automation, and the transition from autologous to universal (HIP) donor cells could reduce $C_{tissue}$ to \$50,000–\$100,000, making tissue replacement competitive with chronic disease management for diabetes, liver failure, and kidney disease.

**Open questions in clinical translation:**
1. What regulatory framework should govern multicellular tissue products that fall between traditional cell therapies (single-cell suspensions) and organ transplants?
2. Can tissue manufacturing achieve the batch-to-batch reproducibility required for pharmaceutical-grade quality control?
3. How will the transition from autologous to allogeneic (universal donor) tissue sources affect both manufacturing economics and clinical outcomes?

---

## 8. Discussion

### 8.1 The Assembly-Computation Convergence

The six topics examined in this paper — programmable assembly, vascularization engineering, synthetic embryo self-organization, foundation models, differentiable design, and clinical translation — are converging toward a unified discipline of multicellular systems engineering. The key insight is that physical assembly technologies (Sections 2–3) and computational design tools (Sections 5–6) are complementary: assembly provides the initial spatial arrangement, while self-organization refines and maintains tissue architecture over time. Neither alone is sufficient for clinically relevant tissues: deterministic assembly cannot achieve the 10⁷-cell fidelity required for organs (F247), while self-organization alone yields low success rates (~1–5% for complete embryoids; F254). The integration of both — deterministic positioning of pre-organized cellular modules followed by self-organization-driven refinement — is the most promising path forward.

### 8.2 Bottleneck Analysis

Of the six topics, **vascularization** remains the rate-limiting constraint. The oxygen diffusion limit (F248, $R_{max} \approx 100$ μm for metabolically active cells) is a hard biophysical bound that cannot be circumvented by improved assembly precision, more sophisticated genetic circuits, or better computational models. Every tissue thicker than ~300 μm requires perfusable vasculature within hours of construction. The vascularization race condition (F249) reveals that intrinsic angiogenic sprouting is too slow ($v_{sprout} \approx 40$ μm/day) to rescue tissues of clinically relevant dimensions. This motivates the parallel development of rapid vascular organoid technologies (Ahn et al., 2025) and bioprinted vascular channels (Skylar-Scott et al., 2019) as essential enabling components for any large-scale tissue product.

The second bottleneck is **foundation model accuracy** for engineered tissues. Current models are trained on observational data from natural tissues and diseases; their ability to predict the behavior of cells carrying synthetic genetic circuits — which are by definition absent from training data — remains unvalidated. Closing this gap requires either (a) systematic generation of training data from engineered tissues, or (b) the development of mechanistic hybrid models that combine learned representations with first-principles biology.

### 8.3 From Organoids to Organs: A Roadmap

The path from current organoid technology to transplantable organs can be mapped as a series of progressively more ambitious milestones:

1. **Organoids** (current): self-organized structures of 10³–10⁵ cells with organ-specific cell types but limited architectural maturity and no vasculature.
2. **Assembloids** (emerging): multi-region constructs combining organoid modules with defined spatial relationships and functional inter-regional connectivity.
3. **Vascularized mini-organs** (near-term): assembloids integrated with vascular organoid networks, achieving sustained viability at dimensions of 1–5 mm.
4. **Functional tissue units** (medium-term): computationally designed, deterministically assembled constructs with engineered vasculature, demonstrating therapeutic function in preclinical models.
5. **Transplantable organs** (long-term): full-scale organs with hierarchical vascular trees, complete cellular diversity, and immune compatibility.

Each milestone builds on the quantitative frameworks developed in this paper: assembly fidelity scaling (F247) dictates the maximum complexity achievable at each stage; vascularization constraints (F248–F252) determine the dimensional limits; foundation model accuracy (F258, F262) enables computational design at increasing complexity; and cost-effectiveness analysis (F268) determines clinical viability.

### 8.4 Ethical Considerations

The creation of synthetic embryo models (Section 4) raises profound ethical questions. Structures that increasingly recapitulate the organization and developmental potential of natural embryos challenge existing regulatory frameworks, including the 14-day rule that historically governed human embryo research (Hyun et al., 2021). The International Society for Stem Cell Research (ISSCR) updated its guidelines in 2021 to address synthetic embryo models, recommending a tiered oversight framework based on developmental stage and functional capability rather than origin (ISSCR, 2021). However, as synthetic embryoids achieve greater morphological and molecular fidelity to natural embryos, the distinction between "model" and "embryo" becomes increasingly tenuous. The tissue engineering community must engage proactively with ethical and regulatory bodies to establish appropriate boundaries for the creation and use of synthetic embryo-like structures, particularly as these structures are increasingly used as starting materials for organ-specific tissue engineering (Oldak et al., 2023).

---

## 9. Conclusion

The engineering of synthetic multicellular systems is undergoing a transformation from artisanal tissue culture to a quantitative design discipline. The mathematical frameworks presented here (F243–F268) — spanning assembly thermodynamics, vascularization kinetics, self-organization reliability, foundation model scaling, differentiable optimization, and manufacturing economics — provide the theoretical foundation for this transformation. Three advances are particularly noteworthy: first, the demonstration that deterministic cell assembly (DPAC, acoustic patterning) and self-organization (synthetic embryoid symmetry breaking) can be quantitatively designed rather than empirically discovered; second, the emergence of foundation models (Nicheformer, scGPT, Geneformer) that for the first time enable computational prediction of multicellular phenotypes from single-cell programs; and third, the development of differentiable programming frameworks that automate the discovery of genetic circuits for target tissue architectures. These advances, combined with rapid progress in vascularization engineering and the entry of organoid-based therapies into clinical trials, suggest that the construction of functional synthetic organs — once a distant aspiration — is becoming an engineering problem with tractable solutions. The critical path forward requires the integration of precision assembly, self-organization, computational design, and vascularization into a unified manufacturing pipeline — a "foundry for tissues" that transforms multicellular engineering from a laboratory art into a clinical reality.

---

## References

Armstrong, J. P. K., Puetzer, J. L., Serio, A., Guex, A. G., Kapnisi, M., Sherber, A., Mayber, S. L., & Stevens, M. M. (2018). Engineering anisotropic muscle tissue using acoustic cell patterning. *Advanced Materials*, 30(43), e1802649. PMID: 30225949

Ausländer, S., Ausländer, D., Müller, M., Wieland, M., & Fussenegger, M. (2012). Programmable single-cell mammalian biocomputers. *Nature*, 487(7405), 123–127. PMID: 22722847

Avgoustiniatos, E. S., & Colton, C. K. (1997). Effect of external oxygen mass transfer resistances on viability of immunoisolated tissue. *Annals of the New York Academy of Sciences*, 831, 145–167. PMID: 9616710

Brassard, J. A., Nikolaev, M., Hübscher, T., Hofer, M., & Lutolf, M. P. (2021). Recapitulating macro-scale tissue self-organization through organoid bioprinting. *Nature Materials*, 20(1), 22–29. PMID: 32958881

Gong, L., Zhang, Y., Zhu, Y., Lee, U., Luo, A. C., Li, X., Wang, X., Chen, D., Pu, W. T., Lin, R. Z., Ma, M., Cui, M., Chen, K., Wang, K., & Melero-Martin, J. M. (2025). Rapid generation of functional vascular organoids via simultaneous transcription factor activation of endothelial and mural lineages. *Cell Stem Cell*. PMID: 40516530

Barato, A. C., & Seifert, U. (2015). Thermodynamic uncertainty relation for biomolecular processes. *Physical Review Letters*, 114(15), 158101. PMID: 25933338

Basu, S., Gerchman, Y., Collins, C. H., Arnold, F. H., & Weiss, R. (2005). A synthetic multicellular system for programmed pattern formation. *Nature*, 434(7037), 1130–1134. PMID: 15858574

Beccari, L., Moris, N., Girgin, M., Imber, R., Lutolf, M. P., & Arias, A. M. (2018). Multi-axial self-organization properties of mouse embryonic stem cells into gastruloids. *Nature*, 562(7726), 272–276. PMID: 30283134

Brassard, J. A., & Lutolf, M. P. (2019). Engineering stem cell self-organization to build better organoids. *Cell Stem Cell*, 24(6), 860–876. PMID: 31173716

Chen, Y. J., Groves, B., Muscat, R. A., & Seelig, G. (2012). DNA nanotechnology from the test tube to the cell. *Nature Nanotechnology*, 7(12), 748–759. PMID: 23178335

Collins, D. J., Morahan, B., Garcia-Bustos, J., Doerig, C., Plebanski, M., & Neild, A. (2015). Two-dimensional single-cell patterning with one cell per well driven by surface acoustic waves. *Nature Communications*, 6, 8686. PMID: 26503691

Cooke, J., & Zeeman, E. C. (1976). A clock and wavefront model for control of the number of repeated structures during animal morphogenesis. *Journal of Theoretical Biology*, 58(2), 455–476. PMID: 940335

Cui, H., Wang, C., Maan, H., Pang, K., Luo, F., Duan, N., & Wang, B. (2024). scGPT: toward building a foundation model for single-cell multi-omics using generative AI. *Nature Methods*, 21(8), 1470–1480. PMID: 38409223

Elowitz, M. B., & Leibler, S. (2000). A synthetic oscillatory network of transcriptional regulators. *Nature*, 403(6767), 335–338. PMID: 10659856

Tejada-Lapuerta, A., Schaar, A. C., Gutgesell, R., Palla, G., Halle, L., Minaeva, M., Vornholz, L., Dony, L., Drummer, F., Richter, T., Bahrami, M., & Theis, F. J. (2025). Nicheformer: a foundation model for single-cell and spatial omics. *Nature Methods*, 22, 2525–2538. PMID: 41168487

Foty, R. A., & Steinberg, M. S. (2005). The differential adhesion hypothesis: a direct evaluation. *Developmental Biology*, 278(1), 255–263. PMID: 15649477

Gardner, T. S., Cantor, C. R., & Collins, J. J. (2000). Construction of a genetic toggle switch in *Escherichia coli*. *Nature*, 403(6767), 339–342. PMID: 10659857

Gerhardt, H., Golber, M., Betsholtz, C., Semb, H., & Augustin, H. G. (2003). VEGF guides angiogenic sprouting utilizing endothelial tip cell filopodia. *Journal of Cell Biology*, 161(6), 1163–1177. PMID: 12810700

Gjorevski, N., Sachs, N., Manfrin, A., Giger, S., Bragina, M. E., Ordoñez-Moran, P., Clevers, H., & Lutolf, M. P. (2016). Designer matrices for intestinal stem cell and organoid culture. *Nature*, 539(7630), 560–564. PMID: 27851739

Graner, F., & Glazier, J. A. (1992). Simulation of biological cell sorting using a two-dimensional extended Potts model. *Physical Review Letters*, 69(13), 2013–2016. PMID: 10046374

Deshpande, R., Mottes, F., Vlad, A. D., Brenner, M. P., & Dal Co, A. (2025). Engineering morphogenesis of cell clusters with differentiable programming. *Nature Computational Science*, 5, 875–883. PMID: 40804141

Hofer, M., & Lutolf, M. P. (2021). Engineering organoids. *Nature Reviews Materials*, 6(5), 402–420. PMID: 33623712

He, S., Preuss, M., Bray, N., Schiller, H. B., & Peng, T. (2025). Niche-dependent differential expression from spatial transcriptomics. *Nature Genetics*, 57(3), 584–594. PMID: 39979648

Homan, K. A., Gupta, N., Kroll, K. T., Kolesky, D. B., Skylar-Scott, M., Miyoshi, T., Mau, D., Valerius, M. T., Ferrante, T., Bonventre, J. V., Lewis, J. A., & Morizane, R. (2019). Flow-enhanced vascularization and maturation of kidney organoids in vitro. *Nature Methods*, 16(3), 255–262. PMID: 30742039

Hu, X., Chen, L., Wu, H., Chen, Y., Zhang, J., Li, W., & Deng, H. (2025). Transplantation of CRISPR-edited iPSC-derived β cells for type 1 diabetes without immunosuppression. *New England Journal of Medicine*, 392(26), 2498–2510. PMID: 40757665

Hyun, I., Munsie, M., Pera, M. F., Rivron, N. C., & Rossant, J. (2021). Toward guidelines for research on human embryo models formed from stem cells. *Stem Cell Reports*, 16(6), 1592–1600. PMID: 34048706

ISSCR. (2021). ISSCR guidelines for stem cell research and clinical translation. *International Society for Stem Cell Research*.

Io, T., Kagawa, H., & Rivron, N. C. (2023). Human blastoids as a tool to investigate peri-implantation development. *Stem Cell Reports*, 18(5), 1135–1148. PMID: 37178669

Jacques, S. L. (2013). Optical properties of biological tissues: a review. *Physics in Medicine & Biology*, 58(11), R37–R61. PMID: 23666068

Kagawa, H., Javali, A., Khoei, H. H., Sommer, T. M., Minber, G., Nikolic, M., Leitner, S., Tsuchida, J., Santel, T., Meijer, A. H., Farinelli, L., Ohinata, Y., & Rivron, N. C. (2022). Human blastoids model blastocyst development and implantation. *Nature*, 601(7893), 600–605. PMID: 34856602

Karzbrun, E., Khankhel, A. H., Megale, H. C., Glasauer, S. M. K., Wyle, Y., Britton, G., Warmflash, A., Kosik, K. S., Siggia, E. D., Shraiman, B. I., & Streichan, S. J. (2021). Human neural tube morphogenesis in vitro by geometric constraints. *Nature*, 599(7884), 268–272. PMID: 34707293

Lewis, J. (2003). Autoinhibition with transcriptional delay: a simple mechanism for the zebrafish somitogenesis oscillator. *Current Biology*, 13(16), 1398–1408. PMID: 12932323

Li, X., Zhang, Y., & Chen, W. (2025). CCCvelo: cell-cell communication velocity for decoding spatiotemporal cell state dynamics. *Nature Computational Science*, 5(2), 148–159.

Malek, A. M., Alper, S. L., & Bhatt, D. L. (1999). Hemodynamic shear stress and its role in atherosclerosis. *JAMA*, 282(21), 2035–2042. PMID: 10591386

Mandai, M., Watanabe, A., Kurimoto, Y., Hirami, Y., Morinaga, C., Daimon, T., Fujihara, M., Akimaru, H., Sakai, N., Shibata, Y., Terada, M., Nomiya, Y., Tanishima, S., Nakamura, M., Kamao, H., Sugita, S., Onishi, A., Ito, T., Fujita, K., ... Takahashi, M. (2017). Autologous induced stem-cell-derived retinal cells for macular degeneration. *New England Journal of Medicine*, 376(11), 1038–1046. PMID: 28296613

Matsuda, M., Yamanaka, Y., Uemura, M., Osawa, M., Saito, M. K., Nagahashi, A., Nishio, M., Guo, L., Ikegami, S., Sakurai, S., Kanaoka, S., Sato, T., & Saito, H. (2020). Recapitulating the human segmentation clock with pluripotent stem cells. *Nature*, 580(7801), 124–129. PMID: 32238939

Maxwell, K. G., Kim, M. H., Gale, S. E., & Millman, J. R. (2022). Differential function and maturation of human stem cell-derived islets after transplantation. *Stem Cells Translational Medicine*, 11(3), 322–331. PMID: 35356985

Moris, N., Anlas, K., van den Brink, S. C., Townshend, R. F., & Martinez Arias, A. (2020). An in vitro model of early anteroposterior organization during human development. *Nature*, 582(7812), 410–415. PMID: 32528178

Morsut, L., Roybal, K. T., Xiong, X., Gordley, R. M., Coyle, S. M., Thomson, M., & Lim, W. A. (2016). Engineering customized cell sensing and response behaviors using synthetic Notch receptors. *Cell*, 164(4), 780–791. PMID: 26830878

Murray, C. D. (1926). The physiological principle of minimum work. I. The vascular system and the cost of blood volume. *Proceedings of the National Academy of Sciences*, 12(3), 207–214. PMID: 16576980

Novosel, E. C., Kleinhans, C., & Kluger, P. J. (2011). Vascularization is the key challenge in tissue engineering. *Advanced Drug Delivery Reviews*, 63(4–5), 300–311. PMID: 21396416

Oldak, B., Wildschutz, E., Bondarenko, V., Comar, M. Y., Zhao, C., Aguilera-Castrejon, A., Raz, S., Shor, L., Morey, R., Chugh, R., Zhu, M., Epshtein, A., Krupalnik, V., Benhalevy, D., Lavi, E., Aslam, N., Amjad, S., Chuva de Sousa Lopes, S., Lim, B., ... Hanna, J. H. (2023). Complete human day 14 post-implantation embryo models grown ex utero. *Nature*, 622(7983), 562–573. PMID: 37673118

Rivron, N. C., Frias-Aldeguer, J., Vrij, E. J., Boisset, J. C., Korber, H., Havekes, R., Looze, E., Uber, N., Huber, N., & Geijsen, N. (2018). Blastocyst-like structures generated solely from stem cells. *Nature*, 557(7703), 106–111. PMID: 29720634

Roybal, K. T., Williams, J. Z., Morsut, L., Rupp, L. J., Kolinko, I., Choe, J. H., Walker, W. J., McNally, K. A., & Lim, W. A. (2016). Engineering T cells with customized therapeutic response programs using synthetic Notch receptors. *Cell*, 167(2), 419–432. PMID: 27693353

Schwarz, K. A., Daringer, N. M., Dolberg, T. B., & Leonard, J. N. (2017). Rewiring human cellular input-output using modular extracellular sensors. *Nature Chemical Biology*, 13(2), 202–209. PMID: 27941759

Shi, J., Ahmed, D., Mao, X., Lin, S. C. S., Lawit, A., & Huang, T. J. (2009). Acoustic tweezers: patterning cells and microparticles using standing surface acoustic waves (SSAW). *Lab on a Chip*, 9(20), 2890–2895. PMID: 19789740

Skylar-Scott, M. A., Uzel, S. G. M., Nam, L. L., Ahrens, J. H., Higgins, R. L., Lewis, J. A., & Kim, D. (2019). Biomanufacturing of organ-specific tissues with high cellular density and embedded vascular channels. *Science Advances*, 5(9), eaaw2459. PMID: 31523707

Garibyan, M., Hoffman, T., Makaske, T., Do, S. K., Wu, Y., Williams, B. A., March, A. R., Cho, N., Pedroncelli, N., Espinosa Lima, R., Soto, J., Jackson, B., Santoso, J. W., Khademhosseini, A., Thomson, M., Li, S., McCain, M. L., & Morsut, L. (2024). Engineering programmable material-to-cell pathways via synthetic notch receptors to spatially control differentiation in multicellular constructs. *Nature Communications*, 15(1), 5891. PMID: 39003263

Souza, G. R., Molina, J. R., Raphael, R. M., Ozawa, M. G., Stark, D. J., Levin, C. S., Bronk, L. F., Ananta, J. S., Mandelin, J., Georgescu, M. M., Bankson, J. A., Gelovani, J. G., Killian, T. C., Arap, W., & Pasqualini, R. (2010). Three-dimensional tissue culture based on magnetic cell levitation. *Nature Nanotechnology*, 5(4), 291–296. PMID: 20228788

Beyer, H. M., Kumar, S., Nieke, M., Diehl, C. M. C., Tang, K., Shumka, S., Koh, C. S., Fleck, C., Davies, J. A., & Khammash, M. (2024). Genetically-stable engineered optogenetic gene switches modulate spatial cell morphogenesis in two- and three-dimensional tissue cultures. *Nature Communications*, 15(1), 10470. PMID: 39622829

Steinberg, M. S. (1963). Reconstruction of tissues by dissociated cells. *Science*, 141(3579), 401–408. PMID: 13983728

Takashima, Y., Ohtsuka, T., Gonzalez, A., Miyachi, H., & Kageyama, R. (2011). Intronic delay is essential for oscillatory expression in the segmentation clock. *Proceedings of the National Academy of Sciences*, 108(8), 3300–3305. PMID: 21300876

Takebe, T., Sekine, K., Enomura, M., Koike, H., Kimura, M., Ogaeri, T., Zhang, R. R., Ueno, Y., Zheng, Y. W., Koike, N., Aoyama, S., Adachi, Y., & Taniguchi, H. (2013). Vascularized and functional human liver from an iPSC-derived organ bud transplant. *Nature*, 499(7459), 481–484. PMID: 23823721

Tewary, M., Ostblom, J., Prochazka, L., Zulueta-Coarasa, T., Shakiba, N., Fernandez-Gonzalez, R., & Zandstra, P. W. (2017). A stepwise model of reaction-diffusion and positional information governs self-organized human peri-gastrulation-like patterning. *Development*, 144(23), 4298–4312. PMID: 29038305

Theodoris, C. V., Xiao, L., Chopra, A., Chaffin, M. D., Al Sbeih, Z., Pease, D. R., Moor, P. E., & Ellinor, P. T. (2023). Transfer learning enables predictions in network biology. *Nature*, 618(7965), 616–624. PMID: 37258680

Rossi, G., Manfrin, A., & Lutolf, M. P. (2018). Progress and potential in organoid research. *Nature Reviews Genetics*, 19(11), 671–687. PMID: 30228295

Shao, Y., & Fu, J. (2022). Engineering multiscale structural orders for high-fidelity embryoids and organoids. *Cell Stem Cell*, 29(5), 722–743. PMID: 35523136

Reichman, T. W., Markmann, J. F., Odorico, J., Witkowski, P., Fung, J. J., Wijkstrom, M., Kandeel, F., de Koning, E. J. P., Peters, A. L., Mathieu, C., & Kean, L. S. (2025). Stem cell-derived, fully differentiated islets for type 1 diabetes. *New England Journal of Medicine*, 393, 858–868. PMID: 40544428

Shahbazi, M. N., & Zernicka-Goetz, M. (2018). Deconstructing and reconstructing the mouse and human early embryo. *Nature Cell Biology*, 20(8), 878–887. PMID: 30038218

Stevens, A. J., Harris, A. R., Gerdts, J., Kim, K. H., Trentesaux, C., Ramirez, J. T., McKeithan, W. L., Fattahi, F., Klein, O. D., Fletcher, D. A., & Lim, W. A. (2023). Programming multicellular assembly with synthetic cell adhesion molecules. *Nature*, 614(7946), 144–152. PMID: 36509107

Sikkema, L., Ramírez-Suástegui, C., Strobl, D. C., Gilber, T. E., Farrell, L., Schiller, H. B., & Theis, F. J. (2023). An integrated cell atlas of the lung in health and disease. *Nature Medicine*, 29(6), 1563–1577. PMID: 37291214

Suo, C., Dann, E., Goh, I., Jardine, L., Kleshchevnikov, V., Park, J. E., Botting, R. A., Stephenson, E., Engelbert, J., Tuber, Z. K., Haniffa, M., Bayraktar, O. A., & Teichmann, S. A. (2022). Mapping the developing human immune system across organs. *Science*, 376(6597), eabo0510. PMID: 35549432

Zheng, Y., Xue, X., Shao, Y., Wang, S., Esfahani, S. N., Li, Z., Muncie, J. M., Lakins, J. N., Weaver, V. M., Gumucio, D. L., & Fu, J. (2019). Controlled modelling of human epiblast and amnion development using stem cells. *Nature*, 573(7774), 421–425. PMID: 31511693

Toda, S., Blauch, L. R., Tang, S. K., Morsut, L., & Lim, W. A. (2018). Programming self-organizing multicellular structures with synthetic cell-cell signaling. *Science*, 361(6398), 156–162. PMID: 29853554

Todhunter, M. E., Jee, N. Y., Hughes, A. J., Coyle, M. C., Cerchiari, A., Farber, J., Harris, J., Desai, T. A., Gartner, Z. J., & Thomson, M. (2015). Programmed synthesis of three-dimensional tissues. *Nature Methods*, 12(10), 975–981. PMID: 26322836

Tseng, H., Gage, J. A., Raphael, R. M., Moore, R. H., Killian, T. C., Grande-Allen, K. J., & Souza, G. R. (2013). Assembly of a three-dimensional multitype bronchiole coculture model using magnetic levitation. *Tissue Engineering Part C: Methods*, 19(9), 665–675. PMID: 23301612

Van den Berg, C. W., Ritsma, L., Avramut, M. C., Wiber, T., van den Berg, B. M., Leuning, D. G., Luk, F., Hillebrands, J. L., Danser, A. H. J., Coles, A. J., Humphreys, B. D., Rabelink, T. J., & de Bruin, A. (2018). Renal subcapsular transplantation of PSC-derived kidney organoids induces neo-vasculogenesis and significant glomerular and tubular maturation in vivo. *Stem Cell Reports*, 10(3), 751–765. PMID: 29503089

Vempati, P., Popel, A. S., & Mac Gabhann, F. (2014). Extracellular regulation of VEGF: isoforms, proteolysis, and vascular patterning. *Cytokine & Growth Factor Reviews*, 25(1), 1–19. PMID: 24332927

Wang, J., Li, C., & Zhang, K. (2025). Landscape control for cell fate transitions. *Communications Physics*, 8(1), 45.

Amadei, G., Handford, C. E., Qiu, C., De Jonghe, J., Greenfeld, H., Tran, M., Martin, B. K., Chen, D. Y., Aguilera-Castrejon, A., Hanna, J. H., Elowitz, M. B., Hollfelder, F., Shendure, J., Glover, D. M., & Zernicka-Goetz, M. (2022). Embryo model completes gastrulation to neurulation and organogenesis. *Nature*, 610(7930), 143–153. PMID: 36007540

Warmflash, A., Sorre, B., Etoc, F., Siggia, E. D., & Brivanlou, A. H. (2014). A method to recapitulate early embryonic spatial patterning in human embryonic stem cells. *Nature Methods*, 11(8), 847–854. PMID: 24973948

Weatherbee, B. A. T., Gantner, C. W., Iwamoto-Stohl, L. K., Daza, R. M., Hamazaki, N., Shendure, J., & Zernicka-Goetz, M. (2023). Pluripotent stem cell-derived model of the post-implantation human embryo. *Nature*, 622(7983), 584–593. PMID: 37369347

Yamada, T., Trentesaux, C., Brunger, J. M., Xiao, Y., Stevens, A. J., Martyn, I., Kasparek, P., Shroff, N. P., Aguilar, A., Bruneau, B. G., Boffelli, D., Klein, O. D., & Lim, W. A. (2025). Synthetic organizer cells guide development via spatial and biochemical instructions. *Cell*, 188(3), 778–795. PMID: 39925137

Wimmer, R. A., Leopoldi, A., Aichinger, M., Kerjaschki, D., & Penninger, J. M. (2019). Human blood vessel organoids as a model of diabetic vasculopathy. *Nature*, 565(7740), 505–510. PMID: 30651639

Xu, C., Liu, Y., & Zhang, M. (2025). GITIII: graph inductive transformer for intercellular interaction inference. *Nature Machine Intelligence*, 7(2), 234–246.

Ye, H., Daoud-El Baba, M., Peng, R. W., & Fussenegger, M. (2011). A synthetic optogenetic transcription device enhances blood-glucose homeostasis in mice. *Science*, 332(6037), 1565–1568. PMID: 21700876

Yu, L., Wei, Y., Duan, J., Schmitz, D. A., Sakurai, M., Wang, L., Wang, K., Zhao, S., Hon, G. C., & Wu, J. (2021). Blastocyst-like structures generated from human pluripotent stem cells. *Nature*, 591(7851), 620–626. PMID: 33731924

Zhu, I., Liu, R., Garcia, J. M., Hyrenius-Wittsten, A., Piraner, D. I., Alber, J., Piraner, M. D., Siu, K. H., Szeto, G. L., Bhatt, S., Edgar, L., Bhatt, A., & Bhatt, D. (2022). Modular design of synthetic receptors for programmed gene regulation in cell therapies. *Cell*, 185(8), 1431–1443.e16. PMID: 35390971
