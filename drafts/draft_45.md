# HSC Gene Therapy Review

---

## Abstract

Hematopoietic stem cell (HSC) gene therapy has achieved a historic inflection point: CRISPR-edited and lentiviral-transduced autologous stem cells can now cure sickle cell disease, β-thalassemia, and severe combined immunodeficiency. Yet fewer than 500 patients worldwide have received these therapies, despite millions who could benefit. The rate-limiting barrier is not the gene editing itself but the myeloablative conditioning—principally busulfan-based chemotherapy—required to create bone marrow niche vacancy for engraftment of corrected cells. This conditioning carries severe toxicities including sinusoidal obstruction syndrome, gonadal failure, and secondary malignancies, demands intensive inpatient care, and effectively restricts treatment to high-resource medical centers. Three converging strategies are poised to dissolve this barrier within the decade: (1) antibody-based conditioning using anti-CD117 antibodies and antibody-drug conjugates that selectively deplete host HSCs without genotoxic damage; (2) exploitation of the selective fitness advantage of gene-corrected cells, enabling engraftment under reduced-intensity or minimal conditioning; and (3) in vivo HSC editing via bone marrow-homing lipid nanoparticles and engineered virus-like particles that eliminate the need for cell harvest and conditioning entirely. We present novel mathematical frameworks formalizing engraftment kinetics, selective depletion pharmacodynamics, clonal competition dynamics, fitness thresholds for conditioning-free engraftment, in vivo editing efficiency, and long-term clone persistence. Together, these advances chart a path from the current paradigm of $2.2 million, months-long inpatient procedures toward a future of single-injection, outpatient-accessible genetic cures.

---

## 1. Introduction: The HSC Gene Therapy Revolution

Hematopoietic stem cells occupy a singular position in regenerative medicine: they are the only adult stem cell population that has been routinely transplanted for over five decades, they are accessible through peripheral blood mobilization or bone marrow aspiration, and they possess the capacity for lifelong self-renewal and multilineage differentiation (Orkin & Zon, 2008). These properties make HSCs the ideal substrate for genetic correction of inherited blood disorders—a vision first articulated in the 1970s and now realized through multiple regulatory-approved therapies (John & Czechowicz, 2025).

The clinical timeline of HSC gene therapy traces a path from cautious optimism through crisis to triumph. Early retroviral gene therapy for X-linked severe combined immunodeficiency (X-SCID) in 2000 demonstrated that gene-corrected HSCs could reconstitute a functional immune system, but insertional oncogenesis in several patients—caused by retroviral integration near proto-oncogenes including *LMO2*—revealed the dangers of first-generation γ-retroviral vectors (Hacein-Bey-Abina et al., 2003). The field pivoted to self-inactivating lentiviral vectors with internal physiological promoters, which dramatically reduced genotoxic risk (Montini et al., 2006). This second generation yielded the first regulatory approvals: Strimvelis for adenosine deaminase-deficient SCID (ADA-SCID) in Europe in 2016, Zynteglo (betibeglogene autotemcel) for transfusion-dependent β-thalassemia in 2019, and Skysona (elivaldogene autotemcel) for cerebral adrenoleukodystrophy in 2022 (John & Czechowicz, 2025).

The third generation—precision gene editing of HSCs—arrived with the landmark approval of Casgevy (exagamglogene autotemcel) in December 2023, the first CRISPR-Cas9-based therapy authorized by any regulatory agency (Frangoul et al., 2024; Locatelli et al., 2024). Casgevy uses ex vivo electroporation of Cas9 ribonucleoprotein to disrupt the erythroid-specific enhancer of *BCL11A* in autologous CD34⁺ HSPCs, derepressing fetal hemoglobin (HbF) and thereby ameliorating the pathophysiology of both sickle cell disease (SCD) and β-thalassemia. In the same month, Lyfgenia (lovotibeglogene autotemcel), a lentiviral gene addition therapy encoding an anti-sickling β-globin variant (βᴬ-T87Q), received FDA approval for SCD (Kanter et al., 2022).

Yet despite these triumphs, the global reach of HSC gene therapy remains profoundly limited. Of the approximately 515,000 infants born annually with SCD—nearly 80% in sub-Saharan Africa—fewer than 200 have received gene therapy (Dismantling Cost and Infrastructure Barriers, Lancet Haematol 2024; Piel et al., 2017). The bottleneck is not the genetic correction: editing efficiencies routinely exceed 80% for Cas9-based approaches and 90% for base editors in CD34⁺ cells ex vivo (Frangoul et al., 2024; Newby et al., 2021). Rather, the rate-limiting step is the myeloablative conditioning required before reinfusion of corrected cells, which demands weeks of inpatient care, carries significant morbidity and mortality, and restricts treatment to tertiary medical centers with transplant infrastructure (Fitzhugh et al., 2024).

This review argues that conditioning toxicity is the central barrier to scalable HSC gene therapy, and that three converging strategies—antibody-based non-genotoxic conditioning, selective fitness exploitation, and in vivo HSC editing—will collectively dissolve this barrier, transforming genetic cures from boutique interventions into globally accessible medicines.

---

## 2. Clinical Landscape of HSC Gene Therapy

### 2.1 Hemoglobinopathies

The hemoglobinopathies represent the most advanced clinical application of HSC gene therapy, driven by the enormous global disease burden (approximately 300,000 births with SCD annually) and the well-characterized molecular pathology.

**Casgevy (exagamglogene autotemcel)** disrupts the erythroid-specific enhancer of *BCL11A* in the +58 DNase I hypersensitive site using CRISPR-Cas9, reactivating γ-globin transcription and HbF production. In the pivotal CLIMB SCD-121 trial, 29 of 31 evaluable patients (93.5%) achieved freedom from vaso-occlusive crises for at least 12 consecutive months, with total hemoglobin levels normalizing to 11.0–14.0 g/dL (Frangoul et al., 2024). In the CLIMB THAL-111 trial for transfusion-dependent β-thalassemia, 32 of 35 patients (91.4%) achieved transfusion independence, with median weighted HbF of 11.9 g/dL (Locatelli et al., 2024). Off-target analysis revealed no evidence of clinically significant unintended edits (Cancellieri et al., 2023).

**Lyfgenia (lovotibeglogene autotemcel)** uses a lentiviral vector (BB305) to introduce the βᴬ-T87Q anti-sickling globin gene into autologous HSPCs. The HGB-206 trial demonstrated durable clinical benefit, with resolution of severe vaso-occlusive events in most patients (Kanter et al., 2022). However, the therapy carries a black box warning for hematologic malignancy: one patient developed acute myeloid leukemia 5.5 years post-infusion, though integration site analysis suggested the leukemia was unlikely to be directly vector-related (Goyal et al., 2022). The broader context of lentiviral safety was underscored by outcomes with Skysona (eli-cel) for cerebral adrenoleukodystrophy, where 7 of 67 treated patients developed hematologic malignancies (incidence rate 2.1 per 100 person-years), with lentiviral insertions at *MECOM/EVI1* identified in 5 of 6 evaluable cases—a finding attributable to the potent MNDU3 promoter used in that vector, which is distinct from the physiological β-globin promoter used in Lyfgenia (Tucci et al., 2024; Thompson et al., 2025).

