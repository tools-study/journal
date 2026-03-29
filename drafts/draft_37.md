# Tissue-Specific Reprogramming Challenges

---

## Abstract

Partial cellular reprogramming — transient expression of Oct4, Sox2, and Klf4 (OSK) or their chemical equivalents — has emerged as the most promising approach to epigenetic age reversal, with the first human clinical trial (ER-100, Life Biosciences) cleared by the FDA in January 2026 for optic neuropathies. Yet the path from single-organ proof-of-concept to whole-body reprogramming confronts a fundamental obstacle: tissue-specific reprogramming incompatibility. Continuous in vivo expression of Yamanaka factors kills mice within one week through hepatic and intestinal failure (Parras et al., 2023), while the same factors safely restore vision in the eye for over 18 months (Karg et al., 2023). Each tissue possesses a distinct "reprogramming competence" profile — a composite of cell cycle state, chromatin accessibility, pioneer factor context, microenvironmental signaling, and somatic mutation burden — that determines its dose-response relationship, therapeutic window, and optimal modality. This review systematically profiles reprogramming competence across eight organ systems (eye, brain, heart, liver, intestine, skeletal muscle, blood, and skin), identifies mesenchymal drift as a unifying reversible aging signature across all tissues, evaluates emerging single-factor and chemical alternatives to OSK(M), and proposes a tissue-stratified framework for achieving clinically meaningful whole-body reprogramming. We present novel mathematical frameworks for multi-tissue optimization under oncogenic constraints and propose a multi-tissue single-cell multi-omic atlas experiment to define tissue-specific dose-response functions. The central argument is that abandoning the one-size-fits-all reprogramming paradigm in favor of organ-optimized, multi-modality rejuvenation strategies is the rate-limiting step for translating partial reprogramming from laboratory curiosity to transformative medicine.

---

## 1. Introduction: The Tissue Incompatibility Crisis

### 1.1 The Promise of Partial Reprogramming

The discovery that transient expression of Oct4, Sox2, Klf4, and c-Myc (OSKM) can reverse age-associated epigenetic changes without inducing full pluripotency represents one of the most consequential findings in modern biology (Ocampo et al., 2016). In the seminal demonstration, cyclic OSKM induction in Lmna^G609G/G609G progeria mice ameliorated hallmarks of aging and extended lifespan without teratoma formation, establishing that epigenetic rejuvenation is separable from dedifferentiation (Ocampo et al., 2016). Subsequent work demonstrated that a single 13-day pulse of OSKM rejuvenates human fibroblasts by approximately 30 years as measured by the Horvath epigenetic clock, while cells retain functional fibroblast identity (Gill et al., 2022). Most strikingly, systemic AAV delivery of an inducible OSK cassette to aged wild-type mice extended median remaining lifespan by 109% (Macip et al., 2024), establishing partial reprogramming as a genuine longevity intervention.

These laboratory advances have now reached a clinical inflection point. In January 2026, Life Biosciences announced FDA clearance of an Investigational New Drug (IND) application for ER-100, an AAV-delivered OSK therapy administered via intravitreal injection for open-angle glaucoma and non-arteritic anterior ischemic optic neuropathy (NAION), marking the first cellular rejuvenation therapy to enter human clinical trials (NCT07290244). The phase 1 study will evaluate safety, tolerability, immune responses, and visual function in patients with optic neuropathies. This milestone validates the therapeutic potential of partial epigenetic reprogramming — yet it also highlights a critical limitation: ER-100 targets a single, immune-privileged organ. The path from eye-specific rejuvenation to whole-body age reversal is obstructed by a problem that no amount of factor engineering or delivery optimization alone can solve: tissue-specific reprogramming incompatibility.

### 1.2 The Toxicity Problem: Why Whole-Body Reprogramming Kills

The severity of tissue-specific incompatibility was unambiguously demonstrated by Parras and colleagues, who showed that continuous in vivo OSKM induction causes hepatic and intestinal dysfunction, decreased body weight, and premature death within approximately one week (Parras et al., 2023). The lethal phenotype is remarkably organ-specific: liver and intestine — the two adult tissues with the highest intrinsic regenerative capacity — are precisely the organs most vulnerable to reprogramming-induced dedifferentiation. Histopathological analysis revealed complete loss of hepatocyte function and intestinal barrier breakdown, with consequent microbial translocation and systemic inflammatory collapse (Parras et al., 2023).

The complementary experiment by Browder and colleagues confirmed this organ-specific vulnerability. By engineering chimeric mouse strains that excluded OSKM expression from liver and intestine using tissue-specific Cre-lox drivers, they reduced early mortality from near-100% to approximately 40% during continuous induction, while still achieving a decrease in organismal biological age in the remaining tissues (Browder et al., 2022). This rescue experiment establishes two foundational principles: first, that systemic rejuvenation is achievable if the dose-limiting organs can be protected; and second, that different tissues have fundamentally different tolerance thresholds for the same reprogramming stimulus.

The standard mitigation — cyclic induction with 2-day ON / 5-day OFF protocols — enables safe long-term reprogramming for up to 35 cycles (approximately 10 months) and produces measurable rejuvenation in kidney, skin, and blood (Browder et al., 2022; Ocampo et al., 2016). However, this protocol represents a compromise: by diluting reprogramming stimulus to accommodate the most sensitive tissues, it limits the achievable rejuvenation depth in tissues that could safely tolerate — and would benefit from — more intensive or prolonged treatment. Recent comparative analysis of multiple reprogrammable mouse strains confirmed that mortality and rejuvenation outcomes depend heavily on the genetic background, transgene insertion locus, and tissue-specific expression pattern of the OSKM cassette (Pico et al., 2025).

### 1.3 Thesis: From One-Size-Fits-All to Tissue-Stratified Rejuvenation

This review argues that the single biggest technical obstacle to clinically meaningful whole-body age reversal is not the absence of effective reprogramming factors, nor the lack of safe delivery vehicles, but rather the fundamental mismatch between a uniform reprogramming stimulus and the profoundly heterogeneous tissue landscape of the adult human body. Each tissue possesses what we term a **reprogramming competence profile** — a composite of cell cycle state, chromatin accessibility, pioneer factor context, microenvironmental signaling, metabolic configuration, and somatic mutation burden — that determines its dose-response relationship, safety threshold, and optimal rejuvenation modality.

We systematically profile reprogramming competence across eight organ systems (Sections 3.1–3.8), identify mesenchymal drift as a unifying and reversible aging signature (Section 4), evaluate emerging alternatives to the OSK paradigm including single-factor and chemical approaches (Section 5), delineate tissue-specific oncogenic risk architectures (Section 6), and propose a quantitative framework for multi-tissue optimization (Section 7). We conclude with a proposed experiment — a multi-tissue single-cell multi-omic reprogramming atlas — designed to generate the tissue-specific dose-response functions required for rational design of tissue-stratified clinical protocols (Section 8).

---

## 2. Molecular Determinants of Tissue-Specific Reprogramming Competence

### 2.1 Cell Cycle State as the Primary Determinant

The single most predictive feature of a tissue's response to reprogramming factors is the cell cycle status of its constituent cells. Adult human tissues span a broad spectrum of mitotic activity: intestinal crypt stem cells divide approximately every 24 hours; hepatocytes are quiescent (G0/G1) but retain full proliferative capacity upon mitogenic stimulation; satellite cells in skeletal muscle are deeply quiescent; and cardiomyocytes and most neurons are terminally post-mitotic, having exited the cell cycle during embryonic or early postnatal development.

Cell cycle state determines reprogramming competence through three converging mechanisms. First, S-phase transit is required for replication-coupled dilution of repressive histone marks, particularly H3K9me3 and H3K27me3, which constitute major barriers to factor-mediated chromatin remodeling (Paine et al., 2024). Second, the availability of cell cycle regulators (CDK2, Cyclin E) gates the transition from initial factor binding to productive transcriptional activation of pluripotency-associated genes (Yucel & Gladyshev, 2024). Third, in post-mitotic cells, forced cell cycle re-entry activates the DNA damage response (DDR), which in neurons triggers apoptosis rather than proliferation — a phenomenon termed the "cell cycle death trap" (Wu et al., 2024).

The consequences are profound. Constitutively cycling tissues (intestinal crypts, skin) respond rapidly to OSKM but are vulnerable to runaway dedifferentiation. Quiescent-but-recruitable tissues (liver, muscle) can be activated to proliferate, creating a transient window of reprogramming permissivity but also of vulnerability. Post-mitotic tissues (heart, brain) resist reprogramming through both chromatin compaction and active suppression of mitotic genes, requiring months of continuous factor expression rather than the short cyclic pulses effective in proliferating tissues (Jo et al., 2025).

### 2.2 Chromatin Accessibility and Pioneer Factor Context

Within any given tissue, only a subset of cells — termed "reprogramming-permissive" cells — can successfully undergo epigenetic remodeling (Cipriano et al., 2024). These cells are characterized by faster cycling, reduced expression of fibroblast-activation genes, and critically, a chromatin accessibility landscape that exposes binding motifs for the reprogramming factors (Sengstack et al., 2026). ATAC-seq profiling across tissues reveals that the same OCT4 and SOX2 motifs that are accessible in skin fibroblasts are occluded by H3K9me3 in mature cardiomyocytes and by heterochromatic H3K27me3 domains in post-mitotic neurons, explaining the dramatically different kinetics and efficiencies of reprogramming across cell types.

The pioneer factor concept provides a mechanistic framework for understanding these tissue-specific differences. OCT4, SOX2, and KLF4 function as pioneer transcription factors capable of engaging nucleosomal DNA in closed chromatin, but their pioneer activity is context-dependent: the specific nucleosomal positions they can access vary by cell type, histone modification landscape, and the presence of co-factors (Jo et al., 2025). In the liver, where hepatocyte chromatin is relatively permissive, OSKM rapidly engages target loci and initiates dedifferentiation within days. In the heart, additional tissue-specific barriers — including limiting concentrations of the positive transcription elongation factor P-TEFb — prevent c-Myc from activating transcription even when it successfully binds DNA at open elements (Villa del Campo et al., 2020). Only ectopic expression of Cyclin T1, a P-TEFb subunit, abrogates this cardiac refractoriness to Myc, revealing that tissue-specific transcriptional co-factor availability constitutes a gatekeeping layer beyond chromatin accessibility itself.

### 2.3 Microenvironmental Signaling Gating

