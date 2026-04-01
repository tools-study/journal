# Tissue Engineering Review

## Abstract

The central challenge of regenerative medicine has historically been framed as a supply problem — engineering sufficient quantities of the right cells and delivering them to damaged tissues. Yet decades of cell transplantation research have exposed a more fundamental barrier: transplanted cells overwhelmingly fail to engraft, with fewer than 5% of injected cardiomyocytes surviving beyond 48 hours and more than half of transplanted islets losing function within five years. This review argues that the field is undergoing a paradigm shift from transplanting exogenous cells toward activating the body's endogenous repair systems in situ. We survey four converging pillars of this transformation. First, in situ direct reprogramming — the conversion of resident somatic cells (fibroblasts, astrocytes) into functional target cell types using transcription factors, CRISPRa, or small molecules delivered directly to injured tissue — has advanced from proof-of-concept to pre-investigational new drug (IND) programs, with AAV-mediated cardiac reprogramming achieving sustained functional improvement in chronic heart failure models. Second, immune-instructive biomaterials have revealed that the immune response to implanted materials is not merely a barrier to overcome but a programmable therapeutic lever; the landmark discovery that senescent T cells drive an IL-17/type 3 immune response that actively blocks biomaterial-mediated regeneration in aged animals fundamentally reframes why tissue engineering fails in elderly patients. Third, cell-free regenerative therapeutics — including mRNA-encoded growth factors injected directly into the myocardium and lipid nanoparticle-mediated in vivo generation of chimeric antigen receptor (CAR) T cells — eliminate the manufacturing bottleneck of ex vivo cell therapy entirely. Fourth, xenotransplantation of gene-edited porcine organs has achieved 271-day kidney survival in human recipients and received FDA approval for multi-center clinical trials, providing an immediate solution for end-stage organ failure while endogenous repair strategies mature. Novel mathematical frameworks formalize the quantitative principles governing reprogramming efficiency landscapes, competing cell fate dynamics, immune-material crosstalk, scaffold infiltration kinetics, cell-free therapeutic pharmacokinetics, and xenograft survival. Together, these four pillars define a new therapeutic paradigm.

---

## 1. The In Vivo Repair Paradigm

### 1.1 The Transplantation Bottleneck

For three decades, the dominant strategy in regenerative medicine has been to generate therapeutic cells ex vivo and transplant them into patients. This approach achieved its foundational validation with hematopoietic stem cell transplantation and received transformative impetus from Takahashi and Yamanaka's discovery that somatic cells could be reprogrammed to pluripotency by four defined transcription factors (Takahashi & Yamanaka, 2006). The subsequent development of directed differentiation protocols enabled the production of virtually any human cell type from induced pluripotent stem cells (iPSCs), and clinical trials of iPSC-derived cardiomyocytes, dopaminergic neurons, retinal pigment epithelial cells, and pancreatic beta cells are now underway worldwide (Blau & Daley, 2019).

Yet the clinical results of cell transplantation have been sobering. Across organ systems, the fundamental problem is not cell quality but engraftment failure: transplanted cells are delivered into hostile microenvironments devoid of the matrix, vascular, and immune signals that sustain cell function in native tissue. This engraftment gap has motivated the parallel development of niche engineering approaches — synthetic hydrogels, decellularized extracellular matrix scaffolds, and three-dimensional bioprinting — that aim to recreate the microenvironment at the transplant site. While these strategies have achieved notable advances, they do not address two deeper limitations of the transplantation paradigm: the manufacturing complexity of producing patient-specific cells at clinical scale, and the immunological challenges of allogeneic or xenogeneic cell delivery.

### 1.2 The Shift to Endogenous Repair

An alternative paradigm has emerged: rather than replacing damaged cells with transplanted substitutes, activate the body's own repair systems to regenerate tissue in situ. This approach is grounded in the observation that mammalian regenerative capacity, while limited in adults, is not absent: neonatal mice can fully regenerate resected myocardium within 21 days, demonstrating that the genetic programs for cardiac regeneration exist but are developmentally silenced (Porrello et al., 2011). This approach exploits two biological insights. First, mammalian tissues harbor resident cell populations — fibroblasts, astrocytes, stellate cells — that can be directly converted into functional target cells through the forced expression of lineage-specific transcription factors, bypassing the pluripotent state entirely (Ieda et al., 2010). Second, the immune system plays an instructive role in tissue repair that can be harnessed through rationally designed biomaterials: the same scaffold that merely provokes inflammation in one immune context can drive functional regeneration in another (Sadtler et al., 2016).

The in vivo repair paradigm offers three fundamental advantages over cell transplantation. First, it eliminates the manufacturing bottleneck — the patient's own cells serve as the starting material, and reprogramming or immune modulation is achieved by delivering genetic or molecular instructions rather than cells. Second, it avoids the engraftment problem — cells that are reprogrammed in situ are already integrated into the tissue architecture, with established matrix contacts, vascular connections, and paracrine signaling. Third, it enables therapeutic approaches at scales that cell transplantation cannot reach: in vivo generation of CAR T cells via lipid nanoparticle delivery of mRNA eliminates the need for leukapheresis, ex vivo activation, and reinfusion, potentially reducing the cost of CAR T therapy from >$400,000 to a fraction of that price (Rurik et al., 2022).

This review surveys four converging pillars of the in vivo repair paradigm — direct reprogramming, immune-instructive biomaterials, cell-free therapeutics, and xenotransplantation — and argues that their convergence will define the next decade of regenerative medicine.

---

## 2. In Situ Direct Reprogramming

### 2.1 Cardiac Direct Reprogramming: From GMT to CRISPRa

The possibility of directly converting one somatic cell type into another without transiting through a pluripotent intermediate was established by Ieda, Srivastava, and colleagues in 2010, who demonstrated that forced expression of three cardiac transcription factors — Gata4, Mef2c, and Tbx5 (GMT) — could convert mouse cardiac fibroblasts into induced cardiomyocyte-like cells (iCMs) in vitro (Ieda et al., 2010). Two years later, the same group achieved in vivo cardiac reprogramming by delivering GMT via retroviral vectors directly into the infarcted mouse heart, demonstrating that resident cardiac fibroblasts could be converted into functional cardiomyocytes in situ, with measurable improvement in cardiac function (Qian et al., 2012). This landmark result established the principle that tissue repair could be achieved by reprogramming resident cells rather than transplanting exogenous ones.

The intervening decade has been devoted to improving reprogramming efficiency — which in initial studies was approximately 1–10% as measured by cardiac gene activation — through three complementary strategies: optimizing transcription factor stoichiometry, adding supplementary factors, and engineering delivery vectors.

**CRISPRa-mediated endogenous gene activation.** A transformative advance in 2024 demonstrated that CRISPR activation (CRISPRa) could replace exogenous transcription factor overexpression for cardiac reprogramming. Huang, Qian, and colleagues showed that dCas9-VPR-mediated activation of endogenous Gata4 — targeting both the promoter and a newly identified distal enhancer — combined with lentiviral expression of exogenous Mef2c and Tbx5, achieved cardiac reprogramming of mouse fibroblasts with efficiency comparable to conventional GMT overexpression (Huang et al., 2024). The CRISPRa approach offers a critical advantage: endogenous gene activation produces physiological expression levels and proper splicing, avoiding the supraphysiological and potentially toxic expression levels associated with strong viral promoters. Furthermore, the CRISPRa system can be targeted to multiple genomic loci simultaneously, enabling combinatorial activation of cardiac gene regulatory networks that may more faithfully recapitulate normal cardiogenesis (Huang et al., 2024).

**Fibroblast-targeted AAV delivery.** A parallel advance addressed the delivery challenge: how to specifically target cardiac fibroblasts in vivo while avoiding transduction of cardiomyocytes and other cell types. Nakano, Ieda, and colleagues developed AAV-DJ vectors driven by the periostin (Postn) promoter, which is selectively active in cardiac fibroblasts but not in cardiomyocytes (Nakano et al., 2024). Using lineage tracing to rigorously confirm fibroblast-to-cardiomyocyte conversion, they demonstrated that AAV-DJ-Postn delivery of an optimized GMT plus Hand2 (GHMT) cocktail with an enhanced M-TAD activation domain achieved a two-fold increase in reprogramming efficiency compared to standard GHMT, with converted cells expressing mature cardiomyocyte markers and integrating into the host myocardium (Nakano et al., 2024). This fibroblast-specific targeting is essential for clinical translation, as untargeted reprogramming factor delivery could cause deleterious effects in non-target cell types.

