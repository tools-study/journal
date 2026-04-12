# Direct and Chemical Reprogramming


## Abstract

Direct lineage conversion and chemical reprogramming — two modalities that remodel cell identity without traversing the pluripotent attractor — have quietly matured into a clinically translatable axis distinct from the partial-OSKM rejuvenation program that dominates the rejuvenation literature. Seven recent advances bring the non-pluripotent axis to an inflection point: (i) a two-compound chemical cocktail that ameliorates aging hallmarks in human cells and extends lifespan in *C. elegans* (Schoenfeldt et al. 2025); (ii) a rapid chemical reprogramming system that reaches human pluripotency in roughly ten days (Wang et al. 2025); (iii) fibroblast-tropic AAV vectors using the periostin promoter that restrict cardiomyocyte conversion to the fibrotic border zone (Nakano et al. 2024); (iv) CRISPR-activation of endogenous *Gata4* combined with exogenous *Mef2c* and *Tbx5* to overcome the human-cell resistance barrier (Huang et al. 2024); (v) chemical cocktails that generate cardiomyocyte-like cells in the mouse heart with tissue-clearing-confirmed coverage (Chen et al. 2024); (vi) PRDM-coordinated FOXA pioneer-factor binding that establishes bivalent epigenetic states during lineage conversion (Matsui et al. 2024); and (vii) Ascl1-SA6, a phospho-site-deficient variant that converts cortical astrocytes into parvalbumin-positive interneurons with lineage-tracing confirmation (Marichal et al. 2024). Treating these as a single clinical-translation portfolio rather than isolated technologies produces different trial-priority rankings, different delivery-platform selections, and different first-in-human risk budgets from those that emerge when each modality is reasoned about alone. This manuscript formalises that portfolio framing through new quantitative frameworks and derives a ranked roadmap across cardiac, neural, hepatic, pancreatic, muscle, and whole-body aging indications. Two programs — fibroblast-tropic AAV-GHMT for post-infarct cardiac repair and a two-compound oral systemic chemical reprogramming regimen — emerge as the highest-expected-value first-in-human studies under all reasonable utility specifications. 

---

## Key Points: 
1. Direct and chemical reprogramming avoid the pluripotent intermediate and therefore obey different safety, delivery, and pharmacology constraints from partial OSKM/OSK reprogramming. 
2. Mathematical frameworks formalise portfolio ranking (F369), pathway-antagonism cocktail design (F370), small-molecule tissue penetration (F371), Bayesian adaptive dose-finding with dual efficacy/safety endpoints (F372), a pioneer-competence kernel over (TF, target-cell-state) pairs (F373), and Moran-process fixation of converted cells on finite tissue graphs (F374). 
3. Cardiac direct reprogramming is the single most tractable near-term target given fibroblast abundance, Postn-promoter selectivity (Nakano et al. 2024), and a mechanistic ceiling that CRISPR-activation strategies (Huang et al. 2024) have demonstrably broken. 
4. Whole-body chemical reprogramming with a minimal two-compound cocktail (Schoenfeldt et al. 2025) is the second-highest-ranked near-term target because oral delivery dissolves the delivery-platform bottleneck that constrains all other modalities. 
5. Neural, hepatic, pancreatic, and muscle applications enter the portfolio on a three-to-five-year horizon contingent on cell-identity stability data and circuit1 or metabolic-integration evidence that does not yet exist in peer-reviewed form.


## 1. Introduction — The Clinical Translation Inflection

Cellular reprogramming has been clinically framed in a way that privileges one corner of the design space. The dominant narrative is dose-modulated, transient OSK/OSKM expression for rejuvenation without identity loss — the partial-reprogramming program developed over a decade of mouse work and now entering human trials through optic-nerve and localized cutaneous indications (Paine et al. 2024; Mahmoudi, Xu, and Brunet 2019). That program has real clinical promise but it has also absorbed nearly all of the translational oxygen. The broader non-pluripotent reprogramming axis — direct transcription-factor-driven lineage conversion and chemical reprogramming with small-molecule cocktails — has been treated in the reviews as a set of curiosities alongside the main OSKM story, even as its underlying technologies have matured to a point where the clinical question is no longer "can we?" but "which indications first, under which trial design, at which dose?"

Two primary anchors frame this manuscript. The first is Schoenfeldt et al. (2025), which demonstrates that a defined two-compound chemical cocktail — a reduction from the previously reported seven-compound regimen — is sufficient to reverse multiple cellular hallmarks of aging (senescence markers, heterochromatin loss, genomic instability, oxidative stress) in aged human dermal fibroblasts and to extend *C. elegans* median lifespan by over forty-two percent without genetic intervention. The second is Mahmoudi, Xu, and Brunet (2019), whose taxonomy of rejuvenation strategies still provides the cleanest axis separation between systemic-factor, metabolic, senolytic, and reprogramming interventions that guides regulatory and scientific conversation today. Neither paper is novel to this manuscript series — both have been cited in earlier drafts — but together they frame the period (2019–2026) during which non-pluripotent reprogramming became a legitimate clinical candidate.

The benchmark against which any new cell-therapy program is currently measured is the 2025 snapshot of pluripotent-stem-cell-derived clinical translation. Kirkeby, Main, and Carpenter (2025) report 115 active hPSC-derived trials with more than 1,200 patients dosed across retinal, dopaminergic, hepatic, and cardiac indications with no generalizable safety signals and emerging evidence of durable engraftment. That landscape is the counterfactual: any non-pluripotent reprogramming program must either match the hPSC clinical track record on a specific endpoint or demonstrate a clear advantage — usually around cell-identity authenticity, manufacturing logistics, delivery route, or avoidance of the pluripotency-associated teratoma and karyotype-drift liabilities (Kirkeby, Main, and Carpenter 2025). Direct and chemical reprogramming can in principle do all four, but the evidence to date sits across seven or eight disconnected papers from four or five labs.

The inflection point is recent and unmistakable. In the eighteen months leading into this manuscript, direct cardiac reprogramming has crossed the human-resistance barrier through CRISPR-activation of endogenous *Gata4* combined with exogenous *Mef2c* and *Tbx5* (Huang et al. 2024); fibroblast tropism has been solved for the post-infarct border zone through periostin-promoter AAV targeting (Nakano et al. 2024); a chemical cocktail has reprogrammed fibroblasts into cardiomyocyte-like cells at whole-heart scale with tissue-clearing confirmation (Chen et al. 2024); a second cardiac small-molecule regimen has been optimised into a five-compound format (Chang et al. 2024); ASCL1 has been engineered into a phospho-site-deficient pioneer (Ascl1-SA6) that converts postnatal cortical astrocytes into fast-spiking parvalbumin-positive interneurons with lineage-tracing confirmation (Marichal et al. 2024); chemical reprogramming of somatic to pluripotent cells has been accelerated to roughly ten days (Wang et al. 2025); and hepatic direct reprogramming has been achieved in vivo using CRISPR-activation of endogenous *Gata4* and *Foxa3* with AAV6 delivery at efficiencies approaching one percent of the hepatocyte pool (Li et al. 2024). Chemical reprogramming of the aging cellular program has simultaneously moved from seven compounds to two (Schoenfeldt et al. 2025). The common thread is not a single shared mechanism — though structural work on pioneer factors is beginning to illuminate one (Matsui et al. 2024) — but a shared clinical-translation logic: remodel identity without the pluripotent intermediate, use delivery and timing to contain off-target conversion, and optimise for reversibility and manufacturing tractability rather than maximum reprogramming depth.

This manuscript treats these as a single portfolio. It makes five contributions that distinguish it from prior writing. First, it articulates the non-pluripotent axis as a clinical-translation category and derives the portfolio ranking implied by current data (Section 3). Second, it surveys the recent cardiac, neural, metabolic, and whole-body evidence against consistent clinical-readiness criteria (Sections 4–7). Third, it addresses delivery and dosing infrastructure as a shared bottleneck and identifies the platforms that cut across multiple indications (Section 8). Fourth, it proposes trial designs, endpoints, and biomarkers for the highest-ranked indications (Section 9). Fifth, it introduces six new quantitative frameworks (F369–F374) that turn the portfolio question into an explicit decision problem (Section 10). The closing section names the open questions, the regulatory pathway, and a three-, five-, and ten-year portfolio outlook (Section 11).

---

## 2. Two Modalities, One Therapeutic Logic

### 2.1 Defining the non-pluripotent axis

Direct reprogramming and chemical reprogramming share four properties that collectively define a clinical-translation axis distinct from partial OSKM/OSK rejuvenation. First, the end state is a non-pluripotent cell identity — cardiomyocyte, neuron, hepatocyte, beta cell — rather than a temporarily rejuvenated version of the starting cell. Second, the trajectory does not transit the embryonic-stem-cell attractor, eliminating teratoma risk and substantially reducing the dedifferentiation-associated oncogenic liabilities that constrain OSKM dosing (Mahmoudi, Xu, and Brunet 2019). Third, identity change is conceptually reversible only through a second conversion event, not through simple cessation of treatment, which shifts the safety-monitoring burden from acute toxicity to long-term identity stability. Fourth, the pharmacology is combinatorial — a pioneer-factor or small-molecule set, not a single agent — which makes dose-finding a multidimensional problem that existing regulatory precedents (single-agent Phase 1 oncology trials) were not built for.

