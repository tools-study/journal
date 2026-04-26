# Brain Reconstruction Review

## Abstract

The completion of synaptic-resolution wiring diagrams for the adult *Drosophila melanogaster* brain (Dorkenwald et al. 2024; Schlegel et al. 2024) and a one-cubic-millimetre volume of awake-mouse visual cortex (Bae et al. 2021; Ding et al. 2025) has carried structural connectomics from the 302-neuron baseline of *Caenorhabditis elegans* (White et al. 1986; Cook et al. 2019; Witvliet et al. 2021) to the threshold of complete vertebrate brain reconstruction. Two scaling barriers now dominate the path to a whole-mouse-brain (~7×10⁷ neurons, ~5×10⁵ mm³) connectome at synaptic resolution. First, an *evolutionary calibration gap*: the simplest extant nervous systems — those of Cnidaria — have never been mapped at synaptic resolution, so segmentation pipelines optimised on bilaterian morphology have no pre-bilaterian groundtruth to control for organism-specific bias. Second, an *algorithmic gating constraint*: per-micron segmentation error in flood-filling-network reconstructions (Januszewski et al. 2017) compounds along neurite arc length, and at present per-micron rates of ~10⁻² this error blockade makes whole-brain mouse axon traceability statistically impossible without proofreading person-years that exceed every connectomics consortium combined. We propose to reconstruct the entire nervous system of an adult *Hydra vulgaris* — ~5,600 neurons distributed across a transparent ~1-mm freshwater polyp with established transgenic tooling (Wittlieb et al. 2006), single-cell transcriptomic atlas (Cazet et al. 2023), and prior whole-animal calcium imaging that has already revealed three non-overlapping functional circuits (Dupre and Yuste 2017) — under a five-stage FUNC-EM-HYDRA pipeline that pairs pre-fixation light-sheet recording with high-pressure-frozen volume electron microscopy and correlative light–EM registration. Because a full *Hydra* connectome is small enough to be exhaustively groundtruthed by manual proofreading, it functions as a calibration anchor: the same pipeline used downstream on mouse cortex can be back-corrected against a complete-coverage reference. We formalise the gating constraint as six new mathematical results — a renewal-process error rate along neurites (F441), a mean-free-path-to-first-error fidelity bound (F442), a compound-Poisson degree-distribution-distortion theorem under split/merge events (F443), a cross-organism transfer-error decomposition (F444), a *Hydra*-as-zero-point calibration parameterisation (F445), and a submodular proofreading-allocation problem under finite human-hours budget (F446). These quantify why MICrONS-style proofreading person-years are dominated by long-range axons (Celii et al. 2025), establish a per-micron error-rate target of ~5×10⁻⁶ for whole-mouse fidelity, and convert the whole-mouse-brain roadmap from open-ended engineering target into a quantitatively bounded program. We further dedicate a section to the three remaining obstacles — light–EM correlative registration (Pierson et al. 2024; Hayashi et al. 2023), vertebrate-scale synapse detection (Buhmann et al. 2021), and multi-beam-SEM acquisition throughput (Maniates-Selvin et al. 2020; Pacureanu et al. 2019) — and identify open questions for further research.

---

## §1. Introduction

The map of every neuron and every synapse of an animal — its connectome — is not merely a structural inventory; it is the substrate of every computation the nervous system performs (White et al. 1986). Because a wiring diagram constrains the universe of possible neural dynamics, mapping connectomes has been one of the longest-running scientific aspirations in neuroscience, predating cellular neuroscience itself. Until 1986, the only complete connectome was a graph drawn from electron micrographs of a single nematode hermaphrodite, *Caenorhabditis elegans*: 302 neurons and approximately 7,000 chemical synapses (White et al. 1986). Three decades passed before serial-section electron microscopy and machine-learning-based segmentation made it possible to scale that effort beyond the worm (Helmstaedter et al. 2013; Kasthuri et al. 2015).

Three step-changes followed. The first was the demonstration in mammalian retina that dense, hundreds-of-neurons reconstructions could in principle reveal previously unknown wiring rules — for example the asymmetric direction-selectivity circuit of starburst amacrine cells (Briggman et al. 2011) and the inner-plexiform-layer connectome of approximately 950 cells (Helmstaedter et al. 2013). The second was the saturated reconstruction of a 1,500 µm³ volume of mouse neocortex, which itemised every axon, dendrite, mitochondrion, and synaptic vesicle in a queryable database and refuted Peters' rule of geometric synaptic prediction (Kasthuri et al. 2015). The third was the publication, between 2020 and 2025, of synaptic-resolution wiring diagrams for entire *Drosophila* brains: first the partial central-brain hemibrain of approximately 25,000 neurons (Scheffer et al. 2020), then the larval brain (Winding et al. 2022), then the adult female whole brain of approximately 139,255 neurons and 5×10⁷ synapses through the FlyWire consortium (Dorkenwald et al. 2024), with companion annotation, taxonomy, and graph-statistical analyses (Schlegel et al. 2024; Lin et al. 2024). The companion ventral nerve cord — the male MANC and female FANC datasets — completed the *Drosophila* sensorimotor circuit at synaptic resolution (Azevedo et al. 2024). In parallel, a multi-area, ~one-cubic-millimetre volume of awake mouse visual cortex was co-registered with calcium imaging of approximately 75,000 functionally characterised neurons through the MICrONS consortium (Bae et al. 2021), and the resulting structure–function dataset has begun to deliver general wiring-rule inferences (Ding et al. 2025) and motivated new automated proofreading and feature-extraction tools (Celii et al. 2025).

The next two scaling targets are the entire mouse brain and, eventually, a human cortical column. The mouse brain comprises approximately 7×10⁷ neurons in approximately 500 mm³ of tissue (Bae et al. 2021); at the standard 4×4×40 nm voxel size used for FlyWire and MICrONS, that target represents on the order of 10²¹ voxels — six orders of magnitude beyond MICrONS and three beyond the FlyWire whole-brain. Two distinct barriers separate the field from this target.

The first is an *evolutionary calibration gap*. Every connectome reconstructed to date has been from a bilaterian — from the nematode *C. elegans* through the annelid *Platynereis dumerilii*, the chordate *Ciona intestinalis* larva, the insect *Drosophila*, and the mammals — and segmentation pipelines, training sets, and synapse detectors are correspondingly tuned to bilaterian neural ultrastructure. The most basal extant animals with a centralised or non-centralised nervous system — Cnidaria, Ctenophora — have never been reconstructed at synaptic resolution. There is partial evidence that ctenophore neural-net architecture differs even at the cellular level from what bilaterians and cnidarians share, with continuous syncytial plasma membranes rather than discrete neurons (Burkhardt et al. 2023), and that neurons may have arisen at least two or three times independently across Metazoa (Moroz 2018). Without a pre-bilaterian groundtruth, segmentation pipelines have no anchor that controls for organism-specific bias when extrapolating to a vertebrate target.

The second is an *algorithmic gating constraint*. Flood-filling networks, the recurrent-CNN segmentation framework that has powered every recent large-scale reconstruction since 2017 (Januszewski et al. 2017), achieve mean error-free neurite-path lengths on the order of 1.1 mm in zebra-finch brain test sets (Januszewski et al. 2017) and approximately 0.8 mm in mouse cortex (Bae et al. 2021). With mouse pyramidal axons that span centimetres — and human axons that span tens of centimetres — error events accumulate exponentially along arc length. This is why the MICrONS proofreading person-years have been dominated by long-range axons (Celii et al. 2025), and why the field must drop the per-micron error rate by approximately 2,000-fold to make whole-mouse axon traceability statistically feasible.

This manuscript proposes to address both barriers together. We propose a complete synaptic-resolution reconstruction of the nervous system of an adult *Hydra vulgaris* — the simplest extant nervous system never mapped — paired with whole-animal pre-fixation light-sheet calcium imaging of single-neuron firing during behaviour. *Hydra* is a freshwater cnidarian polyp roughly 1 mm long, transparent, with approximately 5,600 neurons distributed in a nerve net plus a hypostomal cluster (Dupre and Yuste 2017; Cazet et al. 2023). It has been transgenically tractable since 2006 (Wittlieb et al. 2006) and has served as an in vivo testbed for whole-animal calcium imaging that revealed three anatomically non-overlapping but co-extensive functional networks engaged in distinct behaviours (Dupre and Yuste 2017; Lovas et al. 2021), as well as whole-body epitheliomuscular activity mapping (Szymanski et al. 2019). It has a freshly assembled chromosome-scale genome and an updated single-cell RNA-seq atlas with twelve transcriptionally distinct neuronal subtypes (Cazet et al. 2023; Klimovich et al. 2018; Klimovich et al. 2024). It regenerates its entire body and nervous system within days of dissociation (Lovas et al. 2021), enabling repeat-sample protocols. And it has never been reconstructed at synaptic resolution.

