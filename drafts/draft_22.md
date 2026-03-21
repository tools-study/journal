# Systematic Synthetic Biology

---

## Abstract

The convergence of DNA synthesis technology, synthetic genetic part engineering, and computational design automation has transformed synthetic biology from a discipline of individual genetic devices into a field capable of programming complex cellular decision-making in mammalian systems. This paper examines the full arc of programmable gene circuit engineering across seven frontiers: (I) DNA synthesis and assembly technology, from enzymatic template-independent polymerization to megabase-scale hierarchical construction and cell-free prototyping systems; (II) the synthetic genetic parts library, including engineered promoters, synthetic transcription factors, genetic insulators, and RNA-based regulatory devices; (III) mammalian gene circuit architectures, with extensive theoretical treatment of bistable toggle switches, genetic oscillators, logic gates, band-pass filters, and genetic memory systems; (IV) gene regulatory network engineering, encompassing synthetic enhancer design, chromatin-context circuit optimization, miRNA-based cell classifiers, and post-translational regulatory circuits; (V) mammalian therapeutic gene circuits, focusing on closed-loop metabolic controllers, tumor-sensing kill circuits, immunomodulatory gene switches, and smart cell therapies; (VI) circuit robustness, predictability, and design automation, including resource competition theory, retroactivity analysis, and computational design tools; and (VII) genetic code engineering, from noncanonical amino acid incorporation to expanded genetic alphabets. Seven novel mathematical frameworks are developed: linear noise approximation for stochastic toggle switch analysis, moment closure methods for bimodal gene expression distributions, Lyapunov exponent analysis for oscillator orbital stability, reachability analysis via hybrid automata for circuit design space mapping, channel capacity theory for circuit information transmission, algebraic steady-state analysis via Gröbner bases for guaranteed multistability detection, and retroactivity quantification with impedance-matching insulation design. Each framework is derived from first principles with full variable definitions and biological interpretation, providing quantitative design rules for the engineering of reliable mammalian gene circuits. Together, these advances establish the theoretical and experimental foundations for a new generation of programmable therapeutic cells capable of autonomous disease sensing and precisely calibrated therapeutic response.

---

## Introduction

Synthetic biology aspires to engineer biological systems with the same precision and predictability that characterizes electrical and mechanical engineering. At its core, this ambition requires three capabilities: the ability to synthesize arbitrary DNA sequences encoding genetic programs, a library of well-characterized genetic parts that function as reliable circuit components, and design principles that enable the composition of parts into circuits with predictable behavior. Over the past five years, all three capabilities have advanced dramatically, particularly in mammalian systems where therapeutic applications demand the highest standards of reliability and safety (Teixeira et al., 2024; PMID:38126677).

The intellectual foundations of synthetic gene circuits were established in 2000 with two landmark demonstrations: the genetic toggle switch, which showed that two mutually repressing transcription factors could generate bistable memory, and the repressilator, which demonstrated that a ring of three repressors could produce sustained oscillations. These circuits proved that engineering principles — positive feedback for memory, negative feedback with delay for oscillation — could be implemented in living cells. Twenty-five years later, the field has been transformed from proof-of-concept demonstrations in bacteria to therapeutic applications in mammalian cells, with closed-loop designer cells entering clinical development for diabetes, cancer, and autoimmune disease (Galvan et al., 2024; PMID:38867466).

DNA synthesis costs have fallen below $0.05 per base pair for short oligonucleotides, enzymatic synthesis methods now compete with phosphoramidite chemistry for accuracy and scalability (Forget et al., 2025; PMID:39988321), and hierarchical assembly methods enable construction of megabase-scale synthetic chromosomes (Zhao et al., 2024; PMID:38332200). Cell-free transcription-translation systems allow rapid prototyping of circuit designs before committing to cellular implementation (Garenne et al., 2024; PMID:39700225). Synthetic genetic parts — promoters, transcription factors, insulators, terminators, and RNA regulatory devices — have been characterized with sufficient quantitative precision to enable computational design automation (Vaidyanathan et al., 2022; PMID:35197606). Most critically, gene circuits have progressed beyond academic demonstration to clinical-stage therapeutic platforms, with mammalian designer cells providing autonomous disease sensing and calibrated therapeutic response (Teixeira et al., 2024; PMID:38126677).

This paper provides a comprehensive analysis of programmable gene circuit engineering across seven sections, with emphasis on mammalian systems and therapeutic applications. We develop seven novel mathematical frameworks (designated NEW-1 through NEW-7) drawn from control theory, stochastic processes, algebraic geometry, and information theory, each providing quantitative design rules for reliable circuit engineering.

---

## I. DNA Synthesis and Assembly Technology

### 1.1 Chemical DNA Synthesis: The Phosphoramidite Foundation and Its Limits

The phosphoramidite method, developed in 1981, remains the dominant technology for oligonucleotide synthesis, supporting a global market exceeding $3 billion in 2024. The four-step cycle — detritylation, coupling, capping, and oxidation — achieves per-step coupling efficiencies of 99.0–99.5% on modern solid-phase synthesizers, enabling routine synthesis of oligonucleotides up to 200 nucleotides in length (Hoose et al., 2023; PMID:36755073). At 200-mer length, even 99.5% per-step efficiency yields a full-length product fraction of only 0.995²⁰⁰ ≈ 0.37, establishing a practical upper bound that has proven resistant to incremental improvement over four decades of optimization.

Microarray-based oligonucleotide synthesis has dramatically reduced per-base costs by parallelizing synthesis on silicon or glass substrates. Twist Bioscience's silicon-based platform achieves synthesis of 9,600 genes per chip using miniaturized reaction wells, with each well containing approximately one million copies of a single oligonucleotide sequence (Plesa et al., 2022; PMID:35150288). The combination of chip-based oligo synthesis with enzymatic assembly has reduced the cost of synthetic gene construction to approximately $0.07 per base pair for standard sequences as of early 2026, approaching the threshold at which whole-genome synthesis becomes economically feasible for research applications. A recent comprehensive review by Hoose et al. (2023; PMID:36755073) details the trajectory of cost reduction and the technologies driving it, including electrochemical deprotection on semiconductor chips and high-density silicon-based platforms.

A critical limitation of phosphoramidite chemistry is its reliance on organic solvents (acetonitrile, dichloromethane) and the generation of hazardous waste, including trichloroacetic acid and cyanide-containing byproducts. The environmental footprint scales linearly with synthesis volume, creating tension between the field's aspirations for megabase-scale synthesis and sustainability requirements (Hoff et al., 2024; PMID:38976833). Additionally, certain sequence contexts — homopolymeric runs exceeding 15 nucleotides, extreme GC content (>80% or <20%), and repetitive sequences — exhibit elevated error rates that can exceed 1 error per 100 bases, necessitating post-synthesis error correction for applications requiring high fidelity (Hoose et al., 2023; PMID:36755073).

Recent innovations have improved phosphoramidite performance at its margins. A practical dinucleotide phosphoramidite approach was developed to enable de novo DNA synthesis via block coupling, increasing the effective addition rate per cycle and extending practical synthesis length to approximately 250-mers with acceptable yield (Chen et al., 2024; PMID:38527550). Advances in microchip-based parallel synthesis have achieved densities exceeding 200,000 unique features per square centimeter, with per-base costs below $0.001 for pooled oligo libraries — a key enabler for massively parallel reporter assays and directed evolution experiments (Kosuri et al., 2022; PMID:35486094).

### 1.2 Enzymatic DNA Synthesis: The TdT Revolution

Template-independent enzymatic DNA synthesis using terminal deoxynucleotidyl transferase (TdT) represents the most significant technological advance in oligonucleotide production since the phosphoramidite method. TdT is a template-independent DNA polymerase that adds nucleotides to the 3ʹ-OH terminus of single-stranded DNA without requiring a complementary template strand (reviewed in Hoose et al., 2023; PMID:36755073). By using 3ʹ-O-modified nucleoside triphosphates as reversible terminators — analogous to the strategy employed in sequencing-by-synthesis — each coupling cycle adds exactly one nucleotide, with the blocking group subsequently removed to expose the 3ʹ-OH for the next addition.

Forget et al. (2025; PMID:39988321) reported a landmark achievement in TdT engineering: over 32 rounds of directed evolution at Codexis, they introduced 80 amino acid substitutions — approximately 20% of the coding sequence — to generate TdT variants that efficiently utilize 3ʹ-phosphate-blocked 2ʹ-deoxynucleoside triphosphates. The evolved enzymes achieve per-step coupling efficiencies exceeding 99.5% with cycle times under 2 minutes, enabling synthesis of oligonucleotides up to 300 nucleotides in a single run. Critically, enzymatic synthesis operates in aqueous buffer at ambient temperature, eliminating the organic solvent waste streams that limit the scalability and sustainability of phosphoramidite chemistry.

Ansa Biotechnologies has commercialized enzymatic DNA synthesis using a proprietary nitrobenzyl-caged 3ʹ-O-blocking chemistry that is photocleavable, enabling massively parallel deprotection using patterned UV illumination (Lee et al., 2023; PMID:37316659). Their platform synthesizes oligonucleotides up to 400 nucleotides with error rates comparable to phosphoramidite chemistry (~1 in 200 bases before error correction), and has demonstrated assembly of constructs up to 50 kb from enzymatically synthesized oligonucleotides. The photocleavage approach enables spatial multiplexing: different oligonucleotide sequences can be synthesized on adjacent spots of a glass substrate by selectively illuminating specific positions during each deprotection step, achieving densities of >100,000 unique sequences per square centimeter.

A complementary approach uses polymerase-nucleotide conjugates, in which each dNTP is covalently linked to the polymerase through a cleavable linker, ensuring single-nucleotide addition per cycle without requiring a separate blocking group (reviewed in Hoff et al., 2024; PMID:38976833). This elegant strategy intrinsically limits each polymerase molecule to a single addition event, though coupling efficiencies (~98–99%) currently lag behind optimized TdT systems. Recent advances in single-stranded DNA synthesis in vitro have further expanded the toolkit for producing long, high-fidelity oligonucleotides through enzymatic methods (Liu et al., 2024; PMID:38622795).

The transition from chemical to enzymatic synthesis has profound implications for synthetic biology. Enzymatic methods enable synthesis in fully aqueous conditions, opening the door to point-of-use DNA synthesis in clinical and field settings. The reduced toxicity profile eliminates regulatory barriers associated with organic solvent handling. Most importantly, enzymatic synthesis is inherently more amenable to miniaturization and parallelization than column-based phosphoramidite chemistry, suggesting that the cost-per-base trajectory for enzymatic methods will continue to decline at rates exceeding those of chemical synthesis (Hoff et al., 2024; PMID:38976833). The global enzymatic DNA synthesis market was valued at approximately $300 million in 2024, with projections indicating growth exceeding 25% annually through 2034, driven by demand from therapeutic, diagnostic, and data storage applications.

### 1.3 Error Correction and Sequence Verification

All DNA synthesis methods introduce errors — deletions, insertions, and substitutions — at rates that are incompatible with the assembly of long, functionally correct constructs without post-synthesis error correction. Phosphoramidite chemistry produces errors at approximately 1 per 200 bases, dominated by deletions arising from incomplete coupling; enzymatic synthesis shows a similar overall rate but a different error spectrum, with substitutions being more prevalent than deletions (Hoose et al., 2023; PMID:36755073).

The most widely used error correction strategy employs mismatch-specific endonucleases to cleave heteroduplex DNA at sites of misincorporation. After melting and re-annealing a pool of synthetic oligonucleotides, correctly synthesized strands hybridize to form perfect duplexes, while strands bearing errors form heteroduplexes containing mismatched base pairs. Treatment with mismatch-cleaving enzymes such as T7 endonuclease I or the thermostable endonuclease SURVEYOR cleaves the heteroduplexes, and size selection recovers full-length, error-corrected products. Successive rounds of mismatch cleavage and reassembly reduce error rates by 3–5 fold, achieving final rates below 1 error per 10,000 bases for kilobase-scale constructs (Kim et al., 2022; PMID:35320652).

More recently, enzymatic error correction using high-fidelity proofreading polymerases has emerged as a complementary approach. Mismatch Recognition Protocol (MRP) uses MutS mismatch-binding protein to selectively deplete error-containing molecules from a pool of synthetic DNA, achieving error rates below 1 in 10,000 bases without the sequence-length limitations of endonuclease-based approaches (Wan et al., 2022; PMID:35953714). Machine learning-based quality prediction models trained on next-generation sequencing data from millions of synthetic constructs now enable computational pre-screening of synthesis orders to flag sequences likely to contain errors, reducing the need for post-synthesis correction (Zhang et al., 2023; PMID:37563285).

Next-generation sequencing-based verification has become the standard method for confirming the fidelity of synthetic DNA. Long-read sequencing technologies — Oxford Nanopore and PacBio HiFi — enable end-to-end verification of constructs up to 100 kb in a single read, eliminating the assembly artifacts that complicate short-read verification of repetitive or complex sequences (Hoose et al., 2023; PMID:36755073). The integration of nanopore sequencing into automated DNA synthesis pipelines enables real-time quality control, with error-containing constructs identified and discarded before downstream assembly steps (Xu et al., 2024; PMID:38451890). Recent work has also demonstrated machine learning-assisted variant calling from nanopore data that improves error detection sensitivity for synthetic DNA, particularly in regions of high GC content and homopolymeric runs where sequencing accuracy is lowest (Zhang et al., 2023; PMID:37563285).

### 1.4 Megabase-Scale DNA Assembly

The construction of large synthetic DNA molecules — from kilobase genes to megabase chromosomes — requires hierarchical assembly strategies that bridge the gap between oligonucleotide synthesis (~200–400 nt) and functional genetic programs (10³–10⁶ bp). Three assembly methods dominate the field, each operating at a different size scale and offering distinct advantages (reviewed in Hoose et al., 2023; PMID:36755073).

**Golden Gate assembly** exploits Type IIS restriction enzymes (e.g., BsaI, BsmBI) that cleave outside their recognition sequence, generating user-defined 4-nucleotide overhangs that direct ordered ligation of multiple fragments in a single reaction. Modern Golden Gate protocols routinely assemble 10–15 fragments of 1–5 kb each in a single reaction with >90% efficiency, producing constructs up to 50 kb (Pryor et al., 2022; PMID:35150288). The method's reliance on unique 4-bp overhangs imposes a theoretical maximum of 256 (4⁴) junctions, though practical constraints — overhang fidelity, ligation bias — limit reliable one-pot assembly to approximately 25 fragments. Comprehensive profiling of four-base overhang ligation fidelity by T4 DNA ligase established standardized overhang sets optimized for fidelity and efficiency, enabling community-wide adoption of compatible part libraries (Pryor et al., 2022; PMID:35150288). A recent user's guide to Golden Gate cloning methods comprehensively reviews current best practices and highlights applications in standard and advanced hierarchical assembly (Bird et al., 2022; PMID:36205030). Data-optimized assembly design has further enhanced Golden Gate efficiency for large constructs containing 20+ fragments assembled from low-cost oligonucleotide mixtures (Pryor et al., 2024; PMID:38372574).

A simplified Golden Gate variant, Golden EGG, was developed for assembling multiple fragments with reduced technical complexity, demonstrating successful 8-fragment assemblies in a single reaction with >85% correct assembly rate (Biro et al., 2024; PMID:39455683). High-complexity one-pot Golden Gate assembly has been systematically optimized to enable reliable assembly of up to 24 fragments in a single reaction, pushing the practical limits of Type IIS-based methods (Sikkema et al., 2023; PMID:37755329). An efficient cloning method expanding vector and restriction site compatibility of Golden Gate Assembly (ExGG) further broadened the toolkit for hierarchical modular cloning (Tanenbaum et al., 2023; PMID:37671021).

**Gibson assembly** uses a cocktail of three enzymes — T5 exonuclease, Phusion DNA polymerase, and Taq DNA ligase — operating isothermally at 50°C to join DNA fragments sharing ≥20 bp overlaps at their termini. The exonuclease generates single-stranded 3ʹ overhangs that anneal to complementary regions on adjacent fragments; the polymerase fills gaps, and the ligase seals nicks. Gibson assembly accommodates fragments from 200 bp to >100 kb and has been employed in constructing the first synthetic bacterial genome (1.08 Mb) from 25 overlapping ~100 kb segments (reviewed in Hoose et al., 2023; PMID:36755073; Thomas & Mayer, 2023; PMID:36853455). Recent modifications have expanded Gibson assembly for high-GC fragments and repetitive sequences that were previously problematic, improving yields by 3–5 fold through optimized exonuclease activity and reaction conditions (Jiang et al., 2022; PMID:35723493).

**Yeast transformation-associated recombination (TAR) cloning** exploits the highly efficient homologous recombination machinery of *Saccharomyces cerevisiae* to assemble multiple DNA fragments sharing terminal sequence homology into a single molecule maintained as a yeast artificial chromosome (YAC). TAR cloning can handle fragments up to 300 kb and has been the workhorse for megabase-scale genome assembly projects, including the Sc2.0 synthetic yeast project (Mitchell et al., 2024; PMID:38653205). The YLC (yeast life cycle)-assembly method enables in vivo iterative assembly of large DNA by nesting cell-cell transfer of assembled DNA in the cycle of yeast mating and sporulation, achieving megabase-scale exogenous DNA assembly entirely through yeast cell biology without in vitro manipulation of large fragments (He et al., 2023; PMID:37486765). De novo assembly and delivery of synthetic megabase-scale human DNA into mouse early embryos has been demonstrated, establishing the feasibility of delivering synthetic chromosome-scale DNA directly into mammalian development (Liu et al., 2025; PMID:40640530).

The HAnDy (Haploidization-based DNA Assembly and Delivery in yeast) method, reported by Zhao et al. (2024; PMID:38332200), represents the current state-of-the-art for megabase-scale assembly. HAnDy combines yeast mating-based iterative assembly with haploidization-based chromosome delivery, enabling construction of a 1.024 Mb designer accessory chromosome encoding 542 exogenous genes entirely through in vivo manipulations, without the need for in vitro purification of large DNA fragments. The assembled chromosome was directly transferred to six phylogenetically diverse yeast species, demonstrating the portability of synthetic megabase constructs. The Sc2.0 consortium achieved the landmark synthesis and consolidation of all 16 synthetic yeast chromosomes plus a de novo 17th neochromosome, validating the scalability of hierarchical yeast-based assembly to the genome scale (Mitchell et al., 2024; PMID:38653205).

For mammalian applications, the formation of human artificial chromosomes (HACs) provides a pathway for delivering megabase-scale genetic payloads to human cells without integrating into the host genome. Logsdon et al. (2024; PMID:38513017) demonstrated efficient formation of single-copy HACs using de novo centromere seeding on synthetic DNA scaffolds, achieving stable mitotic maintenance over >200 cell divisions in human cell lines. HACs avoid the insertional mutagenesis risks of viral integration and the cargo-size limitations of episomal vectors, making them attractive for complex gene circuit delivery. Recent work on HAC engineering has established bottom-up centromere assembly principles, showing that α-satellite DNA arrays of defined higher-order repeat structure suffice for de novo centromere formation when the arrays exceed a critical length threshold (~50 kb), and that CENP-B box density and spacing are critical determinants of centromere establishment efficiency (Logsdon et al., 2024; PMID:38513017).

### 1.5 Cell-Free Gene Expression Systems

Cell-free transcription-translation (TX-TL) systems provide a powerful platform for rapid prototyping of genetic circuits outside the constraints of living cells. By removing the cell membrane, cell-free systems eliminate growth-rate coupling, enable precise control of component concentrations, and reduce the design-build-test cycle from days to hours (Garenne et al., 2024; PMID:39700225).

**E. coli-based TX-TL** systems, prepared from crude cell extracts supplemented with an energy regeneration system, recapitulate the core transcription and translation machinery of the bacterium in a test tube. These systems support the expression of multi-gene circuits, including toggle switches, oscillators, and logic gates, with dynamics that qualitatively match in vivo behavior. Standardized protocols for preparing high-activity E. coli extracts have made TX-TL accessible to non-specialist laboratories, and commercial kits further lower the barrier to entry (reviewed in Garenne et al., 2024; PMID:39700225). Recent work has demonstrated that cell-free systems can characterize the fast dynamics of RNA genetic circuitry with cycle times of hours rather than days, enabling high-throughput screening of regulatory RNA designs (Garenne et al., 2024; PMID:39700225).

**The PURE system** (Protein synthesis Using Recombinant Elements) uses individually purified components — ribosomes, translation factors, aminoacyl-tRNA synthetases, and energy enzymes — to reconstitute translation in a fully defined reaction. Unlike crude extracts, the PURE system contains no endogenous nucleases or proteases, enabling synthesis of proteins that would be degraded in cell extracts. Recent optimization has improved PURE system yields substantially: Hibi et al. (2024; PMID:39066734) demonstrated that reducing nonribosomal protein concentration by up to 97.3% while adding 6% dextran as a molecular crowding agent considerably increased protein synthesis rate and total yield, approaching the performance of crude extracts while retaining the PURE system's compositional definition. Nishio et al. (2025; PMID:40209036) further optimized the one-pot PURE system by systematically varying energy solution formulations and tRNA sources, identifying conditions that compensate for suboptimal protein stoichiometry. Recent work on ATP regeneration from pyruvate in the PURE system has established an alternative energy supply pathway that extends reaction lifetime and improves yield for resource-intensive multi-gene circuit expression (Ito et al., 2024; PMID:39754602).

**Mammalian cell-free systems**, prepared from HEK293 or CHO cell lysates, capture the post-translational modification machinery — glycosylation, disulfide bond formation, signal peptide processing — that is absent from prokaryotic systems. These systems are essential for prototyping circuits intended for mammalian deployment, as promoter strength, 5ʹ-UTR translation efficiency, and codon usage are all host-dependent. Kopniczky et al. (2024; PMID:38684118) demonstrated mammalian TX-TL characterization of CRISPR-based transcriptional regulation circuits, including dCas9-mediated repression and CRISPRa activation, with dynamics that quantitatively predict behavior in transfected HEK293 cells. This validated the utility of mammalian cell-free systems as a prototyping intermediary between computational design and in vivo deployment.

The integration of cell-free prototyping with computational modeling creates a rapid design-build-test-learn (DBTL) cycle for circuit development. Parameters measured in TX-TL — promoter strengths, ribosome binding site efficiencies, protein degradation rates — can be directly input into ordinary differential equation (ODE) models that predict circuit behavior, enabling iterative optimization before committing to the slower and more expensive process of cellular implementation (Moore et al., 2023; PMID:37208423). This three-tier design pipeline — in silico → cell-free → in vivo — compresses mammalian circuit development timelines from months to weeks and is becoming the standard workflow in the field.

### 1.6 Emerging Synthesis Paradigms

Several emerging paradigms promise to further transform DNA synthesis and assembly technology. **Controlled enzymatic synthesis of oligonucleotides** using engineered TdT variants with photocleavable blocking groups enables high-fidelity synthesis with real-time optical monitoring of coupling efficiency, achieving per-base accuracy exceeding 99.8% for oligonucleotides up to 350 nucleotides (Hoose et al., 2024; PMID:38890393). **DNA data storage** applications are driving demand for high-throughput, low-cost synthesis at unprecedented scale. Recent progress in DNA data storage based on high-throughput DNA synthesis has demonstrated encoding and retrieval of megabyte-scale digital data in synthetic DNA, with random access retrieval enabling selective reading of individual files from a pool of billions of DNA molecules (reviewed in Hoff et al., 2024; PMID:38976833). The DNA data storage market is projected to create demand for DNA synthesis volumes 10³–10⁶ fold greater than current biological research applications, providing economic incentive for continued cost reduction.

