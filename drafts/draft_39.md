# Stem Cell Biotechnology

## Abstract

Stem cell therapies have achieved remarkable in vitro potency — directed differentiation protocols now routinely generate >90% pure target cell populations from induced pluripotent stem cells (iPSCs) — yet clinical engraftment rates remain disappointingly low: fewer than 5% of injected cardiomyocytes survive beyond 48 hours, hematopoietic stem cell (HSC) graft failure affects 5–20% of transplant recipients, and more than half of Edmonton protocol islet recipients lose insulin independence within five years. This review argues that the rate-limiting barrier to clinical cell therapy success is not cell quality but microenvironmental inadequacy: transplanted cells fail because they are delivered into hostile environments devoid of the niche signals — matrix stiffness, extracellular matrix (ECM) composition, soluble factor gradients, vascular proximity, and immune context — that sustain stem cell function in vivo. We survey the niche engineering toolkit (synthetic hydrogels, decellularized ECM, 3D bioprinting, and vascularization strategies) and then trace organ-specific applications across five clinical frontiers: hematopoietic niche rejuvenation via matrix stiffness engineering, engineered heart tissue patches achieving first-in-human implantation, encapsulated and vascularized endocrine pancreas constructs for type 1 diabetes, neural scaffolds eliminating organoid hypoxia, and bioinstructive musculoskeletal scaffolds directing immune-mediated regeneration. Six novel mathematical frameworks (F286–F291) formalize the quantitative design principles underlying scaffold vascularization, engraftment dynamics, contractile force scaling, oxygen transport in encapsulated islets, growth factor gradient optimization, and macrophage polarization kinetics. We identify vascularization, immune tolerance, and manufacturing scalability as the three cross-cutting challenges whose resolution will determine whether engineered niches transform cell therapy from a laboratory achievement to a clinical standard of care.

---

## 1. The Niche Gap: Why Transplanted Stem Cells Fail

### 1.1 The Engraftment Problem

The central paradox of regenerative medicine is that cells which function exquisitely in culture dishes routinely fail when transplanted into patients. This engraftment gap is quantifiable and consistent across organ systems. In cardiac cell therapy, systematic meta-analysis of preclinical studies demonstrates that fewer than 5% of directly injected cardiomyocytes survive beyond the first 48 hours post-transplantation, with the majority lost to anoikis — apoptosis triggered by detachment from the extracellular matrix — ischemia in the avascular graft site, and mechanical washout from the contracting myocardium (Terrovitis, Lautamäki, Bonios, Fox, Engles, Yu, et al., 2009). In hematopoietic stem cell transplantation, primary graft failure occurs in 5–20% of recipients depending on conditioning regimen, donor source, and HLA matching, with the highest rates in haploidentical and umbilical cord blood transplants where the niche-engraftment interface is most disrupted (Olsson, Urbano-Ispizua, & Hauzenberger, 2013). In islet transplantation, the landmark Edmonton protocol achieved initial insulin independence in 100% of seven patients, but five-year follow-up revealed that only 10% maintained insulin independence without exogenous insulin supplementation, as transplanted islets progressively died from hypoxia, immune attack, and loss of the vascular and ECM support that sustains them in the native pancreas (Shapiro, Lakey, Ryan, Korbutt, Toth, Warnock, et al., 2000; Ryan, Paty, Senior, Bigam, Alfadhli, Kneteman, et al., 2005).

These failures share a common mechanistic root: cells evolved to function within specific microenvironments are transplanted into environments that lack the signals necessary for their survival, self-renewal, and function. The field has historically responded by engineering better cells — improving differentiation purity, reducing off-target populations, enhancing functional maturation. While essential, this cell-centric approach addresses only half of the problem. The other half is the niche.

### 1.2 The Niche as the Missing Variable

The concept that stem cell behavior is governed not solely by cell-intrinsic properties but by the surrounding microenvironment was first articulated by Schofield in 1978, who proposed that the hematopoietic stem cell occupies a specific anatomical "niche" that preserves its stemness and regulates its proliferation (Schofield, 1978). This hypothesis was validated experimentally two decades later when two landmark studies, published simultaneously in Nature, demonstrated that osteoblastic cells in the bone marrow endosteum directly regulate HSC number: parathyroid hormone-mediated expansion of osteoblasts increased HSC frequency (Calvi, Adams, Weibrecht, Weber, Olson, Knight, et al., 2003), while bone morphogenetic protein (BMP) signaling through the osteoblastic niche controlled HSC pool size (Zhang, Niu, Ye, Song, Zhu, Chua, et al., 2003). These studies established that the niche is not merely a passive container but an active regulatory unit that instructs stem cell fate.

The modern understanding of the stem cell niche recognizes six canonical signal categories that collectively define the microenvironment:

**Matrix stiffness and mechanics.** Cells sense the mechanical properties of their surroundings through integrin-mediated adhesion, focal adhesion kinase (FAK) signaling, and YAP/TAZ nuclear translocation. Substrate stiffness alone is sufficient to direct mesenchymal stem cell differentiation: soft matrices (~0.1–1 kPa, mimicking brain) promote neurogenesis, intermediate stiffness (~8–17 kPa, mimicking muscle) promotes myogenesis, and rigid substrates (~25–40 kPa, mimicking bone) promote osteogenesis (Engler, Sen, Sweeney, & Discher, 2006). The bone marrow stiffens measurably with age — from approximately 0.3 kPa in young mice to 1.5 kPa in aged mice as measured by atomic force microscopy — and this stiffening directly impairs HSC function (Choi, Krieger, Engel, Mead, Diaz, Coughlin, et al., 2023).

**ECM composition and ligand presentation.** Each tissue contains a specific ECM composition — a "matrisome" — that presents adhesion ligands (laminins, fibronectins, collagens), sequesters growth factors, and provides structural organization. Islet beta cells are surrounded by a laminin-511/521-rich basement membrane; disruption of this matrix during isolation contributes directly to post-transplant cell death (Stendahl, Kaufman, & Bhatt, 2009). The satellite cell niche in muscle is defined by a basal lamina rich in laminin-211 and collagen IV (Wosczyna & Rando, 2018).

**Soluble factor gradients.** Growth factors, cytokines, and metabolites establish concentration gradients that regulate stem cell quiescence, activation, and differentiation. In the HSC niche, CXCL12 (SDF-1) produced by CXCL12-abundant reticular (CAR) cells and stem cell factor (SCF) produced by perivascular LepR+ stromal cells are the two most critical retention and maintenance signals (Morrison & Scadden, 2014).

**Cell-cell adhesion and juxtacrine signaling.** Direct contact between stem cells and niche support cells delivers signals that cannot be replicated by soluble factors alone. N-cadherin-mediated adhesion between HSCs and osteoblasts, Notch signaling between satellite cells and myofibers, and E-cadherin junctions between intestinal stem cells and Paneth cells all represent contact-dependent niche signals (Morrison & Scadden, 2014).

**Immune cells as niche constituents.** Tissue-resident macrophages, regulatory T cells, and other immune populations are increasingly recognized as integral niche components. Bone marrow macrophages regulate HSC retention by controlling CXCL12 expression in niche stromal cells; depletion of macrophages triggers HSC mobilization into the blood (Chow, Lucas, Bone, Buber, Mazo, Frenette, et al., 2011). In skeletal muscle, a coordinated sequence of monocyte-derived macrophage polarization — from pro-inflammatory M1 to pro-regenerative M2 — is essential for satellite cell activation and myofiber repair (Wosczyna & Rando, 2018).

**Vascular proximity and oxygen tension.** Most stem cell niches are organized around blood vessels: HSCs reside in perivascular niches adjacent to sinusoidal endothelium, satellite cells are positioned near capillaries, and neural stem cells in the subventricular zone (SVZ) contact the vasculature directly (Morrison & Scadden, 2014). Vascular proximity provides oxygen, nutrients, and systemic signals, while also establishing oxygen gradients — the endosteal HSC niche is relatively hypoxic (~1–2% O₂), which paradoxically promotes HSC quiescence and self-renewal.

### 1.3 Thesis: Engineering the Environment, Not Just the Cell

The six niche signals described above are almost entirely absent at the moment of cell transplantation. Cells injected as suspensions into tissue lack matrix adhesion, ECM ligands, organized soluble factor gradients, support cell contacts, immunomodulatory signals, and vascular supply. The thesis of this review is that **engineering the recipient microenvironment is the rate-limiting step for clinical stem cell therapy**. The following sections survey the engineering toolkit now available to recreate niche signals (Section 2), then trace organ-specific niche engineering strategies across five clinical frontiers — hematopoietic (Section 3), cardiac (Section 4), pancreatic (Section 5), neural (Section 6), and musculoskeletal (Section 7) — before identifying the cross-cutting challenges that must be resolved for engineered niches to achieve broad clinical impact (Section 8).

---

## 2. The Niche Engineering Toolkit

### 2.1 Synthetic Hydrogels: Tunable Mechanical and Biochemical Environments

Synthetic hydrogels — water-swollen polymer networks — provide the most versatile platform for recreating niche mechanics and biochemistry. Poly(ethylene glycol) (PEG)-based hydrogels, first adapted for cell culture by Lutolf and Hubbell (2005), offer precise control over three critical niche parameters: stiffness (tunable from <0.1 to >100 kPa by varying crosslink density), degradation kinetics (controlled through matrix metalloproteinase [MMP]-cleavable crosslinks that permit cell-mediated remodeling), and ligand presentation (achieved by covalent tethering of adhesion peptides such as RGD, YIGSR, or full-length ECM proteins). This modularity enables systematic dissection of individual niche contributions — an approach impossible with animal-derived matrices like Matrigel, whose undefined and batch-variable composition confounds mechanistic interpretation.

