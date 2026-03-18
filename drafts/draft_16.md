# Genetic Engineering

Gene editing has crossed the threshold from experimental science to clinical medicine. The December 2023 FDA approval of Casgevy (exagamglogene autotemcel)—the first CRISPR-Cas9-based therapy—marked a watershed, and the two years since have witnessed an explosion of innovation across every dimension of the field: novel effectors, precision editing chemistries, programmable DNA integration, in vivo clinical delivery, and AI-designed editors. This review synthesizes the most significant recent across ten interconnected domains, from next-generation Cas proteins and base/prime editing to bridge recombinases, clinical trial milestones, delivery platforms, and the evolving regulatory landscape. The pace of discovery has accelerated such that an entirely new taxonomy of CRISPR systems—now encompassing 7 types and 46 subtypes—was required by 2025, and multiple clinical programs have delivered curative or near-curative outcomes for previously intractable genetic diseases. Yet fundamental challenges persist: a patient death during Intellia’s Phase 3 ATTR trial placed programs on clinical hold, chromothripsis remains an intrinsic risk of double-strand-break editing, and gene therapy pricing ($2.2–4.25 million per treatment) threatens to confine these technologies to wealthy nations. The field stands at an inflection point where scientific capability has outpaced the infrastructure for safe, equitable deployment.

## 1. From Molecular Scissors to a Complete Genome Engineering Toolkit

The CRISPR-Cas9 system, recognized with the 2020 Nobel Prize in Chemistry awarded to Emmanuelle Charpentier and Jennifer Doudna for their landmark 2012 demonstration of programmable RNA-guided DNA cleavage, has spawned an ecosystem of gene editing tools that now extends far beyond the original nuclease paradigm. The original SpCas9 protein, while revolutionary, generates double-strand breaks (DSBs) that are resolved through error-prone non-homologous end joining (NHEJ) or, less frequently, homology-directed repair (HDR). This fundamental limitation has driven the development of editing modalities that avoid DSBs entirely—base editors, prime editors, epigenome editors, and programmable integrases—each addressing distinct therapeutic needs.

The scale of recent innovation is captured by an updated evolutionary classification of CRISPR-Cas systems published in *Nature Microbiology* in 2025 by Makarova, Wolf, and colleagues, which expanded the taxonomy to 2 classes, 7 types, and 46 subtypes, up from 6 types and 33 subtypes in 2020 (doi: 10.1038/s41564-025-02180-8). This expansion reflects both the discovery of fundamentally new CRISPR functionalities—including type IV variants with DNA cleavage activity and type V variants that inhibit replication without cleaving DNA—and the growing recognition that CRISPR biology extends beyond adaptive immunity into diverse cellular roles.

The clinical pipeline has matured correspondingly. As of early 2026, over 100 CRISPR-based clinical trials are active or completed globally, spanning hematologic diseases, cardiovascular conditions, cancer immunotherapy, and rare metabolic disorders. The FDA has approved multiple gene therapies in 2024–2025, and a transformative new “plausible mechanism” regulatory framework announced in February 2026 promises to enable bespoke CRISPR therapies for ultra-rare diseases without requiring traditional large-scale clinical trials.

## 2. Next-Generation CRISPR Effectors Are Reshaping the Editing Landscape

### Compact Nucleases Open the Door to Single-Vector Delivery

The ~1,368 amino acid size of SpCas9 constrains its packaging into adeno-associated virus (AAV) vectors, whose ~4.7 kb cargo limit has driven intense efforts to identify or engineer smaller CRISPR effectors. Multiple lines of discovery have converged in 2024–2026 to produce a diverse array of compact, clinically viable nucleases.

TnpB and IscB, the evolutionary ancestors of Cas12 and Cas9 respectively, have emerged as particularly promising miniature effectors. Nagahata and colleagues published cryo-EM structures of four phylogenetically diverse RNA-guided nucleases in *Nature Structural & Molecular Biology* (2025), revealing the evolutionary trajectory from transposon-associated IscB (~500 residues) to full-length Cas9 (~1,600 residues) through loss of the PLMP domain and acquisition of REC domains (doi: 10.1038/s41594-025-01743-x). Engineering of IscB variants has yielded practical tools: enDelIscB, with 48.9-fold increased activity over wild-type, functions as a miniature base editor platform (IminiBEs achieving 67% C-to-T and 52% A-to-G efficiency) while recognizing flexible NAC target-adjacent motifs (*Nature Communications*, 2025). A comprehensive assessment of TnpB editing systems published in *Genome Biology* (2026) identified ISYmu1 TnpB as offering the optimal balance of editing activity and specificity among four tested variants (doi: 10.1186/s13059-026-03949-8).

The Cas12f subfamily has undergone rapid optimization. Park, Kim, and colleagues developed eCas12f1, an enhanced Un1Cas12f1 variant with cleavage activity comparable to SpCas9 (*Nature Communications*, 2025; doi: 10.1038/s41467-025-56048-w). An alternative engineering strategy added an N-terminal α-helix to create hpCasMINI variants showing improved gene activation and DNA cleavage in mammalian cells and mice (doi: 10.1038/s41467-025-60124-6). Circular guide RNAs (cgRNAs) designed for Cas12f improved gene activation efficiency 1.9–19.2-fold and, when combined with phase separation systems, achieved further 2.3–3.9-fold increases (doi: 10.1038/s41467-025-58367-4). A type V-N effector, RdCas12n, was structurally characterized and engineered for effective human cell editing, expanding the repertoire of hypercompact nucleases recognizing rare A-rich PAMs (*Nature Communications*, 2025; doi: 10.1038/s41467-025-61290-3).

### TIGR-Tas: A Fundamentally New Class of RNA-Guided Systems

Perhaps the most surprising discovery of 2025 was the identification of TIGR-Tas (Tandem Interspaced Guide RNA-Targeting Associated systems) by Feng Zhang’s laboratory, published in *Science* (Faure, Saito, Wilkinson et al., doi: 10.1126/science.adv9789; PMID: 40014690). TIGR systems represent a modular RNA-guided DNA-targeting architecture distinct from canonical CRISPR. Found in phage genomes and parasitic bacteria, TasR proteins are approximately one-quarter the size of Cas9, require no PAM sequence, and can be reprogrammed for DNA cleavage in human cells. The discovery underscores the vast unexplored reservoir of nucleic acid-guided systems in mobile genetic elements.

Complementing this, Zhang’s lab identified reprogrammable RNA-targeting CRISPR systems that evolved from RNA toxin-antitoxin modules, published in *Cell* (Zilberzwige-Tal, Altae-Tran et al., 2025; doi: 10.1016/j.cell.2025.01.034), and ancestral Cas13 ribonucleases were characterized by Yoon and colleagues in *Science* (2024), further expanding the toolkit for RNA manipulation.

### AI-Designed Editors Represent a Paradigm Shift

The convergence of artificial intelligence with CRISPR biology has produced editors designed de novo rather than borrowed from nature. Ruffolo, Nayfach, and colleagues at Profluent Bio trained large language models on over one million CRISPR operons and generated OpenCRISPR-1, the first AI-designed gene editor, published in *Nature* (2025; PMID: 40739342; doi: 10.1038/s41586-025-09298-z). Despite being ~400 mutations removed from SpCas9 in sequence space, OpenCRISPR-1 achieves comparable or improved activity and specificity and is compatible with base editing architectures. A parallel development, CRISPR-GPT, published in *Nature Biomedical Engineering* by Qu, Huang, and colleagues, provides an LLM agent system that automates CRISPR experiment design, guide RNA optimization, and data analysis (2026; doi: 10.1038/s41551-025-01463-z). A comprehensive review in *Nature Reviews Genetics* (2025) outlined how deep learning is advancing guide RNA design, editor protein engineering, novel effector discovery, and editing outcome prediction (doi: 10.1038/s41576-025-00907-1).

