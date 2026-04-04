# Trajectory of Computational Interfaces

---

## Abstract

The trajectory of computational technology reveals a consistent pattern: each successive platform brings information processing closer to the human body and brain. From room-sized mainframes to personal computers, smartphones, wearable devices, augmented/virtual reality, and brain-computer interfaces, the frontier of computation has migrated progressively inward. This document argues that the next computational frontier lies within cells themselves, enabled by an emerging toolkit of molecular recording, biological memory, and DNA-based computation technologies. We systematically evaluate six classes of biological information systems — CRISPR-based molecular recording, retron-mediated analog recording, transcriptome capture and epigenetic memory, lineage recording, DNA data storage, and molecular computation — through three interconnected lenses: the in vivo translation gap, information-theoretic capacity and fidelity, and systems integration toward sense-record-compute-respond cellular architectures. For each modality, we derive novel mathematical frameworks quantifying recording capacity, error propagation, and fundamental performance limits. We present evidence that molecular recording technologies have achieved critical milestones — 4,300-bit recording capacity per cell, 7-day transcriptome storage stability, supervised learning in DNA neural networks, and near-Shannon-limit DNA data storage — that collectively establish the feasibility of programming cells as information-processing systems. We conclude by examining the evidence for the cellular computation hypothesis within the broader theory of computational interfaces and identify the key engineering challenges separating current capabilities from therapeutic cellular intelligence.

---

## 1. Introduction: The Theory of Computational Interfaces

### 1.1 The Historical Arc of Human-Computer Proximity

The history of computing is, at its core, a history of shrinking distance between the computational device and the human mind. The first general-purpose electronic computer, ENIAC, occupied 167 square meters and served a single institution. The invention of the transistor in 1947 launched a miniaturization cascade governed by Moore's Law, enabling the personal computer revolution of the 1970s–1980s, which brought computation from the institution to the individual desk (Waldrop, 2016). The mobile phone — particularly the smartphone era inaugurated by the iPhone in 2007 — compressed this further, placing a powerful general-purpose computer in the user's hand, available continuously (West & Mace, 2010). Wearable computing, epitomized by smartwatches and fitness trackers, advanced the frontier to the body's surface, enabling continuous biometric monitoring and just-in-time information delivery (Piwek et al., 2016).

The progression continued with immersive computing. Augmented reality (AR) and virtual reality (VR) headsets position computational output directly within the user's visual field, overlaying or replacing sensory input at the perceptual interface (Billinghurst et al., 2015). The physical distance between the computational device and the brain's sensory processing regions is now measured in centimeters. Meanwhile, the world's smallest 'computer' — measuring just 0.3 mm per side, developed at the [University of Michigan](https://news.umich.edu/u-m-researchers-create-worlds-smallest-computer/) — demonstrates that the physical limits of computational hardware continue to shrink (Wu et al., 2018).

### 1.2 Brain-Computer Interfaces: Computation Reaches the Brain

Brain-computer interfaces (BCIs) represent the first technology to place computational systems in direct contact with neural tissue. Intracortical BCIs have demonstrated decoding of imagined speech at rates exceeding 62 words per minute from neural ensemble activity (Willett et al., 2023). Visual imagery has been reconstructed from functional MRI signals using deep generative models, enabling coarse decoding of perceived and imagined visual content (Takagi & Nishimoto, 2023). Motor BCIs have enabled paralyzed individuals to control robotic limbs and computer cursors through decoded neural signals, with the BrainGate consortium demonstrating sustained cursor control over years of implanted use (Hochberg et al., 2012; Simeral et al., 2021).

These achievements confirm that the computational interface frontier has reached the brain. The information flow is bidirectional: neural signals are decoded (read operations) and electrical stimulation delivers sensory or motor information back to neural circuits (write operations). Cochlear implants and retinal prostheses have provided clinical proof that sensory information can be written to the nervous system through direct electrical stimulation (Wilson & Dorman, 2008; da Cruz et al., 2016).

### 1.3 The Cellular Computation Hypothesis

If computation has migrated from the room to the desk, to the hand, to the body surface, to the visual field, and now to the brain, the natural question is: what lies beyond? We propose that the next computational frontier is within cells themselves — the fundamental units of biological organization.

This hypothesis rests on three converging lines of evidence:

**First, cells already perform computation.** Every living cell processes information: gene regulatory networks implement Boolean logic (Davidson, 2010), signal transduction cascades perform analog computation, the adaptive immune system implements pattern recognition with memory (Farber et al., 2016), and epigenetic modifications store heritable state information across cell divisions (Allis & Jenuwein, 2016). The cell is not a passive vessel but an active information-processing system operating on nucleic acid-encoded instructions.

**Second, molecular recording technologies now enable read and write operations on cellular DNA.** CRISPR-based recorders write event histories into genomic DNA (Tang & Liu, 2018; Sheth et al., 2017), prime editing enables sequential recording of cellular events (Choi et al., 2022), and retron-based systems provide continuous analog recording without double-strand breaks (Farzadfard & Lu, 2014). The central dogma of molecular biology — DNA → RNA → protein — can now be viewed as an addressable, programmable information architecture.

**Third, DNA-based computation has achieved non-trivial computational tasks.** DNA strand displacement neural networks have scaled to pattern classification with supervised learning (Cherry & Qian, 2025), molecular decision trees implement Random Forest classifiers for disease diagnosis (Liu et al., 2025), and heat-rechargeable DNA circuits demonstrate reusable logic computation with over 200 molecular species (Song et al., 2025).

### 1.4 The Cellular Computer Analogy

The analogy between cells and computers, while imperfect, is instructive:

- **Genomic DNA** functions as long-term storage (analogous to a hard drive): stable, high-density, and read-mostly, with the complete human genome (T2T-CHM13) encoding approximately 6.1 × 10⁹ base pairs of information (Nurk et al., 2022).
- **mRNA** functions as active working memory (analogous to RAM): transient, rapidly produced and degraded, representing the currently executing program of the cell.
- **Epigenetic modifications** function as a persistent cache: heritable across cell divisions, faster to read and write than genomic sequence changes, encoding cell-type identity and environmental memory (Allis & Jenuwein, 2016).
- **Gene regulatory circuits** function as processors: implementing logic operations, feedback loops, and signal integration (Cameron et al., 2014).
- **Intercellular communication** — through gap junctions, paracrine signaling, and extracellular vesicles — functions as a biological network, enabling distributed computation across cell populations.

### 1.5 Three Interconnected Challenges

The realization of therapeutic cellular computation faces three interconnected challenges that structure this document:

1. **The in vivo translation gap.** Most molecular recording and DNA computation technologies have been demonstrated in bacteria or mammalian cell lines, with limited in vivo mammalian validation. Translating from the test tube to the living organism requires overcoming delivery, immunogenicity, and scalability barriers.

2. **Information capacity and fidelity limits.** How many bits can a cell reliably store? How long does molecular memory persist? What is the fundamental error rate? Information-theoretic analysis provides rigorous answers that guide technology development.

3. **Systems integration.** Recording, computing, and therapeutic response currently exist as separate technologies. The frontier challenge is integrating them into unified sense-record-compute-respond cellular architectures.

For each molecular recording modality reviewed below, we evaluate its current status on all three fronts, quantify its information-theoretic performance, and assess its potential contribution to the broader cellular computation vision.

---

## 2. CRISPR-Based Molecular Recording

### 2.1 Spacer Acquisition Recording: TRACE and CAMERA

The CRISPR-Cas adaptive immune system naturally records the history of viral infections by incorporating short DNA sequences (spacers) from invading genomes into CRISPR arrays (Barrangou et al., 2007). Sheth, Yim, Wu, and Wang (2017) recognized that this natural recording mechanism could be repurposed for synthetic biology, developing TRACE (Temporal Recording in Arrays by CRISPR Expansion). In TRACE, biological signals trigger intracellular production of defined DNA sequences via reverse transcription, which are then incorporated into CRISPR arrays by the Cas1-Cas2 integration machinery. Because new spacers are preferentially added to one end of the array, temporal order is preserved — earlier events appear further from the leader sequence, later events closer. This "biological tape recorder" enables stable recording over multiple days with accurate reconstruction of temporal and lineage information through sequencing (Sheth et al., 2017).

Tang and Liu (2018) extended this approach with CAMERA (CRISPR-mediated Analog Multi-Event Recording Apparatus), demonstrating two complementary recording systems. CAMERA 1 uses Cas1-Cas2 spacer acquisition to record defined trigger sequences into bacterial CRISPR arrays, providing a digital record of specific inputs. CAMERA 2 employs cytidine base editors to convert C→T at target sites in response to stimuli, enabling rewritable analog recording in both bacterial and mammalian cells. The analog recording feature of CAMERA 2 was particularly significant: by measuring the fraction of C→T conversion at a target site across a cell population, the system records signal intensity and duration as a continuous variable rather than a binary event (Tang & Liu, 2018).

**Information metrics.** Spacer acquisition recording encodes approximately log₂(L) bits per spacer, where L is the number of distinguishable spacer sequences. With typical spacer lengths of ~30 bp drawn from a defined library, each spacer encodes approximately 4–5 bits of identity information plus positional information encoding temporal order. However, the acquisition rate is low (estimated at ~10⁻² spacers per cell per hour under strong induction), limiting temporal resolution (Sheth et al., 2017). The recording is genomically encoded and thus permanent — persisting indefinitely through cell divisions — but is write-once per array position, imposing a fundamental capacity ceiling equal to the number of available CRISPR array slots.