Reconstructing *Hydra* under the same pipeline used downstream for mouse provides a *full-coverage calibration anchor*: because its nervous system is small enough to be exhaustively groundtruthed by manual proofreading at modest cost, every segmentation, synapse-detection, and registration error in the pipeline becomes measurable. Those measurements then back-correct the pipeline before it is applied to bilaterian targets. This is the converse of the standard direction of model transfer in connectomics — usually one trains on a small bilaterian (typically *Drosophila*) and extrapolates outward — and has the advantage of being grounded in an organism whose neural population is small enough that *all* error modes are observable. Following the *Hydra* anchor, we develop a renewal-process formalism for long-range segmentation error compounding (F441–F446), back-derive a per-micron error-rate target of approximately 5×10⁻⁶ for whole-mouse fidelity, and demonstrate why current proofreading person-year budgets are dominated by long-range axons rather than soma-local arborisation. In a separate section we treat the three remaining whole-mouse barriers — light–EM correlative registration sub-voxel fidelity, vertebrate-scale synapse detection sensitivity-specificity trade-off, and multi-beam-SEM acquisition throughput — and identify open research directions in each.

The document is therefore three-part. First, *Hydra* is the right pre-bilaterian zero-point. Second, executing the same pipeline on *Hydra* and on mouse provides a calibration anchor that no current connectomics target can offer. Third, the bottleneck on the path to whole-mouse-brain reconstruction is long-range segmentation error compounding, which is mathematically tractable as a renewal-process fidelity bound and which the *Hydra* anchor allows us to back-correct.

---

## §2. State of the Art in Connectome Reconstruction (March 2026)

A useful way to organise the state of the field is by the size and phylogenetic position of the largest brain that has been reconstructed at synaptic resolution. The progression has been roughly factor-of-ten in neuron count per landmark since the late 1990s, with the curve steepening sharply since 2017 as flood-filling networks (Januszewski et al. 2017) replaced manual tracing as the segmentation primitive.

**Nematodes.** *C. elegans* has been reconstructed three times: the original White et al. (1986) hermaphrodite at 302 neurons, a substantially updated Cook et al. (2019) reconstruction that added the male-specific 91 neurons and quantitatively re-examined every synapse, and the developmental connectomes of Witvliet et al. (2021) at eight postnatal time points showing that approximately 40% of synapses change in strength or existence between birth and adulthood. A modern volume-EM pipeline for *C. elegans* sample preparation has been described (Mulcahy et al. 2018), and the worm's connectome has been adopted as both a reference graph for biological neural-network theory and a substrate for image-classification benchmarking.

**Insects.** *Drosophila* has been reconstructed at three life stages. The larval (Winding et al. 2022) brain at approximately 3,016 neurons and 548,000 synapses was the first complete insect brain. The adult hemibrain (Scheffer et al. 2020) at approximately 25,000 neurons and 10⁷ synapses covered most of the central brain in a partial volume. The full FlyWire whole-brain reconstruction (Dorkenwald et al. 2024) at 139,255 neurons and 5×10⁷ chemical synapses, with companion cell-type annotation of 8,453 cell types (Schlegel et al. 2024) and graph-statistical characterisation including motif analysis and rich-club identification (Lin et al. 2024), supersedes the hemibrain as the canonical insect-brain reference. Modular and hierarchical organisation in the *Drosophila* connectome has been independently characterised by community-detection algorithms (Kunin et al. 2022). The companion ventral nerve cord — male MANC and female FANC — adds another approximately 14,600 neurons and 4.5×10⁷ synapses (Azevedo et al. 2024), completing the *Drosophila* sensorimotor circuit. Cross-cutting tools for synaptic-partner identification (Buhmann et al. 2021) and neurotransmitter prediction directly from EM ultrastructure (Eckstein et al. 2020) have made the *Drosophila* connectome interrogable at the level of inferred functional sign.

**Vertebrate fragments.** Vertebrate connectomics is incomplete. *Larval zebrafish* (5–7 days post-fertilisation, ~10⁵ neurons) myelinated tract architecture has been mapped at whole-brain scale by serial-section EM (Hildebrand et al. 2017), and several local circuits have been reconstructed at synaptic resolution — for example the pretectal visual-motion circuit of approximately 208 neurons (Svara et al. 2022) — but no full vertebrate brain at synaptic resolution exists. *Mouse cortex* has been densely reconstructed in subvolumes ranging from 1,500 µm³ (Kasthuri et al. 2015) through 250×140×90 µm³ (Lee et al. 2016), through ~500,000 µm³ in layer 4 of barrel cortex (Motta et al. 2019), to one-cubic-millimetre with co-registered functional imaging through the MICrONS consortium (Bae et al. 2021). The MICrONS dataset has begun to yield wiring-rule inferences across cortical layers and areas (Ding et al. 2025) and has motivated new mesh-decomposition and automated proofreading frameworks, notably NEURD (Celii et al. 2025), which decomposes meshed neurons into compact graphs for automated merge-error correction. *Mouse retina* has been densely reconstructed at the inner-plexiform-layer scale (Helmstaedter et al. 2013; Briggman et al. 2011), with semi-automated segmentation toolkits such as SegEM having reduced reconstruction effort by approximately 100-fold relative to manual analysis (Berning et al. 2015). *Human cortex* has been reconstructed at petavoxel scale: a ~1 mm³ fragment of human temporal cortex containing approximately 57,000 cells, 230 mm of blood vessels, and 150 million synapses comprises 1.4 petabytes of imagery (Shapson-Coe et al. 2024). *Drosophila optic lobe* has been reconstructed in a male right hemisphere at FIB-SEM resolution, classifying approximately 53,000 neurons into 732 cell types (Nern et al. 2025).

**Pre-bilaterians.** No cnidarian or ctenophore has been reconstructed at synaptic resolution. The closest precedent is the syncytial nerve net of the ctenophore *Mnemiopsis*, whose subepithelial nerve net was demonstrated by volume EM and three-dimensional reconstruction to consist of cells with continuous plasma membranes — an architectural primitive that may differ fundamentally from cnidarian or bilaterian neurons (Burkhardt et al. 2023). Hydractinia, a colonial cnidarian, has had its single-cell atlas resolved at approximately 200,000 cells across stolons and zooids (Salamanca-Díaz et al. 2024), and the starlet anemone *Nematostella vectensis* has had its developmental cell atlas updated to 127 distinct cell states with 47 neuroglandular subtypes (Cole et al. 2024). *Hydra vulgaris* itself has been mapped at single-cell transcriptomic resolution (Cazet et al. 2023), at the level of its three functional circuits during behaviour (Dupre and Yuste 2017; Lovas et al. 2021), and at the level of its whole-body epitheliomuscular activity (Szymanski et al. 2019), but never at the level of its synaptic wiring graph.

**Methodological infrastructure.** Three classes of methodological work undergird every reconstruction. The first is the volume-EM acquisition stack — serial block-face SEM, focused-ion-beam SEM, and automated tape-collecting ultramicrotome (ATUM) SEM — whose comparative capabilities and imaging-throughput trade-offs have been catalogued (Titze and Genoud 2016; Kislinger et al. 2023). The second is correlative light–EM, which makes it possible to register fluorescence-imaged cells onto their EM-reconstructed counterparts; recent developments include cryo-CLEM (Pierson et al. 2024) and dynamics-to-structure CLEM (Marshall et al. 2023), and developmental-brain CLEM with ascorbate peroxidase staining (Hayashi et al. 2023). Genetically encoded EM tags include APEX peroxidase (Martell et al. 2012) and FerriTag, a chemically inducible electron-dense ferritin tag with approximately 10-nm labelling resolution (Clarke et al. 2018). The third is hard X-ray nano-holotomography, which images millimetre-scale volumes at sub-100-nm resolution non-destructively and has been used to reconstruct dense wiring in *Drosophila* and mouse nervous tissue (Pacureanu et al. 2019), with ongoing improvements at the European Synchrotron (Livingstone et al. 2025). High-contrast en bloc staining protocols specifically for whole-mouse-brain and human-brain samples have removed a key obstacle for whole-brain reconstruction (Song et al. 2023). Automated image transfer onto silicon wafers via GridTape has made transmission-EM acquisition affordable at the connectome scale (Maniates-Selvin et al. 2020).