Reprogramming does not occur in a cell-autonomous vacuum. Multiple signaling pathways operating at the tissue level gate the response to reprogramming factors, with each tissue employing a distinct combination of pathway activities.

**Hippo/YAP signaling** plays a central role in tissues with high mechanical load. In the intestine, injury activates YAP1-dependent formation of revival stem cells (revSCs) — a rare, clusterin-positive cell type that regenerates the Lgr5+ crypt base columnar compartment (Ayyaz et al., 2019). Damage-induced chromatin remodeling in intestinal crypts converges on redundant TGFβ and Hippo signaling pathways; simultaneous interference in both abolishes revSC formation and leads to rapid intestinal collapse (Fink et al., 2024). In the heart, constitutively active YAP5SA overcomes the mechanical barrier of sarcomere organization to induce mitotic rounding and cardiomyocyte division, but this requires prior sarcomere disassembly — a structural prerequisite unique to this tissue (Monroe et al., 2024).

**Wnt signaling** promotes reprogramming in the nervous system by activating neuron-specific transcription factors through GSK3β inhibition. Chemical Wnt activators enhance both direct neuronal reprogramming and partial reprogramming efficacy in brain tissue, but the same pathway activation in the intestine, which is already Wnt-dependent for homeostatic stem cell maintenance, can exacerbate the dedifferentiation vulnerability of this organ.

**TGFβ signaling** inhibition is a core component of virtually all chemical reprogramming cocktails, reflecting its role as a barrier to mesenchymal-to-epithelial transition (MET) — the first molecular step in factor-mediated reprogramming (Cheng et al., 2025). However, TGFβ also maintains tissue integrity in the intestinal epithelium and liver, creating a fundamental tension: the same pathway that must be suppressed for efficient reprogramming is simultaneously required for organ homeostasis.

### 2.4 Metabolic State and the Epigenetic Interface

Cellular metabolic configuration influences reprogramming competence through its direct effects on epigenetic enzyme cofactors. The NAD+/NADH ratio determines sirtuin activity; acetyl-CoA availability gates histone acetyltransferase function; α-ketoglutarate, a TCA cycle intermediate, is a required co-substrate for TET dioxygenases and Jumonji-domain histone demethylases that remove DNA methylation and repressive histone marks, respectively. Multi-omics profiling of partial chemical reprogramming revealed that the most prominent molecular signature of rejuvenation is upregulation of mitochondrial oxidative phosphorylation, with functional increases in spare respiratory capacity and mitochondrial transmembrane potential (Mitchell et al., 2024). Tissues with compromised mitochondrial function — a hallmark of aging across all organ systems — may therefore have reduced capacity to generate the metabolic cofactors required for epigenetic remodeling, creating a metabolic bottleneck that limits reprogramming efficiency in the most aged cells that would benefit most from rejuvenation.

---

## 3. Organ-Specific Reprogramming Profiles

The following sections profile reprogramming competence across eight organ systems, organized by their position on the competence spectrum from highest to lowest intrinsic reprogramming capacity. For each organ, we detail: the molecular basis of its competence profile, empirical evidence from in vivo reprogramming studies, tissue-specific safety boundaries, and the recommended therapeutic modality for that organ. A summary is provided in Table 1.

**Table 1. Tissue-Specific Reprogramming Competence Profiles**

| Organ | Cell Cycle Status | Reprogramming Competence | Primary Barrier | Dominant Safety Risk | Therapeutic Window | Recommended Modality |
|-------|------------------|------------------------|----------------|---------------------|-------------------|---------------------|
| Intestine | Constitutively cycling | Very High | None (too responsive) | Barrier breakdown, sepsis | Excluded from systemic | Local chemical or excluded |
| Liver | Quiescent, recruitable | Very High | None (too responsive) | Hepatic failure, tumors | Single factor, ultra-short pulse | EZH2 overexpression |
| Skin | Cycling (basal), quiescent (dermal) | High | Low | Minimal | Broad | Chemical or single factor, topical |
| Eye/Retina | Post-mitotic (RGCs) | High (paradoxical) | Incomplete differentiation permits remodeling | Low (compartmentalized) | Months continuous | AAV-OSK intravitreal |
| Skeletal Muscle | Quiescent (satellite cells) | Medium | Satellite cell exhaustion, niche aging | Moderate | Cyclic, niche-targeted | AAV-OSK local or niche remodeling |
| Brain | Post-mitotic (neurons) | Low–Medium | G0 arrest, cell cycle death trap | Cell cycle re-entry → apoptosis | Months continuous, local | AAV-OSK targeted, senescent cell-specific |
| Heart | Post-mitotic | Medium (narrow window) | Sarcomere lock, P-TEFb deficiency | Dedifferentiation → heart failure | 3–6 days maximum | Ultra-short OSKM or direct reprogramming |
| Blood/Immune | Actively dividing (HSCs) | Medium | CHIP clonal selection | Oncogenic transformation (p53-mutant) | Ex vivo only | Ex vivo with mutation screening |

### 3.1 Eye and Retina — The First Clinical Frontier

The eye occupies a unique position in the reprogramming competence landscape: despite containing predominantly post-mitotic retinal ganglion cells (RGCs), it exhibits paradoxically high and sustained responsiveness to OSK-mediated epigenetic rejuvenation. This apparent contradiction is resolved by two properties: the "incomplete differentiation" of RGCs, which retain accessible chromatin at developmental gene loci despite terminal cell cycle exit; and the immune-privileged, anatomically compartmentalized nature of the vitreous cavity, which limits both systemic exposure and inflammatory rejection of virally delivered transgenes.

The foundational study by Lu and colleagues demonstrated that AAV-delivered OSK in mouse RGCs restores youthful DNA methylation patterns and transcriptomes, promotes axon regeneration after optic nerve crush injury, and reverses vision loss in both glaucoma models and naturally aged mice (Lu et al., 2020). Critically, the exclusion of c-Myc from the reprogramming cocktail prevented tumorigenesis while maintaining full rejuvenation capacity — the first clear demonstration that the rejuvenation and pluripotency programs of the Yamanaka factors are separable in vivo. A subsequent study extended these findings by showing that only 2 months of OSK expression fully restored impaired vision in glaucomatous mice, with the restoration sustained for at least 11 months under prolonged expression, and no adverse effects on retinal structure, intraocular pressure, or body weight after 21 months of continuous OSK expression (Karg et al., 2023). This remarkable durability and safety profile is unmatched by any other tissue.

The clinical significance of ocular rejuvenation is reinforced by the discovery that accelerated epigenetic aging, measured by Horvath, Hannum, PhenoAge, and GrimAge clocks in blood DNA methylation, is significantly associated with faster glaucoma progression. Fast progressors showed Horvath clock acceleration of +2.93 years over slow progressors (P < 0.001), establishing epigenetic age as a prognostic biomarker and providing the clinical rationale for ER-100 (Medeiros et al., 2025).

Beyond partial epigenetic reprogramming, the eye serves as a proving ground for complementary regenerative strategies. Direct lineage conversion of Muller glia — the principal glial cell type of the retina — into neurons has been achieved through multiple approaches. Oct4 overexpression alone induces transdifferentiation of mouse Muller glia into bipolar neurons, with synergistic enhancement when combined with Notch pathway inhibition (Le et al., 2025). The identification of Prox1 as a non-cell-autonomous molecular brake on retinal regeneration — transferred intercellularly from neurons to Muller glia in degenerating mammalian retinas but absent in regenerating zebrafish — reveals an additional targetable barrier specific to the mammalian eye (Zhang et al., 2025a).

The eye's status as "Goldilocks organ" for reprogramming derives from three converging properties: (1) post-mitotic cells that resist runaway dedifferentiation; (2) compartmentalized anatomy enabling local delivery without systemic exposure; and (3) quantifiable functional outcomes (visual acuity, pERG, OCT) that accelerate clinical development. These properties make the eye the ideal first target for clinical translation, but also the easiest — scaling from eye to whole body will require confronting tissues that lack all three advantages.

### 3.2 Brain — Post-Mitotic Barriers and the Cell Cycle Death Trap

The brain presents a fundamentally different reprogramming challenge from the eye. Although both contain predominantly post-mitotic cells, neurons occupy a deeper state of terminal differentiation characterized by extensive heterochromatinization of cell cycle gene loci, complex dendritic and axonal morphology that is incompatible with mitotic rounding, and active suppression mechanisms that destroy neurons attempting to re-enter the cell cycle.

The cell cycle death trap is now molecularly characterized. Wu and colleagues demonstrated that terminally differentiated neurons that re-enter the cell cycle predominantly undergo cellular senescence rather than division, with the most affected population being excitatory neurons in cortical and hippocampal regions (Wu et al., 2024). In Alzheimer's disease, these senescent neurons accumulate rather than decrease, presenting proinflammatory, metabolically deregulated signatures that exacerbate rather than ameliorate neurodegeneration. This mechanism explains the narrow therapeutic window for brain reprogramming: any intervention that pushes neurons past the G1/S checkpoint without complete mitotic machinery will trigger apoptosis or senescence rather than rejuvenation.

Despite these barriers, controlled partial reprogramming can productively rejuvenate the brain. Shen and colleagues demonstrated that transient OSKM induction in adult mice expanded neurogenesis, increased upper cortical neuron numbers, and enhanced motor and social behavior without compromising lineage fidelity (Shen et al., 2024). In aged mice, targeted and systemic partial reprogramming restores the production of neuronal progenitors and new neurons in the hippocampal neurogenic niche, with the primary effect being improvement of neuroblast populations committed to generating new neurons (Xu et al., 2024). Intrahippocampal AAV delivery of OSKM in 25-month-old rats improved spatial memory, reversed age-associated methylation increases at bivalent regulatory regions and transcription start sites, and showed no pathological alterations within 39 days of treatment (Moreno-Jimenez et al., 2025).

A particularly elegant approach targets reprogramming specifically to stressed and senescent cells using the Cdkn2a (p16) promoter to drive OSK expression. Sahu and colleagues showed that this strategy extends lifespan, improves overall fitness, and shifts the transcriptome toward younger profiles in both progeria and aged wild-type mice, with no observed tumor increase (Sahu et al., 2024). By restricting reprogramming to cells that express senescence markers, this approach avoids the cell cycle death trap in healthy neurons while rejuvenating the senescent subpopulation that contributes disproportionately to age-related dysfunction.

