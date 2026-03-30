# Developmental Biology Review

## Abstract

Embryonic development has long been understood through the lens of morphogen gradients and transcriptional networks, yet a growing body of evidence demonstrates that physical forces — tissue stiffness, fluid shear stress, hydrostatic pressure, and cell-generated contractility — serve as instructive developmental signals whose contributions rival and, in specific contexts, supersede those of chemical cues. This review synthesizes the mechanotransduction pathways (Piezo channels, YAP/TAZ, integrin-LINC axis), the developmental processes they control (gastrulation, neural tube closure, cardiac trabeculation, branching morphogenesis), and the emerging evidence that mechanical and chemical signals form a context-dependent hierarchy. In some developmental events — cardiac valve formation, neural crest delamination — physical forces are the primary instructive signal; in others — anteroposterior axis specification, dorsoventral patterning — chemical gradients lead while mechanical cues provide noise correction and robustness. We present novel mathematical frameworks for quantifying this interplay and discuss how spatial mechano-transcriptomics is now enabling simultaneous measurement of gene expression and tissue mechanics at single-cell resolution in the developing embryo.

---

## 1. Introduction: The Mechanical Imperative in Development

Over a century ago, D'Arcy Wentworth Thompson articulated a radical proposition: that biological form is fundamentally governed by physical forces, and that the shapes of organisms can be understood through the same mathematical principles that describe soap bubbles, liquid drops, and elastic membranes (Thompson, 1917). This vision, captured in *On Growth and Form*, challenged the prevailing gene-centric view of development and established a research program that sought to explain morphogenesis through mechanics (Coen et al., 2017). For decades, however, the molecular revolution in developmental biology overshadowed Thompson's physical perspective, as researchers focused on identifying the genes and signaling molecules — the morphogens, transcription factors, and receptor-ligand interactions — that pattern the embryo (Mammoto & Ingber, 2010).

The pendulum has swung back. The discovery that cells possess dedicated mechanosensory machinery — most notably the Piezo family of mechanically activated ion channels, identified by Coste et al. (2010) — provided the molecular basis for how cells detect and respond to physical forces. The subsequent demonstration that the transcriptional coactivators YAP and TAZ serve as nuclear relays of mechanical signals, transducing extracellular matrix (ECM) stiffness into gene expression programs that govern stem cell fate (Dupont et al., 2011), established a direct causal link between tissue mechanics and cell identity. The landmark finding that mesenchymal stem cells differentiate toward neural, muscle, or bone lineages based solely on substrate stiffness — soft matrices mimicking brain (~0.1–1 kPa) are neurogenic, intermediate stiffness mimicking muscle (~8–17 kPa) is myogenic, and rigid substrates mimicking bone (~25–40 kPa) are osteogenic — demonstrated that mechanical information is sufficient to specify cell fate independently of soluble factors (Engler et al., 2006).

These molecular and cellular insights are now converging with tissue-scale biomechanics to reveal that developing embryos use mechanical forces not merely as passive consequences of growth but as active instructive signals. Tissue fluidity transitions determine when and where cells can rearrange during gastrulation (Mongera et al., 2018). Blood flow shear stress patterns the developing heart (Vignes et al., 2022; Chen et al., 2025). Hydrostatic pressure fractures cell-cell contacts to form the blastocoel lumen (Dumortier et al., 2019). Supracellular actin networks mechanically couple distant regions of the neural plate to enable closure (Galea et al., 2017). This review argues that the relationship between mechanical forces and chemical gradients in development is neither one of subordination nor redundancy, but rather a context-dependent hierarchy: in some developmental events, forces are the primary instructive signal; in others, chemical gradients lead while mechanical cues provide essential noise correction, robustness, and spatial refinement (Heisenberg & Bellaïche, 2013).

---

## 2. The Mechanotransduction Toolkit of the Developing Embryo

### 2.1 Piezo Channels: Mechanosensitive Ion Channels in Embryogenesis

The identification of Piezo1 and Piezo2 as essential components of mechanically activated cation channels marked a paradigm shift in understanding how cells sense physical forces (Coste et al., 2010). These large (~2,500 amino acid) transmembrane proteins form trimeric propeller-like structures that convert membrane tension into cation influx, with calcium as the primary signaling ion (Ge et al., 2015). In the developing embryo, Piezo channels are indispensable: constitutive Piezo1 deletion in mice causes embryonic lethality at midgestation (E9.5–E14.5) due to defective vascular remodeling, demonstrating that mechanosensation of blood flow is required for normal vascular development (Ranade et al., 2014). Endothelial Piezo1 senses shear stress from nascent blood flow and transduces it into signals that drive vascular network reorganization from a uniform plexus into a hierarchical tree (Li et al., 2014).

Beyond the vasculature, Piezo channels participate in diverse developmental processes. Loss-of-function mutations in human PIEZO1 cause congenital lymphatic dysplasia, while compound heterozygous PIEZO1 variants have been identified in Prune Belly Syndrome, a rare congenital disorder characterized by deficient abdominal wall musculature and urinary tract malformations (McCallie et al., 2024). Gain-of-function mutations in PIEZO2 cause distal arthrogryposis, and loss-of-function mutations cause a syndrome of muscular atrophy with perinatal respiratory distress (Chesler et al., 2016). Most recently, Piezo1 has been shown to regulate neural crest cell delamination: in the developing mouse embryo, increasing cell density and mechanical pressure in the neuroepithelium activates Piezo1 to trigger cell extrusion, expelling neural crest cells as round, pre-migratory cells that subsequently undergo epithelial-to-mesenchymal transition (EMT) and acquire migratory morphology (Ahammad et al., 2025). This finding redefines neural crest delamination as a mechanically triggered process rather than a purely transcriptionally programmed event.

### 2.2 YAP/TAZ: The Nuclear Mechanotransducers

YAP (Yes-associated protein) and TAZ (transcriptional coactivator with PDZ-binding motif, also known as WWTR1) are the primary nuclear relays of mechanical signals in mammalian cells (Dupont et al., 2011). When cells experience high mechanical tension — through growth on stiff substrates, in spread geometries, or under applied strain — YAP and TAZ translocate to the nucleus and activate TEAD family transcription factors to drive programs of proliferation, survival, and lineage specification (Panciera et al., 2017). Conversely, on soft substrates or in confined geometries, YAP/TAZ are sequestered in the cytoplasm and targeted for degradation.

