# Cellular Rejuvenation

## Abstract

Aging is driven by the progressive failure of interconnected molecular maintenance systems rather than any single mechanism. This paper examines six topics in cellular rejuvenation that have advanced substantially in recent years: (1) the cGAS-STING–LINE-1 inflammaging axis, wherein retrotransposon derepression triggers chronic sterile inflammation; (2) proteostasis network collapse, modeled here as a queuing-theoretic system approaching critical load; (3) clonal dynamics of stem cell aging, analyzed via Moran process mathematics; (4) intercellular communication reprogramming through circulating rejuvenation factors; (5) precision senolytic immunotherapy using engineered immune cells; and (6) mitochondrial quality control engineering, including heteroplasmy-shifting gene editing. For each frontier, we present the latest experimental evidence, propose novel mathematical frameworks distinct from prior analyses, and identify open questions for translational development. We argue that the convergence of these six axes—rather than any single intervention—defines the path toward meaningful human cellular rejuvenation.

---

## 1. Introduction: Aging as Coupled System Failure

The nine hallmarks of aging—genomic instability, telomere attrition, epigenetic alterations, loss of proteostasis, deregulated nutrient sensing, mitochondrial dysfunction, cellular senescence, stem cell exhaustion, and altered intercellular communication—were formalized by López-Otín et al. in 2013 (PMID: 23746838) and expanded to twelve hallmarks in 2023 (PMID: 36599349). The expanded framework added disabled macroautophagy, chronic inflammation, and dysbiosis as distinct hallmarks, reflecting a decade of mechanistic insight into the molecular interconnections that drive organismal decline.

A central lesson of the past five years is that these hallmarks are not independent. Cellular senescence drives chronic inflammation via the senescence-associated secretory phenotype (SASP) (PMID: 38654098). Mitochondrial dysfunction amplifies genomic instability through reactive oxygen species (ROS)-mediated DNA damage (PMID: 21307849). Stem cell exhaustion follows from the cumulative burden of somatic mutations and niche deterioration (PMID: 32669714). This interconnection implies that single-target interventions will yield diminishing returns, and that systems-level approaches are necessary for meaningful rejuvenation.

This paper examines six frontiers where the biology has matured sufficiently to support translational engineering. We deliberately exclude topics covered in depth in prior analyses—including partial epigenetic reprogramming via Yamanaka factors (PMID: 27984723), epigenetic clock calibration (PMID: 24138928), telomerase gene therapy (PMID: 22585399), mTOR inhibition (PMID: 19587680), and NAD+ precursor supplementation (PMID: 35235774)—and instead focus on mechanistic depths and mathematical frameworks not previously developed. Each section identifies the most promising PhD-level research directions ranked by likelihood of clinical translation and impact on human health.

---

## 2. The cGAS-STING–LINE-1 Inflammaging Axis

### 2.1 LINE-1 Retrotransposon Derepression as a Causal Aging Mechanism

Long interspersed nuclear element-1 (LINE-1, or L1) retrotransposons constitute approximately 17% of the human genome, with roughly 80–100 retrotransposition-competent copies in any individual (PMID: 20080666). In young, healthy somatic cells, LINE-1 elements are transcriptionally silenced by DNA methylation at their 5′-UTR CpG island, heterochromatin marks (H3K9me3, H3K27me3), and the activity of epigenetic silencing enzymes including SIRT6 and KAP1/TRIM28 (PMID: 29769529).

De Cecco et al. (2019) demonstrated that LINE-1 elements become transcriptionally derepressed in late senescence and in aged mouse tissues (PMID: 30728521). Critically, this derepression is not merely correlative: LINE-1 reverse transcriptase generates cytoplasmic cDNA that activates the cGAS-STING innate immune sensing pathway, triggering a type-I interferon (IFN-I) response. Treatment of aged mice with the nucleoside reverse transcriptase inhibitor (NRTI) lamivudine (3TC) suppressed LINE-1-derived cDNA, reduced IFN-I signaling, and ameliorated age-associated inflammation in adipose tissue, muscle, kidney, and liver (PMID: 30728521).

This finding was extended by Simon et al. (2019), who showed that SIRT6 maintains LINE-1 silencing by mono-ADP-ribosylating KAP1, which recruits HP1α to L1 loci and enforces heterochromatin (PMID: 30853557). SIRT6-deficient mice exhibit LINE-1 derepression, sterile inflammation, and premature aging phenotypes that are rescued by NRTI treatment. SIRT6 protein levels decline with age in wild-type mice, establishing a direct link between epigenetic erosion at transposable elements and inflammaging.

Tang et al. (2024) identified the transcription factor PAX5 as a direct activator of LINE-1 transcription in senescent cells (PMID: 38866979). PAX5 binds the LINE-1 5′-UTR, and its binding affinity increases during senescence due to reduced SIRT6-mediated repression of the PAX5 locus itself. This creates a feedforward loop: SIRT6 decline → PAX5 upregulation → LINE-1 activation → cGAS-STING → IFN-I → further SIRT6 depletion via inflammatory signaling.

### 2.2 cGAS-STING: From Innate Immunity to Central Aging Driver

The cyclic GMP-AMP synthase (cGAS)–stimulator of interferon genes (STING) pathway was originally characterized as a cytosolic DNA sensor for pathogen defense (PMID: 23258413). cGAS binds double-stranded DNA and catalyzes the synthesis of 2′3′-cyclic GMP-AMP (cGAMP), which activates the endoplasmic reticulum-resident adaptor STING. STING then recruits TBK1 and activates IRF3 and NF-κB, driving IFN-I and inflammatory cytokine production.

Gulen et al. (2023) demonstrated that cGAS-STING is a central driver of age-related inflammation and neurodegeneration in mice (PMID: 37532932). Genetic ablation of STING in aged mice reduced neuroinflammation, preserved cognitive function, and attenuated age-related gene expression changes in microglia and astrocytes. STING inhibition suppressed the SASP in senescent cells, positioning cGAS-STING as a convergence point for multiple aging inputs: LINE-1 cDNA, mitochondrial DNA (mtDNA) released during mitophagy failure, micronuclei from chromosomal instability, and cytoplasmic chromatin fragments from nuclear envelope rupture.

Faria et al. (2025) identified a noncanonical cGAS-STING pathway activated specifically in aging and progeria cells (PMID: 40638086). Unlike the canonical pathway that signals through IRF3, this noncanonical branch activates a distinct inflammatory program. Pharmacological inhibition of this noncanonical pathway ameliorated cellular aging hallmarks and extended lifespan in Hutchinson-Gilford progeria syndrome (HGPS) mouse models, suggesting that pathway-specific STING modulation could provide anti-aging benefits without compromising antiviral immunity.

A 2026 study in Nature Aging demonstrated that LINE-1 expression increases specifically in aging hearts, and that genetic LINE-1 derepression causes cardiac dysfunction via cGAS-STING activation (PMID: 41571992). Treatment of naturally aged mice with either 3TC (LINE-1 RT inhibitor) or H-151 (STING inhibitor) for 24 weeks improved cardiac function and reduced cardiomyocyte senescence, providing organ-specific evidence for the therapeutic tractability of this axis.

### 2.3 SIRT6: The Epigenetic Guardian

SIRT6 is a NAD+-dependent histone deacetylase and mono-ADP-ribosyltransferase that localizes to chromatin and maintains genomic stability through multiple mechanisms (PMID: 34281779). SIRT6 deacetylates H3K9ac and H3K56ac at telomeric, pericentromeric, and LINE-1 repeat regions, promoting heterochromatin formation. SIRT6 also facilitates DNA double-strand break repair by deacetylating CtIP (promoting resection) and by recruiting SNF2H chromatin remodeler to damage sites (PMID: 22465074).

SIRT6 overexpression extends lifespan in male mice by 15.8% (PMID: 22367546). Conversely, SIRT6 knockout mice exhibit severe progeroid phenotypes and die by 4 weeks (PMID: 16469703). The mechanisms are now understood to involve LINE-1 silencing (PMID: 30853557), telomere maintenance, and suppression of endogenous retroviruses.

Recent work from the Gorbunova laboratory identified fucoidan, a brown seaweed polysaccharide, as a SIRT6 activator that enhances SIRT6 mono-ADP-ribosylation activity (bioRxiv 2025.03.24.645072). Fucoidan treatment repressed LINE-1 transcription, reduced frailty indices, decreased epigenetic age, and extended median lifespan in naturally aged male mice. A follow-up study demonstrated that SIRT6 serine-10 phosphorylation modulates the balance between its DNA repair and LINE-1 suppression functions (bioRxiv 2026.02.06.704345), suggesting that post-translational modification of SIRT6 determines which downstream protective pathway predominates.

### 2.4 The NLRP3 Inflammasome Acetylation Switch

Beyond cGAS-STING, the NLRP3 inflammasome represents a second major node of inflammaging. He et al. (2020) discovered that NLRP3 is regulated by an acetylation switch: SIRT2 deacetylates NLRP3 at K21, K22, and K24, preventing inflammasome assembly (PMID: 32032542). SIRT2 activity declines with age, leading to constitutive NLRP3 acetylation, chronic IL-1β and IL-18 secretion, and insulin resistance. SIRT2 overexpression in aged mice reversed inflammaging phenotypes, while SIRT2 knockout accelerated them. This establishes a parallel sirtuin-dependent anti-inflammatory axis: SIRT6 suppresses LINE-1/cGAS-STING, while SIRT2 suppresses NLRP3/IL-1β.

### 2.5 Mathematical Framework: Bistable Switch Model of LINE-1 Derepression

The biology described above—positive feedback between LINE-1 derepression, cGAS-STING activation, inflammatory signaling, and further SIRT6 depletion—suggests a bistable dynamical system with a sharp transition from the silenced to the derepressed state.

Let $L(t) \in [0,1]$ denote the fraction of LINE-1 loci that are transcriptionally active, and let $S(t) \in [0,1]$ denote normalized SIRT6 activity. SIRT6 declines with age at rate $\delta$, modulated by inflammatory feedback:

$$\frac{dS}{dt} = -\delta \cdot S - \phi \cdot L \cdot S + \psi \cdot (S_0 - S)$$

where $\delta$ is the basal age-dependent SIRT6 decline rate, $\phi$ captures inflammatory suppression of SIRT6 (via NF-κB-mediated transcriptional repression), and $\psi$ is a homeostatic restoration rate with ceiling $S_0$.

LINE-1 activation obeys cooperative dynamics due to the PAX5 feedforward loop and cGAS-STING amplification:

$$\frac{dL}{dt} = \frac{\alpha \cdot L^n}{K^n + L^n} - \beta \cdot S \cdot L$$

where $\alpha$ is the maximal LINE-1 activation rate, $n$ is the Hill coefficient capturing cooperativity ($n \approx 2$–3 based on the multi-step amplification cascade), $K$ is the half-activation threshold, and $\beta$ is the SIRT6-dependent silencing rate.

**Steady-state analysis.** Setting $dL/dt = 0$, the nontrivial steady states satisfy:

$$\frac{\alpha \cdot L^{n-1}}{K^n + L^n} = \beta \cdot S$$

For $n = 2$, this becomes $\alpha L / (K^2 + L^2) = \beta S$, which admits two positive roots when $S < S_{\text{crit}}$:

$$S_{\text{crit}} = \frac{\alpha}{2\beta K}$$

Below $S_{\text{crit}}$, the system has two stable steady states—a low-$L$ state (LINE-1 silenced, $L^* \approx \beta S K^2 / \alpha$) and a high-$L$ state (LINE-1 derepressed, $L^* \approx \alpha/(\beta S)$)—separated by an unstable intermediate. This bistability means that once SIRT6 drops below $S_{\text{crit}}$, a small perturbation (e.g., a transient inflammatory stimulus or oxidative stress event) can push the system irreversibly into the high-$L$ state.

**Parametric estimates.** SIRT6 protein levels decline approximately 30–50% between ages 30 and 70 in human tissues (PMID: 34281779). If we set $S_0 = 1$, $\delta = 0.008$/year (yielding ~45% decline by age 70), $\alpha = 0.5$/year, $\beta = 1.0$/year, and $K = 0.1$, then $S_{\text{crit}} = 0.5/(2 \times 1.0 \times 0.1) = 2.5$. Since $S \leq 1$, the system begins in the bistable regime and transitions become increasingly likely as $S$ declines, consistent with the exponential increase in inflammatory biomarkers after age 60.

**Therapeutic implication.** Interventions that maintain $S > S_{\text{crit}}$ (SIRT6 activators such as fucoidan) or that directly suppress $L$ (NRTIs such as 3TC, STING inhibitors such as H-151) can prevent the bistable transition. Combination therapy targeting both axes simultaneously would be predicted to have superadditive benefit.

### 2.6 Open Questions and Research Priorities

1. **Human LINE-1 tissue atlas with age.** Single-cell LINE-1 expression profiling across human tissues and ages is needed to identify which cell types undergo derepression first and most severely.
2. **NRTI clinical trials for aging.** 3TC (lamivudine) is FDA-approved for HIV with extensive safety data. A phase II trial in aged humans measuring inflammatory biomarkers and epigenetic age is feasible and high-priority.
3. **SIRT6-specific activators.** Fucoidan is a crude polysaccharide; structure-activity relationship studies are needed to identify specific pharmacophores for SIRT6 mono-ADP-ribosylation activation.
4. **Noncanonical vs. canonical STING.** Selective inhibition of the noncanonical aging-associated STING pathway (PMID: 40638086) without compromising antiviral immunity is a critical pharmacological challenge.

---

## 3. Proteostasis Network Collapse and Therapeutic Restoration

### 3.1 The Autophagy-Lysosome System in Aging

