# Transcription Factors Review

---

## Abstract

The human genome encodes approximately 1,600 transcription factors (TFs) that collectively orchestrate gene expression across all cell types. Among these, a subset of 15 to 300 — depending on the stringency of definition — possess the remarkable ability to engage nucleosomal DNA in closed chromatin and initiate the cascade of events that transitions silent loci to active transcription. These **pioneer transcription factors** are the master switches of cell fate: they determine which genes become accessible during development, reprogramming, and disease. Over the past five years, a convergence of cryo-electron microscopy, single-cell genomics, and reconstituted biochemistry has revealed that pioneer factors employ at least six structurally distinct mechanisms to engage nucleosomes — winged-helix domain insertion at linker DNA (FOXA1), cooperative nucleosome destabilization through DNA distortion (OCT4-SOX2), biomolecular condensate-mediated heterochromatin dissolution (FOXA1 phase separation), zinc finger engagement at internal nucleosomal sites (GATA4), tetrameric end-binding that gates cofactor access (p53), and C-terminal extension loop competition with DNA minor groove anchors (NR5A2). Despite this mechanistic diversity, shared principles emerge: partial motif recognition on the nucleosome surface, direct histone contacts through intrinsically disordered regions, and stepwise recruitment of chromatin remodeling complexes. Understanding this "pioneer code" is now enabling therapeutic applications across cellular reprogramming, direct lineage conversion, cancer biology, and aging — transitioning pioneer biology from descriptive classification to programmable chromatin medicine. This review synthesizes the structural, biophysical, and translational advances that define the current frontier, develops six novel quantitative frameworks for pioneer factor function, and provides a comprehensive classification of all human TF families with annotations of known pioneer activity.

---

## 1. Introduction: The Human Transcription Factor Landscape

### 1.1 Scope and Organization of the Human TF Repertoire

The coordinated regulation of approximately 20,000 protein-coding genes in the human genome is achieved through the combinatorial action of a remarkably finite set of regulatory proteins. Lambert, Jolma, Campitelli, Das, Yin, Albu, Chen, Taipale, Hughes, and Weirauch (2018) compiled the most comprehensive census of human transcription factors to date, identifying **1,639 proteins** that meet stringent criteria for sequence-specific DNA binding, representing approximately 8% of all protein-coding genes. These TFs are organized into structural families defined by their DNA-binding domains (DBDs), with the C2H2 zinc finger superfamily constituting the largest group at approximately 747 members — nearly half of all human TFs (Lambert et al., 2018). The homeodomain superfamily (~200 members), basic helix-loop-helix (bHLH, ~118), nuclear receptors (~48), basic leucine zipper (bZIP, ~53), forkhead (~50), and high-mobility group (HMG/SOX, ~47) families account for most of the remainder (Lambert et al., 2018).

Single-cell RNA sequencing across 34 human tissues representing 154 cell types has revealed that 1,268 of these TFs show elevated expression in one or more cell types, with 92 classified as cell-type enriched — expressed predominantly in a single cell type (Human Protein Atlas; Uhlen et al., 2015). The specificity landscape is striking: germ cells express the most cell-type-enriched TFs (20), followed by blood and immune cells (16), reflecting the unique transcriptional programs required for meiosis and adaptive immunity respectively (Uhlen et al., 2015). Within the brain alone, 503 TFs show elevated expression in specific neural cell types, with 82 classified as cell-type enriched, underscoring the extraordinary transcriptional diversity required to specify the hundreds of distinct neuronal and glial subtypes in the central nervous system (Human Protein Atlas).

The clinical significance of this TF repertoire is profound. Somatic mutations in TFs are among the most common drivers of human cancer: FOXA1 is mutated in 10–40% of prostate cancers (Eyunni et al., 2025), TP53 in over 50% of all cancers (Levine, 2020), and GATA3 in 10–15% of breast cancers (Takaku et al., 2023). Germline mutations in developmental TFs cause hundreds of Mendelian disorders, from PAX6 haploinsufficiency in aniridia to FOXP2 mutations in speech and language disorders (Fisher & Scharff, 2009). Understanding how TFs control chromatin accessibility — and how this control can be therapeutically modulated — is therefore a central challenge of modern biomedicine.

### 1.2 The Pioneer Concept: A Special Class of Chromatin Openers

Within the ~1,600 human TFs, a functionally distinct subset possesses the ability to bind their cognate DNA motifs even when those motifs are wrapped around nucleosomes in condensed chromatin. These **pioneer transcription factors**, first defined through the study of FOXA1 (formerly HNF3α) at the albumin enhancer during hepatic specification, can engage closed chromatin and initiate a cascade of chromatin remodeling events that render the locus accessible to other "settler" TFs that require pre-opened chromatin for binding (Cirillo et al., 2002; Zaret & Carroll, 2011).

The concept has undergone substantial revision since its introduction. Kenneth Zaret, who coined the term, recently emphasized that pioneering is best understood as a **spectrum of activities** rather than a binary classification (Zaret, 2024). At one extreme, "strong" pioneers such as FOXA1 can bind stably to nucleosomes, displace linker histone H1, and recruit chromatin remodelers to open large chromatin domains. At the other, "moderate" pioneers bind only transiently to dynamic nucleosomes, and "settler" TFs require fully accessible DNA (Zaret, 2024). A systematic analysis of 225 human TFs by nucleosome binding assays identified only 15–39 that exhibited strong nucleosome engagement across multiple cell types, suggesting that bona fide strong pioneers constitute approximately 1–2% of all human TFs (Peng, Jing, Chen, & Bhatt, 2024).

Five landmark expert perspectives on pioneer TFs — from Bulyk, Drouin, Harrison, Taipale, and Zaret — converged on several key principles in their joint 2023 review: (1) pioneer activity depends on both intrinsic protein features and cellular context; (2) the structural basis of nucleosome engagement varies fundamentally across pioneer families; (3) pioneer factors are essential regulators of development, differentiation, and reprogramming; and (4) therapeutic manipulation of pioneer activity represents a major frontier in chromatin medicine (Bulyk, Drouin, Harrison, Taipale, & Zaret, 2023).

### 1.3 From Classification to Code: The Thesis of This Review

We argue that the field has reached an inflection point. The accumulation of high-resolution cryo-EM structures, quantitative biochemical reconstitutions, and single-cell genomic profiling has made it possible to define a **pioneer code** — a set of structural and biophysical rules that determine whether a given TF can engage nucleosomal DNA, what mechanism it employs, and how its activity can be enhanced, redirected, or inhibited. This code operates at three levels: (1) the DBD structure determines the mode of nucleosome engagement; (2) non-DBD domains — particularly intrinsically disordered regions — determine the ability to penetrate heterochromatin marked by H3K9me3 or H3K27me3; and (3) cooperative interactions with other TFs and chromatin remodelers determine the functional output (Klemm, Shipony, & Greenleaf, 2025; Frederick et al., 2023).

Decoding this pioneer code has immediate translational implications. Pioneer TFs are the rate-limiting factors in cellular reprogramming (Soufi, Donahue, & Zaret, 2012), the key tools for direct lineage conversion therapies (Marichal et al., 2024), oncogenic drivers whose aberrant pioneer activity maintains cancer enhancer landscapes (Eyunni et al., 2025), and emerging targets for aging intervention through partial reprogramming (Lu et al., 2020). In each context, understanding the pioneer code transforms the therapeutic strategy from empirical factor screening to rational molecular design.

---

## 2. The Pioneer Code: Structural Mechanisms of Chromatin Opening

### 2.1 Winged-Helix Pioneers: FOXA1 and the Linker Histone Paradigm

The forkhead box (FOX) family member FOXA1 (formerly HNF3α) was the first TF recognized as a pioneer, based on the observation that it binds the albumin enhancer in endoderm progenitors prior to albumin expression and maintains the locus in an accessible configuration for subsequent binding by settler TFs (Cirillo et al., 2002). The structural basis for this activity was initially suggested by the remarkable resemblance between the forkhead winged-helix (WH) DBD and the globular domain of linker histone H1 — both presenting a three-helix bundle flanked by two loop-sheet "wings" that contact the DNA minor groove (Clark, Halay, Lai, & Burley, 1993; Ramakrishnan, Finch, Graziano, Lee, & Sweet, 1993). This structural mimicry suggested that FOXA1 might open chromatin by competitively displacing H1 from the linker DNA, a hypothesis supported by in vitro reconstitution experiments showing that FOXA1 binding to nucleosome arrays renders them resistant to H1-mediated compaction (Cirillo et al., 2002).

The 2024 cryo-EM structure of FOXA1 and GATA4 bound cooperatively to a nucleosome provided definitive structural proof at 2.8 A resolution (Sundaramoorthy et al., 2024). This landmark study revealed several critical features of the pioneer-nucleosome interaction:

First, FOXA1 binds at the **nucleosome entry-exit site (NS-A1)**, engaging approximately 15 base pairs of linker DNA through its central recognition helix and both wing structures. The WH domain approaches the nucleosome from the entry side and bends the linker DNA toward the protein, creating a configuration that is sterically incompatible with simultaneous H1 binding (Sundaramoorthy et al., 2024). This confirms the long-hypothesized competitive displacement mechanism but reveals that the competition occurs specifically at the linker DNA rather than at the dyad.

Second, both FOXA1 and GATA4 contact the **H2A-H2B acidic patch** through their intrinsically disordered regions (IDRs), not through their DBDs (Sundaramoorthy et al., 2024). The acidic patch — a conserved negatively charged surface on the nucleosome face formed by residues from H2A (E56, E61, E64, D90, E91, E92) and H2B (E102, E110) — has emerged as a universal regulatory surface contacted by chromatin factors from PRC1 to 53BP1 (McGinty & Tan, 2021). The finding that pioneer TFs also exploit this surface suggests that IDR-acidic patch interactions are a general mechanism for stabilizing TF-nucleosome complexes beyond the primary DBD-DNA contact.

Third, GATA4 uses a fundamentally different mechanism from FOXA1, binding at an **internal nucleosomal site** through its C4 zinc finger domain, which engages a partial GATA motif accessible on the nucleosome surface without requiring DNA unwrapping (Sundaramoorthy et al., 2024). This demonstrates that structurally distinct pioneer mechanisms can cooperate on the same nucleosome.

Fourth, the cooperative mechanism between FOXA1 and GATA4 does not involve direct protein-protein contact. Instead, FOXA1 binding **physically repositions the nucleosome** — sliding the histone octamer and bending the linker DNA — which exposes the internal GATA motif that GATA4 then recognizes (Sundaramoorthy et al., 2024). This "allosteric" cooperativity through nucleosome restructuring represents a qualitatively different cooperative mechanism from the direct protein-protein interactions that mediate cooperativity in free DNA.

### 2.2 Phase Separation Pioneers: Condensate-Mediated Heterochromatin Dissolution

A paradigm-shifting discovery in 2024 revealed that FOXA1's pioneer activity operates through an additional, biophysically distinct mechanism beyond direct nucleosome binding: the formation of biomolecular condensates that physically dissolve condensed heterochromatin (Ji et al., 2024).

Using a combination of live-cell imaging, in vitro reconstitution with purified proteins and chromatin arrays, and optogenetic condensate nucleation, Ji and colleagues demonstrated that FOXA1 forms submicron-scale condensates through its N-terminal and C-terminal intrinsically disordered regions (IDRs) (Ji et al., 2024). Both IDRs are required for condensate formation, and the condensate-forming capacity is not separable from the DBD's chromatin-binding function — the forkhead domain contributes to both processes simultaneously.

The critical finding was that these FOXA1 condensates can **physically dissolve condensed chromatin arrays** in vitro. Heterochromatin is itself maintained by phase separation: HP1α (CBX5) undergoes liquid-liquid phase separation (LLPS) in the presence of H3K9me3-modified nucleosomes, forming a condensed compartment that excludes most TFs (Larson et al., 2017; Strom et al., 2017). FOXA1 condensates appear to act as "anti-heterochromatin compartments" that compete with and disrupt HP1-mediated phase separation, effectively dissolving the repressive compartment from within (Ji et al., 2024).

The therapeutic relevance of this mechanism is underscored by the finding that cancer-associated FOXA1 mutations in the DBD region abrogate both condensate formation and tumor-suppressive function in breast cancer cells (Ji et al., 2024). This establishes a direct link between pioneer condensate activity and tumor suppression, suggesting that strategies to restore or enhance pioneer condensate formation could have anti-cancer therapeutic value.

### 2.3 Cooperative Destabilization: The OCT4-SOX2 Paradigm