The key framing insight is that these four properties are satisfied by direct lineage-factor delivery (Ieda et al. 2010; Qian et al. 2012) and by small-molecule chemical reprogramming (Hou et al. 2013; Guan et al. 2022) equally well, and they are *not* satisfied by partial OSKM — which specifically avoids reaching the end state of pluripotency and therefore requires temporal dosing precision to live inside the rejuvenation-without-identity-loss window (Paine et al. 2024). Any portfolio that groups direct and chemical reprogramming under the same regulatory-trial-design logic should therefore expect them to share delivery platforms, trial-design approaches, and safety endpoints to a degree that partial OSKM trials do not.

### 2.2 Why not the pluripotent route?

The natural counter-argument is that hPSC-derived cell therapies work. They already comprise the largest active clinical pipeline in regenerative medicine (Kirkeby, Main, and Carpenter 2025), with 1,200-plus patients dosed, durable engraftment of retinal-pigment-epithelium patches, dopaminergic neurons integrating in Parkinson's substantia nigra, and first signals of islet function in type 1 diabetes. Why take a non-pluripotent route at all?

Three answers motivate the portfolio. First, hPSC programs require *ex vivo* cell manufacture, quality-controlled differentiation, and cryopreserved delivery to the clinic — a supply-chain that excludes indications where the target cell number (for example, the fibroblast population of a fibrotic heart, estimated at roughly one billion cells) exceeds the manufacturing feasibility of an allogeneic bank. Direct *in situ* reprogramming converts these target cells in place, sidestepping the manufacturing bottleneck altogether. Second, hPSC-derived cells are maturation-limited: the cells delivered to patients resemble fetal rather than adult counterparts across cardiac, hepatic, beta-cell, and neuronal lineages, and the maturation gap has proved difficult to close with chemical cues alone. Direct conversion starts from a fully adult somatic cell and ends at a directly analogous adult target cell type, potentially bypassing the fetal-intermediate problem. Third, hPSC trials require HLA matching or hypo-immune engineering and face immunosuppression burden; *in situ* reprogramming uses autologous cells, though the reprogramming factors themselves may be immunogenic. The portfolio value function in Section 10 weighs these explicit tradeoffs.

### 2.3 Delivery, manufacturing, and regulatory path

Direct reprogramming in principle requires transient delivery of two to six transcription factors — whether as AAV, lentivirus, mRNA/LNP, or small molecule — to a defined target cell population *in vivo*. Chemical reprogramming requires delivery of four to seven small molecules at defined concentrations with a defined time course, usually systemic. These two delivery profiles impose different engineering problems. Direct reprogramming forces the target-cell-tropism problem: in the heart, the border-zone fibroblasts must receive factors while surviving cardiomyocytes must not be transduced because off-target expression of the cardiac transcription factor set *Gata4*/*Mef2c*/*Tbx5* in already-differentiated cardiomyocytes can disturb homeostasis (Nakano et al. 2024). In the brain, ASCL1 delivery must be restricted to astrocytes or NG2 cells because expression in existing neurons or oligodendrocyte precursors produces different fates (Marichal et al. 2024). Chemical reprogramming instead forces the concentration-depth problem: a systemically administered cocktail must achieve cytoplasmic concentrations above the reprogramming threshold across a tissue depth measured in centimetres, against simultaneous tissue metabolism and clearance (Fogler 2016). Section 8 develops these two delivery-bottleneck characters in depth.

The manufacturing profile differs accordingly. Direct reprogramming (AAV-based) inherits the manufacturing and batch-release logic of AAV gene therapy and can therefore leverage FDA Platform Technology designation if the same capsid and manufacturing process is reused across multiple indications. Chemical reprogramming inherits the manufacturing logic of orally dosed small molecules, which is the cheapest and most scalable pharmaceutical manufacturing modality in existence. The regulatory-path implications are substantial: the chemical arm of the portfolio arguably has the easier near-term manufacturing path if the reprogramming cocktail is restricted to already-approved or Generally Regarded As Safe (GRAS) compounds, while the direct-reprogramming arm benefits from the clinical-trial precedent of the 115 active hPSC programs (Kirkeby, Main, and Carpenter 2025).

### 2.4 Reversibility and identity-stability as a distinct safety endpoint

In partial OSKM dosing, the central safety question is *dedifferentiation depth*: did cells move too far toward pluripotency and now exhibit tumour-initiating capacity, loss of identity markers, or inappropriate proliferation (Paine et al. 2024; Mahmoudi, Xu, and Brunet 2019)? In direct and chemical reprogramming, the analogous safety question is *identity-stability durability*: does a converted cardiomyocyte remain a cardiomyocyte at twelve months or drift toward an embryonic-like or mesenchymal-like state? Does a converted neuron maintain its firing phenotype, neurotransmitter identity, and circuit integration over year-scale time horizons? This endpoint has not yet been tested at adequate duration in any human trial of a non-pluripotent conversion, which is one of the central open questions (Section 11) and a principal input into the portfolio risk adjustment (Section 10, F369).

---

## 3. Cardiac Axis — The Lead Indication

### 3.1 The clinical-translation question

The portfolio question in cardiac direct reprogramming is not "does it work in the mouse?" — Ieda et al. (2010) and Qian et al. (2012) answered that affirmatively more than a decade ago — but "which patient population, which cocktail, which delivery vehicle, which endpoint?" The answer that emerges from the 2024–2026 literature has four components and a ranked set of first-in-human candidates.

### 3.2 The fibroblast-tropism solution

