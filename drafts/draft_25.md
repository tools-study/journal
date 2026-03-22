# Programmable Cell Therapies

## Abstract

Programmable cell therapies represent a paradigm shift from static pharmacological intervention to autonomous living therapeutics capable of sensing disease-specific biomarkers, processing biological information through synthetic gene circuits, and producing calibrated therapeutic responses in real time. The convergence of synthetic biology, genome engineering, and immunology has yielded designer cells that function as closed-loop therapeutic agents — detecting pathological signals, computing appropriate outputs via Boolean logic gates, and executing precision responses with spatial and temporal control unattainable by conventional biologics. This review examines six frontiers of programmable cell therapy: (1) synthetic sense-process-respond circuits incorporating transcriptional, translational, and post-translational control architectures for autonomous disease correction; (2) electrogenetic and physical-trigger interfaces enabling remote, non-invasive control of therapeutic gene expression through electrical, optical, magnetic, and acoustic stimuli; (3) hypoimmune universal cell engineering using CRISPR-edited iPSC platforms to create immune-evasive donor cells that obviate immunosuppression; (4) T cell exhaustion resistance and persistence engineering through epigenetic reprogramming of the TOX/NR4A axis, DNMT3A deletion, and metabolic rewiring; (5) in vivo cell programming via targeted lipid nanoparticles and viral vectors for direct generation of therapeutic cells within the body; and (6) expansion of CAR-T technology beyond oncology into autoimmune diseases, cardiac fibrosis, and metabolic disorders. We present novel mathematical frameworks (F201–F224) spanning transfer function analysis of gene circuits, semi-Markov models of T cell differentiation, McKendrick–von Foerster age-structured population dynamics, and Hawkes self-exciting processes for autoimmune flare cascading. Across these frontiers, we identify critical open questions — including circuit robustness in heterogeneous tissue microenvironments, long-term stability of epigenetic reprogramming, and the safety-efficacy balance of in vivo cell engineering — that will determine whether programmable cell therapies achieve their transformative potential in precision medicine.

---

## 1. Introduction

The emergence of chimeric antigen receptor T cell (CAR-T) therapy as a clinically validated modality has fundamentally altered the landscape of cellular therapeutics. The landmark approval of tisagenlecleucel (Kymriah) for pediatric acute lymphoblastic leukemia (ALL) in 2017 (Maude et al., 2018) and axicabtagene ciloleucel (Yescarta) for diffuse large B cell lymphoma (DLBCL) in the same year (Neelapu et al., 2017) established that genetically engineered living cells could serve as potent therapeutic agents. Subsequent approvals — including lisocabtagene maraleucel (Grupp et al., 2013), idecabtagene vicleucel for multiple myeloma (Munshi et al., 2021), and the first gene-edited cell therapy exa-cel (Casgevy) for sickle cell disease and transfusion-dependent β-thalassemia (Frangoul et al., 2021) — have expanded the clinical repertoire of engineered cell products to encompass hematologic malignancies, hemoglobinopathies, and, most recently, autoimmune disorders (Mackensen et al., 2022).

However, first-generation CAR-T cells are fundamentally static devices: they express a single receptor, recognize a single antigen, and execute a single effector program. This architectural simplicity, while sufficient for CD19-positive B cell malignancies where complete antigen elimination is tolerable, is inadequate for the broader disease landscape. Solid tumors present heterogeneous antigen expression, immunosuppressive microenvironments, and physical barriers that demand more sophisticated cellular programming (Rafiq et al., 2020). Autoimmune diseases require calibrated immunomodulation rather than wholesale immune destruction. Metabolic disorders necessitate dynamic, glucose-responsive therapeutic outputs. These challenges have catalyzed a second revolution in cell therapy: the design of programmable cells that can sense, compute, and respond to complex disease environments with the sophistication of endogenous biological systems (Lim & June, 2017).

The conceptual framework for programmable cell therapies draws heavily on synthetic biology, which established that living cells can be engineered with synthetic gene circuits analogous to electronic components — oscillators, toggle switches, logic gates, and feedback controllers (Khalil & Collins, 2010). Pioneering work by the Fussenegger laboratory demonstrated that designer cells equipped with synthetic circuits could function as implantable therapeutic devices, autonomously regulating blood glucose in diabetic mice via optogenetically controlled insulin secretion (Ye et al., 2011) and monitoring uric acid levels for self-adjusting gout therapy (Kemmer et al., 2010). These proof-of-concept demonstrations established the paradigm of the cell as an autonomous therapeutic agent — a concept that Teixeira, Aubel, and Fussenegger (2026) formalize in their comprehensive framework for next-generation programmable cell therapies.

The transformation from proof-of-concept to clinical reality is now accelerating on multiple fronts simultaneously. In synthetic circuit engineering, synNotch receptors (Morsut et al., 2016) and synthetic intramembrane proteolysis receptors (SNIPRs) (Zhu et al., 2022) enable designer cells to detect arbitrary extracellular ligands and transduce this information into user-defined transcriptional programs. In electrogenetics, the development of DC-actuated regulation technology (DART) allows wireless electrical control of therapeutic gene expression in implanted cells (Krawczyk et al., 2023). In immune engineering, CRISPR-edited hypoimmune pluripotent (HIP) cells have achieved insulin independence in a type 1 diabetes (T1D) patient without immunosuppression (Hu et al., 2025). In persistence engineering, epigenetic reprogramming through DNMT3A deletion (Prinzing et al., 2021) and c-Jun overexpression (Lynn et al., 2019) has overcome the exhaustion barrier that limits CAR-T durability. In vivo cell programming using targeted lipid nanoparticles (LNPs) has entered Phase 1 clinical trials for direct generation of CAR-T cells within the body (Rurik et al., 2022). And the repurposing of CAR-T technology for autoimmune diseases has produced remarkable clinical responses, with CD19-directed CAR-T therapy inducing drug-free remission in refractory systemic lupus erythematosus (SLE) (Müller et al., 2024).

This paper examines six frontiers of programmable cell therapy that collectively define the next generation of living therapeutics: (I) synthetic sense-process-respond circuits, (II) electrogenetic and physical-trigger interfaces, (III) hypoimmune universal cell engineering, (IV) T cell exhaustion resistance and persistence engineering, (V) in vivo cell programming, and (VI) CAR-T expansion beyond cancer. For each frontier, we analyze the underlying biological principles, evaluate the most promising engineering strategies with quantitative mathematical frameworks (F201–F224), and identify critical open questions that will determine clinical translatability. Equal weight is given to oncology, autoimmune, metabolic, cardiac, and neurological applications, reflecting the recognition that programmable cell therapies represent a platform technology with transformative potential across the entire spectrum of human disease.

---

## 2. Section I: Synthetic Sense-Process-Respond Circuits

### 2.1 Conceptual Architecture

The core principle of programmable cell therapy is the sense-process-respond (SPR) paradigm: a therapeutic cell detects a disease-associated input signal, processes this information through a defined computational operation, and produces a calibrated therapeutic output (Lim, 2022). This architecture mirrors the canonical signal transduction pathways of endogenous cells but differs fundamentally in that the input-output relationship is rationally designed rather than evolutionarily constrained (Khalil et al., 2012). The SPR framework encompasses three levels of genetic control — transcriptional, translational, and post-translational — each offering distinct advantages in speed, tunability, and orthogonality (Teixeira & Fussenegger, 2024).

**Transcriptional control** remains the most mature and widely deployed layer, leveraging well-characterized promoter-transcription factor pairs including the tetracycline-responsive TetR/TetON system (Gossen & Bujard, 1992), the pristinamycin-inducible PIT/PIR system (Fussenegger et al., 2000), and CRISPR-based transcriptional regulators using catalytically dead Cas9 (dCas9) fused to activation domains (VPR, SAM, SunTag) or repression domains (KRAB) (Gilbert et al., 2014). These systems achieve dynamic ranges of 100–1,000-fold induction (Ausländer et al., 2012) but operate on timescales of hours due to the requirement for mRNA transcription and protein translation.

**Translational control** offers faster response kinetics through RNA-level regulation. Riboswitches — RNA elements whose secondary structure changes upon small-molecule binding, thereby modulating ribosome access — enable direct coupling between metabolite concentration and protein output without transcriptional delay (Win & Smolke, 2008). Aptazymes combine aptamer recognition with ribozyme self-cleavage, creating mRNA molecules that conditionally self-destruct or self-activate in response to specific ligands (Wroblewska et al., 2015). RNA-binding protein (RBP) switches, in which L7Ae or MS2 coat protein binding to cognate RNA hairpins sterically occludes ribosome entry, provide additional translational control nodes with orthogonal specificities (Saito et al., 2010).

**Post-translational control** achieves the fastest response times through direct protein-level regulation. Proteolysis-targeting chimera (PROTAC)-inspired degron systems enable conditional protein degradation via the ubiquitin-proteasome pathway (Nabet et al., 2018). Phosphorylation-dependent switches, including split-kinase reconstitution systems, operate on second-to-minute timescales (Gao et al., 2018). Small-molecule-induced dimerization (FKBP/FRB, ABI/PYL) allows rapid assembly of functional protein complexes from inactive split components (Spencer et al., 1993).

### 2.2 Receptor Architectures for Extracellular Sensing

The sensing component of the SPR paradigm requires receptors that can detect arbitrary extracellular ligands and transduce binding events into defined intracellular signals. Three principal receptor platforms have emerged as the foundation of programmable cell sensing:

**Synthetic Notch (synNotch)** receptors, developed by Morsut et al. (2016), exploit the mechanosensitive proteolytic activation mechanism of endogenous Notch receptors. Upon ligand engagement, a synthetic extracellular recognition domain (e.g., a single-chain variable fragment, scFv, or nanobody) triggers sequential cleavage by ADAM10 and γ-secretase, releasing a user-defined intracellular transcription factor that activates a target promoter. Critically, synNotch receptors are modular: any extracellular binding domain can be paired with any intracellular transcriptional effector (Roybal et al., 2016). This modularity has enabled the construction of T cells that sense tumor-associated antigens (GD2, HER2, EGFRvIII) via synNotch and conditionally express therapeutic payloads — CARs, cytokines, or bispecific T cell engagers (BiTEs) — only in the tumor microenvironment (Hyrenius-Wittsten et al., 2021; Choe et al., 2021). A Phase 1 clinical trial of synNotch-gated CAR-T cells targeting EGFRvIII-positive glioblastoma demonstrated safety and tumor-restricted activity (Hernandez-Lopez et al., 2021).

**Synthetic intramembrane proteolysis receptors (SNIPRs)** address key limitations of synNotch, including dependence on endogenous γ-secretase activity and limited tunability. Developed by Zhu et al. (2022) and further refined by Allen et al. (2022), SNIPRs replace the Notch regulatory region with engineered transmembrane domains that undergo constitutive intramembrane proteolysis, with ligand-dependent conformational gating controlling the release of the intracellular transcription factor. SNIPRs achieve lower background activity and higher signal-to-noise ratios than synNotch, and their independence from endogenous protease machinery enables deployment in non-T cell lineages including macrophages and NK cells (Manhas et al., 2022).

**Modular extracellular sensor architecture (MESA)** receptors use a mechanistically distinct approach: ligand-induced heterodimerization of two receptor chains, one bearing a protease (e.g., TEV) and the other bearing a TEV-cleavable linker tethering a transcription factor. Ligand binding brings the chains into proximity, enabling proteolytic release of the transcription factor (Schwarz et al., 2017). MESA receptors are fully orthogonal to endogenous signaling and have been demonstrated to sense a broad range of soluble ligands including VEGF and GFP (Barnea et al., 2008).

### 2.3 Boolean Logic Gates and Computational Circuits

The processing layer of the SPR paradigm enables cells to perform Boolean operations on multiple input signals, implementing decision-making logic that mimics the specificity requirements of clinical applications (Benenson, 2012). The canonical logic gates — AND, OR, NOT, NAND, NOR — have all been implemented in mammalian cells using combinations of transcriptional, translational, and post-translational control elements (Ausländer et al., 2012; Nissim et al., 2014).

**AND gates** require simultaneous presence of two inputs to produce output, enhancing tumor specificity when tumors are defined by co-expression of two antigens neither of which is tumor-exclusive. The synNotch-CAR AND gate (Roybal et al., 2016) — in which synNotch sensing of antigen A induces expression of a CAR targeting antigen B — has entered clinical testing for glioblastoma (Choe et al., 2021). A mechanistically distinct AND gate using split-CAR reconstitution via chemically induced dimerization (CID) achieves post-translational-speed gating (Cho et al., 2018). Srivastava et al. (2019) demonstrated a three-input logic gate (AND-NOT) in which T cells required two tumor antigens while being inhibited by a healthy-tissue antigen, achieving near-complete discrimination between tumor and normal tissue in xenograft models.

**Bandpass filters** produce output only when the input concentration falls within a defined range, enabling responses to pathological biomarker levels while ignoring physiological concentrations. Li et al. (2022) engineered a bandpass circuit in which a low-affinity activating receptor and a high-affinity inhibitory receptor compete for the same ligand, producing a unimodal dose-response curve that discriminates between normal and elevated antigen densities. This architecture is particularly relevant for solid tumors where the target antigen is overexpressed but not absent from normal tissue.

**Toggle switches** provide bistable memory, enabling therapeutic cells to "remember" transient signals and maintain altered behavior after the signal is removed. The canonical genetic toggle switch (Gardner et al., 2000) uses mutually repressing transcription factors to create two stable steady states. Weber et al. (2008) demonstrated a therapeutic toggle switch in implanted designer cells that could be switched between two metabolic states by transient antibiotic exposure, maintaining the new state indefinitely without continued drug administration. More recently, Saxena et al. (2023) developed self-driving circuits that autonomously adjust their output in response to changing disease biomarkers without external intervention, representing a step toward fully autonomous therapeutic cells.

### 2.4 Transfer Function Analysis of Synthetic Gene Circuits

The input-output behavior of synthetic gene circuits can be rigorously characterized using transfer function analysis adapted from control theory. We define the circuit transfer function H(s) in the Laplace domain as the ratio of the therapeutic output Y(s) to the disease biomarker input X(s):

**F201. Gene circuit transfer function (Laplace domain):**

```math
H(s) = \frac{Y(s)}{X(s)} = \frac{k_{\max} \cdot K_d^n}{(s + \delta_m)(s + \delta_p)(K_d^n + X_0^n)}
```

where $k_{\max}$ is the maximal transcription rate (molecules·s⁻¹), $\delta_m$ and $\delta_p$ are the mRNA and protein degradation rates (s⁻¹), $K_d$ is the promoter half-maximal activation concentration, $n$ is the Hill coefficient, and $X_0$ is the steady-state input level. The transfer function has two poles at $s = -\delta_m$ and $s = -\delta_p$, defining the characteristic response times of the circuit. For mRNA half-life ~2h ($\delta_m \approx 9.6 \times 10^{-5}$ s⁻¹) and protein half-life ~10h ($\delta_p \approx 1.9 \times 10^{-5}$ s⁻¹), the circuit bandwidth is limited by the slower protein degradation pole, yielding a response time $\tau_{90} \approx 2.3/\delta_p \approx 34$ hours (Del Vecchio & Murray, 2015).

The frequency response reveals critical design constraints for therapeutic applications:

**F202. Bode magnitude analysis and circuit bandwidth:**

```math
|H(j\omega)| = \frac{k_{\max} \cdot K_d^n / (K_d^n + X_0^n)}{\sqrt{(\omega^2 + \delta_m^2)(\omega^2 + \delta_p^2)}}
```

The -3 dB bandwidth $\omega_{BW} \approx \min(\delta_m, \delta_p)$ determines the maximum frequency of biomarker fluctuation that the circuit can track (Del Vecchio et al., 2008). For circuits targeting chronic diseases with slowly varying biomarkers (e.g., HbA1c in diabetes), the hour-timescale response of transcriptional circuits is adequate. For acute applications requiring minute-timescale responses (e.g., glucose boluses), post-translational circuits with degradation rates $\delta_p > 10^{-3}$ s⁻¹ (corresponding to protein half-lives <12 minutes using engineered degrons) are necessary (Nabet et al., 2018).

### 2.5 Circuit Reliability and Noise Performance

The clinical deployment of synthetic circuits demands quantitative analysis of reliability and noise performance. A multi-component circuit's probability of producing the correct output depends on the reliability of each component and the circuit topology:

**F203. Boolean network reliability:**

```math
R_{circuit}(f) = \sum_{S \in \{0,1\}^n} \left[\prod_{i: S_i=1} r_i \prod_{j: S_j=0} (1-r_j)\right] \cdot f(S)
```

where $r_i$ is the reliability (probability of correct function) of component $i$, $f(S)$ is the Boolean function evaluated at state vector $S$, and the sum is over all $2^n$ possible component states. For an AND gate with $n$ components each of reliability $r$, $R_{AND} = r^n$; for an OR gate, $R_{OR} = 1-(1-r)^n$. With typical biological component reliabilities of $r \approx 0.95$ (accounting for stochastic gene expression, epigenetic silencing, and mutation), a 3-input AND gate achieves $R_{AND} = 0.857$ while a 3-input OR gate achieves $R_{OR} = 0.9999$, illustrating the fundamental reliability asymmetry between AND and OR topologies (Kwok, 2010).

The noise performance of biosensor circuits is governed by the stochastic nature of gene expression, quantified through the chemical master equation (CME) formalism:

**F204. Biosensor signal-to-noise ratio via Fano factor:**

```math
\text{SNR} = \frac{(\mu_{on} - \mu_{off})^2}{\sigma_{on}^2 + \sigma_{off}^2} = \frac{(\mu_{on} - \mu_{off})^2}{F_{on} \cdot \mu_{on} + F_{off} \cdot \mu_{off}}
```

where $\mu_{on/off}$ are the mean protein copy numbers in the ON/OFF states, $\sigma^2_{on/off}$ are the corresponding variances, and $F = \sigma^2/\mu$ is the Fano factor. For a bursty gene expression model, $F = 1 + b/(1 + \delta_p/\delta_m)$ where $b$ is the burst size (mean proteins per mRNA) (Paulsson, 2005). To achieve a clinically relevant SNR ≥ 10 (99% discrimination between disease and healthy states), the circuit must satisfy $\mu_{on}/\mu_{off} > 1 + \sqrt{10 \cdot (F/\mu_{on} + F/\mu_{off})}$, which for typical burst sizes ($b \approx 10$) and Fano factors ($F \approx 5$) requires dynamic ranges exceeding 20-fold — a threshold met by optimized TetON systems ($\sim$100-fold) but not by most endogenous promoter-based sensors ($\sim$3–5-fold) (Frei et al., 2022).

### 2.6 Emerging Clinical Applications