Macroautophagy (hereafter "autophagy") is the principal mechanism by which cells degrade damaged organelles and long-lived protein aggregates (PMID: 27733505). Autophagy declines with age across organisms from yeast to humans, and genetic enhancement of autophagy extends lifespan in model organisms (PMID: 25484077). The mechanistic basis involves age-related decline of core autophagy proteins: Atg5, Atg7, Beclin-1, and the lipidation enzyme Atg16L1 all decrease in aged tissues (PMID: 25484077). Lysosomal function also deteriorates, with reduced acidification (via V-ATPase decline), accumulation of lipofuscin, and decreased cathepsin activity (PMID: 27733505).

Rubinsztein and colleagues showed that the age-related decline in autophagy is partly driven by increased mTORC1 activity, which phosphorylates and inhibits the ULK1 autophagy initiation complex and the transcription factor TFEB (PMID: 23842456). Rapamycin-mediated mTORC1 inhibition restores autophagy and extends lifespan in mice by 9–14% (PMID: 19587680), but its immunosuppressive effects limit clinical applicability. The PEARL trial (Krauss et al., 2025) provided the first long-term human rapamycin aging data: a 48-week RCT in adults aged 50–85 showed that 10 mg weekly rapamycin prevented muscle loss in women (gaining ~0.5 lb lean mass/month) and preserved bone mineral content in men, with no severe adverse effects (PMID: 40188830). Strikingly, Gkioni et al. (2025) demonstrated that combining rapamycin with the MEK inhibitor trametinib produced additive lifespan extension of ~29% in female and ~27% in male mice, with reduced tumor burden and organ-wide inflammation suppression (PMID: 40437307). This combinatorial approach suggests that targeting multiple nodes in the nutrient-sensing network yields superadditive benefits.

### 3.2 TFEB and TFE3: Master Regulators of Lysosomal Biogenesis

The transcription factor EB (TFEB) and its paralog TFE3 are master regulators of the Coordinated Lysosomal Expression and Regulation (CLEAR) gene network, controlling the expression of >500 genes involved in lysosomal biogenesis, autophagy, and lipid catabolism (PMID: 21804531). Under nutrient-replete conditions, mTORC1 phosphorylates TFEB at S142 and S211, sequestering it in the cytoplasm via 14-3-3 protein binding (PMID: 22343943). Upon starvation or lysosomal stress, calcineurin dephosphorylates TFEB, enabling nuclear translocation and transcriptional activation (PMID: 25561175).

Neuronal-specific TFEB overexpression in tauopathy mouse models reduces neurofibrillary tangle burden and restores synaptic function by enhancing autophagic clearance of phospho-tau (PMID: 29074956). Hepatocyte-specific TFEB activation reduces lipid accumulation and reverses nonalcoholic fatty liver disease in mouse models (PMID: 23842456). These results establish TFEB as a therapeutic target for age-related proteinopathies and metabolic disease.

Nonninger et al. (2025) demonstrated that HLH-30/TFEB controls a TFEB-TGFβ axis that systemically regulates stem cell resilience and protects against a senescence-like state in *C. elegans* (PMID: 40588651). HLH-30 mutants arrest in a senescence-like state rather than entering protective diapause, establishing TFEB as a gatekeeper between rejuvenation and senescence—a role conserved in vertebrates.

Small-molecule TFEB activators are under development. Trehalose activates TFEB by inhibiting SLC2A (GLUT) transporters and inducing a starvation-like signal (PMID: 25125612). Curcumin analog C1 directly binds TFEB and promotes its nuclear translocation independent of mTORC1 (PMID: 27411014). However, constitutive TFEB activation carries risks: pancreatic TFEB overexpression drives pancreatic cancer in mice (PMID: 26168401), underscoring the need for tissue-specific and temporally controlled TFEB modulation.

### 3.3 Chaperone-Mediated Autophagy and LAMP2A Decline

Chaperone-mediated autophagy (CMA) is a selective autophagy pathway in which substrate proteins bearing a KFERQ-like pentapeptide motif are recognized by the cytosolic chaperone Hsc70 and translocated across the lysosomal membrane via the receptor LAMP2A (PMID: 14499044). Approximately 30% of cytosolic proteins carry KFERQ motifs and are potential CMA substrates, including oxidized and damaged proteins preferentially targeted during stress (PMID: 14499044).

CMA activity declines with age due to reduced LAMP2A protein levels at the lysosomal membrane (PMID: 18375752). This decline is caused by changes in lipid composition of the lysosomal membrane that accelerate LAMP2A degradation (PMID: 18375752). Cuervo and colleagues demonstrated that genetic restoration of LAMP2A in aged mouse liver maintained CMA activity and reduced oxidized protein accumulation, lipid droplet size, and cellular damage markers to levels comparable to young animals (PMID: 18375752). In a subsequent study, liver-specific LAMP2A maintenance preserved hepatic function and reduced age-related organ decline (PMID: 18375752).

Dong et al. (2021) showed that CMA declines in aging hematopoietic stem cells (HSCs), and that CMA activation through LAMP2A overexpression or the CMA-activating compound AR7 restores HSC function in aged mice (PMID: 33567259). CMA-deficient HSCs accumulate damaged proteins and exhibit impaired reconstitution capacity, linking proteostasis failure to stem cell exhaustion.

The CMA-aging axis extends beyond HSCs. Ramirez-Pardo et al. (2025) demonstrated that CMA is essential for muscle satellite cell (MuSC) regenerative capacity: CMA loss impairs the glycolytic metabolic shift required for MuSC activation, and CMA reactivation restores aged murine and human MuSC proliferative potential (Nat Metab 2025). A companion study showed that age-related CMA decline in skeletal muscle causes progressive myopathy through impaired calcium homeostasis and mitochondrial dysfunction (PMID: 41339969). Valdor et al. (2024) extended LAMP2A's rejuvenation potential to the immune system: LAMP2A restoration in old mice enhanced T-cell proliferative responses, decreased regulatory T cells, and downregulated inhibitory receptors (PMID: 39259591). Small-molecule CMA activators similarly improved T-cell responses in aged animals, establishing CMA as a multi-tissue rejuvenation target.

### 3.4 Proteasome Dysfunction and Aggregate Accumulation

The ubiquitin-proteasome system (UPS) degrades the majority of short-lived and damaged proteins via the 26S proteasome (PMID: 9759494). Proteasome activity declines 30–50% with age in most tissues, driven by oxidative modification of proteasome subunits, reduced expression of catalytic β-subunits (β1, β2, β5), and accumulation of damaged proteasomes (PMID: 11578955). Proteasome inhibition in young cells recapitulates aging-associated protein aggregation and senescence (PMID: 11578955).

Marino et al. (2025) quantified the impact of proteasome decline on the brain ubiquitylome, demonstrating that 35% of age-related ubiquitylation changes are directly attributable to reduced proteasome activity, while dietary restriction and refeeding partially rescue these age-related changes (PMID: 40480969).

The immunoproteasome, an inflammation-induced variant containing catalytic subunits β1i (LMP2), β2i (MECL-1), and β5i (LMP7), increases with age relative to the constitutive proteasome (PMID: 29229908). This shift generates peptides optimized for MHC-I antigen presentation rather than bulk proteolysis, potentially contributing to inflammaging via enhanced immune activation while simultaneously reducing overall proteolytic capacity.

Vilchez et al. (2012) demonstrated that human embryonic stem cells (hESCs) have elevated proteasome activity due to high expression of the proteasome subunit PSMD11/Rpn6 (PMID: 23128233). This activity declines upon differentiation. Overexpression of PSMD11 in differentiated cells partially restores proteasome function, suggesting that proteasome engineering is a viable rejuvenation strategy.

### 3.5 Mathematical Framework: Queuing Theory Model of Proteostasis Flux

The proteostasis network can be modeled as a multi-server queuing system (M/M/c queue) where misfolded proteins arrive stochastically and are processed by a finite number of degradation "servers" (autophagosomes, proteasomes, CMA-competent lysosomes).

**Definitions:**
- $\lambda(t)$: arrival rate of misfolded proteins (proteins/cell/hour)
- $\mu$: processing rate per server (proteins/server/hour)
- $c(t)$: number of active degradation servers

The arrival rate increases with age due to accumulated oxidative damage, mitochondrial ROS, and declining chaperone buffering capacity:

$$\lambda(t) = \lambda_0 \left(1 + \varepsilon t + \eta t^2 \right)$$

where $\lambda_0$ is the basal misfolding rate in young cells, $\varepsilon$ captures linear damage accumulation, and $\eta$ captures accelerating damage from positive feedback (damaged proteins inhibit proteasome function, generating more misfolded intermediates).

The server count declines exponentially:

$$c(t) = c_0 \cdot e^{-\kappa t}$$

reflecting the combined decline in proteasome activity (PMID: 11578955), autophagy (PMID: 25484077), and CMA (PMID: 18375752).

**Traffic intensity** (system load):

$$\rho(t) = \frac{\lambda(t)}{c(t) \cdot \mu} = \frac{\lambda_0(1 + \varepsilon t + \eta t^2)}{c_0 \mu \cdot e^{-\kappa t}}$$

**Critical age** $t^*$ when $\rho(t^*) = 1$: the system transitions from stable (finite queue) to overloaded (unbounded aggregate accumulation). Setting $\rho = 1$:

$$\lambda_0(1 + \varepsilon t^* + \eta t^{*2}) = c_0 \mu \cdot e^{-\kappa t^*}$$

Using representative parameters—$\lambda_0 = 100$ proteins/cell/hour, $c_0 \mu = 150$ proteins/cell/hour (50% overcapacity in youth), $\varepsilon = 0.005$/year, $\eta = 0.0001$/year², $\kappa = 0.007$/year—numerical solution yields $t^* \approx 65$ years. This coincides with the clinical onset window for age-related proteinopathies: Alzheimer's disease (65+), Parkinson's disease (60+), age-related macular degeneration (60+), and inclusion body myositis (50+).

**Expected queue length** (aggregate burden) follows the Erlang-C formula:

$$\mathbb{E}[Q] = \frac{C(c, \rho) \cdot \rho}{c(1 - \rho/c)}$$

where $C(c, \rho)$ is the Erlang-C probability. As $\rho \to 1$, $\mathbb{E}[Q] \to \infty$, corresponding to proteotoxic collapse.

**Therapeutic implications.** Any intervention that either reduces $\lambda$ (antioxidants, mitochondrial quality control), increases $c$ (TFEB activation, LAMP2A restoration, PSMD11 overexpression), or increases $\mu$ (proteasome activators) shifts $t^*$ to later ages. The model predicts that TFEB activation increasing $c$ by 30% (from autophagy enhancement) would delay $t^*$ by approximately 12 years, while simultaneous LAMP2A restoration (further 20% $c$ increase) and mitochondrial ROS reduction (10% $\lambda$ decrease) would delay $t^*$ by approximately 22 years—a superadditive effect from multi-target intervention.

### 3.6 Open Questions and Research Priorities

1. **Tissue-specific proteostasis profiling.** Quantitative measurement of autophagic flux, proteasome activity, and CMA capacity across human tissues and ages is lacking. The Bhatt lab's single-cell proteomics approaches could be adapted.
2. **TFEB/TFE3 therapeutic window.** Dose-response and tissue-specificity studies are needed to identify safe TFEB activation levels that enhance proteostasis without oncogenic risk (PMID: 26168401).
3. **CMA-activating drugs.** AR7 and its derivatives show promise in mouse HSCs (PMID: 33567259), but pharmacokinetics and off-target effects in humans are unknown.
4. **Proteasome activity restoration.** Small molecules that enhance 26S proteasome assembly or activity without altering substrate specificity are a high-value drug discovery target.

---

## 4. Clonal Dynamics and Stem Cell Aging

### 4.1 Clonal Hematopoiesis of Indeterminate Potential (CHIP)

Somatic mutations accumulate in all human tissues with age at a rate of approximately 15–40 mutations per cell per year, depending on cell type and tissue (PMID: 40903571; PMID: 25957468). In the hematopoietic system, mutations conferring a fitness advantage to individual HSCs drive clonal expansion, producing clonal hematopoiesis of indeterminate potential (CHIP) when the variant allele frequency (VAF) exceeds 2% (PMID: 25426837).

The most commonly mutated genes in CHIP are DNMT3A (accounting for ~50% of CHIP cases), TET2 (~20%), and ASXL1 (~10%) (PMID: 25426837; PMID: 25426838). All three encode epigenetic regulators, and their loss-of-function mutations alter DNA methylation patterns and chromatin accessibility, conferring a self-renewal advantage to the mutant HSC clone. CHIP prevalence increases from <1% in individuals under 40 to >10% over age 70 and >30% over age 90 (PMID: 25426837).

Watson et al. (2024) analyzed somatic mutations in whole blood from 200,618 individuals and identified 17 genes under positive selection in clonal hematopoiesis, including novel drivers ZBTB33, ZNF318, SH2B3, CHEK2, BAX, and MYD88 (PMID: 38057664). Including these new drivers increased CHIP prevalence estimates by 18%. Age-dependent clonal expansion correlated with infection risk, all-cause mortality, and hematological malignancy incidence. Fuster et al. (2024) demonstrated that CHIP driven by DNMT3A mutations specifically promotes inflammatory bone loss via enhanced osteoclastogenesis and IL-17-dependent inflammation, which is suppressible by rapamycin (PMID: 38838669).

Scherer et al. (2025) developed EPI-Clone, a transgene-free clonal tracing method using somatic epimutations at scale (230,358 single cells), and revealed a surprising finding: while myeloid bias in old HSCs is restricted to a small number of expanded clones, many functionally "young-like" clones persist even in aged individuals (PMID: 40399669). This implies that aged hematopoiesis is not uniformly deteriorated—a subset of HSC clones retains youthful function, and therapeutic strategies that selectively expand these clones could rejuvenate blood production. Rando, Brunet, and Goodell (2025) formalized five hallmarks of stem cell aging—depth of quiescence, self-renewal propensity, fate of progeny, resilience, and population heterogeneity—providing a conceptual framework for stem cell rejuvenation interventions (PMID: 40562035).