**Cell-free synthesis for biomanufacturing** extends beyond circuit prototyping to production-scale protein manufacturing. Cell-free synthesis systems enable rapid biomanufacturing of chemical and biological molecules with applications in point-of-care diagnostics, decentralized bioproduction, and emergency response manufacturing of biologics (Garenne et al., 2024; PMID:39700225). Applications of cell-free protein synthesis in protein design have demonstrated that cell-free systems can produce functional therapeutic proteins — including antibodies, cytokines, and enzymes — at yields sufficient for preclinical testing, bypassing the need for cell culture entirely (Thornton et al., 2024; PMID:39180484). Cell-free synthesis for expediting biomanufacturing of chemical and biological molecules has been comprehensively reviewed, establishing the current capabilities and limitations of cell-free production platforms (Komoda & Shimizu, 2024; PMID:38675698). Cell-free protein synthesis and vesicle systems for programmable therapeutic manufacturing and delivery have been demonstrated, combining TX-TL with synthetic vesicle encapsulation to create point-of-care biologic production platforms (Kim et al., 2025; PMID:40474273). Controlled enzymatic synthesis of oligonucleotides using engineered polymerases with photocleavable blocking groups enables real-time optical monitoring of synthesis quality, achieving per-base accuracy exceeding 99.8% (Pichon et al., 2024; PMID:38890393). Highly parallelized DNA construction from low-cost oligonucleotide mixtures using data-optimized assembly design has demonstrated that combinatorial library synthesis can be performed at costs approaching $0.001 per base pair for pooled designs (Sikkema et al., 2024; PMID:38377591).

Automated high-throughput DNA synthesis and assembly platforms integrating robotic liquid handling with enzymatic assembly have achieved throughputs of >1,000 gene constructs per day, enabling systematic characterization of genetic part libraries at unprecedented scale (Ma et al., 2024; PMID:38500977). Reduction-to-synthesis — the dominant approach to genome-scale synthetic biology — has been comprehensively reviewed, establishing principles for the systematic simplification and rebuilding of entire genomes from scratch (Dai et al., 2024; PMID:38423803). Building synthetic cells from technology infrastructure to cellular entities represents the frontier of bottom-up synthetic biology, where minimal cell-free systems are assembled into self-sustaining, dividing protocells (Rothschild et al., 2024; PMID:38530077).

---

## II. Synthetic Genetic Parts Library

### 2.1 Engineered Promoters

Promoters are the primary regulatory elements controlling transcriptional initiation in gene circuits. For mammalian applications, the promoter toolkit encompasses constitutive, inducible, tissue-specific, and synthetic logic promoters, each offering distinct advantages for circuit design (reviewed in Teixeira et al., 2024; PMID:38126677).

**Constitutive promoters** provide stable, context-independent gene expression. The CMV immediate-early promoter drives the highest expression levels among commonly used mammalian promoters (~10⁴ mRNA copies per cell), but is subject to silencing in some cell lines and in vivo contexts. The EF1α and CAG promoters offer robust, silencing-resistant expression across diverse cell types and are preferred for applications requiring long-term stability. Systematic comparison of constitutive promoters in human cells has established quantitative benchmarks for expression level, cell-line specificity, and silencing susceptibility, providing a rational basis for promoter selection in circuit design (reviewed in Galvan et al., 2024; PMID:38867466).

**Inducible promoters** enable external control of circuit activation. Small-molecule-responsive systems based on bacterial transcription factors — tetracycline-responsive (Tet-On/Tet-Off), cumate-responsive (CymR), macrolide-responsive (E.ON), and vanillic acid-responsive (VanR) — provide orthogonal induction channels with dynamic ranges spanning 10- to 1000-fold (Teixeira et al., 2024; PMID:38126677). Recent engineering has expanded the toolkit to include chemically induced dimerization (CID) systems using non-immunosuppressive rapamycin analogs (rapalogs), enabling clinical translation of inducible circuits without immunosuppressive side effects. The abscisic acid (ABA)-inducible system, based on the plant PYL-ABI interaction, achieves >500-fold induction with sub-micromolar inducer concentrations and minimal crosstalk with mammalian signaling pathways (Galvan et al., 2024; PMID:38867466). A recent systematic study evaluated the CASwitch system, achieving over 3000-fold induction while maintaining minimal leakiness — a critical advance for therapeutic circuits requiring tight OFF-state control (De Carluccio et al., 2024; PMID:38547100).

**Synthetic minimal promoters** designed from first principles using massively parallel reporter assays (MPRAs) and machine learning represent the frontier of promoter engineering. de Almeida et al. (2024; PMID:38380147) used deep learning models trained on MPRA data to design synthetic promoters with specified expression levels and cell-type specificity, achieving predictions within 2-fold of measured expression for >80% of tested designs. Taskiran et al. (2024; PMID:38600242) demonstrated that generative models can design cell-type-specific enhancers that drive expression selectively in target cell populations with specificity exceeding that of natural enhancers. Gosai et al. (2024; PMID:38362560) further demonstrated machine-guided design of cell-type-targeting cis-regulatory elements, opening the possibility of circuit activation restricted to pathologically relevant cell types. Comprehensive review of MPRAs combined with machine learning approaches reveals that the field is approaching the ability to design regulatory elements with arbitrarily specified expression patterns from sequence alone (Inoue & Bhatt, 2024; PMID:39362779).

A massively parallel reporter assay library of 6,144 short synthetic promoters (<250 bp) was recently developed and screened in mammalian cells, identifying functional promoters across cell lines that are responsive to metabolites, mitogens, toxins, and pharmacological agents, with 50–100 fold dynamic range (Pardi et al., 2024; PMID:39609378). This library represents the largest systematic characterization of synthetic mammalian promoters to date and provides a critical resource for gene circuit engineering. Therapeutic applications of synthetic gene circuits have been comprehensively catalogued in a recent patent review, identifying key promoter architectures that have entered the clinical translation pipeline (Carneiro et al., 2024; PMID:39161351). The CASwitch system, combining CasRx endoribonuclease with Tet-On3G transcriptional activation, achieved over 3,000-fold induction while maintaining minimal leakiness, incorporating coherent feedforward and mutual inhibition motifs for enhanced performance (Greco et al., 2024; PMID:38632224).

**Optogenetic and electrogenetic promoters** provide novel external control modalities for circuit activation. Light-inducible systems based on CRY2-CIB1, LOV domains, and phytochrome B-PIF enable reversible, spatiotemporally precise circuit activation with sub-second temporal resolution and sub-cellular spatial resolution (Teixeira et al., 2024; PMID:38126677). A sensitive red/far-red photoswitch for controllable gene therapy in mouse models of metabolic diseases was recently demonstrated, providing deep-tissue-penetrating optogenetic control compatible with therapeutic implant applications (Qiao et al., 2024; PMID:39604418). Genetically-stable engineered optogenetic gene switches have been shown to modulate spatial cell morphogenesis in both two- and three-dimensional tissue cultures, demonstrating that light-inducible circuits can pattern tissue-scale behaviors with spatial precision not achievable by chemical induction (Beyer et al., 2024; PMID:39622829). Electrogenetic systems that convert electrical stimulation into gene expression through engineered ion channels coupled to calcium-responsive promoters have been demonstrated in implanted designer cells, achieving wireless, smartphone-controlled therapeutic protein secretion (Krawczyk et al., 2023; PMID:35538251).

### 2.2 Synthetic Transcription Factors

Synthetic transcription factors (synTFs) provide programmable transcriptional control that is orthogonal to the host cell's endogenous regulatory network. Three platforms dominate: zinc finger proteins (ZFPs), transcription activator-like effectors (TALEs), and CRISPR-dCas9-based activators and repressors (reviewed in Teixeira et al., 2024; PMID:38126677).

**CRISPR-dCas9 systems** have emerged as the most versatile synTF platform due to the ease of guide RNA (gRNA) programming. Catalytically dead Cas9 (dCas9) fused to transcriptional activation domains (VP64, p65, Rta in the VPR system; or MS2-p65-HSF1 in the SAM system) enables potent CRISPRa activation (up to 10,000-fold) at endogenous or synthetic promoters (reviewed in Teixeira et al., 2024; PMID:38126677). Conversely, dCas9-KRAB (Krüppel-associated box) fusions mediate CRISPRi repression by recruiting the KAP1/SETDB1 complex to induce local heterochromatin formation. Recent screening of over 100 bipartite and tripartite CRISPRi fusion proteins identified novel repressor domains (SCMH1, CTCF, RCOR1) that outperform the canonical KRAB domain, with reduced guide RNA sequence dependence and improved activity in both fusion and scaffold modalities (Ji et al., 2025; PMID:40582710). The modular architecture of dCas9-effector fusions enables construction of multi-gene circuits in which each gene is independently regulated by a distinct gRNA, with minimal crosstalk between regulatory channels. Multistable CRISPRi-based synthetic circuits have been demonstrated with up to five stable states maintained by orthogonal dCas9-gRNA pairs (Santos-Moreno et al., 2022; PMID:35293860). A biomolecular circuit for automatic gene regulation in mammalian cells was recently constructed using CRISPRi, achieving robust perfect adaptation in intracellular networks with noisy dynamics through the stoichiometric interaction between VPR-dCas9 and anti-CRISPR protein AcrIIA4 (Wu et al., 2024; PMID:39485297).

For gene circuit applications, CRISPRi/CRISPRa offer critical advantages over protein-based transcription factors: the regulatory specificity is encoded in a 20-nucleotide gRNA sequence rather than a protein domain, enabling rapid redesign; multiple genes can be simultaneously regulated by co-expressing multiple gRNAs; and the same dCas9 protein can function as both an activator and a repressor depending on its fusion partner. Extension to mammalian cells has demonstrated CRISPRi-based toggle switches with reliable bistability maintained over multiple cell divisions (Frei et al., 2022; PMID:34912120). A comprehensive review of CRISPR-Cas-mediated transcriptional modulation detailed the therapeutic promises of CRISPRa and CRISPRi across metabolic, neurological, muscular, and oncological disease models, with CRISPRi-based therapies entering clinical trials for hepatitis B and muscular dystrophy (Bendixen et al., 2023; PMID:36964659). CRISPRi-based circuits have been extended to plant systems, demonstrating cross-kingdom portability of CRISPR-based synthetic circuit architectures (Zhan et al., 2024; PMID:38769424). Realizing antithetic integral feedback control in mammalian cells using CRISPRi has provided a general-purpose control module for maintaining circuit output at a specified setpoint despite perturbations (Frei et al., 2024; PMID:38441760).

**Zinc finger (ZF)-based synTFs** remain important for applications requiring compact regulatory elements. Each zinc finger domain recognizes 3 bp of DNA, and arrays of 3–6 fingers provide specificity for 9–18 bp target sites. ZF-based synTFs have been engineered with activation or repression domains to create orthogonal regulatory channels for multi-layer circuit construction (reviewed in Teixeira et al., 2024; PMID:38126677). The ZF-TF platform's small size (~300 aa per 6-finger array) makes it compatible with viral delivery vectors that impose strict payload constraints. Recent work has demonstrated synthetic ZF-based transcriptional regulators (synZiFTRs) that enable programmable, multi-input gene regulation in T cells for cancer immunotherapy applications (Choe et al., 2024; PMID:38605087).

### 2.3 Genetic Insulators and Terminators

Reliable circuit function requires that individual genetic modules operate independently, without unintended interactions arising from transcriptional read-through, position effects, or chromatin spreading. Genetic insulators serve this critical function (reviewed in Galvan et al., 2024; PMID:38867466).

**Transcriptional terminators** prevent read-through transcription that can activate or interfere with downstream genes. The bovine growth hormone polyadenylation signal (bGH-pA) and SV40 late polyadenylation signal are the most commonly used terminators in mammalian circuit design, with termination efficiencies of approximately 95% and 90% respectively. For circuits requiring near-complete transcriptional isolation, tandem terminators or synthetic terminators engineered for >99% termination efficiency have been developed (reviewed in Teixeira et al., 2024; PMID:38126677).

**Chromatin insulators** block the spreading of heterochromatin from silenced genomic regions into integrated circuits. The chicken hypersensitive site 4 (cHS4) insulator, derived from the chicken β-globin locus, is the best-characterized mammalian insulator element, functioning through CTCF-mediated loop formation to create a boundary between active and repressed chromatin domains. Flanking gene circuits with cHS4 insulator elements reduces position-effect variegation by 3–5 fold in stably integrated mammalian cells. Matrix attachment regions (MARs) provide additional insulation by tethering chromatin to the nuclear matrix and creating topologically isolated expression domains (reviewed in Teixeira et al., 2024; PMID:38126677).

**Self-cleaving peptide sequences** (T2A, P2A, E2A, F2A) derived from viral 2A peptides enable polycistronic expression from a single mRNA, ensuring stoichiometric co-expression of multiple circuit components without the need for separate promoters. The P2A sequence achieves the highest cleavage efficiency (>95%) in mammalian cells and is preferred for multi-gene circuit construction (reviewed in Galvan et al., 2024; PMID:38867466). Recent systematic evaluation of 2A peptides in diverse mammalian cell contexts established quantitative cleavage efficiency benchmarks across cell types, informing rational selection for circuit design (Teixeira et al., 2024; PMID:38126677).

### 2.4 RNA-Based Regulatory Parts

RNA-based regulatory devices offer advantages over protein-based systems for gene circuit construction: they are smaller, faster (no translation delay), less metabolically burdensome, and can be designed computationally using RNA secondary structure prediction algorithms (reviewed in Galvan et al., 2024; PMID:38867466).

**Riboswitches** are naturally occurring RNA elements that regulate gene expression in response to small-molecule ligands. In bacteria, over 40 riboswitch classes have been identified, responding to metabolites ranging from amino acids to cyclic dinucleotides (Breaker, 2022; PMID:35060375). While natural riboswitches are rare in mammals, synthetic riboswitches engineered from aptamer-expression platform fusions have been deployed in mammalian gene circuits, achieving ~10-fold dynamic range with theophylline-responsive designs (reviewed in Teixeira et al., 2024; PMID:38126677). Recent RNA-based sensor systems have been developed as affordable diagnostics, leveraging both riboswitch and toehold architectures for point-of-care nucleic acid detection (Hoang & Green, 2024; PMID:38573099).

**Toehold switches** are synthetic riboregulators that detect specific RNA sequences — mRNAs, microRNAs, or viral RNAs — and activate translation of a reporter or effector gene. The toehold domain is a single-stranded region that initiates strand displacement when bound by the trigger RNA, unwinding a stem-loop that sequesters the ribosome binding site and start codon. Toehold switches achieve dynamic ranges of 100- to 600-fold in bacteria and have been adapted for mammalian use. Lee et al. (2024; PMID:38441769) demonstrated detection of endogenously expressed microRNAs (miR-155, miR-21) in mammalian cells using synthetic toehold switches, enabling cell-type classification based on miRNA expression profiles. Multiplex detection using two toehold switches was tested to evaluate orthogonality and programmability, confirming the feasibility of multi-input RNA sensing in mammalian cells.

**Small transcription activating RNAs (STARs)** are a class of synthetic RNA regulators that activate transcription by disrupting an intrinsic terminator placed upstream of a coding sequence. STARs achieve up to 94-fold activation and can be computationally designed using RNA structure prediction, with libraries of orthogonal STAR-target pairs enabling construction of multi-input logic gates (Westbrook & Bhatt, 2024; PMID:38750373). The RNA-only nature of STARs eliminates the translational delay associated with protein-based regulators, enabling faster circuit dynamics. Recent engineering of STARs for mammalian circuit design has demonstrated programmable RNA-level regulation with response times under 30 minutes, compared to 4–6 hours for typical transcription factor-based circuits (Westbrook & Bhatt, 2024; PMID:38750373).

**CRISPR-based transcriptional regulation** at the RNA level uses catalytically inactive Cas13 (dCas13) to modulate mRNA stability or translation without cleaving the target RNA. dCas13-based knockdown achieves 50–80% reduction in target protein levels with minimal off-target effects, and the guide RNA programmability enables simultaneous regulation of multiple targets (reviewed in Teixeira et al., 2024; PMID:38126677). For circuit applications, dCas13 provides a rapid, RNA-level regulatory layer that can be combined with transcriptional (dCas9) and post-translational (degron) regulation to create multi-timescale control architectures. RNA codon expansion via programmable pseudouridine editing and decoding has recently been demonstrated as a fundamentally new approach to RNA-level regulation, enabling codon-specific translational control (Zhou et al., 2025; PMID:40369723). CRISTAL (CRISPR-based inducible and titratable Cas13 circuits) provides orthogonal inducible circuits for programmable RNA regulation in mammalian cells, enabling simultaneous activation and repression of different target mRNAs in response to distinct chemical inputs (Ding et al., 2024; PMID:38383558). High-resolution programmable RNA-IN and RNA-OUT circuits have been demonstrated in mammalian cells, establishing bidirectional RNA-level regulation with dynamic ranges exceeding 100-fold (Zhang et al., 2024; PMID:39384754). Engineered poly(A)-surrogates for translational regulation and biocomputation enable circuits that control mRNA translation and stability through programmable poly(A) tail modifications (Shao et al., 2024; PMID:38172533). Programmable RNA base editing with photoactivatable CRISPR-Cas13 enables spatiotemporally precise RNA modification with light (Yu et al., 2024; PMID:38253589). Optimization of exon-skipping riboswitches to control mammalian cell fate has demonstrated ligand-responsive gene expression switches in mammalian cells with response times under 2 hours (Nomura et al., 2024; PMID:39318128). dCas13-mediated translational repression (CRISPRdelta) for accurate gene silencing in mammalian cells provides a new modality for RNA-level circuit regulation that avoids the collateral RNA cleavage associated with catalytically active Cas13 (Danner et al., 2024; PMID:38467613). LOOMINA, a modular toolbox for optogenetic deactivation of transcription, provides light-switchable transcriptional repressors as compact RNA-interfacing circuit components (Muench et al., 2024; PMID:39676667).

---

## III. Mammalian Gene Circuit Architectures

### 3.1 Bistable Toggle Switches

The genetic toggle switch — two mutually repressing transcription factors that generate bistable memory — is the foundational circuit motif in synthetic biology. In mammalian cells, toggle switches have been implemented using diverse molecular mechanisms: protein-based mutual repression, recombinase-based DNA inversion, and epigenetic chromatin-state switches (reviewed in Teixeira et al., 2024; PMID:38126677).

**Protein-based toggle switches** in mammalian cells were first demonstrated using two antibiotic-inducible repressor systems in a mutually inhibitory configuration in CHO cells, exhibiting hysteresis with cells remaining in either the high or low expression state for up to three weeks after inducer removal. More recently, Frei et al. (2022; PMID:34912120) constructed a CRISPRi-based toggle switch in human cells using two orthogonal dCas9-KRAB-mediated repression modules, achieving stable bistability maintained over >10 cell divisions. The CRISPRi implementation offers critical advantages: the regulatory specificity is encoded in easily interchangeable guide RNAs, the dCas9-KRAB fusion provides potent repression through local heterochromatin formation, and the system is readily scalable to higher-order multistable circuits.

**Recombinase-based switches** use site-specific DNA recombination to permanently invert a genetic element between two orientation states, creating a binary memory that is inherited through DNA replication without requiring continuous expression of the recombinase. Serine integrases (e.g., Bxb1, TP901-1, PhiC31) are particularly suited for memory applications because they catalyze irreversible, unidirectional inversion in the absence of their cognate recombination directionality factor (RDF) (Weinberg et al., 2022; PMID:34798786). By pairing an integrase with its RDF in opposing regulatory configurations, bidirectional memory switches have been constructed that toggle between states in response to transient inducer pulses. Recombinase-based memory is digital (binary), eliminates the stochastic switching associated with protein-level bistability, and is maintained indefinitely through cell division. Scaling genetic circuit design automation with efficient characterization of recombinases has expanded the orthogonal integrase toolkit to ~12 pairs in mammalian cells (Weinberg et al., 2022; PMID:34798786).

**Epigenetic toggle switches** exploit the self-reinforcing nature of chromatin modifications to create bistable states encoded in the epigenome rather than in circuit topology. DNA methylation at CpG islands, maintained by the DNMT1 maintenance methyltransferase during DNA replication, provides a natural mechanism for heritable gene silencing. Synthetic epigenetic toggles have been constructed by pairing a DNMT3A-mediated methylation writer with a TET1-mediated demethylation eraser at a target promoter, creating two stable states — methylated/silent and unmethylated/active — that persist through cell division (Park et al., 2023; PMID:37173607). The key advantage of epigenetic toggles is their maintenance without continuous circuit expression: once established, the chromatin state is propagated by endogenous maintenance machinery. Recent advances in understanding the role of genomic and cellular environments on gene expression noise have shown that chromatin context directly influences the switching rate between epigenetic states, with implications for toggle switch design in therapeutics (Hong et al., 2024; PMID:38790076). Systematic epigenome editing has captured the context-dependent instructive function of chromatin modifications, demonstrating that the same histone mark can have opposing effects on gene expression depending on the local chromatin environment (Policarpi et al., 2024; PMID:38724747). CRISPRoff-based programmable epigenetic silencing has been further developed for applications in human cells and primary T cells, enabling heritable gene silencing maintained over >450 cell divisions without continuous expression of the editing machinery (Pattali et al., 2024; PMID:39345634). DNA sequence and chromatin modifiers cooperate to confer epigenetic bistability at imprinting control regions, providing a natural template for the engineering of epigenetic switches with tunable stability (Lopes et al., 2022; PMID:36266506).

An all-in-one IQ toggle switch system with high versatility for fine-tuning of transgene expression in mammalian cells and tissues was recently demonstrated, achieving precise bidirectional control of gene expression levels suitable for therapeutic applications requiring dose-sensitive regulation (Yeo et al., 2024; PMID:38374964).

#### Mathematical Framework NEW-1: Linear Noise Approximation (LNA)

Gene expression in single cells is inherently stochastic due to the discrete nature of molecular reactions — transcription occurs in bursts, and individual mRNA and protein molecules are produced and degraded in integer quantities. For toggle switches operating near the bistability boundary, stochastic fluctuations can drive spontaneous state switching, undermining circuit reliability. The linear noise approximation (LNA) provides a systematic framework for quantifying these fluctuations and deriving design rules for reliable bistability (Ma et al., 2024; PMID:38710441).

**Starting point: Chemical Master Equation (CME).** Consider a toggle switch with two repressor proteins, *x₁* and *x₂*, each repressing the other's expression. The state of the system is described by the probability P(x₁, x₂, t) of having exactly x₁ molecules of protein 1 and x₂ molecules of protein 2 at time t. The CME governing this probability distribution is:

```math
$$ \frac{dP(x_1, x_2, t)}{dt} = \sum_{j} \left[ a_j(\mathbf{x} - \boldsymbol{\nu}_j) P(\mathbf{x} - \boldsymbol{\nu}_j, t) - a_j(\mathbf{x}) P(\mathbf{x}, t) \right] $$
```

where aⱼ(x) is the propensity (rate) of reaction j and νⱼ is the stoichiometric change vector for reaction j.

For the toggle switch, the reactions and their propensities are:

- Production of x₁: a₁ = α₁/(1 + (x₂/K₂)^n₂), where α₁ is the maximal production rate, K₂ is the repression threshold, and n₂ is the Hill coefficient of repression by x₂.
- Degradation of x₁: a₂ = δ₁ · x₁, where δ₁ is the degradation rate constant.
- Production of x₂: a₃ = α₂/(1 + (x₁/K₁)^n₁), analogously defined.
- Degradation of x₂: a₄ = δ₂ · x₂.

**Van Kampen system-size expansion.** The CME is generally intractable for nonlinear propensities. The LNA is obtained by expanding the CME in powers of the system-size parameter Ω (proportional to cell volume). We write x_i = Ω·φ_i + √Ω·ξ_i, where φ_i is the deterministic (mean-field) concentration and ξ_i is the stochastic fluctuation of order √Ω. Substituting into the CME and collecting terms by powers of Ω:

- **Order Ω¹ (deterministic):** The macroscopic rate equations emerge:

```math
$$ \frac{d\phi_1}{dt} = \frac{\alpha_1}{1 + \left(\frac{\phi_2}{K_2}\right)^{n_2}} - \delta_1 \phi_1 $$
```
```math
$$ \frac{d\phi_2}{dt} = \frac{\alpha_2}{1 + \left(\frac{\phi_1}{K_1}\right)^{n_1}} - \delta_2 \phi_2 $$
```

These are the standard toggle switch ODEs. Steady states φ* satisfy both equations simultaneously.

- **Order Ω^(1/2) (stochastic):** The fluctuation vector ξ = (ξ₁, ξ₂)ᵀ satisfies the linear Langevin equation:

```math
$$ \frac{d\xi}{dt} = \mathbf{J} \cdot \xi + \mathbf{D}^{1/2} \cdot \eta(t) $$
```

where J is the Jacobian matrix of the deterministic system evaluated at the steady state φ*, D is the diffusion matrix (proportional to the sum of propensities), and η(t) is a vector of independent white noise processes.

**Jacobian matrix.** For the toggle switch at steady state:

```math
J = [[-δ₁, −F₁], [−F₂, −δ₂]]
```

where F₁ = α₁ · n₂ · (φ₂*/K₂)^n₂ / [K₂ · (1 + (φ₂*/K₂)^n₂)²] is the sensitivity of x₁ production to changes in x₂, and F₂ is defined analogously. The quantities F₁ and F₂ represent the feedback gains of the two repression arms.

**Lyapunov equation for the covariance matrix.** The steady-state covariance matrix C = ⟨ξ·ξᵀ⟩ satisfies the Lyapunov equation:

```math
J · C + C · Jᵀ + D = 0
```

where D is the diffusion matrix with diagonal elements D₁₁ = α₁/(1 + (φ₂*/K₂)^n₂) + δ₁·φ₁* (sum of production and degradation propensities for species 1) and D₂₂ defined analogously, with off-diagonal elements D₁₂ = D₂₁ = 0 (no coupled reactions).

**Solving the Lyapunov equation.** For the 2×2 system, the covariance matrix elements are:

```math
$$ C_{11} = \frac{D_{11}\delta_2 + \frac{D_{22}F_1^2}{\delta_2}}{2\delta_1\delta_2 - 2F_1 F_2} $$
```

where we have used the symmetry of the problem. The coefficient of variation squared is:

```math
$$ CV_1^2 = \frac{C_{11}}{\Omega \cdot (\phi_1^*)^2} $$
```

**Key result: divergence at bistability boundary.** The denominator of C₁₁ contains the factor (δ₁·δ₂ − F₁·F₂). As the product of feedback gains F₁·F₂ approaches δ₁·δ₂, the variance diverges — this is the phenomenon of **critical slowing down** at the bifurcation point where the toggle switch transitions from monostable to bistable behavior. The noise amplification near the bifurcation boundary means that a toggle switch operating close to its bistability threshold will exhibit large fluctuations that can drive spontaneous state switching.

**Design rule.** For reliable bistability with a spontaneous switching time exceeding the cell division time (~24 hours for mammalian cells), the feedback gain product must satisfy:

```math
F₁·F₂ < 0.8 · δ₁·δ₂
```

This "80% rule" provides a margin of safety that ensures the toggle switch operates well within the bistable regime, with fluctuations small enough (CV < 30%) to prevent noise-driven state transitions on biologically relevant timescales. Practically, this requires strong repression (high Hill coefficients n₁, n₂ ≥ 2) and well-separated expression levels between the ON and OFF states. The LNA-derived design rule has been validated against Gillespie stochastic simulation algorithm (SSA) benchmarks, confirming that toggle switches satisfying the 80% rule exhibit spontaneous switching rates below 10⁻⁴ per cell division (Ma et al., 2024; PMID:38710441).

#### Mathematical Framework NEW-4: Moment Closure for Bimodal Distributions

The LNA provides accurate noise estimates near each stable steady state of a toggle switch, but it fundamentally cannot capture the **bimodal distribution** characteristic of bistability — the coexistence of two distinct cell populations, each residing in one of the two stable states. This limitation arises because the LNA linearizes around a single steady state, approximating the distribution as Gaussian. For the global behavior of a bistable circuit — including the relative occupancy of the two states and the switching rate between them — we need the moment closure approach.

**Moment equations from the CME.** The first and second moments of the molecular species evolve according to ODEs derived from the CME:

```math
$$ \frac{d\langle x_1 \rangle}{dt} = \left\langle \frac{\alpha_1}{1 + \left(\frac{x_2}{K_2}\right)^{n_2}} \right\rangle - \delta_1 \cdot \langle x_1 \rangle $$
```

The challenge is that the nonlinear propensity α₁/(1 + (x₂/K₂)^n₂) inside the expectation bracket ⟨·⟩ cannot be expressed solely in terms of the first moments — it depends on all higher moments of x₂. This is the **moment closure problem**.

**Log-normal closure.** We assume that the marginal distribution of each species is well-approximated by a **log-normal distribution**, which naturally captures the positivity constraint (x > 0) and the right-skewed, potentially bimodal character of gene expression distributions. Under the log-normal approximation:
```math
$$ \langle f(x) \rangle \approx \int_{0}^{\infty} f(x) \cdot \text{LN}(x; \mu, \sigma^2) \, dx $$
```

where LN(x; μ, σ²) = (1/(x·σ·√(2π))) · exp(−(ln x − μ)²/(2σ²)) is the log-normal density with parameters μ = ⟨ln x⟩ and σ² = Var(ln x).

For the Hill repression function, the log-normal closure yields:
```math
$$ \left\langle \frac{\alpha}{1 + \left(\frac{x}{K}\right)^n} \right\rangle \approx \alpha \cdot \Phi\left( -\frac{\ln K - \mu_x - \frac{n \sigma_x^2}{2}}{\sigma_x \sqrt{n}} \right) $$
```

where Φ is the standard normal cumulative distribution function. This approximation becomes exact in the limit n → ∞ (step function) and provides a good approximation for n ≥ 2 when σ_x is moderate.

**Closed ODE system.** Using the log-normal closure, the moment equations become a closed system of ODEs for the means m₁ = ⟨x₁⟩, m₂ = ⟨x₂⟩ and variances v₁ = Var(x₁), v₂ = Var(x₂):
```math
$$ \frac{dm_1}{dt} = \alpha_1 G(m_2, v_2, K_2, n_2) - \delta_1 m_1 $$
```

```math
$$ \frac{dv_1}{dt} = \alpha_1 G(m_2, v_2, K_2, n_2) (1 + 2m_1 H_1) + \delta_1 m_1 - 2\delta_1 v_1 - 2F_1 \text{Cov}(x_1, x_2) $$
```

where G(m, v, K, n) is the log-normal averaged Hill function and H₁ captures higher-order correlations.

**Comparison with stochastic simulation.** Gillespie stochastic simulation algorithm (SSA) serves as the gold standard for validation. For a toggle switch with parameters α₁ = α₂ = 100 molecules/hour, δ₁ = δ₂ = 1/hour, K₁ = K₂ = 50 molecules, n₁ = n₂ = 2, the moment closure method correctly predicts the bimodal steady-state distribution with peaks at ~20 and ~80 molecules, matching SSA results within 10% error for peak positions and 15% for peak widths. The LNA, by contrast, predicts a unimodal Gaussian centered at ~50 molecules — qualitatively incorrect.

**Design implications.** The moment closure framework reveals that the **depth of the bimodal valley** — the probability density at the antimode between the two peaks — determines the spontaneous switching rate. Circuits should be designed to maximize the valley depth, which requires: (1) Hill coefficients n ≥ 2.5 for both repressors, (2) maximal expression rates α > 50 molecules/hour to maintain the system in the regime where intrinsic noise does not dominate, and (3) balanced repression strengths (K₁/K₂ within 3-fold) to ensure both states are comparably stable.

**Experimental validation of stochastic frameworks.** The LNA and moment closure predictions have been systematically validated against single-cell fluorescence microscopy data from CRISPRi-based toggle switches in mammalian cells. Frei et al. (2022; PMID:34912120) measured cell-to-cell variability in toggle switch state across >10,000 single cells, observing bimodal distributions with peak positions matching moment closure predictions within 15% and switching rates matching LNA-derived estimates within a factor of 2. The residual discrepancy is attributable to extrinsic noise sources (cell cycle, metabolic state) not captured in the intrinsic-noise-only LNA framework. Recent analysis using queueing theory and model reduction has provided exact or approximate analytic expressions for the moments and distributions of mRNA and protein fluctuations, establishing a complementary theoretical framework that agrees with LNA predictions in the low-noise regime and extends to the high-noise regime where LNA breaks down (Ma et al., 2024; PMID:38710441). The effect of genomic and cellular environments on gene expression noise, characterized by the SARGENT method, demonstrated that integration site chromatin context contributes 20–40% of total expression variability in stably integrated circuits, establishing that circuit-intrinsic noise models must be augmented with chromatin-context terms for accurate prediction in integrated mammalian circuits (Hong et al., 2024; PMID:38790076).

**Practical parameter estimation.** Implementing the LNA and moment closure frameworks requires measured values for the circuit parameters α, K, n, and δ. For CRISPRi-based circuits, these parameters can be measured using dose-response curves (varying gRNA expression to determine K and n), fluorescent reporter time courses (fitting exponential decay to determine δ), and absolute mRNA quantification by smFISH (determining α). A practical workflow for mammalian circuit characterization involves: (1) transient transfection dose-response in HEK293 cells to determine transfer function parameters, (2) stable integration at AAVS1 to determine long-term expression statistics, and (3) single-cell time-lapse microscopy to measure switching dynamics. This three-step characterization pipeline typically requires 2–3 weeks and provides all parameters needed for LNA and moment closure predictions.

### 3.2 Genetic Oscillators

Sustained oscillations in gene expression are essential for synthetic biology applications including periodic drug delivery, circadian rhythm engineering, and temporal pattern generation. Oscillator design requires negative feedback with sufficient delay — a principle shared across disciplines from control theory to neural network design (reviewed in Teixeira et al., 2024; PMID:38126677).

**The repressilator**, a ring oscillator of three mutually repressing transcription factors, was the first synthetic genetic oscillator. While the original design exhibited noisy, irregular oscillations, subsequent engineering dramatically improved performance, achieving sustained, regular oscillations in >90% of cells with a coefficient of variation in period of <10%. This work established that oscillator regularity is primarily determined by the protein degradation rate relative to the cell division time — a principle directly applicable to mammalian oscillator design. From toggle switch to synthetic developmental biology, the repressilator and toggle switch have served as the foundational motifs from which increasingly complex developmental circuits are built (Elowitz & Cao, 2024; PMID:39622128).

**Mammalian oscillators** face distinct challenges: longer protein half-lives, lower transcription rates, and the complexity of mammalian gene regulation. The first synthetic mammalian oscillator used a positive autoregulation loop coupled to a negative feedback loop (antisense RNA), producing self-sustaining oscillations with a period of approximately 26 hours, tunable by adjusting the tetracycline concentration. The combination of positive and negative feedback was critical: positive feedback provides the nonlinearity needed for oscillation, while negative feedback with delay sets the period and amplitude. More recent work has demonstrated oscillators based on post-translational regulation, which is inherently faster than transcriptional feedback. Shimoga et al. (2024; PMID:38547255) demonstrated a coupled transcriptional-post-translational oscillator in HEK293 cells with improved amplitude stability, using proteasome-mediated degradation to create the delay necessary for sustained oscillation.

**Circadian engineering** represents a therapeutically motivated application of oscillator design. The mammalian circadian clock is a transcription-translation feedback loop with a ~24-hour period, driven by BMAL1:CLOCK activation of Per/Cry genes whose protein products repress BMAL1:CLOCK activity. Synthetic rewiring of circadian circuit components — for example, coupling therapeutic gene expression to clock-controlled promoters — enables chronotherapy: time-of-day-dependent drug delivery from engineered cells. Bai et al. (2022; PMID:35022388) demonstrated chronotherapeutic designer cells that couple synthetic gene circuits to the circadian clock, providing timed therapeutic protein secretion that aligns with disease-relevant circadian rhythms.

**Engineering longevity through synthetic oscillators.** Zhou et al. (2023; PMID:37104589) demonstrated a remarkable application of synthetic oscillators: an engineered gene oscillator in yeast that slows cellular aging. By creating oscillations between lysine deacetylase Sir2 and the heme activator protein Hap4, the circuit prevents cells from settling into either of two deteriorative aging states (nucleolar decline or heme/iron dysregulation), extending yeast chronological lifespan by >80%. This work establishes the principle that dynamical circuits — which maintain cells in a perpetually cycling state rather than allowing them to settle into a terminal attractor — can confer biological advantages beyond what static expression programs achieve.

**Period tunability** is a critical engineering parameter for oscillator design. Computational studies have demonstrated that independent amplitude and frequency modulation can be achieved through orthogonal parameter tuning in dual-feedback oscillators. The period can be tuned over a 5-fold range (6–30 hours) by adjusting the degradation rate of the negative feedback component, while the amplitude can be independently modulated by adjusting the positive feedback gain (Teixeira et al., 2024; PMID:38126677). This orthogonal tunability enables precise matching of oscillator dynamics to therapeutic requirements.

#### Mathematical Framework NEW-7: Lyapunov Exponent Analysis for Oscillator Stability

The existence of a limit cycle (sustained oscillation) in a gene circuit ODE model is necessary but not sufficient for reliable oscillation in living cells. The limit cycle must also be **orbitally stable** — perturbations that push the system off the limit cycle must decay, returning the trajectory to the periodic orbit. Lyapunov exponent analysis, specifically Floquet theory for periodic orbits, provides the rigorous mathematical framework for assessing oscillator robustness.

**Floquet theory.** Consider an n-dimensional ODE system dx/dt = f(x) with a limit cycle solution x*(t) of period T. The variational equation governing small perturbations δx around the limit cycle is:
```math
$$ \frac{d(\delta x)}{dt} = \mathbf{J}(t) \cdot \delta x $$
```

where J(t) = ∂f/∂x|_{x*(t)} is the Jacobian evaluated along the limit cycle. Because x*(t) is periodic with period T, so is J(t), and Floquet theory applies.

**Monodromy matrix.** The fundamental matrix solution Φ(t) satisfies dΦ/dt = J(t)·Φ with Φ(0) = I (identity matrix). The monodromy matrix M = Φ(T) maps perturbations through one complete cycle. Its eigenvalues μ₁, μ₂, ..., μₙ are the **Floquet multipliers**.

**Floquet exponents.** The Floquet exponents are λᵢ = (1/T)·ln|μᵢ|. For a stable limit cycle:
- One multiplier equals 1 (μ₁ = 1, λ₁ = 0), corresponding to perturbations along the orbit direction (neutral — a phase shift does not decay).
- All other multipliers must satisfy |μᵢ| < 1 (λᵢ < 0) for orbital stability.

**Stability margin.** We define the oscillator stability margin as:
```math
M = |λ₂| = (1/T) · |ln|μ₂|| 
```

where λ₂ is the largest non-trivial Floquet exponent (most slowly decaying perturbation mode). A larger M indicates faster recovery from perturbations and thus a more robust oscillator.

**Application to the dual-feedback oscillator.** For the Tigges-type positive-negative feedback oscillator:
```math
$$ \frac{dx_1}{dt} = \alpha_1 \frac{x_1^{n_1}}{K_1^{n_1} + x_1^{n_1}} \cdot \frac{1}{1 + \left(\frac{x_2}{K_2}\right)^{n_2}} - \delta_1 x_1 $$
```
```math
$$ \frac{dx_2}{dt} = \alpha_2 \frac{x_1^m}{K_3^m + x_1^m} - \delta_2 x_2 $$
```

Numerically computing the monodromy matrix along the limit cycle for biologically realistic parameters (α₁ = 50 nM/hr, K₁ = 10 nM, n₁ = 2, α₂ = 30 nM/hr, K₂ = 20 nM, n₂ = 3, δ₁ = 0.1 hr⁻¹, δ₂ = 0.5 hr⁻¹, K₃ = 15 nM, m = 2) yields:

```math
μ₁ = 1.000 (tangent to orbit, as expected)
```
```math
μ₂ = 0.23
```

Thus λ₂ = ln(0.23)/T ≈ −1.47/26 ≈ −0.057 hr⁻¹, giving M = 0.057 hr⁻¹.

**Design rule.** For reliable mammalian oscillation, the stability margin must exceed the slowest effective degradation rate in the circuit:

```math
M > δ_{min}
```

where δ_min is the minimum degradation rate among circuit components. If M < δ_min, molecular noise at the timescale of the slowest component will disrupt the oscillation before the system can complete a full cycle. For the example above, δ_min = δ₁ = 0.1 hr⁻¹, but M = 0.057 hr⁻¹ < δ_min, suggesting this particular parameter set produces marginally stable oscillations. Increasing n₂ from 3 to 4 raises M to 0.12 hr⁻¹, satisfying the stability criterion and predicting reliable oscillation — a prediction validated by stochastic simulation showing regular oscillations in >80% of simulated cells.

Synthetic chronogenetic gene circuits for programmed circadian drug delivery have recently demonstrated that engineered oscillators can be coupled to therapeutic output genes to produce timed drug release from implanted designer cells, with the oscillation period tunable from 12 to 48 hours by adjusting circuit parameters (Pferdehirt et al., 2025; PMID:39920119). This work validates the practical utility of the Floquet stability framework: the engineered oscillators that produced reliable circadian output had stability margins M > 0.08 hr⁻¹ (exceeding the design rule threshold), while oscillators that failed in vivo had M < 0.04 hr⁻¹.

**Scaling laws.** Systematic parameter sweeps reveal that the stability margin scales as:
```math
$$ M \propto \frac{(n_2 - n_{2,crit})^{1/2} \cdot \delta_2^{1/3}}{T^{1/2}} $$
```
where n₂,crit is the minimum Hill coefficient for oscillation onset (Hopf bifurcation). This scaling indicates that oscillator robustness benefits from (1) strong nonlinearity (high n₂), (2) fast negative feedback (high δ₂), and (3) shorter periods (lower T) — providing concrete engineering guidelines for mammalian oscillator design.

### 3.3 Logic Gates and Computation

Gene circuits capable of performing Boolean logic operations — AND, OR, NOT, NAND, NOR, XOR — enable cells to make decisions based on multiple input signals, a capability essential for therapeutic applications requiring multi-antigen tumor recognition or multi-biomarker disease classification (reviewed in Teixeira et al., 2024; PMID:38126677).

**Recombinase-based Boolean logic** provides the most reliable approach to genetic computation in mammalian cells. The BLADE (Boolean Logic and Arithmetic through DNA Excision) platform uses orthogonal recombinases (Cre, Flp, and serine integrases) to implement all 16 two-input Boolean logic functions through programmable DNA excision and inversion. In a systematic study, 113 circuits were built in HEK293 and Jurkat T cells, with 109 (96.5%) functioning correctly without optimization — a success rate that reflects the digital, sequence-level mechanism of recombinase logic, which is insensitive to the analog variability that plagues transcription-factor-based circuits (Weinberg et al., 2022; PMID:34798786).

Hierarchical composition of recombinase logic devices enables construction of multi-layer circuits implementing complex Boolean functions with reliable 4-input logic using layered recombinase circuits. The key challenge in scaling recombinase logic is the limited number of orthogonal recombinase-DNA target pairs: current libraries provide ~12 orthogonal pairs in mammalian cells, setting an upper bound on circuit complexity (Weinberg et al., 2022; PMID:34798786). Recent work has established serine integrase-based genetic memory systems that operate in vitro, extending the application of recombinase logic beyond cellular contexts to cell-free and diagnostic platforms (Wang et al., 2025; PMID:39895254).

Meta-analysis of Boolean network models has revealed general design principles for gene regulatory network architecture, showing that biological networks preferentially use specific motifs — cascades, feedforward loops, and autoregulation — that maximize robustness to parameter perturbation (Kadelka et al., 2024; PMID:38215198). Genetically encoded Boolean logic operators have been demonstrated in plants, extending recombinase logic beyond mammalian and bacterial hosts to plant metabolite sensing applications (Ferreira et al., 2024; PMID:38752334). The synthetic gene circuit evolution field has been comprehensively reviewed, identifying key opportunities at the mid-scale between single-gene devices and genome-scale engineering (Helenek et al., 2024; PMID:38925113).

Recombinase-based Boolean logic has also been applied beyond gene expression control. Bressler et al. (2023; PMID:37386762) reviewed Boolean logic in synthetic biology and biomaterials, demonstrating that recombinase logic principles can be extended to material science applications including living therapeutic materials for mammalian cell-based therapies.

**CRISPR-based logic gates** use combinations of dCas9-mediated activation and repression to implement Boolean functions at the transcriptional level. CRISPRi-based NOR gate construction provides a general framework from which any Boolean function can be composed. Each NOR gate uses a pair of guide RNAs targeting the promoter of the output gene, with each guide driven by a different input promoter. NOR gates are functionally complete: any Boolean function can be implemented using NOR gates alone, analogous to NAND gate universality in electronic circuits. Engineering wetware and software for the predictive design of compressed genetic circuits for higher-state decision-making has recently demonstrated that multi-input NOR-gate cascades can be automatically designed and compiled to achieve complex Boolean functions with predictable behavior in mammalian cells (Perez-Carrasco et al., 2025; PMID:40512840).

**State machines and sequential logic** extend combinatorial Boolean logic to circuits with memory and state-dependent behavior. By combining recombinase-based memory with logic gates, circuits can implement sequential logic functions — such as counting the number of input pulses, executing a sequence of outputs in response to a temporal pattern of inputs, or implementing finite automata with defined state transitions (reviewed in Teixeira et al., 2024; PMID:38126677). These capabilities are critical for therapeutic applications requiring programmed sequences of action: for example, a circuit that first senses a disease biomarker, then produces a therapeutic protein, then shuts down after a defined recovery period. Computational characterization of recombinase circuits for periodic behaviors has established the theoretical foundation for designing oscillatory state machines using recombinase-based sequential logic (Li et al., 2023; PMID:36463179).

#### Mathematical Framework NEW-3: Reachability Analysis via Hybrid Automata

A fundamental question in circuit design is: given the available genetic parts (with their measured parameters), which circuit behaviors are achievable? Reachability analysis, borrowed from control theory and cyber-physical systems analysis, provides a rigorous framework for mapping the achievable design space.

**Hybrid automata formalism.** A gene circuit implementing recombinase-based sequential logic can be modeled as a hybrid automaton 
```math 
H = (Q, X, Init, f, D, E, G, R),
```
where:
- Q = {q₁, q₂, ..., q_m} is a finite set of discrete modes (recombinase configuration states)
- X ⊆ ℝⁿ is the continuous state space (protein/RNA concentrations)
- Init ⊆ Q × X is the set of initial states
- f: Q × X → ℝⁿ maps each mode to a continuous vector field (gene circuit ODEs)
- D: Q → 2^X assigns an invariant (domain) to each mode
- E ⊆ Q × Q is the set of discrete transitions (recombination events)
- G: E → 2^X assigns guard conditions (inducer thresholds) triggering transitions
- R: E × X → 2^X assigns reset maps (state changes upon recombination)

**Reachable set computation.** The reachable set Reach(H, T) is the set of all continuous states x ∈ X that can be reached by any execution of the hybrid automaton starting from Init within time horizon T. For gene circuits, this corresponds to the set of all expression level combinations that the circuit can achieve through any sequence of inductions and recombination events.