The canonical Hippo pathway (MST1/2 → LATS1/2 → YAP/TAZ phosphorylation) represents one mode of YAP/TAZ regulation, but the mechanotransduction arm operates largely independently of Hippo kinases, instead requiring Rho GTPase activity and actomyosin cytoskeletal tension (Dupont et al., 2011). The precise mechanism of force transmission involves the LINC (Linker of Nucleoskeleton and Cytoskeleton) complex — Nesprin-SUN domain proteins spanning the nuclear envelope — which mechanically connects the cytoskeleton to the nuclear lamina and chromatin (Lombardi et al., 2011). Nuclear deformation alters chromatin accessibility and nuclear pore complex conformation, facilitating YAP import under tension (Elosegui-Artola et al., 2017).

In development, YAP/TAZ are essential for organ size control, functioning as the effector arm of the Hippo pathway that restricts tissue growth (Dong et al., 2007). Conditional YAP knockout results in developmental defects across multiple organ systems, while YAP overexpression drives tissue overgrowth. Critically, YAP/TAZ activity integrates mechanical information with morphogen signaling: substrate stiffness modulates cellular sensitivity to Wnt, BMP, and FGF ligands, with YAP/TAZ serving as the integration node where mechanical and chemical inputs converge to determine cell fate (Panciera et al., 2017).

### 2.3 Mechanical Memory and the LINC-Chromatin Axis

A remarkable feature of cellular mechanotransduction is mechanical memory — the ability of cells to retain information about past mechanical environments and use it to influence future behavior. When mesenchymal stem cells (MSCs) are cultured on stiff substrates and subsequently transferred to soft environments, they retain stiffness-induced gene expression programs and differentiation biases for days to weeks, a phenomenon mediated by persistent chromatin modifications (Yang et al., 2014). Specifically, culture on stiff substrates induces histone H3 lysine 27 trimethylation (H3K27me3) patterns at mechanosensitive loci that persist even after mechanical unloading, creating an epigenetic record of mechanical history (Na et al., 2024). This mechanical memory is transmitted through the LINC complex: Nesprin conformational changes alter nuclear shape and size, which in turn modulate lamina-associated domain organization and heterochromatin distribution (Kureel et al., 2025). In the developmental context, mechanical memory may explain how transiently applied forces during critical windows can have lasting effects on cell fate — a mechanism with implications for understanding how mechanical perturbations during embryogenesis lead to congenital defects.

The quantitative relationship between substrate stiffness and YAP nuclear localization can be modeled as a mechanosensitive gene activation function. Let $E$ denote the Young's modulus of the substrate (in kPa), and $[YAP_{\text{nuc}}]$ the nuclear concentration of YAP. The fraction of YAP in the nucleus follows a Hill-type response:

```math
f_{\text{YAP}}(E) = \frac{[YAP_{\text{nuc}}]}{[YAP_{\text{total}}]} = \frac{E^{n_m}}{K_m^{n_m} + E^{n_m}}
```

where $K_m$ is the half-maximal stiffness (experimentally ~5–10 kPa for MSCs), and $n_m$ is the Hill coefficient reflecting cooperative mechanotransduction (experimentally $n_m \approx 2$–$4$, indicating ultrasensitive switching) (Dupont et al., 2011; Elosegui-Artola et al., 2017). The downstream gene activation rate for a YAP/TEAD target gene $g$ is then:

```math
\frac{d[g]}{dt} = k_{\text{on}} \cdot f_{\text{YAP}}(E) \cdot [TEAD] - k_{\text{off}} \cdot [g]
```

where $k_{\text{on}}$ and $k_{\text{off}}$ are the transcriptional activation and mRNA degradation rates, respectively, and $[TEAD]$ is the available TEAD cofactor concentration. This framework captures the key biological insight that substrate stiffness is transduced through a sigmoidal, cooperative mechanism into transcriptional output, enabling cells to make sharp fate decisions across narrow stiffness ranges — a mechanical analog of the morphogen concentration thresholds in Wolpert's French Flag model (Wolpert, 2011).

---

## 3. Gastrulation: Where Mechanics Meets Morphogenesis

### 3.1 Tissue Fluidity and the Jamming Transition

Gastrulation — the process by which the single-layered blastula reorganizes into a multilayered embryo with distinct germ layers — is arguably the most mechanically dramatic event in development. The movements of convergence, extension, involution, and internalization require large-scale tissue remodeling, which in turn demands that tissues transition between solid-like and fluid-like states (Heisenberg & Bellaïche, 2013). The physics of this transition is captured by the concept of tissue jamming, borrowed from soft matter physics: in a jammed (solid-like) state, cells are locked in place by their neighbors and resist rearrangement; in an unjammed (fluid-like) state, cells exchange neighbors freely and the tissue flows (Bi et al., 2016).

The self-propelled Voronoi (SPV) model provides a quantitative framework for this transition. In this model, each cell $i$ has an energy:

```math
\varepsilon_i = K_A (A_i - A_0)^2 + K_P (P_i - P_0)^2
```

where $A_i$ and $P_i$ are the cell's area and perimeter, $A_0$ and $P_0$ are preferred values, and $K_A$, $K_P$ are area and perimeter elastic moduli, respectively. The critical parameter is the target shape index $p_0 = P_0 / \sqrt{A_0}$, which encodes the competition between cell-cell adhesion (favoring larger $P_0$, more elongated cells) and cortical contractility (favoring smaller $P_0$, more compact cells). A rigidity transition occurs at $p_0^* \approx 3.81$: when $p_0 < p_0^*$, the tissue is jammed and solid-like; when $p_0 > p_0^*$, the tissue is unjammed and fluid-like (Bi et al., 2016). This value corresponds remarkably to the perimeter-to-root-area ratio of a regular pentagon ($p_{\text{pentagon}} = 3.812$), suggesting a geometric origin for the transition.

In the developing zebrafish embryo, this jamming framework has direct relevance. A fluid-to-solid jamming transition underlies vertebrate body axis elongation: the posterior presomitic mesoderm (PSM) is fluid-like, allowing cell rearrangements and tissue flow, while the anterior PSM solidifies as cells differentiate into somites (Mongera et al., 2018). Using magnetically deformable ferrofluid droplets injected into live embryos, Mongera et al. (2023) directly measured tissue mechanics along the anteroposterior axis, showing that cells probe a supracellular foam-like architecture and experience spatially graded mechanical environments during differentiation. A 2025 study further revealed that dorsal tissues are most fluid at the posterior end, progressively rigidify anteriorly, and then partially refluidize, establishing a complex spatial map of tissue mechanical states that guides axis elongation (Tse et al., 2025).