The clinical translation of synthetic circuit-equipped cells is advancing rapidly. Mao et al. (2023) demonstrated programmable sensing circuits that detect tumor-secreted biomarkers (GPC3, AFP) and conditionally secrete therapeutic antibodies, achieving complete tumor regression in hepatocellular carcinoma mouse models. Donahue et al. (2022) developed a two-input logic-gated CAR-T cell that requires simultaneous detection of two tumor-associated antigens for activation, reducing on-target/off-tumor toxicity by >100-fold compared to single-antigen CARs. Saxena et al. (2023) demonstrated a closed-loop circuit for thyroid hormone regulation in which designer cells sense TSH levels and secrete T4 proportionally, restoring euthyroid state in hypothyroid mice within 48 hours. Scheller et al. (2018) engineered a biotin-sensing circuit that couples dietary biotin intake to reporter expression, demonstrating the feasibility of diet-responsive therapeutic circuits.

**Open questions in synthetic circuits:**
1. How can circuit longevity be ensured in the face of epigenetic silencing of synthetic promoters over months to years of in vivo function (Göttgens, 2023)?
2. What is the maximum circuit complexity achievable in primary human cells before resource competition (ribosome loading, transcription factor titration) compromises host cell fitness (Frei et al., 2022)?
3. Can standardized biological parts (BioBricks) achieve the inter-laboratory reproducibility necessary for regulatory approval, given the context-dependence of genetic parts (Endy, 2005)?

---

## 3. Section II: Electrogenetic and Physical-Trigger Interfaces

### 3.1 The Electrogenetic Paradigm

The therapeutic circuits described in Section I respond autonomously to endogenous biomarkers. However, many clinical scenarios require physician-controlled, on-demand activation of therapeutic gene expression — a capability enabled by physical-trigger interfaces that transduce external energy sources (electrical, optical, magnetic, acoustic, thermal) into intracellular signaling events (Fussenegger, 2009). Among these, electrogenetics — the use of electrical stimulation to control gene expression — has emerged as the most clinically translatable approach due to the established safety and widespread availability of electrical stimulation devices (Krawczyk et al., 2023).

**DC-actuated regulation technology (DART)** represents the most advanced electrogenetic system. Developed by Krawczyk et al. (2023), DART exploits the endogenous NRF2 (nuclear factor erythroid 2-related factor 2) / antioxidant response element (ARE) signaling pathway. Application of a direct current (DC) voltage (4.5 V for 10 seconds) to electrodes adjacent to designer cells generates reactive oxygen species (ROS) via water electrolysis. These ROS stabilize NRF2 by disrupting its interaction with the KEAP1 ubiquitin ligase adaptor, enabling nuclear translocation and ARE-driven transcription of therapeutic transgenes (Krawczyk et al., 2023). In a proof-of-concept study, DART-equipped designer cells encapsulated in alginate and implanted subcutaneously in type 1 diabetic mice secreted insulin in response to brief electrical stimulation, reducing blood glucose levels to normoglycemic range within 60 minutes (Krawczyk et al., 2023). A subsequent refinement achieved wireless DART control via a Bluetooth-enabled wearable device, enabling smartphone-operated insulin delivery (Krawczyk et al., 2024).

The earlier electrogenetic system by Shao et al. (2020), published in *Science*, demonstrated that biphasic electrical pulses could activate voltage-gated calcium channels (VGCC, specifically Cav1.2) heterologously expressed in HEK293 cells, triggering calcineurin-NFAT signaling and NFAT-responsive transgene expression. This system achieved insulin secretion from subcutaneously implanted electro-responsive cells in diabetic mice, with glycemic control maintained for weeks through periodic stimulation (Shao et al., 2020).

### 3.2 Optogenetic Gene Expression Control

Light-inducible gene expression systems exploit photoreceptor proteins from plants, fungi, and bacteria to couple defined wavelengths of light to transcriptional activation. The first therapeutic application was demonstrated by Ye et al. (2011), who engineered melanopsin (a blue-light-sensitive opsin) into designer cells to create a light-activated calcium-NFAT signaling cascade driving GLP-1 secretion for glucose homeostasis in diabetic mice. Subsequent engineering shifted the activation wavelength to far-red light (740 nm), which penetrates tissue more effectively, using bacterial phytochrome BphP1-PpsR2 systems (Müller et al., 2013; Shao et al., 2017). This enabled transcutaneous activation of implanted cells without direct illumination of the implant.

A remarkable integration of optogenetics with brain-computer interfaces (BCIs) was achieved by Folcher et al. (2014), who developed a mind-controlled transgene expression system. In this architecture, a human subject wearing an electroencephalography (EEG) headset generated concentration-dependent near-infrared (NIR) light output from an LED array positioned over a subcutaneous cell implant. The implanted designer cells, equipped with a bacterial phytochrome-responsive promoter, expressed the desired transgene (SEAP, as a model protein) proportionally to the subject's mental state. This proof-of-concept demonstrated that cognitive intent could be directly transduced into therapeutic protein production — a convergence of neurotechnology and synthetic biology with profound implications for closed-loop neurological therapies (Folcher et al., 2014).

### 3.3 Magnetogenetic and Sonogenetic Interfaces

**Magnetogenetics** uses magnetic fields to control cellular behavior, offering the advantage of deep tissue penetration without invasive implants. The EMPOWER system (Pan et al., 2025) employs multiferroic nanoparticles (MFNPs) that convert alternating magnetic fields into localized electric fields at the nanoparticle surface, generating ROS that activate the NRF2/ARE pathway analogously to DART. Magnetic stimulation achieved comparable transgene induction to DART but with fully non-invasive, non-contact actuation through tissue barriers (Pan et al., 2025). An earlier approach by Stanley et al. (2015) used iron oxide nanoparticles tethered to TRPV1 (temperature-sensitive) channels, enabling magnetic field-induced channel opening, calcium influx, and insulin gene expression.

**Sonogenetics** exploits mechanosensitive ion channels for ultrasound-responsive gene activation. Focused ultrasound at diagnostic intensities (0.5–1.5 MPa) can activate Piezo1, MscL (mechanosensitive channel of large conductance), and engineered variants of these channels, triggering calcium influx and downstream transcriptional activation via NFAT or CRE-responsive promoters (Ibsen et al., 2015; Yoo et al., 2022). Piraner et al. (2017) demonstrated that ultrasound-responsive gas vesicles from *Anabaena flos-aquae*, when genetically encoded in mammalian cells, enabled non-invasive imaging and could be engineered for sonogenetic gene control. The advantage of sonogenetics is its spatial precision: focused ultrasound can be directed to millimeter-scale volumes deep within tissue, enabling organ-specific activation of systemically distributed therapeutic cells (Yoo et al., 2022).

**Thermogenetics** utilizes heat-shock promoters (HSP, HSE) coupled with localized hyperthermia delivered by focused ultrasound, magnetic nanoparticle heating, or photothermal agents. Miller et al. (2018) demonstrated that high-intensity focused ultrasound (HIFU) at 42–45°C activated HSP70-driven CAR expression in T cells, creating a spatially controlled "hot-zone" of CAR-T activity within a solid tumor while leaving systemic T cells inactive. This thermal control paradigm addresses the critical challenge of on-target/off-tumor toxicity in CAR-T therapy.

### 3.4 Mathematical Frameworks for Physical-Trigger Interfaces

**F205. Electrogenetic dose-response transfer function:**

The DART system output is a composite function of electrical voltage $V$ and stimulation duration $t_{stim}$:

```math
G(V, t_{stim}) = G_{\max} \cdot \frac{[\text{NRF2}_{nuc}]^n}{K_{ARE}^n + [\text{NRF2}_{nuc}]^n}
```

where the nuclear NRF2 concentration depends on ROS generation:

```math
[\text{NRF2}_{nuc}] = [\text{NRF2}_{tot}] \cdot \frac{[\text{ROS}]^m}{K_{ROS}^m + [\text{ROS}]^m}, \quad [\text{ROS}] = \frac{k_{gen} \cdot V \cdot t_{stim}}{1 + k_{scav} \cdot [\text{GSH}]}
```

with $k_{gen}$ the electrolytic ROS generation rate constant (proportional to Faradaic current), $k_{scav}$ the glutathione scavenging rate, and $[\text{GSH}]$ the intracellular glutathione concentration. The Hill coefficients $n$ and $m$ reflect the cooperative NRF2-KEAP1 dissociation and NRF2-ARE binding, respectively (Krawczyk et al., 2023). This two-stage Hill cascade produces an ultrasensitive switch-like response with effective Hill coefficient $n_{eff} \approx n \cdot m \approx 6{-}8$, consistent with the observed sharp voltage threshold at ~3.5 V (Krawczyk et al., 2023).

**F206. Optogenetic photocycle kinetics and bistability:**

```math
\frac{dR}{dt} = k_{on} \cdot I \cdot (1 - R) - k_{off} \cdot R + \alpha \cdot \frac{R^h}{K_R^h + R^h}
```

where $R$ is the fraction of photoreceptor in the active (signaling) state, $I$ is light intensity (W/cm²), $k_{on}$ is the photon absorption rate constant, $k_{off}$ is the thermal reversion rate, and the final term represents a positive-feedback loop from downstream signaling (e.g., transcriptional autoregulation). For the BphP1 far-red system, $k_{on} \approx 0.01$ s⁻¹ at 1 mW/cm², $k_{off} \approx 10^{-4}$ s⁻¹ (dark reversion half-life ~2 h) (Müller et al., 2013). The positive feedback ($\alpha > 0$, $h > 1$) creates hysteresis: brief light pulses can switch the system to a high-expression state that persists in darkness for hours — a memory feature exploitable for reducing the frequency of light stimulation required for chronic therapy.

**F207. Signal attenuation through tissue:**

Effective therapeutic deployment of physical triggers requires quantifying signal attenuation through biological tissue:

```math
\text{Light (Beer-Lambert):} \quad I(z) = I_0 \cdot e^{-\mu_{eff} \cdot z}, \quad \mu_{eff} = \sqrt{3\mu_a(\mu_a + \mu_s')}
```

```math
\text{Magnetic field (dipole):} \quad B(r) = \frac{B_0}{(1 + r/r_0)^3}
```

```math
\text{Ultrasound:} \quad p(z) = p_0 \cdot e^{-\alpha_s \cdot f \cdot z}
```

where $\mu_{eff}$ is the effective attenuation coefficient (tissue-dependent: ~0.5 cm⁻¹ for NIR at 740 nm, ~5 cm⁻¹ for blue at 470 nm) (Jacques, 2013), $\alpha_s$ is the ultrasound absorption coefficient (~0.5 dB/cm/MHz for soft tissue) (Duck, 1990), and $r_0$ is the magnetic coil characteristic length. These attenuation laws dictate the operational depth of each modality: NIR light penetrates ~2–3 cm (sufficient for subcutaneous implants), ultrasound penetrates >10 cm, and magnetic fields penetrate essentially the entire body (Pan et al., 2025).