## 3. Base Editing and Prime Editing Have Achieved Clinical-Grade Precision

### Base Editing Transitions from Laboratory to Clinic

David Liu’s laboratory at the Broad Institute continues to drive base editing innovation, but the most dramatic developments of 2025–2026 have been clinical. BEAM-302, developed by Beam Therapeutics for alpha-1 antitrypsin deficiency (AATD), represents the first-ever clinical demonstration of precise genetic correction of a disease-causing point mutation via in vivo base editing. In Phase 1/2 results (NCT06389877), a single LNP-delivered adenine base editor correcting the PiZ→PiM mutation achieved dose-dependent correction with 91% of circulating AAT being corrected M-AAT at Day 28 in the 60 mg cohort, mean total AAT of 12.4 µM exceeding the 11 µM protective threshold, and 79% reduction in toxic mutant Z-AAT. As of August 2025, 17 patients had been dosed across four cohorts with no serious adverse events.

BEAM-101 (risto-cel) for sickle cell disease has delivered robust clinical validation of ex vivo base editing. Updated data presented at ASH 2025 showed durable HbF induction exceeding 60% in 31 treated patients, with HbS below 40% and no severe vaso-occlusive crises post-engraftment through follow-up extending to 20.4 months. The approach uses adenine base editing to modify the BCL11A enhancer in autologous CD34+ HSPCs.

Verve Therapeutics has advanced base editing for cardiovascular disease. VERVE-102, a next-generation GalNAc-LNP-delivered base editor targeting PCSK9, showed dose-dependent LDL-C reductions of up to 59% in the Heart-2 Phase 1b trial (NCT06164730), with well-tolerated safety profile and no treatment-related serious adverse events. VERVE-201 (targeting ANGPTL3) began dosing in the Pulse-1 Phase 1b trial in November 2024.

A critical advance for cell therapy manufacturing was reported by Engel, June, and colleagues in *PNAS* (2025; PMID: 40324075): head-to-head comparison of adenine base editing versus Cas9 nuclease for quadruple-gene-knockout allogeneic CAR-T cells (targeting B2M, CIITA, TRAC, and PVR) demonstrated that ABE achieved higher manufacturing yields, zero translocations (versus Cas9-exclusive translocations), superior effector function under chronic antigen stimulation, and enhanced tumor control in vivo.

### Prime Editing Enters the Clinic and Achieves Disease-Agnostic Capabilities

Prime editing, which uses a Cas9 nickase–reverse transcriptase fusion guided by a pegRNA to write desired sequences directly into the genome without DSBs, has reached two landmark milestones.

PM359 from Prime Medicine became the first prime editing therapy to enter clinical development, receiving IND clearance for ex vivo correction of NCF1 mutations in chronic granulomatous disease (CGD). By December 2025, Prime Medicine reported that two patients had been “effectively cured,” representing the first clinical demonstration of prime editing’s therapeutic potential.

Chauhan, Sharp, and Langer at MIT engineered prime editors with ~60-fold reduced unintended mutations, lowering error rates from approximately 1/7 to 1/101 for common editing types (*Nature*, October 2025; doi: 10.1038/s41586-025-09537-3). This safety improvement is critical for clinical translation.

Perhaps the most conceptually transformative advance was PERT (Prime Editing-mediated Readthrough of premature Termination codons), developed by Pierce, Liu, and colleagues (*Nature*, November 2025; doi: 10.1038/s41586-025-09732-2). PERT permanently converts an endogenous tRNA into an optimized suppressor tRNA, restoring protein production across diseases caused by nonsense mutations. A single editing agent demonstrated restoration of protein function in models of Batten disease, Tay-Sachs disease, and Hurler syndrome—establishing a disease-agnostic platform applicable to the ~11% of all pathogenic mutations that are premature stop codons.

Twin prime editing (twinPE), first described by Anzalone, Liu, and colleagues (*Nature Biotechnology*, 2022; PMID: 34887556), has been further advanced through evolved recombinases. Pandey, Liu, and colleagues developed eePASSIGE using PACE-evolved Bxb1 variants that achieve up to 60% donor integration at pre-installed landing sites and average 23% targeted gene integration at safe-harbor sites, with demonstrated therapeutic cargoes at CCR5, AAVS1, and ALB loci (*Nature Biomedical Engineering*, 2025; doi: 10.1038/s41551-024-01227-1).

## 4. Epigenome Editing Achieves Durable Gene Silencing Without DNA Sequence Changes

Epigenome editing—modifying gene expression through chromatin modifications rather than DNA sequence alterations—has matured from proof-of-concept to therapeutically relevant platforms in 2025.

Zhang’s laboratory at the Broad Institute developed OMEGAoff, a compact epigenetic repressor based on evolution-guided engineering of IscB (creating NovaIscB, 614 amino acids, ~100-fold more active than wild-type). Published in *Nature Biotechnology* (May 2025; PMID: 40335752; doi: 10.1038/s41587-025-02655-3), OMEGAoff can be packaged in a single AAV vector for durable in vivo gene silencing, including Pcsk9 knockdown with sustained cholesterol reduction in mice—demonstrating the clinical feasibility of compact epigenetic editors.

An all-RNA CRISPRoff platform for primary T cells was developed by Goudy, Gilbert, and colleagues at UCSF/Arc Institute (*Nature Biotechnology*, October 2025; doi: 10.1038/s41587-025-02856-w). This system achieves efficient, durable multiplexed epigenetic gene silencing maintained through 30–80 cell divisions, compatible with CAR-T manufacturing using orthogonal Cas12a for simultaneous knock-in. The practical significance is profound: epigenetic silencing avoids the translocations and chromothripsis risks associated with nuclease-mediated gene knockout.

The RENDER platform (Robust ENveloped Delivery of Epigenome-editor Ribonucleoproteins) enables transient RNP delivery of CRISPRoff, CRISPRi, and TET1-dCas9 into human cells, inducing durable epigenetic silencing in primary T cells and stem cell-derived neurons including reduction of tau protein (*Nature Communications*, 2025; doi: 10.1038/s41467-025-63167-x). Bell, Crossley, Weiss, and colleagues demonstrated that epigenetic editing to remove promoter CpG methylation from fetal globin genes reactivates HBG expression without cutting DNA, offering a potentially safer route to treating sickle cell disease (*Nature Communications*, 2025; doi: 10.1038/s41467-025-62177-z). Compact mRNA-delivered epigenetic editors using Cas-SF01 (a Cas12i3 variant) achieved durable Pcsk9 silencing in vivo via LNP delivery with superior specificity profiles (*The Innovation*, 2025).

## 5. Programmable DNA Integration Systems Transcend the Double-Strand Break

The ability to insert large DNA payloads (multi-kilobase genes, regulatory cassettes) at precise genomic locations without inducing DSBs represents perhaps the most sought-after capability in genome engineering. Several distinct technology platforms converged on this goal in 2024–2026.

### Bridge Recombinases Enable Programmable DNA Recombination