The headline observation is that the algorithmic and acquisition machinery is now mature for invertebrates and for cubic-millimetre vertebrate volumes, but no complete vertebrate brain exists, no pre-bilaterian connectome exists, and no segmentation pipeline has been validated against an organism whose entire neural population is groundtruth-known.

---

## §3. *Hydra vulgaris* as the Pre-Bilaterian Reference

*Hydra vulgaris* (Pallas, 1766) is a small freshwater hydrozoan polyp typically 5–25 mm in length when extended, with a body plan organised along a single oral–aboral axis: a foot for adhesion, a tubular body column, a hypostome (mouth) at the oral pole, and a ring of usually 4–7 contractile tentacles surrounding the hypostome (Klimovich et al. 2018). It is one of the longest-studied animals in cell and developmental biology, dating to Trembley's 1744 *Mémoires* on freshwater polyps. Its four properties that matter for connectomics are:

**Phylogenetic position.** Cnidaria is the sister group to Bilateria, with a divergence date estimated at approximately 600 million years ago. Cnidarian nervous systems are accordingly an early-branching, anatomically simple neural architecture against which bilaterian elaborations can be compared. Within Cnidaria, *Hydra* sits in the medusozoan class Hydrozoa and is one of the molecularly best-characterised cnidarians, with chromosome-scale genome assemblies for both the AEP and 105 strains and an updated whole-animal single-cell RNA-seq atlas covering twelve neuronal subtypes (Cazet et al. 2023). Comparative cnidarian atlases — including the anthozoan *Nematostella vectensis* (Cole et al. 2024) and the colonial hydrozoan *Hydractinia symbiolongicarpus* (Salamanca-Díaz et al. 2024) — make it possible to triangulate which neural-cell-type properties are *Hydra*-specific versus cnidarian-general.

**Anatomical tractability.** An adult *Hydra* is approximately 1–5 mm in extended length and approximately 0.1–0.3 mm in body-column diameter. Its body wall is a two-cell-layer epithelium (ectoderm and endoderm) separated by a thin acellular mesoglea. Whole-animal volumes at standard EM resolution (4×4×30 nm voxel) therefore span on the order of 10¹³–10¹⁴ voxels per animal, which is approximately 10² smaller than the FlyWire whole-brain dataset and approximately 10⁷ smaller than a whole mouse brain. The animal is transparent and can be immobilised in 2% low-melt agarose for live imaging, or vitrified by high-pressure freezing within 200 ms of triggered behaviour for EM (Titze and Genoud 2016).

**Neuronal population.** Counts vary across protocols and strains, but a working figure is approximately 5,600 neurons per adult, divided between sensory, ganglion, and ganglion-derived neurons in the body column and a denser cluster at the hypostome (Dupre and Yuste 2017; Lovas et al. 2021). Single-cell transcriptomic atlases resolve at least twelve transcriptionally distinct neuronal subtypes in the body wall plus several additional subtypes in the hypostome, with markers including FMRFamide, RFamide, GLWamide, and Hym-176 neuropeptides (Cazet et al. 2023). The most recent comprehensive molecular and spatial characterisation, integrating single-cell RNA-seq, trajectory inference, and ATAC-seq on sorted neurons, has refined the canonical inventory to eight neuropeptide-defined neuron types resolving into 15 transcriptionally distinct subtypes with unique spatial distributions and morphologies (Little et al. 2025). Antimicrobial peptides are produced by a substantial fraction of *Hydra* neurons in the outer epithelial layer, an observation that connects neural function to host–microbiome regulation and is not paralleled in bilaterians (Klimovich et al. 2024).

**Functional architecture, established by Ca²⁺ imaging.** Whole-animal calcium imaging of transgenic *Hydra* expressing GCaMP under a pan-neuronal promoter has revealed that the nerve net, despite long-standing characterisation as anatomically diffuse, decomposes functionally into three non-overlapping circuits: a contraction-burst (CB) network engaged during longitudinal contractions, a rhythmic-potentials-1 (RP1) network engaged during light-driven elongations, and a rhythmic-potentials-2 (RP2) network engaged during radial contractions, with an additional small hypostomal network active during nodding behaviour (Dupre and Yuste 2017). When *Hydra* is dissociated into single cells and allowed to reaggregate over several days, calcium imaging shows that local synchronised neuronal ensembles form first, then synchronise hierarchically into the global functional networks — a process driven by strengthening of functional connections rather than by neurite outgrowth (Lovas et al. 2021). Whole-body epitheliomuscular activity decomposes into seven basic spatiotemporal patterns, with widely varying kinetics of initiation and wave-like propagation (Szymanski et al. 2019). The synthesis of these and related findings — that *Hydra*'s ensembles can be activated by neuropeptides, interact via cross-inhibition, and implement integrate-to-threshold algorithms — has been argued to expose general principles of neural computation accessible only in this minimal-complexity preparation (Yuste 2024). Together, these results constitute the strongest pre-existing functional groundtruth for any organism whose synaptic connectome is unknown.

**Genetic toolkit.** *Hydra* was the first cnidarian to be made stably transgenic, in 2006, via embryo microinjection (Wittlieb et al. 2006). The protocol has since been used to express EGFP and other fluorescent tags under cell-type-specific promoters, including pan-neuronal, sensory-neuron-specific, and ganglion-neuron-specific drivers. Pan-neuronal Tg(elavl3:GCaMP) lines suitable for whole-animal Ca²⁺ imaging are established laboratory standards (Dupre and Yuste 2017). The combination of transgenic GCaMP plus the recently developed APEX2- or FerriTag-derived genetically encoded EM contrast tags (Martell et al. 2012; Clarke et al. 2018) makes correlative light–EM directly tractable in *Hydra* at nm-scale labelling resolution.

**Regenerative capability as experimental advantage.** *Hydra* regenerates its entire body and nervous system from any tissue fragment, and reaggregates a complete functional nervous system from dissociated single cells within approximately one week (Lovas et al. 2021). This eliminates the sample-availability constraint that has historically slowed connectomics — there is no shortage of identical adult specimens. It also opens an unusual experimental design: a *pre/post-regeneration connectome comparison* in the same individual, which would directly test whether regenerated *Hydra* nervous systems converge on identical wiring or merely on identical functional decomposition. We treat this in §8 as an open question for further research.

**Predicted scientific dividends.** Beyond its function as a calibration anchor, the *Hydra* connectome is expected to test three first-principle hypotheses about pre-bilaterian neural architecture. First, the *random-nerve-net hypothesis*: cnidarian nervous systems have classically been described as having no fixed wiring, with each neuron contacting whatever neighbours its arborisation encounters. The complete connectome will quantify how far this is true — by measuring degree distribution, clustering coefficient, modularity, and rich-club organisation, and comparing them against equivalent statistics for *Drosophila* (Lin et al. 2024) and mouse cortex (Bae et al. 2021). Second, the *functional-anatomical correspondence hypothesis*: the three Dupre–Yuste functional networks (CB, RP1, RP2) should be identifiable as graph-theoretic communities in the connectome. If they are not — if the functional networks transcend connectivity — that result reframes how nerve nets compute. Third, the *non-bilaterian neural primitive hypothesis*: comparison with the syncytial nerve net of ctenophores (Burkhardt et al. 2023) will resolve whether cnidarian neurons are discrete cells with chemical synapses or whether some subset uses gap-junctional or syncytial coupling, with implications for the evolutionary origin of the neuron itself (Moroz 2018).

---

## §4. Proposed Experiment — FUNC-EM-HYDRA

We propose a five-stage pipeline, FUNC-EM-HYDRA, that delivers (i) the first complete pre-bilaterian connectome at synaptic resolution, (ii) a paired functional dataset capturing whole-animal single-neuron activity during behaviour in the *same individual* whose connectome is then reconstructed, and (iii) full-coverage groundtruth for downstream segmentation-pipeline calibration. Approximate timing per animal: 40 hours of light-sheet imaging plus behavioural sampling; 4 hours of high-pressure freezing and freeze-substitution; 6–8 weeks of multi-beam SEM acquisition; 6–12 months of segmentation, synapse detection, and proofreading. We propose n = 5 animals to characterise inter-individual variance.

### 4.1 Functional pre-EM imaging