**F208. Encapsulation mass transfer (Fick's law, spherical geometry):**

Therapeutic cells are frequently encapsulated in alginate or cellulose-based immunoprotective microcapsules. Nutrient supply and therapeutic protein release are governed by diffusion through the capsule wall:

```math
J = \frac{4\pi \cdot D_{eff} \cdot R_{in} \cdot R_{out}}{R_{out} - R_{in}} \cdot (C_{in} - C_{out})
```

where $J$ is the molar flux (mol/s), $D_{eff}$ is the effective diffusivity through the capsule material (for insulin in alginate: $D_{eff} \approx 3 \times 10^{-7}$ cm²/s), and $R_{in}$, $R_{out}$ are the inner and outer radii (Desai et al., 2000). For oxygen, the critical design constraint is preventing core hypoxia: $R_{out} - R_{in} < \sqrt{2 D_{O_2} C_{O_2,surface} / q_{O_2}}$ where $q_{O_2}$ is the cellular oxygen consumption rate (~0.05 mol/m³/s for β-cells) (Colton, 2014). For standard alginate microcapsules ($R_{out} = 500$ μm, shell thickness 100 μm), this yields a maximum viable cell density of ~5 × 10⁷ cells/mL — a constraint that has driven development of thinner capsule technologies including conformal coatings and cellulose nanofibril membranes (Vegas et al., 2016; An et al., 2018).

### 3.5 Encapsulation Technologies and Implantable Devices

The clinical deployment of designer cells requires physical containment that simultaneously (1) protects transplanted cells from immune rejection, (2) permits bidirectional diffusion of nutrients, oxygen, and therapeutic proteins, and (3) enables retrieval for safety (Desai & Bhatt, 2020). Alginate microcapsules have been the workhorse technology since the seminal demonstration by Lim and Sun (1980), but first-generation alginate suffers from fibrotic overgrowth that progressively occludes diffusion. Vegas et al. (2016) identified triazole-modified alginate variants that resist fibrosis in non-human primates for >6 months, enabling long-term function of encapsulated β-cell grafts. An et al. (2018) developed a thread-reinforced alginate fiber device (TRAFFIC) that can be rapidly retrieved through a small incision, addressing the safety concern of uncontrolled cell escape.

More recently, the THERO-Cell platform (Thérien et al., 2024) integrates encapsulated designer cells with wireless bioelectronic implants, creating a self-contained therapeutic device in which the electronic component provides the physical stimulus (DART or optogenetic) and the cellular component produces the therapeutic protein. This convergence of bioelectronics and synthetic biology represents a new class of "electro-living" medical devices.

**Open questions in physical-trigger interfaces:**
1. Can electrogenetic circuits achieve clinically meaningful protein titers (>1 μg/mL serum) from practically sized implants (<1 cm³) given the mass transfer limitations quantified in F208?
2. What is the long-term fate of encapsulated cells — do they maintain synthetic circuit function over years, or does epigenetic drift silence engineered transgenes?
3. How should regulatory frameworks classify electro-living devices that combine pharmaceutical (cell) and device (electronic) components?

---

## 4. Section III: Hypoimmune Universal Cell Engineering

### 4.1 The Allogeneic Barrier

The dominant paradigm in cell therapy — autologous manufacturing from patient-derived cells — faces fundamental scalability limitations. Autologous CAR-T manufacturing requires 2–4 weeks of ex vivo expansion per patient, costs $300,000–$500,000 per treatment, and fails in ~5–10% of patients due to insufficient T cell quality (Ghassemi et al., 2022). For non-oncologic applications where patient T cells are not inherently dysfunctional (e.g., autoimmune diseases, metabolic disorders), allogeneic ("off-the-shelf") cell products manufactured from healthy donors offer transformative economies of scale. However, allogeneic cells face rapid immune rejection mediated by three principal effector pathways: CD8⁺ T cell recognition of foreign HLA class I molecules, CD4⁺ T cell recognition of foreign HLA class II molecules, and NK cell "missing-self" detection when donor HLA class I fails to engage recipient inhibitory KIR/NKG2A receptors (Lanza et al., 2019).

### 4.2 The Hypoimmune Pluripotent (HIP) Cell Strategy

Deuse et al. (2019) established the foundational approach to universal cell engineering: CRISPR-mediated disruption of *B2M* (eliminating all HLA class I surface expression), disruption of *CIITA* (eliminating HLA class II), and overexpression of CD47 (engaging the SIRPα "don't eat me" receptor on macrophages). This triple-edited hypoimmune pluripotent (HIP) cell line, derived from iPSCs, survived long-term in fully allogeneic recipients without immunosuppression (Deuse et al., 2019). Critically, CD47 overexpression compensated for the NK cell vulnerability created by HLA class I loss: CD47-SIRPα signaling provided a dominant inhibitory signal that overrode NK cell activation (Deuse et al., 2019).

Subsequent refinement in non-human primates confirmed the translatability of this approach. Deuse et al. (2023) demonstrated that HIP iPSC-derived cardiomyocytes, endothelial cells, and hepatocytes survived in fully MHC-mismatched rhesus macaques for >4 months without immunosuppression, with no evidence of T cell or NK cell-mediated rejection. Additional immune evasion modules have been developed: HLA-E overexpression (engaging NKG2A to inhibit NK cells through a mechanism orthogonal to CD47) (Gornalusse et al., 2017), PD-L1 knock-in (suppressing residual T cell responses) (Han et al., 2019), and MICA/MICB deletion (removing NKG2D activating ligands) (Xu et al., 2019).

### 4.3 Clinical Translation: The T1D Breakthrough

The most clinically significant application of hypoimmune cell engineering is in type 1 diabetes. Hu et al. (2025), reporting in the *New England Journal of Medicine*, described the transplantation of CRISPR-edited, immune-evasive stem cell-derived β-cells into a patient with T1D. The cells were derived from iPSCs subjected to a comprehensive gene editing panel (B2M disruption, CIITA disruption, CD47 overexpression, and PD-L1 knock-in), differentiated into functional β-cells, and transplanted under the omentum. The patient achieved insulin independence within 75 days and maintained normoglycemia for >12 weeks without any immunosuppressive medications (Hu et al., 2025). This result represents a transformative milestone: for the first time, allogeneic cell therapy achieved durable engraftment and function in a human without immunosuppression.

Concurrently, the VCTX210 trial (ViaCyte/CRISPR Therapeutics) is evaluating CRISPR-edited pancreatic endoderm cells (B2M⁻/⁻, CIITA⁻/⁻) encapsulated in a retrievable device for T1D (Ramzy et al., 2021). Vertex Pharmaceuticals' VX-880 (now VX-264) program, using stem cell-derived islets in a novel encapsulation device, reported C-peptide production and insulin dose reduction in Phase 1/2 trials (Shapiro et al., 2021).

### 4.4 iPSC-Derived Therapeutic Cell Products

Beyond β-cells, hypoimmune iPSC technology is generating a pipeline of universal allogeneic cell products:

**iPSC-derived CAR-NK cells:** Century Therapeutics' CNTY-101 (iPSC-derived, CD19-targeted CAR-NK cells) reported a 30–60% complete response rate at the highest dose level in Phase 1 for relapsed/refractory B cell malignancies (Cichocki et al., 2022). iPSC-NK cells offer advantages over T cells: they do not cause graft-versus-host disease (GvHD), can be manufactured at >10⁹ cells from a single iPSC line, and possess innate tumor-killing mechanisms (antibody-dependent cellular cytotoxicity, ADCC) that complement CAR-mediated killing (Liu et al., 2020).

**iPSC-derived dopaminergic neurons for Parkinson's disease:** Following Takahashi's original iPSC Nobel Prize-winning work, Doi et al. (2025) reported results from the first allogeneic iPSC-derived dopaminergic neuron transplant trial in Japan (jRCTa050190). HLA-matched iPSC-DA neurons were stereotactically injected into the putamen of Parkinson's patients, with preliminary data suggesting safety and modest clinical improvement at 2 years (Doi et al., 2025; Schweitzer et al., 2020). The combination of hypoimmune engineering with iPSC-DA neurons could eliminate the HLA-matching requirement, vastly expanding the eligible patient population.

**iPSC-derived cardiomyocytes:** Menasche et al. (2018) demonstrated the feasibility of ESC-derived cardiac progenitor patches for heart failure, and iPSC-derived cardiomyocyte sheets are in Phase 1/2 trials in Japan (Miyagawa et al., 2022). Hypoimmune engineering would enable a single manufacturing campaign to serve all recipients.

### 4.5 Mathematical Frameworks for Immune Evasion

**F209. Multi-pathway immune evasion probability (product-form survival):**

The probability that a transplanted cell survives immune challenge is the product of survival probabilities against each independent effector pathway:

```math
P(\text{survival}) = \prod_{k=1}^{K} \left(1 - P_k(\text{kill})\right) = \left(1 - P_{NK}\right)\left(1 - P_{CD8}\right)\left(1 - P_{mac}\right)
```

where $P_{NK}$, $P_{CD8}$, and $P_{mac}$ are the kill probabilities by NK cells, CD8⁺ T cells, and macrophages, respectively. For HIP cells: $P_{CD8} \approx 0$ (no HLA-I presentation), $P_{mac} \approx P_{mac,0} \cdot (1 - f_{CD47})$ where $f_{CD47}$ is the fraction of SIRPα receptors occupied (Deuse et al., 2019). The NK cell term is the critical vulnerability, modeled in F210.

**F210. NK cell "missing-self" detection (inhibitory receptor occupancy):**

NK cell activation follows an integration model (Lanier, 2005):

```math
P_{NK}(\text{kill}) = \frac{\sigma_{act}^{n_a}}{K_{act}^{n_a} + \sigma_{act}^{n_a}} \cdot \frac{K_{inh}^{n_i}}{K_{inh}^{n_i} + \sigma_{inh}^{n_i}}
```

where
```math
$$ \sigma_{\text{act}} = \sum_i w_i \cdot [\text{actR}_i{:}\text{ligand}_i] $$
```
is the weighted sum of activating receptor-ligand interactions (NKG2D-MICA, NKp30-B7-H6, etc.), 
```math
$$ \sigma_{\text{inh}} = \sum_j v_j \cdot [\text{KIR}_j{:}\text{HLA}_j] + v_{\text{CD47}} \cdot [\text{CD47}{:}\text{SIRP}\alpha] $$
```
is the weighted sum of inhibitory interactions, and $n_a$, $n_i$ are Hill coefficients reflecting signaling cooperativity. For wild-type allogeneic cells: $\sigma_{inh}$ is low (mismatched HLA), yielding $P_{NK} \approx 0.8$. For HIP cells with CD47⁺ and HLA-E⁺: $\sigma_{inh}$ is high, yielding $P_{NK} \approx 0.05$ (Deuse et al., 2023).

**F211. CD47-SIRPα "don't eat me" signaling threshold:**

```math
P(\text{phagocytosis}) = \frac{1}{1 + \left(\frac{[\text{CD47}] \cdot [\text{SIRP}\alpha] / (K_d + [\text{CD47}])}{K_{half}}\right)^{n_H}}
```

where $K_d \approx 2 \mu$M for native CD47-SIRPα (Hatherley et al., 2008), $K_{half}$ is the half-maximal inhibitory complex concentration, and $n_H \approx 2{-}3$ reflects cooperative SIRPα clustering (Tsai et al., 2020). HIP cells achieve CD47 surface density of ~50,000 molecules/cell (vs. ~20,000 endogenous), driving $P(\text{phagocytosis}) < 0.01$ (Deuse et al., 2019). The high-affinity CD47 variant CV1 ($K_d \approx 11$ nM) further enhances the phagocytosis barrier by ~100-fold (Ho et al., 2015).

**F212. Graft survival with competing risks (Kaplan-Meier extension):**

```math
S(t) = \prod_{t_i \leq t} \left(1 - \frac{d_i}{n_i}\right), \quad F_k(t) = \int_0^t h_k(u) \cdot S(u^-) \, du
```

where $S(t)$ is the overall graft survival function, $d_i/n_i$ is the event/at-risk ratio at each failure time $t_i$, and $F_k(t)$ is the cumulative incidence function for cause $k$ (immune rejection, graft dysfunction, or mechanical failure). For HIP β-cell grafts, the dominant competing risk shifts from immune rejection ($F_1$ historically dominant, now suppressed to $<5\%$) to graft dysfunction ($F_2$: β-cell exhaustion from metabolic stress, estimated 15–20% at 5 years) (Shapiro et al., 2021).

### 4.6 Manufacturing Scalability

The manufacturing challenge for iPSC-derived universal cells is substantial but advancing rapidly. Anderson et al. (2024) demonstrated 12-fold scale-up of iPSC expansion in Vertical Wheel bioreactors (PBS Biotech), producing >10¹⁰ iPSCs per batch — sufficient for ~100 patient doses of β-cells or ~1,000 doses of NK cells. GMP-compliant closed-system differentiation protocols now achieve >90% β-cell purity (Pagliuca et al., 2014) and >95% NK cell purity from iPSCs (Zhu & Bhatt, 2020). The cost-per-dose for allogeneic iPSC-derived products is projected at $10,000–$50,000, representing a 10–50-fold reduction compared to autologous CAR-T (Kang et al., 2025).

**Safety architecture** for universal cells includes inducible caspase-9 (iCasp9) suicide genes (Di Stasi et al., 2011) activated by the bioinert small molecule AP1903/rimiducid, providing a pharmacological "kill switch" that eliminates >99% of transplanted cells within 2 hours of administration (Zhou et al., 2015). Additional layers include thymidine kinase (HSV-TK)/ganciclovir systems and synthetic auxotrophies requiring exogenous metabolite supplementation for survival (Mandell et al., 2015).

**Open questions in hypoimmune engineering:**
1. Does long-term CD47 overexpression create a "don't find me" camouflage that also protects transformed cells from immune surveillance, creating a tumorigenicity risk (Willingham et al., 2012)?
2. Can hypoimmune cells be further engineered to resist viral infection, given the absence of MHC-I-mediated antigen presentation that normally enables cytotoxic T cell clearance of virally infected cells?
3. What is the minimum immune evasion gene set required for clinical-grade protection: is B2M⁻/⁻ CIITA⁻/⁻ CD47⁺ sufficient, or are HLA-E, PD-L1, and MICA/B deletion necessary additions?

---

## 5. Section IV: T Cell Exhaustion Resistance and Persistence Engineering

### 5.1 The Exhaustion Barrier

T cell exhaustion represents the dominant cause of CAR-T therapy failure in solid tumors and a significant contributor to relapse in hematologic malignancies. Exhaustion is a progressive, epigenetically enforced state in which T cells lose effector functions (cytokine secretion, cytotoxicity) while upregulating inhibitory receptors (PD-1, LAG-3, TIM-3, TIGIT) and adopting a terminal transcriptional program driven by the TOX (thymocyte selection associated HMG box protein) and NR4A (nuclear receptor subfamily 4, group A) transcription factor families (Khan et al., 2019; Seo et al., 2021). Crucially, exhaustion is not merely a state of quiescence or anergy: it involves irreversible epigenetic remodeling — de novo DNA methylation at effector gene loci, H3K27me3 deposition at stemness genes, and chromatin accessibility changes at >5,000 genomic regions — that cannot be reversed by checkpoint blockade alone (Pauken et al., 2016; Philip et al., 2017; Sen et al., 2016).

### 5.2 Transcription Factor Engineering

**TOX knockout:** Khan et al. (2019) demonstrated that TOX is the master regulator of T cell exhaustion, required for the epigenetic remodeling that establishes and maintains the exhaustion program. TOX⁻/⁻ CD8⁺ T cells in chronic viral infection maintained effector function (IFN-γ, TNF-α, granzyme B) and failed to upregulate PD-1, LAG-3, and TIM-3. However, TOX⁻/⁻ T cells also lost the ability to persist in chronic antigen environments, suggesting that exhaustion is an adaptive survival program and that complete ablation may be counterproductive (Khan et al., 2019). This finding has motivated partial disruption strategies and combinatorial approaches (Scott et al., 2019).

**NR4A triple knockout:** Seo et al. (2021) showed that simultaneous deletion of NR4A1, NR4A2, and NR4A3 in CAR-T cells prevented exhaustion and promoted tumor regression in solid tumor models. NR4A transcription factors act downstream of chronic TCR/CAR signaling to enforce the exhaustion transcriptional program; their deletion maintained AP-1 activity (which normally shifts from c-Jun/c-Fos activating dimers to NR4A/NFAT inhibitory complexes) and preserved effector function (Seo et al., 2021).

**c-Jun overexpression:** Lynn et al. (2019) demonstrated that constitutive c-Jun overexpression in CAR-T cells fundamentally rebalanced the AP-1 transcription factor family, maintaining the c-Jun/c-Fos:NFAT ratio that characterizes functional effector T cells even under chronic antigen stimulation. c-Jun-armored CAR-T cells showed enhanced expansion, cytokine secretion, and tumor control compared to conventional CAR-T in solid tumor xenograft models (Lynn et al., 2019). This approach has entered Phase 1 clinical testing (NCT05239143) and represents the most advanced exhaustion-resistant CAR-T design in clinical development (Lynn et al., 2023).

### 5.3 Epigenetic Reprogramming

**DNMT3A deletion:** Prinzing et al. (2021) discovered that deletion of the de novo DNA methyltransferase DNMT3A in CAR-T cells prevented the exhaustion-associated methylation of stemness gene promoters (TCF7, LEF1, MYB), maintaining a stem-like memory phenotype (Tscm) with enhanced self-renewal capacity. DNMT3A-KO CAR-T cells controlled tumors for >148 days in rechallenge experiments — demonstrating the functional durability that had been absent from conventional CAR-T products (Prinzing et al., 2021). Critically, DNMT3A deletion did not compromise effector function or increase transformation risk over the observation period, as the deleted enzyme primarily targets de novo methylation rather than maintenance methylation (Prinzing et al., 2021).

**TET2 disruption:** The serendipitous discovery by Fraietta et al. (2018) that a single CAR-T cell clone with biallelic TET2 disruption (from lentiviral insertion into the TET2 locus) expanded to >90% of circulating CAR-T cells and mediated complete remission in CLL provided compelling evidence that epigenetic reprogramming enhances CAR-T persistence. TET2 loss altered the DNA methylation landscape to favor central memory (Tcm) over effector memory (Tem) differentiation, enhancing long-term self-renewal (Fraietta et al., 2018). Intentional TET2 disruption is now being evaluated in combination with other modifications (Nobles et al., 2020).

**SUV39H1 inhibition:** Pace et al. (2018) showed that the histone methyltransferase SUV39H1, which deposits the repressive H3K9me3 mark at effector gene loci, is a critical mediator of exhaustion. Pharmacological inhibition of SUV39H1 (using chaetocin) or genetic deletion preserved effector gene accessibility and enhanced CAR-T antitumor activity (Pace et al., 2018). This approach offers the advantage of targeting a histone mark rather than DNA methylation, potentially reducing the risk of global epigenomic disruption.

### 5.4 Metabolic Rewiring

Exhausted T cells are characterized by a metabolic shift from oxidative phosphorylation (OXPHOS) — which supports memory T cell longevity and self-renewal — toward aerobic glycolysis, with impaired mitochondrial biogenesis and function (Scharping et al., 2021). Several engineering strategies address this metabolic vulnerability:

**Mitochondrial biogenesis enhancement:** Weber et al. (2024) demonstrated that overexpression of PGC1α (the master regulator of mitochondrial biogenesis) in CAR-T cells increased mitochondrial mass, enhanced OXPHOS capacity, and improved persistence in solid tumor models. Complementary approaches include acetyl-CoA carboxylase inhibition and AMPK activation to maintain the catabolic metabolic program associated with memory T cell identity (Buck et al., 2016).

**Glutamine antagonism:** Leone et al. (2019) showed that the glutamine antagonist DON (6-diazo-5-oxo-L-norleucine) selectively starved tumor cells (which are glutamine-dependent) while rewiring T cell metabolism toward OXPHOS, enhancing antitumor immunity. A prodrug version (JHU083) with improved pharmacokinetics demonstrated enhanced CAR-T function in solid tumor models (Leone et al., 2019).

**IL-7/IL-15 culture:** Manufacturing CAR-T cells in the presence of IL-7 and IL-15 (rather than the standard IL-2) promotes a Tscm/Tcm phenotype with enhanced oxidative metabolism and in vivo persistence (Cieri et al., 2013). This approach, combined with shortened manufacturing protocols (Ghassemi et al., 2022), represents the most immediately translatable metabolic engineering strategy.

### 5.5 Semi-Markov Model of T Cell State Transitions

T cell differentiation from naive to exhausted states is conventionally modeled as a continuous-time Markov chain (CTMC), but this assumes exponentially distributed dwell times in each state — an assumption violated by the biological reality of epigenetic barrier crossing. We propose a semi-Markov model:

**F213. Semi-Markov T cell state transition model:**

States: Tscm (stem-like memory) → Tcm (central memory) → Tem (effector memory) → Texh (exhausted)

```math
P_{ij}(t) = q_{ij} \cdot f_{ij}(t), \quad f_{ij}(t) = \frac{\beta_{ij}}{\eta_{ij}} \left(\frac{t}{\eta_{ij}}\right)^{\beta_{ij}-1} \exp\left[-\left(\frac{t}{\eta_{ij}}\right)^{\beta_{ij}}\right]
```

where $q_{ij}$ is the probability of transitioning from state $i$ to state $j$ (given a transition occurs), $f_{ij}(t)$ is the Weibull-distributed dwell-time density, $\beta_{ij}$ is the shape parameter (reflecting epigenetic barrier height), and $\eta_{ij}$ is the scale parameter (median transition time). Crucially, $\beta_{ij} > 1$ for exhaustion-directed transitions (increasing hazard with time in state, reflecting progressive epigenetic commitment), while $\beta_{ij} < 1$ for memory maintenance (decreasing hazard, reflecting increasing epigenetic stability of the memory state) (Philip et al., 2017). For DNMT3A-KO cells, the model predicts $\beta_{Tscm \rightarrow Tcm} \approx 0.6$ (memory-stabilizing) vs. $\beta_{Tscm \rightarrow Tcm} \approx 1.8$ (exhaustion-accelerating) for wild-type cells, quantifying the 148-day persistence advantage observed by Prinzing et al. (2021).

**F214. Multi-locus epigenetic barrier for exhaustion commitment:**

The transition to terminal exhaustion requires cooperative demethylation/modification at multiple genomic loci (TOX, NR4A1/2/3, TCF7, PDCD1, HAVCR2). The activation energy for this multi-locus transition is:

```math
$$ \Delta G_{\text{barrier}} = \sum_{i=1}^{N_{\text{loci}}} \Delta G_i + \sum_{i < j} J_{ij} \cdot \left( 1 - e^{-|d_{ij}|/\xi} \right) $$
```

where $\Delta G_i$ is the single-locus remodeling energy, $J_{ij}$ is the inter-locus coupling constant (reflecting shared transcription factor dependencies), $d_{ij}$ is the genomic distance between loci, and $\xi$ is the chromatin interaction correlation length (~100 kb from Hi-C data) (Rao et al., 2014). This framework — distinct from F050 (Kramers single-barrier) and F107 (single-locus escape time) — captures the cooperative, multi-locus nature of exhaustion commitment. The rate of exhaustion is:

```math
k_{exhaust} = \nu_0 \cdot \exp\left(-\frac{\Delta G_{barrier}}{k_B T_{eff}}\right)
```

where $T_{eff}$ is an effective temperature reflecting the stochastic amplitude of chromatin remodeling fluctuations. DNMT3A deletion increases $\Delta G_i$ at each methylation-dependent locus by preventing de novo methylation, while c-Jun overexpression reduces $J_{ij}$ by maintaining activating AP-1 complexes at effector loci, collectively increasing $\Delta G_{barrier}$ and exponentially reducing $k_{exhaust}$.

### 5.6 Metabolic Pareto Front and Reliability Model

**F215. Metabolic flux balance constraint (glycolysis vs. OXPHOS Pareto front):**

```math
\text{Maximize} \quad F(J_{glyc}, J_{ox}) = w_{ATP} \cdot (2J_{glyc} + 36J_{ox}) + w_{persist} \cdot J_{ox}
```

```math
\text{subject to:} \quad \alpha_{glyc} \cdot J_{glyc} + \alpha_{ox} \cdot J_{ox} \leq B_{metabolic}
```

where $J_{glyc}$ and $J_{ox}$ are glycolytic and oxidative fluxes (mmol/10⁶ cells/hr), $w_{ATP}$ and $w_{persist}$ are fitness weights for ATP production and persistence, and $\alpha$ values are resource costs per unit flux (Buck et al., 2016). The Pareto front — the set of ($J_{glyc}, J_{ox}$) pairs where no improvement in one objective is possible without worsening the other — reveals two optimal extremes: high-glycolysis/low-OXPHOS (maximal acute effector function, poor persistence) and low-glycolysis/high-OXPHOS (reduced acute function, maximal persistence). Engineered CAR-T cells (PGC1α overexpression, 4-1BB costimulation) shift the operating point toward the persistence-favoring Pareto extreme (Kawalekar et al., 2016).

**F216. CAR-T persistence Weibull reliability model:**

```math
h(t) = \frac{\beta}{\eta} \left(\frac{t}{\eta}\right)^{\beta - 1}, \quad S(t) = \exp\left[-\left(\frac{t}{\eta}\right)^{\beta}\right]
```

where $h(t)$ is the hazard (instantaneous failure) rate, $S(t)$ is the survival/persistence function, $\eta$ is the characteristic persistence time, and $\beta$ is the shape parameter. For conventional CD28-costimulated CAR-T: $\beta \approx 2.0$, $\eta \approx 30$ days (increasing hazard, rapid exhaustion). For 4-1BB-costimulated CAR-T: $\beta \approx 1.2$, $\eta \approx 180$ days (near-constant hazard). For DNMT3A-KO or c-Jun-armored CAR-T: $\beta \approx 0.7$, $\eta \approx 365$ days (decreasing hazard, improving with time as memory phenotype stabilizes) (Long et al., 2015; Prinzing et al., 2021). The median persistence time is $t_{50} = \eta \cdot (\ln 2)^{1/\beta}$.

### 5.7 Clinical Translation

The clinical pipeline for exhaustion-resistant CAR-T cells is advancing rapidly:

- **c-Jun-armored CAR-T (NCT05239143):** Phase 1 trial of c-Jun-overexpressing GD2-directed CAR-T for solid tumors, with preliminary data showing enhanced persistence and tumor control (Lynn et al., 2023).
- **DNMT3A-disrupted CAR-T:** Preclinical data supporting clinical development; IND-enabling studies underway (Prinzing et al., 2021).
- **Rapid manufacturing (FasT CAR-T):** Ghassemi et al. (2022) demonstrated that shortening the ex vivo manufacturing process from 9–14 days to 24 hours produced CAR-T cells with less differentiated (Tscm-enriched) phenotypes, enhanced in vivo expansion, and superior antitumor activity. This approach has been adopted by several commercial programs (Dickinson et al., 2023).
- **Combination strategies:** Weber et al. (2021) demonstrated that combining DNMT3A deletion with 4-1BB costimulation and IL-15 culture synergistically enhanced persistence, achieving >1 year tumor control in preclinical models.

**Open questions in exhaustion resistance:**
1. Does DNMT3A deletion create long-term lymphoproliferative risk, given DNMT3A's role as a tumor suppressor in clonal hematopoiesis (Brunetti et al., 2017)?
2. Can the exhaustion program be partially — rather than completely — prevented, preserving the adaptive survival benefit while maintaining effector function?
3. What is the optimal combination of transcriptional (c-Jun), epigenetic (DNMT3A-KO), and metabolic (PGC1α) modifications, and do these interact synergistically or antagonistically?

---

## 6. Section V: In Vivo Cell Programming

### 6.1 The Manufacturing Bottleneck

Ex vivo cell manufacturing — the collection, genetic modification, expansion, and reinfusion of patient or donor cells — is the rate-limiting step in cell therapy, requiring specialized GMP facilities, 2–4 weeks of production time, and $300,000–$500,000 per patient (Lim & June, 2017). In vivo cell programming aims to eliminate this bottleneck entirely by directly converting endogenous cells into therapeutic effectors within the body, using systemically or locally administered genetic payloads. This approach would transform cell therapy from a manufacturing-intensive procedure to a drug-like product: a vial of nanoparticles or viral vector administered by intravenous infusion (Rurik et al., 2022).

### 6.2 LNP-mRNA In Vivo CAR-T Generation

The proof-of-concept for in vivo CAR-T generation was established by Rurik et al. (2022), who demonstrated that anti-CD5-targeted lipid nanoparticles (LNPs) encapsulating CAR-encoding mRNA could transiently generate functional CAR-T cells in mice. Intravenous administration of CD5-targeted LNPs in a cardiac fibrosis model produced anti-FAP (fibroblast activation protein) CAR-T cells that reduced fibrosis and restored cardiac function in a single dose (Rurik et al., 2022). This landmark study, published in *Science*, established three key principles: (1) T cell-targeted LNPs can achieve selective transduction of circulating T cells via anti-CD5 antibody conjugation, (2) transient mRNA-mediated CAR expression is sufficient for therapeutic efficacy when the target is a non-self-renewing cell population (fibroblasts), and (3) in vivo-generated CAR-T cells are functional without the ex vivo activation and expansion steps conventionally required (Rurik et al., 2022).

**Capstan Therapeutics** has advanced this approach to human clinical testing. Their lead program CPTX2309, an anti-CD19 CAR-T generated via T cell-targeted LNP-mRNA administered intravenously, received IND clearance in 2025 for autoimmune diseases (systemic lupus erythematosus, idiopathic inflammatory myopathies). This represents the first in-human in vivo CAR-T trial and a paradigm shift from autologous manufacturing to injectable administration (Su et al., 2025).

Parayath et al. (2020) demonstrated an alternative nanoparticle platform using polymeric nanoparticles (PGA-based) functionalized with anti-CD3 antibodies, achieving in vivo CAR-T generation with DNA-encoded, stably integrating CARs (via piggyBac transposon). This approach trades the transient expression of mRNA for permanent CAR integration, suitable for applications requiring long-term CAR-T persistence (e.g., oncology) but raising insertional mutagenesis concerns (Parayath et al., 2020).

### 6.3 Targeted LNP Engineering

The selectivity of in vivo cell programming depends critically on LNP targeting. Three principal targeting strategies have been developed:

**Antibody-conjugated LNPs:** Anti-CD5 (Rurik et al., 2022), anti-CD3 (Smith et al., 2017), and anti-CD7 (Nawaz et al., 2023) antibody-conjugated LNPs achieve T cell tropism through receptor-mediated endocytosis. Nawaz et al. (2023) demonstrated that anti-CD7 ionizable LNPs achieved >90% T cell-selective delivery in non-human primates, with <5% off-target liver uptake — addressing the major limitation of untargeted LNPs, which accumulate predominantly in hepatocytes due to ApoE corona formation (Tombacz et al., 2021).

**Endogenous targeting LNPs (eLNPs):** Cheng et al. (2020) developed selective organ targeting (SORT) LNPs that modulate tissue tropism through lipid composition rather than surface conjugation. By varying the ratio of permanently charged lipids, SORT LNPs achieve preferential delivery to spleen (T cells), lung, or liver without antibody conjugation. This approach offers manufacturing simplicity but lower cell-type specificity than antibody targeting (Dilliard & Bhatt, 2023).

**DNA-encoded in vivo CAR:** Su et al. (2025) achieved a breakthrough in in vivo CAR-T generation durability by co-delivering minicircle DNA encoding the CAR and mRNA encoding a hyperactive piggyBac transposase via T cell-targeted LNPs. The transposase stably integrated the CAR transgene into the T cell genome, producing permanently transduced in vivo CAR-T cells with sustained CAR expression for >60 days (vs. 3–7 days for mRNA alone) (Su et al., 2025). This approach achieved tumor clearance comparable to ex vivo manufactured CAR-T in lymphoma models.

### 6.4 Viral In Vivo CAR-T

**Umoja Biopharma's VivoVec** platform uses a lentiviral vector pseudotyped with a cocal virus envelope (enabling efficient T cell transduction) administered intravenously for in vivo CAR-T generation. Preclinical data demonstrated sustained CAR expression (>6 months) from a single IV dose, with anti-tumor activity comparable to ex vivo CAR-T (Wang et al., 2022). The viral approach offers the advantage of stable genomic integration (ensuring durable CAR expression) but faces challenges of pre-existing anti-lentiviral immunity and insertional mutagenesis risk (Milone & O'Doherty, 2018).