**In vivo status.** Spacer acquisition recording has been demonstrated exclusively in prokaryotic systems. The Cas1-Cas2 integration machinery has not been successfully reconstituted in mammalian cells at recording-relevant efficiencies, representing a significant translation gap. CAMERA 2's base editing approach partially addresses this limitation by operating in mammalian cells, but at the cost of losing the sequential temporal recording property of spacer acquisition.

### 2.2 Base Editing Recorders: DOMINO and ENGRAM

Farzadfard, Gharaei, Certo, and Lu (2019) developed DOMINO (DNA-based Ordered Memory and Iteration Network Operator), which uses base editors at multiple genomic target sites to implement combinatorial recording. Each target site can be independently converted by a signal-specific base editor, and the pattern of edits across multiple sites encodes the combination and order of experienced signals. DOMINO demonstrated that base editing could create computing and memory circuits that operate at single-nucleotide resolution in living cells, implementing Boolean logic gates (AND, OR, NAND) and sequential recording of up to three independent inputs (Farzadfard et al., 2019).

The major leap in base editing recording came with ENGRAM (Enhancer-driven Genomic Recording of transcriptional Activity in Multiplex), published by Chen, Choi, and colleagues in Nature in 2024. ENGRAM converts the transient activity of cis-regulatory elements into stable, permanent genomic records recoverable by DNA sequencing. The system works by placing the expression of prime editing guide RNAs (pegRNAs) under the control of cis-regulatory elements of interest. When a regulatory element is active, it produces its cognate pegRNA, which directs the prime editor to insert a signal-specific barcode ("symbol") into a genomically encoded recording unit. Because each regulatory element drives a unique pegRNA that inserts a distinct symbol, the system enables multiplex recording of the cell-type-specific activities of dozens to hundreds of cis-regulatory elements simultaneously (Chen et al., 2024).

ENGRAM was applied to record the transient activity of nearly 100 transcription factor consensus motifs across daily time windows spanning the differentiation of mouse embryonic stem cells into gastruloids — an in vitro model of early mammalian development. The system demonstrated time- and concentration-dependent genomic recording of WNT, NF-κB, and Tet-On signaling pathway activities with high fidelity, sensitivity, and reproducibility. A detailed protocol for implementing ENGRAM experiments was subsequently published in Nature Protocols (Nathans et al., 2026).

In a parallel advance, Winter and colleagues developed BASELINE (Base Editing for Analog SIgnaL rEcording using Networks of Evolving sites), a CRISPR base editing platform for mammalian-scale single-cell lineage tracing. BASELINE uses a Cas12a adenine base editor to irreversibly edit nucleotides within 50 synthetic target sites integrated into the genome. Remarkably, the system can record more than 4,300 bits of information per cell — a 50-fold improvement over existing recording systems — enabling the reconstruction of high-resolution lineage trees in conjunction with single-cell transcriptomic profiling (Winter et al., 2025).

**Information metrics.** ENGRAM's recording capacity is determined by the number of recording units × the number of distinguishable symbols per unit. With hundreds of regulatory elements each producing distinct symbols, the theoretical capacity reaches thousands of bits per cell. BASELINE achieves 4,300 bits, establishing the current benchmark. Persistence is genomic (permanent through cell divisions). Error rates are governed by base editing specificity: off-target edits introduce noise, while incomplete editing (false negatives) reduces sensitivity. The ENGRAM system achieves >90% concordance between recorded symbols and independent measures of regulatory element activity (Chen et al., 2024).

**In vivo status.** ENGRAM has been demonstrated in mouse embryonic stem cell-derived gastruloids — a significant step toward in vivo applicability but not yet in vivo in intact organisms. BASELINE has been applied in mouse models of pancreatic cancer, representing genuine in vivo recording in mammalian tissue (Winter et al., 2025).

### 2.3 Prime Editing Sequential Recorders: DNA Typewriter and peCHYRON

The DNA Typewriter, developed by Choi, Chen, and colleagues and published in Nature in 2022, represents a landmark in molecular recording technology. The system uses prime editing — a CRISPR technology that can write new genetic information into a specified DNA site without requiring double-strand breaks or donor DNA templates — to achieve sequential, ordered recording of multiple cellular events.

The core innovation is the DNA Tape: a tandem array of partial CRISPR-Cas9 target sites, in which all but the first are truncated at their 5' ends and therefore inactive. A prime editing guide RNA (pegRNA) directs the prime editor to insert a short sequence (a "symbol") at the active site. Critically, this insertion simultaneously deactivates the current site and activates the next site in the array by completing the truncated protospacer. Recording is thus inherently sequential and unidirectional — the physical order of symbols along the tape directly encodes the temporal order of events, much like a typewriter moving from left to right across a page (Choi et al., 2022).

The DNA Typewriter is highly multiplexable: it is compatible with recording thousands of distinct symbols (each encoded by a different pegRNA), and the array length determines the maximum recording duration. A detailed molecular recording protocol was published in Nature Protocols (Liao et al., 2024), providing standardized experimental procedures for implementing DNA Typewriter in mammalian cells.

Building on the same sequential recording principle, Loveless, Li, and colleagues developed peCHYRON (prime editing-based Chronological History Recording by Ordered iNsertion), published in Nature Chemical Biology in 2024. In each step of recording, the prime editor inserts a variable triplet DNA sequence (encoding signal identity) alongside a constant propagator sequence that deactivates the previous insertion site and activates the next. Insertions accumulate sequentially in a unidirectional order, enabling open-ended recording of multiple cellular signals with high temporal resolution in mammalian cells (Loveless et al., 2025).

**Information metrics.** The DNA Typewriter encodes log₂(k) bits per insertion, where k is the number of distinguishable symbols. With k = 16 symbols and a tape length of L = 10 sites, the theoretical capacity is 10 × log₂(16) = 40 bits per tape. Multiple tapes per cell and larger symbol alphabets can scale this substantially. peCHYRON's triplet insertions encode log₂(4³) = 6 bits per position. Persistence is genomic and permanent. The critical limitation is recording speed: prime editing efficiency (~1–30% per site per exposure) determines how rapidly events can be recorded, imposing a fundamental tradeoff between temporal resolution and recording fidelity.

### 2.4 Information-Theoretic Framework for CRISPR Recording

We derive a unified information-theoretic framework for comparing CRISPR-based recording modalities.

**F304: Shannon Channel Capacity of CRISPR Recording**

We model molecular recording as a discrete memoryless channel. Consider a recording system with n independent target sites, each capable of encoding one of k distinguishable symbols (edits), with per-site editing probability p upon signal exposure and error probability ε (probability of writing the wrong symbol or editing the wrong site).

The channel capacity per site is:

```math
C_{\text{site}} = \log_2(k) \cdot (1 - H(\varepsilon))
```

where H(ε) = −ε log₂(ε) − (1 − ε) log₂(1 − ε) is the binary entropy function. For n independent sites, the total recording capacity per cell per generation is:

```math
C_{\text{cell}} = n \cdot p \cdot C_{\text{site}} = n \cdot p \cdot \log_2(k) \cdot (1 - H(\varepsilon))
```

For BASELINE (n = 50 sites, k ≈ 4 symbols per site from A→G transitions, p ≈ 0.8, ε ≈ 0.02):

```math
C_{\text{BASELINE}} = 50 \times 0.8 \times \log_2(4) \times (1 - H(0.02)) \approx 50 \times 0.8 \times 2 \times 0.858 \approx 68.6 \text{ bits/cell/generation}
```

The reported 4,300 bits reflect the combinatorial diversity across the full 50-site array read at single-cell resolution, where the effective alphabet size per site is much larger due to multiple possible edit patterns and their combinations. This highlights how combinatorial encoding across many sites exponentially expands the effective recording capacity beyond the per-site Shannon limit (Winter et al., 2025).

For DNA Typewriter (n = 10 tape positions, k = 16 symbols, p ≈ 0.15 per exposure, ε ≈ 0.05):

```math
C_{\text{Typewriter}} = 10 \times 0.15 \times \log_2(16) \times (1 - H(0.05)) \approx 10 \times 0.15 \times 4 \times 0.714 \approx 4.28 \text{ bits/cell/exposure}
```

The capacity scales linearly with the number of recording events (exposures), reaching the full 40-bit tape capacity after sufficient recording time.

**F305: Markov Chain Model of Sequential Recording Fidelity**

For sequential recorders (DNA Typewriter, peCHYRON), the recording process is a Markov chain where each step depends on the successful completion of the previous step. Define the state space S = {s₀, s₁, ..., s_L} where s_i represents the tape with i completed insertions. The transition probability from state s_i to s_{i+1} given signal j is:

```math
P(s_{i+1} | s_i, \text{signal}_j) = p_{\text{edit}} \times (1 - \varepsilon_{\text{skip}}) \times (1 - \varepsilon_{\text{symbol}})
```

where p_edit is the per-site editing efficiency, ε_skip is the probability of skipping a site (propagator failure), and ε_symbol is the probability of inserting the wrong symbol.

The probability of correctly recording a sequence of L events in the correct order is:

```math
P(\text{correct sequence of length } L) = \prod_{i=1}^{L} P(s_i | s_{i-1}, \text{signal}_i) = \left[p_{\text{edit}} (1 - \varepsilon_{\text{skip}})(1 - \varepsilon_{\text{symbol}})\right]^L
```

This reveals an exponential decay in recording fidelity with sequence length. For DNA Typewriter with p_edit = 0.15, ε_skip = 0.01, ε_symbol = 0.03:

```math
P(\text{correct, } L=5) = (0.15 \times 0.99 \times 0.97)^5 = (0.144)^5 \approx 5.6 \times 10^{-5}
```

This low per-cell probability is compensated by recording across large populations (>10⁴ cells), where at least some cells will have undergone complete recording — a strategy explicitly leveraged by both DNA Typewriter and peCHYRON, which read recording outcomes across cell populations rather than relying on single-cell perfection (Choi et al., 2022; Loveless et al., 2025).

---

## 3. Retron-Based Recording and Engineered Reverse Transcriptases

### 3.1 SCRIBE: Analog Recording via In Vivo ssDNA Production

Retrons are bacterial genetic elements comprising a reverse transcriptase (RT) and a non-coding RNA (ncRNA) template. The RT uses the ncRNA as a template to produce multicopy single-stranded DNA (ssDNA) in vivo, which can direct precise mutations at target genomic loci through recombination. Farzadfard and Lu (2014) exploited this natural mechanism to develop SCRIBE (Synthetic Cellular Recorders Integrating Biological Events), a system that records biological signals as analog genomic mutations in living bacterial populations. When a signal of interest (e.g., an inducer molecule) activates retron expression, ssDNA is produced and recombines with a target genomic locus, introducing precise mutations at a rate proportional to signal intensity and duration. The fraction of cells in a population carrying the mutation thus serves as an analog record of the input signal (Farzadfard & Lu, 2014).

SCRIBE's analog recording property distinguishes it fundamentally from digital recording systems. Rather than recording a binary "event occurred / did not occur," SCRIBE records the magnitude and duration of exposure — information that would require multiple bits in a digital system but is naturally encoded in the mutation frequency of a cell population.

### 3.2 Retro-Cascorder and Temporal Resolution

The Retro-Cascorder, detailed in a Nature Protocols publication, extended retron-based recording to achieve temporally resolved transcriptional recording in E. coli (Lear et al., 2023). By coupling retron-mediated ssDNA production to transcriptional signals and reading out the accumulated mutations over time, the Retro-Cascorder demonstrated that the temporal dynamics of gene expression could be stably recorded into genomic DNA and subsequently reconstructed.

### 3.3 Multiplexed Retron Arrays and Mammalian Translation

A critical advance came with the development of "multitrons" — retron arrays that enable simultaneously modifying multiple sites on a single genome from a single transcript. González-Delgado, Lopez, and colleagues demonstrated that multiple donor-encoding DNAs can be produced from a single multitron transcript, enabling parallel recording at multiple genomic addresses. Applications include molecular recording, genetic element minimization, and metabolic engineering (González-Delgado et al., 2024).

However, retron efficiency in mammalian cells remained a major bottleneck. Cattle and colleagues identified two critical obstacles: non-coding RNA instability (the retron ncRNA is rapidly degraded in mammalian cells) and impaired Cas9 activity (the retron ncRNA structure interferes with sgRNA function). They engineered the Eco1 ncRNA and devised an RNA processing strategy to increase steady-state ncRNA levels and rescue sgRNA activity, substantially increasing templated repair efficiency in human cells (Cattle et al., 2025).

The most significant retron advance of 2025 came from Buffington and colleagues, who performed a systematic bioinformatic analysis of metagenomic data to discover retron reverse transcriptases that are highly active in mammalian cells. Through functional screening of thousands of candidate retrons, they identified variants with dramatically improved mammalian activity, opening the door to retron-based recording and editing in vertebrate systems (Buffington et al., 2025).

### 3.4 Analog vs. Digital Recording: Complementary Modalities

Retron-based systems offer fundamental advantages for certain recording tasks. Unlike CRISPR spacer acquisition (digital, sequential) or prime editing (digital, sequential), retron recording is inherently analog: the mutation frequency in a population continuously reflects cumulative signal exposure. This makes retrons naturally suited for recording graded signals — hormone concentrations, temperature fluctuations, nutrient availability — where the relevant information is in the magnitude rather than the identity of the stimulus.

The tradeoff is temporal resolution: because retron recording accumulates mutations over time, it provides excellent integration (total signal exposure) but limited temporal discrimination (when specific events occurred). Sequential digital recorders like DNA Typewriter excel at temporal ordering but sacrifice analog magnitude information. Optimal recording architectures may combine both modalities.

**In vivo status.** Retron recording is well-established in bacteria. Mammalian retron efficiency has improved dramatically with engineered ncRNAs (Cattle et al., 2025) and metagenomically-discovered high-activity variants (Buffington et al., 2025), but in vivo mammalian recording has not yet been demonstrated.

### 3.5 Information-Theoretic Framework for Analog Recording

**F306: Fisher Information Bounds on Retron Analog Recording Precision**

We model retron analog recording as estimation of a signal parameter θ (e.g., inducer concentration × exposure time) from the observed mutation frequency f in a population of N cells. Each cell independently undergoes mutation with probability p(θ) = 1 − e^(−λθ), where λ is the retron-mediated mutation rate constant.

The Fisher information for estimating θ from N independent Bernoulli observations is:

```math
I(\theta) = N \cdot \frac{[p'(\theta)]^2}{p(\theta)(1 - p(\theta))} = N \cdot \frac{\lambda^2 e^{-2\lambda\theta}}{(1 - e^{-\lambda\theta}) \cdot e^{-\lambda\theta}} = N \cdot \frac{\lambda^2 e^{-\lambda\theta}}{1 - e^{-\lambda\theta}}
```

By the Cramér-Rao bound, the minimum variance of any unbiased estimator of θ is:

```math
\text{Var}(\hat{\theta}) \geq \frac{1}{I(\theta)} = \frac{1 - e^{-\lambda\theta}}{N \lambda^2 e^{-\lambda\theta}}
```

This yields two important design principles:

1. **Population size N is critical:** The precision of analog recording scales as 1/√N, meaning that recording across 10⁴ cells provides 100-fold better signal resolution than recording across a single cell. This is fundamentally why retron recording operates at the population level (Farzadfard & Lu, 2014).

2. **Optimal operating regime:** The Fisher information is maximized when p(θ) ≈ 0.5 (i.e., λθ ≈ 0.69), corresponding to the point where half the cells have mutated. Operating far from this optimum — either with very low or very high mutation frequencies — degrades signal resolution exponentially.

For SCRIBE with λ ≈ 0.1 hr⁻¹, N = 10⁶ cells, at optimal θ* ≈ 6.9 hours:

```math
\text{Var}(\hat{\theta})_{\min} = \frac{0.5}{10^6 \times 0.01 \times 0.5} = \frac{1}{10^4} = 10^{-4} \text{ hr}^2
```

yielding a minimum detectable signal change of ~0.01 hours (36 seconds) — remarkably precise analog resolution from a population of one million cells.

---

## 4. Transcriptome Capture and Durable Epigenetic Memory

### 4.1 TimeVault: Molecular Time Travel for Cellular Transcriptomes

In 2025, a transformative technology was published in Science: TimeVault, a genetically encoded "molecular time machine" that enables living cells to record and store complete snapshots of their cytosolic transcriptomes for future retrieval and sequencing (Chao et al., 2026).

TimeVault exploits vault particles — large (13 MDa), hollow, barrel-shaped protein shells that naturally self-assemble in the cytoplasm of most eukaryotic cells but whose endogenous function had remained enigmatic for decades. The engineering strategy was elegant: vault particles were modified to incorporate a poly(A)-binding protein (PABPC1) domain on their interior surface. When expressed in cells, these engineered vault particles capture cytosolic mRNAs through their poly(A) tails and encapsulate them within the protective vault shell (Chao et al., 2026).

The stored transcriptome is stable in living cells for more than 7 days — far exceeding the ~2–8 hour average half-life of mammalian mRNAs — because the vault shell physically protects encapsulated RNAs from cytoplasmic nucleases and degradation pathways. Stored mRNAs can be released and sequenced on demand by lysing cells and disrupting vault particles, yielding a transcriptome-wide snapshot of the cell's state at the time of capture.

TimeVault was applied to capture transient stress responses and to reveal gene expression changes underlying drug-naïve persister states in lung cancer cells that evade epidermal growth factor receptor (EGFR) inhibition. By capturing transcriptomes before drug treatment and then analyzing surviving persister cells, TimeVault linked past gene expression patterns to future cell fates — a form of biological retrospection that was previously impossible (Chao et al., 2026).

**Information metrics.** TimeVault captures the full mRNA content of a cell at a single moment — approximately ~200,000 mRNA molecules representing ~10,000–15,000 expressed genes in a typical mammalian cell. At single-gene resolution, this represents ~15,000 × log₂(dynamic range) ≈ 15,000 × 14 ≈ 210,000 bits of transcriptomic information per cell per capture event. Persistence is 7+ days in living cells. The technology does not alter the genome, making it non-heritable but repeatable through re-expression of vault particle components.