Adult Tg(elavl3:GCaMP7f) *Hydra vulgaris* at the asexual budding-bearing stage are immobilised in 2% low-melt agarose at 18 °C and imaged on a dual-illumination light-sheet microscope at 488-nm excitation, 5 Hz volumetric acquisition, isotropic 1 µm voxel. Imaging continues for approximately 30 minutes during spontaneous behaviour and an additional approximately 30 minutes during evoked behaviour: light-driven elongations triggered by transient widefield 405-nm illumination (engaging the RP1 network), and mechanical-stimulus-triggered contractile bursts engaging the CB network. Single-neuron firing is extracted from the resulting 4D Ca²⁺ time-series by automated spot-detection plus deconvolution against the GCaMP7f kernel, and individual neurons are tracked across the full session using particle-tracking algorithms (Dupre and Yuste 2017; Lovas et al. 2021). Output: per-animal, per-neuron Ca²⁺ time-series with approximately 10⁴ behavioural events per animal. Fiducial nanoparticles (1-µm diameter quantum-dot-coated spheres) are co-injected into the body cavity at the start of imaging to enable later EM registration (cf. §4.5).

### 4.2 Cryofixation mid-behaviour

At a precise behavioural moment — the peak of a contractile burst, or mid-elongation — high-pressure freezing (HPF) is triggered within ≤200 ms of behaviour onset. The 200-ms latency is set by the dwell time of high-pressure-freezing chambers and is comparable to a single contractile-burst duration. Freeze-substitution into osmium tetroxide / uranyl acetate / lead citrate over 96 hours yields a sample whose ultrastructure preserves both the membrane integrity and the synaptic-vesicle distribution at the moment of freezing (Titze and Genoud 2016; Hayashi et al. 2023). Following freeze-substitution the sample is embedded in EPON resin in a flat-pack mould oriented for serial-section ATUM (cf. §4.3). High-contrast en bloc staining specifically optimised for whole-organ samples (Song et al. 2023) is applied during the freeze-substitution gradient.

### 4.3 Volume EM acquisition

Embedded *Hydra* are sectioned at 30-nm thickness on an automated tape-collecting ultramicrotome (ATUM) onto carbon-coated Kapton tape (Kislinger et al. 2023). Approximately 30,000–40,000 sections per animal, depending on body length, are collected onto silicon wafers. Multi-beam SEM acquisition (Zeiss MultiSEM 506 or equivalent, 91 beams, 4×4-nm pixel) proceeds at approximately 1 cm² per day per machine. Total volume per animal is approximately 1 mm × 0.3 mm × 0.3 mm, equating to ~9×10¹³ voxels at 4×4×30-nm voxel size. At single-machine throughput, raw acquisition takes approximately 6–8 weeks per animal; the project as a whole therefore consumes approximately 8 machine-months for n = 5 animals. As a complement, X-ray nano-holotomography (Pacureanu et al. 2019; Livingstone et al. 2025) of the same fixed sample is performed at sub-100-nm isotropic resolution prior to ultramicrotomy, providing a low-resolution skeleton that anchors the EM reconstruction during stitching and helps recover any sections lost or damaged during ATUM.

### 4.4 Automated segmentation and synapse detection

Volume EM stacks are aligned, denoised, and segmented by a flood-filling-network variant (Januszewski et al. 2017) retrained on a manually proofread *Hydra* subvolume of approximately 10⁹ voxels. Manual proofreading of this training subvolume — by experienced annotators with visualisation tooling adapted from the FlyWire community platform (Dorkenwald et al. 2020) — is the only manually intensive stage; downstream proofreading is automated through a NEURD-style mesh-decomposition framework (Celii et al. 2025). Synapse detection is performed by an Eckstein-style detector (Eckstein et al. 2020) and a Buhmann-style synaptic-partner-identification network (Buhmann et al. 2021), each retrained on the same proofread subvolume. Two distinguishing features of cnidarian synapses motivate retraining rather than direct transfer from *Drosophila*-trained models: (i) cnidarian chemical synapses lack the T-bar morphology characteristic of *Drosophila* presynapses, and (ii) gap-junctional coupling between epitheliomuscular cells is more prevalent than in bilaterians and must be detected with a parallel detector. Output: a per-animal directed graph of approximately 5,600 nodes (neurons) annotated with twelve canonical neuronal cell types (Cazet et al. 2023) and weighted by quantal synapse counts.

### 4.5 Light–EM correlative registration

The fiducial quantum-dot nanoparticles co-injected in §4.1 serve as multi-modal anchor points: they fluoresce in the light-sheet dataset and produce electron-dense scatter signatures in EM. Coordinate transformation between the two modalities is performed by a deformable B-spline registration whose parameter posterior is constrained by the fiducial point-correspondences (Hayashi et al. 2023; Pierson et al. 2024). To boost registration fidelity beyond fiducials alone, FerriTag-coupled (Clarke et al. 2018) APEX2-derived (Martell et al. 2012) genetically encoded contrast is introduced at the membrane of every neuron prior to fixation, providing dense correspondences across the full field of view. The registration error is evaluated against approximately 200 manually selected soma centroids per animal whose positions in light-sheet and in EM are independently identified.

**Validation criteria.** Three independent validations test the connectome:

1. *Cell-type identity.* Each reconstructed neuron is assigned a cell type from the twelve transcriptomically defined classes (Cazet et al. 2023) using a nearest-neighbour classifier on EM-derived morphological features. Cell-type identity must agree with the known spatial distributions of each class to within manual-curation tolerance.
2. *Functional decomposition.* The three CB, RP1, and RP2 functional networks identified by Dupre–Yuste calcium imaging (Dupre and Yuste 2017) should be predictable from the connectome by spectral graph clustering. If the predicted communities match the imaged communities at >90% per-neuron agreement, the connectome and the functional decomposition mutually validate.
3. *Inter-animal reproducibility.* Across n = 5 animals, the number of neurons per cell type, the per-cell-type degree distributions, and the modular structure should be conserved within bootstrap-derived confidence intervals. Variability beyond those intervals is interpreted as biological inter-individual variance, comparable to the substantial inter-individual connection-strength variability observed in *Drosophila* (Schlegel et al. 2024).

---

## §5. Mathematical Framework — The Long-Range Segmentation Fidelity Bound

We formalise the gating obstacle on whole-mouse-brain reconstruction — error compounding along long-range axons — as a renewal process.

### F441 — Renewal-process error rate along neurites

Let *s* ∈ [0, *L*] index arc length along a neurite of total length *L* (in microns), and let *λ*(*s*) be the instantaneous segmentation-error intensity — the per-micron probability of an error event (split or merge) at position *s*. Segmentation errors are generated by an inhomogeneous Poisson process with intensity *λ*(*s*); the expected number of errors over the neurite is

```math
\mathbb{E}[N_e(L)] = \int_{0}^{L} \lambda(s)\, ds.
```

Empirically, *λ*(*s*) is not constant. It is elevated near branch points (typical multiplicative factor *β*_b ≈ 5) and at axon-axon crossings or fascicle bundles (typical multiplicative factor *β*_x ≈ 10), reflecting the geometric ambiguity that flood-filling networks face when neurite cross-sections converge or diverge (Januszewski et al. 2017; Celii et al. 2025). Define the baseline rate *λ*_0 as the per-micron error rate over straight, isolated neurite segments. Then

```math
\lambda(s) = \lambda_0 \cdot \big[1 + (\beta_b - 1)\,\mathbf{1}_{B}(s) + (\beta_x - 1)\,\mathbf{1}_{X}(s)\big],
```

where **1**_B(*s*) and **1**_X(*s*) are indicator functions for branch points and crossings respectively.

For current MICrONS-class pipelines, *λ*_0 ≈ 10⁻²–10⁻³ /µm in mouse cortex (Bae et al. 2021), with hot-spot-corrected effective rates *λ*_eff in the high end of that range when integrated over realistic axonal arborisations.

### F442 — Mean-Free-Path-to-First-Error (MFPE) and the whole-mouse fidelity bound

For homogeneous *λ* (i.e. ignoring the branch-point and crossing terms), the mean free path to the first segmentation error is

```math
\ell^{*}(\lambda) = \frac{1}{\lambda},
```

and the probability of error-free segmentation over a length *L* is

```math
P_{\text{correct}}(L; \lambda) = e^{-\lambda L}.
```

For a typical mouse pyramidal-cell axon of length *L* ≈ 1 cm = 10⁴ µm and a current *λ* ≈ 10⁻² /µm (Bae et al. 2021), the per-axon probability of error-free reconstruction is