The discovery of bridge recombinases by Patrick Hsu’s group at the Arc Institute, published in *Nature* (2024; PMID: 38926615), revealed that IS110 insertion sequences encode a structured non-coding bridge RNA (bRNA) with two independently programmable loops—one binding target DNA, one binding donor DNA. This bispecific guide molecule enables programmable DNA insertion, excision, and inversion, representing the first nucleic acid-guided recombination system outside CRISPR and RNAi. Structural characterization by Hiraizumi, Nishimasu, and colleagues (*Nature*, 2024; PMID: 38926616) revealed the composite RuvC-Tnp active site spanning two recombinase dimers, phosphoserine intermediates, and Holliday junction resolution mechanisms.

In 2025, Perry, Hsu, and colleagues demonstrated that the ISCro4 bridge recombinase from *Citrobacter rodentium* is highly active in human cells, achieving programmable multi-kilobase excisions, inversions up to 0.93 Mb, and donor DNA insertion exceeding 6% efficiency using plasmid- or all-RNA-based delivery (*Science*, 2025; PMID: 41642947; doi: 10.1126/science.adz1884). Therapeutic proof-of-concept included BCL11A enhancer excision for sickle cell anemia and repeat sequence excision for Friedreich’s ataxia.

### CRISPR-Associated Transposases Achieve Therapeutic Efficiency Through Evolution

The critical barrier for CRISPR-associated transposases (CASTs)—RNA-guided transposon systems that integrate DNA without DSBs—has been their poor activity in human cells. Witte, Lampe, Sternberg, and Liu solved this through phage-assisted continuous evolution (PACE), generating evoCAST with over 200-fold improved integration activity in human cells (*Science*, 2025; PMID: 40373119; doi: 10.1126/science.adt5199). evoCAST achieves 10–30% insertion of kilobase-size DNA cargoes (up to 15 kb) across 14 genomic target sites, with no detected indels and low off-target integration. The system was applied to integration of factor IX for hemophilia, CD19-CAR for cancer immunotherapy, and disease gene correction for Fanconi anemia and phenylketonuria.

Structure-guided engineering complemented the evolutionary approach: Lampe, Sternberg, and colleagues published structural analysis of type I-F CASTs enabling further optimization for targeted gene insertion (*Nature Communications*, 2025). Gelsinger, Sternberg, Wang, and colleagues extended CAST applications to in vivo metagenomic editing of commensal bacteria, opening microbiome engineering possibilities (*Science*, 2025).

### R2 Retrotransposons and the STITCHR System

R2 retrotransposons—naturally occurring RNA-guided elements that insert at specific ribosomal DNA sites—have been reprogrammed for therapeutic gene insertion. Fell, Abudayyeh, Gootenberg, and colleagues developed STITCHR (Site-specific Target-primed Insertion through Targeted CRISPR Homing of Retroelements), identifying R2Tocc as a naturally reprogrammable retrotransposon that, when fused with SpCas9 nickase, enables scarless gene insertion of up to 12.7 kb at programmable genomic sites (*Nature*, 2025; PMID: 40205048; doi: 10.1038/s41586-025-08877-4).

Chen, Li, and colleagues engineered R2Tg from *Taeniopygia guttata* for all-RNA delivery, achieving over 60% targeted integration in mouse embryos with 99% on-target specificity (*Cell*, 2024; doi: 10.1016/j.cell.2024.06.049). Edmonds, Zhang, and colleagues further refined the system, engineering a compact all-RNA R2 system achieving over 80% integration efficiency in human cell lines (*Nature Communications*, 2025; doi: 10.1038/s41467-025-61321-z). Zhang, Collins, and colleagues demonstrated that avian A-clade R2 proteins achieve efficient, precise transgene insertion at native safe-harbor rDNA loci (*Nature Biotechnology*, 2025). Structural insights from Thawani, Collins, and colleagues via cryo-EM revealed the mechanistic basis for high template selectivity during target-primed reverse transcription (*Science Advances*, 2025; PMID: 40540573).

### Retron Editors Reach Practical Efficiency

Retron-based editing, which produces single-stranded DNA templates in situ using bacterial reverse transcriptases, achieved a breakthrough through metagenomic screening. Buffington, Finkelstein, and colleagues identified highly active retron reverse transcriptases from environmental bacteria, including Efe1-RT from clade 9, achieving ~30% editing efficiency in mammalian cells—a 20-fold improvement over previous systems. The approach is compatible with Cas12a and Cas9 nickase and was applied to cystic fibrosis gene correction targeting CFTR (*Nature Biotechnology*, 2025; doi: 10.1038/s41587-025-02879-3). An independently engineered Eco1 retron editor achieved 27-fold improved editing through optimized ncRNA architecture (*Nucleic Acids Research*, 2025; doi: 10.1093/nar/gkaf716).

### INSTALL and Engineered Large Serine Integrases

A fundamentally new approach to large DNA integration was published in *Nature* (2026) by Tou, Kleinstiver, and colleagues: INSTALL (Integration through Nucleus-Synthesized Template Addition of Large Lengths) uses circular single-stranded DNA donors with partial-duplex regions compatible with recombinase recognition sequences, overcoming the lethal innate immune response (cGAS-STING pathway) triggered by conventional dsDNA donors (doi: 10.1038/s41586-026-10241-z). In vivo LNP delivery in mice achieved safe, successful large DNA integration in livers, whereas conventional dsDNA caused fatal immune reactions.

Engineered large serine recombinase variants (superDn29-dCas9, goldDn29-dCas9, hifiDn29-dCas9) achieved up to 53% integration efficiency and 97% genome-wide specificity at endogenous human loci for payloads up to 12 kb (*Nature Biotechnology*, 2025; doi: 10.1038/s41587-025-02895-3).

## 6. Clinical Gene Editing Is Delivering Curative Outcomes Across Disease Areas

### Casgevy Demonstrates Durability Beyond Five Years

The clinical validation of CRISPR-Cas9 genome editing rests most firmly on Casgevy (exagamglogene autotemcel), which targets the BCL11A erythroid enhancer to reactivate fetal hemoglobin production. Phase 3 results published by Frangoul, Grupp, and colleagues in the *New England Journal of Medicine* (2024; PMID: 38661449) showed that 29 of 31 evaluable SCD patients (93.5%) achieved freedom from severe vaso-occlusive crises for ≥12 consecutive months. Long-term follow-up data presented at ASH 2025 extended these findings: 100% of patients (45/45) achieved the primary VOC-free endpoint, with mean VOC-free duration of 35.3 months (range 12.9–67.7) and the longest individual follow-up exceeding 5.5 years. For transfusion-dependent beta-thalassemia, 98.2% (55/56) patients achieved transfusion independence, reported by Locatelli, Grupp, and colleagues (*NEJM*, 2024; doi: 10.1056/NEJMoa2309673). Comprehensive off-target analysis across over 5,000 candidate sites confirmed no detectable off-target editing, as reported by Fine, Altshuler, and colleagues (*NEJM*, 2024; doi: 10.1056/NEJMc2313119).

Vertex Pharmaceuticals has initiated regulatory submissions for pediatric patients ages 5–11 based on Phase 3 data in 4 children, with all achieving the primary endpoint. As of early 2026, nearly 300 patients have been referred for Casgevy treatment, with over 45 authorized treatment centers worldwide.

### In Vivo CRISPR Editing Achieves Landmark Clinical Milestones—and Confronts Safety Limits