**In vivo status.** TimeVault has been demonstrated in mammalian cell lines (including lung cancer cells). In vivo demonstration in living organisms has not yet been reported, but the use of endogenous vault protein scaffolds suggests favorable biocompatibility.

### 4.2 CRISPRoff and Durable Epigenetic Gene Silencing

While molecular recording writes new information into DNA sequence, epigenetic memory stores information as chemical modifications to DNA and histone proteins — without altering the underlying genetic sequence. CRISPRoff, developed by Nuñez, Chen, and colleagues and published in Cell in 2021, is a programmable epigenetic editor that achieves heritable gene silencing by simultaneously installing two repressive epigenetic marks: DNA methylation (via fused DNMT3A/DNMT3L methyltransferase domains) and H3K9me3 (via the KRAB repressor domain). The combination of DNA methylation and H3K9me3 creates a self-reinforcing silencing state that is faithfully propagated through cell divisions by endogenous maintenance machinery (DNMT1 for DNA methylation, HP1/SUV39H1 for H3K9me3), without requiring continued expression of CRISPRoff (Nuñez et al., 2021).

A landmark 2024 study in Nature demonstrated "hit-and-run" epigenome editing in vivo. Researchers delivered zinc-finger-based epigenetic editors via lipid nanoparticles loaded with the editors' mRNAs, achieving near-complete silencing of mouse Pcsk9 that persisted for nearly one year from a single administration. Critically, silencing and accompanying epigenetic repressive marks persisted even after forced liver regeneration (two-thirds partial hepatectomy), demonstrating that the newly installed epigenetic state was genuinely heritable through cell division in vivo (Cappelluti et al., 2024).

CRISPRoff has been further developed for clinical translation. Pattali and colleagues demonstrated programmable CRISPRoff epigenetic editing in human cell lines and primary T cells, showing that CRISPRoff-mediated gene silencing is durable, efficient, and compatible with therapeutic cell engineering workflows (Pattali et al., 2025). Separately, the RENDER (Robust ENveloped Delivery of Epigenome-editor Ribonucleoproteins) system enabled transient delivery of programmable CRISPRoff as ribonucleoprotein complexes, inducing durable epigenetic silencing across various human cell types without permanent transgene integration (Xu et al., 2025). A complementary approach using mRNA-encoded CRISPR epigenetic editors (CRISPR OFF-EE) demonstrated durable gene silencing in vivo, using intein-split SpCas9 or the compact Cas-SF01 to overcome mRNA packaging constraints (Wang et al., 2026).

**Information metrics.** Each CRISPRoff-targeted locus stores 1 bit of state information (silenced/active). With multi-guide targeting, the system can simultaneously control 10–100 loci, encoding up to 100 bits per cell. The defining advantage is persistence: epigenetic memory survives cell division indefinitely (demonstrated over months in vivo), making it the most durable engineered memory system outside of sequence modification. Error rate is asymmetric: spontaneous reactivation occurs at ~1–5% per cell division for single-mark silencing but is effectively zero for the dual CRISPRoff mechanism (Nuñez et al., 2021; Cappelluti et al., 2024).

### 4.3 Analog Epigenetic Memory: Beyond Binary States

A paradigm-shifting discovery published in Cell Genomics in 2025 revealed that epigenetic memory is not merely binary (on/off) but analog. Researchers demonstrated that targeted chromatin editing can install distinct grades of DNA methylation at a locus, and that these graded methylation states lead to corresponding, persistent gene expression levels maintained over multiple cell divisions. This "analog epigenetic memory" means that cells can store continuous-valued information — not just 1 bit per locus, but potentially many bits encoded in the methylation level (Palacios et al., 2025).

This finding transforms the information-theoretic analysis of epigenetic memory. If a locus can maintain, say, 8 distinguishable methylation levels stably over 10+ cell divisions, each locus encodes log₂(8) = 3 bits rather than 1 bit, tripling the information density of epigenetic storage.

### 4.4 Information-Theoretic Frameworks for Transcriptome Capture and Epigenetic Memory

**F307: Poisson Sampling Theory for Transcriptome Capture (TimeVault)**

We model vault particle mRNA capture as a stochastic Poisson sampling process. Let G be the total number of expressed genes, and let N_v be the number of vault particles per cell. Each vault particle captures mRNAs with probability proportional to abundance. For a gene expressed at level r_i (mRNA copies per cell), the expected number of captures by N_v vault particles, each with capture probability α, is:

```math
\lambda_i = \alpha \cdot N_v \cdot \frac{r_i}{R_{\text{total}}}
```

where R_total = Σ r_i is the total mRNA content. The probability of detecting gene i (at least one capture) is:

```math
P(\text{detect gene } i) = 1 - e^{-\lambda_i} = 1 - \exp\left(-\alpha N_v \frac{r_i}{R_{\text{total}}}\right)
```

For a gene at the 10th percentile of expression (r_i/R_total ≈ 10⁻⁵) with N_v = 10⁴ vault particles and α = 0.1:

```math
P(\text{detect}) = 1 - e^{-0.1 \times 10^4 \times 10^{-5}} = 1 - e^{-0.01} \approx 0.01
```

This reveals that TimeVault's transcriptome capture is inherently biased toward highly expressed genes, with low-abundance transcripts requiring either more vault particles or higher capture efficiency for reliable detection — a fundamental sampling limitation shared with all bulk capture approaches. The total information captured scales as:

```math
I_{\text{capture}} = \sum_{i=1}^{G} P(\text{detect } i) \cdot \log_2\left(\frac{r_i}{\delta r_i}\right)
```

where δr_i is the resolution with which abundance can be estimated, governed by the Poisson counting statistics of capture events.

**F308: Fokker-Planck Equation for Analog Epigenetic Memory Dynamics**

We model the methylation state m ∈ [0, 1] of a CpG site as a continuous variable subject to deterministic maintenance (drift) and stochastic fluctuations (diffusion) during DNA replication. The probability density p(m, t) of methylation level m at time t (measured in cell divisions) evolves according to the Fokker-Planck equation:

```math
\frac{\partial p}{\partial t} = -\frac{\partial}{\partial m}\left[\mu(m) \cdot p\right] + \frac{1}{2}\frac{\partial^2}{\partial m^2}\left[\sigma^2(m) \cdot p\right]
```

where the drift coefficient μ(m) captures the deterministic tendency of maintenance methyltransferases (DNMT1) to preserve the methylation state:

```math
\mu(m) = \alpha \cdot m \cdot (1 - m) \cdot \text{sgn}(m - m_0)
```

Here α is the maintenance strength and m₀ is the equilibrium methylation level. The diffusion coefficient σ²(m) = β · m · (1 − m) captures replication-associated stochastic errors (failure to methylate a daughter strand, or inappropriate de novo methylation).

At steady state (∂p/∂t = 0), the equilibrium distribution is:

```math
p_{\text{ss}}(m) \propto \frac{1}{\sigma^2(m)} \exp\left(2\int_0^m \frac{\mu(m')}{\sigma^2(m')} dm'\right) = \frac{1}{\beta m(1-m)} \exp\left(\frac{2\alpha}{\beta}\int_0^m \text{sgn}(m'-m_0) dm'\right)
```

For strong maintenance (α/β >> 1), this distribution becomes sharply peaked around m₀, indicating stable memory. For weak maintenance (α/β ~ 1), the distribution broadens, indicating memory degradation. The memory half-life — the time for the variance of m to double from its installed value — scales as:

```math
t_{1/2} \sim \frac{\alpha}{\beta^2} \propto \frac{\text{maintenance fidelity}}{(\text{replication noise})^2}
```

This framework explains why dual-mark silencing (CRISPRoff) is more durable than single-mark silencing: the two marks (DNA methylation and H3K9me3) provide independent maintenance mechanisms, effectively multiplying α while keeping β constant, yielding an exponentially longer memory half-life (Nuñez et al., 2021; Cappelluti et al., 2024).

---

## 5. Lineage Recording and Developmental Cartography

### 5.1 Foundational Systems: GESTALT and scGESTALT

The application of molecular recording to developmental biology began with GESTALT (Genome Editing of Synthetic Target Arrays for Lineage Tracing), developed by McKenna, Findlay, and colleagues and published in Science in 2016. GESTALT uses an array of CRISPR/Cas9 target sites as a genomically integrated barcode. During development, Cas9-induced mutations accumulate in the barcode array, generating unique patterns of insertions and deletions (indels) that serve as heritable lineage marks. By sequencing barcodes from hundreds of thousands of cells in adult zebrafish, McKenna and colleagues demonstrated that most cells in adult organs derive from relatively few embryonic progenitors and reconstructed phylogenetic lineage trees based on shared mutation patterns (McKenna et al., 2016).

Raj extended this approach with scGESTALT, which combines CRISPR barcode recording with single-cell RNA sequencing. This integration enabled simultaneous readout of lineage histories and cell-type identities from individual cells in the developing zebrafish brain, revealing that transcriptionally similar cell types can arise from distinct lineage origins — a finding with profound implications for understanding the relationship between cell identity and developmental history (Raj et al., 2025).

### 5.2 CARLIN: Inducible Lineage Recording in Mice