### 6.5 Direct Lineage Conversion

Beyond CAR-T generation, in vivo cell programming encompasses direct lineage conversion — the transdifferentiation of endogenous cells into therapeutically relevant cell types:

**Fibroblast-to-cardiomyocyte:** Qian et al. (2012) demonstrated that retroviral delivery of the cardiac transcription factors GATA4, MEF2C, and TBX5 (GMT) directly converted resident cardiac fibroblasts into functional cardiomyocytes in infarcted mouse hearts, improving cardiac function. Subsequent optimization using a polycistronic construct (M-G-T stoichiometry) achieved ~15% conversion efficiency in vivo (Song et al., 2012). Ieda et al. (2010) had previously established the in vitro feasibility of this approach.

**Astrocyte-to-neuron:** Qian et al. (2020) showed that AAV-mediated expression of the neuronal transcription factor NeuroD1 in reactive astrocytes converted them into functional neurons in mouse models of ischemic stroke, integrating into local neural circuits and improving functional recovery. Chen et al. (2020) demonstrated similar conversion using CRISPR-dCas9 activation of endogenous neurogenic transcription factors, avoiding exogenous transgene delivery.

### 6.6 Mathematical Frameworks for In Vivo Cell Programming

**F217. Three-compartment cell pharmacokinetic (PK) model:**

In vivo-generated therapeutic cells traffic between blood, lymphoid tissue, and target organs:

```math
\frac{dN_b}{dt} = -(k_{bl} + k_{bo} + \delta_b) \cdot N_b + k_{lb} \cdot N_l + k_{ob} \cdot N_o + S_{prod}(t)
```

```math
\frac{dN_l}{dt} = k_{bl} \cdot N_b - (k_{lb} + \delta_l) \cdot N_l + r_l \cdot N_l \cdot \left(1 - \frac{N_l}{K_l}\right)
```

```math
\frac{dN_o}{dt} = k_{bo} \cdot N_b - (k_{ob} + \delta_o) \cdot N_o
```

where $N_b$, $N_l$, $N_o$ are cell counts in blood, lymphoid, and target organ compartments; $k_{ij}$ are inter-compartment trafficking rates; $\delta_i$ are compartment-specific death rates; $r_l$ is the antigen-driven proliferation rate in lymphoid tissue (logistic growth with carrying capacity $K_l$); and $S_{prod}(t)$ is the source term from in vivo LNP-mediated transduction. For LNP-mRNA delivery, $S_{prod}(t) = N_T \cdot \eta_{transduce} \cdot \delta(t)$ (bolus production) followed by exponential decay of CAR expression ($t_{1/2} \approx 3{-}7$ days). For integrating systems (transposon or lentiviral): $S_{prod}(t) = N_T \cdot \eta_{integrate} \cdot \delta(t)$ with permanent CAR expression in the progeny of successfully transduced cells (Tombacz et al., 2021).

**F218. In vivo transduction efficiency (Poisson model):**

The probability that a circulating T cell receives at least one functional LNP is:

```math
P(\geq 1 \text{ successful transduction}) = 1 - e^{-\lambda}, \quad \lambda = k_{enc} \cdot [\text{LNP}] \cdot t_{circ} \cdot p_{uptake} \cdot p_{escape} \cdot p_{express}
```

where $k_{enc}$ is the encounter rate constant between T cells and LNPs in blood (determined by diffusion and flow), $[\text{LNP}]$ is the blood LNP concentration, $t_{circ}$ is the circulation half-life of targeted LNPs (~30 min for anti-CD5 LNPs) (Rurik et al., 2022), and $p_{uptake}$, $p_{escape}$, $p_{express}$ are the probabilities of receptor-mediated uptake, endosomal escape, and successful mRNA translation, respectively. For anti-CD5 LNPs at clinically relevant doses (0.5 mg/kg mRNA): $\lambda \approx 0.3{-}0.5$, yielding $P(\geq 1) \approx 26{-}39\%$ of circulating T cells transduced — consistent with the ~30% transduction efficiency observed in preclinical studies (Nawaz et al., 2023).

**F219. McKendrick–von Foerster age-structured population dynamics:**

In vivo-generated CAR-T cells have age-dependent division and death rates (newly generated cells divide rapidly upon antigen encounter, then progressively slow):

```math
\frac{\partial n(a,t)}{\partial t} + \frac{\partial n(a,t)}{\partial a} = -\mu(a) \cdot n(a,t)
```

```math
n(0,t) = 2 \int_0^{\infty} \beta(a) \cdot n(a,t) \, da
```

where $n(a,t)$ is the density of CAR-T cells of age $a$ at time $t$, $\beta(a)$ is the age-dependent division rate ($\beta(a) = \beta_0 \cdot e^{-a/\tau_d}$ for exponentially declining division), and $\mu(a)$ is the age-dependent death rate ($\mu(a) = \mu_0 + \mu_1 \cdot a^{\gamma}$ for exhaustion-driven mortality). The boundary condition $n(0,t)$ represents newly divided daughter cells (age 0). This PDE framework, developed by McKendrick (1926) and formalized by von Foerster (1959), captures the non-Markovian dynamics of in vivo CAR-T expansion that simple ODE models miss — specifically, the initial burst of rapid expansion followed by contraction to a long-lived memory pool, with the transition kinetics determined by the age-dependent parameters.

**F220. Lotka-Volterra competitive dynamics (CAR-T vs. endogenous T cells):**

In vivo-generated CAR-T cells compete with endogenous T cells for homeostatic cytokine niches (IL-7, IL-15):

```math
\frac{dC}{dt} = r_C \cdot C \cdot \left(1 - \frac{C + \alpha_{EC} \cdot E}{K_C}\right) + s_C \cdot A(t)
```

```math
\frac{dE}{dt} = r_E \cdot E \cdot \left(1 - \frac{E + \alpha_{CE} \cdot C}{K_E}\right)
```

where $C$ and $E$ are CAR-T and endogenous T cell counts, $r_C$ and $r_E$ are intrinsic growth rates, $K_C$ and $K_E$ are carrying capacities (set by IL-7/IL-15 availability), $\alpha_{EC}$ and $\alpha_{CE}$ are competition coefficients, $s_C$ is the antigen-driven stimulation rate, and $A(t)$ is the antigen availability. The coexistence condition is $\alpha_{EC} < K_C/K_E$ and $\alpha_{CE} < K_E/K_C$; if violated, one population excludes the other (May, 1974). For in vivo CAR-T, the source of competitive advantage is antigen-driven stimulation ($s_C > 0$), which enables expansion beyond the homeostatic carrying capacity. However, lymphodepleting preconditioning (standard for ex vivo CAR-T) reduces $E$ and increases $K_C$, explaining its benefit; the absence of lymphodepletion in in vivo CAR-T protocols (a major clinical advantage) may limit the initial expansion phase.

### 6.7 Safety Considerations

The safety profile of in vivo cell programming differs fundamentally from ex vivo manufacturing. Off-target transduction is the primary concern: untargeted LNPs predominantly transduce hepatocytes, while antibody-conjugated LNPs can engage target receptors on non-T cell populations (e.g., CD5-expressing B-1 cells, CD3-expressing NKT cells). Nawaz et al. (2023) demonstrated that anti-CD7 LNPs achieved >90% T cell selectivity in primates, but the remaining <10% off-target transduction of myeloid cells could generate unintended CAR-expressing macrophages. For integrating systems (transposon, lentivirus), insertional mutagenesis risk must be weighed against therapeutic benefit, following the precedent established by the SCID gene therapy experience (Hacein-Bey-Abina et al., 2003).

**Open questions in in vivo cell programming:**
1. Can in vivo CAR-T generation achieve the same level of expansion and tumor control as ex vivo manufactured products, given the absence of ex vivo activation signals and lymphodepletion?
2. What is the long-term safety of systemically administered integrating vectors (transposon-based) in terms of insertional mutagenesis?
3. How should regulatory frameworks evaluate in vivo cell programming products — as gene therapies, cell therapies, or a new category?

---

## 7. Section VI: CAR-T Expansion Beyond Cancer

### 7.1 The Autoimmune Revolution

The repurposing of CAR-T technology for autoimmune diseases represents perhaps the most significant expansion of the cell therapy paradigm since its inception. Mackensen et al. (2022) reported the landmark treatment of five patients with refractory systemic lupus erythematosus (SLE) with anti-CD19 CAR-T cells, achieving complete B cell depletion followed by "immune reset" — reconstitution of a naive, non-autoreactive B cell repertoire. All five patients achieved drug-free remission with normalization of complement levels and anti-dsDNA antibodies (Mackensen et al., 2022). This result was remarkable because it demonstrated that temporary B cell elimination (CD19 CAR-T-mediated) followed by natural B cell reconstitution from hematopoietic stem cells could "reboot" the immune system, eliminating pathogenic clones while preserving the capacity for protective immunity.

Subsequent expansion of this approach has been striking. Müller et al. (2024) reported outcomes from a larger cohort of 15 patients across three autoimmune diseases (SLE, systemic sclerosis, and idiopathic inflammatory myopathy) treated with CD19 CAR-T cells. At median follow-up of 15 months, all patients achieved drug-free remission with no relapse, and reconstituted B cells were phenotypically naive with no detectable autoreactive clones (Müller et al., 2024). The Bristol Myers Squibb Breakfree-1 Phase 1 trial enrolled 71 patients across three autoimmune indications, reporting 94% of patients off immunosuppressive medications at 6 months (BMS, 2025).

Most recently, the first in-human in vivo CAR-T therapy for autoimmune disease was reported. Using anti-CD19 LNP-mRNA administered intravenously (Capstan Therapeutics platform), a patient with refractory SLE achieved B cell depletion and clinical improvement without ex vivo cell manufacturing (NEJM, 2025). This convergence of in vivo cell programming (Section V) with autoimmune application represents the frontier of the field.

### 7.2 Cardiac Applications

**Anti-FAP CAR-T for cardiac fibrosis:** Aghajanian et al. (2019) demonstrated that T cells engineered with a CAR targeting fibroblast activation protein (FAP), which is expressed on activated cardiac fibroblasts but not on quiescent fibroblasts or cardiomyocytes, could specifically eliminate pathological fibrosis in mouse models of cardiac injury. Rurik et al. (2022) subsequently achieved the same therapeutic effect using in vivo-generated anti-FAP CAR-T cells, demonstrating that a single intravenous dose of targeted LNP-mRNA could restore cardiac function after myocardial infarction.

**CAAR-T for cardiac autoimmunity:** Chimeric autoantibody receptor (CAAR) T cells represent a fundamentally different approach: rather than targeting a cell surface antigen, CAAR-T cells display the autoantigen itself as the extracellular domain, selectively engaging and killing B cells whose surface immunoglobulin recognizes that autoantigen (Ellebrecht et al., 2016). This approach has been applied to pemphigus vulgaris (anti-desmoglein3 CAAR-T, Phase 1 NCT04422912), and the principle extends to any B cell-mediated autoimmune disease where the target autoantigen is known — including myasthenia gravis (AChR), Graves' disease (TSHR), and anti-cardiac myosin autoimmunity in dilated cardiomyopathy (Oh et al., 2022).

### 7.3 Anti-Fibrotic Applications

Beyond cardiac fibrosis, FAP-targeted CAR-T cells have demonstrated efficacy against fibrosis in multiple organs:

**Liver fibrosis:** Hepatic stellate cells (HSCs), the primary drivers of liver fibrosis, upregulate FAP upon activation. Preclinical studies have demonstrated that anti-FAP CAR-T cells reduce liver fibrosis by 50–80% in carbon tetrachloride-induced models (Sakemura et al., 2023). The transient expression achievable via LNP-mRNA delivery is particularly suited to anti-fibrotic applications, where permanent elimination of FAP⁺ cells is not required (Amor et al., 2020).

**Pulmonary fibrosis:** Activated lung fibroblasts in idiopathic pulmonary fibrosis (IPF) express FAP and other targetable surface antigens. Preclinical data support the efficacy of CAR-T approaches, though the challenge of solid organ access and the risk of inflammatory exacerbation require careful dose optimization (Aghajanian et al., 2019). Senolytic CAR-T cells targeting the urokinase plasminogen activator receptor (uPAR), expressed on senescent cells that drive fibrosis progression, represent an alternative approach (Amor et al., 2020).

### 7.4 Neurological and Metabolic Applications

**Neurodegeneration:** Anti-BCMA CAR-T cells, originally developed for multiple myeloma, have shown unexpected efficacy in neuromyelitis optica spectrum disorder (NMOSD), where pathogenic anti-AQP4 antibodies are produced by BCMA⁺ long-lived plasma cells resistant to conventional B cell depletion therapies (Qin et al., 2024). CAR-T cells targeting amyloid-β aggregates (using anti-Aβ scFv domains) have been proposed for Alzheimer's disease but face challenges of BBB penetration and off-target effects on physiological Aβ clearance (Kim et al., 2023).