The peripheral nervous system offers a complementary perspective. Age-associated loss of Schwann cell plasticity — the ability of myelinating glia to dedifferentiate and support axon regeneration after injury — can be restored by iterative transient OSKM expression, which corrects dysfunctional Runx2-positive transitional states and restores stress granule homeostasis (Wang et al., 2025a). This demonstrates that the reprogramming competence of neural support cells, unlike that of neurons themselves, is recoverable.

Brain-specific reprogramming requirements differ qualitatively from all other tissues: continuous rather than cyclic factor expression over months is needed; local delivery (intrahippocampal, intrathecal) is preferred over systemic to avoid hepatic/intestinal toxicity; and the functional endpoint — cognitive preservation rather than tissue regeneration — demands different safety metrics. The brain will likely be among the last organs to receive whole-body reprogramming, requiring either exquisitely cell-type-targeted promoters or alternative approaches that avoid cell cycle engagement entirely.

### 3.3 Heart — The Sarcomere Lock and the Six-Day Window

The heart epitomizes the challenge of reprogramming post-mitotic tissues with structural constraints. Adult cardiomyocytes have exited the cell cycle, assembled elaborate sarcomeric structures that generate contractile force, and erected tissue-specific barriers that neutralize mitogenic stimuli even when transcription factors successfully bind their target DNA.

The cardiac reprogramming window is extraordinarily narrow. Chen and colleagues demonstrated that heart-specific OSKM expression for six days before or during myocardial infarction induces cardiomyocyte dedifferentiation to a fetal-like transcriptional state with renewed proliferative capacity, reducing scar size and improving cardiac function (Chen et al., 2021). However, twelve days of the same expression causes irreversible dedifferentiation, teratoma formation, and heart failure — establishing that the therapeutic window for cardiac reprogramming is measured in days, not weeks (Chen et al., 2021). This window is approximately 50-fold narrower than the eye's 18-month continuous tolerance, illustrating the extreme tissue specificity of reprogramming safety.

Two tissue-specific barriers explain the heart's unique reprogramming profile. The first is the **sarcomere lock**: adult cardiomyocytes must disassemble their contractile apparatus before they can progress from S to G2 phase and undergo mitotic rounding. Monroe and colleagues showed that even constitutively active YAP5SA, which induces over 20% of cardiomyocyte clones to contain two or more cells, is limited by inefficient G2 progression that can only be improved by simultaneous P21 inhibition (Monroe et al., 2024). The molecular basis of sarcomere disassembly has been identified as alpha/gamma-adducin-mediated destabilization of alpha-actinin interactions, with adducin levels declining precipitously after birth (Xiao et al., 2024). This structural constraint has no parallel in the eye, brain, or any other tissue.

The second barrier is **P-TEFb deficiency**. Villa del Campo and colleagues made the remarkable discovery that c-Myc binds DNA at open chromatin elements in both responsive (liver) and non-responsive (heart) tissues, but fails to activate transcription in the heart due to limiting concentrations of positive transcription elongation factor b (P-TEFb), specifically its Cyclin T1 subunit (Villa del Campo et al., 2020). Ectopic Cyclin T1 overexpression in adult cardiomyocytes abrogated their refractoriness to Myc and permitted efficient Myc target gene expression — identifying P-TEFb as the tissue-specific gatekeeper of cardiac reprogramming responsiveness. This finding explains why the heart is resistant to OSKM-mediated proliferative signals that work efficiently in liver and intestine: the cardiac transcriptional machinery lacks a critical co-factor required to translate factor binding into productive transcription.

Additional molecular checkpoints continue to be discovered. Asparagine synthetase (ASNS) marks a distinct metabolic dependency threshold for cardiomyocyte dedifferentiation across four different induction models including in vivo AAV9-delivered OSKM, indicating that amino acid biosynthesis constitutes a metabolic checkpoint that must be traversed for dedifferentiation (Huang et al., 2024). The natural antisense transcript Zeb2os suppresses ZEB2 reactivation after ischemia-reperfusion injury, preventing the dedifferentiation and metabolic remodeling necessary for effective cardiac repair — an endogenous molecular brake on the very pathway OSKM exploits (Zeb2os study, 2026).

Notably, cellular senescence directly impairs cardiac reprogramming. During GMT-mediated direct fibroblast-to-cardiomyocyte conversion (a complementary strategy to partial epigenetic reprogramming), massive senescence and apoptosis occur as dominant failure modes, with RB1 identified as a key senescence-associated gene whose knockdown significantly enhances conversion efficiency (Li et al., 2025a). Single-factor approaches are also emerging: PHF7 was identified as the most potent single-factor activator of adult fibroblast-to-cardiomyocyte reprogramming in vitro, and in vivo delivery improved cardiac function and survival for up to 16 weeks post-infarction (Li et al., 2025b).

For the heart, the optimal strategy is not systemic partial reprogramming but rather one of two alternatives: ultra-short transient OSKM (3–6 days maximum) for acute regeneration after myocardial infarction, or direct reprogramming using tissue-specific factor cocktails (GMT, PHF7) that bypass the pluripotency program entirely. Neither approach is compatible with the cyclic systemic protocols designed for whole-body reprogramming, underscoring the necessity of tissue-stratified intervention.

### 3.4 Liver — High Competence, Extreme Vulnerability

The liver is the most paradoxical organ in the reprogramming landscape: it possesses the highest reprogramming competence of any adult tissue — and for precisely that reason, it is the most dangerous to reprogram.

Hepatocytes reside in a quiescent G0/G1 state under homeostatic conditions but retain an extraordinary capacity for proliferative expansion, capable of regenerating up to 70% of liver mass after partial hepatectomy. This latent proliferative potential translates directly into reprogramming competence: OSKM engages hepatocyte chromatin rapidly and efficiently, driving dedifferentiation to a progenitor-like state characterized by increased proliferation and topoisomerase 2-dependent chromatin remodeling (Hishida et al., 2022). Short-term hepatocyte-specific 4F expression enhanced liver regenerative capacity beyond the organ's already impressive baseline — but also created a trajectory toward complete identity loss.

The liver's extreme vulnerability to OSKM was quantified by Parras and colleagues: continuous induction produces hepatic failure within approximately 7 days, making the liver (along with the intestine) the dose-limiting organ for systemic reprogramming (Parras et al., 2023). A single one-week burst of OSKM, while insufficient to cause overt hepatic failure, nevertheless induces transient histological changes and, notably, rejuvenation of epigenetic, transcriptomic, and metabolomic characteristics (Chondronasiou et al., 2022). The challenge is that the distance between "sufficient for rejuvenation" and "sufficient for liver failure" is vanishingly small — a therapeutic index problem of a fundamentally different nature than in the eye or brain.

The solution may lie in single-factor approaches that achieve liver rejuvenation without multi-factor reprogramming. Sengstack and colleagues used a Perturb-seq discovery platform in replicatively aged human fibroblasts to systematically identify single transcription factor perturbations that drive rejuvenation without dedifferentiation (Sengstack et al., 2026). Among the validated hits, **EZH2 overexpression** stands out for its liver-specific translational potential: AAV8-mediated liver-specific EZH2 overexpression in 20-month-old mice reversed thousands of age-associated gene changes, decreased steatosis and fibrosis, and improved glucose tolerance. Critically, EZH2 overexpression achieved these rejuvenation endpoints through a single gene perturbation that drives convergent downstream transcriptional programs conserved across aging and rejuvenation models — without inducing dedifferentiation or requiring the dangerous multi-factor cocktail.

The liver's aging trajectory has been mapped at single-cell resolution using spatial transcriptomics, scATAC-seq, and lipidomics, revealing zonation-dependent aging: periportal hepatocytes show decreased mitochondrial fitness while pericentral hepatocytes accumulate large lipid droplets, with epigenetic changes varying by metabolic zone (Nikopoulou et al., 2023). An additional protective mechanism — hepatocyte polyploidy — buffers against age-related transcriptomic changes and reduces steatosis by enriching for wild-type alleles (Yin et al., 2024). Intriguingly, chromatin regulators Arid1a, Uhrf1, and PRC2 components control hepatocyte dedifferentiation competency, suggesting that these factors could be co-targeted to limit the depth of reprogramming while preserving rejuvenation (Jo et al., 2025).

The clinical implication is unambiguous: the liver should **not** receive multi-factor reprogramming under any whole-body protocol. Single-factor approaches (EZH2), chemical cocktails with liver-sparing properties, or tissue-specific exclusion via Cre-lox or promoter engineering represent the only safe paths to hepatic rejuvenation.

### 3.5 Intestine — Revival Stem Cells and the Barrier Integrity Crisis

The intestinal epithelium represents the extreme end of the regenerative spectrum. Lgr5-positive stem cells in the crypt base divide approximately every 24 hours, fueling the complete turnover of the intestinal lining every 3–5 days — the highest basal regenerative rate of any adult tissue (Ayyaz et al., 2019). This constitutive proliferative activity makes the intestine exquisitely sensitive to reprogramming factors that promote dedifferentiation: OSKM expression in the intestine triggers a catastrophic cascade of barrier breakdown, loss of absorptive and secretory epithelial function, microbial translocation across the denuded mucosal surface, and systemic sepsis (Parras et al., 2023).

The paradox is that the intestine already possesses sophisticated damage-response reprogramming machinery that normally operates under tight physiological control. Upon tissue injury, a rare quiescent cell type — the revival stem cell (revSC), marked by high clusterin (Clu) expression — undergoes YAP1-dependent transient expansion to reconstitute the Lgr5+ crypt base columnar compartment (Ayyaz et al., 2019). Single-nuclear multi-omics of regenerating mouse crypts revealed that revSC chromatin accessibility overlaps with both intestinal stem cells and differentiated lineages, and that damage-induced chromatin remodeling converges on redundant TGFβ and Hippo signaling pathways (Fink et al., 2024). Simultaneous interference in both pathways abolishes revSC formation, precludes new stem cell generation, and leads to rapid intestinal collapse — demonstrating both the pathway's redundancy and its essentiality (Fink et al., 2024).

Remarkably, partial OSKM reprogramming can co-opt this endogenous damage-response program even in uninjured intestine. Kim and colleagues demonstrated that partial reprogramming induces fetal-like characteristics in intestinal epithelial cells via Ptgs1-mediated epithelial prostaglandin production, enabling injury-free regeneration without mesenchymal assistance (Kim et al., 2023). Transient OSKM activation mimicked an injury response, inducing two distinct fetal-like cell states — one mirroring crypt injury and one retaining villus epithelial identity. This suggests that the intestine's response to OSKM is not random dedifferentiation but rather an aberrant activation of its endogenous regenerative program.