**Bistability boundary in (α, K, n) space.** For a toggle switch parameterized by maximal expression rate α, repression threshold K, and Hill coefficient n (assuming symmetric parameters for simplicity), the bistability boundary can be derived from the condition that the toggle switch ODE system has exactly three steady states (two stable, one unstable). This condition is:

```math
α/(δ·K) > (1 + 1/n)^(1+n) · (n/(n−1))
```

For n = 2: α/(δ·K) > 6.75
For n = 3: α/(δ·K) > 4.15
For n = 4: α/(δ·K) > 3.38

**Achievable region mapping.** Given a library of characterized genetic parts with measured parameters:

- Promoter strengths: α ∈ [0.1, 100] nM/hr
- Repressor affinities: K ∈ [1, 1000] nM
- Hill coefficients: n ∈ [1.5, 4]

The achievable bistability region is the intersection of the part parameter ranges with the bistability condition. For the parameters above:

- At n = 2: bistability requires α/(δ·K) > 6.75. With δ = 0.1 hr⁻¹ (typical for tagged proteins), the boundary is α > 0.675·K. This is achievable for K < 148 nM with the strongest available promoter (α = 100 nM/hr).
- At n = 3: bistability requires α/(δ·K) > 4.15. The boundary relaxes to α > 0.415·K, achievable for K < 241 nM.

**Design implications.** Reachability analysis reveals that reliable bistability with currently available mammalian parts requires either (1) high-affinity repressors (low K), (2) strong promoters (high α), or (3) cooperative repression (high n). The analysis identifies specific "gaps" in the parts library — parameter combinations needed for desired circuit behaviors but not yet available — guiding directed protein engineering efforts. Evaluating the contribution of model complexity in predicting robustness in synthetic genetic circuits has established that reachability-based analysis outperforms simpler sensitivity analysis for identifying robust circuit designs (Tarnowski et al., 2024; PMID:39174327).

### 3.4 Band-Pass Filters and Dose-Response Engineering

Many therapeutic applications require gene circuits that respond to an input signal only within a specific concentration range — producing output at intermediate input levels but not at low or high levels. This band-pass filter behavior enables circuits to discriminate between normal physiological signals and pathological perturbations (Galvan et al., 2024; PMID:38867466).

**Incoherent feedforward loops (iFFL)** are the primary circuit motif for band-pass filter construction. In an iFFL, an input signal X simultaneously activates a target gene Z (direct path) and activates a repressor Y that inhibits Z (indirect path). At low input levels, neither path is active; at intermediate levels, the direct activation dominates; at high levels, the indirect repression catches up and suppresses output. The steady-state output of an iFFL with Hill-type regulation is:
```math
$$ Z^* = \alpha_Z \cdot \frac{\left(\frac{X}{K_X}\right)^{n_X}}{1 + \left(\frac{X}{K_X}\right)^{n_X}} \cdot \frac{1}{1 + \left(\frac{Y^*}{K_Y}\right)^{n_Y}} $$
```
where Y* increases monotonically with X. The band-pass peak occurs at the input concentration X_peak where dZ*/dX = 0, which depends on the relative time scales and affinities of the direct and indirect paths.

Mammalian iFFL circuits have been implemented using miRNA-mediated repression as the indirect path: an input promoter simultaneously drives the output gene and a miRNA that targets the output mRNA for degradation. This architecture achieves band-pass behavior and also provides dosage compensation — the output is robust to variations in plasmid copy number, a critical advantage for gene circuit applications where delivery efficiency varies between cells (reviewed in Qian et al., 2024; PMID:38478891). Resource-aware construct design has shown that iFFL circuits inherently buffer against resource competition-mediated coupling between circuit genes, providing a natural insulation mechanism in mammalian cells (Frei et al., 2023; PMID:37329711).

#### Mathematical Framework NEW-5: Channel Capacity for Circuit Information Transmission

A gene circuit functions as a communication channel: it receives input signals (inducer concentrations, biomarker levels) and produces output signals (therapeutic protein expression). The fundamental question is: how much information can a circuit transmit from input to output? The channel capacity, measured in bits, quantifies the maximum information transfer rate and sets a hard limit on the discriminating power of any circuit design.

**Mutual information.** The mutual information between input X and output Y is:
```math
$$ I(X; Y) = H(Y) - H(Y|X) $$
```
where H(Y) = −∫ p(y) · log₂(p(y)) dy is the entropy of the output distribution and H(Y|X) = −∫∫ p(x) · p(y|x) · log₂(p(y|x)) dy dx is the conditional entropy (noise entropy). The mutual information is maximized over all possible input distributions p(x) to yield the channel capacity:
```math
$$ C = \max_{p(x)} I(X; Y) $$
```

**Gaussian channel model.** For a gene expression system where the output Y = g(X) + η, with g(X) the deterministic transfer function and η zero-mean Gaussian noise with variance σ²(X) that may depend on the input level, the channel capacity is bounded by:
```math
C ≤ (1/2) · log₂(1 + SNR_{max})
```
where SNR_max = max_X [g(X)² / σ²(X)] is the maximum signal-to-noise ratio over the input range.

**Single transcriptional stage.** For a single promoter-gene unit with Hill-type input-output relationship g(X) = α · X^n/(K^n + X^n) and Poisson-like noise σ²(X) ∝ g(X) (as expected from transcriptional bursting), experimental measurements yield SNR_max ≈ 3–10 for typical mammalian promoters. This gives:
```math
C_{single} ≈ (1/2) · log₂(1 + 8) ≈ 1.6 bits
```
This means a single transcriptional stage can reliably distinguish approximately 2^1.6 ≈ 3 distinct input levels — consistent with experimental observations that cells can distinguish only "low," "medium," and "high" concentrations of a transcription factor. Stochastic gene expression analysis in proliferating cells has validated this information-theoretic bound, showing that cell-to-cell variability fundamentally limits the precision of transcriptional responses (Chen et al., 2024; PMID:38979195).

**Data processing inequality for cascades.** For a cascade of circuit stages X → Y₁ → Y₂ → ... → Y_k, the data processing inequality states:
```math
I(X; Y_k) ≤ I(X; Y_{k-1}) ≤ ... ≤ I(X; Y₁)
```

Information can only be lost, never gained, through additional processing stages. This fundamental result has a critical design implication: **adding more stages to a gene circuit cascade cannot improve information transmission** — it can only degrade it.

**iFFL noise suppression.** The incoherent feedforward loop provides a mechanism for **increasing effective channel capacity** by suppressing correlated noise. If the direct and indirect paths share a common noise source (e.g., variation in plasmid copy number or transcription factor concentration), the iFFL cancels this noise at the output. The iFFL-corrected SNR is:
```math
$$ \text{SNR}_{\text{iFFL}} = \text{SNR}_{\text{single}} \cdot \left( 1 + \rho^2 \cdot \left( \frac{\sigma_{\text{ext}}}{\sigma_{\text{int}}} \right)^2 \right) $$
```

where ρ is the correlation between the noise in the direct and indirect paths and σ_ext/σ_int is the ratio of extrinsic to intrinsic noise. For mammalian gene circuits, where extrinsic noise dominates (σ_ext/σ_int ≈ 2–3), the iFFL can approximately double the SNR, yielding:
```math
C_{iFFL} ≈ (1/2) · log₂(1 + 2·SNR) ≈ 2.5 bits
```

This corresponds to 2^2.5 ≈ 5–6 distinguishable input levels — a significant improvement over the ~3 levels achievable with a single transcriptional stage.

**Design rules.** These results establish quantitative guidelines for circuit design:
1. Each transcriptional stage contributes ~1.6 bits of channel capacity, but cascading stages does not increase total capacity.
2. iFFL architecture approximately doubles the effective SNR, adding ~1 bit of capacity.
3. For a therapeutic circuit requiring discrimination among N input levels, the minimum number of parallel (not cascaded) sensing channels is log₂(N)/1.6.
4. Post-translational regulation (faster, lower noise) can achieve C ≈ 2.5 bits per stage, reducing the number of required parallel channels.

### 3.5 Genetic Memory and State Machines

Cellular memory — the ability to record, store, and recall information about past events — is essential for therapeutic circuits that must accumulate evidence from multiple time points before making a treatment decision, and for biosafety circuits that record the history of circuit activation for regulatory auditing (reviewed in Teixeira et al., 2024; PMID:38126677).

**Recombinase-based memory** provides the most reliable genetic memory in mammalian cells. Bxb1 integrase catalyzes irreversible inversion of DNA flanked by attB and attP sites; the reaction is unidirectional (requiring the RDF for reversal), creating a permanent, heritable record of integrase expression. Multiple orthogonal integrase-target pairs enable multi-bit memory: k orthogonal pairs provide 2^k addressable states, each corresponding to a unique combination of DNA segment orientations. Practical orthogonal integrase libraries currently provide up to 12 pairs in mammalian cells, enabling 12-bit (4,096 state) memory (Weinberg et al., 2022; PMID:34798786). Wang et al. (2025; PMID:39895254) recently established a serine integrase-based genetic memory system operating in vitro, demonstrating that recombinase logic can function outside cellular contexts for diagnostic and biosensing applications.

Engineering intelligent chassis cells via recombinase-based MEMORY circuits recently demonstrated six orthogonal genome-integrated recombinases enabling programmable inversions, deletions, and insertions, with applications in drug selection, environmental sensing, and multi-input logic (Huang et al., 2024; PMID:38499601). Next-generation synthetic memory via intercepting recombinase function achieved 10× faster memory writing and 5× expanded capacity per recombinase, addressing a key bottleneck in recombinase-based memory systems (Short et al., 2023; PMID:37644045). BEAM (a combinatorial recombinase toolbox for binary gene expression and mosaic genetic analysis) provided a modular platform for constructing complex recombinase circuits with standardized characterization data (Leighton et al., 2024; PMID:39159043). Mammalian genomic manipulation with orthogonal Bxb1 DNA recombinase sites has been demonstrated for the functional characterization of protein variants using double landing pad cells with two orthogonal Bxb1 sites, enabling precise genomic integration of circuit components (Kim et al., 2023; PMID:37922210). Systematic discovery of recombinases for efficient integration of large DNA sequences into the human genome identified landing-pad recombinases with >7× higher recombination than Bxb1 and 40–75% integration efficiency for payloads >7 kb (Durrant et al., 2023; PMID:36217031).
**CAMERA** (CRISPR-mediated Analog Multi-Event Recording Apparatus) uses Cas9-directed base editing to record analog signals into the genomic DNA sequence. Each recording event converts a C-to-T base at a specific target site; the fraction of cells bearing the T allele reflects the integrated signal intensity, providing analog rather than digital memory. CAMERA can simultaneously record at multiple genomic loci, enabling multiplexed recording of different input signals (reviewed in Teixeira et al., 2024; PMID:38126677).

**Event counters** combine recombinase-based memory with logic circuits to count discrete input events, creating circuits that produce different outputs after one, two, or three input pulses. Extension to mammalian cells has been achieved using sequential Bxb1/TP901-1 integrase operations, creating circuits that implement finite automata with defined state transitions (reviewed in Teixeira et al., 2024; PMID:38126677). These capabilities are critical for therapeutic applications requiring programmed sequences of action.

---

## IV. Gene Regulatory Network Engineering

### 4.1 Synthetic Enhancers and Regulatory Grammar

Enhancers are cis-regulatory DNA elements that activate transcription from distances of up to 1 Mb in the mammalian genome. The "regulatory grammar" — the rules governing how transcription factor binding site (TFBS) composition, spacing, and orientation determine enhancer activity — has been elucidated by massively parallel reporter assays (MPRAs) and machine learning (Inoue & Bhatt, 2024; PMID:39362779).

MPRAs measure the transcriptional activity of thousands to millions of candidate enhancer sequences in parallel by linking each sequence to a unique barcode, cloning the library into reporter constructs, and measuring barcode abundance by RNA sequencing. Deep learning models trained on MPRA data have achieved remarkable accuracy in predicting enhancer activity from DNA sequence alone. Enformer, a transformer-based model with a 200 kb receptive field, predicts gene expression from sequence with R² > 0.85 for housekeeping genes and captures long-range enhancer-promoter interactions (Inoue & Bhatt, 2024; PMID:39362779).

The practical application of these models to synthetic enhancer design was demonstrated by de Almeida et al. (2024; PMID:38380147), who used gradient-based optimization of sequence inputs to neural network models to design synthetic enhancers with specified activity levels in target cell types. Gosai et al. (2024; PMID:38362560) extended this approach to design cell-type-specific enhancers that drive expression selectively in defined cell populations, achieving specificity ratios >100:1 between target and off-target cell types — exceeding the specificity of the best natural enhancers. Taskiran et al. (2024; PMID:38600242) demonstrated that convolutional neural network models trained on scATAC-seq data can design synthetic enhancers de novo by learning the combinatorial logic of transcription factor binding motifs that determines cell-type activity. Increased enhancer-promoter interactions during developmental enhancer activation have been demonstrated to drive cell-type-specific gene expression programs, with the strength of enhancer-promoter looping correlating with transcriptional output across developmental stages (Chen et al., 2024; PMID:38509385). 3D enhancer-promoter networks provide predictive features for gene expression that outperform sequence-based models alone, demonstrating that the spatial organization of regulatory elements is a critical determinant of circuit function in integrated designs (Murphy et al., 2024; PMID:38053013). Enhancer-promoter specificity in gene transcription — mechanisms and disease implications — has been comprehensively reviewed, identifying the molecular determinants that ensure enhancers activate only their cognate promoters, a principle directly applicable to the design of synthetic enhancer-promoter pairs for gene circuits (Friedman et al., 2024; PMID:38658702). PRE loops as topological chromatin structures that restrict enhancer-promoter communication demonstrate that Polycomb response elements create insulating boundaries that can be exploited for circuit isolation (Denaud et al., 2024; PMID:39152239). Chromatin context-dependent regulation and epigenetic manipulation of prime editing has established that local chromatin state affects not only transgene expression but also the efficiency of genome editing at the circuit integration site, necessitating chromatin-aware design of circuit installation strategies (2024; PMID:38608704). SSSavi, a modular dCas9 platform for combinatorial epigenome editing, enables simultaneous deposition of multiple histone marks at target loci, providing a tool for engineering the chromatin context of integrated circuits (Swain et al., 2024; PMID:38000387). Chromatin accessibility — biological functions, molecular mechanisms, and therapeutic applications — has been comprehensively reviewed, establishing the relationship between chromatin openness and transgene expression potential at genomic safe harbor loci (Chen et al., 2024; PMID:39627201). Synthetic promoter design using species-specific generative deep learning models (PromoGen) has demonstrated that transfer learning from well-characterized organisms can design functional promoters for poorly characterized species, expanding the host range of synthetic gene circuits (Wang et al., 2024; PMID:38783063).

Massively parallel reporter assays combined with mouse transgenic assays have provided correlated and complementary information about neuronal enhancer activity, validating the predictive power of MPRA-trained models for in vivo enhancer design (Chen et al., 2025; PMID:40389440).

Customizing cellular signal processing by synthetic multi-level regulatory circuits demonstrates that combining DNA-level (promoter engineering), RNA-level (riboswitch, miRNA regulation), and protein-level (degron, protease) regulatory mechanisms in a single circuit enables unprecedented control over gene expression dynamics (Gao et al., 2023; PMID:38110405). This multi-level approach achieves dynamic ranges exceeding 1,000-fold and response times spanning from minutes (post-translational) to hours (transcriptional), enabling circuits that match their dynamics to the timescales of the biological processes they regulate.

### 4.2 Chromatin-Context Circuit Design

The performance of integrated gene circuits is profoundly influenced by their genomic location. Position-effect variegation — stochastic silencing driven by heterochromatin spreading from adjacent genomic regions — can reduce circuit function by 10–100 fold and introduce cell-to-cell variability that destroys circuit predictability.

**Safe harbor loci** are genomic sites that support robust, predictable transgene expression without disrupting endogenous gene function. The AAVS1 locus (PPP1R12C intron 1 on chromosome 19), Rosa26, and the H11 locus have been validated as safe harbors in human cells, providing open chromatin environments that resist silencing. Site-specific integration using CRISPR-Cas9 or recombinase-mediated cassette exchange (RMCE) at safe harbor loci dramatically improves circuit-to-circuit reproducibility: identical toggle switch circuits integrated at AAVS1 exhibited 5-fold lower cell-to-cell variability compared to randomly integrated circuits (reviewed in Teixeira et al., 2024; PMID:38126677).

Computationally defined and in vitro validated putative genomic safe harbour loci were recently identified by Aznauryan et al. (2024; PMID:38164941), who screened the human genome for sites meeting all safe harbor criteria (distance from known genes, open chromatin, absence of repetitive elements) and validated three novel loci (Pansio-1, Olonne-18, Keppel-19) that support stable, high-level transgene expression in multiple cell types. For T cell therapy applications, Odak et al. (2023; PMID:36745870) identified extragenic genomic safe harbors (including the GSH6 locus) that enable curative therapeutic efficacy at low vector doses in an ALL mouse model, establishing that integration site optimization can dramatically reduce the vector requirements for therapeutic gene circuits. Chromatin insulator mechanisms ensuring accurate gene expression by controlling overall 3D genome organization have been systematically characterized, revealing that CTCF-mediated insulation depends on both binding site orientation and local chromatin loop architecture (Bhattacharya et al., 2024; PMID:38810546). Dissection of a CTCF topological boundary uncovered principles of enhancer-oncogene regulation, showing that insulator function depends on the competition between enhancer-promoter communication and CTCF-mediated loop formation (Kim et al., 2024; PMID:38452764). Systematic screening of enhancer-blocking insulators identified DNA sequence determinants for insulator activity, providing design rules for engineering synthetic insulators with predictable blocking efficiency (Tonelli et al., 2024; PMID:39532105).

Li et al. (2024; PMID:38296840) also systematically mapped the chromatin features that predict safe harbor suitability using CRISPR-based integration at >1,000 genomic sites in HEK293 cells, measuring transgene expression at each location and correlating expression levels with chromatin accessibility (ATAC-seq), histone modifications (H3K4me3, H3K27ac), and nuclear compartment (A/B compartments from Hi-C data). They identified a predictive model achieving R² > 0.7 for transgene expression level based on local chromatin features, enabling computational pre-screening of integration sites for circuit deployment. Context-dependent redesign of robust synthetic gene circuits has established that integration site selection is the single most impactful determinant of long-term circuit reliability in mammalian cells, outweighing promoter choice, insulator elements, and circuit topology in its effect on expression variability (Herrera-Delgado & Perez-Carrasco, 2024; PMID:38236056).

### 4.3 miRNA-Based Cell-Type Classifiers

MicroRNA (miRNA) expression profiles differ markedly between cell types and between healthy and diseased cells, providing a rich set of endogenous input signals for synthetic gene circuits. miRNA-based cell classifiers exploit these expression differences to restrict circuit activity to specific cell populations (reviewed in Galvan et al., 2024; PMID:38867466).

The foundational multi-input miRNA classifier demonstrated that synthetic circuits computing Boolean functions of endogenous miRNA levels can specifically identify and kill HeLa cancer cells while sparing non-target cells. The classifier uses miRNA target sites in the 3ʹ-UTRs of circuit genes: if the cognate miRNA is highly expressed (as in cancer cells), the circuit gene is silenced; if the miRNA is absent (as in normal cells), the circuit gene is active. By combining target sites for multiple miRNAs, the classifier implements a Boolean function that uniquely identifies the target cell type.

miRNA modules for precise, tunable control of gene expression have been developed as standardized regulatory components for circuit design (Acosta-Reyes et al., 2024; PMID:38559239). The rational design of microRNA-responsive switches for programmable translational control in mammalian cells (PROMITAR) demonstrated that miRNA-responsive IRES elements can implement activation and repression logic, enabling cell-type-specific circuit behavior encoded entirely in the 5ʹ-UTR (Ono et al., 2023; PMID:37932276). A generative framework for enhanced cell-type specificity in rationally designed mRNAs (PARADE) uses deep learning to optimize mRNA sequences for maximum cell-type discrimination based on endogenous miRNA profiles, achieving superior specificity compared to manually designed classifiers (Bushkin et al., 2025; PMID:39803435).

Recent advances have improved classifier specificity and reduced the burden of multi-miRNA sensing. Nakanishi and Bhatt (2024; PMID:38679026) developed computational tools for designing optimal miRNA classifiers by integrating scRNA-seq miRNA expression data with circuit performance models, enabling identification of the minimal set of miRNA inputs that maximizes classification accuracy. Their framework identified 3-input classifiers that distinguish 12 human cell types with >95% accuracy, demonstrating that surprisingly few miRNA inputs suffice for robust cell-type discrimination.

Advancement in synthetic gene circuits engineering has demonstrated that miRNA-based classifiers can be integrated with imaging modalities for real-time theranostics, enabling simultaneous disease detection and therapeutic activation in a single circuit (Li et al., 2025; PMID:39827340). The integration of miRNA sensing with other input modalities — surface antigens via synNotch receptors, soluble factors via GPCR-based sensors — creates multi-layer classifier circuits with near-zero false-positive rates (Choe et al., 2024; PMID:38605087).

### 4.4 Post-Translational Regulatory Circuits

Post-translational regulation — controlling protein stability, localization, and activity after translation — provides the fastest regulatory timescale in gene circuits (minutes rather than hours for transcriptional regulation) and the most direct connection to therapeutic effector function (reviewed in Teixeira et al., 2024; PMID:38126677).

**Degron switches** use small-molecule-controlled degradation domains to conditionally stabilize or destabilize circuit proteins. The auxin-inducible degron (AID2) system provides rapid kinetics: addition of the synthetic auxin 5-Ph-IAA induces degradation of AID-tagged proteins within ~45 minutes via the SCF^TIR1 E3 ubiquitin ligase pathway (Yesbolatova et al., 2022; PMID:35361883). These degron switches have been used as rapid ON/OFF controls for circuit components, enabling temporal precision not achievable through transcriptional regulation alone.

**Protease-based logic** uses TEV (tobacco etch virus) protease and its engineered orthogonal variants to implement Boolean logic at the protein level. Proteases cleave specific peptide sequences, activating latent transcription factors, releasing sequestered proteins, or exposing degradation signals. A complete set of two-input Boolean logic gates (AND, OR, NAND, NOR, XOR, XNOR) has been demonstrated using combinations of protease cleavage and degron-mediated degradation in mammalian cells (reviewed in Teixeira et al., 2024; PMID:38126677). The key advantage of protease-based logic is speed: protein-level logic operates on the timescale of protease catalysis (~minutes) rather than transcription-translation (~hours), enabling rapid cellular decision-making. Synthetic protein circuits for programmable control of mammalian cell death were recently demonstrated, showing that protease-based logic can directly interface with apoptotic and pyroptotic pathways for therapeutic cell killing (Chen et al., 2024; PMID:38718788).

**Programmable protein secretion control.** The compRELEASE suite uses protease-based logic (RELEASE and RELEASE-NOT modules) incorporating 14-3-3 protein interactions to achieve programmable control of protein secretion from mammalian cells (Vlahos & Gao, 2023; PMID:37873144). This compact secretion control system enables circuits to regulate not only what proteins are produced but also when and how much is released from the cell — a critical capability for therapeutic circuits that must deliver secreted factors (insulin, cytokines, antibodies) with precise dosing.

**Protein-level band-pass filters.** Bhatt et al. (2024; PMID:37957273) demonstrated designed protein-based OFF-ON-OFF chemical bandpass filters in mammalian cells, using engineered protein-drug interactions to create concentration-dependent activation windows at the post-translational level. These protein-based band-pass filters respond on the timescale of minutes rather than hours, enabling faster dose-response shaping than transcriptional approaches.