### 3.2 Morphogen Gradients Trigger Mechanical Phase Transitions

A transformative insight of recent years is that morphogen gradients do not merely specify cell identities — they also encode mechanical transitions. In zebrafish gastrulation, a graded Nodal signal orchestrates the internalization of mesendoderm cells by triggering a motility-driven unjamming transition: high Nodal at the margin generates highly protrusive leader cells that autonomously internalize via local unjamming, while lower Nodal levels produce less protrusive followers that are mechanically pulled inward by the leaders (Pinheiro et al., 2022). This demonstrates that a single morphogen gradient simultaneously encodes both fate (mesoderm vs. ectoderm) and mechanical behavior (fluid vs. solid), coupling patterning and morphogenesis through a unified molecular-mechanical mechanism.

### 3.3 Cell Cycle Dynamics Control Tissue Fluidity

The proliferative state of cells is itself a mechanical parameter. In the developing mouse neural tube, interkinetic nuclear movement (IKNM) — the oscillatory migration of nuclei between the apical and basal surfaces of the neuroepithelium during the cell cycle — generates active stresses that drive cell rearrangements and maintain tissue fluidity (Bocanegra-Moreno et al., 2023). At early developmental stages (E8.5–E9.0), high proliferation rates generate sufficient active stress to keep the neuroepithelium in a fluid-like state despite high junctional tension. As development proceeds and proliferation declines, the tissue undergoes a glass-like transition to a more solid state around E9.5, effectively "freezing" cellular positions and stabilizing the emerging pattern. This finding reveals that cell cycle dynamics are not merely a growth mechanism but an active regulator of tissue mechanical state — a form of temporal control over spatial organization.

---

## 4. Neural Tube Closure: A Biomechanical Engineering Problem

### 4.1 Supracellular Force Networks

Neural tube closure (NTC) — the process by which the flat neural plate folds and fuses to form the hollow neural tube — is one of the most mechanically demanding morphogenetic events in vertebrate development. Failure of NTC causes neural tube defects (NTDs), which affect approximately 300,000 births annually worldwide and include conditions such as spina bifida and anencephaly (Copp et al., 2013). The mechanics of NTC involve coordinated force generation across multiple tissue scales.

Using a tissue-level strain-mapping workflow combined with laser ablation in live-imaged mouse embryos, Galea et al. (2017) demonstrated that neural fold elevation is driven by a biomechanically coupled system: laser ablation at the zippering point causes rapid, far-reaching separation of the neural folds, revealing that the entire neural plate is mechanically connected by a supracellular F-actin network. This network includes an actin cable running along the tips of the neural folds, analogous to a purse-string, and a broader meshwork extending ventrally into the neural plate. Pharmacological disruption of F-actin or targeted ablation of the cable causes neural fold separation, confirming that long-range mechanical coupling is essential for closure.

Brillouin microscopy — a non-contact optical technique that measures the local longitudinal modulus of tissue — has enabled in situ mapping of tissue stiffness during NTC. Bevilacqua et al. (2019) acquired two-dimensional mechanical maps of the mouse neural tube region at E8.5 and E9.5 with submicron spatial resolution, revealing that the neural plate exhibits spatially heterogeneous stiffness: the hinge points where bending occurs are softer than the surrounding neuroepithelium, suggesting that local softening facilitates folding while stiffer regions maintain structural integrity.

### 4.2 Neural Crest Delamination: A Piezo1-Mediated Mechanical Event

The neural crest — a transient embryonic cell population that gives rise to craniofacial skeleton, peripheral nervous system, melanocytes, and cardiac outflow tract — must delaminate from the neuroepithelium and migrate extensively through the embryo. Classical models attributed delamination to transcriptionally driven EMT, orchestrated by factors such as Snail, Slug, and FoxD3. However, Ahammad et al. (2025) discovered that cranial neural crest cells are physically extruded from the neuroepithelium through a Piezo1-dependent mechanism. Using time-lapse imaging of mouse embryos, the authors identified a population of round, isolated cells at the neural fold that exit prior to completing EMT. Cell extrusion is driven by increasing cell density and tissue pressure in the neuroepithelium, which activates Piezo1 to trigger calcium-dependent actomyosin contraction and basal expulsion. Piezo1 inhibition reduced the number of delaminated neural crest cells, while the Piezo1 agonist Yoda1 increased extrusion. This finding positions neural crest delamination as a mechanosensory event — tissue-level pressure is the trigger, Piezo1 is the sensor, and cell extrusion is the mechanism — with profound implications for understanding craniofacial development and neurocristopathies.

---

## 5. Cardiac Development: The Force-Sensing Heart

### 5.1 Shear Stress as an Instructive Cardiac Signal

The heart is the first organ to function in the embryo, and its own mechanical output — blood flow — feeds back to shape its subsequent development. From the onset of cardiac contraction, hemodynamic shear stress acts on endocardial cells lining the cardiac lumen, activating mechanosensitive signaling cascades that regulate chamber morphogenesis, valve formation, and trabeculation (Heckel et al., 2015). The mechanosensors on endocardial cells include Piezo1, TRPP2 (polycystin-2), and TRPV4, which collectively detect wall shear stress and transduce it into calcium signaling and downstream transcriptional responses (Heckel et al., 2015).

During cardiac valve morphogenesis in zebrafish, extracellular mechanical forces drive endocardial cell volume decrease: tissue convergence at the atrioventricular boundary generates compressive forces that, sensed through TRPP2 and TRPV4, trigger cell volume reduction via ion and water efflux — a process further regulated by hyaluronic acid in the cardiac jelly (Vignes et al., 2022). This mechanical volume control is essential for proper valve leaflet formation, demonstrating that cell size — a fundamental biophysical parameter — is under direct mechanical regulation during organogenesis.

### 5.2 Trabeculation: Mechanically Activated Transcription

Cardiac trabeculation — the formation of muscular ridges that project into the ventricular lumen, essential for contractile function and coronary vascularization — is initiated by cardiomyocyte delamination from the compact myocardium. A 2025 study by Chen et al. revealed that this process is mechanically triggered: using 4D strain analysis in zebrafish, they demonstrated that myocardial contractile force generates radially aligned strain fields that activate the transcription factor Snai1b in a subset of cardiomyocytes (Chen et al., 2025). CRISPR-mediated activation of snai1b increased the fraction of trabeculating cardiomyocytes to 51.6%, while CRISPR repression reduced it to 6.7% under β-adrenergic stimulation. The strain-activated Snai1b expression occurs independently of the canonical Notch-ErbB2 trabeculation pathway, revealing a parallel, mechanically driven axis for trabeculation initiation. This establishes cardiac trabeculation as a process where mechanical force is the primary instructive signal — cells sense myocardial strain and respond with a transcriptional program for delamination, a paradigm fundamentally different from morphogen-directed patterning.