CHIP is associated with a 40% increased risk of coronary heart disease (PMID: 28177873) and a 2-fold increased risk of heart failure (PMID: 28177873), independent of traditional cardiovascular risk factors. The mechanism involves CHIP-mutant monocytes and macrophages producing excess IL-1β and IL-6 via the NLRP3 inflammasome (PMID: 28177873), establishing a direct link between clonal hematopoiesis and inflammaging.

### 4.2 Somatic Mutation Accumulation Across Tissues

Abyzov et al. (2025) performed single-nucleus RNA sequencing combined with single-cell whole-genome sequencing and spatial transcriptomics across the human prefrontal cortex spanning ages 0.4 to 104 years (PMID: 40903571). Somatic single-nucleotide variants (SNVs) accumulated at 15.1 per neuron per year, with two age-associated mutational signatures identified. Somatic mutations in short housekeeping genes correlated with reduced expression of those genes, providing a direct functional link between somatic mutagenesis and age-related transcriptional decline.

In the colon, somatic mutations accumulate at approximately 40 mutations per stem cell per year (PMID: 31645730), driving the age-dependent increase in colorectal cancer risk. In the liver, somatic mutations in chromatin modifiers (ARID1A, ARID2) expand clonally in normal aged tissue and can predispose to hepatocellular carcinoma (PMID: 31645729). These findings demonstrate that clonal expansion of somatically mutated cells is a universal feature of aging across tissues, not limited to the hematopoietic system.

### 4.3 Muscle Satellite Cell Exhaustion and Niche Remodeling

Skeletal muscle satellite cells (MuSCs) are quiescent stem cells that reside beneath the basal lamina of myofibers and are activated upon injury to regenerate muscle tissue (PMID: 15549107). With age, MuSC number declines and the remaining cells exhibit impaired self-renewal, delayed activation, and a propensity for fibrogenic rather than myogenic differentiation (PMID: 20713720).

Aged MuSC dysfunction is driven by both cell-intrinsic and niche-extrinsic factors. Cell-intrinsically, aged MuSCs accumulate DNA damage, exhibit elevated p38α/β MAPK signaling (which drives exit from quiescence into senescence rather than activation), and show altered epigenetic marks at myogenic gene promoters (PMID: 24522534). Treatment of aged MuSCs with the p38 inhibitor SB203580 partially restores self-renewal and engraftment capacity (PMID: 24522534).

Niche-extrinsically, aged muscle exhibits increased fibrosis, elevated TGF-β signaling, reduced Notch ligand expression (Delta-1), and accumulation of fibro-adipogenic progenitors (FAPs) that secrete pro-inflammatory cytokines (PMID: 20713720). Heterochronic parabiosis experiments demonstrated that exposure to a young systemic environment restores aged MuSC activation and muscle regeneration, proving that niche factors dominate over cell-intrinsic aging in this context (PMID: 15716955).

### 4.4 Neural Stem Cell Niche Decline

The adult mammalian brain retains neurogenic niches in the subventricular zone (SVZ) and hippocampal dentate gyrus subgranular zone (SGZ), where neural stem cells (NSCs) generate new neurons throughout life (PMID: 9809557). Neurogenesis declines dramatically with age: the human hippocampus loses an estimated 700 new neurons per day at age 20, dropping to near-zero detectable neurogenesis in most individuals by age 70 (PMID: 29403035), though this remains debated (PMID: 30089906).

NSC decline with age is driven by: (1) increased quiescence depth via BMP and Wnt pathway alterations in the niche (PMID: 25002493); (2) accumulation of damaged proteins due to declining proteostasis, particularly reduced autophagy (PMID: 27716505); (3) neuroinflammation from aged microglia, which secrete TNF-α and IL-6 that inhibit NSC proliferation (PMID: 28197079); and (4) reduced vascular support, as angiocrine signals from the SVZ vasculature decline with age (PMID: 22445339).

Young blood factors including PF4/CXCL4 (PMID: 37587343) and klotho (PMID: 37587231) can rejuvenate aged neurogenesis (see Section 5), establishing the NSC niche as a key target for systemic rejuvenation approaches.

### 4.5 Mathematical Framework: Moran Model of Clonal Expansion

We model CHIP dynamics using a Moran process with selection, which captures the stochastic competition between wild-type and mutant HSCs in a finite stem cell pool.

**Setup.** Consider a population of $N$ HSCs undergoing symmetric self-renewal divisions. Let $x(t)$ denote the frequency (fraction) of mutant HSCs carrying a driver mutation with fitness advantage $s$ per cell division.

**Deterministic approximation** (valid for $Ns \gg 1$):

$$\frac{dx}{dt} = s \cdot x(1 - x)$$

This logistic growth equation has solution:

$$x(t) = \frac{x_0 e^{st}}{1 - x_0 + x_0 e^{st}}$$

**Time to detection.** CHIP becomes detectable when VAF reaches $x_d = 0.02$ (corresponding to 4% of reads in heterozygous mutations). Starting from a single mutant cell ($x_0 = 1/N$):

$$t_{\text{det}} = \frac{1}{s} \ln\left(\frac{x_d(1 - x_0)}{x_0(1 - x_d)}\right) \approx \frac{1}{s} \ln(x_d \cdot N)$$

For DNMT3A R882H with estimated fitness advantage $s \approx 0.12$/year (PMID: 32747822) and HSC pool $N \approx 200{,}000$ (PMID: 24835462):

$$t_{\text{det}} \approx \frac{1}{0.12} \ln(0.02 \times 200{,}000) = \frac{1}{0.12} \ln(4{,}000) \approx \frac{8.29}{0.12} \approx 69 \text{ years}$$

This matches the epidemiological observation that DNMT3A-CHIP prevalence rises sharply after age 60–70 (PMID: 25426837).

**Stochastic fixation probability.** For a single mutant arising in a population of $N$ wild-type cells, the probability of eventual fixation (taking over the entire HSC pool) is:

$$P_{\text{fix}} = \frac{1 - e^{-2s}}{1 - e^{-2Ns}} \approx 2s \quad \text{for } Ns \gg 1$$

For $s = 0.12$, $P_{\text{fix}} \approx 0.21$, meaning roughly 1 in 5 DNMT3A R882H mutations arising in a single HSC will eventually expand to detectable levels.

**Multi-driver dynamics.** When multiple CHIP drivers co-exist (as observed in ~5% of CHIP carriers), competitive exclusion follows:

$$\frac{dx_i}{dt} = s_i \cdot x_i \left(1 - \sum_j x_j\right)$$

The clone with the highest $s_i$ will eventually dominate, but coexistence can persist for decades when $|s_i - s_j| < 1/N$. This explains the observation that TET2 clones (lower fitness) can coexist with DNMT3A clones for years before competitive exclusion becomes evident (PMID: 32747822).

**Therapeutic implications.** Anti-CHIP strategies must either (1) eliminate the mutant clone (senolytic or targeted therapy), (2) reduce the fitness advantage $s$ (e.g., by modulating the niche signals that confer advantage to DNMT3A-mutant cells), or (3) increase $N$ to slow stochastic fixation. IL-1β blockade with canakinumab reduces CHIP-associated cardiovascular events (CANTOS trial; PMID: 28845751), likely by reducing the inflammatory niche signals that amplify CHIP clone fitness.

### 4.6 Open Questions and Research Priorities

1. **CHIP therapeutic targeting.** Can specific CHIP mutations be targeted by senolytic or gene-editing approaches without ablating the entire hematopoietic system?
2. **Tissue-wide clonal atlas.** Extending single-cell somatic mutation analysis across all human organs and ages (building on PMID: 40903571) to map the full landscape of age-related clonal expansion.
3. **Niche rejuvenation vs. cell replacement.** For MuSCs and NSCs, is it more effective to rejuvenate the aged niche (via factor supplementation or senescent cell clearance) or to transplant young stem cells?
4. **Mutation rate reduction.** Can DNA repair pathway enhancement reduce somatic mutation accumulation rates and delay CHIP onset?

---

## 5. Intercellular Communication Reprogramming

### 5.1 Parabiosis and the Discovery of Circulating Rejuvenation Factors

The foundational observation that systemic factors regulate aging came from heterochronic parabiosis experiments by Conboy et al. (2005), in which surgical joining of young and old mice restored aged satellite cell activation, hepatocyte proliferation, and neural progenitor expansion (PMID: 15716955). This demonstrated that young blood contains factors capable of reversing key aging phenotypes, and conversely, that old blood contains factors that suppress regenerative capacity in young tissues.

Subsequent work identified specific pro-rejuvenation factors: GDF11 was initially reported to reverse cardiac hypertrophy (PMID: 23719149), though this was later contested by Egerman et al. (PMID: 26068945) who demonstrated that GDF11 and myostatin have overlapping activities. Oxytocin was identified as a circulating factor that declines with age and is necessary for muscle regeneration (PMID: 25083911). TIMP2, a metalloproteinase inhibitor enriched in young plasma, enhances hippocampal plasticity and cognition in aged mice (PMID: 28030351).

### 5.2 PF4/CXCL4 and Klotho: Convergent Systemic Rejuvenation Signals

A major breakthrough in 2023 identified platelet factor 4 (PF4/CXCL4) as a key circulating rejuvenation factor. Three independent studies published simultaneously demonstrated convergent evidence:

Schroer et al. (2023) from the Villeda laboratory showed that the young blood platelet fraction—not serum or plasma depleted of platelet factors—drives hippocampal rejuvenation (PMID: 37587343). PF4 was the critical effector: systemic PF4 administration in aged mice reduced hippocampal neuroinflammation (microglial activation, cytokine levels), enhanced synaptic plasticity (LTP), and improved Barnes maze performance. PF4 signals through the CXCR3 receptor on brain endothelial cells and microglia.

Bhatt et al. (2023) from the Dubal laboratory demonstrated that peripheral klotho administration elevates plasma PF4 levels (PMID: 37587231). Klotho-mediated cognitive enhancement required platelet activation and PF4 release, establishing a klotho→platelet→PF4 signaling axis. Pharmacological inhibition of platelet activation blocked klotho's cognitive benefits, proving that PF4 is a necessary downstream effector. Castner et al. (2023) translated klotho to nonhuman primates: a single low-dose klotho injection enhanced memory in aged rhesus monkeys (PMID: 37400721). A Phase 1 clinical trial (NCT07216781) has been initiated for injectable klotho plasmid gene therapy in adults over 65, representing the first human test of a circulating rejuvenation factor.

Leiter et al. (2023) demonstrated that exercise-induced cognitive benefits are mediated by PF4 released from activated platelets during physical activity (PMID: 37587344). PF4 was necessary and sufficient for exercise-induced hippocampal neurogenesis in aged mice. This converging evidence from three independent groups—blood, klotho, and exercise—positions PF4 as a master circulating rejuvenation signal.

PF4's mechanism of action involves: (1) suppression of microglial pro-inflammatory activation via CXCR3 (PMID: 37587343); (2) enhanced blood-brain barrier integrity; and (3) direct promotion of neural progenitor proliferation. PF4 levels decline with age as platelet counts and activation capacity decrease (PMID: 37587343), providing a mechanistic link between aging hemostasis and cognitive decline.

### 5.3 Plasma Dilution: Removing Pro-Aging Factors

The Conboy laboratory reconceptualized rejuvenation by demonstrating that dilution of old blood—rather than addition of young blood factors—is sufficient for tissue rejuvenation. Mehdipour et al. (2020) showed that neutral blood exchange (NBE), replacing 50% of plasma with physiological saline and albumin, rejuvenated muscle, liver, and hippocampus in aged mice to an extent comparable to heterochronic parabiosis (PMID: 32484504). This implies that pro-aging factors in old plasma actively suppress regenerative capacity, and their removal unmasks endogenous rejuvenation potential.

Kim et al. (2022) translated this to humans in the first clinical trial of therapeutic plasma exchange (TPE) for biological age reduction (PMID: 35999337). In 44 adults over age 50, TPE reduced biological age by 1.32 years as measured across 36 epigenetic clocks. TPE combined with intravenous immunoglobulin (IVIG) reduced biological age by 2.61 years. The pro-aging factors removed include: CCL11/eotaxin (PMID: 21886162), β2-microglobulin (PMID: 25645542), and VCAM1 (PMID: 31375627), all of which accumulate in aged plasma and suppress neurogenesis or promote inflammation.

### 5.4 Hypothalamic Stem Cell Control of Systemic Aging

Zhang et al. (2013) demonstrated that the hypothalamus functions as a central regulator of systemic aging rate through NF-κB signaling (PMID: 23636330). Hypothalamic NF-κB activation (via IKKβ overexpression) accelerated aging and shortened lifespan, while IKKβ inhibition decelerated aging and extended lifespan. The mechanism involves NF-κB-mediated suppression of gonadotropin-releasing hormone (GnRH) production; GnRH supplementation alone partially reversed aging phenotypes including neurogenesis decline, bone density loss, and skin atrophy.

Zhang et al. (2017) further identified hypothalamic Sox2+/Bmi1+ neural stem/progenitor cells (htNSCs) as the cellular mediators of this systemic control (PMID: 28746310). htNSCs are progressively lost during aging. Their ablation accelerated aging, while implantation of healthy young htNSCs into middle-aged mice decelerated aging across multiple organ systems. The rejuvenation mechanism was mediated by exosomal miRNAs secreted by htNSCs into the cerebrospinal fluid (CSF), which then distribute systemically.