For whole-body reprogramming strategies, the intestine must be **explicitly excluded** from systemic factor delivery. Tissue-specific exclusion via intestine-specific Cre-lox drivers, as demonstrated by Browder and colleagues, is the established approach (Browder et al., 2022). Alternative strategies include: chemical reprogramming cocktails designed to spare the intestinal epithelium; systemic delivery modalities with minimal intestinal transduction (e.g., certain AAV serotypes with low gut tropism); and local application of rejuvenation agents to the colonic mucosa if intestinal-specific rejuvenation is desired, where the epithelial turnover already provides a natural rejuvenation-like reset.

### 3.6 Skeletal Muscle — Satellite Cell Reactivation and Niche Remodeling

Skeletal muscle regeneration depends on satellite cells — tissue-resident stem cells that occupy a quiescent (G0) niche between the sarcolemma and basal lamina of myofibers. With aging, satellite cells decline in both number and function, with geriatric muscle stem cells switching from reversible quiescence to an irreversible pre-senescent state driven by derepression of p16^INK4a (Cdkn2a) (Sousa-Victor et al., 2014). On injury, these aged satellite cells fail to activate and undergo full senescence even when transplanted into a youthful environment, establishing a cell-intrinsic barrier to muscle repair.

Partial reprogramming addresses this barrier through an unexpected mechanism: niche remodeling rather than direct satellite cell reprogramming. Wang and colleagues showed that local OSKM expression specifically in myofibers — not in satellite cells themselves — activates satellite cell proliferation and accelerates muscle regeneration (Wang et al., 2021). The mechanism is paracrine: OSKM upregulates p21 in myofibers, which downregulates Wnt4, a secreted factor that normally maintains satellite cell quiescence. By reprogramming the niche signaling environment, OSKM indirectly rejuvenates the stem cell population without ever entering the stem cells — a principle with important implications for whole-body strategies where direct stem cell transduction may not be required.

A more recent discovery reveals that the aged muscle niche deterioration has epigenetic origins in the stem cells themselves. Riparini and colleagues demonstrated that reduced H3K27me3 at the Nfkb1 gene in aged muscle stem cells correlates with increased IL-6 and Spp1 secretion, which instructs fibro-adipogenic progenitors (FAPs) to proliferate and acquire a fibrogenic phenotype (Riparini et al., 2025). This creates a feed-forward fibrotic cycle in which epigenetic erosion in stem cells propagates to the niche via inflammatory signaling, recruiting mesenchymal drift in the surrounding tissue — a direct connection between the cellular reprogramming deficit and the organism-wide mesenchymal drift phenotype described in Section 4.

For skeletal muscle, optimal rejuvenation strategies include: local AAV-OSK delivery targeting myofibers (to remodel the niche); systemic partial reprogramming at doses safe for the organ (muscle is moderately tolerant of cyclic OSKM); and combination with pharmacological p16 suppression to restore satellite cell quiescence in the geriatric population. The muscle represents a "medium-competence" tissue where standard cyclic reprogramming protocols achieve meaningful benefit without tissue-specific modifications, though outcomes could be significantly improved with niche-targeted approaches.

### 3.7 Blood and Immune System — The Clonal Selection Minefield

The hematopoietic system presents a qualitatively distinct challenge for reprogramming: the dominant safety concern is not tissue failure from dedifferentiation (as in liver and intestine) but oncogenic transformation driven by the interaction between reprogramming factors and pre-existing somatic mutations.

Hematopoietic stem cells (HSCs) are among the most actively dividing stem cells in the body, acquiring approximately 17 base substitutions per year genome-wide and approximately 14 per year in coding regions (Lee-Six et al., 2018; Mitchell et al., 2022). By age 70, the cumulative mutation burden is substantial, and in a significant fraction of individuals, one or more HSC clones carrying driver mutations have expanded to constitute a measurable fraction of blood cells — a phenomenon termed clonal hematopoiesis of indeterminate potential (CHIP). CHIP prevalence increases steeply with age: 9.5% at ages 70–79, 11.7% at 80–89, and 18.4% at 90–108, with the most common mutations occurring in the epigenetic regulators DNMT3A and TET2, the splicing factors U2AF1, SRSF2, and SF3B1, and the DNA damage response genes PPM1D and TP53 (Jaiswal et al., 2014). CHIP doubles the risk of atherosclerotic cardiovascular disease and carries an 11-fold increased risk of hematological malignancy (Jaiswal et al., 2017).

The interaction between CHIP mutations and reprogramming factors creates a uniquely dangerous landscape. DNMT3A and TET2 mutations directly modify the epigenetic machinery that OSK depends on to remodel chromatin: DNMT3A loss-of-function reduces de novo DNA methylation, potentially facilitating inappropriate gene activation during reprogramming, while TET2 loss impairs demethylation at loci requiring reactivation. These mutations also create a chronic inflammatory bone marrow microenvironment that both promotes clonal expansion and alters the signaling context in which reprogramming occurs. Most critically, TP53-mutant HSCs respond to reprogramming signals by forming undifferentiated malignant tumors rather than benign teratomas — an outcome categorically worse than the normal oncogenic risk of OSKM (Chen et al., 2025a). The molecular mechanism involves mutant p53 dysregulating pre-mRNA splicing in HSPCs, leading to enhanced NF-κB activation and increased IL-1β and IL-6 secretion that generates a chronic inflammatory microenvironment conferring competitive advantage to the mutant clone (Chen et al., 2025a).

The most alarming finding from recent clonal dynamics studies is that hematopoiesis in individuals over 75 is often dominated by 10–20 expanded clones, representing a dramatic shift from the highly polyclonal architecture of youth (Mitchell et al., 2022). This oligoclonal collapse means that systemic reprogramming in elderly individuals would disproportionately affect cells already carrying driver mutations — precisely the population in which reprogramming is most dangerous.

For the blood and immune system, the only acceptable approach is ex vivo reprogramming with mandatory pre-treatment somatic mutation profiling. Patients with high-risk CHIP mutations (TP53, PPM1D) should be excluded from any protocol that exposes HSCs to reprogramming factors. For patients with lower-risk CHIP (DNMT3A, TET2), ex vivo protocols with rigorous clonal monitoring may be feasible, but in vivo blood reprogramming — whether via systemic AAV or LNP delivery — should be considered contraindicated until the mutation-reprogramming interaction is better characterized.

### 3.8 Skin and Fibroblasts — The Accessible Model System

The skin occupies the opposite end of the accessibility spectrum from the brain: it is the most studied, most accessible, and most forgiving tissue for reprogramming interventions. Human dermal fibroblasts served as the original substrate for Takahashi and Yamanaka's discovery of induced pluripotency, and they remain the workhorse model for evaluating reprogramming efficiency, safety, and rejuvenation endpoints.

Multiple modalities achieve skin rejuvenation. The 13-day maturation phase transient reprogramming protocol, in which fibroblasts are exposed to OSKM and then returned to standard culture during the "maturation phase" before pluripotency commitment, rejuvenates cells by approximately 30 years on the epigenetic clock while retaining fibroblast identity, confirmed by functional wound-healing assays (Gill et al., 2022). Chemical reprogramming with a seven-compound (7C) cocktail ameliorates cellular hallmarks of aging including genomic instability, epigenetic alterations, cellular senescence, and oxidative stress; a reduced two-compound (2C) cocktail retains these rejuvenating effects and extends median lifespan by over 42% in *C. elegans* (Schoenfeldt et al., 2025). Multi-omics profiling of the chemical approach revealed that rejuvenation reverses accumulation of aging-related metabolites and mis-spliced mRNA, with upregulation of mitochondrial OXPHOS as the dominant signature (Mitchell et al., 2024).

The skin is also the testing ground for novel single-factor approaches. The SB000 factor, identified by Shift Bioscience through screening 1,500 candidate genes against a transcriptomic aging clock (AC3), achieves multi-germ-layer rejuvenation rivaling the Yamanaka factors while maintaining somatic identity without evidence of pluripotency. Partially reprogrammed aged fibroblasts, when implanted in vivo, show enhanced ECM protein expression (collagen, elastin, fibronectin) and improved wound healing in aged tissue models (Roy et al., 2024).

The skin's clinical accessibility enables topical delivery strategies impossible for internal organs. Chemical cocktails, nanoparticle formulations, and even transdermal factor delivery are feasible for dermal rejuvenation, making the skin the ideal first target after the eye for clinical translation. However, the skin's permissive reprogramming profile also means that results obtained in fibroblasts may not transfer to more resistant tissues — a limitation that has historically led to overoptimistic predictions about the ease of whole-body reprogramming.

---

## 4. Mesenchymal Drift: A Unifying Reversible Aging Signature

### 4.1 Discovery and Characterization

Across the eight organ systems profiled in Section 3, a common theme emerges: aging tissues progressively acquire mesenchymal characteristics — enhanced extracellular matrix synthesis leading to fibrosis, damage to intercellular junction structures compromising tissue integrity, and abnormal secretion of pro-inflammatory factors. Lu and colleagues formalized this observation as **mesenchymal drift (MD)**, demonstrating through analysis of gene expression data from over 40 human tissues and 20 diseases that there is a pervasive upregulation of mesenchymal genes across multiple cell types during aging (Lu et al., 2025). Increased MD correlates with disease progression, reduced patient survival, and elevated mortality risk across diverse pathological contexts including pulmonary fibrosis, liver cirrhosis, cardiac fibrosis, renal disease, and neurodegeneration.

MD is not a simple consequence of fibroblast accumulation; rather, it reflects a transcriptional identity erosion in which epithelial, endothelial, and specialized parenchymal cells progressively express mesenchymal gene programs that are normally restricted to fibroblasts and smooth muscle cells. The molecular drivers include TGFβ/SMAD signaling (activated by matrix stiffening), chronic inflammatory cytokines (IL-1, IL-6/STAT3 from SASP-secreting senescent cells), and YAP/TAZ activation (by mechanical forces in stiffened ECM) — creating self-reinforcing positive feedback loops that accelerate MD over time (de Lima Camillo, 2025). Endothelial-to-mesenchymal transition (EndoMT) weakens barrier function through loss of VE-cadherin; macrophage-to-myofibroblast conversion amplifies fibrosis; and epithelial cells in the lung, kidney, and liver progressively acquire mesenchymal markers while losing their tissue-specific functions.