**Small molecule cardiac reprogramming.** The ultimate goal for clinical translation is to replace transcription factors with small molecules that can be delivered pharmacologically. Chen and colleagues demonstrated in 2024 that a seven-compound chemical cocktail (CRFVPTM: CHIR99021, RepSox, Forskolin, Valproic acid, Parnate, TTNPB, and Myocyte-specific enhancer factor 2C) could reprogram cardiac fibroblasts into cardiomyocyte-like cells in the mouse heart in vivo, as confirmed by three-dimensional whole-heart imaging using the CUBIC tissue-clearing protocol (Chen et al., 2024). Chemical reprogramming eliminates the need for viral vectors entirely, representing the most translatable approach — though current efficiencies remain lower than genetic methods and the pharmacokinetics of maintaining sustained multi-drug exposure in the myocardium present significant challenges.

**Clinical pipeline.** The most advanced cardiac reprogramming program is Tenaya Therapeutics' single-AAV vector encoding an optimized reprogramming cocktail, which achieved dose-dependent cardiac function improvement sustained to 29 weeks in a chronic rat myocardial infarction model — the longest sustained benefit reported for any cardiac reprogramming approach. This program is the closest to an investigational new drug (IND) application among all in vivo cardiac reprogramming efforts (Ding, 2025).

### 2.2 Neural Direct Reprogramming: Astrocyte-to-Neuron Conversion

The brain presents a unique opportunity for in situ reprogramming because neurodegenerative diseases and stroke create regions where neurons have died but reactive astrocytes — which share a common developmental origin with neurons — proliferate in the damaged area. Converting these reactive astrocytes into functional neurons in situ would simultaneously remove the inhibitory glial scar and replace lost neurons, addressing two pathological features with a single intervention.

**ASCL1-SA6: Engineering inhibitory neurons in vivo.** A breakthrough in 2024 demonstrated that a phosphorylation-deficient mutant of the proneural transcription factor ASCL1 — termed ASCL1-SA6, in which six serine phosphorylation sites are mutated to alanine — could reprogram astroglia into parvalbumin-positive (PV+) fast-spiking interneurons in vivo (Marichal et al., 2024). This is significant for three reasons. First, PV+ interneurons are the principal inhibitory neurons of the cerebral cortex, and their loss or dysfunction underlies epilepsy, schizophrenia, and autism spectrum disorders. Second, wild-type ASCL1 primarily generates excitatory-like neurons when used for reprogramming; the SA6 mutation — which prevents CDK-mediated phosphorylation that normally attenuates ASCL1 activity during the cell cycle — dramatically shifts the conversion toward the inhibitory interneuron fate (Marichal et al., 2024). Third, the reprogrammed neurons exhibited electrophysiological properties characteristic of mature PV+ interneurons, including fast-spiking firing patterns, confirming functional maturation in the in vivo environment (Marichal et al., 2024).

**Mechanistic foundations: Ngn2 and the Yy1 epigenome remodeling requirement.** The mechanistic basis of neural reprogramming was substantially clarified in 2024 by Pereira, Gotz, and colleagues, who performed the first comprehensive multiscale epigenome analysis of astrocyte-to-neuron conversion (Pereira et al., 2024). Using Ngn2 as the reprogramming factor, they demonstrated that successful neural conversion requires the transcription factor Yy1 to orchestrate epigenome remodeling across multiple scales — from local chromatin accessibility changes at individual enhancers to large-scale three-dimensional genome reorganization. Depletion of Yy1 abolished reprogramming, establishing it as an essential cofactor. Critically, the study revealed that the epigenetic barriers to astrocyte-to-neuron conversion are not merely the absence of neuronal programs but the active maintenance of astrocytic identity through heterochromatin, suggesting that successful reprogramming requires both activating neuronal genes and dismantling astrocytic chromatin architecture (Pereira et al., 2024).

**NeuroD1: Brain-wide gene therapy for neurodegeneration.** The transcription factor NeuroD1 has emerged as a particularly promising candidate for clinical neural reprogramming, driven by the work of Gong Chen's laboratory. Wu, Chen, and colleagues demonstrated in 2025 that brain-wide delivery of NeuroD1 via AAV improved cognition in a mouse model of Alzheimer's disease, converting reactive astrocytes into functional neurons across multiple brain regions (Wu et al., 2025). Complementing this therapeutic demonstration, Li, Chen, and colleagues identified the core regulatory program driving NeuroD1-induced neuronal reprogramming, revealing that NeuroD1 activates a cascade of downstream transcription factors that progressively silence astrocytic genes while activating neuronal identity programs (Li et al., 2025). This mechanistic dissection is critical for optimizing reprogramming efficiency and predicting which brain regions and disease contexts will be most amenable to NeuroD1-based therapy.

### 2.3 Emerging Frontiers in Direct Reprogramming

**Hepatic reprogramming.** The liver presents an attractive target for in situ reprogramming because liver fibrosis — the accumulation of scar-forming myofibroblasts — is a leading cause of liver failure and death worldwide, and converting these fibrogenic cells into functional hepatocytes would simultaneously resolve fibrosis and restore hepatic function. Li and colleagues demonstrated in 2024 that CRISPRa-mediated activation of endogenous Gata4 and Foxa3 in hepatic stellate cells (the principal fibrogenic cell in the liver) could reprogram them into functional hepatocyte-like cells that expressed albumin, metabolized drugs, and reduced liver fibrosis in a mouse model of chronic liver injury (Li et al., 2024). This result extends the CRISPRa reprogramming paradigm from cardiac to hepatic applications and suggests a general strategy for treating organ fibrosis through in situ cell identity conversion.

**Pancreatic alpha-to-beta cell conversion.** The loss of insulin-producing beta cells is the defining feature of type 1 diabetes, and alpha cells — which produce glucagon and are relatively spared in autoimmune diabetes — represent a potential endogenous source for beta cell regeneration. Small molecule and genetic approaches to promote alpha-to-beta cell conversion in vivo are under active investigation, with several groups demonstrating that modulation of the ARX/PAX4 transcriptional axis or epigenetic manipulation can shift alpha cell identity toward a beta-like phenotype (Zhang et al., 2024). Clinical translation remains challenging due to the need for alpha cell-specific targeting and the risk of autoimmune destruction of newly converted beta cells, but the approach avoids the immunological complications of allogeneic islet transplantation.

**Field-wide perspective.** Multiple comprehensive reviews published in 2024–2025 have assessed the clinical trajectory of in vivo direct reprogramming (Keshri et al., 2024; Nakatsukasa et al., 2025; Lin et al., 2025; Ding, 2025). The consensus emerging from these assessments is that cardiac reprogramming is closest to clinical translation (3–5 years to first-in-human trials), neural reprogramming faces greater safety hurdles but has enormous therapeutic potential, and hepatic and pancreatic reprogramming are at earlier stages but advancing rapidly. Across all organ systems, the critical challenges are achieving sufficient reprogramming efficiency for therapeutic benefit, ensuring long-term safety of converted cells, and developing delivery systems that provide organ-specific targeting.

### 2.4 Framework F298: Epigenetic Barrier Landscape for In Situ Reprogramming

The efficiency of direct reprogramming can be understood through the lens of Kramers escape theory, which describes the rate at which a particle (here, the cellular epigenetic state) escapes from a potential well (the stable cell identity) over an energy barrier (the epigenetic barriers separating cell identities).

Consider a cell in identity state $A$ (e.g., fibroblast) that must cross an epigenetic barrier of height $\Delta U$ to reach identity state $B$ (e.g., cardiomyocyte). The reprogramming rate $k_{\text{rep}}$ is:

```math
k_{\text{rep}} = \nu_0 \cdot \exp\left(-\frac{\Delta U_{\text{epi}}}{D_{\text{stoch}}}\right)
```

where $\nu_0$ is the attempt frequency (related to the rate of chromatin remodeling events, approximately one cell cycle duration $\tau_{\text{cc}} \approx 24$ h, giving $\nu_0 \approx 1/\tau_{\text{cc}}$), $\Delta U_{\text{epi}}$ is the effective epigenetic barrier height, and $D_{\text{stoch}}$ is the stochastic noise intensity (driven by transcriptional bursting and stochastic chromatin remodeling).

The barrier height depends on transcription factor (TF) concentration and chromatin accessibility:

```math
\Delta U_{\text{epi}}([\text{TF}], \alpha) = \Delta U_0 \cdot \left(1 - \frac{[\text{TF}]^{n_H}}{K_{\text{TF}}^{n_H} + [\text{TF}]^{n_H}}\right) \cdot \left(1 - \alpha\right)
```

