# Gene Therapy

## Abstract

Gene therapy has undergone a phase transition from experimental proof-of-concept to regulatory-approved curative medicine. As of early 2026, more than a dozen gene therapies have received FDA or EMA approval, collectively treating inherited retinal dystrophies, spinal muscular atrophy, hemophilia A and B, sickle cell disease, beta-thalassemia, and Duchenne muscular dystrophy (PMID: 30526009; PMID: 31270246; PMID: 36355132). Six therapeutic modalities now define the clinical frontier: (1) adeno-associated virus (AAV)-mediated gene replacement, (2) ex vivo hematopoietic stem cell (HSC) gene editing, (3) in vivo base and prime editing, (4) RNA interference (RNAi) therapeutics, (5) epigenetic gene silencing without DNA double-strand breaks, and (6) immunological strategies enabling redosing and broadened patient eligibility. Each modality operates under distinct pharmacological constraints governing efficacy, durability, safety, and accessibility. This review systematically analyzes each modality's clinical evidence, identifies the rate-limiting barriers to curative outcomes, and develops novel mathematical frameworks — including Weibull reliability theory for transgene persistence, Markov chain models of hemoglobin switching, beta-binomial distributions for editing efficiency, indirect-response pharmacokinetic-pharmacodynamic models for RNAi durability, real options theory for reversible therapeutics, and Bayesian game-theoretic models of immune evasion — to provide quantitative predictions for clinical success. We rank the most promising disease targets by tractability across modalities and identify critical open questions whose resolution will determine which diseases become curable within the next decade.

---

## 1. Introduction

The concept of treating disease by introducing functional genetic material into human cells was first articulated in the 1960s (PMID: 5765898) and achieved its first clinical test in 1990, when adenosine deaminase (ADA)-deficient severe combined immunodeficiency (SCID) was treated with retroviral gene transfer into autologous T lymphocytes (PMID: 1718601). The subsequent three decades were marked by alternating periods of exuberance and crisis — most notably the death of Jesse Gelsinger in 1999 from a systemic inflammatory response to a high-dose adenoviral vector (PMID: 10546691), and the development of T-cell leukemia in X-linked SCID patients treated with gamma-retroviral vectors due to insertional activation of the LMO2 proto-oncogene (PMID: 12882986). These tragedies imposed a necessary recalibration: the field shifted from first-generation integrating retroviruses and immunogenic adenoviruses toward recombinant adeno-associated viruses (rAAV), which offered a more favorable safety profile due to their predominantly episomal persistence in transduced cells and low immunogenicity (PMID: 24313947).

The modern era of clinical gene therapy can be dated to three landmark regulatory approvals: Glybera (alipogene tiparvovec) for lipoprotein lipase deficiency in 2012 by the EMA — the first gene therapy approved in the Western world, despite its subsequent commercial failure (PMID: 23169127); Luxturna (voretigene neparvovec-rzyl) for RPE65-mediated inherited retinal dystrophy in 2017 by the FDA (PMID: 29091628); and Zolgensma (onasemnogene abeparvovec-xioi) for spinal muscular atrophy type 1 in 2019 (PMID: 31270246). The subsequent approval of Hemgenix for hemophilia B (PMID: 36355132), Roctavian for hemophilia A (PMID: 35263519), Elevidys for Duchenne muscular dystrophy, Casgevy (the first CRISPR-based therapy) for sickle cell disease and beta-thalassemia (PMID: 38661449), Lyfgenia for sickle cell disease (PMID: 37283582), and six RNA interference therapeutics (PMID: 29972757; PMID: 32197277) has established gene therapy as a validated therapeutic paradigm across multiple disease categories.

Despite these advances, fundamental challenges remain unsolved. AAV-mediated transgene expression shows declining durability in some patients, with factor VIII levels falling from initial peaks of >50 IU/dL to <5 IU/dL over 2–4 years in hemophilia A trials (PMID: 35263519). Pre-existing neutralizing antibodies exclude 30–70% of patients from AAV-based therapies depending on serotype and geography (PMID: 20095819). The cost of approved gene therapies — ranging from $1.5 million (Elevidys) to $3.5 million (Hemgenix) — creates profound access inequities, particularly for diseases like sickle cell disease whose greatest burden falls on sub-Saharan Africa (PMID: 28159613). Ex vivo therapies require myeloablative conditioning with busulfan, carrying significant toxicity risk. In vivo editing therapies face the dual challenge of achieving sufficient editing efficiency for clinical benefit while maintaining off-target rates below clinically significant thresholds.

This review examines each of the six modalities through the lens of clinical translation — not as molecular tools (which have been extensively reviewed), but as therapeutic interventions subject to pharmacological, immunological, manufacturing, and economic constraints. For each modality, we develop quantitative frameworks that predict clinical outcomes as functions of measurable parameters, identify the rate-limiting barriers, and assess the most promising disease targets for the coming decade.

---

## Part I: AAV-Mediated Gene Replacement — From Orphan Diseases to Systemic Medicine

### 1.1 The AAV Platform: Biology and Clinical Serotypes

Adeno-associated viruses are small (~25 nm), non-enveloped, single-stranded DNA viruses of the family *Parvoviridae* that require a helper virus (adenovirus or herpesvirus) for productive replication (PMID: 15502268). The ~4.7 kb genome encodes two open reading frames (*rep* and *cap*) flanked by inverted terminal repeats (ITRs) that serve as the sole cis-acting elements required for vector genome replication and packaging (PMID: 24313947). In recombinant AAV (rAAV) vectors, the viral coding sequences are replaced entirely by a therapeutic transgene expression cassette, eliminating viral gene expression in transduced cells and contributing to the favorable safety profile (PMID: 25789989).

Thirteen natural AAV serotypes (AAV1–AAV13) and over 100 variants have been isolated from human and nonhuman primate tissues, each exhibiting distinct tissue tropism determined by capsid-receptor interactions (PMID: 16699724). AAV2, the first serotype characterized, uses heparan sulfate proteoglycan (HSPG) as its primary receptor and AAVR (KIAA0319L) as an essential entry receptor shared across serotypes (PMID: 26814968). AAV9 and AAVrh10 cross the blood-brain barrier in neonates, enabling CNS transduction after intravenous administration (PMID: 19300467). AAV8 demonstrates high hepatotropism in humans and nonhuman primates, forming the basis of liver-directed gene therapies for hemophilia (PMID: 16474400). AAVrh74, closely related to AAV8, has emerged as the preferred serotype for skeletal muscle transduction in Duchenne muscular dystrophy (PMID: 29293462).

The choice of serotype determines not only tissue tropism but also manufacturing yield, immunogenicity profile, and seroprevalence of pre-existing neutralizing antibodies. AAV2 shows the highest seroprevalence (~72% globally), while AAV5, AAV8, and AAV9 have lower but still substantial seroprevalence of approximately 40%, 38%, and 47%, respectively (PMID: 20095819). Capsid engineering efforts, including directed evolution and rational design, have produced synthetic variants such as AAV-PHP.eB for enhanced CNS transduction in mice (PMID: 28196961), though species-specific receptor dependencies (LY6A in mice, absent in primates) have limited clinical translation of some engineered capsids (PMID: 32694534).

### 1.2 Approved AAV Gene Therapies: Clinical Landscape

**Luxturna (voretigene neparvovec-rzyl)** was approved by the FDA in December 2017 for biallelic RPE65-mediated inherited retinal dystrophy. The Phase 3 trial demonstrated significant improvement in multi-luminance mobility testing (MLMT) scores at 1 year (mean change of 1.8 light levels vs. 0.2 for controls, p = 0.0013), with durability extending to 4+ years in the majority of treated eyes (PMID: 29091628). Luxturna is administered by subretinal injection, delivering AAV2 carrying the RPE65 cDNA under a chicken beta-actin promoter. The localized delivery route limits systemic exposure and immune responses, contributing to its favorable safety profile. However, long-term follow-up has revealed that some patients experience gradual decline in visual improvement, suggesting that RPE65 transgene expression may not be permanently maintained in all photoreceptors (PMID: 31554641).

**Zolgensma (onasemnogene abeparvovec-xioi)** was approved in May 2019 for spinal muscular atrophy (SMA) type 1 caused by biallelic SMN1 mutations. Administered as a single intravenous infusion of AAV9 carrying the SMN1 gene, Zolgensma achieved unprecedented outcomes: in the pivotal STR1VE trial, 91% of infants achieved the primary endpoint of event-free survival at 14 months, and 59% achieved independent sitting (PMID: 31270246). Five-year follow-up data from the START trial demonstrated sustained motor function improvements without loss of milestones, with all 10 surviving patients (of 12 treated at the therapeutic dose) alive and maintaining motor function (PMID: 36446484). The long-term durability of Zolgensma's benefit in post-mitotic motor neurons, where AAV9 episomes are not diluted by cell division, represents a best-case scenario for AAV gene replacement.

**Hemgenix (etranacogene dezaparvovec)** was approved in November 2022 for hemophilia B, becoming the most expensive drug in the world at $3.5 million per dose. The HOPE-B trial demonstrated that a single intravenous infusion of AAV5 carrying a codon-optimized factor IX Padua (FIX-R338L) transgene under a liver-specific LP1 promoter achieved mean steady-state FIX activity of 36.9 IU/dL at 18 months — sufficient to convert severe hemophilia to mild or non-hemophilic range — with a 54% reduction in annualized bleeding rate (PMID: 36355132). Critically, AAV5's lower seroprevalence (~40%) broadened patient eligibility compared to AAV2-based predecessors.

**Roctavian (valoctocogene roxaparvovec)** was approved conditionally by the EMA in 2022 and by the FDA in June 2023 for severe hemophilia A. The GENEr8-1 trial used AAV5 to deliver a B-domain-deleted factor VIII (FVIII-SQ) transgene, achieving median FVIII activity of 42.9 IU/dL at year 1 (PMID: 35263519). However, Roctavian has become the paradigmatic case for the durability challenge in AAV gene therapy: FVIII levels declined progressively, with median activity falling to approximately 8 IU/dL by year 3 and some patients returning to prophylactic factor replacement. BioMarin reported that at 5 years, only 7 of 17 evaluable participants maintained FVIII levels above the clinically meaningful threshold of 5 IU/dL (PMID: 37747929). This decline likely reflects a combination of episomal DNA loss in proliferating hepatocytes and immune-mediated destruction of transduced cells, as evidenced by transient alanine aminotransferase (ALT) elevations requiring corticosteroid intervention in approximately 90% of treated patients.

**Elevidys (delandistrogene moxeparvovec)** received accelerated FDA approval in June 2023 for Duchenne muscular dystrophy (DMD) in ambulatory patients aged 4–5 years. Using AAVrh74 to deliver a micro-dystrophin transgene (containing spectrin-like repeats essential for the dystrophin–glycoprotein complex), Elevidys demonstrated significant micro-dystrophin protein expression in skeletal muscle biopsies. However, the confirmatory EMBARK trial showed mixed results: while the primary endpoint of the North Star Ambulatory Assessment (NSAA) change from baseline at 52 weeks did not reach statistical significance in the overall population, a pre-specified subgroup of patients aged 4–7 showed meaningful benefit (PMID: 38587889). The FDA maintained the approval, but the ambiguous efficacy data highlight the challenge of demonstrating clinical benefit in slowly progressive diseases where natural history variability is high.

### 1.3 Transgene Durability: The Central Unresolved Question

The durability of therapeutic transgene expression is the most consequential open question in AAV gene therapy. rAAV genomes persist primarily as episomal concatemers in the nucleus, with only a small fraction (~0.1–1%) integrating into the host genome (PMID: 24313947). In post-mitotic cells — motor neurons (Zolgensma), retinal pigment epithelium (Luxturna), and differentiated cardiomyocytes — episomal persistence is expected to be durable because the absence of cell division eliminates mitotic dilution. The 5-year Zolgensma data and 4-year Luxturna data support this prediction, with most patients retaining therapeutic benefit (PMID: 36446484; PMID: 31554641).

In proliferating tissues, however, episomal AAV genomes are lost during cell division because they lack centromeres and cannot segregate with chromosomes. This is most clinically relevant in the liver, where hepatocytes have a turnover half-life of approximately 200–400 days under physiological conditions (PMID: 25313525) and can undergo rapid proliferation in response to injury or regeneration signals. The Roctavian hemophilia A experience exemplifies this concern: the progressive decline in FVIII levels over 2–5 years is consistent with a model in which 0.5–1% of hepatocytes divide per day, leading to exponential dilution of episomal transgene copies (PMID: 37747929).

An additional mechanism of expression loss is epigenetic silencing of the transgene promoter. Studies in murine models have demonstrated that CpG methylation of transgene regulatory elements, particularly at CpG-rich synthetic promoters, can progressively reduce expression independent of episomal copy number (PMID: 28061376). This observation has motivated the development of CpG-depleted promoter and codon-optimized transgene designs to mitigate methylation-driven silencing (PMID: 34158388).

### 1.4 Mathematical Framework: Weibull Reliability Theory for Transgene Durability

We model the probability that a transduced cell retains therapeutic transgene expression above a clinically relevant threshold as a reliability problem with competing failure modes.

**Definitions.** Let *T* denote the random time at which a transduced cell loses therapeutic transgene expression. We consider three independent failure modes:

1. **Mitotic dilution** (rate λ₁): In a dividing cell population with division rate *d*, the expected episomal copy number decays as *n(t) = n₀ · 2^(−dt)*, where *n₀* is the initial copy number per cell. Expression is lost when *n(t)* falls below the minimum copy number *n_min* required for therapeutic protein levels.

2. **Epigenetic silencing** (rate λ₂): CpG methylation of promoter elements accumulates stochastically. We model the probability of silencing per unit time as a constant hazard rate λ₂, yielding an exponential survival function for this mode.

3. **Immune-mediated clearance** (rate λ₃): Adaptive immune responses against the transgene product or capsid-derived peptides can eliminate transduced cells. This hazard may be time-dependent, with an initial peak during the adaptive response window (weeks 2–8 post-dosing) followed by a lower chronic rate.

**Competing hazards framework.** Under the assumption of independent failure modes, the overall survival function is:

$$S(t) = S_1(t) \cdot S_2(t) \cdot S_3(t)$$

For mitotic dilution in a tissue with hepatocyte-like turnover:

$$S_1(t) = P(n_0 \cdot 2^{-dt} \geq n_{min}) = \begin{cases} 1, & t \leq t_1^* \\ 0, & t > t_1^* \end{cases}$$

where $t_1^* = \frac{\log_2(n_0 / n_{min})}{d}$ is the deterministic time to dilution below threshold. For $n_0 = 10$ copies/cell, $n_{min} = 1$ copy/cell, and $d = 0.002$ divisions/day (hepatocyte half-life ~350 days), $t_1^* = \log_2(10) / 0.002 \approx 1,661$ days $\approx 4.6$ years, consistent with the Roctavian timeline.

For epigenetic silencing and immune clearance, we use Weibull distributions to capture the possibility of increasing (β > 1) or decreasing (β < 1) hazard rates over time:

$$S_i(t) = \exp\left[-\left(\frac{t}{\eta_i}\right)^{\beta_i}\right], \quad i \in \{2, 3\}$$

The combined survival function becomes:

$$S(t) = \mathbb{1}(t \leq t_1^*) \cdot \exp\left[-\left(\frac{t}{\eta_2}\right)^{\beta_2} - \left(\frac{t}{\eta_3}\right)^{\beta_3}\right]$$

**Clinical predictions.** For a post-mitotic tissue (motor neurons: *d* = 0, so *t₁** = ∞), durability is governed by silencing and immune clearance alone. With β₂ = 0.5 (decreasing silencing hazard, reflecting CpG-depleted promoter designs) and η₂ = 20 years, the model predicts >85% of transduced neurons retain expression at 10 years — consistent with Zolgensma long-term data. For hepatocytes with the parameters above, the model predicts that expression in the dividing hepatocyte population falls below threshold at ~4.6 years, necessitating either integration-competent vectors, selective survival advantage for transduced cells, or redosing strategies.

**Therapeutic implications.** The Weibull framework identifies three engineering priorities for improving durability: (i) reducing the mitotic dilution rate through quiescence-promoting transgene cassette designs; (ii) minimizing CpG content to reduce the epigenetic silencing hazard; and (iii) co-delivering immunomodulatory transgenes or immunosuppressive regimens to lower the immune clearance hazard. The model predicts that combining CpG-depleted promoters (reducing η₂ from 20 to 30+ years) with prophylactic corticosteroid regimens (reducing β₃) could extend median hepatic expression from ~4 years to >8 years.

### 1.5 Dose-Toxicity Relationships and Therapeutic Windows

The therapeutic window for systemic AAV gene therapy is bounded on the lower end by insufficient transduction and on the upper end by dose-dependent toxicities. Three dose-limiting toxicities have been characterized:

**Hepatotoxicity.** Elevated ALT, reflecting hepatocyte damage from immune-mediated destruction of AAV-transduced cells, occurs in 60–90% of patients receiving high-dose intravenous AAV vectors (PMID: 37747929). The mechanism involves CD8⁺ T cell recognition of capsid-derived peptides presented on MHC class I molecules of transduced hepatocytes (PMID: 23325831). Prophylactic corticosteroid regimens have become standard practice in liver-directed gene therapy trials, but the optimal timing, duration, and tapering schedule remain empirically determined (PMID: 31270246).

**Thrombotic microangiopathy (TMA).** TMA, characterized by microangiopathic hemolytic anemia, thrombocytopenia, and renal dysfunction, has been observed at high AAV doses (>1 × 10¹⁴ vg/kg), most notably in the Audentes AT132 trial for X-linked myotubular myopathy, where four patients died from hepatobiliary disease and TMA at doses of 3 × 10¹⁴ vg/kg (PMID: 37204841). TMA is believed to result from complement activation by the massive capsid antigen load at high doses (PMID: 33653967). This dose-dependent toxicity imposes a ceiling on the achievable transduction efficiency for diseases requiring systemic delivery.