Nexiguran ziclumeran (nex-z/NTLA-2001) from Intellia Therapeutics represents the first systemic in vivo CRISPR therapy, using LNP-delivered Cas9 mRNA and guide RNA targeting hepatic TTR for transthyretin amyloidosis. Fontana, Gutstein, Gillmore, and colleagues published Phase 1 results in *NEJM* (2024; doi: 10.1056/NEJMoa2412309) showing 90% mean serum TTR reduction sustained through 24 months in 36 ATTR-CM patients. Phase 1 data in ATTR polyneuropathy confirmed −92% TTR reduction through 24 months (Adams, Gutstein, Manvelian et al., *NEJM*, 2025; doi: 10.1056/NEJMoa2510209). However, in October 2025, an 80-year-old patient experienced Grade 4 liver transaminase elevation and subsequently died, leading the FDA to place Phase 3 MAGNITUDE and MAGNITUDE-2 trials on clinical hold—a sobering reminder that in vivo gene editing carries serious hepatotoxicity risks even after more than 450 patients had been successfully dosed.

NTLA-2002 (lonvoguran ziclumeran) for hereditary angioedema, targeting the KLKB1 gene, delivered striking results in a Phase 2 randomized trial published by Cohn, Longhurst, and colleagues (*NEJM*, 2025; PMID: 39445704): monthly attack rates decreased by 75–77% versus placebo, with 73% of high-dose recipients achieving complete attack freedom. Long-term Phase 1 data showed 98% mean reduction in monthly attacks through 20+ months of follow-up, suggesting a potential functional cure.

CTX310 from CRISPR Therapeutics, targeting hepatic ANGPTL3, became the first in vivo CRISPR therapy for cardiovascular disease with results published by Laffin, Nissen, and colleagues (*NEJM*, 2025; PMID: 41211945; doi: 10.1056/NEJMoa2511778). A single intravenous dose in 15 patients with refractory dyslipidemia achieved mean reductions of ANGPTL3 −73 to −80%, LDL −49%, and triglycerides −55% at the highest doses—the first therapy ever to substantially and durably reduce both LDL and triglycerides in a single dose.

### Engineered Cell Therapies Benefit from Precision Editing

BE-CAR7, developed by Chiesa, Qasim, and the Great Ormond Street Hospital team, validated base-edited allogeneic CAR-T cells for relapsed/refractory T-cell acute lymphoblastic leukemia. Published in *NEJM* (2026; PMID: 41363805; doi: 10.1056/NEJMoa2505478), the Phase 1 trial showed that all 11 patients achieved complete morphologic remission at day 28, with 82% achieving deep MRD-negative remission enabling allogeneic stem cell transplant. The first patient, Alyssa, remains disease-free beyond three years.

CRISPR-edited tumor-infiltrating lymphocytes entered the clinic with CISH-knockout TILs for metastatic colorectal cancer, reported by Lou, Moriarity, and colleagues in *Lancet Oncology* (2025; PMID: 40315882). One patient achieved an exceptional complete response lasting 21+ months in refractory disease, providing the first evidence that intracellular checkpoint CISH can be targeted therapeutically.

Allogeneic CAR-T development is advancing across multiple programs. Caribou Biosciences’ CB-010 (vispacabtagene regedleucel), incorporating PD-1 knockout via CRISPR chRDNA editing, showed efficacy “on par with autologous treatments” in second-line large B-cell lymphoma. CRISPR Therapeutics’ CTX112 and CTX131 programs continue enrollment, while TyU19—an allogeneic anti-CD19 CAR-T with 5 simultaneous CRISPR edits—is being evaluated for severe autoimmune diseases.

### New Gene Therapy Approvals in 2025

Beyond Casgevy, 2025 brought several notable gene therapy approvals: Waskyra (etuvetidigene autotemcel) became the first gene therapy for Wiskott-Aldrich syndrome and the first developed through regulatory approval by a non-profit organization (Fondazione Telethon); Zevaskyn (prademagene zamikeracel) was approved as the first gene therapy for recessive dystrophic epidermolysis bullosa; and Encelto (revakinagene taroretcel-lwey) was approved for idiopathic macular telangiectasia type 2. In gene editing for ocular disease, Pennesi, Pierce, and colleagues reported BRILLIANCE Phase 1/2 trial results for EDIT-101 (AAV5-delivered SaCas9) in CEP290-associated retinal degeneration, with approximately 79% of 14 patients showing measurable vision improvement (*NEJM*, 2024; doi: 10.1056/NEJMoa2309915).

## 7. Safety, Specificity, and the Imperative of Rigorous Off-Target Assessment

### New Detection Methods Address Editor-Specific Off-Target Profiles

The field has progressed from nuclease-focused off-target detection to editor-specific methods. CHANGE-seq-BE, developed by Lazzarotto, Tsai, and colleagues and published in *Nature Biotechnology* (2026; PMID: 41482541), provides sensitive, unbiased profiling of base editor off-target activity using selective sequencing of base-editor-modified circular genomic DNA. The method found that 98.8% of validated off-target sites were unique to ABE8e versus Cas9 nuclease, underscoring that base editors have fundamentally different off-target signatures requiring dedicated detection tools. CHANGE-seq-BE was applied to support an emergency FDA IND for CD40L-deficient X-HIGM syndrome.

Tracking-seq, developed by Zhu and colleagues, provides a universal in situ method applicable to Cas9, base editors, and prime editors by tracking RPA-bound ssDNA followed by strand-specific library construction (*Nature Biotechnology*, 2025). The CRISPRoffT database integrating off-target data from 85 Cas/gRNA combinations in 34 cell lines confirmed low overlap between detection technologies, underscoring that no single method is comprehensive (*Nucleic Acids Research*, 2025). PE-tag enables genome-wide mapping of prime editing off-targets, as described in *Nature Methods*, while DISCOVER-seq+ provides enhanced detection sensitivity in primary cells and tissues.

### Chromothripsis Remains a Fundamental Concern for DSB-Based Editing

Leibowitz, Pellman, and colleagues established that CRISPR-Cas9 editing generates micronuclei and chromosome bridges initiating chromothripsis—catastrophic chromosomal rearrangement—as an on-target consequence (*Nature Genetics*, 2021; PMID: 33846636). Critically, this occurs even at clinically relevant loci: ~2.5% micronucleation was observed at the BCL11A enhancer in HSPCs. Improving guide specificity does not prevent this risk, as it arises from the DSB itself. Papathanasiou, Jaenisch, Pellman, and colleagues further documented complete chromosome loss in mouse embryos after CRISPR editing (*Nature Communications*, 2021). A Cas9-degron system using pomalidomide-based degradation, developed by Khajanchi and Saha, reduces protein half-life within 4 hours, achieving 3–5× decreased editing as a temporal control strategy to mitigate prolonged Cas9 activity (*Molecular Therapy*, 2025).

These findings provide a powerful rationale for the field’s pivot toward DSB-free editing modalities—base editing, prime editing, and epigenome editing—for therapeutic applications.

### Immunogenicity Demands Engineering Solutions

Pre-existing adaptive immunity to Cas proteins is widespread in the human population. Charlesworth and Porteus documented anti-SaCas9 antibodies in 78% and anti-SpCas9 antibodies in 58% of tested individuals, with T-cell reactivity at similar frequencies (*Nature Medicine*, 2019; PMID: 30692695). Raghavan, Zhang, and colleagues at the Broad Institute responded with Redi (Reduced Immunogenicity) nucleases—SaCas9.Redi and AsCas12a.Redi variants developed through MAPPs analysis and computational modeling that reduce MHC binding and attenuate CTL responses while maintaining wild-type activity (*Nature Communications*, 2025; doi: 10.1038/s41467-024-55522-1). In vivo PCSK9 editing with SaCas9.Redi achieved comparable efficacy to wild-type with significantly reduced immune responses. A comprehensive review by Nitsch and colleagues documented highly variable serum antibody prevalence (SpCas9: 2.5–65%; SaCas9: 10–79%) and reviewed strategies including epitope engineering, delivery optimization, and the discovery of Cas9-reactive regulatory T cells (*Molecular Therapy*, 2025).