### 4.2 Reversal by Partial Reprogramming

The most significant finding of the Lu et al. study is that partial reprogramming markedly reduces mesenchymal drift before cells reach the dedifferentiation threshold — identifying a temporal window in which rejuvenation occurs without identity loss (Lu et al., 2025). Specifically, the early phase of OSKM-induced reprogramming is characterized by rapid downregulation of mesenchymal genes (within the first days of factor expression), while reprogramming-associated epithelial genes only begin to upregulate later. This asymmetric kinetics creates a window of "mesenchymal erasure without epithelial activation" — a period of pure rejuvenation that precedes the dangerous mesenchymal-to-epithelial transition (MET) associated with dedifferentiation.

Two engineered factor variants exploit this window. First, removal of the oncogene c-MYC (using OSK rather than OSKM) preserves MD suppression while lowering oncogenic potential — the same modification used in the ER-100 clinical candidate. Second, an **OCT4-YR mutant** engineered to be unable to dimerize with SOX2 retains the ability to suppress mesenchymal drift without activating NANOG or inducing pluripotency (Lu et al., 2025). This remarkable separation of the MD-reversal function from the pluripotency-induction function of OCT4 demonstrates that the rejuvenation and dedifferentiation programs are mechanistically distinct and independently targetable.

### 4.3 MD as a Convergent Therapeutic Target

The universality of mesenchymal drift across tissues suggests that it may serve as both a biomarker and a therapeutic target for tissue-stratified rejuvenation. Regardless of whether a given tissue receives OSK, single-factor EZH2, chemical cocktails, or senescent-cell-targeted reprogramming, the common endpoint should be MD reversal — assessed by transcriptomic measurement of mesenchymal gene expression relative to age-matched and young-reference profiles. This framing offers a unifying metric for comparing the efficacy of different modalities across different tissues, resolving the current absence of a common rejuvenation endpoint that applies across all organ systems.

Conserved biological processes identified in partial cellular reprogramming — dynamic chromatin remodeling, stress response program modification (inflammation, autophagy, senescence), improved mitochondrial activity, and ECM pathway dysregulation — are consistently observed across in vitro and in vivo mouse studies and in vitro human studies, though the magnitude and kinetics are context-dependent, varying by cell type, species, sex, and reprogramming method (Avelar et al., 2025). The convergence of these programs on MD reversal provides mechanistic coherence to a field that has sometimes appeared heterogeneous.

---

## 5. Beyond OSK: Tissue-Specific Rejuvenation Factors

### 5.1 Single Transcription Factor Perturbations

The assumption that effective rejuvenation requires the full Yamanaka cocktail is now challenged by systematic screening approaches. The Transcriptional Rejuvenation Discovery Platform (TRDP) developed by Sengstack and colleagues used Perturb-seq and combined CRISPRa/CRISPRi screens to evaluate 200 transcription factors for rejuvenation capacity in aged fibroblasts, identifying four validated hits: overexpression of **EZH2** or **E2F3**, and repression of **STAT3** or **ZFX** (Sengstack et al., 2026). Each perturbation independently reversed cellular hallmarks of aging — increasing proliferation, proteostasis, and mitochondrial activity while decreasing senescence — and all four converged on shared downstream transcriptional programs conserved across different aging and rejuvenation models.

The liver-specific significance of EZH2 is discussed in Section 3.4. The broader implication is that the optimal rejuvenation factor may differ by tissue: EZH2 for the liver, OSK for the eye, chemical cocktails for the skin, and as-yet-unidentified single factors for the brain and heart. The Cell Rejuvenation Atlas, which characterized the effects of six rejuvenation strategies across nine studies on 73 cell types, identified **Arntl** (a circadian transcription factor) as the master regulator with the most significant age-related decline in activity, alongside stress response regulators NFE2L2 and MAF (Arcos Hodar et al., 2024). Catalytically inactive EZH2 mutants achieve rejuvenation comparable to wild-type EZH2, suggesting mechanisms distinct from canonical H3K27me3-mediated gene silencing — potentially including structural roles in chromatin organization or protein-protein interactions independent of methyltransferase activity.

### 5.2 Chemical Reprogramming as a Tissue-Accessible Alternative

Small-molecule reprogramming cocktails offer several translational advantages over genetic factor delivery: cell permeability without viral transduction, dose-modulatable pharmacokinetics, transient and reversible effects, and established pharmaceutical manufacturing pathways. The seven-compound (7C) cocktail — comprising valproic acid (HDAC inhibitor), CHIR99021 (GSK3 inhibitor), 616452 (TGFβ inhibitor), tranylcypromine (LSD1 inhibitor), forskolin (cAMP agonist), DZNep (SAH hydrolase inhibitor), and TTNPB (RAR agonist) — was originally developed for mouse chemically induced pluripotent stem cell generation (Hou et al., 2013) and subsequently adapted for human cells through a sequential four-stage protocol (Guan et al., 2022).

For rejuvenation specifically, chemical approaches may be superior to genetic ones for high-competence tissues. The 7C cocktail achieves more pronounced metabolomic changes than the reduced 2C variant (Mitchell et al., 2024), but even 2C is sufficient to reverse major aging hallmarks and extend organismal lifespan. Importantly, comparative analysis of genetic versus chemical reprogramming revealed that chemical approaches induce less cellular stress, produce more homogeneous outcomes, and achieve greater p21 reduction with less p16 induction — a more favorable safety profile for tissues where avoiding senescence induction is critical (Cheng et al., 2025).

### 5.3 Tissue-Specific Factor Selection Principles

The emerging data support a principle of tissue-factor matching based on reprogramming competence:

- **High-competence tissues (liver, intestine)**: Single-factor approaches (EZH2 for liver) or tissue exclusion. Multi-factor reprogramming is contraindicated due to excessive dedifferentiation risk.
- **Medium-competence tissues (muscle, blood)**: OSK cyclic protocols at moderate doses; ex vivo for blood with mutation screening; niche-remodeling approaches for muscle.
- **Low-competence tissues (brain, heart)**: Continuous OSK for months (brain) or ultra-short OSKM pulses of 3–6 days (heart). Alternative single-factor approaches (PHF7 for heart) and senescent-cell-targeted promoters (Cdkn2a-driven for brain) may expand the therapeutic window.
- **Accessible tissues (skin, eye)**: Direct local delivery of OSK (eye) or chemical cocktails (skin) with established safety profiles.

This stratified framework replaces the one-size-fits-all approach with a multi-modality strategy in which the choice of factor, dose, duration, and delivery route is optimized per organ system.

---

## 6. The Safety Architecture: Tissue-Specific Oncogenic Risk

### 6.1 p53-Dependent Quality Control Across Tissues

The p53 tumor suppressor network constitutes the primary safety checkpoint during reprogramming, but its stringency varies dramatically across tissues. In the heart, additional tissue-specific barriers (P-TEFb deficiency, sarcomere lock) neutralize c-Myc's oncogenic potential before p53 is even engaged — making cardiac reprogramming inherently safer from an oncogenic perspective, though dangerous for other reasons (dedifferentiation). In contrast, the liver lacks these additional barriers: p53 is the sole line of defense against factor-driven proliferation, and its inactivation — whether by somatic mutation or pharmacological inhibition — rapidly converts partial reprogramming into malignant transformation.

### 6.2 CHIP as a Patient-Specific Risk Modifier

Clonal hematopoiesis creates patient-specific oncogenic risk that cannot be assessed from tissue type alone. A 70-year-old with no detectable CHIP has a fundamentally different risk profile from one with TP53 or PPM1D CHIP — yet both would receive the same systemic reprogramming dose under current one-size-fits-all protocols. The oligoclonal collapse of hematopoiesis in individuals over 75, with blood production dominated by 10–20 expanded mutant clones (Mitchell et al., 2022), means that systemic reprogramming in the elderly disproportionately targets mutation-bearing cells. Pre-treatment somatic mutation profiling — achievable through inexpensive targeted sequencing panels — should be a mandatory prerequisite for any systemic reprogramming intervention.

### 6.3 The Senescence-Reprogramming Equilibrium

Aging can be conceptualized as a shift in the senescence-reprogramming equilibrium: accumulated senescent cells and epigenetic noise suppress regenerative reprogramming capacity, while strategic interventions can restore some youthful reprogramming potential to enable tissue rejuvenation (Ding et al., 2025). This equilibrium operates differently across tissues. In the skin, where senescent cells are relatively accessible to clearance, sequential senolytic treatment followed by partial reprogramming may achieve synergistic effects. In the brain, where senescent neurons are embedded in functional circuits and cannot be simply eliminated, senescent-cell-specific reprogramming (via Cdkn2a-driven OSK) offers a more nuanced approach. In the blood, the entanglement of senescence with clonal hematopoiesis creates a more complex landscape where senolytics might inadvertently select for CHIP clones.

### 6.4 Dose-Duration Safety Windows

The following tissue-specific safety boundaries emerge from the accumulated evidence:

| Tissue | Maximum Safe Duration (Continuous) | Maximum Safe Duration (Cyclic 2d/5d) | Factor Restriction |
|--------|----------------------------------|--------------------------------------|-------------------|
| Eye | >18 months | Not required | OSK (no Myc) |
| Brain | ~39 days demonstrated | Unknown | OSK, senescent-cell promoter preferred |
| Heart | 6 days | Not applicable | OSKM ultra-short; GMT or PHF7 preferred |
| Liver | <7 days (dangerous) | ~10 months with low expression | Single factor (EZH2) only |
| Intestine | <7 days (lethal) | Only if excluded via Cre-lox | Excluded from systemic protocols |
| Muscle | Weeks (local) | ~10 months systemic | OSK, myofiber-targeted preferred |
| Blood | Not applicable | Not applicable | Ex vivo only with mutation screening |
| Skin | Weeks | Months | Chemical, single factor, or topical |

---

## 7. Quantitative Framework: Multi-Tissue Constrained Optimization

### 7.1 Framework F283: Tissue-Specific Dose-Response Function

We formalize the tissue-specific response to reprogramming as a coupled pair of functions: a rejuvenation function $R_i(d_i, t_i)$ and an oncogenic risk function $O_i(d_i, t_i)$, where $d_i$ is the effective dose (factor expression level integrated over time) and $t_i$ is the duration of exposure for tissue $i$.