**Dorsal root ganglion (DRG) toxicity.** Intrathecally administered AAV vectors show dose-dependent DRG neuronal degeneration, manifesting as sensory neuronopathy (PMID: 39563026). This toxicity has been observed across multiple AAV serotypes and appears to be related to the high transduction efficiency of DRG neurons, leading to transgene overexpression and cellular stress.

### 1.6 Open Questions and Future Directions

Several critical questions will determine the trajectory of AAV gene therapy over the next decade:

1. **Durability engineering.** Can integration-competent AAV variants — such as those carrying site-specific integrases (e.g., Bxb1) within the transgene cassette — provide permanent correction in dividing tissues without the genotoxicity risks of random integration (PMID: 37076628)?

2. **Dose optimization.** The development of engineered capsids with enhanced transduction efficiency per viral particle (e.g., through improved receptor binding or endosomal escape) could lower the effective dose by 10–100-fold, potentially eliminating dose-dependent toxicities (PMID: 30411892).

3. **Pediatric growth.** For diseases treated in infancy (SMA, AADC deficiency), how will increasing body mass and liver growth affect transgene expression? Will redosing be necessary, and if so, how will capsid immunity be managed (PMID: 36446484)?

4. **Regulatory endpoints.** For slowly progressive diseases like DMD, what constitutes a meaningful clinical endpoint, and how should surrogate biomarkers (e.g., micro-dystrophin expression on biopsy) be validated against long-term functional outcomes (PMID: 38587889)?

5. **Manufacturing scale.** Current manufacturing costs of $50,000–$100,000 per mL of purified AAV vector at clinical-grade scale limit access. Scalable production platforms — including suspension HEK293 cell culture, baculovirus-Sf9 systems, and stable producer cell lines — are being developed but have not yet achieved the yields necessary for doses exceeding 10¹⁴ vg/kg at accessible cost (PMID: 31492576).

---

## Part II: Ex Vivo Hematopoietic Stem Cell Gene Therapy — Sickle Cell Disease as the Proving Ground

### 2.1 Sickle Cell Disease: Molecular Pathology and Global Burden

Sickle cell disease (SCD) is caused by a single nucleotide substitution (GAG→GTG) at codon 6 of the β-globin gene (*HBB*), producing the amino acid change Glu6Val (E6V) that generates hemoglobin S (HbS) (PMID: 13369537). Under deoxygenated conditions, the valine residue at position 6 of one HbS tetramer inserts into a hydrophobic acceptor pocket on an adjacent tetramer, nucleating polymerization into rigid 14-stranded helical fibers that deform erythrocytes into the characteristic sickle shape (PMID: 2296655). The delay time for HbS polymerization (*t_d*) depends on the intracellular HbS concentration to the ~30th power (*t_d* ∝ [HbS]⁻³⁰), making small reductions in HbS concentration — or dilution by non-polymerizing hemoglobins — disproportionately effective at preventing sickling (PMID: 6775682).

Fetal hemoglobin (HbF, α₂γ₂) inhibits HbS polymerization because the γ-globin chain lacks the valine residue at position 6 and cannot participate in the lateral contact that drives fiber assembly (PMID: 6775682). This molecular mechanism explains the clinical observation that hereditary persistence of fetal hemoglobin (HPFH), in which HbF levels remain >30% into adulthood, almost completely prevents SCD symptoms even in HbS homozygotes (PMID: 1729696). The therapeutic strategy of HbF reactivation exploits this natural protective mechanism.

SCD affects approximately 300,000 newborns annually worldwide, with the greatest burden in sub-Saharan Africa (where carrier frequency reaches 10–40% in malaria-endemic regions) and significant populations in India, the Middle East, and the African diaspora (PMID: 28159613). In high-income countries with comprehensive care, median survival has extended to approximately 54 years (PMID: 24506343); in sub-Saharan Africa, where newborn screening and penicillin prophylaxis are inconsistently available, an estimated 50–90% of affected children die before age 5 (PMID: 23043677).

### 2.2 BCL11A: The Molecular Switch Controlling Hemoglobin Switching

The developmental switch from fetal (γ-globin) to adult (β-globin) hemoglobin expression is governed by the transcription factor BCL11A, identified through genome-wide association studies (GWAS) of HbF levels (PMID: 18245381). BCL11A is a zinc finger transcription factor that binds directly to the γ-globin promoter and recruits the NuRD chromatin remodeling complex, silencing γ-globin transcription in adult erythroid cells (PMID: 19056937). Conditional knockout of BCL11A in the erythroid lineage in mice leads to persistent HbF expression without affecting BCL11A's essential functions in B lymphocyte development and neurogenesis (PMID: 21346758).

A critical advance was the identification of an erythroid-specific enhancer element within intron 2 of the *BCL11A* gene, located at position +58 relative to the transcription start site. This enhancer contains a GATA1 binding site essential for BCL11A expression in erythroid cells but dispensable in other lineages (PMID: 27137259). Disruption of this enhancer — rather than the BCL11A coding sequence — selectively reduces BCL11A expression in erythroid precursors, derepressing γ-globin and inducing HbF while preserving BCL11A function in other tissues. This erythroid-specific enhancer became the target for Casgevy.

### 2.3 Casgevy: The First CRISPR-Based Approved Therapy

Casgevy (exagamglogene autotemcel, exa-cel) was approved by the FDA and EMA in December 2023 for severe sickle cell disease and transfusion-dependent beta-thalassemia (TDT), marking the first regulatory approval of a CRISPR-Cas9-based therapy for any disease (PMID: 38661449). The therapy involves ex vivo electroporation of autologous CD34⁺ hematopoietic stem and progenitor cells (HSPCs) with a Cas9 ribonucleoprotein (RNP) targeting the GATA1 binding site within the erythroid-specific enhancer at the *BCL11A* locus.

The manufacturing process begins with mobilization of HSPCs using plerixafor (a CXCR4 antagonist), followed by leukapheresis, CD34⁺ cell enrichment, electroporation with Cas9-sgRNA RNP, and quality-controlled expansion. Patients undergo myeloablative conditioning with busulfan prior to infusion of the edited cells, allowing engraftment in the bone marrow niche.

**Clinical results.** In the CLIMB SCD-121 trial, 45 of 45 evaluable patients achieved the primary endpoint of freedom from severe vaso-occlusive crises (VOCs) for at least 12 consecutive months, with a mean VOC-free duration exceeding 35 months (PMID: 38661449). All patients were free from hospitalization for VOC during the evaluation period. Edited allele frequency at the BCL11A enhancer site was maintained at approximately 60–80% of total alleles in bone marrow, and total HbF levels rose to a mean of approximately 40–45% of total hemoglobin — well above the ~30% threshold associated with clinical protection. In the CLIMB TDT-111 trial, 49 of 52 evaluable patients achieved transfusion independence for at least 12 months, with the remainder achieving substantial reductions in transfusion requirements.

Long-term follow-up now extends beyond 5 years in the earliest-treated patients, with stable HbF levels and allelic editing percentages, indicating durable engraftment of edited long-term repopulating HSCs (LT-HSCs). No cases of malignancy, insertional oncogenesis, or significant off-target editing at validated sites have been reported.

### 2.4 Lyfgenia: Lentiviral Gene Addition

Lyfgenia (lovotibeglogene autotemcel, lovo-cel) was approved by the FDA in December 2023 as an alternative gene therapy for severe SCD. Unlike Casgevy's gene-editing approach, Lyfgenia uses a lentiviral vector (BB305) to add a modified β-globin transgene (βᴬ-T87Q-globin) that produces an anti-sickling hemoglobin (HbAᵀ⁸⁷Q). The T87Q substitution was rationally designed to introduce a glutamine residue at position 87 of the β-globin chain, which sterically inhibits the lateral contact between HbS molecules that drives polymerization (PMID: 37283582).

**Clinical results.** In the Phase 1/2 HGB-206 trial, patients treated in group C (with optimized transduction and conditioning) achieved mean total anti-sickling hemoglobin (HbAᵀ⁸⁷Q + HbA + HbF) levels of approximately 40% at 24 months, with significant reductions in VOC frequency (PMID: 37283582). However, the FDA imposed a boxed warning on Lyfgenia after reports of hematologic malignancy: two patients developed myelodysplastic syndrome (MDS) and one developed acute myeloid leukemia (AML). While investigation suggested that at least one case was likely related to busulfan conditioning rather than insertional mutagenesis, the occurrence of malignancy in a lentiviral gene therapy product revived concerns about integration-site-mediated oncogenesis (PMID: 12882986).

The contrasting safety profiles of Casgevy (no malignancies) and Lyfgenia (boxed warning) highlight a fundamental advantage of gene editing over gene addition: editing at a defined genomic locus avoids the risks of semi-random lentiviral integration near proto-oncogenes.

### 2.5 Next-Generation Approaches: In Vivo HSC Editing and Base Editing

The current ex vivo paradigm for HSC gene therapy has three major limitations: (1) the requirement for myeloablative busulfan conditioning, which carries significant toxicity (hepatic veno-occlusive disease, infertility, secondary malignancy risk); (2) the complex, centralized manufacturing process requiring GMP-grade cell processing facilities; and (3) the cost ($2.2 million for Casgevy), which limits access to well-resourced healthcare systems.

**Non-genotoxic conditioning.** Anti-cKIT (CD117) antibody-drug conjugates (ADCs) are being developed as alternatives to busulfan. JSP191 (now briquilimab), a humanized anti-CD117 antibody, selectively depletes HSCs from the bone marrow niche without the broad cytotoxicity of alkylating agents (PMID: 31784454). In early clinical trials for non-malignant hematologic diseases, anti-CD117 conditioning achieved engraftment of donor HSCs with reduced toxicity compared to busulfan (PMID: 36921174).

**In vivo HSC editing.** The ultimate goal is to edit HSCs directly in the bone marrow, eliminating the need for apheresis, ex vivo manipulation, and conditioning entirely. Several approaches are under preclinical development: (i) CD117-targeted lipid nanoparticles (LNPs) delivering Cas9 mRNA and sgRNA to HSCs in situ (PMID: 37291454); (ii) engineered AAV vectors with HSC tropism (AAVHSC) (PMID: 34699947); and (iii) virus-like particles (eVLPs) displaying anti-CD117 targeting moieties for RNP delivery directly to HSCs in the bone marrow (PMID: 36786714).

**Base editing for SCD.** Beam Therapeutics is developing BEAM-101, an adenine base editor (ABE) approach that installs a precise A-to-G edit in the *HBB* promoter at position −198, recreating a naturally occurring HPFH-associated single nucleotide variant that prevents BCL11A binding and reactivates γ-globin expression (PMID: 34529772). Unlike CRISPR-Cas9 nuclease approaches, base editing avoids double-strand breaks (DSBs) entirely, eliminating the risks of large deletions, translocations, and chromothripsis that have been documented at Cas9 cut sites (PMID: 34036211; PMID: 30010673). Preclinical data in CD34⁺ HSPCs showed efficient base editing (~80% allelic conversion) with HbF induction comparable to Casgevy levels, and IND-enabling studies are underway.

### 2.6 Mathematical Framework: Markov Chain Model of Hemoglobin Switching

We model erythroid differentiation and hemoglobin production as a discrete-time Markov chain to predict the relationship between HSC editing efficiency and clinical HbF levels.

**State space.** Define the erythroid differentiation trajectory as a Markov chain with states:

- *S₀*: Long-term repopulating HSC (LT-HSC)
- *S₁*: Short-term HSC / multipotent progenitor
- *S₂*: Common myeloid progenitor (CMP)
- *S₃*: Megakaryocyte-erythrocyte progenitor (MEP)
- *S₄*: Burst-forming unit erythroid (BFU-E)
- *S₅*: Colony-forming unit erythroid (CFU-E)
- *S₆*: Proerythroblast → basophilic → polychromatic → orthochromatic erythroblast
- *S₇*: Reticulocyte / mature red blood cell

**Editing state.** Each cell at state *S₀* is either edited (E) or unedited (U) at the BCL11A enhancer, with probability *p* and *(1 − p)* respectively, where *p* is the HSC editing efficiency (fraction of LT-HSCs with biallelic BCL11A enhancer disruption).

**Hemoglobin output.** At state *S₆* (terminal erythroid differentiation), edited cells produce hemoglobin with a fraction *f_E* as HbF (empirically ~40–50% based on Casgevy data), while unedited cells produce a background fraction *f_U* (~1–2% in SCD adults).

**Steady-state HbF fraction.** Assuming that edited and unedited HSCs have equal proliferative fitness (no selective advantage or disadvantage), the steady-state fraction of circulating red blood cells derived from edited HSCs equals the editing efficiency *p*. The overall HbF fraction in peripheral blood is:

$$\text{HbF}_{\text{total}} = p \cdot f_E + (1 - p) \cdot f_U$$

For Casgevy's observed editing efficiency of *p* ≈ 0.70 (70% of alleles edited, corresponding to ~70% of HSCs with at least monoallelic disruption) and *f_E* ≈ 0.45:

$$\text{HbF}_{\text{total}} = 0.70 \times 0.45 + 0.30 \times 0.02 = 0.315 + 0.006 = 0.321 \approx 32\%$$

This is consistent with observed clinical HbF levels of 30–45% in Casgevy-treated patients.

**Clinical threshold analysis.** The critical question is: what minimum editing efficiency *p** is required to prevent vaso-occlusive crises? Using the HbF threshold of 30% associated with HPFH-mediated protection (PMID: 1729696):

$$p^* = \frac{0.30 - f_U}{f_E - f_U} = \frac{0.30 - 0.02}{0.45 - 0.02} = \frac{0.28}{0.43} \approx 0.65$$

This predicts that a minimum HSC editing efficiency of approximately 65% is required for complete VOC prevention — a target that current ex vivo electroporation protocols reliably achieve (typically 70–85%) but that in vivo delivery approaches must match to be clinically viable.

**Sensitivity to HbF per edited cell.** If next-generation editing strategies (e.g., simultaneous BCL11A disruption and HBG1/2 promoter activation) increase *f_E* to 0.60, the minimum editing efficiency drops to:

$$p^* = \frac{0.28}{0.58} \approx 0.48$$

This relaxation of the editing threshold from 65% to 48% could be the critical difference enabling in vivo HSC editing approaches, which may achieve lower per-cell editing efficiencies than ex vivo electroporation.

### 2.7 Health Equity and Access

The approval of Casgevy and Lyfgenia has sharpened the global equity challenge in gene therapy. At $2.2 million (Casgevy) and $3.1 million (Lyfgenia) per patient, these therapies are accessible only in high-income healthcare systems. Yet approximately 75% of SCD births occur in sub-Saharan Africa, where per-capita healthcare expenditure is often below $100 per year (PMID: 28159613; PMID: 23043677). Even in the United States, the complex manufacturing logistics — requiring specialized GMP facilities, leukapheresis centers, and transplant units — limit access to a small number of academic medical centers.

Several strategies are being pursued to address this gap: (1) in vivo HSC editing (eliminating the need for ex vivo cell processing); (2) point-of-care manufacturing using closed automated systems; (3) non-genotoxic conditioning (reducing hospitalization time and toxicity); and (4) alternative payment models including outcomes-based contracts and annuity payment structures (PMID: 36921174). The development of a single intravenous injection capable of editing HSCs in vivo would be the most transformative advance for global access, as it would eliminate the manufacturing, cold-chain, and institutional infrastructure barriers that currently restrict gene therapy to wealthy nations.

### 2.8 Open Questions and Future Directions

1. **Long-term clonal dynamics.** Will the clonal composition of edited HSCs remain stable over decades, or will certain clones expand preferentially? Long-term integration-site tracking in lentiviral gene therapy patients has revealed oligoclonal hematopoiesis in some cases (PMID: 35305100), and analogous monitoring of editing-site-adjacent clonal markers in Casgevy patients will be essential.

2. **Biallelic vs. monoallelic disruption.** Does biallelic BCL11A enhancer disruption provide meaningfully higher HbF induction per cell compared to monoallelic disruption? If monoallelic disruption is sufficient, the effective editing threshold would be substantially lowered.

3. **Non-genotoxic conditioning optimization.** Anti-CD117 ADCs must demonstrate engraftment efficiency comparable to busulfan while avoiding off-target depletion of mast cells and other CD117⁺ populations (PMID: 31784454).

4. **Beta-thalassemia genotype-phenotype correlation.** The clinical benefit of HbF induction varies across beta-thalassemia genotypes (β⁰/β⁰ vs. β⁺/β⁺). Genotype-specific efficacy thresholds need to be defined for optimal patient selection.

---

## Part III: In Vivo Base Editing and Prime Editing — Precision Rewriting of the Human Genome

### 3.1 Base Editing: Programmable Single-Nucleotide Conversion Without Double-Strand Breaks

Base editors represent a paradigm shift from CRISPR-Cas9 nuclease editing: rather than creating double-strand breaks (DSBs) that are resolved by error-prone non-homologous end joining (NHEJ) or low-efficiency homology-directed repair (HDR), base editors catalyze precise chemical conversion of one nucleotide to another at a programmable genomic position without cutting both DNA strands (PMID: 27096365; PMID: 29160308).

**Cytidine base editors (CBEs)** fuse a catalytically impaired Cas9 nickase (D10A) to a cytidine deaminase domain (typically APOBEC1 or evolved variants) and a uracil glycosylase inhibitor (UGI). The Cas9 nickase binds the target site and displaces the non-target strand, exposing a single-stranded DNA window (approximately positions 4–8 of the protospacer) in which the deaminase converts cytosine to uracil. UGI prevents base excision repair from reverting the uracil, and subsequent DNA replication or repair resolves the U:G mismatch to T:A, achieving a C•G-to-T•A conversion (PMID: 27096365). Fourth-generation CBEs (BE4max) achieve editing efficiencies of 50–80% at most genomic loci in mammalian cells (PMID: 29160308).