```math
P_{\text{correct}}(10^4\,\mu\text{m};\,10^{-2}/\mu\text{m}) = e^{-100} \approx 0.
```

A *whole-mouse fidelity criterion* fixes the per-axon error-free probability at some target *p* ∈ (0, 1) (a reasonable choice: *p* = 0.95) and asks what *λ* is required. Inverting the above expression gives the **F442 long-range fidelity bound**:

```math
\boxed{\;\lambda^{*} \;\le\; -\,\frac{\ln p}{L_{\max}}\;}
```

where *L*_max is the longest axon to be traced. For *p* = 0.95 and *L*_max = 10⁴ µm, *λ*\* ≤ 5.13 × 10⁻⁶ per µm — approximately a 2,000-fold improvement over current rates. For *L*_max = 10⁵ µm (some thalamocortical axons), the required *λ*\* drops by another order of magnitude, to approximately 5 × 10⁻⁷ per µm. This bound is the quantitative target that any segmentation algorithm must hit to enable end-to-end whole-mouse axon traceability.

### F443 — Compound-Poisson degree-distribution distortion

Consider the connectome as a directed graph whose vertex *i* has true in-degree *k*_i drawn from distribution *P*(*k*). Segmentation errors deform the observed graph in two ways: a *split* event divides one true neuron into two reconstructed pieces, halving the observed degree of the original neuron and creating a low-degree spurious neuron; a *merge* event fuses two true neurons into one reconstructed object, summing their degrees. Let *ε*_s be the per-neuron probability of a split error and *ε*_m the per-neuron probability of a merge error. The observed degree distribution becomes

```math
\hat{P}(k) = (1 - \varepsilon_m - \varepsilon_s)\, P(k) \;+\; \varepsilon_s \cdot \pi_s\!\left[P\right](k) \;+\; \varepsilon_m \cdot \pi_m\!\left[P\right](k),
```

where *π*_s[*P*](*k*) and *π*_m[*P*](*k*) are the operators that convolve *P* against the split-event size distribution (typically halving) and the merge-event partner distribution (a self-convolution of *P*) respectively.

Two consequences follow. First, splits inject mass into the low-*k* tail of *P̂*(*k*), and merges inject mass into the high-*k* tail; these biases are not symmetric and do not cancel. Second, if *P*(*k*) is heavy-tailed (scale-free with exponent *γ*, as has been observed in *Drosophila* connectome statistics for the rich-club neurons; Lin et al. 2024), even a 1% per-neuron error rate skews the empirically estimated *γ* by approximately 0.2 — sufficient to reverse conclusions about whether a connectome exhibits rich-club organisation. The *Hydra* anchor (§4) makes *ε*_s and *ε*_m measurable, because every true neuron is groundtruth-known.

### F444 — Cross-organism transfer-error decomposition

A segmentation pipeline trained on organism *X* and tested on organism *Y* incurs a transfer error that decomposes as

```math
\varepsilon_{X \to Y} = \varepsilon_{XX} + \beta \cdot D_{\mathrm{KL}}(P_X \,\Vert\, P_Y),
```

where *ε*_XX is the pipeline's in-distribution error on *X*, *D*_KL(*P*_X ‖ *P*_Y) is the Kullback–Leibler divergence between the voxel-feature distributions of organism *X* and organism *Y* (in the EM-image domain), and *β* > 0 is an organism-pair-specific sensitivity parameter that depends on the inductive bias of the pipeline. The interpretation is that the in-distribution error sets a floor, and the transfer penalty grows linearly in feature-distribution shift.

For practical use, *β* must be estimated. A natural three-organism estimation protocol:

1. Train on *Drosophila* (FlyWire). Test on *Drosophila*. Measure *ε*_DD.
2. Train on *Drosophila*. Test on *Hydra*. Measure *ε*_DH.
3. Compute *β*_DH = (*ε*_DH − *ε*_DD) / *D*_KL(*P*_D ‖ *P*_H).
4. Train on *Drosophila*. Test on mouse. Predict *ε*_DM = *ε*_DD + *β*_DH · *D*_KL(*P*_D ‖ *P*_M), under the assumption that *β*_DH and *β*_DM share a common pipeline-determined value.

The validity of step 4 — whether *β* is approximately invariant across target organisms — is itself a falsifiable prediction. If *β*_DH ≠ *β*_DM, the transfer-error decomposition needs an additional term, and the *Hydra* anchor accelerates its discovery.

### F445 — *Hydra*-as-zero-point calibration

Let *G*\* be the groundtruth *Hydra* connectome (assembled by exhaustive manual proofreading of the n = 5 animals; cf. §4). Let *Ĝ*(*pipeline*; *organism*) be the connectome reconstructed by a candidate pipeline applied to a given organism. Define a multiplicative pipeline-bias correction *κ*(*τ*, *g*) that depends on cell type *τ* and on neurite-geometry features *g* (radius, branching density, fascicle membership):

```math
\hat{P}_{\text{corrected}}(k\,\vert\,\tau, g) = \kappa(\tau, g) \cdot \hat{P}_{\text{raw}}(k\,\vert\,\tau, g),
```

with *κ*(*τ*, *g*) chosen to minimise the discrepancy between *Ĝ*(*pipeline*; *Hydra*) and *G*\* in *L*² norm:

```math
\hat{\kappa} = \arg\min_{\kappa} \;\sum_{\tau, g} \big\|\,\kappa(\tau, g)\,\hat{P}_{\text{raw}}(k\,\vert\,\tau, g) - P^{*}(k\,\vert\,\tau, g)\,\big\|_2^2.
```

The resulting *κ̂* is then applied to all downstream targets (*Drosophila*, mouse, ultimately human) under the *transfer-of-bias hypothesis*: pipeline-induced biases that are systematic in *Hydra* are systematic across organisms. The transfer-of-bias hypothesis is itself testable: applying *κ̂*(*τ*, *g*) derived from *Hydra* to a *Drosophila* test reconstruction and comparing against the FlyWire groundtruth (Dorkenwald et al. 2024; Schlegel et al. 2024) measures the cross-organism portability of the calibration. F445 is therefore both a calibration tool and a falsification protocol.

### F446 — Submodular proofreading allocation under finite human-hours budget

Let *B* be the total budget of human proofreader-hours available for a given reconstruction project. Let *i* index neurites (or neurite segments) under reconstruction, and let *x*_i ≥ 0 be the proofreader-hours allocated to neurite *i*. Define *p*_i(*x*_i) as the probability that neurite *i* is reconstructed without error after *x*_i hours of proofreading; this is empirically a saturating function of *x*_i, well approximated as *p*_i(*x*_i) = 1 − exp(−*α*_i *x*_i) with rate *α*_i depending on neurite length, branch density, and current segmentation quality. Let *v*_i be the *downstream connectivity impact* of neurite *i* — the number of synaptic partners or, more refined, the contribution of neurite *i* to the connectome's mutual information about behaviour. The optimal allocation problem is

```math
\max_{\{x_i \ge 0\}}\;\;\sum_i v_i\, p_i(x_i) \quad \text{subject to}\quad \sum_i x_i \le B.
```

The objective Σ *v*_i *p*_i(*x*_i) is monotone and concave in *x* (as *p*_i is concave and increasing), and the constraint set is a budget polytope. By the Karush–Kuhn–Tucker conditions, the optimum *x*\* satisfies, for all active *i*,

```math
v_i\,p_i'(x_i^{*}) = \mu, \quad \mu \ge 0,
```

with Lagrange multiplier *μ* set so that Σ *x*\*_i = *B*. For the exponential parameterisation, *p*_i'(*x*_i) = *α*_i exp(−*α*_i *x*_i), so the optimum is

```math
x_i^{*} = \max\!\left(0,\; \frac{1}{\alpha_i}\ln\!\frac{v_i\alpha_i}{\mu}\right).
```

Two operational consequences. First, neurites with high *v*_i *α*_i — i.e. high downstream impact and high marginal-fix-rate — receive disproportionate budget. This is why MICrONS-style proofreading person-years are dominated by long-range axons (Celii et al. 2025): long axons have high *v*_i (many downstream partners) and low *α*_i (slow fix rate), and the F446 KKT optimum still allocates them a substantial fraction of the budget despite their low marginal productivity. Second, when *α*_i and *v*_i are estimated from the *Hydra* anchor, F446 transitions from heuristic to provably optimal allocation.

### Summary of F441–F446