where $\Delta U_0$ is the baseline barrier height in the absence of reprogramming factors, $[\text{TF}]$ is the effective transcription factor concentration, $K_{\text{TF}}$ is the half-maximal TF concentration for barrier reduction, $n_H$ is a Hill coefficient reflecting cooperative TF binding, and $\alpha \in [0,1]$ is the local chromatin accessibility (measurable by ATAC-seq signal at target loci, normalized to fully open chromatin).

For cardiac reprogramming with GMT: $\Delta U_0 / D_{\text{stoch}} \approx 8$–$10$ (consistent with ~1–10% conversion over 2 weeks), yielding $k_{\text{rep}} \approx 10^{-4}$–$10^{-3}$ per cell per day. CRISPRa enhancement of endogenous factor levels effectively increases $[\text{TF}]$ while simultaneously increasing $\alpha$ at target loci (because CRISPRa-recruited transcriptional activators remodel local chromatin), providing a dual reduction of the barrier height that explains the comparable efficiency achieved by Huang et al. (2024) despite replacing one exogenous factor with endogenous activation.

The framework predicts that the most efficient reprogramming strategies will combine high TF concentration (viral overexpression or CRISPRa) with chromatin pre-opening (epigenetic modifiers such as valproic acid or p300/CBP inhibitors) — a prediction consistent with the empirical finding that adding small molecule chromatin modulators to TF cocktails substantially improves reprogramming efficiency across organ systems.

### 2.5 Framework F299: Competing Fates in the Target Cell Population

In the in vivo setting, cells exposed to reprogramming factors do not simply convert or remain unchanged — they face a competition among multiple fates. We model the target cell population as a system of coupled ordinary differential equations describing three competing fates: reprogramming, proliferation (remaining as the original cell type), and apoptosis.

Let $N_F(t)$ be the number of fibroblasts (or astrocytes), $N_C(t)$ the number of successfully converted cells, and $N_D(t)$ the cumulative number of dead cells:

```math
\frac{dN_F}{dt} = \left(r_{\text{prolif}} - k_{\text{rep}} - k_{\text{apop}}\right) N_F
```

```math
\frac{dN_C}{dt} = k_{\text{rep}} \cdot N_F - \delta_C \cdot N_C
```

```math
\frac{dN_D}{dt} = k_{\text{apop}} \cdot N_F + \delta_C \cdot N_C
```

where $r_{\text{prolif}}$ is the fibroblast proliferation rate, $k_{\text{rep}}$ is the reprogramming rate (from F298), $k_{\text{apop}}$ is the apoptosis rate induced by reprogramming factor expression (a significant concern with viral overexpression), and $\delta_C$ is the death rate of converted cells (which may be elevated during the maturation period before full integration into the tissue).

The therapeutic conversion efficiency at time $t$ is:

```math
\eta(t) = \frac{N_C(t)}{N_C(t) + N_F(t) + N_D(t)}
```

At steady state (long time limit), the conversion efficiency approaches:

```math
\eta_{\infty} = \frac{k_{\text{rep}}}{k_{\text{rep}} + k_{\text{apop}}} \cdot \frac{1}{1 + \delta_C / r_{\text{net}}}
```

where $r_{\text{net}} = r_{\text{prolif}} - k_{\text{rep}} - k_{\text{apop}}$ is the net fibroblast growth rate. This reveals two critical design principles: first, minimizing apoptosis ($k_{\text{apop}} \to 0$) is as important as maximizing reprogramming rate — CRISPRa and small molecule approaches that achieve physiological expression levels may outperform high-expression viral systems by reducing toxicity-driven cell death. Second, the long-term fate of converted cells ($\delta_C$) is a critical determinant of therapeutic outcome — converted cardiomyocytes that fail to establish proper electrical coupling and mechanical integration will die, reducing the net therapeutic benefit regardless of initial conversion efficiency.

For cardiac reprogramming, representative parameter values — $r_{\text{prolif}} \approx 0.02$ d$^{-1}$, $k_{\text{rep}} \approx 5 \times 10^{-3}$ d$^{-1}$, $k_{\text{apop}} \approx 0.01$ d$^{-1}$, $\delta_C \approx 0.005$ d$^{-1}$ — yield $\eta_{\infty} \approx 0.25$, suggesting that approximately one-quarter of fibroblasts in the transduced region can be durably converted, consistent with the functional improvements reported in preclinical studies.

---

## 3. Immune-Instructive Biomaterials

### 3.1 The Senescent T Cell / IL-17 Barrier: A Paradigm Shift

The immune response to implanted biomaterials was long viewed as a nuisance — a foreign body reaction to be minimized through material chemistry and surface modification. This view was overturned in 2016 when Sadtler, Elisseeff, and colleagues demonstrated that the adaptive immune system actively directs the outcome of biomaterial implantation: scaffolds derived from extracellular matrix (ECM) promoted functional muscle regeneration specifically through the recruitment of T helper 2 (Th2) cells, and depletion of Th2 responses converted the regenerative outcome to fibrosis (Sadtler et al., 2016). This result established that the immune response to biomaterials is not merely permissive or obstructive but instructive — the type of immune response determines whether the tissue regenerates or scars.

A paradigm-shifting discovery in 2024 extended this principle to explain one of the most persistent clinical puzzles in tissue engineering: why biomaterial-based regenerative therapies that work robustly in young animals consistently fail in aged patients. Han, Elisseeff, and colleagues demonstrated that aged animals harbor expanded populations of senescent T cells that produce interleukin-17 (IL-17) and drive a type 3 immune response — characterized by neutrophil recruitment, IL-17 signaling, and sustained inflammation — that actively blocks the pro-regenerative type 2 immune response required for biomaterial-mediated tissue repair (Han et al., 2024a). Critically, neutralization of IL-17 in aged animals restored the regenerative response to levels comparable to young animals (Han et al., 2024a). This result has three profound implications. First, it provides the first mechanistic explanation for the age-dependent decline in biomaterial efficacy that has confounded clinical translation for decades. Second, it identifies a specific, druggable target (IL-17) for restoring regenerative capacity in elderly patients. Third, it reframes the challenge of tissue engineering in aging from a materials problem to an immunological problem — the scaffold may be perfectly designed, but if the recipient's immune system is programmed to reject regeneration, the material will fail regardless.

The broader context of immunoengineering across the lifespan was systematically reviewed by Han, Rindone, and Elisseeff, who catalogued the age-dependent changes in immune composition and function that alter biomaterial responses from the neonatal period through senescence (Han et al., 2024b). Their analysis reveals that the immune system's response to biomaterials is not a fixed property but a dynamic variable that changes dramatically with age, disease state, and prior immune experience — requiring that biomaterial design be tailored not only to the target tissue but to the immunological age of the recipient.

### 3.2 ECM-Based Immunomodulation: From Regeneration to Cancer Immunotherapy

The discovery that ECM scaffolds can program immune responses has opened therapeutic applications far beyond tissue repair.

**ECM tumor vaccines.** Pal, Wolf, and colleagues demonstrated in 2024 that ECM scaffolds loaded with tumor antigens function as potent in situ cancer vaccines, achieving complete tumor regression in 50–75% of treated animals and inducing long-term immune memory lasting more than 10 months (Pal et al., 2024). The ECM scaffold serves as both an adjuvant — providing danger signals and creating a pro-inflammatory microenvironment that activates dendritic cells — and a sustained-release depot that presents tumor antigens over an extended period. This dual function is difficult to replicate with synthetic materials, as the complex composition of native ECM includes hundreds of matrisome proteins, glycosaminoglycans, and sequestered growth factors that collectively program the immune response (Pal et al., 2024).

**The microbiome-biomaterial axis.** A surprising connection between gut microbiota and biomaterial response was revealed by Rutkowski, Elisseeff, and colleagues in 2025. Antibiotic-induced depletion of the gut microbiome impaired the pro-regenerative immune response to ECM scaffolds, reducing type 2 immune activation and functional tissue repair (Rutkowski et al., 2025). This finding establishes a gut-tissue immune axis in which commensal microorganisms prime the systemic immune response toward regeneration-permissive states. The clinical implication is significant: patients receiving broad-spectrum antibiotics perioperatively — a near-universal practice in surgery — may inadvertently compromise the regenerative response to implanted biomaterials (Rutkowski et al., 2025).