The wall shear stress $\tau_w$ experienced by endocardial cells can be estimated from embryonic cardiac hemodynamics:

```math
\tau_w = \mu \left. \frac{\partial v}{\partial r} \right|_{r=R} \approx \frac{4 \mu Q}{\pi R^3}
```

where $\mu$ is blood viscosity (~0.003 Pa·s for embryonic blood), $Q$ is volumetric flow rate, and $R$ is the local vessel/chamber radius. For the zebrafish embryonic ventricle at 48 hours post-fertilization, $Q \approx 0.5$ nL/s and $R \approx 30$ μm, yielding $\tau_w \approx 0.07$ Pa — a value within the range known to activate endothelial Piezo1 and initiate downstream signaling cascades (Ranade et al., 2014; Lee et al., 2022). The conversion of this continuous mechanical signal into a binary transcriptional decision (Snai1b on/off) implies a thresholding mechanism, potentially mediated by the ultrasensitive Hill-type YAP/TAZ response described in Section 2.

---

## 6. Branching Morphogenesis: The Mechanics of Organ Architecture

### 6.1 Mechanical Constraints on Epithelial Branching

The ramified tubular architectures of the lung, kidney, mammary gland, and salivary gland are generated through branching morphogenesis — iterative rounds of epithelial bud growth, bifurcation, and elongation guided by reciprocal signaling between epithelial tips and surrounding mesenchyme (Affolter et al., 2009). While morphogen gradients (FGF10 in lung, GDNF in kidney) provide the chemotactic cues that orient branch growth, the mechanical properties of the surrounding tissue constrain and sculpt the branching pattern.

In the developing kidney, image-based modeling combined with experimental perturbation revealed that branching follows a Turing-type reaction-diffusion mechanism, with GDNF as the activator and WNT11 as the long-range feedback modulator, operating within the mechanical constraints set by tissue geometry (Menshykau et al., 2019). The mechanical environment imposes a "Goldilocks" constraint: hydrogel culture studies show that matrix stiffness of approximately 2 kPa is optimal for maintaining kidney shape and branching patterns, with stiffer matrices suppressing branching and softer matrices causing tissue disorganization (Prahl et al., 2023). A 2025 study demonstrated that culture boundary conditions — the physical shape and confinement of the culture environment — engineer kidney developmental trajectory, with geometric constraints directing branching angles and segment lengths independently of chemical signaling (Kim et al., 2025).

### 6.2 Hydraulic Fracturing and Lumen Formation

The formation of fluid-filled lumens — a defining feature of epithelial organs — is fundamentally a mechanical process driven by hydrostatic pressure. During mouse blastocyst formation, pressurized fluid accumulates at cell-cell contacts and fractures them into hundreds of micrometer-scale lumens, which then coarsen into a single blastocoel through a process analogous to Ostwald ripening in foams (Dumortier et al., 2019). The coarsening dynamics follow:

```math
\frac{dR_k}{dt} = \frac{\kappa}{\eta} \left( \frac{2\gamma}{R_k} - P_{\infty} \right)
```

where $R_k$ is the radius of microlumen $k$, $\gamma$ is the effective surface tension of the cell-cell contact, $\eta$ is the effective viscosity of the intercellular fluid, $\kappa$ is the hydraulic permeability, and $P_{\infty}$ is the far-field pressure set by the largest lumen. Lumens with $R_k < 2\gamma / P_{\infty}$ have higher Laplace pressure than the dominant lumen and therefore shrink, discharging their contents into larger neighbors — a positive feedback that drives single-lumen selection. The timescale of coarsening is $\tau \sim \eta R_0 / (\kappa \gamma)$, where $R_0$ is the characteristic microlumen size.

This hydraulic fracturing mechanism is augmented by active cellular pumping. Inverse membrane blebs — protrusions that extend into the intercellular space — operate as hydraulic pumps: they fill with fluid during growth phases and discharge it upon actomyosin-driven retraction, actively directing fluid flow toward the nascent lumen (Duclut et al., 2024). Manipulation of embryo topology reveals that without a dominant lumen sink, inverse blebs pump fluid into one another in futile cycles, demonstrating that the combination of passive Ostwald ripening and active hydraulic pumping is required for efficient lumen positioning.

---

## 7. Mechano-Morphogen Coupling: When Force Corrects Chemistry

### 7.1 Mechano-Gradients Correct Noisy Morphogen Patterns

Perhaps the most striking evidence for mechano-morphogen coupling comes from the zebrafish anteroposterior (AP) axis, where a Wnt/β-catenin gradient specifies brain regionalization. The Wnt gradient is inherently noisy — stochastic gene expression and variable ligand production create cells with aberrant Wnt activity that would, if uncorrected, generate patterning errors. Akieda et al. (2019) first showed that the embryo corrects this noise through cell competition: cells with aberrant Wnt signaling are identified and eliminated by their neighbors. The subsequent discovery of the underlying mechanism revealed a sophisticated mechano-chemical feedback loop: the Wnt/β-catenin gradient controls membrane cadherin levels, which in turn generate an intercellular tension gradient — a "mechano-gradient" — along the AP axis (Akieda et al., 2024).

Cells producing noisy Wnt signals locally deform the mechano-gradient, activating mechanosensitive calcium channels (likely Piezo-family) in neighboring "fit" cells. The calcium influx triggers secretion of annexin A1a, which induces apoptosis in the noisy cell (Akieda et al., 2024). This system operates as a mechanical quality control mechanism: the chemical gradient (Wnt) is converted into a mechanical gradient (cadherin-tension), which provides a second, independent readout of positional information. Cells whose chemical and mechanical signals are inconsistent are flagged and eliminated. The conversion of Wnt/β-catenin signaling activity into mechanical force via cadherin and actomyosin is essential for proper AP brain patterning, as disruption of the mechano-gradient — even with intact Wnt signaling — leads to patterning defects (Akieda et al., 2024).

### 7.2 Tissue Phase Transitions Shape Morphogen Gradient Range