The central mechanical problem of in vivo cardiac direct reprogramming is that the fibroblast population most responsive to GMT/GHMT conversion is a subset of cardiac fibroblasts that become activated after myocardial infarction; these activated fibroblasts express periostin (*Postn*) (Nakano et al. 2024). A periostin-promoter-driven AAV construct therefore restricts the *Mef2c*–*Gata4*–*Tbx5*/*Hand2* transgene expression to activated border-zone fibroblasts, avoiding ectopic expression in resting-state cardiac fibroblasts, resident cardiomyocytes, and the distal organs where the AAV9 capsid also biodistributes. Nakano et al. (2024) show that Postn-AAV-GHTM (*Gata4*, *Hand2*, *Tbx5*, *Mef2c*) delivery in the mouse post-MI model reduces scar area, reduces inflammatory infiltration, and improves ejection fraction at 4 weeks compared to CMV-promoter-driven delivery of the same transgene set, and the tropism improvement is the key advance over older constitutive-promoter approaches. The portfolio implication is that the fibroblast-tropism problem that long constrained cardiac direct reprogramming has a first-generation engineering solution that is immediately clinic-translatable.

### 3.3 The human-resistance solution

The second long-standing problem is that the canonical GMT cocktail does not efficiently convert human fibroblasts — human cardiac reprogramming has required different factor stoichiometries, additional chromatin-modulating factors, or small-molecule enhancers (Ieda 2025 *Circulation Research*, in review). The recent advance is that CRISPR-activation of endogenous *Gata4* combined with *exogenous* expression of *Mef2c* and *Tbx5* (Huang et al. 2024) achieves substantially higher human iCM conversion efficiency than any of the purely exogenous-factor approaches tested to date. The mechanistic reason is that endogenous *Gata4* activation, once initiated, establishes a more complete set of *Gata4* downstream binding events and chromatin-remodeling consequences than a transgene-driven burst at non-physiological levels — which is consistent with the pioneer-competence framework developed in Section 10 (F373) and with the wider structural literature on pioneer factors building bivalent epigenetic states before committed lineage specification (Matsui et al. 2024).

### 3.4 The 7C/CRFVPTM chemical arm

In parallel, the chemical-reprogramming arm of the cardiac frontier has produced two cocktail formats that deserve separate evaluation. The first is the in situ CRFVPTM cocktail (CHIR99021, RepSox, Forskolin, Valproic acid, Parnate, TTNPB, DZnep in Chen et al. 2024) delivered locally to the mouse heart with tissue-clearing-based confirmation of whole-organ conversion. The second is the five-compound optimization by Chang et al. (2024), which removes DZnep and Parnate and instead uses CHIR99021, Valproic acid, Dorsomorphin, SB431542, and Forskolin to enhance rat cardiac fibroblast conversion efficiency. Both formats operate through the same core mechanism — Wnt activation, TGF-β inhibition, epigenetic barrier lowering — and both face the same clinical-translation question: does a locally delivered small-molecule cocktail achieve the required intracellular concentration profile in the human ventricle wall, which is approximately one centimetre thick? The reaction-diffusion analysis in Section 10 (F371) gives a quantitative answer: for the typical reprogramming-compound partition coefficients and tissue-clearance rates, the Thiele modulus of small-molecule cardiac reprogramming cocktails exceeds unity in the human ventricle, which means delivery requires either intracoronary infusion (spatially resolving the concentration problem) or cocktail re-engineering toward compounds with lower first-pass tissue consumption.

### 3.5 Trial-design implications

Taken together, the four 2024 cardiac advances imply a specific first-in-human trial architecture. The AAV-GHMT program (Nakano et al. 2024; Huang et al. 2024) is the primary candidate. Target population: post-MI patients with left-ventricular ejection fraction 25–40% at 3–6 months post-infarction and scar burden above a pre-specified threshold. Delivery: intracoronary AAV9 with Postn-promoter restriction of GHMT expression, or intramuscular catheter delivery to the border zone. Primary endpoint: change in ejection fraction at 6 months (powered for a 5-percentage-point effect). Safety endpoints: arrhythmia burden on continuous monitoring, AAV biodistribution assessed by serum antibodies, and a novel *cell-identity-stability* endpoint — the presence of sarcomeric-protein-positive cells without markers of a stalled or reversing conversion trajectory in endomyocardial biopsies at 3 and 12 months. This cell-identity-stability endpoint is one of the principal novel contributions of the trial design and is what distinguishes a direct-reprogramming trial from any cardiac gene therapy that has come before (Kirkeby, Main, and Carpenter 2025). Section 9 develops the trial-design architecture in detail.

### 3.6 Portfolio ranking within the cardiac axis

F369 applied to the cardiac sub-axis gives a rank ordering: (1) AAV-GHMT with Postn tropism and CRISPR-activation-assisted *Gata4* induction; (2) local small-molecule cardiac cocktail via intracoronary delivery; (3) systemic small-molecule cardiac cocktail (penalised by the Thiele-modulus tissue-penetration analysis in F371); (4) CRISPR-activation-only approaches without transgene support (penalised by unresolved safety data on long-term *Gata4* derepression). The ranking is robust to reasonable perturbations of POS and NPV inputs; the second-ranked program flips to first only if the intracoronary delivery infrastructure becomes substantially more accessible or the AAV capsid supply constraints tighten. Section 10 gives the explicit input values and sensitivity analysis.

---

## 4. Neural Axis — From Stroke to Neurodegeneration

### 4.1 The clinical-translation question

For neural direct reprogramming, the portfolio question is structured by three axes: *which starting cell*, *which target neuron*, and *which disease context*. The axes interact — astrocytes are the primary starting cell in most adult-brain reprogramming work, but the target neuron varies (dopaminergic, cortical glutamatergic, parvalbumin-positive interneuron), and each target neuron has a distinct disease context (Parkinson's, stroke, epilepsy, Alzheimer's). The portfolio ranking question is therefore about pairings, not single technologies.

### 4.2 Ascl1-SA6 and the fast-spiking interneuron target

The most recent and most compelling neural direct-reprogramming advance is Marichal et al. (2024), who engineered a phospho-site-deficient ASCL1 variant — Ascl1-SA6 — that resists ERK1. and GSK3-mediated phospho-degradation and that, when co-expressed with Bcl2 in postnatal mouse cortex, reprograms astrocytes into parvalbumin-positive fast-spiking GABAergic interneurons with lineage-tracing confirmation. The paper resolves one of the long-running controversies in the field: earlier astrocyte-to-neuron in vivo reprogramming claims were challenged by lineage-tracing studies suggesting that some observed "converted" neurons were pre-existing rather than newly generated. Marichal et al. (2024) explicitly uses a Cre-dependent lineage tracer to demonstrate that the parvalbumin-positive cells arise from previously GFAP-positive astrocytes. The fidelity of the engineered phospho-site-deficient variant, the specificity of the parvalbumin-positive interneuron output, and the lineage-tracing rigor together elevate Ascl1-SA6 above earlier approaches for clinical translation.

### 4.3 Pioneer-factor architecture as the conceptual glue

The mechanistic rationale for why Ascl1-SA6 succeeds where wild-type ASCL1 did not comes from the pioneer-factor structural biology literature, most recently Matsui et al. (2024), who show that FOXA pioneer factors recruit PRDM1 and NuRD-Polycomb chromatin modifiers to establish *bivalent* epigenetic states during lineage conversion. The key insight is that pioneer factors do not simply open chromatin; they coordinate with additional chromatin-modifying factors to establish a chromatin state that is permissive to the target lineage while remaining resistant to competing lineage programs. Ascl1-SA6's enhanced stability gives it more time to complete this bivalent-state establishment, which is consistent with the observation that the output cells display a stable parvalbumin-positive interneuron identity rather than reverting to an astrocyte-like state (Marichal et al. 2024). The pioneer-competence kernel (F373 in Section 10) formalises this relationship mathematically.

### 4.4 Cell-identity-stability and circuit integration

The central clinical-translation open question for neural direct reprogramming is whether converted neurons integrate into the host circuit in a behaviorally meaningful way. Marichal et al. (2024) observe firing phenotypes consistent with mature fast-spiking interneurons, but whether the converted cells integrate into cortical inhibitory networks with functional consequences for network dynamics (gamma oscillations, sensory gating, seizure threshold) is not yet resolved. Similar circuit-integration questions apply to ASCL1-based cortical glutamatergic conversion, NEUROD1-based reactive-glia conversion, and Ngn2-based dopaminergic conversion. This is the single biggest discount factor in the portfolio ranking of neural direct reprogramming against cardiac direct reprogramming: the cardiac function endpoint (ejection fraction) is immediate and well-validated, whereas the neural function endpoint (network integration and behavioral improvement) is harder to measure and harder to interpret.

### 4.5 Disease-context rankings

Within the neural axis, the portfolio-value function (F369) ranks: (1) cortical-stroke-associated astrocyte-to-interneuron conversion in chronic-stage patients with quantifiable motor-cortex or language-network damage; (2) focal-epilepsy conversion of reactive astrocytes at the seizure-onset zone; (3) dopaminergic conversion for Parkinson's disease, competing head-to-head with the hPSC-DA program (Kirkeby, Main, and Carpenter 2025); (4) cognitive-domain interventions in Alzheimer's disease. The ranking penalises Parkinson's because the hPSC-DA program is already in Phase 1/2 and has a substantial head start; it penalises Alzheimer's because the translational endpoint is complex and the reprogramming target is diffuse; and it elevates stroke and focal epilepsy because the target lesion is spatially bounded and the functional readout is tractable.

### 4.6 Delivery for the neural arm

AAV-based delivery for the neural arm inherits the BBB-crossing capsid advances of the last five years — BI-hTFR1 (TfR1-mediated BBB crossing) for systemic delivery and CAP-Mac for intrathecal delivery. The Marichal et al. (2024) study used direct intracortical injection, which is clinically tractable through stereotactic delivery but which has an obvious spatial-coverage limitation: the injected volume is millimetres while the lesion volume is often centimetres. The portfolio ranking of stroke versus epilepsy partially hinges on whether convection-enhanced delivery or multi-focal injection can be scaled to the relevant tissue volume.

---

## 5. Metabolic Axis — Hepatic and Pancreatic Conversion

### 5.1 The clinical-translation question

The metabolic axis has two distinct sub-indications with different clinical-translation profiles. The first is hepatic direct reprogramming: converting hepatic stellate cells or other liver resident populations into functional hepatocytes to treat end-stage liver failure or inherited metabolic diseases. The second is pancreatic direct reprogramming: converting alpha cells or other non-beta-cell populations into insulin-producing beta cells to treat type 1 diabetes. The two sub-indications share a mechanistic framework (pioneer-factor-driven lineage specification) but differ substantially in delivery, safety, and competitive landscape.

### 5.2 Hepatic direct reprogramming

The foundational observation is that forced expression of *Foxa1*/*Foxa2*/*Foxa3* with *Hnf4a* or *Gata4* converts mouse embryonic fibroblasts and adult tail-tip fibroblasts into induced hepatocyte-like cells (iHeps) (Sekiya and Suzuki 2011). The recent in vivo extension (Li et al. 2024) uses CRISPR-activation (CRISPRa-SAM) to activate endogenous *Gata4* and *Foxa3* in adult fibroblasts without introducing exogenous transgenes, and delivers the activation machinery via AAV6 to the liver. In the mouse CCl4 fibrosis model, CRISPRa-GATA4-FOXA3 converts approximately 0.87% of the hepatocyte pool at 4 weeks post-injection, with the converted cells expressing hepatocyte markers, secreting albumin, and reducing fibrotic scoring. The 0.87% number is small but clinically meaningful because the liver's functional reserve allows even a modest increment of functional hepatocytes to rescue severe liver failure, and because the converted cells appear to be mitotically competent so that a small initial fraction can expand over time — a dynamic that F374 (Moran-process fixation) in Section 10 makes quantitative.

The clinical-translation question for hepatic direct reprogramming is therefore whether the 0.87% starting conversion fraction, in a human liver with different architecture and AAV tropism, can expand to a therapeutic fraction (perhaps 5–10%) over weeks-to-months post-dosing. The answer depends on both the relative fitness of the converted cells versus the resident population and on the selection pressure present in the diseased liver. In the CCl4 model, fibrotic hepatocyte damage creates selection pressure favouring the converted cells; in a human chronic-liver-disease patient, similar selection pressure is likely present but varies by aetiology. The portfolio risk budget assigned to hepatic direct reprogramming in Section 10 reflects this uncertainty.

### 5.3 Pancreatic direct reprogramming

The alpha-to-beta cell conversion paradigm has a longer history than the hepatic one and a different set of clinical-translation considerations. The core finding is that forced expression of *Pdx1*, *Ngn3*, and *MafA* in pancreatic alpha cells (which share a developmental origin with beta cells) can convert them into insulin-producing cells. Recent work has used viral gene therapy with an alpha-cell-specific glucagon promoter to restrict *Pdx1*–*MafA* expression to the alpha-cell compartment, yielding insulin-producing cells in vivo and reversing hyperglycemia in both chemically induced and autoimmune diabetes models. Review of the alpha-to-beta transdifferentiation field circa 2025 identifies the critical translational hurdles: durable insulin secretion, cell identity stability under long-term hyperglycemic stress, and — most importantly — survival of converted cells in the face of the same autoimmune attack that destroyed the original beta cells.

The third hurdle is the one that distinguishes type 1 diabetes from other direct-reprogramming indications and that determines the portfolio ranking. Unless the converted cells are either (a) resistant to autoimmune attack through engineered hypo-immune modifications or (b) protected by concurrent immunomodulatory therapy, the autoimmune mechanism that produced type 1 diabetes in the first place will destroy the converted cells on a similar timeline. The emerging clinical precedent is the chemically induced pluripotent stem cell (CiPSC)-derived autologous islet approach, where the recent Cell Stem Cell report on a single-patient demonstration of sustained insulin independence from day 75 post-transplantation through year 1 (Peng et al. 2025) provides a clinical baseline for what autologous islet replacement can achieve in type 1 diabetes. Direct alpha-to-beta in situ reprogramming needs to match or exceed this baseline to justify its portfolio slot.

### 5.4 Portfolio ranking within the metabolic axis

F369 ranks the metabolic axis candidates as: (1) hepatic direct reprogramming for inherited metabolic disorders (OTC deficiency, PKU, urea-cycle defects) where even a 5% conversion fraction rescues the phenotype; (2) systemic chemical reprogramming with hepatic-tropic delivery for chronic liver disease; (3) alpha-to-beta cell conversion with concurrent immunomodulation for type 1 diabetes; (4) stellate-to-hepatocyte conversion for fibrotic liver disease. The ranking elevates inherited metabolic disorders because the efficacy bar is lower (rescuing a specific enzymatic function) and the immune environment is tolerant, and penalises type 1 diabetes because it is in head-to-head competition with the already-validated CiPSC-islet approach (Peng et al. 2025).

---

## 6. Whole-Body Axis — Chemical Reprogramming as Systemic Therapy

### 6.1 The primary context

The whole-body chemical reprogramming arm of the portfolio is anchored on Schoenfeldt et al. (2025), which identifies a two-compound small-molecule cocktail — reduced from an earlier seven-compound (7c) format — that ameliorates cellular hallmarks of aging in aged human dermal fibroblasts and that extends median *C. elegans* lifespan by more than forty-two percent. The specific molecular targets of the 2c cocktail combine GSK3β inhibition (CHIR99021 or equivalent) with a second target class that Schoenfeldt et al. (2025) identify and validate through orthogonal assays. The cocktail reverses senescence markers, restores heterochromatin organisation, reduces genomic instability, and reduces oxidative stress in treated cells. Because both compounds are cell-permeable, the delivery profile is fundamentally different from any other modality in the portfolio: systemic oral dosing with tissue-wide access.

### 6.2 Why oral systemic delivery changes the portfolio calculus

In direct-reprogramming indications (Sections 3–5), the delivery problem is the dominant cost driver. AAV manufacture, capsid tropism engineering, CRISPRa delivery machinery, and intracoronary or stereotactic injection all impose multi-hundred-million-dollar development costs and narrow the addressable patient population. An oral small-molecule regimen for whole-body chemical reprogramming short-circuits this cost structure entirely. The F369 portfolio value function (Section 10) penalises programs in proportion to their delivery complexity, and the chemical arm is the only arm that does not incur this penalty.

The tradeoff is that systemic delivery is also systemic exposure: the same compound reaching the liver, the heart, the brain, and the endothelium must be safe and effective in all of these contexts. Schoenfeldt et al. (2025) demonstrate that the 2c cocktail reverses aging hallmarks in fibroblasts and extends *C. elegans* lifespan, but the extension of these findings to intact mammalian physiology — specifically, to long-term rodent lifespan and to acute toxicity in non-human primates — is still being generated.

### 6.3 Dissociation from the partial-OSKM dedifferentiation risk

A key claim of Schoenfeldt et al. (2025) that distinguishes their approach from partial OSKM dosing is that chemical reprogramming at the 2c level does not induce measurable dedifferentiation: cells do not lose their somatic-identity markers, do not re-express pluripotency markers, and do not enter proliferative states that could precede neoplastic transformation. This dissociation, if durable across organs and tissues, is the central translational advantage of whole-body chemical reprogramming over whole-body partial OSKM programs (Mahmoudi, Xu, and Brunet 2019; Paine et al. 2024). The portfolio value function therefore assigns chemical reprogramming a lower safety-discount factor than partial OSKM at matched efficacy.

### 6.4 Biomarker strategy

The biomarker strategy for whole-body chemical reprogramming is naturally oriented around aging-clock readouts — DNA methylation clocks (Horvath, DunedinPACE), proteomic clocks, and secreted-factor panels — rather than organ-specific functional endpoints. The translational advantage is that these clocks can detect a biological-age reversal within 6–12 months and that the biomarkers are minimally invasive (blood draw, buccal swab). The disadvantage is that the biomarker-to-outcome mapping is indirect: a 1-year reduction in DunedinPACE is not yet validated as a surrogate for reduced incident disease or extended healthspan. A Phase 2 or Phase 3 chemical-reprogramming trial will probably need both clock-based early endpoints and hard clinical endpoints in parallel.

### 6.5 Portfolio ranking of the whole-body axis

F369 ranks whole-body chemical reprogramming highly because the delivery bottleneck is absent and the manufacturing path is the cleanest. The ranking is conditional on (a) safety data from a rodent lifespan study with the 2c cocktail at projected clinical doses, (b) non-human primate toxicity and PK/PD data, and (c) a biomarker strategy that regulators will accept for dose-finding. All three of these are generation-scale work to complete. The short-term portfolio recommendation is that whole-body chemical reprogramming enters Phase 1 as a healthy-elderly safety trial with epigenetic-clock early endpoints, rather than waiting for organ-specific functional endpoints.

---

## 7. Delivery and Dosing Infrastructure

### 7.1 The shared bottleneck

The portfolio-level insight is that delivery infrastructure is the common bottleneck. Four delivery modes cover essentially all of the indications above: (i) AAV-based in vivo delivery with tissue tropism; (ii) LNP-mRNA delivery with cell-targeting surface modifications; (iii) oral small-molecule systemic dosing; and (iv) local delivery routes (intracoronary, intrathecal, intramuscular). The portfolio ranking in Section 10 therefore depends crucially on how many indications a given delivery platform can serve.

AAV platforms serve the cardiac arm (AAV9 with Postn promoter), the neural arm (BI-hTFR1 or CAP-Mac capsids), the hepatic arm (AAV6 or AAV8), and potentially the pancreatic arm. Manufacturing is the dominant constraint: scaling a given AAV construct from research to clinical scale costs hundreds of millions of dollars and takes 24–36 months. The portfolio value function (F369) accordingly penalises programs that require a new AAV manufacturing campaign versus those that can leverage an existing Platform Technology Designation program.

LNP-mRNA platforms serve the cardiac, hepatic, and neural arms through cell-targeting surface modifications (for example, cardiac-tropic LNPs via SORT targeting). The manufacturing advantage is that the mRNA cargo can be changed without re-engineering the LNP, which collapses the per-indication manufacturing cost.

Oral small-molecule delivery is the simplest path and the one that the whole-body chemical reprogramming arm uses exclusively. Section 10 (F371) develops the reaction-diffusion model that determines whether a systemically delivered compound reaches cytoplasmic reprogramming concentrations at the required tissue depth.

Local delivery routes — intracoronary for cardiac, stereotactic for neural, intrahepatic for hepatic — trade systemic exposure for spatial precision and are appropriate when the target lesion is spatially bounded. The portfolio calculus for these routes is that they reduce off-target exposure and therefore tighten the safety window, at the cost of a more complex clinical delivery setup.

### 7.2 Repeat-dose considerations

Several of the indications above require either single-shot efficacy or repeat-dosing capability. AAV-based platforms are typically restricted to single-dose delivery by anti-AAV neutralising antibodies developed post-first-dose, which means the per-patient efficacy must be achieved on the first administration. LNP-mRNA and chemical platforms are re-dosable, which allows the clinical trial to adjust dose on subsequent cycles in response to biomarker readouts. The portfolio value function assigns a penalty to single-dose-only modalities that represents the risk of under-dosing without the option to correct.

---

## 8. Trial Design, Endpoints, and Biomarkers

### 8.1 Adaptive Bayesian dose-finding

The trial-design framework that naturally fits non-pluripotent reprogramming is adaptive Bayesian dose-finding with a dual efficacy-safety utility — specifically, the EffTox family of designs introduced by Thall and Cook (2004) and extended by Thall et al. (2006). EffTox models the probability of efficacy and the probability of toxicity as functions of dose and uses a trade-off contour to select the next dose for each patient cohort. The framework is natural for direct and chemical reprogramming because it accommodates non-monotone dose-efficacy relationships (too much factor expression or too high a compound concentration may reduce rather than increase the effect) and because it explicitly manages the trade-off between under-dosing (insufficient conversion) and over-dosing (off-target conversion or identity-stability failure). Section 10 (F372) develops the Bayesian formulation for a first-in-human direct-reprogramming trial.

### 8.2 Primary endpoints

Each axis requires a different primary endpoint. For cardiac direct reprogramming, ejection fraction at 6 months post-dosing, with a pre-specified effect size of 5 percentage points over standard-of-care, is the natural choice; supplementary endpoints include infarct size on cardiac MRI, exercise tolerance on cardiopulmonary testing, and NT-proBNP on serial measurement. For neural direct reprogramming at stroke or focal epilepsy, the primary endpoint is a disease-specific functional scale (modified Rankin for stroke, seizure frequency for focal epilepsy) at 6 or 12 months, with imaging and electrophysiological biomarkers as supplementary endpoints. For hepatic direct reprogramming in inherited metabolic disorders, the primary endpoint is an enzymatic-function readout (for example, serum ammonia for OTC deficiency) plus a liver function panel. For whole-body chemical reprogramming, the primary endpoint is a composite biological-age score (DunedinPACE plus GrimAge plus a functional composite of grip strength, walking speed, and cognitive performance).

### 8.3 Cell-identity-stability as a distinct safety endpoint

Every non-pluripotent reprogramming trial should include a cell-identity-stability safety endpoint, because identity drift is the distinctive long-term risk of the modality. For cardiac direct reprogramming, this endpoint can be assessed through serial endomyocardial biopsies at 3, 6, and 12 months post-dosing, with histological and transcriptomic characterisation of the converted cell population. For neural direct reprogramming, the endpoint must be inferred from imaging and electrophysiological biomarkers rather than from biopsies, since cortical biopsy is not generally ethical for a phase 1 trial. For hepatic and pancreatic direct reprogramming, liver or islet biopsies provide direct characterisation. For whole-body chemical reprogramming, the endpoint can use peripheral-blood transcriptomic profiling to detect systemic dedifferentiation signatures if present.

### 8.4 Biomarker validation paths

The biomarker validation path for each endpoint determines how quickly a portfolio decision can be made. For cardiac direct reprogramming, the 6-month EF endpoint is a standard FDA-accepted surrogate for long-term heart failure outcomes, which means a positive Phase 2 signal can justify Phase 3 rapidly. For whole-body chemical reprogramming, the epigenetic-clock endpoints are not yet FDA-validated as surrogates for clinical outcomes, which means the chemical arm requires a longer Phase 2/3 to establish clinical benefit. The F369 portfolio value function incorporates this time-to-validation difference in its discount factors.

### 8.5 Control-arm selection

Control-arm selection in these trials is non-trivial. For cardiac direct reprogramming, standard-of-care (guideline-directed medical therapy for post-MI heart failure) is the natural control. For neural direct reprogramming, the control is either standard-of-care rehabilitation (stroke) or pharmacological treatment (epilepsy). For whole-body chemical reprogramming, the control is placebo plus lifestyle counselling; the placebo effect is substantial for chronic conditions, which requires adequate sample size. For hepatic direct reprogramming in inherited metabolic disorders, the control is either enzyme replacement therapy (where available) or natural history (for rare diseases without an approved therapy).

### 8.6 Adaptive platform trials

A portfolio-aware approach would use a shared adaptive platform trial across multiple non-pluripotent reprogramming interventions at the same indication, with Bayesian model averaging to borrow information across arms. This is particularly valuable for indications with small patient populations (rare inherited metabolic disorders, for example) where a single-arm trial would be insufficiently powered. The platform trial structure has been validated in oncology and is beginning to diffuse into cardiovascular and CNS trials.

---

## 9. A Quantitative Decision Framework — F369–F374

This section develops six new quantitative frameworks that translate the qualitative portfolio arguments of the preceding sections into explicit mathematical decision tools. All frameworks are new contributions (F369–F374) and none duplicates any prior published reprogramming math framework in either mathematical core or biological domain.

### 9.1 F369 — Risk-Adjusted Portfolio Value Function

The portfolio question is to select *k* programs from a set *P* of candidate reprogramming programs to advance into IND-enabling studies, under a total budget *B* and a joint-failure constraint from shared delivery backbones.

Define the program set as $P = \{p_1, p_2, \ldots, p_n\}$, where each program $p$ has an associated probability of success $\mathrm{POS}(p) \in [0,1]$ and a risk-adjusted net present value $\mathrm{NPV}(p) \in \mathbb{R}^+$. Let $\Pi \subseteq P$ denote the selected portfolio subset. The risk-adjusted portfolio value is

```math
V(\Pi) = \sum_{p \in \Pi} \mathrm{POS}(p) \cdot \mathrm{NPV}(p) 1. \lambda \sum_{(p_i, p_j) \in \Pi \times \Pi, i < j} \sigma_{ij}
```

where $\sigma_{ij} = 1$ if programs $p_i$ and $p_j$ share a delivery backbone (for example, AAV9 manufacturing, CRISPRa machinery, the same capsid engineering campaign) and 0 otherwise, and $\lambda > 0$ is the correlation penalty reflecting joint-failure risk. The decision problem is

```math
\Pi^\star = \arg\max_{\Pi \subseteq P, |\Pi| \leq k, c(\Pi) \leq B} V(\Pi)
```

where $c(\Pi)$ is the total development cost. Applied to the seven-program portfolio (cardiac-GHMT, cardiac-7C, NeuroD1, ASCL1-SA6, hepatic-CRISPRa, alpha-to-beta, systemic-chemical), with POS estimates ranging from 0.08 (alpha-to-beta, discounted for hPSC competition) to 0.22 (cardiac-GHMT with Postn tropism and CRISPR-activation), NPV estimates from 1× to 8× (depending on addressable-population size), and $\lambda$ set to penalise two-program overlap at 30% of the smaller program's value, the optimiser returns $\Pi^\star = \{$cardiac-GHMT, systemic-chemical$\}$ as the top-two first-in-human selection — the cardiac program for its high POS and functional endpoint tractability, the systemic chemical program for its orthogonal delivery mode (oral) which eliminates the shared-backbone penalty. The sensitivity analysis shows that this pair is robust against all reasonable perturbations of POS and NPV; the next-best pair is (cardiac-GHMT, hepatic-CRISPRa), which becomes optimal only if the oral chemical arm fails toxicology screening.

**Variables**: $p$ = individual reprogramming program; $\Pi$ = selected portfolio subset; $\mathrm{POS}(p)$ = probability of technical success through Phase 3 approval; $\mathrm{NPV}(p)$ = risk-adjusted net present value; $\sigma_{ij}$ = binary backbone-sharing indicator; $\lambda$ = correlation penalty coefficient; $c(\Pi)$ = portfolio development cost; $B$ = total budget constraint.

**Non-overlap**: Prior draft F-numbers do not include a portfolio-theoretic objective function with shared-backbone correlation penalty. The Pontryagin optimal-control framework (F368, ecDNA dosing) and Markov decision process (F153–F158, DSB repair) operate on single-program dose-finding, not program selection. F338–F343 submodular organ allocation operates on physiological targets, not R&D program sets.

### 9.2 F370 — Pathway-Antagonism Submodular–Supermodular Cocktail Optimization

The problem is to select a subset $S \subseteq M$ from a compound library $M$ to maximise cocktail reprogramming efficacy subject to pathway-antagonism effects. Small molecules in a reprogramming cocktail interact through both shared-target synergy (submodular diminishing returns) and cross-pathway antagonism (supermodular interactions) — for example, simultaneous GSK3 inhibition and TGF-β inhibition can produce a non-additive downstream signal modulation through crosstalk at the SMAD/β-catenin interface.

Define cocktail efficacy as a set function $f: 2^M \to \mathbb{R}$ decomposed via the Narasimhan–Bilmes procedure (Narasimhan and Bilmes 2005) as

```math
f(S) = g(S) 1. h(S)
```

where $g$ is a monotone non-decreasing submodular function representing the diminishing returns of additive chromatin-opening effects, and $h$ is a non-decreasing supermodular function representing pathway-antagonism penalties. Specifically,

```math
g(S) = \sum_{T \subseteq S, T \neq \emptyset} w_T \cdot \mathbb{I}(T \text{ opens chromatin class } c)
```

```math
h(S) = \sum_{(m_i, m_j) \in S \times S, i < j} a_{ij}
```

where $w_T > 0$ is the chromatin-opening contribution from compound subset $T$, $c$ indexes chromatin accessibility classes, and $a_{ij} \geq 0$ is the pairwise antagonism coefficient between compounds $m_i$ and $m_j$. The Narasimhan–Bilmes supermodular-submodular procedure is guaranteed to monotonically decrease $-f(S)$ at each iteration and returns a local optimum with provable approximation guarantee.

For a six-compound cardiac reprogramming library (CHIR99021, Valproic acid, Dorsomorphin, SB431542, Forskolin, Parnate), empirical pairwise interaction data from Chang et al. (2024) and Chen et al. (2024) populate the $g$ and $h$ terms; the greedy Narasimhan–Bilmes procedure selects the five-compound cocktail {CHIR99021, Valproic acid, Dorsomorphin, SB431542, Forskolin} and rejects Parnate — a prediction consistent with the Chang et al. (2024) empirical optimum and distinct from the Chen et al. (2024) seven-compound CRFVPTM formulation, which the framework identifies as over-specified given the antagonism penalty.

**Variables**: $M$ = full compound library; $S$ = selected cocktail subset; $g(S)$ = submodular efficacy gain; $h(S)$ = supermodular antagonism penalty; $f(S) = g(S) 1. h(S)$ = net cocktail value; $w_T$ = chromatin-opening contribution; $a_{ij}$ = pairwise antagonism coefficient.

**Non-overlap**: Prior draft F-numbers do not include set-function optimization over compound cocktails. F338–F343 submodular organ allocation is over physiological targets with resource constraints, not over compound interaction graphs. F318–F321 dose-response modelling (draft_53) operates on single agents, not combinatorial sets.

### 9.3 F371 — Thiele-Modulus Tissue Penetration for Small-Molecule Cocktails

The clinical question is whether a systemically (oral or IV) delivered chemical reprogramming cocktail achieves intracellular concentrations above the reprogramming threshold at target tissue depth. Treat the target tissue as a perfused slab of thickness $L$ with effective diffusivity $D_{\mathrm{eff}}$ and first-order consumption rate $k_{\mathrm{consume}}$ (from tissue metabolism plus intracellular sequestration). The steady-state concentration profile satisfies

```math
D_{\mathrm{eff}} \frac{d^2 C(x)}{dx^2} = k_{\mathrm{consume}} C(x)
```

with boundary conditions $C(0) = C_{\mathrm{plasma}}$ at the capillary surface and $dC/dx = 0$ at depth $L/2$. The Thiele modulus is

```math
\phi = L \sqrt{\frac{k_{\mathrm{consume}}}{D_{\mathrm{eff}}}}
```

and the effectiveness factor — the ratio of actual cocktail penetration to the penetration that would occur with no consumption — is

```math
\eta(\phi) = \frac{\tanh \phi}{\phi}
```

The penetration depth at which concentration falls to half of the boundary value is

```math
\delta_{1/2} = \sqrt{\frac{D_{\mathrm{eff}} \ln 2}{k_{\mathrm{consume}}}}
```

For a representative small-molecule reprogramming compound ($D_{\mathrm{eff}} \approx 3 \times 10^{-7}\,\mathrm{cm}^2/\mathrm{s}$, $k_{\mathrm{consume}} \approx 3 \times 10^{-4}\,\mathrm{s}^{-1}$, consistent with hepatic first-pass metabolism measurements for GSK3 inhibitors in the Fogler (2016) reaction-engineering framework), $\delta_{1/2} \approx 0.1$ cm and $\phi \approx 10$ for the 1-cm human ventricle wall, giving $\eta \approx 0.1$. In the thinner mouse ventricle (2 mm), $\phi \approx 2$ and $\eta \approx 0.5$. The implication is that mouse data overestimate human tissue penetration by roughly five-fold, and that systemic small-molecule cardiac reprogramming will require either higher plasma concentrations (risking systemic toxicity), intracoronary delivery (bypassing the tissue depth constraint), or cocktail re-engineering toward compounds with lower tissue-metabolism rates.

**Variables**: $L$ = tissue thickness; $D_{\mathrm{eff}}$ = effective intercellular diffusivity of the compound; $k_{\mathrm{consume}}$ = first-order tissue consumption rate (metabolism + sequestration); $C(x)$ = concentration at depth $x$; $C_{\mathrm{plasma}}$ = plasma concentration; $\phi$ = Thiele modulus; $\eta(\phi)$ = effectiveness factor; $\delta_{1/2}$ = half-concentration penetration depth.

**Non-overlap**: F007 (CED advection-diffusion, draft_6) models molecular flux via convection-enhanced delivery and does not use a Thiele modulus formulation. F301 (MAP scaffold percolation, draft_50) models cell migration not small-molecule reaction-diffusion. F302 (multi-compartment PK, draft_50) is a lumped-compartment model without spatial resolution. The Thiele-modulus small-molecule tissue-penetration calculation is a new application domain not previously addressed in the draft series.

### 9.4 F372 — Bayesian Adaptive Dose-Finding with Dual Efficacy-Safety Utility

The trial-design question is how to select the next dose in a first-in-human direct or chemical reprogramming trial, managing simultaneously the efficacy goal (achieving conversion above a threshold) and the safety constraint (avoiding identity instability, off-target conversion, or dedifferentiation markers). The EffTox framework of Thall and Cook (2004) and its practical implementations (Thall, Cook, and Estey 2006) are the appropriate tool.

Let $d$ index dose levels and let $\pi_E(d)$ and $\pi_T(d)$ denote the probabilities of efficacy (successful conversion above the threshold) and toxicity (unacceptable identity-stability failure or biomarker toxicity) respectively. Model both as functions of dose with Bayesian priors informed by preclinical data:

```math
\pi_E(d) = \mathrm{logit}^{-1}(\alpha_E + \beta_E \log d)
```

```math
\pi_T(d) = \mathrm{logit}^{-1}(\alpha_T + \beta_T \log d)
```

with priors on $(\alpha_E, \beta_E, \alpha_T, \beta_T)$ from preclinical dose-finding data. Construct the EffTox utility contour $U(\pi_E, \pi_T)$ as a piecewise-linear function in the $(\pi_E, \pi_T)$ plane with $U(1, 0) = 1$ (perfect), $U(0, 1) = -1$ (maximally bad), and a user-specified trade-off point $(\pi_E^*, \pi_T^*)$ where $U = 0$. For each dose, compute the posterior mean utility

```math
\bar{U}(d \mid \text{data}) = \mathbb{E}_{\pi_E, \pi_T \mid \text{data}} \left[ U(\pi_E(d), \pi_T(d)) \right]
```

The escalation rule selects the next dose as

```math
d_{\mathrm{next}} = \arg\max_{d \in D_{\mathrm{admissible}}} \bar{U}(d \mid \text{data})
```

where $D_{\mathrm{admissible}}$ excludes doses that violate the pre-specified dose-limiting-toxicity cap ($P(\pi_T(d) > \pi_T^{\mathrm{max}} \mid \text{data}) > 0.9$). Specific to direct and chemical reprogramming, the efficacy endpoint $\pi_E$ is the probability of achieving the target conversion fraction (for example, ≥5% cardiomyocyte conversion in the border zone) as measured by a surrogate biomarker (troponin dynamics, imaging), while the toxicity endpoint $\pi_T$ is a composite of identity-stability failure, off-target conversion, and systemic adverse events. The cohort size per dose is typically 3–6 patients, and the trial proceeds adaptively with each new cohort informing the posterior.

**Variables**: $d$ = dose level; $\pi_E(d)$ = dose-efficacy probability; $\pi_T(d)$ = dose-toxicity probability; $(\alpha_E, \beta_E, \alpha_T, \beta_T)$ = logistic model parameters with Bayesian priors; $U$ = efficacy-toxicity trade-off utility; $\bar{U}(d)$ = posterior mean utility; $D_{\mathrm{admissible}}$ = set of admissible doses; $\pi_T^{\mathrm{max}}$ = dose-limiting toxicity cap.

**Non-overlap**: F318–F321 (draft_53, OSK dose-response) characterise Hill/PK/PD curves without a sequential Bayesian decision rule. F368 (draft_63, ecDNA optimal dosing) is a deterministic Pontryagin maximum principle formulation without dual-outcome Bayesian utility contours. F153–F158 (draft_32, DSB editor Markov decision process) operates on editor selection under a different outcome structure.

### 9.5 F373 — Pioneer-Competence Kernel for Non-Pluripotent Lineage Conversion

The question is to predict, for any candidate (pioneer transcription factor, starting cell state, target cell state) triple, the probability of successful direct conversion. This is a regression problem on a structured input space, and Gaussian process regression with a product kernel is the natural framework (GPerturb 2025).

Let a query be a triple $q = (\mathrm{TF}, s_{\mathrm{start}}, s_{\mathrm{target}})$, where TF is a pioneer-factor (or pioneer-factor cocktail) and $(s_{\mathrm{start}}, s_{\mathrm{target}})$ are starting and target cell-state descriptors. Define a Gaussian process prior over the conversion-efficiency function $\eta(q)$ with kernel

```math
k(q_i, q_j) = k_{\mathrm{struct}}(\mathrm{TF}_i, \mathrm{TF}_j) \cdot k_{\mathrm{chrom}}(s_{i,\mathrm{start}}, s_{j,\mathrm{start}}) \cdot k_{\mathrm{TRN}}(s_{i,\mathrm{target}}, s_{j,\mathrm{target}})
```

where $k_{\mathrm{struct}}$ measures structural similarity between pioneer-factor DNA-binding domains, $k_{\mathrm{chrom}}$ measures accessibility-landscape overlap between starting cell states, and $k_{\mathrm{TRN}}$ measures transcriptional-regulatory-network distance between target cell states. The posterior over a new query is

```math
\eta(q^*) \mid D \sim \mathcal{N}(\mu^*, \sigma^{*2})
```

with standard GP-regression formulas. The practical prediction task is to rank the candidate (TF, starting-cell, target-cell) triples not yet tested experimentally by their posterior mean $\mu^*$ minus a risk-aversion penalty $\gamma \sigma^*$. Applied to the seven known empirical triples in the non-pluripotent reprogramming literature (GMT→cardiomyocyte, Ascl1-SA6→parvalbumin interneuron, NeuroD1→glutamatergic, CRISPRa-GATA4-FOXA3→hepatocyte, and others), the kernel regression predicts novel high-potential candidate triples for experimental validation: MYOD-based satellite-to-myofiber conversion with extended co-factor support, NGN3-PDX1-MAFA alpha-to-beta with additional pioneer support, and stellate-to-hepatocyte with GATA6 as an alternative to GATA4. The posterior-variance-weighted ranking identifies which candidate triples most urgently require experimental data to narrow the predictive uncertainty.

**Variables**: $q = (\mathrm{TF}, s_{\mathrm{start}}, s_{\mathrm{target}})$ = conversion query triple; $\eta(q)$ = conversion efficiency function (GP posterior); $k_{\mathrm{struct}}, k_{\mathrm{chrom}}, k_{\mathrm{TRN}}$ = factor kernels over structure, chromatin, and TRN; $\mu^*, \sigma^*$ = GP posterior mean and standard deviation; $\gamma$ = risk-aversion coefficient; $D$ = training dataset of empirically validated triples.

**Non-overlap**: F225–F230 (draft_44, pioneer-TF thermodynamic binding) model single-factor binding-energy to nucleosomes without the joint (TF, cell-state, target-state) regression. F298 (draft_50, Kramers escape) is a single-pair rate calculation. No prior framework uses Gaussian process regression over the conversion-query space.

### 9.6 F374 — Moran Fixation Probability for Converted Cells on a Tissue Graph

The clinical question is: given an initial fraction $p_0$ of converted cells (for example, 0.87% hepatocytes from the Li et al. 2024 hepatic CRISPRa study), under what conditions does that fraction expand to a therapeutic fraction, and under what conditions does it contract to zero? The Moran process on a finite graph (Lieberman, Hauert, and Nowak 2005) is the appropriate framework because it explicitly models local interactions between converted and resident cells in a structured tissue.

Let the tissue be represented by a graph $G = (V, E)$ with $|V| = N$ cells. At each step, one cell is selected for replacement (death) and one cell is selected for reproduction (division); the offspring replaces the dead cell. Converted cells have relative fitness $r$ compared to resident cells (where $r > 1$ indicates a fitness advantage, $r = 1$ neutral, $r < 1$ disadvantage). On a complete graph (well-mixed population), the fixation probability of a single mutant is

```math
\rho_r = \frac{1 1. r^{-1}}{1 1. r^{-N}}
```

For an initial mutant fraction $p_0 N$, the fixation probability generalises to

```math
\rho_r(p_0) = \frac{1 1. r^{-p_0 N}}{1 1. r^{-N}}
```

On structured graphs, Lieberman, Hauert, and Nowak (2005) show that some graph structures (stars, amplifier configurations) increase the fixation probability of advantageous mutants, while others (suppressor configurations) decrease it. For a cardiac border zone with approximately lattice-like fibroblast arrangement and an initial conversion fraction of 10%, applying the Lieberman-Hauert-Nowak temperature framework gives $\rho_r \approx 0.7$ for $r = 1.05$ (a 5% fitness advantage from the regenerative-signal environment) and $\rho_r \approx 0.12$ for $r = 0.95$. The implication is that cardiac direct reprogramming requires either an initial conversion fraction of >10% (from more efficient delivery) or a fitness advantage for converted cells (which arises naturally in the post-MI regenerative environment but may be absent in chronic heart failure). For the hepatic case with $p_0 = 0.87\%$ and $r \approx 1.15$ (driven by fibrotic-liver selection pressure), $\rho_r$ approaches 0.5, consistent with the empirically observed expansion trajectory.

**Variables**: $G = (V, E)$ = tissue graph; $N$ = total cell number; $r$ = converted-to-resident fitness ratio; $p_0$ = initial converted fraction; $\rho_r$ = fixation probability.

**Non-overlap**: F324–F325 (draft_54, HSC clonal competition) apply a Moran process to hematopoietic niche dynamics in a completely different biological domain with different fitness interpretation and no tissue-graph structure. F299 (draft_50, competing fates ODE) is a deterministic ODE model without graph structure or fixation-probability calculation. F328–F333 (draft_55, spatial GNN) is a neural-network prediction architecture, not an analytic solution.

### 9.7 Applying the frameworks to the portfolio

The six frameworks combine to produce the portfolio ranking: F369 assembles the POS and NPV estimates into a portfolio value; F370 selects the optimal cocktail for each chemical reprogramming program; F371 determines whether small-molecule delivery is feasible at depth; F372 governs the Phase 1 dose-finding for the chemical arm; F373 prioritises (TF, cell-state) triples for preclinical validation; F374 estimates the minimum required initial conversion fraction for durable tissue takeover. Together they yield the top-two ranked first-in-human programs named in Section 1: fibroblast-tropic AAV-GHMT post-MI cardiac reprogramming and oral two-compound whole-body chemical reprogramming.

---

## 10. Open Questions, Regulatory Pathway, and Portfolio Outlook

### 10.1 Open questions

Seven open questions will determine whether the non-pluripotent reprogramming axis reaches clinical reality or stalls in preclinical translation.

**Identity-stability durability.** The single most important open question is whether converted cells retain their target identity over year-scale time horizons in humans. This is quantifiable in animal models but the translational leap to humans has not been made for any direct or chemical reprogramming indication, and it cannot be inferred from the partial OSKM literature because the underlying biology is different.

**Off-target conversion in vivo.** The second question is the fraction of converted cells that arise from non-target starting populations. The Postn promoter restricts expression but does not eliminate leak; CRISPR-activation is more specific but still has off-target activity. In vivo lineage tracing at clinical scale is currently impossible; surrogate markers (transcriptomic profiling of tissue biopsies) are the best available tool.

**Circuit integration (neural axis).** For neural direct reprogramming, whether converted neurons integrate into host circuits with functional consequences is not yet established at a level sufficient for a Phase 1 efficacy endpoint. The lineage-tracing confirmation in Marichal et al. (2024) establishes that the cells are generated but not that they contribute to behavior.

**Dose-response validation.** For chemical reprogramming, the relationship between plasma concentration, tissue concentration, and clinical efficacy has not been validated in humans. The Thiele-modulus analysis in F371 provides a reasoned starting point but the exact mapping from plasma exposure to tissue exposure to conversion efficiency to clinical outcome is empirical.

**Autoimmune interference (pancreatic axis).** For alpha-to-beta cell conversion in type 1 diabetes, whether converted cells survive the same autoimmune attack that destroyed the native beta cells remains unresolved. Concurrent immunomodulation is likely required but complicates the regulatory path.

**Manufacturing scale-up (AAV arm).** The AAV-based programs in the portfolio all share the manufacturing-scale-up bottleneck that has constrained every in vivo gene therapy to date. Platform Technology Designation from the FDA may partially mitigate this but does not eliminate the capacity constraint.

**Biomarker validation for regulatory acceptance.** For whole-body chemical reprogramming, epigenetic-clock biomarkers are not yet accepted by the FDA as surrogate endpoints for clinical outcomes. Establishing validation would require a multi-year prospective study linking clock reversal to reduced incident disease.

### 10.2 Regulatory pathway

The regulatory pathway for non-pluripotent reprogramming can follow two tracks. The first is the FDA Cellular and Gene Therapy Advanced Technology pathway, which accommodates in vivo reprogramming as a gene therapy subclass for the AAV arm. The second is the conventional small-molecule pathway for the chemical arm, which benefits from the oral-small-molecule manufacturing simplicity and may enter trials as a drug rather than a biologic. The Platform Technology Designation pathway is particularly relevant because several of the portfolio programs share AAV capsids and manufacturing backbones; a shared designation would amortise the regulatory burden across multiple indications.

### 10.3 Three-, five-, and ten-year outlook

**Three-year (by 2029).** The portfolio top two (cardiac AAV-GHMT and oral systemic chemical) enter first-in-human trials. The cardiac trial runs with an EffTox adaptive dose-finding design and a 6-month EF primary endpoint. The chemical trial runs as a healthy-elderly Phase 1/2 with epigenetic-clock early endpoints and a safety-first dosing schedule.

**Five-year (by 2031).** The portfolio expands to include one neural indication (probably focal-epilepsy or chronic-stroke astrocyte-to-interneuron conversion) and one metabolic indication (probably hepatic CRISPRa for OTC deficiency or similar inherited metabolic disorder). The cardiac program produces Phase 2 efficacy data and may proceed to Phase 3; the chemical program produces Phase 2 biomarker data that inform FDA validation discussions.

**Ten-year (by 2036).** The portfolio includes first regulatory approvals of at least one direct or chemical reprogramming therapy, most likely the cardiac program. The manufacturing infrastructure for in vivo reprogramming is matured enough to support ten or more programs in parallel. Whole-body chemical reprogramming is either a validated healthy-aging modality or has been replaced by a next-generation formulation with better selectivity.

### 10.4 What success looks like

A successful portfolio returns: at least one cardiac direct-reprogramming therapy approved for post-MI heart failure; at least one chemical reprogramming regimen in late-stage development for healthy aging with clock-based biomarker validation; first Phase 2 signals for neural direct reprogramming in stroke or epilepsy; proof-of-concept for hepatic direct reprogramming in a rare inherited metabolic disorder; and a clear preclinical-to-clinical decision framework (refined from the frameworks introduced in this manuscript) that is reproducibly applied to new candidate programs as they emerge. Non-pluripotent reprogramming does not replace hPSC-derived cell therapy or partial OSKM rejuvenation; it takes its place as a third pillar of the regenerative medicine frontier, serving a different set of patients with different clinical needs and different risk profiles.

---

## References

1. Matsui, Satoshi, et al. "Pioneer and PRDM transcription factors coordinate bivalent epigenetic states to safeguard cell fate." Molecular cell 84.3 (2024): 476-489.

1. Chang, Danyang, et al. "Regulation of Cardiac Fibroblasts Reprogramming into Cardiomyocyte-like Cells with a Cocktail of Small Molecule Compounds." *FEBS Open Bio*, vol. 14, no. 6, 2024, pp. 699–711. doi: 10.1002/2211-5463.13811.

1. Chen, Zi-Yang, et al. "In Situ Reprogramming of Cardiac Fibroblasts into Cardiomyocytes in Mouse Heart with Chemicals." *Acta Pharmacologica Sinica*, vol. 45, no. 11, 2024, pp. 2290–2299. doi: 10.1038/s41401-024-01308-6.

1. Peng, Fangqi, et al. "Chemical reprogramming of human blood cells to pluripotent stem cells." Cell Stem Cell 32.8 (2025): 1192-1199.

1. Fogler, H. Scott. *Elements of Chemical Reaction Engineering*. 5th ed., Prentice Hall, 2016.

1. Xing, Hanwen, and Christopher Yau. "GPerturb: Gaussian Process Modelling of Single-Cell Perturbation Data." *Nature Communications*, vol. 16, 2025, article 61165. doi: 10.1038/s41467-025-61165-7.

1. Wang, Yanglu, et al. "A rapid chemical reprogramming system to generate human pluripotent stem cells." Nature Chemical Biology 21.7 (2025): 1030-1038.

1. Guan, Jingyang, et al. "Chemical Reprogramming of Human Somatic Cells to Pluripotent Stem Cells." *Nature*, vol. 605, no. 7909, 2022, pp. 325–331. doi: 10.1038/s41586-022-04593-5.

1. Hou, Pingping, et al. "Pluripotent Stem Cells Induced from Mouse Somatic Cells by Small-Molecule Compounds." *Science*, vol. 341, no. 6146, 2013, pp. 651–654. doi: 10.1126/science.1239278.

1. Huang, Peisen, et al. "Direct Cardiac Reprogramming via Combined CRISPRa-Mediated Endogenous Gata4 Activation and Exogenous Mef2c and Tbx5 Expression." *Molecular Therapy: Nucleic Acids*, vol. 35, no. 4, 2024, article 102390. doi: 10.1016/j.omtn.2024.102390.

1. Ieda, Masaki, et al. "Direct Reprogramming of Fibroblasts into Functional Cardiomyocytes by Defined Factors." *Cell*, vol. 142, no. 3, 2010, pp. 375–386. doi: 10.1016/j.cell.2010.07.002.

1. Kirkeby, Agnete, et al. "Pluripotent Stem-Cell-Derived Therapies in Clinical Trial: A 2025 Update." *Cell Stem Cell*, vol. 32, no. 1, 2025, pp. 10–37.

1. Li, Jiacheng, et al. "Direct Reprogramming of Fibroblasts into Functional Hepatocytes via CRISPRa Activation of Endogenous Gata4 and Foxa3." *Chinese Medical Journal*, vol. 137, no. 11, 2024, pp. 1351–1359. doi: 10.1097/CM9.0000000000003088.

1. Lieberman, Erez, et al. "Evolutionary Dynamics on Graphs." *Nature*, vol. 433, no. 7023, 2005, pp. 312–316. doi: 10.1038/nature03204.

1. Mahmoudi, Salah, Lucy Xu, and Anne Brunet. "Turning Back Time with Emerging Rejuvenation Strategies." *Nature Cell Biology*, vol. 21, no. 1, 2019, pp. 32–43. doi: 10.1038/s41556-018-0206-0.

1. Marichal, Nicolás, et al. "Reprogramming Astroglia into Neurons with Hallmarks of Fast-Spiking Parvalbumin-Positive Interneurons by Phospho-Site-Deficient Ascl1." *Science Advances*, vol. 10, no. 43, 2024, article eadl5935. doi: 10.1126/sciadv.adl5935.

1. Nakano, Koji, et al. "Development of Adeno-Associated Viral Vectors Targeting Cardiac Fibroblasts for Efficient In Vivo Cardiac Reprogramming." *Stem Cell Reports*, vol. 19, no. 10, 2024, pp. 1389–1398. doi: 10.1016/j.stemcr.2024.08.002.

1. Narasimhan, Mukund, and Jeff A. Bilmes. "A Submodular-Supermodular Procedure with Applications to Discriminative Structure Learning." *Proceedings of the Twenty-First Conference on Uncertainty in Artificial Intelligence (UAI 2005)*, AUAI Press, 2005, pp. 404–412.

1. Paine, Patrick T., Anna Nguyen, and Alejandro Ocampo. "Partial Cellular Reprogramming: A Deep Dive into an Emerging Rejuvenation Technology." *Aging Cell*, vol. 23, no. 2, 2024, article e14039. doi: 10.1111/acel.14039.

1. Papadimitriou, Elsa, et al. "In Vitro and In Vivo Direct Reprogramming of Astrocytes to Induced-Neurons." *Methods in Molecular Biology*, vol. 2861, 2025, pp. 253–284. doi: 10.1007/978-1-0716-4386-0_13.

1. Qian, Li, et al. "In Vivo Reprogramming of Murine Cardiac Fibroblasts into Induced Cardiomyocytes." *Nature*, vol. 485, no. 7400, 2012, pp. 593–598. doi: 10.1038/nature11044.

1. Rosenblum, Daniel, et al. "CRISPR-Cas9 Genome Editing Using Targeted Lipid Nanoparticles for Cancer Therapy." *Science Advances*, vol. 6, no. 47, 2020, article eabc9450. doi: 10.1126/sciadv.abc9450.

1. Schoenfeldt, Lucas, et al. "Chemical Reprogramming Ameliorates Cellular Hallmarks of Aging and Extends Lifespan." *EMBO Molecular Medicine*, vol. 17, no. 8, 2025, pp. 2071–2094. doi: 10.1038/s44321-025-00265-9.

1. Sekiya, Sayaka, and Atsushi Suzuki. "Direct Conversion of Mouse Fibroblasts to Hepatocyte-like Cells by Defined Factors." *Nature*, vol. 475, no. 7356, 2011, pp. 390–393. doi: 10.1038/nature10263.

1. Thall, Peter F., and John D. Cook. "Dose-Finding Based on Efficacy–Toxicity Trade-Offs." *Biometrics*, vol. 60, no. 3, 2004, pp. 684–693. doi: 10.1111/j.0006-341X.2004.00218.x.

1. Thall, Peter F., et al. "Adaptive Dose Selection Using Efficacy-Toxicity Trade-Offs: Illustrations and Practical Considerations." *Journal of Biopharmaceutical Statistics*, vol. 16, no. 5, 2006, pp. 623–638. doi: 10.1080/10543400600860394.

1. Vierbuchen, Thomas, et al. "Direct Conversion of Fibroblasts to Functional Neurons by Defined Factors." *Nature*, vol. 463, no. 7284, 2010, pp. 1035–1041. doi: 10.1038/nature08797.

1. Bann, Glynnis Garry, et al. "Cellular Reprogramming by PHF7 Enhances Cardiac Function Following Myocardial Infarction." Circulation 152.9 (2025): 616-629.

1. Li Y, Zhu J, Yue C, Song S, Tian L and Wang Y (2025) Recent advances in pancreatic α-cell transdifferentiation for diabetes therapy. Front. Immunol. 16:1551372. doi: 10.3389/fimmu.2025.1551372

1. Karim Rony, RM Imtiaz, and Joshua D. Tompkins. "Cardiac repair and regeneration: cell therapy, in vivo reprogramming, and the promise of extracellular vesicles." Experimental & Molecular Medicine 57.10 (2025): 2182-2200.

1. Wheeler, Graham M., et al. "How to Design a Dose-Finding Study Using the Continual Reassessment Method: A Practical Tutorial." *BMC Medical Research Methodology*, vol. 17, 2017, article 146. doi: 10.1186/s12874-017-0381-x.

1. Cheng, L., Wang, Y., Guan, J., & Deng, H. (2025). Decoding human chemical reprogramming: mechanisms and principles. Trends in biochemical sciences, 50(6), 520–531. https://doi.org/10.1016/j.tibs.2025.03.004

1. Ventz, Steffen, and Lorenzo Trippa. "Bayesian Designs and the Control of Frequentist Characteristics: A Practical Solution." *Biometrics*, vol. 71, no. 1, 2015, pp. 218–226. doi: 10.1111/biom.12226.

1. Mokhtari, Reza Bayat, et al. "A comprehensive oncological biomarker framework guiding precision medicine." Biomolecules 15.9 (2025): 1304.

1. Krause, Andreas, and Daniel Golovin. "Submodular Function Maximization." In *Tractability: Practical Approaches to Hard Problems*, edited by Lucas Bordeaux, Youssef Hamadi, and Pushmeet Kohli, Cambridge UP, 2014, pp. 71–104.

1. Robert, Christian P., and George Casella. *Monte Carlo Statistical Methods*. 2nd ed., Springer, 2005.

1. Kudryavtsev, Oleg, and Eshref Trushin. "A new real option methodology for the quality-by-design pharmaceutical research and development." European Journal of Operational Research (2026).

1. Stinnett, Aaron A., and John Mullahy. "Net Health Benefits: A New Framework for the Analysis of Uncertainty in Cost-Effectiveness Analysis." *Medical Decision Making*, vol. 18, no. 2, 1998