**Tolerogenic dendritic cell recruitment.** Lokwani, Sadtler, and colleagues at the National Institutes of Health demonstrated in 2024 that pro-regenerative ECM biomaterials specifically recruit immunoregulatory dendritic cells (DCs) to the implant site after traumatic muscle injury (Lokwani et al., 2024). These tolerogenic DCs suppress inflammatory T cell responses and promote tissue-resident regulatory T cell expansion, creating a local immunosuppressive niche that permits regeneration. Importantly, the study demonstrated that this DC recruitment is biomaterial-dependent — pro-inflammatory materials recruited conventional inflammatory DCs, while pro-regenerative ECM scaffolds recruited the tolerogenic subset — establishing that immune cell recruitment is programmable through material composition (Lokwani et al., 2024). Complementing this finding, DeStefano, Sadtler, and colleagues systematically mapped the conserved and tissue-specific features of immune responses to biologic scaffolds across multiple anatomical sites, revealing that while some immune signatures (e.g., initial neutrophil infiltration) are universal, the subsequent adaptive immune response is tissue-specific and dictates whether the outcome is regeneration or fibrosis (DeStefano et al., 2024).

**The SASP connection.** The molecular link between aging, senescence, and altered biomaterial responses was further elucidated by Wang, Elisseeff, and Demaria, who comprehensively reviewed the senescence-associated secretory phenotype (SASP) — the complex cocktail of cytokines, chemokines, matrix metalloproteinases, and growth factors secreted by senescent cells (Wang et al., 2024). The SASP creates a chronic inflammatory microenvironment that, in the context of biomaterial implantation, favors fibrosis over regeneration. This understanding suggests that senolytics — drugs that selectively eliminate senescent cells — may serve as adjunct therapies to restore biomaterial-mediated regeneration in aged patients.

### 3.3 Microporous Annealed Particle (MAP) Scaffolds

The physical architecture of biomaterial scaffolds profoundly influences the immune and regenerative response. A key parameter is porosity: cells can only infiltrate scaffolds with pores larger than their diameter (~10–20 micrometers for most mammalian cells), and the void fraction determines the available volume for cell migration, vascularization, and tissue formation. Garg and colleagues established in 2013 that scaffold fiber diameter and pore size directly control macrophage polarization: scaffolds with larger pores promoted anti-inflammatory M2 macrophage phenotypes associated with constructive remodeling, while smaller pores promoted pro-inflammatory M1 phenotypes and foreign body giant cell formation (Garg et al., 2013). This structure-function relationship has been exploited by several groups to design scaffolds that actively program the immune response through physical architecture alone.

The microporous annealed particle (MAP) hydrogel platform, developed by Segura and colleagues, represents a particularly innovative approach to scaffold porosity. MAP hydrogels consist of microgel particles (typically 50–200 micrometers in diameter) that are annealed together at their contact points, creating a scaffold with interconnected micropores in the interstitial spaces between particles (Segura, 2024). This granular architecture provides immediate porosity upon injection — unlike bulk hydrogels that must degrade before cells can infiltrate — enabling rapid cell invasion, vascularization, and tissue integration. The platform has been applied to stroke brain repair, where MAP hydrogels delivering clustered VEGF nanoparticles promoted angiogenesis and neural progenitor cell migration into the stroke cavity, demonstrating that injectable, pore-forming scaffolds can drive regeneration in the most challenging tissue engineering context: the central nervous system (Segura, 2024).

### 3.4 Framework F300: Macrophage Polarization Dynamics with IL-17 Inhibition

The interplay between macrophage polarization, biomaterial signals, and senescent T cell-derived IL-17 can be formalized as a system of coupled ordinary differential equations.

Let $M_1(t)$ and $M_2(t)$ represent the populations of pro-inflammatory (M1) and pro-regenerative (M2) macrophages at the biomaterial implant site, and $I_{17}(t)$ the local IL-17 concentration:

```math
\frac{dM_1}{dt} = \alpha_{M1} \cdot \left(S_{\text{damage}} + \kappa \cdot I_{17}\right) \cdot \left(1 - \frac{M_1 + M_2}{M_{\max}}\right) - \beta_{12} \cdot \frac{B^{n_B}}{K_B^{n_B} + B^{n_B}} \cdot M_1 - \delta_{M1} \cdot M_1
```

```math
\frac{dM_2}{dt} = \beta_{12} \cdot \frac{B^{n_B}}{K_B^{n_B} + B^{n_B}} \cdot M_1 + \alpha_{M2} \cdot C_{\text{ECM}} - \gamma_{21} \cdot I_{17} \cdot M_2 - \delta_{M2} \cdot M_2
```

```math
\frac{dI_{17}}{dt} = k_{\text{senT}} \cdot N_{\text{senT}} - \mu_{17} \cdot I_{17}
```

where $S_{\text{damage}}$ is the tissue damage signal (DAMPs), $\kappa$ is the IL-17-mediated M1 recruitment coefficient, $B$ is the biomaterial-derived signal strength (dependent on material composition), $n_B$ and $K_B$ parameterize the Hill-type M1-to-M2 conversion response to biomaterial signals, $\beta_{12}$ is the maximum M1-to-M2 conversion rate, $C_{\text{ECM}}$ is the ECM scaffold concentration (which directly recruits M2 macrophages), $\gamma_{21}$ is the IL-17-mediated M2-to-M1 reversion rate, $N_{\text{senT}}$ is the number of senescent T cells (which increases with age), and $k_{\text{senT}}$ is their IL-17 secretion rate.

The steady-state ratio $M_2^*/M_1^*$ — the **Regeneration Index** — determines the tissue outcome:

```math
\text{RI} = \frac{M_2^*}{M_1^*} = \frac{\beta_{12} \cdot B^{n_B}/(K_B^{n_B} + B^{n_B}) + \alpha_{M2} \cdot C_{\text{ECM}} / M_1^*}{\gamma_{21} \cdot k_{\text{senT}} \cdot N_{\text{senT}} / \mu_{17} + \delta_{M2}}
```

When RI > 1, the tissue environment favors regeneration; when RI < 1, fibrosis dominates. The model predicts three therapeutic interventions consistent with experimental data: (1) increasing biomaterial signal $B$ through ECM-derived scaffolds that drive M1→M2 conversion, (2) neutralizing IL-17 ($\mu_{17} \to \infty$) to remove the M2 suppression signal, and (3) reducing senescent T cell burden ($N_{\text{senT}} \to 0$) through senolytic therapy. The model explains why identical biomaterials produce different outcomes in young versus aged recipients: in young animals ($N_{\text{senT}}$ low), $I_{17} \approx 0$ and RI is dominated by the biomaterial term; in aged animals ($N_{\text{senT}}$ high), the IL-17 feedback suppresses M2 polarization regardless of scaffold quality.

### 3.5 Framework F301: MAP Scaffold Cell Infiltration Kinetics

The rate of cell infiltration into a porous scaffold determines the timeline for vascularization and functional tissue formation. We model cell migration into a MAP scaffold as a modified diffusion process with chemotactic guidance.

The cell density $c(x,t)$ at depth $x$ into the scaffold at time $t$ follows:

```math
\frac{\partial c}{\partial t} = D_{\text{eff}}(\phi) \cdot \frac{\partial^2 c}{\partial x^2} - \chi \cdot \frac{\partial}{\partial x}\left(c \cdot \frac{\partial G}{\partial x}\right)
```

where $D_{\text{eff}}(\phi)$ is the effective cell diffusion coefficient dependent on scaffold void fraction $\phi$, $\chi$ is the chemotactic sensitivity coefficient, and $G(x,t)$ is the growth factor concentration (e.g., VEGF released from the scaffold).

The effective diffusivity scales with void fraction through a percolation-theory correction:

```math
D_{\text{eff}}(\phi) = D_0 \cdot \left(\frac{\phi - \phi_c}{1 - \phi_c}\right)^{\mu} \quad \text{for } \phi > \phi_c
```

where $D_0 \approx 10^{-10}$ cm$^2$/s is the free cell diffusion coefficient, $\phi_c \approx 0.29$ is the percolation threshold for 3D random packing of spheres (below which the pore network is disconnected and no infiltration occurs), and $\mu \approx 2.0$ is the universal percolation exponent in three dimensions.

For MAP scaffolds with typical void fractions $\phi \approx 0.25$–$0.40$ (depending on microgel size and packing), the model predicts: (1) standard spherical microgels at random close packing ($\phi \approx 0.36$) provide $D_{\text{eff}} \approx 0.01 \cdot D_0$, yielding infiltration depths of ~500 micrometers over 7 days; (2) the critical importance of exceeding the percolation threshold $\phi_c$ — scaffolds with $\phi < 0.29$ have zero effective diffusivity and will not support cell infiltration regardless of other design parameters; (3) rod-shaped microgels that increase void fraction to $\phi \approx 0.40$–$0.50$ can increase $D_{\text{eff}}$ by 3–5 fold, consistent with recent experimental observations of enhanced cell invasion in anisotropic MAP scaffolds.