The six results above quantify, respectively: the local rate of segmentation error (F441), the global fidelity bound for whole-mouse-brain reconstruction (F442), the systematic distortion of degree distributions under split/merge errors (F443), the cross-organism transfer of segmentation error (F444), the *Hydra*-anchored bias correction that propagates downstream (F445), and the optimal allocation of finite proofreading budget (F446). Together, they convert the whole-mouse-brain reconstruction roadmap from an open-ended engineering target into a quantitatively bounded program with an explicit per-micron error-rate target (~5 × 10⁻⁶ /µm), an explicit calibration anchor (*Hydra*), and an explicit allocation algorithm.

---

## §6. Predicted Results

### 6.1 *Hydra* connectome graph properties

We predict, on the basis of partial single-cell transcriptomic data (Cazet et al. 2023) and prior Ca²⁺ imaging (Dupre and Yuste 2017; Lovas et al. 2021), that the *Hydra* connectome will display:

- **Modular but not random** topology: three principal communities corresponding to the CB, RP1, and RP2 networks plus a hypostomal cluster, with within-community connection density approximately 5–10× the across-community density.
- **Heavy-tailed but not scale-free** degree distribution: lognormal-like with mean degree ⟨*k*⟩ ≈ 8 and standard deviation σ_k ≈ 12, with no rich-club organisation comparable to the 30%-rich-club structure observed in *Drosophila* (Lin et al. 2024). The absence of a rich club, if confirmed, would be a structural correlate of the absence of a centralised brain.
- **High clustering coefficient** *C* ≈ 0.3–0.5, intermediate between random (0.001) and lattice (0.5–0.7), consistent with small-world architecture.
- **Twelve cell-type-specific connectivity profiles** matching the transcriptomic atlas (Cazet et al. 2023), with sensory neurons preferentially upstream of ganglion neurons and ganglion neurons preferentially upstream of effector epitheliomuscular cells.

Departures from these predictions will themselves be informative: a strictly random nerve net would falsify the long-standing conjecture that cnidarian behaviour requires structured connectivity, and a scale-free degree distribution would reveal pre-bilaterian rich-club organisation predating centralised brains.

### 6.2 Functional-anatomical correspondence

We predict that the three Dupre–Yuste networks will be recoverable from spectral graph clustering of the connectome at >90% per-neuron agreement (Dupre and Yuste 2017). This would be the first demonstration in any organism that whole-animal functional decomposition derived from Ca²⁺ imaging maps cleanly onto whole-animal synaptic-graph community structure. A failure to recover the three networks from connectivity alone would be diagnostically valuable: it would indicate that *Hydra* nerve-net function depends on diffuse modulation (e.g. neuropeptide release outside of synapses; Klimovich et al. 2024) more than on hard-wired synaptic connectivity, with consequences for how cnidarian — and perhaps early bilaterian — circuits are conceptualised.

### 6.3 Calibration constants for downstream targets

We predict that the *κ̂*(*τ*, *g*) function fit on *Hydra* (F445) will reduce reconstructed-vs-groundtruth degree-distribution discrepancy by approximately 5–10× when applied to the FlyWire (Dorkenwald et al. 2024) or MICrONS (Bae et al. 2021) test datasets, and will reduce the cross-organism transfer-error sensitivity *β* (F444) by a comparable factor. If the predicted reduction holds, the *Hydra*-calibrated pipeline becomes the recommended preprocessing step for any future invertebrate or vertebrate connectome reconstruction. If it does not hold, the transfer-of-bias hypothesis (cf. F445) is falsified and the *Hydra* anchor must be supplemented with additional cross-organism calibrations — perhaps via Hydractinia (Salamanca-Díaz et al. 2024) or *Nematostella* (Cole et al. 2024).

### 6.4 Quantitative target for whole-mouse-brain reconstruction

Combining F442 with the per-machine throughput of multi-beam SEM (~1 cm² per day; Maniates-Selvin et al. 2020) and the F446 KKT-optimal proofreading allocation, we project that whole-mouse-brain reconstruction at *p* = 0.95 per-axon fidelity requires a per-micron segmentation error rate of approximately 5×10⁻⁶ /µm, approximately 100 multi-beam-SEM machine-years for raw acquisition (or approximately 10 machine-years if X-ray nano-holotomography (Pacureanu et al. 2019; Livingstone et al. 2025) is used to skeletonise targeted subvolumes), and approximately 2,000 proofreader person-years even with NEURD-style automated proofreading (Celii et al. 2025) reducing manual burden by approximately 5×. These figures set explicit milestones against which any whole-mouse-brain consortium can be evaluated. Reductions in any of the three (per-micron error rate, acquisition throughput, automated proofreading multiplier) directly compound.

---

## §7. The Other Three Bottlenecks

Although §5 established long-range segmentation error compounding as the gating constraint on whole-mouse-brain reconstruction, three additional barriers will become rate-limiting once F442 has been satisfied. We treat each in turn.

### 7.1 Light–EM correlative registration sub-voxel fidelity

Functional connectomics — knowing which physically-imaged neuron in EM corresponds to which functionally-recorded one — requires deformable registration between two imaging modalities at sub-synaptic resolution. For *Hydra* and other small organisms, fiducial nanoparticles plus FerriTag-coupled (Clarke et al. 2018) APEX2 (Martell et al. 2012) staining can achieve approximately 10-nm correspondence resolution under cryo-CLEM protocols (Pierson et al. 2024). For mouse cortex, the problem is substantially harder: the brain expands, distorts, and shrinks during fixation in non-uniform ways, and the per-cell correspondences are sparse because functional imaging (typically 2-photon Ca²⁺) records only a subset of neurons at limited optical depth. Recent dynamics-to-structure CLEM pipelines (Marshall et al. 2023) and developmental-brain vCLEM with ascorbate peroxidase (Hayashi et al. 2023) have substantially advanced the field, but provable sub-voxel error bounds across an entire mouse cortex remain unestablished.

The mathematical structure of the problem is a constrained Bayesian inverse problem: given a set of fiducial point-correspondences {(*y*_i, *z*_i)} where *y* is a position in light-microscopy coordinates and *z* in EM coordinates, infer a deformation field *T*(·) on the volume such that *T*(*y*_i) ≈ *z*_i for all *i*, with priors on the smoothness and Jacobian of *T*. The posterior *P*(*T* | data) supports calibrated error bounds via the posterior covariance, and these bounds can in principle be back-propagated to per-neuron correspondence uncertainty. To our knowledge no current pipeline reports calibrated per-correspondence posteriors at the whole-cortex scale; closing this gap is a clear priority for vertebrate functional connectomics.

### 7.2 Vertebrate-scale synapse detection sensitivity-specificity trade-off

Synapse-detection networks trained on *Drosophila* electron-micrograph datasets (e.g. SynFul; Buhmann et al. 2021) achieve test-set F₁ scores of approximately 0.92 on the FlyWire data. The same architectures applied to mammalian volumes — where synapses lack T-bar morphology, are smaller (typically 0.2–0.4 µm vs. 0.5 µm in fly), and are more morphologically heterogeneous — drop to test-set F₁ ≈ 0.7 on mouse cortex test sets. Neurotransmitter-prediction networks face a similar transfer gap (Eckstein et al. 2020), although they tolerate it better because the underlying ultrastructural cues (vesicle morphology, postsynaptic density) are partly conserved.

The consequence of an F₁ ≈ 0.7 detector applied to a mouse-brain-scale connectome is severe. A vertex-degree distribution computed under detector false-positive rate *β*_FP and miss rate *β*_FN deviates systematically from the true distribution: hubs are inflated by *β*_FP-driven spurious in-edges, and low-degree neurons are deflated by *β*_FN-driven missed in-edges. The mathematical machinery of F443 applies directly to this distortion. The recommended path forward is per-cell-type detectors trained via active learning on a small but diverse mammalian groundtruth set, plus posterior calibration that returns synapse detections with confidence intervals rather than binary calls.

### 7.3 Multi-beam SEM acquisition throughput

A whole mouse brain at standard 4×4×40-nm voxel resolution comprises approximately 10²¹ voxels. At current 91-beam multi-beam SEM throughput of approximately 1 cm² per machine per day (Maniates-Selvin et al. 2020), the raw acquisition time for the entire brain is on the order of 100 machine-years. Two complementary acceleration paths exist.