Bowling, Sritharan, and colleagues developed CARLIN (CRISPR Array Repair Lineage Tracing), the first inducible lineage recording system in mice. The CARLIN mouse carries a stably integrated array of Cas9 target sites and an inducible Cas9 transgene, enabling lineage recording to be initiated at any point during development or adulthood. Upon Cas9 induction, mutations accumulate in the target array, generating up to 44,000 distinguishable transcribed barcodes. Critically, because the barcodes are transcribed, they can be simultaneously captured with single-cell transcriptomics, enabling joint readout of lineage and gene expression (Bowling et al., 2020).

CARLIN has been applied to study hematopoietic stem cell dynamics, tissue homeostasis, and tumor evolution, demonstrating the power of inducible recording for longitudinal studies in adult organisms. The system has been further refined as DARLIN, with enhanced clonal diversity and improved lineage resolution (Yang et al., 2025).

### 5.3 BASELINE: The 4,300-Bit Barrier

As described in Section 2.2, BASELINE's 4,300-bit recording capacity represents a 50-fold improvement over prior lineage recording systems. When applied to a mouse model of pancreatic cancer, BASELINE resolved fine-grained clonal structures within tumors, identified rare clones with distinct transcriptional programs, and tracked clonal evolution during tumor progression — demonstrating that high-information recording enables biological insights that were previously invisible at lower resolution (Winter et al., 2025).

### 5.4 DuTracer and Temporal Recording of Development

DuTracer, published in Cell Reports in 2025, introduced a dual-nuclease approach to lineage recording. By employing two orthogonal CRISPR nucleases (Cas9 and Cas12a) that edit independent barcode arrays, DuTracer achieves enhanced recording with minimized target dropout and potentially deeper phylogenetic tree reconstruction. Applied in mouse embryoid bodies and neuromesodermal organoids, DuTracer resolved lineage relationships between differentiated cell types and identified transcription factors such as Foxb1 as modulators of cell fate determination (Chen et al., 2025a).

A particularly significant advance was the development of a multipurpose single-cell CRISPR platform for temporal recording of mammalian development and precancer, published in Nature in 2024 by Islam, Yang, and colleagues. This system incorporates a molecular clock approach — using the accumulation rate of CRISPR-induced mutations as a temporal reference — to record not just lineage relationships but the precise timing of cellular events in vivo. Applied during mouse embryonic development, the platform uncovered the timing of tissue-specific cell expansion and identified unconventional developmental relationships between cell types. Extended to precancerous tissues, the same platform tracked the timing of clonal expansion events that precede malignant transformation (Islam et al., 2024).

### 5.5 Information-Theoretic Framework for Lineage Reconstruction

**F309: Maximum Likelihood Phylogenetic Reconstruction from Molecular Barcodes**

Lineage tree reconstruction from molecular barcodes is fundamentally an inference problem: given the observed pattern of mutations across cells, what is the most likely phylogenetic tree? We formalize this using maximum likelihood estimation.

Let T denote a candidate phylogenetic tree topology with branch lengths {b_e} for each edge e, and let D = {d₁, d₂, ..., d_N} denote the observed barcode data from N cells, where each d_i is a vector of mutation states at M barcode sites. Assuming independence across barcode sites, the likelihood function is:

```math
L(T, \{b_e\} | D) = \prod_{j=1}^{M} P(D_j | T, \{b_e\}, \mu)
```

where D_j is the column of mutations at site j across all cells, and μ is the per-site mutation rate per unit time. For a given tree topology, the per-site likelihood P(D_j | T, {b_e}, μ) is computed by the pruning algorithm, summing over all possible ancestral states at internal nodes (Yang & Rannala, 2012).

The Cramér-Rao bound on the minimum variance of branch-length estimation is:

```math
\text{Var}(\hat{b}_e) \geq \frac{1}{I_{ee}} = \frac{1}{M \cdot \mathcal{I}(\mu, b_e)}
```

where I_ee is the diagonal element of the Fisher information matrix corresponding to edge e, and 𝓘(μ, b_e) is the per-site Fisher information for that branch. For an edit-based recording system with mutation rate μ:

```math
\mathcal{I}(\mu, b_e) = \frac{\mu^2 e^{-2\mu b_e}}{(1 - e^{-\mu b_e}) e^{-\mu b_e}} = \frac{\mu^2 e^{-\mu b_e}}{1 - e^{-\mu b_e}}
```

This reveals a critical design tradeoff: **barcode complexity M determines resolution.** BASELINE's M = 50 sites with combinatorial edit patterns provides ~4,300 bits of barcode diversity, enabling discrimination of ~2^4300 unique lineage histories — vastly exceeding the ~10¹⁴ cells in a human body. The tree reconstruction accuracy scales as 1/√M, establishing a direct quantitative link between recording capacity and developmental cartography resolution (Winter et al., 2025).

**In vivo status.** Lineage recording represents the most mature in vivo application of molecular recording technology. CARLIN and DARLIN mice, the temporal recording platform, and BASELINE have all been demonstrated in living mice, including in disease models (cancer, development). Non-human primate studies are emerging. Human applications remain future goals, but the path from mouse to human is well-defined.

---

## 6. DNA Data Storage and Molecular Computation

### 6.1 DNA as an Information Storage Medium

DNA possesses extraordinary information storage properties. With four bases (A, T, G, C) encoding 2 bits per nucleotide and a molecular density of ~10¹⁸ bytes per cubic millimeter, DNA offers approximately 10⁶-fold greater storage density than state-of-the-art semiconductor memory (Church et al., 2012). DNA is also remarkably durable: intact DNA has been recovered from permafrost specimens tens of thousands of years old, and properly stored synthetic DNA maintains fidelity for centuries at room temperature (Grass et al., 2015).

Erlich and Zielinski (2017) demonstrated that DNA storage could approach the theoretical information capacity limit by applying fountain codes (a class of rateless erasure codes) to the encoding problem. Their DNA Fountain scheme stored a complete computer operating system, a movie, and other files totaling 2.14 megabytes in DNA oligonucleotides, achieving an information density of 1.57 bits per nucleotide — 60% of the 2-bit theoretical maximum — while maintaining perfect data recovery after synthesis, storage, and sequencing (Erlich & Zielinski, 2017).

Organick, Ang, and colleagues (2018) extended this to random-access DNA storage, demonstrating that specific files could be selectively retrieved from a pool of 200 MB of data encoded in DNA using PCR-based random access — analogous to reading a specific file from a hard drive without sequencing the entire archive (Organick et al., 2018).

### 6.2 Living DNA Storage: Cells as Data Archives

A frontier development is the use of living cells as DNA storage containers. Liu, Ping, and colleagues (2025) engineered a living memory microspheroid-based archival file system using bacteria encapsulated in matrix material via droplet microfluidics. Each bacterial population carries a specific plasmid encoding digital data, and the microspheroids can be stored at room temperature following lyophilization. Upon rehydration, each type exhibits specific functions expressed by the plasmids, enabling random access to stored information. The system achieved 94% rewriting reliability and stable storage over hundreds of bacterial generations, demonstrating that living organisms can serve as self-replicating data archives (Liu et al., 2025).

This approach exploits a fundamental advantage of biological storage: living cells possess endogenous machinery for DNA replication and error correction. While semiconductor storage media degrade through charge leakage and environmental damage, biological storage is actively maintained by cellular repair systems — at the cost of introducing a low rate of mutations (~10⁻⁹ per base per replication in bacteria with mismatch repair) that must be managed through error-correcting codes.

### 6.3 DNA Strand Displacement Neural Networks

Beyond passive storage, DNA molecules can perform active computation through carefully designed strand displacement reactions. Qian and Winfree (2011) demonstrated that DNA strand displacement cascades can implement neural network computation, constructing a four-input, four-output neural network that performed pattern recognition — specifically, identifying handwritten digits from a simplified 20-pixel representation. The system used ~100 distinct DNA strands that interact through toehold-mediated strand displacement reactions, implementing weighted sums and thresholding operations analogous to artificial neurons (Qian & Winfree, 2011).

Cherry and Qian (2018) scaled this approach dramatically, constructing winner-take-all DNA neural networks with up to 9 classes and 100-bit inputs. The system correctly classified handwritten digits and demonstrated that molecular pattern recognition could approach the complexity of simple machine learning tasks (Cherry & Qian, 2018).

### 6.4 Supervised Learning in DNA (2025)

A breakthrough published in Nature in 2025 demonstrated that DNA molecules can be programmed to autonomously carry out supervised learning in vitro. Cherry and Qian showed that a DNA neural network could learn to classify three different sets of 100-bit patterns by integrating training data directly into molecular memories stored as DNA concentrations. The system processes molecular examples of inputs and desired responses, updates its internal "weights" (encoded as strand concentrations), and then uses these learned memories to classify subsequent test data — implementing the fundamental learning-from-examples paradigm that underlies modern machine learning, but using DNA molecules instead of silicon transistors (Cherry & Qian, 2025).

### 6.5 DNA Decision Trees and Molecular Classifiers

Liu and colleagues published an interpretable molecular decision-making system in Nature Communications in 2025, demonstrating that classification rules could be modularly embedded into DNA strand displacement reaction cascades organized as decision trees. The system supports cascaded networks exceeding 10 layers, parallel computation of 13 decision trees in a Random Forest classifier involving 333 distinct DNA strands, and multimode operation (linear/nonlinear, binary/multi-class). When coupled with a DNA-methylation sensing module, the system translated biomarker profiles into molecular instructions for tree traversal, enabling accurate disease subtype classification directly from biological inputs (Liu et al., 2025).

