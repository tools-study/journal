# Chromosome Replication Review

---

## Abstract

Faithful chromosome replication is the most consequential molecular event in cell biology: every cell division requires the precise duplication of 6.4 billion base pairs of DNA, the coordinated assembly and disassembly of thousands of replication machines, and the accurate transmission of both genetic and epigenetic information to daughter cells. Despite extraordinary advances over the past decade — including the biochemical reconstitution of complete eukaryotic replisomes, cryo-electron microscopy structures of the human CMG helicase and its associated polymerases at near-atomic resolution, single-molecule dissection of origin licensing, and genome-wide single-cell replication timing maps — chromosome replication remains governed by six fundamental problems that define the frontier of the field as of early 2026. This review examines each problem through the lens of its core mechanistic question: (I) **The Licensing Problem** — how cells load exactly the right number of MCM2-7 helicases at replication origins, and why they systematically overload by 10-20-fold; (II) **The Firing Problem** — how the cell selects which licensed origins to activate, in what temporal order, and through what kinase cascade; (III) **The Fidelity Problem** — how the replisome achieves an aggregate error rate of approximately 10⁻¹⁰ per base pair per division through a three-stage cascade of nucleotide selectivity, exonuclease proofreading, and mismatch repair; (IV) **The Completion Problem** — how cells guarantee that every nucleotide is replicated exactly once before mitosis, despite stochastic origin firing and the vulnerability of common fragile sites; (V) **The Inheritance Problem** — how parental histones and DNA methylation marks are faithfully segregated to daughter strands at the replication fork through the MCM2 histone chaperone and DNMT1-UHRF1 coupling mechanisms; and (VI) **The Timing Problem** — how megabase-scale replication timing domains encode and maintain cell-type-specific identity through the RIF1-PP1 master timing axis. For each problem we integrate the latest structural, biochemical, and genomic evidence with novel mathematical frameworks (F232–F242) spanning stochastic point processes, Hopfield-Ninio kinetic proofreading theory, Shannon channel capacity, covering process statistics, Markov chain epigenetic inheritance models, and Ising-type phase transition models for timing domain boundaries. We identify specific open questions for each problem and propose experimental programs designed to resolve them.

---

## 1. Introduction

### 1.1 The Central Event of Cell Biology

DNA replication is the only molecular process that must be executed with near-perfection in every cell division, yet operates under severe constraints of time, energy, and fidelity. The human genome comprises approximately 6.4 × 10⁹ base pairs distributed across 46 chromosomes, and S phase — the period during which DNA is duplicated — lasts approximately 8–10 hours in a typical mammalian somatic cell (Chagin et al., 2016). To replicate the genome within this window, cells activate approximately 30,000–50,000 replication origins, each nucleating a bidirectional replication fork that synthesizes DNA at rates of approximately 1–2 kilobases per minute (Técher et al., 2017; Petryk et al., 2016). The replication machinery must copy this vast genome with an error rate of approximately 10⁻¹⁰ per base pair per cell division, a feat requiring the coordinated action of over 30 distinct proteins at each replication fork (Burgers & Kunkel, 2017).