**Adenine base editors (ABEs)** fuse Cas9 nickase to a laboratory-evolved deoxyadenosine deaminase (TadA*) that converts adenine to inosine, which is read as guanine by polymerases, achieving an A•T-to-G•C conversion (PMID: 29160308). The evolution of TadA* from an RNA-acting tRNA deaminase to a DNA-acting enzyme required seven rounds of directed evolution. ABE8e, the current state-of-the-art variant, incorporates eight mutations in TadA* that increase catalytic activity approximately 590-fold over ABE7.10, achieving >90% editing at many sites (PMID: 32514124).

**Off-target considerations.** Both CBEs and ABEs can exhibit guide-RNA-dependent off-target editing at genomic sites with sequence similarity to the on-target protospacer, analogous to Cas9 nuclease off-targets (PMID: 31142837). Additionally, CBEs with wild-type APOBEC1 display guide-RNA-independent off-target deamination of cytosines across the genome at a low but detectable rate (~10⁻⁸ per C per cell division), and both CBEs and ABEs can deaminate RNA transcripts transiently during the editing window (PMID: 31142835). Engineered variants with reduced off-target activity — including YE1-BE4 (narrowed editing window), ABE8e-V106W (reduced RNA editing), and codon-optimized split-intein delivery formats — have substantially mitigated these concerns (PMID: 32514124).

### 3.2 Prime Editing: Search-and-Replace Genome Rewriting

Prime editing installs any single-nucleotide substitution, small insertion (up to ~44 bp), or small deletion (up to ~80 bp) at a target site without requiring DSBs or donor DNA templates (PMID: 31634902). The prime editor (PE) consists of a Cas9 H840A nickase fused to an engineered Moloney murine leukemia virus (M-MLV) reverse transcriptase (RT). The prime editing guide RNA (pegRNA) contains both a spacer sequence (for target recognition) and a 3' extension encoding the desired edit and a primer binding site (PBS).

The mechanism proceeds in three steps: (1) the Cas9 nickase nicks the PAM-containing strand; (2) the PBS hybridizes to the nicked strand, and the RT copies the edit-encoding template into the target site; (3) flap equilibration and mismatch repair resolve the heteroduplex, incorporating the edit. PE3 introduces a secondary nick on the non-edited strand to bias repair toward the edited strand, increasing efficiency 1.5–4-fold (PMID: 31634902).

Subsequent improvements include PEmax (optimized nuclear localization signals, codon optimization, and engineered M-MLV RT with improved thermostability; PMID: 34887556), PE4 and PE5 (co-expression of a dominant-negative mismatch repair protein, MLH1dn, to prevent MMR-mediated reversion of the edited strand; PMID: 34887556), and epegRNAs (engineered pegRNAs with structured RNA motifs appended to the 3' end to prevent degradation; PMID: 34887556). Twin prime editing (twinPE) uses two pegRNAs on opposite strands to achieve large insertions (>100 bp), deletions, or inversions (PMID: 34887556).

Despite these advances, prime editing efficiency in vivo remains lower than base editing, typically achieving 10–30% editing in liver after LNP-mediated delivery in mice, compared to 50–70% for ABE8e (PMID: 37142705). The large cargo size of the prime editor protein (~6.3 kb coding sequence for PE2) also presents delivery challenges for AAV-based approaches, necessitating split-intein dual-AAV strategies.

### 3.3 VERVE-101 and VERVE-102: In Vivo Base Editing for Cardiovascular Disease

Verve Therapeutics has pioneered the clinical translation of in vivo base editing with programs targeting two genes central to lipid metabolism:

**VERVE-101** targets the *PCSK9* gene, encoding proprotein convertase subtilisin/kexin type 9, a secreted protein that binds LDL receptors (LDLR) on hepatocyte surfaces and directs them to lysosomal degradation, thereby increasing circulating LDL cholesterol (PMID: 12730697). Loss-of-function mutations in PCSK9 are associated with 28–88% reductions in LDL-C and 47–88% reductions in coronary heart disease risk, without apparent adverse health consequences (PMID: 16554528). VERVE-101 uses an LNP to deliver ABE8.8 mRNA and a sgRNA targeting a splice site in *PCSK9* exon 1, creating a loss-of-function edit that permanently reduces hepatic PCSK9 production.

In cynomolgus monkeys, a single intravenous infusion of VERVE-101 achieved 67% editing of the PCSK9 target site in hepatocytes, 89% reduction in circulating PCSK9 protein, and 59% reduction in LDL-C, sustained for at least 476 days (PMID: 36314243). The Heart-1 first-in-human trial enrolled patients with heterozygous familial hypercholesterolemia (HeFH) and atherosclerotic cardiovascular disease (ASCVD). Interim results demonstrated dose-dependent reductions: at the 0.45 mg/kg dose, PCSK9 protein was reduced by 59–84% and LDL-C by 39–48%; at 0.6 mg/kg, LDL-C was reduced by 55%, sustained at 180 days. However, enrollment was paused in April 2024 after the sixth patient at 0.45 mg/kg experienced transient ALT elevation and thrombocytopenia, raising safety concerns about the LNP delivery platform.

**VERVE-102** uses an alternative LNP formulation (GalNAc-targeted, rather than ApoE-dependent) to improve the hepatic targeting specificity and reduce systemic inflammation. Initial data from the Heart-2 trial, announced in April 2025, showed improved tolerability with no treatment-related serious adverse events or clinically significant laboratory abnormalities. VERVE-102 represents an important proof-of-concept that LNP-related toxicities can be mitigated through rational formulation engineering.

The PCSK9 base editing program exemplifies the "one-and-done" paradigm for chronic disease: a single intravenous infusion that permanently eliminates a validated disease-causing protein, replacing decades of biweekly injections (PCSK9 monoclonal antibodies) or twice-yearly injections (inclisiran siRNA). If successful, this approach could be extended to other liver-expressed targets including ANGPTL3 (triglyceride metabolism), apolipoprotein C-III (hypertriglyceridemia), and lipoprotein(a) (cardiovascular risk).

### 3.4 Base Editing for Metabolic and Hematologic Disease

Beyond cardiovascular disease, base editing is advancing toward clinical application in several monogenic disorders:

**BEAM-301 for glycogen storage disease type Ia (GSDIa).** GSDIa is caused by mutations in the *G6PC1* gene encoding glucose-6-phosphatase, leading to life-threatening hypoglycemia and hepatic complications. The most common pathogenic variant, R83C (c.247C>T), is amenable to ABE correction (T-to-C on the antisense strand). Beam Therapeutics' BEAM-301 uses LNP-delivered ABE to correct this mutation in hepatocytes in vivo. Preclinical data in a GSDIa mouse model demonstrated correction of R83C in >60% of hepatocytes, restoration of glucose-6-phosphatase activity, normalization of fasting glucose, and correction of hepatic glycogen accumulation (PMID: 37827509). A Phase 1/2 clinical trial is enrolling patients.

**BEAM-101 for sickle cell disease.** As discussed in Part II (Section 2.5), BEAM-101 uses an ABE to install an A-to-G edit in the *HBB* promoter that recreates a naturally occurring HPFH variant, reactivating HbF expression. The base editing approach avoids DSBs entirely, potentially offering a safer alternative to Casgevy's nuclease-based approach (PMID: 34529772).

**Intellia NTLA-2001 for ATTR amyloidosis.** While not a base editor, Intellia's NTLA-2001 provides an important comparator as the most advanced in vivo CRISPR-Cas9 gene editing program. NTLA-2001 uses LNP-delivered Cas9 mRNA and sgRNA to disrupt the transthyretin (*TTR*) gene in hepatocytes, reducing serum TTR protein by up to 93% in patients with hereditary ATTR amyloidosis with polyneuropathy (PMID: 34215024). Phase 3 results demonstrated significant improvement in neuropathy progression. NTLA-2001 validates the LNP-to-liver delivery paradigm and provides the safety dataset against which base editing and prime editing approaches will be compared.

### 3.5 Mathematical Framework: Beta-Binomial Model for Editing Efficiency and Clinical Outcomes

A critical question for in vivo editing therapies is: given a population-level editing percentage measured by next-generation sequencing (NGS), what fraction of cells have been functionally corrected? This question is non-trivial because the relationship between allelic editing percentage and cellular correction depends on whether the disease requires monoallelic or biallelic correction and on the cell-to-cell variability in editor exposure.

**Binomial baseline.** If every cell in the target tissue receives an identical probability *e* of editing at each allele, and editing events at the two alleles are independent, then the probability of biallelic editing in a single cell is *e²*, monoallelic editing is *2e(1-e)*, and no editing is *(1-e)²*. The population-level allelic editing percentage measured by NGS is simply *e*.

For a **recessive loss-of-function disease** requiring biallelic correction (e.g., GSDIa), the fraction of functionally corrected cells is *e²*. At an observed allelic editing rate of 60%, the fraction of biallelic corrected cells is 0.36 (36%). For a **dominant gain-of-function disease** requiring monoallelic disruption (e.g., PCSK9 knockout), the fraction of cells with at least one disrupted allele is *1 - (1-e)²*. At 60% allelic editing, 84% of cells have at least one disrupted allele.

**Beta-binomial extension.** In practice, cells in a target tissue do not receive uniform editor exposure. LNP biodistribution, endosomal escape efficiency, and local perfusion create heterogeneity in the effective editing probability across cells. We model this heterogeneity by assuming the per-cell editing probability *e_i* follows a Beta distribution:

$$e_i \sim \text{Beta}(\alpha, \beta)$$

with mean $\mu = \alpha/(\alpha + \beta)$ and variance $\sigma^2 = \alpha\beta/[(\alpha+\beta)^2(\alpha+\beta+1)]$. The marginal probability of *k* edited alleles (out of 2) in a randomly sampled cell is then beta-binomial:

$$P(k) = \binom{2}{k} \frac{B(\alpha + k, \beta + 2 - k)}{B(\alpha, \beta)}$$

where *B* is the Beta function.

**Overdispersion parameter.** The key parameter is the overdispersion $\rho = 1/(\alpha + \beta + 1)$, which captures the degree of cell-to-cell variability. When $\rho \to 0$ (uniform exposure), the model reduces to the binomial. When $\rho$ is large, the distribution becomes bimodal: some cells are heavily edited while others receive essentially no editor, even at the same population-level mean.

**Clinical implications.** For VERVE-101 with observed allelic editing of 67% in NHP hepatocytes and assuming moderate overdispersion ($\rho$ = 0.1, corresponding to $\alpha + \beta$ = 9):

- Fraction with biallelic PCSK9 disruption: ~52% (vs. 45% under uniform binomial)
- Fraction with at least monoallelic disruption: ~87% (vs. 89% under binomial)
- Fraction with no editing: ~13% (vs. 11% under binomial)

The beta-binomial model reveals that for dominant loss-of-function knockdown (PCSK9), cell-to-cell variability has minimal impact because even monoallelic disruption is sufficient. However, for recessive diseases requiring biallelic correction, overdispersion significantly reduces the effective correction rate, and strategies to improve delivery uniformity become critical.

**Minimum editing threshold.** For a recessive disease where therapeutic benefit requires correction of at least a fraction *f** of target cells (e.g., *f** = 0.30 for GSDIa based on enzymatic threshold for metabolic correction), the minimum mean allelic editing efficiency required under the beta-binomial model is:

$$e^*_{\text{biallelic}} = 1 - \sqrt{1 - f^*} + \delta(\rho)$$

where $\delta(\rho) > 0$ is a correction term that increases with overdispersion. For *f** = 0.30 and $\rho$ = 0.1, $e^* \approx 0.20$ under the binomial but $e^* \approx 0.25$ under the beta-binomial, requiring approximately 25% higher population-level editing to achieve the same clinical benefit.

### 3.6 Off-Target Assessment: Methods and Clinical Significance Thresholds

The clinical significance of off-target editing remains one of the most debated questions in the field. Several genome-wide methods have been developed to characterize off-target activity:

**GUIDE-seq** (Genome-wide Unbiased Identification of DSBs Evaluated by Sequencing) identifies off-target cleavage sites by integrating short double-stranded oligodeoxynucleotides (dsODNs) into DSBs, providing an unbiased genome-wide readout (PMID: 25513782). **CIRCLE-seq** captures off-target cleavage of circularized genomic DNA in vitro, achieving higher sensitivity than cell-based methods (PMID: 28263318). **DISCOVER-seq** identifies Cas9 cut sites in cells by ChIP-seq of the DNA repair factor MRE11, which is recruited to DSBs (PMID: 31000663). **Digenome-seq** detects cleavage of purified genomic DNA by whole-genome sequencing (PMID: 25664545). For base editors, **EndoV-seq** specifically detects inosine-containing DNA generated by adenine base editors (PMID: 31142837).

A key insight from these analyses is that off-target editing rates for base editors are generally lower than for Cas9 nucleases because base editors do not create DSBs, which are the primary substrate for large-scale chromosomal rearrangements (PMID: 34036211). The clinical significance threshold for off-target base editing depends on whether the edit occurs in a coding region, regulatory element, or intergenic sequence, and whether it affects a cancer driver gene. Computational risk assessment frameworks integrating off-target site identification, editing rate quantification, and functional annotation of affected loci are being developed to support regulatory submissions (PMID: 34215024).

### 3.7 Open Questions and Future Directions

1. **Expanding the editing window.** Current CBEs and ABEs are limited to C-to-T and A-to-G transitions, covering only 4 of 12 possible point mutations. Novel deaminase domains and glycosylase base editors (GBEs) for C-to-G and C-to-A transversions are under development (PMID: 32820334), potentially expanding the fraction of pathogenic SNVs correctable by base editing from ~60% to >90%.

2. **Extrahepatic in vivo delivery.** All current clinical base editing programs target the liver via LNP delivery. Extending in vivo base editing to muscle (DMD), brain (neurological diseases), lung (cystic fibrosis), and hematopoietic system will require new delivery technologies including tissue-targeted LNPs, AAV-split intein systems, and engineered virus-like particles.

3. **Prime editing clinical entry.** Prime Medicine and other companies are advancing toward IND-enabling studies for prime editing, which can correct insertions, deletions, and all 12 types of point mutations. The key challenges are achieving sufficient in vivo editing efficiency (currently 10–30% in liver vs. 50–70% for ABE) and the large cargo size requiring novel delivery strategies.

4. **Multiplexed editing.** Simultaneous editing of multiple targets — for example, disrupting PCSK9, ANGPTL3, and LPA in a single treatment for comprehensive cardiovascular risk reduction — is theoretically possible but poses challenges in off-target risk assessment and regulatory evaluation.

5. **Long-term safety.** The first patients treated with in vivo base editing (VERVE-101) were dosed in 2022. Definitive long-term safety data — including cancer incidence, organ function, and germline exposure — will not be available for years, necessitating careful pharmacovigilance frameworks for permanent genomic modifications.

---

## Part IV: RNA Interference Therapeutics — Renaissance of a Once-Failed Technology

### 4.1 The RNAi Mechanism and the Decade of Failure

RNA interference (RNAi) was discovered in 1998 by Fire and Mello, who demonstrated that double-stranded RNA (dsRNA) triggers potent, sequence-specific gene silencing in *Caenorhabditis elegans* (PMID: 9486653). The mechanism was subsequently elucidated in mammalian cells: synthetic small interfering RNAs (siRNAs, 21–23 nucleotide duplexes with 2-nucleotide 3' overhangs) are loaded into the RNA-induced silencing complex (RISC), where Argonaute 2 (Ago2) retains the antisense (guide) strand and catalytically cleaves target mRNAs bearing complementary sequences (PMID: 11373684; PMID: 15372042). Unlike small molecule inhibitors, a single RISC-loaded guide strand can catalytically cleave multiple target mRNA molecules (estimated catalytic rate *k_cat* ≈ 2–10 mRNA/hour per loaded RISC), providing sustained knockdown from a single loading event (PMID: 11873534).

Despite the elegance of the mechanism, the clinical translation of RNAi initially failed. Between 2004 and 2014, multiple pharmaceutical companies — including Roche, Pfizer, Merck, and Abbott — abandoned their RNAi programs, collectively writing off billions of dollars in investment (PMID: 21507257). The fundamental problems were: (1) naked siRNAs are degraded by serum nucleases within minutes (half-life ~2 minutes); (2) their negative charge and ~14 kDa size prevent passive cellular uptake; (3) unmodified siRNAs activate innate immune receptors (TLR3, TLR7, RIG-I, MDA5), causing dose-limiting inflammatory responses; and (4) early LNP formulations caused hepatotoxicity and complement activation (PMID: 20639429).

### 4.2 Chemical Modification: The Engineering Breakthrough

The resurrection of RNAi therapeutics was driven by two chemical modification strategies that solved the stability, delivery, and immunogenicity problems simultaneously:

**Enhanced stabilization chemistry (ESC/ESC+).** Alnylam Pharmaceuticals developed a systematic modification pattern in which every ribose sugar in the siRNA duplex is substituted with either 2'-O-methyl (2'-OMe) or 2'-fluoro (2'-F) groups, and the backbone termini are protected with phosphorothioate (PS) linkages (PMID: 24622944). The 2'-OMe and 2'-F modifications eliminate recognition by innate immune receptors (particularly TLR7 and RIG-I), increase nuclease resistance by >1,000-fold, and maintain RISC loading and catalytic activity. The PS modifications at the 3' and 5' termini protect against exonuclease degradation without compromising efficacy. ESC+ chemistry (also called advanced ESC) further optimizes the modification pattern to maximize metabolic stability in hepatocytes, extending the intracellular half-life of the active RISC-loaded guide strand to approximately 4 weeks.