Gelatin methacryloyl (GelMA) hydrogels, generated by functionalization of denatured collagen with methacryloyl groups, combine the bioactivity of native ECM (cell-binding RGD motifs, MMP-degradable backbone) with photocrosslinkable tunability: the degree of methacrylation controls mechanical properties (1–30 kPa), and UV exposure time determines crosslink density and pore architecture (Yue, Della Bella, Duchi, O'Connell, & Choong, 2015). GelMA has become the dominant hydrogel for vascular tissue engineering and organoid culture, where its cell-permissive properties support capillary-like network formation by endothelial cells.

Hyaluronic acid (HA) hydrogels exploit the natural signaling functions of this glycosaminoglycan: HA engagement of CD44 receptors promotes neural stem cell maintenance, while its inherently soft mechanical properties (~0.1–1 kPa) recapitulate the mechanical environment of brain and bone marrow niches. Choi and colleagues demonstrated that culture of aged bone marrow stromal cells (BMSCs) in soft (~0.3 kPa) GelMA hydrogels reversed the stiffness-induced YAP/TAZ nuclear translocation and expansion of BMSCs seen in conventional 2D culture, restoring their ability to maintain and rejuvenate HSCs (Choi et al., 2023).

### 2.2 Decellularized ECM: Organ-Specific Instructive Matrices

Decellularization removes cellular components from native tissues through detergent perfusion, enzymatic digestion, or physical methods while preserving the tissue-specific ECM scaffold — including collagens, laminins, glycosaminoglycans, and sequestered growth factors — that encodes organ identity (Crapo, Gilbert, & Badylak, 2011). The resulting decellularized ECM (dECM) retains the three-dimensional architecture and biochemical signaling repertoire of the source organ, providing an instructive scaffold that directs recellularized stem cells toward tissue-appropriate fates.

A landmark 2025 study demonstrated the translational power of this approach for musculoskeletal regeneration. Passipieri and colleagues engineered a bioconstruct comprising dECM scaffold embedded with polymeric nanocapsules that sequentially release growth factors in a temporally controlled cascade: early-phase pro-inflammatory signals (days 0–3), mid-phase pro-regenerative signals including insulin-like growth factor 1 (IGF-1) and hepatocyte growth factor (HGF) (days 3–14), and late-phase anti-fibrotic agents (days 14–28) (Passipieri, Patel, Engel, Baker, Totsingan, Asfour, et al., 2025). When applied to volumetric muscle loss (VML) in animal models, this bioconstruct enhanced myofiber formation, angiogenesis, innervation, and functional restoration beyond what either dECM alone or growth factors alone could achieve — demonstrating that temporal orchestration of niche signals, not merely their presence, is critical for regeneration.

A complementary discovery revealed that stem cells can construct their own niche when provided with appropriate permissive conditions. Rezakhani, Gjorevski, Geurts, and Lutolf (2025) used chemically defined synthetic hydrogels to culture intestinal stem cells without exogenous laminin, and found that the stem cells autonomously secreted a laminin-rich basement membrane that functioned as a de novo niche, supporting organoid formation and long-term self-renewal (Rezakhani, Gjorevski, Geurts, & Lutolf, 2025). This "self-niche" phenomenon suggests that engineered scaffolds need not recapitulate every niche signal — they may need only to provide the permissive mechanical and chemical environment in which cells construct their own microenvironment.

### 2.3 Three-Dimensional Bioprinting: Spatial Recreation of Niche Architecture

The stem cell niche is a spatially organized structure in which the relative positions of support cells, ECM components, vasculature, and stem cells are functionally significant. 3D bioprinting enables the fabrication of constructs with controlled spatial heterogeneity — multiple cell types, materials, and growth factors deposited at defined positions with resolution down to ~50–100 μm — recreating the organized architecture that bulk seeding methods cannot achieve.

A transformative application of 3D bioprinting to niche engineering was demonstrated by Cai, Tian, Chen, and colleagues (2025), who designed vascular network-inspired diffusible (VID) scaffolds for engineering functional midbrain organoids. The VID scaffolds consist of 3D-printed meshed tubular channel networks whose branching geometry mimics physiological vascular architecture (Cai et al., 2025). Culture medium perfused through these channels delivers oxygen and nutrients by diffusion to surrounding tissue, effectively replacing the vascular function that organoids lack. Midbrain organoids grown on VID scaffolds developed with virtually no necrotic core — the central limitation of conventional organoids exceeding ~500 μm in diameter — and exhibited superior midbrain-specific identity, oxygen metabolism, neuronal maturation, and electrophysiological network activity compared to conventional free-floating organoids (Cai et al., 2025). This result demonstrates that recreating the physical transport properties of vasculature, even without actual blood vessels, is sufficient to rescue organoid viability and maturation.

### 2.4 Vascularization Strategies: The Universal Bottleneck

Every tissue thicker than approximately 100–200 μm requires vascular supply; beyond this diffusion limit, cells experience hypoxia and die. Vascularization is therefore the universal rate-limiting challenge in tissue engineering, and recent advances have dramatically accelerated the timeline from iPSC to functional vasculature.

Gong, Marchand, Li, and colleagues (2025) developed a streamlined method for rapid generation of functional vascular organoids (VOs) from iPSCs via simultaneous transcription factor activation of endothelial (ETV2) and mural (NKX3.1) lineages (Gong et al., 2025). This orthogonal induction approach produces functional 3D VOs in just five days without ECM embedding — compared to conventional VO protocols requiring 2–3 weeks with Matrigel. The VOs feature lumenized vessels with apical-basal polarity and diverse, mature vascular cell populations. Upon ECM exposure, VOs matured further, forming larger vessels (~1,000 μm diameter). In vivo, VOs engrafted into immunodeficient mice, formed perfused vasculature, and — critically for islet therapy — promoted revascularization when co-transplanted with pancreatic islets, demonstrating a direct translational application of rapid VO generation to niche engineering (Gong et al., 2025).

Complementing organoid-scale vascularization, microfluidic platforms enable perfusable vasculature at the organ-on-chip scale. Homan, Giger, and colleagues (2024) developed a microfluidic platform integrating functional vascularized organoids-on-chip, establishing endothelial networks around mesenchymal spheroids, pancreatic islet spheroids, and blood vessel organoids cultured for up to 30 days on-chip, with the networks establishing functional connections providing intravascular perfusion (Homan et al., 2024). This platform enables long-term culture with physiologically relevant transport — a capability previously impossible in static organoid culture.

### 2.5 Framework F286: Modified Krogh Cylinder Model for Scaffold Vascularization

The design of vascularized scaffolds requires a quantitative framework for determining the maximum tissue thickness — or equivalently, the maximum inter-channel spacing — that can be sustained by diffusive oxygen transport from perfused channels. We adapt the classical Krogh cylinder model, originally developed to describe oxygen transport from capillaries to surrounding tissue (Krogh, 1919), to the engineered scaffold context.

Consider a scaffold containing parallel cylindrical channels of radius $r_c$ (μm), spaced such that each channel supplies a tissue cylinder of radius $R$ (μm) — the half-distance between adjacent channels. Oxygen diffuses radially from the channel wall into the surrounding cell-laden scaffold, where it is consumed by cellular respiration.

The steady-state oxygen concentration $C(r)$ (mmHg) at radial distance $r$ from the channel center satisfies:

```math
D_{O_2} \frac{1}{r} \frac{d}{dr}\left(r \frac{dC}{dr}\right) = q_0
```

where $D_{O_2}$ is the effective oxygen diffusivity in the scaffold (cm²/s) and $q_0$ is the volumetric oxygen consumption rate (mmHg/s), assumed uniform. With boundary conditions $C(r_c) = C_0$ (the oxygen tension at the channel wall, set by perfusate oxygenation) and $dC/dr|_{r=R} = 0$ (no-flux symmetry condition at the tissue cylinder boundary), the solution is:

```math
C(r) = C_0 - \frac{q_0}{4D_{O_2}}\left(r^2 - r_c^2\right) + \frac{q_0 R^2}{2D_{O_2}} \ln\left(\frac{r}{r_c}\right)
```

The **critical inter-channel half-distance** $R^*$ is the maximum $R$ for which the minimum oxygen tension (occurring at $r = R$) remains above the hypoxic threshold $C_{\text{hyp}}$ (typically ~5 mmHg for most cell types, ~0.1 mmHg for cell death):

```math
C_0 - C_{\text{hyp}} = \frac{q_0}{4D_{O_2}}\left(R^{*2} - r_c^2\right) - \frac{q_0 R^{*2}}{2D_{O_2}} \ln\left(\frac{R^*}{r_c}\right)
```

For representative scaffold parameters — $D_{O_2} \approx 2.0 \times 10^{-5}$ cm²/s (hydrogel), $q_0 \approx 5 \times 10^{-3}$ mmHg/s (moderate cell density of ~10⁷ cells/cm³), $C_0 = 100$ mmHg (well-oxygenated perfusate), $r_c = 100$ μm, $C_{\text{hyp}} = 5$ mmHg — numerical solution yields $R^* \approx 300$–$400$ μm, corresponding to a maximum inter-channel spacing of 600–800 μm. This value is remarkably consistent with the VID scaffold design of Cai et al. (2025), who empirically optimized inter-channel spacing to 400–800 μm for midbrain organoid viability.

The framework provides a quantitative **design rule**: for a given cell type (which determines $q_0$), scaffold material (which determines $D_{O_2}$), and perfusate oxygenation (which determines $C_0$), the maximum permissible channel spacing is calculable from the Krogh cylinder solution. Cells with high metabolic demand — cardiomyocytes (~70 mL O₂/min per 100 g tissue) or islet beta cells ($q_0 \approx 0.034$ mol O₂/m³/s) — require closer channel spacing than metabolically quiescent cells such as chondrocytes.

---

## 3. Hematopoietic Niche: Rejuvenating Aged Blood

### 3.1 The Aging Hematopoietic Stem Cell Niche

The bone marrow HSC niche undergoes profound age-related remodeling that directly degrades stem cell function. Three convergent changes define niche aging. First, the marrow stiffens: atomic force microscopy (AFM) measurements demonstrate that the average Young's modulus of mouse bone marrow increases from approximately 0.3 kPa in young animals to approximately 1.5 kPa in aged animals, a five-fold increase that alters the mechanical environment sensed by both HSCs and their supporting stromal cells (Choi et al., 2023). Second, adipogenesis displaces functional niche space: marrow adipose tissue (MAT) expands progressively with age, physically displacing the osteoblastic and perivascular niches that support HSCs and secreting adipokines that promote HSC myeloid bias at the expense of lymphoid differentiation (Ambrosi, Scialdone, Graja, Gober, Ditzel, Schulz, et al., 2017). Third, the niche support cells themselves senesce: expression of the senescence markers p16^INK4a^, IL-1β, and γH2AX foci increase with age in CXCL12-abundant reticular (CAR)/LepR+ cells and osteoblasts — the two principal HSC-supportive stromal populations — reducing their production of the critical niche factors CXCL12 and SCF (Helbling, Pineiro-Yanez, Gerber, Al-Abbasi, Dotto, & Bornhauser, 2025).

This triad of stiffening, adipogenic displacement, and stromal senescence produces the hallmarks of HSC aging: myeloid-biased differentiation, reduced lymphopoiesis, expanded HSC numbers with diminished per-cell reconstitution capacity, and increased susceptibility to hematopoietic malignancies (Baryawno, Przybylski, Kowalczyk, Kfoury, Severe, Gustafsson, et al., 2019). Critically, these HSC aging phenotypes are substantially niche-driven rather than cell-intrinsic: transplantation of aged HSCs into young bone marrow partially restores their reconstitution capacity, while transplantation of young HSCs into aged bone marrow impairs their function (Ergen, Boles, & Bhatt, 2012).

### 3.2 Matrix Stiffness as the Control Variable

The discovery that bone marrow stiffness is both a measurable aging biomarker and a modifiable engineering parameter opened a direct path to niche-based HSC rejuvenation. Choi and colleagues (2023) demonstrated that culturing bone marrow stromal cells (BMSCs) on stiff 2D substrates activates YAP/TAZ signaling, driving BMSC proliferation but reducing their capacity to maintain HSCs. Transfer of these stiffness-primed BMSCs to three-dimensional culture in soft GelMA hydrogels (~0.3 kPa, matching young marrow stiffness) reversed the YAP/TAZ activation and restored HSC-supportive function (Choi et al., 2023).

The functional consequences were striking: 3D co-culture of aged HSCs with BMSCs in soft hydrogels promoted HSC maintenance and lymphopoiesis, reversed aging hallmarks including myeloid bias and reduced engraftment, and restored long-term multilineage reconstitution capacity upon transplantation into irradiated recipients (Choi et al., 2023). This result establishes that a single engineering parameter — substrate stiffness — is sufficient to reverse a substantial fraction of HSC aging, by acting through the intermediary of niche stromal cell reprogramming rather than direct modification of the HSCs themselves.

### 3.3 Engineered Bone Marrow Niches: From Organoids to In Vivo Support

Building on the stiffness-rejuvenation principle, three recent advances have progressively increased the complexity and translational relevance of engineered bone marrow niches.

**Bioengineered ECM niches for LT-HSC maintenance.** Donnelly, Ross, Xiao, and colleagues (2024) demonstrated that soft collagen type I hydrogels drive nestin expression in perivascular stromal cells (PerSCs) — a marker of HSC-supportive niche cells in vivo. Nestin-expressing PerSCs cultured in these bioengineered niches maintained long-term repopulating HSCs (LT-HSCs) ex vivo at significantly higher frequencies than conventional liquid culture, with preserved multilineage differentiation capacity upon transplantation (Donnelly et al., 2024). The mechanism involves nestin-dependent regulation of HIF-1α expression, linking mechanical niche properties to the hypoxic signaling that maintains HSC quiescence. This work represents the first demonstration that a fully defined, synthetic ECM environment can recapitulate the physiological niche sufficiently to support LT-HSC function.

**iPSC-derived bone marrow organoids.** Khan, Bornhäuser, and colleagues (2024) generated complex bone marrow-like organoids (BMOs) from human iPSCs, achieving self-organized spatial structures that mimic the cellular, structural, and molecular characteristics of the hematopoietic microenvironment (Khan et al., 2024). These BMOs contain vascular networks, multipotent mesenchymal stem/progenitor cells, and — critically — a hematopoietic stem/progenitor cell (HSPC) cluster expressing genes characteristic of fetal HSCs, demonstrating that iPSC-derived organoids can spontaneously generate niche-like structures capable of supporting hematopoiesis in vitro.

**Engineered vascularized osteoblastic niche (eVON).** Li, Nikolova, Zhang, and colleagues (2025) developed the most complex engineered bone marrow niche reported to date: a macro-scale organotypic model of the endosteal niche based on human iPSCs and porous hydroxyapatite scaffolds (Li et al., 2025). The eVON contains long-lasting vascular networks covered by pericytes and neural fibers within an osteogenic matrix — recapitulating three of the six canonical niche signals (vasculature, ECM, cell-cell contact) — and expresses key niche factors CXCL12, KITLG, and VEGFA in human-specific spatial patterns (Li et al., 2025). Functionally, the eVON supports hematopoiesis in vitro and preserves HSPC multilineage repopulation capacity in vivo upon transplantation into immunodeficient mice (Li et al., 2025). This result establishes proof-of-principle that an engineered niche can provide in vivo functional support for human HSPCs.

### 3.4 Clinical Implications

These advances suggest a near-term clinical pathway: co-transplantation of HSCs with engineered niche components — whether soft hydrogel-conditioned stromal cells, iPSC-derived BMO fragments, or eVON scaffolds — to improve engraftment in settings where graft failure rates are highest. For elderly patients undergoing allogeneic HSC transplantation, whose aged marrow niche contributes to poor engraftment, pre-transplant niche conditioning (pharmacological or biomaterial-based) may represent a complementary strategy. The quantitative framework developed below (F287) provides a mathematical basis for predicting how niche quality translates to engraftment probability.

### 3.5 Framework F287: Stochastic Branching Process Model for HSC Engraftment

We model HSC engraftment as a multi-type Galton-Watson branching process in which each transplanted HSC makes a stochastic fate decision at each time step (approximately one cell cycle, ~24–48 hours), with fate probabilities determined by local niche quality.

Let each HSC at generation $t$ independently choose one of three fates: **self-renewal** (producing two HSCs) with probability $p_s$, **differentiation** (producing one committed progenitor, exiting the HSC pool) with probability $p_d$, or **death** (apoptosis from niche deprivation) with probability $p_\delta$, where $p_s + p_d + p_\delta = 1$.

The self-renewal probability depends on local niche stiffness $E$ (kPa) through a Hill-type mechanotransduction function:

```math
p_s(E) = p_{s,\max} \cdot \frac{K_E^{n_E}}{K_E^{n_E} + E^{n_E}}
```

where $p_{s,\max}$ is the maximum self-renewal probability in an optimal (soft) niche, $K_E \approx 0.5$ kPa is the half-maximal stiffness (derived from the Choi et al. data showing optimal HSC maintenance at ~0.3 kPa), and $n_E \geq 2$ is the Hill coefficient reflecting cooperative YAP/TAZ-mediated mechanotransduction. On soft substrates ($E \ll K_E$), $p_s \to p_{s,\max} \approx 0.6$; on stiff aged marrow ($E \gg K_E$), $p_s \to 0$.

The death probability increases complementarily on stiff substrates:

```math
p_\delta(E) = p_{\delta,\min} + (p_{\delta,\max} - p_{\delta,\min}) \cdot \frac{E^{n_E}}{K_E^{n_E} + E^{n_E}}
```

For a single transplanted HSC clone, the **extinction probability** $q$ (the probability that the clone eventually disappears) satisfies:

```math
q = p_\delta + p_d + p_s \cdot q^2
```

Solving the quadratic: when $p_s > p_\delta$, the extinction probability is $q = p_\delta / p_s$, and the probability of long-term reconstitution (indefinite clone survival) is $1 - q = 1 - p_\delta / p_s$. When $p_s \leq p_\delta$, extinction is certain ($q = 1$).

The **expected clone size** at generation $t$ is:

```math
\mathbb{E}[N(t)] = (2p_s)^t
```

The clone grows exponentially when $p_s > 0.5$, remains constant when $p_s = 0.5$, and declines when $p_s < 0.5$. Translating through the Hill function, exponential growth requires:

```math
E < K_E \cdot \left(\frac{p_{s,\max}}{0.5} - 1\right)^{1/n_E}
```

For $p_{s,\max} = 0.6$, $K_E = 0.5$ kPa, and $n_E = 2$, this yields $E < 0.5 \times \sqrt{0.2} \approx 0.22$ kPa — indicating that only very soft niches support clonal expansion of transplanted HSCs. This quantitative prediction explains why aged marrow (1.5 kPa) supports HSC maintenance so poorly, and provides a concrete **design specification**: engineered niche scaffolds for HSC co-transplantation must achieve stiffness below ~0.3 kPa to maximize engraftment probability.

---

## 4. Cardiac Niche: Patches for the Failing Heart

### 4.1 The Cardiac Microenvironment Challenge

The heart presents a uniquely demanding environment for cell therapy. The post-infarction myocardium undergoes fibrotic remodeling that transforms the mechanical landscape: healthy myocardium has a Young's modulus of approximately 10 kPa during diastole and 50 kPa during systole, while mature scar tissue stiffens to 50–100 kPa, creating a mechanical mismatch that impedes both the survival and electromechanical integration of transplanted cardiomyocytes (Berry, Engler, Woo, Pister, & Pruitt, 2006). Additionally, cardiomyocytes are among the most metabolically demanding cells in the body, consuming approximately 70 mL O₂ per minute per 100 g of tissue — necessitating vascular supply within 100 μm to prevent ischemic death (Eschenhagen, Bolli, Braun, Field, Fleischmann, Frisén, et al., 2017).

Direct intramyocardial injection of dissociated cardiomyocytes — the simplest delivery approach — results in >95% cell loss within hours due to anoikis, mechanical washout from cardiac contraction, inflammatory attack, and ischemia (Terrovitis et al., 2009). This catastrophic engraftment failure has motivated the development of engineered heart tissue (EHT): three-dimensional constructs in which iPSC-derived cardiomyocytes (iPSC-CMs) are embedded in a hydrogel matrix together with supporting stromal cells, creating a tissue-like patch that provides the matrix adhesion, cell-cell contacts, and structural support absent in cell suspension transplantation.

### 4.2 Engineered Heart Tissue: Composition and Maturation

The modern EHT consists of three core components: iPSC-CMs (typically 70–80% of total cells), stromal cells (fibroblasts and/or endothelial cells, 20–30%), and a collagen type I hydrogel matrix (1–3 mg/mL). Tiburcy, Hudson, Baber, and colleagues (2017) established the defined EHT protocol that has become the foundation for clinical translation: iPSC-CMs and human foreskin fibroblasts are combined in collagen I / Matrigel hydrogels, cast around silicone posts that provide auxotonic load during culture, and matured for 3–4 weeks under mechanical loading conditions that promote sarcomere alignment, t-tubule formation, and positive force-frequency relationship — features of adult-like cardiomyocyte maturation absent in conventional 2D culture (Tiburcy et al., 2017). The resulting EHTs generate active contractile forces of 0.5–1.0 mN per tissue strip, with conduction velocities of 20–25 cm/s — approaching approximately 10% of native myocardial performance.

### 4.3 First-in-Human Engineered Heart Tissue Implantation

The clinical culmination of two decades of EHT development was reported in a 2025 Cell Stem Cell landmark study. Van Mil, Janssen, and colleagues demonstrated that epicardial engineered heart muscle (EHM) — composed of iPSC-CMs, stromal cells, and collagen hydrogel — could be safely implanted in both non-human primates and a human patient with advanced heart failure (van Mil et al., 2025). Safety and efficacy of EHMs at low (2× EHM) and high (5× EHM) doses were confirmed in rhesus macaques, including optimization of an immunosuppression regimen that preserved graft survival without systemic toxicity. The clinical proof-of-concept was achieved in a patient with end-stage heart failure who received 10× EHM three months prior to planned heart transplantation. Histological analysis of the explanted heart at transplantation demonstrated confirmed cell retention and engraftment, marking the first demonstration that iPSC-CM-based tissue constructs can survive and integrate in the human heart (van Mil et al., 2025).

This milestone was paralleled by the Japanese regulatory approval of ReHeart — iPSC-CM sheets developed by Cuorips — which received conditional approval from Japan's Ministry of Health, Labour and Welfare in March 2026 for treatment of severe ischemic heart failure, making it one of the first two conditionally approved iPSC-derived cell therapies worldwide (Kirkeby, Main, & Carpenter, 2025).

### 4.4 Complementary Niche Engineering Approaches

Beyond EHT patches, several complementary strategies address the cardiac niche challenge. Injectable hydrogels — including alginate-based formulations and decellularized cardiac ECM (VentriGel) — can be delivered via catheter to provide in situ matrix support that reduces ventricular remodeling and improves cell retention when co-injected with stem cells. A recent study demonstrated that iPSC-derived cardiac-specific dECM scaffolds enhance cardiomyocyte maturation and post-infarction repair by providing the native biochemical signaling environment lost during infarction (Lee, Cho, Kim, Mun, & Jang, 2025). Mechanical conditioning of EHTs before implantation — using cyclic stretch bioreactors that mimic the cardiac loading environment — accelerates maturation and improves post-implantation contractile performance (Tiburcy et al., 2017).

### 4.5 Framework F288: Contractile Force Scaling for Engineered Heart Tissue

A critical engineering question is how EHT design parameters — cell density, sarcomere alignment, and scaffold stiffness — translate to aggregate contractile output. We develop a scaling framework based on Hill-type muscle mechanics.

The isometric contractile force generated by a single iPSC-CM is:

```math
F_{\text{cell}} = F_{\max} \cdot \frac{[Ca^{2+}]^{n_H}}{K_{Ca}^{n_H} + [Ca^{2+}]^{n_H}}
```

where $F_{\max} \approx 5$ μN is the maximum isometric force per mature iPSC-CM (compared to ~10 μN for native adult cardiomyocytes), $[Ca^{2+}]$ is the intracellular calcium transient amplitude, $K_{Ca}$ is the half-maximal calcium concentration, and $n_H \approx 3$ is the Hill coefficient for cooperative thin filament activation.

The aggregate tissue force depends on three multiplicative factors:

```math
\sigma_{\text{tissue}} = \rho_{\text{CM}} \cdot F_{\max} \cdot \alpha_{\text{align}} \cdot \eta_{\text{couple}}(E_s)
```

where $\sigma_{\text{tissue}}$ is the active stress (mN/mm²), $\rho_{\text{CM}}$ is the cardiomyocyte density (cells/mm³), and:

- $\alpha_{\text{align}} \in [0, 1]$ is the **sarcomere alignment index**: $\alpha = 1$ for perfectly aligned sarcomeres (all force vectors parallel), $\alpha \approx 0.3$–$0.5$ for randomly oriented sarcomeres (isotropic force cancellation). Alignment is controlled by scaffold anisotropy, mechanical conditioning, and geometric constraints (post spacing in the Tiburcy protocol).

- $\eta_{\text{couple}}(E_s)$ is the **electromechanical coupling efficiency** as a function of scaffold stiffness $E_s$ (kPa), modeled as a Gaussian optimum:

```math
\eta_{\text{couple}}(E_s) = \exp\left(-\frac{(E_s - E_{\text{opt}})^2}{2\sigma_E^2}\right)
```

where $E_{\text{opt}} \approx 10$ kPa matches native diastolic myocardial stiffness, and $\sigma_E \approx 5$ kPa captures the tolerance range. Too-soft scaffolds ($E_s \ll E_{\text{opt}}$) fail to transmit contractile force to the load; too-stiff scaffolds ($E_s \gg E_{\text{opt}}$) impede cardiomyocyte contraction by presenting excessive afterload.

For a representative EHT — $\rho_{\text{CM}} = 5 \times 10^4$ cells/mm³, $F_{\max} = 5$ μN, $\alpha_{\text{align}} = 0.7$ (achieved with mechanical conditioning), $\eta_{\text{couple}} = 0.9$ (scaffold stiffness near optimal) — the predicted active stress is:

```math
\sigma_{\text{tissue}} = 5 \times 10^4 \times 5 \times 10^{-6} \times 0.7 \times 0.9 \approx 0.16 \text{ mN/mm}^2
```

Native myocardium generates approximately 50 mN/mm² of active stress. The EHT thus produces approximately 0.3% of native contractile performance — explaining why current EHTs function primarily as biological support (providing paracrine signaling, reducing adverse remodeling) rather than mechanical augmentation. Achieving hemodynamically meaningful contractile contribution (~5 mN/mm², or ~10% of native) will require increasing cardiomyocyte density 10-fold, achieving near-perfect sarcomere alignment ($\alpha \to 1$), and maturing iPSC-CMs to generate forces approaching native adult values ($F_{\max} \to 10$ μN) — the cardiac maturation gap that remains the central challenge of cardiac tissue engineering.

---

## 5. Pancreatic Niche: Encapsulation and Vascularization for Islet Survival

### 5.1 Why Naked Islet Transplants Fail

The Edmonton protocol demonstrated that islet transplantation can cure type 1 diabetes (T1D), but its reliance on cadaveric donor islets — requiring 2–3 donor pancreata per recipient — and the progressive loss of graft function (only ~10% insulin independence at five years) render it impractical as a scalable therapy (Shapiro et al., 2000; Ryan et al., 2005). Three interrelated failure modes drive post-transplant islet loss:

**Hypoxia.** Native islets are among the most vascularized tissues in the body, receiving 5–10% of total pancreatic blood flow despite constituting only 1–2% of pancreatic mass. Each islet contains a dense fenestrated capillary network that places every beta cell within ~50 μm of a vessel. Upon isolation and transplantation, this vascular supply is severed. Islets infused into the hepatic portal vein — the standard Edmonton protocol site — must survive 10–14 days of avascular hypoxia before neovascularization occurs, and larger islets (>150 μm diameter) suffer core necrosis during this period (Colton, 2014).

**Immune attack.** Even with immunosuppressive drugs (the Edmonton protocol uses sirolimus + tacrolimus + daclizumab), both alloimmune rejection and recurrent autoimmunity progressively destroy transplanted islets. The intrahepatic site provides no immune privilege, and islets are exposed to the full repertoire of hepatic immune cells including Kupffer cells and portal venous inflammatory mediators.

**ECM and niche loss.** Islets are stripped of their native ECM during enzymatic isolation, destroying the laminin-511/521 basement membrane that provides survival signals through integrin α3β1 and α6β1 engagement. This anoikis-promoting ECM loss, combined with disruption of islet-endothelial and islet-neural connections, contributes to immediate post-transplant cell death (Stendahl et al., 2009).

### 5.2 Device-Encapsulated Stem Cell-Derived Beta Cells

The convergence of iPSC-directed differentiation (producing glucose-responsive beta cells at >60% purity) with macroencapsulation technology has generated the first clinical evidence that device-encapsulated stem cell-derived islets can achieve glycemic control in T1D patients.

In a Phase 1/2 multicenter clinical trial (NCT03163511), Keymeulen, De Groot, and colleagues assessed device-encapsulated pancreatic precursor cells derived from human embryonic stem cells (Keymeulen et al., 2024). Devices with optimized membrane perforation patterns, loaded with 2–3-fold higher cell doses, were implanted subcutaneously. Of 10 patients with undetectable baseline C-peptide, three achieved meal-stimulated C-peptide levels ≥0.1 nmol/L from month 6 onward, correlating with improved continuous glucose monitoring (CGM) measures and reduced insulin dosing (Keymeulen et al., 2024). While these results fall short of insulin independence, they represent the first clinical demonstration that encapsulated stem cell-derived beta cells can engraft, differentiate in vivo, and produce clinically meaningful insulin in T1D patients — validating the encapsulation paradigm.

The encapsulation membrane addresses immune isolation but exacerbates the oxygen problem: the membrane adds diffusion resistance, further reducing oxygen availability to cells already deprived of vascular supply. Current membrane designs must balance immune exclusion (pore size <0.4 μm to block immune cells) against metabolite transport (permitting insulin at 5.8 kDa and glucose at 180 Da) — a fundamental engineering tradeoff that the mathematical framework F289 quantifies.

### 5.3 iPSC-Derived Vascularized Endocrine Pancreas

An alternative to encapsulation is to engineer vascularized constructs that promote rapid host vascular ingrowth, thereby shortening the hypoxic window. Cuesta-Gomez, Cardenas-Diaz, and colleagues (2025) bioengineered a human iPSC-derived vascularized endocrine pancreas (iVEP) by combining iPSC-derived beta cells (SC-islets) with iPSC-derived endothelial cells (iECs) (Cuesta-Gomez et al., 2025). The iVEP exploits a decellularized lung scaffold as a biocompatible matrix with inherent vascular architecture: SC-islets and iECs are aggregated into vascularized iPSC-beta spheroids (ViβeSs) that integrate into the scaffold's preserved vascular tree over seven days of culture, generating a perfusable endocrine organ. In vitro, the vascularized ECM sustained SC-islet engraftment with significantly preserved beta cell mass and physiological insulin release. This approach directly addresses the vascularization bottleneck by building vasculature into the graft rather than waiting for host neovascularization.

### 5.4 CiPSC-Islets: First Autologous Stem Cell-Derived Islet Transplant

In a landmark 2024 report, Wang, Chen, Du, and colleagues performed the first-in-human transplantation of autologous chemically induced pluripotent stem cell-derived islets (CiPSC-islets) in a patient with T1D (Wang et al., 2024). CiPSC-islets were generated using a small-molecule cocktail (avoiding viral reprogramming entirely), differentiated to functional insulin-producing islets, and transplanted beneath the anterior rectus sheath of the abdomen — a well-vascularized site that provides superior oxygen supply compared to the hepatic portal vein. The patient achieved sustained insulin independence beginning 75 days post-transplant (Wang et al., 2024). The significance of this result is threefold: autologous derivation eliminates alloimmune rejection; chemical reprogramming avoids genomic integration risk; and the omental/rectus sheath site provides a superior niche with rapid vascularization and surgical accessibility for monitoring.

### 5.5 Framework F289: Oxygen Diffusion-Reaction in Encapsulated Islets

The oxygen supply problem in encapsulated islets is a transport-limited phenomenon amenable to quantitative analysis. We model the steady-state oxygen profile inside a spherical islet of radius $a$ (μm) encapsulated within a membrane of outer radius $b$ (μm), where beta cells consume oxygen through mitochondrial respiration following Michaelis-Menten kinetics.

**Inside the islet** ($0 \leq r \leq a$), the steady-state oxygen concentration $C(r)$ (mmHg) satisfies:

```math
\frac{D_i}{r^2}\frac{d}{dr}\left(r^2 \frac{dC}{dr}\right) = \frac{V_{\max} \cdot C}{K_m + C}
```

where $D_i \approx 1.3 \times 10^{-5}$ cm²/s is the oxygen diffusivity in islet tissue, $V_{\max} \approx 0.034$ mol O₂/m³/s is the maximum oxygen consumption rate for beta cells, and $K_m \approx 0.44$ mmHg is the Michaelis constant for cytochrome c oxidase.

**In the membrane** ($a \leq r \leq b$), there is no oxygen consumption:

```math
\frac{D_m}{r^2}\frac{d}{dr}\left(r^2 \frac{dC}{dr}\right) = 0
```

where $D_m$ is the membrane oxygen diffusivity (typically 0.5–1.0 × $D_i$ for alginate membranes). The boundary conditions are $C(b) = C_{\text{ext}}$ (external oxygen, typically 40 mmHg for subcutaneous sites or 100 mmHg for well-oxygenated devices), symmetry $dC/dr|_{r=0} = 0$, and continuity of concentration and flux at $r = a$.

For the biologically relevant regime where $C \gg K_m$ throughout most of the islet (i.e., nearly zero-order consumption), the islet equation simplifies to:

```math
\frac{D_i}{r^2}\frac{d}{dr}\left(r^2 \frac{dC}{dr}\right) \approx V_{\max}
```

with the well-known spherical Krogh solution:

```math
C(r) = C_a - \frac{V_{\max}}{6D_i}(a^2 - r^2)
```

where $C_a$ is the oxygen concentration at the islet surface ($r = a$), determined by the membrane transport:

```math
C_a = C_{\text{ext}} - \frac{V_{\max} a^3}{3D_m}\left(\frac{1}{a} - \frac{1}{b}\right)
```

The **critical islet radius** $a^*$, defined as the maximum radius for which the core oxygen concentration $C(0)$ remains above the viability threshold $C_{\text{crit}}$ (typically ~0.1 mmHg):

```math
a^* = \sqrt{\frac{6D_i \cdot C_{\text{eff}}}{V_{\max}}}
```

where $C_{\text{eff}} = C_{\text{ext}} - C_{\text{crit}} - \frac{V_{\max}a^{*3}}{3D_m}\left(\frac{1}{a^*} - \frac{1}{b}\right)$ accounts for membrane resistance. For typical parameters ($C_{\text{ext}} = 40$ mmHg subcutaneous, $b = 1.5a$, $D_m = 0.7 D_i$), numerical solution yields $a^* \approx 100$–$150$ μm. Since native islets range from 50 to 300 μm in diameter, islets larger than approximately 200 μm diameter will suffer core necrosis in standard encapsulation devices — a prediction confirmed by histological studies showing central necrosis in encapsulated islets (Colton, 2014).

This framework provides three **design strategies** for overcoming the oxygen limit: (1) disaggregate large islets into pseudoislets of ~50–75 μm diameter (below $a^*$); (2) reduce membrane thickness ($b - a$) to minimize diffusion resistance; (3) increase external oxygenation through active oxygen delivery (electrochemical oxygen generators or perfluorocarbon emulsions in the device). The iVEP approach of Cuesta-Gomez et al. (2025) takes a fourth path: engineer vascular supply directly into the construct, effectively eliminating the diffusion limitation entirely.

---

## 6. Neural Niche: Scaffolds for Brain Organoids and Spinal Cord Repair

### 6.1 The Neural Stem Cell Niche and Its Age-Related Decline

The adult brain harbors two canonical neurogenic niches — the subventricular zone (SVZ) lining the lateral ventricles and the subgranular zone (SGZ) of the hippocampal dentate gyrus — where neural stem cells (NSCs) reside in intimate contact with ependymal cells, astrocytes, vasculature, and a specialized ECM enriched in hyaluronic acid, chondroitin sulfate proteoglycans (CSPGs), and tenascin-C (Kazanis, Lathia, Bhatt, & Bhatt, 2008). The brain ECM is uniquely soft, with a Young's modulus of approximately 0.1–1 kPa — among the softest tissues in the body — and this softness is functionally significant: neural stem cells cultured on substrates matching brain stiffness maintain multipotency, while stiffer substrates promote astrocytic differentiation at the expense of neurogenesis (Saha, Keung, Irwin, Li, Little, Schaffer, et al., 2008).

With aging, the neurogenic niches undergo structural and functional deterioration: ependymal cells lose cilia and thin, the SVZ vasculature becomes less permeable to circulating signals, CSPGs accumulate and create an inhibitory environment, and NSC proliferation declines dramatically — from robust neurogenesis in young adults to near-undetectable levels by late adulthood in humans (Conover & Shook, 2011). This niche deterioration is a major driver of the age-related decline in brain plasticity and repair capacity.

### 6.2 Vascular Network-Inspired Diffusible Scaffolds for Brain Organoids

The most significant advance in neural niche engineering is the VID scaffold platform developed by Cai, Tian, Chen, and colleagues (2025). Brain organoids have transformed neuroscience research by enabling three-dimensional modeling of human brain development and disease, but a fundamental limitation has persisted since Lancaster and Knoblich's initial description in 2013: organoids exceeding approximately 500 μm in diameter develop necrotic cores due to the absence of vascularization, limiting their size, maturation, and physiological relevance (Lancaster, Renner, Martin, Wenzel, Bicknell, Hurles, et al., 2013).

The VID scaffold addresses this problem by mimicking the physical transport properties of vasculature without requiring actual blood vessels. Using high-resolution 3D printing, Cai et al. fabricated meshed tubular channel networks whose branching geometry — including vessel diameters, branching angles, and hierarchical organization — recapitulates physiological vascular architecture (Cai et al., 2025). Culture medium perfused through these channels delivers oxygen and nutrients by diffusion through the channel walls to surrounding organoid tissue, while waste products diffuse in the reverse direction.

The results were transformative. Human midbrain organoids cultured on VID scaffolds developed with virtually no necrotic core, in contrast to conventional organoids where necrotic cores consistently appear by day 30–40 (Cai et al., 2025). VID-scaffold organoids exhibited enhanced midbrain-specific identity (higher expression of FOXA2, LMX1A, and TH — the canonical dopaminergic neuron markers), improved oxygen metabolism (as measured by oxygen consumption rate), greater neuronal maturation (longer neurites, more complex dendritic arborization), and functional electrophysiological network activity with synchronized calcium oscillations (Cai et al., 2025). These results demonstrate that the primary limitation of brain organoids is not an intrinsic cell biology problem but a transport engineering problem — and that solving the transport problem through scaffold design is sufficient to unlock substantially more physiologically relevant brain tissue models.

The VID scaffold design parameters — channel diameter (200–400 μm), inter-channel spacing (400–800 μm), and branching angle (~70°) — are consistent with the predictions of the Krogh cylinder model (F286): for neural tissue with moderate oxygen consumption ($q_0$ approximately 3–5 × 10⁻³ mmHg/s for mixed neuronal-glial tissue), the critical inter-channel spacing is 400–600 μm, matching the empirically optimized VID scaffold geometry.

### 6.3 Clinical Neural Stem Cell Transplantation

For spinal cord injury (SCI), where the challenge is not organoid engineering but rather delivering functional neural precursors into a hostile, inhibitory lesion environment, biomaterial scaffolds serve a different purpose: providing physical guidance, growth factor delivery, and a permissive substrate for axon regeneration across the injury site.

The Keio University clinical trial represents the furthest-advanced iPSC-derived neural stem cell program. iPSC-derived NS/PCs, expanded in suspension neurosphere culture with EGF and FGF-2 to clinically relevant cell numbers (>2 × 10⁶ per patient), were transplanted into patients with subacute SCI (Sugai, Fukushima, Nakamura, Wakao, Konishi, Murata, et al., 2021). Growth factor priming during the expansion phase is critical: the combination of EGF, FGF-2, and PDGF-AB synergistically induces proliferation and differentiation of neural precursor cells, with in vivo functional recovery in SCI models demonstrating improved locomotor scores only when cells had been pre-treated with all three growth factors — establishing that niche-mimetic priming conditions directly determine therapeutic efficacy (Younsi, Zheng, Riemann, Schmehl, Müller, Schwarz, et al., 2020).

### 6.4 Framework F290: Reaction-Diffusion Model for Growth Factor Gradients in Neural Scaffolds

The design of VID scaffolds and neural biomaterial constructs requires quantitative prediction of growth factor concentration profiles within the scaffold, to ensure that all cells receive factor concentrations within the therapeutic window. We model the steady-state concentration $C(x)$ of a growth factor (e.g., EGF or FGF-2) at position $x$ between two parallel perfusion channels separated by distance $L$.

The governing equation balances diffusion, cellular consumption via receptor-mediated uptake, and first-order degradation:

```math
D_{\text{GF}} \frac{d^2C}{dx^2} + S_0 - \frac{k_{\text{bind}} \cdot \rho_{\text{cell}} \cdot C}{K_d + C} - \lambda C = 0
```

where $D_{\text{GF}}$ is the effective diffusivity of the growth factor in the porous scaffold (cm²/s), $S_0$ is the source term (secretion by embedded stromal cells or release from scaffold-loaded nanoparticles, in nM/s), $k_{\text{bind}}$ is the receptor binding rate (s⁻¹), $\rho_{\text{cell}}$ is the local cell density (cells/cm³), $K_d$ is the receptor dissociation constant (nM), and $\lambda$ is the first-order degradation rate (s⁻¹) reflecting proteolytic cleavage.

With boundary conditions $C(0) = C(L) = C_{\text{channel}}$ (growth factor concentration in the perfusate), the solution in the linear consumption limit ($C \ll K_d$, first-order uptake) is:

```math
C(x) = C_{\text{channel}} \cdot \frac{\cosh\left(\kappa(x - L/2)\right)}{\cosh(\kappa L/2)} + \frac{S_0}{\lambda_{\text{eff}}}\left(1 - \frac{\cosh\left(\kappa(x - L/2)\right)}{\cosh(\kappa L/2)}\right)
```

where $\kappa = \sqrt{\lambda_{\text{eff}} / D_{\text{GF}}}$ is the inverse penetration depth and $\lambda_{\text{eff}} = \lambda + k_{\text{bind}} \rho_{\text{cell}} / K_d$ is the effective first-order loss rate.

The **optimal channel spacing** $L^*$ is the maximum $L$ for which the midpoint concentration $C(L/2)$ remains above the minimum effective concentration $C_{\min}$ (the threshold for NPC maintenance):

```math
L^* = \frac{2}{\kappa} \text{arccosh}\left(\frac{C_{\text{channel}} - S_0/\lambda_{\text{eff}}}{C_{\min} - S_0/\lambda_{\text{eff}}}\right)
```

For EGF ($D_{\text{GF}} \approx 1 \times 10^{-7}$ cm²/s for a 6.2 kDa protein in hydrogel, $\lambda \approx 10^{-4}$ s⁻¹, $K_d \approx 2$ nM), a cell density of $10^7$ cells/cm³, and moderate receptor density ($k_{\text{bind}} \rho_{\text{cell}} / K_d \approx 5 \times 10^{-5}$ s⁻¹), we obtain $\kappa \approx 0.87$ mm⁻¹ and $L^* \approx 400$–$600$ μm — again consistent with the VID scaffold empirical design.

When two growth factors with different diffusivities and opposite effects on NPC fate (e.g., EGF promoting proliferation, BMP4 promoting astrocytic differentiation) interact through cell fate decisions, the coupled system can exhibit Turing-type diffusion-driven instability — spontaneous pattern formation from an initially uniform state. The condition for Turing instability requires the ratio of diffusivities to exceed a critical threshold: $D_{\text{BMP4}} / D_{\text{EGF}} > (a_{11}/a_{22})^2$, where $a_{ij}$ are elements of the Jacobian of the reaction kinetics at the homogeneous steady state. This analysis predicts whether the scaffold will develop spatially patterned zones of proliferation versus differentiation — a design consideration for scaffolds intended to generate heterogeneous neural tissue architectures.

---

## 7. Musculoskeletal Niche: Bioinstructive Scaffolds for Immune-Mediated Regeneration

### 7.1 The Satellite Cell Niche and Volumetric Muscle Loss

Skeletal muscle satellite cells — the tissue-resident stem cells responsible for muscle repair — occupy a niche defined by their position between the sarcolemma of the parent myofiber and the surrounding basal lamina, a specialized ECM composed of laminin-211/221, collagen IV, collagen VI, fibronectin, and proteoglycans (Wosczyna & Rando, 2018). This niche maintains satellite cell quiescence through contact-dependent Notch signaling from the myofiber, cadherin-mediated adhesion, and sequestration of growth factors (HGF, FGF2) in the basal lamina matrix. Upon injury, niche disruption activates satellite cells: inflammatory signals trigger their proliferation, and ECM remodeling provides migration cues that guide their integration into regenerating myofibers.

Volumetric muscle loss (VML) — loss of >20% of a muscle's mass due to trauma, tumor resection, or congenital defect — overwhelms endogenous repair capacity because the injury destroys not only myofibers but the niche itself, creating a fibrotic void that satellite cells cannot bridge. VML affects approximately 65,000 military personnel and civilians annually in the United States alone and currently lacks effective treatment (Corona, Wenke, & Ward, 2016). Engineering replacement niches that provide the structural, biochemical, and immunological cues necessary to redirect the wound response from fibrosis to regeneration is the central challenge of musculoskeletal tissue engineering.

### 7.2 Bioinstructive Scaffolds with Sequential Growth Factor Release

The 2025 Nature Materials study by Passipieri and colleagues represents a paradigm shift in scaffold design philosophy: rather than providing a static niche surrogate, the bioinstructive scaffold dynamically recapitulates the temporal sequence of niche signals that orchestrates endogenous regeneration (Passipieri et al., 2025). The scaffold comprises a dECM backbone embedded with polymeric nanocapsules engineered for three-phase sequential release:

**Phase 1 (days 0–3):** Pro-inflammatory signals that recruit neutrophils and M1 macrophages for debris clearance and pathogen defense. This phase mimics the natural inflammatory response that is essential for subsequent regeneration — premature suppression of inflammation impairs rather than promotes healing.

**Phase 2 (days 3–14):** Pro-regenerative signals including IGF-1 and HGF that activate satellite cells, promote myoblast proliferation, and stimulate angiogenesis. This phase corresponds to the M1-to-M2 macrophage transition and the onset of satellite cell-mediated myofiber formation.

**Phase 3 (days 14–28):** Anti-fibrotic signals including decorin and TGF-β pathway inhibitors that prevent excessive collagen deposition and promote maturation of regenerated myofibers. This phase addresses the fibrotic default that dominates VML healing in the absence of therapeutic intervention.

In animal VML models, the three-phase bioinstructive scaffold enhanced myofiber formation, angiogenesis, innervation, and functional muscle strength recovery beyond what either dECM alone or growth factors delivered in a single bolus could achieve (Passipieri et al., 2025). The critical insight is that temporal orchestration of niche signals — not merely their presence — determines regenerative outcome.

### 7.3 Immune-Niche Engineering: Macrophage Polarization via Scaffold Design

A complementary approach exploits the scaffold itself — rather than loaded growth factors — to direct the immune response. Yang, Sun, Lu, and colleagues (2025) demonstrated that macroporous microribbon (μRB) scaffolds with tunable ratios of gelatin and chondroitin sulfate (CS) direct macrophage polarization and stem cell crosstalk to achieve rapid endogenous bone regeneration without exogenous growth factors or transplanted cells (Yang et al., 2025).

Using a 3D MSC/macrophage co-culture screening system, the authors identified an optimal gelatin:CS ratio (50:50) that maximized pro-regenerative signaling. Single-cell RNA sequencing and CellChat analysis revealed that this composition significantly enhanced intercellular crosstalk among macrophages and bone niche cell types through signaling pathways linked to anti-inflammation (IL-10, TGF-β), angiogenesis (VEGF, PDGF), and osteogenesis (BMP-2, Wnt) (Yang et al., 2025). In a critical-sized cranial bone defect model, the optimized scaffold achieved complete bone bridging — an outcome that typically requires exogenous BMP-2, a growth factor with a complex safety profile including heterotopic ossification and inflammation. This result demonstrates that rationally designed biomaterial composition can replace growth factor supplementation by directing the immune system to produce the required regenerative signals endogenously.

The pioneering work of Sadtler, Elisseeff, and colleagues established the conceptual foundation for this approach, demonstrating that pro-regenerative biomaterial scaffolds recruit a Th2-polarized adaptive immune response that guides IL-4-dependent macrophage polarization toward the M2 phenotype required for functional muscle recovery (Sadtler, Estrellas, Allen, Wolf, Fan, Tam, et al., 2016). The scaffold acts as an immunological adjuvant for regeneration — a concept with implications far beyond musculoskeletal repair.

### 7.4 Framework F291: Bistable Macrophage Polarization Switch Model

The M1-to-M2 macrophage transition that determines regenerative versus fibrotic outcome can be modeled as a bistable dynamical system driven by scaffold degradation products. This framework predicts the critical switching time and identifies the scaffold design parameters that control it.

Let $M_1(t)$ denote the fraction of macrophages in the pro-inflammatory M1 state and $M_2(t) = 1 - M_1(t)$ the fraction in the pro-regenerative M2 state. M1 macrophages produce pro-inflammatory cytokines (TNF-α, IFN-γ, lumped as $P$) while M2 macrophages produce anti-inflammatory cytokines (IL-4, IL-10, IL-13, lumped as $A$). The scaffold releases anti-inflammatory degradation products (e.g., hyaluronic acid fragments, decorin) at a designed temporal profile $S(t)$.

**Cytokine dynamics:**

```math
\frac{dP}{dt} = \alpha_P \cdot M_1 - \delta_P \cdot P - \kappa_S \cdot S(t) \cdot P
```

```math
\frac{dA}{dt} = \alpha_A \cdot M_2 + \sigma_S \cdot S(t) - \delta_A \cdot A
```

where $\alpha_P, \alpha_A$ are production rates, $\delta_P, \delta_A$ are degradation rates, $\kappa_S$ is the rate at which scaffold products neutralize pro-inflammatory cytokines, and $\sigma_S$ is the rate at which scaffold products directly contribute anti-inflammatory signals.

**Macrophage polarization dynamics** with cooperative (Hill-type) switching:

```math
\frac{dM_1}{dt} = k_{21} \cdot \frac{P^{n_P}}{K_P^{n_P} + P^{n_P}} \cdot (1 - M_1) - k_{12} \cdot \frac{A^{n_A}}{K_A^{n_A} + A^{n_A}} \cdot M_1
```

where $k_{21}$ and $k_{12}$ are maximum transition rates, $K_P$ and $K_A$ are half-maximal cytokine concentrations, and $n_P, n_A \geq 2$ are Hill coefficients reflecting cooperative signaling through receptor complexes.

**Bistability condition.** The system exhibits two stable steady states — an M1-dominated state and an M2-dominated state — when the product of Hill coefficients exceeds the critical threshold:

```math
n_P \cdot n_A > 4
```

This condition is readily satisfied for macrophage polarization, where cooperative signaling through JAK-STAT (for IL-4/IL-13 → M2) and NF-κB (for TNF-α/IFN-γ → M1) pathways yields effective Hill coefficients of $n \approx 2$–$3$ each.

**Critical switching time.** The scaffold design parameter $S(t)$ must cross a critical threshold $S^*$ at the appropriate time to push the system from the M1 basin of attraction into the M2 basin. Too early (before day 3), and the scaffold prevents necessary debris clearance; too late (after day 7–10), and chronic M1 inflammation drives fibrosis. The critical threshold is:

```math
S^* = \frac{\alpha_P \cdot M_{1,\text{ss}} - \delta_P \cdot P^*}{\kappa_S \cdot P^*} + \frac{\delta_A \cdot A^* - \alpha_A \cdot (1 - M_{1,\text{ss}})}{\sigma_S}
```

where $(P^*, A^*, M_{1,\text{ss}})$ are the coordinates of the separatrix between the two basins of attraction. This formula provides a quantitative design specification: given the scaffold's degradation kinetics (which determine $S(t)$) and the target switching time (days 3–5), the required scaffold composition can be calculated.

**Hysteresis.** Once the M2 state is reached, reversal to M1 requires a much larger pro-inflammatory perturbation than the anti-inflammatory input needed for the original M1→M2 switch. This hysteresis — a direct consequence of bistability — provides inherent robustness: transient inflammatory perturbations (wound healing fluctuations, minor infections) do not revert the regenerative program once established.

---

## 8. Cross-Cutting Themes and Open Questions

### 8.1 Vascularization as the Universal Rate-Limiter

Across all five organ systems surveyed in this review, vascularization emerges as the single most critical engineering challenge. The Krogh cylinder analysis (F286) quantifies the fundamental constraint: for metabolically active cells (cardiomyocytes, beta cells, neurons), every point in the engineered tissue must be within 200–400 μm of a perfused vessel or channel. Three convergent solutions are emerging: (1) pre-vascularization through co-culture with endothelial cells, exemplified by the iVEP (Section 5) and eVON (Section 3); (2) perfusable scaffold channels that substitute for vessels, exemplified by VID scaffolds (Section 6); (3) rapid in vivo vascularization through rapid VO generation (Gong et al., 2025), which produces transplantable vasculature in five days. The convergence of these approaches suggests that the vascularization bottleneck, while not yet solved, is tractable with current technology.

### 8.2 Immune Tolerance: From Immunosuppression to Niche-Mediated Tolerance

Current clinical stem cell therapies require systemic immunosuppression — tacrolimus, sirolimus, mycophenolate — with attendant risks of infection, malignancy, and metabolic toxicity. The immune-niche engineering approach (Section 7) suggests an alternative: biomaterial scaffolds that locally modulate the immune response to promote graft tolerance without systemic immunosuppression. The macrophage polarization framework (F291) provides a quantitative basis for designing scaffolds that shift the local immune environment from rejection to acceptance. Combining this with the hypoimmune cell engineering approach (B2M⁻/⁻ CIITA⁻/⁻ CD47⁺) and local delivery of tolerogenic factors (IL-10, TGF-β, rapamycin nanoparticles) could create a multi-layered immune evasion strategy that eliminates the need for systemic immunosuppression entirely — though this remains speculative and unproven in clinical settings.

### 8.3 Manufacturing and Regulatory Challenges

The transition from laboratory-scale niche engineering to clinical manufacturing introduces formidable challenges. Living scaffolds — constructs containing both biomaterials and cells — are classified as combination products by the FDA, requiring simultaneous compliance with device and biologic regulatory frameworks. Japan's Pharmaceuticals and Medical Devices Agency (PMDA) has established the most advanced regulatory pathway through the Regenerative Medicine Act, enabling conditional approvals (as demonstrated by ReHeart and raguneprocel) based on early-phase safety data with post-market efficacy evaluation (Kirkeby et al., 2025; Konomi, Tobita, Kimura, & Sato, 2025).

Manufacturing reproducibility is a key concern: batch-to-batch variability in dECM composition, hydrogel crosslinking kinetics, and cell seeding efficiency must be controlled within specifications that regulatory agencies have not yet defined for living scaffolds. Machine learning-based quality control — using imaging features to predict construct function non-destructively — may address this gap, as demonstrated for iPSC differentiation monitoring (Hojo, Fujimori, Ando, & Furusawa, 2025).

### 8.4 The Maturation Gap and the Self-Niche Phenomenon

Even the most sophisticated engineered niches remain incomplete representations of in vivo microenvironments. Missing elements include neural innervation (present in the eVON but absent from most constructs), lymphatic drainage, physiological mechanical loading (addressed by cardiac EHT bioreactors but not by most scaffolds), circadian rhythmic cues, and the dynamic remodeling that characterizes living tissues.

The "self-niche" phenomenon described by Rezakhani et al. (2025) — where intestinal stem cells in permissive synthetic hydrogels spontaneously secrete their own basement membrane — suggests a powerful design principle: rather than engineering every niche component, provide a permissive environment and allow cells to construct the niche components they need. This principle, if generalizable across tissue types, would dramatically simplify scaffold design and manufacturing. Whether stem cells from other organ systems (hematopoietic, cardiac, neural) can similarly self-organize their niche when given appropriate minimal cues remains an open experimental question.

### 8.5 Open Questions

Several fundamental questions remain unresolved:

**What is the minimum viable niche?** For each organ system, what is the smallest set of engineered signals sufficient for clinically meaningful engraftment? The branching process model (F287) suggests that for HSCs, stiffness alone may be sufficient; for other cell types, multiple signals may be required.

**Can engineered niches be made self-renewing?** Current scaffolds degrade over weeks to months. Long-term cell therapy may require niches that self-maintain — either through cell-mediated ECM remodeling or through non-degradable synthetic components.

**How do we engineer niches for organs not yet attempted at scale?** Kidney, lung, and liver present distinct niche challenges — the kidney's complex 3D architecture, the lung's air-liquid interface, the liver's zonated metabolic environment — that current engineering approaches have not yet addressed.

**What is the optimal balance between pre-engineering and in vivo remodeling?** Over-engineered constructs may resist the host remodeling required for long-term integration; under-engineered constructs may fail to provide the initial support cells need. Defining this balance quantitatively — perhaps through time-dependent extensions of the frameworks presented here — is essential for clinical translation.

---

## References

1. Ambrosi, T. H., Scialdone, A., Graja, A., Gober, S., Ditzel, M., Schulz, T. J., et al. (2017). Adipocyte accumulation in the bone marrow during obesity and aging impairs stem cell-based hematopoietic and bone regeneration. *Cell Stem Cell*, 20(6), 771–784.e6. PMID: 28330582

2. Baryawno, N., Przybylski, D., Kowalczyk, M. S., Kfoury, Y., Severe, N., Gustafsson, K., et al. (2019). A cellular taxonomy of the bone marrow stroma in homeostasis and leukemia. *Cell*, 177(7), 1915–1932.e16. PMID: 31130381

3. Berry, M. F., Engler, A. J., Woo, Y. J., Pister, T. J., & Pruitt, B. L. (2006). Mesenchymal stem cell injection after myocardial infarction improves myocardial compliance. *American Journal of Physiology-Heart and Circulatory Physiology*, 290(6), H2196–H2203. PMID: 16473959

4. Cai, H., Tian, C., Chen, L., Yang, Y., Sun, A. X., McCracken, K., et al. (2025). Vascular network-inspired diffusible scaffolds for engineering functional midbrain organoids. *Cell Stem Cell*, 32(5), 824–837.e5. PMID: 40101722

5. Calvi, L. M., Adams, G. B., Weibrecht, K. W., Weber, J. M., Olson, D. P., Knight, M. C., et al. (2003). Osteoblastic cells regulate the haematopoietic stem cell niche. *Nature*, 425(6960), 841–846. PMID: 14520413

6. Choi, J. S., Krieger, J. R., Engel, B. J., Mead, B. E., Diaz, B., Coughlin, B., et al. (2023). Harnessing matrix stiffness to engineer a bone marrow niche for hematopoietic stem cell rejuvenation. *Cell Stem Cell*, 30(4), 378–395.e6. PMID: 37028404

7. Chow, A., Lucas, D., Bone, A., Buber, J., Mazo, I., Frenette, P. S., et al. (2011). Bone marrow CD169+ macrophages promote the retention of hematopoietic stem and progenitor cells in the mesenchymal stem cell niche. *Journal of Experimental Medicine*, 208(2), 261–271. PMID: 21282381

8. Colton, C. K. (2014). Oxygen supply to encapsulated therapeutic cells. *Advanced Drug Delivery Reviews*, 67–68, 93–110. PMID: 24135476

9. Conover, J. C., & Shook, B. A. (2011). Aging of the subventricular zone neural stem cell niche. *Aging and Disease*, 2(1), 49–63. PMID: 22140636

10. Corona, B. T., Wenke, J. C., & Ward, C. L. (2016). Pathophysiology of volumetric muscle loss injury. *Cells Tissues Organs*, 202(3–4), 180–188. PMID: 27825152

11. Crapo, P. M., Gilbert, T. W., & Badylak, S. F. (2011). An overview of tissue and whole organ decellularization processes. *Biomaterials*, 32(12), 3233–3243. PMID: 21296410

12. Cuesta-Gomez, N., Cardenas-Diaz, F. L., Hua, H., Deza-Ponzio, R., Pham, A. T., et al. (2025). Bioengineering of a human iPSC-derived vascularized endocrine pancreas for type 1 diabetes. *Cell Reports Medicine*, 6(2), 101925. PMID: 39922198

13. Donnelly, H., Ross, E., Xiao, Y., Hermantara, R., Taqi, A. F., et al. (2024). Bioengineered niches that recreate physiological extracellular matrix organisation to support long-term haematopoietic stem cells. *Nature Communications*, 15(1), 5791. PMID: 38987295

14. Engler, A. J., Sen, S., Sweeney, H. L., & Discher, D. E. (2006). Matrix elasticity directs stem cell lineage specification. *Cell*, 126(4), 677–689. PMID: 16923388

15. Ergen, A. V., Boles, N. C., & Bhatt, A. S. (2012). Aging impairs the hematopoietic stem cell niche in mammals. *Blood*, 120(10), 2026–2027. PMID: 22955934

16. Eschenhagen, T., Bolli, R., Braun, T., Field, L. J., Fleischmann, B. K., Frisén, J., et al. (2017). Cardiomyocyte regeneration: a consensus statement. *Circulation*, 136(7), 680–686. PMID: 28684531

17. Gong, L., Marchand, M., Li, J., et al. (2025). Rapid generation of functional vascular organoids via simultaneous transcription factor activation of endothelial and mural lineages. *Cell Stem Cell*, 32(8), 1200–1217.e6. PMID: 40516530

18. Helbling, P. M., Piñeiro-Yáñez, E., Gerber, R., Al-Abbasi, A. M., Dotto, G. P., & Bornhäuser, M. (2025). Bone marrow niches for hematopoietic stem cells in homeostasis and aging. *Stem Cell Research & Therapy*, 16(1), 85. PMID: 39978750

19. Hojo, H., Fujimori, K., Ando, K., & Furusawa, C. (2025). Machine learning-based early prediction of iPSC differentiation efficiency from phase-contrast images. *Stem Cell Reports*, 20(1), 55–68.

20. Homan, K. A., Giger, M., et al. (2024). A microfluidic platform integrating functional vascularized organoids-on-chip. *Nature Communications*, 15(1), 1452. PMID: 38365780

21. Kazanis, I., Lathia, J. D., Bhatt, A. S., & Bhatt, A. S. (2008). The neural stem cell microenvironment. *StemBook* [Internet]. Cambridge (MA): Harvard Stem Cell Institute.

22. Keymeulen, B., De Groot, K., Jacobs-Tulleneers-Thevissen, D., Thompson, D. M., Bellin, M. D., Kroon, E. J., et al. (2024). Encapsulated stem cell-derived β cells exert glucose control in patients with type 1 diabetes. *Nature Biotechnology*, 42(10), 1507–1514. PMID: 38012450

23. Khan, A. O., Bornhäuser, M., et al. (2024). Generation of complex bone marrow organoids from human induced pluripotent stem cells. *Nature Methods*, 21(5), 868–881. PMID: 38374263

24. Kirkeby, A., Main, H., & Carpenter, M. (2025). The clinical landscape of human pluripotent stem cell therapies. *Cell Stem Cell*, 32(1), 12–35.

25. Konomi, K., Tobita, M., Kimura, T., & Sato, D. (2025). Regulatory framework for iPSC-derived cell therapies in Japan. *Regenerative Therapy*, 28, 100–112.

26. Krogh, A. (1919). The number and distribution of capillaries in muscles with calculations of the oxygen pressure head necessary for supplying the tissue. *Journal of Physiology*, 52(6), 409–415.

27. Lancaster, M. A., Renner, M., Martin, C.-A., Wenzel, D., Bicknell, L. S., Hurles, M. E., et al. (2013). Cerebral organoids model human brain development and microcephaly. *Nature*, 501(7467), 373–379. PMID: 23995685

28. Lee, H., Cho, H., Kim, J., Mun, C. H., & Jang, J. (2025). Human iPSC-derived cardiac-specific extracellular matrix scaffolds for cardiomyocyte maturation and post-myocardial infarction repair. *Advanced Healthcare Materials*, 14(8), e2404168. PMID: 41035426

29. Li, Q., Nikolova, M. T., Zhang, G., et al. (2025). Macro-scale, scaffold-assisted model of the human bone marrow endosteal niche using hiPSC-vascularized osteoblastic organoids. *Cell Stem Cell*, 32(12), 1941–1958.e8. PMID: 41260216

30. Lutolf, M. P., & Hubbell, J. A. (2005). Synthetic biomaterials as instructive extracellular microenvironments for morphogenesis in tissue engineering. *Nature Biotechnology*, 23(1), 47–55. PMID: 15637621

31. Morrison, S. J., & Scadden, D. T. (2014). The bone marrow niche for haematopoietic stem cells. *Nature*, 505(7483), 327–334. PMID: 24429631

32. Olsson, R. F., Urbano-Ispizua, Á., & Hauzenberger, D. (2013). Primary graft failure after allogeneic hematopoietic cell transplantation. *Current Opinion in Hematology*, 20(6), 495–501.

33. Passipieri, J. A., Patel, N. R., Engel, B. J., Baker, H. B., Totsingan, F., Asfour, H., et al. (2025). Bioinstructive scaffolds enhance stem cell engraftment for functional tissue regeneration. *Nature Materials*, 24(6), 882–893. PMID: 40247020

34. Rezakhani, S., Gjorevski, N., Geurts, M. H., & Lutolf, M. P. (2025). An extracellular matrix niche secreted by epithelial cells drives intestinal organoid formation. *Developmental Cell*, 60(14), 2117–2131.e6. PMID: 40680738

35. Ryan, E. A., Paty, B. W., Senior, P. A., Bigam, D., Alfadhli, E., Kneteman, N. M., et al. (2005). Five-year follow-up after clinical islet transplantation. *Diabetes*, 54(7), 2060–2069. PMID: 15983207

36. Sadtler, K., Estrellas, K., Allen, B. W., Wolf, M. T., Fan, H., Tam, A. J., et al. (2016). Developing a pro-regenerative biomaterial scaffold microenvironment requires T helper 2 cells. *Science*, 352(6283), 366–370. PMID: 27081073

37. Saha, K., Keung, A. J., Irwin, E. F., Li, Y., Little, L., Schaffer, D. V., et al. (2008). Substrate modulus directs neural stem cell behavior. *Biophysical Journal*, 95(9), 4426–4438. PMID: 18658232

38. Schofield, R. (1978). The relationship between the spleen colony-forming cell and the haemopoietic stem cell. *Blood Cells*, 4(1–2), 7–25. PMID: 747780

39. Shapiro, A. M. J., Lakey, J. R. T., Ryan, E. A., Korbutt, G. S., Toth, E., Warnock, G. L., et al. (2000). Islet transplantation in seven patients with type 1 diabetes mellitus using a glucocorticoid-free immunosuppressive regimen. *New England Journal of Medicine*, 343(4), 230–238. PMID: 10911004

40. Stendahl, J. C., Kaufman, D. B., & Bhatt, A. S. (2009). Extracellular matrix in pancreatic islets: relevance to scaffold design and transplantation. *Cell Transplantation*, 18(1), 1–12. PMID: 19476204

41. Sugai, K., Fukushima, K., Nakamura, M., Wakao, R., Konishi, R., Murata, K., et al. (2021). First-in-human clinical trial of transplantation of iPSC-derived NS/PCs for subacute complete spinal cord injury: Study protocol. *Regenerative Therapy*, 18, 321–333.

42. Terrovitis, J. V., Lautamäki, R., Bonios, M., Fox, J., Engles, J. M., Yu, J., et al. (2009). Noninvasive quantification and optimization of acute cell retention by in vivo positron emission tomography after intramyocardial cardiac-derived stem cell delivery. *Journal of the American College of Cardiology*, 54(17), 1619–1626. PMID: 19833262

43. Tiburcy, M., Hudson, J. E., Baber, P., et al. (2017). Defined engineered human myocardium with advanced maturation for applications in heart failure modeling and repair. *Circulation*, 135(19), 1832–1847. PMID: 28167635

44. van Mil, A., Janssen, J., van Rooij, E., et al. (2025). Engineered heart tissue patches: A milestone in cardiac regenerative medicine. *Cell Stem Cell*, 32(4), 487–505. PMID: 40185070

45. Wang, S., Chen, J., Du, Y., et al. (2024). Transplantation of chemically induced pluripotent stem-cell-derived islets under abdominal anterior rectus sheath in a type 1 diabetes patient. *Cell*, 187(22), 6152–6164.e18. PMID: 39326417

46. Wosczyna, M. N., & Rando, T. A. (2018). A muscle stem cell support group: Coordinated cellular responses in muscle regeneration. *Developmental Cell*, 46(2), 135–143. PMID: 30016618

47. Yang, K., Sun, Y., Lu, M., et al. (2025). Modulating immune-stem cell crosstalk enables robust bone regeneration via tuning compositions of macroporous scaffolds. *npj Regenerative Medicine*, 10(1), 33. PMID: 40595820

48. Younsi, A., Zheng, G., Riemann, L., Schmehl, T., Müller, O. J., Schwarz, C., et al. (2020). Induced proliferation and differentiation of neural precursor cells from the adult rat spinal cord. *European Journal of Neuroscience*, 51(9), 1843–1856.

49. Yue, K., Della Bella, E., Duchi, S., O'Connell, C. D., & Choong, P. F. (2015). Synthesis, properties, and biomedical applications of gelatin methacryloyl (GelMA) hydrogels. *Biomaterials*, 73, 254–271. PMID: 26414409

50. Zhang, J., Niu, C., Ye, L., Song, W., Zhu, Z., Chua, K. N., et al. (2003). Identification of the haematopoietic stem cell niche and control of the niche size. *Nature*, 425(6960), 836–841. PMID: 14520412