---

## 4. Cell-Free Regenerative Medicine

### 4.1 mRNA Therapeutics for Tissue Repair

The COVID-19 pandemic validated lipid nanoparticle (LNP)-encapsulated mRNA as a clinical-grade therapeutic platform, and the same technology is now being applied to regenerative medicine. The leading program is AZD8601, an LNP-formulated modified mRNA encoding vascular endothelial growth factor A (VEGF-A), developed by Moderna and AstraZeneca for cardiac regeneration.

In the Phase 2a EPICCURE trial, Anttila and colleagues performed the first direct intramyocardial injection of VEGF-A mRNA in human patients undergoing coronary artery bypass grafting (Anttila et al., 2023). The mRNA was injected in a 30-site epicardial pattern into the ischemic border zone during open-heart surgery. Safety was confirmed with no mRNA-related serious adverse events. At 6-month follow-up, all seven treated patients had N-terminal pro-B-type natriuretic peptide (NT-proBNP) levels below the heart failure diagnostic threshold, and exploratory efficacy signals included trends toward improved myocardial perfusion in the injected territory (Anttila et al., 2023). While the trial was not powered for efficacy, it established the safety and feasibility of direct mRNA injection into the human myocardium — a milestone for the entire field of mRNA-based tissue regeneration.

The VEGF mRNA approach has a fundamental advantage over recombinant VEGF protein delivery: mRNA produces VEGF locally from the patient's own cells for a controlled duration (approximately 24–72 hours of active translation), generating a physiological concentration gradient that promotes angiogenesis without the systemic toxicity (hypotension, edema) and rapid clearance that have plagued protein-based VEGF delivery strategies for decades.

### 4.2 In Vivo Generation of Therapeutic Cells

The most transformative application of LNP-mRNA technology to regenerative medicine is the in vivo generation of chimeric antigen receptor (CAR) T cells — eliminating the need for leukapheresis, ex vivo T cell culture, and reinfusion that make current CAR T therapy logistically complex and prohibitively expensive.

**The foundational demonstration.** Rurik, Epstein, and colleagues demonstrated in 2022 that CD5-targeted LNPs encapsulating CAR mRNA could transiently generate anti-fibroblast activation protein (FAP) CAR T cells in vivo, which then attacked and eliminated activated cardiac fibroblasts responsible for heart fibrosis (Rurik et al., 2022). A single intravenous injection reduced cardiac fibrosis and restored cardiac function in mice with established heart failure. This proof-of-concept demonstrated three principles: LNPs can target specific immune cell subsets in vivo (via surface ligand targeting), transient CAR expression from mRNA is sufficient for therapeutic effect (because the CAR T cells eliminate their targets and then the CAR expression naturally decays), and in vivo CAR T generation eliminates every step of the current ex vivo manufacturing process (Rurik et al., 2022).

**Clinical translation.** The in vivo CAR T platform has advanced rapidly toward the clinic. Hunter and colleagues published in Science in 2025 a comprehensive demonstration that LNP-mediated in vivo CAR T cell generation could treat both cancer and autoimmune disease in preclinical models, establishing the breadth of the platform (Hunter et al., 2025). In parallel, Capstan Therapeutics (acquired by AbbVie in June 2025) initiated the first Phase 1 clinical trial (CPTX2309) of in vivo generated anti-CD19 CAR T cells in healthy volunteers in Australia — the first time CAR T cells have been generated inside a human body (Hunter et al., 2025). The trial uses targeted LNPs delivered by standard intravenous infusion without lymphodepleting chemotherapy — a transformative simplification of the treatment protocol. Complementing the LNP-mRNA approach, Bimbo and colleagues demonstrated in 2025 that T cell-specific LNPs delivering DNA and a transposase could achieve stable CAR integration — rather than transient mRNA expression — generating permanent in vivo CAR T cells with sustained anti-tumor activity (Bimbo et al., 2025). This DNA-based approach may be necessary for applications requiring long-term CAR expression, such as cancer immunotherapy, while the transient mRNA approach may be preferred for fibrosis and autoimmunity where temporary immune cell activation is sufficient.

**Senolytic CAR T cells for aging.** Amor, Lowe, and colleagues demonstrated in 2024 that CAR T cells targeting urokinase plasminogen activator receptor (uPAR) — a surface marker of senescent cells — could selectively eliminate senescent cells in vivo, producing prophylactic and long-lasting improvements in metabolic function, exercise capacity, and healthspan in aged mice (Amor et al., 2024). A single dose of uPAR CAR T cells provided benefits lasting months, suggesting that senolytic CAR T therapy could serve as a one-time rejuvenation treatment. The convergence of in vivo CAR T generation (Section 4.2) with senolytic targeting (this section) raises the possibility of an injectable, off-the-shelf anti-aging therapy: LNP-delivered CAR mRNA targeting senescent cell surface markers, administered as a periodic intravenous infusion.

### 4.3 Exosome and Extracellular Vesicle Therapeutics

Extracellular vesicles (EVs) — including exosomes (30–150 nm) and microvesicles (100–1000 nm) — are natural intercellular communication vehicles that carry mRNA, microRNA, proteins, and lipids from donor to recipient cells. Mesenchymal stem cell (MSC)-derived EVs recapitulate many of the therapeutic effects of MSC transplantation — including anti-inflammatory, anti-fibrotic, and pro-angiogenic activities — without the risks of cell transplantation (immune rejection, tumorigenicity, embolism).

The clinical development of EV therapeutics reached an inflection point in January 2024 when Aruna Bio received the first FDA IND approval for a purified EV product (AB126) — neural cell-derived EVs for neurological disorders. As of early 2025, 292 clinical trials involving EVs have been registered globally, of which 170 are interventional (Hadizadeh et al., 2024). A Phase II randomized controlled trial demonstrated that localized administration of MSC-derived exosomes achieved complete closure of refractory perianal fistulas in 60% of Crohn's disease patients, compared to lower rates with conventional therapy (Hadizadeh et al., 2024).

### 4.4 Framework F302: Multi-Compartment Pharmacokinetics for Cell-Free Therapeutics

The pharmacokinetics of LNP-mRNA therapeutics differ fundamentally from small molecule drugs because the therapeutic agent (protein) is produced by the patient's own cells after mRNA uptake and translation. We model this as a two-stage process: LNP biodistribution followed by local protein production.

**Stage 1: LNP biodistribution.** For systemically delivered LNPs, the mRNA concentration in tissue compartment $i$ follows standard multi-compartment kinetics:

```math
\frac{dC_i^{\text{mRNA}}}{dt} = k_{\text{in},i} \cdot C_{\text{blood}} - k_{\text{out},i} \cdot C_i^{\text{mRNA}} - k_{\text{deg}} \cdot C_i^{\text{mRNA}}
```

For locally injected mRNA (e.g., intramyocardial VEGF mRNA), the initial condition is $C_{\text{local}}(0) = D_{\text{inject}} / V_{\text{local}}$ with clearance:

```math
\frac{dC_{\text{local}}^{\text{mRNA}}}{dt} = -\left(k_{\text{uptake}} + k_{\text{leak}} + k_{\text{deg,extra}}\right) \cdot C_{\text{local}}^{\text{mRNA}}
```

**Stage 2: Protein production.** Intracellular mRNA drives protein synthesis with translation rate $k_{\text{trans}}$ and mRNA decay rate $k_{\text{mRNA,deg}}$ (half-life ~8–12 hours for modified mRNA):

```math
\frac{dP_i}{dt} = k_{\text{trans}} \cdot C_{i,\text{intra}}^{\text{mRNA}} - \delta_P \cdot P_i
```

The protein production rate peaks approximately 6–12 hours after mRNA delivery and decays with the mRNA half-life, producing a transient pulse of therapeutic protein. For VEGF mRNA with $k_{\text{trans}} \approx 50$ proteins/mRNA/hour and intracellular mRNA half-life $\approx 10$ hours, peak local VEGF concentration reaches ~1–10 ng/mL — within the pro-angiogenic range but below the vascular permeability threshold — explaining the favorable safety profile observed in the EPICCURE trial (Anttila et al., 2023). The transient kinetics (protein production over ~48–72 hours) followed by decay is ideal for angiogenic signaling, which requires an initial VEGF stimulus to initiate endothelial sprouting but sustained supraphysiological levels cause aberrant vascular formation.

---

## 5. Xenotransplantation: The Clinical Frontier

### 5.1 Gene-Edited Pig Organs Reach Human Patients