Mechanical forces also control morphogen gradients by regulating tissue material properties. When a tissue undergoes a rigidity phase transition (from fluid to solid), it alters the effective diffusivity and stability of morphogen gradients. In a fluid tissue, morphogen molecules diffuse through a rearranging cellular landscape where cell-cell junctions are continuously remodeled, potentially disrupting gradient formation. As the tissue solidifies, intercellular spaces become more stable, restricting ligand dispersal and sharpening the gradient. This coupling between tissue phase state and morphogen range creates a feedback loop: morphogen gradients can trigger tissue solidification (through transcriptional effects on adhesion molecules), which in turn sharpens and stabilizes the very gradient that induced the transition (Pinheiro et al., 2022).

### 7.3 YAP/TAZ as the Integration Hub

The convergence of mechanical and chemical signals at YAP/TAZ creates an integration hub where tissue mechanics modulates morphogen pathway sensitivity. Substrate stiffness regulates the amplitude of Wnt, BMP, and FGF transcriptional responses through YAP/TAZ nuclear availability: on stiff substrates, nuclear YAP potentiates Wnt target gene expression, while on soft substrates, cytoplasmic YAP sequesters β-catenin and dampens Wnt output (Panciera et al., 2017). This means that identical morphogen concentrations can produce different transcriptional outcomes depending on tissue stiffness — effectively making the "French Flag" interpretation of morphogen gradients conditional on the mechanical context. In the developing embryo, where tissue stiffness varies spatially and temporally, this integration ensures that cell fate decisions reflect the full mechanical and chemical environment rather than chemical concentration alone.

The information-theoretic framework for this dual encoding reveals synergistic integration. Let $X$ denote position along a developmental axis. A cell reads two channels: chemical concentration $C$ (morphogen) and mechanical signal $F$ (force/stiffness). The mutual information between position and the joint signal is:

```math
I(X; C, F) = I(X; C) + I(X; F | C)
```

By the chain rule of mutual information, we can decompose the joint signal into unique, redundant, and synergistic components:

```math
I(X; C, F) = I_{\text{unique}}(X; C) + I_{\text{unique}}(X; F) + I_{\text{redundant}} + I_{\text{synergy}}
```

If $I_{\text{synergy}} > 0$, the combined mechano-chemical signal carries more positional information than the sum of its parts — meaning that some positional information is accessible only when both channels are read jointly (Tkačik et al., 2015). The mechano-gradient noise correction mechanism (Akieda et al., 2024) is precisely such a synergistic system: the mechanical channel cannot specify AP position alone (cadherin levels are too noisy), and the chemical channel is also noisy, but by requiring consistency between the two, cells achieve robust positional readout. This predicts that the precision of AP patterning exceeds what either gradient alone could theoretically achieve, consistent with the observed robustness of brain regionalization despite substantial morphogen noise (Tkačik et al., 2015).

---

## 8. Spatial Mechano-Transcriptomics: Seeing Force and Fate Together

### 8.1 A Computational Pipeline for Joint Analysis

The central challenge in developmental mechanobiology has been measuring mechanical forces and gene expression simultaneously in the same tissue. Spatial transcriptomics technologies (Visium, MERFISH, Slide-seq, Stereo-seq) provide spatially resolved gene expression maps but lack direct mechanical readout. Conversely, techniques such as Brillouin microscopy, traction force microscopy, and ferrofluid droplet deformation measure tissue mechanics but not gene expression. The development of a computational pipeline for spatial mechano-transcriptomics — published in Nature Methods in 2025 by Hallou et al. — bridges this gap by inferring mechanical forces from the geometric arrangement of cells in spatial transcriptomics data (Hallou et al., 2025).

The pipeline uses the segmented cell boundaries from spatial transcriptomics images to construct a vertex model representation of the tissue, then applies force inference algorithms to estimate the tension at each cell-cell junction and the pressure within each cell. These inferred mechanical parameters are then jointly analyzed with the spatially resolved transcriptome using geoadditive structural equation modeling, identifying gene modules that predict mechanical behavior and vice versa (Hallou et al., 2025).

Applied to the developing mouse embryo at E8.5, this approach revealed that tissue compartment boundaries — the interfaces between distinct developmental regions in the head — are characterized by elevated mechanical tension at cell-cell junctions compared to the surrounding tissue compartments. Furthermore, the pipeline identified specific gene expression signatures that are predictive of high-tension boundaries, suggesting that cells at tissue interfaces express distinct mechanical programs. This work demonstrates that mechanical forces and transcriptional states are not independent variables but are coupled through a quantifiable relationship that can be decoded from spatial transcriptomics data.

### 8.2 Force Inference: A Bayesian Framework

The inference of tissue-scale forces from cell geometry represents an inverse problem: given the observed cell shapes and arrangements, what distribution of tensions and pressures would produce the observed configuration? The Bayesian force inference framework formalizes this as:

```math
P(\boldsymbol{\sigma} | \mathbf{x}) = \frac{P(\mathbf{x} | \boldsymbol{\sigma}) \cdot P(\boldsymbol{\sigma})}{P(\mathbf{x})}
```

where $\boldsymbol{\sigma}$ is the vector of unknown tensions and pressures, $\mathbf{x}$ is the observed cell vertex positions, $P(\mathbf{x} | \boldsymbol{\sigma})$ is the likelihood under the vertex model energy (how likely the observed geometry is given the mechanical parameters), and $P(\boldsymbol{\sigma})$ is the prior encoding biological constraints (e.g., tensions must be positive, pressures bounded). The maximum a posteriori (MAP) estimate $\hat{\boldsymbol{\sigma}} = \arg\max P(\boldsymbol{\sigma} | \mathbf{x})$ gives the most probable force distribution consistent with the observed tissue geometry. When combined with gene expression data from spatial transcriptomics, this framework enables identification of mechanosensitive gene regulatory modules — genes whose expression correlates with inferred mechanical state — providing a mechanogenomic atlas of the developing embryo (Hallou et al., 2025).

---

## 9. Quantitative Frameworks for Developmental Mechanobiology

### 9.1 Vertex Model Energy Functional and the Jamming Phase Diagram

The vertex model provides a minimal physical description of epithelial tissue mechanics. Each cell $i$ in a two-dimensional epithelium is described by the energy functional:

```math
E = \sum_{i=1}^{N} \left[ K_A (A_i - A_0)^2 + K_P (P_i - P_0)^2 \right]
```