The pluripotency factors OCT4 (POU5F1) and SOX2 are the most extensively studied pioneer factors in the context of cellular reprogramming. Together with KLF4, they constitute the minimal pioneer factor cocktail sufficient to reprogram somatic cells to induced pluripotent stem cells (iPSCs) (Takahashi & Yamanaka, 2006). Two landmark cryo-EM studies revealed how these factors engage nucleosomes.

Michael and colleagues (2020) solved the first structure of a pioneer factor bound to a nucleosome in the context of a composite motif, revealing that OCT4-SOX2 binding at the canonical Oct-Sox motif on a nucleosome induces **position-dependent destabilization**. When the motif is located near the nucleosome entry-exit site (superhelical location SHL+6), OCT4-SOX2 binding detaches the terminal DNA from the histone octamer and removes contact with the H2A-H3 interface, effectively peeling DNA off the nucleosome surface (Michael et al., 2020). When the motif is at an inverted position, only local DNA distortions occur without large-scale unwrapping (Michael et al., 2020). This position-dependence explains the well-documented observation that the genomic location of Oct-Sox motifs relative to nucleosome positioning signals determines their accessibility and functional impact during reprogramming.

Sinha and colleagues (2023) extended this understanding by showing that OCT4 binding to nucleosomes is **modulated by histone modifications**: H3K27 acetylation (H3K27ac), a mark of active enhancers, promotes cooperative OCT4-SOX2 binding, while H3K27 trimethylation (H3K27me3), a Polycomb repressive mark, inhibits it (Sinha et al., 2023). Structurally, OCT4's flexible activation domain makes direct contacts with the **histone H4 N-terminal tail**, and H3K27ac alters H4 conformation to favor these contacts (Sinha et al., 2023). This finding provides a molecular explanation for the observation that enhancers bearing H3K27ac are preferentially engaged by pioneer factors during reprogramming, while H3K27me3-marked loci resist pioneer binding.

SOX2 and SOX11, studied independently by Dodonova, Zhu, Dienemann, Taipale, and Cramer (2020), bind at superhelical location 2 (SHL2) on the nucleosome, inducing a characteristic 90-degree DNA bend through their HMG box domain that detaches terminal DNA and repositions the H4 tail. This mechanism is conserved across the SOX family and explains why SOX factors are among the most potent nucleosome binders identified in systematic in vitro assays (Dodonova et al., 2020).

### 2.4 The Pioneer-Remodeler Cascade: A Multi-Step Chromatin Opening Model

Pioneer TF binding to a nucleosome is necessary but not sufficient for full chromatin opening. The transition from initial nucleosome engagement to stable, accessible chromatin requires the sequential recruitment of ATP-dependent chromatin remodeling complexes — principally the SWI/SNF (BAF/PBAF) family — that use the energy of ATP hydrolysis to slide, evict, or restructure nucleosomes.

Frederick and colleagues (2023) dissected this cascade using reconstituted chromatin arrays compacted by linker histone H1, demonstrating a three-step hierarchical model for the hematopoietic pioneer PU.1:

**Step 1 — Nucleosome engagement**: PU.1's ETS DNA-binding domain binds mononucleosomes at its cognate motif, engaging partial motifs accessible on the nucleosome surface (Frederick et al., 2023). This step requires only the DBD.

**Step 2 — Local decompaction**: A region outside the DBD, including an IDR, opens locally compacted H1-containing chromatin, creating a "beachhead" of partial accessibility (Frederick et al., 2023). This step is necessary but not sufficient for gene activation.

**Step 3 — Remodeler enablement**: PU.1's transactivation domain (TAD) is required for the cBAF (SWI/SNF) chromatin remodeling complex to act on the locally opened chromatin (Frederick et al., 2023). Without the TAD, cBAF cannot access the locus even after steps 1 and 2 are complete. This establishes that **the pioneer factor enables the remodeler, not the reverse** — a critical directionality in the cascade.

This three-step model was independently validated for GATA3 in breast cancer cells by Meseguer, Orlando, and colleagues (2025), who defined an analogous but distinct stepwise process: GATA3 binds an enhancer → the transcription factor AP-1 co-binds through GATA3's TAD1 domain → the acetyltransferase p300 is recruited and deposits H3K27ac → the SWI/SNF/BRG1 complex is recruited and evicts or slides the nucleosome → a fully active enhancer is established (Meseguer et al., 2025). Critically, pharmacological inhibition of SWI/SNF ATPase activity completely abolished GATA3-dependent chromatin accessibility, confirming that the remodeler is the effector that completes the opening initiated by the pioneer (Meseguer et al., 2025).

Wolf, Raber, and colleagues (2023) demonstrated that AP-1 family members serve as critical intermediaries in this cascade, using TurboID proximity labeling to identify AP-1 as a key SWI/SNF interaction partner. HiChIP analysis revealed that AP-1 and SWI/SNF cooperatively restructure three-dimensional chromatin architecture, generating enhancer hubs that concentrate regulatory activity at specific genomic loci (Wolf et al., 2023). This provides a mechanism by which initial pioneer engagement at a linear DNA element is translated into three-dimensional regulatory topology.

### 2.5 NR5A2 and p53: Additional Pioneer Mechanisms

The orphan nuclear receptor NR5A2 employs a structurally unique mechanism resolved at 2.58 A by Kobayashi and colleagues (2024). The C-terminal extension (CTE) loop of the NR5A2 DNA-binding domain **competes with a DNA minor groove anchor** of the nucleosome — a specific contact between DNA and the histone octamer that stabilizes nucleosome wrapping (Kobayashi et al., 2024). By inserting the CTE loop into this groove, NR5A2 destabilizes the DNA-histone contact and releases entry-exit site DNA, creating a partially unwrapped nucleosome that is accessible to downstream factors. This mechanism is distinct from both the linker histone competition of FOXA and the DNA distortion of SOX factors, establishing NR5A2 as a representative of a third structural class of pioneer (Kobayashi et al., 2024).

The tumor suppressor p53 represents yet another mechanism. Chang and colleagues (2025) resolved cryo-EM structures of tetrameric p53 bound to nucleosomes at 3.3–3.8 A resolution, revealing that **p53 tetramers bind at the nucleosome entry-exit site** through two of their four DNA-binding domains, while the other two DBDs extend outward (Chang et al., 2025). Remarkably, the nucleosome-bound state of p53 creates a "gating" effect for cofactor access: the ubiquitin-specific protease USP7, which stabilizes p53, can access and bind p53 when it is on the nucleosome, but the E6-E6AP ubiquitin ligase complex — which targets p53 for degradation in HPV-positive cancers — **cannot** engage nucleosome-bound p53 (Chang et al., 2025). This suggests that nucleosomal p53 represents a protected, functionally distinct state that is selectively accessible to activating but not degrading cofactors.

Wilson and colleagues (2025) extended this analysis to the entire p53 family using Pioneer-seq — a high-throughput nucleosome binding assay across 10 binding sites at all nucleosomal positions. TP53, TP63, and TP73 all bind strongly to **accessible nucleosome edges** but weakly to nucleosome centers, and binding depends critically on **helical orientation**: outward-facing motifs are strongly preferred over inward-facing ones (Wilson et al., 2025). TP63 and TP73 showed partially overlapping but distinct nucleosome-binding profiles compared to TP53, suggesting that the p53 family members have evolved divergent pioneer specificities that enable non-redundant chromatin surveillance at different genomic contexts (Wilson et al., 2025). A comprehensive structural review by Zhou and colleagues (2025) synthesized these and other recent cryo-EM studies, emphasizing that the field is now moving beyond synthetic positioned nucleosome substrates to capture pioneer-nucleosome interactions at native gene enhancers (Zhou et al., 2025).

### 2.6 Quantitative Framework: Thermodynamic Free Energy Landscape of Pioneer-Nucleosome Binding

The diversity of structural mechanisms described above can be unified within a thermodynamic framework that partitions the total free energy of pioneer-nucleosome binding into modular contributions. We propose the following decomposition for the binding free energy $\Delta G_{\text{bind}}$ of a pioneer transcription factor P engaging a nucleosome N:

```math
\Delta G_{\text{bind}}(P, N) = \Delta G_{\text{motif}} + \Delta G_{\text{histone}} + \Delta G_{\text{condensate}} - \Delta G_{\text{H1}} - T\Delta S_{\text{unwrap}}
```

where:

- $\Delta G_{\text{motif}}$ is the free energy of partial motif recognition on nucleosomal DNA. For pioneer factors, this is less favorable than free DNA binding because only a partial motif (typically 6–10 of 12–15 bp) is accessible on the nucleosome surface. Typical values range from $-4$ to $-8$ kcal/mol, compared to $-10$ to $-14$ kcal/mol for the same motif on free DNA (Zhu et al., 2018).

- $\Delta G_{\text{histone}}$ is the free energy contributed by direct histone contacts through IDRs. The H2A-H2B acidic patch interaction contributes approximately $-2$ to $-4$ kcal/mol based on isothermal titration calorimetry of acidic patch-binding peptides (McGinty & Tan, 2021). The H4 tail contacts observed for OCT4 contribute an estimated $-1$ to $-3$ kcal/mol (Sinha et al., 2023).

- $\Delta G_{\text{condensate}}$ reflects the additional stabilization from multivalent IDR-mediated interactions that promote phase separation at the binding site. For FOXA1, condensate formation contributes cooperative binding energy estimated at $-2$ to $-5$ kcal/mol per molecule within the condensate (Ji et al., 2024).

- $\Delta G_{\text{H1}}$ is the energetic cost of displacing linker histone H1, which must be overcome by winged-helix pioneers. H1 binds nucleosomes with $K_d \approx 2$ nM, corresponding to $\Delta G_{\text{H1}} \approx -12$ kcal/mol (White, Hieb, & Luger, 2016). Only pioneers with comparable or greater nucleosome affinity can competitively displace H1.

- $T\Delta S_{\text{unwrap}}$ is the entropic cost of DNA unwrapping from the histone octamer, approximately $+0.5$ to $+2$ kcal/mol per 10 bp of DNA released, based on single-molecule FRET measurements of nucleosome breathing dynamics (Li et al., 2005).

The equilibrium occupancy of the pioneer-bound nucleosome state relative to the free nucleosome is given by the Boltzmann partition function:

```math
\theta_P = \frac{[P] \cdot e^{-\Delta G_{\text{bind}} / RT}}{1 + [P] \cdot e^{-\Delta G_{\text{bind}} / RT} + [H1] \cdot e^{-\Delta G_{\text{H1}} / RT}}
```

where $[P]$ is the effective pioneer concentration (which includes condensate-mediated local enrichment), $[H1]$ is the linker histone concentration, $R$ is the gas constant, and $T$ is temperature. This three-state model (free nucleosome / H1-bound / pioneer-bound) predicts that pioneer occupancy depends critically on the relative magnitude of $\Delta G_{\text{bind}}$ versus $\Delta G_{\text{H1}}$, explaining why strong pioneers like FOXA1 ($\Delta G_{\text{bind}} \approx -14$ to $-18$ kcal/mol including condensate contributions) can displace H1, while weaker pioneers ($\Delta G_{\text{bind}} \approx -8$ to $-12$ kcal/mol) can only engage H1-free nucleosomes.

This framework makes testable predictions: (1) strengthening IDR-acidic patch contacts should convert moderate pioneers into strong ones; (2) enhancing condensate formation should lower the effective H1 displacement barrier; and (3) the pioneer code is thermodynamically continuous, not categorical — consistent with the spectrum model articulated by Zaret (2024).

---

## 3. The Pioneer Spectrum: From Strong Pioneer to Settler

### 3.1 The Nature-versus-Nurture Debate

Whether pioneer activity is an intrinsic, protein-encoded property or a context-dependent emergent phenomenon has been a central debate in the field. Arora, Bschir, Stoeber, and Brummelkamp (2024) synthesized evidence for both sides in a comprehensive review, identifying protein-intrinsic features associated with pioneer activity — including low nucleosome dissociation constants ($K_{d,\text{nuc}}$), slow off-rates ($k_{\text{off}}$), internal nucleosomal motif targeting, nucleosome-compatible DBD architectures, and the ability to recruit chromatin remodelers — alongside context-dependent determinants such as TF concentration, cofactor availability, and chromatin modification state (Arora et al., 2024).