The rejuvenation response follows a sigmoidal dose-response:

```math
R_i(d_i) = \frac{R_{i,\max}}{1 + \left(\frac{EC_{50,i}}{d_i}\right)^{n_i}}
```

where $R_{i,\max}$ is the maximum achievable rejuvenation (in epigenetic clock years reversed) for tissue $i$, $EC_{50,i}$ is the dose at which half-maximal rejuvenation is achieved, and $n_i$ is the Hill coefficient capturing the steepness of the dose-response curve.

The oncogenic risk function captures the observation that risk increases superlinearly at high doses:

```math
O_i(d_i, t_i) = \alpha_i \cdot d_i^{\beta_i} \cdot t_i^{\gamma_i} \cdot (1 + \mu_i \cdot M_i)
```

where $\alpha_i$ is a tissue-specific baseline risk coefficient, $\beta_i$ and $\gamma_i$ are dose and duration exponents (empirically $\beta_i > 1$ for high-competence tissues reflecting superlinear dedifferentiation kinetics), and $M_i$ is the somatic mutation burden in tissue $i$, weighted by the mutation risk factor $\mu_i$ (highest for blood where CHIP mutations directly modify epigenetic machinery).

The **tissue-specific therapeutic index** is defined as:

```math
TI_i = \frac{\max_{d_i, t_i} R_i(d_i, t_i)}{\min_{d_i, t_i : R_i > R_{\min}} O_i(d_i, t_i)}
```

This ratio quantifies the maximum achievable rejuvenation relative to the minimum oncogenic risk required to achieve a clinically meaningful rejuvenation threshold $R_{\min}$. Empirical estimates suggest $TI_{\text{eye}} \gg TI_{\text{skin}} > TI_{\text{muscle}} > TI_{\text{brain}} > TI_{\text{heart}} > TI_{\text{blood}} > TI_{\text{liver}} \approx TI_{\text{intestine}}$, reflecting the ordering in Table 1.

### 7.2 Framework F284: Multi-Tissue Pareto Optimization

whole-body reprogramming requires simultaneously optimizing across $N$ tissues, each with its own dose-response and risk function. The optimization problem is:

```math
\max_{\{d_i, t_i, m_i\}_{i=1}^N} \sum_{i=1}^{N} w_i \cdot R_i(d_i, t_i, m_i)
```

subject to the safety constraints:

```math
O_i(d_i, t_i, m_i) \leq \theta_i \quad \forall \, i \in \{1, \ldots, N\}
```

where $m_i \in \mathcal{M}$ denotes the choice of reprogramming modality for tissue $i$ (e.g., OSK continuous, OSK cyclic, EZH2 single factor, chemical 7C, chemical 2C, excluded), $w_i$ is the clinical importance weight for tissue $i$, and $\theta_i$ is the maximum acceptable oncogenic risk threshold for tissue $i$.

The key insight is that the constraint set is **tissue-specific**: different tissues have different risk thresholds $\theta_i$, and the same modality $m$ achieves different risk-rejuvenation profiles in different tissues. A single-modality approach (e.g., systemic cyclic OSK for all tissues) constrains all $d_i$ and $t_i$ to be coupled through shared pharmacokinetics, forcing the optimization to respect the most sensitive tissue's constraint — effectively limiting whole-body reprogramming to the lowest-common-denominator dose. Multi-modality approaches (different factors/routes per tissue) decouple the tissue-specific optimization variables, accessing a much larger region of the Pareto frontier.

The Pareto frontier represents the set of solutions where no tissue's rejuvenation can be increased without either increasing another tissue's oncogenic risk or decreasing another tissue's rejuvenation. We predict that single-modality approaches occupy only a small fraction of the Pareto-optimal surface, while tissue-stratified multi-modality strategies access rejuvenation depths 3–10-fold greater under equivalent aggregate safety constraints.

### 7.3 Framework F285: Reprogramming Competence Composite Score

We define a tissue-specific reprogramming competence score $C_i$ as a weighted linear combination of measurable molecular features:

```math
C_i = w_1 \cdot A_i + w_2 \cdot F_i + w_3 \cdot P_i - w_4 \cdot M_i - w_5 \cdot S_i
```

where:
- $A_i$ = chromatin accessibility index (fraction of OSK/pioneer factor motifs in ATAC-seq peaks, normalized to fibroblast reference)
- $F_i$ = cycling fraction (proportion of cells in S/G2/M by flow cytometry or scRNA-seq cell cycle scoring)
- $P_i$ = pioneer factor co-factor availability (P-TEFb expression level, Mediator complex occupancy)
- $M_i$ = somatic mutation burden (SNVs per megabase, weighted by driver mutation presence)
- $S_i$ = senescent cell fraction (p16+ or SA-β-gal+ cells as proportion of total)

The weights $\{w_1, \ldots, w_5\}$ can be estimated by linear discriminant analysis or logistic regression on empirical reprogramming outcome data across tissues, with the binary outcome being "successful rejuvenation without oncogenic transformation." This score provides a pre-treatment predictor of tissue response, enabling patient-specific optimization of the tissue-stratified protocol based on biopsy or circulating biomarker data.

---

## 8. Proposed Experiment: Multi-Tissue Reprogramming Atlas

### 8.1 Rationale

No existing dataset provides tissue-specific dose-response functions for partial reprogramming across multiple organs, doses, timepoints, and modalities. The experiments reviewed in Section 3 are predominantly single-tissue, single-dose, single-modality studies that cannot be directly compared due to differences in mouse strains, transgene systems, ages at treatment, and readout methods. A systematic multi-tissue reprogramming atlas is the rate-limiting dataset for enabling rational tissue-stratified protocol design.

### 8.2 Experimental Design

We propose a factorial experiment in 12-month-old C57BL/6J mice (corresponding to approximately 40 human-equivalent years) using three reprogramming modalities:

- **Modality 1**: Systemic doxycycline-inducible OSK/OSKM (Col1a1::tetOP-OSKM; Rosa26-rtTA) at three dose levels (low, medium, high doxycycline concentration)
- **Modality 2**: AAV8-mediated liver-specific EZH2 overexpression at three titers
- **Modality 3**: Systemic 2C chemical cocktail at three concentrations

For each modality × dose combination, tissues are harvested at five timepoints: baseline (day 0), day 1, day 3, day 7, and day 14.

**Tissues collected**: retina, hippocampus, heart (left ventricle), liver, small intestine (jejunal crypts), tibialis anterior muscle, bone marrow (whole and sorted HSCs), and dorsal skin.

### 8.3 Readouts

Each tissue sample is processed for:

1. **Single-cell RNA-seq** (10x Chromium): transcriptomic age (tissue-specific clocks where available), mesenchymal drift score (MD gene signature), cell identity retention (correlation with young-reference atlas), senescence markers (p16, p21, SASP genes), oncogenic markers (Myc targets, cell cycle, telomerase)
2. **Single-cell ATAC-seq** (10x Multiome): chromatin accessibility at OSK target loci, pioneer factor motif accessibility, tissue-specific enhancer activity
3. **Reduced representation bisulfite sequencing (RRBS)**: DNA methylation at epigenetic clock CpGs, tissue-specific regulatory regions, imprinting control regions
4. **Histopathology**: H&E, Ki67 (proliferation), cleaved caspase-3 (apoptosis), p53 (activation), teratoma markers

### 8.4 Computational Analysis

The primary output is a set of tissue-specific dose-response functions: $R_i(d, t)$ and $O_i(d, t)$ for each tissue $i$, modality, and readout. These are fit to the sigmoidal/power-law models of Framework F283, with parameters estimated by maximum likelihood. The reprogramming competence score (Framework F285) is computed for each tissue at baseline and validated against observed reprogramming outcomes. The Pareto frontier (Framework F284) is computed numerically to identify optimal multi-modality tissue-stratified protocols.

### 8.5 Expected Outcomes and Clinical Application

We predict that: (1) liver and intestine will show the steepest dose-response curves with the narrowest safety margins (high $n_i$, low $EC_{50,i}$, high $\alpha_i$); (2) brain and heart will show shallow dose-response curves requiring sustained exposure for meaningful rejuvenation (low $n_i$, high $EC_{50,i}$); (3) EZH2 will achieve liver rejuvenation comparable to OSKM at dramatically lower oncogenic risk; (4) chemical reprogramming will show a more favorable safety profile than genetic approaches for high-competence tissues; and (5) the multi-modality Pareto frontier will dramatically exceed the single-modality frontier, quantitatively justifying the tissue-stratified approach.

The resulting atlas would enable evidence-based design of clinical protocols in which: the liver receives EZH2 via liver-tropic AAV; the eye receives intravitreal OSK; the brain receives senescent-cell-targeted OSK via intrathecal delivery; the heart is treated only after acute MI with ultra-short OSKM; the intestine is excluded; skeletal muscle receives systemic cyclic OSK at moderate doses; the blood is treated ex vivo; and the skin receives topical chemical cocktails. Each modality is calibrated to its tissue's measured dose-response function, achieving the Pareto-optimal balance of whole-body reprogramming and safety.

---

## 9. Open Questions and Future Directions

1. **Can tissue-targeted delivery alone solve incompatibility?** If AAV serotype engineering or LNP surface modification achieves sufficient organ tropism, can a single factor be delivered differentially to each tissue at its optimal dose — or will the overlapping biodistribution of all delivery systems force multi-modality approaches?

2. **Inter-organ communication and rejuvenation propagation.** Does rejuvenating one organ propagate benefits to others through circulating factors, exosomes, or improved blood composition? The mesenchymal drift framework predicts that reversing MD in a secretory organ (liver) may reduce inflammatory signaling to downstream tissues — a potential "rejuvenation cascade" that could simplify tissue-stratified protocols.

3. **Is mesenchymal drift reversal sufficient for functional rejuvenation?** MD is a transcriptomic signature, but its functional consequences — fibrosis, barrier loss, inflammation — are the proximate causes of tissue dysfunction. Does reversing the transcriptomic signature reliably reverse the functional phenotype, or are there irreversible structural changes (e.g., ECM crosslinks, advanced glycation end-products) that persist even after cellular rejuvenation?

4. **Patient-specific optimization.** Individual variation in CHIP status, tissue-specific mutation burden, epigenetic age acceleration, and microbiome composition will produce patient-specific reprogramming competence profiles. Incorporating these variables into the multi-tissue optimization framework (F284) would enable personalized rejuvenation protocols — but requires biomarkers that can be assessed non-invasively.