The first is *raw throughput acceleration*: more beams per machine, faster pixel dwell times, better automation of section transfer. ATUM-derived pipelines have substantially reduced section-loss rates and enabled silicon-wafer mounting at scale (Kislinger et al. 2023), and high-contrast en bloc staining protocols specifically optimised for whole-organ samples (Song et al. 2023) have removed a key obstacle for sub-millimetre brain regions. Sample-preparation protocols for human-brain biopsies up to 2×2×2 mm volumes — combining immersion fixation, heavy-metal staining, and processing for excellent ultrastructural preservation including extracellular space — extend these advances toward clinically relevant volumes (Karlupia et al. 2023).

The second is *adaptive sampling*: instead of imaging the entire brain at the same resolution, image a coarse skeleton at low resolution (e.g. 100×100×100-nm voxels via X-ray nano-holotomography; Pacureanu et al. 2019; Livingstone et al. 2025) and then re-image targeted subvolumes at full resolution where dense reconstruction is required. The mathematical problem is multi-resolution allocation under the joint constraints of total-time budget and target-resolution-per-region — a class of problem closely related to the F446 proofreading-allocation submodular optimisation. Adaptive sampling could in principle reduce raw acquisition time by 5–10× without sacrificing connectivity reconstruction in the interesting subvolumes (the dense neuropil layers), at the cost of losing soma-and-axon-only resolution in the white-matter tracts.

A third, longer-horizon, possibility is denoising-based image-compression frameworks that reduce the storage burden of petabyte-scale connectome data by approximately an order of magnitude with minimal reconstruction-accuracy loss, which when combined with adaptive sampling enables a non-linear scaling of effective throughput per machine-day. The mature precedent here is the SegEM toolset for efficient semi-automated analysis of large 3D-EM datasets, which delivered approximately 100-fold speedup over manual analysis and approximately 10-fold over earlier automated tools at the time of its release (Berning et al. 2015), and the petavoxel human-cortex dataset of Shapson-Coe et al. (2024) demonstrates that the storage and curation burden has become as binding a constraint as raw acquisition.

---

## §8. Open Questions and Recommendations for Further Research

### 8.1 Generalisability of the *Hydra* calibration to vertebrates

The *Hydra*-as-zero-point calibration (F445) rests on the transfer-of-bias hypothesis: pipeline-induced biases that are systematic in *Hydra* are systematic across organisms. This hypothesis is testable, and if it fails we will need additional pre-bilaterian or invertebrate anchors. A natural sequential calibration would be *Hydra* → *Hydractinia* (Salamanca-Díaz et al. 2024) → *Nematostella* (Cole et al. 2024) → *Platynereis* → *Drosophila* (Dorkenwald et al. 2024) → *C. elegans* (Cook et al. 2019; Witvliet et al. 2021) → larval zebrafish (Hildebrand et al. 2017; Svara et al. 2022) → mouse cortex (Bae et al. 2021). The cumulative residuals across this sequence would parameterise a phylogenetically informed pipeline-bias model.

### 8.2 The pre-neural reference

If the hypothesis that neurons evolved independently in ctenophores versus cnidarians-plus-bilaterians (Burkhardt et al. 2023; Moroz 2018) is correct, then the *Hydra* calibration anchors only one of two independent neural lineages. A complementary calibration on a ctenophore — perhaps *Mnemiopsis leidyi* — would test whether the cnidarian-bilaterian neural primitive and the ctenophore syncytial-net primitive share calibration constants or not. If they do not, the pipeline-bias model has a phylogenetic discontinuity, which is itself a major scientific result.

A still more radical reference is *Trichoplax adhaerens* or a sponge species: animals without neurons. They would calibrate the cell-membrane and organelle-detection components of the pipeline against a substrate that lacks the very structures the pipeline was designed for, sharpening the boundary between organism-general and organism-specific bias.

### 8.3 Pre/post-regeneration connectome comparison

*Hydra* regenerates its full nervous system within approximately one week of dissociation (Lovas et al. 2021). Reconstructing the connectomes of one animal pre-dissociation and the same animal post-regeneration would test, for the first time, whether vertebrate-style developmental wiring rules apply at the cnidarian level: do regenerated nervous systems converge on identical wiring (down to per-neuron synaptic identity), or only on identical functional decomposition? The answer has implications for *Hydra* as a regenerative-medicine reference and for the broader question of how much of nervous-system architecture is genetically specified vs. emergent.

### 8.4 Online / continual segmentation during acquisition

Currently, segmentation begins after acquisition is complete. The whole-mouse-brain acquisition time of approximately 100 machine-years (see §6.4 and §7.3) is incompatible with this serial workflow: segmentation must run continuously during acquisition, with completed subvolumes available immediately for proofreading and downstream analysis. The mathematical problem is online learning under streaming volumetric input, with adaptive resolution and budget constraints. Recent automated-proofreading frameworks (Celii et al. 2025) are a step in this direction, but full continual-learning pipelines for connectomics are unestablished.

### 8.5 Synapse-by-synapse uncertainty quantification

Most existing connectome data products report binary synapse calls. F443 demonstrated that even small per-call errors propagate to systematic degree-distribution distortions. The recommended path is for synapse detectors to return calibrated posterior probabilities per synapse — and for downstream graph-theoretic analyses to propagate those uncertainties into the connectome's reported network statistics. Recent work on neurotransmitter prediction (Eckstein et al. 2020) provides a template for how per-synapse confidence can be reported and consumed by downstream analyses.

### 8.6 Cross-validation against reaggregation Hydra

Lovas et al. (2021) showed that *Hydra* dissociated into single cells reassembles a complete nervous system, with calcium-imaging-derived functional ensembles converging hierarchically over several days. A natural extension is to acquire EM connectomes at multiple time points during reaggregation — parallel to the Witvliet et al. (2021) developmental-time-series approach for *C. elegans* — yielding the first connectome time-series of nervous-system *de novo* assembly. The dynamical principles uncovered would directly inform engineering of regenerative neural circuits in higher organisms.

### 8.7 Intrinsic-excitability-based plasticity as confounder

Recent theoretical work has argued that ensemble formation may be driven not solely by Hebbian synaptic plasticity but additionally by changes in intrinsic neuronal excitability, with implications for how connectome-only inferences map to behaviour (Hansel et al. 2024). A *Hydra* connectome paired with its functional decomposition is the cleanest substrate on which to test the relative weight of synaptic-connectivity vs. intrinsic-excitability contributions to functional ensemble identity, because both can in principle be measured exhaustively in the same animal.

---

## §9. Conclusion

Connectomics has now reached the threshold at which the next decade will deliver complete vertebrate brains. The two dominant scaling barriers — an evolutionary calibration gap, and a long-range segmentation-error gating constraint — both admit attack from the same vector. Reconstructing the simplest extant nervous system never mapped — the ~5,600-neuron nerve net of *Hydra vulgaris* — provides a calibration anchor whose entirety can be groundtruthed by manual proofreading, against which the pipeline can be back-corrected before it is deployed at vertebrate scale. The renewal-process formalism of F441–F446 quantifies the per-micron error-rate target (~5 × 10⁻⁶ /µm) required for whole-mouse-brain fidelity, the systematic distortions in degree distributions induced by split and merge errors, the cross-organism transfer of pipeline bias, and the optimal allocation of finite proofreading budget. The *Hydra* anchor is the experimental key; the F441–F446 results are the analytical key. Together, they convert the whole-mouse-brain reconstruction roadmap from an open-ended engineering target into a quantitatively bounded program. Beyond mouse, the same calibration logic — pre-bilaterian zero-point plus phylogenetic sequence of intermediate anchors plus per-pipeline back-correction — extends naturally to non-human primates and to human cortex. The pre-bilaterian reference is the missing rung on the connectomics ladder.

---

## §10. References

Azevedo, Anthony, et al. "Connectomic reconstruction of a female *Drosophila* ventral nerve cord." *Nature* 631 (2024): 360–368.

Bae, J. Alexander, et al. "Functional connectomics spanning multiple areas of mouse visual cortex." *Nature* 598 (2021): 161–168.

Berning, Manuel, Kevin M. Boergens, and Moritz Helmstaedter. "SegEM: efficient image analysis for high-resolution connectomics." *Neuron* 87 (2015): 1193–1206.

Briggman, Kevin L., Moritz Helmstaedter, and Winfried Denk. "Wiring specificity in the direction-selectivity circuit of the retina." *Nature* 471 (2011): 183–188.

Buhmann, Julia M., et al. "Automatic detection of synaptic partners in a whole-brain *Drosophila* electron microscopy data set." *Nature Methods* 18 (2021): 771–774.