Complementarily, a spatially localized DNA integrated circuits classifier was constructed on two-dimensional DNA origami, using the origami as a framework with localized processing modules that execute arithmetic operations for efficient linear classification of complex molecular patterns for cancer diagnosis (Li et al., 2024).

### 6.6 Heat-Rechargeable DNA Circuits

A fundamental limitation of DNA strand displacement computing is that reactions are thermodynamically irreversible — once a computation is performed, the circuit reaches equilibrium and cannot compute again without resynthesizing all components. Song, Hernandez, and colleagues, publishing in Nature in 2025, demonstrated that heat can restore enzyme-free DNA circuits from equilibrium to out-of-equilibrium states, enabling complex logic operations and neural networks to perform multiple computations. During heating, nucleic acids with strong secondary structures reach kinetically trapped states, providing energy for subsequent computation upon cooling. The system demonstrated at least 16 rounds of computation with varying sequential inputs, using circuits with more than 200 distinct molecular species — establishing a universal energy source for molecular machines (Song et al., 2025).

### 6.7 Information-Theoretic Frameworks

**F310: Gilbert-Varshamov and Singleton Coding-Theoretic Bounds for DNA Data Storage**

We derive the fundamental limits of DNA data storage capacity under biologically relevant constraints. DNA encodes information in a quaternary alphabet Σ = {A, T, G, C}, but biological constraints — GC-content balance (required for thermal stability and synthesis fidelity), avoidance of homopolymer runs (which cause sequencing errors), and absence of restriction enzyme sites — reduce the effective alphabet.

For an unconstrained quaternary channel of length n, the maximum information content is 2n bits. Under a constraint that sequences must have GC-content within [0.4, 0.6] and maximum homopolymer run length ≤ 3, the effective per-nucleotide capacity is reduced to:

```math
C_{\text{eff}} = \lim_{n \to \infty} \frac{1}{n} \log_2 |\mathcal{S}_n|
```

where 𝒮_n is the set of valid sequences of length n satisfying all constraints. For the GC-content and homopolymer constraints, the effective capacity is approximately 1.58 bits per nucleotide (Erlich & Zielinski, 2017).

The Gilbert-Varshamov bound provides the maximum achievable code rate for error correction. For a quaternary code of length n that can correct up to t substitution errors, the maximum code rate R satisfies:

```math
R \geq 1 - H_4\left(\frac{2t}{n}\right)
```

where H₄(x) = −x log₄(x) − (1 − x) log₄(1 − x) is the quaternary entropy function and 2t/n is the fractional minimum distance. For a target error tolerance of 10⁻¹² (archival quality) with raw synthesis/sequencing error rate of ~1% and oligo length n = 200:

```math
R \geq 1 - H_4(0.02) \approx 1 - 0.049 = 0.951
```

yielding an achievable net capacity of ~0.951 × 1.58 ≈ 1.50 bits per nucleotide after error correction — close to the 1.57 bits/nt achieved empirically by DNA Fountain (Erlich & Zielinski, 2017).

The Singleton bound provides an absolute upper limit: any code with minimum distance d over an alphabet of size q satisfies:

```math
R \leq 1 - \frac{d - 1}{n} \cdot \frac{\log_2 q}{\log_2 q}  = 1 - \frac{d-1}{n}
```

For practical DNA storage with d = 5 (correcting 2 errors) and n = 200: R ≤ 1 − 4/200 = 0.98, confirming that current coding schemes operate near the theoretical optimum.

**F311: Computational Complexity and Expressiveness of DNA Strand Displacement Networks**

We characterize the computational power of DNA strand displacement (DSD) networks using circuit complexity theory. A DSD network with N distinct molecular species and maximum concentration C_max can be modeled as an analog circuit where each species represents a node and each strand displacement reaction represents a weighted connection.

The computational expressiveness of a DSD neural network with d layers (cascade depth) and w species per layer (width) is bounded by:

```math
\text{VC dimension} \leq O(d \cdot w \cdot \log_2(d \cdot w))
```

This follows from the fact that DSD reactions implement piecewise-linear activation functions (through toehold-mediated threshold behavior), and piecewise-linear neural networks have VC dimension polynomial in depth × width (Bartlett et al., 2019).

For Cherry and Qian's supervised learning system (d ≈ 3 layers, w ≈ 100 species):

```math
\text{VC dim} \leq O(3 \times 100 \times \log_2(300)) \approx O(2500)
```

This is sufficient to correctly classify the 100-bit input patterns demonstrated experimentally (requiring VC dimension ≥ 100 for arbitrary classification of 100 patterns). The computational bottleneck is not expressiveness but **speed**: each DSD reaction requires ~10 minutes to hours to approach equilibrium, limiting the throughput to ~1–10 classifications per hour compared to ~10⁹ per second for silicon neural networks (Cherry & Qian, 2025).

**In vivo status.** DNA data storage is almost entirely an in vitro technology. The notable exception is living memory microspheroids, which store data in living bacteria (Liu et al., 2025). DNA computation via strand displacement has not been demonstrated in living cells, as the controlled concentrations and purified conditions required for reliable computation are difficult to achieve in the complex intracellular environment. This represents the largest in vivo gap of any molecular information technology.

---

## 7. The Cellular Computation Horizon: From Recording to Therapeutic Intelligence

### 7.1 Sense-Record-Compute-Respond: The Integration Frontier

The technologies reviewed in Sections 2–6 represent individual capabilities — recording, memory, storage, computation — that currently exist as separate systems. The transformative potential of molecular information technology lies in their integration into unified cellular architectures that can sense environmental signals, record their history, compute appropriate responses, and execute therapeutic actions.

Early steps toward integration have been demonstrated. ENGRAM combines signal sensing (via cis-regulatory elements) with recording (via prime editing), creating a system where the identity and intensity of signaling pathway activity is written into DNA (Choi et al., 2024). Synthetic biology has produced cells with sense-and-respond circuits using engineered receptors (synNotch, MESA, SNIPR) that detect specific extracellular ligands and trigger programmable transcriptional responses (Morsut et al., 2016; Roybal et al., 2016). CAR-T cells already implement a basic sense-respond architecture: the chimeric antigen receptor senses tumor antigens and triggers T cell activation.

The missing capabilities are recording and computation. Current CAR-T cells cannot record the history of signals they have encountered (e.g., the sequence of antigens in the tumor microenvironment), nor can they compute complex decisions (e.g., "activate only if antigen A was detected before antigen B, and the cumulative exposure exceeded a threshold"). Integrating molecular recording with gene circuit computation would enable "smart" therapeutic cells with unprecedented decision-making capabilities.

A concrete near-term integration would couple TimeVault transcriptome capture with ENGRAM signaling recording: a cell that simultaneously captures its mRNA state (via TimeVault) and records the history of signaling inputs it has received (via ENGRAM), creating a comprehensive "black box" record linkable to therapeutic outcomes.

### 7.2 The Theory of Computational Interfaces Extended

The progression of computational interfaces from institutional mainframes to cellular molecular recording systems reveals a consistent pattern governed by two principles:

**Principle 1: Proximity to cognition.** Each successive computational interface reduces the physical and functional distance between the computing device and the site of human information processing. The brain is the organ of cognition; BCIs have demonstrated that direct neural interface is both feasible and therapeutically valuable (Willett et al., 2023). Cellular computation extends this trajectory to the fundamental units of biological organization — the cells that constitute the brain and every other tissue.

**Principle 2: Integration with biological substrate.** External computational devices (PCs, phones) interact with biology through sensory transduction — photons hitting the retina, sound waves hitting the cochlea. Wearables measure biological parameters (heart rate, motion) through physical sensors. BCIs directly interface with neural electrical signals. Cellular computation represents the ultimate integration: the computational device *is* the biological substrate. DNA serves as both the cell's endogenous instruction set and the engineered recording medium; gene regulatory circuits serve as both the cell's natural control system and the engineered computational logic.

The evidence supporting the cellular computation hypothesis has grown substantially:

1. **Information capacity is sufficient.** A single human cell can store >4,300 bits of recording information (BASELINE; Winter et al., 2025), capture ~210,000 bits of transcriptomic data (TimeVault; Chao et al., 2026), and maintain >100 bits of epigenetic state information (CRISPRoff; Nuñez et al., 2021). DNA data storage achieves 1.57 bits per nucleotide (Erlich & Zielinski, 2017), yielding ~10¹⁸ bytes per cubic millimeter — more than sufficient for any foreseeable therapeutic application.

2. **Computation in DNA is feasible.** DNA neural networks perform supervised learning (Cherry & Qian, 2025), DNA decision trees implement multi-class disease classification (Liu et al., 2025), and heat-rechargeable circuits enable reusable computation (Song et al., 2025).

3. **Durable memory is achievable.** CRISPRoff epigenetic silencing persists for nearly a year in vivo (Cappelluti et al., 2024), analog epigenetic memory maintains graded states through cell division (Palacios et al., 2025), and genomic recording (DNA Typewriter, BASELINE) is permanent.

4. **In vivo operation is advancing.** Lineage recording works in living mice (CARLIN, BASELINE, temporal recording), epigenome editing is durable in vivo (Cappelluti et al., 2024), and retron engineering has achieved mammalian efficiency (Buffington et al., 2025).