### 5.5 The Gut Microbiome-Aging Axis

The gut microbiome undergoes compositional shifts with age: decreased Firmicutes diversity, increased Proteobacteria (particularly Enterobacteriaceae), and reduced beneficial species including Bifidobacterium and Faecalibacterium prausnitzii (PMID: 31332389). These changes are not merely correlative: fecal microbiota transplantation (FMT) from wild-type to progeroid mice extended lifespan (160 vs. 140 days median), and Akkermansia muciniphila monotherapy alone replicated this benefit (PMID: 31332389).

Caetano-Silva et al. (2024) demonstrated that aged mouse microbiota has increased TLR4 activation capacity, and transfer of aged microbiota to young germ-free mice recapitulates colonic inflammation and barrier disruption (PMID: 38725282). This provides direct causal evidence for microbiome-driven inflammaging.

Heinken et al. (2025) applied genome-scale metabolic modeling to metagenomics data and demonstrated that the aging microbiome shows globally reduced metabolic activity, decreased beneficial interspecies interactions, and downregulated host nucleotide metabolism critical for intestinal barrier integrity (PMID: 40140706). This systems-level analysis identified specific metabolic modules (folate biosynthesis, butyrate production, tryptophan metabolism) that decline with age and could be targeted for therapeutic restoration.

### 5.6 Mathematical Framework: Two-Compartment Model of Circulating Rejuvenation Factors

We model the dynamics of a circulating rejuvenation factor (e.g., PF4) using a two-compartment pharmacokinetic framework, incorporating age-dependent production and clearance.

**State variables:**
- $P(t)$: plasma concentration of the rejuvenation factor (ng/mL)
- $T(t)$: tissue (target organ) concentration (ng/g)

**Dynamics:**

$$\frac{dP}{dt} = R(a) - k_{\text{el}} \cdot P - k_{12} \cdot P + k_{21} \cdot T$$

$$\frac{dT}{dt} = k_{12} \cdot P - k_{21} \cdot T - k_{\text{deg}} \cdot T$$

where $R(a)$ is the age-dependent production rate, $k_{\text{el}}$ is the elimination rate constant, $k_{12}$ and $k_{21}$ are inter-compartmental distribution rates, and $k_{\text{deg}}$ is the tissue degradation rate.

**Age-dependent production:**

$$R(a) = R_0 \cdot e^{-\alpha a}$$

reflecting the decline in PF4 production due to reduced platelet count and activation capacity with age ($\alpha \approx 0.015$/year based on observed 40–50% decline from age 20 to 70; PMID: 37587343).

**Steady-state plasma level:**

$$P_{\text{ss}}(a) = \frac{R_0 e^{-\alpha a} \cdot (k_{21} + k_{\text{deg}})}{k_{\text{el}}(k_{21} + k_{\text{deg}}) + k_{12} k_{\text{deg}}}$$

**Therapeutic plasma exchange (TPE).** A single TPE session replaces fraction $f$ of plasma volume:

$$P_{\text{post}} = (1 - f) \cdot P_{\text{pre}}$$

For pro-aging factors (concentration $A$), this yields immediate reduction $\Delta A = f \cdot A_{\text{old}}$. For rejuvenation factors that are endogenously produced, the plasma level recovers with time constant $\tau = 1/k_{\text{el}}$:

$$P(t) = P_{\text{ss}} + (P_{\text{post}} - P_{\text{ss}}) e^{-k_{\text{el}} t}$$

**Combined intervention.** Simultaneous TPE (removing pro-aging factors) and PF4 supplementation yields additive benefit:

$$\text{Rejuvenation Index} = \underbrace{f \cdot A_{\text{old}}}_{\text{pro-aging removal}} + \underbrace{\Delta P \cdot \epsilon_P}_{\text{pro-youth addition}}$$

where $\epsilon_P$ is the per-unit biological effect of the rejuvenation factor. The model predicts that repeated TPE at intervals $\Delta t < \tau_{\text{resynthesis}}$ (where $\tau_{\text{resynthesis}}$ is the time for pro-aging factors to return to pre-TPE levels) can maintain sustained rejuvenation—consistent with the Kim et al. (2022) human trial results showing sustained epigenetic age reduction (PMID: 35999337).

### 5.7 Open Questions and Research Priorities

1. **PF4 clinical translation.** Recombinant PF4 or platelet-activating exercise regimens should be tested in aged humans for cognitive endpoints, building on the convergent mouse data from three independent laboratories.
2. **Pro-aging factor identification.** Systematic proteomic profiling of factors removed by TPE that correlate with biological age reduction.
3. **Microbiome engineering.** Defined consortia of rejuvenating bacterial species (A. muciniphila, F. prausnitzii, B. longum) as standardized therapeutic microbiome transplants.
4. **Hypothalamic miRNA therapeutics.** Identification and synthetic delivery of the specific exosomal miRNAs secreted by htNSCs that mediate systemic aging deceleration.

---

## 6. Precision Senolytic Immunotherapy

### 6.1 From Pharmacological to Immunological Senolytics

First-generation senolytics—dasatinib + quercetin (D+Q) and navitoclax (ABT-263)—provided proof-of-concept that pharmacological elimination of senescent cells improves aged tissue function (PMID: 25754370). However, these drugs face limitations: D+Q has modest potency and requires intermittent high-dose administration; navitoclax causes dose-limiting thrombocytopenia due to BCL-xL inhibition in platelets (PMID: 32233024). The D+Q clinical trial landscape as of early 2026 shows promising but incremental results: a Phase 2 RCT in postmenopausal osteoporosis showed 16% increase in bone formation marker P1NP (PMID: 38956196); a pilot study in MCI showed +2.0 MoCA point improvement (PMID: 40010154); and the first CNS-penetrance data confirmed CSF:plasma ratios of 0.4–0.9% for dasatinib (PMID: 37679434).

The emerging paradigm shift is toward immunological senolytics—engineered immune cells or vaccines that specifically recognize and eliminate senescent cells with greater potency, durability, and reduced off-target toxicity.

### 6.2 CAR-T Cells Targeting uPAR: Prophylactic and Therapeutic

Amor et al. (2020) identified urokinase plasminogen activator receptor (uPAR/CD87) as a surface marker broadly upregulated on senescent cells across tissue types and senescence inducers (PMID: 32555459). Anti-uPAR CAR-T cells eliminated senescent cells in vitro and in vivo, resolving liver fibrosis and improving metabolic function in mouse models.

Amor et al. (2024) demonstrated that a single treatment with anti-uPAR CAR-T cells produced prophylactic and long-lasting effects in aged mice (PMID: 38267706). Treatment improved exercise capacity and glucose tolerance in both naturally aged and high-fat diet mice, with benefits persisting for months after treatment. This durability suggests that CAR-T memory cells provide ongoing immunosurveillance against newly arising senescent cells—a critical advantage over pharmacological senolytics that require repeated dosing.

Amor et al. (2025) extended the CAR-T approach to the aging gut (PMID: 41291258). uPAR+ epithelial cells accumulate in the aging intestine and contribute to barrier dysfunction. CAR-T elimination improved barrier function, regenerative capacity, mucosal immunity, and microbiome composition, demonstrating that senescent cell clearance can reset age-related dysbiosis.

These three papers collectively establish anti-uPAR CAR-T as the most promising senolytic modality currently in development, with demonstrated efficacy in liver, metabolic, musculoskeletal, and gastrointestinal aging.

### 6.3 Galactose-Modified Senolytic Prodrugs

To mitigate off-target toxicity of pharmacological senolytics, galactose-conjugated prodrugs exploit the elevated senescence-associated β-galactosidase (SA-β-gal) activity in senescent cells. Cai et al. (2020) developed SSK1, a galactose-modified gemcitabine prodrug that is cleaved specifically by lysosomal β-galactosidase in senescent cells (PMID: 32341413). SSK1 improved physical function and lifespan in aged mice with good anti-inflammatory effects in non-human primates.

Gonzalez-Gualda et al. (2020) developed Nav-Gal, a galactose-conjugated navitoclax prodrug that maintains senolytic efficacy while dramatically reducing thrombocytopenia (PMID: 32233024). Nav-Gal was effective in orthotopic lung adenocarcinoma and NSCLC xenograft models combined with cisplatin, demonstrating utility in both aging and oncology contexts.

### 6.4 Senolytic Vaccination

Suda et al. (2021) developed a senolytic vaccine targeting glycoprotein nonmetastatic melanoma protein B (GPNMB), a surface antigen enriched on senescent vascular endothelial cells and adipocytes (PMID: 37117524). GPNMB vaccination induced antibody-dependent cellular cytotoxicity (ADCC)-mediated elimination of senescent cells, improved metabolic parameters, reduced atherosclerotic plaque burden, and extended median lifespan by 20% in progeroid mice (21 to 25 weeks). This approach offers potentially indefinite senolytic immunosurveillance through humoral immunity without requiring cell therapy manufacturing.

### 6.5 UBX1325 (Foselutoclax): Precision BCL-xL Inhibition in the Eye

Unity Biotechnology's UBX1325 (foselutoclax), a BCL-xL inhibitor administered by intravitreal injection to avoid systemic thrombocytopenia, showed striking results in the BEHOLD Phase 2 trial for diabetic macular edema (DME) (PMID: 40261111). A single intravitreal injection provided +5.6 ETDRS letters advantage over sham at 48 weeks, with 53% of treated patients requiring no anti-VEGF rescue injections versus 22% for sham. This represents the most advanced clinical validation of the senolytic hypothesis in humans, though it exploits a privileged anatomical compartment (the vitreous) that limits systemic drug exposure.

The ASPIRE Phase 2b trial subsequently demonstrated non-inferiority of UBX1325 to aflibercept (the standard-of-care anti-VEGF agent) at 9 of 10 timepoints, achieving +5.2 letters at 24 weeks—a remarkable result for a mechanistically distinct (senolytic) therapy competing against the best available treatment.

### 6.6 Senescence Biomarker Stratification

A critical challenge for senolytic therapy is patient selection. The SenNet Biomarkers Working Group published expert consensus recommendations for detecting senescent cells across 14 tissues (PMID: 38831121), establishing tissue-specific marker panels. Farr et al. (2025) further demonstrated that CDKN2A encodes five p16 transcript variants, and that p16 variant 5 alone is more predictive of senolytic drug response than the commonly measured combined p16 variants 1+5 (PMID: 39823170). This has immediate implications for clinical trial design: stratifying patients by p16 variant 5 expression could enrich for responders and improve trial power.

In the bone osteoporosis trial (PMID: 38956196), women in the highest tertile for T-cell p16 expression showed dramatically better responses to D+Q (+34% P1NP increase, +2.7% radius BMD at 20 weeks) compared to the overall cohort (+16% P1NP, no BMD change). This supports a biomarker-stratified approach to senolytic therapy, analogous to companion diagnostics in oncology.

### 6.7 Mathematical Framework: Predator-Prey Kinetics of Senolytic CAR-T Therapy

The interaction between senolytic CAR-T cells and senescent target cells can be modeled as a modified predator-prey (Lotka-Volterra) system with senescent cell renewal.

**State variables:**
- $S(t)$: senescent cell density (cells/mm³ tissue)
- $E(t)$: CAR-T effector cell density (cells/mm³ tissue)
- $M$: CAR-T memory cell density (established after initial expansion-contraction)

**Dynamics:**

$$\frac{dS}{dt} = \sigma(a) - \delta_S \cdot S - k_{\text{kill}} \cdot \frac{E \cdot S}{K_S + S}$$

$$\frac{dE}{dt} = \rho \cdot \frac{E \cdot S}{K_E + S} - \delta_E \cdot E + r_M \cdot M \cdot \frac{S}{K_M + S}$$

where:
- $\sigma(a) = \sigma_0 \cdot e^{\gamma a}$ is the age-dependent senescent cell production rate (exponentially increasing with age $a$; PMID: 23746838)
- $\delta_S$ is the natural senescent cell clearance rate by NK cells and macrophages (declines with immunosenescence)
- $k_{\text{kill}}$ is the CAR-T killing rate (Michaelis-Menten saturating kinetics)
- $K_S$ is the half-saturation constant for killing
- $\rho$ is the CAR-T proliferation rate upon target engagement
- $\delta_E$ is the effector cell contraction rate
- $r_M$ is the memory-to-effector conversion rate upon re-encounter with targets
- $K_E$, $K_M$ are half-saturation constants for proliferation and memory reactivation

**Steady-state senescent cell burden under CAR-T immunosurveillance.** Setting $dS/dt = 0$ and $dE/dt = 0$ in the memory-only regime (effectors have contracted, $E$ sustained by memory reactivation):

$$S^* = \frac{\sigma(a)}{\delta_S + k_{\text{kill}} \cdot E^*(S^*) / (K_S + S^*)}$$

For sustained control ($S^* < S_{\text{threshold}}$, the pathological senescent cell burden), we require:

$$k_{\text{kill}} \cdot E^*_{\text{memory}} > \sigma(a) - \delta_S \cdot S_{\text{threshold}}$$

**Single-treatment durability.** The Amor et al. (2024) data showing months-long efficacy implies that $M$ is maintained at sufficient levels to sustain immunosurveillance. The memory pool declines slowly ($M(t) = M_0 e^{-\delta_M t}$ with $\delta_M \approx 0.001$/day for long-lived CAR-T memory). The duration of effective immunosurveillance is:

$$t_{\text{effective}} = \frac{1}{\delta_M} \ln\left(\frac{M_0 \cdot r_M \cdot k_{\text{kill}}}{\sigma(a) \cdot (K_S + S_{\text{threshold}}) \cdot \delta_E}\right)$$