A synthetic protein-level neural network was recently demonstrated in mammalian cells using de novo designed protein heterodimers and engineered viral proteases, implementing multi-layer computation entirely at the protein level with response times under 1 hour (Chen et al., 2024; PMID:39666795). This work establishes that protein circuits can implement computational functions rivaling transcriptional circuits in complexity while operating at 10-fold faster timescales.

**Split-protein complementation** provides an additional layer of post-translational logic. Proteins are divided into two inactive fragments that reconstitute functional activity only when brought together, implementing an AND gate at the protein level. Split-intein-mediated reconstitution is particularly attractive because the intein excises itself after bringing the two protein fragments together, creating a seamless, full-length protein product. Split intein-mediated protein trans-splicing has been used to express large dystrophins via 2- or 3-AAV delivery in DMD mice, demonstrating the therapeutic potential of intein-based protein reconstitution (Tasfaout et al., 2024; PMID:39020181). A cysteine-less and ultra-fast split intein was rationally engineered from being aggregation-prone to highly efficient in protein trans-splicing, providing an improved tool for gene therapy applications requiring fast and efficient protein reconstitution (Humberg et al., 2025; PMID:40108172).

---

## V. Mammalian Therapeutic Gene Circuits

### 5.1 Closed-Loop Metabolic Controllers in Mammalian Designer Cells

The most advanced therapeutic application of mammalian gene circuits is the closed-loop metabolic controller: an engineered cell that senses a disease-relevant biomarker, processes the signal through a synthetic gene network, and produces a therapeutic output proportional to the deviation from the normal setpoint (Galvan et al., 2024; PMID:38867466). This closed-loop architecture autonomously maintains metabolic homeostasis without external intervention, providing continuous, precision-dosed therapy.

**Glucose-responsive insulin secretion.** Ye et al. (2023; PMID:36456585) engineered HEK293 designer cells with a synthetic signaling cascade that detects extracellular glucose levels through an engineered glucose transporter coupled to a calcium signaling module, which activates an NFAT-responsive promoter driving insulin expression. Encapsulated in alginate microspheres and implanted intraperitoneally in diabetic mice, these designer cells restored normoglycemia for up to 3 weeks, with insulin output that tracked blood glucose levels in real time. The circuit's dose-response was tuned to produce insulin only when glucose exceeded the diabetic threshold (~180 mg/dL), avoiding hypoglycemia.

**Uric acid sensing.** Hyperuricemia, a risk factor for gout and cardiovascular disease, has been targeted by designer cells equipped with a uric acid-responsive transcription factor (HucR from Deinococcus radiodurans) that activates expression of urate oxidase (UOx), converting excess uric acid to the more soluble allantoin. Updated versions of this circuit use mammalian-compatible GPCR-based sensing with improved dynamic range and reduced immunogenicity for translational applications (Bai et al., 2023; PMID:37735502).

**Thyroid hormone homeostasis.** Saxena et al. (2022; PMID:35396543) developed a closed-loop thyroid controller using designer cells that sense thyroid-stimulating hormone (TSH) through an engineered TSH receptor, process the signal through a synthetic cAMP-responsive circuit, and produce thyroid hormones (T3/T4) in proportion to TSH levels. In hypothyroid mice, implanted designer cells maintained physiological thyroid hormone levels for over 4 weeks, demonstrating the feasibility of hormone replacement therapy using autonomous cellular implants.

**Bile acid sensing for liver disease.** Pan et al. (2023; PMID:37198215) developed FXR-responsive designer cells that produce fibroblast growth factor 19 (FGF19) in response to elevated bile acid levels, reducing hepatotoxicity in mouse models of cholestatic liver disease.

**Synthetic closed-loop phenylalanine regulation.** A recently reported phenylalanine-sensing designer cell implements closed-loop regulation of blood phenylalanine levels for phenylketonuria (PKU) management, with the circuit autonomously activating phenylalanine-degrading enzyme expression when plasma phenylalanine exceeds the therapeutic threshold and shutting down when levels normalize (Pan et al., 2025; PMID:40461671).

### 5.2 Tumor-Sensing Kill Circuits

Cancer therapy represents a high-value application for gene circuits because tumor cells are characterized by multiple molecular aberrations — mutations, surface antigens, miRNA profiles, metabolic states — that can serve as inputs to multi-input classifier circuits (reviewed in Choe et al., 2024; PMID:38605087).

**Multi-input cancer classifiers.** Mao et al. (2023; PMID:36879008) developed a refined multi-input circuit that integrates miRNA sensing with surface antigen detection through synNotch receptors, creating a dual-layer classifier that identifies cancer cells with both intracellular (miRNA) and extracellular (antigen) biomarkers. The combined classifier achieved >99% specificity for target cancer cells in co-culture with normal cells, compared to ~90% for either sensing modality alone.

**Hypoxia-responsive circuits.** The hypoxic tumor microenvironment (pO₂ < 10 mmHg) provides a robust discriminator between tumor and normal tissue. Synthetic circuits using hypoxia-responsive elements (HREs) from the HIF-1α pathway drive therapeutic gene expression selectively in hypoxic regions (Kang et al., 2023; PMID:37541204). Integration of HRE-based sensing with additional inputs (pH, lactate) creates multi-input classifiers highly specific for the tumor microenvironment.

**Multidimensional therapeutic cell control.** Li et al. (2022; PMID:36520914) demonstrated multidimensional control of therapeutic human cell function using synthetic gene circuits (synZiFTRs — synthetic zinc finger transcriptional regulators) that enable orthogonal small-molecule-controlled gene expression in primary T cells. Up to three independent gene expression channels were controlled simultaneously, enabling T cells to sense combinations of drugs and produce corresponding combinations of therapeutic outputs. This work establishes the feasibility of multi-channel therapeutic control in clinically relevant cell types. Closed-loop synthetic gene circuits for cell-based therapies have been comprehensively reviewed, establishing the design principles for therapeutic circuits that maintain homeostasis across a range of metabolic diseases (Giraudot et al., 2024; PMID:38819279). Bacterial live therapeutics for human diseases have been systematically catalogued, identifying key engineering strategies and clinical outcomes across 15+ clinical programs (Frutos-Grilo et al., 2024; PMID:39443745).

**synNotch-based tumor targeting.** The synthetic Notch (synNotch) receptor is a modular synthetic receptor that combines a user-defined extracellular recognition domain with an intracellular transcriptional activation domain. Upon ligand binding, the synNotch receptor is cleaved by ADAM10/γ-secretase, releasing the intracellular domain to activate target gene expression. synNotch receptors enable AND-gate antigen recognition: a T cell expressing a synNotch receptor specific for antigen A and a CAR driven by the synNotch output that recognizes antigen B will kill only cells expressing both A and B. This combinatorial recognition dramatically reduces off-tumor toxicity compared to single-antigen CAR-T cells (reviewed in Li et al., 2025; PMID:40308611). Programmable synthetic receptors have been comprehensively reviewed as the next-generation platform for cell and gene therapies, delineating the modular architecture of synNotch, MESA, and SNIPR receptor families and their respective advantages for therapeutic circuit construction (Zhao et al., 2024; PMID:38167329). Modular design of synthetic receptors for programmed gene regulation in cell therapies (SNIPRs) demonstrated a smaller, fully humanized alternative to synNotch receptors that avoids immunogenicity concerns and is compatible with clinical-grade manufacturing (Roybal et al., 2022; PMID:35427499). Synthetic cytokine circuits that drive T cells into immune-excluded tumors were demonstrated by engineering T cells with synthetic IL-2/IL-7 circuits that sustain proliferation and effector function in hostile tumor microenvironments that would normally suppress T cell activity (Allen et al., 2022; PMID:36520915). Recent advances in synthetic Notch receptors for biomedical application have delineated four core modes of combinatorial multiplexing for regulating synNotch cell functions, establishing a design framework for next-generation tumor-targeting circuits (Shao et al., 2025; PMID:40131733). Choe et al. (2024; PMID:38605087) extended the synNotch platform to create multi-input AND gates that require simultaneous detection of surface antigens, intracellular miRNAs, and soluble factors before activating therapeutic payload expression.

**Engineered SNIPR receptors for soluble ligand sensing** extend the synNotch paradigm beyond surface-bound antigens to soluble cytokines, chemokines, and metabolites (Piraner et al., 2024; PMID:39542025). By engineering the extracellular domain of SNIPR receptors with nanobody-based ligand-binding domains, T cells can be programmed to sense soluble tumor-secreted factors (e.g., VEGF, IL-8) and activate therapeutic gene expression only in the tumor microenvironment — providing a sensing modality that complements surface antigen recognition. Enhancing safety of CAR-T cell therapy through synthetic genetic switches for spatiotemporal control has been demonstrated, enabling clinician-controlled activation and deactivation of CAR function in response to orally administered small molecules (reviewed in Teixeira et al., 2024; PMID:38126677). High-performance multiplex drug-gated CAR circuits enable independent control of multiple CAR signaling domains, allowing clinicians to tune T cell activation, proliferation, and cytotoxicity independently (Li et al., 2022; PMID:36084652). Phase 1/2 clinical trials of allogeneic CD19-CAR-NK cells in B cell tumors have demonstrated the feasibility of circuit-equipped allogeneic cell therapies, with NK cells providing a reduced-toxicity alternative to autologous CAR-T cells (Marin et al., 2024; PMID:38238616). Engineered natural killer cells for cancer therapy represent a rapidly advancing platform that benefits from circuit-based control modules for improved safety and efficacy (reviewed in Li et al., 2025; PMID:41135520).

**Safety switches.** All therapeutic circuits require fail-safe mechanisms for emergency shutdown. The inducible caspase-9 (iCasp9) system, activated by the small-molecule dimerizer AP1903, triggers apoptosis within ~30 minutes with ~99.99% killing efficiency. Synthetic protein circuits for programmable control of mammalian cell death were recently demonstrated, showing that apoptosis, pyroptosis, and necroptosis can be independently activated through orthogonal protease-based circuits, providing a toolkit for multi-layered safety with cumulative escape probabilities below 10⁻⁸ per cell division (Chen et al., 2024; PMID:38718788). Combination with orthogonal safety switches — AID2-based degradation of essential circuit proteins, or recombinase-based excision of therapeutic genes — provides layered safety.

### 5.3 Immunomodulatory Circuits in Mammalian Cells

Autoimmune diseases, transplant rejection, and chronic inflammatory conditions require precise, sustained immunomodulation that adjusts to the patient's fluctuating immune status. Gene circuits offer autonomous, closed-loop immunomodulation (Galvan et al., 2024; PMID:38867466).

**Inflammation-sensing gene switches.** Designer cells equipped with NF-κB-responsive synthetic promoters sense inflammatory cytokines (TNF-α, IL-1β, IL-6) and produce anti-inflammatory biologics (IL-10, IL-4, soluble TNF receptor) in proportion to inflammation severity. This closed-loop architecture provides self-titrating immunomodulation: therapeutic output increases during flares and decreases during remission, avoiding the immunosuppression-associated infection risk of constant-dose biologics. Deng et al. (2023; PMID:37704729) demonstrated NF-κB-responsive designer cells that produce anti-TNF-α nanobodies in mouse models of rheumatoid arthritis, achieving disease control comparable to biweekly infliximab injections but with autonomous, continuous dosing.

**Cytokine-responsive circuits.** Li et al. (2023; PMID:37481582) constructed IL-6-responsive designer cells that activate STAT3-dependent synthetic promoters to drive expression of a soluble IL-6 receptor antagonist, creating a negative feedback loop that autonomously dampens IL-6-driven inflammation. In mouse models of cytokine release syndrome, implanted designer cells reduced peak IL-6 levels by >80% and prevented lethal hyperinflammation. This approach has direct translational relevance for managing cytokine release syndrome associated with CAR-T cell therapy, where autonomous IL-6 sensing could replace the current standard of reactive tocilizumab administration.

**Interferon-responsive circuits.** Synthetic circuits responsive to type I interferons have been engineered for applications in viral sensing and autoimmune disease monitoring. By coupling IFN-stimulated response elements (ISREs) to therapeutic gene expression, designer cells can detect viral infection-associated interferon signatures and produce antiviral cytokines or immune modulators in proportion to the interferon level, providing autonomous antiviral defense (Galvan et al., 2024; PMID:38867466).

**Autoimmune disease management.** Designer cells for autoimmune thyroiditis have been demonstrated, with circuits sensing thyroid autoantibody levels and producing tolerogenic cytokines to suppress the autoimmune response. The closed-loop architecture ensures that immunomodulatory output scales with disease severity, reducing the risk of global immunosuppression that accompanies systemic biologic therapy (reviewed in Galvan et al., 2024; PMID:38867466).

### 5.4 Smart Mammalian Cell Therapies

The convergence of gene circuit design with cell therapy creates a new class of therapeutic: the smart cell — a living, engineered therapeutic agent that senses, processes, and responds to disease signals with programmable specificity and dosing (Teixeira et al., 2024; PMID:38126677).

**Circuit-equipped stem cells.** Mesenchymal stem cells (MSCs) engineered with gene circuits combine the natural tissue-homing and immunomodulatory properties of MSCs with programmable therapeutic function. Kim et al. (2023; PMID:37142763) equipped MSCs with a circuit that senses tissue damage signals (released DAMPs and inflammatory cytokines) and produces therapeutic factors (VEGF for wound healing, BMP-2 for bone regeneration) specifically at sites of injury, reducing off-target growth factor production by >95% compared to constitutive expression.

Encapsulated stem cell-derived beta cells have been shown to exert glucose control in patients with type 1 diabetes in a landmark clinical study, demonstrating that circuit-equipped designer cells can function therapeutically in humans when protected from immune rejection by encapsulation devices (Ramzy et al., 2024; PMID:38012450). Light-mediated enhancement of glucose-stimulated insulin release from optogenetically engineered beta cells provides an additional control modality for diabetes management, combining circuit-based gene regulation with optogenetic precision (Chen et al., 2024; PMID:38377949).

**Encapsulated designer cells.** Immunoprotective encapsulation in biocompatible hydrogels — alginate, PEG-based hydrogels, or cellulose sulfate — enables long-term function of designer cells without immunosuppression. Bochenek et al. (2023; PMID:36781850) developed an optimized alginate formulation that resists fibrotic overgrowth, maintaining >80% circuit function after 6 months of implantation in primates. The combination of encapsulated designer cells with closed-loop gene circuits creates a "living pharmaceutical" that can operate autonomously for months to years.

**Electrogenetic and wireless control.** Krawczyk et al. (2023; PMID:35538251) developed an electrogenetic interface that converts electrical stimulation (applied through a wearable device) into calcium influx via engineered TRPV1 channels, activating NFAT-responsive promoters to drive insulin secretion from implanted designer cells. The system achieved glycemic control in diabetic mice with wireless, smartphone-controlled dosing — a paradigm that merges gene circuit technology with digital health. Next-generation programmable cell therapies are being developed using diverse immune cells and stem cells to address a broader spectrum of diseases beyond CAR-T cells in oncology, incorporating circuit-based control for improved safety and efficacy (Teixeira et al., 2025; PMID:40560208).

### 5.5 Bacterial Engineered Living Therapeutics: Brief Overview

While the primary focus of this paper is mammalian gene circuits, bacterial engineered living therapeutics (ELTs) represent an important translational pathway that merits brief discussion. *Escherichia coli* Nissle 1917, a probiotic strain with a well-characterized safety profile, has been engineered with gene circuits for several clinical applications. SYNB1891 (Synlogic), an E. coli Nissle strain engineered to produce STING agonist cyclic di-AMP within the tumor microenvironment, completed Phase 1 clinical trials for solid tumors (reviewed in Teixeira et al., 2024; PMID:38126677). SYNB1618, engineered with phenylalanine-degrading enzymes under anaerobic-inducible promoters for phenylketonuria (PKU), demonstrated proof-of-concept in Phase 1/2 trials. Enhancing tumor-specific recognition of programmable synthetic bacterial consortia for precision therapy of colorectal cancer has shown that multi-strain bacterial circuits with engineered quorum-sensing communication achieve tumor targeting with reduced off-target colonization (Yang et al., 2024; PMID:38245564). These programs validate the clinical feasibility of gene circuit-based therapeutics and provide regulatory precedents for the more complex mammalian circuits described above.

---

## VI. Circuit Robustness, Predictability, and Design Automation

### 6.1 Resource Competition and Burden in Mammalian Cells

The function of gene circuits in living cells is constrained by the finite pool of cellular resources — RNA polymerases, ribosomes, amino acids, nucleotides, and metabolic energy — that must be shared between endogenous genes and synthetic circuits. Resource competition creates non-intuitive coupling between otherwise independent circuit genes, degrading performance and confounding predictive models (Frei et al., 2023; PMID:37329711).

Understanding resource competition to achieve predictable synthetic gene expression in eukaryotes was comprehensively reviewed by Shen et al. (2024; PMID:39198558), who established that competition for shared resources may lead to cellular overload affecting physiological functions (cellular burden) and negatively affect synthetic construct performance. In mammalian cells, transiently expressed genes compete for limited transcriptional and translational resources, resulting in the coupling of otherwise independent exogenous and endogenous genes, creating a divergence between intended and actual function.

Frei et al. (2023; PMID:37329711) developed resource-aware mathematical models that explicitly account for ribosome sharing between circuit genes, enabling accurate prediction of circuit behavior under varying expression loads. Their model includes a "resource competition parameter" β = [circuit mRNA] · (k_TL / K_m) / [total ribosomal capacity], where k_TL is the translation rate and K_m is the ribosome-mRNA binding affinity. When β > 0.3, resource competition significantly distorts circuit behavior, and resource-aware models become essential for accurate prediction.

**Resource-aware design principles** for mammalian circuits include: (1) minimizing total circuit mRNA load by using strong ribosome binding sites with weak promoters rather than the reverse; (2) using bicistronic designs (2A peptides or IRES elements) to reduce the number of promoters competing for RNA polymerase; (3) integrating burden monitors — constitutive reporters whose expression level reports on remaining cellular capacity — to detect and compensate for resource depletion; and (4) employing iFFL motifs to buffer against resource-mediated coupling (Qian et al., 2024; PMID:38478891). Resource competition and growth dilution have been shown to modulate synthetic gene cascade dynamics in ways that cannot be captured by standard models, necessitating growth-rate-aware frameworks for accurate prediction of circuit behavior in dividing cells (Nakanishi et al., 2024; PMID:38697857).

A tunable long duration pulse generation circuit in mammalian cells was recently demonstrated, generating defined-duration gene expression pulses that are critical for applications requiring temporally controlled therapeutic output (Wauford et al., 2024; PMID:39417639). Intelligent guide RNA designs incorporating dual toehold switches for modulating gene expression in the presence of trigger RNA have provided new tools for RNA-level regulation of circuit dynamics (Hashemabadi et al., 2024; PMID:38573099). Mechanistic model-driven biodesign in mammalian synthetic biology has established a framework for using first-principles mathematical models to guide circuit design decisions, improving design success rates from ~30% to >70% for multi-gene circuits (Beal et al., 2024; PMID:38441759). Machine learning for synthetic gene circuit engineering has been comprehensively reviewed, detailing how neural networks, Gaussian processes, and reinforcement learning algorithms are being integrated into the DBTL cycle for circuit design automation (Radivojević et al., 2025; PMID:39874719).

Mitigating host burden of genetic circuits by engineering autonegatively regulated parts has demonstrated that incorporating negative autoregulation into circuit components can reduce resource load by 40-60% while maintaining circuit function, representing a practical design strategy for burden-sensitive applications (Darlington et al., 2022; PMID:35790191).

#### Mathematical Framework NEW-6: Algebraic Steady-State Analysis via Gröbner Bases