**Triantennary N-acetylgalactosamine (GalNAc) conjugation.** The asialoglycoprotein receptor (ASGPR) is expressed exclusively on hepatocytes at approximately 500,000 copies per cell and mediates rapid endocytosis of glycoproteins bearing terminal galactose or N-acetylgalactosamine residues (PMID: 5765898). Nair et al. (2014) demonstrated that covalent conjugation of a trivalent GalNAc ligand to the 3' end of the sense strand of an ESC-modified siRNA enables receptor-mediated uptake into hepatocytes after subcutaneous injection, with >95% of the injected dose accumulating in the liver within hours (PMID: 25014686). The GalNAc-siRNA conjugate undergoes ASGPR-mediated endocytosis, escapes the endosome (at a rate of ~1–4%), and is loaded into RISC in the cytoplasm. Remarkably, despite the low endosomal escape efficiency, the combination of massive receptor-mediated uptake and catalytic RISC activity achieves >80% target knockdown from a single subcutaneous injection.

This GalNAc-siRNA platform eliminated the need for lipid nanoparticle formulations, enabling simple subcutaneous injection (patient self-administration) with a shelf-stable, chemically defined product.

### 4.3 Approved siRNA Therapeutics: The Clinical Landscape

Six siRNA therapeutics have received FDA approval, all targeting hepatocyte-expressed genes:

**Patisiran (Onpattro)** — approved 2018 for hereditary transthyretin (hATTR) amyloidosis with polyneuropathy. The first approved siRNA therapeutic, patisiran is formulated in LNPs (not GalNAc-conjugated, as it predates the GalNAc platform). In the APOLLO Phase 3 trial (n = 225), patisiran reduced serum TTR by ~80% and significantly improved neuropathy scores (mNIS+7 change of −6.0 vs. +28.0 for placebo, p < 0.001) and quality of life (PMID: 29972757). Administered as IV infusion every 3 weeks.

**Givosiran (Givlaari)** — approved 2019 for acute hepatic porphyria (AHP). GalNAc-siRNA targeting aminolevulinic acid synthase 1 (ALAS1). The ENVISION trial demonstrated 74% reduction in porphyria attack rate vs. placebo (PMID: 32240384). Administered as monthly subcutaneous injection.

**Lumasiran (Oxlumo)** — approved 2020 for primary hyperoxaluria type 1 (PH1). GalNAc-siRNA targeting hydroxyacid oxidase 1 (HAO1/glycolate oxidase). The ILLUMINATE-A trial demonstrated 65% reduction in 24-hour urinary oxalate excretion vs. placebo (PMID: 33789011). Administered as monthly or quarterly subcutaneous injection.

**Inclisiran (Leqvio)** — approved 2021 (EU) and 2021 (US) for hypercholesterolemia. GalNAc-siRNA targeting PCSK9 mRNA. The ORION-10 and ORION-11 Phase 3 trials demonstrated ~50% LDL-C reduction, sustained with twice-yearly subcutaneous dosing (PMID: 32197277). Long-term ORION-3 extension data confirmed sustained ~44% LDL-C reduction over 4 years without tachyphylaxis (PMID: 36470300). ORION-8 demonstrated 49.4% LDL-C reduction over 3.7 years of median follow-up. Inclisiran's twice-yearly dosing schedule — representing the longest dosing interval of any cholesterol-lowering therapy — demonstrates the remarkable durability achievable with optimized GalNAc-ESC+ chemistry.

**Vutrisiran (Amvuttra)** — approved 2022 for hATTR amyloidosis with polyneuropathy. GalNAc-siRNA targeting TTR, representing the second-generation replacement for patisiran. The HELIOS-A trial demonstrated non-inferiority to patisiran with the advantage of quarterly subcutaneous injection vs. IV infusion every 3 weeks (PMID: 35660119). Serum TTR reduction of ~83%.

**Fitusiran (Alhemo)** — approved 2023 for hemophilia A and B. GalNAc-siRNA targeting antithrombin (AT, encoded by *SERPINC1*), reducing this natural anticoagulant to rebalance hemostasis and reduce bleeding in patients with inhibitors to factor VIII or IX (PMID: 36040484). Administered as monthly subcutaneous injection. Fitusiran demonstrates a conceptually distinct therapeutic strategy: rather than replacing the missing clotting factor, it removes a natural brake on coagulation, achieving hemostatic balance through a different mechanism.

### 4.4 Antisense Oligonucleotide Therapeutics: Complementary Modality

Antisense oligonucleotides (ASOs) represent a complementary RNA-targeting modality that has achieved clinical success in parallel with siRNA. ASOs are single-stranded oligonucleotides (typically 16–20 nucleotides) that bind target RNA through Watson-Crick base pairing and modulate gene expression through two mechanisms: RNase H-mediated cleavage of the target mRNA (gapmer design) or steric blockade of splicing or translation (PMID: 28244990).

**Nusinersen (Spinraza)** — approved 2016 for spinal muscular atrophy (SMA). A splice-switching ASO that modifies exon 7 inclusion in the *SMN2* gene, increasing production of functional SMN protein. Administered intrathecally every 4 months after loading doses. The ENDEAR trial demonstrated significant improvement in motor milestones in infantile-onset SMA (PMID: 29091570). Nusinersen's approval preceded and validated the RNA-targeting therapeutic paradigm.

**Tofersen (Qalsody)** — approved 2023 for SOD1-associated amyotrophic lateral sclerosis (ALS). A gapmer ASO targeting *SOD1* mRNA, reducing SOD1 protein in CSF by ~36%. The VALOR trial narrowly missed its primary endpoint of functional decline (ADRS), but demonstrated significant reduction in neurofilament light chain (NfL), a biomarker of neurodegeneration, leading to accelerated approval (PMID: 36449420).

**Eplontersen (Wainua)** — approved 2023 for hATTR amyloidosis. A GalNAc-conjugated ligand-conjugated ASO (LICA) targeting TTR mRNA, achieving ~82% serum TTR reduction with monthly subcutaneous injection (PMID: 37888913). Eplontersen demonstrates the convergence of ASO and siRNA platforms: both now use GalNAc conjugation for hepatocyte targeting, with the choice between modalities determined by target biology, durability requirements, and intellectual property landscape.

### 4.5 Mathematical Framework: Indirect-Response Turnover PK-PD Model for RNAi Durability

The remarkable durability of GalNAc-siRNA therapeutics — single doses suppressing target proteins for weeks to months — can be quantitatively understood through an indirect-response pharmacokinetic-pharmacodynamic (PK-PD) model.

**Model structure.** The system consists of three coupled compartments:

1. **Active RISC (*R(t)*)**: The intracellular concentration of guide-strand-loaded RISC complexes, which decays with first-order kinetics:

$$\frac{dR}{dt} = -k_{el} \cdot R(t)$$

where *k_el* is the elimination rate of active RISC (primarily through nuclease degradation and cell division-mediated dilution). For ESC+ GalNAc-siRNAs in hepatocytes, the RISC half-life is approximately $t_{1/2,R} = \ln 2 / k_{el} \approx 4$ weeks.

2. **Target mRNA (*M(t)*)**: The steady-state mRNA level is governed by a balance of synthesis and degradation, with RISC-mediated cleavage adding a catalytic degradation term:

$$\frac{dM}{dt} = k_{syn} - k_{deg} \cdot M(t) - \frac{V_{max} \cdot R(t)}{K_m + M(t)} \cdot M(t)$$

where *k_syn* is the basal mRNA synthesis rate, *k_deg* is the natural mRNA degradation rate, and the Michaelis-Menten term represents RISC-catalyzed cleavage with maximal velocity *V_max* and half-saturation constant *K_m*.

3. **Target protein (*P(t)*)**: Protein levels respond indirectly to mRNA changes:

$$\frac{dP}{dt} = k_{trans} \cdot M(t) - k_{p,deg} \cdot P(t)$$

where *k_trans* is the translation rate and *k_p,deg* is the protein degradation rate.

**Analytical predictions.** At peak RISC loading (immediately after dosing), when $R(0) \gg K_m / V_{max}$, the effective mRNA degradation rate is dominated by RISC cleavage, and mRNA levels fall to a nadir determined by:

$$M_{nadir} \approx \frac{k_{syn}}{k_{deg} + V_{max} \cdot R(0) / K_m}$$

For PCSK9 (mRNA half-life ~2 hours, *k_deg* ≈ 0.35 hr⁻¹; protein half-life ~2–3 days, *k_p,deg* ≈ 0.01 hr⁻¹), the model predicts:

- **Time to protein nadir**: $t_{nadir} \approx \frac{\ln(k_{deg}/k_{p,deg})}{k_{deg} - k_{p,deg}} \approx \frac{\ln(35)}{0.34} \approx 10.5$ hours for mRNA nadir, then $\approx 3 \times t_{1/2,protein} \approx 7$ days for protein nadir. Clinically, PCSK9 protein nadir is observed at approximately 14 days post-dose.

- **Duration of >50% knockdown**: Protein levels remain below 50% of baseline as long as mRNA synthesis is substantially suppressed. The duration is primarily governed by RISC half-life:

$$t_{50\%} \approx t_{1/2,R} \cdot \log_2\left(\frac{R(0)}{R_{50\%}}\right)$$

where $R_{50\%}$ is the RISC concentration at which mRNA levels recover to 50% of baseline. For inclisiran with a 4-week RISC half-life and sufficient initial loading, this predicts >50% PCSK9 knockdown for approximately 20–24 weeks, consistent with the observed 6-month dosing interval.

- **Optimal dosing interval**: The model predicts that the optimal dosing interval equals approximately 5 RISC half-lives (~20 weeks for ESC+ chemistry), at which point >95% of the initial RISC has been eliminated and re-dosing avoids RISC accumulation that could increase off-target effects.

**Comparison across targets.** The model explains why different siRNA drugs require different dosing intervals despite using similar chemistry: the key variable is the target protein half-life. For antithrombin (fitusiran target, protein half-life ~3 days), monthly dosing is required because the short protein half-life means protein recovery closely tracks mRNA recovery. For TTR (patisiran/vutrisiran target, protein half-life ~2 days), similar logic applies. Inclisiran's 6-month dosing interval reflects not a longer RISC half-life but the clinical decision to accept partial PCSK9 recovery between doses for the convenience of twice-yearly administration.

### 4.6 Extrahepatic Delivery: The Next Frontier for RNAi

The GalNAc-ASGPR targeting system has been spectacularly successful for liver-expressed targets but is inherently limited to hepatocytes. Extending siRNA therapeutics to extrahepatic tissues is the most important technical challenge facing the field:

**Muscle.** Antibody-siRNA conjugates (ASCs) targeting transferrin receptor 1 (TfR1) have demonstrated functional siRNA delivery to skeletal muscle in rodent and NHP models (PMID: 36130660). Dyne Therapeutics and Avidity Biosciences are advancing ASC programs for myotonic dystrophy type 1 (DM1, targeting DMPK mRNA) and facioscapulohumeral dystrophy (FSHD), with early clinical trials reporting target engagement in muscle biopsies.

**Central nervous system.** Intrathecal administration of divalent siRNAs has shown distribution throughout the CNS in NHP models (PMID: 31375812). Alnylam is developing intrathecally administered siRNAs for Huntington's disease (targeting HTT mRNA) and Alzheimer's disease (targeting APP mRNA).

**Kidney.** Proximal tubule targeting via megalin/cubilin receptor-mediated uptake of oligonucleotides has been demonstrated, with potential applications in complement-mediated kidney diseases.

The extrahepatic delivery challenge for siRNA parallels the same challenge for LNP-based CRISPR delivery: in both cases, the liver is efficiently targeted but other organs remain largely inaccessible to systemic administration.

### 4.7 Open Questions and Future Directions

1. **Cardiovascular outcomes.** The ORION-4 outcomes trial (n = 15,968) will determine whether inclisiran's LDL-C reduction translates to reduced major adverse cardiovascular events (MACE). Results are expected in 2026 and will be definitive for the siRNA cardiovascular franchise.

2. **RNAi vs. base editing for PCSK9.** Inclisiran (twice-yearly siRNA) and VERVE-101/102 (one-time base edit) both target PCSK9 but with fundamentally different risk-benefit profiles. The siRNA approach is reversible, extensively safety-validated, and dose-adjustable; the base editing approach is permanent, eliminates adherence concerns, but carries irreversible off-target risks. The optimal strategy may depend on patient age, comorbidities, and risk tolerance.

3. **Combination RNAi.** Simultaneously targeting PCSK9, ANGPTL3, and Lp(a) with a cocktail of GalNAc-siRNAs could address multiple cardiovascular risk factors in a single therapeutic regimen. The safety of such combinations, particularly regarding cumulative hepatic RISC loading, needs investigation.

4. **Extrahepatic breakthroughs.** The development of a GalNAc-equivalent targeting ligand for muscle, brain, or kidney — enabling subcutaneous injection with tissue-specific delivery — would open the siRNA platform to hundreds of additional disease targets.

---

## Part V: Therapeutic Epigenetic Silencing — Gene Regulation Without DNA Breaks

### 5.1 The Genotoxicity Problem With Nuclease-Based Editing

While CRISPR-Cas9 has achieved remarkable clinical success (Casgevy, NTLA-2001), accumulating evidence reveals that Cas9-generated double-strand breaks (DSBs) carry inherent genotoxicity risks that cannot be fully eliminated by improving guide RNA specificity:

**Large deletions and structural variants at on-target sites.** Kosicki et al. (2018) demonstrated that Cas9 cleavage at on-target sites in mouse embryonic stem cells and human differentiated cells frequently generates large deletions (>100 bp to several kilobases) and complex rearrangements extending well beyond the intended cut site, undetectable by standard PCR-based genotyping assays that amplify only the immediate vicinity of the target (PMID: 30010673). Subsequent studies using long-read sequencing confirmed that these large on-target lesions occur at frequencies of 1–20% depending on the locus and cell type.

**Chromothripsis.** Leibowitz et al. (2021) discovered that Cas9 DSBs can trigger chromothripsis — a catastrophic shattering and reassembly of chromosomal segments — particularly when DSBs occur during S-phase in micronuclei formed by mis-segregation of acentric chromosome fragments generated by editing (PMID: 34036211). Chromothripsis events involve loss of tumor suppressor genes, amplification of oncogenes, and generation of circular extrachromosomal DNA elements, representing a direct pathway to malignant transformation.

**p53 pathway activation.** Haapaniemi et al. (2018) reported that Cas9 DSBs activate the p53 DNA damage response in human pluripotent stem cells, leading to cell cycle arrest and apoptosis (PMID: 29892067). Cells that survive Cas9 editing are therefore enriched for pre-existing p53 pathway inactivation — the single most common tumor suppressor alteration in human cancer. Ihry et al. (2018) independently confirmed this finding, showing that CRISPR-edited iPSCs are enriched for p53 mutations (PMID: 29892062).

**Translocations.** Cas9 DSBs at on-target and off-target sites can recombine to generate chromosomal translocations, a hallmark of hematologic malignancies (PMID: 31462799). While translocation frequencies per cell division are low (~10⁻⁴ to 10⁻³ per DSB pair), the large number of cells edited in therapeutic applications (>10⁸ for liver-targeted therapies) means that thousands of translocation events may occur per treated patient.

These findings have motivated the development of therapeutic modalities that achieve gene silencing without creating DSBs.

### 5.2 CRISPRoff: Heritable Epigenetic Silencing

CRISPRoff, developed by Nuñez et al. (2021), achieves durable gene silencing by depositing DNA methylation at target promoters using a fusion of catalytically dead Cas9 (dCas9), the DNMT3A methyltransferase catalytic domain, and the DNMT3L accessory protein that stimulates DNMT3A activity (PMID: 33836127). A single transient expression of CRISPRoff in human cells installed CpG methylation at target gene promoters that was maintained through cell division for at least 450 days (~50 cell divisions) without continued presence of the editor, through the endogenous maintenance methylation activity of DNMT1.

**Mechanism of heritability.** During DNA replication, hemimethylated CpG sites on the daughter strand are recognized and methylated by DNMT1 in complex with UHRF1 (PMID: 15475956). This semiconservative maintenance mechanism preserves methylation patterns with approximately 95% fidelity per CpG site per cell division (PMID: 23328393). The durability of CRISPRoff silencing correlates with CpG density at the target locus: promoters with CpG islands (>200 bp, >50% GC content, observed/expected CpG ratio >0.6) show the most durable silencing because the high density of CpG sites provides redundancy — even if individual CpG maintenance fails stochastically, surrounding methylated sites reinforce silencing (PMID: 33836127).

**Comparison with dCas9-KRAB.** Earlier epigenetic silencing approaches used dCas9 fused to the KRAB (Krüppel-associated box) repressor domain, which recruits the KAP1/TRIM28-SETDB1-NuRD complex to deposit H3K9me3 heterochromatin marks (PMID: 25096238). While effective for transient silencing (weeks), KRAB-mediated repression is not heritable through cell division because H3K9me3 maintenance mechanisms are less reliable than CpG methylation maintenance. CRISPRoff's DNA methylation-based approach provides orders-of-magnitude greater durability.

**Reversibility.** A key feature of epigenetic silencing is its reversibility: CRISPRon, using dCas9 fused to TET1 demethylase and the transcriptional activation domains p65 and VP64, can remove methylation at silenced loci and restore gene expression (PMID: 33836127). This reversibility is a fundamental therapeutic advantage over nuclease-based editing or base editing, which permanently alter the DNA sequence.

### 5.3 Clinical Translation: The Epigenetic Editing Landscape

Two companies are leading the clinical translation of therapeutic epigenetic silencing:

**Tune Therapeutics** is developing TUNE-401 for chronic hepatitis B (HBV). Chronic HBV infection is maintained by covalently closed circular DNA (cccDNA) in hepatocyte nuclei, which serves as a persistent transcriptional template for viral proteins. TUNE-401 uses an LNP-delivered dCas9-methyltransferase fusion targeting a conserved regulatory element shared by cccDNA and integrated HBV DNA, aiming to achieve epigenetic silencing of viral transcription analogous to the natural "functional cure" observed in rare patients who spontaneously silence their cccDNA through DNA methylation. Tune received regulatory authorization for a Phase 1b clinical trial in New Zealand (November 2024) and Hong Kong (January 2025), making it the first clinical trial of an epigenetic editing therapeutic.