where $A_i$ and $P_i$ are the area and perimeter of cell $i$, $A_0$ and $P_0$ are the target area and perimeter, and $K_A$ and $K_P$ are the area and perimeter elastic moduli (Bi et al., 2016). The target shape index $p_0 = P_0 / \sqrt{A_0}$ is the single dimensionless parameter controlling the rigidity transition. The tissue undergoes a jamming transition at $p_0^* \approx 3.81$: for $p_0 < p_0^*$, energy barriers prevent cell rearrangements and the tissue is solid; for $p_0 > p_0^*$, energy barriers vanish and the tissue is fluid (Bi et al., 2016).

The biological interpretation is that $p_0$ encodes the balance between cell-cell adhesion (which increases preferred perimeter, raising $p_0$) and cortical contractility (which decreases preferred perimeter, lowering $p_0$). In the developing embryo, this balance is dynamically regulated: Wnt signaling increases cadherin expression (decreasing $p_0$, promoting solidification), while Rho-ROCK signaling increases contractility (also decreasing $p_0$). Conversely, EMT-inducing signals (Snail, Twist) downregulate cadherins and decrease contractility, increasing $p_0$ and fluidizing the tissue — consistent with the unjamming observed during gastrulation and neural crest migration.

### 9.2 Active Matter Continuum with Active Stress

At tissue scales, developing embryos can be described as active matter — systems that consume energy (ATP) to generate internal stresses, driving flows and deformations that are impossible in equilibrium materials (Marchetti et al., 2013). The continuum description couples mass conservation, force balance, and constitutive relations:

```math
\boldsymbol{\sigma} = \boldsymbol{\sigma}^{\text{elastic}} + \boldsymbol{\sigma}^{\text{viscous}} + \boldsymbol{\sigma}^{\text{active}}
```

The active stress tensor for a tissue with nematic order (characteristic of elongated cells with a preferred orientation) is:

```math
\sigma_{ij}^{\text{active}} = \zeta \Delta\mu \, Q_{ij}
```

where $\zeta$ is the activity coefficient (coupling ATP consumption to stress generation), $\Delta\mu$ is the chemical potential difference driving the non-equilibrium process, and $Q_{ij} = \langle n_i n_j - \frac{1}{2}\delta_{ij} \rangle$ is the nematic order parameter tensor describing cell alignment ($\mathbf{n}$ is the local cell elongation axis) (Marchetti et al., 2013). The sign of $\zeta$ determines whether the active stress is contractile ($\zeta > 0$, as in actomyosin-driven systems) or extensile ($\zeta < 0$, as in some microtubule-based systems).

In the developing neuroepithelium, the active contribution from interkinetic nuclear movement (IKNM) generates stresses that maintain tissue fluidity. The effective active stress scales with proliferation rate $\lambda$: $|\sigma^{\text{active}}| \propto \lambda \cdot \xi^2 \cdot k_{\text{cortex}}$, where $\xi$ is the IKNM amplitude and $k_{\text{cortex}}$ is the cortical stiffness (Bocanegra-Moreno et al., 2023). As proliferation declines during neural tube maturation, active stress decreases, and the tissue transitions from fluid to solid — a dynamically controlled phase transition that freezes the spatial pattern established during the fluid phase.

### 9.3 Mechanochemical Reaction-Diffusion

Classical Turing reaction-diffusion models treat the tissue as a passive medium through which morphogens diffuse. Mechanochemical extensions couple morphogen dynamics to tissue mechanics by introducing stress-dependent production or degradation terms. For a morphogen concentration $c(\mathbf{x}, t)$ in a tissue with stress field $\boldsymbol{\sigma}(\mathbf{x}, t)$:

```math
\frac{\partial c}{\partial t} = D \nabla^2 c + f(c) + \alpha \cdot \text{tr}(\boldsymbol{\sigma})
```

where $D$ is the effective diffusion coefficient, $f(c)$ captures reaction kinetics (production, degradation), and $\alpha \cdot \text{tr}(\boldsymbol{\sigma})$ is the mechanochemical coupling term: compressive stress ($\text{tr}(\boldsymbol{\sigma}) < 0$) can either enhance or suppress morphogen production depending on the sign of the coupling constant $\alpha$. The tissue stress is in turn influenced by morphogen-driven changes in cell mechanics:

```math
\nabla \cdot \boldsymbol{\sigma} + \mathbf{f}^{\text{active}}(c) = 0
```

where $\mathbf{f}^{\text{active}}(c)$ represents morphogen-dependent active force generation (e.g., Rho-mediated contractility downstream of Wnt signaling). This coupled system can generate patterns that are impossible in either mechanical or chemical models alone, including mechanically stabilized Turing patterns where tissue stiffness gradients set the wavelength of chemical patterns, and chemically driven tissue flows where morphogen-induced contractility generates advective transport (Howard et al., 2011; Tissue Active Matter Consortium, 2024).

### 9.4 Tissue Fluidity Order Parameter

The tissue fluidity $\phi$ can be defined as an order parameter for the solid-liquid transition using the rate of T1 topological transitions (neighbor exchanges):

```math
\phi = \frac{\langle N_{T1} \rangle}{\tau \cdot N_{\text{cells}}}
```

where $\langle N_{T1} \rangle$ is the mean number of T1 events in time interval $\tau$ and $N_{\text{cells}}$ is the number of cells. In the self-propelled Voronoi model, $\phi$ depends on two dimensionless parameters: the self-propelled speed $v_0$ (normalized by cell size and inverse persistence time) and the target shape index $p_0$. The phase diagram in the $(v_0, p_0)$ plane shows a solid phase at low $v_0$ and low $p_0$ (cells are neither motile nor adhesive enough to rearrange) and a fluid phase at high $v_0$ or high $p_0$ (Bi et al., 2016). In the developing embryo, the effective values of $v_0$ and $p_0$ are dynamically regulated: morphogens, growth factors, and cell cycle state modulate cell motility ($v_0$), while cadherins and cortical tension modulate cell shape preference ($p_0$). The trajectory of a tissue through this phase diagram during development — from the fluid mesenchyme of the early embryo to the jammed epithelium of the mature organ — represents a mechanical developmental program.

---

## 10. Translational Mechanobiology and Open Questions

### 10.1 Congenital Defects as Mechanical Failures