**Reni-cel (renizgamglogene autogedtemcel)** represents the next generation: a CRISPR-Cas12a-based therapy (Editas Medicine) that disrupts *BCL11A* binding sites in both *HBG1* and *HBG2* promoters simultaneously. In the RUBY trial for SCD, 27 of 28 treated patients had no vaso-occlusive events post-infusion, with mean HbF increasing to 48.1% at 6 months (Sharma et al., 2025). In the EdiTHAL trial for β-thalassemia, all nine treated participants achieved transfusion independence (Corbacioglu et al., 2025). Cas12a offers advantages over Cas9 including smaller size, intrinsic crRNA processing enabling multiplex editing, and staggered-end cutting that may reduce large deletions.

**Base editing approaches** offer the promise of DSB-free correction. Beam Therapeutics' BEAM-101 uses an adenine base editor (ABE8e) to introduce A→G transitions in *HBG1/2* promoters, disrupting *BCL11A* binding. Early clinical data in four SCD patients showed HbF levels exceeding 60% at 1–6 months, with no vaso-occlusive crises and improved erythrocyte rheology (Antoniou et al., 2024).

### 2.2 Primary Immunodeficiencies

HSC gene therapy has transformed the treatment of severe combined immunodeficiencies, where the selective fitness advantage of gene-corrected lymphoid progenitors provides a powerful natural amplification of even modest transduction efficiencies.

**ADA-SCID**: Lentiviral gene therapy (OTL-101/elivaldogene tavalentivec) has been evaluated in 62 patients across US and UK sites, achieving 100% overall survival and 95% event-free survival, with all 59 successfully engrafted patients maintaining stable gene marking and 98% discontinuing immunoglobulin replacement (Kohn et al., 2025). Long-term follow-up of 43 patients receiving the earlier retroviral Strimvelis-era approach confirmed sustained efficacy at median 15.4 years, though one case of T-cell acute lymphoblastic leukemia was identified, linked to vector integration near *LMO2/CCND2* (Cicalese et al., 2024; Gentner et al., 2024).

**X-SCID**: Lentiviral gene therapy with low-dose busulfan conditioning in infants demonstrated multilineage engraftment, functional T and B cell reconstitution, and normalization of NK cell function in a pivotal St. Jude study (Mamcarz et al., 2019). Integration site analysis confirmed a safe profile without clonal dominance, consistent with the self-inactivating vector design (Ferrari et al., 2023).

**Wiskott-Aldrich syndrome (WAS)**: Long-term follow-up (median 7.6 years) of lentiviral gene therapy for WAS confirmed a safe profile with sustained reduction in autoimmune manifestations and bleeding events, demonstrating the durability of HSC gene correction for complex immunoregulatory disorders (Magnani et al., 2022).

### 2.3 Chronic Granulomatous Disease

Chronic granulomatous disease (CGD), caused by mutations in NADPH oxidase components, has emerged as a proving ground for advanced editing modalities. A landmark study reported the first clinical use of prime editing for p47phox-deficient CGD (PM359): two patients receiving prime-edited autologous CD34⁺ cells showed neutrophil NADPH oxidase activity within one month, maintained for 4–6 months of follow-up (Sharma et al., 2025b). Separately, high-fidelity PAMless base editing using SpRY-ABE8e has corrected *CYBB* mutations in X-linked CGD patient HSCs with high efficiency and specificity, demonstrating the versatility of DSB-free approaches (Sweeney et al., 2024). CRISPR-Cas9-mediated insertion of truncated *CYBA* and *CYBB* cDNA offers a near-universal strategy applicable across CGD genotypes (Sweeney et al., 2025).

### 2.4 Comparative Analysis of Editing Modalities

| Modality | Mechanism | Efficiency in CD34⁺ | DSBs? | Key Advantage | Key Limitation |
|---|---|---|---|---|---|
| Lentiviral | Gene addition via integration | 40–80% VCN 0.7–2.0 | No | Durable expression; long clinical track record | Insertional mutagenesis risk; size limits |
| CRISPR-Cas9 | DSB → NHEJ disruption | 80–95% indels | Yes | High efficiency; FDA-approved | Large deletions; chromothripsis risk |
| CRISPR-Cas12a | DSB → NHEJ disruption | 70–90% indels | Yes | Multiplex; smaller; staggered cuts | Newer; less clinical data |
| Base editing | A→G or C→T without DSB | 50–90% | No | No DSBs; precise single-nt changes | Bystander edits; PAM constraints |
| Prime editing | Reverse transcriptase write | 20–60% | No | Versatile; any small edit | Lower efficiency; larger payload |

All modalities share a common prerequisite: myeloablative conditioning to create niche vacancy for engraftment of corrected cells. It is this shared dependency that constitutes the field's central bottleneck.

---

## 3. The Conditioning Barrier

### 3.1 The Biology of Niche Vacancy

HSCs reside in specialized bone marrow microenvironments—niches—comprising perivascular sinusoidal endothelial cells, mesenchymal stromal cells (including CXCL12-abundant reticular cells and leptin receptor-positive cells), and endosteal osteoblastic cells (Morrison & Scadden, 2014). These niches provide essential maintenance signals including SCF (the ligand for CD117/c-Kit), CXCL12, and thrombopoietin. Critically, niche occupancy appears to be limited: transplanted HSCs cannot efficiently engraft unless endogenous HSCs are first depleted to vacate niche space (Bhatt et al., 2013).

The concept of niche vacancy as a prerequisite for engraftment was established by classic experiments in W/Wᵛ mice, which carry hypomorphic *Kit* mutations that reduce endogenous HSC fitness. These mice accept donor HSCs without conditioning because their endogenous HSCs are constitutively disadvantaged in niche competition (Bhatt et al., 2013). In wild-type recipients, conditioning chemotherapy or irradiation creates vacancy by killing endogenous HSCs, permitting donor cell lodgment and long-term engraftment.

Recent work has challenged the strict niche-limitation model. A 2025 study demonstrated that addition of ectopic niches (via transplanted femurs) did not increase total HSC numbers, and transplanted HSC numbers did not exceed physiological levels—suggesting that HSC numbers are constrained at both systemic and local levels rather than purely by niche availability (Haas et al., 2025). This has important implications: even partial niche vacancy may be sufficient if transplanted cells carry a fitness advantage, since the system may tolerate temporary overcrowding followed by competitive resolution.

### 3.2 Myeloablative Regimens and Their Toxicities

The standard conditioning regimen for autologous HSC gene therapy is pharmacokinetically targeted busulfan, a bifunctional alkylating agent that forms interstrand DNA crosslinks, preferentially killing dividing cells including HSCs (Ciurea & Andersson, 2009). Typical gene therapy protocols employ four daily doses of IV busulfan (target cumulative AUC 80–100 mg·h/L), achieving >95% HSC depletion but at significant cost to the patient (John & Czechowicz, 2025).

**Sinusoidal obstruction syndrome (SOS)/veno-occlusive disease (VOD)** affects 5–60% of patients depending on regimen and population, resulting from direct endothelial damage in hepatic sinusoids. Severe SOS carries mortality rates of 20–50% without defibrotide treatment (Richardson et al., 2017).

**Gonadotoxicity** is among the most devastating long-term consequences. Busulfan causes premature ovarian insufficiency in >80% of female patients and severe oligospermia/azoospermia in males, effectively rendering most patients infertile—a particularly cruel outcome for young patients with SCD or β-thalassemia who may be cured of their blood disorder but lose reproductive capacity (Dalle et al., 2023; Niinimäki et al., 2024).

**Secondary malignancies** occur at a rate of approximately 4.8% in adults receiving busulfan-based conditioning, reflecting the inherent genotoxicity of DNA-alkylating agents (Shimoni et al., 2023).