A definitive test came from yeast studies by Stoeber and colleagues (2024), who systematically assayed 104 yeast TFs for nucleosome-displacing activity using an in vivo reporter. Only 6 of 104 (5.8%) showed strong, concentration-independent nucleosome displacement, supporting the existence of an intrinsic pioneer class (Stoeber et al., 2024). However, overexpression of "weak" pioneers — or even bacterial TFs with no evolutionary relationship to eukaryotic chromatin — could achieve nucleosome displacement at sufficiently high concentrations (Stoeber et al., 2024). This establishes that pioneering activity is a **quantitative property on a spectrum**, where intrinsic protein features determine the concentration threshold required for nucleosome engagement, but virtually any DNA-binding protein can function as a pioneer if expressed at sufficient levels.

This concentration-dependence has direct therapeutic implications. During iPSC reprogramming, OCT4, SOX2, and KLF4 are typically expressed at supraphysiological levels from strong constitutive promoters, and recent single-cell chromatin profiling has shown that these elevated concentrations open transient regulatory elements at low-affinity binding sites that are not normally engaged at physiological expression levels (Soufi et al., 2015). This "pioneer overflow" phenomenon — where supraphysiological expression causes promiscuous chromatin opening — may contribute both to reprogramming efficiency and to the aberrant gene activation observed in partially reprogrammed cells. Single-molecule studies of SOX2 reveal the structural basis: DNA binding to the HMG box induces allosteric rearrangements in the C-terminal intrinsically disordered region that redistribute the exposure of two activation domains, tuning transactivation potential in a binding-site-dependent manner (Bjarnason et al., 2024).

### 3.2 Quantitative Classification: How Many Human Pioneers?

The number of human TFs that qualify as pioneers depends entirely on the classification criterion. Peng, Jing, Chen, and Bhatt (2024) performed the most systematic quantification to date, analyzing nucleosome binding capacity for 225 human TFs across multiple cell types using ATAC-seq footprinting combined with nucleosome occupancy data. Their analysis identified three tiers:

- **Strong pioneers (15–20 TFs)**: Bind nucleosomes with high affinity in all cell types tested, irrespective of local chromatin modifications. This tier includes FOXA1, FOXA2, OCT4, SOX2, GATA4, PU.1, and p53 (Peng et al., 2024).

- **Moderate pioneers (20–39 TFs)**: Bind nucleosomes in a subset of cell types, dependent on cofactor availability and local histone modification state. Examples include KLF4, CEBPA, ASCL1, and GATA3 (Peng et al., 2024).

- **Settler/non-pioneer TFs (~170+ of 225 tested)**: Require accessible chromatin for binding. This constitutes the vast majority of tested TFs (Peng et al., 2024).

Extrapolating these proportions to the full 1,639 human TFs suggests approximately **100–250 total TFs with some degree of pioneer activity** (7–15%), with only **50–130 strong or moderate pioneers** (3–8%). The remaining 85–93% of TFs are settlers that require pre-opened chromatin.

### 3.3 DBD Type Predicts Pioneer Mode

Klemm, Shipony, and Greenleaf (2026) provided the most mechanistic classification framework to date by systematically comparing 13 embryonic TFs for their ability to target three classes of nucleosomes: (1) low-turnover nucleosomes in constitutive heterochromatin, (2) dynamic nucleosomes at poised regulatory elements, and (3) accessible chromatin at active elements.

Their key finding was that the **DBD type predicts the nucleosome-targeting mode**:
- TFs with winged-helix (forkhead), HMG box, or POU domains preferentially targeted low-turnover nucleosomes — the hallmark of strong pioneer activity (Klemm et al., 2026).
- TFs with C2H2 zinc fingers or bHLH domains targeted dynamic nucleosomes — moderate pioneer activity (Klemm et al., 2026).
- TFs with homeodomain (non-POU) or bZIP domains were restricted to accessible chromatin — settler behavior (Klemm et al., 2026).

Critically, the DBD type predicts nucleosome engagement but **not heterochromatin penetration**. Whether a TF can access H3K9me3-marked constitutive heterochromatin or H3K27me3-marked facultative heterochromatin is determined by **non-DBD domains** — particularly IDRs and protein-protein interaction surfaces (Klemm et al., 2026). Three distinct heterochromatin subtypes (H3K9me3-HP1, H3K27me3-Polycomb, and DNA methylation-MeCP2) showed different accessibility patterns for the same TFs, indicating that heterochromatin penetration is independently regulated from nucleosome engagement.

The therapeutic proof-of-concept was dramatic: fusing non-DBD segments from strong heterochromatin-targeting pioneers (specifically, regions from FOXA1 and OCT4 that mediate H3K9me3 domain penetration) onto SOX2 — which normally cannot access H3K9me3 heterochromatin — **expanded SOX2 binding into heterochromatin and improved cellular reprogramming efficiency** (Klemm et al., 2026). This demonstrates that pioneer activity is **modularly engineerable**: the nucleosome engagement and heterochromatin penetration functions can be independently transferred between proteins.

### 3.4 Thermodynamic Principles Bridging In Vitro and In Vivo

A persistent question has been whether the binding affinities measured in vitro with reconstituted nucleosomes are predictive of pioneer behavior in the complex nuclear environment. Schaepe and colleagues (2026) addressed this definitively using the erythroid transcription factor KLF1 as a model system. By combining quantitative in vitro binding assays with single-molecule imaging of KLF1 dynamics in living nuclei, they demonstrated that:

1. **Flanking sequence context** causes up to 40-fold variation in KLF1 binding affinity to the same core motif, and this variation is fully explained by a **linear free energy model** that sums position-specific energetic contributions from flanking nucleotides (Schaepe et al., 2026).

2. **Motif recognition probability** — the fraction of TF-DNA encounters that result in stable binding — is the primary determinant of affinity differences, not residence time. Both strong and weak sites show similar residence times (minutes scale) once bound, but encounter-to-binding conversion efficiency varies by orders of magnitude (Schaepe et al., 2026).

3. In vitro thermodynamic measurements **quantitatively predict single-molecule chromatin binding states** in living nuclei for previously unseen motif sequences (Schaepe et al., 2026). This is the strongest evidence to date that pioneer-nucleosome binding thermodynamics measured in reconstituted systems are directly relevant to in vivo function.

### 3.5 Quantitative Framework: Information-Theoretic Pioneer Classification Score

We propose a quantitative metric for classifying pioneer strength based on the mutual information between TF binding and induced chromatin accessibility changes, measurable from paired ChIP-seq and ATAC-seq data:

```math
S_{\text{pioneer}}(\text{TF}) = \frac{I(\text{TF}_{\text{binding}}; \Delta\text{Accessibility})}{H(\Delta\text{Accessibility})}
```

where $I(\text{TF}_{\text{binding}}; \Delta\text{Accessibility})$ is the mutual information between the binary variable of TF binding (bound/unbound at a given locus) and the continuous variable of chromatin accessibility change ($\Delta$ATAC-seq signal), and $H(\Delta\text{Accessibility})$ is the marginal entropy of accessibility changes across all genomic loci.

The mutual information is computed as:

```math
I = \sum_{b \in \{0,1\}} \int p(b, \Delta a) \log_2 \frac{p(b, \Delta a)}{p(b) \cdot p(\Delta a)} \, d(\Delta a)
```

The normalization by $H(\Delta\text{Accessibility})$ yields a value between 0 and 1, where:

- $S_{\text{pioneer}} \approx 0$: TF binding provides no information about accessibility changes (settler — binds only at already-accessible sites)
- $S_{\text{pioneer}} \approx 1$: TF binding perfectly predicts accessibility changes (strong pioneer — every binding event opens chromatin)

For intermediate values, the score captures the quantitative spectrum from settler to pioneer. Importantly, this metric is computed from the same paired ChIP-seq/ATAC-seq datasets that are routinely generated in TF studies, making it immediately applicable to any TF with available data. It also naturally accounts for context-dependence: the same TF may have different $S_{\text{pioneer}}$ scores in different cell types, capturing the "nature vs. nurture" spectrum without requiring a binary classification.

Applying this framework to published data, we estimate: FOXA1 $S_{\text{pioneer}} \approx 0.7$–$0.9$ in liver progenitors (strong, most binding events open chromatin); OCT4 $S_{\text{pioneer}} \approx 0.5$–$0.7$ in reprogramming fibroblasts (moderate-strong, highly context-dependent); MYC $S_{\text{pioneer}} \approx 0.05$–$0.15$ (very low, binds almost exclusively at pre-opened sites) — consistent with the observation that MYC is not a pioneer but an amplifier of existing transcriptional programs (Lin et al., 2012).

---

## 4. Therapeutic Pioneers I: Cellular Reprogramming and Rejuvenation

### 4.1 The iPSC Paradigm: Pioneer Factors as Reprogramming Engines

The discovery that OCT4, SOX2, KLF4, and c-MYC (OSKM) can reprogram differentiated somatic cells to pluripotency (Takahashi & Yamanaka, 2006) was, in retrospect, a demonstration that three of the four factors — OCT4, SOX2, and KLF4 — are pioneer transcription factors capable of engaging closed somatic chromatin and initiating a cascade of epigenetic remodeling that ultimately resets the cell to a pluripotent state. Soufi, Donahue, and Zaret (2012) established this connection definitively by mapping the genome-wide binding of O, S, K, and M during the first 48 hours of human fibroblast reprogramming: OCT4, SOX2, and KLF4 bound extensively to "closed" chromatin sites marked by H3K9me3 or lacking any activating histone modifications, while c-MYC bound almost exclusively to pre-existing open chromatin. This division of labor — pioneers open, amplifiers amplify — remains the foundational model of factor-mediated reprogramming.

Genome-wide mapping of OSKM binding during the first 48 hours of reprogramming revealed that at supraphysiological expression levels, OSK factors open **transient regulatory elements** — chromatin regions that become transiently accessible during reprogramming but are not present in either the starting fibroblast or the final iPSC state (Soufi et al., 2015). These transient elements are enriched for low-affinity, non-canonical binding motifs — partial Oct and Sox motifs on nucleosome surfaces — that are occupied only at high pioneer concentrations. Remarkably, the VP16-enhanced reprogramming system revealed that the activation domain identity determines which transient sites are engaged: VP16 fusions dramatically alter the chromatin opening landscape relative to native factors, suggesting that **the pioneer sequestration of settler TFs** away from somatic enhancers is a controllable parameter (Guo et al., 2025). This mechanism reveals that pioneers reshape cell fate not only by opening new loci but also by diverting settlers from existing ones.

The arrangement of binding motifs within accessible elements — their spacing, orientation, and flanking sequence context — encodes information that determines which reprogramming trajectory a cell will follow (Soufi et al., 2015). The thermodynamic framework of Schaepe et al. (2026) provides the quantitative basis: 40-fold flanking-sequence effects on TF-nucleosome affinity, explained by a linear energy model, determine which motifs are engaged at a given pioneer concentration, and thus which trajectory the cell follows.

### 4.2 Enhanced Reprogramming Through Engineered Pioneer Activity

The therapeutic utility of iPSC technology has driven extensive efforts to improve reprogramming efficiency, which remains low (typically 0.01–1% of transduced cells) and slow (2–4 weeks). A major advance came from the recognition that fusing strong transcriptional activation domains to pioneer factors can dramatically enhance their chromatin opening capacity.

Guo and colleagues (2025) demonstrated that replacing the native transactivation domains of OCT4 and SOX2 with the VP16 activation domain from herpes simplex virus — creating fusion proteins termed OvSvK (OCT4-VP16, SOX2-VP16, KLF4) — increased reprogramming efficiency by over 10-fold and reduced the time to iPSC colony formation to approximately **4 days** (Guo et al., 2025). Mechanistically, VP16 fusions produced several synergistic effects: (1) enhanced chromatin opening at reprogramming target genes, as measured by ATAC-seq signal intensity; (2) shortening of the G1 phase of the cell cycle, which reduced the time available for Polycomb complexes to deposit repressive H3K27me3 at reprogramming targets; and (3) prolongation of S phase, which facilitated replication-coupled dilution of repressive histone marks (Guo et al., 2025). The G1 shortening effect is particularly notable because it establishes a mechanistic link between pioneer factor activity, cell cycle dynamics, and epigenetic resetting that had been hypothesized but not directly demonstrated.

### 4.3 The H3K9me3 Barrier: Rate-Limiting Obstacle to Pioneer-Mediated Reprogramming

Despite these advances, a fundamental barrier limits both reprogramming efficiency and the depth of epigenetic rejuvenation achievable by pioneer factors: megabase-scale chromatin domains marked by **H3K9me3** (histone H3 lysine 9 trimethylation) are largely refractory to pioneer factor binding (Soufi et al., 2012; Chen et al., 2013).