5. **The tissue-specific epigenetic clock problem.** Current epigenetic clocks are predominantly trained on blood methylation data and show poor cross-tissue concordance, with average differences of nearly 30 years between oral and blood tissues using some clocks (Apsley et al., 2025). Meaningful assessment of tissue-stratified rejuvenation will require validated organ-specific clocks for each target tissue — a measurement infrastructure that does not yet exist.

6. **Safety monitoring at whole-body scale.** How will clinicians detect early signs of tissue-specific adverse effects in organs that cannot be easily biopsied? Liquid biopsy approaches (cell-free DNA methylation, circulating SASP biomarkers, organ-specific protein panels) may provide minimally invasive monitoring, but their sensitivity for detecting early reprogramming-associated pathology is unknown.

7. **Combinatorial strategies.** The interaction between senolytics, partial reprogramming, and metabolic interventions (caloric restriction, NAD+ precursors) has been explored only in isolation. Optimal whole-body reprogramming may require sequential multi-modal therapy: senolytic clearance first, followed by tissue-stratified reprogramming, followed by metabolic support for sustained rejuvenation. The optimal sequencing and timing of such combined protocols remains entirely unexplored.

---

## References

1. Apsley, A. T., Ye, Q., Caspi, A., Chiaro, C., Etzel, L., Hastings, W. J., Heim, C. M., Kozlosky, J., Noll, J. G., Schreier, H. M. C., Shenk, C. E., Sugden, K., & Shalev, I. (2025). Cross-tissue comparison of epigenetic aging clocks in humans. *Aging Cell*, 24(4), e14451. PMID: 39780748

2. Arcos Hodar, J., Jung, S., Soudy, M., Barvaux, S., & Del Sol, A. (2024). The cell rejuvenation atlas: leveraging network biology to identify master regulators of rejuvenation strategies. *Aging*, 16(17), 12168–12190. PMID: 39264584

3. Avelar, R. A., Palmer, D., Kulaga, A. Y., & Fuellen, G. (2025). Conserved biological processes in partial cellular reprogramming: Relevance to aging and rejuvenation. *Ageing Research Reviews*, 108, 102737. PMID: 40122394

4. Ayyaz, A., Kumar, S., Sangiorgi, B., Ghoshal, B., Gosio, J., Ouladan, S., Fink, M., Barutcu, S., Trcka, D., Shen, J., Chan, K., Wrana, J. L., & Gregorieff, A. (2019). Single-cell transcriptomes of the regenerating intestine reveal a revival stem cell. *Nature*, 569, 121–125. PMID: 31019301

5. Browder, K. C., Reddy, P., Yamamoto, M., Haghani, A., Guillen Guillen, I., Sahu, S., Wang, C., Luque, Y., Prieto, J., Shi, L., Shojima, K., Hishida, T., Lai, Z., Li, Q., Choudhury, F. K., Wong, W. R., Liang, Y., Sangaraju, D., Sandoval, W., … Izpisua Belmonte, J. C. (2022). In vivo partial reprogramming alters age-associated molecular changes during physiological aging in mice. *Nature Aging*, 2, 243–253. PMID: 37118377

6. Chen, S., Barajas, S., Vemula, S., Yang, Y., et al. (2025a). Mutant p53 promotes clonal hematopoiesis by generating a chronic inflammatory microenvironment. *Journal of Clinical Investigation*. PMID: 41468163

7. Chen, Y., Luttmann, F. F., Schoger, E., Scholer, H. R., Zelarayan, L. C., Kim, K. P., … Engel, F. B. (2021). Reversible reprogramming of cardiomyocytes to a fetal state drives heart regeneration in mice. *Science*, 373(6550), 1537–1540. PMID: 34554778

8. Cheng, L., Wang, Y., Guan, J., & Deng, H. (2025). Decoding human chemical reprogramming: mechanisms and principles. *Trends in Biochemical Sciences*, 50(6), 520–531. PMID: 40169299

9. Chondronasiou, D., Gill, D., Mosteiro, L., Urdinguio, R. G., Berenguer-Llergo, A., Aguilera, M., Durand, S., Aprahamian, F., Nirmalathasan, N., Abad, M., Martin-Herranz, D. E., Stephan-Otto Attolini, C., Prats, N., Kroemer, G., Fraga, M. F., Reik, W., & Serrano, M. (2022). Multi-omic rejuvenation of naturally aged tissues by a single cycle of transient reprogramming. *Aging Cell*, 21, e13578. PMID: 35235716

10. Cipriano, A., Moqri, M., Maybury-Lewis, S. Y., Rogers-Hammond, R., de Jong, T. A., Parker, A., Rasouli, S., Scholer, H. R., Sinclair, D. A., & Sebastiano, V. (2024). Mechanisms, pathways and strategies for rejuvenation through epigenetic reprogramming. *Nature Aging*, 4(1), 14–26. PMID: 38102454

11. de Lima Camillo, L. P. (2025). Inhibition of mesenchymal drift as a strategy for rejuvenation. *Frontiers in Pharmacology*, 16, 1715559. PMID: 41322283

12. Ding, F., Yu, Y., Zhao, J., Wei, S., Zhang, Y., Han, J. H., Li, Z., Jiang, H. B., Ryu, D., Cho, M., Bae, S. J., Park, W., Ha, K. T., & Gao, B. (2025). The interplay of cellular senescence and reprogramming shapes the biological landscape of aging and cancer revealing novel therapeutic avenues. *Frontiers in Cell and Developmental Biology*, 13, 1593096. PMID: 40356604

13. Fink, M., Njah, K., Patel, S. J., Cook, D. P., Man, V., Ruso, F., Rajan, A., Narimatsu, M., Obersterescu, A., Pye, M. J., Trcka, D., Chan, K., Ayyaz, A., & Wrana, J. L. (2024). Chromatin remodelling in damaged intestinal crypts orchestrates redundant TGFβ and Hippo signalling to drive regeneration. *Nature Cell Biology*, 26, 2084–2098. PMID: 39548329

14. Gill, D., Parry, A., Santos, F., Okkenhaug, H., Todd, C. D., Hernando-Herraez, I., Stubbs, T. M., Milagre, I., & Reik, W. (2022). Multi-omic rejuvenation of human cells by maturation phase transient reprogramming. *eLife*, 11, e71624. PMID: 35390271

15. Guan, J., Wang, G., Wang, J., Zhang, Z., Fu, Y., Cheng, L., Meng, G., Lyu, Y., Zhu, J., Li, Y., … Deng, H. (2022). Chemical reprogramming of human somatic cells to pluripotent stem cells. *Nature*, 605(7909), 325–331. PMID: 35418683

16. Herzog, C. M. S., Redl, E., Barrett, J., Aminzadeh-Gohari, S., Weber, D. D., Tevini, J., Lang, R., Kofler, B., & Widschwendter, M. (2025). Functionally enriched epigenetic clocks reveal tissue-specific discordant aging patterns in individuals with cancer. *Communications Medicine*, 5(1), 98. PMID: 40175686

17. Hishida, T., Yamamoto, M., Hishida-Nozaki, Y., Shao, C., Huang, L., Wang, C., … Izpisua Belmonte, J. C. (2022). In vivo partial cellular reprogramming enhances liver plasticity and regeneration. *Cell Reports*, 39(4), 110730. PMID: 35476977

18. Hou, P., Li, Y., Zhang, X., Liu, C., Guan, J., Li, H., Zhao, T., Ye, J., Yang, W., Liu, K., Ge, J., Xu, J., Zhang, Q., Zhao, Y., & Deng, H. (2013). Pluripotent stem cells induced from mouse somatic cells by small-molecule compounds. *Science*, 341(6146), 651–654. PMID: 23868920

19. Huang, G., Liu, C., et al. (2024). Asparagine synthetase marks a distinct dependency threshold for cardiomyocyte dedifferentiation. *Circulation*, 149(23), 1833–1851. PMID: 38586957

20. Jaiswal, S., Fontanillas, P., Flannick, J., Manning, A., Grauman, P. V., Mar, B. G., … Ebert, B. L. (2014). Age-related clonal hematopoiesis associated with adverse outcomes. *New England Journal of Medicine*, 371, 2488–2498. PMID: 25426837

21. Jaiswal, S., Natarajan, P., Silver, A. J., Gibson, C. J., Bick, A. G., Shvartz, E., … Ebert, B. L. (2017). Clonal hematopoiesis and risk of atherosclerotic cardiovascular disease. *New England Journal of Medicine*, 377, 111–121. PMID: 28636844

22. Jo, B. K., Lee, S. Y., Eom, H. J., Kim, J., & Cha, H. J. (2025). Organ-specific dedifferentiation and epigenetic remodeling in in vivo reprogramming. *Aging Cell*, 24(11), e70268. PMID: 41114535

23. Karg, M. M., Lu, Y. R., Refaian, N., Cameron, J., Hoffmann, E., Hoppe, C., … Ksander, B. R. (2023). Sustained vision recovery by OSK gene therapy in a mouse model of glaucoma. *Cellular Reprogramming*, 25(6), 288–299. PMID: 38060815

24. Kim, J., Kim, S., Lee, S. Y., Jo, B. K., Oh, J. Y., Kwon, E. J., … Cha, H. J. (2023). Partial in vivo reprogramming enables injury-free intestinal regeneration via autonomous Ptgs1 induction. *Science Advances*, 9(47), eadi8454. PMID: 38000027

25. Le, N., Awad, S., Palazzo, I., Hoang, T., & Blackshaw, S. (2025). Viral-mediated Pou5f1 (Oct4) overexpression and inhibition of Notch signaling synergistically induce neurogenic competence in mammalian Muller glia. *eLife*, 14, RP106450. PMID: 40388211

26. Lee-Six, H., Obro, N. F., Shepherd, M. S., Grossmann, S., Dawson, K., Belmonte, M., … Campbell, P. J. (2018). Somatic mutations reveal lineage relationships and age-related mutagenesis in human hematopoiesis. *Cell Reports*, 25(9), 2308–2316.e4. PMID: 30485801

27. Li, J., et al. (2025a). Enhancing cardiomyocyte reprogramming efficiency by targeting cellular senescence is mediated via Rb1 gene. *Stem Cell Research & Therapy*, 16, 685. PMID: 41462332

28. Li, Y., et al. (2025b). Cellular reprogramming by PHF7 enhances cardiac function following myocardial infarction. *Circulation*. PMID: 40631661