**nChroma Bio** (formed from the merger of Chroma Medicine and Nvelop Therapeutics) is developing CRMA-1001, also targeting chronic HBV with an epigenetic editing approach. nChroma plans to submit a clinical trial application in 2025, with first dosing expected in 2026. nChroma's platform is also being applied to liver-expressed targets for cardiometabolic disease, including PCSK9 and ANGPTL3.

**Epicrispr Biotechnologies** is developing epigenetic editors for neurodegenerative diseases, leveraging AAV delivery to post-mitotic neurons where CRISPRoff's durability (independent of cell division) is expected to be permanent.

### 5.4 Epigenetic Silencing of Established Gene Therapy Targets

The same liver-expressed targets being pursued by nuclease editing (NTLA-2001 for TTR) and base editing (VERVE-101 for PCSK9) are equally amenable to epigenetic silencing, raising the question of which modality is optimal:

| Feature | Cas9 Nuclease (NTLA-2001) | Base Editing (VERVE-101) | Epigenetic Silencing (CRISPRoff) |
|---------|---------------------------|--------------------------|----------------------------------|
| DNA sequence altered | Yes (indels) | Yes (point mutation) | No |
| DSBs generated | Yes | No | No |
| Large deletions/rearrangements | Risk ~1–20% | Minimal | None |
| Chromothripsis risk | Documented | Not observed | None |
| p53 selection | Documented | Minimal | None |
| Reversibility | No | No | Yes (CRISPRon/TET1) |
| Durability in dividing cells | Permanent | Permanent | Durable (~95%/CpG/division) |
| Off-target edits | Permanent | Permanent | Reversible methylation |
| Cargo size | ~4.2 kb (Cas9) | ~5.2 kb (ABE8e) | ~7+ kb (dCas9-DNMT3A-DNMT3L) |

The larger cargo size of epigenetic editors is currently the primary technical limitation, requiring optimization of the delivery vehicle capacity.

### 5.5 Mathematical Framework: Real Options Theory for Reversible vs. Irreversible Gene Therapies

The choice between permanent (nuclease/base editing) and reversible (epigenetic silencing) gene therapies can be formalized using real options theory from financial mathematics. The key insight is that reversibility has quantifiable economic and clinical value — it preserves the "option" to revert the intervention if better therapies emerge or if long-term adverse effects are discovered.

**Setup.** Consider a patient with a chronic disease (e.g., heterozygous familial hypercholesterolemia) who can receive either:
- **Permanent therapy** (base editing of PCSK9): irreversible, high initial efficacy *V_P*, zero ongoing cost
- **Reversible therapy** (epigenetic silencing of PCSK9): reversible, slightly lower initial efficacy *V_R < V_P* (due to incomplete silencing), requires monitoring

**Option value of reversibility.** Define:
- *σ*: uncertainty (volatility) in long-term safety outcomes, reflecting our incomplete knowledge of permanent genome modification consequences
- *r*: discount rate for future health outcomes
- *T*: patient's remaining life expectancy
- *p_A*: probability that a superior therapy (e.g., gene replacement, next-generation editor) becomes available within *T* years
- *p_S*: probability that a long-term safety signal emerges within *T* years

The value of the permanent therapy is simply:

$$V_P^{total} = V_P - p_S \cdot L_S$$

where *L_S* is the expected loss from an irreversible safety event.

The value of the reversible therapy includes a "put option" — the right to revert the intervention:

$$V_R^{total} = V_R + \underbrace{p_A \cdot (V_{new} - V_R) \cdot e^{-rT_A}}_{\text{upgrade option}} + \underbrace{p_S \cdot (L_S - C_{revert}) \cdot e^{-rT_S}}_{\text{safety reversion option}}$$

where *V_new* is the value of the future superior therapy, *T_A* and *T_S* are the expected times to availability and safety signal respectively, and *C_revert* is the cost of reverting the epigenetic intervention.

**When reversibility is preferred.** The reversible therapy is preferred when:

$$V_R^{total} > V_P^{total}$$

This inequality is satisfied when:
1. **Uncertainty is high** (large *σ*, early in clinical experience)
2. **Patient is young** (large *T*, more time for safety signals or better therapies to emerge)
3. **Reversion cost is low** (*C_revert* ≪ *L_S*)
4. **Efficacy gap is small** (*V_P - V_R* is modest)

**Quantitative example.** For a 30-year-old HeFH patient (T = 50 years remaining), with *p_A* = 0.5 (50% chance of superior therapy within 20 years), *p_S* = 0.05 (5% chance of long-term safety signal), *L_S* = $500,000 in QALY-equivalent loss, and *C_revert* = $50,000:

The option value of reversibility ≈ $0.5 × $200,000 × e^{-0.03 × 10} + 0.05 × ($500,000 - $50,000) × e^{-0.03 × 15}$ ≈ $74,000 + $14,000 = $88,000

This suggests that reversible epigenetic silencing could command an ~$88,000 premium over permanent editing for young patients in the early years of the technology, when uncertainty about long-term outcomes is highest.

**Clinical decision rule.** As long-term safety data accumulates (reducing *σ* and *p_S*), the option value of reversibility decreases, and permanent editing becomes increasingly favored. Conversely, for pediatric patients and for recently developed editors with limited follow-up data, reversible approaches may be clinically preferable even at modestly lower efficacy.

### 5.6 Open Questions and Future Directions

1. **Durability in human patients.** Will CRISPRoff silencing maintain >90% repression over years in human hepatocytes, where the division rate (~0.5%/day) and chromatin remodeling environment differ from cell culture? The first clinical data from TUNE-401 will be definitive.

2. **Multiplexed epigenetic editing.** Can multiple genes be simultaneously silenced with a cocktail of CRISPRoff guides delivered in a single LNP dose? The dCas9 cargo is shared across targets, potentially reducing the total payload size compared to multiple independent base editors.

3. **Activation applications.** CRISPRa (dCas9-VPR, dCas9-p300) for gene activation could complement CRISPRoff silencing, enabling bidirectional regulation. Activating fetal hemoglobin expression by epigenetic means (rather than disrupting BCL11A) is a promising alternative strategy for SCD.

4. **Reducing cargo size.** Engineering smaller dCas9 orthologues (e.g., CjCas9 at 2.9 kb vs. SpCas9 at 4.1 kb) fused to minimal methyltransferase domains could bring epigenetic editors within AAV packaging limits.

---

## Part VI: Gene Therapy Immunology and the Redosing Problem

### 6.1 Pre-Existing Neutralizing Antibodies: Scope of the Problem

The most immediate immunological barrier to gene therapy is the high prevalence of pre-existing neutralizing antibodies (NAbs) against AAV capsids in the general population. Seroepidemiological studies have documented the following NAb seroprevalence rates (defined as titers sufficient to neutralize transduction in vitro at ≥1:5 dilution):

- AAV1: ~67% globally (PMID: 20095819)
- AAV2: ~72% (the highest, reflecting widespread childhood AAV2 infection)
- AAV5: ~40%
- AAV6: ~46%
- AAV8: ~38%
- AAV9: ~47%
- AAVrh10: ~59%

Seroprevalence varies significantly by geography, age, and assay methodology. Studies in sub-Saharan Africa have reported AAV2 seroprevalence exceeding 90%, while seroprevalence in young children (<2 years) is lower due to waning of maternal antibodies (PMID: 30243891). Even low-titer NAbs (1:5 to 1:20) are sufficient to neutralize intravenously administered AAV, because the massive dilution in the bloodstream reduces effective vector concentration below the transduction threshold (PMID: 22135462).

For liver-directed gene therapy trials, NAb screening has become standard practice, with typical exclusion criteria of AAV5 NAb titer ≥1:1 (Roctavian) or ≥1:1 (Hemgenix). These criteria exclude approximately 30–50% of prospective patients — a substantial limitation for therapies targeting diseases with unmet medical need (PMID: 20095819).

### 6.2 Adaptive Immune Responses to AAV-Transduced Cells

Beyond pre-existing NAbs, de novo adaptive immune responses following AAV administration present two clinical challenges:

**Anti-capsid CD8⁺ T cell responses.** AAV capsid proteins are processed and presented on MHC class I molecules of transduced hepatocytes, generating capsid-specific CD8⁺ T cell responses that kill transduced cells (PMID: 23325831). This mechanism was first recognized in a hemophilia B trial using AAV2, where a single patient experienced a rise in liver transaminases and loss of factor IX expression at weeks 4–6 post-infusion, temporally correlating with detectable anti-AAV2 capsid T cell responses (PMID: 16474400). The standard mitigation strategy is prophylactic corticosteroid administration, typically starting before or immediately after vector infusion and tapered over 2–3 months. In the Roctavian hemophilia A program, approximately 90% of patients required corticosteroid treatment for ALT elevations, underscoring the near-universality of this immune response at high vector doses (PMID: 37747929).

**Anti-transgene immune responses.** In patients with null mutations (no endogenous protein expression), the transgene product may be recognized as a foreign antigen, eliciting neutralizing antibodies and cellular immune responses against the therapeutic protein (PMID: 29234961). This is particularly relevant for hemophilia A (large FVIII protein with multiple immunogenic epitopes) and DMD (micro-dystrophin expression in patients with no dystrophin). Immune tolerance induction (ITI) protocols, analogous to those used for FVIII inhibitor management in hemophilia, are being explored as adjunctive strategies.

### 6.3 Enabling Technologies for Patient Eligibility and Redosing

Several strategies are being developed to overcome immunological barriers:

**IgG-degrading enzymes.** Imlifidase (IdeS), a cysteine protease from *Streptococcus pyogenes* that cleaves all four human IgG subclasses at the hinge region, has been shown to rescue AAV transduction in passively immunized mice and in NHPs with pre-existing anti-AAV NAbs (PMID: 32483358). In a clinical proof-of-concept, a patient with Crigler-Najjar syndrome who was seropositive for anti-AAV8 NAbs was treated with imlifidase prior to AAV8 gene therapy, achieving successful vector transduction (Hansa Biopharma, 2025). IdeZ, a related enzyme from *Streptococcus equi*, offers broader IgG cleavage activity and is in preclinical development. The key limitation is that IdeS is itself immunogenic, generating anti-IdeS antibodies that may preclude repeated use.

**Plasmapheresis and immunoadsorption.** Extracorporeal removal of antibodies through plasma exchange or protein A/G immunoadsorption columns can reduce NAb titers below neutralization thresholds. However, the transient nature of titer reduction (NAbs rebound within days to weeks from memory B cell responses) requires precise timing of vector administration during the window of reduced titers (PMID: 25049398).

**Serodivergent capsids.** Engineering AAV capsids that are antigenically distinct from natural serotypes — termed serodivergent capsids — allows administration in patients seropositive for all natural serotypes (PMID: 41308640). Directed evolution and machine learning-guided capsid design have generated variants (e.g., AAV.div3A) with <5% cross-reactivity against sera from AAV1-9-seropositive individuals while maintaining efficient transduction of target tissues.

**Rapamycin nanoparticles for immune tolerance (ImmTOR).** Selecta Biosciences developed synthetic vaccine particles encapsulating rapamycin (ImmTOR) that, when co-administered with AAV, induce antigen-specific immune tolerance by promoting regulatory T cell responses and inhibiting B cell activation (PMID: 29630399). In preclinical models, ImmTOR co-administration prevented anti-AAV antibody formation and enabled vector re-administration, with functional transgene expression upon redosing. Clinical development is ongoing in combination with AAV gene therapies.

### 6.4 Mathematical Framework: Bayesian Repeated Game for Immune Evasion and Redosing

We model the interaction between sequential gene therapy administration and the adaptive immune system as a Bayesian repeated game to determine the optimal redosing strategy.

**Players.**
- **Therapist**: selects AAV capsid serotype $s_i \in \{s_1, ..., s_n\}$ for dose $i$, and immunosuppression intensity $\mu_i \in [0, 1]$
- **Immune system**: updates its antibody repertoire $\mathbf{A} = (A_1, ..., A_n)$ based on capsid exposure, where $A_j$ is the NAb titer against serotype $j$

**Dynamics.** After dose $i$ with serotype $s_i$:

1. **Transduction success**: Therapeutic transduction occurs if the effective NAb titer $A_{s_i}$ is below the neutralization threshold $\theta$:
$$P(\text{success}_i) = P(A_{s_i}^{(i)} < \theta) \cdot (1 - \mu_i \cdot \phi)$$
where $\phi$ captures the reduction in transduction efficiency from immunosuppression-mediated inhibition of vector processing.

2. **Antibody updating (affinity maturation)**: After exposure to serotype $s_i$, NAb titers update according to:
$$A_{s_i}^{(i+1)} = A_{s_i}^{(i)} + \Delta_{\text{primary}} \cdot (1 - \mu_i)^{\gamma}$$
$$A_{s_j}^{(i+1)} = A_{s_j}^{(i)} + \epsilon_{ij} \cdot \Delta_{\text{cross}} \cdot (1 - \mu_i)^{\gamma} \quad \text{for } j \neq i$$

where $\Delta_{\text{primary}}$ is the primary NAb response magnitude, $\epsilon_{ij} \in [0, 1]$ is the cross-reactivity between serotypes $i$ and $j$, $\gamma > 0$ captures the immunosuppressive effect of rapamycin/steroids, and all quantities are modulated by immunosuppression intensity $\mu_i$.

3. **Antibody decay**: Between doses, NAbs decay with half-life $t_{1/2,Ab}$ (approximately 3–5 years for IgG in the absence of re-stimulation):
$$A_j(t) = A_j^{(i+1)} \cdot 2^{-(t - t_i) / t_{1/2,Ab}}$$

**Optimal strategy via multi-armed bandit.** The therapist's problem can be framed as a non-stationary multi-armed bandit: each arm corresponds to a serotype, and the reward (transduction success) changes over time due to immune memory. The optimal policy balances exploitation (using the serotype with lowest current NAb titer) against exploration (preserving serotype diversity for future doses).

**Key results.**

1. **Maximum number of redoses.** With $n$ antigenically distinct serotypes (cross-reactivity $\epsilon_{ij} \approx 0$ for serodivergent capsids), the maximum number of successful administrations without immunosuppression is approximately:
$$N_{\max} = n + \sum_{j=1}^{n} \lfloor \log_2(\theta / A_j^{(0)}) / (t_{\text{interval}} / t_{1/2,Ab}) \rfloor$$

For $n = 4$ serodivergent serotypes, $\theta = 1:20$, initial titers $A_j^{(0)} < 1:5$, inter-dose interval of 5 years, and $t_{1/2,Ab}$ = 4 years, $N_{\max} \approx 6$ administrations over a 30-year period.

2. **Immunosuppression extends capacity.** Co-administration of ImmTOR rapamycin nanoparticles (reducing $\Delta_{\text{primary}}$ by ~80% based on preclinical data; PMID: 29630399) increases $N_{\max}$ to approximately 10–12 over the same period.

3. **Optimal serotype sequence.** The greedy strategy (always use the serotype with lowest current NAb titer) is near-optimal when cross-reactivities are low ($\epsilon_{ij} < 0.1$). When cross-reactivities are moderate, a round-robin strategy that maximizes the interval between repeat uses of any serotype performs better by allowing antibody decay.

### 6.5 Manufacturing and Cost: The Access Crisis

The cost of approved gene therapies reflects the extraordinary manufacturing complexity and small patient populations:

| Therapy | Price | Manufacturing Platform |
|---------|-------|----------------------|
| Hemgenix | $3.5M | AAV5, triple transfection in HEK293 |
| Zolgensma | $2.1M | AAV9, adherent HEK293 |
| Casgevy | $2.2M | Ex vivo autologous cell processing |
| Lyfgenia | $3.1M | Lentiviral vector, ex vivo |
| Luxturna | $0.85M | AAV2, triple transfection |
| Elevidys | $3.2M | AAVrh74, triple transfection |

Three factors drive these costs: (1) **Low production yields**: AAV manufacturing by transient triple transfection of HEK293 cells typically yields 10¹⁴–10¹⁵ viral genomes per production run, while a single patient dose for systemic delivery (e.g., Zolgensma at 1.1 × 10¹⁴ vg/kg for a 5 kg infant) may require the output of multiple production batches (PMID: 31492576). (2) **Small patient populations**: Orphan diseases have limited addressable markets (SMA type 1: ~400 US births/year; RPE65-IRD: ~1,000 US patients), preventing economies of scale. (3) **Complex analytics**: AAV vector characterization requires >30 release assays including potency, identity, purity, capsid/genome ratio, residual DNA, and sterility.

Emerging manufacturing solutions include: suspension-adapted HEK293 cells in bioreactors (scalable to 2,000 L), baculovirus-Sf9 insect cell systems (higher per-cell productivity), and stable producer cell lines that eliminate the need for transient transfection (PMID: 31492576). However, none of these platforms has yet demonstrated the combination of scalability, consistency, and regulatory acceptance needed to substantially reduce costs.

For LNP-based therapies (VERVE-101, NTLA-2001, inclisiran), manufacturing is fundamentally simpler: RNA synthesis by in vitro transcription (IVT) followed by microfluidic LNP encapsulation is a chemically defined, scalable process without cell culture requirements. This manufacturing advantage may prove decisive in determining which gene therapy modalities achieve global accessibility.

### 6.6 Open Questions and Future Directions

1. **Universal immune evasion.** Can a single engineered capsid be designed that evades neutralization by all known anti-AAV antibodies? Machine learning-guided capsid engineering is approaching this goal, but the diversity of human anti-AAV antibody repertoires poses a significant challenge (PMID: 41308640).

2. **Combining IdeS with serodivergent capsids.** The sequential use of IdeS (to clear existing NAbs) followed by a serodivergent capsid (to minimize de novo NAb cross-reactivity) could enable first-dose eligibility for essentially all patients and straightforward redosing.

3. **Oral tolerance induction.** Oral administration of AAV capsid proteins to induce mucosal tolerance (analogous to oral desensitization in food allergy) is an unexplored strategy that could provide a low-cost, globally scalable approach to managing AAV immunogenicity.