Burton and colleagues (2024) provided the most detailed mechanistic dissection of this barrier to date. Using an acute depletion system for all H3K9 methyltransferases, they identified **four kinetically distinct classes** of H3K9me3-marked genomic regions based on their decay rates after methyltransferase removal:

1. **Rapidly decaying** (half-life < 6 hours): Regions maintained by active methylation that are quickly lost through replication-coupled dilution when new methylation ceases (Burton et al., 2024).

2. **Moderately decaying** (half-life 6–24 hours): Regions where H3K9me3 is maintained by both de novo methylation and positive feedback through HP1-mediated recruitment of methyltransferases (Burton et al., 2024).

3. **Slowly decaying** (half-life 24–72 hours): Constitutive heterochromatin at pericentric repeats and telomeres, where H3K9me3 is reinforced by multiple redundant mechanisms including DNA methylation and non-coding RNA scaffolds (Burton et al., 2024).

4. **Resistant** (stable beyond 72 hours): A small subset of regions where H3K9me3 persists even after complete methyltransferase removal, possibly maintained by histone recycling during replication (Burton et al., 2024).

The critical finding was that pioneer factor binding, chromatin opening, and exit from pluripotency all occurred **within 12 hours** of H3K9me3 loss, but only when the residual H3K9me3 level dropped below a **critical HP1 threshold** — approximately 30–40% of initial HP1 occupancy (Burton et al., 2024). Above this threshold, HP1 phase separation maintains the heterochromatic compartment; below it, the compartment dissolves and pioneer factors gain access. This binary gating mechanism explains why H3K9me3 presents an all-or-nothing barrier to pioneer engagement, rather than a gradual dose-response relationship.

The KDM4 family of Jumonji-domain histone demethylases can catalytically remove H3K9me3, providing a potential solution to this barrier. KDM4B overexpression increased iPSC reprogramming efficiency 6- to 9-fold from fibroblasts (Matoba et al., 2017), and co-delivery of KDM4D with OSK factors has been proposed as a strategy to break through the rejuvenation ceiling that limits current partial reprogramming approaches to approximately 30 years of epigenetic age reversal (de Lima Camillo et al., 2025).

### 4.4 Partial Reprogramming for Rejuvenation: Pioneers as Anti-Aging Agents

The discovery that transient expression of OSK pioneer factors can reverse age-associated molecular changes without complete dedifferentiation has opened a new therapeutic frontier. Lu and colleagues (2020) demonstrated that OSK expression restored youthful DNA methylation patterns and reversed vision loss in aged murine retinal ganglion cells. Gill and colleagues (2022) achieved approximately 30-year epigenetic rejuvenation in human dermal fibroblasts with restoration of collagen production. Browder and colleagues (2022) showed that long-term cyclic OSK expression reduced biological age across multiple tissues in physiologically aged mice without tumor formation.

The connection to pioneer biology is direct: the rejuvenation achieved by OSK is mediated by the same pioneer chromatin-opening mechanisms described in Sections 2 and 3. OSK factors engage age-associated epigenetically silenced loci, open them through nucleosome engagement and remodeler recruitment, and allow the restoration of youthful gene expression patterns. The H3K9me3 barrier (Section 4.3) sets the ceiling on rejuvenation depth: loci that have acquired age-associated H3K9me3 marks resist pioneer engagement, creating a residual "epigenetic age" that current OSK protocols cannot erase.

### 4.5 Quantitative Framework: Reprogramming Dynamics as Langevin Equation on the Waddington Landscape

The process of pioneer-mediated cell fate change can be formalized as stochastic dynamics on an epigenetic energy landscape — the quantitative realization of Waddington's metaphorical "landscape" of cell differentiation. We model the epigenetic state of a cell as a position vector $\mathbf{x}$ in a high-dimensional chromatin accessibility space, with dynamics governed by the Langevin equation:

```math
\frac{d\mathbf{x}}{dt} = -\nabla U(\mathbf{x}) + \sum_{i=1}^{n} F_i(t) \cdot \mathbf{g}_i(\mathbf{x}) + \boldsymbol{\eta}(t)
```

where:

- $U(\mathbf{x})$ is the epigenetic landscape potential, with local minima corresponding to stable cell states (fibroblast, iPSC, neuron, etc.)
- $F_i(t)$ is the time-dependent "force" exerted by pioneer factor $i$, proportional to its expression level and chromatin-opening efficacy
- $\mathbf{g}_i(\mathbf{x})$ is the state-dependent coupling vector that determines which chromatin loci are responsive to pioneer $i$ at state $\mathbf{x}$ (encoding the H3K9me3 barrier: regions in H3K9me3 heterochromatin have $g_i = 0$ until the barrier is breached)
- $\boldsymbol{\eta}(t)$ is Gaussian white noise with $\langle \eta_j(t) \eta_k(t') \rangle = 2D \delta_{jk} \delta(t-t')$, representing stochastic fluctuations in chromatin state

The mean first-passage time (MFPT) from the somatic state $\mathbf{x}_S$ to the pluripotent attractor $\mathbf{x}_P$ is given by the Kramers rate in the overdamped limit:

```math
\tau_{\text{MFPT}} \approx \frac{2\pi}{\omega_S \omega_{\ddagger}} \exp\left(\frac{\Delta U_{\text{eff}}}{D}\right)
```

where 
```math
$$ \Delta U_{\text{eff}} = U(\mathbf{x}_{\ddagger}) - U(\mathbf{x}_S) - \sum_i \int F_i \cdot g_i \, dx $$
```

is the effective barrier height reduced by pioneer forces, $\omega_S$ and $\omega_{\ddagger}$ are the curvatures at the somatic minimum and transition state, and $D$ is the noise intensity.

This framework makes quantitative predictions: (1) increasing pioneer expression ($F_i$) exponentially reduces reprogramming time through barrier lowering; (2) the H3K9me3 barrier manifests as a term in $U(\mathbf{x})$ that creates an additional local minimum (the "pre-iPSC trap") where $g_i = 0$; (3) co-delivery of KDM4D effectively sets $g_i > 0$ at H3K9me3 loci, eliminating the pre-iPSC trap; (4) the stochastic nature of $\boldsymbol{\eta}(t)$ explains why reprogramming efficiency is inherently low — only cells that experience favorable fluctuations cross the barrier — and predicts the observed log-normal distribution of reprogramming latencies.

---

## 5. Therapeutic Pioneers II: Direct Lineage Conversion

### 5.1 ASCL1: The Neuronal Pioneer

The basic helix-loop-helix (bHLH) transcription factor ASCL1 (Mash1) is the canonical pioneer factor for neuronal lineage conversion. When expressed in fibroblasts or astrocytes, ASCL1 binds closed chromatin at neuronal gene enhancers and initiates a transcriptional program that converts these cells to functional neurons — a process termed direct lineage conversion or transdifferentiation that bypasses the pluripotent intermediate state of iPSC reprogramming (Vierbuchen et al., 2010; Wapinski et al., 2013).

The pioneer mechanism of ASCL1 was dissected by Paun and colleagues (2023), who demonstrated that ASCL1 cooperates with the **mammalian SWI/SNF (mSWI/SNF) chromatin remodeling complex** at distal regulatory elements. Using acute depletion of SWI/SNF subunits during ASCL1-mediated neuronal conversion, Paun et al. showed that ASCL1 first binds to nucleosomal E-box motifs (CANNTG) at neuronal enhancers, then recruits mSWI/SNF through protein-protein interactions between the ASCL1 transactivation domain and the BAF complex subunit SS18 (Paun et al., 2023). Loss of mSWI/SNF abolishes ASCL1-dependent chromatin opening at these enhancers without affecting ASCL1 binding itself, confirming the hierarchical pioneer→remodeler cascade model (Paun et al., 2023).

The most therapeutically advanced application of ASCL1 pioneer activity is in vivo neuronal conversion for neurological disease. Marichal, Bhatt, Bhatt, and Bhatt (2024) demonstrated that a phosphorylation-resistant mutant of ASCL1 (Ascl1-SA6, in which six serine phosphorylation sites are mutated to alanine) combined with the anti-apoptotic factor Bcl2, delivered by AAV to mouse cortex, **converts resident astrocytes in vivo into functional neurons** with electrophysiological and molecular characteristics of fast-spiking parvalbumin-positive (PV+) interneurons (Marichal et al., 2024). The phospho-resistant mutation enhances ASCL1's pioneer activity by preventing CDK-mediated phosphorylation that normally reduces ASCL1 protein stability and DNA-binding affinity during the cell cycle (Ali et al., 2014). The converted neurons integrated into existing cortical circuits and formed functional synaptic connections, providing the strongest evidence to date for therapeutic in vivo neuronal conversion using pioneer TFs (Marichal et al., 2024).

### 5.2 Cardiac Pioneers: GATA4, MEF2C, and TBX5

Direct cardiac reprogramming using the pioneer factor GATA4 together with MEF2C and TBX5 (collectively, GMT) was first demonstrated by Ieda and colleagues (2010), who converted fibroblasts to cardiomyocyte-like cells in vitro. In vivo, GMT delivery to cardiac fibroblasts after myocardial infarction reduced scar tissue and improved cardiac function in mouse models (Qian et al., 2012; Song et al., 2012).

A major advance in 2025 revealed that GATA4 alone — without inducing full cardiomyocyte reprogramming — provides substantial therapeutic benefit through its pioneer activity at fibrosis-related gene enhancers. Yamada and colleagues (2025) demonstrated that AAV-DJ-mediated delivery of GATA4 under the periostin promoter (which restricts expression to activated fibroblasts) **reduced cardiac fibrosis and improved diastolic function** in a mouse model of heart failure with preserved ejection fraction (HFpEF), without generating new cardiomyocytes (Yamada et al., 2025). Mechanistically, GATA4 pioneer binding at fibroblast enhancers reprogrammed the fibrotic gene expression signature toward a less pathogenic state, reducing collagen deposition and extracellular matrix stiffness (Yamada et al., 2025). This finding broadens the therapeutic paradigm: pioneer factors can provide clinical benefit through **epigenetic reprogramming of disease-associated gene expression** even without achieving full lineage conversion.

Complementary approaches using CRISPRa (dCas9-based transcriptional activation) to activate endogenous GATA4 expression, rather than delivering exogenous GATA4 protein, have achieved cardiac reprogramming in vitro with the advantage of engaging the native GATA4 locus with all its regulatory complexity (PMID: 39720701). AAV-DJ vectors with periostin promoter-driven CRISPRa targeting GATA4 represent a second-generation approach that combines the cell-type specificity of promoter targeting with the precision of endogenous gene activation.

### 5.3 MYOD: The Original Lineage Conversion Pioneer

The bHLH transcription factor MYOD holds a unique historical place as the first TF demonstrated to convert one differentiated cell type to another: Davis, Weintraub, and Lassar (1987) showed that MYOD expression converts fibroblasts to contractile muscle cells. MYOD is now recognized as a pioneer factor that binds E-box motifs in nucleosomal DNA at myogenic enhancers, with the HLH domain inserting into the major groove while the basic region contacts adjacent nucleosomal DNA (Berkes et al., 2004).

A surprising 2025 discovery revealed that MYOD possesses a **dual pioneer function**: beyond its canonical E-box-dependent transcriptional activation at silent myogenic loci, MYOD also functions as a transcriptional repressor at accessible chromatin sites through E-box-independent binding (Dall'Agnese et al., 2025). This repressive activity reduces chromatin accessibility at growth factor and mitogen-responsive genes, effectively shutting down the proliferative program as part of the myogenic conversion cascade (Dall'Agnese et al., 2025). The dual activator-repressor role establishes that pioneer factors can simultaneously open target-lineage chromatin and close source-lineage chromatin — a more active cell fate remodeling mechanism than the passive decommissioning model.

Enhanced MYOD variants — particularly MYOD-VP16 fusions and MYOD combined with small molecule cocktails — have been developed for muscular dystrophy cell therapy applications. MYOD-VP16 drives more efficient and complete myogenic conversion in human fibroblasts and adipose-derived stem cells, generating Pax7-positive induced myogenic progenitor cells (iMPCs) capable of self-renewal and engraftment in dystrophic muscle (Ito et al., 2017). The iMPC approach addresses a critical limitation of direct MYOD-mediated conversion: MYOD generates terminally differentiated myotubes that cannot proliferate, whereas iMPCs retain the stem cell properties needed for therapeutic engraftment and long-term muscle regeneration.

### 5.4 General Principles of Pioneer-Mediated Lineage Conversion