29. Li, Y. Y., & Tay, F. R. (2026). The epigenetic rejuvenation promise: Partial reprogramming as a therapeutic strategy for aging and disease. *Ageing Research Reviews*, 115, 103009. PMID: 41490578

30. Lu, Y., Brommer, B., Tian, X., Krishnan, A., Meer, M., Wang, C., … Sinclair, D. A. (2020). Reprogramming to recover youthful epigenetic information and restore vision. *Nature*, 588(7836), 124–129. PMID: 33268865

31. Lu, J. Y., Tu, W. B., Li, R., Weng, M., Sanketi, B. D., Yuan, B., Reddy, P., Rodriguez Esteban, C., & Izpisua Belmonte, J. C. (2025). Prevalent mesenchymal drift in aging and disease is reversed by partial reprogramming. *Cell*, 188(21), 5895–5911.e17. PMID: 40816266

32. Macip, C. C., Hasan, R., Hoznek, V., Kim, J., Lu, Y. R., Metzger, L. E., Sethna, S., & Davidsohn, N. (2024). Gene therapy-mediated partial reprogramming extends lifespan and reverses age-related changes in aged mice. *Cellular Reprogramming*, 26(1), 24–32. PMID: 38381405

33. Medeiros, F. A., Varma, A., Jammal, A. A., Tseng, H., & Scott, W. K. (2025). Accelerated epigenetic aging is associated with faster glaucoma progression: a DNA methylation study. *Ophthalmology*, 132(5), 550–560. PMID: 39716635

34. Mitchell, E., Spencer Chapman, M., Williams, N., Dawson, K. J., Mende, N., Calderbank, E. F., … Campbell, P. J. (2022). Clonal dynamics of haematopoiesis across the human lifespan. *Nature*, 606, 343–350. PMID: 35650442

35. Mitchell, W., Goeminne, L. J. E., Tyshkovskiy, A., Zhang, S., Chen, J. Y., Paulo, J. A., … Gladyshev, V. N. (2024). Multi-omics characterization of partial chemical reprogramming reveals evidence of cell rejuvenation. *eLife*, 12, RP90579. PMID: 38517750

36. Monroe, T. O., Hill, M. C., Morikawa, Y., Leach, J. P., Heallen, T., Cao, S., … Martin, J. F. (2024). YAP overcomes mechanical barriers to induce mitotic rounding and adult cardiomyocyte division. *Circulation*, 150(10), 791–805. PMID: 39392007

37. Moreno-Jimenez, E. P., Terreros-Roncal, J., Flor-Garcia, M., Rabano, A., & Llorens-Martin, M. (2025). Cognitive rejuvenation in old rats by hippocampal OSKM gene therapy. *GeroScience*, 47(1), 809–823. PMID: 39037528

38. Nikopoulou, C., Kleinenkuhnen, N., Parekh, S., Sandoval, T., Ziegenhain, C., Schneider, F., … Tessarz, P. (2023). Spatial and single-cell profiling of the metabolome, transcriptome and epigenome of the aging mouse liver. *Nature Aging*, 3, 1430–1445. PMID: 37946043

39. Ocampo, A., Reddy, P., Martinez-Redondo, P., Platero-Luengo, A., Hatanaka, F., Hishida, T., … Izpisua Belmonte, J. C. (2016). In vivo amelioration of age-associated hallmarks by partial reprogramming. *Cell*, 167(7), 1719–1733.e12. PMID: 27984723

40. Paine, P. T., Nguyen, A., & Ocampo, A. (2024). Partial cellular reprogramming: A deep dive into an emerging rejuvenation technology. *Aging Cell*, 23(2), e14039. PMID: 38040663

41. Parras, A., Vilchez-Acosta, A., Desdin-Mico, G., Pico, S., Mrabti, C., Montenegro-Borbolla, E., … Ocampo, A. (2023). In vivo reprogramming leads to premature death linked to hepatic and intestinal failure. *Nature Aging*, 3, 1509–1520. PMID: 38012287

42. Pico, S., Vilchez-Acosta, A., Agostinho de Sousa, J., Maza, M. C., et al. (2025). Comparative analysis of mouse strains for in vivo induction of reprogramming factors. *Cell Reports*, 44(7), 115879. PMID: 40560729

43. Richardson, M., Brandt, C., Jain, N., Li, J. L., Demanelis, K., Jasmine, F., Kibriya, M. G., Tong, L., & Pierce, B. L. (2025). Characterization of DNA methylation clock algorithms applied to diverse tissue types. *Aging*, 17(1), 67–96. PMID: 39754638

44. Riparini, G., Mackenzie, M., Naz, F., Brooks, S., Jiang, K., Deewan, A., … Sartorelli, V. (2025). Epigenetic dysregulation in aged muscle stem cells drives mesenchymal progenitor expansion via IL-6 and Spp1 signaling. *Nature Aging*, 5, 2399–2416. PMID: 41162675

45. Rose, M., & Adashi, E. Y. (2025). Targeted partial reprogramming as a novel therapeutic strategy for age-related decline. *Ageing Research Reviews*, 108, 102731. PMID: 40096911

46. Roy, B., Pekec, T., Yuan, L., & Shivashankar, G. V. (2024). Implanting mechanically reprogrammed fibroblasts for aged tissue regeneration and wound healing. *Aging Cell*, 23, e14032. PMID: 38010905

47. Sahu, S. K., Reddy, P., Lu, J., Shao, Y., Wang, C., Tsuji, M., … Izpisua Belmonte, J. C. (2024). Targeted partial reprogramming of age-associated cell states improves markers of health in mouse models of aging. *Science Translational Medicine*, 16(764), eadg1777. PMID: 39259812

48. Schoenfeldt, L., Paine, P. T., Pico, S., Kamaludeen, N. H., Phelps, G. B., Mrabti, C., Desdin-Mico, G., Del Carmen Maza, M., Perez, K., & Ocampo, A. (2025). Chemical reprogramming ameliorates cellular hallmarks of aging and extends lifespan. *EMBO Molecular Medicine*, 17(8), 2071–2094. PMID: 40588563

49. Sengstack, J., Zheng, J., Aghayev, T., Bieri, G., Mobaraki, M., Lin, J., Deng, C., Villeda, S. A., & Li, H. (2026). Systematic identification of single transcription factor perturbations that drive cellular and tissue rejuvenation. *Proceedings of the National Academy of Sciences*, 123(2), e2515183123. PMID: 41512022

50. Shen, Y. R., Zaballa, S., Bech, X., et al. (2024). Expansion of the neocortex and protection from neurodegeneration by in vivo transient reprogramming. *Cell Stem Cell*, 31(12), 1741–1759.e8. PMID: 39426381

51. Sousa-Victor, P., Gutarra, S., Garcia-Prat, L., Rodriguez-Ubreva, J., Ortet, L., Ruiz-Bonilla, V., … Munoz-Canoves, P. (2014). Geriatric muscle stem cells switch reversible quiescence into senescence. *Nature*, 506, 316–321. PMID: 24522534

52. Tong, H., Guo, X., Jacques, M., Luo, Q., Eynon, N., & Teschendorff, A. E. (2024). Cell-type specific epigenetic clocks to quantify biological age at cell-type resolution. *Aging*, 16(22), 13452–13504. PMID: 39760516

53. Villa del Campo, C., Raiola, M., Sierra, R., et al. (2020). Reactivation of Myc transcription in the mouse heart unlocks its proliferative capacity. *Nature Communications*, 11(1), 1827. PMID: 32286286

54. Wang, C., Rabadan Ros, R., Martinez-Redondo, P., Ma, Z., Shi, L., Xue, Y., … Izpisua Belmonte, J. C. (2021). In vivo partial reprogramming of myofibers promotes muscle regeneration by remodeling the stem cell niche. *Nature Communications*, 12, 3094. PMID: 34035273

55. Wang, P., Wang, R., Huo, Y., Peng, Y., Fu, C., Hu, Y., … et al. (2025a). Partial reprogramming in senescent Schwann cells enhances peripheral nerve regeneration via restoration of stress granule homeostasis. *Advanced Science*, 12(44), e2511019. PMID: 40899516

56. Wu, D., Sun, J. K.-L., & Chow, K. H.-M. (2024). Neuronal cell cycle reentry events in the aging brain are more prevalent in neurodegeneration and lead to cellular senescence. *PLoS Biology*, 22(4), e3002559. PMID: 38652714

57. Xiao, F., Nguyen, N. U. N., Wang, P., Li, S., Hsu, C., Thet, S., … Sadek, H. (2024). Adducin regulates sarcomere disassembly during cardiomyocyte mitosis. *Circulation*, 149(23), 1833–1851. PMID: 38708635

58. Xu, L., Ramirez-Matias, J., Hauptschein, M., Sun, E. D., Lunger, J. C., Buckley, M. T., & Brunet, A. (2024). Restoration of neuronal progenitors by partial reprogramming in the aged neurogenic niche. *Nature Aging*, 4(4), 546–567. PMID: 38553564

59. Yin, K., Buttner, M., Deligiannis, I. K., Strzelecki, M., Zhang, L., Talavera-Lopez, C., Theis, F., Odom, D. T., & Martinez-Jimenez, C. P. (2024). Polyploidisation pleiotropically buffers ageing in hepatocytes. *Journal of Hepatology*, 81(2), 289–302. PMID: 38583492

60. Yucel, A. D., & Gladyshev, V. N. (2024). The long and winding road of reprogramming-induced rejuvenation. *Nature Communications*, 15(1), 1941. PMID: 38431638

61. Zhang, Y., Zhong, H., Dong, Y., Sun, J., Liu, S., Chen, M., Ke, Y., Wang, Y., & Xu, H. (2025a). Restoration of retinal regenerative potential of Muller glia by disrupting intercellular Prox1 transfer. *Nature Communications*, 16(1), 2928. PMID: 40133314

62. Blackshaw, S., et al. (2024). Robust reprogramming of glia into neurons by inhibition of Notch signaling and nuclear factor I (NFI) factors in adult mammalian retina. *Science Advances*, 10(28), eadn2091. PMID: 38996013

63. Villa del Campo, C., Raiola, M., Sierra, R., et al. (2025). Myc overexpression improves recovery from myocardial infarction associated with cardiomyocyte hyperplasia in the mouse heart. *Communications Biology*, 8, 1069. PMID: 40681845