Burkhardt, Pawel, et al. "Syncytial nerve net in a ctenophore adds insights on the evolution of nervous systems." *Science* 380 (2023): 293–297.

Cazet, Jack F., et al. "A chromosome-scale epigenetic map of the *Hydra* genome reveals conserved regulators of cell state." *Genome Research* 33 (2023): 283–298.

Celii, Brendan, et al. "NEURD offers automated proofreading and feature extraction for connectomics." *Nature* 638 (2025): 943–952.

Clarke, Nicholas I., et al. "FerriTag is a new genetically-encoded inducible tag for correlative light-electron microscopy." *Nature Communications* 9 (2018): 2604.

Cole, Alison G., et al. "Updated single cell reference atlas for the starlet anemone *Nematostella vectensis*." *Frontiers in Zoology* 21 (2024): 8.

Cook, Steven J., et al. "Whole-animal connectomes of both *Caenorhabditis elegans* sexes." *Nature* 571 (2019): 63–71.

Ding, Zhuokun, et al. "Functional connectomics reveals general wiring rule in mouse visual cortex." *Nature* 640 (2025): 459–469.

Dorkenwald, Sven, et al. "FlyWire: online community for whole-brain connectomics." *Nature Methods* 19 (2022): 119–128.

Dorkenwald, Sven, et al. "Neuronal wiring diagram of an adult brain." *Nature* 634 (2024): 124–138.

Dupre, Christophe, and Rafael Yuste. "Non-overlapping neural networks in *Hydra vulgaris*." *Current Biology* 27 (2017): 1085–1097.

Eckstein, Nils, et al. "Neurotransmitter classification from electron microscopy images at synaptic sites in *Drosophila melanogaster*." *Cell* 187 (2024): 2574–2594.

Hansel, Christian, et al. "Neural ensembles: role of intrinsic excitability and its plasticity." *Frontiers in Cellular Neuroscience* 18 (2024): 1440588.

Hayashi, Shu, et al. "Correlative light and volume electron microscopy to study brain development." *Microscopy* 72 (2023): 297–306.

Helmstaedter, Moritz, et al. "Connectomic reconstruction of the inner plexiform layer in the mouse retina." *Nature* 500 (2013): 168–174.

Hildebrand, David Grant Colburn, et al. "Whole-brain serial-section electron microscopy in larval zebrafish." *Nature* 545 (2017): 345–349.

Januszewski, Michał, et al. "High-precision automated reconstruction of neurons with flood-filling networks." *Nature Methods* 15 (2017): 605–610.

Kasthuri, Narayanan, et al. "Saturated reconstruction of a volume of neocortex." *Cell* 162 (2015): 648–661.

Kislinger, Georg, et al. "Neurons on tape: automated tape-collecting ultramicrotomy-mediated volume EM for targeting neuropathology." *Methods in Cell Biology* 177 (2023): 125–170.

Klimovich, Alexander, et al. "Rethinking the role of the nervous system: lessons from the *Hydra* holobiont." *BioEssays* 40 (2018): 1800060.

Klimovich, Alexander, et al. "Novel technologies uncover novel 'anti'-microbial peptides in *Hydra* shaping the species-specific microbiome." *Philosophical Transactions of the Royal Society B: Biological Sciences* 379 (2024): 20230058.

Karlupia, Neha, et al. "Immersion fixation and staining of multi-cubic millimeter volumes for electron microscopy-based connectomics of human brain biopsies." *Biological Psychiatry* 94 (2023): 484–494.

Kunin, Alex, et al. "Hierarchical modular structure of the *Drosophila* connectome." *The Journal of Neuroscience* 43 (2023): 6384–6400.

Lee, Wei-Chung Allen, et al. "Anatomy and function of an excitatory network in the visual cortex." *Nature* 532 (2016): 370–374.

Lin, Albert, et al. "Network statistics of the whole-brain connectome of *Drosophila*." *Nature* 634 (2024): 153–165.

Little, Hannah Morris, et al. "A molecular, spatial, and regulatory atlas of the *Hydra vulgaris* nervous system." *Development* 152 (2025): dev204544.

Livingstone, Jayde, et al. "Scaling up X-ray holographic nanotomography for neuronal tissue imaging." *Biomedical Optics Express* 16 (2025): 1241–1256.

Lovas, Jonathan R., et al. "Ensemble synchronization in the reassembly of *Hydra*'s nervous system." *Current Biology* 31 (2021): 3491–3502.

Maniates-Selvin, Jasper T., et al. "Reconstruction of motor control circuits in adult *Drosophila* using automated transmission electron microscopy." *Cell* 183 (2020): 710–728.

Marshall, Andrea G., et al. "Correlative light-electron microscopy: integrating dynamics to structure." *Trends in Biochemical Sciences* 48 (2023): 826–841.

Martell, Jeffrey D., et al. "Engineered ascorbate peroxidase as a genetically encoded reporter for electron microscopy." *Nature Biotechnology* 30 (2012): 1143–1148.

Moroz, Leonid L. "NeuroSystematics and periodic system of neurons: model vs reference species at single-cell resolution." *ACS Chemical Neuroscience* 9 (2018): 1884–1903.

Motta, Alessandro, et al. "Dense connectomic reconstruction in layer 4 of the somatosensory cortex." *Science* 366 (2019): eaay3134.

Mulcahy, Ben, et al. "A pipeline for volume electron microscopy of the *Caenorhabditis elegans* nervous system." *Frontiers in Neural Circuits* 12 (2018): 94.

Nern, Aljoscha, et al. "Connectome-driven neural inventory of a complete visual system." *Nature* 641 (2025): 152–164.

Pacureanu, Alexandra, et al. "Dense neuronal reconstruction through X-ray holographic nano-tomography." *Nature Neuroscience* 22 (2019): 1503–1513.

Pierson, Josh, et al. "Recent advances in correlative cryo-light and electron microscopy." *Current Opinion in Structural Biology* 86 (2024): 102816.

Salamanca-Díaz, David A., et al. "The *Hydractinia* cell atlas reveals cellular and molecular principles of cnidarian coloniality." *Nature Communications* 15 (2024): 8989.

Scheffer, Louis K., et al. "A connectome and analysis of the adult *Drosophila* central brain." *eLife* 9 (2020): e57443.

Schlegel, Philipp, et al. "Whole-brain annotation and multi-connectome cell typing of *Drosophila*." *Nature* 634 (2024): 139–152.

Shapson-Coe, Alexander, et al. "A petavoxel fragment of human cerebral cortex reconstructed at nanoscale resolution." *Science* 384 (2024): eadk4858.

Song, Kun, et al. "High-contrast en bloc staining of mouse whole-brain and human brain samples for EM-based connectomics." *Nature Methods* 20 (2023): 836–840.

Svara, Fabian, et al. "Automated synapse-level reconstruction of neural circuits in the larval zebrafish brain." *Nature Methods* 19 (2022): 1357–1366.

Szymanski, John R., and Rafael Yuste. "Mapping the whole-body muscle activity of *Hydra vulgaris*." *Current Biology* 29 (2019): 1807–1817.

Titze, Benjamin, and Christel Genoud. "Volume scanning electron microscopy for imaging biological ultrastructure." *Biology of the Cell* 108 (2016): 307–323.

White, John G., Eileen Southgate, J. Nichol Thomson, and Sydney Brenner. "The structure of the nervous system of the nematode *Caenorhabditis elegans*." *Philosophical Transactions of the Royal Society of London. B, Biological Sciences* 314 (1986): 1–340.

Winding, Michael, et al. "The connectome of an insect brain." *Science* 379 (2023): eadd9330.

Witvliet, Daniel K., et al. "Connectomes across development reveal principles of brain maturation." *Nature* 596 (2021): 257–261.

Wittlieb, Jörg, et al. "Transgenic *Hydra* allow in vivo tracking of individual stem cells during morphogenesis." *Proceedings of the National Academy of Sciences USA* 103 (2006): 6208–6211.

Yuste, Rafael. "Breaking the neural code of a cnidarian: learning principles of neuroscience from the 'vulgar' *Hydra*." *Current Opinion in Neurobiology* 87 (2024): 102859.

Vaxenburg, Roman, et al. "Whole-body physics simulation of fruit fly locomotion." Nature 643.8074 (2025): 1312-1320.

Jin, Zehao, et al. "Whole-Brain Connectomic Graph Model Enables Whole-Body Locomotion Control in Fruit Fly." arXiv preprint arXiv:2602.17997 (2026).