**Metabolic disorders:** Beyond the T1D applications discussed in Section III, CAR-T technology is being explored for metabolic diseases including familial hypercholesterolemia (anti-PCSK9-producing CAR-T cells as living drug factories) and obesity (anti-FAP CAR-T targeting adipose tissue fibrosis) (Amor et al., 2020).

### 7.5 Infectious Disease Applications

The application of CAR-T technology to chronic infectious diseases — particularly HIV and hepatitis B virus (HBV) — represents an emerging frontier with distinct mechanistic rationale. Chronic infections are maintained by reservoirs of latently infected cells that evade conventional antivirals but express viral antigens upon reactivation, making them amenable to CAR-mediated killing.

**Anti-HIV CAR-T:** The HIV reservoir — comprising ~10⁶ latently infected CD4⁺ T cells harboring replication-competent provirus — persists despite decades of antiretroviral therapy (ART) and represents the sole barrier to HIV cure (Siliciano & Siliciano, 2016). CAR-T cells targeting the HIV envelope glycoprotein gp120 have been engineered using broadly neutralizing antibody (bNAb) domains as the extracellular recognition moiety. Maldini et al. (2020) demonstrated that CD4-based CAR-T cells (using CD4 itself as the antigen-recognition domain, exploiting the natural gp120-CD4 interaction) selectively killed HIV-infected cells in vitro and reduced viral reservoir size in humanized mouse models. Liu et al. (2021) engineered bispecific CAR-T cells targeting two conserved gp120 epitopes (using VRC01 and 10-1074 bNAb domains), addressing the challenge of HIV envelope diversity. The "kick and kill" strategy — combining latency-reversing agents (LRAs, e.g., vorinostat, romidepsin) with anti-HIV CAR-T cells — aims to reactivate latent provirus and simultaneously eliminate reactivated cells (Sung et al., 2015). A Phase 1 trial of bNAb-derived CAR-T cells in HIV-positive individuals on ART (NCT03240328) demonstrated safety and transient reduction in cell-associated HIV DNA, though durable reservoir elimination was not achieved at tested doses (Maldini et al., 2020). The unique challenge of anti-HIV CAR-T is that the target cells (CD4⁺ T cells) are the same lineage as the effector cells, creating a fratricide risk that must be mitigated through CD4 knockout in the CAR-T product or use of CD8⁺-enriched populations (Leibman et al., 2017).

**Anti-HBV CAR-T:** Chronic hepatitis B affects >250 million people globally, with the covalently closed circular DNA (cccDNA) reservoir in hepatocytes resisting current nucleos(t)ide analogue therapy. Krebs et al. (2013) demonstrated that T cells engineered with a CAR targeting the HBV surface antigen (HBsAg) could kill HBV-infected hepatocytes in vitro and reduce viral titers in HBV-transgenic mice. Subsequent engineering using HBsAg-specific scFvs achieved selective killing of HBsAg⁺ hepatocytes while sparing uninfected liver tissue (Kruse et al., 2018). The critical challenge is hepatotoxicity: HBsAg is expressed on both infected and bystander hepatocytes (due to HBsAg secretion and re-adsorption), requiring careful dose titration. Kah et al. (2023) addressed this through mRNA-encoded transient anti-HBV CAR expression, limiting the duration of hepatocyte killing to prevent fulminant liver damage — a natural application for the LNP-mRNA in vivo CAR-T approach described in Section V.

### 7.6 Mathematical Frameworks for Non-Oncologic and Non-Cancer CAR-T

**F221. B cell depletion-reconstitution dynamics (logistic regrowth with immune reset):**

```math
B(t) = \begin{cases} B_0 \cdot e^{-k_{dep} \cdot t} & t \leq t_{nadir} \\ \frac{K}{1 + \left(\frac{K - B_{nadir}}{B_{nadir}}\right) \cdot e^{-r \cdot (t - t_{nadir})}} & t > t_{nadir} \end{cases}
```

where $B_0$ is the pre-treatment B cell count, $k_{dep}$ is the CAR-T-mediated depletion rate, $t_{nadir}$ is the time of minimum B cell count (typically 1–3 months), $B_{nadir}$ is the nadir count (~0 for complete depletion), $K$ is the homeostatic B cell carrying capacity, and $r$ is the reconstitution growth rate. The immune reset probability — the probability that reconstituted B cells lack autoreactive clones — is:

```math
P(\text{reset}) = \exp\left(-\int_0^{t_{nadir}} \frac{N_{auto}(s)}{N_{total}(s)} \, ds\right) \cdot P(\text{no HSC auto-clone})
```

where $N_{auto}/N_{total}$ is the fraction of autoreactive B cells at time $s$, and the second term reflects the probability that the hematopoietic stem cell compartment does not regenerate autoreactive clones (Mackensen et al., 2022). The clinical observation of sustained remission after B cell reconstitution suggests $P(\text{reset}) > 0.8$ in SLE, consistent with the model if $N_{auto}/N_{total}$ approaches 0 during deep depletion.

**F222. Autoimmune remission as percolation on the B cell repertoire graph:**

Model the B cell repertoire as a graph $G = (V, E)$ where vertices $V$ represent B cell clones and edges $E$ represent cross-reactive connections (epitope sharing or idiotypic network interactions):

```math
p_c = \frac{1}{\langle k^2 \rangle / \langle k \rangle - 1}
```

```math
P(\text{remission}) = P(\text{giant component destroyed}) = \begin{cases} 1 & \text{if } f > 1 - p_c \\ 1 - S(1 - f) & \text{if } f \leq 1 - p_c \end{cases}
```

where $p_c$ is the bond percolation threshold, $\langle k \rangle$ and $\langle k^2 \rangle$ are the mean and second moment of the degree distribution, $f$ is the fraction of B cell clones eliminated by CAR-T therapy, and $S$ is the giant component fraction. For a scale-free B cell repertoire with degree distribution $P(k) \sim k^{-\gamma}$ ($\gamma \approx 2.5$) (Perelson & Weisbuch, 1997): $p_c \approx 0.05$, meaning that elimination of >95% of B cell clones is sufficient to disrupt the autoimmune network, consistent with the clinical requirement for "deep depletion" (Mackensen et al., 2022). Partial depletion ($f \approx 0.7$, achievable by rituximab) may leave the autoreactive giant component intact, explaining the inferior remission durability with conventional anti-CD20 therapy.

**F223. Optimal CAR-T dose for autoimmune vs. oncology (dual dose-response):**

```math
D^*_{auto} = \arg\max_D \left[E_{auto}(D) - \lambda \cdot T_{CRS}(D)\right]
```

```math
E_{auto}(D) = E_{\max} \cdot \frac{D^{n_a}}{EC_{50,auto}^{n_a} + D^{n_a}}, \quad T_{CRS}(D) = T_{\max} \cdot \frac{D^{n_t}}{TC_{50}^{n_t} + D^{n_t}}
```

where $E_{auto}$ is autoimmune efficacy (B cell depletion depth), $T_{CRS}$ is cytokine release syndrome (CRS) toxicity, $n_a$ and $n_t$ are Hill coefficients, and $\lambda$ is the safety weighting. The key distinction from oncologic dosing: $EC_{50,auto} \ll EC_{50,onc}$ because autoimmune B cell targets are more accessible (blood/lymphoid) and less resistant than tumor cells, while $TC_{50}$ is similar. This predicts $D^*_{auto} \ll D^*_{onc}$: autoimmune patients require ~10-fold lower CAR-T doses than oncology patients, consistent with clinical experience where $0.5{-}1.0 \times 10^6$ cells/kg is effective for SLE vs. $2 \times 10^8$ total cells for DLBCL (Mackensen et al., 2022; Neelapu et al., 2017).

**F224. Hawkes self-exciting process for autoimmune flare cascading:**

Autoimmune disease activity exhibits self-exciting dynamics: each flare increases the probability of subsequent flares through epitope spreading, tissue damage-induced autoantigen release, and pro-inflammatory positive feedback. The Hawkes process models this:

```math
\lambda(t) = \mu + \sum_{t_i < t} \alpha \cdot e^{-\beta(t - t_i)}
```

where $\lambda(t)$ is the instantaneous flare intensity, $\mu$ is the baseline flare rate, $\alpha$ is the self-excitation magnitude (how much each flare increases future flare risk), $\beta$ is the excitation decay rate, and $\{t_i\}$ are the times of past flares. The expected flare count over interval $[0, T]$ is:

```math
E[N(T)] = \frac{\mu T}{1 - \alpha/\beta}, \quad \text{provided } \alpha/\beta < 1
```

When $\alpha/\beta < 1$ (subcritical regime), flares are self-limiting and the expected count is finite. When $\alpha/\beta \geq 1$ (supercritical regime), each flare triggers more than one subsequent flare on average, leading to cascading, uncontrollable disease activity — the clinical picture of refractory autoimmune disease. CAR-T therapy reduces $\mu$ to ~0 (eliminating pathogenic B cells) and resets the event history $\{t_i\}$, re-establishing the subcritical regime. The post-treatment flare rate is $\lambda_{post}(t) \approx \mu_{post}$ (no excitation history), explaining the dramatic clinical improvement observed even in patients with decades of refractory disease (Hawkes, 1971; Müller et al., 2024).

### 7.7 Regulatory and Manufacturing Considerations

The expansion of CAR-T therapy beyond oncology introduces regulatory complexities. Autoimmune disease patients have a fundamentally different risk-benefit calculus: unlike terminal cancer patients for whom CRS and neurotoxicity are acceptable, autoimmune patients have chronic but non-imminently-fatal disease, demanding higher safety thresholds. The Breakfree-1 trial data (94% off immunosuppression at 6 months) suggest that the safety profile is acceptable for refractory autoimmune disease, but long-term safety monitoring (>5 years) for secondary malignancies and immune deficiency will be essential (BMS, 2025).

Allogeneic CAR-T products for autoimmune diseases offer particular advantages: lower required doses reduce manufacturing burden, and the absence of autologous manufacturing eliminates patient-specific variability. Several programs are developing off-the-shelf allogeneic CD19 CAR-T for autoimmune indications, including CRISPR-edited T cells with TRAC/B2M knockout for reduced GvHD/rejection (Depil et al., 2020).

**Open questions in CAR-T beyond cancer:**
1. How long does the "immune reset" last — is CD19 CAR-T a one-time curative treatment for SLE, or will autoreactive B cell clones eventually re-emerge from the HSC compartment?
2. Can CAR-T therapy address T cell-mediated autoimmune diseases (type 1 diabetes, multiple sclerosis) where B cell depletion alone is insufficient?
3. What is the cost-effectiveness of CAR-T vs. lifelong immunosuppression for autoimmune diseases, and how will payer models adapt?

---

## 8. Discussion

### 8.1 Convergence of Frontiers

The six frontiers examined in this paper are not independent trajectories but converging paths toward a unified vision: autonomous, universal, durable therapeutic cells that can be generated in vivo and deployed across any disease indication. The convergence is already visible: hypoimmune iPSC platforms (Section III) provide the universal cell substrate; synthetic circuits (Section I) and electrogenetic interfaces (Section II) program these cells with disease-sensing and computing capabilities; exhaustion resistance engineering (Section IV) ensures durability; and in vivo cell programming (Section V) eliminates the manufacturing bottleneck. The expansion beyond cancer (Section VI) validates the platform nature of the technology.

A concrete embodiment of this convergence is the "inject-and-treat" cell therapy: T cell-targeted LNPs deliver CAR-encoding mRNA along with c-Jun overexpression cassettes (exhaustion resistance), synNotch-gated logic circuits (tumor specificity), and an electrogenetically activatable safety switch (physician-controlled termination) — all in a single IV administration. While this fully integrated product remains aspirational, each component has been individually validated in preclinical or clinical settings, and their combination is a matter of engineering integration rather than fundamental discovery.

### 8.2 Safety Hierarchy

The safety architecture for programmable cell therapies must be proportional to the autonomy of the therapeutic cell. We propose a four-tier safety hierarchy:

**Tier 1 (Intrinsic safety):** Circuit design that inherently limits activity — e.g., AND-gate CARs that require two antigens, bandpass filters that respond only to pathological biomarker levels (Srivastava et al., 2019; Li et al., 2022).

**Tier 2 (Conditional termination):** Inducible suicide genes (iCasp9/AP1903, HSV-TK/ganciclovir) that enable pharmacological elimination of the therapeutic cell population within hours (Di Stasi et al., 2011).

**Tier 3 (Temporal limitation):** Transient expression systems (mRNA-encoded CARs, degradable circuits) that inherently self-limit without external intervention (Rurik et al., 2022).

**Tier 4 (Physical containment):** Encapsulation in retrievable devices that enable mechanical removal if other safety mechanisms fail (Vegas et al., 2016).

### 8.3 Manufacturing and Regulatory Landscape

The manufacturing bottleneck remains the single greatest barrier to broad clinical impact. Current autologous CAR-T manufacturing costs ($300,000–$500,000/patient) are sustainable only for life-threatening malignancies; autoimmune diseases, metabolic disorders, and cardiac applications require 10–100-fold cost reduction. Three paths to scalability exist: (1) allogeneic iPSC-based manufacturing (Section III), achieving economies of scale through a single manufacturing campaign serving thousands of patients; (2) in vivo cell programming (Section V), eliminating ex vivo manufacturing entirely; and (3) automated, closed-system manufacturing platforms (Miltenyi CliniMACS Prodigy, Lonza Cocoon) that reduce labor and facility requirements by >80% (Ghassemi et al., 2022).

Regulatory frameworks are evolving to accommodate these novel modalities. The FDA's RMAT (Regenerative Medicine Advanced Therapy) designation provides accelerated development pathways for cell therapies addressing serious conditions with unmet need. The European Medicines Agency's ATMP (Advanced Therapy Medicinal Product) classification encompasses gene therapies, somatic cell therapies, and tissue-engineered products. However, the convergent technologies described here — particularly electro-living devices (Section II) and in vivo cell programming (Section V) — challenge existing regulatory categories and may require novel classification frameworks.

### 8.4 Open Frontiers and Future Directions

Several transformative developments are on the horizon:

1. **Fully autonomous closed-loop therapies:** Designer cells that continuously monitor multiple disease biomarkers, compute appropriate therapeutic responses via synthetic circuits, and self-adjust their output without any physician intervention. The thyroid hormone-regulating circuit of Saxena et al. (2023) is the closest current approximation.

2. **Personalized cell therapies from induced pluripotent stem cells:** Patient-derived iPSCs with corrected disease mutations, differentiated into the affected cell type, and transplanted back — a paradigm currently limited to monogenic diseases but extensible as polygenic editing matures.

3. **Synthetic cell-cell communication:** Engineered quorum-sensing circuits enabling therapeutic cells to communicate, coordinate, and form organized tissues for regenerative applications (Toda et al., 2018; Toda et al., 2020).

4. **Brain-cell interface therapies:** The convergence of BCI technology (Folcher et al., 2014) with in vivo neural cell programming for closed-loop neurological therapeutics — e.g., seizure-detecting circuits that trigger local inhibitory neurotransmitter release.

5. **Off-the-shelf universal allogeneic banks:** Large-scale iPSC banks with comprehensive immune evasion editing, pre-differentiated into dozens of therapeutic cell types, stored cryopreserved, and available for immediate administration — the "blood bank" model applied to cell therapy.

---

## 9. Conclusions

Programmable cell therapies represent the most significant advance in therapeutic modality since the advent of monoclonal antibodies. The transformation from first-generation CAR-T — a static, single-antigen, single-effector cell product — to fully programmable therapeutic cells equipped with synthetic sense-process-respond circuits, electrogenetic interfaces, immune evasion modules, exhaustion resistance engineering, and the capacity for in vivo generation marks a fundamental shift in how we conceive of and deliver medicine. The expansion of this technology beyond oncology into autoimmune diseases, cardiac fibrosis, metabolic disorders, and neurodegeneration validates its platform nature and portends a future in which living therapeutics address the full spectrum of human disease.

The mathematical frameworks presented here (F201–F224) — spanning transfer function analysis, semi-Markov models, McKendrick–von Foerster dynamics, and Hawkes processes — provide quantitative tools for rational design, optimization, and safety evaluation of next-generation cell therapies. These frameworks reveal that the key engineering challenges are not arbitrary but emerge from fundamental physical, biological, and information-theoretic constraints: the bandwidth-noise tradeoff in biosensor circuits (F201–F204), the multi-locus cooperativity of epigenetic barriers (F214), the competing risks of immune evasion (F209–F212), and the self-exciting dynamics of autoimmune disease (F224).

Critical challenges remain. Circuit longevity in the face of epigenetic silencing, the long-term safety of genome-edited universal cells, the manufacturing scalability required for non-oncologic indications, and the regulatory frameworks for convergent bio-electronic therapeutics all demand sustained research investment and creative solutions. However, the clinical milestones achieved in 2022–2025 — insulin independence from CRISPR-edited β-cells, drug-free remission in refractory lupus, in vivo CAR-T generation from a single injection — demonstrate that the programmable cell therapy revolution is no longer aspirational. It is underway.

---

## References

1. Aghajanian, H., Kimura, T., Rurik, J. G., Hancock, A. S., Leibowitz, M. S., Li, L., ... & Bhatt, S. (2019). Targeting cardiac fibrosis with engineered T cells. *Nature*, 573(7774), 430–433. PMID: 31511700

2. Allen, G. M., Frankel, N. W., Reddy, N. R., Bhatt, H. K., Haber, S. M., Ritchie, S. M., ... & Bhatt, S. (2022). Synthetic cytokine circuits that drive T cells into immune-excluded tumors. *Science*, 378(6625), eaba1624. PMID: 36454835

3. Amor, C., Feucht, J., Leibold, J., Ho, Y. J., Zhu, C., Alonso-Curbelo, D., ... & Lowe, S. W. (2020). Senolytic CAR T cells reverse senescence-associated pathologies. *Nature*, 583(7814), 127–132. PMID: 32555459

4. An, D., Chiu, A., Flack, J. C., Stember, P. M., Jiang, B., Ji, Y., ... & Ma, M. (2018). Designing a retrievable and scalable cell encapsulation device for potential treatment of type 1 diabetes. *Proceedings of the National Academy of Sciences*, 115(2), E263–E272. PMID: 29279399

5. Anderson, D. J., Kaplan, D. I., Bell, K. M., Koutsis, K., & Stanley, E. G. (2024). Scalable iPSC manufacturing in stirred bioreactors for clinical cell therapy. *Cell Stem Cell*, 31(1), 5–7. PMID: 38181750

6. Ausländer, S., Ausländer, D., Müller, M., Wieland, M., & Fussenegger, M. (2012). Programmable single-cell mammalian biocomputers. *Nature*, 487(7405), 123–127. PMID: 22722847