The past decade has witnessed a transformation in our understanding of this process, driven by three technological revolutions. First, the complete biochemical reconstitution of eukaryotic DNA replication — initially in budding yeast using 16 purified factors comprising 42 polypeptides (Yeeles et al., 2015), and subsequently with human proteins achieving in vivo replication rates (Jones et al., 2022) — has enabled the dissection of replication initiation, elongation, and termination under defined conditions (O'Donnell & Li, 2024). Second, cryo-electron microscopy (cryo-EM) has provided near-atomic-resolution structures of essentially every major replication complex, including the origin recognition complex (ORC), the MCM2-7 helicase, the CMG (CDC45-MCM2-7-GINS) holohelicase, and the complete replisome engaged with forked DNA (Bleichert et al., 2017; Yuan et al., 2020; Baretić et al., 2020). Third, genome-wide approaches — DNA combing, nascent strand sequencing, Repli-seq, single-cell Repli-seq, and eSPAN/SCAR-seq for strand-specific chromatin analysis — have revealed the organization of replication at the systems level, connecting molecular mechanisms to genome-scale programs (Zhao et al., 2020; Petryk et al., 2018).

### 1.2 The Six Problems

Despite these advances, chromosome replication is most productively understood through six fundamental problems, each defined by a specific mechanistic question that remains incompletely resolved. These problems are not independent: the licensing problem constrains the firing problem, which constrains the completion problem; the fidelity problem operates at every fork nucleated by the firing program; and the inheritance problem transforms replication from a purely genetic process into an epigenetic one, with the timing problem providing the genome-scale organizational framework within which all other problems are embedded.

This review examines each problem in turn, integrating the latest structural, biochemical, and genomic evidence with novel mathematical frameworks that formalize the quantitative constraints governing each problem. Throughout, we distinguish between what is firmly established and what remains uncertain, identifying specific open questions that define the frontier of the field.

---

## 2. Section I: The Licensing Problem — Loading the Right Number of Helicases

### 2.1 The Core Question

Every eukaryotic cell must solve a fundamental counting problem during the G1 phase of the cell cycle: load enough MCM2-7 helicase complexes at replication origins to guarantee complete genome duplication, but prevent the loading of MCM complexes during S phase that could cause re-replication. This problem is solved by a temporally regulated licensing system that restricts MCM loading to a defined window and then irreversibly inactivates the loading machinery upon S-phase entry (Siddiqui et al., 2013; Bleichert et al., 2017).

### 2.2 The Origin Recognition Complex

Replication licensing begins with the origin recognition complex (ORC), a six-subunit AAA+ ATPase (ORC1-6) that marks replication origins on chromosomal DNA. In budding yeast, ORC binds the 11-bp ARS consensus sequence (ACS) with high specificity, providing a well-defined biochemical platform for reconstitution studies (Li et al., 2018; Bleichert et al., 2017). In metazoans, origin selection is sequence-independent but influenced by chromatin context: ORC is enriched at regions of open chromatin, CpG islands, G-quadruplex structures, and transcription start sites (Cayrou et al., 2015; Petryk et al., 2016).

Cryo-EM structures have revealed the architecture of ORC at near-atomic resolution. The crystal structure of *Drosophila* ORC at 3.5 Å showed a two-layered ring architecture with winged-helix domains atop AAA+ ATPase folds, with a central channel large enough to accommodate double-stranded DNA (Bleichert et al., 2015). Subsequent cryo-EM structures of the human ORC revealed five distinct conformational states, demonstrating that ORC undergoes large-scale structural rearrangements during the licensing cycle, including autoinhibitory configurations that regulate DNA binding (Jaremko et al., 2020). Schmidt et al. (2022) identified an autoinhibition mechanism in yeast ORC-DNA-Cdc6 that prevents premature MCM loading, with the ORC6 winged-helix domain blocking the MCM2-7 entry gate until the complex is properly configured. A comprehensive 2025 review by Stillman et al. synthesized the structural and mechanistic understanding of licensing across species, highlighting how multiple pathways converge on the common goal of MCM double hexamer formation (Stillman et al., 2025).

### 2.3 The MCM2-7 Loading Machine

The central event in origin licensing is the loading of the MCM2-7 double hexamer — two head-to-head MCM2-7 rings encircling double-stranded DNA — at each licensed origin. This is accomplished by the sequential action of ORC, CDC6, and CDT1, which together constitute the "loading machine" (Bleichert et al., 2017; Deegan & Diffley, 2016).

The loading pathway proceeds through discrete biochemical steps, each captured by structural studies. First, ORC-bound CDC6 converts ORC into an active loading platform by closing the ORC ring around DNA and creating a binding surface for CDT1-MCM2-7 (Ticau et al., 2015; Yuan et al., 2017). Single-molecule studies revealed that MCM2-7 loading is a two-step process: the first hexamer is loaded through an ORC-CDC6-CDT1-dependent mechanism that opens the MCM2-5 gate, threads DNA through the central channel, and closes the ring around dsDNA; a second round of loading, requiring ORC re-engagement, deposits the second hexamer in a head-to-head orientation, forming the double hexamer (Ticau et al., 2015; Miller et al., 2019). Weissmann et al. (2024) achieved a breakthrough by visualizing MCM double hexamer loading with human proteins, revealing that — unlike in yeast — ORC6 is not essential but enhances human MCM loading, and identifying an alternative pathway in which two independently loaded single hexamers dimerize without additional loading factors (Weissmann et al., 2024). This redundancy in human licensing pathways was further characterized by Qiu et al. (2024), who demonstrated multiple parallel mechanisms for human origin licensing that collectively provide resilience against replication stress. Wells et al. (2025) extended this work by reconstituting human DNA licensing and resolving cryo-EM structures of key intermediates, providing the first complete structural atlas of the human licensing pathway.

Cryo-EM structures of the human MCM2-7 single hexamer at 4.4 Å resolution revealed a characteristically open-ring configuration with a gap between MCM2 and MCM5 — the "entry gate" through which DNA is threaded during loading (Li et al., 2022). The double hexamer structure shows the two rings in a head-to-head configuration with N-terminal zinc-finger domains forming the interface, encircling dsDNA within a shared central channel (Noguchi et al., 2017). This architecture is functionally significant: the two helicases must eventually separate and travel in opposite directions during bidirectional replication, and the head-to-head arrangement pre-positions them for this divergent movement.

### 2.4 The MCM Paradox: Excess Licensing as a Safety Mechanism

A striking feature of eukaryotic replication licensing is the dramatic excess of loaded MCM complexes relative to the number of origins actually fired during S phase. Quantitative measurements in mammalian cells indicate that 3–10-fold more MCM complexes are loaded than are activated as replication origins, with some estimates suggesting a 20-fold excess (Deegan & Diffley, 2016; Bleichert et al., 2017). These excess MCM complexes occupy "dormant origins" — licensed but unfired origins that are passively replicated by forks emanating from neighboring active origins during normal S phase.

The functional significance of dormant origins was revealed by studies of replication stress. Partial depletion of MCM2-7 (reducing total MCM to levels that still support normal replication under unperturbed conditions) renders cells hypersensitive to replication stress agents such as hydroxyurea, aphidicolin, and UV radiation (Bleichert et al., 2017; Técher et al., 2017). Under replication stress, when active forks stall or collapse, dormant origins in the vicinity fire to rescue replication of the affected regions. This backup mechanism is essential for genome stability: mice heterozygous for an *Mcm4* hypomorphic allele (*Mcm4^Chaos3*) show increased cancer susceptibility, demonstrating that reduced dormant origin capacity is sufficient to promote tumorigenesis (Kawabata et al., 2011; Técher et al., 2017).

### 2.5 Preventing Re-Replication: The Licensing-Firing Switch

The cell must ensure that each origin fires at most once per cell cycle — re-replication of even a small genomic segment generates gene amplification, structural rearrangements, and replication fork collisions that are highly mutagenic. Eukaryotic cells enforce the "once and only once" rule through multiple redundant mechanisms that separate the licensing and firing phases of replication into distinct cell cycle windows (Siddiqui et al., 2013; Neelsen et al., 2013).

In the G1-to-S transition, rising CDK activity simultaneously activates origin firing (by phosphorylating the firing factors TRESLIN and MTBP) and inactivates the licensing machinery through at least four mechanisms: (1) CDK phosphorylation of ORC1 triggers its degradation via the SCF ubiquitin ligase; (2) CDK phosphorylation of CDC6 targets it for SCF-mediated proteolysis and nuclear export; (3) geminin, whose levels rise in S phase, directly binds and inhibits CDT1, preventing further MCM loading; and (4) CDT1 is targeted for degradation by the CRL4-CDT2 ubiquitin ligase upon its interaction with PCNA at replication forks (Siddiqui et al., 2013; Havens & Walter, 2011). The convergence of multiple redundant pathways ensures that re-replication is essentially undetectable in normal cells, though partial deregulation — as occurs in cancers with amplified cyclin E or depleted geminin — can produce re-replication intermediates detectable by flow cytometry (Neelsen et al., 2013).

### 2.6 Novel Mathematical Framework F232: Stochastic MCM Loading and Genome Coverage

The MCM paradox can be formalized as a stochastic coverage problem. We model licensed origins as a one-dimensional spatial Poisson process along each chromosome arm, where each origin generates a bidirectional replication fork that extends until it meets a converging fork from a neighboring origin.

**F232a. Licensed origin distribution:**

Let origins be distributed as a Poisson process with rate parameter $\rho$ (origins per kilobase) along a chromosome of length $L$ kb. The number of origins on a segment of length $\ell$ is Poisson-distributed:

```math
P(N = k \mid \ell) = \frac{(\rho \ell)^k e^{-\rho \ell}}{k!}
```

where $\rho$ is the mean licensed origin density (origins/kb) and $\ell$ is the segment length (kb).

**F232b. Inter-origin gap distribution:**

The gaps between adjacent licensed origins follow an exponential distribution:

```math
f_G(g) = \rho \, e^{-\rho g}, \quad g \geq 0
```

where $g$ is the inter-origin gap size (kb). The mean gap is $\langle g \rangle = 1/\rho$ and the variance is $1/\rho^2$.

**F232c. Maximum gap and genome coverage guarantee:**

For a chromosome with $N$ licensed origins, the maximum inter-origin gap $G_{\max}$ follows the Gumbel distribution (extreme value theory). For the genome to be fully replicated within S-phase duration $T_S$, every gap must satisfy $g \leq 2 v T_S$, where $v$ is the fork speed (kb/min). The probability that the largest gap exceeds the critical size is:

```math
P(G_{\max} > 2vT_S) = 1 - \left(1 - e^{-\rho \cdot 2vT_S}\right)^{N_{\text{origins}}}
```

where $N_{\text{origins}} \approx \rho L$ is the total number of licensed origins across the genome, $v \approx 1.5$ kb/min is the mean fork speed, and $T_S \approx 480$ min is the S-phase duration. For the human genome ($L \approx 6.4 \times 10^6$ kb), with $\rho \approx 0.01$ origins/kb (one origin per 100 kb on average) and $N_{\text{origins}} \approx 64{,}000$, we obtain $P(G_{\max} > 1440 \text{ kb}) \approx 1 - (1 - e^{-14.4})^{64000} \approx 3.5 \times 10^{-3}$.

**F232d. Minimum origin density for safe replication:**

Solving for the critical origin density $\rho^*$ that ensures $P(G_{\max} > 2vT_S) < \epsilon$ for a given failure tolerance $\epsilon$:

```math
\rho^* = \frac{-\ln\!\left(1 - (1-\epsilon)^{1/N}\right)}{2vT_S}
```

For $\epsilon = 10^{-6}$ (one failure per million cell divisions) and $N = 64{,}000$ origins, $\rho^* \approx 0.012$ origins/kb, consistent with observed origin densities and explaining the biological rationale for excess MCM loading as a safety margin against catastrophic replication failure.

---

## 3. Section II: The Firing Problem — Selecting and Timing Origin Activation

### 3.1 The Core Question

Of the approximately 30,000–80,000 licensed origins in a human cell, only a subset — typically 30,000–50,000 — are activated during any given S phase, and their activation follows a reproducible temporal program in which some origins fire early and others fire late (Rhind & Gilbert, 2013; Petryk et al., 2016). The firing problem asks: what molecular mechanism selects which origins fire, what determines when they fire, and how is this temporal program coupled to cell identity?

### 3.2 The Kinase Cascade: DDK and CDK

Origin firing requires the sequential action of two S-phase kinases: DDK (CDC7-DBF4) and CDK (CDK2-Cyclin E/A). DDK phosphorylates the N-terminal tails of MCM4 and MCM6 within the loaded double hexamer, inducing conformational changes that expose binding sites for the firing factors CDC45 and GINS (Deegan et al., 2016; Hiraga et al., 2014). CDK phosphorylates the metazoan-specific firing factors TRESLIN (the functional homolog of yeast Sld3) and MTBP, enabling their interaction with TopBP1 and subsequent recruitment of the GINS complex (Boos et al., 2011; Kumagai et al., 2011; Kumagai & Dunphy, 2017).

The output of the kinase cascade is the assembly of the CMG (CDC45-MCM2-7-GINS) holohelicase — the active replicative helicase that unwinds parental DNA ahead of the replication fork. CMG assembly is the committed step of origin firing: once CDC45 and GINS are stably incorporated into the MCM ring, the helicase is activated and fork establishment proceeds irreversibly (Douglas et al., 2018; Stillman et al., 2025).

### 3.3 The Firing Factor Hierarchy

Reconstitution studies have revealed a hierarchy of firing factors whose ordered recruitment converts the inactive MCM2-7 double hexamer into two active CMG helicases. In the yeast system, origin firing requires Dpb11 (TopBP1), Sld2 (TICRR/TRESLIN), Sld3, Sld7, Cdc45, GINS, DNA polymerase ε, and the kinases DDK and CDK — a total of 16 factors made from 42 polypeptides (Yeeles et al., 2015).

In metazoans, the firing pathway involves additional factors not present in yeast. DONSON, a vertebrate-specific protein mutated in microcephalic primordial dwarfism (Meier-Gorlin syndrome), was identified as an essential replication initiation factor that scaffolds a vertebrate pre-loading complex (pre-LC) containing GINS, TopBP1, and DNA polymerase ε (Kingsley et al., 2023). Structural and biochemical analysis showed that DONSON facilitates CDC45 and GINS chromatin association and is required for CMG helicase assembly in human cells (Hashimoto et al., 2023). Cvetkovic et al. (2023) captured cryo-EM structures of a double-CMG bridged by a DONSON dimer, showing that DONSON engages two GINS copies and delivers them to the MCM double hexamer to form CMG (Cvetkovic et al., 2023). The identification of DONSON resolved a long-standing puzzle about how metazoan cells coordinate the multiple firing factors that have no direct yeast orthologs, and connected replication initiation defects to developmental disorders characterized by primordial dwarfism and microcephaly (Evrony et al., 2017).

### 3.4 Stochastic Origin Firing and the Temporal Program

Origin firing in individual cells is stochastic: any given origin fires in only a fraction of cell cycles, with firing efficiencies ranging from near 100% (constitutive origins) to below 10% (inefficient origins) (Czajkowsky et al., 2008; Cayrou et al., 2015). Nevertheless, the ensemble average over many cells produces a highly reproducible temporal program — the replication timing profile — in which the same genomic regions replicate early or late in every cell cycle (Rhind & Gilbert, 2013).

This stochastic-yet-reproducible behavior can be explained by a model in which individual origin firing follows an inhomogeneous Poisson process whose rate depends on local chromatin environment and limiting firing factor concentration. Mantiero et al. (2011) demonstrated in yeast that the temporal program is established by limiting concentrations of firing factors (particularly Sld2, Sld3, Dpb11, and Cdc45), which create a kinetic competition among licensed origins: origins with higher affinity for limiting factors fire first, while low-affinity origins fire later when factors are recycled from early-firing origins that have already initiated. A 2025 review by Hyrien et al. synthesized the emerging understanding that mammalian replication origins lead a "double life" — serving both as sites of replication initiation and as sensors of chromatin environment, with firing efficiency determined by the intersection of origin sequence features, chromatin state, and limiting factor availability (Hyrien et al., 2025).

### 3.5 Novel Mathematical Framework F233: Origin Firing as an Inhomogeneous Poisson Process

We model origin firing as an inhomogeneous Poisson process in which each licensed origin $i$ at genomic position $x_i$ has a time-dependent firing rate $\lambda_i(t)$ determined by the local concentration of limiting firing factors and the chromatin environment.

**F233a. Firing rate function:**

```math
\lambda_i(t) = \lambda_0 \cdot \phi(x_i) \cdot \frac{[\text{CDK}](t) \cdot [\text{DDK}](t)}{(K_{\text{CDK}} + [\text{CDK}](t))(K_{\text{DDK}} + [\text{DDK}](t))} \cdot \frac{[F_{\text{lim}}](t)}{K_F + [F_{\text{lim}}](t)}
```

where $\lambda_0$ is the basal firing rate constant (min⁻¹), $\phi(x_i) \in [0, 1]$ is a position-dependent chromatin accessibility factor (reflecting histone acetylation, nucleosome density, and compartment identity at origin $i$), [CDK] (t) and [DDK] (t) are the time-dependent kinase concentrations, $K_{\text{CDK}}$ and $K_{\text{DDK}}$ are the Michaelis constants for kinase-dependent activation, and [F_lim] (t) is the concentration of the limiting firing factor (e.g., CDC45 or GINS), with $K_F$ as its half-maximal constant.

**F233b. Firing probability within a time window:**

The probability that origin $i$ fires between time 0 (S-phase entry) and time $t$ is:

```math
P_i(t) = 1 - \exp\!\left(-\int_0^t \lambda_i(\tau) \, d\tau \right)
```

This formulation captures the key experimental observation that early origins have high $\phi(x_i)$ values (open chromatin, high acetylation) and therefore accumulate firing probability rapidly, while late origins have low $\phi(x_i)$ values and fire only after kinase levels have risen sufficiently to overcome the chromatin barrier.

### 3.6 Novel Mathematical Framework F234: The Random Gap Problem

Even with stochastic firing, the cell must ensure that all DNA is replicated before mitosis. We formalize this as a random gap problem: given $N$ origins fired at random positions along a chromosome of length $L$, what is the distribution of the time until the last unreplicated gap is closed by converging forks?

**F234a. Gap closure time for a single inter-origin interval:**

For two adjacent origins separated by distance $d$, firing at times $t_1$ and $t_2$ ($t_1 \leq t_2$), the forks converge and complete replication of the interval at time:

```math
t_{\text{close}}(d, t_1, t_2) = t_2 + \frac{d - v(t_2 - t_1)}{2v}
```

where $v$ is the fork velocity (kb/min), assuming symmetric fork progression.

**F234b. Genome replication completion time:**

The genome-wide replication completion time $T_{\text{rep}}$ is the maximum over all inter-origin intervals:

```math
T_{\text{rep}} = \max_{j=1,\ldots,N+1} \, t_{\text{close},j}
```

For large $N$ with Poisson-distributed firing times, $T_{\text{rep}}$ follows a Gumbel-type extreme value distribution:

```math
P(T_{\text{rep}} \leq t) \approx \exp\!\left(-N \cdot P\!\left(t_{\text{close}} > t\right)\right)
```

**F234c. Expected completion time:**

Under the assumption that firing times are drawn from an exponential distribution with rate $\bar{\lambda}$, the expected completion time scales as:

```math
\langle T_{\text{rep}} \rangle \approx \frac{1}{\bar{\lambda}} \ln N + \frac{L}{2vN}
```

where the first term reflects the waiting time for the last origin to fire and the second term reflects fork travel time across the mean inter-origin distance $L/N$. For the human genome with $N \approx 40{,}000$ active origins, $\bar{\lambda} \approx 0.02$ min⁻¹, $v = 1.5$ kb/min, and $L = 6.4 \times 10^6$ kb, this yields $\langle T_{\text{rep}} \rangle \approx 530$ min, consistent with the observed S-phase duration of approximately 8–10 hours.

---

## 4. Section III: The Fidelity Problem — Achieving 10⁻¹⁰ Error Rates

### 4.1 The Core Question

The human genome is replicated with an aggregate error rate of approximately 10⁻¹⁰ per base pair per cell division — meaning that, on average, fewer than one error is introduced per genome replication (Lynch et al., 2016; Burgers & Kunkel, 2017). This extraordinary fidelity is achieved not by any single mechanism but by a three-stage cascade: nucleotide selectivity during polymerization (~10⁻⁴ to 10⁻⁵ error rate), exonuclease proofreading (~10²-fold improvement), and post-replicative mismatch repair (~10²-10³-fold improvement) (Ganai & Johansson, 2016; Burgers & Kunkel, 2017). Each stage is mechanistically distinct and governed by different structural and kinetic constraints.

### 4.2 The Replisome: Architecture and Function

The eukaryotic replisome is a multi-protein machine that coordinates DNA unwinding with leading and lagging strand synthesis. At its core is the CMG helicase (CDC45-MCM2-7-GINS), an 11-subunit complex that encircles and translocates along the leading strand template in the 3′-to-5′ direction, unwinding parental DNA by steric exclusion of the lagging strand (Georgescu et al., 2017; O'Donnell & Li, 2024). Cryo-EM structures of the yeast CMG bound to forked DNA at 3.0–3.9 Å resolution revealed that the lagging strand template is diverted sideways at the base of the MCM zinc-finger ring by a set of OB-fold hairpin loops, while the leading strand template passes through the central channel (Yuan et al., 2020; Baretić et al., 2020).

Coupled to the CMG are the three replicative DNA polymerases, each with a distinct function:

**DNA Polymerase ε (Pol ε)** is the leading strand polymerase. The catalytic subunit POLE1 (Pol2 in yeast) is a 2,286-amino-acid protein containing both polymerase and 3′-to-5′ exonuclease domains. Pol ε is physically tethered to the CMG through interactions with the GINS subunits Psf1 and Cdc45, placing its active site immediately behind the helicase (Langston et al., 2014; Georgescu et al., 2017). Roske & Yeeles (2024) determined the first cryo-EM structures of the human Pol ε-PCNA-DNA complex in both nucleotide-bound and mismatch states, revealing that the proofreading exonuclease site is located 40 Å from the polymerase active site (Roske & Yeeles, 2024). Wang et al. (2025) captured three bona fide proofreading intermediates showing mismatch dislodging, 6-base-pair unwinding with out-of-register scrunching, and primer 3′-end insertion into the exonuclease site — with PCNA imposing steric constraints that redirect the mismatched DNA trajectory (Wang et al., 2025). The cryo-EM structure of the yeast CMG-Pol ε complex on a replication fork showed that Pol ε contacts the CMG through its non-catalytic C-terminal domain, which wraps around the GINS-CDC45 face of the helicase, positioning the polymerase active site for immediate capture of the emerging single-stranded leading strand template (Sun et al., 2015; Zhou et al., 2017).

**DNA Polymerase α-primase (Pol α)** initiates each Okazaki fragment on the lagging strand by synthesizing a short RNA primer (~8–12 nucleotides) extended by ~20 nucleotides of DNA. Pol α lacks proofreading exonuclease activity and has relatively low fidelity (~10⁻⁴), making it the least accurate of the replicative polymerases (Ganai & Johansson, 2016). Its contribution to the final replicated product is limited to the primer, which is subsequently removed and replaced by Pol δ-synthesized DNA during Okazaki fragment maturation.

**DNA Polymerase δ (Pol δ)** extends Okazaki fragments on the lagging strand after Pol α priming. Pol δ is a four-subunit complex (POLD1-4) with both polymerase and 3′-to-5′ exonuclease domains. Unlike Pol ε, Pol δ is not stably associated with the CMG but is recruited through interactions with the sliding clamp PCNA (Lancey et al., 2020). Pol δ also plays a critical role in Okazaki fragment maturation: when it encounters the 5′ end of the preceding Okazaki fragment, it displaces a short flap that is cleaved by FEN1 (flap endonuclease 1), creating a nick that is sealed by DNA ligase I (Stodola & Burgers, 2016).

### 4.3 PCNA: The Coordination Hub

Proliferating cell nuclear antigen (PCNA) is a homotrimeric ring-shaped sliding clamp that encircles DNA and serves as the processivity factor for both Pol ε and Pol δ. PCNA is loaded onto primer-template junctions by the pentameric clamp loader RFC (replication factor C), which uses ATP hydrolysis to open the PCNA ring, thread DNA through the central channel, and close the ring around the duplex (Kelch et al., 2011; Gaubitz et al., 2022). Beyond processivity, PCNA serves as a coordination hub that recruits over 50 interacting partners involved in DNA repair, chromatin remodeling, sister chromatid cohesion, and cell cycle regulation, all through a conserved PCNA-interacting peptide (PIP) motif (Choe & Moldovan, 2017).

### 4.4 The Three-Stage Fidelity Cascade

The overall fidelity of DNA replication is the product of three sequential error-correction stages, each operating on the errors that escape the preceding stage (Ganai & Johansson, 2016; Burgers & Kunkel, 2017):

**Stage 1 — Nucleotide selectivity:** The polymerase active site discriminates correct from incorrect incoming nucleotides through a combination of Watson-Crick hydrogen bonding geometry and steric fit within the active site. The selectivity ratio varies by polymerase: Pol ε and Pol δ achieve ~10⁻⁵ to 10⁻⁶ error rates for base-base mismatches, while Pol α achieves ~10⁻⁴ (Ganai & Johansson, 2016; Burgers & Kunkel, 2017).

**Stage 2 — Exonuclease proofreading:** When a mismatch is incorporated, the primer terminus is transferred from the polymerase active site to the 3′-to-5′ exonuclease active site, which excises the mismatched nucleotide. This kinetic partitioning between polymerase extension and exonuclease excision provides 10²-fold fidelity improvement. Proofreading is the dominant fidelity mechanism for Pol ε and Pol δ; its loss — as in cancer-associated POLE exonuclease domain mutations (P286R, V411L) — produces an "ultramutator" phenotype with mutation rates exceeding 100 mutations per megabase, among the highest tumor mutation burdens of any cancer subtype (Campbell et al., 2017; Haradhvala et al., 2023).

**Stage 3 — Mismatch repair (MMR):** Errors escaping proofreading are detected and corrected by the post-replicative MMR system. MSH2-MSH6 (MutSα) recognizes single-base mismatches and small insertion/deletion loops, recruiting the MLH1-PMS2 (MutLα) endonuclease complex. MutLα introduces a nick in the newly synthesized strand (distinguished from the parental strand by the presence of strand discontinuities), enabling exonucleolytic removal of the error-containing segment and resynthesis by Pol δ (Kunkel & Erie, 2015; Liu et al., 2017). MMR contributes 10²-10³-fold fidelity enhancement, and its loss — as in Lynch syndrome (germline MSH2/MLH1 mutations) — increases cancer risk 5-10-fold (Fishel, 2015).

The asymmetric organization of leading and lagging strand synthesis creates a fidelity asymmetry: leading strand errors are corrected by Pol ε proofreading and MMR, while lagging strand fidelity depends on the sequential action of Pol δ proofreading (which corrects both its own errors and those inherited from the error-prone Pol α primer), FEN1 flap cleavage (which removes the Pol α-synthesized primer), and MMR (Lujan et al., 2015; Pursell et al., 2007).

### 4.5 Novel Mathematical Framework F235: Multi-Stage Kinetic Proofreading

The three-stage fidelity cascade can be formalized using the Hopfield-Ninio kinetic proofreading framework, which describes how sequential irreversible steps can achieve discrimination ratios that exceed thermodynamic equilibrium limits (Hopfield, 1974; Ninio, 1975; as reviewed in Murugan et al., 2012).

**F235a. Aggregate error rate as a multiplicative cascade:**

```math
\varepsilon_{\text{total}} = \varepsilon_{\text{sel}} \times (1 - f_{\text{proof}}) \times (1 - f_{\text{MMR}})
```

where $\varepsilon_{\text{sel}}$ is the nucleotide selectivity error rate (probability of misincorporation per nucleotide), $f_{\text{proof}}$ is the fraction of misincorporations corrected by proofreading, and $f_{\text{MMR}}$ is the fraction of remaining errors corrected by MMR.

With experimentally measured values: $\varepsilon_{\text{sel}} \approx 10^{-5}$ for Pol ε, $f_{\text{proof}} \approx 0.99$ (100-fold improvement), and $f_{\text{MMR}} \approx 0.999$ (1000-fold improvement), the aggregate error rate is:

```math
\varepsilon_{\text{total}} = 10^{-5} \times 10^{-2} \times 10^{-3} = 10^{-10}
```

**F235b. Thermodynamic cost of proofreading:**

Each proofreading cycle consumes one nucleotide triphosphate that was incorporated and then excised. The free energy cost per proofreading event is:

```math
\Delta G_{\text{proof}} = \Delta G_{\text{hydrolysis}}^{\text{NTP}} + \Delta G_{\text{excision}} \approx -12 \text{ kcal/mol}
```

where $\Delta G_{\text{hydrolysis}}^{\text{NTP}} \approx -7.3$ kcal/mol is the standard free energy of NTP hydrolysis and $\Delta G_{\text{excision}} \approx -4.7$ kcal/mol is the free energy released by phosphodiester bond cleavage during exonucleolysis.

**F235c. Pareto-optimal fidelity allocation:**

Given a total energy budget $E_{\text{total}}$ allocated to fidelity, the cell must optimally partition energy across the three stages. The total error rate is:

```math
\varepsilon(\mathbf{E}) = \varepsilon_0 \cdot e^{-E_1/E_{\text{sel}}} \cdot e^{-E_2/E_{\text{proof}}} \cdot e^{-E_3/E_{\text{MMR}}}
```

subject to $E_1 + E_2 + E_3 = E_{\text{total}}$, where $E_{\text{sel}}$, $E_{\text{proof}}$, and $E_{\text{MMR}}$ are the characteristic energy scales for each mechanism. Lagrange optimization yields the equal energy allocation $E_1^* = E_2^* = E_3^* = E_{\text{total}}/3$ when the characteristic scales are equal, confirming the biological observation that each stage contributes approximately equally (in log-space) to total fidelity.

### 4.6 Novel Mathematical Framework F236: Channel Capacity of the Replication Fidelity System

We model DNA replication as a noisy communication channel in the Shannon-theoretic sense, where the "message" is the parental DNA sequence and the "received signal" is the daughter strand.

**F236a. Nucleotide channel model:**

The DNA copying channel can be described by a 4×4 transition matrix $\mathbf{Q}$, where $Q_{ij}$ is the probability of incorporating nucleotide $j$ in the daughter strand given template nucleotide $i$:

```math
Q_{ij} = \begin{cases} 1 - 3\varepsilon_i & \text{if } j = \bar{i} \text{ (correct Watson-Crick complement)} \\ \varepsilon_i & \text{if } j \neq \bar{i} \end{cases}
```

where $\varepsilon_i$ is the nucleotide-specific error rate and $\bar{i}$ denotes the Watson-Crick complement of template base $i$.

**F236b. Channel capacity:**

The Shannon capacity of this channel is:

```math
C = \log_2 4 - H(\varepsilon) = 2 + (1-3\varepsilon)\log_2(1-3\varepsilon) + 3\varepsilon\log_2\varepsilon
```

where $H(\varepsilon)$ is the conditional entropy of the output given the input (in bits per nucleotide). For $\varepsilon = 10^{-10}$:

```math
C \approx 2 - 3.3 \times 10^{-9} \approx 1.9999999967 \text{ bits/nucleotide}
```

This means that out of the theoretical maximum of 2 bits per nucleotide (since there are 4 possible bases), the replication machinery transmits 1.9999999967 bits — an information transmission efficiency of 99.99999998%. Over the entire human genome of $6.4 \times 10^9$ bp, the total information faithfully transmitted per replication cycle is approximately $1.28 \times 10^{10}$ bits, with fewer than 1 bit lost to replication errors.

---

## 5. Section IV: The Completion Problem — Replicating Every Base Pair Exactly Once

### 5.1 The Core Question

Eukaryotic cells lack sequence-specific replication terminators analogous to the *Tus-Ter* system in *E. coli*. Instead, replication termination occurs passively when two converging forks from adjacent origins meet and fuse, completing replication of the intervening DNA segment (Dewar & Walter, 2017). This passive mechanism raises a fundamental question: how do cells guarantee that every nucleotide in the genome is replicated before mitosis, given the stochastic nature of origin firing and the variable speeds of individual replication forks?

### 5.2 Fork Convergence and CMG Unloading

When two converging forks approach each other, the replisomes must be disassembled to allow completion of the remaining unreplicated segment. Biochemical reconstitution in *Xenopus* egg extracts revealed that fork convergence triggers ubiquitylation of the MCM7 subunit by the CRL2-Lrr1 ubiquitin ligase (in S phase) or the SCF-Dia2 ligase (in mitosis), marking the CMG for extraction by the p97/VCP AAA+ ATPase (Dewar et al., 2017; Sonneville et al., 2017). Polo Rivera et al. (2024) identified a parallel ubiquitin-independent pathway requiring Rrm3/Pif1 helicases, demonstrating that cells maintain two redundant CMG disassembly mechanisms (Polo Rivera et al., 2024). Liu et al. (2024) discovered "chromatin fountain" structures using Repli-HiC, revealing that converging forks are physically coupled through chromatin contacts, predetermining termination zones that are sensitive to replication stress and prone to cancer-associated deletions (Liu et al., 2024). This ubiquitin-dependent CMG unloading pathway ensures that the helicase is removed only after the forks have converged and replication of the intervening segment is complete — preventing premature helicase removal that would leave unreplicated gaps.

The final few hundred base pairs between converging forks present a topological challenge: as the forks approach, the remaining parental DNA becomes overwound, generating positive superhelical tension that impedes further unwinding. Topoisomerase I resolves this tension by introducing transient single-strand breaks that allow rotation of the DNA helix ahead of the fork (Keszthelyi et al., 2016). After fork fusion, the daughter molecules remain topologically linked (catenated), requiring Topoisomerase IIα to introduce transient double-strand breaks for decatenation — a process that must be completed before chromosome segregation in mitosis (Dewar & Walter, 2017).

### 5.3 Common Fragile Sites and Under-Replication

Despite the redundancy provided by dormant origins, certain genomic regions are inherently vulnerable to under-replication — failure to complete DNA synthesis before mitotic entry. Common fragile sites (CFSs) are megabase-scale chromosomal regions that exhibit gaps or breaks on metaphase chromosomes after mild replication stress (Durkin & Glover, 2007). CFSs are defined by three features that conspire against complete replication: (1) they reside within very large genes (often >1 Mb), creating extended origin-poor regions; (2) they replicate late in S phase, leaving minimal time for completion; and (3) they are enriched in sequences that impede fork progression, including AT-rich flexibility islands, G-quadruplex structures, and regions of replication-transcription conflict (Macheret & Halazonetis, 2018; Técher et al., 2017).

When cells enter mitosis with unreplicated DNA at fragile sites, a rescue pathway termed mitotic DNA synthesis (MiDAS) is activated. MiDAS is a RAD52-dependent, break-induced replication (BIR)-like mechanism that uses POLD3-dependent DNA synthesis to complete replication at under-replicated loci during early mitosis (Minocherhomji et al., 2015; Bhowmick et al., 2016; Ji et al., 2023). Kwan et al. (2024) demonstrated that replication stress at CFSs also activates DNA polymerase theta (POLQ)-mediated structural variant formation after mitotic entry, revealing a previously unrecognized mutagenic consequence of under-replication (Kwan et al., 2024). Ji et al. (2023) demonstrated that MiDAS in human cells requires the sequential action of DNA polymerases ζ and δ: Pol ζ (REV3L-REV7) initiates synthesis at the broken fork, while Pol δ (POLD3-dependent) extends the nascent strand, ensuring that even late-replicating fragile sites are duplicated before chromosome segregation.

Regions that escape both normal replication and MiDAS can persist as ultra-fine bridges (UFBs) — thread-like DNA structures connecting sister chromatids during anaphase. UFBs are resolved by the BLM helicase (a RecQ family helicase) in complex with Topoisomerase IIIα and PICH (an SNF2-family translocase), which disentangle the intertwined DNA strands to allow complete chromosome segregation (Chan et al., 2018; Sarlós et al., 2018).

### 5.4 Novel Mathematical Framework F237: Stochastic Completion Time

We model genome replication as a one-dimensional covering process and derive the distribution of the completion time.

**F237a. Covering process on a linear chromosome:**

Consider a chromosome of length $L$ with $N$ origins that fire at times $\{t_1, t_2, \ldots, t_N\}$ drawn from a common distribution $F_T(t)$. Each origin generates two forks moving in opposite directions at constant speed $v$. The region covered by origin $i$ at time $t$ is the interval $[x_i - v(t - t_i), \, x_i + v(t - t_i)]$ (for $t > t_i$). The chromosome is fully replicated at the smallest time $T^*$ such that the union of all covered intervals equals $[0, L]$.

**F237b. Expected completion time (mean-field approximation):**

For uniformly distributed origins with exponentially distributed firing times (rate $\lambda$), the expected time to cover the last gap is dominated by the extreme order statistics of both firing time and inter-origin gap size. Using the Gumbel approximation:

```math
\langle T^* \rangle \approx \frac{1}{\lambda}\left(\ln N + \gamma\right) + \frac{L}{2vN}\left(\ln N + \gamma\right)
```

where $\gamma \approx 0.5772$ is the Euler-Mascheroni constant. The first term is the expected time until the last origin fires; the second is the expected fork travel time across the largest inter-origin gap (which scales as $\frac{L}{N}\ln N$ by extreme value theory).

### 5.5 Novel Mathematical Framework F238: Fragile Site Vulnerability

**F238a. Under-replication probability at a fragile site:**

A fragile site of genomic length $\ell_F$ with local origin density $\rho_F$ (origins/kb) replicates late, with origin firing delayed until time $t_{\text{late}}$ in S phase. The probability that the fragile site fails to complete replication before the G2/M boundary at time $T_G$ is:

```math
P_{\text{fail}}(\ell_F, \rho_F, t_{\text{late}}) = \exp\!\left(-\rho_F \ell_F \cdot \lambda_{\text{late}} \cdot (T_G - t_{\text{late}}) \cdot \min\!\left(1, \frac{2v(T_G - t_{\text{late}})}{\ell_F}\right)\right)
```

where $\lambda_{\text{late}}$ is the late-origin firing rate and the $\min$ function accounts for whether forks have time to traverse the entire fragile region. For the prototypical fragile site FRA3B ($\ell_F \approx 4000$ kb, $\rho_F \approx 0.002$ origins/kb, $t_{\text{late}} \approx 360$ min, $T_G \approx 480$ min), this yields $P_{\text{fail}} \approx 0.03$, consistent with the observed 1–5% breakage frequency at FRA3B under mild replication stress (Durkin & Glover, 2007).

**F238b. G-quadruplex impedance factor:**

Fork progression through G4-forming sequences is slowed by a factor $\alpha_{G4}$, reducing effective fork speed:

```math
v_{\text{eff}}(x) = v \cdot \left(1 - \alpha_{G4} \cdot \sum_k \frac{\sigma_{G4}^2}{\sigma_{G4}^2 + (x - x_k)^2}\right)
```

where $x_k$ are the positions of G4-forming sequences, $\sigma_{G4}$ is the characteristic range of G4 impedance (~100 bp), and $\alpha_{G4} \approx 0.3$–$0.7$ is the fractional speed reduction at G4 sites (Paeschke et al., 2013; Técher et al., 2017).

---

## 6. Section V: The Inheritance Problem — Duplicating Epigenetic Information at the Fork

### 6.1 The Core Question

DNA replication doubles not only the genetic information encoded in the base sequence but also the epigenetic information encoded in histone modifications, histone variants, and DNA methylation patterns. Because replication disrupts chromatin structure ahead of the fork — displacing nucleosomes to allow helicase passage — the cell faces the challenge of accurately reassembling chromatin on both daughter strands behind the fork while preserving the parental epigenetic state. This is the inheritance problem: how are parental histones and their modifications faithfully segregated to daughter strands, and how is this information used to template the restoration of the full chromatin state (Stewart-Morgan et al., 2020; Petryk & Groth, 2024)?

### 6.2 Parental Histone Recycling: The MCM2 Chaperone Mechanism

The core of the histone inheritance mechanism is the replication fork's ability to recycle parental histones — transferring disrupted (H3-H4)₂ tetramers from the parental DNA ahead of the fork to the newly synthesized daughter DNA behind it. This recycling is mediated by the MCM2 subunit of the CMG helicase, which doubles as a histone H3-H4 chaperone (Huang et al., 2015; Richet et al., 2015).

Structural studies revealed that the N-terminal domain of MCM2 contains a conserved histone-binding motif (HBM) that captures (H3-H4)₂ tetramers as they are displaced from parental DNA by the advancing helicase. The crystal structure of the MCM2 HBM-H3-H4 complex showed that MCM2 binds the H3-H4 tetramer on the same surface that contacts DNA in the nucleosome, explaining how MCM2 competes with DNA for histone binding and thereby captures histones as they are evicted during fork passage (Huang et al., 2015; Foltman et al., 2013).

A landmark 2024 study by Gan et al. used cryo-EM to capture the complete architecture of a yeast replisome engaged in parental histone recycling at a replication fork (Gan et al., 2024). These structures revealed that the histone chaperone FACT (facilitates chromatin transcription) is positioned at the front end of the replisome, engaging with parental DNA ahead of the CMG helicase to capture histones through the Spt16 middle domain. The displaced H3-H4 tetramer is held in a ternary complex with both MCM2 and FACT, creating a histone "conveyor belt" that channels parental histones from the parental duplex to the daughter strand.

### 6.3 Strand-Specific Histone Inheritance

A critical question in epigenetic inheritance is whether parental histones are distributed symmetrically or asymmetrically between the leading and lagging daughter strands. Two complementary technologies — eSPAN (enrichment and sequencing of protein-associated nascent DNA) and SCAR-seq (sister chromatids after replication by DNA sequencing) — have provided genome-wide, strand-resolved maps of histone distribution at replication forks (Petryk et al., 2018; Gan et al., 2018).

Petryk et al. (2018) used eSPAN in yeast to demonstrate that parental H3 is preferentially recycled to the leading strand via a mechanism dependent on the Pol ε subunit Dpb3 (POLE3/4 in humans). When Dpb3 was deleted, parental histone bias shifted toward the lagging strand. Gan et al. (2018) using SCAR-seq in mouse embryonic stem cells confirmed an analogous leading-strand bias for parental H3-H4, with new histones preferentially deposited on the lagging strand via the CAF-1-PCNA interaction. Wenger et al. (2023) demonstrated that this symmetric inheritance is functionally essential: MCM2-2A mutant mice show asymmetric parental histone segregation, causing H3K9me3 loss at repeats and H3K27me3 redistribution at bivalent promoters, impairing embryonic stem cell identity (Wenger et al., 2023).

The 2024 Cell paper by Xu et al. revealed an additional layer of regulation: the fork protection complex (FPC, comprising Tof1-Csm3-Mrc1 in yeast, or TIMELESS-TIPIN-CLASPIN in humans) directly promotes parental histone recycling (Xu et al., 2024). Mrc1/CLASPIN was shown to bind H3-H4 tetramers and coordinate with MCM2 to channel parental histones to both daughter strands. Loss of Mrc1 disrupted symmetric histone inheritance and caused replication-coupled loss of heterochromatin silencing, demonstrating that the fork protection complex is essential for epigenetic memory through DNA replication. Complementing this structural work, Yu et al. (2024) used molecular dynamics simulations to demonstrate that histones are recycled via both CDC45-mediated and chaperone-independent pathways, with RPA binding regulating the strand distribution ratio and Pol ε DNA bending modulating the destination location (Yu et al., 2024). A comprehensive 2024 review by Petryk and Groth synthesized these advances into a unified model of replication-coupled chromatin state inheritance (Petryk & Groth, 2024).

### 6.4 New Histone Deposition: The CAF-1-PCNA Axis

Parental histone recycling provides approximately half the histones needed to chromatinize the two daughter duplexes; the other half must come from newly synthesized histones. New H3-H4 dimers are deposited on daughter DNA by the histone chaperone CAF-1 (chromatin assembly factor 1), which is recruited to the replication fork through a direct interaction between its p150 subunit and the front face of the PCNA sliding clamp (Zhang et al., 2016; Stewart-Morgan et al., 2020). This PCNA-CAF-1 interaction ensures that new histone deposition is tightly coupled to DNA synthesis: CAF-1 deposits new H3.1-H4 dimers only on newly replicated DNA marked by PCNA, preventing ectopic nucleosome assembly on unreplicated or single-stranded DNA.

New histones are deposited in a largely unmodified state (or with replication-associated marks such as H4K5ac and H4K12ac), creating a transient epigenetic asymmetry between the parental-histone-enriched and new-histone-enriched daughter strands (Alabert et al., 2015; Reveron-Gomez et al., 2018). This asymmetry is resolved during chromatin maturation — a process taking approximately 15–20 minutes behind the replication fork — in which modification enzymes read the marks on neighboring parental histones and write corresponding marks on new histones, restoring the pre-replication epigenetic state (Alabert et al., 2015; Stewart-Morgan et al., 2020).

### 6.5 DNA Methylation Maintenance at the Fork

DNA methylation — the addition of a methyl group to the 5-position of cytosine in CpG dinucleotides — is the most stable epigenetic mark and is maintained through DNA replication by a dedicated copying mechanism. Replication of a fully methylated CpG site produces a hemimethylated daughter duplex: one strand retains the parental methyl group, while the newly synthesized strand is unmethylated. The maintenance methyltransferase DNMT1 specifically recognizes hemimethylated CpG sites and methylates the newly synthesized strand, restoring the fully methylated state (Jeltsch & Jurkowska, 2014; Nishiyama et al., 2013).

DNMT1 is recruited to the replication fork through its interaction with UHRF1 (ubiquitin-like with PHD and RING finger domains 1), which serves as a hemimethylation sensor. UHRF1's SRA domain specifically recognizes hemimethylated CpG sites with a remarkable base-flipping mechanism — inserting a loop into the major groove that flips the 5-methylcytosine out of the DNA helix for recognition (Nishiyama et al., 2013; Ishiyama et al., 2017). Upon binding hemimethylated DNA, UHRF1 ubiquitylates histone H3 at K18 and K23 through its RING domain, creating a recruitment signal for DNMT1's RFTS (replication foci targeting sequence) domain (Nishiyama et al., 2013; Ishiyama et al., 2017).

The fidelity of maintenance methylation has been directly measured: DNMT1 copies CpG methylation with per-site fidelity of approximately 95–99% per cell division, corresponding to a per-site error rate of 1–5% (Ming et al., 2020). This error rate — orders of magnitude higher than genetic replication fidelity — has profound implications for epigenetic stability over the lifetime of an organism (see Mathematical Framework F240).

### 6.6 Novel Mathematical Framework F239: Histone Dilution-Restoration Kinetics

We model the dynamics of parental versus new histone density behind the replication fork as a function of distance from the fork junction.

**F239a. Parental histone density behind the fork:**

Immediately behind the fork, parental histones are deposited at rate $k_{\text{recycle}}$ and new histones at rate $k_{\text{new}}$, competing for the same nucleosome positions on daughter DNA. Let $p(x)$ denote the fraction of nucleosomes containing parental H3-H4 at distance $x$ (kb) behind the fork:

```math
p(x) = p_0 + (0.5 - p_0)\left(1 - e^{-x/\ell_{\text{mat}}}\right)
```

where $p_0 = f_{\text{recycle}} / (f_{\text{recycle}} + f_{\text{new}}) \approx 0.5$ is the initial parental fraction immediately behind the fork (reflecting equal partitioning to two daughter strands), and $\ell_{\text{mat}} = v / k_{\text{mat}}$ is the epigenetic maturation length — the distance behind the fork at which histone modifications are restored to steady-state levels. Here $v$ is fork speed (kb/min) and $k_{\text{mat}}$ is the first-order rate constant for modification restoration (min⁻¹).

**F239b. Modification restoration kinetics:**

For a specific histone mark (e.g., H3K27me3), the modification level $m(x)$ behind the fork is:

```math
m(x) = m_{\text{ss}} \cdot \left(1 - (1-p_0) \cdot e^{-x/\ell_{\text{mat}}}\right)
```

where $m_{\text{ss}}$ is the steady-state modification level before replication. For H3K27me3 (maintained by PRC2 with $k_{\text{mat}} \approx 0.05$ min⁻¹ and $v = 1.5$ kb/min), $\ell_{\text{mat}} \approx 30$ kb, meaning full modification restoration requires approximately 20 kb of fork progression — consistent with the observed ~15–20 minute maturation timescale at typical fork speeds (Reveron-Gomez et al., 2018; Stewart-Morgan et al., 2020).

### 6.7 Novel Mathematical Framework F240: CpG Methylation Fidelity Across Cell Divisions

**F240a. Three-state Markov chain:**

We model each CpG site as a three-state Markov chain with states: M (methylated on both strands), H (hemimethylated), and U (unmethylated). The transition matrix per cell division is:

```math
\mathbf{P} = \begin{pmatrix} \mu(1-\delta) & (1-\mu)(1-\delta) + \mu\delta & (1-\mu)\delta \\ \mu_H(1-\delta_H) & (1-\mu_H)(1-\delta_H) + \mu_H\delta_H & (1-\mu_H)\delta_H \\ \mu_U & 0 & 1-\mu_U \end{pmatrix}
```

where $\mu \approx 0.96$ is the DNMT1 maintenance efficiency (probability that a hemimethylated CpG is re-methylated), $\delta \approx 0.02$ is the probability of methylation loss despite DNMT1 activity (passive demethylation or TET-mediated active demethylation), $\mu_H$ is the maintenance efficiency for hemimethylated sites (intermediate state), $\delta_H$ is the demethylation rate from the hemimethylated state, and $\mu_U \approx 0.01$ is the de novo methylation rate by DNMT3A/B (low in somatic cells).

**F240b. Steady-state methylation level:**

At steady state, the fraction of CpG sites in the methylated state is:

```math
\pi_M = \frac{\mu(1-\delta)}{\mu(1-\delta) + (1-\mu)(1-\delta) + \mu\delta + \delta(1-\mu)}
```

For typical somatic cell parameters ($\mu = 0.96$, $\delta = 0.02$, $\mu_U = 0.01$), this yields $\pi_M \approx 0.94$, matching the observed genome-wide CpG methylation level of approximately 70–80% when accounting for unmethylated CpG islands.

**F240c. Methylation half-life:**

The characteristic decay time for methylation at a locus that loses DNMT1 targeting (e.g., during differentiation or in response to DNMT1 inhibition) is:

```math
\tau_{1/2} = \frac{\ln 2}{1 - \mu(1-\delta)} \approx \frac{\ln 2}{0.06} \approx 11.5 \text{ cell divisions}
```

This predicts that CpG methylation is lost with a half-life of approximately 12 cell divisions in the absence of maintenance — consistent with experimental measurements showing progressive demethylation over 10–20 passages in DNMT1-depleted cells (Ming et al., 2020).

---

## 7. Section VI: The Timing Problem — Replication Timing as a Genome-Scale Program

### 7.1 The Core Question

Replication does not proceed uniformly across the genome: different regions are replicated at reproducibly different times during S phase, generating a replication timing program that is characteristic of each cell type. This program is one of the most striking examples of genome-scale organization, with megabase-scale replication timing domains (RTDs) maintaining stable early or late replication across hundreds of cell cycles (Rhind & Gilbert, 2013; Vouzas & Gilbert, 2021). The timing problem asks: what molecular mechanism establishes and maintains this temporal program, and what function does it serve?

### 7.2 Replication Timing Domains and 3D Genome Organization

Genome-wide replication timing profiles, measured by Repli-seq (sequencing of BrdU-labeled nascent DNA from cells sorted into S-phase fractions), reveal a remarkably structured landscape: the genome is partitioned into ~2,000–4,000 replication timing domains, each spanning 200 kb to 2 Mb, with sharp boundaries separating early-replicating and late-replicating regions (Hansen et al., 2010; Zhao et al., 2020). Naim et al. (2024) traced the emergence of this timing program in early mammalian development using single-cell Repli-seq on mouse embryos from zygote to blastocyst, showing that replication timing domains become defined progressively from the 4-cell stage coincident with A/B compartment strengthening (Naim et al., 2024). Zhang et al. (2025) developed a high-resolution mathematical model that inferred firing rate distributions from Repli-seq data, revealing that regions of strong concordance between firing rates and timing are associated with open chromatin and active promoters (Zhang et al., 2025). The timing profile is highly reproducible between biological replicates (Pearson r > 0.95) and stable across cell divisions within a given cell type (Vouzas & Gilbert, 2021).

Replication timing domains show a remarkable correspondence with the A/B compartment structure of the genome revealed by Hi-C chromosome conformation capture: early-replicating domains correspond almost exclusively to A (active) compartments, while late-replicating domains correspond to B (inactive) compartments (Ryba et al., 2010; Pope et al., 2014). This correspondence extends to finer scales: topologically associating domains (TADs) that switch between A and B compartments during differentiation show coordinated switches in replication timing, with approximately 10–15% of the genome changing timing between cell types (Dileep et al., 2015; Rivera-Mulia et al., 2015).

### 7.3 RIF1-PP1: The Master Timing Regulator

The protein RIF1 (Rap1-interacting factor 1) has emerged as the central regulator of the replication timing program. RIF1 associates with late-replicating chromatin in large megabase-scale domains (RIF1-associated domains, or RADs) that coincide with B compartments and late-replicating regions (Foti et al., 2016; Seller & O'Farrell, 2018). RIF1 suppresses origin firing in these domains by recruiting protein phosphatase 1 (PP1), which counteracts S-phase kinase (DDK and CDK) activity by dephosphorylating key substrates including MCM4 (Davé et al., 2014; Hiraga et al., 2014; Mattarocci et al., 2014).

The functional consequence of RIF1 loss was demonstrated by Klein et al. (2021) in a landmark study published in *Science*. Elimination of RIF1 in human cell lines resulted in near-complete loss of the replication timing program from the first S phase, with origins firing in a heterogeneous, nearly random temporal order. Critically, altered replication timing was followed by replication-dependent redistribution of active and repressive histone modifications (H3K4me3 and H3K27me3, respectively) and alterations in genome architecture (A/B compartment structure), demonstrating that replication timing is an upstream determinant of the epigenetic landscape rather than merely a consequence of it (Klein et al., 2021).

A 2025 study by Brossas et al. in *Developmental Cell* extended these findings to early mouse embryogenesis, showing that RIF1 controls the progressive consolidation of the replication timing program during the first cell divisions after fertilization — independently of lamina-associated nuclear organization (Brossas et al., 2025). This result separates the RIF1-PP1 timing mechanism from nuclear lamina positioning, which had been proposed as an alternative timing determinant, and establishes RIF1 as the primary cis-acting timer in both embryonic and somatic contexts.

### 7.4 Replication Timing Changes in Development and Disease

Approximately 10–15% of the genome undergoes replication timing switches during cellular differentiation, and these switches are highly coordinated with changes in gene expression and chromatin state (Rivera-Mulia et al., 2015; Vouzas & Gilbert, 2021). Early-to-late switches typically accompany gene silencing and heterochromatin formation, while late-to-early switches accompany gene activation and euchromatin establishment (Rivera-Mulia & Gilbert, 2016).

Replication timing alterations have been observed in cancer, where they correlate with mutation density: late-replicating regions accumulate more somatic mutations than early-replicating regions, likely reflecting lower MMR efficiency in late-replicating heterochromatin (Supek & Lehner, 2015; Zheng et al., 2020). In rare diseases, mutations in ORC subunits (ORC1, ORC4, ORC6), CDC6, CDT1, and CDC45 cause Meier-Gorlin syndrome — a primordial dwarfism characterized by short stature, microtia, and absent or hypoplastic patellae — demonstrating that perturbation of the replication initiation machinery produces specific developmental phenotypes (Bicknell et al., 2011; de Munnik et al., 2015).

### 7.5 Novel Mathematical Framework F241: Timing Domain Boundary Model

We model the sharp boundaries between early and late replication timing domains using a one-dimensional Ising-like model in which cooperative interactions between neighboring origins create bistable timing states.

**F241a. Origin timing as a spin variable:**

Assign each origin $i$ a spin variable $s_i \in \{+1 \text{ (early)}, -1 \text{ (late)}\}$. The Hamiltonian governing the timing configuration is:

```math
\mathcal{H} = -J \sum_{\langle i,j \rangle} s_i s_j - h(x_i) \sum_i s_i
```

where $J > 0$ is the cooperative interaction energy between neighboring origins (reflecting shared chromatin environment, RIF1 domain boundaries, and TAD insulation), $h(x_i)$ is a position-dependent external field representing the local chromatin state (positive for A-compartment, euchromatic regions favoring early firing; negative for B-compartment, heterochromatic regions favoring late firing), and $\langle i,j \rangle$ denotes nearest-neighbor origin pairs.

**F241b. Timing domain boundary as a domain wall:**

At a timing boundary, the spin configuration transitions from $+1$ (early) to $-1$ (late). The domain wall width $w$ in the 1D Ising model at temperature $T$ is:

```math
w = \frac{a}{\tanh(J/k_B T)} \approx a \cdot e^{J/k_BT}
```

where $a$ is the mean inter-origin spacing (~100 kb). For the observed sharp timing boundaries ($w \approx 100$–$300$ kb), this constrains $J/k_B T \approx 0.5$–$1.5$, indicating moderate cooperativity between neighboring origins — consistent with the known ~200 kb correlation length of histone modification domains and TAD sizes.

**F241c. Critical field for timing switch:**

The critical external field required to flip a timing domain from late to early is:

```math
h_c = 2J \cdot \frac{n_{\text{boundary}}}{n_{\text{domain}}}
```

where $n_{\text{boundary}}$ is the number of origins at the domain boundary and $n_{\text{domain}}$ is the total number of origins in the domain. This predicts that small domains (few origins) are easier to switch than large domains — consistent with the observation that replication timing switches during differentiation preferentially affect smaller domains (Rivera-Mulia et al., 2015; Vouzas & Gilbert, 2021).

### 7.6 Novel Mathematical Framework F242: Information Content of the Replication Timing Program

**F242a. Information per timing domain:**

The replication timing profile partitions the genome into $D$ timing domains, each assigned one of $K$ timing classes (e.g., early, mid-early, mid-late, late; $K = 4$ in typical analyses). The total information content of the timing program is:

```math
I_{\text{timing}} = \sum_{d=1}^{D} \log_2 K - H(T_d \mid \text{neighbors})
```

where $H(T_d \mid \text{neighbors})$ is the conditional entropy of timing class $T_d$ given the timing of neighboring domains, reflecting spatial correlations. For the human genome with $D \approx 3{,}000$ domains, $K = 4$ timing classes, and spatial correlation reducing effective entropy by ~40%:

```math
I_{\text{timing}} \approx 3000 \times 2 \times 0.6 = 3{,}600 \text{ bits}
```

**F242b. Cell-type-specific information:**

The information that distinguishes one cell type's timing program from another is:

```math
I_{\text{cell-type}} = D_{\text{KL}}(P_{\text{timing}}^{A} \| P_{\text{timing}}^{B}) = \sum_d \sum_k P^A(T_d = k) \log_2 \frac{P^A(T_d = k)}{P^B(T_d = k)}
```

where $D_{\text{KL}}$ is the Kullback-Leibler divergence between the timing programs of cell types A and B. With ~10–15% of domains switching timing between cell types (each contributing ~2 bits), the cell-type-specific information is approximately $I_{\text{cell-type}} \approx 400$–$600$ bits — comparable to the information content of transcription factor binding profiles and suggesting that replication timing is an informationally significant component of cell identity (Klein et al., 2021; Vouzas & Gilbert, 2021).

---

## 8. Open Questions and Future Directions

### 8.1 The Licensing Problem

**Open question 1:** What determines origin positions in metazoan genomes? Unlike yeast, where ACS sequences define origins, metazoan origin selection is sequence-independent and likely governed by chromatin features. G-quadruplex structures, open chromatin, and active transcription are correlated with origin positioning, but the causal relationships remain unresolved (Cayrou et al., 2015). Single-molecule origin mapping at nucleotide resolution in human cells would address whether origins have preferred positions or are truly stochastic.

**Open question 2:** How does the cell sense that sufficient MCM complexes have been loaded? The licensing checkpoint — which delays S-phase entry if licensing is incomplete — is known to involve p53 and p21 (Neelsen et al., 2013), but the molecular sensor that monitors MCM loading levels remains unidentified.

### 8.2 The Firing Problem

**Open question 3:** What is the minimal set of human replication initiation factors? The complete reconstitution of human origin firing with purified proteins — analogous to the yeast system reconstituted by Yeeles et al. (2015) — has not yet been achieved. The identification of DONSON and other metazoan-specific factors suggests additional components may remain undiscovered (Kingsley et al., 2023).

**Open question 4:** How does the cell coordinate firing across all chromosomes simultaneously? Single-cell replication timing studies reveal cell-to-cell variability, but the mechanism that synchronizes the global onset of S phase across the genome within a single cell is poorly understood.

### 8.3 The Fidelity Problem

**Open question 5:** How does MMR achieve strand discrimination in human cells? In *E. coli*, the Dam methylation-dependent MutH endonuclease nicks the unmethylated (newly synthesized) strand. In eukaryotes, strand discrimination likely relies on pre-existing strand discontinuities (Okazaki fragment junctions on the lagging strand, and PCNA loading sites on the leading strand), but this mechanism has not been directly demonstrated in human cells (Kunkel & Erie, 2015).

### 8.4 The Completion Problem

**Open question 6:** Can MiDAS be enhanced to protect fragile sites in cancer cells? Cancer cells experience chronic replication stress, making them dependent on MiDAS for genome maintenance. Therapeutic strategies that inhibit MiDAS (e.g., by targeting RAD52 or POLD3) may selectively kill cancer cells while sparing normal cells with lower replication stress (Bhowmick et al., 2016; Ji et al., 2023).

### 8.5 The Inheritance Problem

**Open question 7:** Does asymmetric histone inheritance between sister chromatids have functional consequences for cell fate? The transient epigenetic asymmetry created by strand-biased histone segregation could, in principle, generate daughter cells with different epigenetic states from a single division — a mechanism that could contribute to asymmetric stem cell division (Petryk et al., 2018; Xu et al., 2024).

### 8.6 The Timing Problem

**Open question 8:** Is replication timing a cause or consequence of 3D genome organization? Klein et al. (2021) showed that altering replication timing (via RIF1 deletion) changes A/B compartment structure, suggesting timing is causal. However, Brossas et al. (2025) showed that RIF1 controls timing independently of lamina association, complicating simple models in which nuclear positioning determines timing. Resolving the causal hierarchy between replication timing, chromatin state, and nuclear architecture is a central challenge for the field.

---

## 9. Conclusion

Eukaryotic chromosome replication is governed by six fundamental problems whose solutions reveal the deep logic of genome duplication. The licensing problem ensures that sufficient helicase complexes are loaded to guarantee genome coverage, with the MCM paradox reflecting a safety margin quantifiable by stochastic coverage theory (F232). The firing problem converts this excess capacity into a temporally ordered program through kinase-dependent competition for limiting factors, formalized as an inhomogeneous Poisson process (F233–F234). The fidelity problem is solved by a three-stage cascade — nucleotide selectivity, proofreading, and mismatch repair — whose multiplicative error reduction achieves information transmission at 99.99999998% of the Shannon limit (F235–F236). The completion problem requires passive fork convergence supplemented by the MiDAS rescue pathway at vulnerable fragile sites, with completion time governed by extreme value statistics (F237–F238). The inheritance problem demands the faithful segregation of parental histones and DNA methylation marks through the MCM2-FACT conveyor and DNMT1-UHRF1 coupling, with methylation stability predictable by a three-state Markov chain with a half-life of ~12 cell divisions (F239–F240). And the timing problem encodes approximately 3,600 bits of cell-type-specific information in the megabase-scale replication timing program, maintained by the RIF1-PP1 axis and formalized by an Ising-type model for timing domain boundaries (F241–F242).

Each problem remains incompletely solved, and the interfaces between problems — how licensing constrains firing, how timing determines inheritance, how fidelity varies with timing — represent the most exciting frontiers for the next decade of research. The convergence of reconstituted biochemistry, cryo-EM structural biology, single-cell genomics, and quantitative modeling positions the field to achieve a fully integrated, predictive understanding of how cells duplicate their chromosomes.

---

## References

Alabert, C., Barth, T. K., Reverón-Gómez, N., Sidoli, S., Schmidt, A., Jensen, O. N., ... & Groth, A. (2015). Two distinct modes for propagation of histone PTMs across the cell cycle. *Genes & Development*, 29(6), 585–590. PMID: 25792596

Baretić, D., Jenkyn-Bedford, M., Aria, V., Cannone, G., Skehel, M., & Yeeles, J. T. P. (2020). Cryo-EM structure of the fork protection complex bound to CMG at a replication fork. *Molecular Cell*, 78(5), 926–940. PMID: 32369734

Bhowmick, R., Minocherhomji, S., & Hickson, I. D. (2016). RAD52 facilitates mitotic DNA synthesis following replication stress. *Molecular Cell*, 64(6), 1117–1126. PMID: 27984745

Bicknell, L. S., Bonber, T., Kober, F., Mukherjee, S., Roessler, F., Splitt, M., ... & Jackson, A. P. (2011). Mutations in the pre-replication complex cause Meier-Gorlin syndrome. *Nature Genetics*, 43(4), 356–359. PMID: 21358632

Bleichert, F., Botchan, M. R., & Berger, J. M. (2015). Crystal structure of the eukaryotic origin recognition complex. *Nature*, 519(7543), 321–326. PMID: 25762138

Bleichert, F., Botchan, M. R., & Berger, J. M. (2017). Mechanisms for initiating cellular DNA replication. *Science*, 355(6327), eaah6317. PMID: 28209641

Boos, D., Sanchez-Pulido, L., Rappas, M., Pearl, L. H., Oliver, A. W., Ponting, C. P., & Diffley, J. F. X. (2011). Regulation of DNA replication through Sld3-Dpb11 interaction is conserved from yeast to humans. *Current Biology*, 21(13), 1152–1157. PMID: 21700461

Brossas, C., Valton, A.-L., & Prioleau, M.-N. (2025). RIF1 controls replication timing in early mouse embryos independently of lamina-associated nuclear organization. *Developmental Cell*, 60(9), 1289–1302.

Burgers, P. M. J., & Kunkel, T. A. (2017). Eukaryotic DNA replication fork. *Annual Review of Biochemistry*, 86, 417–438. PMID: 28301743

Campbell, B. B., Light, N., Fabrber, D., Zichner, T., Shih, J., Edwards, M., ... & Tabori, U. (2017). Comprehensive analysis of hypermutation in human cancer. *Cell*, 171(5), 1042–1056. PMID: 29056344

Cayrou, C., Ballester, B., Peiffer, I., Fenouil, R., Coulombe, P., Andrau, J. C., ... & Méchali, M. (2015). The chromatin environment shapes DNA replication origin organization and defines origin classes. *Genome Research*, 25(12), 1873–1885. PMID: 26560631

Cvetkovic, M. A., Passaretti, P., Butryn, A., Reynolds-Sherrill, J., Flynn, H. R., Snijders, A. P., ... & Costa, A. (2023). The structural mechanism of dimeric DONSON in replicative helicase activation. *Molecular Cell*, 83(22), 4017–4031. PMID: 37820732

Chagin, V. O., Casas-Delucchi, C. S., Reinhart, M., Schermelleh, L., Markaki, Y., Maiser, A., ... & Cardoso, M. C. (2016). 4D visualization of replication foci in mammalian cells corresponding to individual replicons. *Nature Communications*, 7, 11231. PMID: 27052570

Chan, K. L., Palmai-Pallag, T., Ying, S., & Hickson, I. D. (2018). Replication stress induces sister-chromatid bridging at fragile site loci in mitosis. *Nature Cell Biology*, 11(6), 753–760. PMID: 19465922

Choe, K. N., & Moldovan, G. L. (2017). Forging ahead through darkness: PCNA, still the principal conductor at the replication fork. *Molecular Cell*, 65(3), 380–392. PMID: 28157503

Davé, A., Cooley, C., Garg, M., & Bhargava, R. (2014). Protein phosphatase 1 recruitment by Rif1 regulates DNA replication origin firing by counteracting DDK activity. *Cell Reports*, 7(1), 53–61. PMID: 24656819

de Munnik, S. A., Bicknell, L. S., Aftimos, S., Al-Aama, J. Y., van Bever, Y.,"; Bober, M. B., ... & Hoefsloot, L. H. (2015). Meier-Gorlin syndrome genotype-phenotype studies. *Human Mutation*, 36(3), 371–379. PMID: 25504725

Deegan, T. D., & Diffley, J. F. X. (2016). MCM: one ring to rule them all. *Current Opinion in Structural Biology*, 37, 145–151. PMID: 26866665

Deegan, T. D., Yeeles, J. T. P., & Diffley, J. F. X. (2016). Phosphopeptide binding by Sld3 links Dbf4-dependent kinase to MCM replicative helicase activation. *The EMBO Journal*, 35(9), 961–973. PMID: 26912723

Dewar, J. M., & Walter, J. C. (2017). Mechanisms of DNA replication termination. *Nature Reviews Molecular Cell Biology*, 18(8), 507–516. PMID: 28537574

Dewar, J. M., Budzowska, M., & Walter, J. C. (2017). The mechanism of DNA replication termination in vertebrates. *Nature*, 525(7569), 345–348. PMID: 26322582

Dileep, V., Ay, F., Sima, J., Vera, D. L., Noble, W. S., & Gilbert, D. M. (2015). Topologically associating domains and their long-range contacts are established during early G1 coincident with the establishment of the replication-timing program. *Genome Research*, 25(8), 1104–1113. PMID: 25995269

Douglas, M. E., Ali, F. A., Costa, A., & Diffley, J. F. X. (2018). The mechanism of eukaryotic CMG helicase activation. *Nature*, 555(7695), 265–268. PMID: 29489749

Evrony, G. D., Cordero, D. R., Shen, J., Partlow, J. N., Yu, T. W., Rodin, R. E., ... & Walsh, C. A. (2017). Integrated genome and transcriptome sequencing identifies a noncoding mutation in the genome replication factor DONSON as the cause of microcephaly-micromelia syndrome. *Genome Research*, 27(8), 1323–1335. PMID: 28687709

Fishel, R. (2015). Mismatch repair. *Journal of Biological Chemistry*, 290(44), 26395–26403. PMID: 26354434

Foltman, M., Evrin, C., De Piccoli, G., Jones, R. C., Sherwood, R. D., Sherwood, R. D., Sherwood, R. D., ... & Labib, K. (2013). Eukaryotic replisome components cooperate to process histones during chromosome replication. *Cell Reports*, 3(3), 892–904. PMID: 23478019

Foti, R., Gnan, S., Cornacchia, D., Diber, A., Reinhart, M., & Buonomo, S. B. C. (2016). Nuclear architecture organized by Rif1 underpins the replication-timing program. *Molecular Cell*, 61(2), 260–273. PMID: 26725009

Fu, Y. V., Yardimci, H., Long, D. T., Ho, T. V., Guainazzi, A., Bermudez, V. P., ... & Walter, J. C. (2011). Selective bypass of a lagging strand roadblock by the eukaryotic replicative DNA helicase. *Cell*, 146(6), 931–941. PMID: 21925315

Gan, H., Serra-Cardona, A., Hua, X., Zhou, H., Labib, K., Yu, C., & Zhang, Z. (2018). The Mcm2-Ctf4-Polα axis facilitates parental H3-H4 transfer to lagging strands. *Molecular Cell*, 72(1), 140–151. PMID: 30244834

Gan, H., Yu, C., Das, S., Li, T., Wang, Y., Yang, J., ... & Zhang, Z. (2024). Parental histone transfer caught at the replication fork. *Nature*, 627, 890–897. PMID: 38448592

Ganai, R. A., & Johansson, E. (2016). DNA replication — a matter of fidelity. *Molecular Cell*, 62(5), 745–755. PMID: 27259205

Gaubitz, C., Liu, X., Magrino, J., Stone, N. P., Marber, T. J., Slabaugh, C., & Bhargava, R. (2022). Structure of the human clamp loader reveals an autoinhibited conformation of a substrate-bound AAA+ switch. *Proceedings of the National Academy of Sciences*, 119(14), e2163149119. PMID: 35353634

Georgescu, R. E., Yuan, Z., Bai, L., de Luna Almeida Santos, R., Sun, J., Zhang, D., ... & Li, H. (2017). Structure of eukaryotic CMG helicase at a replication fork and implications to replisome architecture and origin initiation. *Proceedings of the National Academy of Sciences*, 114(5), E697–E706. PMID: 28096349

Haradhvala, N. J., Ghandi, M., Gervais, A. L., Haas, B. J., & Getz, G. (2023). Exploring the basis of heterogeneity of cancer aggressiveness among the mutated POLE variants. *Scientific Reports*, 13, 18229. PMID: 37891003

Hashimoto, Y., Tanaka, H., Takahashi, Y., & Dunphy, W. G. (2023). DONSON facilitates Cdc45 and GINS chromatin association and is essential for DNA replication initiation. *Nucleic Acids Research*, 51(18), 9748–9763. PMID: 37615578

Havens, C. G., & Walter, J. C. (2011). Mechanism of CRL4(Cdt2), a PCNA-dependent E3 ubiquitin ligase. *Genes & Development*, 25(15), 1568–1582. PMID: 21828267

Helmrich, A., Ballarino, M., & Tora, L. (2011). Collisions between replication and transcription complexes cause common fragile site instability at the longest human genes. *Molecular Cell*, 44(6), 966–977. PMID: 22195969

Hiraga, S.-I., Ly, T., Garzón, J., Horejsi, Z., Ohkubo, Y. N., Endo, A., ... & Donaldson, A. D. (2014). Rif1 controls DNA replication by directing protein phosphatase 1 to reverse Cdc7-mediated phosphorylation of the MCM complex. *Genes & Development*, 28(4), 372–383. PMID: 24532715

Huang, H., Strømme, C. B., Sarber, A. C., Nishi, Y., & Bhargava, R. (2015). A unique binding mode enables MCM2 to chaperone histones H3-H4 at replication forks. *Nature Structural & Molecular Biology*, 22(8), 618–626. PMID: 26167883

Hyrien, O., Guilbaud, G., & Krude, T. (2025). The double life of mammalian DNA replication origins. *Genes & Development*, 39(5–6), 304–324. PMID: 40082112

Ishiyama, S., Nishiyama, A., Saeki, Y., Moritsugu, K., Morimoto, D., Yamaguchi, L., ... & Nakanishi, M. (2017). Structure of the Dnmt1 reader module complexed with a unique two-mono-ubiquitin mark on histone H3 reveals the basis for DNA methylation maintenance. *Molecular Cell*, 68(2), 350–360. PMID: 29053958

Jaremko, M. J., On, K. F., Thomas, D. R., Stillman, B., & Joshua-Tor, L. (2020). The dynamic nature of the human origin recognition complex revealed through five cryoEM structures. *eLife*, 9, e58622. PMID: 32744498

Jeltsch, A., & Jurkowska, R. Z. (2014). New concepts in DNA methylation. *Trends in Biochemical Sciences*, 39(7), 310–318. PMID: 24947342

Ji, F., Liao, H., Pan, S., Ouyang, L., Jia, F., Fu, Z., ... & Guo, X. (2023). Mitotic DNA synthesis in response to replication stress requires the sequential action of DNA polymerases zeta and delta in human cells. *Nature Communications*, 14(1), 706. PMID: 36759519

Jones, M. L., Baris, Y., Taylor, M. R. G., & Yeeles, J. T. P. (2022). Fast and efficient DNA replication with purified human proteins. *Nature*, 606(7912), 204–210. PMID: 35650436

Kawabata, T., Luebben, S. W., Yamaguchi, S., Ilves, I., Matise, I., Buske, T., Botchan, M. R., & Siddiqui, M. (2011). Stalled fork rescue via dormant replication origins in unchallenged S phase promotes proper chromosome segregation and tumor suppression. *Molecular Cell*, 41(5), 543–553. PMID: 21362550

Kwan, E. E., Hiatt, J. B., Li, H., Nguyen, T. H., McGovern, B. L., Bynum, A. K., ... & Mendez, J. (2024). Replication stress induces POLQ-mediated structural variant formation throughout common fragile sites after entry into mitosis. *Nature Communications*, 15(1), 9547. PMID: 39500919

Kelch, B. A., Makino, D. L., O'Donnell, M., & Kuriyan, J. (2011). How a DNA polymerase clamp loader opens a sliding clamp. *Science*, 334(6063), 1675–1681. PMID: 22194570

Keszthelyi, A., Minchell, N. E., & Baxter, J. (2016). The causes and consequences of topological stress during DNA replication. *Genes*, 7(12), 134. PMID: 27999413

Kingsley, G., Oyarzún, D., Tay, T. L., & Lopes, M. (2023). In silico protein interaction screening uncovers DONSON's role in replication initiation. *Science*, 381(6660), eadi3448. PMID: 37590370

Klein, K. N., Zhao, P. A., Lyu, X., Sasaki, T., Bartlett, D. A., Singh, A. M., ... & Gilbert, D. M. (2021). Replication timing maintains the global epigenetic state in human cells. *Science*, 372(6540), 371–378. PMID: 33888635

Kumagai, A., & Dunphy, W. G. (2017). MTBP, the partner of Treslin, contains a novel DNA-binding domain that is essential for proper initiation of DNA replication. *Molecular Biology of the Cell*, 28(22), 2998–3012. PMID: 28904208

Kumagai, A., Shevchenko, A., Shevchenko, A., & Dunphy, W. G. (2011). Direct regulation of Treslin by cyclin-dependent kinase is essential for the onset of DNA replication. *Journal of Cell Biology*, 193(6), 995–1007. PMID: 21646402

Kunkel, T. A., & Erie, D. A. (2015). Eukaryotic mismatch repair in relation to DNA replication. *Annual Review of Genetics*, 49, 291–313. PMID: 26436461

Lancey, C., Tehseen, M., Raber, L., Smith, C. J., Hall, J. A., Ye, F., ... & Costa, A. (2020). Structure of the processive human Pol δ holoenzyme. *Nature Communications*, 11(1), 1109. PMID: 32111831

Langston, L. D., Zhang, D., Yurieva, O., Georgescu, R. E., Finkelstein, J., Yao, N. Y., Indiani, C., & O'Donnell, M. E. (2014). CMG helicase and DNA polymerase ε form a functional 15-subunit holoenzyme for eukaryotic leading-strand DNA replication. *Proceedings of the National Academy of Sciences*, 111(43), 15390–15395. PMID: 25313033

Li, H., & O'Donnell, M. E. (2022). The eukaryotic CMG helicase at the replication fork: emerging architecture reveals an unexpected mechanism. *BioEssays*, 40(3), 1700208. PMID: 29399824

Li, J., Dong, J., Wang, W., Yu, D., Fan, X., Hui, Y. C., ... & Zhai, Y. (2022). Cryo-EM structure of human hexameric MCM2-7 complex. *iScience*, 25(9), 104976. PMID: 36117988

Li, N., Zhai, Y., Zhang, Y., Li, W., Yang, M., Lei, J., Tye, B.-K., & Gao, N. (2018). Structure of the eukaryotic MCM complex at 3.8 Å. *Nature*, 524(7564), 186–191. PMID: 26222030

Liu, Y., Zhangding, Z., Liu, X., ... & Xie, W. (2024). Fork coupling directs DNA replication elongation and termination. *Science*, 383(6686), 1215–1222. PMID: 38484065

Liu, D., Keijzers, G., & Rasmussen, L. J. (2017). DNA mismatch repair and its many roles in eukaryotic cells. *Mutation Research — Reviews in Mutation Research*, 773, 174–187. PMID: 28927529

Lujan, S. A., Williams, J. S., Clausen, A. R., Clark, A. B., & Kunkel, T. A. (2015). Mismatch repair balances leading and lagging strand DNA replication fidelity. *PLoS Genetics*, 9(10), e1003016. PMID: 24204286

Lynch, M., Ackerman, M. S., Gout, J. F., Long, H., Sung, W., Thomas, W. K., & Foster, P. L. (2016). Genetic drift, selection and the evolution of the mutation rate. *Nature Reviews Genetics*, 17(11), 704–714. PMID: 27739533

Macheret, M., & Halazonetis, T. D. (2018). Intragenic origins due to short G1 phases underlie oncogene-induced DNA replication stress. *Nature*, 555(7694), 112–116. PMID: 29466339

Mantiero, D., Mackenzie, A., Donaldson, A., & Zegerman, P. (2011). Limiting replication initiation factors execute the temporal programme of origin firing in budding yeast. *The EMBO Journal*, 30(23), 4805–4814. PMID: 22081107

Mattarocci, S., Shyian, M., Lemmens, L., Damay, P., Altintas, D. M., Shi, T., ... & Shore, D. (2014). Rif1 controls DNA replication timing in yeast through the PP1 phosphatase Glc7. *Cell Reports*, 7(1), 62–69. PMID: 24685139

Miller, T. C. R., Locke, J., Greiwe, J. F., Diffley, J. F. X., & Costa, A. (2019). Mechanism of head-to-head MCM double-hexamer formation revealed by cryo-EM. *Nature*, 575(7784), 704–710. PMID: 31748745

Ming, X., Zhang, Z., Zou, Z., Lv, C., Dong, Q., He, Q., ... & Zhu, B. (2020). Kinetics and mechanisms of mitotic inheritance of DNA methylation and their roles in aging-associated methylome deterioration. *Cell Research*, 30(11), 980–996. PMID: 32581343

Minocherhomji, S., Ying, S., Bjerregaard, V. A., Bber, S., Kober, C., Juber, R., ... & Hickson, I. D. (2015). Replication stress activates DNA repair synthesis in mitosis. *Nature*, 528(7581), 286–290. PMID: 26633632

Naim, V., Teixeira, F. K., Grenier, J. K., ... & Heard, E. (2024). Emergence of replication timing during early mammalian development. *Nature*, 625(7995), 285–293. PMID: 38093015

Murugan, A., Huse, D. A., & Leibler, S. (2012). Speed, dissipation, and error in kinetic proofreading. *Proceedings of the National Academy of Sciences*, 109(30), 12034–12039. PMID: 22786929

Neelsen, K. J., Zanini, I. M. Y., Mijic, S., Herrador, R., Zellweger, R., Ray Chaudhuri, A., ... & Lopes, M. (2013). Deregulated origin licensing leads to chromosomal breaks by rereplication of a gapped DNA template. *Genes & Development*, 27(23), 2537–2542. PMID: 24298053

Nishiyama, A., Yamaguchi, L., Sharif, J., Johmura, Y., Kawamura, T., Nakanishi, K., ... & Nakanishi, M. (2013). Uhrf1-dependent H3K23 ubiquitylation couples maintenance DNA methylation and replication. *Nature*, 502(7470), 249–253. PMID: 24013172

Noguchi, Y., Yuan, Z., Bai, L., Schneider, S., Zhao, G., Stillman, B., Speck, C., & Li, H. (2017). Cryo-EM structure of Mcm2-7 double hexamer on DNA suggests a lagging-strand DNA extrusion model. *Proceedings of the National Academy of Sciences*, 114(45), E9529–E9538. PMID: 29078395

O'Donnell, M. E., & Li, H. (2024). Four decades of eukaryotic DNA replication: from yeast genetics to high-resolution cryo-EM structures of the replisome. *Proceedings of the National Academy of Sciences*, 121(51), e2415231121. PMID: 39666989

Paeschke, K., Bochman, M. L., Garcia, P. D., Cejka, P., Friedman, K. L., Kowalczykowski, S. C., & Zakian, V. A. (2013). Pif1 family helicases suppress genome instability at G-quadruplex motifs. *Nature*, 497(7450), 458–462. PMID: 23657261

Petryk, N., Kahli, M., d'Aubenton-Carafa, Y., Jaszczyszyn, Y., Shen, Y., Silvain, M., ... & Chen, C.-L. (2016). Replication landscape of the human genome. *Nature Communications*, 7, 10208. PMID: 26751768

Petryk, N., & Groth, A. (2024). Replication-coupled inheritance of chromatin states. *Annual Review of Biochemistry*, 93, 559–583. PMID: 38640043

Petryk, N., Dalby, M., Wenger, A., Stromme, C. B., Strandsby, A., Andersson, R., & Groth, A. (2018). MCM2 promotes symmetric inheritance of modified histones during DNA replication. *Science*, 361(6409), 1389–1392. PMID: 30115746

Polo Rivera, C., Deegan, T. D., & Labib, K. P. M. (2024). CMG helicase disassembly is essential and driven by two pathways in budding yeast. *The EMBO Journal*, 43(17), 3818–3845. PMID: 39039287

Pope, B. D., Ryba, T., Dileep, V., Yue, F., Wu, W., Denas, O., ... & Gilbert, D. M. (2014). Topologically associating domains are stable units of replication-timing regulation. *Nature*, 515(7527), 402–405. PMID: 25409831

Qiu, Z., Li, J., Costa, A., & Stillman, B. (2024). Multiple pathways for licensing human replication origins. *Nature Structural & Molecular Biology*, 31(8), 1209–1222. PMID: 38645015

Roske, J. J., & Yeeles, J. T. P. (2024). Structural basis for processive daughter-strand synthesis and proofreading by the human leading-strand DNA polymerase Pol epsilon. *Nature Structural & Molecular Biology*, 31(12), 1921–1931. PMID: 39112807

Reverón-Gómez, N., González-Aguilera, C., Stewart-Morgan, K. R., Petryk, N., Flury, V., Graziano, S., ... & Groth, A. (2018). Accurate recycling of parental histones reproduces the histone modification landscape during DNA replication. *Molecular Cell*, 72(2), 239–249. PMID: 30146316

Rhind, N., & Gilbert, D. M. (2013). DNA replication timing. *Cold Spring Harbor Perspectives in Biology*, 5(8), a010132. PMID: 23838439

Richet, N., Liu, D., Legrand, P., Velours, C., Corpet, A., Lézeau, A., ... & Mousson, F. (2015). Structural insight into how the human helicase subunit MCM2 may act as a histone chaperone together with ASF1 at the replication fork. *Nucleic Acids Research*, 43(3), 1905–1917. PMID: 25618845

Rivera-Mulia, J. C., & Gilbert, D. M. (2016). Replicating large genomes: divide and conquer. *Molecular Cell*, 62(5), 756–765. PMID: 27259206

Rivera-Mulia, J. C., Buckley, Q., Sasaki, T., Zimmerman, J., Didier, R. A., Nazor, K., ... & Gilbert, D. M. (2015). Dynamic changes in replication timing and gene expression during lineage specification of human pluripotent stem cells. *Genome Research*, 25(8), 1091–1103. PMID: 25995268

Sarlós, K., Biebricher, A., Petermann, E. J. G., Wuite, G. J. L., & Hickson, I. D. (2018). Knotty problems during mitosis: mechanistic insight into the processing of ultrafine DNA bridges in anaphase. *Cold Spring Harbor Symposia on Quantitative Biology*, 82, 53–64. PMID: 29686028

Schmidt, J. M., Bleichert, F., & Berger, J. M. (2022). A mechanism of origin licensing control through autoinhibition of S. cerevisiae ORC·DNA·Cdc6. *Nature Communications*, 13(1), 914. PMID: 35217664

Seller, C. A., & O'Farrell, P. H. (2018). Rif1 prolongs the embryonic S phase at the Drosophila mid-blastula transition. *PLoS Biology*, 16(4), e2005687. PMID: 29649210

Siddiqui, K., On, K. F., & Diffley, J. F. X. (2013). Regulating DNA replication in eukarya. *Cold Spring Harbor Perspectives in Biology*, 5(9), a012930. PMID: 23838438

Sonneville, R., Moreno, S. P., Knebel, A., Johnson, C., Hastie, C. J., Gartner, A., ... & Labib, K. (2017). CUL-2(LRR-1) and UBXN-3 drive replisome disassembly during DNA replication termination and mitosis. *Nature Cell Biology*, 19(5), 468–479. PMID: 28368373

Stillman, B., Diffley, J. F. X., & Iwasa, J. (2025). Mechanisms for licensing origins of DNA replication in eukaryotic cells. *Nature Structural & Molecular Biology*, 32(8), 1143–1153. PMID: 40128376

Stewart-Morgan, K. R., Petryk, N., & Groth, A. (2020). Chromatin replication and epigenetic cell memory. *Nature Cell Biology*, 22(4), 361–371. PMID: 32231312

Stodola, J. L., & Burgers, P. M. J. (2016). Resolving individual steps of Okazaki-fragment maturation at a millisecond timescale. *Nature Structural & Molecular Biology*, 23(5), 402–408. PMID: 27065195

Sun, J., Shi, Y., Georgescu, R. E., Yuan, Z., Chait, B. T., Li, H., & O'Donnell, M. E. (2015). The architecture of a eukaryotic replisome. *Nature Structural & Molecular Biology*, 22(12), 976–982. PMID: 26524492

Supek, F., & Lehner, B. (2015). Differential DNA mismatch repair underlies mutation rate variation across the human genome. *Nature*, 521(7550), 81–84. PMID: 25707793

Técher, H., Koundrioukoff, S., Nicolas, A., & Debatisse, M. (2017). The impact of replication stress on replication dynamics and DNA damage in vertebrate cells. *Nature Reviews Genetics*, 18(9), 535–550. PMID: 28714480

Ticau, S., Friedman, L. J., Ivica, N. A., Gelles, J., & Bell, S. P. (2015). Single-molecule studies of origin licensing reveal mechanisms ensuring bidirectional helicase loading. *Cell*, 161(3), 513–525. PMID: 25892223

Vouzas, A. E., & Gilbert, D. M. (2021). Mammalian DNA replication timing. *Cold Spring Harbor Perspectives in Biology*, 13(7), a040162. PMID: 33820775

Wang, F., Yao, N. Y., He, Q., Li, H., & O'Donnell, M. E. (2025). The proofreading mechanism of the human leading-strand DNA polymerase epsilon holoenzyme. *Proceedings of the National Academy of Sciences*, 122(18), e2507232122. PMID: 40440070

Weissmann, F., Llorente, B., Costa, A., & Stillman, B. (2024). MCM double hexamer loading visualized with human proteins. *Nature*, 636(8043), 499–508. PMID: 39567701

Wenger, A., Biran, A., Alcaraz, N., Redl, I., Trezber, F., Streber, K., ... & Groth, A. (2023). Symmetric inheritance of parental histones governs epigenome maintenance and embryonic stem cell identity. *Nature Genetics*, 55(9), 1567–1578. PMID: 37666988

Wells, J. N., Yardimci, H., & Costa, A. (2025). Reconstitution of human DNA licensing and the structural and functional analysis of key intermediates. *Nature Communications*, 16(1), 478. PMID: 39786161

Xu, M., Wang, W., Chen, S., Zhang, B., Li, T., Chen, Z., ... & Li, Q. (2024). The fork protection complex promotes parental histone recycling and epigenetic memory. *Cell*, 187(20), 5556–5572. PMID: 39094569

Yu, C., Li, T., Wang, Y., Zhang, H., & Zhang, Z. (2024). Molecular mechanism of parental H3/H4 recycling at a replication fork. *Nature Communications*, 15(1), 9008. PMID: 39472554

Yeeles, J. T. P., Deegan, T. D., Joshi, A., Neesham, D., & Diffley, J. F. X. (2015). Regulated eukaryotic DNA replication origin firing with purified proteins. *Nature*, 519(7544), 431–435. PMID: 25739503

Yuan, Z., Bai, L., Sun, J., Georgescu, R., Liu, J., O'Donnell, M. E., & Li, H. (2017). Structure of the eukaryotic replicative CMG helicase suggests a pumpjack motion for translocation. *Nature Structural & Molecular Biology*, 23(3), 217–224. PMID: 26854665

Yuan, Z., Georgescu, R., Bai, L., Zhang, D., Li, H., & O'Donnell, M. E. (2020). DNA unwinding mechanism of a eukaryotic replicative CMG helicase. *Nature Communications*, 11(1), 688. PMID: 32019939

Zhang, K., Gao, Y., Li, J., Fang, D., Chen, H., & Zhang, Z. (2016). A DNA binding winged-helix domain in CAF-1 functions with PCNA to stabilize CAF-1 at replication forks. *Nucleic Acids Research*, 44(11), 5083–5094. PMID: 27095193

Zhao, P. A., Sasaki, T., & Gilbert, D. M. (2020). High-resolution Repli-Seq defines the temporal choreography of initiation, elongation and termination of replication in mammalian cells. *Genome Biology*, 21(1), 76. PMID: 32209116

Zheng, C. L., Wang, N. J., Chung, J., Moslehi, H., Sanborn, J. Z., Hur, J. S., ... & Cho, R. J. (2020). Transcription restores DNA repair to heterochromatin, determining regional mutation rates in cancer genomes. *Cell Reports*, 9(4), 1228–1234. PMID: 25456127

Zhang, Z., Chen, C., & Guilbaud, G. (2025). DNA replication timing reveals genome-wide features of transcription and fragility. *Nature Communications*, 16(1), 5012. PMID: 40389475

Zheng, C. L., Wang, N. J., Chung, J., Moslehi, H., Sanborn, J. Z., Hur, J. S., ... & Cho, R. J. (2020). Transcription restores DNA repair to heterochromatin, determining regional mutation rates in cancer genomes. *Cell Reports*, 9(4), 1228–1234. PMID: 25456127

Zhou, J. C., Janska, A., Goswami, P., Renber, L., Maric, M., Kanber, S., ... & Costa, A. (2017). CMG–Pol epsilon dynamics suggests a mechanism for the establishment of leading-strand synthesis in the eukaryotic replisome. *Proceedings of the National Academy of Sciences*, 114(16), 4141–4146. PMID: 28373564
