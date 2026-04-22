# Repair of Cortical Tissue Review

## Abstract

Over 20 million U.S. adults live with chronic neocortical damage from stroke, traumatic brain injury, and neurodegenerative disease; none of the currently approved interventions restore the neurons and circuits that were lost (Ondriš et al.; Hao et al.). Recent progress in human induced pluripotent stem cell (iPSC)–derived cortical organoid transplantation has demonstrated that grafted human neurons can mature, vascularize, receive thalamocortical and corticocortical input, extend long axons into host targets, and — in the most striking case — drive host behavior when optogenetically activated (Revah et al.; Cao et al.; Wilson et al.). Yet a formally causal demonstration that the graft, rather than spared peri-infarct host tissue, mediates the recovered behavior after a focal motor-cortex lesion has not been delivered in a cortical graft model at all, and the one partial attempt in an iPSC cortical-neuron paradigm returned a negative result for graft-specific causality (Palma-Tortosa et al.). We argue that functional repair of neocortical tissue requires simultaneous closure of five multiplicatively coupled bottlenecks — area identity, laminar cytoarchitecture, vascular anastomosis, host–graft circuit integration, and a causal functional readout — and that the rate-limiting hurdle in the current literature is circuit integration. We introduce five new quantitative frameworks, covering areal morphogen polarization, laminar birthdate Markov dynamics, host-capillary first-contact kinetics, topographic wiring-correctness via Wasserstein distance, and per-pillar closure under a multiplicative survival model. We then specify a single preregistered experiment in a C57BL/6J photothrombotic motor-cortex stroke model (n=24; power = 0.83 at Cohen's d = 1.2) in which an area-patterned, pre-vascularized, six-layer iPSC-derived cortical organoid is grafted into the caudal forelimb area and causally tested by cell-type-specific optogenetic silencing. The predictions are quantitative, the fail criteria are preregistered, and the experiment is capable of rejecting the five-pillar framework.

---

## 1. Introduction

### 1.1 The unmet need

Stroke, traumatic brain injury, and progressive neocortical neurodegeneration together account for the largest single pool of chronic disability in adult neurology; no existing pharmacological, behavioral, or device-based intervention restores the neurons and local circuits that have been lost to necrosis (Hao et al.; Ondriš et al.). Current standard-of-care therapies — physical, occupational, and speech rehabilitation — recruit peri-infarct plasticity and spared contralateral circuits, but in patients with large or chronic lesions the ceiling of recovery is bounded by how much tissue remains (Longo et al.; Moon et al.). The implication is unambiguous: beyond a certain lesion size and chronicity, functional recovery requires the physical replacement of lost cortical tissue.

### 1.2 Why "tissue" replacement is the right framing

It is tempting, given the last decade of progress in cellular reprogramming, to reduce the problem to a cell-replacement question. Two families of cellular approaches have matured to in vivo testing: (i) direct in situ reprogramming of reactive astrocytes to induced neurons by ectopic transcription factors such as NeuroD1 (Guo et al.; Ge et al.; Jiang et al.); and (ii) transplantation of dissociated iPSC-derived cortical neurons or neural progenitors into or adjacent to the lesion cavity (Tatarishvili et al.; Yamashita et al.). Both strategies produce functional neurons at the cellular level. Neither, alone, rebuilds the multi-layered, area-specific, vascularized, circuit-integrated architecture of mature neocortex. The gap between "cells" and "tissue" is the gap between a node and a network.

Tissue-level replacement, by contrast, starts from the position that the neocortex is a structured six-layer, area-specific computational substrate whose function depends on cytoarchitectural order, vascular support, and correctly wired long-range connectivity (O'Leary et al.; Leone et al.; Britanova et al.). This is the framing adopted by recent work that implants three-dimensional, self-organizing cortical organoids rather than dissociated cell suspensions — and which has demonstrated that organoid-format grafts outperform suspension-format grafts on every measured dimension of repair (Cao et al.; Quezada et al.; Somaa et al.).

### 1.3 Five coupled bottlenecks

From a reading of the last decade of cortical graft literature, we identify five bottlenecks that together determine whether a neocortical graft restores function:

1. **Area identity** — motor, somatosensory, visual, and associative cortices differ not only in their inputs and outputs but in their internal transcriptional identities established by FGF8, EMX2, PAX6, COUP-TFI, and related morphogen-regulated transcription factors (O'Leary et al.; Tomassy et al.; Bertacchi et al.). An area-mismatched graft is a functionally wrong organ in the right location.
2. **Laminar cytoarchitecture** — within a cortical area, deep-layer subcerebral projection neurons (FEZF2, CTIP2, TBR1) and upper-layer callosal neurons (SATB2, BRN2, CUX1) arise in a birthdate-dependent transcriptional cascade (Britanova et al.; Leone et al.; Miskinyte et al.). A graft that generates neurons but not layers is a disorganized slab of grey matter, not functional cortex.
3. **Vascular anastomosis** — cortical tissue beyond ~200 μm from the nearest capillary undergoes hypoxic death; organoid grafts larger than ~1–2 mm³ without vasculature develop necrotic cores that cap the usable graft volume orders of magnitude below clinically meaningful stroke lesions (Cakir et al.; Matsui et al.; Pham et al.; Kistemaker et al.).
4. **Host–graft circuit integration** — for a grafted neuron to carry useful function it must be innervated by host axons, project to its natural target, and participate in activity-dependent circuit refinement (Revah et al.; Kelley et al.; Espuny-Camacho et al.; Linaro et al.; Wilson et al.; Keck et al.; Lopez-Ortega et al.).
5. **Falsifiable functional readout** — recovery is meaningful only to the extent that the behavior recovered is *mediated* by the graft, a claim that can be tested only by selective, cell-type-restricted causal interventions such as optogenetic silencing (Daadi et al.; Wahl et al.; Palma-Tortosa et al.; Cheng et al.).

No prior published cortical graft study has simultaneously addressed all five pillars in a single preregistered causal framework. Many have closed one or two pillars, and several have rigorously tested circuit integration without resolving area-identity or vascularization (Revah et al.; Wilson et al.); others have closed the vascular pillar without addressing circuit integration (Cakir et al.; Somaa et al.).

### 1.4 Why Pillar IV is the rate-limiting step today

A careful reading of the recent literature suggests that the current rate-limiting bottleneck is Pillar IV (circuit integration) — and specifically the absence of a cell-type-specific causal demonstration that graft activity is what mediates the recovered behavior. Revah and colleagues established that human cortical organoid neurons in rat somatosensory cortex receive thalamocortical input, show stimulus-evoked responses, and that their optogenetic activation drives reward-seeking behavior (Revah et al.). Wilson and colleagues confirmed visual-cortex-specific functional integration with electrode-array readouts (Wilson et al.). Palma-Tortosa and colleagues, however, provided the only published loss-of-function causal test in the iPSC cortical-neuron stroke paradigm and obtained a negative result for graft-specific causality, showing instead that transcallosal host neurons mediated the behavioral recovery (Palma-Tortosa et al.). That published negative result is the motivating puzzle for this manuscript: it is the exact test our framework must pass, not avoid.

### 1.5 Contribution

This manuscript (i) organizes cortical tissue replacement into five explicit pillars; (ii) argues on the basis of the published literature that Pillar IV is currently rate-limiting; (iii) introduces five new quantitative frameworks that formalize each pillar and their multiplicative coupling; and (iv) specifies a single, fully preregistered mouse experiment whose optogenetic-silencing readout is capable of falsifying the five-pillar claim for a specific graft configuration. The framework is human-iPSC-only; we explicitly do not address xenotransplantation strategies in this manuscript.

---

## 2. Pillar I — Area Identity Specification

### 2.1 The biological fact: cortex is areally organized

The mammalian neocortex is not a homogeneous sheet; it is subdivided into areas that differ in cytoarchitecture, input/output connectivity, and function, and these areas are specified in development by a combination of intrinsic transcriptional gradients and extrinsic thalamic inputs (O'Leary et al.). The canonical anterior-to-posterior gradient is governed by FGF8 secreted from the commissural plate at the anterior pole and by EMX2, PAX6, and COUP-TFI expressed in graded patterns across the dorsal telencephalon; loss or gain of each of these signals shifts the areal map in predictable directions (O'Leary et al.; Tomassy et al.; Bertacchi et al.). Work in genetics and developmental biology has established that these gradients are necessary and partially sufficient to specify areal identity.

### 2.2 Translation to human cortical organoids

In human pluripotent stem cell systems, area identity is not a default property of cortical differentiation. Conventional cerebral and cortical organoid protocols produce a mix of regional identities biased toward dorsal forebrain without fine control of anterior-posterior or medio-lateral axis (Magni et al.; Whye et al.). Bertacchi and colleagues demonstrated in 2023 that exogenous FGF8 treatment of cerebral organoids shifts regional gene expression, biases the balance of glutamatergic versus GABAergic neurons, and modulates spontaneous network activity, supporting the conclusion that the FGF8 gradient is both necessary and sufficient to push human organoid tissue along the antero-posterior axis (Bertacchi et al.). Tomassy and colleagues had earlier shown that the COUP-TFI transcription factor controls the timing and area-specificity of corticospinal motor neuron differentiation, supporting the interpretation that each area is not simply patterned by global gradients but by specific area-restricted temporal programs (Tomassy et al.).

### 2.3 Why area identity matters for grafting

Area identity is not an academic refinement. Espuny-Camacho and colleagues grafted human pluripotent stem cell–derived visual cortical cells into either adult mouse visual cortex or adult mouse motor cortex, and found that the grafts integrated into host circuits in an area-specific fashion: the visual-cortex-identity graft matured and projected to visual targets when placed in visual cortex, while the same cells in motor cortex failed to mature and project properly (Espuny-Camacho et al.). This is, to our knowledge, the clearest published demonstration that an area-mismatched graft fails at the integration step even when the neurons themselves are electrophysiologically competent. Quezada and colleagues reached a parallel conclusion from mouse-donor telencephalic grafts into aspiration-lesioned adult mouse cortex: the grafts differentiated into upper- and deep-layer neurons, became vascularized within one week post-transplant, projected to appropriate targets, and responded to visual stimuli, with the authors explicitly framing their platform as a testbed for neocortical-like tissue prototypes (Quezada et al.).

### 2.4 Mathematical framing of areal polarization in organoids

At the scale of an organoid, area identity is a spatial-pattern-formation problem in a growing, finite-size tissue. Let $c_{\mathrm{F}}(x,t)$ denote the FGF8 concentration and $c_{\mathrm{E}}(x,t)$ the EMX2 transcription-factor concentration at position $x$ along the nascent antero-posterior axis of an organoid at time $t$. The coupled reaction-diffusion system can be written as:

```math
\frac{\partial c_{\mathrm{F}}}{\partial t} = D_{\mathrm{F}} \nabla^2 c_{\mathrm{F}} + \alpha_{\mathrm{F}}\,\delta(x - x_{\mathrm{source}}) - \beta_{\mathrm{F}} c_{\mathrm{F}} - \gamma\,c_{\mathrm{F}} c_{\mathrm{E}}
```

```math
\frac{\partial c_{\mathrm{E}}}{\partial t} = D_{\mathrm{E}} \nabla^2 c_{\mathrm{E}} + \frac{V_{\mathrm{E}}\,K^n}{K^n + c_{\mathrm{F}}^n} - \beta_{\mathrm{E}} c_{\mathrm{E}}
```

where $D_\cdot$ is the diffusion coefficient, $\alpha_{\mathrm{F}}$ is the FGF8 secretion rate at a localized source, $\beta_\cdot$ is a degradation rate, $\gamma$ is the FGF8-EMX2 cross-repression rate, $V_{\mathrm{E}}$ is the EMX2 maximum expression rate under derepression, $K$ is the half-inhibition constant, and $n$ is the Hill coefficient of EMX2 repression by FGF8. We label this coupled system **F436**.

The relevant biophysical inference is that a stable, monotonic antero-posterior FGF8/EMX2 gradient requires the organoid to exceed a minimum diameter proportional to $\sqrt{D_{\mathrm{F}}/\beta_{\mathrm{F}}}$ — the morphogen decay length — so that the source and sink are separated by at least one decay length. With typical morphogen decay lengths of 100–300 μm, this predicts a minimum organoid diameter of roughly 300 μm for a stable single-gradient areal polarization, and larger for multi-area patterning. This is consistent with the empirical observation that sub-millimeter organoids tend to carry a single regional identity while larger fused organoids or assembloids develop multi-region architecture (Miura et al.; Magni et al.).

### 2.5 Practical translation

Two engineering consequences follow. First, an iPSC-derived motor cortical graft intended to replace caudal forelimb area tissue should be patterned with a precisely-timed antero-posterior FGF8 exposure during neural induction to bias identity toward posterior frontal cortex. Second, because assembloid and multi-region organoid protocols reliably produce spatially distinct regional identities (Miura et al.), area identity can be positively verified by single-nucleus transcriptomics before grafting (Xu et al.), using regional marker panels derived from the human Allen Brain Atlas reference. Grafts failing a prespecified regional-identity threshold should be excluded from transplantation.

---

## 3. Pillar II — Laminar Cytoarchitecture

### 3.1 The six-layer organization

Mature neocortex is a layered structure in which six horizontal laminae are generated in an inside-out temporal sequence from a shared population of cortical radial glial progenitors (Leone et al.). Deep-layer neurons (layers V–VI) are born early and project subcerebrally to thalamus, brainstem, and spinal cord; they are specified by FEZF2, CTIP2 (BCL11B), and TBR1 and in the mature brain include corticospinal motor neurons and corticothalamic neurons. Upper-layer neurons (layers II–IV) are born later and project within and across hemispheres; they are specified by SATB2, BRN2 (POU3F2), and CUX1 and in the mature brain include callosal projection neurons and local interneuron-targeted pyramidal neurons (Britanova et al.; Leone et al.). The two programs are reciprocally antagonistic: SATB2 represses CTIP2 and the FEZF2 deep-layer program, and in SATB2-null cortex the upper-layer neurons mis-specify as CTIP2+ subcerebral-projecting neurons and form an ectopic corticospinal tract (Britanova et al.).

### 3.2 Lamination in human cortical organoids

Human cortical organoids generate deep- and upper-layer neurons in an approximately correct temporal order with the appropriate transcriptional markers, though the proportions drift with protocol and batch. In the Yamashita 2025 study, iPSC-derived cortical neuron grafts transplanted into the peri-infarct cortex of photothrombotic-stroke mice were found to contain 16.4% CTIP2+ deep-layer neurons and 47.3% SATB2+ upper-layer neurons, with grafts projecting along the corticospinal tract in 68% of transplanted animals and to the thalamus, superior colliculus, and vestibular nucleus (Yamashita et al.). These ratios are meaningfully displaced from the approximately 30:70 deep-to-upper ratio of adult human motor cortex, which is relevant because the ratio of subcerebral to callosal projection neurons is the biologically most important laminar parameter for motor-cortex function.

### 3.3 A birthdate Markov model of laminar composition

We formalize laminar composition as a time-inhomogeneous Markov chain over transcriptional states. Let the state space be $\mathcal{S} = \{P, \mathrm{VI}, \mathrm{V}, \mathrm{IV}, \mathrm{III}, \mathrm{II}\}$ where $P$ denotes progenitor and $\mathrm{VI}$ through $\mathrm{II}$ denote the six-layer post-mitotic identities. A cell in state $P$ at time $t$ transitions to post-mitotic state $s \in \{\mathrm{VI}, \mathrm{V}, \mathrm{IV}, \mathrm{III}, \mathrm{II}\}$ with time-dependent probability $q_s(t)$ satisfying $\sum_s q_s(t) = 1 - q_P(t)$, where $q_P(t)$ is the self-renewal probability at time $t$. We label the transition-kernel family **F437**:

```math
q_s(t) = \frac{\exp\!\left(-\frac{(t - t_s^*)^2}{2\sigma_s^2}\right)}{\sum_{s'} \exp\!\left(-\frac{(t - t_{s'}^*)^2}{2\sigma_{s'}^2}\right)} \cdot (1 - q_P(t))
```

where $t_s^*$ is the birthdate peak for layer $s$ and $\sigma_s$ is the birthdate spread. The expected fraction of post-mitotic neurons in layer $s$ after $T$ days of differentiation is:

```math
f_s(T) = \int_0^T q_s(t) \cdot \pi_P(t) \, dt
```

with $\pi_P(t)$ the progenitor-pool size at time $t$ (a second, coupled ODE). Fitting the Yamashita 2025 CTIP2/SATB2 fractions to this model yields an estimate for the deep-to-upper birthdate separation; more importantly, it identifies the design lever available to the experimenter: lengthening the deep-layer window (advancing $t_{\mathrm{VI}}^*$ and $t_{\mathrm{V}}^*$, or increasing $\sigma_{\mathrm{V}}$) or shortening the upper-layer window shifts the composition back toward the 30:70 ratio of adult motor cortex.

### 3.4 Two laminar design levers

Two experimentally tractable levers follow. The first is temporal control of differentiation: the Whye 2023 accelerated cortical organoid protocol demonstrates that lineage specification can be brought forward by ~30% relative to long-form protocols (Whye et al.), and the Magni 2022 survey of three organoid protocols shows that guided differentiation without WNT activation produces the highest regional identity fidelity while default conditions produce the broadest laminar diversity (Magni et al.). The second lever is direct transcription-factor programming: Miskinyte 2018 showed that NGN2 combined with FEZF2 or SATB2 drives human embryonic stem cells into pyramidal-shaped neurons expressing cortical projection markers, but with the important caveat that even after TF programming the cells continued to co-express upper- and deep-layer markers, suggesting that additional area-identity cues are needed to lock in a single laminar identity (Miskinyte et al.). The practical implication is that robust laminar control requires both guided morphogen patterning (Pillar I) and time-resolved transcription-factor gating (Pillar II), operating together.

### 3.5 Electrical maturation as an accelerant

Beyond transcriptional programming, Li 2024 demonstrated that pre-transplantation electrical stimulation of cortical organoids via multi-electrode arrays facilitated differentiation and maturation through a CAMKII–PKA–pCREB pathway, and that electrically pre-conditioned organoids showed superior cell viability, cortical-plate architecture, and post-transplant integration with host somatosensory cortex (Li et al.). Electrical pre-conditioning therefore provides a non-genetic adjunct to laminar maturation that can be layered on top of morphogen patterning.

---

## 4. Pillar III — Vascular Co-graft and Anastomosis

### 4.1 The 200-μm hypoxia rule

Oxygen delivery in cortex is limited by a ~150–250 μm diffusion distance from the nearest perfused capillary; tissue beyond that distance transitions into chronic hypoxia (Cakir et al.; Matsui et al.). For organoids — which until recently were grown entirely without vasculature — this translates into a hard upper bound of approximately 1–4 mm³ on the size of a viable graft before necrotic-core formation dominates (Cakir et al.). Cerebral strokes of clinical consequence are typically 10–100 cm³, four to five orders of magnitude larger. Vascularization is therefore not a refinement — it is a precondition for any attempt at scale.

### 4.2 ETV2-induced endothelium in cortical organoids

Cakir and colleagues in 2019 engineered human embryonic stem cells to ectopically express the endothelial master regulator ETV2 (ETS variant 2) and co-aggregated these cells with unmodified hESCs at a controlled ratio during cortical organoid differentiation. The resulting vascularized cortical organoids developed a self-organized CD31+ endothelial network penetrating the organoid interior, acquired tight-junction markers and trans-endothelial electrical resistance consistent with nascent blood-brain-barrier features, and — most importantly for grafting — the ETV2-induced endothelium supported the formation of perfused blood vessels after transplantation in vivo (Cakir et al.). The 2025 review by Kistemaker and colleagues critically assesses the field and notes that vessel-like structures in vascularized brain organoids still do not carry blood-like flow in vitro and do not form a fully mature blood-brain barrier, but that they meaningfully advance the in vivo anastomosis step (Kistemaker et al.).

### 4.3 Patient-iPSC endothelium as a co-graft

An alternative to genetic engineering of the host organoid is to differentiate patient-derived iPSCs in parallel along the endothelial lineage and then combine organoid and endothelial cell populations during final aggregation. Pham and colleagues demonstrated that coating day-34 cerebral organoids with 250,000 patient-iPSC-derived endothelial cells yielded robust CD31+ vascularization within the organoid interior after 3–5 weeks in vitro and persisted in vivo after transplantation into immunodeficient mice (Pham et al.). The advantage of the co-graft approach is that it avoids introducing an integrating transgene (ETV2) into the patient's graft; the trade-off is a less tightly-regulated vascular density.

### 4.4 Scaffold-based vascular support

A complementary approach is to co-graft the cell population with a biomaterial scaffold engineered for vascular recruitment. Somaa and colleagues assembled peptide hydrogels presenting the laminin-derived IKVAV epitope and combined them with human embryonic stem cell–derived cortical progenitors into necrotic stroke lesion cavities in rats; the scaffold-supported grafts produced progressive motor improvement over 9 months that was larger than either the scaffold alone or the cell suspension alone could achieve, and produced more mature and electrophysiologically integrated neurons (Somaa et al.). McCrary and colleagues developed a chondroitin-sulfate-A hyaluronic-acid hydrogel that released basic fibroblast growth factor and encapsulated mouse-iPSC-derived neural progenitor cells; the CS-A–encapsulated grafts significantly improved vascular remodeling, cortical blood flow, and sensorimotor recovery in a mini-stroke mouse model, with blocking experiments showing that the effect required bFGF (McCrary et al.). Moshayedi and colleagues systematically optimized a hyaluronic-acid hydrogel with matrix-metalloproteinase-sensitive crosslinkers for stroke and showed that the optimized matrix supported iPSC-NPC survival and differentiation in the infarct core with selective control over glial versus neuronal fate (Moshayedi et al.). Zhang and colleagues developed a reactive-oxygen-species-triggered platelet-lysate-docosahexaenoic-acid hydrogel that improved behavioral recovery in a mouse focal ischemic stroke model via reduced oxidative stress and enhanced neovascularization (Zhang et al.). Across these four scaffold studies the common finding is that biomaterial co-graft accelerates angiogenesis and improves functional outcome over cells-alone controls.

### 4.5 Host capillary anastomosis as a first-contact process

We now model the host–graft vascular anastomosis as a Poisson point process in which tip cells of host capillaries encounter tip cells of the pre-vascularized graft endothelium across the graft–host interface. Let $\rho_{\mathrm{H}}(t)$ be the areal density of host capillary tips at the graft surface at time $t$, $\rho_{\mathrm{G}}$ the areal density of graft tips, and $A$ the graft surface area; under the assumption that pairwise contacts follow a Poisson process with rate $\lambda = \kappa \rho_{\mathrm{H}}(t)\rho_{\mathrm{G}}A$, the expected first-contact time is:

```math
\langle T_{\mathrm{first}} \rangle = \frac{1}{\kappa \rho_{\mathrm{H}}(0)\rho_{\mathrm{G}} A}
```

where $\kappa$ is a contact-formation rate constant. We label this **F438**. The number of patent anastomoses at time $t$ is then well-approximated by:

```math
N(t) = N_{\max}\left(1 - \exp\!\left(-\int_0^t \kappa \rho_{\mathrm{H}}(s)\rho_{\mathrm{G}}A\,ds\right)\right)
```

with $N_{\max}$ the maximum number of patent anastomoses supported by the interface geometry. This predicts that doubling $\rho_{\mathrm{G}}$ (the graft's pre-existing endothelial density) approximately halves the first-contact time, which is consistent with the observed acceleration of anastomosis when ETV2-vascularized organoids are used rather than cells-only grafts (Cakir et al.; Pham et al.). The model also predicts that the hypoxic-core radius $r_{\mathrm{hyp}}(t)$ shrinks approximately as:

```math
r_{\mathrm{hyp}}(t) \approx r_{\mathrm{hyp}}(0)\cdot\exp\!\left(-\frac{N(t)}{N_{\max}}\right)
```

for graft radii where diffusion-limited oxygenation dominates.

### 4.6 The vascular pillar is necessary but not alone sufficient

The empirical record makes clear that vascularization is necessary for grafts beyond ~1–2 mm³ but is not alone sufficient for functional repair. The scaffold and vascular-cograft studies reviewed above produce improved survival and motor recovery, but the scale of recovery plateaus well below the scale needed for centimeter-sized lesions. The logical consequence is that the vascular pillar has to be closed simultaneously with Pillars I, II, IV, and V — which is the central claim of our five-pillar framework.

---

## 5. Pillar IV — Host–Graft Circuit Integration (Anchor)

### 5.1 Evidence that grafts integrate

The most mechanistically detailed demonstration of host–graft circuit integration in a cortical graft model is the Revah 2022 study. Human iPSC-derived cortical organoids were transplanted into the somatosensory cortex of newborn athymic rats; MRI over months showed organoid growth across multiple cell lines and animals, single-nucleus RNA sequencing revealed progression of corticogenesis and the emergence of activity-dependent transcriptional programs in the grafted neurons, and transplanted cortical neurons displayed more mature morphological, synaptic, and intrinsic membrane properties than their in vitro counterparts (Revah et al.). Critically, anatomical and functional tracing showed that the grafted organoids received thalamocortical and corticocortical input, that these inputs evoked sensory responses in the human neurons, that grafted neurons sent axons throughout the rat brain, and that optogenetic activation of the graft could drive reward-seeking behavior. The Kelley 2024 protocol paper codifies the methodology and confirms reproducibility across laboratories (Kelley et al.).

### 5.2 Evidence of area-specific integration

Wilson and colleagues in 2022 extended the integration story into the visual domain: transparent microelectrode arrays combined with two-photon imaging of human cortical organoids transplanted into the retrosplenial cortex of adult mice showed that visual stimuli evoked graft electrophysiological responses that matched the surrounding cortex, that graft multi-unit activity and gamma-band power were modulated by visual input, and that stimulus-evoked MUA phase-locked to slow cortical oscillations (Wilson et al.). Linaro and colleagues demonstrated that single human cortical pyramidal neurons xenografted into mouse visual cortex display tuned, decorrelated visual responses similar to those of the mouse host neurons, and that the human neurons retain a neoteny-like extended developmental timeline (Linaro et al.). Espuny-Camacho and colleagues showed that lesioned adult mouse visual cortex supports area-specific maturation and projection of human visual cortical grafts far more efficiently than lesioned motor cortex does, reinforcing the area-identity interaction with circuit integration (Espuny-Camacho et al.).

### 5.3 Evidence from the motor-cortex stroke paradigm

Cao and colleagues transplanted human cerebral organoids into the junction of the infarct core and peri-infarct zone of NOD-SCID stroke mice and reported that the grafts survived in the infarcted core, differentiated into target neurons, repaired infarcted tissue, sent axons to distant brain targets, and integrated into the host neural circuit, producing elimination of sensorimotor deficit behaviors; by direct contrast, transplantation of dissociated single cells from the same organoids failed to repair the infarcted tissue (Cao et al.). This is a critical control — tissue format out-performs cellular format for tissue repair. Wang and colleagues in an independent MCAO rat stroke paradigm reported analogous benefits of organoid-format transplantation with multilineage differentiation and region-specific motor-cortex reconstruction (Wang, S-N. et al.). Dong and colleagues showed that human cerebral organoids transplanted into mouse prefrontal cortex extended axonal projections exceeding 4.5 mm into basal brain regions, formed bidirectional synaptic connections with host neurons, and potentiated startle fear responses (Dong et al.).

### 5.4 The causal-test problem

All of these studies collectively establish that grafts *can* integrate into host circuits. None of them, however, delivers the specific causal proof that the behavior recovered in a focal motor-cortex stroke is *mediated by the graft*. Palma-Tortosa and colleagues are, to our knowledge, the only group to have performed this specific causal test in an iPSC cortical-neuron cortical-stroke paradigm. They intracortically grafted human iPSC-derived cortical neurons into rats with ischemic cerebral cortex lesions; the grafted neurons sent widespread axonal projections to both hemispheres, monosynaptic transsynaptic tracing revealed contralateral host neurons receiving direct inputs from grafted neurons, and the stroke-induced cylinder-test asymmetry was reversed by transplantation. Crucially, when they selectively silenced graft neurons expressing halorhodopsin with light, the impairment was *not* recreated; rather, silencing of endogenous halorhodopsin-expressing cortical neurons on the contralateral side reproduced the motor-test deficit (Palma-Tortosa et al.). The interpretation the authors favored was that transcallosal activity in endogenous cortex, indirectly influenced by graft activity, mediated the behavioral recovery. That result is a negative for the direct-causal-mediation interpretation in their specific graft configuration, and it is the central scientific puzzle that our preregistered experiment is designed to resolve.

### 5.5 Activity-dependent refinement as the closing mechanism

Keck and colleagues showed in adult mouse visual cortex that after a small retinal lesion, dendritic spine dynamics increase three-fold in the deafferented cortex and drive an almost complete replacement of spines over two months, supporting the interpretation that activity-dependent synaptic remodeling is the dominant mechanism of post-lesion cortical circuit reorganization in adult cortex (Keck et al.). Lopez-Ortega and colleagues extended this picture with two-photon imaging in mouse V1 showing that repeated visual stimulation reduces the number of responsive neurons but potentiates their responses through specific changes in AMPA receptor content and spine density (Lopez-Ortega et al.). Together these studies frame the closing mechanism of graft integration as prolonged activity-dependent refinement over months — a time window consistent with the Revah 2022 in vivo observations of progressive maturation of graft dendritic complexity and membrane properties (Revah et al.). The same principle also motivates an important choice in our preregistered design: the behavioral readout must span months, not weeks, in order to allow activity-dependent refinement to complete.

### 5.6 Host glial response and the integration niche

Microglia and astrocytes shape the graft niche and therefore its integration probability. Wang and colleagues (2022) in the spinal-cord model demonstrated that grafted human ESC-derived astroglia shift host microglia toward an anti-inflammatory phenotype through interleukin-4 signaling and that depleting anti-inflammatory microglia reverses the repair effect (Wang, J. et al.). Ballout and colleagues in a mouse cortical-lesion model showed that delaying graft implantation by one week after cortical lesion — when the M2 microglial phenotype dominates the lesion — significantly enhances graft vascularization, survival, and axonal projection density (Ballout et al.). Wang and colleagues (2016) using two-photon imaging in parabiotic mice showed that host-derived infiltrating microglia colonize the graft and differentiate into resting ramified morphology, while donor-tissue microglia are rapidly lost (Wang, C. et al.). The engineering implication is that the graft timing (delay of days to one week post-lesion) and the endogenous microglial state (anti-inflammatory) should be selected as critical experimental parameters.

### 5.7 A wiring-correctness functional

We now formalize circuit integration correctness. Let $\mathcal{P}_{\mathrm{natural}}$ denote the empirical distribution of thalamocortical projection termination coordinates within a healthy target cortical area (for the caudal forelimb area in mouse, this is the ventral anterior–ventral lateral thalamic complex), and $\mathcal{P}_{\mathrm{graft}}$ the empirical distribution of thalamocortical projection termination coordinates within the graft. The wiring-correctness functional is the 2-Wasserstein distance:

```math
W_2(\mathcal{P}_{\mathrm{natural}}, \mathcal{P}_{\mathrm{graft}}) = \left(\inf_{\pi \in \Pi(\mathcal{P}_{\mathrm{natural}}, \mathcal{P}_{\mathrm{graft}})} \int \|x - y\|^2\, d\pi(x,y)\right)^{1/2}
```

where $\Pi(\mathcal{P}_{\mathrm{natural}}, \mathcal{P}_{\mathrm{graft}})$ is the set of couplings of the two distributions. We label this **F439**. A healthy graft has $W_2 \to 0$ in the limit of perfect topographic precision. Under the null hypothesis that graft termination is spatially random, $W_2$ is large and approximately equal to the standard deviation of the target-area geometry. The wiring-correctness functional can be computed directly from AAV-traced thalamocortical termination coordinates acquired from the graft and from age-matched sham-control cortex, providing a graft-integration quality metric that is continuous, interpretable, and directly testable.

### 5.8 Synthesis of Pillar IV

The evidence permits three robust conclusions and one open question. (Robust) Human iPSC-derived cortical neurons in organoid or dissociated form can survive, mature, and integrate into host cortex including receipt of thalamocortical input and formation of bidirectional synaptic connections (Revah et al.; Dong et al.; Wilson et al.; Linaro et al.). (Robust) Organoid format outperforms dissociated-cell format for tissue-level repair (Cao et al.). (Robust) Area and laminar identity gate the efficiency of integration (Espuny-Camacho et al.; Yamashita et al.). (Open) Whether the behavior recovered after graft is directly mediated by graft activity or by host plasticity catalyzed by the graft has been tested only once in an iPSC cortical-neuron stroke paradigm, with a negative result for direct graft-mediated causality (Palma-Tortosa et al.). Resolving this open question is the objective of the preregistered experiment in §6.

---

## 6. Pillar V — Functional Readout and the Preregistered Experiment

### 6.1 Objective of the experiment

The single preregistered experiment is designed to determine whether an area-patterned, laminar-correct, pre-vascularized, iPSC-derived cortical organoid graft, implanted into the caudal forelimb area of the motor cortex of an adult mouse after a photothrombotic stroke, restores skilled forelimb reaching through *graft-mediated* circuit activity rather than through host plasticity catalyzed by the graft. The test is a cell-type-specific optogenetic silencing of the graft delivered at a pre-specified time point post-graft; the outcome is prespecified with a quantitative fail criterion.

### 6.2 Model selection

The Rose-bengal photothrombotic model targeting the caudal forelimb area of motor cortex (CFA) is selected for four reasons. First, it produces a focal, anatomically well-defined lesion of reproducible size (approximately 1–2 mm³ when calibrated), with minimal damage to white matter tracts, which is an important control against lesions that involve both cortex and underlying fiber bundles (Moon et al.; Longo et al.). Second, the CFA is selectively required for skilled forelimb reaching in mice, meaning that a lesion creates a behaviorally assayable deficit that is specifically attributable to cortical tissue loss rather than a diffuse motor-network disruption. Third, the photothrombotic method is well-established and produces the same lesion in multiple independent published stroke-graft studies against which we can compare (Yamashita et al.; Longo et al.). Fourth, the mouse model allows access to the transgenic and optogenetic toolkit required for the causal test.

### 6.3 Graft specification

The graft is a human iPSC-derived cortical organoid prepared as follows. We will use an allelic-HLA-matched iPSC line (autologous in the human-clinical translation; MHC-matched or immunodeficient in the mouse test), differentiate the line along an accelerated cortical organoid protocol with explicit FGF8 antero-posterior patterning to bias motor-frontal area identity (Whye et al.; Bertacchi et al.; Magni et al.), co-aggregate with 10% ETV2-inducible endothelial cells to produce a pre-vascularized organoid (Cakir et al.), and mature organoids to day 60 under intermittent electrical pre-conditioning via multielectrode arrays to accelerate laminar maturation (Li et al.). Before transplantation every organoid will undergo single-nucleus RNA sequencing to verify regional identity and laminar composition; organoids failing prespecified thresholds (≥70% motor-frontal marker enrichment; deep-to-upper neuron ratio 25–35:65–75) are excluded. Grafts are delivered at one week post-lesion in order to exploit the M2-microglial-dominant anti-inflammatory peri-infarct window that has been shown to maximize graft vascularization, survival, and projection density (Ballout et al.; Wang, J. et al.).

### 6.4 Surgical and behavioral design

Twenty-four adult C57BL/6J-background mice (6–8 weeks old, 12 male and 12 female) are trained on the single-pellet reaching task until they achieve ≥60% first-attempt success across five consecutive days (Moon et al.). A photothrombotic stroke is induced in the left CFA (contralateral to the trained forelimb) using intravenous Rose Bengal (30 mg/kg) and cold-light illumination of a 2 mm craniotomy window (Longo et al.). One week after stroke, mice are randomly assigned (stratified by pre-stroke reaching performance and sex) to graft (n=12) or sham-PBS injection (n=12) groups. The graft group receives 2.5 × 10⁵ cells in organoid format (1–2 mm³) via stereotaxic injection at the peri-infarct/infarct-core boundary. Reaching is reassessed at weeks 4, 8, 12, 16, and 20 post-graft.

### 6.5 The optogenetic causal arm

At week 18 post-graft, every graft-group animal receives an intracortical injection of AAV9-CaMKIIa-eArchT3.0-eYFP targeting graft neurons (confirmed by post-hoc histology of YFP-expressing human-NuMA+ cells). A separately implanted 593 nm optical cannula above the graft provides light stimulation. At week 20, reaching is assessed under two conditions (within-animal crossover, counterbalanced, randomized block order): (i) laser-off reaching, and (ii) laser-on (593 nm, 10 mW/mm², continuous during each reach). The key prespecified analysis is the within-animal difference between laser-off and laser-on reaching success in graft-group animals, compared to the same manipulation in a concurrent "graft-adjacent host eArchT3.0" control arm in a separate set of 12 sham-grafted photothrombotic-stroke animals in which AAV9-CaMKIIa-eArchT3.0 is injected into peri-infarct host cortex rather than graft tissue.

### 6.6 Preregistered outcome predictions

The four prespecified outcomes are:

1. **Primary behavioral** (pass criterion): at week 20 post-graft, graft-group mice achieve mean reaching success ≥60% of pre-lesion baseline, with the sham group achieving ≤30% of pre-lesion baseline; two-tailed Welch's $t$-test, $\alpha = 0.05$, one-sided pre-specified direction. Predicted effect size Cohen's $d \geq 1.2$ based on Cao 2023 and Yamashita 2025 effect sizes (Cao et al.; Yamashita et al.). Power $\geq 0.83$ at $n=12$ per group.

2. **Optogenetic causal** (pass criterion): within-animal difference between laser-on and laser-off reaching success is at least 25 percentage points in the graft-group (graft-silencing reduces performance) and less than 5 percentage points in the host-eArchT3.0 control arm. Two-tailed paired $t$-test with Bonferroni correction.

3. **Anatomical integration**: ≥50% of graft-derived human NuMA+ neurons co-express either CTIP2 or SATB2 at week 20; graft receives ≥100 retrogradely labeled thalamic inputs per 100 μm² of graft surface as traced by AAV9-retro-mCherry from VA/VL thalamus (relative to sham-graft cavity, which receives zero human-specific inputs by construction).

4. **Wiring correctness** (F439): the 2-Wasserstein distance between graft thalamocortical termination distribution and age-matched sham-control CFA thalamocortical termination distribution is within 1.5× of the within-animal test-retest Wasserstein noise floor.

### 6.7 Preregistered falsification criteria

The five-pillar framework is *rejected* for this graft configuration if any of the following occurs:

- Primary behavioral: graft-group reaching at week 20 fails to exceed sham-group reaching by the prespecified magnitude.
- Optogenetic causal: graft-silencing fails to produce a behavioral decrement of at least 25 percentage points in the graft-group, OR the host-eArchT3.0 control arm produces a decrement of comparable magnitude (in which case the observed graft-silencing decrement cannot be attributed to the graft specifically).
- Anatomical integration: any of the three anatomical thresholds is missed.
- Wiring correctness: F439 Wasserstein distance exceeds 1.5× the test-retest noise floor.

A failure on (i) rejects the overall clinical utility of the graft configuration; a failure on (ii) with a pass on (i) is the Palma-Tortosa 2020 pattern — recovery mediated by host plasticity rather than by graft — and is interpretable without necessarily rejecting the five-pillar framework, but does reject the specific claim that direct graft causality is necessary; failures on (iii) or (iv) would isolate the mechanistic stage at which the graft configuration fails.

### 6.8 Statistical plan

The analysis plan, the inclusion/exclusion rules, the randomization scheme, the blinding protocol (all reaching is scored by an investigator blinded to group allocation), the criteria for laser sham-failure, and the data-exclusion rules for mice that die or reach pre-specified welfare endpoints are all deposited prior to animal work. Preregistration on Open Science Framework is required before IACUC protocol initiation.

### 6.9 Power, sample size, and Bayesian complement

Sample size was calculated using G*Power 3.1 assuming a two-group $t$-test with Cohen's $d = 1.2$, $\alpha = 0.05$ one-tailed, and power = 0.83, yielding $n = 12$ per group. A supplementary Bayesian complement (default Cauchy prior on effect size with scale = 0.707; JZS Bayes factor) is prespecified to accompany the frequentist $t$-test; a Bayes factor $\mathrm{BF}_{10} > 10$ is required to declare the primary outcome met in conjunction with the frequentist pass criterion. This dual-criterion approach is robust against both Type-I and Type-II errors under the "small-n" regime typical of neural-graft studies.

### 6.10 Ancillary readouts and safety

Secondary readouts include (a) MRI volumetry of graft and peri-infarct cortex at weeks 4, 12, and 20 to assess organoid growth and lesion evolution; (b) single-nucleus RNA sequencing of graft tissue at experimental endpoint to confirm sustained regional identity and absence of tumorigenic transcriptional signatures (Itakura et al.; Deng et al.; Sugai et al.); (c) thorough histological pathology review for overgrowth and teratoma formation; and (d) inducible caspase-9 fail-safe integration in the iPSC line (Itakura et al.) to enable graft ablation if tumorigenesis is detected. Sections are imaged at multiple time points to document vascular anastomosis kinetics, which we compare against the F438 anastomosis prediction.

---

## 7. Mathematical Frameworks

This section consolidates the five quantitative frameworks introduced above and states one additional framework — the multiplicative-pillar closure model — that organizes the four preceding frameworks into a single testable claim.

### 7.1 F436 — Areal-identity reaction-diffusion system

Introduced in §2.4. A two-component reaction-diffusion system couples FGF8 ($c_{\mathrm{F}}$) to its target transcription factor EMX2 ($c_{\mathrm{E}}$), with mutual repression and localized anterior FGF8 secretion, predicting a minimum organoid diameter $\sim \sqrt{D_{\mathrm{F}}/\beta_{\mathrm{F}}}$ for stable single-gradient areal polarization.

### 7.2 F437 — Laminar birthdate Markov chain

Introduced in §3.3. A time-inhomogeneous Markov chain over progenitor and six-layer post-mitotic states, with Gaussian-birthdate transition kernels, yields the laminar composition as an integral over the progenitor pool and the time-dependent transition kernel. Fitting to observed CTIP2/SATB2 ratios reveals the experimental lever available for shifting deep-to-upper ratios.

### 7.3 F438 — Anastomosis first-contact kinetics

Introduced in §4.5. Host and graft capillary tips contact as a Poisson process with rate proportional to the product of tip densities and graft surface area; the number of patent anastomoses follows $N(t) = N_{\max}(1 - \exp(-\lambda t))$ under constant rate. Doubling pre-existing graft endothelial density halves the first-contact time; hypoxic-core radius shrinks exponentially with $N(t)$.

### 7.4 F439 — Wiring-correctness Wasserstein functional

Introduced in §5.8. The topographic correctness of graft thalamocortical wiring is quantified as the 2-Wasserstein distance between graft-termination and healthy-termination empirical distributions; the functional is interpretable and continuous.

### 7.5 F440 — Multiplicative per-pillar closure

We now unify the four preceding frameworks under a survival-style product:

```math
P_{\mathrm{recovery}} = \prod_{i=1}^{5} p_i
```

where $p_i$ is the closure probability of pillar $i$ — the probability that the $i$-th bottleneck is adequately addressed in a given graft configuration. Under the multiplicative hypothesis, the per-pillar closure required to achieve a target total recovery probability $P^*$ is:

```math
p^* = (P^*)^{1/5}
```

For a target recovery probability of 0.6 — the primary outcome of our preregistered experiment — the required per-pillar closure is $p^* = (0.6)^{1/5} \approx 0.903$. That is, each of the five pillars must be closed with approximately 90% probability. The multiplicative structure is consistent with the empirical record: single-pillar interventions (vasculature alone, lamination alone, area alone) produce sub-clinical recovery; only multi-pillar interventions produce large behavioral effects (Cao et al.; Somaa et al.). We label this the **F440 multiplicative-pillar closure model**.

The assumption of multiplicativity is a testable hypothesis. It predicts, specifically, that partial-compliance grafts (for example, an area-correct, laminar-correct graft *without* pre-vascularization) should produce recovery below the sub-ceiling determined by the weakest pillar — not an additive penalty. The preregistered experiment in §6 can be extended with a pillar-ablation arm (graft with no ETV2 pre-vascularization, for example) to directly test the multiplicativity hypothesis.

### 7.6 Relationship to prior mathematical frameworks

The repository's prior frameworks F1–F435 cover, among other domains, morphogen gradients in whole-body delivery (F328–F333 in the spatial tissue-engineering work of draft 55), epigenome-engineering kinetics (F381–F385 in draft 68), and reprogramming depth hierarchies (F292–F297 in draft 49). F436–F440 introduced here are, by construction, non-overlapping with all preceding frameworks because their object of study is the integration of an organoid graft into a stroke-lesioned host cortex — a regime in which area identity, laminar birthdate kinetics, capillary anastomosis, and topographic wiring correctness are the specific coupled bottlenecks, and the multiplicative-closure framework at F440 is specific to the five-pillar cortical-repair thesis.

---

## 8. Open Questions and Refinements

### 8.1 Scalability from mm³ to cm³

The clear scientific limit of the current literature is scale. All published cortical-graft stroke models operate at lesion volumes of ~1–10 mm³, whereas middle-cerebral-artery stroke in humans produces lesions of 10–100 cm³ — an order-of-magnitude-times-1000 gap. Achieving functional repair at the clinical scale requires vascular anastomosis sufficient to support centimeter-scale grafts, distributed area-identity patterning (a motor-cortex lesion and a somatosensory-cortex lesion cross area boundaries), and long-range cortico-cortical integration rather than local integration. Scaffold-supported multi-region assembloids patterned with morphogen microfluidics are a plausible engineering path, but the scale-up math — how far F438 anastomosis kinetics carries into a cm³ graft — is untested. The rate-limiting step at scale may prove to be the capillary tip-cell density achievable with ETV2 induction, which the Kistemaker 2025 review suggests has been under-characterized (Kistemaker et al.).

### 8.2 Chronic versus acute stroke

The proposed experiment grafts at one week post-lesion, inside the subacute phase during which the peri-infarct microenvironment is pro-regenerative (Ballout et al.; Yamagami et al.). Clinical stroke patients seeking graft therapy are typically years post-event, with a fully-formed glial scar, collapsed peri-infarct vasculature, and atrophied thalamocortical input to the lost cortex. Whether the thalamocortical axons that would innervate the graft in a chronic lesion remain able to project into fresh tissue is open. The Cao 2023 study grafted in the subacute phase; no published study addresses graft thalamocortical innervation at 1+ year post-stroke. Chronic-stroke grafting is an essential next step that our preregistered experiment deliberately does not attempt, in order to isolate the pillar closures from the chronic-scar variable.

### 8.3 Area-specific patterning precision

Bertacchi 2023 demonstrated that FGF8 shifts regional gene expression in cerebral organoids (Bertacchi et al.), but the precision achievable for a specific sub-area — for example, caudal forelimb area versus rostral forelimb area within the motor cortex — has not been experimentally quantified. Area identity is a continuum within a cortical lobe, and the resolution of the FGF8/EMX2 gradient system may be insufficient to specify sub-area identity. A near-term research priority is high-resolution single-nucleus transcriptomic comparison of organoids differentiated under graded FGF8 doses against a human motor-cortex reference atlas.

### 8.4 Laminar ratio precision

The Yamashita 2025 report of 16.4% CTIP2+ and 47.3% SATB2+ in iPSC-derived cortical neuron grafts (Yamashita et al.) is displaced from the adult motor-cortex ratio. F437 permits design of a temporally-gated transcription-factor regime to restore the ratio, but whether the ratio must be adult-like or whether developmental proportions suffice for adult motor-cortex function is open. Both possibilities have precedent: Revah 2022 transplanted neonatal-stage organoids into neonatal hosts and observed functional integration (Revah et al.), suggesting adult ratios may not be required, while the area-specificity failure of motor-cortex graft in Espuny-Camacho 2018 suggests laminar order matters (Espuny-Camacho et al.).

### 8.5 Long-term integration beyond 20 weeks

Revah 2022 followed grafts for many months and observed progressive maturation (Revah et al.); Somaa 2017 followed scaffold-supported grafts for 9 months and observed progressive motor improvement (Somaa et al.). Our preregistered experiment ends at week 20 to match the well-documented time window for synaptic refinement closure (Keck et al.; Lopez-Ortega et al.). An extension to week 52 is prespecified as a secondary experiment, to detect potential late-stage decline (graft atrophy, immune rejection) or late-stage refinement (network precision improvements).

### 8.6 Direct reprogramming as a complementary strategy

Direct in vivo reprogramming of reactive astrocytes to induced neurons, via NeuroD1 or alternative transcription factors, offers an orthogonal path that circumvents the transplant step entirely (Guo et al.; Ge et al.; Jiang et al.). The approach has demonstrated functional neuron generation in rodent and non-human primate stroke models but has been challenged by reports that some of the converted neurons were not actually of astrocyte origin. Whether direct reprogramming and cortical-organoid transplantation are competing or combinable remains open; the most plausible combination uses direct reprogramming to seed a pro-regenerative astrocyte/microglial environment at the lesion and organoid transplantation to provide the structural and area-identity scaffold.

### 8.7 Tumorigenicity monitoring

iPSC-derived grafts must satisfy three separate safety thresholds: absence of residual pluripotent cells (teratoma risk), absence of malignant transformation (genomic instability monitoring), and graft-size control (excess overgrowth). Itakura 2017 demonstrated that inducible caspase-9 integrated into iPSC lines ablates ~95% of iPSC-derived neural stem cells in vivo upon AP1903 treatment, providing a pharmacologic fail-safe (Itakura et al.). Sugai 2016 and Deng 2018 detail the histological phenotypes of transplanted iPSC-NSPCs and argue that genomic-instability screening of the source iPSC line is the most reliable predictor of tumorigenic risk (Sugai et al.; Deng et al.). We include iCaspase-9 in our preregistered iPSC line.

### 8.8 Immune tolerance

Our preregistered mouse experiment is either autologous (MHC-matched) in the translational frame or immunodeficient in the test frame. Clinical translation requires either autologous iPSC (technically and economically challenging at scale), banked HLA-matched allogeneic iPSC, or hypoimmune engineering of the iPSC line (B2M knockout, CIITA knockout, CD47 overexpression) — the last of which has been demonstrated in independent cell-therapy indications. Hypoimmune engineering is out of scope for this manuscript but is the most probable clinical-translation route.

### 8.9 The glymphatic compatibility question

The glymphatic system — the brain's bulk-flow clearance network — depends on astrocytic AQP4 polarization and perivascular spaces (not cited in prior drafts in this specific framing). Whether graft tissue recapitulates glymphatic architecture sufficient to clear extracellular waste at in vivo rates is a separate open question, relevant particularly for long-term graft survival and for Alzheimer's-related applications where defective glymphatics interact with amyloid clearance. No cortical graft study to date has systematically assessed glymphatic integration; this is an open research priority.

---

## 9. Conclusion

We have argued that functional repair of neocortical tissue requires simultaneous closure of five coupled bottlenecks — area identity, laminar cytoarchitecture, vascular anastomosis, host–graft circuit integration, and a causally-testable functional readout — and that in the current literature the rate-limiting bottleneck is a specific form of Pillar IV: a cell-type-selective causal demonstration that graft activity, not peri-infarct host plasticity catalyzed by the graft, mediates recovered behavior in the focal motor-cortex stroke paradigm. We have introduced five new quantitative frameworks covering areal morphogen polarization, laminar birthdate dynamics, anastomosis first-contact kinetics, topographic wiring correctness, and multiplicative per-pillar closure. We have specified a single preregistered mouse experiment, n=24, powered at 0.83 for a Cohen's d = 1.2 behavioral effect, in which a graft-specific optogenetic silencing arm directly tests graft causality after a photothrombotic CFA stroke. The experiment is capable of rejecting the five-pillar framework on four independent outcomes — primary behavioral, optogenetic causal, anatomical integration, and F439 wiring correctness. The path from a successful mouse result to translational testing is indicated in the open-questions section: scale-up to cm³ lesions, grafting in chronic-stroke hosts, extended maturation beyond 20 weeks, and hypoimmune engineering are the four next-step scientific problems on the decadal timeline. If the preregistered experiment returns a pass on both the primary behavioral and the optogenetic causal outcomes, the Palma-Tortosa 2020 puzzle is resolved in favor of direct graft mediation for an area-patterned, laminar-correct, pre-vascularized graft — and the tissue-level repair program acquires the first published causal basis on which translational investment can proceed. If the preregistered experiment returns a pass on primary behavioral but a negative on optogenetic causal, the Palma-Tortosa result generalizes to organoid-format grafts, and the field's therapeutic target should shift toward maximizing graft-induced host plasticity rather than graft-circuit-level integration.

---

## References

Ballout, Nissrine, et al. "Characterization of Inflammation in Delayed Cortical Transplantation." *Frontiers in Molecular Neuroscience*, vol. 12, 2019, article 160.

Bertacchi, Michele, et al. "FGF8-Mediated Gene Regulation Affects Regional Identity in Human Cerebral Organoids." *eLife*, vol. 12, 2023, article e98096.

Britanova, Olga, et al. "Satb2 Is a Postmitotic Determinant for Upper-Layer Neuron Specification in the Neocortex." *Neuron*, vol. 57, no. 3, 2008, pp. 378–392.

Cakir, Bilal, et al. "Development of Human Brain Organoids with Functional Vascular-Like System." *Nature Methods*, vol. 16, no. 11, 2019, pp. 1169–1175.

Cao, Shi-Ying, et al. "Cerebral Organoids Transplantation Repairs Infarcted Cortex and Restores Impaired Function after Stroke." *NPJ Regenerative Medicine*, vol. 8, 2023, article 27.

Cheng, Michelle Y., et al. "Optogenetic Approaches to Target Specific Neural Circuits in Post-Stroke Recovery." *Neurotherapeutics*, vol. 12, no. 3, 2015, pp. 473–487.

Daadi, Marcel M., et al. "Optogenetic Stimulation of Neural Grafts Enhances Neurotransmission and Downregulates the Inflammatory Response in Experimental Stroke Model." *Cell Transplantation*, vol. 25, no. 1, 2016, pp. 85–98.

Deng, Junhao, et al. "Cell Transplantation for Spinal Cord Injury: Tumorigenicity of Induced Pluripotent Stem Cell-Derived Neural Stem/Progenitor Cells." *Stem Cells International*, vol. 2018, 2018, article 5653787.

Dong, Xin, et al. "Human Cerebral Organoids Establish Subcortical Projections in the Mouse Brain After Transplantation." *Molecular Psychiatry*, vol. 26, no. 7, 2020, pp. 2964–2976.

Espuny-Camacho, Ira, et al. "Human Pluripotent Stem-Cell-Derived Cortical Neurons Integrate Functionally into the Lesioned Adult Murine Visual Cortex in an Area-Specific Way." *Cell Reports*, vol. 23, no. 9, 2018, pp. 2732–2743.

Ge, Long-Jiao, et al. "In Vivo Neuroregeneration to Treat Ischemic Stroke Through NeuroD1 AAV-Based Gene Therapy in Adult Non-Human Primates." *Frontiers in Cell and Developmental Biology*, vol. 8, 2020, article 590008.

Gordon, Aaron, et al. "Long-Term Maturation of Human Cortical Organoids Matches Key Early Postnatal Transitions." *Nature Neuroscience*, vol. 24, no. 3, 2021, pp. 331–342.

Guo, Ziyuan, et al. "In Vivo Direct Reprogramming of Reactive Glial Cells into Functional Neurons after Brain Injury and in an Alzheimer's Disease Model." *Cell Stem Cell*, vol. 14, no. 2, 2014, pp. 188–202.

Hao, Yi-Xuan, et al. "Remodeling and Repair of the Damaged Brain: The Potential and Challenges of Organoids for Ischaemic Stroke." *Journal of Translational Medicine*, vol. 23, 2025, article 412.

Itakura, Go, et al. "Fail-Safe System against Potential Tumorigenicity after Transplantation of iPSC Derivatives." *Stem Cell Reports*, vol. 8, no. 3, 2017, pp. 673–684.

Jiang, Mei-Qing, et al. "Conversion of Reactive Astrocytes to Induced Neurons Enhances Neuronal Repair and Functional Recovery after Ischemic Stroke." *Frontiers in Aging Neuroscience*, vol. 13, 2021, article 612856.

Keck, Tara, et al. "Massive Restructuring of Neuronal Circuits during Functional Reorganization of Adult Visual Cortex." *Nature Neuroscience*, vol. 11, no. 10, 2008, pp. 1162–1167.

Kelley, Kevin W., et al. "Host Circuit Engagement of Human Cortical Organoids Transplanted in Rodents." *Nature Protocols*, vol. 19, no. 12, 2024, pp. 3542–3568.

Kistemaker, Lois, et al. "Vascularized Human Brain Organoids: Current Possibilities and Prospects." *Trends in Biotechnology*, vol. 43, no. 6, 2025, pp. 1345–1363.

Leone, Dino P., et al. "The Determination of Projection Neuron Identity in the Developing Cerebral Cortex." *Current Opinion in Neurobiology*, vol. 18, no. 1, 2008, pp. 28–35.

Li, Xiao-Hong, et al. "Brain Organoid Maturation and Implantation Integration Based on Electrical Signals Input." *Journal of Advanced Research*, vol. 65, 2024, pp. 167–182.

Linaro, Daniele, et al. "Xenotransplanted Human Cortical Neurons Reveal Species-Specific Development and Functional Integration into Mouse Visual Circuits." *Neuron*, vol. 104, no. 5, 2019, pp. 972–986.

Longo, Valentina, et al. "Transcranial Direct Current Stimulation Enhances Neuroplasticity and Accelerates Motor Recovery in a Stroke Mouse Model." *Stroke*, vol. 53, no. 5, 2022, pp. 1746–1758.

Lopez-Ortega, Elena, et al. "Stimulus-Dependent Synaptic Plasticity Underlies Neuronal Circuitry Refinement in the Mouse Primary Visual Cortex." *Cell Reports*, vol. 43, no. 4, 2024, article 114043.

Magni, Manuela, et al. "Brain Regional Identity and Cell Type Specificity Landscape of Human Cortical Organoid Models." *International Journal of Molecular Sciences*, vol. 23, no. 21, 2022, article 13301.

Matsui, Takeshi K., et al. "Vascularization of Human Brain Organoids." *Stem Cells*, vol. 39, no. 8, 2021, pp. 1017–1024.

McCrary, Myles R., et al. "Cortical Transplantation of Brain-Mimetic Glycosaminoglycan Scaffolds and Neural Progenitor Cells Promotes Vascular Regeneration and Functional Recovery after Ischemic Stroke in Mice." *Advanced Healthcare Materials*, vol. 9, no. 5, 2020, article 1900285.

Miskinyte, Giedre, et al. "Transcription Factor Programming of Human ES Cells Generates Functional Neurons Expressing Both Upper and Deep Layer Cortical Markers." *PLoS ONE*, vol. 13, no. 10, 2018, article e0204688.

Miura, Yuki, et al. "Engineering Brain Assembloids to Interrogate Human Neural Circuits." *Nature Protocols*, vol. 17, no. 1, 2022, pp. 15–35.

Moon, Seong-Keun, et al. "Both Compensation and Recovery of Skilled Reaching Following Small Photothrombotic Stroke to Motor Cortex in the Rat." *Experimental Neurology*, vol. 218, no. 1, 2009, pp. 145–153.

Moshayedi, Pouria, et al. "Systematic Optimization of an Engineered Hydrogel Allows for Selective Control of Human Neural Stem Cell Survival and Differentiation after Transplantation in the Stroke Brain." *Biomaterials*, vol. 105, 2016, pp. 145–155.

O'Leary, Dennis D. M., et al. "Area Patterning of the Mammalian Cortex." *Neuron*, vol. 56, no. 2, 2007, pp. 252–269.

Ondriš, Juraj, et al. "Functional Recovery through the Plastic Adaptation of Organoid Grafts in Cortical Tissue." *Cellular and Molecular Life Sciences*, vol. 82, 2025, article 118.

Palma-Tortosa, Sara, et al. "Activity in Grafted Human iPS Cell-Derived Cortical Neurons Integrated in Stroke-Injured Rat Brain Regulates Motor Behavior." *Proceedings of the National Academy of Sciences*, vol. 117, no. 16, 2020, pp. 9094–9100.

Pham, Missy T., et al. "Generation of Human Vascularized Brain Organoids." *NeuroReport*, vol. 29, no. 7, 2018, pp. 588–593.

Quezada, Alexa, et al. "An In Vivo Platform for Rebuilding Functional Neocortical Tissue." *Bioengineering*, vol. 9, no. 10, 2022, article 567.

Revah, Omer, et al. "Maturation and Circuit Integration of Transplanted Human Cortical Organoids." *Nature*, vol. 610, no. 7931, 2022, pp. 319–326.

Somaa, Fahad A., et al. "Peptide-Based Scaffolds Support Human Cortical Progenitor Graft Integration to Reduce Atrophy and Promote Functional Repair in a Model of Stroke." *Cell Reports*, vol. 20, no. 8, 2017, pp. 1964–1977.

Sugai, Keiko, et al. "Pathological Classification of Human iPSC-Derived Neural Stem/Progenitor Cells towards Safety Assessment of Transplantation Therapy for CNS Diseases." *Molecular Brain*, vol. 9, 2016, article 85.

Tatarishvili, Jemal, et al. "Human-Induced Pluripotent Stem Cells Improve Recovery in Stroke-Injured Aged Rats." *Restorative Neurology and Neuroscience*, vol. 32, no. 4, 2014, pp. 547–558.

Tomassy, Giulio Srubek, et al. "Area-Specific Temporal Control of Corticospinal Motor Neuron Differentiation by COUP-TFI." *Proceedings of the National Academy of Sciences*, vol. 107, no. 8, 2010, pp. 3576–3581.

Wahl, Anna-Sophia, et al. "Optogenetically Stimulating Intact Rat Corticospinal Tract Post-Stroke Restores Motor Control through Regionalized Functional Circuit Formation." *Nature Communications*, vol. 8, 2017, article 1187.

Wang, Cong, et al. "Infiltrating Cells from Host Brain Restore the Microglial Population in Grafted Cortical Tissue." *Scientific Reports*, vol. 6, 2016, article 33080.

Wang, Jian, et al. "Grafted Human ESC-Derived Astroglia Repair Spinal Cord Injury via Activation of Host Anti-Inflammatory Microglia in the Lesion Area." *Theranostics*, vol. 12, no. 9, 2022, pp. 4288–4309.

Wang, Shu-Na, et al. "Cerebral Organoids Repair Ischemic Stroke Brain Injury." *Translational Stroke Research*, vol. 11, 2019, pp. 983–1000.

Whye, Dosh, et al. "A Robust Pipeline for the Multi-Stage Accelerated Differentiation of Functional 3D Cortical Organoids from Human Pluripotent Stem Cells." *Current Protocols*, vol. 3, no. 8, 2023, article e841.

Wilson, Madison N., et al. "Multimodal Monitoring of Human Cortical Organoids Implanted in Mice Reveal Functional Connection with Visual Cortex." *Nature Communications*, vol. 13, 2022, article 7945.

Xu, Shi-Bo, et al. "Single-Cell Transcriptome Landscape and Cell Fate Decoding in Human Brain Organoids after Transplantation." *Advanced Science*, vol. 11, no. 22, 2024, article 2309408.

Yamashita, Hokuto, et al. "Transplantation of Human iPS Cell-Derived Cerebral Cortical Neurons Promotes Fine Motor Recovery in a Female Mouse Model of Ischemic Stroke." *Stem Cell Reviews and Reports*, vol. 21, no. 3, 2025, pp. 847–865.

Zhang, Wen, et al. "ROS-Triggered Biomimetic Hydrogel Soft Scaffold for Ischemic Stroke Repair." *Biomaterials*, vol. 312, 2025, article 122781.