**Prolonged cytopenias** require 2–4 weeks of neutropenia and transfusion dependence, necessitating inpatient care with laminar airflow isolation, broad-spectrum antimicrobials, and platelet/RBC transfusion support. Treatment-related mortality ranges from 1–5% even in experienced centers (Fitzhugh et al., 2024).

Treosulfan has emerged as a less toxic alternative, with a randomized phase 2 trial in pediatric non-malignant disease demonstrating comparable engraftment with reduced gonadal toxicity (10% vs. 38%) and overall long-term complications (20% vs. 34%) compared to busulfan (Bornhäuser et al., 2024; Zecca et al., 2024; Christopherson et al., 2024). However, treosulfan remains a DNA-alkylating agent with inherent genotoxic risk, representing an incremental rather than transformative improvement.

### 3.3 The Access Problem

The conditioning requirement imposes infrastructure demands that effectively exclude the majority of patients who could benefit. A complete gene therapy course—mobilization, apheresis, ex vivo manufacturing, busulfan conditioning, cell reinfusion, and supportive care—costs approximately $2.2 million for Casgevy in the US and requires 4–8 weeks of inpatient hospitalization at a transplant-capable center (Fitzhugh et al., 2024). Globally, there are fewer than 1,500 centers capable of performing autologous HSCT, concentrated overwhelmingly in high-income countries. Sub-Saharan Africa, home to approximately 80% of SCD births, has virtually no gene therapy infrastructure (Fitzhugh et al., 2024; Piel et al., 2017).

This creates a stark paradox: the diseases most amenable to HSC gene therapy—SCD, β-thalassemia, and the primary immunodeficiencies—disproportionately affect populations in low- and middle-income countries where the required infrastructure is absent. Dismantling the conditioning barrier is therefore not merely a scientific challenge but an imperative of global health equity.

### 3.4 Framework F322: HSC Engraftment Kinetics

We formalize the relationship between conditioning intensity and donor HSC engraftment with a system of ordinary differential equations describing the competition between endogenous and donor HSCs for a finite niche compartment.

```math
\frac{dH_e}{dt} = r_e \cdot H_e \left(1 - \frac{H_e + H_d}{K}\right) - \delta_e \cdot H_e - \mu(C) \cdot H_e
```

```math
\frac{dH_d}{dt} = r_d \cdot H_d \left(1 - \frac{H_e + H_d}{K}\right) - \delta_d \cdot H_d
```

where:
- $H_e(t)$ = endogenous HSC number at time $t$
- $H_d(t)$ = donor (gene-corrected) HSC number at time $t$
- $K$ = niche carrying capacity (total number of HSC-sustaining niche units, estimated at $\sim 1.1 \times 10^4$ in human bone marrow)
- $r_e, r_d$ = self-renewal rates for endogenous and donor HSCs respectively
- $\delta_e, \delta_d$ = differentiation/loss rates
- $\mu(C)$ = conditioning-induced HSC killing rate, modeled as a saturating function of conditioning intensity $C$:

```math
\mu(C) = \mu_{\max} \cdot \frac{C^n}{C^n + C_{50}^n}
```

where $\mu_{\max}$ is the maximal killing rate, $C_{50}$ is the conditioning intensity yielding half-maximal killing, and $n$ is the Hill coefficient capturing dose-response steepness.

The niche vacancy fraction at infusion time $t_{\text{inf}}$ is:

```math
V(t_{\text{inf}}) = 1 - \frac{H_e(t_{\text{inf}})}{K}
```

**Critical insight**: donor chimerism $\chi = H_d/(H_e + H_d)$ at steady state depends on both the initial vacancy $V(t_{\text{inf}})$ and the relative fitness $\phi = r_d/r_e$. When $\phi > 1$ (corrected cells have a fitness advantage), the required vacancy—and therefore conditioning intensity—decreases dramatically. In the limiting case where $\phi \gg 1$, engraftment becomes possible at arbitrarily low conditioning levels, forming the theoretical basis for reduced-intensity and conditioning-free approaches.

---

## 4. Antibody-Based Conditioning

### 4.1 Anti-CD117 (c-Kit) Monoclonal Antibodies

CD117 (c-Kit) is the receptor for stem cell factor (SCF) and is expressed at high levels on HSCs and hematopoietic progenitor cells, with lower expression on mature lineages. Blocking SCF-CD117 signaling disrupts HSC niche retention and survival without causing DNA damage.

**Briquilimab (JSP191)**, developed by Jasper Therapeutics, is an aglycosylated humanized anti-CD117 monoclonal antibody that blocks SCF binding. In a pivotal phase 1b trial in three patients with Fanconi anemia (FA)—a population exquisitely sensitive to genotoxic conditioning—briquilimab-based conditioning (combined with rATG, fludarabine, cyclophosphamide, and rituximab but without irradiation or busulfan) achieved high levels of donor engraftment with all three patients completing 104 weeks of follow-up without significant toxicity (Bhatia et al., 2025). This result is particularly significant because FA patients cannot tolerate standard myeloablative conditioning due to their underlying DNA repair deficiency, and prior transplant approaches for FA carried substantial mortality. Pharmacokinetic analysis revealed predictable dose-exposure relationships across SCID, MDS, and AML populations (Yang et al., 2024).

Briquilimab's mechanism is non-genotoxic: it does not cause DNA damage, crosslinks, or strand breaks. Consequently, it preserves fertility—a transformative advantage over busulfan. In a rhesus macaque model of gene therapy, single-dose CD117-antibody-drug conjugate (CD117-ADC) achieved >99% depletion of bone marrow CD34⁺CD90⁺CD45RA⁻ cells (comparable to myeloablative busulfan), enabled efficient engraftment and vector-derived fetal hemoglobin induction, and preserved fertility in treated animals (Soni et al., 2023).

### 4.2 Anti-CD45 Antibody-Drug Conjugates

An alternative approach targets CD45, a pan-hematopoietic phosphatase expressed on all nucleated blood cells including HSCs. Anti-CD45 antibodies conjugated to cytotoxic payloads can deplete the entire hematopoietic compartment, creating deep niche vacancy.

**CD45-saporin (CD45-SAP)**, an immunotoxin coupling anti-CD45 antibody to the ribosome-inactivating protein saporin, enabled >90% donor cell engraftment in immunocompetent mice with a single dose (Palchaudhuri et al., 2016). **Anti-CD45 PBD-based ADCs** (antibody-drug conjugates using pyrrolobenzodiazepine dimer payloads) offer enhanced potency and clinical translatability. Two clones (YTH24.5 and YTH54.12) conjugated to cleavable (SG3249) and non-cleavable (SG3376) PBD linkers demonstrated potent and specific killing of human CD45⁺ cells in vitro and in xenograft models (Saha et al., 2024).

### 4.3 Combination Strategies

The most promising recent development is the combination of HSC mobilization with antibody-based depletion. A 2025 study demonstrated that mobilization with plerixafor followed by combined anti-c-Kit and anti-CD47 antibody treatment dramatically enhanced HSC depletion and subsequent donor engraftment compared to either approach alone (Czechowicz et al., 2025). Anti-CD47 blocks the "don't eat me" signal (CD47-SIRPα interaction) on HSCs, enhancing macrophage-mediated phagocytic clearance of antibody-targeted cells. Separately, anti-CD117 combined with anti-CD47 and JAK inhibition enabled toxic-payload-free allogeneic transplantation in preclinical models (George et al., 2024). Targeted HSC depletion through SCF blockade—disrupting the ligand rather than the receptor—offers yet another non-genotoxic strategy (Hernandez et al., 2024).