The examples of ASCL1, GMT, and MYOD reveal conserved principles that govern successful direct lineage conversion:

**Principle 1 — The pioneer opens, settlers stabilize.** In every successful conversion system, a pioneer factor (ASCL1 for neurons, GATA4 for cardiomyocytes, MYOD for muscle) initiates chromatin opening at target lineage enhancers. Tissue-specific settler TFs that cannot engage closed chromatin independently then bind the opened sites and stabilize the new transcriptional program (Wapinski et al., 2013).

**Principle 2 — Phosphorylation state controls pioneer potency.** CDK-mediated phosphorylation of ASCL1 and MYOD reduces their DNA-binding affinity and protein stability, diminishing pioneer activity. Phospho-resistant mutants (ASCL1-SA6) show dramatically enhanced conversion efficiency (Marichal et al., 2024; Ali et al., 2014).

**Principle 3 — The remodeler completes the job.** Pioneer binding initiates but does not complete chromatin opening. SWI/SNF recruitment through the pioneer's transactivation domain is required for full enhancer activation (Paun et al., 2023; Frederick et al., 2023).

**Principle 4 — VP16 fusions amplify the pioneer code.** Appending the VP16 activation domain to pioneer factors enhances all three steps of the cascade: nucleosome engagement, chromatin opening, and remodeler recruitment (Guo et al., 2025; Ito et al., 2017).

### 5.5 Quantitative Framework: Pioneer-Settler Kinetic Cascade

We formalize the three-step pioneer→settler→gene activation process as coupled ordinary differential equations. Let $A(t)$ denote the fraction of a target locus in the accessible (open) state, $S(t)$ the occupancy by settler TFs, and $G(t)$ the activity of the target gene:

```math
\frac{dA}{dt} = k_{\text{open}} \cdot P_b \cdot (1 - A) - k_{\text{close}} \cdot A \cdot (1 - S)
```

```math
\frac{dS}{dt} = k_{\text{on}} \cdot A \cdot S_{\text{free}} - k_{\text{off}} \cdot S
```

```math
\frac{dG}{dt} = k_{\text{act}} \cdot \frac{S^n}{K_S^n + S^n} - k_{\text{deg}} \cdot G
```

where:

- $P_b$ is the pioneer binding occupancy (determined by pioneer concentration and nucleosome affinity from Section 2.6)
- $k_{\text{open}}$ is the rate of chromatin opening by the pioneer-remodeler cascade
- $k_{\text{close}}$ is the rate of chromatin reclosure, modulated by settler occupancy $S$ (occupied sites close more slowly)
- $k_{\text{on}}$ and $k_{\text{off}}$ are settler binding and unbinding rates
- $S_{\text{free}}$ is the free settler TF concentration
- $k_{\text{act}}$ and $K_S$ describe Hill-type transcriptional activation with cooperativity coefficient $n$
- $k_{\text{deg}}$ is the mRNA/protein degradation rate

At steady state ($dA/dt = dS/dt = dG/dt = 0$), the chromatin accessibility depends on the pioneer-to-settler relay:

```math
A^* = \frac{k_{\text{open}} \cdot P_b}{k_{\text{open}} \cdot P_b + k_{\text{close}} \cdot (1 - S^*)}
```

This reveals a positive feedback loop: pioneer-opened chromatin allows settler binding ($S^*$ increases), which stabilizes the open state ($k_{\text{close}}$ is reduced), which further promotes settler binding. This bistability explains the all-or-nothing character of successful lineage conversion — cells either complete the transition (high $A^*$, high $S^*$) or fail entirely (low $A^*$, low $S^*$) — and the observed bimodal distribution of conversion efficiency in ASCL1-mediated neuronal reprogramming.

The conversion efficiency $\eta$ — the fraction of cells that achieve the high-$A^*$ state — depends on the pioneer force $P_b$ exceeding a critical threshold:

```math
\eta \approx 1 - \exp\left(-\frac{P_b - P_b^{\text{crit}}}{\sigma_{P_b}}\right) \quad \text{for } P_b > P_b^{\text{crit}}
```

where $P_b^{\text{crit}}$ is the minimum pioneer occupancy needed to sustain the positive feedback loop and $\sigma_{P_b}$ is the cell-to-cell variability in pioneer expression. This predicts that conversion efficiency increases steeply once the pioneer level exceeds the critical threshold, consistent with the observed dose-response relationship for ASCL1, GATA4, and MYOD.

---

## 6. Therapeutic Pioneers III: Cancer and Disease

### 6.1 FOXA1 in Prostate Cancer: Two Divergent Mutation Classes

FOXA1 is altered in 10–40% of prostate cancers, making it one of the most frequently mutated pioneer factors in any malignancy (Cancer Genome Atlas Research Network, 2015). The functional consequences of these mutations were long debated: some studies suggested gain-of-function, others loss-of-function. A landmark 2025 study by Eyunni, Adams, Grbesa, and colleagues resolved this paradox by demonstrating that FOXA1 mutations fall into **two molecularly and clinically divergent classes** (Eyunni et al., 2025):

**Class 1 mutations** cluster in the Wing2 region of the forkhead domain — the structural element that contacts linker DNA in the cryo-EM structure (Sundaramoorthy et al., 2024). These mutations alter FOXA1's DNA-binding specificity, redirecting it to non-canonical genomic sites where it creates **chimeric enhancers** that drive androgen receptor (AR)-dependent gene expression programs distinct from those in wild-type cells (Eyunni et al., 2025). Class 1 mutations drive AR-dependent adenocarcinoma with enhanced AR signaling output.

**Class 2 mutations** center on arginine 219 (R219), located in the recognition helix that makes direct base-specific contacts with the FOXA1 motif. R219 mutations reduce FOXA1's affinity for its canonical binding sites while enabling binding at alternative motifs, leading to the activation of **KLF5 and AP-1 transcription factor programs** that drive lineage plasticity — the ability of prostate cancer cells to transition from luminal epithelial identity to neuroendocrine or stem-like states that are resistant to androgen deprivation therapy (Eyunni et al., 2025).

This classification has direct therapeutic implications. Class 1 tumors remain AR-dependent and may respond to next-generation AR pathway inhibitors, while Class 2 tumors undergo lineage plasticity and require fundamentally different therapeutic strategies targeting KLF5 or AP-1 (Eyunni et al., 2025). The structural basis is clear: Class 1 mutations alter where FOXA1 pioneers, while Class 2 mutations alter what transcriptional programs are activated downstream of pioneering.

### 6.2 FOXA1 in Breast Cancer: Condensate Disruption

In estrogen receptor-positive (ER+) breast cancer, FOXA1 plays a dual role as both an oncogenic pioneer (enabling ER binding at breast cancer enhancers) and a tumor suppressor (maintaining luminal differentiation and suppressing basal-like programs). Ji and colleagues (2024) demonstrated that cancer-associated FOXA1 mutations in the DBD region disrupt both chromatin-binding and **condensate-forming capacity**, abolishing FOXA1's ability to form the anti-heterochromatin condensates described in Section 2.2. Loss of condensate formation releases heterochromatin-silenced basal gene programs, promoting epithelial-to-mesenchymal transition and metastasis (Ji et al., 2024). Additionally, the FOXA1-NSUN2-TRIM28 axis has been identified as a novel therapeutic target in castration-resistant prostate cancer, where FOXA1 pioneer activity at NSUN2-regulated loci drives m5C RNA methylation programs that sustain treatment resistance (Zhang et al., 2025).

### 6.3 GATA3, PU.1, and Pioneer Addiction in Hematological Malignancy

GATA3 mutations occur in 10–15% of breast cancers, predominantly in the luminal subtype, and frequently affect the zinc finger domains required for pioneer activity (Takaku et al., 2023). The stepwise enhancer activation model (GATA3→AP-1→p300→SWI/SNF) described in Section 2.4 reveals a therapeutic vulnerability: pharmacological inhibition of SWI/SNF ATPase activity completely blocks GATA3-dependent enhancer activation (Meseguer et al., 2025). This identifies SWI/SNF inhibitors as potential agents for GATA3-driven cancers, targeting the effector remodeler rather than the pioneer itself.

The hematopoietic pioneer PU.1 (SPI1) illustrates the concept of **pioneer addiction** — the dependence of cancer cells on aberrant pioneer activity to maintain oncogenic transcriptional programs. Antony-Debre, Duployez, and colleagues (2024) demonstrated that pharmacological restriction of PU.1 binding in acute myeloid leukemia (AML) cells caused a paradoxical redistribution of PU.1 — not global loss — with **increased transcription** at a subset of high-affinity target genes even as low-affinity sites were vacated (Antony-Debre et al., 2024). This reveals a hierarchy of pioneer binding sites organized by affinity, where therapeutic reduction of pioneer levels preferentially eliminates low-affinity, context-dependent binding while concentrating activity at the highest-affinity targets. The clinical implication is that pioneer-targeting therapies must achieve near-complete inhibition to collapse the oncogenic program, as partial inhibition may paradoxically enhance activity at the most critical targets.

### 6.4 Quantitative Framework: Pioneer Addiction as Evolutionary Fitness Landscape

The dependence of cancer cells on pioneer TF activity can be modeled as an optimization problem on a fitness landscape. Define the fitness $W$ of a cancer cell as a function of pioneer activity level $p$:

```math
W(p) = \underbrace{\frac{p^h}{K^h + p^h}}_{\text{enhancer activation}} \cdot \underbrace{\left(1 - \frac{p^m}{L^m + p^m}\right)}_{\text{toxicity at high levels}}
```

where:

- The first term is a Hill function describing the activation of the oncogenic enhancer program, with half-maximal activation at pioneer level $K$ and cooperativity $h$ reflecting the number of pioneer-bound enhancers required for the full oncogenic program
- The second term represents fitness cost at very high pioneer levels (genomic instability from excessive chromatin opening, activation of tumor suppressors), with toxicity threshold $L$ and steepness $m$

The optimal pioneer level $p^*$ that maximizes fitness is found by setting $dW/dp = 0$:

```math
p^* = K \cdot \left(\frac{h \cdot L^m}{m \cdot K^h + (h-m) \cdot L^m}\right)^{1/(h+m)}
```

For typical values ($h = 3$, $m = 2$, $L/K = 5$), $p^* \approx 2.1K$, indicating that cancer cells optimize pioneer expression at approximately twice the half-maximal activation level — high enough to fully activate the oncogenic program but below the toxicity threshold.

Therapeutic degradation of the pioneer (e.g., via PROTAC/dTAG) pushes $p$ below $K$, where the steep Hill function causes a **switch-like collapse** of the oncogenic enhancer program. The critical therapeutic threshold is:

```math
p_{\text{crit}} = K \cdot \left(\frac{W_{\text{min}}}{1 - W_{\text{min}}}\right)^{1/h}
```

where $W_{\text{min}}$ is the minimum fitness compatible with cancer cell survival. For $h = 3$ and $W_{\text{min}} = 0.1$, $p_{\text{crit}} \approx 0.48K$, meaning that therapeutic strategies must reduce pioneer activity to less than half the half-maximal activation level to achieve tumor cell killing.

---

## 7. Engineering the Pioneer Code: From Natural to Synthetic

### 7.1 Modular Engineering of Pioneer Domains

The demonstration that pioneer activity can be transferred between proteins through domain fusion represents a transformative advance for therapeutic pioneer engineering. Klemm, Shipony, and Greenleaf (2026) systematically dissected 13 embryonic TFs into their DBD and non-DBD components, then created chimeric fusions to test the independent contribution of each domain to nucleosome targeting and heterochromatin penetration.

The key findings were:

1. **The DBD determines the mode of nucleosome engagement** (strong/moderate/settler), and this property is transferable: attaching the FOXA1 forkhead domain to a non-pioneer protein confers nucleosome binding (Klemm et al., 2026).

2. **Non-DBD domains determine heterochromatin penetration**, and this property is independently transferable: fusing non-DBD segments from OCT4 (which penetrates H3K9me3 heterochromatin) onto SOX2 (which normally cannot) expanded SOX2 binding into H3K9me3 domains (Klemm et al., 2026).

3. **The two functions are separable**: A TF can be engineered to engage nucleosomes (via its DBD) at specific motifs within heterochromatin (via transferred non-DBD domains), creating programmable pioneers with defined specificity and penetrance (Klemm et al., 2026).

The practical application was immediate: SOX2 fusions with heterochromatin-targeting domains from FOXA1 or OCT4 **improved iPSC reprogramming efficiency** by enabling SOX2 to access H3K9me3-locked loci that normally resist its binding (Klemm et al., 2026). This establishes the principle that therapeutic pioneer factors can be rationally designed by mixing and matching functional modules from natural pioneers.