### High-Fidelity Cas9 Variants for Clinical Applications

The clinical standard for ex vivo RNP-delivered editing is HiFi Cas9 (R691A single mutation), which retains approximately 82% of wild-type activity while substantially reducing off-target cleavage (Vakulskas et al., *Nature Medicine*, 2018; PMID: 30082871). Multi-mutant variants (eSpCas9, SpCas9-HF1, HypaCas9, evoCas9) achieve higher specificity but suffer significant activity losses when delivered as ribonucleoprotein. The AsCas12a nuclease has been engineered for enhanced potency by reducing protein-DNA interactions to mediate faster R-loop formation, with Doudna and colleagues revealing the dynamic basis of supercoiling-dependent DNA interrogation through R-loop intermediates (*Nature Communications*, 2025; PMID: 40133266) and a rapid two-step target capture mechanism underlying efficient Cas9 genome editing (*Molecular Cell*, 2025; PMID: 40273916; doi: 10.1016/j.molcel.2025.03.024).

## 8. Delivery Technologies Are Diversifying Toward Organ-Specific Precision

### Virus-Like Particles Reach Fifth-Generation Optimization

Engineered virus-like particles (eVLPs), developed by the Liu laboratory, have progressed through five generations of optimization. The v4 eVLP architecture, first described in *Cell* (2022; PMID: 35021064), achieved 63% liver Pcsk9 editing in mice with virtually no off-target effects. PE-eVLPs (v3/v3b) achieved 65–170× higher prime editing than initial architectures, with therapeutic retinal editing demonstrated in mouse blindness models (*Nature Biotechnology*, 2024; PMID: 38191664). The v5 generation, developed through barcoded guide RNA evolution, shows 2–4× increased delivery potency over v4, with capsid mutations optimized for RNP packaging (*Nature Biotechnology*, 2025).

RIDE (Reconfigurable VLP-mediated Delivery), developed by Ling and colleagues, provides a cell-tropism-programmable VLP system achieving comparable efficiency to AAV and lentivirus with reprogrammable targeting to dendritic cells, T cells, and neurons (*Nature Nanotechnology*, 2025). The ENVLPE system uses aptamer-mediated RNP recruitment for near-stoichiometric Cas9:pegRNA ratios, achieving ~5.5-fold greater functional rescue in retinal models versus earlier PE-eVLPs at 10-fold lower doses.

### Lipid Nanoparticles Enable Organ-Targeted In Vivo Editing

LNPs have become the leading non-viral delivery platform for in vivo gene editing, with multiple clinical programs demonstrating efficacy. The SORT (Selective Organ Targeting) technology, developed by Cheng, Siegwart, and colleagues, uses a supplemental fifth lipid component to redirect organ targeting: 50% DOTAP formulations target lung, low-percentage formulations target liver, and 18PA targets spleen (*Nature Nanotechnology*, 2020). Clinical-stage LNP-CRISPR programs include Intellia’s nex-z and lonvo-z (liver-targeted), ReCode Therapeutics’ CT1100 using lung SORT LNPs for cystic fibrosis, and Verve’s GalNAc-LNP platform for cardiovascular targets. Intellia demonstrated the feasibility of redosing with in vivo CRISPR via LNP in 2024, showing additive pharmacodynamic effects—a critical milestone establishing that single-dose limitations of gene editing can be overcome.

A comprehensive review in *Small Methods* (2026) detailed the state-of-the-art in LNP component design, including ionizable lipids, helper lipids, cholesterol modifications, and PEG-lipid optimization for CRISPR cargo delivery (doi: 10.1002/smtd.202401632). Emerging strategies include anti-CD5 antibody-conjugated LNPs for T cell reprogramming, mannose-mediated LSEC targeting, and DNA/RNA barcoding systems for high-throughput LNP screening.

### Engineered AAV Capsids Achieve Transformative Tissue Specificity

AAV capsid engineering has produced remarkable tissue-specific variants enabling 10–400× dose reductions compared to natural serotypes. Nisanov, Schaffer, and colleagues reviewed three converging approaches—rational design, directed evolution, and machine learning—in *Molecular Therapy* (2025; PMID: 40176349). For CNS delivery, BI-hTFR1 (developed at the Broad Institute) binds human transferrin receptor 1 for 40–50× higher CNS expression than AAV9, while VCAP-102 (Voyager Therapeutics) achieves 20–400× improvement over AAV9 in brain transduction. For muscle delivery, MyoAAV capsids incorporating RGD-motifs enable up to 250× dose reduction, with MyoAAV4A demonstrating 10-fold lower dosing while outperforming AAV9 for glycogen storage disease IIIa (*Molecular Therapy Methods*, 2025). However, AAV safety concerns persist: two deaths from acute liver failure and three cardiac deaths among approximately 800 Elevidys (DMD gene therapy) recipients in 2025 underscore the risks of systemic high-dose AAV administration.

## 9. Anti-CRISPR Proteins and the Arms Race Between Phages and Bacteria

The discovery of anti-CRISPR (Acr) proteins has expanded from a curiosity of phage biology to a practical toolkit for temporal and spatial control of gene editing. Johnson, Terns, and colleagues discovered AcrIIIA2, a type III-A Acr that co-opts host enolase (a glycolysis enzyme) to form a ternary complex blocking crRNA-guided recognition—the first Acr to exploit a host “moonlighting” protein (*Nature Microbiology*, 2025; PMID: 41219509). Katz, Bondy-Denomy, Meeske, and colleagues made the startling discovery that phages encode their own viral Cas proteins that antagonize host CRISPR immunity, representing a fundamentally new anti-defense mechanism (*Nature*, 2024; PMID: 39232173).

The therapeutic potential of Acrs received two important demonstrations. Vera, Raines, and colleagues developed LFN-Acr/PA, the first protein-based Acr delivery platform using engineered anthrax toxin components to deliver Acrs at picomolar concentrations, inhibiting up to 95% of Cas9-mediated editing and increasing Cas9 specificity by 41% through temporal control (*PNAS*, 2025; PMID: 40758882). Paradoxically, AcrIIA5 was shown to enhance prime editing efficiency by up to 8.2-fold while simultaneously reducing unintended indels, demonstrating that an inhibitor protein can function as an editing enhancer (*Nature Communications*, 2025; doi: 10.1038/s41467-025-66237-2). AI-driven protein design entered the Acr field with de novo-designed artificial anti-CRISPRs (AIcrs) achieving potent, specific inhibition of Cas13a (*Nature Chemical Biology*, 2025; doi: 10.1038/s41589-025-02136-3).

## 10. RNA Editing and Mitochondrial Gene Editing Extend Beyond DNA

### ADAR-Based RNA Editing Achieves Clinical Proof-of-Mechanism

Endogenous ADAR (adenosine deaminase acting on RNA) recruitment strategies have advanced to clinical validation. Wave Life Sciences’ WVE-006, a GalNAc-conjugated editing oligonucleotide recruiting endogenous ADAR for A-to-I RNA editing, achieved durable plasma AAT levels of ~11 µM with over 60% functional wild-type M-AAT from a single subcutaneous dose in Phase 1b/2a trials for alpha-1 antitrypsin deficiency—the first proof-of-mechanism for therapeutic ADAR-based RNA editing in patients. Structural work by Xiang and colleagues elucidated ADAR1-RNA complex structures revealing substrate selection mechanisms relevant to therapeutic design (*Molecular Cell*, 2025).