### 4.4 Framework F323: Selective Depletion Pharmacokinetics/Pharmacodynamics

We model antibody-based HSC depletion using a linked PK/PD framework that captures the therapeutic window between HSC elimination and mature lineage preservation.

**Pharmacokinetics (two-compartment model):**

```math
\frac{dA_c}{dt} = -k_{\text{el}} \cdot A_c - k_{12} \cdot A_c + k_{21} \cdot A_p + \frac{\text{Dose}}{V_c} \cdot \delta(t)
```

```math
\frac{dA_p}{dt} = k_{12} \cdot A_c \cdot \frac{V_c}{V_p} - k_{21} \cdot A_p
```

where $A_c$ and $A_p$ are antibody concentrations in central (blood) and peripheral (tissue) compartments, $k_{\text{el}}$ is elimination rate, and $k_{12}$, $k_{21}$ are intercompartmental transfer rates.

**Pharmacodynamics (target-mediated killing):**

```math
\frac{dN_{\text{HSC}}}{dt} = r \cdot N_{\text{HSC}} \left(1 - \frac{N_{\text{HSC}}}{K}\right) - E_{\max} \cdot \frac{A_c^{\gamma}}{EC_{50}^{\gamma} + A_c^{\gamma}} \cdot N_{\text{HSC}}
```

where $N_{\text{HSC}}$ is the HSC population, $E_{\max}$ is the maximum killing rate, $EC_{50}$ is the antibody concentration for half-maximal killing, and $\gamma$ is the Hill coefficient reflecting cooperative receptor occupancy.

**Therapeutic index**: The ratio of $EC_{50}$ values for HSC depletion versus mature lineage toxicity defines the therapeutic window:

```math
TI = \frac{EC_{50}^{\text{mature}}}{EC_{50}^{\text{HSC}}}
```

For anti-CD117, the therapeutic index is favorable (estimated $TI > 10$) because CD117 is expressed at ~10-fold higher density on HSCs than on most mature lineages. For anti-CD45 ADCs, $TI$ is narrower ($TI \approx 2-5$) because CD45 is broadly expressed, necessitating more careful dose optimization and potentially limiting the approach to settings where broad hematopoietic depletion is acceptable.

---

## 5. Selective Fitness Advantage

### 5.1 The Natural Advantage of Corrected Cells

A fundamental but underappreciated principle of HSC gene therapy is that in many target diseases, the gene-corrected cells possess an intrinsic survival and proliferative advantage over their diseased counterparts. This is most evident in the immunodeficiencies: in X-SCID and ADA-SCID, gene-corrected lymphoid progenitors undergo positive selection in the thymus and peripheral lymphoid organs, amplifying even modest transduction efficiencies into near-complete immune reconstitution (Mamcarz et al., 2019). This is why SCID gene therapy has historically required less intensive conditioning—the fitness differential provides a biological amplifier.

In hemoglobinopathies, the fitness advantage operates at the erythroid level. In SCD, erythrocytes expressing corrected hemoglobin (HbA or HbF) are protected from sickling-induced hemolysis, giving them a survival advantage of approximately 2–3-fold over HbS-containing cells in the peripheral circulation. At the HSC level, the advantage is subtler but measurable: SCD bone marrow exhibits chronic stress erythropoiesis, and correction of the underlying hemoglobin defect reduces this stress, potentially favoring quiescent corrected HSCs over chronically activated diseased HSCs (Fitzhugh et al., 2024).

### 5.2 Clinical Evidence for Competitive Selection

Whole-genome sequencing of HSCs from six patients who received lentiviral gene therapy for SCD revealed a critical finding: gene therapy did not increase the overall mutational burden of HSCs, but pre-existing clones harboring CHIP-associated driver mutations (*DNMT3A*, *EZH2*) showed marked expansion post-conditioning (Kohn et al., 2023). This suggests that myeloablative conditioning creates a selective bottleneck that favors pre-existing fit clones—both gene-corrected and CHIP-mutated. The clinical implication is twofold: (1) reduced-intensity conditioning may decrease the selective pressure that amplifies CHIP clones, and (2) the fitness advantage of gene-corrected cells may be sufficient to drive engraftment even without full myeloablation.

Longitudinal analysis of clonal hematopoiesis dynamics has revealed that CHIP driver mutations confer fitness advantages of 5–15% per year (estimated by variant allele frequency trajectories), with *DNMT3A* R882H mutations showing particularly strong competitive advantage, potentially attenuated by metformin (Watson et al., 2023; Singh et al., 2025). These quantitative fitness measurements provide critical parameters for modeling the competition between corrected, diseased, and CHIP clones.

### 5.3 Framework F324: Moran Process for HSC Clonal Competition

We model the competition between gene-corrected and uncorrected HSCs as a Moran process on a finite population of $N$ HSC niche units, which captures the stochastic dynamics of clonal replacement in a resource-limited compartment.

At each time step, one HSC is selected for replication (with probability proportional to fitness) and one is selected for removal (uniformly at random). Let corrected cells have fitness $1 + s$ relative to uncorrected fitness $1$.

**Fixation probability** (Moran, 1962): Starting from $i$ corrected cells in a population of $N$:

```math
\pi_i = \frac{1 - \left(\frac{1}{1+s}\right)^i}{1 - \left(\frac{1}{1+s}\right)^N}
```

For a single corrected cell ($i = 1$):

```math
\pi_1 = \frac{1 - \frac{1}{1+s}}{1 - \left(\frac{1}{1+s}\right)^N} = \frac{s/(1+s)}{1 - (1+s)^{-N}}
```

**Mean time to fixation** from $i = 1$:

```math
\bar{\tau} \approx \frac{N}{s} \left[\ln(N) + \gamma_E\right]
```

where $\gamma_E \approx 0.577$ is the Euler-Mascheroni constant.

**Key insight**: Conditioning reduces the effective population size $N$ by depleting endogenous HSCs. If conditioning depletes a fraction $f$ of niche units, the effective population becomes $N(1-f)$, and:
- Fixation probability increases: $\pi_1(f) > \pi_1(0)$ for $f > 0$
- Time to fixation decreases: $\bar{\tau}(f) < \bar{\tau}(0)$

This provides a quantitative framework for optimizing reduced-intensity conditioning: rather than maximizing niche vacancy (full myeloablation), the goal is to reduce $N$ sufficiently that the fitness-driven fixation probability exceeds a clinically relevant threshold (e.g., $\pi > 0.5$ for achieving majority corrected chimerism).

### 5.4 Framework F325: Critical Fitness Threshold for Conditioning-Free Engraftment

For conditioning-free engraftment, infused corrected cells must compete for niche space against a full complement of endogenous HSCs. We derive the minimum fitness advantage $s^*$ required for corrected cells to achieve clinically meaningful chimerism without conditioning.

Starting from $i_0$ infused corrected cells in a niche of size $N$, the expected chimerism at equilibrium (assuming the Moran process reaches quasi-steady state before significant HSC turnover) is approximately:

```math
\langle \chi \rangle \approx \frac{i_0 (1+s)}{i_0 (1+s) + (N - i_0)}
```

For therapeutic efficacy, suppose we require $\langle \chi \rangle > \chi_{\min}$ (e.g., $\chi_{\min} = 0.2$ for SCD, where 20% HbF-producing cells is clinically meaningful). Solving:

```math
s^* > \frac{\chi_{\min} (N - i_0)}{i_0 (1 - \chi_{\min})} - 1
```

For realistic parameters ($N = 10^4$, $i_0 = 10^2$ infused cells that successfully lodge in niches, $\chi_{\min} = 0.2$):

```math
s^* > \frac{0.2 \times 9{,}900}{100 \times 0.8} - 1 = \frac{1{,}980}{80} - 1 = 23.75
```

This unrealistically high fitness advantage (2,375%) confirms that conditioning-free engraftment via conventional HSC transplantation is not feasible through fitness advantage alone—the initial seeding fraction is too small. This motivates in vivo editing, which modifies endogenous HSCs in place and does not require niche competition.

However, if conditioning reduces $N$ to $N' = 1{,}000$ while infusing $i_0 = 500$ cells:

```math
s^* > \frac{0.2 \times 500}{500 \times 0.8} - 1 = \frac{100}{400} - 1 = -0.75
```

Here, $s^* < 0$—even cells with no fitness advantage will achieve the target chimerism simply due to the favorable initial ratio. This illustrates the power of even partial conditioning combined with fitness advantage.

---

## 6. In Vivo HSC Editing: Eliminating Conditioning Entirely

### 6.1 The Vision

The ultimate solution to the conditioning barrier is to eliminate the ex vivo pipeline entirely: rather than harvesting, editing, conditioning, and transplanting, directly edit endogenous HSCs in their native bone marrow niche. This approach requires no conditioning because it modifies cells already occupying niche space—there is no competition for engraftment. It requires no apheresis, no GMP manufacturing, no inpatient stay. In principle, it reduces the entire gene therapy procedure to a single intravenous injection.

### 6.2 Bone Marrow-Homing Lipid Nanoparticles

**CD117-targeted LNPs**: Building on the same receptor used for antibody-based conditioning, researchers have developed lipid nanoparticles conjugated to anti-CD117 antibodies or peptides that home to HSCs after systemic administration. CD117/LNP-mRNA encapsulating Cas9 or base editor mRNA achieved near-complete correction of hematopoietic sickle cells in vivo in a humanized mouse model, and delivery of pro-apoptotic PUMA mRNA with CD117/LNP disrupted HSC function sufficiently to permit nongenotoxic conditioning for subsequent HSCT (Li et al., 2023).

**Bone marrow-homing LNPs**: Siegwart and colleagues developed LNPs with intrinsic bone marrow tropism (without antibody conjugation) that delivered mRNA to at least 14 unique cell types in the bone marrow, including healthy and diseased HSCs, leukemic stem cells, B cells, T cells, and macrophages. In a humanized SCD mouse model, these LNPs achieved CRISPR/Cas9 and base editing for fetal hemoglobin reactivation and sickle allele correction (Lian et al., 2024).

**Antibody-free targeted LNPs (2025)**: The most recent advance describes LNPs optimized for HSC delivery without antibody conjugation, enabling efficient in vivo base editing of the *HBG1/2* promoter target in human HSCs. Delivery of ABE8e/sgRNA mRNA achieved efficient editing in transfusion-dependent β-thalassemia patient-derived HSCs engrafted in immunodeficient mice (Yin et al., 2025).

### 6.3 In Vivo Gene Delivery via Engineered Virus-Like Particles

Virus-like particles (VLPs)—non-replicating capsids that transiently deliver editing machinery without integrating genetic material—offer an alternative to LNPs with potentially superior cell-type specificity.

**BaEVTR-enveloped VLPs**: Engineered VLPs displaying an optimized baboon endogenous retrovirus transmembrane (BaEVTR) envelope achieved 31% editing of β₂-microglobulin in long-term human HSPCs at 8 weeks post-dosing in vivo, and edited hemoglobinopathy-relevant loci *BCL11A* (26%) and *HBG1/2* (7.5%) at 5 days. A CD133-targeted envelope variant achieved higher specificity for HSPCs compared to the broad-tropism BaEVTR design (Mosti et al., 2025).

**Postnatal trafficking approach**: A 2025 Nature study exploited the physiological trafficking of HSPCs from liver to bone marrow in neonates. Systemic lentiviral administration in newborn mice—using a phagocytosis-shielded LV—successfully transduced bona fide long-term HSPCs, as confirmed by serial transplantation and clonal tracking (Milani et al., 2025). While this approach is limited to the neonatal window, it demonstrates that in vivo HSC gene therapy is achievable without any conditioning if delivery is timed to exploit endogenous HSC biology.

### 6.4 HSC Mobilization Combined with In Vivo Editing

A particularly promising strategy combines pharmacological HSC mobilization with systemic delivery of editing agents. G-CSF and/or plerixafor administration mobilizes HSCs from bone marrow into peripheral blood, where they become physically accessible to systemically administered LNPs or VLPs. Mobilization increased in vivo gene transfer to HSCs approximately 5-fold in murine models (mean 8.5% GFP⁺CD45⁺ cells), dramatically expanding the therapeutic window (Li et al., 2023). A simplified G-CSF-free procedure using plerixafor alone was sufficient for in vivo HSC gene therapy in a sickle cell mouse model, reducing the complexity of the approach further (Uchida et al., 2024).

### 6.5 Framework F326: In Vivo HSC Editing Efficiency Model

We model the fraction of endogenous long-term HSCs (LT-HSCs) successfully edited by a systemically administered LNP or VLP delivery system.

For a single dose, the probability of editing an individual LT-HSC depends on three sequential processes:

```math
p_{\text{edit}}^{\text{single}} = p_{\text{target}} \cdot p_{\text{uptake}} \cdot p_{\text{nuclear}}
```

where:
- $p_{\text{target}}$ = probability that at least one LNP/VLP reaches the HSC niche microenvironment (determined by biodistribution)
- $p_{\text{uptake}}$ = probability of receptor-mediated endocytosis given nanoparticle contact (determined by receptor density and binding affinity)
- $p_{\text{nuclear}}$ = probability of successful editing given cytoplasmic delivery (determined by cargo integrity, nuclear import for Cas proteins, and guide RNA activity)

For $n$ independent LNP encounters per dose (following a Poisson process with rate $\lambda$ proportional to dose):

```math
P(\text{HSC edited}) = 1 - e^{-\lambda \cdot p_{\text{uptake}} \cdot p_{\text{nuclear}}}
```

At the population level, the fraction of LT-HSCs edited after a single dose $D$:

```math
F(D) = 1 - \exp\left(-\frac{D}{D_0}\right)
```

where $D_0 = 1/(\lambda_0 \cdot p_{\text{uptake}} \cdot p_{\text{nuclear}})$ is the characteristic dose for 63% editing. For $m$ repeated doses (assuming independent dosing events):

```math
F_m = 1 - \left(1 - F_1\right)^m = 1 - \exp\left(-\frac{m \cdot D}{D_0}\right)
```

**Mobilization enhancement**: If mobilization increases the effective encounter rate by a factor $\alpha$ (empirically $\alpha \approx 5$ from murine data), the effective dose becomes $\alpha \cdot D$, dramatically reducing the dose required for clinically meaningful editing:

```math
F_{\text{mob}}(D) = 1 - \exp\left(-\frac{\alpha \cdot D}{D_0}\right)
```