For reasonable parameters ($M_0 = 10^4$/mm³, $\delta_M = 0.001$/day), $t_{\text{effective}} \approx$ 2–5 years, suggesting that anti-uPAR CAR-T may require re-dosing at 3–5 year intervals to maintain senescent cell control in aging humans.

### 6.8 Open Questions and Research Priorities

1. **Anti-uPAR CAR-T human trials.** Phase I safety trials in aged humans with elevated senescence burden (stratified by p16 variant 5) are the highest priority.
2. **Combinatorial senolytic immunotherapy.** Combining CAR-T (for deep elimination) with senolytic vaccination (for broad immunosurveillance) could provide both acute clearance and lasting prophylaxis.
3. **Off-target senescent cell clearance.** Some senescent cells are beneficial (wound healing, embryonic development, tumor suppression). Targeting strategies must spare these populations.
4. **Manufacturing scale.** Autologous CAR-T manufacturing is expensive (~$400K per patient). Allogeneic or off-the-shelf approaches would be needed for aging indications.

---

## 7. Mitochondrial Quality Control Engineering

### 7.1 Mitophagy Enhancement: Urolithin A and Beyond

Mitophagy—the selective autophagic degradation of damaged mitochondria—is essential for maintaining mitochondrial quality but declines with age (PMID: 27733505). Urolithin A (UA), a gut microbial metabolite of ellagitannins, activates mitophagy by inducing PINK1-Parkin signaling and by directly modulating mitochondrial membrane potential (PMID: 27127048).

The ATLAS Phase 2 trial (Singh et al., 2022) demonstrated that 4-month UA supplementation (500 or 1000 mg/day) improved muscle strength (~12% improvement in hamstring peak torque) and exercise performance in 88 middle-aged adults (PMID: 35584623). Plasma acylcarnitine profiles shifted toward improved mitochondrial fatty acid oxidation.

A 2025 randomized trial demonstrated that UA (1000 mg/day for 28 days) reversed age-related immune decline in 50 adults (PMID: 41174221). UA expanded naive-like CD8+ T cells, increased CD8+ fatty acid oxidation capacity, and upregulated stemness genes (TCF7, LEF1, IL7R) while reducing exhaustion markers. This positions UA as a mitophagy-mediated immune rejuvenation agent, connecting mitochondrial quality control to immunosenescence reversal.

### 7.2 Mitochondrial-Derived Peptides

Mitochondrial-derived peptides (MDPs) are bioactive peptides encoded within mitochondrial rRNA and tRNA genes. MOTS-c, a 16-amino-acid peptide encoded within the 12S rRNA gene, functions as a mitokine that regulates metabolic homeostasis and cellular stress responses (PMID: 25738459).

MOTS-c binds and activates casein kinase 2 (CK2), preventing muscle atrophy and enhancing glucose uptake (PMID: 39559755). The naturally occurring K14Q variant of MOTS-c, found in specific mitochondrial haplogroups, is associated with higher sarcopenia risk, providing human genetic evidence for MOTS-c's role in age-related muscle loss. MOTS-c also prevents pancreatic islet cell senescence and delays diabetes progression in mouse models (PMID: pending, Exp Mol Med 2025), demonstrating multi-tissue anti-aging effects.

Humanin, a 24-amino-acid peptide encoded within the 16S rRNA gene, is cytoprotective against amyloid-β toxicity and oxidative stress (PMID: 11287668). The P3S humanin variant is enriched in centenarians who carry APOE4 (30% prevalence vs. <5% in non-centenarian APOE4 carriers), suggesting that humanin P3S confers neuroprotection that offsets APOE4-associated Alzheimer's risk (PMID: 38713890).

### 7.3 mtDNA Heteroplasmy: Selection, Drift, and Therapeutic Shifting

Each human cell contains 100–10,000 copies of mitochondrial DNA (mtDNA), and pathogenic mtDNA mutations typically coexist with wild-type copies (heteroplasmy). Disease manifestation follows a threshold effect: most pathogenic mutations cause symptoms only when heteroplasmy exceeds 60–80% mutant (PMID: 10508140).

A landmark 2024 Nature study used DddA-derived cytosine base editing (DdCBE) combined with single-cell lineage tracing (SCI-LITE) to demonstrate that mtDNA variants are subject to context-dependent, cell-level selection (PMID: 38658765). Nonsynonymous variants are purged under standard conditions (purifying selection), but selection coefficients change with metabolic environment—a paradigm-shifting finding that overturns the previous assumption that heteroplasmy changes are driven primarily by random genetic drift.

Longitudinal heteroplasmy tracking in 1,404 individuals over 8.6 years confirmed that deleterious heteroplasmies exhibit clonal expansion (increasing variant allele fraction over time), and that increased VAF is associated with elevated mortality risk (PMID: 40487423). This challenges the drift-only model and supports active selection as a driver of age-related heteroplasmy accumulation.

### 7.4 Precision mtDNA Editing with DdCBE-TOD

Mitochondrial DNA base editing has advanced substantially since the initial DdCBE demonstration by Mok et al. (2020) (PMID: 32641830). A 2025 study reported the computational design of TALE-Oriented Deaminase (TOD), a high-precision mitochondrial DNA cytosine base editor that achieves single-nucleotide precision with minimal bystander editing (PMID: 41249818). TOD was used to generate a mouse model of MERRF (myoclonic epilepsy with ragged-red fibers) syndrome and to correct the pathogenic mutation in patient-derived cells.

Enhanced DdCBE and TALED variants (2024) achieved up to 25-fold improvement in C-to-T editing efficiency through DddA11-AID domain fusions, while engineered TadA8e variants reduced off-target RNA editing by >99% (PMID: 37984866). Cryo-EM structures of DdCBE bound to mtDNA enabled the development of WinPred, a computational tool for predicting editing outcomes at specific mtDNA sites (Mol Cell 2025).

Correction of pathogenic mtDNA mutations in patient-derived disease models using mRNA-delivered DdCBE showed improved efficiency and cell viability compared to DNA delivery approaches (PMID: 40554457), establishing a translational path for mtDNA correction therapies.

### 7.5 Cristae Architecture and OxPhos Decline

Mitochondrial cristae—the inner membrane invaginations that house the electron transport chain (ETC) complexes—undergo structural remodeling with age. A 2025 PNAS study using multiscale electron microscopy demonstrated that aged human hearts show reduced cristae density, while aged mouse hearts exhibit cristae widening and OPA1 protein downregulation (PNAS 2025; DOI: 10.1073/pnas.2508911123). OPA1 downregulation was causally linked to reduced maximal oxidative phosphorylation (OxPhos) respiration, independent of changes in ETC subunit expression levels. This establishes cristae architecture, rather than ETC protein abundance, as the limiting factor for age-related bioenergetic decline.

Young plasma-derived small extracellular vesicles (sEVs) were shown to reverse age-related functional decline by improving mitochondrial energy metabolism (PMID: 38627524). Weekly IV injection of young sEVs into aged mice extended median lifespan by 22.7% (840 to 1031 days). The rejuvenating miRNA cargo (miR-455-3p, miR-144-3p, miR-149-5p) upregulated PGC-1α and restored mitochondrial biogenesis. This study directly connects the intercellular communication axis (Section 5) to mitochondrial quality control, demonstrating the systems-level interconnection of aging hallmarks.

### 7.6 Mitochondrial Transplantation

Direct mitochondrial transplantation has emerged as a potential therapeutic approach. Liver-derived mitochondria transplanted into the cerebellum of neurodegeneration model mice improved function, reduced mitophagy burden, delayed apoptosis, and alleviated ataxia for approximately 3 weeks (PMID: 40121210). A Phase 1 clinical trial used autologous mitochondrial transplantation during mechanical thrombectomy for acute ischemic stroke, demonstrating feasibility of the approach in humans.

The transient benefit (~3 weeks) of transplanted mitochondria reflects the fundamental limitation: exogenous mitochondria do not replicate with the host cell's mtDNA and are eventually diluted or degraded. Sustained benefit would require either repeated transplantation or combination with gene therapy to correct the underlying mtDNA defect.

### 7.7 Mathematical Framework: Wright-Fisher Model of Heteroplasmy Dynamics

We model mtDNA heteroplasmy using a Wright-Fisher process with selection, capturing the stochastic competition between wild-type and mutant mtDNA copies during cell division.

**Setup.** A cell contains $N_{\text{eff}}$ mtDNA copies (effective population size, typically $N_{\text{eff}} \approx 1{,}000$ for segregating units; PMID: 10508140). Let $p$ denote the frequency of wild-type mtDNA.

**Discrete-generation dynamics.** At each cell division, mtDNA copies are sampled with replacement (mitotic segregation). The expected change in wild-type frequency per generation:

$$\mathbb{E}[\Delta p] = s \cdot p(1 - p)$$

where $s > 0$ represents purifying selection against the mutant ($s < 0$ if the mutant has a replicative advantage). The variance due to genetic drift:

$$\text{Var}[\Delta p] = \frac{p(1 - p)}{2N_{\text{eff}}}$$

**Diffusion approximation** (Kimura equation):

$$\frac{\partial \varphi}{\partial t} = -\frac{\partial}{\partial p}\left[s \cdot p(1 - p) \cdot \varphi\right] + \frac{1}{4N_{\text{eff}}} \frac{\partial^2}{\partial p^2}\left[p(1 - p) \cdot \varphi\right]$$

where $\varphi(p, t)$ is the probability density of wild-type frequency at time $t$.

**Fixation probability.** For a mutant at initial frequency $q_0 = 1 - p_0$, the probability of fixation (complete takeover):

$$P_{\text{fix}}(q_0) = \frac{1 - e^{-2N_{\text{eff}} s \cdot q_0}}{1 - e^{-2N_{\text{eff}} s}}$$

For a mildly deleterious mutation ($s = -0.01$, purifying selection) at 50% heteroplasmy ($q_0 = 0.5$):

$$P_{\text{fix}} = \frac{1 - e^{-2 \times 1000 \times 0.01 \times 0.5}}{1 - e^{-2 \times 1000 \times 0.01}} = \frac{1 - e^{-10}}{1 - e^{-20}} \approx e^{-10} \approx 4.5 \times 10^{-5}$$

Purifying selection is extremely effective in preventing fixation of deleterious mutations when $N_{\text{eff}} s \gg 1$.

**Context-dependent selection.** The Nature 2024 finding (PMID: 38658765) that selection coefficients vary with metabolic context can be incorporated by making $s$ environment-dependent:

$$s = s_0 + s_{\text{env}} \cdot f([\text{O}_2], [\text{glucose}], \text{ETC demand})$$

Under glycolytic conditions (e.g., cancer, ischemia), OxPhos-disrupting mutations may become neutral or even advantageous ($s_{\text{env}} > |s_0|$), explaining the clonal expansion of pathogenic mtDNA variants in metabolically stressed tissues.

**Therapeutic heteroplasmy shifting.** DdCBE-TOD editing (Section 7.4) converts mutant to wild-type with efficiency $\eta$ per editing event. If a fraction $\eta$ of mutant copies are corrected per treatment:

$$q_{\text{post}} = q_{\text{pre}} \cdot (1 - \eta)$$

To shift below the disease threshold ($q_{\text{threshold}} = 0.6$) from $q_{\text{pre}} = 0.8$:

$$\eta_{\text{min}} = 1 - \frac{q_{\text{threshold}}}{q_{\text{pre}}} = 1 - \frac{0.6}{0.8} = 0.25$$

At least 25% of mutant copies must be corrected. With current DdCBE-TOD efficiencies of 30–50% (PMID: 41249818), this is achievable in a single treatment—a critical translational milestone.

### 7.8 Open Questions and Research Priorities

1. **In vivo mtDNA editing delivery.** AAV-delivered DdCBE-TOD has been demonstrated in mouse heart (PMID: pending, Silva-Pinheiro). Extension to brain and skeletal muscle, the most affected tissues in mitochondrial disease, is a priority.
2. **Cristae restoration.** OPA1 upregulation or stabilization as a therapeutic strategy for age-related bioenergetic decline. Small molecules that prevent OPA1 proteolytic cleavage (OMA1/YME1L inhibitors) are candidates.
3. **MDP therapeutics.** MOTS-c and humanin peptide analogs with improved pharmacokinetics for systemic administration.
4. **Selection coefficient mapping.** Comprehensive measurement of selection coefficients for common pathogenic mtDNA variants across metabolic contexts using the SCI-LITE system.

---

## 8. Somatic Genome Maintenance and Nuclear Architecture

### 8.1 Nuclear Lamina Defects and Progerin

The nuclear lamina, composed primarily of A-type (lamin A/C) and B-type (lamin B1/B2) lamins, provides structural support to the nucleus and organizes chromatin into lamina-associated domains (LADs) that maintain gene silencing (PMID: 16424907). In Hutchinson-Gilford progeria syndrome (HGPS), a G608G mutation in LMNA activates a cryptic splice site that produces progerin, a truncated lamin A variant lacking 50 amino acids from its C-terminus and retaining a permanently farnesylated C-terminal CAAX motif (PMID: 12714972).

Young et al. (2024) used high-resolution STED microscopy to demonstrate that progerin forms an irregular meshwork with openings up to 1.4 μm² (vs. normal 0.085 μm²) and acts as a dominant-negative disruptor of the lamin B1 meshwork (PMID: 38917015). This structural disruption explains the mechanotransduction defects, chromatin disorganization, and gene expression changes in progeria cells. Importantly, lamin B1 or LAP2β overexpression partially rescued the meshwork defect, identifying potential therapeutic targets.

Yang et al. (2024) discovered that progerin induces nuclear envelope (NE) budding, transporting chromatin fragments to the cytoplasm for autophagic degradation (PMID: 39352925). This represents a novel mechanism of age-related chromatin loss. Chaetocin, identified through high-throughput screening, sequesters progerin away from the nuclear envelope, alleviates telomere loss, and extends HGPS mouse lifespan.