A novel SPRING system using hairpin guide RNAs with blocking sequences enhanced both editing efficiency and specificity (*Molecular Therapy Nucleic Acids*, 2025). An engineered universal guide RNA scaffold from the U7 snRNA was demonstrated to boost editing efficiency from minimal AAV doses, particularly relevant for organs with limited AAV transduction (*Nature Communications*, 2025).

### Mitochondrial Base Editing Reaches Structural Maturity

Mitochondrial DNA editing—impossible through standard CRISPR systems due to the inability to import guide RNAs into mitochondria—relies on protein-only base editors targeted by TALE arrays. The foundational DdCBE (DddA-derived cytosine base editor) system, developed by Mok, Liu, and colleagues (*Nature*, 2020), enabled the first programmable C•G-to-T•A editing of mtDNA. TALED (transcription activator-like effector-linked deaminase), developed by Cho, Kim, and colleagues (*Cell*, 2022), added A-to-G capability by combining DddAtox with TadA8e adenosine deaminase.

In 2024–2025, mitoBEs using TALE-fused nickases enabled strand-selective editing with reduced off-target risk (*Nature Biotechnology*, 2024). Cryo-EM structures of DdCBE targeting native mitochondrial gene loci, published by Xiang and colleagues (*Molecular Cell*, 2025), enabled structure-guided engineering that narrowed the editing window to 2–3 nucleotides with near-background off-target levels. Enhanced DdCBE and TALED variants (DddA11-xAID and DddA6-TALED) achieved up to 25-fold improved editing at previously refractory sequence contexts. A comprehensive review of engineered mitochondria for therapeutic applications was published in *Signal Transduction and Targeted Therapy* (2025; doi: 10.1038/s41392-024-02081-y).

## 11. George Church’s Multiplex Vision Advances Toward the Clinic

George Church’s laboratory continues to push the boundaries of genome engineering scale, from single genes to whole genomes to entire species. The most clinically advanced program is xenotransplantation through eGenesis, built on Church’s landmark 2015 demonstration of CRISPR-Cas9 inactivation of all 62 porcine endogenous retroviruses in the pig genome (*Science*, 2015). In March 2024, Massachusetts General Hospital performed the first transplant of an eGenesis CRISPR-modified pig kidney into a human patient (Rick Slayman). A second recipient (Tim Andrews) survived 271 days. In September 2025, the FDA authorized a full clinical trial of gene-edited pig kidneys for end-stage kidney disease, with 30 additional patients planned. These organs carry approximately 70 genetic modifications including PERV inactivation, immune compatibility edits, and growth regulation changes.

Colossal Biosciences, co-founded by Church and Ben Lamm in 2021 for de-extinction research, raised $200 million in Series C funding at a $10.2 billion valuation in January 2025. The company created gene-edited “woolly mice” with mammoth-like traits (longer, golden, wavy fur) through simultaneous CRISPR editing of 7 genes (Chen et al., bioRxiv, 2025; doi: 10.1101/2025.03.03.641227). Additional programs include dire wolf de-extinction (three cloned, gene-edited pups born in 2025) and thylacine (Tasmanian tiger) restoration through acquired Melbourne laboratory resources.

Church’s foundational work on MAGE (Multiplex Automated Genome Engineering) continues to inform approaches for whole-genome recoding—the systematic replacement of codons to create organisms resistant to viral infection—with recent advances enabling up to 26,000 simultaneous edits using base editors to avoid cytotoxic DSBs.

## 12. Gene Drives Approach Field Testing for Malaria Control

CRISPR-based gene drives—selfish genetic elements that spread modifications through wild populations at super-Mendelian rates—have advanced from laboratory cage experiments to the threshold of field deployment. Li, Bier, and colleagues published a landmark study in *Nature* (2025; PMID: 40702179) demonstrating a protective FREP1 allele drive in *Anopheles stephensi* mosquitoes. A single amino acid change (L224→Q224) confers robust resistance to both *P. falciparum* and rodent malaria parasites with negligible fitness costs. A novel “allelic-drive” system spread Q224 from 25% to over 94% frequency in 10 generations, with the drive mechanism designed to self-eliminate, leaving only resistant populations.

In an extraordinary milestone, Habtewold, Christophides, and colleagues from the Transmission Zero consortium demonstrated that gene-drive-capable mosquitoes suppress patient-derived malaria in Tanzania—the first gene-drive mosquito study conducted in Africa by African scientists (*Nature*, 2026; doi: 10.1038/s41586-025-09685-6). Engineered *A. gambiae* expressing antimicrobial peptides inhibited *P. falciparum* development when tested against genetically diverse parasites from Tanzanian children. When crossed with gene-drive helper strains, the antimalarial trait was inherited by over 90% of offspring.

Biosafety research has kept pace: anti-CRISPR mosquito strains that prevent spread of population suppression drives were validated in large-cage trials (*Nature Communications*, 2024; doi: 10.1038/s41467-024-44907-x).

## 13. Homologous Recombination Enhancement Remains Critical for HDR-Dependent Applications

Despite the proliferation of DSB-free editing modalities, many therapeutic applications still require HDR for precise sequence changes. Enhancement strategies have matured considerably. Small molecule inhibitors of competing NHEJ pathways include NU7441 (DNA-PKcs inhibitor), SCR7 (Ligase IV inhibitor, increasing HDR up to 19-fold; Maruyama, Ploegh et al., *Nature Biotechnology*, 2015), and i53 (53BP1 inhibitor). Protein engineering approaches include Cas9-CtIP fusions that increase the HDR/NHEJ ratio 4.5–6-fold, and dominant-negative RNF168 fusions enhancing error-free editing 1.5–7-fold in primary human cells. A comprehensive 2025 review in the *International Journal of Molecular Sciences* detailed the current state of HDR enhancement including cell cycle synchronization strategies, donor template optimization, and the emerging use of AZD7648 (DNA-PKcs inhibitor) in the ChemiCATI system for efficient knock-in across multiple loci in mouse embryos.

## 14. The Regulatory Landscape Is Evolving as Fast as the Science

### The FDA’s “Plausible Mechanism” Framework Transforms Rare Disease Therapy

The most significant regulatory development of 2025–2026 was the FDA’s announcement on February 23, 2026 of a new pathway enabling approval of personalized gene editing therapies for rare diseases based on “plausible mechanism” rather than large clinical trials. First outlined in *NEJM* by FDA Commissioner Marty Makary and CBER Director Vinay Prasad (November 2025), this framework was inspired by the treatment of “Baby KJ” at Children’s Hospital of Philadelphia with a bespoke CRISPR therapy (Musunuru et al., *NEJM*, 2025). The pathway targets genome editing and RNA-based methods and could enable treatment of thousands of individually rare genetic conditions.

The FDA approved 8 novel cell and gene therapy products in 2024 and continued active review in 2025, with PDUFA dates scheduled through 2026 for multiple gene therapies including tabelecleucel, marnetegragene autotemcel, and DTX401. The EMA adopted a comprehensive guideline on quality, non-clinical, and clinical requirements for investigational ATMPs (EMA/CAT/22473/2025), effective July 2025.

### Access and Equity Present the Field’s Most Intractable Challenge