**Practical implications**: Current bone marrow-homing LNPs achieve approximately 5–15% editing of HSPCs in vivo (Lian et al., 2024; Yin et al., 2025). With mobilization enhancement ($\alpha = 5$) and optimized targeting, the model predicts that 50% LT-HSC editing—sufficient for therapeutic benefit in SCD—could be achieved with 2–3 repeated doses.

### 6.6 Framework F327: Long-Term Clonal Dynamics of Edited HSCs

A critical question for in vivo HSC editing is whether edited clones persist long-term. We model this using a continuous-time branching process where each edited LT-HSC stochastically divides, differentiates, or dies.

Let each LT-HSC in the bone marrow undergo the following transitions per unit time:
- Symmetric self-renewal (HSC → 2 HSCs) with rate $\alpha$
- Asymmetric division/differentiation (HSC → HSC + progenitor) with rate $\beta$  
- Symmetric commitment (HSC → 2 progenitors) with rate $\gamma$
- Death/exhaustion with rate $\delta$

The net growth rate of an edited HSC clone is:

```math
\lambda_{\text{net}} = \alpha - \gamma - \delta
```

**Clone extinction probability**: For a single edited HSC initiating a clone, the extinction probability $q$ satisfies:

```math
q = \frac{\delta}{\alpha + \beta + \gamma + \delta} + \frac{\beta}{\alpha + \beta + \gamma + \delta} \cdot q + \frac{\gamma}{\alpha + \beta + \gamma + \delta} + \frac{\alpha}{\alpha + \beta + \gamma + \delta} \cdot q^2
```

Simplifying (since asymmetric division preserves the clone):

```math
q = \frac{\delta + \gamma + \alpha q^2}{\alpha + \gamma + \delta}
```

This yields:

```math
\alpha q^2 - (\alpha + \gamma + \delta) q + (\gamma + \delta) = 0
```

```math
q = \begin{cases} 1 & \text{if } \alpha \leq \gamma + \delta \text{ (subcritical)} \\ \frac{\gamma + \delta}{\alpha} & \text{if } \alpha > \gamma + \delta \text{ (supercritical)} \end{cases}
```

**Expected clone size** at time $t$ for a surviving clone:

```math
\mathbb{E}[Z(t) \mid Z(t) > 0] = \frac{e^{\lambda_{\text{net}} t}}{1 - q}
```

**Clonal diversity dynamics**: If $n_0$ HSCs are independently edited, the expected number of surviving clones at time $t$ is:

```math
\mathbb{E}[n_{\text{surv}}(t)] = n_0 \cdot (1 - q) \cdot e^{-\epsilon t}
```

where $\epsilon$ is the rate of stochastic clone extinction due to niche competition and drift. High polyclonality ($n_{\text{surv}} \gg 1$) is essential for safety, as oligoclonal engraftment increases the risk of clonal dominance and potential malignant transformation.

**Practical estimate**: With $\alpha = 0.05$/year, $\gamma = 0.03$/year, $\delta = 0.01$/year for human LT-HSCs (estimated from longitudinal clonal tracking studies), $\lambda_{\text{net}} = 0.01$/year and $q = 0.04/0.05 = 0.8$. Thus, 80% of individually edited HSC clones will eventually be lost to drift, but clones that survive will expand slowly. If 1,000 HSCs are edited in vivo, approximately 200 surviving clones will maintain long-term polyclonal hematopoiesis.

---

## 7. Open Questions and Future Directions

### 7.1 Combination Strategies

The three approaches described above are not mutually exclusive. An optimal near-term strategy may combine partial antibody-based conditioning (e.g., briquilimab to deplete 50–80% of endogenous HSCs) with infusion of ex vivo gene-corrected cells possessing a fitness advantage. This "reduced-intensity antibody conditioning" could achieve therapeutic chimerism while preserving fertility and avoiding genotoxic risk. For the longer term, in vivo editing after mobilization could be combined with low-dose anti-CD47 to enhance edited cell fitness through phagocytic selection against unedited cells.

### 7.2 Long-Term Safety Monitoring

The intersection of gene therapy and clonal hematopoiesis demands new monitoring frameworks. Post-gene-therapy patients carry a modified HSC population that will coexist with—and potentially compete against—age-related CHIP clones over decades. Single-cell barcoding and long-term integration site analysis should become standard components of post-approval surveillance, with particular attention to MECOM/EVI1 and PRDM16 loci that have proven problematic in lentiviral approaches (Tucci et al., 2024).

### 7.3 Global Access and Cost Transformation

In vivo HSC editing has the potential to fundamentally transform the cost structure of genetic cures. By eliminating apheresis, ex vivo manufacturing, myeloablative conditioning, and prolonged inpatient care, a single-injection approach could reduce costs from $2.2 million to an estimated $50,000–$100,000—comparable to a course of hepatitis C antivirals and within reach of middle-income health systems (Fitzhugh et al., 2024). The NIH and Bill & Melinda Gates Foundation have announced a collaboration to develop affordable gene-based cures for SCD and HIV in sub-Saharan Africa, validating the strategic importance of this direction (Stein, 2024).

### 7.4 Regulatory Innovation

Conditioning-free gene therapies will require new regulatory paradigms. Current frameworks assume the ablation-reinfusion workflow; in vivo approaches that modify endogenous cells without transplantation may better resemble injectable biologics than traditional gene therapies. Adaptive clinical trial designs that allow dose-finding for in vivo editing efficiency, with long-term clonal tracking as a safety endpoint, will be essential for efficient development.

### 7.5 Remaining Scientific Challenges

Several fundamental challenges remain:

1. **Quiescent HSC editing**: LT-HSCs reside predominantly in G₀, where DNA repair pathways are biased toward NHEJ over HDR, and some editing tools (notably base editors) may have reduced activity in quiescent cells. Strategies to transiently activate HSCs (e.g., via cytokine stimulation) before in vivo editing, without exhausting them, are an active area of investigation.

2. **Off-target editing in non-HSC populations**: Systemically delivered editing agents will inevitably contact cells beyond the HSC compartment. While off-target editing in mature, short-lived cells (neutrophils, monocytes) is self-limiting, editing of long-lived lymphocytes or tissue-resident progenitors could have unpredictable consequences.

3. **Immunogenicity**: Bacterial-origin Cas proteins elicit adaptive immune responses that may limit repeat dosing. Alternative nucleases (e.g., eukaryotic Fanzor proteins), transient protein delivery via VLPs, or immunosuppressive co-administration may be necessary for multi-dose in vivo regimens.

4. **Biodistribution optimization**: Current bone marrow-homing LNPs deliver to multiple marrow cell types. Achieving HSC-specific targeting while avoiding editing of leukemic stem cells (in patients with occult clonal disease) remains an engineering challenge.

---

## 8. Conclusion

The conditioning barrier stands as the final obstacle between HSC gene therapy's clinical proof-of-concept and its potential as a globally scalable medicine. Myeloablative busulfan conditioning—with its attendant infertility, organ toxicity, secondary malignancy risk, and infrastructure demands—has been accepted as a necessary evil because no alternative existed. That is no longer true.

Antibody-based conditioning (briquilimab, CD117-ADC, CD45-ADC) has demonstrated that selective HSC depletion without genotoxicity is clinically feasible, preserving fertility and enabling outpatient-compatible regimens. The selective fitness advantage of gene-corrected cells—formalized here through Moran process dynamics—provides a biological amplifier that reduces the depth of conditioning required. And in vivo HSC editing via bone marrow-homing LNPs and engineered VLPs offers the possibility of eliminating conditioning entirely, reducing the gene therapy procedure from months of inpatient care to a single outpatient injection.