The mechanobiological perspective reframes a substantial fraction of congenital defects as mechanical failures rather than purely genetic or signaling errors. Neural tube defects — affecting ~300,000 births annually — can result from failures in the supracellular force networks required for neural fold elevation (Galea et al., 2017; Copp et al., 2013). Congenital heart defects — the most common class of birth defects at ~1% of live births — include anomalies in trabeculation, valve formation, and septation that are directly linked to aberrant hemodynamic forces during cardiac development (Vignes et al., 2022; Chen et al., 2025). Neurocristopathies including craniofacial malformations may involve defective Piezo1-mediated neural crest extrusion (Ahammad et al., 2025). Understanding the mechanical etiology of these conditions opens therapeutic avenues: correcting tissue mechanical properties — through targeted drug delivery to modify ECM stiffness, or modulation of Piezo/YAP activity — could prevent developmental defects even when the upstream genetic lesion is not directly treatable.

### 10.2 Mechanically-Informed Organoid Design

Current organoid differentiation protocols primarily optimize chemical conditions (growth factor cocktails, small molecules), with mechanical parameters addressed only implicitly through substrate choice. The mechanobiological insights reviewed here argue for explicit mechanical engineering of organoid environments: matching tissue-specific stiffness ranges (brain organoids on ~0.5 kPa, cardiac on ~10 kPa), providing appropriate fluid shear (cardiac, vascular organoids), and engineering Goldilocks stiffness for branching morphogenesis (~2 kPa for kidney) (Engler et al., 2006; Prahl et al., 2023). Spatial mechano-transcriptomics now enables benchmarking of organoid mechanical states against in vivo reference atlases, providing a quantitative readout of how well organoid mechanics recapitulate the native developmental environment (Hallou et al., 2025).

### 10.3 Open Questions

Several critical questions remain unresolved at the frontier of developmental mechanobiology:

**How many bits of positional information does mechanical signaling encode?** Information-theoretic analysis of morphogen gradients in *Drosophila* has shown that chemical gradients encode 1–2 bits of positional information per gene (Tkačik et al., 2015). Whether mechanical signals carry comparable information — and whether the mechano-chemical synergy significantly exceeds the sum of individual channel capacities — remains to be quantified in any developmental system.

**What determines the mechanical-chemical hierarchy in each tissue?** Our thesis posits a context-dependent hierarchy, but the rules governing which signal type leads in a given developmental event are unclear. In cardiac trabeculation and neural crest delamination, forces are primary; in AP axis patterning, morphogens lead. Is this determined by the relative kinetics of mechanical vs. chemical signal transduction, by the evolutionary history of the tissue, or by the spatial scale at which patterning operates?

**Can mechanical interventions prevent congenital defects?** If NTDs and CHDs are mechanical failures, can targeted modification of tissue mechanics — through Piezo agonists/antagonists, ECM-modifying enzymes, or direct mechanical manipulation — rescue defective closure or trabeculation in animal models? Early evidence from Piezo1 agonist (Yoda1) experiments in neural crest (Ahammad et al., 2025) suggests this may be feasible.

**How does mechanical memory intersect with developmental timing?** If cells retain epigenetic records of mechanical history (Na et al., 2024; Kureel et al., 2025), how does this memory interact with the temporal windows of developmental competence? Does mechanical memory explain why certain developmental perturbations have lasting effects while others are buffered?

**Is there a complete mechanochemical atlas of human embryogenesis?** The spatial mechano-transcriptomics pipeline (Hallou et al., 2025) provides the technology; the Human Developmental Cell Atlas (Haniffa et al., 2021) provides the organizational framework. Combining these would produce a four-dimensional map of gene expression, tissue mechanics, and morphogenetic flows throughout human development — a resource that would transform our understanding of both normal development and its failures.

---

## References

1. Affolter, M., Zeller, R., & Caussinus, E. (2009). Tissue remodelling through branching morphogenesis. *Nature Reviews Molecular Cell Biology*, 10(12), 831–842. PMID: 19888266

2. Ahammad, I., et al. (2025). Cell extrusion drives neural crest cell delamination. *Proceedings of the National Academy of Sciences*, 122(11), e2416566122. PMID: 40063802

3. Akieda, Y., et al. (2019). Cell competition corrects noisy Wnt morphogen gradients to achieve robust patterning in the zebrafish embryo. *Nature Communications*, 10(1), 4710. PMID: 31624259

4. Akieda, Y., et al. (2024). Mechano-gradients drive morphogen-noise correction to ensure robust patterning. *Science Advances*, 10(46), eadp2357. PMID: 39546611

5. Bevilacqua, C., et al. (2019). Tissue biomechanics during cranial neural tube closure measured by Brillouin microscopy and optical coherence tomography. *Cell Reports*, 26(11), 3000–3008.e4. PMID: 30865888

6. Bi, D., Yang, X., Marchetti, M. C., & Manning, M. L. (2016). Motility-driven glass and jamming transitions in biological tissues. *Physical Review X*, 6(2), 021011. PMID: 28966874

7. Bocanegra-Moreno, L., Singh, A., Hannezo, E., Zagorski, M., & Kicheva, A. (2023). Cell cycle dynamics control fluidity of the developing mouse neuroepithelium. *Nature Physics*, 19(7), 1050–1058. PMID: 37456593

8. Chen, Z., et al. (2025). Mechanically activated snai1b coordinates the initiation of myocardial delamination for trabeculation. *Nature Communications*, 16, 5932. PMID: 40993149

9. Chesler, A. T., et al. (2016). The role of PIEZO2 in human mechanosensation. *New England Journal of Medicine*, 375(14), 1355–1364. PMID: 27653382

10. Coen, E., Kennaway, R., & Whitewoods, C. (2017). On growth and form: A Cartesian coordinate system for biological morphogenesis. *Development*, 144(23), 4284–4297. PMID: 29183941

11. Copp, A. J., Stanier, P., & Greene, N. D. (2013). Neural tube defects: Recent advances, unsolved questions, and controversies. *The Lancet Neurology*, 12(8), 799–810. PMID: 23790957

12. Coste, B., et al. (2010). Piezo1 and Piezo2 are essential components of distinct mechanically activated cation channels. *Science*, 330(6000), 55–60. PMID: 20813920

13. Dong, J., et al. (2007). Elucidation of a universal size-control mechanism in Drosophila and mammals. *Cell*, 130(6), 1120–1133. PMID: 17889654

14. Duclut, C., et al. (2024). Inverse blebs operate as hydraulic pumps during mouse blastocyst formation. *Nature Cell Biology*, 26(10), 1669–1679. PMID: 39261717

15. Dumortier, J. G., et al. (2019). Hydraulic fracturing and active coarsening position the lumen of the mouse blastocyst. *Science*, 365(6452), 465–468. PMID: 31371608