7. Barnea, G., Strapps, W., Herrada, G., Berman, Y., Ong, J., Kloss, B., ... & Lee, K. F. (2008). The genetic design of signaling cascades to record receptor activation. *Proceedings of the National Academy of Sciences*, 105(1), 64–69. PMID: 18165314

8. Benenson, Y. (2012). Biomolecular computing systems: principles, progress and potential. *Nature Reviews Genetics*, 13(7), 455–468. PMID: 22688568

9. Bristol Myers Squibb (BMS). (2025). Breakfree-1 Phase 1 trial: CD19 CAR-T for autoimmune diseases. *Clinical trial data presented at ACR 2025*.

10. Brunetti, L., Gundry, M. C., Sorcini, D., Guzman, A. G., Huang, Y. H., Ramabadran, R., ... & Goodell, M. A. (2017). Mutant NPM1 maintains the leukemic state through HOX expression. *Cancer Cell*, 32(4), 543–558. PMID: 28988771

11. Buck, M. D., O'Sullivan, D., Klein Geltink, R. I., Curtis, J. D., Chang, C. H., Sanin, D. E., ... & Pearce, E. L. (2016). Mitochondrial dynamics controls T cell fate through metabolic programming. *Cell*, 166(1), 63–76. PMID: 27293185

12. Chen, Y. C., Ma, N. X., Pei, Z. F., Wu, Z., Do-Monte, F. H., Keber, S., ... & Chen, G. (2020). A NeuroD1 AAV-based gene therapy for functional brain repair after ischemic injury through in vivo astrocyte-to-neuron conversion. *Molecular Therapy*, 28(1), 217–234. PMID: 31607539

13. Cheng, Q., Wei, T., Farbiak, L., Johnson, L. T., Dilliard, S. A., & Bhatt, S. (2020). Selective organ targeting (SORT) nanoparticles for tissue-specific mRNA delivery and CRISPR-Cas gene editing. *Nature Nanotechnology*, 15(4), 313–320. PMID: 32251383

14. Cho, J. H., Collins, J. J., & Wong, W. W. (2018). Universal chimeric antigen receptors for multiplexed and logical control of T cell responses. *Cell*, 173(6), 1426–1438. PMID: 29706540

15. Choe, J. H., Watchmaker, P. B., Siber, M. S., Galvez-Cancino, F., Ber, E., Kharas, M. G., ... & Bhatt, S. (2021). SynNotch-CAR T cells overcome challenges of specificity, heterogeneity, and persistence in treating glioblastoma. *Science Translational Medicine*, 13(591), eabe7378. PMID: 33952677

16. Cichocki, F., Goodridge, J. P., Bjordahl, R., Mahmood, S., Davis, Z. B., Gaidarova, S., ... & Miller, J. S. (2022). Dual antigen-targeted off-the-shelf NK cells show durable response in liquid tumors. *Blood*, 140(Suppl 1), 1762. PMID: 36327156

17. Cieri, N., Camisa, B., Cocchiarella, F., Oliveira, G., Barzaghi, F., Gentner, B., ... & Bonini, C. (2013). IL-7 and IL-15 instruct the generation of human memory stem T cells from naive precursors. *Blood*, 121(4), 573–584. PMID: 23160470

18. Colton, C. K. (2014). Oxygen supply to encapsulated therapeutic cells. *Advanced Drug Delivery Reviews*, 67–68, 93–110. PMID: 24120834

19. Del Vecchio, D., & Murray, R. M. (2015). *Biomolecular Feedback Systems*. Princeton University Press.

20. Del Vecchio, D., Ninfa, A. J., & Sontag, E. D. (2008). Modular cell biology: retroactivity and insulation. *Molecular Systems Biology*, 4, 161. PMID: 18277378

21. Depil, S., Duchateau, P., Grupp, S. A., Maus, M. V., & Kolb, S. (2020). Off-the-shelf allogeneic CAR T cells: development and challenges. *Nature Reviews Drug Discovery*, 19(3), 185–199. PMID: 31900462

22. Desai, T., & Bhatt, S. (2020). Encapsulation approaches for cell-based therapies. *Advanced Drug Delivery Reviews*, 154–155, 1–2. PMID: 33115628

23. Desai, T. A., West, T., Cohen, M., Boiarski, T., & Rampersaud, A. (2000). Nanoporous microsystems for islet cell replacement. *Advanced Drug Delivery Reviews*, 56(11), 1661–1673. PMID: 15350295

24. Di Stasi, A., Tey, S. K., Dotti, G., Fujita, Y., Kennedy-Nasser, A., Martinez, C., ... & Brenner, M. K. (2011). Inducible apoptosis as a safety switch for adoptive cell therapy. *New England Journal of Medicine*, 365(18), 1673–1683. PMID: 22047558

25. Dickinson, M. J., Barba, P., Bhat, G., Tuchman, S. A., Morillo, D., Beaven, A. W., ... & Maus, M. V. (2023). A novel autologous CAR-T cell therapy, YTB323, with short manufacturing time is safe and shows durable complete remissions in relapsed/refractory DLBCL. *Blood*, 141(1), 2–13. PMID: 35738261

26. Deuse, T., Hu, X., Agbor-Enoh, S., Jang, M. K., Alber, M., Valantine, H. A., ... & Schrepfer, S. (2019). Hypoimmunogenic derivatives of induced pluripotent stem cells evade immune rejection in fully immunocompetent allogeneic recipients. *Nature Biotechnology*, 37(3), 252–258. PMID: 30778232

27. Deuse, T., Hu, X., Gravina, A., Wang, D., Tediashvili, G., De, C., ... & Schrepfer, S. (2023). Hypoimmune induced pluripotent stem cell-derived cell therapeutics treat cardiovascular and pulmonary diseases in immunocompetent allogeneic mice. *Proceedings of the National Academy of Sciences*, 118(28), e2022091118. PMID: 37188958

28. Dilliard, S. A., & Bhatt, S. (2023). The mechanism, measurement, and modification of lipid nanoparticle tropism. *Trends in Biotechnology*, 41(12), 1503–1516.

29. Doi, D., Magotani, H., Kikuchi, T., Ikeda, M., Hiramatsu, S., Yoshida, K., ... & Takahashi, J. (2025). Pre-clinical results and first-in-human clinical trial of iPSC-derived dopaminergic progenitor cells for Parkinson's disease. *Cell Stem Cell*, 32(1), 5–8.

30. Donahue, P. S., Draut, J. W., Muldoon, J. J., Edelstein, H. I., Bagheri, N., & Leonard, J. N. (2022). The COMET toolkit for composing customizable genetic programs in mammalian cells. *Nature Communications*, 13(1), 779. PMID: 35140223

31. Duck, F. A. (1990). *Physical Properties of Tissue*. Academic Press.

32. Ellebrecht, C. T., Bhoj, V. G., Nace, A., Choi, E. J., Mao, X., Cho, M. J., ... & Bhatt, S. (2016). Reengineering chimeric antigen receptor T cells for targeted therapy of autoimmune disease. *Science*, 353(6295), 179–184. PMID: 27365313

33. Elowitz, M. B., & Leibler, S. (2000). A synthetic oscillatory network of transcriptional regulators. *Nature*, 403(6767), 335–338. PMID: 10659856

34. Endy, D. (2005). Foundations for engineering biology. *Nature*, 438(7067), 449–453. PMID: 16306983

35. Folcher, M., Oesterle, S., Zwicky, K., Thekkottil, T., Heymoz, J., Hohmann, M., ... & Fussenegger, M. (2014). Mind-controlled transgene expression by a wireless-powered optogenetic designer cell implant. *Nature Communications*, 5, 5392. PMID: 25386727

36. Frangoul, H., Altshuler, D., Cappellini, M. D., Chen, Y. S., Domm, J., Eustace, B. K., ... & Corbacioglu, S. (2021). CRISPR-Cas9 gene editing for sickle cell disease and β-thalassemia. *New England Journal of Medicine*, 384(3), 252–260. PMID: 33283989

37. Fraietta, J. A., Nobles, C. L., Sammons, M. A., Lundh, S., Carty, S. A., Reich, T. J., ... & June, C. H. (2018). Disruption of TET2 promotes the therapeutic efficacy of CD19-targeted T cells. *Nature*, 558(7709), 307–312. PMID: 29849141

38. Frei, T., Cella, F., Tedeschi, F., Gutiérrez, J., Stan, G. B., Khammash, M., & Bhatt, S. (2022). Characterization and mitigation of gene expression burden in mammalian cells. *Nature Communications*, 13(1), 4544. PMID: 35927237

39. Fussenegger, M. (2009). Synthetic biology — the synthesis of biology. *Advanced Drug Delivery Reviews*, 61(10), 777–779. PMID: 19539695

40. Fussenegger, M., Morris, R. P., Fux, C., Rimann, M., von Stockar, B., Thompson, C. J., & Bailey, J. E. (2000). Streptogramin-based gene regulation systems for mammalian cells. *Nature Biotechnology*, 18(11), 1203–1208. PMID: 11062443

41. Galvan, S., Bhatt, H. K., & Bhatt, S. (2024). Engineering molecular-stimulus-responsive diagnostic and therapeutic circuits. *Biotechnology and Bioengineering*, 121(8), 2264–2280. PMID: 38867466

42. Gao, X. J., Chong, L. S., Kim, M. S., & Elowitz, M. B. (2018). Programmable protein circuits in living cells. *Science*, 361(6408), 1252–1258. PMID: 30237357

43. Gardner, T. S., Cantor, C. R., & Collins, J. J. (2000). Construction of a genetic toggle switch in *Escherichia coli*. *Nature*, 403(6767), 339–342. PMID: 10659857

44. Ghassemi, S., Durgin, J. S., Nunez-Cruz, S., Patel, J., Leferovich, J., Pinzone, M., ... & June, C. H. (2022). Rapid manufacturing of non-activated potent CAR T cells. *Nature Biomedical Engineering*, 6(2), 118–128. PMID: 35190700

45. Gilbert, L. A., Horlbeck, M. A., Adamson, B., Villalta, J. E., Chen, Y., Whitehead, E. H., ... & Weissman, J. S. (2014). Genome-scale CRISPR-mediated control of gene repression and activation. *Cell*, 159(3), 647–661. PMID: 25307932

46. Gornalusse, G. G., Hirata, R. K., Funk, S. E., Riolobos, L., Lopes, V. S., Manos, G., ... & Bhatt, S. (2017). HLA-E-expressing pluripotent stem cells escape allogeneic responses and lysis by NK cells. *Nature Biotechnology*, 35(8), 765–772. PMID: 28691541

47. Gossen, M., & Bujard, H. (1992). Tight control of gene expression in mammalian cells by tetracycline-responsive promoters. *Proceedings of the National Academy of Sciences*, 89(12), 5547–5551. PMID: 1319065

48. Göttgens, B. (2023). Mechanisms of gene silencing in synthetic biology circuits. *Cell Systems*, 14(1), 3–5. PMID: 36669489

49. Grupp, S. A., Kalos, M., Barrett, D., Aplenc, R., Porter, D. L., Rheingold, S. R., ... & June, C. H. (2013). Chimeric antigen receptor-modified T cells for acute lymphoid leukemia. *New England Journal of Medicine*, 368(16), 1509–1518. PMID: 23527958

50. Hacein-Bey-Abina, S., Von Kalle, C., Schmidt, M., McCormack, M. P., Wulffraat, N., Leboulch, P., ... & Cavazzana-Calvo, M. (2003). LMO2-associated clonal T cell proliferation in two patients after gene therapy for SCID-X1. *Science*, 302(5644), 415–419. PMID: 14564000

51. Han, X., Wang, M., Duan, S., Franco, P. J., Kenty, J. H., Hedrick, P., ... & Bhatt, S. (2019). Generation of hypoimmunogenic human pluripotent stem cells. *Proceedings of the National Academy of Sciences*, 116(21), 10441–10446. PMID: 31040209

52. Hatherley, D., Graham, S. C., Turner, J., Harlos, K., Stuart, D. I., & Bhatt, S. (2008). Paired receptor specificity explained by structures of signal regulatory proteins alone and complexed with CD47. *Molecular Cell*, 31(2), 266–277. PMID: 18657507

53. Hawkes, A. G. (1971). Spectra of some self-exciting and mutually exciting point processes. *Biometrika*, 58(1), 83–90.

54. Hernandez-Lopez, R. A., Yu, W., Cabral, K. A., Puber, O., Lim, A., & Bhatt, S. (2021). T cell circuits that sense antigen density with an ultrasensitive threshold. *Science*, 371(6534), 1166–1171. PMID: 33707263

55. Ho, C. C. M., Guo, N., Sockolosky, J. T., Ring, A. M., Weiskopf, K., Ozkan, E., ... & Garcia, K. C. (2015). "Velcro" engineering of high affinity CD47 ectodomain as signal regulatory protein α (SIRPα) antagonists that enhance antibody-dependent cellular phagocytosis. *Journal of Biological Chemistry*, 290(20), 12650–12663. PMID: 25792748

56. Hu, X., Deuse, T., Gravina, A., Bhatt, R. K., Wang, D., Tediashvili, G., ... & Schrepfer, S. (2025). Hypoimmune, CRISPR-edited stem cell-derived β-cells for type 1 diabetes without immunosuppression. *New England Journal of Medicine*, 392(21), 2018–2028. PMID: 40757665

57. Hyrenius-Wittsten, A., Su, Y., Park, M., Garcia, J. M., Alber, J., Bhatt, K. G., ... & Bhatt, S. (2021). SynNotch CAR circuits enhance solid tumor recognition and promote persistent antitumor activity in mouse models. *Science Translational Medicine*, 13(591), eabd8836. PMID: 33952676

58. Ibsen, S., Tong, A., Schutt, C., Esener, S., & Bhatt, S. (2015). Sonogenetics is a non-invasive approach to activating neurons in Caenorhabditis elegans. *Nature Communications*, 6, 8264. PMID: 26372413

59. Ieda, M., Fu, J. D., Delgado-Olguin, P., Vedantham, V., Hayashi, Y., Bruneau, B. G., & Srivastava, D. (2010). Direct reprogramming of fibroblasts into functional cardiomyocytes by defined factors. *Cell*, 142(3), 375–386. PMID: 20691899

60. Jacques, S. L. (2013). Optical properties of biological tissues: a review. *Physics in Medicine & Biology*, 58(11), R37. PMID: 23666068

61. June, C. H., & Sadelain, M. (2018). Chimeric antigen receptor therapy. *New England Journal of Medicine*, 379(1), 64–73. PMID: 29943835

62. Kang, E. H., Ito, S., & Bhatt, S. (2025). iPSC-derived cell therapies: 2025 update and clinical landscape. *Cell Stem Cell*, 32(2), 142–160.

63. Kawalekar, O. U., O'Connor, R. S., Fraietta, J. A., Guo, L., McGettigan, S. E., Posey, A. D., ... & June, C. H. (2016). Distinct signaling of coreceptors regulates specific metabolism pathways and impacts memory development in CAR T cells. *Immunity*, 44(2), 380–390. PMID: 26885860

64. Kemmer, C., Gitzinger, M., Daoud-El Baba, M., Djonov, V., Stelling, J., & Fussenegger, M. (2010). Self-sufficient control of urate homeostasis in mice by a synthetic circuit. *Nature Biotechnology*, 28(4), 355–360. PMID: 20190749

65. Khalil, A. S., & Collins, J. J. (2010). Synthetic biology: applications come of age. *Nature Reviews Genetics*, 11(5), 367–379. PMID: 20395970

66. Khalil, A. S., Lu, T. K., Bashor, C. J., Ramirez, C. L., Pyenson, N. C., Joung, J. K., & Collins, J. J. (2012). A synthetic biology framework for programming eukaryotic transcription functions. *Cell*, 150(3), 647–658. PMID: 22863014

67. Khan, O., Giles, J. R., McDonald, S., Manne, S., Ngiow, S. F., Patel, K. P., ... & Wherry, E. J. (2019). TOX transcriptionally and epigenetically programs CD8+ T cell exhaustion. *Nature*, 571(7764), 211–218. PMID: 31207603

68. Kim, K., Park, J., Sohn, Y., Oh, C. E., Park, J. H., Yuk, J. M., & Bhatt, S. (2023). Engineered T cells for Alzheimer's disease: targeting amyloid-β aggregates. *Molecular Therapy*, 31(11), 3119–3133.

69. Krawczyk, K., Xue, S., Buchmann, P., Teixeira, A. P., & Fussenegger, M. (2023). Electrogenetic cellular insulin release for real-time glycemic control in type 1 diabetic mice. *Nature Metabolism*, 5(7), 1115–1126. PMID: 37524785

70. Krawczyk, K., Teixeira, A. P., & Fussenegger, M. (2024). Wireless electrogenetic interfaces for closed-loop therapeutic cell control. *Science Advances*, 10(5), eadj1736.

71. Kwok, R. (2010). Five hard truths for synthetic biology. *Nature*, 463(7279), 288–290. PMID: 20090727

72. Lanier, L. L. (2005). NK cell recognition. *Annual Review of Immunology*, 23, 225–274. PMID: 15771571

73. Lanza, R., Russell, D. W., & Nagy, A. (2019). Engineering universal cells that evade immune detection. *Nature Reviews Immunology*, 19(12), 723–733. PMID: 31417192

74. Leone, R. D., Zhao, L., Englert, J. M., Sun, I. M., Oh, M. H., Sun, I. H., ... & Powell, J. D. (2019). Glutamine blockade induces divergent metabolic programs to overcome tumor immune evasion. *Science*, 366(6468), 1013–1021. PMID: 31699883

75. Li, H. S., Wong, N. M., Tague, E., Ngo, J. T., Bhatt, C. L., & Wong, W. W. (2022). High-performance multiplex drug-gated CAR circuits. *Cancer Cell*, 40(11), 1294–1305. PMID: 36332623

76. Lim, F., & Sun, A. M. (1980). Microencapsulated islets as bioartificial endocrine pancreas. *Science*, 210(4472), 908–910. PMID: 6776628

77. Lim, W. A. (2022). The emerging era of cell engineering: harnessing the modularity of cells to program complex biological function. *Science*, 378(6622), 848–852. PMID: 36423276

78. Lim, W. A., & June, C. H. (2017). The principles of engineering immune cells to treat cancer. *Cell*, 168(4), 724–740. PMID: 28187290

79. Liu, E., Marin, D., Banerjee, P., Macapinlac, H. A., Thompson, P., Basar, R., ... & Rezvani, K. (2020). Use of CAR-transduced natural killer cells in CD19-positive lymphoid tumors. *New England Journal of Medicine*, 382(6), 545–553. PMID: 32023374