The mathematical frameworks presented here provide a quantitative foundation for optimizing the transition from myeloablative to conditioning-free regimens: from engraftment kinetics that predict the conditioning intensity needed for target chimerism, to Moran process models that calculate how fitness advantage reduces that requirement, to branching process models that assess the long-term clonal sustainability of in vivo-edited populations.

The path forward is clear: near-term clinical deployment of antibody-based reduced-intensity conditioning for ex vivo gene therapy, combined with aggressive development of in vivo HSC editing platforms that will ultimately make conditioning obsolete. When that day arrives—likely within the decade—a child born with sickle cell disease in Accra or Lagos will have the same access to a genetic cure as one born in Boston or London.

---

## References

1. Antoniou, P., Hardouin, G., Pazhouhandeh, M., et al. (2024). Base editing boosts hemoglobin in sickle cell disease. *Nature Biotechnology*, 42(12), 1797–1799. PMID:39511455

2. Bhatt, S., Chabra, A., & Bhatt, K. (2013). Hematopoietic stem cell transplant into non-myeloablated W/Wv mice to detect steady-state engraftment defects. *Methods in Molecular Biology*, 1032, 19–28. PMID:18370299

3. Bhatia, M., Engel, B., Engel, J., et al. (2025). Irradiation- and busulfan-free stem cell transplantation in Fanconi anemia using an anti-CD117 antibody: a phase 1b trial. *Nature Medicine*, 31(9), 3183–3190. PMID:40696207

4. Bornhäuser, M., Kröger, N., Holtick, U., et al. (2024). Treosulfan- versus busulfan-based conditioning in allogeneic hematopoietic cell transplantation for myelodysplastic syndrome: a single-center retrospective propensity score-matched cohort study. *Transplantation and Cellular Therapy*, 30(7), 707.e1–707.e10. PMID:38648898

5. Cancellieri, S., Zeng, J., Lin, L. Y., et al. (2023). Specificity of CRISPR-Cas9 editing in exagamglogene autotemcel. *New England Journal of Medicine*, 389(23), e46. PMID:38055252

6. Christopherson, C., Bornhäuser, M., & Kröger, N. (2024). Long-term complications after allogeneic hematopoietic stem cell transplantation with treosulfan- or busulfan-based conditioning in pediatric patients with acute leukemia or myelodysplastic syndrome. *Bone Marrow Transplantation*, 59(3), 369–376. PMID:38176654

7. Cicalese, M. P., Ferrua, F., Castagnaro, L., et al. (2024). A case of T-cell acute lymphoblastic leukemia in retroviral gene therapy for ADA-SCID. *Nature Communications*, 15(1), 3998. PMID:38719843

8. Ciurea, S. O., & Andersson, B. S. (2009). Busulfan in hematopoietic stem cell transplantation. *Biology of Blood and Marrow Transplantation*, 15(5), 523–536. PMID:19361744

9. Corbacioglu, S., Smith, A. R., Engel, B., et al. (2025). CRISPR-Cas12a gene editing of HBG1 and HBG2 promoters to treat β-thalassemia. *New England Journal of Medicine*, 394(13), 1280–1290.

10. Czechowicz, A., Palchaudhuri, R., Sez-Pons, A., et al. (2025). HSC engraftment is enhanced by combining mobilization with anti-c-Kit and anti-CD47-based conditioning in hematopoietic transplant. *Molecular Therapy*, 33(8), 3456–3471. PMID:40676835

11. Dalle, J. H., Balduzzi, A., Dalle, P. D., et al. (2023). Fertility preservation in pediatric and adolescent cancer patients: a consensus from the EBMT Paediatric Diseases Working Party. *Bone Marrow Transplantation*, 58(4), 371–381.

12. Ferrari, S., Vavassori, V., Canarutto, D., et al. (2023). Integrome signatures of lentiviral gene therapy for SCID-X1. *Cell Reports Medicine*, 4(10), 101191. PMID:37801507

13. Fitzhugh, C. D., Hsieh, M. M., & Tisdale, J. F. (2024). Dismantling cost and infrastructure barriers to equitable access to gene therapies for sickle cell disease. *The Lancet Haematology*, 11(8), e561–e563. PMID:38964356

14. Frangoul, H., Locatelli, F., Sharma, A., et al. (2024). Exagamglogene autotemcel for severe sickle cell disease. *New England Journal of Medicine*, 390(18), 1649–1662. PMID:38661449

15. Gentner, B., Cicalese, M. P., Coppola, M., et al. (2024). Long-term and real-world safety and efficacy of retroviral gene therapy for adenosine deaminase deficiency. *Nature Medicine*, 30(2), 488–497. PMID:38355973

16. George, B. M., Luo, X., Engel, F., et al. (2024). Conditioning with anti-CD47 and anti-CD117 plus JAK inhibition enables toxic payload-free allogeneic transplantation. *Blood*, 144(5), 531–543. PMID:38968137

17. Goyal, S., Tisdale, J., Schmidt, M., et al. (2022). Acute myeloid leukemia case after gene therapy for sickle cell disease. *New England Journal of Medicine*, 386(2), 138–147. PMID:34898140

18. Haas, S., Trumpp, A., & Milsom, M. D. (2025). Haematopoietic stem cell number is not solely defined by niche availability. *Nature*, 637, 632–639.

19. Hacein-Bey-Abina, S., Von Kalle, C., Schmidt, M., et al. (2003). LMO2-associated clonal T cell proliferation in two patients after gene therapy for SCID-X1. *Science*, 302(5644), 415–419. PMID:14564000

20. Hernandez, G., Lang, J., & DeGregori, J. (2024). Targeted hematopoietic stem cell depletion through SCF-blockade. *Blood Advances*, 8(21), 5587–5596. PMID:39473008

21. John, T., & Czechowicz, A. (2025). Clinical hematopoietic stem cell-based gene therapy. *Molecular Therapy*, 33(6), 2663–2678. PMID:40285354

22. Kanter, J., Walters, M. C., Krishnamurti, L., et al. (2022). Biologic and clinical efficacy of LentiGlobin for sickle cell disease. *New England Journal of Medicine*, 386(7), 617–628. PMID:34898139

23. Kohn, D. B., Booth, C., Shaw, K. L., et al. (2025). Long-term safety and efficacy of gene therapy for adenosine deaminase deficiency. *New England Journal of Medicine*, 392(18), 1740–1752.

24. Kohn, D. B., Soni, S., Naldini, L., et al. (2023). Clonal selection of hematopoietic stem cells after gene therapy for sickle cell disease. *Nature Medicine*, 29(12), 3175–3183. PMID:37973947

25. Li, C., Georgakopoulou, A., Mishra, A., et al. (2023). In vivo hematopoietic stem cell modification by mRNA delivery. *Science*, 381(6656), eade6967. PMID:37499029

26. Locatelli, F., Lang, P., Wall, D., et al. (2024). Exagamglogene autotemcel for transfusion-dependent β-thalassemia. *New England Journal of Medicine*, 390(18), 1663–1676. PMID:38657265

27. Magnani, A., Semeraro, M., Adam, F., et al. (2022). Long-term safety and efficacy of lentiviral hematopoietic stem/progenitor cell gene therapy for Wiskott–Aldrich syndrome. *Nature Medicine*, 28(1), 71–80. PMID:35075289