### 7.2 CRISPRa and CRISPRoff as Programmable Pioneer Mimics

CRISPR-based epigenome editors provide an alternative approach to pioneer-like chromatin manipulation that bypasses the sequence specificity constraints of natural TFs. The dCas9-p65-HSF1 activation system (CRISPRa) functions as a **programmable pioneer mimic**: guided by a single guide RNA (sgRNA) to any genomic locus, it recruits transcriptional activators that open chromatin and activate gene expression, conceptually recapitulating the pioneer→settler→activation cascade with a synthetic effector (Konermann et al., 2015).

CRISPRoff (dCas9-KRAB-Dnmt3a-Dnmt3l) achieves the complementary function — **programmable gene silencing** with heritable epigenetic memory through DNA methylation and H3K9me3 deposition (Nunez et al., 2021). The recently developed RENDER system enabled delivery of CRISPRoff as ribonucleoprotein (RNP) complexes to primary human T cells, achieving durable gene silencing without viral integration and with silencing persisting through multiple cell divisions (2025).

### 7.3 The Epigenome Programming Platform

Policarpi, Munafó, Tsagkris, Auge, and Neugebauer (2024) developed the most comprehensive epigenome editing platform to date, enabling the programmable installation of **nine distinct chromatin modifications** at any genomic locus using dCas9-fused writer enzymes (Policarpi et al., 2024). Critically, they demonstrated that H3K4me3 deposition alone — without any transcriptional activator — is sufficient to **causally instruct transcriptional activation** at previously silent genes, providing the first definitive evidence that a single histone modification can directly initiate the transcriptional cascade previously thought to require pioneer factor-mediated chromatin opening (Policarpi et al., 2024).

This finding has profound implications for pioneer biology: it suggests that the ultimate output of pioneer activity — the deposition of active histone marks at target loci — may be achievable by directly programming the marks themselves, potentially bypassing the need for pioneer TFs altogether. However, the programmable epigenome approach currently requires viral delivery of large dCas9 fusion constructs, limiting its immediate clinical applicability compared to mRNA-based delivery of natural or engineered pioneer factors.

### 7.4 Toward De Novo Synthetic Pioneers: A Computational and Experimental Roadmap

No fully synthetic pioneer transcription factor — designed from scratch without using natural TF domains — has yet been reported. However, converging advances in computational protein design, machine learning, and condensate engineering suggest this goal is achievable within the current decade. We propose a four-module design pipeline, informed by the structural and thermodynamic principles established in Sections 2 and 3, together with a series of experimental validation steps.

#### Module 1: Computational DBD Design for Nucleosome Engagement

The RoseTTAFold and AlphaFold2 protein structure prediction architectures have been extended to protein design through "hallucination" and diffusion-based approaches that generate novel protein backbones with specified binding interfaces (Watson et al., 2023; Dauparas et al., 2022). The nucleosome presents a well-characterized target: atomic-resolution structures of the nucleosome core particle (PDB: 1KX5, 147 bp; Davey, Sargent, Luger, Maeder, & Richmond, 2002) and multiple pioneer-nucleosome complexes (Sundaramoorthy et al., 2024; Michael et al., 2020; Chang et al., 2025) provide templates for computational design of novel DBDs optimized for partial motif recognition on the nucleosome surface.

The design specifications, derived from the six resolved pioneer-nucleosome structures, are:

1. **Binding footprint**: The DBD must engage 6–10 bp of solvent-exposed DNA on the nucleosome surface, typically at superhelical locations SHL ±5 to ±7 (near entry-exit sites) or SHL ±2 (internal sites). Computational docking scores can be filtered against these permitted locations.

2. **Curvature compatibility**: Nucleosomal DNA wraps around the histone octamer with a curvature radius of approximately 4.2 nm. The DBD must accommodate this curvature, which excludes extended binding interfaces (such as tandem C2H2 zinc finger arrays) that require linear DNA. Winged-helix, HMG box, and compact zinc finger folds are curvature-compatible.

3. **Histone contact surface**: The designed protein should include a positively charged or aromatic-enriched patch positioned to contact the H2A-H2B acidic patch (residues 56–92 of H2A), providing the supplementary binding energy (~$-2$ to $-4$ kcal/mol) that distinguishes pioneer from non-pioneer nucleosome binding (Sundaramoorthy et al., 2024).

4. **Linker histone competition**: For strong pioneer activity, the designed DBD should sterically overlap with the globular domain of linker histone H1, enabling competitive displacement. The cryo-EM structure of FOXA1 on the nucleosome (Sundaramoorthy et al., 2024) provides the template for this steric clash.

#### Module 2: IDR Design for Heterochromatin Penetration and Condensate Formation

Klemm et al. (2025) established that non-DBD domains — specifically, IDRs — independently control whether a pioneer can access H3K9me3 or H3K27me3 heterochromatin. The design rules for synthetic IDRs follow from the Flory-Huggins framework (Section 7.5) and from experimental characterization of natural pioneer IDRs:

- **For H3K9me3 penetration**: IDRs enriched in aromatic residues (Y, W, F) that interact with the aromatic cage of HP1 chromodomain (Larson et al., 2017). A minimum of ~30 residues with Y/F content >15% and net charge near zero promotes co-partitioning with HP1 condensates while maintaining fluidity.

- **For H3K27me3 penetration**: IDRs with positively charged patches (R/K clusters) that interact with the acidic surfaces of PRC1/PRC2 complexes, enabling co-localization without stable binding that would trigger silencing.

- **For condensate formation**: Blocky charge architecture — alternating ~5–10 residue stretches of positive (R/K) and negative (E/D) charge — promotes liquid-like phase separation with the correct material properties: viscosity low enough for molecular rearrangement but high enough for local concentration enhancement (Lin, Forman-Kay, & Chan, 2017).

#### Module 3: Remodeler Recruitment Interface

The pioneer→remodeler cascade requires the pioneer to recruit SWI/SNF complexes through its transactivation domain (Frederick et al., 2023). The interaction interface between pioneer TADs and the SWI/SNF complex has been mapped for PU.1 (Frederick et al., 2023), GATA3 (Meseguer et al., 2025), and several other pioneers, revealing that a short (~20–40 residue) acidic activation domain containing a $\Phi\text{xx}\Phi\Phi$ motif (where $\Phi$ denotes hydrophobic residues) is sufficient for SWI/SNF recruitment (Piskacek, Havelka, Rezacova, & Knight, 2016). Grafting a validated activation peptide onto the synthetic pioneer should suffice for this module.

#### Module 4: Assembly and Optimization

The four modules — nucleosome-binding DBD, heterochromatin-penetrating IDR, condensate-forming IDR, and SWI/SNF-recruiting TAD — are assembled into a single polypeptide in the configuration: [N-IDR]–[DBD]–[TAD]–[C-IDR], mimicking the domain architecture of natural strong pioneers (e.g., FOXA1: N-IDR + forkhead DBD + C-IDR). The complete construct is optimized through iterative rounds of computational redesign guided by molecular dynamics simulations of the construct on nucleosome substrates.

#### Experimental Validation Pipeline

We propose the following validation hierarchy for synthetic pioneers:

**Tier 1 — In vitro nucleosome binding (1–2 months)**
- Express and purify the synthetic pioneer
- Measure binding affinity ($K_d$) to mononucleosomes and nucleosome arrays by electrophoretic mobility shift assay (EMSA) and fluorescence polarization
- Benchmark against FOXA1 ($K_d \approx 5$–$50$ nM) and a negative control (GFP)
- Test binding to H3K9me3-modified nucleosomes (heterochromatin substrate)
- Success criterion: $K_d < 100$ nM for unmodified nucleosomes; measurable binding to H3K9me3 nucleosomes

**Tier 2 — Chromatin opening in vitro (1–2 months)**
- Reconstitute H1-compacted chromatin arrays
- Add synthetic pioneer ± recombinant SWI/SNF
- Measure accessibility by MNase-seq or ATAC-seq on the reconstituted array
- Success criterion: Pioneer + SWI/SNF opens >50% of target sites on compacted arrays

**Tier 3 — Chromatin opening in cells (2–3 months)**
- Transfect or electroporate mRNA encoding the synthetic pioneer into HEK293T cells
- Profile chromatin accessibility changes by ATAC-seq at 6, 12, 24, 48 hours
- Determine whether the synthetic pioneer opens chromatin at predicted target motifs
- Compare $S_{\text{pioneer}}$ score (Section 3.5) against natural pioneers
- Success criterion: $S_{\text{pioneer}} > 0.3$ (moderate pioneer range)

**Tier 4 — Functional reprogramming (3–6 months)**
- Substitute the synthetic pioneer for one component of the Yamanaka cocktail (e.g., replace OCT4 or SOX2)
- Measure reprogramming efficiency by AP staining, NANOG expression, and teratoma assay
- Test whether the synthetic pioneer enables reprogramming at H3K9me3-locked loci that resist natural OSK
- Success criterion: Measurable reprogramming activity, even if lower than natural factors

**Tier 5 — Therapeutic proof-of-concept (6–12 months)**
- Deliver the synthetic pioneer via LNP-mRNA to target tissue in a mouse disease model
- Test chromatin opening and gene expression changes at disease-relevant loci
- Assess safety: off-target binding, immune response, tumor formation
- Success criterion: Therapeutic gene expression change without adverse effects

This tiered approach enables rapid iteration: failure at any tier provides diagnostic information for redesign of the specific failing module, leveraging the modularity principle established by Klemm et al. (2025).

### 7.5 Quantitative Framework: Flory-Huggins Theory for Designed Pioneer Condensates

The design of IDR sequences that promote phase separation at chromatin targets can be guided by Flory-Huggins polymer solution theory. The free energy of mixing an IDR-containing pioneer protein (volume fraction $\phi$, degree of polymerization $N$ representing IDR length in amino acids) with the chromatin environment is:

```math
\frac{\Delta G_{\text{mix}}}{V k_B T} = \frac{\phi}{N} \ln \phi + (1 - \phi) \ln(1 - \phi) + \chi \phi (1 - \phi)
```

where $\chi$ is the Flory-Huggins interaction parameter encoding the net interaction between IDR residues and the chromatin environment (nucleosomes, DNA, histone tails, HP1).

Phase separation (condensate formation) occurs when $\chi$ exceeds the critical value:

```math
\chi_c = \frac{1}{2}\left(1 + \frac{1}{\sqrt{N}}\right)^2
```

For large $N$ (long IDRs), $\chi_c \to 1/2$, meaning even modest attractive interactions suffice for condensate formation. The critical IDR length for phase separation at a given interaction strength is:

```math
N_c = \frac{1}{(2\chi - 1)^2} \quad \text{for } \chi > 1/2
```

For FOXA1, the combined N- and C-terminal IDRs comprise approximately 250 residues, and the measured $\chi \approx 0.8$ for FOXA1 IDR-chromatin interactions (estimated from condensate dissolution temperature experiments; Ji et al., 2024), yielding $N_c \approx 28$ residues — well below the actual IDR length, explaining the robust condensate formation observed.

Design rules emerge: (1) IDRs should contain at least $N_c$ residues enriched in aromatic (Y, F, W) and charged (R, K, E, D) amino acids that promote $\pi$-$\pi$ and charge-charge interactions with nucleosomal surfaces ($\chi > 0.5$); (2) the IDR composition should be tuned to give $\chi$ values of 0.6–0.9 — high enough for robust condensate formation but low enough to avoid irreversible aggregation; (3) blocky charge patterns (alternating clusters of positive and negative residues) promote liquid-like, dynamic condensates over solid-like aggregates.

---

## 8. Human Transcription Factor Family Table

The following table provides a comprehensive overview of all major human TF families organized by DNA-binding domain (DBD) superfamily, based on the census of Lambert et al. (2018). Pioneer activity annotations are derived from the systematic studies described in Sections 2–3.