While the endogenous repair strategies described above mature toward clinical application, xenotransplantation offers an immediate solution for the ~100,000+ patients on organ transplant waiting lists in the United States alone. The convergence of CRISPR gene editing and pig genetics has produced donor animals with unprecedented immunological compatibility, and 2024–2025 marked the transition from preclinical research to human clinical application.

**The eGenesis 69-gene pig.** The most extensively engineered xenotransplant donor is the eGenesis pig, which carries 69 genomic modifications: knockout of three porcine glycan antigens (αGal, Neu5Gc, Sda) that trigger hyperacute rejection, insertion of seven human transgenes (CD46, CD55, CD59, thrombomodulin, EPCR, HO1, CD47) that regulate complement, coagulation, and innate immunity, and inactivation of endogenous porcine retroviruses (PERVs) through 59 simultaneous gene edits — the largest multiplexed gene editing in any organism (Kawai et al., 2025). In 2025, Kawai and colleagues at Massachusetts General Hospital transplanted an eGenesis pig kidney into a living human patient with end-stage kidney disease. The patient achieved immediate dialysis independence and maintained kidney function for the duration of the study, with no evidence of hyperacute or antibody-mediated rejection — a historic milestone validating two decades of xenotransplantation research (Kawai et al., 2025). The patient ultimately died on day 52 from cardiac causes unrelated to the xenograft, with no pathological evidence of kidney rejection at autopsy (Kawai et al., 2025).

**Pig kidney survival records.** In parallel with the eGenesis approach, pig kidney xenotransplants using Revivicor 10-gene-edited pigs achieved extraordinary survival durations in decedent (brain-dead) human recipients maintained on ventilatory support. Tim Andrews achieved 271-day pig kidney survival — the longest reported — while Towana Looney maintained dialysis-free kidney function for over 130 days.

**FDA-approved clinical trials.** In September 2025, the FDA approved the first multi-center clinical trials of pig kidney xenotransplantation, with both eGenesis and United Therapeutics receiving clearance to enroll 30+ patients in prospective studies. This regulatory milestone marks the transition from compassionate-use cases to controlled clinical evaluation.

### 5.2 Multi-Omics Immunology of Xenografts

Understanding why some xenografts succeed and others fail requires comprehensive molecular characterization of the xenograft immune response. Schmauch, Keating, and colleagues published in Nature in 2026 the first multi-omics atlas of a pig-to-human kidney xenotransplant, integrating single-cell RNA sequencing, spatial transcriptomics, proteomics, and metabolomics (Schmauch et al., 2026). This analysis revealed several previously unknown features of the xenograft immune response. First, plasmablast expansion — rapidly proliferating antibody-secreting B cells — was the earliest detectable immune event, preceding clinical signs of rejection. Second, CXCL9-positive macrophages were the dominant immune cell population within the xenograft, suggesting that macrophage-mediated inflammation rather than T cell-mediated cytotoxicity may be the primary driver of chronic xenograft injury. Third, natural killer (NK) cell and dendritic cell (DC) expansion occurred in distinct temporal waves, providing potential therapeutic windows for targeted immunosuppression (Schmauch et al., 2026).

A companion study by Montgomery, Keating, and colleagues provided a comprehensive assessment of the physiology and immunology of the same xenotransplant, demonstrating that the pig kidney maintained normal human physiological parameters (creatinine clearance, electrolyte balance, erythropoietin production) while revealing the specific immune pathways that require further engineering in the donor pig or pharmacological management in the recipient (Montgomery et al., 2026).

### 5.3 Pig Heart Xenotransplantation

Cardiac xenotransplantation presents greater immunological challenges than renal xenotransplantation due to the heart's high metabolic demand and sensitivity to inflammation. Griffith, Mohiuddin, and colleagues at the University of Maryland published in Nature Medicine in 2025 the clinical details and lessons from the transplantation of a genetically modified porcine heart into a live human patient — the second such procedure worldwide (Griffith et al., 2025). The patient survived 40 days before succumbing to multiorgan failure. Comprehensive analysis revealed that porcine cytomegalovirus (pCMV) reactivation in the xenograft contributed to graft dysfunction — identifying viral screening as a critical quality control step for future xenotransplantation protocols (Griffith et al., 2025).

### 5.4 Framework F303: Competing Risks Model for Xenograft Survival

Xenograft failure can result from multiple independent causes — antibody-mediated rejection (AMR), infection, and organ-specific non-immunologic failure — that compete to determine the time to graft loss. We model this using a competing risks framework with cause-specific Weibull hazard functions.

The overall survival function is:

```math
S(t) = \exp\left(-\sum_{k=1}^{K} H_k(t)\right)
```

where $H_k(t)$ is the cumulative hazard for cause $k$. For three competing risks:

**Antibody-mediated rejection** with Weibull hazard (increasing risk over time as de novo antibodies develop):

```math
h_{\text{AMR}}(t) = \frac{\alpha_{\text{AMR}}}{\beta_{\text{AMR}}} \left(\frac{t}{\beta_{\text{AMR}}}\right)^{\alpha_{\text{AMR}} - 1}
```

with shape parameter $\alpha_{\text{AMR}} > 1$ (risk increases over time) and scale parameter $\beta_{\text{AMR}}$.

**Infection** with constant hazard (memoryless, reflecting ongoing immunosuppression risk):

```math
h_{\text{infect}}(t) = \lambda_{\text{infect}}
```

**Non-immunologic organ failure** with bathtub-shaped hazard (early surgical complications + late wear):

```math
h_{\text{organ}}(t) = \frac{\alpha_{\text{early}}}{\beta_{\text{early}}} \left(\frac{t}{\beta_{\text{early}}}\right)^{\alpha_{\text{early}} - 1} + \lambda_{\text{base}} + \frac{\alpha_{\text{late}}}{\beta_{\text{late}}} \left(\frac{t}{\beta_{\text{late}}}\right)^{\alpha_{\text{late}} - 1}
```

The cause-specific cumulative incidence function (CIF) — the probability of graft loss from cause $k$ by time $t$ — is:

```math
F_k(t) = \int_0^t h_k(u) \cdot S(u) \, du
```

This framework enables quantitative assessment of where therapeutic effort should be directed. From the available clinical data: for kidney xenografts, AMR is the dominant early risk (antibody-mediated), while infection dominates the intermediate period (immunosuppression-related). The eGenesis 69-gene pig substantially reduces $h_{\text{AMR}}$ through elimination of xenoantigens and insertion of human complement regulators, shifting the primary risk toward infection management. For heart xenografts, the data from Griffith et al. suggest that $h_{\text{infect}}$ is elevated due to pCMV reactivation, identifying viral monitoring as a priority intervention. As clinical trial data accumulate, Bayesian updating of the Weibull parameters will enable patient-specific risk stratification and adaptive immunosuppression protocols.

---

## 6. Smart Injectable Biomaterials for In Vivo Repair

The clinical implementation of in vivo tissue repair requires minimally invasive delivery systems that can be injected via catheter or syringe and then form functional scaffolds in situ. Recent advances in smart biomaterials have produced injectable systems that respond to physiological cues, deliver therapeutic payloads with controlled kinetics, and match the mechanical properties of target tissues.

**pH-responsive conductive hydrogels for cardiac repair.** Cheng and colleagues developed in 2025 an injectable pH-responsive conductive hydrogel designed specifically for myocardial infarction (MI) repair (Cheng et al., 2025). The hydrogel exploits the acidic pH of ischemic myocardium (pH ~6.5, versus healthy tissue pH ~7.4) to trigger gelation upon injection into the infarct zone. The conductive component restores electrical propagation across the scar, addressing the electromechanical uncoupling that causes fatal arrhythmias after MI. The hydrogel simultaneously delivers two therapeutic payloads — metformin (which activates AMPK-mediated cardioprotective pathways) and MSC-derived exosomes (which provide anti-inflammatory and pro-angiogenic signals) — with the acidic pH triggering accelerated release of both payloads specifically in the ischemic zone (Cheng et al., 2025). In a rat MI model, the smart hydrogel reduced infarct size, improved ejection fraction, and suppressed ventricular arrhythmias compared to non-responsive hydrogels or individual component delivery.

**Hydrogel design principles for cardiac regeneration.** Comprehensive reviews published in 2024–2025 have established the design principles for injectable cardiac hydrogels: mechanical modulus matching native myocardium (~10–50 kPa), controlled degradation over 2–8 weeks (matching the remodeling timeline), electrical conductivity to restore signal propagation, and capacity for controlled release of therapeutic agents (Xu et al., 2024; Holme et al., 2025). The field is converging on multi-functional hydrogel systems that simultaneously provide mechanical support, electrical continuity, drug delivery, and immune modulation — embodying the principle that effective tissue repair requires coordinated intervention across multiple biological axes simultaneously.