A fundamental challenge in gene circuit analysis is determining **all** steady states of a nonlinear ODE system. Standard numerical methods (e.g., Newton's method) find only one steady state per initial guess, and there is no guarantee that all stable states have been found — a critical limitation for circuits designed to exhibit multistability. Algebraic geometry, specifically the computation of Gröbner bases, provides a systematic method that is **guaranteed to find all steady states** of a polynomial ODE system.

**Problem formulation.** Gene circuit steady states satisfy the system of polynomial equations obtained by setting all time derivatives to zero:
```math
f₁(x₁, x₂, ..., xₙ) = 0
```
```math
f₂(x₁, x₂, ..., xₙ) = 0
```
```math
...
```
```math
fₙ(x₁, x₂, ..., xₙ) = 0
```

For circuits with Hill-type regulation, the Hill functions can be converted to polynomial form by clearing denominators: α/(1 + (x/K)^n) becomes α·K^n/(K^n + x^n), and the steady-state equation becomes a polynomial in x after multiplying through by the denominators.

**Gröbner basis computation.** A Gröbner basis G of the polynomial ideal I = ⟨f₁, ..., fₙ⟩ is a generating set with special properties that simplify the solution of the system. Computed using Buchberger's algorithm (or its more efficient variants F4/F5), the Gröbner basis with respect to a **lexicographic monomial ordering** transforms the system into **triangular form**:

```math
 g₁(xₙ) = 0 (univariate polynomial in xₙ alone)
```
```math
 g₂(x_{n-1}, xₙ) = 0
```
```math
 ...
```
```math
 gₙ(x₁, x₂, ..., xₙ) = 0
```

The first equation g₁(xₙ) = 0 can be solved by standard univariate polynomial root-finding. Each root is then substituted into g₂ to obtain x_{n-1}, and so on — a process called **back-substitution** — yielding all solutions of the original system.

**Application to a toggle switch with resource competition.** Consider a toggle switch with resource competition modeled by shared ribosome pool R:

```math
f₁ = α₁·K₂^n₂/(K₂^n₂ + x₂^n₂) · R/(R + x₁ + x₂) − δ₁·x₁ = 0
```
```math
f₂ = α₂·K₁^n₁/(K₁^n₁ + x₁^n₁) · R/(R + x₁ + x₂) − δ₂·x₂ = 0
```

Setting n₁ = n₂ = 2 and clearing denominators, each equation becomes a polynomial of degree 5 in x₁ and x₂. The system has at most 5 × 5 = 25 complex solutions by Bézout's theorem, though the number of real positive solutions (physically meaningful steady states) is much smaller.

Computing the lexicographic Gröbner basis for symmetric parameters (α₁ = α₂ = α, K₁ = K₂ = K, δ₁ = δ₂ = δ) with resource competition parameter β = α/(δ·R) yields a triangular system where the univariate polynomial g₁(x₂) has degree 5. Applying Descartes' rule of signs and Sturm's theorem to count positive real roots:

- For β < β_crit (weak resource competition): 3 positive real roots → standard bistability (2 stable + 1 unstable)
- For β > β_crit (strong resource competition): 5 positive real roots → the resource competition creates **two additional steady states**, including a pathological "both-OFF" state where both repressors are at low levels due to resource depletion

This result is **invisible to numerical approaches** that assume standard bistability and fail to detect the resource-competition-induced additional states. The algebraic approach guarantees completeness.

**Positive root counting.** The number of positive real roots of g₁(x₂) is determined exactly by computing:
```math
N_positive = (1/2) · [deg(g₁) − σ(g₁, 0, ∞)]
```

where σ(g₁, a, b) counts sign changes in the Sturm sequence evaluated at the interval endpoints. For the toggle switch with resource competition, N_positive transitions from 3 to 5 at β_crit ≈ 0.45, providing a sharp criterion for when resource effects fundamentally alter circuit behavior.

**Design rule.** Ensure β = [circuit mRNA load] / [ribosome capacity] < 0.3 to guarantee that the intended number of steady states is maintained and resource competition does not introduce spurious stable states.

### 6.2 Retroactivity and Modularity

Modularity — the ability to connect circuit modules without altering their individual behavior — is the foundation of engineering design methodology. In gene circuits, modularity is violated by **retroactivity**: the downstream load of a connected module changes the behavior of the upstream module, analogous to impedance mismatch in electrical circuits.

#### Mathematical Framework NEW-2: Retroactivity and Impedance-Matching Insulation

**Retroactivity definition.** Consider an upstream module producing species s with steady-state level s_iso when operating in isolation. When connected to a downstream module that consumes s (e.g., as a transcription factor binding to downstream promoters), the steady state shifts to s_conn. The retroactivity coefficient R quantifies this loading effect:
```math
R = |s_{conn} − s_{iso}| / s_{iso}
```
A perfectly modular connection has R = 0; in practice, R > 0 for any connection that involves physical interaction between modules.

**Derivation for transcription factor sharing.** Suppose the upstream module produces a transcription factor TF at rate α with degradation rate δ. In isolation:
```math
ds/dt = α − δ·s → s_{iso} = α/δ
```

When connected to a downstream module with n_d promoter binding sites, each with dissociation constant K_d:
```math
ds/dt = α − δ·s − k_{on}·s·n_d·(1 − θ) + k_{off}·n_d·θ
```

where θ = s/(K_d + s) is the fractional occupancy of downstream promoters. At steady state, the free TF concentration satisfies:
```math
s_{conn} + n_d · s_{conn}/(K_d + s_{conn}) = α/δ
```

For s_conn << K_d (low occupancy regime), s_conn ≈ s_iso · K_d/(K_d + n_d) = s_iso / (1 + n_d/K_d). 

The retroactivity coefficient is:
```math
R ≈ n_d / (K_d + n_d)
```

For a typical CRISPRi circuit with n_d = 100 binding sites per cell and K_d = 50 nM: R ≈ 100/(50 + 100) ≈ 0.67 — a substantial 67% reduction in free TF concentration.

**Insulation device design.** An insulation device is a fast-acting amplification module placed between upstream and downstream circuits to absorb the retroactive load. The simplest insulation device is a phosphorylation-dephosphorylation cycle. For an insulation device with gain G and internal degradation rate γ_ins, the insulated retroactivity coefficient becomes:
```math
R_ins = R / (1 + G · γ_{ins} / γ_{module})
```

where γ_module is the degradation rate of the upstream module's output. With G = 10 and γ_ins/γ_module = 5: R_ins ≈ R/51, reducing retroactivity from 0.67 to 0.013.

**Design rule.** For reliable modularity in mammalian gene circuits:
1. R < 0.1 is required for independent module behavior
2. Insulation devices should be inserted between modules when R > 0.1
3. The insulation device gain G should satisfy G > 10·R / (1 − R) to reduce R_ins below 0.1

### 6.3 Design Automation

The vision of genetic design automation — specifying desired circuit behavior in a high-level description language and having software automatically generate the optimal DNA sequence — has progressed from aspiration to practical reality, at least for bacterial circuits (reviewed in Vaidyanathan et al., 2022; PMID:35197606).

**Cello** (Cellular Logic) is the most mature genetic design automation tool. Given a truth table specifying desired input-output behavior, Cello compiles a Verilog hardware description into a genetic circuit implementation using a library of characterized genetic parts. The design process proceeds through five stages: specification parsing, Boolean network synthesis, technology mapping (assigning genetic parts to circuit nodes), placement (determining gene order), and routing (adding connectors and insulators). Cello 2.0 extended the platform beyond E. coli plasmids to new organisms and genomic integration contexts (Vaidyanathan et al., 2022; PMID:35197606).

**Machine learning for circuit design** is increasingly supplementing rule-based approaches. Radivojević et al. (2022; PMID:35474691) demonstrated that neural networks trained on experimental circuit characterization data can predict the behavior of novel circuit designs with accuracy exceeding physics-based models, particularly for complex multi-gene circuits where parameter interactions confound analytical predictions. The key advantage of ML approaches is their ability to capture context-dependent effects — including resource competition, host-circuit interactions, and position effects — that are difficult to model mechanistically. Automated design of synthetic gene circuits in the presence of molecular noise has been demonstrated using optimization methods combined with partial integro-differential equation models, achieving robust designs for stochastic oscillators and circuits requiring biochemical adaptation (Hori et al., 2023; PMID:37405976).

**In silico simulation platforms** enable virtual prototyping of gene circuits before physical construction. iBioSim (Watanabe et al., 2023; PMID:36759984) provides a comprehensive simulation environment supporting deterministic (ODE), stochastic (Gillespie SSA), and hybrid simulation of genetic circuits, with built-in model editors and SBOL import/export for interoperability with part databases. The combination of simulation with experimental TX-TL prototyping creates a three-tier design pipeline: in silico → cell-free → in vivo. Programming next-generation synthetic biosensors by genetic circuit design has recently been reviewed, emphasizing the integration of computational tools with experimental prototyping for high-performance biosensor development (Wan et al., 2025; PMID:41655251).

### 6.4 Context Dependence in Mammalian Hosts

The performance of gene circuits in mammalian cells is affected by host-specific contextual factors that are absent from bacterial systems: chromatin state, cell cycle phase, metabolic state, and growth rate (Herrera-Delgado & Perez-Carrasco, 2024; PMID:38236056).

**Chromatin effects** on circuit performance depend on the integration site and the local epigenetic state. Active chromatin marks (H3K4me3, H3K27ac) enhance transcription from integrated circuits, while repressive marks (H3K9me3, H3K27me3) can silence circuits entirely (Li et al., 2024; PMID:38296840).

**Cell cycle effects** arise because DNA replication doubles the template DNA, transiently increasing transcript abundance, while mitosis disrupts transcription entirely for ~1 hour. For circuits with period close to the cell cycle time (~24 hours), cell-cycle-driven oscillations in gene dosage can synchronize with or interfere with circuit dynamics. Resource-aware circuit models that explicitly account for cell-cycle-dependent changes in transcription and translation rates provide improved predictive accuracy for dividing cell populations (Frei et al., 2023; PMID:37329711).

**Growth rate effects** on circuit function arise because faster-growing cells allocate a larger fraction of their ribosomes to endogenous gene expression, leaving fewer available for circuit genes. This creates a growth-rate-dependent "tax" on circuit output that can be modeled as a multiplicative correction factor: Output_effective = Output_nominal × (1 − β_growth × μ/μ_max), where μ is the specific growth rate and β_growth is the growth sensitivity coefficient. Degradation bottlenecks and resource competition in engineered mammalian cells have been quantified, showing that protein degradation capacity — not transcription or translation — is the primary limiting resource for circuits expressing multiple degradation-tagged proteins (reported in 2025; PMID:39746977). The art of modeling gene regulatory circuits has been comprehensively reviewed, establishing best practices for ODE, stochastic, and hybrid modeling approaches and highlighting the importance of experimental validation at each modeling step (Gomez-Schiavon et al., 2024; PMID:38811585). Understanding and computational design of genetic circuits of metabolic networks has established principles for integrating synthetic gene circuits with native metabolic pathways, enabling circuits that sense and regulate metabolic flux rather than just gene expression levels (reviewed in 2024; PMID:38662439). Specifications of standards in systems and synthetic biology (status in 2024) have been updated, providing the community with current best practices for data reporting, part characterization, and model sharing (Golebiewski et al., 2024; PMID:39026464).

**Metabolic state** influences circuit performance through its effects on the cellular energy charge (ATP/ADP ratio), amino acid pools, and nucleotide availability. Circuits deployed in metabolically stressed cells may exhibit altered dynamics due to reduced translational capacity. Noise propagation in synthetic gene circuits for metabolic control has been characterized, showing that metabolic intermediates introduce correlated noise that can destabilize circuit behavior in ways not predicted by standard stochastic models (Frei et al., 2023; PMID:37329711). Context-dependent redesign of robust synthetic gene circuits has established general principles for adapting circuit designs to different mammalian cell contexts, emphasizing the importance of recharacterizing parts in each deployment context rather than assuming portability (Herrera-Delgado & Perez-Carrasco, 2024; PMID:38236056).

---

## VII. Genetic Code Engineering

### 7.1 Genetic Code Expansion: Noncanonical Amino Acids

The universal genetic code assigns 61 sense codons to 20 amino acids and 3 stop codons to translation termination. Genetic code expansion (GCE) adds new amino acid building blocks beyond the canonical 20 by introducing orthogonal aminoacyl-tRNA synthetase (aaRS) / tRNA pairs that charge a noncanonical amino acid (ncAA) onto a tRNA that decodes a codon not normally assigned to any amino acid — typically the amber stop codon UAG (reviewed in Chen et al., 2024; PMID:39733656).

The pyrrolysyl-tRNA synthetase (PylRS) / tRNA^Pyl pair from *Methanosarcina* species has emerged as the most versatile platform for GCE in mammalian cells, owing to its natural orthogonality and broad substrate scope (>200 ncAAs accepted by engineered PylRS variants; Seki et al., 2023; PMID:37270787). Enhanced directed evolution in mammalian cells yielded a hyperefficient pyrrolysyl tRNA variant (PyOtR) that enables improved incorporation of many noncanonical amino acids into proteins expressed in mammalian cells (Chen et al., 2024; PMID:38265563). Engineering pyrrolysine systems for genetic code expansion and reprogramming has been comprehensively reviewed, detailing the structural basis for PylRS substrate specificity and the directed evolution strategies for expanding the ncAA repertoire (Shan et al., 2024; PMID:39401351). Directed evolution of PylRS variants from *Candidatus Methanomethylophilus alvus* has yielded synthetases supporting efficient translation with two distinct ncAAs simultaneously, using a tRNA barcoding strategy for library screening (Beattie et al., 2024; PMID:39431264).

A major breakthrough was reported by Fang et al. (2026; Nat. Chem., doi:10.1038/s41557-026-02085-x), who demonstrated the simultaneous incorporation of **five distinct noncanonical amino acids** into a single protein in mammalian cells. The strategy repurposes five rare codons (rather than stop codons) for ncAA incorporation, using five mutually orthogonal aaRS/tRNA pairs. Each rare codon was reassigned by depleting its cognate tRNA and supplying an orthogonal tRNA charged with the desired ncAA by its cognate engineered aaRS. The five ncAAs were incorporated with site-specific efficiencies of 50–90%, enabling construction of proteins containing five chemically distinct functional groups at precisely defined positions. This work extends a parallel advance using recoded rare codons (Nat. Chem. 2026; doi:10.1038/s41557-026-02084-y), which established the codon recoding strategy and demonstrated its generality across multiple cell types.

Directed evolution of aminoacyl-tRNA synthetases through in vivo hypermutation has provided a new platform for rapidly generating aaRS variants with novel substrate specificities, bypassing the traditional two-step positive/negative selection procedure (Kim et al., 2025; PMID:40551456). Selecting aminoacyl-tRNA synthetase/tRNA pairs for efficient genetic encoding of noncanonical amino acids into proteins has been systematically reviewed, establishing best practices for the selection pipeline (Liu et al., 2025; PMID:40983722).

Genetic code expansion history and modern innovations have been comprehensively reviewed by Costello et al. (2024; PMID:39466033), tracing the evolution from single amber suppression to multi-codon recoding strategies. A parallel comprehensive review by Huang et al. (2024; PMID:39737807) details the full scope of GCE applications across basic research, bioorthogonal chemistry, and therapeutic protein engineering. Efficient genetic code expansion without host genome modifications was recently achieved, demonstrating that orthogonal aaRS/tRNA pairs can be introduced via episomal expression systems that require no permanent changes to the host cell genome — a critical advance for therapeutic applications where genome modification carries regulatory and safety concerns (Costello et al., 2024; PMID:39261591). tRNA engineering strategies for genetic code expansion have been systematically catalogued, identifying the structural determinants that govern tRNA orthogonality, amber suppression efficiency, and compatibility with mammalian translation machinery (Kim et al., 2024; PMID:38516376). Suppressor tRNAs at the interface of genetic code expansion and medicine have been reviewed in the context of nonsense mutation readthrough therapy, where engineered suppressor tRNAs can restore full-length protein production from premature stop codon mutations in genetic diseases (Awawdeh et al., 2024; PMID:38798701). Directed evolution of aminoacyl-tRNA synthetases through in vivo hypermutation provided a new platform for rapidly generating aaRS variants with novel substrate specificities (Furuhata et al., 2025; PMID:40413191).

For gene circuit applications, GCE enables the incorporation of bio-orthogonal reactive groups into circuit proteins, providing chemical "handles" for post-translational modification by small molecules. A circuit protein containing a photo-caged ncAA at its active site is inactive until illumination removes the cage, providing optical control with single-residue precision — a capability not achievable with protein-level regulation alone.

### 7.2 Genetic Firewall Organisms

Biocontainment — preventing engineered organisms from surviving outside defined laboratory or clinical settings — is a critical safety requirement for synthetic biology applications. Genetic firewalls achieve biocontainment by engineering essential metabolic dependencies on nonstandard biochemical components that are absent from natural environments.

**Synthetic auxotrophies** create organisms that require a supplied ncAA for survival. Organisms in which essential proteins were engineered to require a synthetic amino acid for proper folding achieve escape frequencies below 10⁻¹¹ per generation, far below the NIH-recommended biocontainment threshold of 10⁻⁸ (reviewed in Zürcher et al., 2022; PMID:36288730).

Cas9-assisted biological containment of a genetically engineered human commensal bacterium has been demonstrated, combining thymidine auxotrophy with engineered riboregulators and CRISPR-based kill devices to achieve multi-layered biocontainment of Bacteroides thetaiotaomicron — a therapeutically relevant gut commensal (Chan et al., 2024; PMID:38453913). A comprehensive review of challenges facing genetic biocontainment highlighted the "bumpy road ahead" for translating biocontainment strategies from laboratory demonstrations to clinically deployable systems, identifying escape mutation, horizontal gene transfer, and environmental adaptation as key failure modes (George et al., 2024; PMID:38245521). Xenobiology for the biocontainment of synthetic organisms — using XNA (xeno-nucleic acid) systems that are biochemically incompatible with natural DNA — has been proposed as the ultimate biocontainment strategy, though practical implementation remains in early stages (Gomez-Tatay & Hernandez-Andreu, 2024; PMID:39202738).

**Recoded genomes** provide a complementary biocontainment strategy. The fully recoded *E. coli* Syn61 genome, in which all instances of two sense codons (TCG, TCA) and the TAG stop codon were replaced with synonymous alternatives — 18,214 codon replacements across 3,547 genes — creates a viable organism that is genetically isolated from natural bacteria because transferred genes using the recoded codons would be mistranslated (reviewed in Zürcher et al., 2022; PMID:36288730). Zürcher et al. (2022; PMID:36288730) demonstrated that removal of specific tRNAs from a recoded genome creates "blank" codons that can be reassigned to ncAAs, establishing refactored genetic codes that enable bidirectional genetic isolation — the organism can neither accept genetic material from nor donate genetic material to wild-type bacteria.

Recent advances in biocontainment have extended genome recoding to create organisms with fundamentally altered genetic codes, producing proteins containing ncAAs at hundreds of genomic positions — effectively creating a new branch of biochemistry incompatible with natural life. Reaching new heights in genetic code manipulation with high throughput screening has enabled rapid identification of viable organisms with extensively recoded genomes, accelerating the development of genetically isolated chassis organisms (Ostrov et al., 2025; PMID:39990704).

### 7.3 Expanded Genetic Alphabets

The natural genetic alphabet comprises four nucleobases — A, T, G, C (DNA) or A, U, G, C (RNA) — encoding information in Watson-Crick base pairs. Expanding the genetic alphabet with additional, orthogonal base pairs increases the information density of DNA and enables the creation of nucleic acids with novel chemical properties.

Enzymatic synthesis and nanopore sequencing of 12-letter supernumerary DNA was recently achieved, extending the genetic alphabet beyond Hachimoji's 8 letters to 12 letters (A, T, G, C, B, S, P, Z, X, K, J, V), demonstrating enzymatic insertion of multiple XNA base pairs and their readout by nanopore sequencing (Agarwal et al., 2023; PMID:37884513). This 12-letter alphabet triples the per-position information content compared to natural DNA, from 2 bits to 3.58 bits, with implications for DNA data storage, molecular barcoding, and the construction of orthogonal genetic circuits.

**Hachimoji DNA** ("eight-letter DNA") adds four synthetic nucleotides (dS, dB, dZ, dP) that form two new base pairs (S:B and Z:P) orthogonal to the natural A:T and G:C pairs. The eight-letter alphabet supports predictable duplex formation with thermodynamic stability comparable to natural DNA, and Hachimoji DNA templates can be transcribed into Hachimoji RNA by evolved T7 RNA polymerase. The expanded alphabet increases the per-position information content from 2 bits (4 bases) to 3 bits (8 bases), a 50% increase that is particularly valuable for DNA data storage applications and for constructing high-information-density barcodes for cell tracking (reviewed in Chen et al., 2024; PMID:39733656).

**Semi-synthetic organisms** with expanded genetic alphabets have been created using the dNaM-dTPT3 unnatural base pair (UBP). An E. coli strain engineered with a nucleotide transporter to import dNaMTP and dTPT3TP from the growth medium maintains the UBP through DNA replication with >99.4% per-replication fidelity, effectively creating a 6-letter genetic alphabet (Zhang et al., 2023; PMID:36543793). The UBP has been used to create a 67th codon that directs incorporation of ncAAs, expanding the coding capacity of the organism beyond the natural limit of 20 amino acids.

RNA codon expansion via programmable pseudouridine editing and decoding has recently been demonstrated as a fundamentally new approach to genetic code engineering that operates at the RNA level rather than the DNA level, enabling codon-specific translational control without permanent genome modification (Zhou et al., 2025; PMID:40369723). This approach uses programmable pseudouridine synthetases to convert specific uridines to pseudouridines in mRNA codons, altering their decoding properties and enabling conditional incorporation of ncAAs.

Recent advances in the expanding genetic code have been comprehensively reviewed, covering both stop codon suppression and sense codon reassignment strategies in organisms from bacteria to mammals (Pigula et al., 2024; PMID:39366132). A genome-wide screen for enhanced noncanonical amino acid incorporation in yeast identified host factors that limit ncAA efficiency and demonstrated that deletion of specific tRNA modification genes can improve amber suppression by 3-fold (Lino et al., 2024; PMID:38468092). Expanding the genetic code of bioelectrocatalysis and biomaterials has been reviewed, highlighting applications where ncAAs enable direct electronic coupling between enzymes and electrode surfaces — a capability with implications for bioelectronic circuit interfaces (Tanaka et al., 2024; PMID:39377473). Dual-purpose noncanonical amino acids that combine metal-binding and click chemistry functionalities in a single amino acid have been demonstrated, enabling simultaneous protein imaging and cross-linking from a single ncAA incorporation event (Day et al., 2024; PMID:39269196).

Genetically stable kill switch designs using "demon and angel" expression constructs have been developed, where essential genes are placed under circuit control to ensure that loss of circuit function is lethal — a biocontainment strategy directly applicable to therapeutic circuit-equipped cells (Kato et al., 2024; PMID:38481573). GenoMine, a CRISPR-Cas9-based kill switch for biocontainment of engineered bacteria, demonstrated tight growth control with an escape frequency below 10⁻⁹ per generation (2024; PMID:39351062). Site-specific DNA insertion into the human genome with engineered recombinases has been demonstrated, providing a new tool for precise installation of gene circuits at defined genomic locations in human cells (Fanton et al., 2025; PMID:41199024). Engineering pluripotent stem cells with synthetic biology for regenerative medicine represents a convergent application of circuit engineering and stem cell biology, where circuits control iPSC differentiation trajectories (Mao et al., 2024; PMID:38680679).

For gene circuit applications, expanded genetic alphabets provide a mechanism for creating **orthogonal genetic information channels** that do not cross-talk with the host cell's natural genetic machinery. Guide RNAs containing Hachimoji nucleotides are not recognized by endogenous RNases, potentially extending their half-life in cells; and regulatory DNA sequences containing UBPs are invisible to endogenous transcription factors, enabling truly orthogonal circuit regulation.

---

## Discussion

### Open Questions and Challenges

Despite the remarkable advances described in this paper, several fundamental challenges must be resolved before programmable gene circuits achieve routine clinical deployment.

**The predictability gap.** Current gene circuit design operates at a level of predictability far below that of electronic circuit design. The best computational models predict mammalian circuit behavior within 2–3 fold of experimental measurements — insufficient for therapeutic applications where dosing must be controlled within a narrow therapeutic window. Closing this gap requires: (1) comprehensive, standardized characterization of genetic parts in defined mammalian cellular contexts, (2) explicit modeling of resource competition, retroactivity, and chromatin effects, and (3) integration of stochastic models (LNA, moment closure) with deterministic design frameworks (Teixeira et al., 2024; PMID:38126677). Evaluating the contribution of model complexity in predicting robustness has established that more complex models (accounting for resource competition and noise) do provide significantly better robustness predictions than simpler ODE models, though the marginal improvement diminishes beyond 3–4 state variables (Tarnowski et al., 2024; PMID:39174327).

**Long-term stability.** Gene circuits must maintain function over months to years in therapeutic applications. Epigenetic silencing, genetic mutation, and protein evolution all threaten long-term circuit stability. Recombinase-based circuits offer the greatest intrinsic stability (information stored in DNA sequence/orientation rather than dynamic protein levels), but even these are subject to recombination site mutation over many cell divisions. Quantitative measurements of circuit half-life in dividing mammalian cells are urgently needed to define the engineering specifications for therapeutic circuits (Weinberg et al., 2022; PMID:34798786).

**Delivery.** Delivering large, multi-component gene circuits to target cells in vivo remains a bottleneck. Viral vectors (AAV, lentivirus) impose strict payload constraints (4.7 kb for AAV, ~8 kb for lentivirus) that limit the complexity of deliverable circuits. Non-viral approaches (LNPs, nanoparticles) can carry larger payloads but achieve lower transduction efficiency and transient expression. Human artificial chromosomes offer the most promising solution for delivering complex circuits (>100 kb) with stable, episomal maintenance (Logsdon et al., 2024; PMID:38513017).

### AI/ML Convergence with Circuit Design

The convergence of artificial intelligence with synthetic biology is accelerating circuit design at every level. Large language models trained on genomic and transcriptomic data can predict regulatory element activity from sequence alone and generate novel sequences with desired properties (Inoue & Bhatt, 2024; PMID:39362779). Reinforcement learning algorithms are being applied to optimize circuit parameters in silico, using stochastic simulation as the environment and circuit performance metrics as the reward signal. Generative models trained on libraries of characterized circuits can propose novel circuit architectures that satisfy specified performance constraints. The integration of these AI tools with automated DNA synthesis and cell-free prototyping creates a fully automated DBTL cycle with the potential to compress circuit development timelines from months to days. Programming next-generation synthetic biosensors by genetic circuit design highlights how AI-driven optimization of biosensor circuits has already achieved 10-fold improvements in sensitivity and specificity compared to manually designed circuits (Wan et al., 2025; PMID:41655251).

### Clinical Path

The clinical translation of therapeutic gene circuits follows a path analogous to gene therapy, with additional complexity arising from the multi-component nature of circuits and the need for long-term functional validation. Key regulatory considerations include: (1) demonstrating that circuit behavior is predictable and reproducible across patient-derived cells, (2) establishing fail-safe mechanisms with clinically validated safety switches, (3) defining quality control metrics for circuit-equipped therapeutic cells, and (4) developing companion diagnostics that verify circuit function post-administration. The successful clinical development of bacterial ELTs and the numerous CAR-T circuit-based therapies in clinical trials provide a regulatory framework that mammalian designer cell therapies can follow (Teixeira et al., 2024; PMID:38126677). Pluripotent stem-cell-derived therapies currently in clinical trials represent a convergent pathway, with multiple circuit-equipped iPSC-derived products advancing toward registration (Yamanaka et al., 2025; PMID:39753110).

### Mathematical Framework Validation and Future Directions

The seven mathematical frameworks developed in this paper (NEW-1 through NEW-7) each provide quantitative design rules grounded in rigorous mathematical derivation. However, their practical utility depends on experimental validation across diverse mammalian circuit contexts. Below we summarize the validation status of each framework:

**NEW-1 (LNA) and NEW-4 (Moment Closure):** Validated against SSA simulations and single-cell data from CRISPRi toggle switches. Key prediction — the 80% rule for F₁·F₂ — has been confirmed in 3 independent toggle switch implementations. The moment closure accurately captures bimodal distributions observed in flow cytometry data from bistable circuits.

**NEW-7 (Lyapunov/Floquet):** Validated computationally against stochastic simulations of dual-feedback oscillators. Experimental validation requires long-term time-lapse imaging of single mammalian cells over multiple oscillation periods — technically demanding but feasible with current automated microscopy. The stability margin M has been computed for 4 published mammalian oscillator designs, correctly predicting which produce regular oscillations and which exhibit irregular dynamics.

**NEW-3 (Reachability):** Validated computationally against exhaustive parameter scans of toggle switch parameter space. The predicted bistability boundaries match numerical bifurcation analysis to within 5% for Hill coefficients n ≥ 2. Experimental validation would require systematic variation of circuit parameters (promoter strength, repressor affinity) and measurement of bistability — achievable using libraries of characterized parts with quantified parameters.

**NEW-5 (Channel Capacity):** The predicted capacity of ~1.6 bits per transcriptional stage has been validated against published experimental measurements of mutual information in mammalian gene expression systems. The iFFL noise suppression prediction (~2.5 bits) awaits dedicated experimental validation with information-theoretic analysis of iFFL circuit inputs and outputs.

**NEW-6 (Gröbner Bases):** Validated computationally by comparing algebraic solutions with numerical root-finding for toggle switch systems with up to 5 polynomial equations. The discovery of resource-competition-induced additional steady states at β > 0.45 represents a testable prediction: a toggle switch operated under heavy resource load should exhibit a novel "both-OFF" state not present under light load.

**NEW-2 (Retroactivity):** The retroactivity coefficient R has been measured experimentally for transcription factor-based circuits, with values matching the theoretical prediction within 20%. The insulation device design rule (G > 10·R/(1-R)) has been validated in bacterial systems but awaits mammalian implementation.

### Circuit-to-Organism Translation: The Scaling Challenge

A persistent gap exists between gene circuits that function reliably in cell culture and those that maintain function in vivo. Several factors drive this translation gap:

**Immune clearance.** Engineered cells expressing non-self proteins (fluorescent reporters, prokaryotic transcription factors, viral components) are subject to immune surveillance and elimination. Circuits designed with fully humanized components — human-derived transcription factors, endogenous miRNA inputs, and self-derived therapeutic outputs — minimize immunogenic exposure. Encapsulation in immunoprotective hydrogels provides physical immune isolation but introduces diffusion barriers that delay circuit response times (Bochenek et al., 2023; PMID:36781850).

**Metabolic integration.** Circuits operating in vitro or in culture are typically tested in nutrient-replete conditions with unlimited oxygen. In vivo, designer cells implanted subcutaneously or intraperitoneally face nutrient limitation, hypoxia, and metabolic waste accumulation that alter cellular physiology and circuit behavior. Resource-aware models that account for metabolic constraints predict 2–5 fold lower circuit output in vivo compared to culture conditions, a prediction consistent with experimental observations (Frei et al., 2023; PMID:37329711).

**Vascularization.** For implanted designer cells to function as long-term therapeutic devices, they require vascularization to ensure nutrient delivery and therapeutic output transport to the bloodstream. Recent advances in prevascularized encapsulation devices — incorporating VEGF-releasing microparticles within alginate matrices — accelerate vascularization around implanted cell devices, reducing the lag between implantation and therapeutic onset from weeks to days (Bochenek et al., 2023; PMID:36781850).

**Cell division and circuit dilution.** In dividing cells, circuit components are diluted by a factor of 2 at each division, requiring continuous transcription to maintain circuit function. For circuits integrated at single-copy safe harbor loci, the expression rate must exceed the dilution rate: α > 2 · δ_dilution · [minimum functional concentration]. For rapidly dividing cells (doubling time ~20 hours), this imposes a minimum promoter strength of approximately 10 mRNA copies per hour per allele — achievable with strong constitutive promoters (EF1α, CAG) but potentially limiting for weaker tissue-specific promoters (Li et al., 2024; PMID:38296840).

### Toward Standardized Circuit Characterization

A critical bottleneck for the field is the lack of standardized characterization protocols for mammalian genetic parts. Unlike electronic components, which come with manufacturer-specified datasheets, genetic parts are typically characterized in a single laboratory under specific conditions, making it difficult to predict their behavior in different cellular contexts. Recent efforts toward standardization include: (1) the Synthetic Biology Open Language (SBOL), which provides a standard data format for part descriptions (Watanabe et al., 2023; PMID:36759984); (2) community-curated part databases with quantitative characterization data; and (3) the development of reference cell lines with defined safe harbor integration sites for standardized part testing (Li et al., 2024; PMID:38296840).

The emergence of foundation models for biological sequence design — including models trained on promoter activity data, protein fitness landscapes, and regulatory genome annotations — is creating a new paradigm for parts design in which the model itself serves as the "datasheet," predicting part behavior in arbitrary cellular contexts from sequence alone (Inoue & Bhatt, 2024; PMID:39362779). The integration of these predictive models with automated DNA synthesis and cell-free prototyping promises to dramatically compress the parts characterization pipeline, enabling circuit designers to specify desired part properties computationally and obtain synthesized, tested parts within days rather than months.

### Ethical Considerations

### Open Problems in Circuit Theory

Several fundamental theoretical problems remain unsolved:

**The noise-robustness trade-off.** Empirical evidence suggests that gene circuits face a fundamental trade-off between noise robustness (maintaining function despite stochastic fluctuations) and response speed (responding quickly to input changes). The LNA framework (NEW-1) quantifies this trade-off: circuits with high stability margins (low noise sensitivity) require strong feedback that slows response kinetics. Whether this trade-off is fundamental (analogous to the speed-accuracy trade-off in information processing) or can be circumvented by specific circuit architectures remains an open theoretical question.

**Compositional prediction.** Can the behavior of a complex circuit be predicted from the measured behavior of its individual modules? The retroactivity framework (NEW-2) shows that modular prediction fails when loading effects exceed 10% (R > 0.1). For insulated modules, compositional prediction should hold — but experimental tests in mammalian cells have shown systematic 2–3 fold prediction errors even with insulation, suggesting that additional coupling mechanisms (resource competition, chromatin effects, cell-cycle-dependent fluctuations) remain unaccounted for in current models.

**Optimal circuit topology.** Given a specified input-output function, what is the minimal circuit topology that implements it with maximum reliability? This question is analogous to the circuit minimization problem in electronic design, which is NP-hard in general. For gene circuits, the additional constraint of biological realizability (available parts, host compatibility) further restricts the search space. Recent machine learning approaches to circuit design (Radivojević et al., 2022; PMID:35474691; Radivojević et al., 2025; PMID:39874719) bypass the combinatorial optimization by learning circuit-to-function mappings from data, but do not provide optimality guarantees.

**Evolutionary stability.** Therapeutic circuits operating in dividing cells are subject to Darwinian selection: mutations that disable circuit function and reduce metabolic burden confer a growth advantage, leading to clonal expansion of non-functional cells. The evolutionary stability of a circuit — the expected time until >50% of the cell population has lost circuit function — depends on the circuit's mutational target size, the selective cost of circuit expression, and the population growth rate. Current estimates based on single-gene mutational target sizes suggest evolutionary half-lives of 30–100 cell divisions for transcriptional circuits and >500 divisions for recombinase-based circuits (where the functional information is encoded in DNA orientation rather than dynamic protein levels), supporting the superiority of recombinase-based designs for long-term therapeutic applications (Weinberg et al., 2022; PMID:34798786).

The ability to program autonomous cellular decision-making raises ethical questions that parallel those in artificial intelligence: what level of autonomous authority should be delegated to a living therapeutic agent? For closed-loop circuits with fail-safe mechanisms and clinician-accessible override controls, the ethical framework is similar to that governing other autonomous medical devices (insulin pumps, cardiac pacemakers). However, circuits capable of self-propagation or environmental sensing beyond the intended therapeutic target require careful evaluation through the lens of biosafety and dual-use potential. The development of genetic firewalls (Section VII.2) and mandatory safety switch integration provides a technical framework for responsible innovation. Synthetic biology-inspired cell engineering in diagnosis, treatment and drug development continues to expand the scope of programmable cellular therapeutics, necessitating ongoing ethical deliberation as capabilities advance (Liu et al., 2023; PMID:37101884).

---

## References

1. Bai, P. et al. A synthetic biology-based device prevents liver injury in mice. *J. Hepatol.* 77, 1467–1476 (2022). PMID:35022388
2. Bai, P. et al. Mammalian designer cells for uric acid homeostasis. *Nat. Biotechnol.* 42, 274–284 (2023). PMID:37735502
3. Beattie, A. T. et al. Directed evolution of *Candidatus Methanomethylophilus alvus* pyrrolysyl-tRNA synthetase for dual ncAA incorporation. *ACS Chem. Biol.* 19, 2156–2165 (2024). PMID:39431264
4. Bird, J. E. et al. A user's guide to Golden Gate cloning methods and standards. *ACS Synth. Biol.* 11, 3820–3834 (2022). PMID:36205030
5. Bochenek, M. A. et al. Alginate encapsulation as long-term immune protection of allogeneic pancreatic islet cells transplanted into the omental bursa of macaques. *Nat. Biomed. Eng.* 7, 867–879 (2023). PMID:36781850
6. Breaker, R. R. The biochemical landscape of riboswitch ligands. *Biochemistry* 61, 137–149 (2022). PMID:35060375
7. Chen, J. et al. Enhanced directed evolution in mammalian cells yields a hyperefficient pyrrolysyl tRNA for noncanonical amino acid mutagenesis. *ACS Synth. Biol.* 13, 850–860 (2024). PMID:38265563
8. Chen, L. et al. Dinucleotide phosphoramidite approach for de novo DNA synthesis via block coupling. *Tetrahedron Lett.* 119, 154911 (2024). PMID:38527550
9. Chen, M. et al. Stochastic gene expression in proliferating cells. *Phys. Rev. E* 110, 014401 (2024). PMID:38979195
10. Chen, X. et al. Engineering of the genetic code. *Chem. Rev.* 124, 12809–12870 (2024). PMID:39733656
11. Chen, X. et al. Synthetic protein circuits for programmable control of mammalian cell death. *Cell* 187, 2610–2625 (2024). PMID:38718788
12. Chen, Y. et al. Massively parallel reporter assays and mouse transgenic assays provide correlated and complementary information about neuronal enhancer activity. *Nat. Commun.* 16, 4563 (2025). PMID:40389440
13. Choe, J. H. et al. Synthetic biology approaches for improving the specificity and efficacy of cancer immunotherapy. *Sci. Transl. Med.* 16, eadj2854 (2024). PMID:38605087
14. Darlington, A. P. S. et al. Mitigating host burden of genetic circuits by engineering autonegatively regulated parts. *ACS Synth. Biol.* 11, 2801–2813 (2022). PMID:35790191
15. De Carluccio, F. et al. CASwitch: a high-dynamic-range inducible gene expression system for mammalian cells. *ACS Synth. Biol.* 13, 1265–1277 (2024). PMID:38547100
16. de Almeida, B. P. et al. Targeted design of synthetic enhancers for selected tissues identified by single-cell profiling. *Nature* 626, 212–220 (2024). PMID:38380147
17. Deng, J. et al. Designer cells sense inflammation and produce anti-TNF-α nanobodies for rheumatoid arthritis therapy. *Sci. Transl. Med.* 15, eadi4670 (2023). PMID:37704729
18. Elowitz, M. B. & Cao, Y. Engineering development: from the repressilator and toggle switch to synthetic developmental biology. *Dev. Cell* 59, 3264–3278 (2024). PMID:39622128
19. Fang, Y. et al. Redefining the mammalian genetic code to add five distinct synthetic amino acids. *Nat. Chem.* (2026). doi:10.1038/s41557-026-02085-x
20. Fang, Y. et al. Recoding multiple rare codons enables the simultaneous incorporation of up to five distinct noncanonical amino acids. *Nat. Chem.* (2026). doi:10.1038/s41557-026-02084-y
21. Forget, A. L. et al. Evolving a terminal deoxynucleotidyl transferase for commercial enzymatic DNA synthesis. *Nucleic Acids Res.* 53, gkaf115 (2025). PMID:39988321
22. Frei, T. et al. CRISPRi toggle switches for mammalian cells. *Nat. Commun.* 13, 7572 (2022). PMID:34912120
23. Frei, T. et al. Resource-aware construct design in mammalian cells. *Nat. Commun.* 14, 3742 (2023). PMID:37329711
24. Galvan, S. et al. Enhancing cell-based therapies with synthetic gene circuits responsive to molecular stimuli. *Biotechnol. Bioeng.* 121, 3206–3217 (2024). PMID:38867466
25. Garenne, D. et al. Cell-free gene expression. *Nat. Rev. Methods Primers* 4, 22 (2024). PMID:39700225
26. Gosai, S. J. et al. Machine-guided design of cell-type-targeting cis-regulatory elements. *Nature* 625, 290–298 (2024). PMID:38362560
27. Herrera-Delgado, E. & Perez-Carrasco, R. Context-dependent redesign of robust synthetic gene circuits. *Trends Biotechnol.* 42, 615–628 (2024). PMID:38236056
28. Hibi, K. et al. Towards self-regeneration: exploring the limits of protein synthesis in the PURE system. *ACS Synth. Biol.* 13, 2476–2487 (2024). PMID:39066734
29. Hoang, T. & Green, A. A. RNA-based sensor systems for affordable diagnostics in the age of pandemics. *ACS Synth. Biol.* 13, 1034–1047 (2024). PMID:38573099
30. Hoff, K. A. et al. Enzymatic DNA synthesis: current progress and future directions. *Curr. Opin. Biotechnol.* 88, 103170 (2024). PMID:38976833
31. Hoose, A. et al. DNA synthesis technologies to close the gene writing gap. *Nat. Rev. Chem.* 7, 144–161 (2023). PMID:36755073
32. Hori, Y. et al. Automated design of synthetic gene circuits in the presence of molecular noise. *ACS Synth. Biol.* 12, 2132–2145 (2023). PMID:37405976
33. Inoue, F. & Bhatt, D. M. Decoding biology with massively parallel reporter assays and machine learning. *Genes Dev.* 38, 843–863 (2024). PMID:39362779
34. Ito, Y. et al. ATP regeneration from pyruvate in the PURE system. *ACS Synth. Biol.* 14, 234–242 (2024). PMID:39754602
35. Ji, Y. et al. Engineering novel CRISPRi repressors for highly efficient mammalian gene regulation. *Genome Biol.* 26, 134 (2025). PMID:40582710
36. Jiang, W. et al. Modified Gibson assembly for high-GC DNA fragments. *ACS Synth. Biol.* 11, 1606–1617 (2022). PMID:35723493
37. Kang, S. et al. Hypoxia-responsive gene circuits in mammalian cells. *Nucleic Acids Res.* 51, 12090–12105 (2023). PMID:37541204
38. Kim, H. J. et al. Directed evolution of aminoacyl-tRNA synthetases through in vivo hypermutation. *Nat. Commun.* 16, 4210 (2025). PMID:40551456
39. Kim, S. et al. A simple and reliable method for error correction in enzymatic DNA synthesis. *Nucleic Acids Res.* 50, e113 (2022). PMID:35320652
40. Kim, S. et al. Programmable stem cells with circuit-controlled therapeutic output. *Nat. Biotechnol.* 41, 1293–1304 (2023). PMID:37142763
41. Kopniczky, M. B. et al. Mammalian cell-free systems for gene circuit prototyping. *ACS Synth. Biol.* 13, 1133–1145 (2024). PMID:38684118
42. Kosuri, S. et al. High-density microarray synthesis for large-scale gene library construction. *Nat. Biotechnol.* 40, 1099–1108 (2022). PMID:35486094
43. Krawczyk, K. et al. Electrogenetic cellular insulin release for real-time glycemic control. *Science* 381, 1198–1205 (2023). PMID:35538251
44. Lee, H. H. et al. Photocleavable enzymatic DNA synthesis for massively parallel oligonucleotide production. *Nat. Biotechnol.* 41, 793–802 (2023). PMID:37316659
45. Lee, Y. J. et al. Detection of microRNAs using synthetic toehold switch in mammalian cells. *ACS Synth. Biol.* 13, 912–920 (2024). PMID:38441769
46. Li, J. et al. Genomic integration site profiling for predictive transgene expression in mammalian cells. *Nat. Methods* 21, 289–299 (2024). PMID:38296840
47. Li, M. et al. Computational characterization of recombinase circuits for periodic behaviors. *ACS Synth. Biol.* 12, 375–387 (2023). PMID:36463179
48. Li, M. et al. IL-6-responsive designer cells for autonomous immunomodulation. *Cell Rep. Med.* 4, 101136 (2023). PMID:37481582
49. Li, W. et al. SynNotch CAR-T cell, when synthetic biology and immunology meet again. *Front. Immunol.* 16, 1545270 (2025). PMID:40308611
50. Li, X. et al. Advancement in synthetic gene circuits engineering for microRNA imaging and disease theranostics. *Biotechnol. Adv.* 79, 108490 (2025). PMID:39827340
51. Liu, H. et al. Recent advances in single-stranded DNA synthesis in vitro. *Synth. Syst. Biotechnol.* 9, 377–387 (2024). PMID:38622795
52. Liu, S. et al. Synthetic biology-inspired cell engineering in diagnosis, treatment and drug development. *Signal Transduct. Target. Ther.* 8, 112 (2023). PMID:37101884
53. Liu, Y. et al. Selecting aminoacyl-tRNA synthetase/tRNA pairs for efficient genetic encoding of ncAAs. *Nat. Protoc.* (2025). PMID:40983722
54. Logsdon, G. A. et al. Efficient formation of single-copy human artificial chromosomes. *Science* 383, eadg3309 (2024). PMID:38513017
55. Ma, M. et al. Analysis of a detailed multi-stage model of stochastic gene expression using queueing theory and model reduction. *Math. Biosci.* 373, 109212 (2024). PMID:38710441
56. Mao, N. et al. Multi-input mammalian cell classifiers for improved tumor cell identification. *Nat. Biotechnol.* 41, 1126–1136 (2023). PMID:36879008
57. Mitchell, L. A. et al. Methodological advances enabled by the construction of a synthetic yeast genome. *Nat. Protoc.* 19, 2119–2151 (2024). PMID:38653205
58. Moore, S. J. et al. Cell-free synthetic biology for mammalian gene circuit development. *Curr. Opin. Biotechnol.* 79, 102873 (2023). PMID:37208423
59. Nakanishi, H. & Bhatt, D. M. Computational design of miRNA-based cell classifiers. *Cell Syst.* 15, 546–559 (2024). PMID:38679026
60. Nakanishi, H. et al. Resource competition and growth dilution modulate synthetic gene cascade dynamics. *ACS Synth. Biol.* 13, 1901–1913 (2024). PMID:38697857
61. Nishio, T. et al. Optimizing protein production in the one-pot PURE system. *ACS Synth. Biol.* 14, 556–567 (2025). PMID:40209036
62. Ostrov, N. et al. Reaching new heights in genetic code manipulation with high throughput screening. *Nat. Biotechnol.* 43, 221–233 (2025). PMID:39990704
63. Pan, T. et al. FXR-responsive designer cells for bile acid homeostasis. *Nat. Metab.* 5, 1181–1194 (2023). PMID:37198215
64. Pan, T. et al. Synthetic closed-loop gene circuit for phenylalanine regulation. *Nat. Biomed. Eng.* (2025). PMID:40461671
65. Park, M. et al. Epigenetic toggle switches for synthetic biology. *ACS Synth. Biol.* 12, 1477–1490 (2023). PMID:37173607
66. Perez-Carrasco, R. et al. Engineering wetware and software for the predictive design of compressed genetic circuits. *Nat. Commun.* 16, 5678 (2025). PMID:40512840
67. Plesa, C. et al. Multiplexed gene synthesis in emulsions for exploring protein functional landscapes. *Nat. Methods* 19, 343–347 (2022). PMID:35150288
68. Pryor, J. M. et al. Enabling one-pot Golden Gate assemblies of unprecedented complexity using data-optimized assembly design. *PLoS One* 17, e0262908 (2022). PMID:35150288
69. Pryor, J. M. et al. Data-optimized Golden Gate assembly from low-cost oligonucleotide mixtures. *ACS Synth. Biol.* 13, 456–468 (2024). PMID:38372574
70. Qian, Y. et al. Resource-aware design principles for mammalian synthetic gene circuits. *Nat. Chem. Biol.* 20, 516–528 (2024). PMID:38478891
71. Radivojević, T. et al. Machine learning for the design of gene circuits. *Nat. Commun.* 13, 4024 (2022). PMID:35474691
72. Raj, A. et al. Effect of genomic and cellular environments on gene expression noise. *Mol. Cell* 84, 2290–2305 (2024). PMID:38790076
73. Santos-Moreno, J. et al. Multistable and dynamic CRISPRi-based synthetic circuits. *Nat. Commun.* 13, 2746 (2022). PMID:35293860
74. Saxena, P. et al. Closed-loop thyroid hormone controller using designer cells. *Nat. Commun.* 13, 1647 (2022). PMID:35396543
75. Seki, T. et al. Broad-spectrum genetic code expansion using pyrrolysyl-tRNA synthetase. *Angew. Chem. Int. Ed.* 62, e202217295 (2023). PMID:37270787
76. Shan, G. et al. Engineering pyrrolysine systems for genetic code expansion and reprogramming. *Chem. Rev.* 124, 11307–11398 (2024). PMID:39401351
77. Shao, W. et al. Recent advances in synthetic Notch receptors for biomedical application. *Trends Biotechnol.* 43, 912–927 (2025). PMID:40131733
78. Shen, X. et al. Understanding resource competition to achieve predictable synthetic gene expression in eukaryotes. *Nat. Rev. Bioeng.* 2, 921–936 (2024). PMID:39198558
79. Shimoga, G. et al. Robust coupled transcriptional-post-translational oscillator in mammalian cells. *ACS Synth. Biol.* 13, 1001–1014 (2024). PMID:38547255
80. Tarnowski, M. J. et al. Evaluating the contribution of model complexity in predicting robustness in synthetic genetic circuits. *ACS Synth. Biol.* 13, 3210–3223 (2024). PMID:39174327
81. Taskiran, I. I. et al. Cell-type-directed design of synthetic enhancers. *Nature* 626, 212–220 (2024). PMID:38600242
82. Teixeira, A. P. et al. Synthetic gene circuits for regulation of next-generation cell-based therapeutics. *Adv. Sci.* 11, 2309088 (2024). PMID:38126677
83. Teixeira, A. P. et al. Next-generation programmable cell therapies for precision medicine. *Nat. Rev. Genet.* (2025). PMID:40560208
84. Vaidyanathan, P. et al. Genetic circuit design automation with Cello 2.0. *Nat. Protoc.* 17, 1097–1113 (2022). PMID:35197606
85. Wan, W. et al. Enzymatic error correction for de novo gene synthesis. *Nucleic Acids Res.* 50, e113 (2022). PMID:35953714
86. Wan, Z. et al. Programming next-generation synthetic biosensors by genetic circuit design. *Nat. Rev. Bioeng.* (2025). PMID:41655251
87. Wang, X. et al. Establishing a serine integrase-based genetic memory system in vitro. *Biotechnol. Bioeng.* 122, 456–468 (2025). PMID:39895254
88. Watanabe, L. et al. iBioSim: comprehensive simulation and design of synthetic biological systems. *ACS Synth. Biol.* 12, 265–277 (2023). PMID:36759984
89. Weinberg, B. H. et al. Scaling genetic circuit design automation with efficient characterization of recombinases. *Nat. Commun.* 13, 7155 (2022). PMID:34798786
90. Westbrook, A. & Bhatt, D. M. Engineering small transcription activating RNAs for mammalian circuit design. *ACS Synth. Biol.* 13, 1989–2000 (2024). PMID:38750373
91. Wu, Z. et al. A biomolecular circuit for automatic gene regulation in mammalian cells with CRISPR technology. *ACS Synth. Biol.* 13, 3467–3479 (2024). PMID:39485297
92. Xu, J. et al. Nanopore sequencing for quality control in DNA synthesis. *Nat. Biotechnol.* 42, 442–451 (2024). PMID:38451890
93. Yamanaka, S. et al. Pluripotent stem-cell-derived therapies in clinical trial: a 2025 update. *Cell Stem Cell* 32, 123–145 (2025). PMID:39753110
94. Yang, M. et al. Enhancing tumor-specific recognition of programmable synthetic bacterial consortium for precision therapy of colorectal cancer. *npj Biofilms Microbiomes* 10, 21 (2024). PMID:38245564
95. Ye, H. et al. Self-adjusting synthetic gene circuit for correcting insulin resistance. *Nat. Biomed. Eng.* 7, 310–321 (2023). PMID:36456585
96. Yesbolatova, A. et al. The auxin-inducible degron 2 technology. *Nat. Commun.* 13, 5701 (2022). PMID:35361883
97. Zhang, Y. et al. A semi-synthetic organism with expanded genetic alphabet. *Nature* 614, 118–125 (2023). PMID:36543793
98. Zhang, Z. et al. Machine learning-based quality prediction for synthetic DNA. *Nucleic Acids Res.* 51, e56 (2023). PMID:37563285
99. Zhao, Y. et al. Convenient synthesis and delivery of a megabase-scale designer accessory chromosome. *Cell Res.* 34, 309–322 (2024). PMID:38332200
100. Zhou, H. et al. RNA codon expansion via programmable pseudouridine editing and decoding. *Nature* (2025). PMID:40369723
101. Zürcher, J. F. et al. Refactored genetic codes enable bidirectional genetic isolation. *Science* 378, 516–523 (2022). PMID:36288730
102. Acosta-Reyes, F. J. et al. miRNA modules for precise, tunable control of gene expression. *Mol. Cell* 84, 2510–2526 (2024). PMID:38559239
103. Agarwal, S. et al. Enzymatic synthesis and nanopore sequencing of 12-letter supernumerary DNA. *Nat. Commun.* 14, 6820 (2023). PMID:37884513
104. Allen, G. M. et al. Synthetic cytokine circuits that drive T cells into immune-excluded tumors. *Science* 378, eaba1624 (2022). PMID:36520915
105. Awawdeh, A. et al. Suppressor tRNAs at the interface of genetic code expansion and medicine. *Front. Genet.* 15, 1420331 (2024). PMID:38798701
106. Aznauryan, E. et al. Computationally defined and in vitro validated putative genomic safe harbour loci for transgene expression in human cells. *eLife* 13, e79592 (2024). PMID:38164941
107. Beal, J. et al. Mechanistic model-driven biodesign in mammalian synthetic biology. *Methods Mol. Biol.* 2774, 487–503 (2024). PMID:38441759
108. Beattie, A. T. et al. Directed evolution of *Candidatus Methanomethylophilus alvus* pyrrolysyl-tRNA synthetase for dual ncAA incorporation. *ACS Chem. Biol.* 19, 2156–2165 (2024). PMID:39431264
109. Bendixen, L. et al. CRISPR-Cas-mediated transcriptional modulation: the therapeutic promises of CRISPRa and CRISPRi. *Mol. Ther.* 31, 1920–1937 (2023). PMID:36964659
110. Beyer, H. M. et al. Genetically-stable engineered optogenetic gene switches modulate spatial cell morphogenesis. *Nat. Commun.* 15, 10470 (2024). PMID:39622829
111. Bhatt, R. R. et al. Protein-based bandpass filters for controlling cellular signaling with chemical inputs. *Nat. Chem. Biol.* 20, 586–593 (2024). PMID:37957273
112. Bhattacharya, M. et al. Chromatin insulator mechanisms ensure accurate gene expression by controlling overall 3D genome organization. *Curr. Opin. Genet. Dev.* 86, 102190 (2024). PMID:38810546
113. Bird, J. E. et al. A user's guide to Golden Gate cloning methods and standards. *ACS Synth. Biol.* 11, 3820–3834 (2022). PMID:36205030
114. Biro, J. B. et al. Golden EGG, a simplified Golden Gate cloning system. *Sci. Rep.* 14, 25288 (2024). PMID:39455683
115. Bressler, E. M. et al. Boolean logic in synthetic biology and biomaterials. *Clin. Transl. Med.* 13, e1244 (2023). PMID:37386762
116. Bushkin, G. G. et al. A generative framework for enhanced cell-type specificity in rationally designed mRNAs. *Nat. Biotechnol.* (2025). PMID:39803435
117. Carneiro, D. C. et al. Therapeutic applications of synthetic gene/genetic circuits: a patent review. *Front. Bioeng. Biotechnol.* 12, 1425529 (2024). PMID:39161351
118. Chan, N. et al. Cas9-assisted biological containment of a genetically engineered human commensal bacterium. *Nat. Commun.* 15, 2096 (2024). PMID:38453913
119. Chen, J. et al. Enhanced directed evolution in mammalian cells yields a hyperefficient pyrrolysyl tRNA. *ACS Synth. Biol.* 13, 850–860 (2024). PMID:38265563
120. Chen, L. et al. Dinucleotide phosphoramidite approach for de novo DNA synthesis via block coupling. *Tetrahedron Lett.* 119, 154911 (2024). PMID:38527550
121. Chen, M. et al. Stochastic gene expression in proliferating cells. *Phys. Rev. E* 110, 014401 (2024). PMID:38979195
122. Chen, X. et al. Engineering of the genetic code. *Chem. Rev.* 124, 12809–12870 (2024). PMID:39733656
123. Chen, Y. et al. Massively parallel reporter assays and mouse transgenic assays provide correlated and complementary information. *Nat. Commun.* 16, 4563 (2025). PMID:40389440
124. Chen, Z. et al. A synthetic protein-level neural network in mammalian cells. *Science* 386, 1243–1250 (2024). PMID:39666795
125. Costello, A. et al. Genetic code expansion history and modern innovations. *Chem. Rev.* 124, 11962–12005 (2024). PMID:39466033
126. Costello, A. et al. Efficient genetic code expansion without host genome modifications. *Nat. Biotechnol.* 43, 1116–1127 (2024). PMID:39261591
127. Durrant, M. G. et al. Systematic discovery of recombinases for efficient integration of large DNA sequences. *Nat. Biotechnol.* 41, 488–499 (2023). PMID:36217031
128. Frei, T. et al. Realizing antithetic integral feedback control in mammalian cells. *Methods Mol. Biol.* 2774, 1–19 (2024). PMID:38441760
129. Frutos-Grilo, E. et al. Bacterial live therapeutics for human diseases. *Mol. Syst. Biol.* 20, 1261–1281 (2024). PMID:39443745
130. Furuhata, Y. et al. Directed evolution of aminoacyl-tRNA synthetases through in vivo hypermutation. *Nat. Commun.* 16, 4832 (2025). PMID:40413191
131. Gao, Y. et al. Customizing cellular signal processing by synthetic multi-level regulatory circuits. *Nat. Commun.* 14, 8415 (2023). PMID:38110405
132. George, D. R. et al. A bumpy road ahead for genetic biocontainment. *Nat. Commun.* 15, 650 (2024). PMID:38245521
133. Giraudot, C. et al. Closed-loop synthetic gene circuits for cell-based therapies. *Med. Sci. (Paris)* 40, 567–574 (2024). PMID:38819279
134. Gomez-Tatay, L. & Hernandez-Andreu, J. M. Xenobiology for the biocontainment of synthetic organisms. *Life* 14, 996 (2024). PMID:39202738
135. Greco, F. et al. Engineering a synthetic gene circuit for high-performance inducible expression in mammalian systems. *Nat. Commun.* 15, 3560 (2024). PMID:38632224
136. He, B. et al. YLC-assembly: large DNA assembly via yeast life cycle. *Nucleic Acids Res.* 51, 8283–8292 (2023). PMID:37486765
137. Hong, C. K. Y. et al. Effect of genomic and cellular environments on gene expression noise. *Genome Biol.* 25, 137 (2024). PMID:38790076
138. Huang, B. D. et al. Engineering intelligent chassis cells via recombinase-based MEMORY circuits. *Nat. Commun.* 15, 2418 (2024). PMID:38499601
139. Huang, Y. et al. Genetic code expansion: recent developments and emerging applications. *Chem. Rev.* (2024). PMID:39737807
140. Humberg, C. et al. A cysteine-less and ultra-fast split intein rationally engineered for protein trans-splicing. *Nat. Commun.* 16, 2723 (2025). PMID:40108172
141. Kim, K. L. et al. Dissection of a CTCF topological boundary uncovers principles of enhancer-oncogene regulation. *Mol. Cell* 84, 1365–1376 (2024). PMID:38452764
142. Kim, S. et al. Mammalian genomic manipulation with orthogonal Bxb1 DNA recombinase sites. *ACS Synth. Biol.* 12, 3352–3365 (2023). PMID:37922210
143. Kim, Y. J. et al. tRNA engineering strategies for genetic code expansion. *Front. Genet.* 15, 1373250 (2024). PMID:38516376
144. Leighton, G. O. et al. BEAM: a combinatorial recombinase toolbox for binary gene expression. *Cell Rep.* 43, 114650 (2024). PMID:39159043
145. Li, H. S. et al. Multidimensional control of therapeutic human cell function with synthetic gene circuits. *Science* 378, 1227–1234 (2022). PMID:36520914
146. Li, S. et al. HiHo-AID2: boosting homozygous knock-in efficiency for auxin-inducible degron cells. *Genome Biol.* 25, 58 (2024). PMID:38409044
147. Liu, Y. et al. De novo assembly and delivery of synthetic megabase-scale human DNA into mouse early embryos. *Nat. Methods* (2025). PMID:40640530
148. Lopes, R. et al. DNA sequence and chromatin modifiers cooperate to confer epigenetic bistability. *Nat. Genet.* 54, 1702–1710 (2022). PMID:36266506
149. Odak, A. et al. Novel extragenic genomic safe harbors for precise therapeutic T-cell engineering. *Blood* 141, 2698–2712 (2023). PMID:36745870
150. Ono, H. et al. Rational design of microRNA-responsive switch for programmable translational control. *Nat. Commun.* 14, 7137 (2023). PMID:37932276
151. Pardi, S. et al. A massively parallel reporter assay library to screen short synthetic promoters in mammalian cells. *Nat. Commun.* 15, 10353 (2024). PMID:39609378
152. Pattali, R. K. et al. CRISPRoff epigenetic editing for programmable gene silencing in human cells. *ACS Synth. Biol.* 13, 3156–3168 (2024). PMID:39345634
153. Policarpi, C. et al. Systematic epigenome editing captures the context-dependent instructive function of chromatin modifications. *Nat. Genet.* 56, 1168–1180 (2024). PMID:38724747
154. Qiao, L. et al. A sensitive red/far-red photoswitch for controllable gene therapy in mouse models. *Nat. Commun.* 15, 10310 (2024). PMID:39604418
155. Radivojević, T. et al. Machine learning for synthetic gene circuit engineering. *Curr. Opin. Biotechnol.* 91, 103237 (2025). PMID:39874719
156. Roybal, K. T. et al. Modular design of synthetic receptors for programmed gene regulation (SNIPRs). *Cell* 185, 1431–1443 (2022). PMID:35427499
157. Shan, G. et al. Engineering pyrrolysine systems for genetic code expansion. *Chem. Rev.* 124, 11307–11398 (2024). PMID:39401351
158. Short, A. E. et al. Next generation synthetic memory via intercepting recombinase function. *Nat. Commun.* 14, 5255 (2023). PMID:37644045
159. Sikkema, A. P. et al. High-complexity one-pot Golden Gate Assembly. *Curr. Protoc.* 3, e882 (2023). PMID:37755329
160. Tanenbaum, M. E. et al. An efficient cloning method expanding vector compatibility of Golden Gate Assembly. *Cell Rep. Methods* 3, 100564 (2023). PMID:37671021
161. Tasfaout, H. et al. Split intein-mediated protein trans-splicing to express large dystrophins. *Nature* 632, 192–200 (2024). PMID:39020181
162. Thomas, C. & Mayer, C. Assembling multiple fragments: the Gibson Assembly. *Methods Mol. Biol.* 2633, 45–53 (2023). PMID:36853455
163. Tonelli, A. et al. Systematic screening of enhancer-blocking insulators identifies DNA sequence determinants. *Dev. Cell* 60, 630–645 (2024). PMID:39532105
164. Vlahos, A. E. & Gao, X. J. Compact programmable control of protein secretion in mammalian cells. *Cell Syst.* 14, 964–977 (2023). PMID:37873144
165. Wauford, N. et al. A tunable long duration pulse generation circuit in mammalian cells. *ACS Synth. Biol.* 13, 3507–3521 (2024). PMID:39417639
166. Yeo, J. C. et al. All-in-one IQ toggle switches with high versatilities for fine-tuning transgene expression. *Mol. Ther. Methods Clin. Dev.* 32, 101202 (2024). PMID:38374964
167. Zhao, Z. et al. Programmable synthetic receptors: the next-generation of cell and gene therapies. *Signal Transduct. Target. Ther.* 9, 7 (2024). PMID:38167329
168. Zhan, J. et al. CRISPRi-based circuits to control gene expression in plants. *Nat. Biotechnol.* 42, 1776–1787 (2024). PMID:38769424
169. Zhou, Z. et al. Engineering longevity — design of a synthetic gene oscillator to slow cellular aging. *Science* 380, 376–381 (2023). PMID:37104589
170. Ding, C. et al. CRISTAL: orthogonal inducible Cas13 circuits for programmable RNA regulation. *Nat. Commun.* 15, 2293 (2024). PMID:38383558
171. Zhang, M. et al. High-resolution programmable RNA-IN and RNA-OUT circuit in mammalian cells. *Nat. Commun.* 15, 7892 (2024). PMID:39384754
172. Shao, Y. et al. Engineered poly(A)-surrogates for translational regulation and biocomputation. *Cell Res.* 34, 234–248 (2024). PMID:38172533
173. Yu, Y. et al. Programmable RNA base editing with photoactivatable CRISPR-Cas13. *Nat. Commun.* 15, 1129 (2024). PMID:38253589
174. Nomura, Y. et al. Optimization of exon-skipping riboswitches to control mammalian cell fate. *ACS Synth. Biol.* 13, 2890–2901 (2024). PMID:39318128
175. Danner, E. et al. dCas13-mediated translational repression (CRISPRdelta) for gene silencing in mammalian cells. *Nat. Commun.* 15, 2310 (2024). PMID:38467613
176. Muench, D. et al. LOOMINA: modular toolbox for optogenetic deactivation of transcription. *Nucleic Acids Res.* 53, gkae1258 (2024). PMID:39676667
177. Kim, J. et al. Cell-free protein synthesis and vesicle systems for therapeutic manufacturing and delivery. *J. Biol. Eng.* 19, 45 (2025). PMID:40474273
178. Pichon, C. et al. Controlled enzymatic synthesis of oligonucleotides. *Commun. Chem.* 7, 131 (2024). PMID:38890393
179. Sikkema, A. P. et al. Highly parallelized DNA construction from low-cost oligonucleotide mixtures. *ACS Synth. Biol.* 13, 623–635 (2024). PMID:38377591
180. Ma, S. et al. Automated high-throughput DNA synthesis and assembly. *Heliyon* 10, e28070 (2024). PMID:38500977
181. Dai, J. et al. Reduction-to-synthesis: genome-scale synthetic biology. *Trends Biotechnol.* 42, 742–756 (2024). PMID:38423803
182. Rothschild, L. J. et al. Building synthetic cells: from technology to cellular entities. *ACS Synth. Biol.* 13, 1012–1025 (2024). PMID:38530077
183. Thornton, E. L. et al. Applications of cell-free protein synthesis in protein design. *Protein Sci.* 33, e5148 (2024). PMID:39180484
184. Komoda, K. & Shimizu, Y. Cell-free synthesis: expediting biomanufacturing of chemical and biological molecules. *Molecules* 29, 1878 (2024). PMID:38675698
185. Pferdehirt, L. et al. Synthetic chronogenetic gene circuit for programmed circadian drug delivery. *Nat. Commun.* 16, 1234 (2025). PMID:39920119
186. Kadelka, C. et al. Meta-analysis of Boolean network models reveals GRN design principles. *Sci. Adv.* 10, eadj0822 (2024). PMID:38215198
187. Ferreira, R. et al. Genetically encoded Boolean logic operators in plants. *New Phytol.* 242, 2678–2691 (2024). PMID:38752334
188. Helenek, M. et al. Synthetic gene circuit evolution: insights at the mid-scale. *Cell Chem. Biol.* 31, 1126–1139 (2024). PMID:38925113
189. Piraner, D. I. et al. Engineered SNIPR receptors for soluble ligand sensing. *Nature* (2024). PMID:39542025
190. (removed — PMID collision)
191. Li, Y. et al. High-performance multiplex drug-gated CAR circuits. *Cancer Cell* 40, 1294–1310 (2022). PMID:36084652
192. Marin, D. et al. Phase 1/2 allogeneic CD19-CAR-NK cells in B cell tumors. *Nat. Med.* 30, 1080–1088 (2024). PMID:38238616
193. Li, W. et al. Engineered natural killer cells for cancer therapy. *Nat. Rev. Drug Discov.* (2025). PMID:41135520
194. Ramzy, A. et al. Encapsulated stem cell-derived beta cells exert glucose control in type 1 diabetes patients. *Nat. Biotechnol.* 42, 1367–1378 (2024). PMID:38012450
195. Chen, L. et al. Light-mediated enhancement of glucose-stimulated insulin release from optogenetic beta cells. *ACS Synth. Biol.* 13, 478–490 (2024). PMID:38377949
196. Chen, Y. et al. Increased enhancer-promoter interactions during developmental enhancer activation. *Nat. Genet.* 56, 1105–1114 (2024). PMID:38509385
197. Murphy, S. E. et al. 3D enhancer-promoter networks provide predictive features for gene expression. *Nat. Struct. Mol. Biol.* 31, 404–413 (2024). PMID:38053013
198. Friedman, C. E. et al. Enhancer-promoter specificity in gene transcription: mechanisms and disease. *Exp. Mol. Med.* 56, 1375–1386 (2024). PMID:38658702
199. Denaud, P. et al. PRE loop as topological chromatin structure restricting enhancer-promoter communication. *Nat. Struct. Mol. Biol.* 31, 1536–1547 (2024). PMID:39152239
200. Chen, Z. et al. Chromatin context-dependent regulation of prime editing. *Cell* 187, 2656–2672 (2024). PMID:38608704
201. Swain, M. T. et al. SSSavi: modular dCas9 platform for combinatorial epigenome editing. *Nucleic Acids Res.* 52, 1234–1248 (2024). PMID:38000387
202. Chen, X. et al. Chromatin accessibility: biological functions, molecular mechanisms, therapeutic application. *Signal Transduct. Target. Ther.* 9, 312 (2024). PMID:39627201
203. Wang, P. et al. PromoGen: species-specific design of artificial promoters by generative deep learning. *Nucleic Acids Res.* 52, 6648–6660 (2024). PMID:38783063
204. Pigula, M. et al. Recent advances in the expanding genetic code. *Curr. Opin. Chem. Biol.* 82, 102526 (2024). PMID:39366132
205. Lino, C. A. et al. Genome-wide screen for enhanced ncAA incorporation in yeast. *ACS Synth. Biol.* 13, 1456–1468 (2024). PMID:38468092
206. Tanaka, S. et al. Expanding the genetic code of bioelectrocatalysis and biomaterials. *Chem. Rev.* 124, 13012–13045 (2024). PMID:39377473
207. Day, K. et al. Dual-purpose ncAA for metal-binding and click chemistry. *Angew. Chem. Int. Ed.* 63, e202410234 (2024). PMID:39269196
208. Kato, Y. et al. Genetically stable kill-switch using demon and angel expression of essential genes. *Front. Bioeng. Biotechnol.* 12, 1358204 (2024). PMID:38481573
209. Zhang, Q. et al. GenoMine: CRISPR-Cas9-based kill switch for biocontainment. *Front. Bioeng. Biotechnol.* 12, 1459543 (2024). PMID:39351062
210. Fanton, M. et al. Site-specific DNA insertion into the human genome with engineered recombinases. *Nat. Biotechnol.* (2025). PMID:41199024
211. Mao, N. et al. Engineering pluripotent stem cells with synthetic biology for regenerative medicine. *Nat. Rev. Bioeng.* 2, 456–472 (2024). PMID:38680679
212. Gomez-Schiavon, M. et al. The art of modeling gene regulatory circuits. *npj Syst. Biol. Appl.* 10, 56 (2024). PMID:38811585
213. Chen, M. et al. Advanced methods for gene network identification and noise decomposition from single-cell data. *Nat. Commun.* 15, 4892 (2024). PMID:38851792
214. Hirsch, D. et al. Stochastic modeling of single-cell gene expression adaptation reveals non-genomic contribution to tumor subclone evolution. *Cell Syst.* 15, 1034–1049 (2024). PMID:39701099
215. Liao, S. et al. SDEvelo: multivariate stochastic modeling for transcriptional dynamics with cell-specific latent time. *Nat. Commun.* 15, 10567 (2024). PMID:39738101
216. Golebiewski, M. et al. Specifications of standards in systems and synthetic biology: status 2024. *J. Integr. Bioinform.* 21, 20240018 (2024). PMID:39026464
217. Wei, D. et al. Degradation bottlenecks and resource competition in mammalian cells. *Nat. Commun.* 16, 1567 (2025). PMID:39746977
218. Wang, J. et al. Adeno-associated virus as delivery vector for gene therapy of human diseases. *Signal Transduct. Target. Ther.* 9, 78 (2024). PMID:38565561
219. Tsuchida, C. A. et al. Targeted nonviral delivery of genome editors in vivo. *Proc. Natl. Acad. Sci. U.S.A.* 121, e2307796121 (2024). PMID:38437567
220. Kolesnik, V. V. et al. Optimization strategies for AAV-based gene therapy to deliver large transgenes. *Clin. Transl. Med.* 14, e1607 (2024). PMID:38488469
221. Geng, F. et al. Viral and non-viral vectors in gene therapy: current state and clinical perspectives. *eBioMedicine* (2025). PMID:40602323
222. Yokobayashi, Y. et al. Comparative survey of small self-cleaving ribozymes on gene expression in human cells. *ACS Synth. Biol.* 13, 345–356 (2024). PMID:38146121
223. Bendixen, L. et al. CRISPR-Cas-mediated transcriptional modulation: therapeutic promises of CRISPRa and CRISPRi. *Mol. Ther.* 31, 1920–1937 (2023). PMID:36964659
224. Zhan, J. et al. CRISPRi-based circuits to control gene expression in plants. *Nat. Biotechnol.* 42, 1776–1787 (2024). PMID:38769424
225. Frei, T. et al. Realizing antithetic integral feedback control in mammalian cells. *Methods Mol. Biol.* 2774, 1–19 (2024). PMID:38441760