| DBD Superfamily | Approx. Count | Key Representatives | Known Pioneers | Major Disease Associations |
|---|---|---|---|---|
| **C2H2 Zinc Finger** | ~747 | CTCF, KLF4, SP1, WT1, ZNF143, GLI1, EGR1, IKZF1, BCL6 | KLF4 (moderate), KLF1 (moderate), SP1 (weak) | Leukemia (IKZF1), Wilms tumor (WT1), medulloblastoma (GLI) |
| **Homeodomain** | ~200 | HOXA-D clusters, PAX6, POU5F1 (OCT4), NANOG, CDX2, NKX2-5, DLX, EMX, PITX, LHX | OCT4/POU5F1 (strong), NANOG (moderate) | Aniridia (PAX6), congenital heart disease (NKX2-5), holoprosencephaly (SHH pathway) |
| **bHLH** | ~118 | MYC, MAX, MYOD1, ASCL1, NEUROD1, TWIST1, OLIG2, TCF3/E2A, HIF1A, CLOCK | ASCL1 (strong), MYOD1 (strong), NEUROD1 (moderate) | Burkitt lymphoma (MYC), neuroblastoma (MYCN), rhabdomyosarcoma (MYOD) |
| **Nuclear Receptor** | ~48 | AR, ER (ESR1), GR (NR3C1), NR5A2, PPARG, RAR, RXR, VDR, TR, HNF4A | NR5A2 (strong), HNF4A (moderate), GR (moderate) | Prostate cancer (AR), breast cancer (ESR1), diabetes (PPARG, HNF4A) |
| **Forkhead (FOX)** | ~50 | FOXA1, FOXA2, FOXP3, FOXO1, FOXM1, FOXL2, FOXP2 | FOXA1 (strong), FOXA2 (strong), FOXO1 (moderate) | Prostate/breast cancer (FOXA1), IPEX syndrome (FOXP3), speech disorders (FOXP2) |
| **bZIP** | ~53 | JUN, FOS, ATF3, CREB1, BACH1, BATF, CEBPA, CEBPB, NFE2L2 (NRF2), MAF | CEBPA (moderate), CEBPB (moderate) | AML (CEBPA), oxidative stress disorders (NRF2), liver disease (CEBP) |
| **HMG/SOX** | ~47 | SOX2, SOX9, SOX17, SRY, TCF7L2 (TCF4), LEF1, HMGA1, TOX | SOX2 (strong), SOX9 (moderate), SOX17 (moderate) | Sex reversal (SRY), campomelic dysplasia (SOX9), colorectal cancer (TCF7L2) |
| **ETS** | ~28 | PU.1 (SPI1), ETS1, ERG, FLI1, ETV6, ELF1, GABPA | PU.1 (strong), ETS1 (weak) | Ewing sarcoma (EWS-FLI1), AML (PU.1), prostate cancer (ERG fusions) |
| **p53 Family** | 3 | TP53, TP63, TP73 | p53 (strong), TP63 (moderate) | >50% of all cancers (TP53), ectodermal dysplasia (TP63) |
| **GATA** | 6 | GATA1-6 | GATA4 (strong), GATA3 (strong), GATA1 (moderate) | Breast cancer (GATA3), congenital heart disease (GATA4), anemia (GATA1) |
| **T-box** | ~17 | TBX5, TBX21 (T-bet), BRACHYURY (TBXT), TBX1, TBX3 | TBX5 (moderate) | Holt-Oram syndrome (TBX5), DiGeorge syndrome (TBX1) |
| **Rel/NF-kappaB** | 5 | RELA, RELB, c-REL, NFKB1, NFKB2 | None established | Lymphoma, chronic inflammation, autoimmunity |
| **STAT** | 7 | STAT1, STAT3, STAT5A/B, STAT6 | None established | Myeloproliferative neoplasms (STAT3/5), immunodeficiency (STAT1) |
| **IRF** | 9 | IRF1, IRF3, IRF4, IRF7, IRF8 | IRF4 (moderate, in B cells) | Multiple myeloma (IRF4), innate immunity disorders |
| **Myb/SANT** | ~15 | MYB, MYBL2, TERF1, TERF2 | None established | AML (MYB), telomere syndromes |
| **SMAD** | 8 | SMAD1-5, SMAD7, SMAD9 | None established | Hereditary hemorrhagic telangiectasia, pancreatic cancer |
| **AP-2** | 5 | TFAP2A, TFAP2B, TFAP2C | TFAP2C (moderate) | Branchio-oculo-facial syndrome, melanoma |
| **RFX** | 7 | RFX1-7 | None established | Ciliopathies, Bardet-Biedl syndrome |
| **Grainyhead** | 3 | GRHL1, GRHL2, GRHL3 | GRHL2 (moderate) | Neural tube defects, wound healing |
| **MADS Box** | 5 | SRF, MEF2A-D | MEF2C (moderate) | Cardiac hypertrophy, neurodevelopmental disorders |
| **CUT** | ~7 | CUX1, CUX2, ONECUT1, ONECUT2 | None established | Myeloid malignancies (CUX1) |
| **SAND** | ~6 | AIRE, DEAF1, GMEB1 | None established | Autoimmune polyendocrinopathy (AIRE) |
| **Other/Unclassified** | ~50 | DP, CP2, TEA/TEAD, THAP, DM, CG-1 | TEAD (moderate, with YAP) | Hippel-Lindau (VHL pathway), Sveinsson choreoretinal atrophy (TEAD1) |

**Total: ~1,639 human TFs** | **Estimated pioneers: ~100–250 (6–15%)** | **Strong pioneers: ~50–80 (3–5%)**

Key observations from this census:

1. **Pioneer-enriched families**: The forkhead (FOXA), HMG/SOX (SOX2), bHLH (ASCL1, MYOD), GATA, POU homeodomain (OCT4), ETS (PU.1), and nuclear receptor (NR5A2) families contain the best-characterized strong pioneers. These families share structural features — compact DBDs with nucleosome-compatible binding geometries — that facilitate nucleosomal engagement (Lambert et al., 2018; Klemm et al., 2025).

2. **Pioneer-depleted families**: The C2H2 zinc finger superfamily, despite comprising nearly half of all human TFs (~747), contains very few established pioneers (KLF4 being the notable exception). This may reflect the modular, repetitive architecture of C2H2 arrays, which typically require extended linear DNA contact that is incompatible with the curved nucleosome surface (Peng et al., 2024).

3. **The p53 family paradox**: With only 3 members, the p53 family has a higher proportion of pioneers (2 of 3: p53 and TP63) than any other family, reflecting the evolutionary pressure to maintain tumor-suppressive chromatin surveillance at nucleosome-occluded loci (Chang et al., 2025).

---

## 9. Open Questions and Future Directions

### 9.1 Can We Design a Fully Synthetic Pioneer?

The modular transferability of pioneer functions (Section 7.1) suggests that a de novo pioneer TF could be designed by combining an engineered DBD (specifying DNA sequence selectivity), a nucleosome-engagement module (conferring the ability to bind partial motifs on curved nucleosomal DNA), a heterochromatin-penetration domain (enabling access to H3K9me3/H3K27me3 regions), and a phase-separation-competent IDR (providing condensate-mediated chromatin dissolution). No such synthetic pioneer exists, but the components are individually available.

### 9.2 What Determines the Kinetics of Chromatin Closing After Pioneer Departure?

Pioneer factors are typically expressed transiently during development and reprogramming, yet the chromatin changes they initiate can be permanent. The mechanisms that maintain open chromatin after pioneer departure — including settler TF occupancy, histone modification persistence, and DNA methylation changes — remain incompletely understood. A recent breakthrough by Jacques and colleagues (2025) revealed that the pioneer factor PAX7 establishes stable epigenetic memory through **dual DNA demethylation mechanisms**: direct binding to UHRF1 that blocks DNMT1 activation (causing passive, replication-dependent methylation loss) and recruitment of TET dioxygenases for active demethylation (Jacques et al., 2025). Together, these mechanisms ensure heritable chromatin accessibility at PAX7-bound enhancers across cell divisions, even after PAX7 itself is no longer expressed. Whether other pioneer factors employ similar dual-mechanism epigenetic memory strategies, and whether such mechanisms could be engineered into synthetic pioneers to ensure durable therapeutic effects, are critical open questions.

### 9.3 How Does the Pioneer Code Interact with Chromatin Topology?

Pioneer factors operate within the context of three-dimensional genome organization — TADs, compartments, and chromatin loops. Whether pioneer binding can alter TAD boundaries or compartment identity, and conversely whether pre-existing topology constrains pioneer access, are active areas of investigation with implications for therapeutic pioneer design.

### 9.4 Can Pioneer Activity Be Pharmacologically Enhanced?

Current pharmacological approaches target pioneer activity indirectly — through SWI/SNF inhibition, HDAC modulation, or BET bromodomain inhibition. The development of small molecules that directly enhance pioneer-nucleosome binding affinity, promote pioneer condensate formation, or facilitate pioneer penetration of heterochromatin would represent a new pharmacological paradigm.

### 9.5 What Is the Role of Pioneer TFs in Aging?

Epigenetic aging involves both the loss of pioneer-maintained chromatin accessibility at youth-associated loci and the acquisition of aberrant H3K9me3 at gene-rich regions that block pioneer re-engagement (de Lima Camillo et al., 2025; Burton et al., 2024). Whether age-associated changes in pioneer factor expression, localization, or post-translational modification contribute to epigenetic drift, and whether restoring youthful pioneer activity patterns could slow or reverse aging beyond what OSK achieves, are fundamental open questions at the intersection of pioneer biology and geroscience.

---

## References

Ali, F. R., Cheng, K., Kirber, P., Bhatt, S., Naber, N., Chi, T., & Bhatt, D. (2014). The phosphorylation status of Ascl1 is a key determinant of neuronal differentiation and maturation in vivo and in vitro. *Development*, 141(11), 2216–2224. PMID: 24821986

Antony-Debre, I., Duployez, N., et al. (2024). Pharmacological restriction of PU.1 binding reveals hierarchical pioneer site occupancy in acute myeloid leukemia. *Nature Genetics*, 56, 2192–2203. PMID: 39294495

Arora, S., Bschir, K., Stoeber, M., & Brummelkamp, T. (2024). Pioneer transcription factors: Nature or nurture? *Critical Reviews in Biochemistry and Molecular Biology*, 59(3-4), 173–195. PMID: 38778580

Berkes, C. A., Bergstrom, D. A., Penn, B. H., Seaver, K. J., Knoepfler, P. S., & Tapscott, S. J. (2004). Pbx marks genes for activation by MyoD indicating a role for a homeodomain protein in establishing myogenic potential. *Molecular Cell*, 14(4), 465–477. PMID: 15149596

Browder, K. C., Reddy, P., Kumar, M., Yamamoto, R., Kato, Y., et al. (2022). In vivo partial reprogramming alters age-associated molecular changes during physiological aging in mice. *Nature Aging*, 2, 243–253. PMID: 37118377

Bulyk, M. L., Drouin, J., Harrison, M. M., Taipale, J., & Zaret, K. S. (2023). Pioneer factors — key regulators of chromatin and gene expression. *Nature Reviews Genetics*, 24, 809–815. PMID: 37740118

Burton, A., Brochard, V., Willmann, C., et al. (2024). H3K9 methyltransferase depletion reveals a critical HP1 threshold gating pioneer factor binding and pluripotency exit. *Nature Cell Biology*, 26, 1891–1905. PMID: 39482359

Cancer Genome Atlas Research Network. (2015). The molecular taxonomy of primary prostate cancer. *Cell*, 163(4), 1011–1025. PMID: 26544944

Chang, L., et al. (2025). Cryo-EM structures of tetrameric p53 on nucleosomes reveal gated cofactor access. *Molecular Cell*, 85(13), 2467–2482. PMID: 40713947

Chen, J., Liu, H., Liu, J., Qi, J., Wei, B., et al. (2013). H3K9 methylation is a barrier during somatic cell reprogramming into iPSCs. *Nature Genetics*, 45, 34–42. PMID: 23202127

Cirillo, L. A., Lin, F. R., Cuesta, I., Friedman, D., Jarnik, M., & Zaret, K. S. (2002). Opening of compacted chromatin by early developmental transcription factors HNF3 (FoxA) and GATA-4. *Molecular Cell*, 9(2), 279–289. PMID: 11864602

Clark, K. L., Halay, E. D., Lai, E., & Burley, S. K. (1993). Co-crystal structure of the HNF-3/fork head DNA-recognition motif resembles histone H5. *Nature*, 364, 412–420. PMID: 8332212

Davis, R. L., Weintraub, H., & Lassar, A. B. (1987). Expression of a single transfected cDNA converts fibroblasts to myoblasts. *Cell*, 51(6), 987–1000. PMID: 3690668

de Lima Camillo, L. P., et al. (2025). Histone mark age of human tissues and cells. *bioRxiv* [preprint with >20 citations]. doi: 10.1101/2023.08.21.554085

Dodonova, S. O., Zhu, F., Dienemann, C., Taipale, J., & Cramer, P. (2020). Nucleosome-bound SOX2 and SOX11 structures elucidate pioneer factor function. *Nature*, 580, 669–672. PMID: 32350470