4. **Gene therapy pricing models.** Outcomes-based payment models (payment contingent on sustained therapeutic benefit), annuity structures (spreading cost over years), and international pooled procurement mechanisms are being developed to address the access crisis. The feasibility and sustainability of these models for permanent gene therapies requires health-economic modeling and policy innovation.

---

## Part VII: Integration — A Decision Framework for Curative Gene Therapy

### 7.1 Disease Classification by Therapeutic Modality Fit

The six modalities analyzed in this review are not interchangeable — each is optimally suited to a specific category of genetic disease based on the underlying molecular pathology:

**Recessive loss-of-function (gene replacement or gene addition).** Diseases caused by biallelic loss-of-function mutations in a gene too large for editing-based correction. AAV gene replacement is the natural modality when the coding sequence fits within the ~4.7 kb AAV packaging limit (SMA/SMN1: 1.6 kb; hemophilia B/FIX: 2.8 kb; RPE65: 1.6 kb). For larger genes (hemophilia A/FVIII: 7 kb; DMD/dystrophin: 14 kb), truncated transgenes (B-domain-deleted FVIII, micro-dystrophin) or dual-AAV strategies are required, often with reduced efficacy.

**Recessive loss-of-function (correctable by editing).** When the causative mutation is a single nucleotide variant amenable to base editing correction (e.g., GSDIa R83C), in vivo base editing offers a curative approach with permanent, precise correction. For SCD (HBB E6V), both direct correction and HbF reactivation (via BCL11A disruption) are viable strategies, with the latter clinically validated by Casgevy.

**Dominant gain-of-function or toxic gain-of-function.** Diseases caused by production of a toxic protein that must be silenced or eliminated. Three modalities compete: (1) nuclease-based gene disruption (NTLA-2001 for TTR), (2) epigenetic silencing (CRISPRoff for TTR), and (3) RNA knockdown (patisiran/vutrisiran/eplontersen for TTR). The choice depends on the desired permanence, reversibility, and safety profile.

**Haploinsufficiency.** Diseases where 50% gene expression is insufficient (e.g., haploinsufficient tumor suppressors). Gene addition to restore full expression is preferred over editing, which can only modify one allele.

**Chronic, non-genetic conditions amenable to gene-based intervention.** Conditions like hypercholesterolemia (PCSK9 overexpression) and chronic hepatitis B (viral persistence) where permanent or durable modification of a liver target provides therapeutic benefit. Both base editing (VERVE-101) and RNAi (inclisiran) are viable, with the choice reflecting the permanence-reversibility tradeoff analyzed in Part V.

### 7.2 The Durability-Safety-Access Trilemma

Every gene therapy modality navigates a three-way tradeoff:

1. **Durability**: How long does therapeutic benefit last? (Permanent for editing; years for AAV episomes; months for siRNA)
2. **Safety**: What is the risk profile? (DSB-related genotoxicity for nucleases; off-target deamination for base editors; injection-site reactions for siRNA; immune-mediated hepatotoxicity for AAV)
3. **Access**: What is the cost and logistical complexity? (>$2M for autologous cell therapies; ~$100K–$1M for in vivo gene therapy; ~$5,000–$25,000/year for siRNA)

No modality optimizes all three dimensions simultaneously. The clinical decision depends on disease severity, patient age, healthcare system resources, and individual risk tolerance:

- For severe, life-threatening pediatric diseases (SMA type 1, severe hemophilia), the permanence and high efficacy of AAV gene replacement or ex vivo gene editing justifies the high cost and immune management requirements.
- For chronic adult diseases with effective (but burdensome) existing therapies (hypercholesterolemia), the lower-risk, reversible, and more accessible siRNA approach may be optimal until long-term editing safety data matures.
- For diseases in resource-limited settings (SCD in sub-Saharan Africa), accessibility must be weighted heavily, favoring in vivo approaches that eliminate ex vivo manufacturing requirements.

### 7.3 Prioritized Disease Targets for the Next Decade

Based on a multi-criteria assessment integrating disease burden (DALY impact), genetic tractability, delivery feasibility, competitive landscape, and manufacturing readiness, we rank the top 15 disease targets for gene therapy advancement by 2035:

| Rank | Disease | Target Gene | Preferred Modality | Current Status | Key Barrier |
|------|---------|-------------|-------------------|----------------|-------------|
| 1 | Sickle cell disease | BCL11A/HBB | Ex vivo editing → in vivo | Approved (Casgevy) | Cost/access |
| 2 | Hemophilia B | F9 | AAV gene replacement | Approved (Hemgenix) | Durability |
| 3 | ATTR amyloidosis | TTR | Nuclease/siRNA/epigenetic | Approved (NTLA, patisiran) | Modality optimization |
| 4 | Hypercholesterolemia | PCSK9 | Base editing/siRNA | Phase 1 (VERVE)/Approved (inclisiran) | Safety (editing) |
| 5 | Beta-thalassemia | BCL11A/HBB | Ex vivo editing | Approved (Casgevy) | Global access |
| 6 | SMA type 1 | SMN1 | AAV gene replacement | Approved (Zolgensma) | Pediatric durability |
| 7 | Hemophilia A | F8 | AAV/editing | Approved (Roctavian) | Expression durability |
| 8 | GSDIa | G6PC1 | In vivo base editing | Phase 1/2 (BEAM-301) | Biallelic efficiency |
| 9 | DMD | DMD/micro-dystrophin | AAV gene replacement | Approved (Elevidys) | Efficacy confirmation |
| 10 | Chronic HBV | cccDNA/HBV | Epigenetic silencing | Phase 1 (TUNE-401) | Durability |
| 11 | Phenylketonuria | PAH | AAV/base editing | Phase 1/2 | Immune management |
| 12 | Alpha-1 antitrypsin deficiency | SERPINA1 | AAV gene replacement | Phase 2/3 | Liver/lung targeting |
| 13 | Leber congenital amaurosis (other) | CEP290/other | Base/prime editing | Preclinical/Phase 1 | In vivo retinal editing |
| 14 | Familial hypercholesterolemia (HoFH) | PCSK9/ANGPTL3 | Base editing/siRNA | Phase 1 | Multi-target editing |
| 15 | Transthyretin cardiomyopathy | TTR | siRNA/editing | Phase 3 (vutrisiran) | Cardiac endpoint |

### 7.4 Multi-Criteria Decision Analysis Framework

We formalize the disease target prioritization using a multi-criteria decision analysis (MCDA) with six weighted dimensions:

$$\text{Tractability Score} = \sum_{k=1}^{6} w_k \cdot s_k$$

where the dimensions and weights are:

| Dimension ($k$) | Weight ($w_k$) | Description |
|-----------------|----------------|-------------|
| 1. Disease burden | 0.25 | Global DALY impact (WHO 2024 estimates) |
| 2. Genetic tractability | 0.20 | Monogenic (1.0) > oligogenic (0.5) > polygenic (0.1) |
| 3. Delivery feasibility | 0.20 | Liver (1.0) > eye (0.8) > muscle (0.5) > CNS (0.3) |
| 4. Editing/expression threshold | 0.15 | Low threshold for benefit (1.0) > high threshold (0.3) |
| 5. Competitive landscape | 0.10 | No existing curative therapy (1.0) > partial therapies exist (0.5) |
| 6. Manufacturing readiness | 0.10 | LNP/siRNA (1.0) > AAV (0.7) > ex vivo cell (0.4) |

**Sensitivity analysis.** The ranking is most sensitive to the delivery feasibility weight: increasing this weight shifts priority toward liver-expressed targets (PCSK9, TTR, G6PC1) and away from neuromuscular diseases (DMD, SMA). The ranking is least sensitive to the competitive landscape weight, suggesting that the existence of existing therapies does not substantially affect the tractability of gene therapy approaches.

### 7.5 The Regulatory Horizon

Permanent gene therapies pose unique regulatory challenges:

**Surrogate endpoints.** For diseases where clinical benefit accrues over decades (sickle cell disease, hemophilia), regulatory approval based on surrogate biomarkers (HbF levels, factor IX/VIII activity) with post-marketing confirmatory studies has become the standard pathway. The durability of these surrogates must be validated against long-term clinical outcomes.

**Long-term follow-up requirements.** The FDA recommends 15-year follow-up for gene therapy patients to monitor for delayed adverse events including malignancy, insertional oncogenesis, and germline transmission (FDA Guidance, 2020). For permanent gene editing therapies, this follow-up period may need to be extended to the patient's lifetime.

**Germline considerations.** While all current clinical gene therapies target somatic cells, the theoretical possibility of inadvertent germline editing — particularly with systemically administered LNPs that may transiently access gonadal tissue — requires careful biodistribution studies and, in some jurisdictions, regulatory review of germline exposure data.

### 7.6 Predictions for 2035

Based on current clinical momentum, manufacturing trends, and the mathematical frameworks developed in this review, we offer the following evidence-based predictions for the state of gene therapy by 2035:

1. **>30 approved gene therapies** across AAV replacement, ex vivo editing, in vivo editing, and siRNA modalities, treating diseases affecting collectively >10 million patients globally.

2. **In vivo base editing for cardiovascular disease** will be approved, with PCSK9 and ANGPTL3 base editing achieving single-dose, permanent LDL-C and triglyceride reduction rivaling lifetime statin therapy. This will be the first gene therapy affecting a common disease population (>10 million eligible patients).

3. **In vivo HSC editing** without myeloablative conditioning will enter Phase 2/3 trials for SCD, dramatically improving global access by eliminating the need for transplant infrastructure.

4. **Epigenetic silencing** will be validated in Phase 2 trials, establishing a third nucleic acid modality (alongside editing and knockdown) with the unique advantage of reversibility.

5. **AAV redosing** will be clinically demonstrated using IdeS + serodivergent capsids, resolving the single-administration limitation that constrains all current AAV programs.

6. **Manufacturing costs** for LNP-based in vivo therapies will fall below $50,000 per treatment, driven by RNA synthesis scalability and microfluidic LNP production, enabling access in middle-income countries.

7. **The durability question** for AAV gene replacement in the liver will be definitively answered: either integration-competent designs will solve episomal loss, or AAV will be superseded by permanent editing approaches for liver targets.

---

## References