---

## 7. Open Questions and Clinical Outlook

### 7.1 Critical Challenges Across Pillars

**In situ reprogramming.** The primary obstacle to clinical translation is efficiency: current cardiac reprogramming approaches convert approximately 1–25% of targeted fibroblasts, and it remains unclear whether this is sufficient for clinically meaningful functional improvement in patients with large infarcts. Long-term safety data are also essential — do reprogrammed cardiomyocytes maintain their identity indefinitely, or do they revert to fibroblast-like states over months to years? The ASCL1-SA6 approach to neural reprogramming raises the additional question of whether converted inhibitory neurons integrate into existing cortical circuits with appropriate synaptic specificity. The competing fates framework (F299) predicts that reducing apoptosis during reprogramming will have a greater impact on net conversion than increasing the intrinsic reprogramming rate — suggesting that cytoprotective agents co-delivered with reprogramming factors may be as important as the factors themselves.

**Immune-instructive biomaterials.** The discovery of the senescent T cell/IL-17 barrier raises the question of whether IL-17 neutralization should become a standard adjunct therapy for biomaterial implantation in patients over 60 years of age. Given that anti-IL-17 antibodies (secukinumab, ixekizumab) are already FDA-approved for psoriasis, clinical trials of anti-IL-17 + biomaterial combination therapy could be initiated rapidly. The microbiome-biomaterial axis identified by Rutkowski et al. (2025) raises concerns about the nearly universal perioperative use of broad-spectrum antibiotics and its potential impact on biomaterial-mediated repair.

**Cell-free therapeutics.** The in vivo CAR T field must address durability: mRNA-based CAR expression is inherently transient (~48–72 hours), which is advantageous for fibrosis applications but may be insufficient for cancer indications requiring sustained tumor surveillance. The DNA-based stable integration approach (Bimbo et al., 2025) addresses this concern but introduces the safety risks of insertional mutagenesis that have historically complicated gene therapy.

**Xenotransplantation.** The multi-omics atlas (Schmauch et al., 2026) identified CXCL9+ macrophages as the dominant xenograft immune population, suggesting that macrophage-targeted immunosuppression — rather than the current T cell-focused regimens borrowed from allotransplantation — may be more effective. The pCMV reactivation event in the Maryland pig heart case (Griffith et al., 2025) mandates comprehensive pathogen screening protocols that the field is now implementing.

### 7.2 Convergence: Combining Pillars

The most powerful therapeutic approaches will likely combine multiple pillars. In situ cardiac reprogramming (Section 2.1) could be delivered via injectable smart hydrogels (Section 6) that provide both the reprogramming factors (GMT via AAV or mRNA) and the immunomodulatory signals (ECM-derived components) needed to create a pro-regenerative immune environment (Section 3). Xenotransplanted organs (Section 5) could be pre-conditioned with biomaterial coatings that recruit tolerogenic dendritic cells (Section 3.2) to reduce immunosuppression requirements. In vivo CAR T cells (Section 4.2) targeting senescent cells could be administered before biomaterial implantation in elderly patients to remove the senescent T cell barrier (Section 3.1), restoring the regenerative immune response.

### 7.3 The Next Decade

The clinical trajectory of in vivo tissue regeneration is accelerating. Xenotransplantation has already reached controlled clinical trials (FDA-approved, 2025). In vivo CAR T generation has entered Phase 1 (CPTX2309, 2025). VEGF mRNA cardiac injection has completed Phase 2a (EPICCURE, 2023). In situ cardiac reprogramming is approaching IND-enabling studies (Tenaya, estimated 2026–2027). Within a decade, the first generation of in vivo repair therapies — likely beginning with in vivo CAR T cells for autoimmunity and xenotransplanted kidneys for end-stage renal disease — will enter routine clinical practice, fundamentally transforming regenerative medicine from an ex vivo manufacturing challenge into an in vivo programming problem.

---

## References

Amor, C., Fernandez-Maestre, I., Chowdhury, S., Ho, Y. J., Zhu, Z., Massague, J., ... & Lowe, S. W. (2024). Prophylactic and long-lasting efficacy of senolytic CAR T cells against age-related metabolic dysfunction. *Nature Aging*, 4(3), 336–349. https://doi.org/10.1038/s43587-023-00560-5

Anttila, V., Saraste, A., Knuuti, J., Jaakkola, P., Hedman, M., Svedstrom, K., ... & Kaikkonen, M. U. (2023). Direct intramyocardial injection of VEGF mRNA in patients undergoing coronary artery bypass grafting. *Molecular Therapy*, 31(3), 866–874. https://doi.org/10.1016/j.ymthe.2022.11.017

Bimbo, J. F., van Diest, E., Murphy, D. E., Wouters, A. K., de Wilt, J. H. W., & Bol, K. F. (2025). T cell-specific non-viral DNA delivery and in vivo CAR-T generation using targeted lipid nanoparticles. *Journal for ImmunoTherapy of Cancer*, 13(7), e011759. https://doi.org/10.1136/jitc-2025-011759

Blau, H. M., & Daley, G. Q. (2019). Stem cells in the treatment of disease. *New England Journal of Medicine*, 380(18), 1748–1760. https://doi.org/10.1056/NEJMra1716145

Chen, Z. Y., Ji, S. J., Huang, C. W., Gu, W. Z., Wang, S. Y., Jiang, Y., ... & Wang, Y. (2024). In situ reprogramming of cardiac fibroblasts into cardiomyocytes in mouse heart with chemicals. *Acta Pharmacologica Sinica*, 45(11), 2290–2299. https://doi.org/10.1038/s41401-024-01308-6

Cheng, N., Luo, Q., Yang, Y., Sun, Y., Zhang, L., Xu, S., ... & Xiao, Z. (2025). Injectable pH responsive conductive hydrogel for intelligent delivery of metformin and exosomes to enhance cardiac repair after myocardial ischemia-reperfusion injury. *Advanced Science*, 12(24), e2410590. https://doi.org/10.1002/advs.202410590

DeStefano, S., Hartigan, D. R., Josyula, A., Frias, A. M., Chen, Y., & Sadtler, K. (2024). Conserved and tissue-specific immune responses to biologic scaffold implantation. *Acta Biomaterialia*, 184, 68–80. https://doi.org/10.1016/j.actbio.2024.06.013

Ding, S. (2025). Therapeutic reprogramming toward regenerative medicine. *Chemical Reviews*, 125(4), 1805–1822. https://doi.org/10.1021/acs.chemrev.4c00332

Garg, K., Pullen, N. A., Oskeritzian, C. A., Ryan, J. J., & Bowlin, G. L. (2013). Macrophage functional polarization (M1/M2) in response to varying fiber and pore dimensions of electrospun scaffolds. *Biomaterials*, 34(18), 4439–4451. https://doi.org/10.1016/j.biomaterials.2013.02.065

Griffith, B. P., Grazioli, A., Singh, A. K., Toth, K., Pierson, R. N., Eby, J., ... & Mohiuddin, M. M. (2025). Transplantation of a genetically modified porcine heart into a live human. *Nature Medicine*, 31(2), 589–598. https://doi.org/10.1038/s41591-024-03429-1

Hadizadeh, A., Akbari Asbagh, R., Heirani-Tabasi, A., Khoshfetrat, A. B., Pourfathollah, A. A., & Haeri, A. (2024). Localized administration of mesenchymal stem cell-derived exosomes for the treatment of refractory perianal fistula in patients with Crohn's disease: A phase II clinical trial. *Diseases of the Colon and Rectum*, 67(12), 1564–1575. https://doi.org/10.1097/DCR.0000000000003502

Han, J., Cherry, C., Mejias, J. C., Krishnan, N., Khan, A., Rao, S., ... & Elisseeff, J. H. (2024a). Age-associated senescent–T cell signaling promotes type 3 immunity that inhibits the biomaterial regenerative response. *Advanced Materials*, 36(43), e2310476. https://doi.org/10.1002/adma.202310476

Han, J., Rindone, A. N., & Elisseeff, J. H. (2024b). Immunoengineering biomaterials for musculoskeletal tissue repair across lifespan. *Advanced Materials*, 36(28), e2311646. https://doi.org/10.1002/adma.202311646

Holme, S., Richardson, S. M., Bella, J., & Sherborne, C. (2025). Hydrogels for cardiac tissue regeneration: Current and future developments. *International Journal of Molecular Sciences*, 26(5), 2309. https://doi.org/10.3390/ijms26052309