The cost barrier is stark: Casgevy is priced at $2.2 million, Lyfgenia at $3.1 million, and Lenmeldy (for metachromatic leukodystrophy) at $4.25 million. The CMS Cell and Gene Therapy Access Model, launched January 2025, represents the first systematic attempt to address Medicaid payment challenges for the estimated 50–60% of SCD patients covered by Medicaid. However, commercial viability remains uncertain: Pfizer discontinued Beqvez (hemophilia B gene therapy) in February 2025 due to zero patient uptake after approval. Multiple gene editing companies saw stock prices reach all-time lows in 2025, with Editas Medicine trading at $0.91 and Intellia declining to $5.90. Globally, most sickle cell disease patients live in Sub-Saharan Africa with essentially no access to gene therapies. Mastroleo and colleagues argued that affordable pricing of CRISPR treatments is a pressing ethical imperative (*The CRISPR Journal*, 2024; doi: 10.1089/crispr.2024.0042).

## 15. CRISPR Diagnostics Approach but Have Not Yet Achieved Routine Clinical Deployment

CRISPR-based diagnostic platforms—SHERLOCK (Cas13) and DETECTR (Cas12)—have demonstrated remarkable sensitivity and specificity for nucleic acid detection. Integration into portable devices, electrochemical biosensors, and lateral flow assays has been reviewed comprehensively (*Clinical and Experimental Medicine*, 2025; *Biosensors*, 2025). Kohabir and colleagues reviewed strategies for achieving single-nucleotide fidelity in CRISPR diagnostics (*Communications Medicine*, 2025; doi: 10.1038/s43856-025-00933-4). However, as of early 2026, no CRISPR diagnostic assay has achieved full FDA approval for routine clinical use beyond emergency contexts. Sherlock Biosciences (acquired by OraSure Technologies in 2024) has advanced FDA application submissions, and Sense Biodetection’s VerosCOVID-19 test achieved CE certification, but the regulatory gap between laboratory performance and clinically cleared products remains significant.

## Conclusion

The gene editing field of 2026 is qualitatively different from that of even three years ago. The convergence of four transformative trends—AI-designed editors, DSB-free precision chemistries, programmable large-DNA integration, and organ-targeted non-viral delivery—is creating a toolkit capable of addressing a far broader range of genetic diseases than any single technology could achieve alone.

Several findings from this review are particularly notable. First, the clinical durability of Casgevy through 5+ years of follow-up with 100% VOC-free rates establishes a benchmark that all subsequent gene editing therapies will be measured against. Second, the demonstration that base editing achieves zero chromosomal translocations in head-to-head comparison with Cas9 nuclease for CAR-T manufacturing provides a compelling safety argument for the transition away from DSB-based editing in cell therapy. Third, the evolution of CRISPR-associated transposases (evoCAST) to 10–30% integration efficiency in human cells, combined with bridge recombinases achieving megabase-scale rearrangements, suggests that the long-sought goal of routine, efficient, DSB-free large-DNA insertion is within reach. Fourth, the PERT system’s disease-agnostic approach to correcting nonsense mutations through suppressor tRNA installation could, in principle, address ~11% of all pathogenic mutations with a single editing strategy. Fifth, the INSTALL system’s solution to the lethal innate immune response against dsDNA donors fundamentally enables kilobase-scale non-viral genome writing in vivo.

Open questions remain abundant. The optimal balance between editing efficiency and safety for in vivo applications has not been established, as the Intellia ATTR clinical hold demonstrates. Whether epigenetic editing can achieve truly permanent gene silencing across all relevant cell types and developmental stages is unknown. The immunological consequences of repeated LNP-delivered gene editing—now demonstrated feasible through redosing—require long-term evaluation. The ecological consequences of releasing gene-drive mosquitoes, despite encouraging cage trials and anti-drive safeguards, present irreversible risks that demand extraordinary caution.

The regulatory and economic landscape may prove as challenging as the science. The FDA’s plausible mechanism pathway represents the most progressive regulatory innovation for genetic medicines, but its implementation will test the agency’s capacity for individualized risk assessment. Gene therapy pricing models are unsustainable for global health impact, and the field must develop solutions—outcomes-based contracts, managed entry agreements, technology transfer to endemic regions—or risk creating a two-tier world of genomic medicine.

What is clear is that gene editing has permanently altered the trajectory of medicine. The question is no longer whether we can rewrite the human genome with precision—but whether we can do so safely, equitably, and wisely at scale.

-----

## References

Adams, D., Gutstein, D. E., Manvelian, G., et al. (2025). Nexiguran ziclumeran in transthyretin amyloidosis polyneuropathy. *New England Journal of Medicine*. doi: 10.1056/NEJMoa2510209

Anzalone, A. V., Liu, D. R., et al. (2022). Twin prime editing. *Nature Biotechnology*. PMID: 34887556

Bell, C., Crossley, M., Weiss, M. J., et al. (2025). Epigenetic editing of fetal globin genes for sickle cell disease. *Nature Communications*. doi: 10.1038/s41467-025-62177-z

Buffington, S. A., Finkelstein, I. J., et al. (2025). Metagenomic screening of retron reverse transcriptases for mammalian cell editing. *Nature Biotechnology*. doi: 10.1038/s41587-025-02879-3

Charlesworth, C. T., & Porteus, M. H. (2019). Pre-existing adaptive immunity to Cas9 in humans. *Nature Medicine*. PMID: 30692695

Chauhan, V. P., Sharp, P. A., & Langer, R. (2025). Prime editors with reduced unintended mutations. *Nature*. doi: 10.1038/s41586-025-09537-3

Chen, J., Li, J., et al. (2024). Engineered R2Tg retrotransposon for all-RNA delivery. *Cell*. doi: 10.1016/j.cell.2024.06.049

Chen, S., et al. (2025). Gene-edited woolly mice with mammoth-like traits. *bioRxiv*. doi: 10.1101/2025.03.03.641227

Chiesa, R., Qasim, W., et al. (2026). BE-CAR7 base-edited allogeneic CAR-T cells for T-ALL. *New England Journal of Medicine*. PMID: 41363805. doi: 10.1056/NEJMoa2505478

Cho, S. I., Kim, J. S., et al. (2022). TALED for mitochondrial A-to-G editing. *Cell*.

Cohn, D. M., Longhurst, H. J., et al. (2025). Lonvoguran ziclumeran for hereditary angioedema. *New England Journal of Medicine*. PMID: 39445704

Conley, J. M., Robinson, W. M., Wilson, R. F., et al. (2025). Global regulatory landscape for heritable genome editing. *Journal of Community Genetics*. doi: 10.1007/s12687-025-00809-z

Edmonds, R., Zhang, F., et al. (2025). Compact all-RNA R2 system for human cell editing. *Nature Communications*. doi: 10.1038/s41467-025-61321-z

Engel, M., June, C. H., et al. (2025). Adenine base editing versus Cas9 for allogeneic CAR-T manufacturing. *PNAS*. PMID: 40324075

Faure, G., Saito, M., Wilkinson, M. E., et al. (2025). TIGR-Tas RNA-guided DNA-targeting systems. *Science*. doi: 10.1126/science.adv9789. PMID: 40014690

Fell, G., Abudayyeh, O. O., Gootenberg, J. S., et al. (2025). STITCHR: programmable gene insertion via R2 retrotransposons. *Nature*. PMID: 40205048. doi: 10.1038/s41586-025-08877-4

Fine, E. J., Altshuler, D., et al. (2024). Off-target analysis of Casgevy. *New England Journal of Medicine*. doi: 10.1056/NEJMc2313119

Fontana, L., Gutstein, D. E., Gillmore, J. D., et al. (2024). Nexiguran ziclumeran for ATTR cardiomyopathy. *New England Journal of Medicine*. doi: 10.1056/NEJMoa2412309