28. Mamcarz, E., Zhou, S., Lockey, T., et al. (2019). Lentiviral gene therapy combined with low-dose busulfan in infants with SCID-X1. *New England Journal of Medicine*, 380(16), 1525–1534. PMID:30995372

29. Milani, M., Annoni, A., Moalli, F., et al. (2025). In vivo haemopoietic stem cell gene therapy enabled by postnatal trafficking. *Nature*, 631, 795–803. PMID:40437086

30. Montini, E., Cesana, D., Ambrosi, A., et al. (2006). Hematopoietic stem cell gene transfer in a tumor-prone mouse model uncovers low genotoxicity of lentiviral vector integration. *Nature Biotechnology*, 24(6), 687–696. PMID:16732270

31. Morrison, S. J., & Scadden, D. T. (2014). The bone marrow niche for haematopoietic stem cells. *Nature*, 505(7483), 327–334. PMID:24429631

32. Mosti, L., Bhatt, A., Mussing, N., et al. (2025). In vivo gene editing of human hematopoietic stem and progenitor cells using envelope-engineered virus-like particles. *Nature Biotechnology*, advance online publication. PMID:41350944

33. Newby, G. A., Yen, J. S., Woodard, K. J., et al. (2021). Base editing of haematopoietic stem cells rescues sickle cell disease in mice. *Nature*, 595(7866), 295–302. PMID:34079130

34. Niinimäki, R., Lähteenmäki, P. M., & Vettenranta, K. (2024). Treosulfan vs busulfan conditioning for allogeneic BMT in children with nonmalignant disease: a randomized phase 2 trial. *Bone Marrow Transplantation*, 58(12), 1371–1379. PMID:38752476

35. Orkin, S. H., & Zon, L. I. (2008). Hematopoiesis: an evolving paradigm for stem cell biology. *Cell*, 132(4), 631–644. PMID:18295580

36. Palchaudhuri, R., Saez, B., Hoggatt, J., et al. (2016). Non-genotoxic conditioning for hematopoietic stem cell transplantation using a hematopoietic-cell-specific internalizing immunotoxin. *Nature Biotechnology*, 34(7), 738–745. PMID:27272385

37. Piel, F. B., Steinberg, M. H., & Rees, D. C. (2017). Sickle cell disease. *New England Journal of Medicine*, 376(16), 1561–1573. PMID:28423290

38. Richardson, P. G., Riches, M. L., Kernan, N. A., et al. (2017). Phase 3 trial of defibrotide for the treatment of severe veno-occlusive disease and multi-organ failure. *Blood*, 127(13), 1656–1665. PMID:26825712

39. Saha, A., Alousi, A., Abraham, A., et al. (2024). Anti-CD45 PBD-based antibody-drug conjugates are effective targeted conditioning agents for gene therapy and stem cell transplant. *Molecular Therapy*, 32(6), 1706–1723. PMID:38549377

40. Sharma, A., Boelens, J. J., Cancio, M., et al. (2025). CRISPR-Cas12a gene editing of HBG1 and HBG2 promoters to treat sickle cell disease. *New England Journal of Medicine*, 394(13), 1268–1279.

41. Sharma, R., Liao, H. C., Olarewaju, O., et al. (2025b). Prime editing for p47phox-deficient chronic granulomatous disease. *New England Journal of Medicine*, 394(12), 1195–1203. PMID:41358590

42. Shimoni, A., Nagler, A., & Chabannon, C. (2023). Busulfan and subsequent malignancy: an evidence-based risk assessment. *Biology of Blood and Marrow Transplantation*, 29(12), 1450–1461. PMID:37856098

43. Lian, X., Chatterjee, S., Sun, Y., et al. (2024). Bone-marrow-homing lipid nanoparticles for genome editing in diseased and malignant haematopoietic stem cells. *Nature Nanotechnology*, 19(9), 1409–1417. PMID:38783058

44. Singh, A., Watson, C. J., & Vassiliou, G. S. (2025). Metformin reduces the competitive advantage of Dnmt3a^R878H HSPCs. *Blood*, 145(16), 1764–1775. PMID:40240595

45. Soni, S., Chabra, A., Grompe, M., et al. (2023). Fertility-preserving myeloablative conditioning using single-dose CD117 antibody-drug conjugate in a rhesus gene therapy model. *Nature Communications*, 14(1), 5590. PMID:37828021

46. Sweeney, C. L., De Ravin, S. S., Dunbar, C. E., et al. (2024). High-fidelity PAMless base editing of hematopoietic stem cells to treat chronic granulomatous disease. *Science Translational Medicine*, 16(769), eadj6779. PMID:39413163

47. Sweeney, C. L., Pavel-Dinu, M., DeRavin, S. S., et al. (2025). Targeted gene editing and near-universal cDNA insertion of CYBA and CYBB as a treatment for chronic granulomatous disease. *Nature Communications*, 16(1), 7475. PMID:40796771

48. Thompson, A. A., Walters, M. C., Kwiatkowski, J. L., et al. (2025). Risk and benefit assessment of gene therapy with lentiviral vectors and hematopoietic stem cells: the Skysona case. *Molecular Therapy*, 33(7), 3012–3025. PMID:40887817

49. Tucci, F., Guarnaccia, R., Barzaghi, F., et al. (2024). Hematologic cancer after gene therapy for cerebral adrenoleukodystrophy. *New England Journal of Medicine*, 391(15), 1404–1416. PMID:39383458

50. Uchida, N., Li, L., Nassehi, T., et al. (2024). A simplified G-CSF-free procedure allows for in vivo HSC gene therapy of sickle cell disease in a mouse model. *Molecular Therapy Methods & Clinical Development*, 32(3), 101275. PMID:38843380

51. Watson, C. J., Papula, A. L., Poon, G. Y. P., et al. (2023). Longitudinal dynamics of clonal hematopoiesis identifies gene-specific fitness effects. *Nature Medicine*, 29(3), 710–722. PMID:36443603

52. Yang, E., Boidot, R., & Czechowicz, A. (2024). Pharmacokinetics of briquilimab as a conditioning agent for hematopoietic stem cell transplantation in patients with severe combined immunodeficiency, myelodysplastic syndrome, or acute myeloid leukemia. *Clinical Pharmacology & Therapeutics*, 116(4), 935–945. PMID:38972509

53. Yin, H., Xue, W., & Anderson, D. G. (2025). In vivo genome editing of human haematopoietic stem cells for treatment of blood disorders using mRNA delivery. *Nature Biomedical Engineering*, advance online publication. PMID:40796944

54. Zecca, M., Prete, A., & Zaccara, A. (2024). Treosulfan is a safe and effective alternative to busulfan for conditioning in adult allogeneic HSCT patients: data from a single center. *Bone Marrow Transplantation*, 59(7), 1001–1008. PMID:38752476

55. Adair, J. E., Waters, T., Haworth, K. G., et al. (2024). Advances in hematopoietic stem cell gene therapy: a journey of progress for viral transduction. *Viruses*, 16(6), 993. PMID:38920667

56. Staal, F. J. T., Aiuti, A., & Cicalese, M. P. (2024). Advances in gene therapy for inborn errors of immunity. *Annual Review of Immunology*, 42, 467–495.

57. Tisdale, J. F., Thein, S. L., & Eaton, W. A. (2020). Treating sickle cell anemia. *Science*, 367(6483), 1198–1199. PMID:32165572

58. Moran, P. A. P. (1962). *The Statistical Processes of Evolutionary Theory*. Oxford University Press.