Huang, P., Xu, J., Keepers, B., Bhatt, A. B., Qian, L., & Song, K. (2024). Direct cardiac reprogramming via combined CRISPRa-mediated endogenous Gata4 activation and exogenous Mef2c and Tbx5 expression. *Molecular Therapy: Nucleic Acids*, 35(4), 102390. https://doi.org/10.1016/j.omtn.2024.102390

Hunter, T. L., Bao, Y., Zhang, Y., Tran, K. A., Rotolo, L., Li, X., ... & Bhatt, A. (2025). In vivo CAR T cell generation to treat cancer and autoimmune disease. *Science*, 388(6753), 1311–1317. https://doi.org/10.1126/science.ads8473

Ieda, M., Fu, J. D., Delgado-Olguin, P., Vedantham, V., Hayashi, Y., Bruneau, B. G., & Srivastava, D. (2010). Direct reprogramming of fibroblasts into functional cardiomyocytes by defined factors. *Cell*, 142(3), 375–386. https://doi.org/10.1016/j.cell.2010.07.002

Kawai, T., Williams, W. W., Elias, N., Adams, A. B., O'Connor, K. M., Tector, A. J., ... & Markmann, J. F. (2025). Xenotransplantation of a porcine kidney for end-stage kidney disease. *New England Journal of Medicine*, 392(19), 1933–1940. https://doi.org/10.1056/NEJMoa2412747

Keshri, R., Detraux, D., Phal, A., Herring, L. E., & Bhutani, N. (2024). Next-generation direct reprogramming. *Frontiers in Cell and Developmental Biology*, 12, 1343106. https://doi.org/10.3389/fcell.2024.1343106

Li, J., Li, R., Bai, X., Zhang, L., Chen, W., & Zhang, S. (2024). Direct reprogramming of fibroblasts into functional hepatocytes via CRISPRa activation of endogenous Gata4 and Foxa3. *Chinese Medical Journal*, 137(11), 1351–1359. https://doi.org/10.1097/CM9.0000000000003088

Li, W., Su, D., Li, X., Zhang, Y., Yuan, X., & Chen, G. (2025). Identification of the core regulatory program driving NEUROD1-induced neuronal reprogramming. *Cell Reports*, 44(4), 115523. https://doi.org/10.1016/j.celrep.2025.115523

Lin, H., Wang, X., Chung, M., Chen, J., & Li, T. (2025). Direct fibroblast reprogramming: An emerging strategy for treating organic fibrosis. *Journal of Translational Medicine*, 23(1), 240. https://doi.org/10.1186/s12967-024-06060-3

Lokwani, R., Josyula, A., Ngo, T. B., Patel, M., Frias, A., & Sadtler, K. (2024). Pro-regenerative biomaterials recruit immunoregulatory dendritic cells after traumatic injury. *Nature Materials*, 23(1), 147–157. https://doi.org/10.1038/s41563-023-01689-9

Marichal, N., Peron, S., Beltran Arranz, A., Galante, C., Gascon, S., & Berninger, B. (2024). Reprogramming astroglia into neurons with hallmarks of fast-spiking parvalbumin-positive interneurons by phospho-site-deficient Ascl1. *Science Advances*, 10(43), eadl5935. https://doi.org/10.1126/sciadv.adl5935

Montgomery, R. A., Stern, J. M., Fathi, F., Smith, D. E., Lorber, M. I., Arend, L. J., ... & Keating, B. J. (2026). Physiology and immunology of a pig-to-human decedent kidney xenotransplant. *Nature*, 650(8100), 218–229. https://doi.org/10.1038/s41586-025-09847-6

Nakano, K., Sadahiro, T., Fujita, R., Oura, S., Tsuchiya, M., & Ieda, M. (2024). Development of adeno-associated viral vectors targeting cardiac fibroblasts for efficient in vivo cardiac reprogramming. *Stem Cell Reports*, 19(10), 1389–1398. https://doi.org/10.1016/j.stemcr.2024.08.002

Nakatsukasa, Y., Yamada, Y., & Yamada, Y. (2025). Research of in vivo reprogramming toward clinical applications in regenerative medicine: A concise review. *Regenerative Therapy*, 28, 12–19. https://doi.org/10.1016/j.reth.2024.11.008

Pal, S., Chaudhari, R., Baurceanu, I., Bhatt, A., Carlson, J. C., Cramer, R. A., & Wolf, M. T. (2024). Extracellular matrix scaffold-assisted tumor vaccines induce tumor regression and long-term immune memory. *Advanced Materials*, 36(15), e2309843. https://doi.org/10.1002/adma.202309843

Pereira, A., Diwakar, J., Masserdotti, G., Marangon, D., Irmler, M., Beckers, J., ... & Gotz, M. (2024). Direct neuronal reprogramming of mouse astrocytes is associated with multiscale epigenome remodeling and requires Yy1. *Nature Neuroscience*, 27(7), 1260–1273. https://doi.org/10.1038/s41593-024-01677-5

Porrello, E. R., Mahmoud, A. I., Simpson, E., Hill, J. A., Richardson, J. A., Olson, E. N., & Sadek, H. A. (2011). Transient regenerative potential of the neonatal mouse heart. *Science*, 331(6020), 1078–1080. https://doi.org/10.1126/science.1200708

Qian, L., Huang, Y., Spencer, C. I., Foley, A., Vedantham, V., Liu, L., ... & Srivastava, D. (2012). In vivo reprogramming of murine cardiac fibroblasts into induced cardiomyocytes. *Nature*, 485(7400), 593–598. https://doi.org/10.1038/nature11044

Rurik, J. G., Tombacz, I., Yadegari, A., Mendez Fernandez, P. O., Shewale, S. V., Li, L., ... & Epstein, J. A. (2022). CAR T cells produced in vivo to treat cardiac injury. *Science*, 375(6576), 91–96. https://doi.org/10.1126/science.abm0594

Rutkowski, N., Yang, B., Gray-Gaillard, E., Fournelle, S., Li, Y., Bhatt, A., ... & Elisseeff, J. H. (2025). Antibiotic-induced microbiota depletion impairs the proregenerative response to a biological scaffold. *Proceedings of the National Academy of Sciences*, 122(52), e2510841122. https://doi.org/10.1073/pnas.2510841122

Sadtler, K., Estrellas, K., Allen, B. W., Wolf, M. T., Fan, H., Tam, A. J., ... & Elisseeff, J. H. (2016). Developing a pro-regenerative biomaterial scaffold microenvironment requires T helper 2 cells. *Science*, 352(6283), 366–370. https://doi.org/10.1126/science.aad9272

Schmauch, E., Piening, B. D., Dowdell, A. K., Gao, B., Gibbs, D., Kim, S. J., ... & Keating, B. J. (2026). Multi-omics analysis of a pig-to-human decedent kidney xenotransplant. *Nature*, 650(8100), 205–217. https://doi.org/10.1038/s41586-025-09846-7

Segura, T. (2024). From soft microgel assemblies to advanced healthcare materials. *Advanced Healthcare Materials*, 13(25), e2402905. https://doi.org/10.1002/adhm.202402905

Takahashi, K., & Yamanaka, S. (2006). Induction of pluripotent stem cells from mouse embryonic and adult fibroblast cultures by defined factors. *Cell*, 126(4), 663–676. https://doi.org/10.1016/j.cell.2006.07.024

Wang, B., Han, J., Elisseeff, J. H., & Demaria, M. (2024). The senescence-associated secretory phenotype and its physiological and pathological implications. *Nature Reviews Molecular Cell Biology*, 25(12), 958–978. https://doi.org/10.1038/s41580-024-00727-x

Wu, Z., Xu, L., Xie, Y., Zhang, Y., Feng, R., Zhang, J., ... & Chen, G. (2025). Brain-wide neuroregenerative gene therapy improves cognition in a mouse model of Alzheimer's disease. *Advanced Science*, 12(14), e2410080. https://doi.org/10.1002/advs.202410080

Xu, Q., Xiao, Z., Yang, Q., Yang, L., Shi, Y., & He, L. (2024). Hydrogel-based cardiac repair and regeneration function in the treatment of myocardial infarction. *Materials Today Bio*, 25, 100978. https://doi.org/10.1016/j.mtbio.2024.100978

Zhang, H., Wei, Y., Wang, Y., Xu, Y., Li, X., & Li, Y. (2024). Emerging diabetes therapies: Regenerating pancreatic beta cells. *Tissue Engineering Part B: Reviews*, 30(6), 644–656. https://doi.org/10.1089/ten.TEB.2024.0041