Frangoul, H., Grupp, S. A., et al. (2024). Casgevy Phase 3 results for sickle cell disease. *New England Journal of Medicine*. PMID: 38661449

Gelsinger, D. R., Sternberg, S. H., Wang, H. H., et al. (2025). In vivo metagenomic editing of commensal bacteria via CASTs. *Science*.

Goudy, L., Gilbert, L. A., et al. (2025). All-RNA CRISPRoff for primary T cells. *Nature Biotechnology*. doi: 10.1038/s41587-025-02856-w

Habtewold, T., Christophides, G. K., et al. (2026). Gene-drive mosquitoes suppress malaria in Tanzania. *Nature*. doi: 10.1038/s41586-025-09685-6

Hiraizumi, M., Nishimasu, H., et al. (2024). Structural characterization of bridge recombinases. *Nature*. PMID: 38926616

Hsu, P. D., et al. (2024). Bridge recombinases from IS110 insertion sequences. *Nature*. PMID: 38926615

International Coalition (2025). Call for 10-year moratorium on heritable human genome editing. *Cytotherapy*.

Johnson, M. C., Terns, M. P., et al. (2025). AcrIIIA2 anti-CRISPR exploiting host enolase. *Nature Microbiology*. PMID: 41219509

Katz, L., Bondy-Denomy, J., Meeske, A. J., et al. (2024). Phage-encoded viral Cas proteins antagonize host CRISPR immunity. *Nature*. PMID: 39232173

Khajanchi, N., & Saha, K. (2025). Cas9-degron system for temporal control of editing. *Molecular Therapy*.

Kohabir, K. A., et al. (2025). Single-nucleotide fidelity in CRISPR diagnostics. *Communications Medicine*. doi: 10.1038/s43856-025-00933-4

Laffin, L. J., Nissen, S. E., et al. (2025). CTX310 in vivo CRISPR for cardiovascular disease. *New England Journal of Medicine*. PMID: 41211945. doi: 10.1056/NEJMoa2511778

Lampe, G. D., Sternberg, S. H., et al. (2025). Structural analysis of type I-F CASTs. *Nature Communications*.

Lazzarotto, C. R., Tsai, S. Q., et al. (2026). CHANGE-seq-BE for base editor off-target profiling. *Nature Biotechnology*. PMID: 41482541

Leibowitz, M. L., Pellman, D., et al. (2021). Chromothripsis from CRISPR-Cas9 editing. *Nature Genetics*. PMID: 33846636

Li, M., Bier, E., et al. (2025). FREP1 allele drive in *Anopheles stephensi* for malaria resistance. *Nature*. PMID: 40702179

Ling, S., et al. (2025). RIDE: reconfigurable VLP-mediated delivery. *Nature Nanotechnology*.

Locatelli, F., Grupp, S. A., et al. (2024). Casgevy for transfusion-dependent beta-thalassemia. *New England Journal of Medicine*. doi: 10.1056/NEJMoa2309673

Lou, E., Moriarity, B. S., et al. (2025). CISH-knockout TILs for metastatic colorectal cancer. *Lancet Oncology*. PMID: 40315882

Makarova, K. S., Wolf, Y. I., et al. (2025). Updated evolutionary classification of CRISPR-Cas systems. *Nature Microbiology*. doi: 10.1038/s41564-025-02180-8

Maruyama, T., Ploegh, H. L., et al. (2015). SCR7 increases HDR efficiency. *Nature Biotechnology*.

Mastroleo, I., et al. (2024). Affordable pricing of CRISPR treatments as ethical imperative. *The CRISPR Journal*. doi: 10.1089/crispr.2024.0042

Mok, B. Y., Liu, D. R., et al. (2020). DdCBE for mitochondrial base editing. *Nature*.

Musunuru, K., et al. (2025). Bespoke CRISPR therapy for Baby KJ. *New England Journal of Medicine*.

Nagahata, T., et al. (2025). Cryo-EM structures of RNA-guided nucleases from IscB to Cas9. *Nature Structural & Molecular Biology*. doi: 10.1038/s41594-025-01743-x

Nisanov, M., Schaffer, D. V., et al. (2025). AAV capsid engineering approaches. *Molecular Therapy*. PMID: 40176349

Nitsch, S., et al. (2025). Immunogenicity of CRISPR-Cas systems. *Molecular Therapy*.

Pandey, S., Liu, D. R., et al. (2025). eePASSIGE with PACE-evolved Bxb1 variants. *Nature Biomedical Engineering*. doi: 10.1038/s41551-024-01227-1

Papathanasiou, S., Jaenisch, R., Pellman, D., et al. (2021). Chromosome loss after CRISPR editing in mouse embryos. *Nature Communications*.

Park, J., Kim, J. S., et al. (2025). eCas12f1 enhanced Cas12f variant. *Nature Communications*. doi: 10.1038/s41467-025-56048-w

Pennesi, M. E., Pierce, E. A., et al. (2024). BRILLIANCE trial for EDIT-101 in retinal degeneration. *New England Journal of Medicine*. doi: 10.1056/NEJMoa2309915

Perry, N. T., Hsu, P. D., et al. (2025). ISCro4 bridge recombinase in human cells. *Science*. PMID: 41642947. doi: 10.1126/science.adz1884

Pierce, J. B., Liu, D. R., et al. (2025). PERT: prime editing-mediated readthrough of premature termination codons. *Nature*. doi: 10.1038/s41586-025-09732-2

Qu, J., Huang, Y., et al. (2026). CRISPR-GPT: LLM agent for CRISPR experiment design. *Nature Biomedical Engineering*. doi: 10.1038/s41551-025-01463-z

Raghavan, A., Zhang, F., et al. (2025). Redi nucleases with reduced immunogenicity. *Nature Communications*. doi: 10.1038/s41467-024-55522-1

Ruffolo, J. A., Nayfach, S., et al. (2025). OpenCRISPR-1: AI-designed gene editor. *Nature*. PMID: 40739342. doi: 10.1038/s41586-025-09298-z

Thawani, A., Collins, K., et al. (2025). Cryo-EM of R2 retrotransposon mechanism. *Science Advances*. PMID: 40540573

Tou, C. J., Kleinstiver, B. P., et al. (2026). INSTALL for large DNA integration in vivo. *Nature*. doi: 10.1038/s41586-026-10241-z

Vakulskas, C. A., et al. (2018). HiFi Cas9 variant. *Nature Medicine*. PMID: 30082871

Vera, M. K., Raines, R. T., et al. (2025). LFN-Acr/PA protein-based anti-CRISPR delivery. *PNAS*. PMID: 40758882

Witte, I. P., Lampe, G. D., Sternberg, S. H., & Liu, D. R. (2025). evoCAST with 200-fold improved integration. *Science*. PMID: 40373119. doi: 10.1126/science.adt5199

Xiang, J., et al. (2025). Cryo-EM structures of DdCBE on mitochondrial loci. *Molecular Cell*.

Zhang, F., et al. (2025). OMEGAoff compact epigenetic repressor. *Nature Biotechnology*. PMID: 40335752. doi: 10.1038/s41587-025-02655-3

Zhang, Y., Collins, K., et al. (2025). Avian A-clade R2 proteins for transgene insertion. *Nature Biotechnology*.

Zilberzwige-Tal, S., Altae-Tran, H., et al. (2025). RNA-targeting CRISPR from toxin-antitoxin modules. *Cell*. doi: 10.1016/j.cell.2025.01.034