16. Dupont, S., et al. (2011). Role of YAP/TAZ in mechanotransduction. *Nature*, 474(7350), 179–183. PMID: 21654799

17. Elosegui-Artola, A., et al. (2017). Force triggers YAP nuclear entry by regulating transport across nuclear pores. *Cell*, 171(6), 1397–1410.e14. PMID: 29107331

18. Engler, A. J., Sen, S., Sweeney, H. L., & Discher, D. E. (2006). Matrix elasticity directs stem cell lineage specification. *Cell*, 126(4), 677–689. PMID: 16923388

19. Galea, G. L., et al. (2017). Biomechanical coupling facilitates spinal neural tube closure in mouse embryos. *Proceedings of the National Academy of Sciences*, 114(26), E5177–E5186. PMID: 28607062

20. Ge, J., et al. (2015). Architecture of the mammalian mechanosensitive Piezo1 channel. *Nature*, 527(7576), 64–69. PMID: 26390154

21. Hallou, A., et al. (2025). A computational pipeline for spatial mechano-transcriptomics. *Nature Methods*, 22(4), 698–710. PMID: 40097810

22. Haniffa, M., et al. (2021). A roadmap for the Human Developmental Cell Atlas. *Nature*, 597(7875), 196–205. PMID: 34497388

23. Heckel, E., et al. (2015). Oscillatory flow modulates mechanosensitive klf2a expression through trpv4 and trpp2 during heart valve development. *Current Biology*, 25(10), 1354–1361. PMID: 25959971

24. Heisenberg, C.-P., & Bellaïche, Y. (2013). Forces in tissue morphogenesis and patterning. *Cell*, 153(5), 948–962. PMID: 23706734

25. Howard, J., Grill, S. W., & Bois, J. S. (2011). Turing's next steps: The mechanochemical basis of morphogenesis. *Nature Reviews Molecular Cell Biology*, 12(6), 392–398. PMID: 21602907

26. Kim, S., et al. (2025). Engineering kidney developmental trajectory using culture boundary conditions. *Nature Communications*, 16(1), 3958. PMID: 40295568

27. Kureel, S. K., et al. (2025). Cellular mechanical memory: A potential tool for mesenchymal stem cell-based therapy. *Stem Cell Research & Therapy*, 16, 159. PMID: 40176143

28. Lee, J., et al. (2022). Piezo1 is a mechanosensitive channel in cardiac fibroblasts. *Journal of Biological Chemistry*, 298(5), 101904. PMID: 35381243

29. Li, J., et al. (2014). Piezo1 integration of vascular architecture with physiological force. *Nature*, 515(7526), 279–282. PMID: 25119035

30. Lombardi, M. L., et al. (2011). The interaction between nesprins and SUN proteins at the nuclear envelope is critical for force transmission between the nucleus and cytoskeleton. *Journal of Biological Chemistry*, 286(30), 26743–26753. PMID: 21652697

31. Mammoto, T., & Ingber, D. E. (2010). Mechanical control of tissue and organ development. *Development*, 137(9), 1407–1420. PMID: 20388652

32. Marchetti, M. C., et al. (2013). Hydrodynamics of soft active matter. *Reviews of Modern Physics*, 85(3), 1143–1189.

33. Martin, A. C., Kaschube, M., & Wieschaus, E. F. (2009). Pulsed contractions of an actin-myosin network drive apical constriction. *Nature*, 457(7228), 495–499. PMID: 19029882

34. McCallie, K. R., et al. (2024). PIEZO1 loss-of-function compound heterozygous mutations in the rare congenital human disorder Prune Belly Syndrome. *Nature Communications*, 15(1), 339. PMID: 38168043

35. Menshykau, D., et al. (2019). Image-based modeling of kidney branching morphogenesis reveals GDNF-RET based Turing-type mechanism and pattern-modulating WNT11 feedback. *Nature Communications*, 10(1), 239. PMID: 30651551

36. Mongera, A., et al. (2018). A fluid-to-solid jamming transition underlies vertebrate body axis elongation. *Nature*, 561(7723), 401–405. PMID: 30185907

37. Mongera, A., et al. (2023). Mechanics of the cellular microenvironment as probed by cells in vivo during zebrafish presomitic mesoderm differentiation. *Nature Materials*, 22(1), 135–143. PMID: 36577855

38. Na, J., et al. (2024). Mechanical memory based on chromatin and metabolism remodeling promotes proliferation and smooth muscle differentiation in mesenchymal stem cells. *The FASEB Journal*, 38(5), e23526. PMID: 38482729

39. Panciera, T., Azzolin, L., Cordenonsi, M., & Piccolo, S. (2017). Mechanobiology of YAP and TAZ in physiology and disease. *Nature Reviews Molecular Cell Biology*, 18(12), 758–770. PMID: 28951564

40. Pinheiro, D., et al. (2022). Morphogen gradient orchestrates pattern-preserving tissue morphogenesis via motility-driven unjamming. *Nature Physics*, 18(11), 1482–1493. PMID: 36415767

41. Prahl, L. S., et al. (2023). Jamming of nephron-forming niches in the developing mouse kidney creates cyclical mechanical stresses. *Nature Materials*, 22, 1024–1033.

42. Ranade, S. S., et al. (2014). Piezo1, a mechanically activated ion channel, is required for vascular development in mice. *Proceedings of the National Academy of Sciences*, 111(28), 10347–10352. PMID: 24958852

43. Tissue Active Matter Consortium. (2024). Tissue active matter: Integrating mechanics and signaling into dynamical models. *Cold Spring Harbor Perspectives in Biology*, 17(4), a041653. PMID: 38951023

44. Tkačik, G., et al. (2015). Positional information, positional error, and readout precision in morphogenesis: A mathematical framework. *Genetics*, 199(1), 39–59. PMID: 25361898

45. Tse, Y. C., et al. (2025). The physical roles of different posterior tissues in zebrafish axis elongation. *Nature Communications*, 16(1), 1831.

46. Vignes, H., et al. (2022). Extracellular mechanical forces drive endocardial cell volume decrease during zebrafish cardiac valve morphogenesis. *Developmental Cell*, 57(5), 598–609.e5. PMID: 35245444

47. Wolpert, L. (2011). Positional information and patterning revisited. *Journal of Theoretical Biology*, 269(1), 359–365. PMID: 21044633

48. Yang, C., Tibbitt, M. W., Basta, L., & Bhatt, D. L. (2014). Mechanical memory and dosing influence stem cell fate. *Nature Materials*, 13(6), 645–652. PMID: 24747782