### 7.3 Comparative Analysis: Three Challenges Synthesized

Table 1 synthesizes the information-theoretic performance, in vivo status, and integration potential of each molecular information technology reviewed in this document.

**Table 1. Comparative Analysis of Molecular Information Technologies**

| Technology | Bits/Cell | Persistence | Error Rate | In Vivo Status | Integration Potential |
|---|---|---|---|---|---|
| CAMERA (spacer) | ~5/spacer | Permanent (genomic) | ~5% (off-target spacers) | Prokaryotic only | Low (no mammalian) |
| CAMERA 2 (base edit) | ~1/site | Permanent (genomic) | ~2–5% (off-target editing) | Mammalian cell lines | Medium |
| ENGRAM | ~1,000 (100 elements) | Permanent (genomic) | ~10% (symbol error) | Gastruloids (in vitro) | High (signal sensing built-in) |
| BASELINE | 4,300 | Permanent (genomic) | <5% (site dropout) | Mouse in vivo | High (single-cell compatible) |
| DNA Typewriter | 40/tape | Permanent (genomic) | ~3–5% (symbol/skip) | Mammalian cell lines | High (sequential temporal) |
| peCHYRON | ~60/array | Permanent (genomic) | ~5% | Mammalian cell lines | High (open-ended) |
| SCRIBE (retron) | Analog (continuous) | Permanent (genomic) | N/A (population-level) | Bacteria in vivo | Medium |
| Multitron | ~10/transcript | Permanent (genomic) | ~5–10% | Bacteria | Medium |
| TimeVault | ~210,000 (transcriptome) | 7+ days (vault protected) | ~5% (capture bias) | Mammalian cell lines | Very High (transcriptome-wide) |
| CRISPRoff | ~1/locus × N loci | Months–years (epigenetic) | ~1–5%/division | Mouse in vivo | High (therapeutic) |
| Analog epigenetic | ~3/locus (8 levels) | Weeks–months | ~10% (level drift) | Cell lines | High (graded control) |
| DNA data storage | 1.57 bits/nt | Centuries (in vitro) | 10⁻¹² (after ECC) | Bacteria (living storage) | Low (in vitro) |
| DNA neural network | N/A (computation) | Minutes–hours | ~5–10% | In vitro only | Low (test tube) |

### 7.4 The Road from Recording to Therapeutic Cellular Intelligence

Three engineering challenges must be overcome to translate molecular information technologies into therapeutic cellular intelligence:

**Challenge 1: In vivo delivery and biocompatibility.** Recording systems must operate in the complex intracellular environment without toxicity or immune activation. LNP-mRNA delivery has emerged as the leading platform for in vivo delivery of molecular editors (Cappelluti et al., 2024), but delivery of the multi-component recording systems (DNA Tape + prime editor + pegRNAs) remains challenging. AAV vectors can deliver smaller recording components but face packaging limits (~4.7 kb). The most promising near-term approach is integrating recording components into the genome of therapeutic cells (e.g., CAR-T cells) before transplantation, rather than delivering them in vivo.

**Challenge 2: Scalable readout.** Current molecular recording readout requires cell lysis and sequencing — destructive to the cell and incompatible with real-time therapeutic decision-making. Non-destructive readout methods — such as TimeVault's vault particle capture (which preserves cell viability) or fluorescence-based reporters coupled to recording states — are needed for closed-loop therapeutic applications.

**Challenge 3: Computation speed.** DNA strand displacement computing operates on timescales of minutes to hours, while cellular therapeutic responses may require decisions within seconds. Gene regulatory circuits offer faster response (minutes) but limited computational complexity. Hybrid architectures that combine DNA-based recording (slow, high-capacity) with protein-based computation (fast, lower-capacity) may provide optimal performance.

### 7.5 Open Questions and Future Directions

1. **What is the maximum information capacity achievable in a single mammalian cell?** Current systems reach ~4,300 bits (BASELINE) for recording and ~210,000 bits (TimeVault) for capture. The theoretical maximum for genomic recording, limited by genome size and editing efficiency, is on the order of 10⁵–10⁶ bits per cell.

2. **Can molecular recording be combined with real-time computation?** No system yet records events AND computes responses from the recorded history within the same cell. Closing this loop is the central engineering challenge for therapeutic cellular intelligence.

3. **How will cellular computation interface with electronic computation?** The most powerful near-term applications may combine molecular recording (for sensing and memory within the biological system) with external electronic computation (for complex analysis and decision-making), connected through sequencing as the readout interface.

4. **What are the safety and ethical implications of cellular surveillance?** Molecular recording systems that permanently inscribe event histories into cellular DNA raise novel questions about biological privacy, consent, and the boundary between therapy and surveillance.

5. **What is the realistic timeline?** Individual components (recording, memory, computation) are mature. Integration into therapeutic systems is 5–10 years away for first-in-human applications. Fully autonomous cellular computers operating in vivo represent a longer-term (15–25 year) horizon that will require advances in delivery, biocompatibility, non-destructive readout, and computational speed.

---

## 8. Conclusion

The molecular memory frontier represents a convergence of three historically separate fields: CRISPR genome engineering, synthetic biology, and information theory. The technologies reviewed here — CRISPR-based recording (CAMERA, ENGRAM, DNA Typewriter, peCHYRON), retron-mediated analog recording, transcriptome capture (TimeVault), durable epigenetic memory (CRISPRoff), lineage recording (GESTALT, CARLIN, BASELINE), DNA data storage, and DNA-based computation — collectively establish that cells can be engineered to store, retrieve, and process information with quantifiable capacity, fidelity, and persistence.

The information-theoretic analysis presented in this documnet reveals both the remarkable capabilities and the fundamental limits of each modality. BASELINE achieves 4,300 bits per cell with permanent genomic persistence. TimeVault captures transcriptome-wide snapshots stable for over a week. CRISPRoff installs epigenetic memory lasting months to years in vivo. DNA data storage approaches the Shannon limit at 1.57 bits per nucleotide. DNA neural networks demonstrate supervised learning from molecular examples. Yet significant gaps remain: most technologies await in vivo validation, computation speeds lag silicon by orders of magnitude, and no system yet integrates recording, computation, and therapeutic response in a single cell.

Viewed through the lens of the Theory of Computational Interfaces, these technologies represent the engineering toolkit for the next computational frontier. Just as the transistor enabled personal computing, and electrode arrays enabled brain-computer interfaces, molecular recording and DNA-based computation are enabling the programmable cell — a biological device that senses, records, computes, and acts. The trajectory from room-sized mainframes to cellular computers is not a teleological inevitability but an observed pattern driven by the dual forces of miniaturization and integration with human biology. The evidence reviewed here suggests that the cellular computation horizon, while still distant, is grounded in demonstrated capabilities rather than speculation.

The path forward requires interdisciplinary collaboration spanning genome engineering, information theory, synthetic biology, materials science, and clinical medicine. The molecular memory revolution has begun; its therapeutic realization will define the next era of precision medicine.

---

## References

1. Xu, D., Besselink, S., Ramadoss, G.N. et al. Programmable epigenome editing by transient delivery of CRISPR epigenome editor ribonucleoproteins. Nat Commun 16, 7948 (2025). https://doi.org/10.1038/s41467-025-63167-x

3. Allis, C. D., & Jenuwein, T. (2016). The molecular hallmarks of epigenetic control. *Nature Reviews Genetics*, 17(8), 487–500.

4. Billinghurst, M., Clark, A., & Lee, G. (2015). A survey of augmented reality. *Foundations and Trends in Human-Computer Interaction*, 8(2–3), 73–272.

5. Barrangou, R., et al. (2007). CRISPR provides acquired resistance against viruses in prokaryotes. *Science*, 315(5819), 1709–1712.

6. Bartlett, P. L., et al. (2019). Nearly-tight VC-dimension and pseudodimension bounds for piecewise linear neural networks. *Journal of Machine Learning Research*, 20(63), 1–17.

7. Lear, S. K., Lopez, S. C., González-Delgado, A., Bhattarai-Kline, S., & Shipman, S. L. (2023). Temporally resolved transcriptional recording in E. coli DNA using a Retro-Cascorder. Nature protocols, 18(6), 1866-1892.

8. Palacios, S., Bruno, S., Weiss, R., Salibi, E., Goodchild-Michelman, I., Kane, A., ... & Del Vecchio, D. (2025). Analog epigenetic memory revealed by targeted chromatin editing. Cell Genomics, 5(11).

9. Bowling, S., et al. (2020). An engineered CRISPR-Cas9 mouse line for simultaneous readout of lineage histories and gene expression profiles in single cells. *Cell*, 181(6), 1410–1422.

10. Buffington, J. D., Kuo, H. C., Hu, K., Chang, Y. C., Javanmardi, K., Voigt, B., ... & Finkelstein, I. J. (2025). Discovery and engineering of retrons for precise genome editing. Nature biotechnology, 1-11.

11. Cappelluti, M. A., et al. (2024). Durable and efficient gene silencing in vivo by hit-and-run epigenome editing. *Nature*, 627, 416–423.

12. Chen, C., et al. (2025a). Dual-nuclease single-cell lineage tracing by Cas9 and Cas12a. *Cell Reports*, 44(1), 115105.