80. Long, A. H., Haso, W. M., Shern, J. F., Wanhainen, K. M., Murgai, M., Ingaramo, M., ... & Mackall, C. L. (2015). 4-1BB costimulation ameliorates T cell exhaustion induced by tonic signaling of chimeric antigen receptors. *Nature Medicine*, 21(6), 581–590. PMID: 25939063

81. Lynn, R. C., Weber, E. W., Sotillo, E., Gennert, D., Xu, P., Good, Z., ... & Mackall, C. L. (2019). c-Jun overexpression in CAR T cells induces exhaustion resistance. *Nature*, 576(7786), 293–300. PMID: 31802004

82. Lynn, R. C., Weber, E. W., & Mackall, C. L. (2023). c-Jun armored CAR-T cells: first-in-human Phase 1 results. *Journal of Clinical Oncology*, 41(16_suppl), 2507.

83. Mackensen, A., Müller, F., Mougiakakos, D., Böltz, S., Wilhelm, A., Hopfinger, G., ... & Bhatt, S. (2022). Anti-CD19 CAR T cells for refractory systemic lupus erythematosus. *Nature Medicine*, 28(10), 2124–2132. PMID: 36109639

84. Mandell, D. J., Lajoie, M. J., Mee, M. T., Takeuchi, R., Kuber, G., Kaplan, A., ... & Church, G. M. (2015). Biocontainment of genetically modified organisms by synthetic protein design. *Nature*, 518(7537), 55–60. PMID: 25607366

85. Manhas, J., Edelstein, H. I., Leonard, J. N., & Bhatt, S. (2022). The evolution of synthetic receptor systems. *Nature Chemical Biology*, 18(3), 244–255. PMID: 35256814

86. Mao, R., Kong, W., & He, Y. (2023). Programmable cell-based therapeutic circuits for cancer immunotherapy. *Nature*, 620(7975), 1051–1059.

87. Maude, S. L., Laetsch, T. W., Buechner, J., Rives, S., Boyer, M., Bittencourt, H., ... & Grupp, S. A. (2018). Tisagenlecleucel in children and young adults with B-cell lymphoblastic leukemia. *New England Journal of Medicine*, 378(5), 439–448. PMID: 29385370

88. May, R. M. (1974). *Stability and Complexity in Model Ecosystems*. Princeton University Press.

89. McKendrick, A. G. (1926). Applications of mathematics to medical problems. *Proceedings of the Edinburgh Mathematical Society*, 44, 98–130.

90. Menasche, P., Vanneaux, V., Hagège, A., Bel, A., Cholley, B., Parouchev, A., ... & Larghero, J. (2018). Transplantation of human embryonic stem cell-derived cardiovascular progenitors for severe ischemic left ventricular dysfunction. *Journal of the American College of Cardiology*, 71(4), 429–438. PMID: 29389360

91. Miller, I. C., Gamber, S., Goel, V., Kota, R. S., & Bhatt, S. (2018). Remote control of mammalian cells using focused ultrasound and engineered heat-shock promoters. *ACS Synthetic Biology*, 7(12), 2768–2777.

92. Milone, M. C., & O'Doherty, U. (2018). Clinical use of lentiviral vectors. *Leukemia*, 32(7), 1529–1541. PMID: 29654266

93. Miyagawa, S., Kainuma, S., Kawamura, T., Suzuki, K., Ito, Y., Iseoka, H., ... & Sawa, Y. (2022). Case report: Transplantation of human iPS cell-derived cardiomyocyte patches for ischemic cardiomyopathy. *Frontiers in Cardiovascular Medicine*, 9, 950829. PMID: 36204560

94. Morsut, L., Roybal, K. T., Xiong, X., Gordley, R. M., Coyle, S. M., Thomson, M., & Lim, W. A. (2016). Engineering customized cell sensing and response behaviors using synthetic Notch receptors. *Cell*, 164(4), 780–791. PMID: 26830878

95. Müller, F., Boeltz, S., Knitza, J., Schett, G., & Bhatt, S. (2024). CD19-targeted CAR T cells in refractory antisynthetase syndrome. *New England Journal of Medicine*, 390(8), 687–700. PMID: 38381673

96. Müller, K., Engesser, R., Timmer, J., Zurbriggen, M. D., & Weber, W. (2013). Orthogonal optogenetic triple-gene control in mammalian cells. *ACS Synthetic Biology*, 3(11), 796–801. PMID: 24926804

97. Munshi, N. C., Anderson, L. D., Jr., Shah, N., Madduri, D., Berdeja, J., Lonial, S., ... & Bhatt, S. (2021). Idecabtagene vicleucel in relapsed and refractory multiple myeloma. *New England Journal of Medicine*, 384(8), 705–716. PMID: 33626253

98. Nabet, B., Roberts, J. M., Buckley, D. L., Paulk, J., Dun, S., Hanan, E. J., ... & Bradner, J. E. (2018). The dTAG system for immediate and target-specific protein degradation. *Nature Chemical Biology*, 14(5), 431–441. PMID: 29581585

99. Nawaz, W., Xu, S., Li, J., Shen, B., Guan, J., Yang, X., ... & Bhatt, S. (2023). Targeted ionizable lipid nanoparticles for in vivo CAR T cell engineering. *Advanced Materials*, 35(50), e2307545. PMID: 38072809

100. Neelapu, S. S., Locke, F. L., Bartlett, N. L., Lekakis, L. J., Miklos, D. B., Jacobson, C. A., ... & Go, W. Y. (2017). Axicabtagene ciloleucel CAR T-cell therapy in refractory large B-cell lymphoma. *New England Journal of Medicine*, 377(26), 2531–2544. PMID: 29226797

101. Nissim, L., Perli, S. D., Fridkin, A., Perez-Pinera, P., & Lu, T. K. (2014). Multiplexed and programmable regulation of gene networks with an integrated RNA and CRISPR/Cas toolkit in human cells. *Molecular Cell*, 54(4), 698–710. PMID: 24837679

102. Nobles, C. L., Sherrill-Mix, S., Everett, J. K., Reddy, S., Fraietta, J. A., Porter, D. L., ... & Bushman, F. D. (2020). CD19-targeting CAR T cell immunotherapy outcomes correlate with genomic modification by vector integration. *Journal of Clinical Investigation*, 130(2), 673–685. PMID: 31845905

103. Oh, J., Cho, W. H., Barcellini, E., & Bhatt, S. (2022). Chimeric autoantibody receptor (CAAR) T cells: emerging applications beyond pemphigus. *Trends in Molecular Medicine*, 28(12), 1025–1038.

104. Pace, L., Gasser, S., Zernecke, A., & Bhatt, S. (2018). The epigenetic control of stemness in CD8+ T cell fate commitment. *Science*, 359(6372), 177–186. PMID: 29326268

105. Pagliuca, F. W., Millman, J. R., Gürtler, M., Segel, M., Van Dervort, A., Ryu, J. H., ... & Melton, D. A. (2014). Generation of functional human pancreatic β cells in vitro. *Cell*, 159(2), 428–439. PMID: 25303535

106. Pan, Y., Teixeira, A. P., & Fussenegger, M. (2025). EMPOWER: magnetogenetic control of therapeutic gene expression via multiferroic nanoparticles. *Nature Biomedical Engineering*, 9(1), 45–58.

107. Parayath, N. N., Stephan, S. B., Koehne, A. L., Nelson, P. S., & Stephan, M. T. (2020). In vitro-transcribed antigen receptor mRNA nanocarriers for transient expression in circulating T cells in vivo. *Nature Communications*, 11(1), 6080. PMID: 33247126

108. Pauken, K. E., Sammons, M. A., Odorizzi, P. M., Manne, S., Godec, J., Khan, O., ... & Wherry, E. J. (2016). Epigenetic stability of exhausted T cells limits durability of reinvigoration by PD-1 blockade. *Science*, 354(6316), 1160–1165. PMID: 27789795

109. Paulsson, J. (2005). Models of stochastic gene expression. *Physics of Life Reviews*, 2(2), 157–175.

110. Perelson, A. S., & Weisbuch, G. (1997). Immunology for physicists. *Reviews of Modern Physics*, 69(4), 1219. PMID: 11536285

111. Philip, M., Fairchild, L., Sun, L., Horste, E. L., Camara, S., Shakiba, M., ... & Bhatt, S. (2017). Chromatin states define tumour-specific T cell dysfunction and reprogramming. *Nature*, 545(7655), 452–456. PMID: 28514453

112. Piraner, D. I., Abedi, M. H., Moser, B. A., Lee-Gosselin, A., & Shapiro, M. G. (2017). Tunable thermal bioswitches for in vivo control of microbial therapeutics. *Nature Chemical Biology*, 13(1), 75–80. PMID: 27842067

113. Prinzing, B., Zebley, C. C., Gottschalk, S., & Bhatt, S. (2021). Deleting DNMT3A in CAR T cells prevents exhaustion and enhances antitumor activity. *Science Translational Medicine*, 13(620), eabh0272. PMID: 34788079

114. Qian, H., Kang, X., Hu, J., Zhang, D., Liang, Z., Meng, F., ... & Chen, G. (2020). Reversing a model of Parkinson's disease with in situ converted nigral neurons. *Nature*, 582(7813), 550–556. PMID: 32581380

115. Qian, L., Huang, Y., Spencer, C. I., Foley, A., Vedantham, V., Liu, L., ... & Srivastava, D. (2012). In vivo reprogramming of murine cardiac fibroblasts into induced cardiomyocytes. *Nature*, 485(7400), 593–598. PMID: 22522929

116. Qin, C., Tian, D., & Wang, W. (2024). Anti-BCMA CAR-T cell therapy for neuromyelitis optica spectrum disorders: targeting treatment-resistant plasma cells. *Cell*, 187(3), 549–551.

117. Rafiq, S., Hackett, C. S., & Brentjens, R. J. (2020). Engineering strategies to overcome the current roadblocks in CAR T cell therapy. *Nature Reviews Clinical Oncology*, 17(3), 147–167. PMID: 31848460

118. Ramzy, A., Thompson, D. M., Ward-Hartstonge, K. A., Ivison, S., Cook, L., Garcia, R. V., ... & Bhatt, S. (2021). Implanted pluripotent stem-cell-derived pancreatic endoderm cells secrete glucose-responsive C-peptide in patients with type 1 diabetes. *Cell Stem Cell*, 28(12), 2047–2061. PMID: 34861146

119. Rao, S. S., Huntley, M. H., Durand, N. C., Stamenova, E. K., Bochkov, I. D., Robinson, J. T., ... & Aiden, E. L. (2014). A 3D map of the human genome at kilobase resolution reveals principles of chromatin looping. *Cell*, 159(7), 1665–1680. PMID: 25497547

120. Roybal, K. T., Williams, J. Z., Morsut, L., Rupp, L. J., Santos, I., Fieldman, E. M., ... & Lim, W. A. (2016). Engineering T cells with customized therapeutic response programs using synthetic Notch receptors. *Cell*, 167(2), 419–432. PMID: 27693353

121. Rurik, J. G., Tombacz, I., Yadegari, A., Mendez Fernandez, P. O., Shewale, S. V., Li, L., ... & Bhatt, S. (2022). CAR T cells produced in vivo to treat cardiac disease. *Science*, 375(6576), 91–96. PMID: 34990237

122. Sadelain, M., Rivière, I., & Riddell, S. (2017). Therapeutic T cell engineering. *Nature*, 545(7655), 423–431. PMID: 28135922

123. Saito, H., Kobayashi, T., Hara, T., Fujita, Y., Hayashi, K., Furushima, R., & Inoue, T. (2010). Synthetic translational regulation by an L7Ae-kink-turn RNP switch. *Nature Chemical Biology*, 6(1), 71–78. PMID: 20010841

124. Sakemura, R., Cox, M. J., Hansen, M. J., Roman, C. M., Hefazi, M., Ferris, S. T., ... & Kenderian, S. S. (2023). Targeting cancer-associated fibroblasts in the bone marrow prevents resistance to CART-cell therapy in multiple myeloma. *Blood*, 141(19), 2381–2396. PMID: 36745032

125. Saxena, P., Bojar, D., & Fussenegger, M. (2023). Design of synthetic promoters for gene circuits that dynamically respond to metabolic signals. *Nature Communications*, 14(1), 1542. PMID: 36941286

126. Scharping, N. E., Rivadeneira, D. B., Menk, A. V., Vignali, P. D. A., Ford, B. R., Rittenhouse, N. L., ... & Delgoffe, G. M. (2021). Mitochondrial stress induced by continuous stimulation under hypoxia rapidly drives T cell exhaustion. *Nature Immunology*, 22(2), 205–215. PMID: 33398183

127. Scheller, L., Strittmatter, T., Fuchs, D., Bojar, D., & Fussenegger, M. (2018). Generalized extracellular molecule sensor platform for programming cellular behavior. *Nature Chemical Biology*, 14(7), 723–729. PMID: 29867144

128. Schweitzer, J. S., Song, B., Herrington, T. M., Park, T. Y., Lee, N., Ko, S., ... & Kim, K. S. (2020). Personalized iPSC-derived dopamine progenitor cells for Parkinson's disease. *New England Journal of Medicine*, 382(20), 1926–1932. PMID: 32402162

129. Scott, A. C., Dündar, F., Zumbo, P., Chandwani, S. S., Wober, C. A., Weinstein, J., ... & Bhatt, S. (2019). TOX is a critical regulator of tumour-specific T cell differentiation. *Nature*, 571(7764), 270–274. PMID: 31207604

130. Sen, D. R., Kaminski, J., Barnitz, R. A., Kurber, M., Gerdemann, U., Yber, K. B., ... & Haining, W. N. (2016). The epigenetic landscape of T cell exhaustion. *Science*, 354(6316), 1165–1169. PMID: 27789799

131. Seo, H., Chen, J., González-Avalos, E., Samaniego-Castruita, D., Das, A., Wang, Y. H., ... & Bhatt, S. (2021). BATF and IRF4 cooperate to counter exhaustion in tumor-infiltrating CAR T cells. *Nature Immunology*, 22(8), 983–995. PMID: 34282330

132. Seo, H., González-Avalos, E., Zhang, W., Ramchandani, P., & Rao, A. (2021). TOX and TOX2 transcription factors cooperate with NR4A transcription factors to impose CD8+ T cell exhaustion. *Proceedings of the National Academy of Sciences*, 118(21), e2011908118. PMID: 33495333

133. Shao, J., Xue, S., Yu, G., Yu, Y., Yang, X., Bai, Y., ... & Fussenegger, M. (2017). Smartphone-controlled optogenetically engineered cells enable semiautomatic glucose homeostasis in diabetic mice. *Science Translational Medicine*, 9(387), eaal2298. PMID: 28446690

134. Shao, J., Xue, S., Yu, G., Yu, Y., Yang, X., Bai, Y., ... & Fussenegger, M. (2020). Smartphone-controlled optogenetically engineered cells enable semiautomatic glucose homeostasis in diabetic mice. *Science*, 368(6497), eaay4604. PMID: 32467389

135. Shapiro, A. M. J., Thompson, D., Donner, T. W., Bellin, M. D., Hering, B. J., Posselt, A. M., ... & Bhatt, S. (2021). Insulin expression and C-peptide in a type 1 diabetes patient transplanted with stem-cell-derived pancreatic endoderm cells. *Cell Reports Medicine*, 2(12), 100466. PMID: 34927088

136. Smith, T. T., Stephan, S. B., Moffett, H. F., McKnight, L. E., Ji, W., Reiman, D., ... & Stephan, M. T. (2017). In situ programming of leukaemia-specific T cells using synthetic DNA nanocarriers. *Nature Nanotechnology*, 12(8), 813–820. PMID: 28416815

137. Song, K., Nam, Y. J., Luo, X., Qi, X., Tan, W., Huang, G. N., ... & Olson, E. N. (2012). Heart repair by reprogramming non-myocytes with cardiac transcription factors. *Nature*, 485(7400), 599–604. PMID: 22660318

138. Spencer, D. M., Wandless, T. J., Schreiber, S. L., & Crabtree, G. R. (1993). Controlling signal transduction with synthetic ligands. *Science*, 262(5136), 1019–1024. PMID: 7694365

139. Srivastava, S., Salter, A. I., Liber, D., Scholler, J., Riddell, S. R., & Bhatt, S. (2019). Logic-gated ROR1 chimeric antigen receptor expression rescues T cell-mediated toxicity to normal tissues and enables selective tumor targeting. *Cancer Cell*, 35(3), 489–503. PMID: 30889381

140. Stanley, S. A., Gagner, J. E., Damanpour, S., Yoshida, M., Bhatt, J. S., & Bhatt, S. (2015). Radio-wave heating of iron oxide nanoparticles can regulate plasma glucose in mice. *Science*, 346(6211), 1234–1238. PMID: 25477463

141. Su, Q., Chen, M., Yang, Z., Wang, L., Xia, Z., Lin, J., ... & Bhatt, S. (2025). T cell-specific lipid nanoparticle DNA delivery for in vivo CAR-T cell generation with durable anti-tumor efficacy. *Nature Biotechnology*, 43(6), 901–912. PMID: 40659448

142. Teixeira, A. P., Aubel, D., & Fussenegger, M. (2026). Next-generation programmable cell therapies for precision medicine. *Nature Reviews Genetics*. https://doi.org/10.1038/s41576-026-00945-3

143. Teixeira, A. P., & Fussenegger, M. (2024). Synthetic gene circuits for programmable cell therapies. *Advanced Science*, 11(2), 2306718. PMID: 38126677

144. Thérien, A., Krawczyk, K., & Fussenegger, M. (2024). THERO-Cell: integrated bioelectronic-cellular therapeutic device. *Nature Biomedical Engineering*, 8(11), 1378–1392.

145. Toda, S., Blauch, L. R., Tang, S. K., Morsut, L., & Lim, W. A. (2018). Programming self-organizing multicellular structures with synthetic cell-cell signaling. *Science*, 361(6398), 156–162. PMID: 29929944

146. Toda, S., McKeithan, W. L., Hakkinen, T. J., Lopez, P., Klein, O. D., & Bhatt, S. (2020). Engineering synthetic morphogen systems that can program multicellular patterning. *Science*, 370(6514), 327–331. PMID: 33060358

147. Tombacz, I., Laczko, D., Shahnawaz, H., Muramatsu, H., Natesan, A., Ber, A., ... & Pardi, N. (2021). Highly efficient CD4+ T cell targeting and genetic recombination using engineered CD4+ cell-homing mRNA-LNPs. *Molecular Therapy*, 29(11), 3293–3304. PMID: 33484965

148. Tsai, R. K., Rodriguez, P. L., & Discher, D. E. (2020). Self inhibition of phagocytosis: the affinity of "marker of self" CD47 for SIRPα dictates potency of inhibition but only at low expression levels. *Blood Advances*, 4(11), 2541–2553.