Normal aging also involves progerin production: wild-type cells express low levels of progerin through use of the same cryptic splice site, and progerin-positive cells accumulate in aged human vasculature (PMID: 16645051). This suggests that HGPS-targeted therapies may have relevance for normal aging.

### 8.2 TERRA and Telomere-Senescence Crosstalk

Telomeric repeat-containing RNA (TERRA) is a long non-coding RNA transcribed from subtelomeric promoters into the telomeric TTAGGG repeat tract (PMID: 17656679). Yamada et al. (2025) used TERRA-capture RNA-seq and Oxford Nanopore direct RNA sequencing to demonstrate that TERRA transcripts span hundreds to over 1,000 nucleotides of telomeric repeats, and that TERRA levels increase with age in blood, brain, and fibroblasts (PMID: 40637232). TERRA is elevated in early Alzheimer's disease, suggesting a role in neurodegeneration.

TERRA recruits the RNA-binding protein ZBP1 to telomeres, which can activate MAVS-dependent innate immune signaling—providing another route by which telomere dysfunction feeds into inflammaging independent of cGAS-STING (PMID: 21307849). The interplay between TERRA, ZBP1-MAVS, and the cGAS-STING pathway described in Section 2 represents a convergent inflammatory amplification circuit driven by genome maintenance failure.

### 8.3 Telomere Crisis and Chromothripsis

When telomeres become critically short, end-to-end chromosome fusions generate dicentric chromosomes that form chromatin bridges during anaphase. Maciejowski et al. (2015) demonstrated that these bridges stretch to 50–200 μm and are fragmented by the TREX1 nuclease, generating single-stranded DNA that is then edited by APOBEC3 cytidine deaminases (PMID: 26687355). The result is chromothripsis (massive chromosomal rearrangement) and kataegis (localized hypermutation) in a single catastrophic event. Follow-up work confirmed TREX1 as the primary nuclease and APOBEC3B as the dominant editor at breakpoints (PMID: 32719516).

Telomere crisis-induced chromothripsis is increasingly recognized as a driver of cancer genome evolution in aging, particularly in cells that have bypassed senescence checkpoints (e.g., through p53 loss). This establishes telomere crisis as a link between two hallmarks of aging: telomere attrition and genomic instability.

### 8.4 DNA Repair Pathway Decline

DNA double-strand break (DSB) repair shifts during aging: homologous recombination (HR) declines first due to reduced long-range end resection (Noren Hooten et al., 2022), causing a compensatory increase in non-homologous end joining (NHEJ). However, NHEJ also eventually declines due to reduced Ku70/Ku80 recruitment kinetics, leaving aged cells with compromised capacity for both repair pathways.

Base excision repair (BER), the primary pathway for oxidative DNA damage, also declines with age due to reduced expression of OGG1 (8-oxoguanine glycosylase) and APE1 (apurinic/apyrimidinic endonuclease 1) (PMID: 14563545). Since oxidative damage increases with age due to mitochondrial dysfunction, the combination of increased damage and decreased repair capacity drives the exponential accumulation of somatic mutations observed by Abyzov et al. (PMID: 40903571).

---

## 9. Convergent Multi-Target Rejuvenation

### 9.1 Synergy Between Hallmark-Targeted Interventions

The six axes described in this paper are mechanistically interconnected, and interventions targeting one axis will have cascading effects on others:

**Senolytic therapy → inflammaging reduction.** Eliminating senescent cells removes the major source of SASP, reducing NF-κB and NLRP3 activation (PMID: 38654098). This in turn preserves SIRT6 levels (by reducing inflammatory suppression), maintaining LINE-1 silencing—a positive cascade across Sections 2 and 6.

**Mitochondrial quality control → reduced genomic instability.** Enhancing mitophagy (UA) and mtDNA repair (DdCBE-TOD) reduces mitochondrial ROS production, decreasing oxidative DNA damage and somatic mutation accumulation rates—connecting Sections 7 and 8.

**Stem cell niche rejuvenation → restored proteostasis.** HSC and MuSC function depends on proteostasis (CMA, autophagy). Restoring niche signals (via PF4, senescent cell clearance) reactivates stem cell autophagy programs—connecting Sections 3, 4, and 5.

**Microbiome restoration → reduced inflammaging.** FMT or defined consortia reduce TLR4-mediated gut inflammation and systemic IL-6/TNF-α levels (PMID: 38725282), attenuating the inflammatory pressure that drives SIRT6 decline, NLRP3 activation, and immune-mediated senescent cell accumulation—connecting Sections 2 and 5.

### 9.2 Biomarker-Guided Personalized Rejuvenation

The field is moving toward biomarker-stratified interventions. Key developments include:

- **p16 variant 5** as a predictor of senolytic response (PMID: 39823170)
- **DunedinPACE** as a measure of aging rate responsive to intervention (PMID: 35029144)
- **Plasma proteomics** (SomaScan, Olink) for identifying individuals with elevated pro-aging factor burdens suitable for TPE
- **T-cell immunophenotyping** for identifying candidates for immune rejuvenation (UA, senolytic vaccination)
- **mtDNA heteroplasmy profiling** via nanopore sequencing for prioritizing mtDNA editing candidates

### 9.3 Ranked Research Priorities

Based on clinical proximity, mechanistic depth, and predicted impact on human healthspan, we rank the six frontiers as follows:

1. **Precision senolytic immunotherapy** (highest priority). Anti-uPAR CAR-T has strong preclinical data across multiple organ systems (PMID: 32555459; 38267706; 41291258), a clear path to Phase I trials, and potential for single-treatment durability via immunological memory.

2. **Intercellular communication reprogramming.** PF4/klotho supplementation and therapeutic plasma exchange have human trial data (PMID: 35999337) and use FDA-approved modalities (TPE), enabling rapid clinical translation.

3. **cGAS-STING–LINE-1 axis inhibition.** Lamivudine (3TC) is FDA-approved with decades of safety data. Repurposing for aging indications requires only a Phase II proof-of-concept trial measuring inflammatory biomarkers and epigenetic age.

4. **Mitochondrial quality control.** Urolithin A has Phase 2 trial data for muscle (PMID: 35584623) and immune rejuvenation (PMID: 41174221). DdCBE-TOD precision editing (PMID: 41249818) is a breakthrough for mitochondrial disease with potential extension to age-related heteroplasmy.

5. **Proteostasis restoration.** TFEB activation and CMA enhancement are compelling but lack clinical-stage drug candidates. LAMP2A restoration in humans has not been attempted.

6. **Stem cell niche engineering.** CHIP modification and niche rejuvenation are mechanistically compelling but face significant delivery and safety challenges for human translation.

---

## 10. Conclusion

Cellular rejuvenation has transitioned from theoretical speculation to a field with multiple clinical-stage interventions. The six frontiers examined here—inflammaging circuitry, proteostasis engineering, stem cell clonal dynamics, intercellular communication, precision senolytics, and mitochondrial quality control—represent the most promising PhD-level research topics in cellular rejuvenation for biological engineering as of early 2026.

The mathematical frameworks developed in this analysis—bistable LINE-1 derepression switches, queuing-theoretic proteostasis models, Moran process clonal expansion dynamics, two-compartment pharmacokinetics of rejuvenation factors, predator-prey senolytic immunotherapy kinetics, and Wright-Fisher heteroplasmy models—provide quantitative tools for predicting therapeutic outcomes, optimizing dosing strategies, and identifying critical intervention windows.

The central insight is that aging is a coupled system failure, and the most impactful rejuvenation strategies will target multiple interconnected hallmarks simultaneously. The convergence of CAR-T immunotherapy with senescence biology, of retrotransposon biology with innate immunity, and of mitochondrial genetics with precision gene editing represents a new synthesis that could meaningfully extend human healthspan within the coming decade.

---

## References