13. Choi, J., Chen, W., Minkina, A., Chardon, F. M., Suiter, C. C., Regalado, S. G., ... & Shendure, J. (2022). A time-resolved, multi-symbol molecular recorder via sequential genome editing. Nature, 608(7921), 98-107.

14. Liao, H., Choi, J., & Shendure, J. (2024). Molecular recording using DNA Typewriter. Nature Protocols, 19(10), 2833-2862.

15. Cherry, K. M., & Qian, L. (2018). Scaling up molecular pattern recognition with DNA-based winner-take-all neural networks. *Nature*, 559, 370–376.

16. Cherry, K. M., & Qian, L. (2025). Supervised learning in DNA neural networks. *Nature*, 645, 639–647.

17. Chen, W., Choi, J., Li, X., Nathans, J. F., Martin, B., Yang, W., ... & Shendure, J. (2024). Symbolic recording of signalling and cis-regulatory element activity to DNA. Nature, 632(8027), 1073-1081.

18. Nathans, J. F., McDiarmid, T. A., Chen, W., & Shendure, J. (2026). Multichannel genomic recording of biological information with ENGRAM. Nature Protocols, 1-26.

19. Church, G. M., Gao, Y., & Kosuri, S. (2012). Next-generation digital information storage in DNA. *Science*, 337(6102), 1628.

20. da Cruz, L., et al. (2016). Five-year safety and performance results from the Argus II retinal prosthesis system clinical trial. *Ophthalmology*, 127(12), 1703–1715.

21. Song, T., & Qian, L. (2025). Heat-rechargeable computation in DNA logic circuits and neural networks. Nature, 646(8084), 315-322.

22. Davidson, E. H. (2010). Emerging properties of animal gene regulatory networks. *Nature*, 468, 911–920.

23. Cameron, D. E., Bashor, C. J., & Collins, J. J. (2014). A brief history of synthetic biology. *Nature Reviews Microbiology*, 12(5), 381–390.

24. Erlich, Y., & Zielinski, D. (2017). DNA Fountain enables a robust and efficient storage architecture. *Science*, 355(6328), 950–954.

25. Farber, D. L., Netea, M. G., et al. (2016). Immunological memory: Lessons from the past and a look to the future. *Nature Reviews Immunology*, 16(2), 124–128.

26. Farzadfard, F., & Lu, T. K. (2014). Genomically encoded analog memory with precise in vivo DNA writing in living cell populations. *Science*, 346(6211), 1256272.

27. Farzadfard, F., et al. (2019). Single-nucleotide-resolution computing and memory in living cells. *Molecular Cell*, 75(4), 769–780.

28. Nurk, S., et al. (2022). The complete sequence of a human genome. *Science*, 376(6588), 44–53.

29. Wilson, B. S., & Dorman, M. F. (2008). Cochlear implants: A remarkable past and a brilliant future. *Hearing Research*, 242(1–2), 3–21.

30. Grass, R. N., Heckel, R., et al. (2015). Robust chemical preservation of digital information on DNA in silica with error-correcting codes. *Angewandte Chemie International Edition*, 54(8), 2552–2555.

31. Hochberg, L. R., et al. (2012). Reach and grasp by people with tetraplegia using a neurally controlled robotic arm. *Nature*, 485, 372–375.

32. Chao, Y. K., Wu, M., Gong, Q., & Chen, F. (2026). A genetically encoded device for transcriptome storage in mammalian cells. Science, eadz9353.

33. Yang, Z., & Rannala, B. (2012). Molecular phylogenetics: Principles and practice. *Nature Reviews Genetics*, 13(5), 303–314.

34. Islam, M., et al. (2024). Temporal recording of mammalian development and precancer. *Nature*, 634, 1187–1195.

35. Wu, X., Lee, I., Dong, Q., Yang, K., Kim, D., Wang, J., ... & Blaauw, D. (2018, June). A 0.04 MM 3 16NW wireless and batteryless sensor system with integrated cortex-m0+ processor and optical communication for cellular temperature measurement. In 2018 IEEE Symposium on VLSI Circuits (pp. 191-192). IEEE.

36. Yang, L., Tang, Q., Zhang, M., Tian, Y., Chen, X., Xu, R., ... & Han, D. (2024). A spatially localized DNA linear classifier for cancer diagnosis. Nature Communications, 15(1), 4583.

37. Li, L., Bowling, S., Lin, H., Chen, D., Wang, S. W., & Camargo, F. D. (2025). DARLIN mouse for in vivo lineage tracing at high efficiency and clonal diversity. Nature Protocols, 20(8), 2319-2344.

38. Luo, H., Huang, W., He, Z., Fang, Y., Tian, Y., & Xiong, Z. (2025). Engineered living memory microspheroid‐based archival file system for random accessible in vivo DNA storage. Advanced Materials, 37(13), 2415358.

39. González-Delgado, A., Lopez, S. C., Rojas-Montero, M., Fishman, C. B., & Shipman, S. L. (2024). Simultaneous multi-site editing of individual genomes using retron arrays. Nature chemical biology, 20(11), 1482-1492.

40. Loveless, T. B., et al. (2025). Open-ended molecular recording of sequential cellular events into DNA. *Nature Chemical Biology*, 20, 1622–1631.

41. McKenna, A., et al. (2016). Whole-organism lineage tracing by combinatorial and cumulative genome editing. *Science*, 353(6298), aaf7907.

42. Waldrop, M. M. (2016). The chips are down for Moore's law. *Nature*, 530, 144–147.

43. Morsut, L., et al. (2016). Engineering customized cell sensing and response behaviors using synthetic notch receptors. *Cell*, 164(4), 780–791.

44. Nuñez, J. K., et al. (2021). Genome-wide programmable transcriptional memory by CRISPR-based epigenome editing. *Cell*, 184(9), 2503–2519.

45. Organick, L., et al. (2018). Random access in large-scale DNA data storage. *Nature Biotechnology*, 36(3), 242–248.

46. Piwek, L., et al. (2016). The rise of consumer health wearables: Promises and barriers. *PLoS Medicine*, 13(2), e1001953.

47. Pietak, A., & Levin, M. (2025). Harnessing the analog computing power of regulatory networks with the Regulatory Network Machine. iScience, 28(6), 112536. https://doi.org/10.1016/j.isci.2025.112536

48. Qian, L., & Winfree, E. (2011). Scaling up digital circuit computation with DNA strand displacement cascades. *Science*, 332(6034), 1196–1201.

49. Raj, B. (2025). Single-Cell Profiling of Lineages and Cell Types in the Vertebrate Brain. In Lineage Tracing: Methods and Protocols (pp. 299-310). New York, NY: Springer US.

50. Roybal, K. T., et al. (2016). Precision tumor recognition by T cells with combinatorial antigen-sensing circuits. *Cell*, 164(4), 770–779.

51. Winter, E., Emiliani, F., Cook, A., Abderrahim, A., & McKenna, A. 

52. Sheth, R. U., Yim, S. S., Wu, F. L., & Wang, H. H. (2017). Multiplex recording of cellular events over time on CRISPR biological tape. *Science*, 358(6369), 1457–1461.

53. Simeral, J. D., et al. (2021). Home use of a percutaneous wireless intracortical brain-computer interface by individuals with tetraplegia. *IEEE Transactions on Biomedical Engineering*, 68(7), 2313–2325.

54. Takagi, Y., & Nishimoto, S. (2023). High-resolution image reconstruction with latent diffusion models from human brain activity. *Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition*, 14453–14463.

55. Tang, W., & Liu, D. R. (2018). Rewritable multi-event analog recording in bacterial and mammalian cells. *Science*, 360(6385), 149–153.

56. Pattali, R. K., Ornelas, I. J., Nguyen, C. D., Xu, D., Divekar, N. S., & Nuñez, J. K. (2025). CRISPRoff epigenome editing for programmable gene silencing in human cell lines and primary T cells. In Methods in enzymology (Vol. 712, pp. 517-551). Academic Press.

57. Xu, C., Zeng, C., Wang, M., Wei, X., Song, M., Liu, X., ... & Zhu, J. K. (2026). mRNA-engineered CRISPR-Cas epigenetic editors enable durable and efficient gene silencing in vivo. The Innovation, 7(3).

58. West, J., & Mace, M. (2010). Browsing as the killer app: Explaining the rapid success of Apple's iPhone. *Telecommunications Policy*, 34(5–6), 270–286.

59. Willett, F. R., et al. (2023). A high-performance speech neuroprosthesis. *Nature*, 620, 1031–1036.

60. Shipman, S. L., Nivala, J., Macklis, J. D., & Church, G. M. (2017). CRISPR-Cas encoding of a digital movie into the genomes of a population of living bacteria. *Nature*, 547, 345–349.

61. Liu, J., Tang, Q., Han, Y., Song, J., Wang, F., Guo, P., ... & Han, D. (2025). Interpretable molecular decision-making with DNA-based scalable and memory-efficient tree computation. Nature Communications, 16(1), 10311.

62. Cattle, M. A., Aguado, L. C., Sze, S., Venkittu, S., Wang, Y., Papagiannakopoulos, T., ... & Poirier, J. T. (2025). An enhanced Eco1 retron editor enables precision genome engineering in human cells without double-strand breaks. Nucleic acids research, 53(14), gkaf716