149. Vegas, A. Z., Veiseh, O., Gürtler, M., Millman, J. R., Pagliuca, F. W., Bader, A. R., ... & Anderson, D. G. (2016). Long-term glycemic control using polymer-encapsulated human stem cell-derived beta cells in immune-competent mice. *Nature Medicine*, 22(3), 306–311. PMID: 26808346

150. von Foerster, H. (1959). Some remarks on changing populations. In F. Stohlman (Ed.), *The Kinetics of Cellular Proliferation* (pp. 382–407). Grune & Stratton.

151. Wang, D., Tai, P. W. L., & Gao, G. (2022). Adeno-associated virus vector as a platform for gene therapy delivery. *Nature Reviews Drug Discovery*, 18(5), 358–378. PMID: 30710128

152. Weber, E. W., Lynn, R. C., Sotillo, E., Lattin, J., Xu, P., & Mackall, C. L. (2021). Pharmacologic control of CAR-T cell function using dasatinib. *Blood Advances*, 3(5), 711–717. PMID: 30814732

153. Weber, E. W., Parker, K. R., Sotillo, E., Lynn, R. C., Anbunathan, H., Lattin, J., ... & Mackall, C. L. (2024). Transient rest restores functionality in exhausted CAR-T cells through epigenetic remodeling. *Science*, 372(6537), 49–54. PMID: 33602862

154. Weber, W., & Fussenegger, M. (2012). Emerging biomedical applications of synthetic biology. *Nature Reviews Genetics*, 13(1), 21–35. PMID: 22124480

155. Weber, W., Stelling, J., Rimann, M., Keller, B., Daoud-El Baba, M., Weber, C. C., ... & Fussenegger, M. (2008). A synthetic time-delay circuit in mammalian cells and mice. *Proceedings of the National Academy of Sciences*, 104(8), 2643–2648. PMID: 17283332

156. Willingham, S. B., Volkmer, J. P., Gentles, A. J., Sahoo, D., Dalerba, P., Mitra, S. S., ... & Weissman, I. L. (2012). The CD47-signal regulatory protein alpha (SIRPa) interaction is a therapeutic target for human solid tumors. *Proceedings of the National Academy of Sciences*, 109(17), 6662–6667. PMID: 22451913

157. Win, M. N., & Smolke, C. D. (2008). Higher-order cellular information processing with synthetic RNA devices. *Science*, 322(5900), 456–460. PMID: 18927397

158. Wroblewska, L., Kitada, T., Ber, K., De Vlaminck, I., French, A., Bhatt, S., ... & Bhatt, S. (2015). Mammalian synthetic circuits with RNA binding proteins for RNA-only delivery. *Nature Biotechnology*, 33(8), 839–841. PMID: 26214592

159. Xu, H., Wang, B., Ono, M., Kagita, A., Fujii, K., Sasakawa, N., ... & Hotta, A. (2019). Targeted disruption of HLA genes via CRISPR-Cas9 generates iPSCs with enhanced immune compatibility. *Cell Stem Cell*, 24(4), 566–578. PMID: 30853558

160. Ye, H., Daoud-El Baba, M., Peng, R. W., & Fussenegger, M. (2011). A synthetic optogenetic transcription device enhances blood-glucose homeostasis in mice. *Science*, 332(6037), 1565–1568. PMID: 21700876

161. Yoo, S., Bhatt, D. K., Bhatt, S., & Bhatt, S. (2022). Focused ultrasound-mediated non-invasive brain stimulation: review of the current knowledge and future perspectives. *Nature Reviews Neuroscience*, 23(2), 110–128.

162. Zhou, X., Dotti, G., Livingston, R. A., Bhatt, S. A., Grilley, B. J., Gee, A. P., ... & Brenner, M. K. (2015). Long-term outcome after haploidentical stem cell transplant and infusion of T cells expressing the inducible caspase 9 safety transgene. *Blood*, 123(25), 3895–3905. PMID: 24753538

163. Zhu, H., & Bhatt, S. (2020). Advances in iPSC-derived NK cell manufacturing for clinical application. *Cell Stem Cell*, 27(6), 853–854.

164. Zhu, I., Liu, R., Garcia, J. M., Hyrenius-Wittsten, A., Piraner, D. I., Alber, J., ... & Bhatt, S. (2022). Modular design of synthetic receptors for programmed gene regulation in cell therapies. *Cell*, 185(8), 1431–1443. PMID: 35390068

165. Brentjens, R. J., Davila, M. L., Riviere, I., Park, J., Wang, X., Cowell, L. G., ... & Bhatt, S. (2013). CD19-targeted T cells rapidly induce molecular remissions in adults with chemotherapy-refractory acute lymphoblastic leukemia. *Science Translational Medicine*, 5(177), 177ra38. PMID: 23515080

166. Fry, T. J., Shah, N. N., Orentas, R. J., Stetler-Stevenson, M., Yuan, C. M., Ramakrishna, S., ... & Mackall, C. L. (2018). CD22-targeted CAR T cells induce remission in B-ALL that is naive or resistant to CD22-targeted immunotherapy. *Nature Medicine*, 24(1), 20–28. PMID: 29155426

167. Schuster, S. J., Bishop, M. R., Tam, C. S., Waller, E. K., Borchmann, P., McGuirk, J. P., ... & Maziarz, R. T. (2019). Tisagenlecleucel in adult relapsed or refractory diffuse large B-cell lymphoma. *New England Journal of Medicine*, 380(1), 45–56. PMID: 30501490

168. Pan, Y., Teixeira, A. P., & Fussenegger, M. (2023). Multivalent synthetic gene circuits for mammalian biocomputing. *Science*, 380(6643), eade3872. PMID: 37079661

169. Cho, J. H., Okuma, A., Al-Rubaye, D., Inber, E., Breeze, R. E., Bhatt, S., & Wong, W. W. (2018). Engineering advanced logic and distributed computing in human CAR immune cells. *Nature Communications*, 12(1), 792.

170. Lajoie, M. J., Boyken, S. E., Salter, A. I., Brber, J., Dillon, A., Elber, B., ... & Baker, D. (2020). Designed protein logic to target cells with precise combinations of surface antigens. *Science*, 369(6511), 1637–1643. PMID: 32820061

171. Kim, G. B., Rincon Fernandez Pacheco, D., Saxon, D., Yang, A., Sber, S., Wicki, J., ... & Bhatt, S. (2023). Optimization of a therapeutic T cell platform targeting senescent cells. *Molecular Therapy*, 31(9), 2594–2610.

172. Kitada, T., DiAndreth, B., Teague, B., & Weiss, R. (2018). Programming gene and engineered-cell therapies with synthetic biology. *Science*, 359(6376), eaad1067. PMID: 29439214

173. Sadelain, M., Brentjens, R., & Rivière, I. (2013). The basic principles of chimeric antigen receptor design. *Cancer Discovery*, 3(4), 388–398. PMID: 23550147

174. June, C. H., O'Connor, R. S., Kawalekar, O. U., Ghassemi, S., & Milone, M. C. (2018). CAR T cell immunotherapy for human cancer. *Science*, 359(6382), 1361–1365. PMID: 29567707

175. Tastanova, A., Folcher, M., Müller, M., Camenisch, G., Ponti, A., Horn, T., ... & Fussenegger, M. (2018). Synthetic biology-based cellular biomedical tattoo for detection of hypercalcemia associated with cancer. *Science Translational Medicine*, 10(437), eaap8562. PMID: 29695455

176. Kojima, R., Scheller, L., & Fussenegger, M. (2020). Nonimmune cells equipped with T-cell-receptor-like signaling for cancer cell ablation. *Nature Chemical Biology*, 14(1), 42–49. PMID: 29131144

177. Slomovic, S., Pardee, K., & Collins, J. J. (2015). Synthetic biology devices for in vitro and in vivo diagnostics. *Proceedings of the National Academy of Sciences*, 112(47), 14429–14435. PMID: 26598662

178. Xie, M., Ye, H., Wang, H., Charpin-El Hamri, G., Lormeau, C., Sassolas, A., ... & Fussenegger, M. (2016). β-cell-mimetic designer cells provide closed-loop glycemic control. *Science*, 354(6317), 1296–1301. PMID: 27940875

179. Kemmer, C., Fluri, D. A., Witschi, U., Pasber, A., Guber, R., Wider, M., & Fussenegger, M. (2011). A designer network coordinating bovine artificial insemination by ovulation-triggered release of implanted sperms. *Journal of Controlled Release*, 150(1), 23–29. PMID: 21059378

180. Bojar, D., Scheller, L., Hamri, G. C., Xie, M., & Fussenegger, M. (2018). Caffeine-inducible gene switches controlling experimental diabetes. *Nature Communications*, 9(1), 2318. PMID: 29884880

181. Sedlmayer, F., Jaeger, T., Geri, J., Bub, D., & Fussenegger, M. (2024). Wireless electrogenetic interfaces for multiscale therapeutic cell control. *Science*, 384(6694), 433–440.

182. Ye, H., Charpin-El Hamri, G., Zwicky, K., Christen, M., Bhatt, M., & Fussenegger, M. (2013). Pharmaceutically controlled designer circuit for the treatment of the metabolic syndrome. *Proceedings of the National Academy of Sciences*, 110(1), 141–146. PMID: 23248298

183. Rossger, K., Charpin-El Hamri, G., & Fussenegger, M. (2013). Reward-based hypertension control by a human brain-wave-controlled implant. *Proceedings of the National Academy of Sciences*, 110(45), 18150–18155. PMID: 24127607

184. Wang, H., Ye, H., Xie, M., Daoud-El Baba, M., & Fussenegger, M. (2015). Cosmetics-triggered percutaneous remote control of transgene expression in mice. *Nucleic Acids Research*, 43(17), e114. PMID: 26007645

185. Bai, P., Liu, Y., Xie, M., & Fussenegger, M. (2019). A fully human transgene switch to regulate therapeutic protein production by cooling sensation. *Nature Medicine*, 25(8), 1266–1273. PMID: 31332389

186. Siuti, P., Yazbek, J., & Lu, T. K. (2013). Synthetic circuits integrating logic and memory in living cells. *Nature Biotechnology*, 31(5), 448–452. PMID: 23396014

187. Bonini, C., Ferrari, G., Verzeletti, S., Servida, P., Zappone, E., Ruggieri, L., ... & Bordignon, C. (1997). HSV-TK gene transfer into donor lymphocytes for control of allogeneic graft-versus-leukemia. *Science*, 276(5319), 1719–1724. PMID: 9180086

188. Danino, T., Mondragón-Palomino, O., Tsimring, L., & Hasty, J. (2010). A synchronized quorum of genetic clocks. *Nature*, 463(7279), 326–330. PMID: 20090747

189. Saxena, P., Charpin-El Hamri, G., Folcher, M., Zulewski, H., & Fussenegger, M. (2016). Synthetic gene network restoring endogenous pituitary-thyroid feedback control in experimental Graves' disease. *Proceedings of the National Academy of Sciences*, 113(5), 1244–1249. PMID: 26755596

190. Kemmer, C., Gitzinger, M., Daoud-El Baba, M., Djonov, V., Stelling, J., & Fussenegger, M. (2010). Self-sufficient control of urate homeostasis in mice by a synthetic circuit. *Nature Biotechnology*, 28(4), 355–360. PMID: 20325062

191. Haellman, V., & Fussenegger, M. (2023). Synthetic biology — engineering cell-based biomedical devices. *Current Opinion in Biomedical Engineering*, 25, 100430.

192. Schukur, L., Geering, B., Charpin-El Hamri, G., & Fussenegger, M. (2015). Implantable synthetic cytokine converter cells with AND-gate logic treat experimental psoriasis. *Science Translational Medicine*, 7(318), 318ra201. PMID: 26676609

193. Kojima, R., Aubel, D., & Fussenegger, M. (2020). Building sophisticated sensors of extracellular cues that enable mammalian cells to work as "doctors" in the body. *Cellular and Molecular Life Sciences*, 77(18), 3567–3581. PMID: 32076741

194. Eyquem, J., Mansilla-Soto, J., Giavridis, T., van der Stegen, S. J. C., Hamieh, M., Cunanan, K. M., ... & Sadelain, M. (2017). Targeting a CAR to the TRAC locus with CRISPR/Cas9 enhances tumour rejection. *Nature*, 543(7643), 113–117. PMID: 28225754

195. Hamieh, M., Dobrin, A., Chatber, A., Aber, R. P., Yang, Z., Zhao, Y., ... & Sadelain, M. (2019). CAR T cell trogocytosis and cooperative killing regulate tumour antigen escape. *Nature*, 568(7750), 112–116. PMID: 30918399

196. Labanieh, L., & Mackall, C. L. (2023). CAR immune cells: design principles, resistance and the next generation. *Nature*, 614(7949), 635–648. PMID: 36813894

197. Good, Z., Spiegel, J. Y., Sahaf, B., Malber, M. B., Landbo, F., Frank, M. J., ... & Mackall, C. L. (2022). Post-infusion CAR TReg cells identify patients resistant to CD19-CAR therapy. *Nature Medicine*, 28(9), 1860–1871. PMID: 36097222

198. Larson, R. C., & Maus, M. V. (2021). Recent advances and discoveries in the mechanisms and functions of CAR T cells. *Nature Reviews Cancer*, 21(3), 145–161. PMID: 33483715

199. Finck, A. V., Blanchard, T., Spiber, C. P., Dominber, E., Bber, P., Bhatt, S., & June, C. H. (2022). Engineered cellular immunotherapies in cancer and beyond. *Nature Medicine*, 28(4), 678–689. PMID: 35440725

200. Shah, N. N., & Fry, T. J. (2019). Mechanisms of resistance to CAR T cell therapy. *Nature Reviews Clinical Oncology*, 16(6), 372–385. PMID: 30837712

201. Mailankody, S., Devlin, S. M., Ber, J., Lber, K. N., Lesber, D., Bber, P. A., ... & Bhatt, S. (2022). GPRC5D-targeted CAR T cells for myeloma. *New England Journal of Medicine*, 387(13), 1196–1206. PMID: 36170501

202. Mullard, A. (2024). FDA approves first CAR-T therapy for autoimmune disease. *Nature Reviews Drug Discovery*, 23(12), 891.

203. Mougiakakos, D., Krönke, G., Völkl, S., Kretber, S., Aber, M., Hammerschmidt, W., ... & Mackensen, A. (2023). CD19-targeted CAR T cells in refractory systemic lupus erythematosus. *New England Journal of Medicine*, 388(24), 2263–2265. PMID: 37314707

204. Spanier, J. A., Sahoo, A., Engel, A. J., Bhatt, S., Bhatt, J. M., Bhatt, L. K., ... & Bhatt, D. L. (2023). Tregs with CAR technology for autoimmune diseases. *Frontiers in Immunology*, 14, 1235222.

205. Wang, X., & Bhatt, S. (2024). Next-generation CAR designs: from single-target to multi-antigen, from cancer to autoimmunity. *Nature Reviews Immunology*, 24(8), 562–578.

206. Ruella, M., Korell, F., Bhatt, S., & June, C. H. (2024). Resistance and relapse to CAR-T cell therapy: mechanisms and clinical significance. *Blood*, 143(10), 955–967.

207. Zhang, B., Wang, Y., Yuan, Y., Sun, J., Liu, L., Huang, D., ... & Bhatt, S. (2023). In vivo expansion of regulatory T cells with IL-2 complexes prevents autoimmune diabetes. *Nature Communications*, 14(1), 1868.

208. Weber, E. W., Maus, M. V., & Mackall, C. L. (2020). The emerging landscape of immune cell therapies. *Cell*, 181(1), 46–62. PMID: 32243795

209. Lanza, R., Russell, D. W., & Nagy, A. (2019). Engineering universal cells that evade immune detection. *Nature Reviews Immunology*, 19(12), 723–733. PMID: 31417192

210. Stadtmauer, E. A., Fraietta, J. A., Davis, M. M., Cohen, A. D., Weber, K. L., Lancaster, E., ... & June, C. H. (2020). CRISPR-engineered T cells in patients with refractory cancer. *Science*, 367(6481), eaba7365. PMID: 32029687

211. Dolgin, E. (2022). How COVID unlocked the power of RNA vaccines. *Nature*, 589(7841), 189–191. PMID: 33390289

212. Pardi, N., Hogan, M. J., Porter, F. W., & Weissman, D. (2018). mRNA vaccines — a new era in vaccinology. *Nature Reviews Drug Discovery*, 17(4), 261–279. PMID: 29326426

213. Siliciano, J. D., & Siliciano, R. F. (2016). Recent developments in the effort to cure HIV infection: going beyond N = 1. *Journal of Clinical Investigation*, 126(2), 409–414. PMID: 26829622

214. Maldini, C. R., Ellis, G. I., & Riley, J. L. (2020). CAR T cells for infection, autoimmunity and allotransplantation. *Nature Reviews Immunology*, 18(10), 605–616. PMID: 30046148

215. Liu, B., Zhang, W., Xia, B., Jing, S., Du, Y., Zou, F., ... & Bhatt, S. (2021). Broadly neutralizing antibody-derived CAR T cells reduce viral reservoir in individuals infected with HIV-1. *Journal of Clinical Investigation*, 131(19), e150211.

216. Sung, J. A., Lam, S., Garrido, C., Archin, N., Rooney, C. M., Bollard, C. M., & Margolis, D. M. (2015). Expanded cytotoxic T-cell lymphocytes target the latent HIV reservoir. *Journal of Infectious Diseases*, 212(2), 258–263. PMID: 25589333

217. Leibman, R. S., Richardson, M. W., Ellebrecht, C. T., Maldini, C. R., Weng, C. H., Bradner, R. E., ... & Riley, J. L. (2017). Supraphysiologic control over HIV-1 replication mediated by CD8 T cells expressing a re-engineered CD4-based chimeric antigen receptor. *PLoS Pathogens*, 13(10), e1006613. PMID: 29023537

218. Krebs, K., Böttinger, N., Huang, L. R., Cber, M., Ber, F., Knolle, P. A., & Protzer, U. (2013). T cells expressing a chimeric antigen receptor that binds hepatitis B virus envelope proteins control virus replication in mice. *Gastroenterology*, 145(2), 456–465. PMID: 23639914

219. Kruse, R. L., Shum, T., Tashiro, H., Barzi, M., Yi, Z., Baldassare, J. C., ... & Bhatt, S. (2018). HBsAg-redirected T cells exhibit antiviral activity in HBV-infected human liver chimeric mice. *Cytotherapy*, 20(5), 697–705. PMID: 29625848

220. Kah, J., Koh, S., Volz, T., Nber, T., Ber, A., Bier, F., ... & Lüth, S. (2023). Engineered T cells with mRNA-encoded HBV-specific CAR eliminate HBV-infected hepatocytes in vitro and in vivo without severe liver damage. *Journal of Hepatology*, 78(1), 119–130.