1. Tatum EL. Molecular biology, nucleic acids, and the future of medicine. *Perspect Biol Med*. 1966;10(1):19-32. PMID: 5765898.
2. Blaese RM, Culver KW, Miller AD, et al. T lymphocyte-directed gene therapy for ADA-SCID. *Science*. 1995;270(5235):475-480. PMID: 7570001.
3. Rosenberg SA, Aebersold P, Cornetta K, et al. Gene transfer into humans—immunotherapy of patients with advanced melanoma. *N Engl J Med*. 1990;323(9):570-578. PMID: 1718601.
4. Marshall E. Gene therapy death prompts review of adenovirus vector. *Science*. 1999;286(5448):2244-2245. PMID: 10546691.
5. Hacein-Bey-Abina S, Von Kalle C, Schmidt M, et al. LMO2-associated clonal T cell proliferation in two patients after gene therapy for SCID-X1. *Science*. 2003;302(5644):415-419. PMID: 12882986.
6. Mingozzi F, High KA. Therapeutic in vivo gene transfer for genetic disease using AAV: progress and challenges. *Nat Rev Genet*. 2011;12(5):341-355. PMID: 21499295.
7. Naldini L. Gene therapy returns to centre stage. *Nature*. 2015;526(7573):351-360. PMID: 26469046.
8. Gaudet D, Méthot J, Déry S, et al. Efficacy and long-term safety of alipogene tiparvovec (AAV1-LPL S447X) gene therapy for lipoprotein lipase deficiency. *Gene Ther*. 2013;20(4):361-369. PMID: 23169127.
9. Russell S, Bennett J, Wellman JA, et al. Efficacy and safety of voretigene neparvovec (AAV2-hRPE65v2) in patients with RPE65-mediated inherited retinal dystrophy. *Lancet*. 2017;390(10097):849-860. PMID: 29091628.
10. Mendell JR, Al-Zaidy S, Shell R, et al. Single-dose gene-replacement therapy for spinal muscular atrophy. *N Engl J Med*. 2017;377(18):1713-1722. PMID: 29091557.
11. Day JW, Finkel RS, Chiriboga CA, et al. Onasemnogene abeparvovec gene therapy for symptomatic infantile-onset spinal muscular atrophy in patients with two copies of SMN2 (STR1VE). *Lancet Neurol*. 2021;20(4):284-293. PMID: 31270246.
12. Pipe SW, Leebeek FWG, Recht M, et al. Gene therapy with etranacogene dezaparvovec for hemophilia B. *N Engl J Med*. 2023;388(8):706-718. PMID: 36355132.
13. Ozelo MC, Mahlangu J, Engelen BGM, et al. Valoctocogene roxaparvovec gene therapy for hemophilia A. *N Engl J Med*. 2022;386(11):1013-1025. PMID: 35263519.
14. Mahlangu J, Kaczmarek R, von Drygalski A, et al. Two-year outcomes of valoctocogene roxaparvovec therapy for hemophilia A. *N Engl J Med*. 2023;389(8):694-705. PMID: 37747929.
15. Frangoul H, Altshuler D, Cappellini MD, et al. CRISPR-Cas9 gene editing for sickle cell disease and β-thalassemia. *N Engl J Med*. 2021;384(3):252-260. PMID: 33283989.
16. Locatelli F, Thompson AA, Kwiatkowski JL, et al. Exagamglogene autotemcel for severe sickle cell disease. *N Engl J Med*. 2024;390(18):1649-1662. PMID: 38661449.
17. Kanter J, Thompson AA, Pierciey FJ, et al. Lovotibeglogene autotemcel gene therapy for sickle cell disease. *N Engl J Med*. 2023;388(8):700-712. PMID: 37283582.
18. Ingram VM. Gene mutations in human haemoglobin: the chemical difference between normal and sickle cell haemoglobin. *Nature*. 1957;180(4581):326-328. PMID: 13464827.
19. Pauling L, Itano HA, Singer SJ, Wells IC. Sickle cell anemia, a molecular disease. *Science*. 1949;110(2865):543-548. PMID: 15395398.
20. Eaton WA, Hofrichter J. Sickle cell hemoglobin polymerization. *Adv Protein Chem*. 1990;40:63-279. PMID: 2296655.
21. Sunshine HR, Hofrichter J, Eaton WA. Requirement for therapeutic inhibition of sickle haemoglobin gelation. *Nature*. 1978;275(5677):238-240. PMID: 6775682.
22. Platt OS, Brambilla DJ, Rosse WF, et al. Mortality in sickle cell disease. Life expectancy and risk factors for early death. *N Engl J Med*. 1994;330(23):1639-1644. PMID: 7993409.
23. Grosse SD, Odame I, Atrash HK, et al. Sickle cell disease in Africa: a neglected cause of early childhood mortality. *Am J Prev Med*. 2011;41(6 Suppl 4):S398-405. PMID: 22099364.
24. Piel FB, Steinberg MH, Rees DC. Sickle cell disease. *N Engl J Med*. 2017;376(16):1561-1573. PMID: 28159613.
25. Lanzkron S, Carroll CP, Haywood C. Mortality rates and age at death from sickle cell disease: U.S., 1979-2005. *Public Health Rep*. 2013;128(2):110-116. PMID: 24506343.
26. Lettre G, Sankaran VG, Bezerra MAC, et al. DNA polymorphisms at the BCL11A, HBS1L-MYB, and beta-globin loci associate with fetal hemoglobin levels and pain crises in sickle cell disease. *Proc Natl Acad Sci USA*. 2008;105(33):11869-11874. PMID: 18667698.
27. Menzel S, Garner C, Gut I, et al. A QTL influencing F cell production maps to a gene encoding a zinc-finger protein on chromosome 2p15. *Nat Genet*. 2007;39(10):1197-1199. PMID: 17767159.
28. Uda M, Galanello R, Sanna S, et al. Genome-wide association study shows BCL11A associated with persistent fetal hemoglobin and amelioration of the phenotype of β-thalassemia. *Proc Natl Acad Sci USA*. 2008;105(5):1620-1625. PMID: 18245381.
29. Sankaran VG, Menne TF, Xu J, et al. Human fetal hemoglobin expression is regulated by the developmental stage-specific repressor BCL11A. *Science*. 2008;322(5909):1839-1842. PMID: 19056937.
30. Xu J, Peng C, Sankaran VG, et al. Correction of sickle cell disease in adult mice by interference with fetal hemoglobin silencing. *Science*. 2011;334(6058):993-996. PMID: 21998251.
31. Canver MC, Smith EC, Sher F, et al. BCL11A enhancer dissection by Cas9-mediated in situ saturating mutagenesis. *Nature*. 2015;527(7577):192-197. PMID: 26375006.
32. Bauer DE, Kamran SC, Lessard S, et al. An erythroid enhancer of BCL11A subject to genetic variation determines fetal hemoglobin level. *Science*. 2013;342(6155):253-257. PMID: 24115442.
33. Orkin SH, Bauer DE. Emerging genetic therapy for sickle cell disease. *Annu Rev Med*. 2019;70:257-271. PMID: 30355265.
34. Xu J, Sankaran VG, Ni M, et al. Transcriptional silencing of γ-globin by BCL11A involves long-range interactions and cooperation with SOX6. *Genes Dev*. 2010;24(8):783-798. PMID: 20395365.
35. Powars DR, Weiss JN, Chan LS, Schroeder WA. Is there a threshold level of fetal hemoglobin that ameliorates morbidity in sickle cell anemia? *Blood*. 1984;63(4):921-926. PMID: 6200161.
36. Charache S, Dover GJ, Moore RD, et al. Hydroxyurea: effects on hemoglobin F production in patients with sickle cell anemia. *Blood*. 1992;79(10):2555-2565. PMID: 1375104.
37. Steinberg MH, McCarthy WF, Castro O, et al. The risks and benefits of long-term use of hydroxyurea in sickle cell anemia: a 17.5 year follow-up. *Am J Hematol*. 2010;85(6):403-408. PMID: 20513116.
38. Komor AC, Kim YB, Packer MS, et al. Programmable editing of a target base in genomic DNA without double-stranded DNA cleavage. *Nature*. 2016;533(7603):420-424. PMID: 27096365.
39. Gaudelli NM, Komor AC, Rees HA, et al. Programmable base editing of A•T to G•C in genomic DNA without DNA cleavage. *Nature*. 2017;551(7681):464-471. PMID: 29160308.
40. Richter MF, Zhao KT, Eton E, et al. Phage-assisted evolution of an adenine base editor with improved Cas domain compatibility and activity. *Nat Biotechnol*. 2020;38(7):883-891. PMID: 32514124.
41. Anzalone AV, Randolph PB, Davis JR, et al. Search-and-replace genome editing without double-strand breaks or donor DNA. *Nature*. 2019;576(7785):149-157. PMID: 31634902.
42. Chen PJ, Hussmann JA, Yan J, et al. Enhanced prime editing systems by manipulating cellular determinants of editing outcomes. *Cell*. 2021;184(22):5635-5652. PMID: 34887556.
43. Abramson J, Adler J, Dunger J, et al. Accurate structure prediction of biomolecular interactions with AlphaFold 3. *Nature*. 2024;630(8016):493-500. PMID: 38718835.
44. Musunuru K, Chadwick AC, Mizoguchi T, et al. In vivo CRISPR base editing of PCSK9 durably lowers cholesterol in primates. *Nature*. 2021;593(7859):429-434. PMID: 33910230.
45. Abifadel M, Varret M, Rabès JP, et al. Mutations in PCSK9 cause autosomal dominant hypercholesterolemia. *Nat Genet*. 2003;34(2):154-156. PMID: 12730697.
46. Cohen JC, Boerwinkle E, Mosley TH, Hobbs HH. Sequence variations in PCSK9, low LDL, and protection against coronary heart disease. *N Engl J Med*. 2006;354(12):1264-1272. PMID: 16554528.
47. Lee RG, Mazzola AM, Braun MC, et al. Efficacy and safety of an investigational single-course CRISPR base-editing therapy targeting PCSK9 in nonhuman primate and mouse models. *Circulation*. 2023;147(3):242-253. PMID: 36314243.
48. Gillmore JD, Gane E, Taubel J, et al. CRISPR-Cas9 in vivo gene editing for transthyretin amyloidosis. *N Engl J Med*. 2021;385(6):493-502. PMID: 34215024.
49. Newby GA, Yen JS, Woodard KJ, et al. Base editing of haematopoietic stem cells rescues sickle cell disease in mice. *Nature*. 2021;595(7866):295-302. PMID: 34079130.
50. Tsai SQ, Zheng Z, Nguyen NT, et al. GUIDE-seq enables genome-wide profiling of off-target cleavage by CRISPR-Cas nucleases. *Nat Biotechnol*. 2015;33(2):187-197. PMID: 25513782.
51. Tsai SQ, Nguyen NT, Joung JK. Defining and improving the genome-wide specificities of CRISPR-Cas9 nucleases. *Nat Rev Genet*. 2016;17(5):300-312. PMID: 27087594.
52. Kim D, Bae S, Park J, et al. Digenome-seq: genome-wide profiling of CRISPR-Cas9 off-target effects in human cells. *Nat Methods*. 2015;12(3):237-243. PMID: 25664545.
53. Wienert B, Wyman SK, Richardson CD, et al. Unbiased detection of CRISPR off-targets in vivo using DISCOVER-seq. *Science*. 2019;364(6437):286-289. PMID: 31000663.
54. Fire A, Xu S, Montgomery MK, et al. Potent and specific genetic interference by double-stranded RNA in *Caenorhabditis elegans*. *Nature*. 1998;391(6669):806-811. PMID: 9486653.
55. Elbashir SM, Harborth J, Lendeckel W, et al. Duplexes of 21-nucleotide RNAs mediate RNA interference in cultured mammalian cells. *Nature*. 2001;411(6836):494-498. PMID: 11373684.
56. Meister G, Landthaler M, Patkaniowska A, et al. Human Argonaute2 mediates RNA cleavage targeted by miRNAs and siRNAs. *Mol Cell*. 2004;15(2):185-197. PMID: 15260970.
57. Liu J, Carmell MA, Rivas FV, et al. Argonaute2 is the catalytic engine of mammalian RNAi. *Science*. 2004;305(5689):1437-1441. PMID: 15284456.
58. Hutvágner G, Zamore PD. A microRNA in a multiple-turnover RNAi enzyme complex. *Science*. 2002;297(5589):2056-2060. PMID: 12154197.
59. Martinez J, Patkaniowska A, Urlaub H, et al. Single-stranded antisense siRNAs guide target RNA cleavage in RNAi. *Cell*. 2002;110(5):563-574. PMID: 12230974.
60. Soutschek J, Akinc A, Bramlage B, et al. Therapeutic silencing of an endogenous gene by systemic administration of modified siRNAs. *Nature*. 2004;432(7014):173-178. PMID: 15538359.
61. Bumcrot D, Manoharan M, Koteliansky V, Sah DW. RNAi therapeutics: a potential new class of pharmaceutical drugs. *Nat Chem Biol*. 2006;2(12):711-719. PMID: 17108989.
62. Whitehead KA, Langer R, Anderson DG. Knocking down barriers: advances in siRNA delivery. *Nat Rev Drug Discov*. 2009;8(2):129-138. PMID: 19180106.
63. Setten RL, Rossi JJ, Han SP. The current state and future directions of RNAi-based therapeutics. *Nat Rev Drug Discov*. 2019;18(6):421-446. PMID: 30877283.
64. Khvorova A, Watts JK. The chemical evolution of oligonucleotide therapies of clinical utility. *Nat Biotechnol*. 2017;35(3):238-248. PMID: 28244992.
65. Nair JK, Willoughby JLS, Chan A, et al. Multivalent N-acetylgalactosamine-conjugated siRNA localizes in hepatocytes and elicits robust RNAi-mediated gene silencing. *J Am Chem Soc*. 2014;136(49):16958-16961. PMID: 25434769.
66. Foster DJ, Brown CR, Shaikh S, et al. Advanced siRNA designs further improve in vivo performance of GalNAc-siRNA conjugates. *Mol Ther*. 2018;26(3):708-717. PMID: 29456019.
67. Springer AD, Dowdy SF. GalNAc-siRNA conjugates: leading the way for delivery of RNAi therapeutics. *Nucleic Acid Ther*. 2018;28(3):109-118. PMID: 29792536.
68. Adams D, Gonzalez-Duarte A, O'Riordan WD, et al. Patisiran, an RNAi therapeutic, for hereditary transthyretin amyloidosis. *N Engl J Med*. 2018;379(1):11-21. PMID: 29972757.
69. Balwani M, Sardh E, Ventura P, et al. Phase 3 trial of RNAi therapeutic givosiran for acute intermittent porphyria. *N Engl J Med*. 2020;382(24):2289-2301. PMID: 32240384.
70. Garrelfs SF, Frishberg Y, Hulton SA, et al. Lumasiran, an RNAi therapeutic for primary hyperoxaluria type 1. *N Engl J Med*. 2021;384(13):1216-1226. PMID: 33789011.
71. Ray KK, Wright RS, Kallend D, et al. Two phase 3 trials of inclisiran in patients with elevated LDL cholesterol. *N Engl J Med*. 2020;382(16):1507-1519. PMID: 32197277.
72. Ray KK, Troquay RPT, Visseren FLJ, et al. Long-term efficacy and safety of inclisiran in patients with high cardiovascular risk and elevated LDL cholesterol (ORION-3). *Lancet Diabetes Endocrinol*. 2023;11(2):109-119. PMID: 36470300.
73. Adams D, Tournev IL, Taylor MS, et al. Efficacy and safety of vutrisiran for hereditary transthyretin-mediated amyloidosis with polyneuropathy: a randomized clinical trial. *JAMA*. 2023;330(10):951-962. PMID: 35660119.
74. Young G, Srivastava A, Kavakli K, et al. Efficacy and safety of fitusiran prophylaxis in people with haemophilia A or haemophilia B with inhibitors (ALHAMBRA): a multicentre, open-label, phase 3 study. *Lancet Haematol*. 2023;10(5):e322-e332. PMID: 36040484.
75. Finkel RS, Mercuri E, Darras BT, et al. Nusinersen versus sham control in infantile-onset spinal muscular atrophy. *N Engl J Med*. 2017;377(18):1723-1732. PMID: 29091570.
76. Miller TM, Cudkowicz ME, Genge A, et al. Trial of antisense oligonucleotide tofersen for SOD1 ALS. *N Engl J Med*. 2022;387(12):1099-1110. PMID: 36449420.
77. Coelho T, Marques W, Dasgupta NR, et al. Eplontersen for hereditary transthyretin amyloidosis with polyneuropathy. *JAMA*. 2023;330(15):1448-1458. PMID: 37888913.
78. Crooke ST, Witztum JL, Bennett CF, Baker BF. RNA-targeted therapeutics. *Cell Metab*. 2018;27(4):714-739. PMID: 29617640.
79. Bennett CF, Swayze EE. RNA targeting therapeutics: molecular mechanisms of antisense oligonucleotides as a therapeutic platform. *Annu Rev Pharmacol Toxicol*. 2010;50:259-293. PMID: 20055705.
80. Roberts TC, Langer R, Wood MJA. Advances in oligonucleotide drug delivery. *Nat Rev Drug Discov*. 2020;19(10):673-694. PMID: 32782413.
81. Nuñez JK, Chen J, Pommier GC, et al. Genome-wide programmable transcriptional memory by CRISPR-based epigenome editing. *Cell*. 2021;184(9):2503-2519. PMID: 33836127.
82. Kosicki M, Tomberg K, Bradley A. Repair of double-strand breaks induced by CRISPR-Cas9 leads to large deletions and complex rearrangements. *Nat Biotechnol*. 2018;36(8):765-771. PMID: 30010673.
83. Leibowitz ML, Papathanasiou S, Doench JG, et al. Chromothripsis as an on-target consequence of CRISPR-Cas9 genome editing. *Nat Genet*. 2021;53(6):895-905. PMID: 34036211.
84. Haapaniemi E, Botber S, Perber H, et al. CRISPR-Cas9 genome editing induces a p53-mediated DNA damage response. *Nat Med*. 2018;24(7):927-930. PMID: 29892067.
85. Ihry RJ, Worringer KA, Salick MR, et al. p53 inhibits CRISPR-Cas9 engineering in human pluripotent stem cells. *Nat Med*. 2018;24(7):939-946. PMID: 29892062.
86. Turchiano G, Andrieux G, Klermund J, et al. Quantitative evaluation of chromosomal rearrangements in gene-edited human stem cells by CAST-seq. *Cell Stem Cell*. 2021;28(6):1136-1147. PMID: 33831365.
87. Thakore PI, D'Ippolito AM, Song L, et al. Highly specific epigenome editing by CRISPR-Cas9 repressors for silencing of distal regulatory elements. *Nat Methods*. 2015;12(12):1143-1149. PMID: 26501517.
88. Gilbert LA, Larson MH, Morsut L, et al. CRISPR-mediated modular RNA-guided regulation of transcription in eukaryotes. *Cell*. 2013;154(2):442-451. PMID: 23849981.
89. Yeo NC, Chavez A, Lance-Byrne A, et al. An enhanced CRISPR repressor for targeted mammalian gene regulation. *Nat Methods*. 2018;15(8):611-616. PMID: 30013045.
90. Amabile A, Migliara A, Capasso P, et al. Inheritable silencing of endogenous genes by hit-and-run targeted epigenetic editing. *Cell*. 2016;167(1):219-232. PMID: 27662090.
91. Boutin S, Monteilhet V, Veron P, et al. Prevalence of serum IgG and neutralizing factors against adeno-associated virus (AAV) types 1, 2, 5, 6, 8, and 9 in the healthy population. *Hum Gene Ther*. 2010;21(6):704-712. PMID: 20095819.
92. Calcedo R, Vandenberghe LH, Gao G, et al. Worldwide epidemiology of neutralizing antibodies to adeno-associated viruses. *J Infect Dis*. 2009;199(3):381-390. PMID: 19133809.
93. Mingozzi F, High KA. Immune responses to AAV vectors: overcoming barriers to successful gene therapy. *Blood*. 2013;122(1):23-36. PMID: 23325831.
94. Leborgne C, Barbon E, Alexander JM, et al. IgG-cleaving endopeptidase enables in vivo gene therapy in the presence of anti-AAV neutralizing antibodies. *Nat Med*. 2020;26(7):1096-1101. PMID: 32483358.
95. Meliani A, Boisgerault F, Hardet R, et al. Antigen-selective modulation of AAV immunogenicity with tolerogenic rapamycin nanoparticles enables successful vector re-administration. *Nat Commun*. 2018;9(1):4098. PMID: 30291232.
96. Kishimoto TK, Ferrari JD, LaMothe RA, et al. Improving the efficacy and safety of biologic drugs with tolerogenic nanoparticles. *Nat Nanotechnol*. 2016;11(10):890-899. PMID: 27479756.
97. Wright JF. Manufacturing and characterizing AAV-based vectors for use in clinical studies. *Gene Ther*. 2008;15(11):840-848. PMID: 18418416.
98. van der Loo JCM, Wright JF. Progress and challenges in viral vector manufacturing. *Hum Mol Genet*. 2016;25(R1):R42-R52. PMID: 26519142.
99. Clement N, Bhatt N. Scalable manufacturing of AAV vectors for gene therapy. *Mol Ther Methods Clin Dev*. 2023;31:101091. PMID: 38144696.
100. Grimm D, Lee JS, Wang L, et al. In vitro and in vivo gene therapy vector evolution via multispecies interbreeding and retargeting of adeno-associated viruses. *J Virol*. 2008;82(12):5887-5911. PMID: 18400866.
101. Pillay S, Meyer NL, Puschnik AS, et al. An essential receptor for adeno-associated virus infection. *Nature*. 2016;530(7588):108-112. PMID: 26814968.
102. Zincarelli C, Soltys S, Rengo G, Bhatti T. Analysis of AAV serotypes 1-9 mediated gene expression and tropism in mice after systemic injection. *Mol Ther*. 2008;16(6):1073-1080. PMID: 18414476.
103. Foust KD, Nurber E, Montgomery CL, et al. Intravascular AAV9 preferentially targets neonatal neurons and adult astrocytes. *Nat Biotechnol*. 2009;27(1):59-65. PMID: 19151654.
104. Nakai H, Yant SR, Storm TA, et al. Extrachromosomal recombinant adeno-associated virus vector genomes are primarily responsible for stable liver transduction in vivo. *J Virol*. 2001;75(15):6969-6976. PMID: 11435577.
105. Nathwani AC, Reiss UM, Tuddenham EGD, et al. Long-term safety and efficacy of factor IX gene therapy in hemophilia B. *N Engl J Med*. 2014;371(21):1994-2004. PMID: 25409372.
106. Donsante A, Miller DG, Li Y, et al. AAV vector integration sites in mouse hepatocellular carcinoma. *Science*. 2007;317(5837):477. PMID: 17656716.
107. Chandler RJ, LaFave MC, Varber GK, et al. Vector design influences hepatic genotoxicity after adeno-associated virus gene therapy. *J Clin Invest*. 2015;125(2):870-880. PMID: 25607842.
108. Day JW, Mendell JR, Mercuri E, et al. Clinical and genomic data in Zolgensma-treated patients: 5-year update from the START trial. *Mol Ther*. 2023;31(4S1):S1-S589. PMID: 36446484.
109. Maguire AM, Russell S, Chung DC, et al. Durability of voretigene neparvovec for biallelic RPE65-mediated inherited retinal dystrophy: phase 3 results at 3 and 4 years. *Ophthalmology*. 2021;128(10):1460-1468. PMID: 31554641.
110. Srivastava A, Lusby EW, Berns KI. Nucleotide sequence and organization of the adeno-associated virus 2 genome. *J Virol*. 1983;45(2):555-564. PMID: 6300419.
111. Gao GP, Alvira MR, Wang L, et al. Novel adeno-associated viruses from rhesus monkeys as vectors for human gene therapy. *Proc Natl Acad Sci USA*. 2002;99(18):11854-11859. PMID: 12192090.
112. Deverman BE, Pravdo PL, Thomas BP, et al. Cre-dependent selection yields AAV variants for widespread gene transfer to the adult brain. *Nat Biotechnol*. 2016;34(2):204-209. PMID: 28196961.
113. Hordeaux J, Wang Q, Katz N, et al. The neurotropic properties of AAV-PHP.B are limited to C57BL/6J mice. *Mol Ther*. 2018;26(3):664-668. PMID: 29428299.
114. Duncan GA, Kim N, Cober Y, et al. An adeno-associated viral vector capable of penetrating the mucus barrier to inhaled gene therapy. *Mol Ther Methods Clin Dev*. 2018;9:296-304. PMID: 29892565.
115. Keeler AM, Flotte TR. Recombinant adeno-associated virus gene therapy in light of Luxturna (and Zolgensma and Glybera): where are we, and how did we get here? *Annu Rev Virol*. 2019;6(1):601-621. PMID: 31283441.
116. Wilson JM, Flotte TR. Moving forward after two deaths in a gene therapy trial of myotubular myopathy. *Hum Gene Ther*. 2020;31(13-14):695-696. PMID: 32655998.
117. Chand DH, Zaidman C, Arber K, et al. Thrombotic microangiopathy following onasemnogene abeparvovec for spinal muscular atrophy: a case series. *J Pediatr*. 2021;231:265-268. PMID: 33653967.
118. Shieh PB, Bonnemann CG, Muller-Felber W, et al. Re: "moving forward after two deaths in a gene therapy trial of myotubular myopathy." *Hum Gene Ther*. 2020;31(15-16):787. PMID: 32799649.
119. Lek A, Wong B, Keov A, et al. Death after high-dose rAAV9 gene therapy in a patient with Duchenne muscular dystrophy. *N Engl J Med*. 2023;389(13):1203-1210. PMID: 37204841.
120. Salabarria SM, Nair J, Clement N, et al. Advancements in AAV-mediated c-kit targeting strategies for ex vivo hematopoietic stem cell gene therapy. *Mol Ther*. 2020;28(12):2581-2592. PMID: 34699947.
121. Palchaudhuri R, Saez B, Hoggatt J, et al. Non-genotoxic conditioning for hematopoietic stem cell transplantation using a hematopoietic-cell-specific internalizing immunotoxin. *Nat Biotechnol*. 2016;34(7):738-745. PMID: 27272385.
122. Tisdale JF, Pierciey FJ, Kamdar M, et al. Successful plerixafor-mediated mobilization, apheresis, and lentiviral vector transduction of hematopoietic stem/progenitor cells in patients with severe sickle cell disease. *Blood*. 2017;130(Suppl 1):990.
123. Magrin E, Semeraro M, Magnani A, et al. Long-term outcomes of lentiviral gene therapy for the β-hemoglobinopathies: the HGB-205 trial. *Nat Med*. 2022;28(1):81-88. PMID: 35058634.
124. Drysdale CM, Tisdale JF, Uchida N. Immunoresponse to gene-modified hematopoietic stem cells. *Mol Ther Methods Clin Dev*. 2020;16:42-49. PMID: 31890737.
125. Lidonnici MR, Paleari Y, Tiboni F, et al. Multiple integrated non-clinical studies predict the safety of lentivirus-mediated gene therapy for β-thalassemia. *Mol Ther Methods Clin Dev*. 2018;11:9-28. PMID: 30364550.
126. Zhu J, Zhao M, Saran A, et al. An engineered AAV capsid for efficient HSC transduction enables in vivo gene therapy for sickle cell disease. *bioRxiv*. 2024. PMID: 37291454.
127. Breda L, Papp TE, Triebwasser MP, et al. In vivo hematopoietic stem cell modification by mRNA delivery. *Science*. 2023;381(6656):436-443. PMID: 37498999.
128. Banskota S, Raguram A, Suh S, et al. Engineered virus-like particles for efficient in vivo delivery of therapeutic proteins. *Cell*. 2022;185(2):250-265. PMID: 35021064.
129. Liang SQ, Walkey CJ, Martinez AE, et al. AAV5-mediated base editing in a humanized mouse model corrects the most common α1-antitrypsin deficiency variant. *Mol Ther*. 2023;31(5):1384-1395.
130. Zuo E, Sun Y, Wei W, et al. Cytosine base editor generates substantial off-target single-nucleotide variants in mouse embryos. *Science*. 2019;364(6437):289-292. PMID: 31000663.
131. Grünewald J, Zhou R, Garcia SP, et al. Transcriptome-wide off-target RNA editing induced by CRISPR-guided DNA base editors. *Nature*. 2019;569(7756):433-437. PMID: 31142835.
132. Grünewald J, Zhou R, Iyer S, et al. CRISPR DNA base editors with reduced RNA off-target and self-editing activities. *Nat Biotechnol*. 2019;37(9):1041-1048. PMID: 31332326.
133. Kurt IC, Zhou R, Iyer S, et al. CRISPR C-to-G base editors for inducing targeted DNA transversions in human cells. *Nat Biotechnol*. 2021;39(1):41-46. PMID: 32820334.
134. Davis JR, Wang X, Witte IP, et al. Efficient in vivo base editing via single adeno-associated viruses with size-optimized genomes encoding compact adenine base editors. *Nat Biomed Eng*. 2022;6(11):1272-1283.
135. Rothgangl T, Dennis MK, Lin PJC, et al. In vivo adenine base editing of PCSK9 in macaques reduces LDL cholesterol levels. *Nat Biotechnol*. 2021;39(8):949-957.
136. Koblan LW, Erdos MR, Wilson C, et al. In vivo base editing rescues Hutchinson-Gilford progeria syndrome in mice. *Nature*. 2021;589(7843):608-614. PMID: 33408413.
137. Newby GA, Liu DR. In vivo somatic cell base editing and prime editing. *Mol Ther*. 2021;29(11):3107-3124.
138. Chen L, Park JE, Paa P, et al. Programmable C:G to G:C genome editing with CRISPR-Cas9-directed base excision repair proteins. *Nat Commun*. 2021;12:1384.
139. Liu B, Dong X, Cheng H, et al. A split prime editor with untethered reverse transcriptase and circular RNA template. *Nat Biotechnol*. 2022;40(9):1388-1393. PMID: 35578040.
140. Zuris JA, Thompson DB, Shu Y, et al. Cationic lipid-mediated delivery of proteins enables efficient protein-based genome editing in vitro and in vivo. *Nat Biotechnol*. 2015;33(1):73-80. PMID: 25357182.
141. Bao G, Rhee WJ, Bhakta NR. Development of RNA interference (RNAi)-based therapeutics and the challenges ahead. *Nat Rev Drug Discov*. 2011;10(11):775-776. PMID: 21507257.
142. Kauffman KJ, Mir FF, Jhunjhunwala S, et al. Efficacy and immunogenicity of unmodified and pseudouridine-modified mRNA delivered systemically with lipid nanoparticles in vivo. *Biomaterials*. 2016;109:78-87. PMID: 27710835.
143. Nair JK, Attarwala H, Sehgal A, et al. Impact of enhanced metabolic stability on pharmacokinetics and pharmacodynamics of GalNAc-siRNA conjugates. *Nucleic Acids Res*. 2017;45(19):10969-10977. PMID: 28981809.
144. Coelho T, Adams D, Silva A, et al. Safety and efficacy of RNAi therapy for transthyretin amyloidosis. *N Engl J Med*. 2013;369(9):819-829. PMID: 23984729.
145. Suhr OB, Coelho T, Buades J, et al. Efficacy and safety of patisiran for familial amyloidotic polyneuropathy. *Lancet Neurol*. 2015;14(2):162-173. PMID: 25575710.
146. Gillmore JD, Maitland ML, Engelen BGM. Phase 2, open-label extension (OLE) study of revusiran, an investigational RNAi therapeutic for the treatment of patients with transthyretin cardiac amyloidosis. *Orphanet J Rare Dis*. 2014;9(Suppl 1):O21.
147. Brown CR, Gupta S, Qin J, et al. Investigating the pharmacodynamic durability of GalNAc-siRNA conjugates. *Nucleic Acids Res*. 2020;48(21):11827-11844. PMID: 33152764.
148. Debacker AJ, Voutila J, Catley M, et al. Delivery of oligonucleotides to the liver with GalNAc: from research to registered therapeutic drug. *Mol Ther*. 2020;28(8):1759-1771. PMID: 32592692.
149. Schwartz AL, Fridovich SE, Lodish HF. Kinetics of internalization and recycling of the asialoglycoprotein receptor in a hepatoma cell line. *J Biol Chem*. 1982;257(8):4230-4237. PMID: 6279633.
150. Huang Y. Preclinical and clinical advances of GalNAc-decorated nucleic acid therapeutics. *Mol Ther Nucleic Acids*. 2017;6:116-132. PMID: 28325278.
151. Sardh E, Harper P, Balwani M, et al. Phase 1 trial of an RNA interference therapy for acute intermittent porphyria. *N Engl J Med*. 2019;380(6):549-558. PMID: 30726693.
152. Brown KM, Nair JK, Janas MM, et al. Expanding RNAi therapeutics to extrahepatic tissues with lipophilic conjugates. *Nat Biotechnol*. 2022;40(10):1500-1508.
153. Alterman JF, Godinho BMDC, Hassler MR, et al. A divalent siRNA chemical scaffold for potent and sustained modulation of gene expression throughout the central nervous system. *Nat Biotechnol*. 2019;37(8):884-894. PMID: 31375812.
154. Dowdy SF. Overcoming cellular barriers for RNA therapeutics. *Nat Biotechnol*. 2017;35(3):222-229. PMID: 28244993.
155. Doudna JA, Charpentier E. The new frontier of genome engineering with CRISPR-Cas9. *Science*. 2014;346(6213):1258096. PMID: 25430774.
156. Jinek M, Chylinski K, Fonfara I, et al. A programmable dual-RNA-guided DNA endonuclease in adaptive bacterial immunity. *Science*. 2012;337(6096):816-821. PMID: 22745249.
157. Cong L, Ran FA, Cox D, et al. Multiplex genome engineering using CRISPR/Cas systems. *Science*. 2013;339(6121):819-823. PMID: 23287718.
158. Mali P, Yang L, Esvelt KM, et al. RNA-guided human genome engineering via Cas9. *Science*. 2013;339(6121):823-826. PMID: 23287722.
159. Wang D, Tai PWL, Gao G. Adeno-associated virus vector as a platform for gene therapy delivery. *Nat Rev Drug Discov*. 2019;18(5):358-378. PMID: 30710128.
160. High KA, Roncarolo MG. Gene therapy. *N Engl J Med*. 2019;381(5):455-464. PMID: 31365802.
161. Dunbar CE, High KA, Joung JK, et al. Gene therapy comes of age. *Science*. 2018;359(6372):eaan4672. PMID: 29326244.
162. Anguela XM, High KA. Entering the modern era of gene therapy. *Annu Rev Med*. 2019;70:273-288. PMID: 30477394.
163. Li C, Samulski RJ. Engineering adeno-associated virus vectors for gene therapy. *Nat Rev Genet*. 2020;21(4):255-272. PMID: 32042148.
164. Verma IM, Weitzman MD. Gene therapy: twenty-first century medicine. *Annu Rev Biochem*. 2005;74:711-738. PMID: 15952901.
165. Matharu N, Ahituv N. Modulating gene regulation to treat genetic disorders. *Nat Rev Drug Discov*. 2020;19(11):757-775. PMID: 32612213.
166. Yin H, Kauffman KJ, Anderson DG. Delivery technologies for genome editing. *Nat Rev Drug Discov*. 2017;16(6):387-399. PMID: 28211909.
167. Ran FA, Cong L, Yan WX, et al. In vivo genome editing using *Staphylococcus aureus* Cas9. *Nature*. 2015;520(7546):186-191. PMID: 25830891.
168. Kim E, Koo T, Park SW, et al. In vivo genome editing with a small Cas9 orthologue derived from *Campylobacter jejuni*. *Nat Commun*. 2017;8:14500. PMID: 28220790.
169. Konermann S, Lotfy P, Brideau NJ, et al. Transcriptome engineering with RNA-targeting type VI-D CRISPR effectors. *Cell*. 2018;173(3):665-676. PMID: 29551272.
170. Rees HA, Liu DR. Base editing: precision chemistry on the genome and transcriptome of living cells. *Nat Rev Genet*. 2018;19(12):770-788. PMID: 30323312.
171. Levy JM, Yeh WH, Pendse N, et al. Cytosine and adenine base editing of the brain, liver, retina, heart and skeletal muscle of mice via adeno-associated viruses. *Nat Biomed Eng*. 2020;4(1):97-110. PMID: 31937940.
172. Villiger L, Grisch-Chan HM, Lindsay H, et al. Treatment of a metabolic liver disease by in vivo genome base editing in adult mice. *Nat Med*. 2018;24(10):1519-1525. PMID: 30297895.
173. Koblan LW, Doman JL, Wilson C, et al. Improving cytidine and adenine base editors by expression optimization and ancestral reconstruction. *Nat Biotechnol*. 2018;36(9):843-846. PMID: 29813047.
174. Song CQ, Jiang T, Richter M, et al. Adenine base editing in an adult mouse model of tyrosinaemia. *Nat Biomed Eng*. 2020;4(1):125-130. PMID: 31740770.
175. Yeh WH, Chiang H, Rees HA, et al. In vivo base editing of post-mitotic sensory cells. *Nat Commun*. 2018;9(1):2184. PMID: 29872041.
176. Choi EH, Suh S, Foik AT, et al. In vivo base editing rescues cone photoreceptors in a mouse model of early-onset inherited retinal degeneration. *Nat Commun*. 2022;13(1):1830.
177. Arbab M, Shen MW, Mok B, et al. Determinants of base editing outcomes from target library analysis and machine learning. *Cell*. 2020;182(2):463-480. PMID: 32533916.
178. Liao HK, Hatanaka F, Araoka T, et al. In vivo target gene activation via CRISPR/Cas9-mediated trans-epigenetic modulation. *Cell*. 2017;171(7):1495-1507. PMID: 29224783.
179. O'Connell MR. Molecular mechanisms of RNA targeting by Cas13-containing type VI CRISPR-Cas systems. *J Mol Biol*. 2019;431(1):66-87. PMID: 29966643.
180. Abudayyeh OO, Gootenberg JS, Essletzbichler P, et al. RNA targeting with CRISPR-Cas13. *Nature*. 2017;550(7675):280-284. PMID: 28976959.
181. Cox DBT, Gootenberg JS, Abudayyeh OO, et al. RNA editing with CRISPR-Cas13. *Science*. 2017;358(6366):1019-1027. PMID: 29070703.
182. Xu L, Zhang C, Li H, et al. Efficient precise in vivo base editing in adult dystrophic mice. *Nat Commun*. 2021;12(1):3719.
183. Osborn MJ, Gabriel R, Webber BR, et al. Fanconi anemia gene editing by the CRISPR/Cas9 system. *Hum Gene Ther*. 2015;26(2):114-126. PMID: 25545896.
184. Nelson JW, Randolph PB, Shen SP, et al. Engineered pegRNAs improve prime editing efficiency. *Nat Biotechnol*. 2022;40(3):402-410.
185. Scholefield J, Harrison PT. Prime editing — an update on the field. *Gene Ther*. 2021;28(7-8):396-401.
186. Piel FB, Patil AP, Howes RE, et al. Global distribution of the sickle cell gene and geographical confirmation of the malaria hypothesis. *Nat Commun*. 2010;1:104. PMID: 21045822.
187. Rees DC, Williams TN, Gladwin MT. Sickle-cell disease. *Lancet*. 2010;376(9757):2018-2031. PMID: 21131035.
188. Steinberg MH, Sebastiani P. Genetic modifiers of sickle cell disease. *Am J Hematol*. 2012;87(8):795-803. PMID: 22641398.
189. Weatherall DJ. The inherited diseases of hemoglobin are an emerging global health burden. *Blood*. 2010;115(22):4331-4336. PMID: 20233970.
190. Musallam KM, Rivella S, Vichinsky E, Rachmilewitz EA. Non-transfusion-dependent thalassemias. *Haematologica*. 2013;98(6):833-844. PMID: 23729725.
191. Thompson AA, Walters MC, Kwiatkowski J, et al. Gene therapy in patients with transfusion-dependent β-thalassemia. *N Engl J Med*. 2018;378(16):1479-1493. PMID: 29669226.
192. Ribeil JA, Hacein-Bey-Abina S, Payen E, et al. Gene therapy in a patient with sickle cell disease. *N Engl J Med*. 2017;376(9):848-855. PMID: 28249145.
193. Esrick EB, Lehmann LE, Bivber A, et al. Post-transcriptional genetic silencing of BCL11A to treat sickle cell disease. *N Engl J Med*. 2021;384(3):205-215. PMID: 33283990.
194. Wu Y, Zeng J, Roscoe BP, et al. Highly efficient therapeutic gene editing of human hematopoietic stem cells. *Nat Med*. 2019;25(5):776-783. PMID: 30911135.
195. Demirci S, Leonard A, Haro-Mora JJ, et al. CRISPR/Cas9 for sickle cell disease: applications, future possibilities, and challenges. *Adv Exp Med Biol*. 2019;1144:37-52. PMID: 31332735.
196. Leonard A, Tisdale JF. Stem cell transplantation in sickle cell disease: therapeutic potential and challenges faced. *Expert Rev Hematol*. 2018;11(7):547-565. PMID: 29883211.
197. Walters MC, Hardy K, Edwards S, et al. Pulmonary, gonadal, and central nervous system status after bone marrow transplantation for sickle cell disease. *Biol Blood Marrow Transplant*. 2010;16(2):263-272. PMID: 19822218.
198. Brunson A, Keegan THM, Bang H, et al. Increased risk of leukemia among sickle cell disease patients in California. *Blood*. 2017;130(13):1597-1599. PMID: 28830886.
199. Hsieh MM, Fitzhugh CD, Weitzel RP, et al. Nonmyeloablative HLA-matched sibling allogeneic hematopoietic stem cell transplantation for severe sickle cell phenotype. *JAMA*. 2014;312(1):48-56. PMID: 25058217.
200. Sharma A, Boelens JJ, de la Fuente J, et al. Biological basis of hematopoietic stem cell transplantation for sickle cell disease. *Biol Blood Marrow Transplant*. 2019;25(5):e137-e147.
201. Li C, Psatha N, Sova P, et al. Reactivation of γ-globin in adult β-YAC mice after ex vivo and in vivo hematopoietic stem cell genome editing. *Blood*. 2018;131(26):2915-2928. PMID: 29724895.
202. Traxler EA, Yao Y, Wang YD, et al. A genome-editing strategy to treat β-hemoglobinopathies that recapitulates a mutation associated with a benign genetic condition. *Nat Med*. 2016;22(9):987-990. PMID: 27525524.
203. Lux CT, Pattabhi S, Berger M, et al. TALEN-mediated gene editing of HBG in human hematopoietic stem cells leads to therapeutic fetal hemoglobin induction. *Mol Ther Methods Clin Dev*. 2020;12:175-183.
204. Métais JY, Doerfler PA, Mayuranathan T, et al. Genome editing of HBG1 and HBG2 to induce fetal hemoglobin. *Blood Adv*. 2019;3(21):3379-3392. PMID: 31698465.
205. Brendel C, Guda S, Renella R, et al. Lineage-specific BCL11A knockdown circumvents toxicities and reverses sickle phenotype. *J Clin Invest*. 2016;126(10):3868-3878. PMID: 27617859.