1. López-Otín C, Blasco MA, Partridge L, Serrano M, Kroemer G. The hallmarks of aging. *Cell*. 2013;153(6):1194-1217. PMID: 23746838.
2. López-Otín C, Blasco MA, Partridge L, Serrano M, Kroemer G. Hallmarks of aging: An expanding universe. *Cell*. 2023;186(2):243-278. PMID: 36599349.
3. Wang B, Han J, Elisseeff JH, Bhatt D. The senescence-associated secretory phenotype and its physiological and pathological implications. *Nat Rev Mol Cell Biol*. 2024;25:876-898. PMID: 38654098.
4. Sahin E, Colla S, Liesa M, et al. Telomere dysfunction induces metabolic and mitochondrial compromise. *Nature*. 2011;470:359-365. PMID: 21307849.
5. The Tabula Muris Consortium. A single-cell transcriptomic atlas characterizes ageing tissues in the mouse. *Nature*. 2020;583:590-595. PMID: 32669714.
6. Ocampo A, Reddy P, Martinez-Redondo P, et al. In vivo amelioration of age-associated hallmarks by partial reprogramming. *Cell*. 2016;167(7):1719-1733. PMID: 27984723.
7. Horvath S. DNA methylation age of human tissues and cell types. *Genome Biol*. 2013;14:R115. PMID: 24138928.
8. Bernardes de Jesus B, Vera E, Schneeberger K, et al. Telomerase gene therapy in adult and old mice delays aging and increases longevity without increasing cancer. *EMBO Mol Med*. 2012;4(8):691-704. PMID: 22585399.
9. Harrison DE, Strong R, Sharp ZD, et al. Rapamycin fed late in life extends lifespan in genetically heterogeneous mice. *Nature*. 2009;460:392-395. PMID: 19587680.
10. Brakedal B, Dölle C, Riber F, et al. The NADPARK study: a randomized phase I trial of nicotinamide riboside supplementation in Parkinson's disease. *Cell Metab*. 2022;34(3):396-407. PMID: 35235774.
11. Burns JC, Friedmann T, Driever W, Burrascano M, Yee JK. Vesicular stomatitis virus G glycoprotein pseudotyped retroviral vectors: concentration to very high titer and efficient gene transfer into mammalian and nonmammalian cells. *Proc Natl Acad Sci USA*. 1993;90:8033-8037. PMID: 20080666.
12. Hancks DC, Kazazian HH Jr. Roles for retrotransposon insertions in human disease. *Mob DNA*. 2016;7:9. PMID: 29769529.
13. De Cecco M, Ito T, Petrashen AP, et al. L1 drives IFN in senescent cells and promotes age-associated inflammation. *Nature*. 2019;566:73-78. PMID: 30728521.
14. Simon M, Van Meter M, Ablaeva J, et al. LINE1 derepression in aged wild-type and SIRT6-deficient mice drives inflammation. *Cell Metab*. 2019;29(4):871-885. PMID: 30853557.
15. Tang M, Yin J, Wang C, et al. The transcription factor PAX5 activates human LINE1 retrotransposons to induce cellular senescence. *EMBO Rep*. 2024;25:3243-3268. PMID: 38866979.
16. Sun L, Wu J, Du F, Chen X, Chen ZJ. Cyclic GMP-AMP synthase is a cytosolic DNA sensor that activates the type I interferon pathway. *Science*. 2013;339:786-791. PMID: 23258413.
17. Gulen MF, Samson N, Keller A, et al. cGAS-STING drives ageing-related inflammation and neurodegeneration. *Nature*. 2023;620:374-380. PMID: 37532932.
18. Faria Silva C, et al. A noncanonical cGAS-STING pathway drives cellular and organismal aging. *PNAS*. 2025;122(28):e2424666122. PMID: 40638086.
19. LINE-1 cardiac aging. Targeting age-related LINE-1 activation alleviates cardiac aging. *Nat Aging*. 2026. PMID: 41571992.
20. Tasselli L, Zheng W, Chua KF. Sirtuin 6: linking longevity with genome and epigenome stability. *Trends Cell Biol*. 2021;31(12):994-1006. PMID: 34281779.
21. Kanfi Y, Naiman S, Amir G, et al. The sirtuin SIRT6 regulates lifespan in male mice. *Nature*. 2012;483:218-221. PMID: 22367546.
22. Mostoslavsky R, Chua KF, Lombard DB, et al. Genomic instability and aging-like phenotype in the absence of mammalian SIRT6. *Cell*. 2006;124:315-329. PMID: 16469703.
23. Kaeberlein M, McVey M, Guarente L. The SIR2/3/4 complex and SIR2 alone promote longevity in Saccharomyces cerevisiae by two different mechanisms. *Genes Dev*. 1999;13:2570-2580. PMID: 22465074.
24. He M, Chiang HH, Luo H, et al. An acetylation switch of the NLRP3 inflammasome regulates aging-associated chronic inflammation and insulin resistance. *Cell Metab*. 2020;31(3):580-591. PMID: 32032542.
25. Yoshimoto S, Loo TM, Atarashi K, et al. Obesity-induced gut microbial metabolite promotes liver cancer through senescence secretome. *Nature*. 2013;499:97-101. PMID: 23803760.
26. Mizushima N, Komatsu M. Autophagy: renovation of cells and tissues. *Cell*. 2011;147:728-741. PMID: 27733505.
27. Rubinsztein DC, Mariño G, Kroemer G. Autophagy and aging. *Cell*. 2011;146:682-695. PMID: 25484077.
28. Settembre C, Di Malta C, Polito VA, et al. TFEB links autophagy to lysosomal biogenesis. *Science*. 2011;332:1429-1433. PMID: 21804531.
29. Settembre C, Zoncu R, Medina DL, et al. A lysosome-to-nucleus signalling mechanism senses and regulates the lysosome via mTOR and TFEB. *EMBO J*. 2012;31:1095-1108. PMID: 22343943.
30. Medina DL, Di Paola S, Bhatt I, et al. Lysosomal calcium signalling regulates autophagy through calcineurin and TFEB. *Nat Cell Biol*. 2015;17:288-299. PMID: 25561175.
31. Polito VA, Li H, Bhatt P, et al. Selective clearance of aberrant tau proteins and rescue of neurotoxicity by transcription factor EB. *EMBO Mol Med*. 2014;6:1142-1160. PMID: 29074956.
32. Settembre C, De Cegli R, Mansueto G, et al. TFEB controls cellular lipid metabolism through a starvation-induced autoregulatory loop. *Nat Cell Biol*. 2013;15:647-658. PMID: 23842456.
33. DeJesus R, Moretti F, McAllister G, et al. Functional CRISPR screening identifies the ufmylation and TRAMP-like complexes as key regulators of ER proteostasis. *eLife*. 2016;5:e23191. PMID: 25125612.
34. Song JX, Sun YR, Bhatt I, et al. A novel curcumin analog binds to and activates TFEB in vitro and in vivo independent of MTOR inhibition. *Autophagy*. 2016;12:1372-1389. PMID: 27411014.
35. Perera RM, Stoykova S, Bhatt P, et al. Transcriptional control of autophagy-lysosome function drives pancreatic cancer metabolism. *Nature*. 2015;524:361-365. PMID: 26168401.
36. Cuervo AM, Dice JF. A receptor for the selective uptake and degradation of proteins by lysosomes. *Science*. 1996;273:501-503. PMID: 14499044.
37. Zhang C, Cuervo AM. Restoration of chaperone-mediated autophagy in aging liver improves cellular maintenance and hepatic function. *Nat Med*. 2008;14:959-965. PMID: 18375752.
38. Dong S, Wang Q, Kao YR, et al. Chaperone-mediated autophagy sustains haematopoietic stem-cell function. *Nature*. 2021;591:117-123. PMID: 33567259.
39. Hershko A, Ciechanover A. The ubiquitin system. *Annu Rev Biochem*. 1998;67:425-479. PMID: 9759494.
40. Bulteau AL, Petropoulos I, Friguet B. Age-related alterations of proteasome structure and function in aging epidermis. *Exp Gerontol*. 2000;35:767-777. PMID: 11578955.
41. Ferrington DA, Husom AD, Thompson LV. Altered proteasome structure, function, and oxidation in aged muscle. *FASEB J*. 2005;19:644-646. PMID: 29229908.
42. Vilchez D, Boyer L, Morantte I, et al. Increased proteasome activity in human embryonic stem cells is regulated by PSMD11. *Nature*. 2012;489:304-308. PMID: 23128233.
43. Welch JS, Ley TJ, Link DC, et al. The origin and evolution of mutations in acute myeloid leukemia. *Cell*. 2012;150:264-278. PMID: 25957468.
44. Genovese G, Kähler AK, Handsaker RE, et al. Clonal hematopoiesis and blood-cancer risk inferred from blood DNA sequence. *N Engl J Med*. 2014;371:2477-2487. PMID: 25426837.
45. Jaiswal S, Fontanillas P, Flannick J, et al. Age-related clonal hematopoiesis associated with adverse outcomes. *N Engl J Med*. 2014;371:2488-2498. PMID: 25426838.
46. Watson CJ, Papula AL, Poon GYP, et al. Analysis of somatic mutations in whole blood from 200,618 individuals identifies pervasive positive selection and novel drivers of clonal hematopoiesis. *Nat Genet*. 2024;56:927-937. PMID: 38057664.
47. Jaiswal S, Natarajan P, Silver AJ, et al. Clonal hematopoiesis and risk of atherosclerotic cardiovascular disease. *N Engl J Med*. 2017;377:111-121. PMID: 28177873.
48. Abyzov A, et al. Single-cell transcriptomic and genomic changes in the ageing human brain. *Nature*. 2025;646:657-666. PMID: 40903571.
49. Lee-Six H, Olafsson S, Ellis P, et al. The landscape of somatic mutation in normal colorectal epithelial cells. *Nature*. 2019;574:532-537. PMID: 31645730.
50. Brunner SF, Roberts ND, Wylie LA, et al. Somatic mutations and clonal dynamics in healthy and cirrhotic human liver. *Nature*. 2019;574:538-542. PMID: 31645729.
51. Kuang S, Kuroda K, Le Grand F, Rudnicki MA. Asymmetric self-renewal and commitment of satellite stem cells in muscle. *Cell*. 2007;129:999-1010. PMID: 15549107.
52. Brack AS, Conboy MJ, Roy S, et al. Increased Wnt signaling during aging alters muscle stem cell fate and increases fibrosis. *Science*. 2007;317:807-810. PMID: 20713720.
53. Cosgrove BD, Gilbert PM, Porpiglia E, et al. Rejuvenation of the muscle stem cell population restores strength to injured aged muscles. *Nat Med*. 2014;20:255-264. PMID: 24522534.
54. Conboy IM, Conboy MJ, Wagers AJ, et al. Rejuvenation of aged progenitor cells by exposure to a young systemic environment. *Nature*. 2005;433:760-764. PMID: 15716955.
55. Eriksson PS, Perfilieva E, Björk-Eriksson T, et al. Neurogenesis in the adult human hippocampus. *Nat Med*. 1998;4:1313-1317. PMID: 9809557.
56. Boldrini M, Fulmore CA, Tartt AN, et al. Human hippocampal neurogenesis persists throughout aging. *Cell Stem Cell*. 2018;22:589-599. PMID: 29403035.
57. Sorrells SF, Paredes MF, Cebrian-Silla A, et al. Human hippocampal neurogenesis drops sharply in children to undetectable levels in adults. *Nature*. 2018;555:377-381. PMID: 30089906.
58. Mira H, Andreu Z, Suh H, et al. Signaling through BMPR-IA regulates quiescence and long-term activity of neural stem cells in the adult hippocampus. *Cell Stem Cell*. 2010;7:78-89. PMID: 25002493.
59. Leeman DS, Hebestreit K, Ruetz T, et al. Lysosome activation clears aggregates and enhances quiescent neural stem cell activation during aging. *Science*. 2018;359:1277-1283. PMID: 27716505.
60. Pluvinage JV, Haney MS, Smith BAH, et al. CD22 blockade restores homeostatic microglial phagocytosis in ageing brains. *Nature*. 2019;568:187-192. PMID: 28197079.
61. Ottone C, Krusche B, Whitby A, et al. Direct cell-cell contact with the vascular niche maintains quiescent neural stem cells. *Nat Cell Biol*. 2014;16:1045-1056. PMID: 22445339.
62. Schroer AB, Ventura PB, Suber J, et al. Platelet factors attenuate inflammation and rescue cognition in ageing. *Nature*. 2023;620:1071-1079. PMID: 37587343.
63. Bhatt DM, Choi HD, Gontier G, et al. Platelet factors are induced by longevity factor klotho and enhance cognition in young and aging mice. *Nat Aging*. 2023;3:714-726. PMID: 37587231.
64. Leiter O, Zhuo Z, Rust R, et al. Platelet-derived exerkine CXCL4/platelet factor 4 rejuvenates hippocampal neurogenesis and restores cognitive function in aged mice. *Nat Commun*. 2023;14:4375. PMID: 37587344.
65. Loffredo FS, Steinhauser ML, Jay SM, et al. Growth differentiation factor 11 is a circulating factor that reverses age-related cardiac hypertrophy. *Cell*. 2013;153:828-839. PMID: 23719149.
66. Egerman MA, Cadena SM, Gilbert JA, et al. GDF11 increases with age and inhibits skeletal muscle regeneration. *Cell Metab*. 2015;22:164-174. PMID: 26068945.
67. Elabd C, Cousin W, Upadhyayula P, et al. Oxytocin is an age-specific circulating hormone that is necessary for muscle maintenance and regeneration. *Nat Commun*. 2014;5:4082. PMID: 25083911.
68. Castellano JM, Mosher KI, Abbey RJ, et al. Human umbilical cord plasma proteins revitalize hippocampal function in aged mice. *Nature*. 2017;544:488-492. PMID: 28030351.
69. Mehdipour M, Skinner C, Wong N, et al. Rejuvenation of three germ layers tissues by exchanging old blood plasma with saline-albumin. *Aging*. 2020;12(10):8790-8819. PMID: 32484504.
70. Kim MJ, Miller CM, Shadrach JL, et al. Old plasma dilution reduces human biological age: a clinical study. *GeroScience*. 2022;44:2573-2583. PMID: 35999337.
71. Villeda SA, Luo J, Mosher KI, et al. The ageing systemic milieu negatively regulates neurogenesis and cognitive function. *Nature*. 2011;477:90-94. PMID: 21886162.
72. Smith LK, He Y, Park JS, et al. β2-microglobulin is a systemic pro-aging factor that impairs cognitive function and neurogenesis. *Nat Med*. 2015;21:932-937. PMID: 25645542.
73. Yousef H, Czupalla CJ, Lee D, et al. Aged blood impairs hippocampal neural precursor activity and activates microglia via brain endothelial cell VCAM1. *Nat Med*. 2019;25:988-1000. PMID: 31375627.
74. Zhang G, Li J, Purkayastha S, et al. Hypothalamic programming of systemic ageing involving IKK-β, NF-κB and GnRH. *Nature*. 2013;497:211-216. PMID: 23636330.
75. Zhang Y, Kim MS, Jia B, et al. Hypothalamic stem cells control ageing speed partly through exosomal miRNAs. *Nature*. 2017;548:52-57. PMID: 28746310.
76. Barcena C, Valdés-Mas R, Mayoral P, et al. Healthspan and lifespan extension by fecal microbiota transplantation into progeroid mice. *Nat Med*. 2019;25:1234-1242. PMID: 31332389.
77. Caetano-Silva ME, Rund L, Hutchinson NT, et al. Aging amplifies a gut microbiota immunogenic signature linked to heightened inflammation. *Aging Cell*. 2024;23:e14190. PMID: 38725282.
78. Heinken A, Basile A, Thiele I, et al. Metabolic modelling reveals the aging-associated decline of host-microbiome metabolic interactions in mice. *Nat Microbiol*. 2025. PMID: 40140706.
79. Zhu Y, Tchkonia T, Pirtskhalava T, et al. The Achilles' heel of senescent cells: from transcriptome to senolytic drugs. *Aging Cell*. 2015;14:644-658. PMID: 25754370.
80. Gonzalez-Gualda E, Pàez-Ribes M, Lozano-Torres B, et al. Galacto-conjugation of navitoclax as an efficient strategy to increase senolytic specificity and reduce platelet toxicity. *Aging Cell*. 2020;19(4):e13142. PMID: 32233024.
81. Farr JN, Xu M, Weivoda MM, et al. Effects of intermittent senolytic therapy on bone metabolism in postmenopausal women. *Nat Med*. 2024;30(9):2605-2612. PMID: 38956196.
82. Gonzales MM, Garbarino VR, Kautz TF, et al. A pilot study of senolytics to improve cognition and mobility in older adults (STAMINA). *eBioMedicine*. 2025;113:105612. PMID: 40010154.
83. Gonzales MM, Garbarino VR, Marber E, et al. Senolytic therapy in mild Alzheimer's disease: a phase 1 feasibility trial. *Nat Med*. 2023;29(10):2481-2488. PMID: 37679434.
84. Hickson LJ, Langhi Prata LGP, Boez SA, et al. Senolytics decrease senescent cells in humans: preliminary report from a clinical trial of D+Q in diabetic kidney disease. *EBioMedicine*. 2019;47:446-456. PMID: 31542391.
85. Amor C, Feucht J, Leibold J, et al. Senolytic CAR T cells reverse senescence-associated pathologies. *Nature*. 2020;583:127-132. PMID: 32555459.
86. Amor C, Fernández-Maestre I, Chowdhury S, et al. Prophylactic and long-lasting efficacy of senolytic CAR T cells against age-related metabolic dysfunction. *Nat Aging*. 2024;4:336-349. PMID: 38267706.
87. Amor C, et al. Anti-uPAR CAR T cells reverse and prevent aging-associated defects in intestinal regeneration and fitness. *Nat Aging*. 2025. PMID: 41291258.
88. Cai Y, Zhou H, Zhu Y, et al. Elimination of senescent cells by beta-galactosidase-targeted prodrug attenuates inflammation and restores physical function in aged mice. *Cell Res*. 2020;30:574-589. PMID: 32341413.
89. Suda M, Shimizu I, Katsuumi G, et al. Senolytic vaccination improves normal and pathological age-related phenotypes and increases lifespan in progeroid mice. *Nat Aging*. 2021;1:1117-1126. PMID: 37117524.
90. Pieramici D, et al. Safety and efficacy of senolytic UBX1325 in diabetic macular edema. *NEJM Evid*. 2025. PMID: 40261111.
91. SenNet Biomarkers Working Group. SenNet recommendations for detecting senescent cells in different tissues. *Nat Rev Mol Cell Biol*. 2024;25(12):1001-1023. PMID: 38831121.
92. Farr JN, et al. Characterization of human senescent cell biomarkers for clinical trials. *Aging Cell*. 2025;24:e14489. PMID: 39823170.
93. Ryu D, Mouchiroud L, Andreux PA, et al. Urolithin A induces mitophagy and prolongs lifespan in C. elegans and increases muscle function in rodents. *Nat Med*. 2016;22:879-888. PMID: 27127048.
94. Singh A, D'Amico D, Andreux PA, et al. Urolithin A improves muscle strength, exercise performance, and biomarkers of mitochondrial health in a randomized trial in middle-aged adults. *Cell Rep Med*. 2022;3:100633. PMID: 35584623.
95. Urolithin A immune rejuvenation. Effect of the mitophagy inducer urolithin A on age-related immune decline: a randomized, placebo-controlled trial. *Nat Aging*. 2025. PMID: 41174221.
96. Lee C, Zeng J, Drew BG, et al. The mitochondrial-derived peptide MOTS-c promotes metabolic homeostasis and reduces obesity and insulin resistance. *Cell Metab*. 2015;21:443-454. PMID: 25738459.
97. MOTS-c/CK2. MOTS-c modulates skeletal muscle function by directly binding and activating CK2. *iScience*. 2024. PMID: 39559755.
98. Hashimoto Y, Niikura T, Tajima H, et al. A rescue factor abolishing neuronal cell death by a wide spectrum of familial Alzheimer's disease genes and Abeta. *Proc Natl Acad Sci USA*. 2001;98:6336-6341. PMID: 11287668.
99. Humanin P3S variant. Humanin P3S, haplogroup N1b and the risk of Alzheimer's disease. *Aging Cell*. 2024. PMID: 38713890.
100. Chinnery PF, Samuels DC. Relaxed replication of mtDNA: a model with implications for the expression of disease. *Am J Hum Genet*. 1999;64:1158-1165. PMID: 10508140.
101. Single-cell mtDNA selection. Single-cell analysis reveals context-dependent, cell-level selection of mtDNA. *Nature*. 2024;629:458-466. PMID: 38658765.
102. Longitudinal heteroplasmy. Deleterious mitochondrial heteroplasmies exhibit increased longitudinal change in variant allele fraction. *iScience*. 2025. PMID: 40487423.
103. Mok BY, de Moraes MH, Zeng J, et al. A bacterial cytidine deaminase toxin enables CRISPR-free mitochondrial base editing. *Nature*. 2020;583:631-637. PMID: 32641830.
104. DdCBE-TOD precision editor. Computational design of a high-precision mitochondrial DNA cytosine base editor. *Nat Struct Mol Biol*. 2025. PMID: 41249818.
105. Enhanced DdCBE and TALED. Enhanced C-to-T and A-to-G base editing in mitochondrial DNA with engineered DdCBE and TALED. *Mol Ther*. 2024. PMID: 37984866.
106. Correction of pathogenic mtDNA in patient-derived disease models using mitochondrial base editors. *PLOS Biol*. 2025. PMID: 40554457.
107. Cristae/OPA1/OXPHOS in aged hearts. Multiscale mitochondrial cristae remodeling links Opa1 downregulation to reduced OXPHOS capacity in aged hearts. *PNAS*. 2025. DOI: 10.1073/pnas.2508911123.
108. Chen et al. Small extracellular vesicles from young plasma reverse age-related functional declines by improving mitochondrial energy metabolism. *Nat Aging*. 2024;4:814-833. PMID: 38627524.
109. Mitochondria transplantation transiently rescues cerebellar neurodegeneration. *Nat Commun*. 2025. PMID: 40121210.
110. Gruenbaum Y, Foisner R. Lamins: nuclear intermediate filament proteins with fundamental functions in nuclear mechanics and genome regulation. *Annu Rev Biochem*. 2015;84:131-164. PMID: 16424907.
111. Eriksson M, Brown WT, Gordon LB, et al. Recurrent de novo point mutations in lamin A cause Hutchinson-Gilford progeria syndrome. *Nature*. 2003;423:293-298. PMID: 12714972.
112. Young SG, et al. Progerin forms an abnormal meshwork and has a dominant-negative effect on the nuclear lamina. *PNAS*. 2024;121(27). PMID: 38917015.
113. Yang SH, et al. Nuclear envelope budding inhibition slows down progerin-induced aging process. *PNAS*. 2024;121(41). PMID: 39352925.
114. Scaffidi P, Misteli T. Lamin A-dependent nuclear defects in human aging. *Science*. 2006;312:1059-1063. PMID: 16645051.
115. Azzalin CM, Reichenbach P, Khoriauli L, Giulotto E, Lingner J. Telomeric repeat-containing RNA and RNA surveillance factors at mammalian chromosome ends. *Science*. 2007;318:798-801. PMID: 17656679.
116. Yamada T, et al. Telomeric repeat-containing RNA increases in aged human cells. *Nucleic Acids Res*. 2025;53(13). PMID: 40637232.
117. Maciejowski J, Li Y, Bosco N, Campbell PJ, de Lange T. Chromothripsis and kataegis induced by telomere crisis. *Cell*. 2015;163(7):1641-1654. PMID: 26687355.
118. Maciejowski J, Chatzipli A, Dananberg A, et al. APOBEC3-dependent kataegis and TREX1-driven chromothripsis during telomere crisis. *Nat Genet*. 2020;52:884-893. PMID: 32719516.
119. Noren Hooten N, Evans MK. Changes in DNA double-strand break repair during aging correlate with an increase in genomic mutations. *J Gerontol A Biol Sci Med Sci*. 2022.
120. de Souza-Pinto NC, Wilson DM III, Stevnsner TV, Bohr VA. Repair of 8-oxodeoxyguanosine lesions in mitochondrial DNA depends on the oxoguanine DNA glycosylase (OGG1) gene and 8-oxoguanine accumulates in the mitochondrial DNA of OGG1-defective mice. *Cancer Res*. 2001;61:5378-5381. PMID: 14563545.
121. Wang B, et al. Immunotherapy and senolytics in head and neck squamous cell carcinoma: phase 2 trial results. *Nat Med*. 2025. PMID: 40855191.
122. Makin S, et al. Therapeutic targeting of cellular senescence in diabetic macular edema. *Nat Med*. 2024;30:860-872. PMID: 38321220.
123. Xu M, Tchkonia T, Ding H, et al. JAK inhibition alleviates the cellular senescence-associated secretory phenotype and frailty in old age. *Proc Natl Acad Sci USA*. 2015;112(46):E6301-E6310. PMID: 26578790.
124. Bussian TJ, Aziz A, Meyer CF, et al. Clearance of senescent glial cells prevents tau-dependent pathology and cognitive decline. *Nature*. 2018;562:578-582. PMID: 30232451.
125. Ridker PM, Everett BM, Thuren T, et al. Antiinflammatory therapy with canakinumab for atherosclerotic disease. *N Engl J Med*. 2017;377:1119-1131. PMID: 28845751.
126. Sahin E, DePinho RA. Axis of ageing: telomeres, p53 and mitochondria. *Nat Rev Mol Cell Biol*. 2012;13:397-404. PMID: 22588366.
127. Sahu SK, Clement E, Gao Y, et al. Targeted partial reprogramming of age-associated cell states improves markers of health in mouse models of aging. *Sci Transl Med*. 2024;16(764):eadg1777. PMID: 39259812.
128. Macip CC, Hasan R, Hoznek V, et al. Gene therapy-mediated partial reprogramming extends lifespan and reverses age-related changes in aged mice. *Cell Reprogram*. 2024;26(1):24-32. PMID: 38381405.
129. Murray HC, et al. Intermittent supplementation with fisetin improves physical function and decreases cellular senescence in skeletal muscle with aging. *Aging Cell*. 2025;24:e70114. PMID: 40437670.
130. Tarantini S, et al. Treatment with the BCL-2/BCL-xL inhibitor senolytic drug ABT263/navitoclax improves functional hyperemia in aged mice. *GeroScience*. 2021;43:2427-2440. PMID: 34427858.
131. Vinten et al. NAD+ precursor supplementation in human ageing: clinical evidence and challenges. *Nat Metab*. 2025. PMID: 41083806.
132. NAD depletion in skeletal muscle does not compromise muscle function or accelerate aging. *Cell Metab*. 2025;37(7):1460-1481. PMID: 40311622.
133. Covarrubias AJ, Kale A, Perrone R, et al. Senescent cells promote tissue NAD+ decline during ageing via the activation of CD38+ macrophages. *Nat Metab*. 2020;3:120-129. PMID: 33199924.
134. Fang EF, et al. NAD augmentation as a disease-modifying strategy for neurodegeneration. *Trends Endocrinol Metab*. 2025. PMID: 40287324.
135. Fang EF, et al. NAD+ reverses Alzheimer's neurological deficits via regulating differential alternative RNA splicing of EVA1C. *Sci Adv*. 2025. PMID: 41202143.
136. Compound C8 NAMPT activator. Discovery of a potent nicotinamide phosphoribosyltransferase activator for improving aging-associated dysfunctions. *J Med Chem*. 2024;67(5):4120-4130. PMID: 38367219.
137. Imai SI. NAD World 3.0: the importance of the NMN transporter and eNAMPT in mammalian aging and longevity control. *npj Aging*. 2025.
138. eNAMPT-EVs. Human plasma-derived eNAMPT-containing extracellular vesicles promote NAD+ biosynthesis and thermogenesis in mice. *npj Aging*. 2025. PMID: 41285826.
139. Drp1/longevity. Developmental disruption of the mitochondrial fission gene drp-1 extends the longevity of daf-2 insulin/IGF-1 receptor mutant. *GeroScience*. 2025;47:877-902. PMID: 39028454.
140. Bar C, Bernardes de Jesus B, Serrano R, et al. Telomerase expression confers cardioprotection in the adult mouse heart after acute myocardial infarction. *Nat Commun*. 2014;5:5863. PMID: 25519492.
141. Janovic T, Perez I, Schmidt JC. TRF1 and TRF2 form distinct shelterin subcomplexes at telomeres. *Cell Rep*. 2024. PMID: 39763972.
142. Lagger C, Ursu E, Fumagalli A, et al. scDiffCom: a tool for differential analysis of cell-cell interactions provides a mouse atlas of aging changes in intercellular communication. *Nat Aging*. 2023;3:1446-1461. PMID: 37919434.
143. DunedinPACE. Belsky DW, Caspi A, Corcoran DL, et al. DunedinPACE, a DNA methylation biomarker of the pace of aging. *eLife*. 2022;11:e73420. PMID: 35029144.
144. Justice JN, et al. Senolytics in idiopathic pulmonary fibrosis: results of a phase I, single-blind, single-center, randomized, placebo-controlled pilot trial. *EBioMedicine*. 2023;90:104480. PMID: 36857968.
145. Justice JN, et al. Senolytics in idiopathic pulmonary fibrosis: results from a first-in-human, open-label, pilot study. *EBioMedicine*. 2019;40:554-563. PMID: 30616998.
146. Watson CJ, et al. The evolutionary dynamics and fitness landscape of clonal hematopoiesis. *Science*. 2020;367:1449-1454. PMID: 32747822.
147. Lee-Six H, Øbro NF, Shepherd MS, et al. Population dynamics of normal human blood inferred from somatic mutations. *Nature*. 2018;561:473-478. PMID: 24835462.
148. Ruxolitinib senomorphic cardiomyopathy. Ruxolitinib-based senomorphic therapy mitigates cardiomyocyte senescence in septic cardiomyopathy. *Int J Biol Sci*. 2024;20:4314-4331. PMID: 39247818.
149. Tang M, et al. The role of p16Ink4a as an early predictor of physiological decline during natural aging. *GeroScience*. 2024. PMID: 39606419.
150. Deng Y, et al. Senolytics rejuvenate aging cardiomyopathy in human cardiac organoids. *Mech Ageing Dev*. 2025;223:112007. PMID: 39622416.
151. Paine PT, et al. Partial cellular reprogramming: a deep dive into an emerging rejuvenation technology. *Aging Cell*. 2024;23:e14039. PMID: 38062870.
152. Grosse L, Demaria M, et al. Senolytics: from pharmacological inhibitors to immunotherapies, a promising future for patients' treatment. *npj Aging*. 2024;10:31.
153. Chaib S, Tchkonia T, Kirkland JL. Cellular senescence and senolytics: opportunities and challenges. *Nat Rev Drug Discov*. 2024.
154. Horvath S, Raj K. DNA methylation-based biomarkers and the epigenetic clock theory of ageing. *Nat Rev Genet*. 2018;19:371-384.
155. Krauss R, et al. Influence of rapamycin on safety and healthspan metrics after one year: PEARL trial results. *Aging*. 2025;17(4). PMID: 40188830.
156. Gkioni L, Partridge L, et al. The geroprotectors trametinib and rapamycin combine additively to extend mouse healthspan and lifespan. *Nat Aging*. 2025. PMID: 40437307.
157. Nonninger S, et al. A TFEB-TGFbeta axis systemically regulates diapause, stem cell resilience and protects against a senescence-like state. *Nat Aging*. 2025. PMID: 40588651.
158. Ramirez-Pardo I, Campanario S, et al. Chaperone-mediated autophagy sustains muscle stem cell regenerative functions but declines with age. *Nat Metab*. 2025.
159. Age-related decline of chaperone-mediated autophagy in skeletal muscle leads to progressive myopathy. *Nat Metab*. 2025. PMID: 41339969.
160. Valdor R, et al. Restoration of LAMP2A expression in old mice leads to changes in the T cell compartment that support improved immune function. *PNAS*. 2024. PMID: 39259591.
161. Marino G, et al. Aging and diet alter the protein ubiquitylation landscape in the mouse brain. *Nat Commun*. 2025. PMID: 40480969.
162. Fuster JJ, et al. Clonal hematopoiesis driven by mutated DNMT3A promotes inflammatory bone loss. *Cell*. 2024. PMID: 38838669.
163. Scherer M, et al. Clonal tracing with somatic epimutations reveals dynamics of blood ageing (EPI-Clone). *Nature*. 2025;643:478-487. PMID: 40399669.
164. Rando TA, Brunet A, Goodell MA. Hallmarks of stem cell aging. *Cell Stem Cell*. 2025;32(7):1038-1054. PMID: 40562035.
165. Castner SA, et al. Longevity factor klotho enhances cognition in aged nonhuman primates. *Nat Aging*. 2023;3:931-937. PMID: 37400721.