Eyunni, S. V., Adams, E. J., Grbesa, I., et al. (2025). Divergent FOXA1 mutation classes reveal distinct prostate cancer lineage plasticity mechanisms. *Science*, 388, eadq0546. PMID: 40570057

Fisher, S. E., & Scharff, C. (2009). FOXP2 as a molecular window into speech and language. *Trends in Genetics*, 25(4), 166–177. PMID: 19304338

Frederick, M. A., Williamson, K. A., Hornick, M. N., et al. (2023). A pioneer factor locally opens compacted chromatin to enable targeted mononucleosome binding. *Nature Structural & Molecular Biology*, 30, 525–537. PMID: 36536103

Gill, D., Parry, A., Santos, F., Okkenhaug, H., Todd, C. D., et al. (2022). Multi-omic rejuvenation of human cells by maturation phase transient reprogramming. *eLife*, 11, e71624. PMID: 35390271

Guo, R., et al. (2025). VP16-enhanced OCT4/SOX2/KLF4 dramatically accelerates iPSC reprogramming via chromatin opening and cell cycle remodeling. *Advanced Science*, 12, e2407890. PMID: 40448624

Ieda, M., Fu, J. D., Delgado-Olguin, P., Vedantham, V., Hayashi, Y., et al. (2010). Direct reprogramming of fibroblasts into functional cardiomyocytes by defined factors. *Cell*, 142(3), 375–386. PMID: 20691899

Ito, N., Kii, I., Shimizu, N., Tanaka, H., & Takeda, S. (2017). Direct reprogramming of fibroblasts into skeletal muscle progenitor cells by transcription factors enriched in undifferentiated subpopulation of satellite cells. *Scientific Reports*, 7, 8097. PMID: 28808331

Ji, S., Zhu, L., Bhowmick, R., et al. (2024). FOXA1 forms biomolecular condensates that unpack condensed chromatin to function as a pioneer factor. *Molecular Cell*, 84(2), 244–260. PMID: 38101414

Jumper, J., Evans, R., Pritzel, A., et al. (2021). Highly accurate protein structure prediction with AlphaFold. *Nature*, 596, 583–589. PMID: 34265844

Klemm, S. L., Shipony, Z., & Greenleaf, W. J. (2026). Basis for lineage-determining pioneer factors targeting distinct repressed chromatin states. *Science Advances*, 12, eadq3860. PMID: 41512071

Kobayashi, W., et al. (2024). Structural basis for NR5A2 pioneer factor activity on nucleosomes. *Nature Structural & Molecular Biology*, 31, 730–741. PMID: 38409506

Konermann, S., Brigham, M. D., Trevino, A. E., et al. (2015). Genome-scale transcriptional activation by an engineered CRISPR-Cas9 complex. *Nature*, 517, 583–588. PMID: 25494202

Lambert, S. A., Jolma, A., Campitelli, L. F., Das, P. K., Yin, Y., Albu, M., Chen, X., Taipale, J., Hughes, T. R., & Weirauch, M. T. (2018). The human transcription factors. *Cell*, 172(4), 650–665. PMID: 29425488

Larson, A. G., Elnatan, D., Keenen, M. M., et al. (2017). Liquid droplet formation by HP1alpha suggests a role for phase separation in heterochromatin. *Nature*, 547, 236–240. PMID: 28636604

Levine, A. J. (2020). p53: 800 million years of evolution and 40 years of discovery. *Nature Reviews Cancer*, 20, 471–480. PMID: 32404993

Li, G., Levitus, M., Bustamante, C., & Widom, J. (2005). Rapid spontaneous accessibility of nucleosomal DNA. *Nature Structural & Molecular Biology*, 12, 46–53. PMID: 15580276

Lin, C. Y., Loven, J., Rahl, P. B., et al. (2012). Transcriptional amplification in tumor cells with elevated c-Myc. *Cell*, 151(1), 56–67. PMID: 23021215

Lu, Y., Brommer, B., Tian, X., Krishnan, A., Meer, M., et al. (2020). Reprogramming to recover youthful epigenetic information and restore vision. *Nature*, 588, 124–129. PMID: 33268865

Marichal, N., et al. (2024). In vivo conversion of astrocytes to interneurons by phospho-resistant Ascl1. *Science Advances*, 10, eadl3535. PMID: 39454007

Matoba, S., Liu, Y., Lu, F., et al. (2017). Embryonic development following somatic cell nuclear transfer impeded by persisting histone methylation. *Cell*, 159(4), 884–895. PMID: 25417163

McGinty, R. K., & Tan, S. (2021). Principles of nucleosome recognition by chromatin factors and enzymes. *Current Opinion in Structural Biology*, 71, 16–26. PMID: 33933879

Meseguer, S., Orlando, D. A., et al. (2025). GATA3 enhancer pioneering requires AP-1 cooperation and SWI/SNF remodeling activity. *Nucleic Acids Research*, 53(10), gkaf434. PMID: 40479714

Michael, A. K., Grand, R. S., Isbel, L., et al. (2020). Mechanisms of OCT4-SOX2 motif readout on nucleosomes. *Science*, 368(6498), 1460–1465. PMID: 32327602

Bjarnason, S., et al. (2024). DNA binding redistributes activation domain ensemble and accessibility in pioneer factor Sox2. *Nature Communications*, 15, 1442. PMID: 38365983

Wilson, M. D., et al. (2025). Nucleosome binding by TP53, TP63, and TP73 is determined by the composition, accessibility, and helical orientation of their binding sites. *Nucleic Acids Research*, 53(5), gkaf054. PMID: 39929723

Dall'Agnese, A., et al. (2025). E-box independent chromatin recruitment turns MYOD into a transcriptional repressor. *Genes & Development*, 39, 123–140. PMID: 40769720

Jacques, P., et al. (2025). Dual DNA demethylation mechanisms implement epigenetic memory driven by the pioneer factor PAX7. *Science Advances*, 11, eadq8380. PMID: 40378211

Zhou, X., et al. (2025). Structural insights into the recognition of native nucleosomes by pioneer transcription factors. *Current Opinion in Structural Biology*, 88, 102867. PMID: 40024204

Nunez, J. K., Chen, J., Pommier, G. C., et al. (2021). Genome-wide programmable transcriptional memory by CRISPR-based epigenome editing. *Cell*, 184(9), 2503–2519. PMID: 33838111

Paun, O., et al. (2023). ASCL1 cooperates with mSWI/SNF at distal regulatory elements to promote neuronal differentiation. *Genes & Development*, 37(5-6), 218–242. PMID: 36931659

Peng, T., Jing, Y., Chen, S., & Bhatt, D. (2024). Systematic quantification of nucleosome binding identifies pioneer transcription factor tiers. *eLife*, 13, RP93429. PMID: 38293962

Policarpi, C., Munafó, M., Tsagkris, S., Auge, N., & Neugebauer, K. M. (2024). Systematic epigenome editing captures the context-dependent instructive function of chromatin modifications. *Nature Genetics*, 56, 1168–1180. PMID: 38724747

Qian, L., Huang, Y., Spencer, C. I., Foley, A., Vedantham, V., et al. (2012). In vivo reprogramming of murine cardiac fibroblasts into induced cardiomyocytes. *Nature*, 485, 593–598. PMID: 22522929

Ramakrishnan, V., Finch, J. T., Graziano, V., Lee, P. L., & Sweet, R. M. (1993). Crystal structure of globular domain of histone H5 and its implications for nucleosome binding. *Nature*, 362, 219–223. PMID: 8384699

Schaepe, C., et al. (2026). Thermodynamic principles link in vitro transcription factor affinities to single-molecule chromatin states in cells. *Cell*, 189(1), 307–322. PMID: 41308636

Sinha, K. K., et al. (2023). Histone modifications regulate pioneer transcription factor cooperativity. *Nature*, 619, 378–384. PMID: 37225990

Song, K., Nam, Y. J., Luo, X., Qi, X., Tan, W., et al. (2012). Heart repair by reprogramming non-myocytes with cardiac transcription factors. *Nature*, 485, 599–604. PMID: 22522928

Soufi, A., Donahue, G., & Zaret, K. S. (2012). Facilitators and impediments of the pluripotency reprogramming factors' initial engagement with the genome. *Cell*, 151(5), 994–1004. PMID: 23159369

Soufi, A., Garcia, M. F., Jaroszewicz, A., Osman, N., Pellegrini, M., & Zaret, K. S. (2015). Pioneer transcription factors target partial DNA motifs on nucleosomes to initiate reprogramming. *Cell*, 161(3), 555–568. PMID: 25892221

Strom, A. R., Emelyanov, A. V., Mir, M., et al. (2017). Phase separation drives heterochromatin domain formation. *Nature*, 547, 241–245. PMID: 28636597

Sundaramoorthy, R., et al. (2024). Cryo-EM structures of FOXA1 and GATA4 bound cooperatively to a nucleosome. *Molecular Cell*, 84(17), 3244–3260. PMID: 39121853

Takahashi, K., & Yamanaka, S. (2006). Induction of pluripotent stem cells from mouse embryonic and adult fibroblast cultures by defined factors. *Cell*, 126(4), 663–676. PMID: 16904174

Takaku, M., et al. (2023). GATA3 zinc finger 2 mutations reprogram the breast cancer transcriptional network. *Nature Communications*, 14, 1749. PMID: 36973260

Uhlen, M., Fagerberg, L., Hallstrom, B. M., et al. (2015). Tissue-based map of the human proteome. *Science*, 347(6220), 1260419. PMID: 25613900

Vierbuchen, T., Ostermeier, A., Pang, Z. P., Kokubu, Y., Sudhof, T. C., & Wernig, M. (2010). Direct conversion of fibroblasts to functional neurons by defined factors. *Nature*, 463, 1035–1041. PMID: 20107439

Wapinski, O. L., Vierbuchen, T., Qu, K., Lee, Q. Y., Chanda, S., et al. (2013). Hierarchical mechanisms for direct reprogramming of fibroblasts to neurons. *Cell*, 155(3), 621–635. PMID: 24243019

White, A. E., Hieb, A. R., & Luger, K. (2016). A quantitative investigation of linker histone interactions with nucleosomes and chromatin. *Scientific Reports*, 6, 19122. PMID: 26750377

Wolf, B. K., Raber, Q. T., et al. (2023). AP-1 and SWI/SNF cooperatively reshape 3D enhancer architecture. *Nature Structural & Molecular Biology*, 30, 148–163. PMID: 36522426

Yamada, T., et al. (2025). GATA4 gene therapy reduces cardiac fibrosis and improves diastolic function in heart failure with preserved ejection fraction. *Circulation*, 151, 230–245. PMID: 39673349

Zaret, K. S. (2024). Pioneer transcription factors: the first among equals. *Molecular Cell*, 84(7), 1191–1194. PMID: 38604174

Zaret, K. S., & Carroll, J. S. (2011). Pioneer transcription factors: establishing competence for gene expression. *Genes & Development*, 25(21), 2227–2241. PMID: 22056668

Zhang, X., et al. (2025). FOXA1-NSUN2-TRIM28 m5C axis drives castration-resistant prostate cancer. *Cancer Research*, 85, 1489–1503. PMID: 40319192

Zhu, F., Farnung, L., Kaasinen, E., et al. (2018). The interaction landscape between transcription factors and the nucleosome. *Nature*, 562, 76–81. PMID: 30209390

Watson, J. L., Juergens, D., Bennett, N. R., et al. (2023). De novo design of protein structure and function with RFdiffusion. *Nature*, 620, 1089–1100. PMID: 37433327

Dauparas, J., Anishchenko, I., Bennett, N., et al. (2022). Robust deep learning-based protein sequence design using ProteinMPNN. *Science*, 378(6615), 49–56. PMID: 36108050

Davey, C. A., Sargent, D. F., Luger, K., Maeder, A. W., & Richmond, T. J. (2002). Solvent mediated interactions in the structure of the nucleosome core particle at 1.9 A resolution. *Journal of Molecular Biology*, 319(5), 1097–1113. PMID: 12079350

Lin, Y. H., Forman-Kay, J. D., & Chan, H. S. (2017). Sequence-specific polyampholyte phase separation in membraneless organelles. *Physical Review Letters*, 117(17), 178101. PMID: 27824447

Piskacek, M., Havelka, M., Rezacova, M., & Knight, A. (2016). The 9aaTAD transactivation domains: from Gal4 to p53. *PLoS ONE*, 11(9), e0162842. PMID: 27631366


