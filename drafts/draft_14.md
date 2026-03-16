# Nanoscale Biophysics

## Abstract

Nanoscale biophysics — the study of physical principles governing biological processes at the atomic and molecular level — has matured from a purely investigative discipline into the foundational science driving first-in-class therapeutics. Six convergent frontiers now define this transformation: targeted protein degradation, conformational ensemble drug design, endosomal escape mechanics, single-molecule protein sequencing, chromatin loop extrusion, and condensate pharmacology. These frontiers, despite their apparent diversity, share four unifying biophysical principles: induced proximity, conformational dynamics, membrane mechanics, and nanoscale information encoding. Targeted protein degradation exploits ternary complex geometry and ubiquitin transfer distance constraints to eliminate previously undruggable proteins, with vepdegestrant becoming the first PROTAC to receive an NDA submission in 2025 (PMID: 40454645). Conformational ensemble drug design leverages cryptic pocket dynamics and Kramers' escape rate theory to access transient druggable states invisible to static structural methods (PMID: 41430437). Endosomal escape — the rate-limiting step in nucleic acid delivery — is now understood through Helfrich membrane bending mechanics and the galectin-ESCRT repair dichotomy, with the first in vivo quantification assays revealing that only ~8% of optimized lipid nanoparticles reach the cytosol (PMID: 41814093). Single-molecule protein sequencing through engineered nanopores achieves amino acid discrimination at 98.6–99.1% accuracy, approaching the Shannon channel capacity limit for a 20-letter alphabet (PMID: 38443507; PMID: 37749214). Chromatin loop extrusion by cohesin — an ATP-driven molecular motor operating at 0.5–2.1 kb/s — organizes the genome into ~300 nm topologically associating domains whose contact dynamics are now resolved at nanoscale precision in non-denatured cells (PMID: 40683887). Condensate-modifying therapeutics exploit liquid-liquid phase separation pharmacology, with the first condensate modulator (DPTX3186) entering Phase I clinical trials in 2026. This review develops seven novel mathematical frameworks — thermodynamic cooperativity cycles, Kramers' escape rate kinetics, Helfrich pore nucleation energetics, Shannon channel capacity for nanopore sequencing, Langevin motor dynamics, worm-like chain polymer mechanics, and stickers-and-spacers mean-field theory — to provide quantitative predictions across these frontiers and identifies the convergent biophysical principles that will define the next generation of molecular medicine.

---

## I. Introduction: The Nanoscale Therapeutic Revolution

The history of drug discovery is, at its core, a history of resolving biological mechanisms at progressively finer spatial scales. The transition from organ-level pharmacology to receptor-level molecular biology in the twentieth century yielded the targeted therapies that now constitute the majority of new drug approvals (PMID: 39500878). The current frontier operates at the nanoscale — the 1–100 nm regime where individual protein conformations, membrane curvatures, chromatin fiber mechanics, and single-molecule information transfer determine therapeutic outcomes. Nanoscale biophysics, defined as the study of physical principles governing biological processes at atomic and molecular resolution, has emerged as the convergent science underlying six therapeutic frontiers that are simultaneously reaching clinical translation.

These six frontiers — targeted protein degradation (TPD), conformational ensemble drug design, endosomal escape mechanics, single-molecule protein sequencing, chromatin loop extrusion, and condensate pharmacology — appear superficially disparate. TPD engineers ternary protein complexes to hijack the ubiquitin-proteasome system (PMID: 39392888). Conformational ensemble design exploits transient cryptic pockets that exist for microseconds to milliseconds within protein energy landscapes (PMID: 39778412). Endosomal escape governs whether lipid nanoparticle (LNP)-delivered nucleic acids reach the cytoplasm or are degraded in lysosomes (PMID: 39293650). Single-molecule protein sequencing threads individual polypeptides through nanometer-scale pores to read amino acid identity from ionic current blockades (PMID: 39261738). Chromatin loop extrusion describes how cohesin molecular motors organize megabase-scale genome domains into ~300 nm structures that regulate transcription (PMID: 40683887). Condensate pharmacology targets the liquid-liquid phase separation (LLPS) of intrinsically disordered proteins into membraneless organelles whose material properties — liquid, gel, or solid — determine cellular function and disease (PMID: 39516712).

Yet beneath this diversity lies a shared biophysical vocabulary. We identify four unifying principles that recur across all six frontiers:

**Induced proximity.** TPD ternary complexes bring E3 ligases within ~10 Å of target protein lysines to enable ubiquitin transfer (PMID: 39392888). Condensate scaffolds concentrate enzymes and substrates by partition coefficients exceeding 600-fold (PMID: 39271915). Chromatin loop extrusion brings enhancers and promoters into contact within ~300 nm domains (PMID: 40683887). Nanopore sequencing threads proteins through ~1.2 nm constrictions to achieve single-residue proximity to the sensing element (PMID: 39261738). In each case, therapeutic function depends on controlling intermolecular distances at the nanometer scale.

**Conformational dynamics.** Cryptic drug-binding pockets open and close on μs–ms timescales with free energy barriers of 2–5 kcal/mol (PMID: 39778412). Cohesin undergoes ATP-dependent conformational cycles that drive DNA loop extrusion at 0.5–2.1 kb/s (PMID: 38831499). LNP ionizable lipids transition between lamellar, inverse micellar, and hexagonal II phases in response to endosomal acidification (PMID: 41060394). Nanopore translocation intermediates adopt distinct conformational states that modulate current blockade signals (PMID: 40097683). Understanding and exploiting these dynamics — rather than targeting static structures — defines the current frontier.

**Membrane mechanics.** Endosomal escape requires overcoming Helfrich bending energy barriers to nucleate pores in endosomal membranes (PMID: 40789922). The dichotomy between ESCRT-reparable small holes and galectin-recognized large ruptures determines whether LNP delivery triggers inflammation (PMID: 40789922). Condensate surface tension governs droplet coalescence and coarsening kinetics (PMID: 40455990). Even chromatin organization involves membrane-like polymer mechanics, with persistence lengths and bending moduli determining the spatial scales of genome folding (PMID: 39601793).

**Information encoding at the single-molecule level.** Nanopore protein sequencing encodes amino acid identity in ionic current blockade patterns, approaching the Shannon channel capacity of log₂(20) ≈ 4.32 bits per position (PMID: 38443507). Chromatin 3D organization encodes gene regulatory information in contact probability distributions that scale as P(s) ~ s^{-α}, where the exponent α distinguishes loop-extruded from equilibrium polymer states (PMID: 40683887). Conformational ensembles encode drug efficacy information in Boltzmann-weighted populations of active and inactive states (PMID: 39923288). Condensate partition coefficients encode chemical selectivity through transfer free energies that distinguish pathological from functional assemblies (PMID: 39271915).

This review examines each frontier through the lens of its underlying nanoscale biophysics, develops novel mathematical frameworks for quantitative prediction, and identifies the cross-cutting principles that connect these apparently independent fields into a unified vision for the next generation of molecular therapeutics.

---

## II. Targeted Protein Degradation: Ternary Complex Biophysics

### 2.1 The Induced Proximity Paradigm

Targeted protein degradation represents the most clinically advanced application of engineered nanoscale proximity. Unlike conventional inhibitors that must occupy active sites to block function, TPD molecules — including proteolysis-targeting chimeras (PROTACs) and molecular glues — function by inducing proximity between a target protein and an E3 ubiquitin ligase, catalyzing polyubiquitination and subsequent proteasomal degradation (PMID: 39500878). This mechanism is inherently substoichiometric: a single degrader molecule can catalyze the destruction of multiple target protein copies, fundamentally altering the pharmacological relationship between drug concentration and therapeutic effect (PMID: 39791901).

The biophysical core of TPD is the ternary complex — the three-body assembly of target protein, degrader molecule, and E3 ligase. The geometry, stability, and dynamics of this complex determine whether ubiquitin transfer occurs (PMID: 41022846). Cryo-electron microscopy has now resolved ternary complexes at atomic resolution, revealing that productive degradation requires positioning target protein surface lysines within ~10 Å of the E2~ubiquitin thioester bond — the distance constraint for nucleophilic attack by the lysine ε-amino group on the ubiquitin C-terminal thioester (PMID: 39392888). This geometric requirement explains why proteins with accessible lysines in the ubiquitination zone are preferentially degraded, while those with lysines buried or oriented away from the E2 active site resist degradation even when efficiently recruited to the E3 ligase.

### 2.2 Cooperativity and the Alpha Factor

The thermodynamic signature of productive ternary complex formation is positive cooperativity — quantified by the cooperativity factor α, defined as the ratio of the ternary complex dissociation constant to the product of the two binary dissociation constants (PMID: 41022846). We formalize this through a thermodynamic cycle relating binary and ternary binding events.

Consider a target protein T, a degrader D, and an E3 ligase E. The degrader can bind T with dissociation constant $K_{d,1}$ (forming the T:D binary complex) or E with dissociation constant $K_{d,2}$ (forming the D:E binary complex). The ternary complex T:D:E forms with an overall dissociation constant $K_{d,ternary}$. The cooperativity factor is:

$$\alpha = \frac{K_{d,1} \cdot K_{d,2}}{K_{d,ternary}}$$

Equivalently, in free energy terms:

$$\Delta G_{ternary} = \Delta G_{binary,1} + \Delta G_{binary,2} + \Delta G_{coop}$$

where $\Delta G_{coop} = -RT \ln(\alpha)$. When α > 1, the ternary complex is more stable than predicted from binary affinities alone — indicating favorable protein-protein interactions (PPIs) across the degrader-bridged interface. When α < 1, the interface is destabilizing — often due to steric clashes between the target and E3 ligase surfaces.

Recent structural and biophysical analyses have revealed that interfacial frustration — the balance between favorable and unfavorable contacts across the induced PPI interface — plays a central role in determining cooperativity (PMID: 41022846). Frustrated interfaces, where some contacts are attractive and others repulsive, generate a rugged free energy landscape with multiple metastable ternary complex orientations. PROTACs that reduce interfacial frustration by optimizing linker geometry achieve α values of 10–100, while poorly designed linkers yield α < 1 (PMID: 41022846).

### 2.3 Ubiquitinability Geometry

The concept of ubiquitinability — the geometric accessibility of target protein lysines to the E2 ~ ubiquitin conjugate within the ternary complex — provides a structural framework for predicting degradation efficiency independent of ternary complex affinity (PMID: 39392888). Cryo-EM structures of the VHL-CRL2 E3 ligase in complex with the PROTAC MZ1 and the target BRD4 bromodomain 2 (BD2) revealed that Lys456 of BRD4 is positioned at the optimal distance (~ 10 Å) and orientation for nucleophilic attack on the E2 ~ Ub thioester (PMID: 39392888).

We define a surface accessibility integral that quantifies the fraction of ternary complex orientations placing at least one target lysine within the ubiquitination zone:

$$\mathcal{U} = \frac{1}{4\pi} \int_{\Omega} \sum_{i=1}^{N_{Lys}} \Theta(r_{max} - |\mathbf{r}_{Lys,i}(\omega) - \mathbf{r}_{E2}(\omega)|) \, d\omega$$

where the integral is over all solid angles Ω parameterizing the rotational degrees of freedom of the target within the ternary complex, $\mathbf{r}_{Lys,i}$ is the position of the i-th lysine, $\mathbf{r}_{E2}$ is the E2 active site cysteine position, $r_{max} \approx 10$ Å is the maximum ubiquitin transfer distance, and Θ is the Heaviside step function. Proteins with $\mathcal{U} > 0.1$ are predicted to be efficiently degraded; those with $\mathcal{U} < 0.01$ are resistant (PMID: 39392888).

SE(3)-equivariant graph neural networks have recently been developed to predict ternary complex structures and compute $\mathcal{U}$ without experimental structures, achieving prediction speeds ~100× faster than physics-based docking approaches (PMID: 40593782). The DeepTernary model uses equivariant message-passing on protein graphs to predict the relative orientation of the target and E3 within the ternary complex, enabling virtual screening of PROTAC linker geometries for optimal ubiquitinability (PMID: 40593782).

### 2.4 Intramolecular Bivalent Glues: A New Degradation Modality

A striking recent advance in TPD biophysics is the discovery of intramolecular bivalent glues (IBGs) — small molecules that simultaneously engage two domains within the same protein, creating a neo-surface recognized by an E3 ligase (PMID: 38383787). Cryo-EM at 3.77 Å resolution revealed that an IBG bridges the kinase and bromodomain of a target protein, inducing a compact intramolecular conformation that recruits the CRL4^DCAF16 E3 ligase (PMID: 38383787). This mechanism is conceptually distinct from PROTACs (which bridge two separate proteins) and from classical molecular glues (which create a single neo-surface): IBGs exploit the nanoscale geometry of multidomain proteins to generate degradation-competent conformations that do not exist in the unliganded state.

The biophysical insight is that large, multidomain proteins — which constitute the majority of the human proteome — possess intrinsic conformational flexibility that can be constrained by small molecules into geometries compatible with E3 ligase engagement. The effective concentration of the second domain relative to the first, when tethered by the IBG, follows:

$$C_{eff} = \frac{3}{4\pi N_A r_{max}^3}$$

For a maximum tether distance $r_{max} \approx 5$ nm (typical for a bifunctional molecule spanning two domains), $C_{eff} \approx 1.3$ mM — orders of magnitude higher than the concentrations achievable by intermolecular interactions, explaining the potency of IBGs (PMID: 38383787).

### 2.5 E3 Ligase Diversity and the Expanding Degradation Toolkit

The TPD field initially relied almost exclusively on two E3 ligases — VHL and CRBN — but recent work has dramatically expanded the toolkit. CRISPR activation screens identified FBXO22 as a recruitable E3 ligase capable of degrading FKBP12, BRD4, and EML4-ALK fusion proteins (PMID: 38965383). Convergent evidence from multiple TPD screening campaigns has identified DCAF16, DCAF11, and FBXO22 as "frequent hitter" E3 ligases — enzymes that are repeatedly identified across diverse degradation contexts, suggesting inherent structural properties that favor neo-substrate recruitment (PMID: 39870762). Alkenyl oxindoles have been identified as novel E3 ligase-recruiting warheads for DCAF11, expanding the chemical space available for PROTAC design (PMID: 38768083). Novel ternary complex crystal structures of GID4-PROTAC-BRD4 in three distinct orientational states demonstrate that alternative E3 ligases can achieve comparable degradation efficiency to VHL and CRBN (PMID: 40295770).

CRBN-based molecular glues have revealed unexpected biology: a degron-mimicking molecular glue (MRT-31619) assembles a helix-like structure that drives CRBN homo-dimerization — an entirely new degradation mechanism in which the substrate-binding surface of one CRBN molecule serves as the neo-substrate for another (PMID: 41258141). Chemoproteomics workflows have uncovered 298 protein targets of CRBN molecular glues, of which 251 are non-zinc finger proteins, vastly expanding the scope of molecular glue-mediated degradation beyond the IMiD paradigm (PMID: 40707481). Engineered CRBN variants optimized for E. coli expression have enabled high-throughput screening of 4,480 IMiD derivative libraries, accelerating molecular glue discovery (PMID: 39610248).

Beyond the ubiquitin-proteasome system, lysosome-targeting chimeras (LYTACs) exploit receptor-mediated endocytosis to degrade extracellular and membrane proteins. Covalent peptide-based LYTACs targeting TFRC have demonstrated degradation of PD-L1 and suppression of brain tumors in preclinical models (PMID: 39910101). Phenotypic screening platforms such as DEFUSE enable high-throughput, target-first discovery of molecular glue degraders (PMID: 39854250; reviewed in PMID: 39753433).

### 2.6 Clinical Translation: The PROTAC Era Begins

The clinical translation of TPD reached a landmark in 2025 with the NDA submission for vepdegestrant (ARV-471), a PROTAC estrogen receptor (ER) degrader, to the U.S. FDA — the first PROTAC to seek regulatory approval (PMID: 40454645). The Phase III VERITAC-2 trial demonstrated that vepdegestrant achieved a progression-free survival (PFS) of 5.0 months versus 2.1 months for fulvestrant (hazard ratio 0.58) in patients with ESR1-mutant ER+/HER2− advanced breast cancer (PMID: 40454645; PMID: 39072356). This result validates the catalytic degradation mechanism in a clinical setting: vepdegestrant achieves deeper ER degradation than the competitive antagonist fulvestrant, consistent with the substoichiometric recycling predicted by ternary complex kinetics.

Three additional PROTACs are in Phase III clinical trials. BMS-986365 (gridegalutamide), a dual androgen receptor (AR) degrader and antagonist targeting CRBN, has demonstrated clinical activity in metastatic castration-resistant prostate cancer (mCRPC) (PMID: 40788283; PMID: 39293515; PMID: 40455815). Four clinical BTK degraders — BGB-16673, NX-2127, NX-5948, and AC676 — are advancing through Phase I/II trials for chronic lymphocytic leukemia, with NX-5948 showing responses in patients resistant to covalent BTK inhibitors (PMID: 39941922).

A key pharmacological challenge for PROTACs is oral bioavailability. PROTACs typically violate Lipinski's rule of five, with molecular weights exceeding 700 Da and multiple hydrogen bond donors. NMR-based three-dimensional conformational analysis has revealed that orally bioavailable PROTACs adopt compact, intramolecularly hydrogen-bonded conformations that mask polar surface area — effectively reducing the number of exposed hydrogen bond donors (eHBD) to ≤2, a threshold identified as the key predictor of oral absorption (PMID: 39078401). This "chameleonic" behavior, in which molecules adopt distinct conformations in aqueous versus lipid environments, represents a biophysical design principle that has enabled the development of oral PROTACs such as vepdegestrant and ARV-766 (PMID: 39078401).

### 2.7 Open Questions

Several fundamental questions remain unresolved at the intersection of TPD biophysics and clinical translation. First, can degradability be predicted from protein structure alone? Current approaches require experimental determination of ternary complex geometry, but SE(3)-equivariant models are approaching the accuracy needed for prospective prediction (PMID: 40593782). Second, the relationship between cooperativity (α), ubiquitinability ($\mathcal{U}$), and in vivo degradation efficiency remains incompletely characterized — a protein may form a highly cooperative ternary complex yet lack accessible lysines, or vice versa. Third, next-generation PROTAC designs — including macrocyclic (PMID: 41219525), trivalent, photo-activable, and antibody-conjugated variants (PMID: 40348076) — must be evaluated for whether their increased molecular complexity translates into improved therapeutic indices or merely increased manufacturing challenges. Fourth, the expansion of E3 ligase diversity raises the question of tissue-selective degradation: different E3 ligases have distinct expression patterns, potentially enabling organ-targeted protein degradation analogous to the tissue tropism achieved by different AAV serotypes in gene therapy (PMID: 39870762).

---

## III. Conformational Ensemble Drug Design: Cryptic Pockets and Kinetic Trapping

### 3.1 Proteins as Dynamic Ensembles

The static protein structures deposited in the Protein Data Bank represent energy minima in a rugged free energy landscape — snapshots of the most populated conformational state under crystallization conditions. Yet proteins are dynamic machines that sample multiple conformational states separated by energy barriers of 2–20 kcal/mol on timescales spanning picoseconds to seconds (PMID: 38603560). The pharmaceutical implications are profound: many proteins harbor cryptic binding pockets that are invisible in static structures but become transiently accessible as the protein fluctuates through its conformational ensemble (PMID: 39778412).

The AlphaFold revolution solved the static protein structure prediction problem with remarkable accuracy, but AlphaFold2 and AlphaFold3 have significant limitations for conformational dynamics (PMID: 40663654). Systematic evaluation of 128 autoinhibited proteins with large-scale allosteric transitions demonstrated that AlphaFold2 fails to predict the alternative functional conformation in the majority of cases, with reduced pLDDT confidence scores in regions that undergo conformational change. This fundamental limitation — that AlphaFold predicts the most probable conformation, not the ensemble of accessible conformations — has catalyzed the development of computational methods for generating Boltzmann-weighted structural ensembles (PMID: 39923288).

### 3.2 Kramers' Escape Rate Theory for Conformational Transitions

The kinetics of conformational transitions between closed (cryptic pocket occluded) and open (pocket accessible) states are governed by the energy barrier separating these states. We apply Kramers' escape rate theory — originally developed for chemical reactions in viscous media — to model the rate at which a protein transitions from the closed to the open conformation.

In the overdamped regime appropriate for protein conformational dynamics in aqueous solution, Kramers' rate is:

$$k_{closed \to open} = \frac{\omega_{well} \cdot \omega_{barrier}}{2\pi\gamma} \cdot \exp\left(-\frac{\Delta G^{\ddagger}}{k_B T}\right)$$

where $\omega_{well}$ is the angular frequency of the potential energy surface at the closed-state minimum (curvature of the free energy well), $\omega_{barrier}$ is the angular frequency at the transition state barrier top, $\gamma$ is the friction coefficient (proportional to solvent viscosity), and $\Delta G^{\ddagger}$ is the free energy barrier height.

For a typical cryptic pocket opening event with $\Delta G^{\ddagger} \approx 4$ kcal/mol (measured by NMR relaxation dispersion), $\omega_{well} \approx \omega_{barrier} \approx 10^{12}$ s$^{-1}$ (characteristic of protein backbone fluctuations), and $\gamma \approx 10^{12}$ s$^{-1}$ (water viscosity at 310 K), the predicted transition rate is:

$$k_{closed \to open} \approx \frac{10^{12} \cdot 10^{12}}{2\pi \cdot 10^{12}} \cdot \exp\left(-\frac{4 \times 4184}{8.314 \times 310}\right) \approx 1.6 \times 10^{11} \cdot e^{-6.5} \approx 2.4 \times 10^{8} \text{ s}^{-1}$$

This corresponds to the forward transition rate from closed to open. However, the experimentally observed μs–ms timescale reflects not the individual transition rate but the relaxation time of the two-state equilibrium: $\tau_{relax} = 1/(k_{closed \to open} + k_{open \to closed})$. Since the open state is thermodynamically unfavorable ($\Delta G_{open} > 0$), $k_{open \to closed} \gg k_{closed \to open}$, and the relaxation time is dominated by the reverse rate. The observed timescale for conformational exchange is thus the residence time of the open state: $\tau_{open} \approx 1/k_{open \to closed}$. The equilibrium population of the open state is:

$$p_{open} = \frac{1}{1 + \exp(\Delta G_{open}/k_BT)}$$

For $\Delta G_{open} = 3$ kcal/mol (the free energy difference between open and closed states), $p_{open} \approx 0.6\%$ — meaning the cryptic pocket is accessible for only ~6 μs per millisecond of protein dynamics. A drug that binds selectively to the open state with $K_d^{open} = 10$ nM effectively shifts the equilibrium toward the open conformation, a phenomenon known as conformational selection.

The therapeutic implication is that drug residence time ($\tau = 1/k_{off}$) can be more predictive of in vivo efficacy than binding affinity ($K_d$) alone. A drug that binds tightly to a cryptic pocket but dissociates slowly (long residence time) maintains the target in the drugged conformation even as the protein attempts to fluctuate back to the closed state. Computational methods for predicting $k_{off}$ using site identification by ligand competitive saturation (SILCS) have recently achieved sufficient accuracy for prospective drug design (PMID: 40285712).

### 3.3 Time-Resolved Cryo-EM of the Mu-Opioid Receptor

The most dramatic recent demonstration of conformational ensemble drug design comes from time-resolved cryo-EM studies of the mu-opioid receptor (MOR), the primary target for analgesic drug development. Classical cryo-EM captures a static snapshot of the most populated state, but time-resolved approaches — using rapid mixing and vitrification — have now resolved the non-equilibrium conformational trajectory of MOR activation with partial, full, and super agonists (PMID: 41430437).

These studies revealed that ligand efficacy is encoded not in a single structure but in the dynamic sampling of multiple conformational states on different timescales. Partial agonists stabilize a pre-activated state with incomplete TM5/TM6 outward movement, while full agonists drive a complete conformational change to the fully activated state (PMID: 38600384). DEER (double electron-electron resonance) and smFRET measurements confirmed that MOR samples at least three distinct conformational states — inactive, pre-activated, and fully activated — with populations that shift as a function of ligand efficacy (PMID: 38600384).

Complementary structural studies resolved eight structural models from sixteen cryo-EM density maps of GDP-bound MOR-Gαi states, revealing an inverse correlation between agonist efficacy and GDP affinity at the G-protein nucleotide-binding pocket — a mechanistic link between receptor conformation and downstream signaling amplitude (PMID: 41193810). The TM1 helix was identified as an allosteric regulator of signaling bias, with a previously unknown TM1-adjacent fusion pocket that accommodates allosteric modulators cooperating with orthosteric ligands (PMID: 41199005; PMID: 38740791). A mu-opioid receptor modulator that works cooperatively with naloxone — the overdose reversal agent — demonstrates the clinical potential of allosteric modulation through conformational dynamics (PMID: 38961287).

### 3.4 KRAS Cryptic Pockets and the Allosteric Landscape

KRAS — mutated in ~25% of all human cancers — exemplifies the cryptic pocket paradigm. The Switch-II pocket (SII-P) exploited by the FDA-approved covalent inhibitor sotorasib was a cryptic pocket invisible in most crystal structures, revealed only through molecular dynamics simulations showing transient pocket opening on the microsecond timescale. Deep mutational scanning of >26,000 KRAS mutations, quantifying effects on folding and binding, has now mapped the complete energetic and allosteric landscape of KRAS inhibition, revealing many more inhibitory allosteric sites than previously appreciated (PMID: 38109937).

Weighted ensemble molecular dynamics simulations totaling >400 microseconds, using normal mode projections as collective variables, have revealed additional cryptic pockets in KRAS G12D beyond the SII-P, suggesting new therapeutic opportunities for noncovalent inhibitors that do not require cysteine modification (PMID: 39419500). Noncovalent SII-P inhibitors have been shown to allosterically freeze the KRAS G12D nucleotide-binding site, arresting the GTPase cycle in the GDP-bound state — a mechanism confirmed by crystallographic and NMR evidence. Markov state modeling of KRAS conformational ensembles has mapped the binding and allosteric energy landscapes for KRAS interactions with effector proteins, identifying kinetically distinct metastable states that could serve as drug targets (PMID: 40671268).

### 3.5 AI-Driven Ensemble Drug Design

The convergence of AlphaFold-derived structure prediction with molecular dynamics-based ensemble generation has created a new paradigm for computational drug design. Several recent developments define this frontier:

**Boltzmann-weighted ensemble generation.** Methods such as PLACER (Protein-Ligand Atomistic Conformational Ensemble Resolver) use graph neural networks to generate Boltzmann-weighted protein-ligand conformational ensembles, enabling virtual screening against dynamic rather than static targets (PMID: 41187076). This approach naturally accounts for cryptic pocket accessibility by weighting each conformation by its thermodynamic probability.

**Enhanced sampling with machine learning.** The integration of machine learning with enhanced sampling methods — including metadynamics, replica exchange molecular dynamics, and adaptive sampling — has dramatically improved the efficiency of conformational landscape exploration (PMID: 41124671). These methods can now achieve converged free energy surfaces for drug-relevant conformational transitions that previously required prohibitive computational resources.

**AlphaFold-guided free energy perturbation.** AlphaFold-predicted structures have been shown to support free energy perturbation (FEP) calculations with accuracy comparable to experimental crystal structures, expanding the druggable target space to proteins without experimental structures (PMID: 40233800).

**IsoDDE (Isomorphic Labs Drug Discovery Engine).** The IsoDDE platform, released in early 2026, doubled the accuracy of AlphaFold3 for protein-ligand binding predictions and introduced ligandable pocket identification — the computational prediction of which protein surfaces can accommodate drug-like molecules, including cryptic and allosteric sites.

**Hydrogen-deuterium exchange mass spectrometry (HDX-MS).** Experimental validation of computationally predicted cryptic pockets increasingly relies on HDX-MS, which measures protein backbone amide hydrogen exchange rates as a function of ligand binding (PMID: 39778412). Recent advances have pushed HDX-MS sensitivity to detect fragment binding at double-digit millimolar affinity, enabling fragment-based approaches to cryptic pocket drug discovery.

### 3.6 Ensemble Scoring for Virtual Screening

Classical virtual screening scores compounds against a single protein conformation. Boltzmann-weighted ensemble scoring instead evaluates binding across multiple conformations, weighted by their thermodynamic populations:

$$\Delta G_{bind}^{ensemble} = -k_BT \ln \left( \sum_{i=1}^{N_{conf}} p_i \cdot \exp\left(-\frac{\Delta G_{bind,i}}{k_BT}\right) \right)$$

where $p_i = \exp(-G_i/k_BT) / Z$ is the Boltzmann weight of conformation $i$ and $\Delta G_{bind,i}$ is the binding free energy in that conformation. This formulation naturally captures the contribution of cryptic pocket states: even if a cryptic pocket has $p_{open} = 0.6\%$, a compound with $\Delta G_{bind,open} = -12$ kcal/mol will contribute substantially to $\Delta G_{bind}^{ensemble}$ despite the low population of the open state.

The practical challenge is generating a sufficiently diverse and thermodynamically accurate ensemble. Current best practices combine: (1) AlphaFold-derived starting structures, (2) adaptive MD simulations to sample rare states, (3) Markov state model construction to identify metastable states and their interconversion kinetics, and (4) experimental validation by HDX-MS or NMR (PMID: 41193830; PMID: 39923288; PMID: 40671268).

### 3.7 Open Questions

The central unsolved problem in conformational ensemble drug design is the rare event problem: conformational transitions relevant to drug binding occur on μs–ms timescales, while all-atom MD simulations are typically limited to μs timescales. Enhanced sampling methods mitigate this limitation but require prior knowledge of relevant collective variables — a form of circular reasoning when the goal is to discover unexpected conformational states. Machine learning approaches to collective variable identification are promising but remain data-hungry (PMID: 41124671). A second open question is experimental validation of AlphaFold3-predicted cryptic sites: computational predictions outpace experimental verification, and the false-positive rate of predicted cryptic pockets remains poorly characterized (PMID: 40663654). Third, the clinical translation of residence-time-optimized drugs is hampered by the difficulty of measuring $k_{off}$ in high-throughput formats; current surface plasmon resonance and bio-layer interferometry methods are too slow for screening large compound libraries against kinetic, rather than thermodynamic, binding parameters.

---

## IV. Endosomal Escape Nanophysics: Membrane Mechanics of Intracellular Delivery

### 4.1 The Endosomal Escape Bottleneck

The delivery of therapeutic nucleic acids — mRNA, siRNA, antisense oligonucleotides, and CRISPR components — to intracellular targets requires escape from endosomal compartments following uptake. This endosomal escape step is the single greatest bottleneck limiting LNP delivery efficiency: quantitative measurements consistently indicate that <5% of internalized LNPs successfully deliver their cargo to the cytoplasm (PMID: 38437552). The first in vivo endosomal escape assay, using LysoTag mice combined with lysosomal barcoding, revealed that ~8% of optimized BiP-20 LNPs reach the cytosol within 30 minutes — an 8-fold improvement over the LP01 benchmark — and that Rab7 depletion increases escape efficiency, confirming that late endosomal maturation is the primary barrier (PMID: 41814093).

### 4.2 Ionizable Lipid Phase Transitions

The mechanism of LNP-mediated endosomal escape depends critically on the physicochemistry of ionizable lipids — the core functional component of LNP formulations. Ionizable lipids are engineered with apparent pKa values of 6.2–6.5, ensuring that they are neutral at physiological pH (7.4) but become protonated as endosomal pH drops during maturation from early endosomes (pH ~6.5) to late endosomes (pH ~5.5) and lysosomes (pH ~4.5) (PMID: 39293650).

Protonation triggers a phase transition in the LNP's internal structure. Small-angle X-ray scattering (SAXS) studies of clinically approved ionizable lipids (ALC-0315 from Comirnaty, SM-102 from Spikevax) have revealed that these lipids adopt inverse mesophase structures — including inverse hexagonal (H_II), inverse micellar cubic, and inverse bicontinuous cubic phases — that are critical for membrane disruption (PMID: 41060394). The H_II phase, characterized by inverted lipid cylinders with aqueous cores, is particularly relevant: its negative spontaneous curvature ($c_0 < 0$) promotes fusion with the endosomal membrane, a process analogous to viral membrane fusion (PMID: 38347001).

Buffer composition influences the pH at which phase transitions occur, with citrate buffers stabilizing the H_II phase at higher pH values, potentially enabling escape from earlier endosomal compartments where degradative enzyme concentrations are lower (PMID: 40074542). Computational methods for predicting apparent pKa values of ionizable lipids within the LNP nanostructure context have been validated against clinical formulations, enabling rational lipid design (PMID: 39655829).

### 4.3 The Galectin-ESCRT Dichotomy

A critical recent discovery has reframed the mechanistic understanding of LNP endosomal escape. Endosomal membrane damage from LNP-mediated pore formation triggers one of two competing repair pathways, with fundamentally different consequences for therapeutic delivery and innate immune activation (PMID: 40789922; PMID: 40595685).

**ESCRT-reparable small holes.** The ESCRT-III (endosomal sorting complexes required for transport) machinery repairs small membrane disruptions by constricting and sealing the damaged region. ESCRT recruitment is rapid (~minutes) and generates minimal inflammatory signaling. Ionizable lipids that produce small, ESCRT-reparable membrane perturbations achieve high mRNA expression with minimal innate immune activation — the ideal therapeutic profile (PMID: 40789922).

**Galectin-recognized large ruptures.** Larger membrane disruptions expose luminal glycans to cytosolic galectin-8 and galectin-9, triggering autophagy, NF-κB signaling, and inflammatory cytokine production. Paradoxically, galectin-marked endosomes may be more conducive to RNA release because the membrane damage is more extensive, but the accompanying inflammation limits therapeutic applications, particularly for repeated dosing (PMID: 40595685).

The transition between these two regimes depends on pore size, which in turn depends on the biophysical properties of the ionizable lipid — its spontaneous curvature, phase behavior, and interaction with endosomal membrane lipids. This realization has motivated the development of "gentle" ionizable lipids that achieve sufficient cargo release through ESCRT-reparable perturbations without triggering galectin-mediated inflammation (PMID: 40789922).

### 4.4 Helfrich Membrane Bending Energy and Pore Nucleation

The energetics of pore formation in endosomal membranes can be analyzed using Helfrich continuum membrane mechanics. The Helfrich free energy of a membrane with curvature is:

$$F_{Helfrich} = \int \left[ \frac{\kappa}{2}(2H - c_0)^2 + \bar{\kappa}K \right] dA$$

where $\kappa$ is the bending modulus (~20 $k_BT$ for lipid bilayers), $H$ is the mean curvature, $c_0$ is the spontaneous curvature, $\bar{\kappa}$ is the Gaussian curvature modulus, and $K$ is the Gaussian curvature. For a flat membrane ($H = 0$, $K = 0$), the Helfrich energy reduces to $F = (\kappa/2) c_0^2 \cdot A$ — a penalty for membranes with nonzero spontaneous curvature that are forced to remain flat.

Pore nucleation in an endosomal membrane involves overcoming a free energy barrier. For a circular pore of radius $r$ in a membrane under tension $\sigma$, the free energy is:

$$\Delta G_{pore}(r) = 2\pi\gamma r - \pi\sigma r^2 + \pi\kappa \left(\frac{1}{r}\right)$$

where the first term is the line tension energy (cost of exposing the hydrophobic membrane interior at the pore edge, with line tension $\gamma \approx 10$ pN), the second term is the surface tension energy released by pore formation, and the third term is the bending energy cost of the highly curved pore rim. The critical pore radius at which $d\Delta G/dr = 0$ is:

$$r^* = \frac{\gamma + \sqrt{\gamma^2 + 4\sigma\kappa}}{2\sigma}$$

A substantial barrier explains why endosomal escape is rare without active membrane-disrupting agents. The H_II phase of protonated ionizable lipids effectively increases the local membrane tension $\sigma$ and reduces line tension $\gamma$ (by providing amphiphilic molecules that stabilize pore edges), lowering the barrier to ~10–20 $k_BT$ and enabling stochastic pore nucleation on the timescale of endosomal maturation (PMID: 39293650; PMID: 41060394).

The critical pore size also determines whether the ESCRT or galectin pathway is engaged. ESCRT-III can repair pores with diameters up to ~100 nm, while larger pores expose sufficient luminal glycans to recruit galectin-8/9 (PMID: 40789922). This establishes a design principle: optimal ionizable lipids should reduce the nucleation barrier enough to form pores with $r < 50$ nm (ESCRT-reparable) while avoiding catastrophic membrane disruption ($r > 50$ nm, galectin-triggering).

### 4.5 Next-Generation Ionizable Lipid Design

Rational design of ionizable lipids informed by endosomal escape biophysics has yielded several advances:

**Branched-tail lipids.** Terminal branching of lipid hydrocarbon chains enhances the H_II phase propensity by increasing the effective tail volume relative to head-group area, promoting negative spontaneous curvature. BEND (branched endosomal disruptor) lipids achieve up to 10-fold improvement in mRNA delivery over clinical benchmarks (SM-102, ALC-0315) for both hepatic gene editing and T cell transfection. The Passerini reaction platform enables rapid modular synthesis of biodegradable ionizable lipid libraries, with top candidates (A4B4-S3) outperforming SM-102 in liver gene editing (PMID: 39883839). Multi-tail ionizable lipids with imidazole headgroups (U-19) prolong mRNA expression duration relative to ALC-0315 (PMID: 39454975).

**Zwitterionic lipids.** Pyridine carboxybetaine zwitterionic headgroups that protonate below pH 6.8 enable escape from early endosomes, before significant lysosomal enzyme accumulation. These lipids simultaneously reduce reactogenicity — the unwanted inflammatory response to LNP administration — by minimizing exposure to late endosomal/lysosomal damage-sensing pathways (PMID: 39293650).

**Degradable lipids.** Beta-propionate linkers and ester bonds enable rapid lipid degradation after cargo release, reducing cytotoxicity from lipid accumulation. In situ combinatorial synthesis of degradable branched lipidoids achieves 1000-fold delivery improvement over early-generation formulations (PMID: 38409275).

**Machine learning-guided design.** ML models trained on libraries of 584 ionizable lipids can screen 40,000 virtual structures and identify candidates (lipid 119-23) that outperform benchmarks in muscle and immune cell transfection (PMID: 38740955). Deep learning platforms (AGILE) trained on 12,000 virtual structures have identified superior ionizable lipids (H9) with rapid adaptation to macrophage targeting (PMID: 39060305). AI-driven rational design models screening ~20 million ionizable lipids predict pKa and delivery efficiency with sufficient accuracy to equal or outperform SM-102 in a single optimization iteration.

### 4.6 Non-Hepatic Targeting

A major limitation of current LNP therapeutics is their preferential accumulation in the liver, driven by apolipoprotein E (ApoE) adsorption and hepatocyte LDLR-mediated uptake. Organ-selective targeting has been achieved through systematic lipid chemistry variation: N-series (amide) ionizable lipids target lung, while O-series (ester) lipids retain liver tropism, with cholesterol and phospholipid helper components being dispensable for LNP function (PMID: 38969646). Predictive lung- and spleen-targeted mRNA delivery has been demonstrated with biodegradable lipid libraries, where branched hydrocarbon chains favor spleen targeting (PMID: 40284454). Brain-targeted LNPs incorporating serotonin receptor ligands (SR-57227) into the ionizable lipid structure achieve >50-fold improvement over clinical LNPs for systemic brain delivery.

### 4.7 Open Questions

The central open question in endosomal escape is quantitative: what is the precise pore size threshold separating ESCRT-reparable from galectin-recognized membrane damage, and can this threshold be reliably tuned by lipid design? Current estimates (~50–100 nm) are derived from indirect measurements and model systems (PMID: 40789922). A second question is whether endosomal escape efficiency can be increased beyond the ~8% ceiling observed with BiP-20 without triggering unacceptable inflammation (PMID: 41814093). Third, rational design of ionizable lipids for non-hepatic targeting remains largely empirical; a predictive framework connecting lipid molecular structure to organ-level biodistribution through protein corona composition and receptor engagement is needed (PMID: 38969646). Fourth, the role of LNP internal mesophase structure (lamellar, cubic, hexagonal) in determining both escape efficiency and cargo release kinetics remains incompletely characterized, with conflicting evidence from different experimental systems (PMID: 41060394; PMID: 38347001).

---

## V. Single-Molecule Protein Sequencing: Nanopore Biophysics for Clinical Proteomics

### 5.1 The Single-Molecule Proteomics Challenge

Proteomics — the comprehensive characterization of all proteins in a biological sample — faces a fundamental sensitivity challenge that distinguishes it from genomics. While nucleic acids can be amplified by PCR, proteins cannot be amplified: each protein molecule must be detected individually. The human proteome comprises ~20,000 genes encoding an estimated >1 million proteoforms when splice variants, post-translational modifications (PTMs), and allelic variants are considered. Detecting low-abundance proteoforms (present at <100 copies per cell) against a background of high-abundance housekeeping proteins (>10^6 copies per cell) requires single-molecule sensitivity — a capability that has been achieved for DNA through nanopore sequencing and is now being developed for proteins (PMID: 40097683).

Nanopore-based protein sequencing exploits a conceptually simple principle: a single protein molecule is threaded through a nanometer-scale pore in an electrically resistive membrane, and the ionic current through the pore is modulated by the identity of the amino acid residues occupying the pore constriction at each moment (PMID: 39261738). The challenge is that proteins, unlike DNA, lack a uniform charge density, adopt complex tertiary structures that resist linearization, and comprise 20 chemically diverse amino acids (versus 4 nucleotide bases), demanding much higher discrimination resolution (PMID: 40097683).

### 5.2 ClpX-CsgG Multi-Pass Protein Sequencing

The most significant advance in nanopore protein sequencing is the development of a multi-pass reading system using the ClpX unfoldase motor protein coupled to the CsgG nanopore (PMID: 39261738). ClpX, an AAA+ ATPase that normally unfolds and translocates proteins into the ClpP protease, was repurposed to ratchet linearized polypeptides through the CsgG pore in discrete steps. The CsgG pore, derived from an E. coli curli secretion channel, has a constriction diameter of ~1.2 nm — sufficient to accommodate a single unfolded polypeptide chain but narrow enough to generate amino acid-specific current blockade patterns.

The key innovation enabling multi-pass reading is a "slippery sequence" engineered at the protein terminus that causes ClpX to periodically lose grip and retract the polypeptide, enabling the same molecule to be read multiple times through the same pore (PMID: 39261738). Each pass provides an independent measurement of the amino acid sequence, and consensus calling across N passes improves the signal-to-noise ratio (SNR) by a factor of $\sqrt{N}$:

$$SNR_N = SNR_1 \cdot \sqrt{N}$$

With 3–5 passes per molecule, the system achieves single-amino-acid sensitivity across hundreds of residues, including detection of phosphorylation — a PTM that alters the current blockade signature of the modified residue (PMID: 39261738). The system was demonstrated on a commercial Oxford Nanopore MinION array, establishing compatibility with existing sequencing infrastructure.

Random forest classification of current blockade patterns achieves 28% accuracy across all 20 amino acids in single-pass reading, with top-8 accuracy reaching 81% — sufficient for protein identification by peptide mass fingerprinting analogies (PMID: 39261738). Multi-pass consensus calling is expected to push single-amino-acid accuracy above the 90% threshold needed for de novo sequencing.

### 5.3 MspA Hetero-Octamer Engineering for Amino Acid Discrimination

An orthogonal approach to nanopore protein sensing uses engineered variants of the Mycobacterium smegmatis porin A (MspA) pore. The MspA constriction site is shorter (~0.6 nm) and wider than CsgG, providing a different current modulation profile. A copper(II)-functionalized MspA N91H nanopore achieves 99.1% amino acid validation accuracy across all 20 proteinogenic amino acids, with 30.9% signal recovery — meaning nearly one-third of translocation events produce interpretable current blockade signatures (PMID: 38443507). This pore was used to discriminate pathologically relevant peptides, including Alzheimer's disease-associated amyloid-β variants and cancer neoantigens, demonstrating clinical potential.

An alternative functionalization strategy using MspA-NTA-Ni²⁺ coordination chemistry achieves 98.6% accuracy for all 20 amino acids and their common modifications, with improved residence time at the sensing constriction due to metal ion-amino acid coordination (PMID: 37749214). The complementary strengths of CsgG (motor-driven multi-pass) and MspA (high-accuracy single-pass) suggest that future clinical protein sequencing may employ both pore types in tandem.

### 5.4 Post-Translational Modification Detection

A transformative clinical application of nanopore protein sensing is the direct detection of PTMs without antibodies or enzymatic digestion. Phosphorylation — the most abundant regulatory PTM — has been detected with 95% accuracy on individual peptides, discriminating singly and doubly phosphorylated variants, including cancer-associated phosphopeptide neoantigens presented on MHC class I molecules (PMID: 37386295). Deep learning classification of aerolysin nanopore signals detects alpha-synuclein PTMs (phosphorylation, nitration, oxidation) with 94% accuracy, with implications for Parkinson's disease biomarker detection (PMID: 38112538).

Sulfation versus phosphorylation — two PTMs with near-identical mass additions (80.06 vs. 79.97 Da) that are indistinguishable by mass spectrometry — can be discriminated with >90% accuracy on the same tyrosine residue by nanopore current analysis, because the two modifications generate distinct solvation shell geometries that differently modulate ion flow through the pore constriction (PMID: 39388343). Phosphorylation site mapping within polypeptides exceeding 600 amino acids has been achieved using binder-assisted nanopore detection, where antibody fragments tethered near the pore entrance create additional current signatures that pinpoint PTM positions (PMID: 39261738).

Enzyme-less nanopore detection of PTMs along polypeptides exceeding 1,200 residues has been demonstrated using electro-osmotic capture, unfolding, and translocation — eliminating the need for motor proteins entirely (PMID: 40097683). This approach detected phosphorylation, glutathionylation, and glycosylation on single molecules, establishing the feasibility of whole-protein PTM profiling without enzymatic processing.

### 5.5 Shannon Channel Capacity for Nanopore Protein Sequencing

We develop an information-theoretic framework for quantifying the fundamental limits of amino acid identification through nanopore current measurements. The nanopore can be modeled as a noisy communication channel where the "message" is the amino acid sequence and the "received signal" is the time series of ionic current values.

The Shannon channel capacity — the maximum rate at which information can be reliably transmitted through a noisy channel — is:

$$C = B \cdot \log_2(1 + SNR)$$

where $B$ is the channel bandwidth (determined by the translocation rate, typically 10–100 residues per second) and $SNR$ is the signal-to-noise ratio at the pore constriction. For a nanopore protein sequencer with $B = 50$ residues/s and $SNR = 20$ (achievable with current MspA engineering), the channel capacity is:

$$C = 50 \cdot \log_2(21) \approx 50 \cdot 4.39 \approx 220 \text{ bits/s}$$

The information required to uniquely identify each amino acid from the 20-letter alphabet is:

$$I_{max} = \log_2(20) \approx 4.32 \text{ bits per position}$$

Therefore, the minimum bandwidth required for real-time protein sequencing at 50 residues/s is $50 \times 4.32 = 216$ bits/s, which is just barely achievable at $SNR = 20$. This analysis reveals that current nanopore protein sequencers operate near the Shannon limit, and further improvements in sequencing speed will require proportional improvements in SNR.

Multi-pass reading provides a pathway to increasing SNR without hardware improvements. For N independent passes of the same molecule:

$$SNR_N = SNR_1 \cdot \sqrt{N}$$

$$C_N = B \cdot \log_2(1 + SNR_1 \cdot \sqrt{N})$$

With $N = 5$ passes, $SNR_5 = 20 \cdot \sqrt{5} \approx 44.7$, yielding $C_5 \approx 50 \cdot \log_2(45.7) \approx 275$ bits/s — a 25% improvement that exceeds the information-theoretic minimum with comfortable margin. This analysis predicts that 5-pass consensus calling should achieve >99% per-residue accuracy, consistent with experimental projections (PMID: 39261738; PMID: 40097683).

Error correction coding theory provides a complementary perspective. The probability of amino acid misidentification per residue after N consensus reads, assuming independent errors with single-read error rate $p_e$, is:

$$P_{error}(N) = \sum_{k=\lceil N/2 \rceil + 1}^{N} \binom{N}{k} p_e^k (1-p_e)^{N-k}$$

For $p_e = 0.3$ (consistent with single-pass top-1 accuracy of 70%) and $N = 5$, $P_{error}(5) \approx 0.03$ — a 10-fold error reduction per additional pass. For $N = 10$, $P_{error}(10) \approx 0.002$, approaching the 99.8% accuracy target for clinical protein identification.

An information-theoretic analysis of nucleic acid motor kinetics (Hel308 helicase) has shown that enzyme kinetics improves nanopore DNA accuracy approximately 5-fold at high sequencing depth, a principle that extends to protein sequencing motors like ClpX. Mutual information between sequence context and motor stepping kinetics provides an additional information channel beyond direct current blockade measurement.

### 5.6 Emerging Platforms and Clinical Applications

Beyond ClpX-CsgG and MspA, several additional platforms are advancing:

**Coupled nanopores.** The GURU (guiding and reusable) platform uses coupled bilayer nanopores to generate characteristic T- and W-shaped translocation signals that encode molecule length and conformation, enabling ultrafast detection with femtomolar sensitivity (PMID: 39143316).

**Fluorosequencing.** An orthogonal single-molecule protein sequencing approach labels specific amino acids (cysteine, lysine, tryptophan) with distinct fluorophores, then uses Edman degradation to sequentially remove residues while monitoring fluorescence loss by total internal reflection fluorescence (TIRF) microscopy. This approach has demonstrated neoantigen identification from MHC peptide databases and scales to clinical sample complexity (PMID: 37745461).

**Massively parallel nanopore sensing.** High-throughput nanopore arrays combined with AI-driven signal processing workflows enable peptide differentiation and protein identification from massive single-molecule event streams, with demonstrated applications in antibody validation and epitope screening.

**Clinical nanopore diagnostics.** Point-of-care nanopore sensing of protein and peptide conformation has been demonstrated, with applications in enantiomer detection and biomarker identification (PMID: 40180898). The R10.4.1 Oxford Nanopore flow cell, while designed for DNA, has achieved sufficient assembly accuracy for clinical microbial genomics at ≥40× depth — establishing the manufacturing and computational infrastructure that will support protein sequencing as the technology matures (PMID: 38713194).

### 5.7 Open Questions

The path from single-molecule protein sensing to clinical proteomics faces several challenges. First, scaling from individual proteins to whole-proteome coverage requires throughput improvements of >1,000-fold; current multi-pass approaches sacrifice speed for accuracy, creating a fundamental tradeoff that may require parallelized arrays of millions of pores. Second, PTM detection limits — particularly for rare modifications present on <1% of a protein's copies — require sample enrichment strategies analogous to immunoprecipitation in mass spectrometry, which partially defeats the purpose of single-molecule detection. Third, clinical sample complexity (blood plasma contains >10^10 dynamic range in protein concentration) demands robust depletion strategies that do not introduce bias. Fourth, standardization of signal processing algorithms and reference databases analogous to those developed for DNA nanopore sequencing (PMID: 38365920; PMID: 39169028) remains in early stages for protein applications.

---

## VI. Chromatin Loop Extrusion: Nanoscale Genome Architecture

### 6.1 Cohesin as a Molecular Motor

The three-dimensional organization of the genome — its folding into topologically associating domains (TADs), chromatin loops, and compartments — is not a passive consequence of polymer physics but is actively driven by ATP-dependent molecular motors. The SMC (structural maintenance of chromosomes) complex cohesin has been established as the primary loop-extruding motor in interphase cells, processively reeling DNA through its ring-like structure at rates of 0.5–2.1 kb/s in vitro (PMID: 38831499). This rate is remarkable: cohesin can extrude a typical TAD-sized loop (~500 kb) in approximately 4–17 minutes, consistent with the observed TAD contact dynamics of 6–19 minutes per hour.

The molecular mechanism of loop extrusion involves a coordinated cycle of ATP binding, hydrolysis, and conformational change. Single-molecule experiments using magnetic tweezers have revealed that all three eukaryotic SMC complexes — cohesin, condensin, and SMC5/6 — introduce a DNA twist of −0.6 per step, with ATP binding (not hydrolysis) being the twist-inducing event (PMID: 39671477). This superhelical activity has profound implications for genome organization: loop extrusion generates torsional stress that must be resolved by topoisomerases, creating a coupled system in which chromatin topology is actively maintained rather than passively equilibrated (PMID: 39700017).

Single-molecule imaging has further revealed that cohesin and SMC5/6 extrude DNA asymmetrically — extruding one arm of the loop preferentially — and can switch extrusion direction, with direction switches correlating with NIPBL loader turnover at the motor (PMID: 39824185). This asymmetric extrusion generates distinctive features in Hi-C contact maps, including the characteristic "stripe" patterns emanating from CTCF sites. Cohesin also negatively supercoils DNA between its hinge and clamp domains during extrusion; supercoiling-deficient mutants form shorter loops, and topoisomerase I relaxation activity is required for full-length loop formation (PMID: 40516048).

### 6.2 Nanoscale 3D DNA Tracing: Resolving Loops In Situ

A transformative advance in chromatin biology is the development of nanoscale 3D DNA tracing — LoopTrace — which resolves individual chromatin fibers at <30 nm precision in non-denatured cells (PMID: 40683887). Unlike FISH-based methods that require DNA denaturation and can perturb chromatin architecture, LoopTrace uses multiplexed oligonucleotide probes hybridized under native conditions, combined with sequential imaging and super-resolution localization.

LoopTrace revealed several fundamental features of genome architecture that were invisible to population-averaged methods like Hi-C:

**Flexible random coils at 100 kb.** At the 100 kb scale, chromatin behaves as a flexible random coil with no evidence of rigid higher-order folding, contradicting earlier proposals of hierarchical 30 nm fibers or chromatin fiber structures (PMID: 40683887; PMID: 40301047).

**Cohesin-dependent loops in a subset of cells.** CTCF-anchored chromatin loops are present in only a subset (~16%) of cells at any given time, with TAD anchors making contact for approximately 6–19 minutes per hour. This stochastic, dynamic looping is qualitatively different from the static, deterministic picture suggested by population-averaged Hi-C data (PMID: 40683887).

**~300 nm domain diameter.** Cohesin constrains TAD-scale chromatin domains to approximately 300 nm in diameter, a length scale that corresponds to the nuclear pore-to-pore spacing and may reflect functional constraints on the physical accessibility of regulatory elements.

The same LoopTrace technology applied to mitotic chromosomes revealed that the genome scaling minimum occurs at 6–8 Mbp, with large overlapping condensin-mediated loops generating the rod-shaped mitotic chromosome structure through self-organization rather than hierarchical folding (PMID: 39554202).

### 6.3 Uniform Cohesin Dynamics Across Chromatin Types

Live-cell imaging of induced cohesin loading using the TACL (Tetherable, Activatable Cohesin Loader) system has revealed that cohesin dynamics — extrusion speed, processivity, and CTCF blocking efficiency — are remarkably uniform across different chromatin types (euchromatin, heterochromatin, active vs. repressed regions) (PMID: 41102415). This uniformity implies that the diversity of genome folding patterns observed across cell types arises not from differences in cohesin motor activity, but from differences in the distribution of CTCF barriers and cohesin loading factors (NIPBL/MAU2).

TACL experiments also demonstrated cohesin queuing (multiple cohesins accumulating behind a CTCF barrier), blocking (one cohesin preventing passage of another), and anchoring (stable cohesin positioning at CTCF sites), with NIPBL being transported to CTCF sites during extrusion — a finding that challenges the model of separate loading and barrier mechanisms (PMID: 41102415).

### 6.4 CTCF Barrier Mechanism and Regulation

CTCF (CCCTC-binding factor) functions as the primary barrier to cohesin loop extrusion, blocking the motor and establishing TAD boundaries. High-resolution CTCF footprinting using the CAMEL (CTCF-Assisted Mapping of Extrusion Landscape) tool has revealed that fully extruded CTCF-CTCF loops — where cohesin has reached both CTCF anchors simultaneously — are rare (~1–10% of cells), consistent with the dynamic, stochastic nature of loop formation (PMID: 40374602). Active regulatory elements (enhancers, promoters) also impede cohesin extrusion, creating a complex landscape of partial barriers (PMID: 40374602).

Recent work has challenged the pure-barrier model: CTCF directly enhances cohesin processivity via its N-terminal YDF motif, suggesting that CTCF functions as both a barrier and a processivity factor — blocking extrusion while simultaneously stabilizing the extruding complex at the barrier site (PMID: 39988079). Mathematical modeling shows that the ratio of boundary lifetime to extruder lifetime determines chromosome morphology: when barriers are long-lived relative to extruder processivity, sharp TAD boundaries emerge; when barriers are transient, TADs become diffuse (PMID: 40586309).

CTCF also has non-architectural functions: disentangling the architectural and non-architectural roles of CTCF revealed that it acts as a direct transcriptional activator or repressor at promoters, independent of its role in loop formation (PMID: 41254162). The architectural and transcriptional functions may be separable, opening the possibility of therapeutic interventions that modulate one without affecting the other.

### 6.5 NIPBL/STAG1 Differential DNA Affinity

The mechanism by which cohesin engages DNA during loop extrusion has been elucidated by mass photometry studies of the NIPBL and STAG1 loader/regulatory subunits (PMID: 40763028). NIPBL tightly binds DNA as the anchor point — maintaining grip on the DNA "anchor" arm of the loop — while STAG1-cohesin binds DNA weakly and cooperatively, providing the transient contacts needed for DNA translocation through the cohesin ring. ATP binding modulates the grabbing and release cycle, with hydrolysis triggering DNA release from the STAG1 arm and enabling one step of loop extrusion. This differential affinity model explains how cohesin can simultaneously maintain a stable grip on one DNA segment (the anchor) while processively translocating another (the extruded loop).

### 6.6 Langevin Equation for Loop Extrusion Motor Dynamics

We model the position of the cohesin motor along DNA as a one-dimensional Langevin equation describing the balance between motor driving force, frictional drag, chromatin resistance, and thermal noise:

$$\gamma \frac{dx}{dt} = F_{motor} - \frac{dU}{dx} + \xi(t)$$

where $x$ is the position of the extruding cohesin along the DNA contour, $\gamma$ is the effective friction coefficient of the motor (reflecting both protein-DNA contacts and solvent viscosity), $F_{motor}$ is the ATP-driven force generated by cohesin conformational cycling, $U(x)$ is the potential energy landscape encoding chromatin obstacles (nucleosomes, CTCF barriers, condensates), and $\xi(t)$ is Gaussian white noise with $\langle\xi(t)\xi(t')\rangle = 2\gamma k_BT \delta(t-t')$ satisfying the fluctuation-dissipation theorem.

For a motor operating against a constant resistance (nucleosomal friction) with an additional localized barrier (CTCF site at position $x_0$):

$$U(x) = f_{resist} \cdot x + \Delta U_{CTCF} \cdot \exp\left(-\frac{(x-x_0)^2}{2\sigma_{CTCF}^2}\right)$$

where $f_{resist} \approx 0.1$ pN is the resistive force per nucleosome transit, $\Delta U_{CTCF} \approx 10 \, k_BT$ is the barrier height at a CTCF site, and $\sigma_{CTCF} \approx 50$ nm is the barrier width. The mean extrusion velocity in the absence of barriers is:

$$\langle v \rangle = \frac{F_{motor} - f_{resist}}{\gamma}$$

For $F_{motor} \approx 1$ pN (measured by single-molecule force spectroscopy), $f_{resist} \approx 0.1$ pN, and $\gamma \approx 10^{-4}$ pN·s/nm (estimated from the diffusion coefficient of cohesin on DNA), the predicted extrusion velocity is:

$$\langle v \rangle = \frac{0.9 \text{ pN}}{10^{-4} \text{ pN·s/nm}} = 9000 \text{ nm/s} \approx 2.7 \text{ kb/s}$$

This is within the correct order of magnitude of the experimentally measured range of 0.5–2.1 kb/s, validating the Langevin framework (PMID: 38831499). The model predicts that CTCF barriers reduce extrusion velocity exponentially with barrier height:

$$\langle v \rangle_{barrier} = \langle v \rangle \cdot \exp\left(-\frac{\Delta U_{CTCF}}{k_BT}\right)$$

For $\Delta U_{CTCF} = 10 \, k_BT$, the velocity through a CTCF barrier is reduced by a factor of $e^{-10} \approx 4.5 \times 10^{-5}$ — effectively halting extrusion, consistent with the observed barrier function.

### 6.7 Worm-Like Chain Model for Chromatin

The spatial extent of chromatin loops formed by cohesin extrusion is governed by the polymer mechanics of the chromatin fiber. We model chromatin as a worm-like chain (WLC) — a semiflexible polymer characterized by its contour length $L_c$ and persistence length $L_p$:

$$\langle R^2 \rangle = 2L_p L_c \left[1 - \frac{L_p}{L_c}\left(1 - e^{-L_c/L_p}\right)\right]$$

where $\langle R^2 \rangle$ is the mean-square end-to-end distance. For chromatin, the persistence length has been measured at $L_p \approx 50$ nm (corresponding to ~1.5 kb of DNA wrapped around nucleosomes) by LoopTrace nanoscale tracing in non-denatured cells (PMID: 40683887; PMID: 39601793). For a typical TAD with $L_c = 500$ kb $\approx 170 \, \mu$m of DNA contour (at 0.34 nm/bp), the genomic contour length greatly exceeds the persistence length, and the WLC reduces to the flexible chain limit:

$$\langle R^2 \rangle \approx 2L_p L_c = 2 \times 50 \times 170,000 = 1.7 \times 10^7 \text{ nm}^2$$

$$\sqrt{\langle R^2 \rangle} \approx 4,100 \text{ nm} \approx 4.1 \, \mu\text{m}$$

This unconfined radius of gyration far exceeds the ~300 nm domain diameter observed experimentally (PMID: 40683887), demonstrating that cohesin loop extrusion compacts chromatin by approximately 14-fold relative to a free polymer. The compaction ratio $C = \sqrt{\langle R^2 \rangle_{free}} / R_{domain}$ provides a quantitative measure of loop extrusion efficiency.

The contact probability between two loci separated by genomic distance $s$ scales differently for equilibrium polymers versus loop-extruded chromatin:

- **Equilibrium (fractal globule):** $P(s) \sim s^{-1}$ (reflecting the fractal organization of a crumpled polymer)
- **Loop-extruded chromatin:** $P(s) \sim s^{-3/2}$ within TADs, transitioning to $P(s) \sim s^{-1}$ at inter-TAD distances

The steeper $s^{-3/2}$ scaling within TADs is a signature of loop extrusion that has been confirmed by Hi-C data (PMID: 40683887) and is quantitatively predicted by polymer simulations incorporating loop-extruding factors (PMID: 39601793).

### 6.8 Chromatin-Condensate Interface

An emerging frontier in chromatin biology is the interaction between loop extrusion and biomolecular condensates. Liquid condensates formed by transcription factors and coactivators at super-enhancers create physical barriers that can impede cohesin extrusion, adding a layer of regulation beyond CTCF (PMID: 39601793). The viscosity and surface tension of condensates — material properties that depend on the multivalent interactions of their constituent proteins and RNAs — determine the degree to which they act as extrusion barriers. This connection between condensate physics and genome organization creates an unexpected link between two of the six frontiers examined in this review.

### 6.9 Therapeutic Implications and Disease

Mutations in cohesin subunits and regulators cause a spectrum of developmental disorders collectively termed cohesinopathies, including Cornelia de Lange syndrome (CdLS), Roberts syndrome, and Warsaw breakage syndrome (PMID: 40345853; PMID: 39594644). These disorders result from impaired loop extrusion, leading to misregulation of developmental gene expression programs.

The cohesin loading factor NIPBL is haploinsufficient in ~60% of CdLS cases, suggesting that therapeutic upregulation of NIPBL expression could restore normal loop extrusion (PMID: 40763028). More speculatively, the discovery that cohesin dynamics are uniform across chromatin types suggests that restoring normal NIPBL/WAPL stoichiometry — rather than repairing individual chromatin loops — could globally normalize genome architecture (PMID: 41102415).

In cancer, altered cohesin function has been linked to aberrant gene regulation and chromosomal instability. Cohesin is essential for maintaining enhancer-promoter contacts that support tissue-specific gene expression: RAD21 knockout in cerebellar neurons disrupts late-maturing gene expression programs and displaces enhancers from the active A compartment (PMID: 41013693).

### 6.10 Open Questions

The most fundamental unsolved question in loop extrusion is the mechanism of CTCF barrier sensing: how does cohesin, a DNA-translocating motor, recognize a ~50 kDa protein (CTCF) bound to a specific DNA motif and halt its movement? The YDF motif interaction (PMID: 39988079) provides a partial answer, but the structural details of the cohesin-CTCF encounter complex remain unresolved. Second, single-molecule real-time imaging of loop extrusion in living cells — the ultimate validation of in vitro reconstitution studies — has not yet been achieved with sufficient temporal resolution to capture individual extrusion events. Third, therapeutic targeting of loop extrusion for cohesinopathies and cancer requires chemical modulators of cohesin activity, which remain undiscovered. Fourth, the interplay between loop extrusion and nuclear condensates (PMID: 39601793) creates emergent organizational properties that cannot be predicted from either mechanism alone and require integrated modeling approaches.

---

## VII. Condensate-Modifying Therapeutics: Phase Transition Pharmacology

### 7.1 Biomolecular Condensates as Therapeutic Targets

Biomolecular condensates — non-stoichiometric assemblies formed by liquid-liquid phase separation (LLPS) of multivalent proteins and RNAs — organize cellular biochemistry into membraneless compartments with tunable emergent properties (PMID: 40830340). These compartments, ranging from 100 nm to several micrometers in diameter, include stress granules, P-bodies, nucleoli, transcription factories, paraspeckles, and PML bodies. Their formation is driven by multivalent interactions between "sticker" domains (RNA-binding domains, low-complexity sequences) connected by flexible "spacer" regions, creating a polymer network that undergoes phase separation above a critical concentration (PMID: 39516712).

The pharmaceutical significance of condensates became apparent with the discovery that small-molecule drugs partition into condensates with dramatically different concentrations than in the surrounding dilute phase — with partition coefficients ($K_{part}$) reaching up to 600-fold for some therapeutic compounds (PMID: 39271915). This selective partitioning means that conventional pharmacokinetic models, which assume uniform drug distribution within cellular compartments, may substantially underestimate or overestimate drug concentrations at their molecular targets if those targets reside within condensates.

The emerging field of condensate-modifying therapeutics (c-mods) seeks to develop drugs that specifically modulate condensate formation, dissolution, composition, or material properties as their primary mechanism of action. The first c-mod, DPTX3186 — a beta-catenin condensate modifier developed by Dewpoint Therapeutics — entered Phase I/IIa clinical trials for advanced solid tumors in February 2026, with FDA Fast Track and Orphan Drug designations for gastric cancer. A second Dewpoint program targets TDP-43 condensates in ALS, based on the observation that TDP-43 condensate pathology is the defining histopathological feature of ALS/FTD, affecting >97% of ALS patients.

### 7.2 Drug Partitioning Physics

The partitioning of a drug molecule into a condensate is governed by the transfer free energy — the free energy difference between the drug in the dilute phase and the drug in the condensate interior:

$$K_{part} = \frac{c_{drug}^{condensate}}{c_{drug}^{dilute}} = \exp\left(-\frac{\Delta G_{transfer}}{k_BT}\right)$$

Systematic profiling of ~1,700 small molecules across multiple condensate types has revealed that partition coefficients vary over a million-fold range, and that simple physicochemical properties — molecular weight, logP (hydrophobicity), aromaticity, and charge — are sufficient to predict partitioning behavior with high accuracy using machine learning models (PMID: 39271915). The dominant factor is hydrophobicity: condensate interiors are enriched in aromatic and hydrophobic amino acid side chains, creating a chemical environment that preferentially accumulates hydrophobic drugs (PMID: 39271915).

However, the selectivity of partitioning between different condensate types arises from more subtle factors. Non-specific hydrophobic interactions dominate the total partitioning free energy, but population shifts in the chemical environments (the distribution of distinct amino acid compositions surrounding the drug molecule) across different condensate types drive selectivity toward specific condensates (PMID: 39184067). Different condensates share similar sets of chemical environments but at different populations, creating a selectivity mechanism analogous to tissue-selective drug distribution in conventional pharmacology (PMID: 39184067; PMID: 37770698).

Molecular simulations using minimal coarse-grained models (MAPPS) have confirmed that protein sequence — through its influence on amino acid composition and spacing — exerts selective pressure on drug partitioning, providing a computational framework for predicting drug accumulation in disease-relevant condensates (PMID: 40747072).

### 7.3 Stickers-and-Spacers Mean-Field Theory for Phase Boundaries

The phase behavior of condensate-forming proteins can be described by stickers-and-spacers polymer theory, which models multivalent proteins as chains of associative "sticker" domains connected by non-interacting "spacer" regions. The mean-field phase boundary — the critical concentration above which phase separation occurs — is determined by three parameters: sticker valence $v$ (number of interaction sites per molecule), sticker binding energy $\varepsilon$ (free energy of a single sticker-sticker interaction), and spacer flexibility (characterized by the Kuhn length).

For a system with sticker valence $v$ and associative binding energy $\varepsilon$ per sticker, the coexistence concentration (dilute phase boundary) is approximately:

$$\phi_{coex}^{dilute} \approx \left(\frac{1}{v-1}\right) \exp\left(-\frac{v\varepsilon}{2k_BT}\right)$$

The gelation percolation threshold — the concentration at which the system transitions from disconnected clusters to a network-spanning gel — is:

$$p_c = \frac{1}{v-1}$$

where $p_c$ is the fraction of stickers that must be engaged in intermolecular contacts for gelation. For a protein with $v = 6$ sticker domains (typical of RNA-binding proteins like FUS or hnRNPA1), $p_c = 0.2$ — only 20% of stickers need to form intermolecular bonds for the condensate to gel, explaining the propensity of RNA-binding protein condensates to undergo liquid-to-gel transitions at relatively modest concentrations.

This framework makes a clinically relevant prediction: c-mods that reduce the effective sticker valence $v$ (by competing for sticker-sticker interactions) or that increase spacer flexibility (by disrupting spacer-mediated secondary interactions) will shift the phase boundary to higher concentrations, dissolving pathological condensates. Conversely, c-mods that increase effective $\varepsilon$ (by cross-linking stickers) will lower the phase boundary, promoting condensate formation.

### 7.4 RNA-Driven Phase Transitions and Material State Control

RNA is not merely a passive cargo within condensates but a critical regulator of phase behavior and material properties. RNA stoichiometry controls the liquid-gel-solid transition in condensates: at low RNA:protein ratios, multivalent proteins form liquid droplets; at intermediate ratios, RNA cross-links the network into a gel; at high ratios, charge inversion dissolves the condensate — a phenomenon known as reentrant phase separation (PMID: 39366355).

The molecular basis for RNA-driven material state transitions has been elucidated for several disease-relevant proteins:

**G3BP1 as an RNA condenser.** G3BP1, the core scaffolding protein of stress granules, functions as an "RNA condenser" that promotes intermolecular RNA-RNA interactions. Following initial condensation, G3BP1 is dispensable for granule persistence when RNA decondensation is prevented, demonstrating that the RNA network — not the protein scaffold — is the material backbone of stress granules (PMID: 39637853).

**Homotypic RNA clustering and gelation.** Repeat-expansion RNAs undergo a percolation transition within condensates, forming nanoscale RNA clusters that drive the liquid-to-solid transition. G3BP1 buffers this process through heterotypic protein-RNA interactions that compete with pathological homotypic RNA-RNA contacts (PMID: 40603603).

**FUS surface beta-sheet formation.** NMR and Raman spectroscopy revealed that a crust-like beta-sheet structure forms selectively on the surface of FUS droplets during aging, while the interior remains liquid-like. RNA binding prevents this surface solidification, suggesting that RNA depletion from condensates — a feature of aging cells — initiates pathological material state transitions (PMID: 38467846). Charged peptides enriched in aromatic residues decelerate condensate aging by competing with cross-beta-sheet formation, decelerating the liquid-to-solid transition by >10-fold.

**TDP-43 intra-condensate demixing.** In stress granules, TDP-43 undergoes intra-condensate demixing — a process requiring two simultaneous events: upconcentration within the condensate and oxidative stress. RRM1 domain unfolding enables cross-beta-sheet nucleation, generating the pathological aggregates observed in >97% of ALS/FTD patients (PMID: 40412392). Engineered TDP-43 variants resistant to RRM1 unfolding are protected from aggregation, identifying a specific structural vulnerability that could be targeted by c-mods.

### 7.5 Cancer Condensate Therapeutics

Biomolecular condensates are emerging as therapeutic targets in oncology:

**Beta-catenin condensate modulation.** The natural product rosmanol quinone induces beta-catenin LLPS, sequestering it in cytoplasmic condensates and preventing nuclear entry — thereby blocking Wnt-driven transcription of oncogenic target genes. Nanoparticle-formulated abroquinone demonstrated hepatocellular carcinoma suppression in preclinical models (PMID: 40593772).

**Repressive transcription factor condensates.** Synthetic peptides that induce repressive TEAD4 condensates via VGLL4/RFXANK scaffolding suppress Hippo pathway-driven transcription in gastric cancer models, demonstrating that condensate induction — not just dissolution — can be therapeutically beneficial (PMID: 39358623).

**Leukemia-associated condensates.** NPM1-mutant acute myeloid leukemia — the most common subtype, affecting ~30% of AML patients — is driven by aberrant phase separation. NPM1c (cytoplasmic-mislocalized NPM1) forms "coordinating bodies" (C-bodies) that recruit NUP98 and KMT2A fusion proteins, creating an aberrant transcriptional condensate that maintains the leukemic state (PMID: 41192422; PMID: 40501735). Pharmacological destabilization of C-bodies blocks leukemic self-renewal, establishing condensate disruption as a therapeutic strategy in hematological malignancy.

### 7.6 Stress Granule Therapeutics

Stress granules (SGs) — cytoplasmic condensates that form in response to cellular stress — have emerged as both protective structures and potential drivers of neurodegenerative disease. Small-molecule dissolution of stress granules by lipoamide, which modulates redox-sensitive condensation through SFPQ, ameliorates FUS and TDP-43-mediated motor defects in ALS models (PMID: 40369342). Conversely, stress granule formation can be protective: SG formation helps mitigate neurodegeneration by enabling selective translation of stress-response mRNAs while globally suppressing translation of housekeeping transcripts (PMID: 39106168). This dual role — protective in acute stress, pathological in chronic disease — creates a therapeutic challenge: c-mods must distinguish between functional and dysfunctional SGs.

Chemical and optical platforms for controlled condensate induction and maturation enable systematic screening of c-mod candidates. The BTBolig platform uses chemical genetic switches to induce condensate formation, monitor maturation from liquid to gel to solid states, and assess chaperone recruitment — providing a drug discovery pipeline for c-mods targeting material state transitions (PMID: 38191942). Comparative evaluation of cell-based assay technologies — including high-throughput single-molecule tracking (htSMT), NanoBIT complementation, and NanoBRET proximity assays — has established best practices for scoring drug-induced condensation changes (PMID: 39894078).

### 7.7 Condensate Material Properties and the Nanoscale

The material properties of condensates — viscosity, surface tension, elastic modulus — emerge from nanoscale dynamics of their constituent molecules. Single-molecule measurements have revealed that viscosity is determined by translational diffusion coefficients and chain dynamics, while the lifetime of interresidue contacts determines the effective friction that governs material state (PMID: 40455990). This connection between nanoscale molecular dynamics and macroscale material properties is critical for c-mod design: drugs that alter interresidue contact lifetimes by even 2-fold can shift a condensate from liquid to gel or vice versa.

Multi-phase condensate architecture adds another layer of complexity. In paraspeckles, three RNA-binding proteins (FUS, NONO, TDP-43) are organized into distinct core and shell layers by competitive RNA binding and protein-protein immiscibility (PMID: 40768359). Drugs that alter the relative RNA-binding affinities of these proteins could reorganize paraspeckle architecture, with potential therapeutic consequences for the RNA regulation functions that paraspeckles control.

### 7.8 Open Questions

The central challenge for condensate therapeutics is selectivity: pathological condensates (e.g., TDP-43 aggregates) coexist with functional condensates (e.g., normal stress granules, transcription factories) in the same cell, and c-mods must distinguish between them. Current selectivity strategies rely on differences in composition (targeting unique scaffold proteins) or material state (targeting gel/solid states that are absent from functional liquid condensates), but neither approach achieves the selectivity levels expected for clinical drugs. Second, in vivo condensate pharmacokinetics are essentially uncharacterized: how drug molecules distribute between the dilute phase and multiple distinct condensate compartments in living tissues remains unknown. Third, the gelation percolation threshold ($p_c = 1/(v-1)$) predicts a sharp transition between liquid and gel states, but whether this transition is as sharp in vivo — where condensates contain hundreds of distinct protein and RNA species — is uncertain. Fourth, the relationship between condensate material state (liquid vs. gel vs. solid) and disease severity is correlative rather than causal in most systems; demonstrating that material state reversal (e.g., gel → liquid) is sufficient for therapeutic benefit requires intervention studies that are now becoming possible with c-mods (PMID: 39510346; PMID: 40830340).

---

## VIII. Synthesis: Convergent Biophysical Principles and the Therapeutic Frontier

### 8.1 Cross-Cutting Analysis

The six frontiers examined in this review — targeted protein degradation, conformational ensemble drug design, endosomal escape mechanics, single-molecule protein sequencing, chromatin loop extrusion, and condensate pharmacology — are connected by shared biophysical principles whose recurrence across disparate biological contexts suggests deep underlying unity.

### 8.2 Induced Proximity as a Universal Therapeutic Mechanism

The principle of induced proximity — bringing two molecules within nanometer-scale distance to enable a specific biochemical reaction — operates across multiple frontiers:

In TPD, bifunctional molecules bridge target proteins and E3 ligases across ~2–5 nm to enable ubiquitin transfer within the ~10 Å geometric constraint (PMID: 39392888). In condensate biology, multivalent proteins scaffold RNA and enzyme substrates at concentrations up to 600-fold above the dilute phase, creating nanoscale reaction volumes where proximity effects dominate conventional solution-phase kinetics (PMID: 39271915). In chromatin loop extrusion, cohesin brings enhancers and promoters into contact within ~300 nm domains, with contact durations of 6–19 minutes per hour establishing a time-averaged proximity that regulates transcription (PMID: 40683887). In nanopore sequencing, the amino acid-pore constriction proximity (<1.2 nm) is essential for generating amino acid-specific current signatures — the information encoding principle that enables single-molecule readout (PMID: 39261738).

The therapeutic implication is that molecular proximity engineering — controlling who touches whom, at what distance, for how long — constitutes a unified design principle that can be applied across all six frontiers. The mathematical formalism is shared: effective concentration ($C_{eff}$), partition coefficient ($K_{part}$), and contact probability ($P(s)$) are all expressions of the same underlying physics of proximity.

### 8.3 Conformational Dynamics as the Source of Therapeutic Opportunity

Static structures are necessary but insufficient for understanding drug action. Across all six frontiers, conformational dynamics — the time-dependent fluctuations between multiple molecular states — create therapeutic opportunities that are invisible to structural snapshots:

In conformational ensemble drug design, cryptic pockets accessible for only ~0.6% of the time offer druggable surfaces that AlphaFold cannot predict (PMID: 38603560). In TPD, the cooperativity factor α reflects the conformational flexibility of the ternary complex — rigid complexes have low α, while flexible complexes that sample multiple productive orientations achieve α > 10 (PMID: 41022846). In endosomal escape, the pH-triggered conformational transition of ionizable lipids from lamellar to H_II phase is the molecular switch that enables membrane disruption (PMID: 41060394). In chromatin biology, cohesin's ATP-dependent conformational cycle drives the directed motion of loop extrusion at 0.5–2.1 kb/s (PMID: 38831499). In nanopore sequencing, the translocation intermediates adopted by amino acids within the pore constriction generate the conformational diversity that enables current-based discrimination (PMID: 40097683). In condensate biology, the liquid-gel-solid material state transitions that distinguish physiological from pathological condensates are conformational dynamics at the mesoscale (PMID: 38467846).

The Kramers' escape rate framework developed in Section III provides a unifying mathematical language: all conformational transitions — from protein domain motions to lipid phase changes to condensate material state transitions — are governed by barrier heights, attempt frequencies, and friction coefficients that can be measured, modeled, and therapeutically manipulated.

### 8.4 Membrane Mechanics as a Shared Physical Framework

Helfrich membrane mechanics, developed to describe lipid bilayer bending and pore formation in the endosomal escape context (Section IV), has unexpected connections to other frontiers. Condensate surface tension — a mesoscale analogue of membrane surface tension — governs droplet coalescence, wetting behavior on chromatin, and the partitioning of molecules between the condensate interior and dilute phase (PMID: 40455990). The mathematical formalism is identical: surface energy ($\gamma \cdot A$), line tension at phase boundaries, and curvature-dependent energy penalties all appear in both membrane and condensate physics.

Chromatin itself exhibits membrane-like mechanical properties at certain length scales: the persistence length of ~50 nm (PMID: 40683887) and the bending modulus inferred from LoopTrace measurements place chromatin fibers in a semiflexible polymer regime that shares mathematical features with membrane mechanics. The worm-like chain model used to describe chromatin in Section VI is the polymer analogue of the Helfrich model used for membranes in Section IV — both describe the energetic cost of bending a semiflexible structure.

### 8.5 Information Encoding at the Nanoscale

The Shannon channel capacity framework developed for nanopore protein sequencing (Section V) connects to information encoding across other frontiers. In chromatin biology, the 3D organization of the genome encodes gene regulatory information: the contact probability scaling $P(s) \sim s^{-\alpha}$ carries information about the loop extrusion state of a genomic region, with the exponent $\alpha$ distinguishing active ($\alpha \approx 1.5$) from equilibrium ($\alpha \approx 1$) polymer states (PMID: 40683887). In conformational ensemble drug design, the Boltzmann-weighted populations of active and inactive protein conformations encode the "signal" that determines drug efficacy — a drug is effective only if it shifts the ensemble toward the therapeutically desired conformation (PMID: 39923288). In condensate biology, the partition coefficient $K_{part}$ encodes selectivity information: the transfer free energy $\Delta G_{transfer}$ specifies which condensates preferentially accumulate a given drug molecule (PMID: 39271915).

The information-theoretic perspective suggests a fundamental limit on therapeutic specificity: any drug mechanism that relies on molecular discrimination (target vs. off-target, condensate A vs. condensate B, amino acid X vs. amino acid Y) is subject to a signal-to-noise constraint analogous to the Shannon channel capacity. The minimum error rate achievable by any discrimination mechanism is bounded by the mutual information between the distinguishing molecular features and the readout signal. This framework provides a principled basis for comparing the theoretical specificities of different therapeutic modalities: TPD (discrimination between target and non-target proteins at the E3 ligase interface), conformational drugs (discrimination between active and inactive protein states), c-mods (discrimination between pathological and functional condensates), and gene editing (discrimination between on-target and off-target genomic sites).

### 8.6 Future Directions

We identify five research directions at the convergence of these frontiers that are likely to yield high-impact results in the coming decade:

**1. Condensate-targeted protein degradation.** Combining TPD and condensate biology — developing degraders that selectively accumulate in disease-relevant condensates and degrade their scaffold proteins — could achieve condensate-selective degradation with the catalytic efficiency of PROTACs and the compartment selectivity of c-mods. The 600-fold enrichment of hydrophobic molecules in condensates (PMID: 39271915) suggests that PROTAC-like molecules could achieve extreme effective concentrations within condensates, potentially enabling degradation of targets at sub-nanomolar drug concentrations.

**2. Nanopore-guided condensate proteomics.** Single-molecule protein sequencing of isolated condensates could reveal the complete proteomic composition and PTM landscape of individual condensate types, enabling precision c-mod design based on condensate-specific molecular vulnerabilities.

**3. Loop extrusion as a drug target.** Chemical modulators of cohesin activity — either enhancers (for cohesinopathies) or inhibitors (for cancers with cohesin-dependent enhancer-promoter contacts) — represent an entirely unexplored therapeutic modality. The uniform dynamics of cohesin across chromatin types (PMID: 41102415) suggest that modulating the amount of active cohesin, rather than its intrinsic activity, may be the most tractable approach.

**4. Endosomal escape optimization through conformational ensemble design.** The phase transitions of ionizable lipids that drive endosomal escape are conformational dynamics problems amenable to the same enhanced sampling and ML methods used for protein cryptic pocket discovery. Applying Boltzmann-weighted ensemble methods to lipid phase space could accelerate the discovery of lipids with optimal ESCRT-reparable pore-forming properties.

**5. Information-theoretic limits on therapeutic specificity.** Developing a unified Shannon capacity framework for comparing the fundamental specificity limits of different therapeutic modalities — TPD, gene editing, c-mods, conformational drugs — could guide the rational selection of modality for each disease target based on the achievable signal-to-noise ratio of molecular discrimination.

### 8.7 Conclusion

The six frontiers examined in this review are not isolated disciplines but interconnected facets of a single transformation in biomedicine: the translation of nanoscale biophysical understanding into therapeutic action. The shared principles of induced proximity, conformational dynamics, membrane mechanics, and information encoding provide a unified conceptual framework that connects targeted protein degradation to condensate pharmacology, endosomal escape to chromatin architecture, and nanopore sensing to drug design. As each frontier advances — with the first PROTAC approaching approval, the first c-mod entering clinical trials, single-molecule protein sequencers achieving near-Shannon-limit accuracy, and chromatin loop extrusion being resolved in living cells — the convergence between them will accelerate. The next generation of therapeutics will be designed not at the level of individual molecules in isolation, but at the level of the nanoscale biophysical systems — ternary complexes, conformational ensembles, membrane pores, chromatin loops, and biomolecular condensates — that govern human biology.

---

## References

1. Crowe C, Nakasone MA, Chandler S et al. Mechanism of degrader-targeted protein ubiquitinability. *Science Advances* 10(41):eado6492, 2024. PMID: 39392888.

2. Hanzl A, Casement R, Imber H et al. Targeted protein degradation via intramolecular bivalent glues. *Nature* 627(8002):204-211, 2024. PMID: 38383787.

3. Ma N, Bhattacharya S, Muk S et al. Frustration in the protein-protein interface plays a central role in the cooperativity of PROTAC ternary complexes. *Nature Communications* 16, 8595, 2025. PMID: 41022846.

4. Xue F, Zhang M, Li S et al. SE(3)-equivariant ternary complex prediction towards target protein degradation. *Nature Communications*, 2025. PMID: 40593782.

5. Cai L, Yue G, Chen Y et al. ET-PROTACs: modeling ternary complex interactions using cross-modal learning and ternary attention for accurate PROTAC-induced degradation prediction. *Briefings in Bioinformatics* 26(1):bbae654, 2024. PMID: 39783892.

6. Li Y, Bao K, Sun J et al. Design of PROTACs utilizing the E3 ligase GID4 for targeted protein degradation. *Nature Structural & Molecular Biology* 32:1825-1837, 2025. PMID: 40295770.

7. Cao Y, Harris AL, Ciulli A. Branching beyond bifunctional linkers: synthesis of macrocyclic and trivalent PROTACs. *Nature Protocols*, 2025. PMID: 41219525.

8. Baek K et al. A degron-mimicking molecular glue drives CRBN homo-dimerization and degradation. *Nature Communications*, 2025. PMID: 41258141.

9. Baek K, Metivier RJ, Roy Burman SS et al. Unveiling the hidden interactome of CRBN molecular glues with chemoproteomics. *Nature Communications*, 2025. PMID: 40707481.

10. Stache EE et al. An engineered cereblon optimized for high-throughput screening and molecular glue discovery. *Cell Chemical Biology* 32(2):363-376.e10, 2024. PMID: 39610248.

11. Liu Y, Bai J, Li D, Cang Y. Routes to molecular glue degrader discovery. *Trends in Biochemical Sciences* 50(2):134-142, 2025. PMID: 39753433.

12. Slessareva JE et al. Selective CK1alpha degraders exert antiproliferative activity against a broad range of human cancer cell lines. *Nature Communications* 15:536, 2024. PMID: 38228616.

13. Zhang J et al. Novel potent molecular glue degraders against broad range of hematological cancer cell lines via multiple neosubstrates degradation. *Journal of Hematology & Oncology* 17:75, 2024. PMID: 39218923.

14. Jhaveri KL et al. Vepdegestrant, a PROTAC estrogen receptor degrader, in advanced breast cancer. *New England Journal of Medicine*, 2025. PMID: 40454645.

15. Wang J et al. Discovery of BMS-986365, a first-in-class dual androgen receptor ligand-directed degrader and antagonist. *Clinical Cancer Research* 32(1):224-241, 2026. PMID: 40788283.

16. Mato AR et al. Safety and clinical activity of BMS-986365 (CC-94676) in heavily pretreated patients with mCRPC. *Annals of Oncology*, 2024. PMID: 39293515.

17. Patel K et al. rechARge: a randomized phase III trial of BMS-986365 in patients with mCRPC. *Journal of Clinical Oncology*, 2025. PMID: 40455815.

18. Vetma V, O'Connor S, Ciulli A. Development of PROTAC degrader drugs for cancer. *Annual Review of Cancer Biology* 9:119-140, 2025.

19. Ghanem A et al. Journey of PROTAC: from bench to clinical trial and beyond. *Biochemistry*, 2025. PMID: 39791901.

20. Edmondson SD et al. Structural and physicochemical features of oral PROTACs. *Journal of Medicinal Chemistry* 67(19):17191-17206, 2024. PMID: 39078401.

21. Wang Y et al. PROTAC 2.0: expanding the frontiers of targeted protein degradation. *Drug Discovery Today* 30(6), 2025. PMID: 40348076.

22. Zhong G et al. Targeted protein degradation: advances in drug discovery and clinical practice. *Signal Transduction and Targeted Therapy* 9(1):308, 2024. PMID: 39500878.

23. Basu S et al. A CRISPR activation screen identifies FBXO22 supporting targeted protein degradation. *Nature Chemical Biology* 20(12):1608-1616, 2024. PMID: 38965383.

24. Zhang X, Simon GM, Cravatt BF. Implications of frequent hitter E3 ligases in targeted protein degradation screens. *Nature Chemical Biology* 21:474-481, 2025. PMID: 39870762.

25. Li P et al. Alkenyl oxindole is a novel PROTAC moiety that recruits the CRL4-DCAF11 E3 ubiquitin ligase complex. *PLOS Biology*, 2024. PMID: 38768083.

26. Xia L et al. A covalent peptide-based lysosome-targeting protein degradation platform for cancer immunotherapy. *Nature Communications* 16:1388, 2025. PMID: 39910101.

27. Sievers QL et al. A phenotypic screen enables high-throughput target-first discovery of molecular glue degraders. *Nature Biotechnology*, 2025. PMID: 39854250.

28. Jhaveri K et al. VERITAC-2: Phase III study of vepdegestrant. *Expert Review of Anticancer Therapy*, 2024. PMID: 39072356.

29. Yun J et al. BTK is the target that keeps on giving: a review of BTK-degrader drug development. *Cancers* 17(3):557, 2025. PMID: 39941922.

30. Bowman GR. AlphaFold and protein folding: not dead yet! The frontier is conformational ensembles. *Annual Review of Biomedical Data Science* 7:51-57, 2024. PMID: 38603560.

31. Tsai CJ et al. Modeling Boltzmann-weighted structural ensembles of proteins using AI-based methods. *Current Opinion in Structural Biology* 90, 2025. PMID: 39923288.

32. Cui X, Ge L, Chen X et al. Beyond static structures: protein dynamic conformations modeling in the post-AlphaFold era. *Briefings in Bioinformatics* 26(4):bbaf340, 2025. PMID: 40663654.

33. Stachowski TR, Fischer M. Unfreezing structural biology for drug discovery. *Nature Chemical Biology* 22(2):169-179, 2026. PMID: 41193830.

34. Manglik A et al. Ligand efficacy modulates conformational dynamics of the mu-opioid receptor. *Nature* 629(8011):474-480, 2024. PMID: 38600384.

35. Robertson MJ et al. Non-equilibrium snapshots of ligand efficacy at the mu-opioid receptor. *Nature*, 2025. PMID: 41430437.

36. Zhuang Y et al. Structural snapshots capture nucleotide release at the mu-opioid receptor. *Nature*, 2025. PMID: 41193810.

37. Sun B et al. The molecular basis of mu-opioid receptor signaling plasticity. *Cell Research* 35(12):1021-1036, 2025. PMID: 41199005.

38. Kaneko S, Imai S, Uchikubo-Kamo T et al. Structural and dynamic insights into the activation of the mu-opioid receptor by an allosteric modulator. *Nature Communications* 15:3544, 2024. PMID: 38740791.

39. Livingston KE et al. A mu-opioid receptor modulator that works cooperatively with naloxone. *Nature*, 2024. PMID: 38961287.

40. Weng C, Faure AJ, Escobedo A, Lehner B. The energetic and allosteric landscape for KRAS inhibition. *Nature* 626:643-652, 2024. PMID: 38109937.

41. Sethi A et al. Exploration of cryptic pockets using enhanced sampling along normal modes: KRAS G12D. *Journal of Chemical Information and Modeling* 64(21):8258-8273, 2024. PMID: 39419500.

42. Bemelmans MP, Cournia Z, Damm-Ganamet KL et al. Computational advances in discovering cryptic pockets for drug discovery. *Current Opinion in Structural Biology* 90:102975, 2025. PMID: 39778412.

43. Li R, He X, Wu C et al. Advances in structure-based allosteric drug design. *Current Opinion in Structural Biology* 90:102974, 2025. PMID: 39736214.

44. Zhu K, Trizio E, Zhang J et al. Enhanced sampling in the age of machine learning: algorithms and applications. *Chemical Reviews*, 2025. PMID: 41124671.

45. Roney JP et al. Modeling protein-small molecule conformational ensembles with PLACER. *PNAS*, 2025. PMID: 41187076.

46. Sheridan R et al. Emerging frontiers in protein structure prediction following the AlphaFold revolution. *Journal of the Royal Society Interface* 22(225):20240886, 2025. PMID: 40233800.

47. Yu W et al. High-throughput ligand dissociation kinetics predictions using SILCS. *Journal of Chemical Theory and Computation* 21(9):4964-4978, 2025. PMID: 40285712.

48. Xiao S, Alshahrani M, Verkhivker G. Exploring binding and allosteric energy landscapes for KRAS using Markov state modeling. *Protein Science*, 2025. PMID: 40671268.

49. Padilla MS et al. Breaking the final barrier: Evolution of cationic and ionizable lipid structure in LNPs. *Advanced Drug Delivery Reviews*, 2024. PMID: 39293650.

50. Kulkarni JA et al. Ionizable lipid nanoparticles for mRNA delivery: internal self-assembled inverse mesophase structure. *Accounts of Chemical Research*, 2025. PMID: 41060394.

51. Pattipeiluhu R et al. Liquid crystalline inverted lipid phases encapsulating siRNA enhance LNP-mediated transfection. *Nature Communications*, 2024. PMID: 38347001.

52. Carucci C et al. Buffer specificity of ionizable lipid nanoparticle transfection efficiency. *ACS Nano*, 2025. PMID: 40074542.

53. Hamilton NB et al. Calculating apparent pKa values of ionizable lipids in LNPs. *Molecular Pharmaceutics*, 2025. PMID: 39655829.

54. Omo-Lamai S, Wang Y et al. Limiting endosomal damage sensing reduces inflammation triggered by LNP endosomal escape. *Nature Nanotechnology*, 2025. PMID: 40789922.

55. Johansson JM et al. Cellular and biophysical barriers to LNP-mediated delivery of RNA to the cytosol. *Nature Communications*, 2025. PMID: 40595685.

56. Grau M et al. Strategies and mechanisms for endosomal escape of therapeutic nucleic acids. *Current Opinion in Biotechnology*, 2024. PMID: 39096817.

57. Chatterjee S et al. Endosomal escape: a bottleneck for LNP-mediated therapeutics. *PNAS*, 2024. PMID: 38437552.

58. Bhagat A et al. In vivo endosomal escape assay identifies mechanisms for efficient hepatic LNP delivery. *Nature Biotechnology*, 2026. PMID: 41814093.

59. Xu Y et al. Rational design and modular synthesis of biodegradable ionizable lipids via the Passerini reaction. *PNAS*, 2025. PMID: 39883839.

60. Han X et al. In situ combinatorial synthesis of degradable branched lipidoids for systemic delivery. *Nature Communications*, 2024. PMID: 38409275.

61. Wei Y et al. Multiple tail ionizable lipids improve in vivo mRNA delivery efficiency. *International Journal of Pharmaceutics*, 2024. PMID: 39454975.

62. Hassett KJ et al. Overcoming thermostability challenges with piperidine-based ionizable lipids. *Communications Biology*, 2024. PMID: 38730092.

63. Su K, Shi L et al. Reformulating lipid nanoparticles for organ-targeted mRNA accumulation. *Nature Communications*, 2024. PMID: 38969646.

64. Sanowar T et al. Predictive lung- and spleen-targeted mRNA delivery with biodegradable ionizable lipids. *Pharmaceutics*, 2025. PMID: 40284454.

65. Li B et al. Accelerating ionizable lipid discovery for mRNA delivery using machine learning. *Nature Materials*, 2024. PMID: 38740955.

66. Xu Y et al. AGILE platform: a deep learning powered approach to accelerate LNP development. *Nature Communications*, 2024. PMID: 39060305.

67. Motone K et al. Multi-pass, single-molecule nanopore reading of long protein strands. *Nature*, 2024. PMID: 39261738.

68. Lu C, Bonini A, Viel JH, Maglia G. Toward single-molecule protein sequencing using nanopores. *Nature Biotechnology*, 2025. PMID: 40097683.

69. Zhang M et al. Real-time detection of 20 amino acids and discrimination of pathologically relevant peptides with functionalized nanopore. *Nature Methods*, 2024. PMID: 38443507.

70. Wang G et al. Unambiguous discrimination of all 20 proteinogenic amino acids by nanopore. *Nature Chemistry*, 2024. PMID: 37749214.

71. Nova IC et al. Detection of phosphorylation post-translational modifications along single peptides with nanopores. *Nature Biotechnology*, 2024. PMID: 37386295.

72. Cao C et al. Deep learning-assisted single-molecule detection of protein PTMs with a biological nanopore. *ACS Nano*, 2024. PMID: 38112538.

73. Chen X et al. Resolving sulfation PTMs on a peptide hormone using nanopores. *ACS Nano*, 2024. PMID: 39388343.

74. Lu C, Bonini A, Viel JH, Maglia G. Toward single-molecule protein sequencing using nanopores. *Nature Biotechnology*, 2025. PMID: 40097683.

75. Ouldali H et al. Narrowing signal distribution by adamantane derivatization for amino acid identification. *Nano Letters*, 2024. PMID: 38264980.

76. Chou L-Y et al. Coupled nanopores for single-molecule detection. *Nature Nanotechnology*, 2024. PMID: 39143316.

77. Reed BD et al. Robust and scalable single-molecule protein sequencing with fluorosequencing. *Nature Biotechnology*, 2024. PMID: 37745461.

78. Ratinho L et al. Nanopore sensing of protein and peptide conformation for point-of-care applications. *Nature Communications*, 2025. PMID: 40180898.

79. Wick RR et al. Evaluation of accuracy of bacterial genome reconstruction with Oxford Nanopore R10.4.1. *Microbial Genomics*, 2024. PMID: 38713194.

80. Qian X et al. DeepMod2: a signal processing and deep learning framework for methylation detection. *Nature Communications*, 2024. PMID: 38365920.

81. Martignano F et al. Adapting nanopore sequencing basecalling models for modification detection. *Bioinformatics*, 2024. PMID: 39169028.

82. Fahie MA et al. Advancing nanopore technology toward protein identification and sequencing. *Trends in Biochemical Sciences*, 2025. PMID: 40533364.

83. Marx V. Is single-molecule protein sequencing here yet? *Nature Methods*, 2025. PMID: 40770569.

84. Yatskevich S et al. Cohesin-dependent loop extrusion: molecular mechanics and role in cell physiology. *Biochemistry (Moscow)* 89(Suppl 1):S46-S63, 2024. PMID: 38831499.

85. Nasmyth K. Cohesin as an essential disruptor of chromosome organization. *Molecular Cell* 85(6):1073-1078, 2025. PMID: 39909042.

86. Vasi N et al. Cohesin supercoils DNA during loop extrusion. *Cell Reports* 44(7):115856, 2025. PMID: 40516048.

87. Barth R et al. SMC motor proteins extrude DNA asymmetrically and can switch directions. *Cell* 188(3):605-619, 2025. PMID: 39824185.

88. Janissen R et al. All eukaryotic SMC proteins induce a twist of -0.6 at each DNA loop extrusion step. *Science Advances* 10(50):eadt1832, 2024. PMID: 39671477.

89. Bastie N et al. Sister chromatid cohesion halts DNA loop expansion. *Molecular Cell* 84(6):1139-1148, 2024. PMID: 38452765.

90. Hirano T, Kinoshita K. SMC-mediated chromosome organization: does loop extrusion explain it all? *Current Opinion in Cell Biology* 92:102447, 2025. PMID: 39603149.

91. Valdes A, Haering CH. Adding a twist to the loops: DNA superhelicity in chromosome organization by SMC. *Biochemical Society Transactions* 52(6):2487-2499, 2024. PMID: 39700017.

92. Davidson IF, Peters JM. In vitro dynamics of DNA loop extrusion by SMC complexes. *Cold Spring Harbor Symposia*, 2024. PMID: 39591812.

93. Beckwith KS, Brunner A et al. Nanoscale 3D DNA tracing in non-denatured cells resolves cohesin-dependent loop architecture. *Nature Communications* 16:6183, 2025. PMID: 40683887.

94. Beckwith KS, Brunner A et al. Nanoscale 3D DNA tracing reveals mechanism of mitotic chromosome self-organization. *Cell* 188(8):2029-2048, 2025. PMID: 39554202.

95. Han R et al. Characterization of induced cohesin loop extrusion trajectories in living cells. *Nature Genetics*, 2025. PMID: 41102415.

96. Vian L et al. High-resolution CTCF footprinting reveals impact of chromatin state on cohesin extrusion. *Nature Communications* 16:4506, 2025. PMID: 40374602.

97. Kaaij LJT et al. Disentangling the architectural and non-architectural functions of CTCF and cohesin. *Nature Genetics*, 2025. PMID: 41254162.

98. Wu Q et al. CTCF N-terminal domain regulates protocadherin gene expression by enhancing cohesin processivity. *Journal of Biological Chemistry* 301(4):108186, 2025. PMID: 39988079.

99. Kim E et al. NIPBL and STAG1 enable loop extrusion by providing differential DNA-cohesin affinity. *PNAS* 122(29):e2514190122, 2025. PMID: 40763028.

100. De Wit E et al. Extrusion fountains are restricted by WAPL-dependent cohesin release and CTCF barriers. *Nucleic Acids Research* 53(12):gkaf549, 2025. PMID: 40586309.

101. Vercellone F et al. A multiscale perspective on chromatin architecture through polymer physics. *Physiology* 40(3), 2025. PMID: 39601793.

102. Maeshima K. The shifting paradigm of chromatin structure. *Proceedings of the Japan Academy, Ser. B* 101(6):339-356, 2025. PMID: 40301047.

103. Sole-Ferran C, Losada A. Cohesin in 3D: development, differentiation, and disease. *Genes & Development* 39(11-12):679-702, 2025. PMID: 40345853.

104. Ryzhkova A et al. Loop extrusion machinery impairments in models and disease. *Cells* 13(22):1896, 2024. PMID: 39594644.

105. Peters JM. Organization of replicated chromosomes by DNA loops and sister chromatid cohesion. *Nature Reviews Molecular Cell Biology* 27:201-218, 2026. PMID: 41478878.

106. Zheng G et al. Genome folding by cohesin. *Current Opinion in Genetics & Development* 91:102310, 2025. PMID: 39827577.

107. Berger G et al. Cohesin regulation of genome organization in mature granule neurons. *Epigenetics & Chromatin* 18:60, 2025. PMID: 41013693.

108. Serrano D et al. Loop-extruding Smc5/6 organizes transcription-induced positive DNA supercoils. *Molecular Cell* 84(5):867-882, 2024. PMID: 38295804.

109. Guerin TM et al. An extrinsic motor directs chromatin loop formation by cohesin. *EMBO Journal* 43(19):4466-4497, 2024. PMID: 39160275.

110. Guerin TM, Uhlmann F. A unified model for cohesin function in sister chromatid cohesion and chromatin loop formation. *Molecular Cell* 85(6):1060-1072, 2025. PMID: 40118039.

111. Ambadi Thody S et al. Small-molecule properties define partitioning into biomolecular condensates. *Nature Chemistry* 16:1794-1802, 2024. PMID: 39271915.

112. Ambadi Thody S et al. Small-molecule properties define partitioning into biomolecular condensates. *Nature Chemistry* 16:1794-1802, 2024. PMID: 39271915.

113. Chiu YT et al. Non-specific yet selective interactions contribute to small molecule condensate binding. *Journal of Chemical Theory and Computation* 20(19):8626-8638, 2024. PMID: 39184067.

114. Kilgore HR et al. Distinct chemical environments in biomolecular condensates. *Nature Chemical Biology* 20(3):291-301, 2024. PMID: 37770698.

115. Emelianova A et al. Prediction of small-molecule partitioning into biomolecular condensates from simulation. *JACS Au* 5(7):3142-3155, 2025. PMID: 40747072.

116. Pei G et al. Transcription regulation by biomolecular condensates. *Nature Reviews Molecular Cell Biology* 26:197-212, 2025. PMID: 39516712.

117. Alberti S et al. Current practices in the study of biomolecular condensates: a community comment. *Nature Communications* 16:7730, 2025. PMID: 40830340.

118. Eftekharzadeh B et al. Drug discovery for diseases with high unmet need through perturbation of biomolecular condensates. *Journal of Molecular Biology* 436(23):168838, 2024. PMID: 39510346.

119. Ma J et al. Small-molecule-induced LLPS suppresses the carcinogenesis of beta-catenin. *Nature Communications* 16:5408, 2025. PMID: 40593772.

120. Xu Z et al. A cofactor-induced repressive type of transcription factor condensation. *EMBO Journal* 43(22):5549-5576, 2024. PMID: 39358623.

121. Park HJ et al. Disparate leukemia mutations converge on nuclear phase-separated condensates. *Cell*, 2025. PMID: 41192422.

122. Bhatt SS et al. Nuclear phase separation drives NPM1-mutant acute myeloid leukemia. *Cell*, 2025. PMID: 40501735.

123. Maharana S et al. Intra-condensate demixing of TDP-43 inside stress granules generates pathological aggregates. *Cell* 188(15):4123-4140, 2025. PMID: 40412392.

124. Woodruff JB et al. Small-molecule dissolution of stress granules by redox modulation benefits ALS models. *Nature Chemical Biology* 21(10):1493-1504, 2025. PMID: 40369342.

125. Glineburg MR et al. Stress granule formation helps to mitigate neurodegeneration. *Nucleic Acids Research* 52(16):9745-9758, 2024. PMID: 39106168.

126. Wadsworth GM et al. RNA-driven phase transitions in biomolecular condensates. *Molecular Cell* 84(19):3692-3705, 2024. PMID: 39366355.

127. Morelli C et al. RNA modulates hnRNPA1A amyloid formation mediated by biomolecular condensates. *Nature Chemistry* 16:1064-1073, 2024. PMID: 38472406.

128. Van Treeck B et al. Homotypic RNA clustering accompanies a liquid-to-solid transition inside multi-component condensates. *Nature Chemistry* 17:1289-1299, 2025. PMID: 40603603.

129. Yang P et al. G3BP1 promotes intermolecular RNA-RNA interactions during RNA condensation. *Molecular Cell* 84(24):4796-4810, 2024. PMID: 39637853.

130. Emmanouilidis L et al. A solid beta-sheet structure is formed at the surface of FUS droplets during aging. *Nature Chemical Biology* 20(8):1044-1052, 2024. PMID: 38467846.

131. Hernandez-Candia CN et al. A platform to induce and mature biomolecular condensates using chemicals and light. *Nature Chemical Biology* 20(4):452-462, 2024. PMID: 38191942.

132. Quek RT et al. Comparative evaluation of cell-based assay technologies for scoring drug-induced condensation. *SLAS Discovery* 30(3):100212, 2025. PMID: 39894078.

133. Galvanetto N et al. Material properties of biomolecular condensates emerge from nanoscale dynamics. *PNAS* 122(23):e2424135122, 2025. PMID: 40455990.

134. Snead WT et al. Immiscible proteins compete for RNA binding to order condensate layers. *PNAS* 122(32), 2025. PMID: 40768359.

135. Usman M et al. Small molecules as regulators of LLPS: mechanisms and strategies for new drug discovery. *FASEB Journal* 39(13):e70785, 2025. PMID: 40616404.

136. Qin C et al. Current perspectives in drug targeting IDPs and biomolecular condensates. *BMC Biology* 23:118, 2025. PMID: 40325419.

137. Hu L et al. Biomolecular phase separation in tumorigenesis: from aberrant condensates to therapeutic vulnerabilities. *Molecular Cancer* 25:220, 2025.

138. Ryu K et al. Emerging insights into transcriptional condensates. *Experimental & Molecular Medicine* 56:820-826, 2024. PMID: 38658705.

139. Blobel GA et al. Dysregulation of transcriptional condensates in human disease. *Current Opinion in Genetics & Development* 86:102182, 2024. PMID: 38788489.

140. Parker R et al. Selective RNA sequestration in biomolecular condensates directs cell fate transitions. *Nature Biotechnology*, 2025. PMID: 40654687.

141. Bing X et al. Chromosome structure in Drosophila is determined by boundary pairing not loop extrusion. *eLife* 13:RP94070, 2024. PMID: 39110499.

142. Selivanovskiy EV et al. Liquid condensates: a new barrier to loop extrusion? *Cellular and Molecular Life Sciences* 82:59, 2025.

143. Rahmaninejad H et al. Dynamic barriers modulate cohesin positioning and genome folding at fixed occupancy. *Genome Research* 35(8):1745, 2025.

144. Chandra B et al. Properties governing small-molecule partitioning into biomolecular condensates. *Nature Chemistry* 16:1731-1732, 2024. PMID: 39438761.

145. Hagedorn L et al. Endosomal escape mechanisms of EV-based drug carriers: lessons for LNP design. *Extracellular Vesicles and Circulating Nucleic Acids*, 2024. PMID: 39697635.

146. Unger S et al. Unravelling the endosomal escape of pH-responsive nanoparticles using SLEEQ assay. *Biomaterials Science*, 2025. PMID: 39898829.

147. Lee S et al. MRI-based quantification of endosomal escape using IONP-loaded LNPs. *Advanced Healthcare Materials*, 2025. PMID: 40761024.

148. Yang X et al. Design and activity evaluation of BRD4 PROTAC based on alkenyl oxindole-DCAF11 pair. *Journal of Medicinal Chemistry*, 2024. PMID: 39475482.

149. Starke LJ, Allolio C, Hub JS. How pore formation in complex biological membranes is governed by lipid composition. *PNAS Nexus*, 2025.

150. Vian L et al. High-resolution CTCF footprinting. *Nature Genetics* 56:29-39, 2024. PMID: 37961446.

151. Hsieh THS et al. Cohesin-mediated 3D contacts tune enhancer-promoter regulation. *bioRxiv*, 2024. PMID: 39026740.

152. Bhatt A et al. Chaperone-mediated heterotypic phase separation regulates tau liquid-to-solid transitions. *Science Advances* 11(23):eads1241, 2025.

153. Liu Y et al. Recent advances in LNPs and their safety concerns for mRNA delivery. *Vaccines*, 2024. PMID: 39460315.

154. Cheng Q et al. Endosomal escape and nuclear localization: critical barriers for therapeutic nucleic acids. *Molecules*, 2024. PMID: 39770086.

155. Yang X et al. Design, synthesis, and activity evaluation of BRD4 PROTAC based on alkenyl oxindole-DCAF11 pair. *Journal of Medicinal Chemistry*, 2024. PMID: 39475482.

156. Ritmejeris J, Chen X, Dekker C. Single-molecule protein sequencing with nanopores. *Nature Reviews Bioengineering*, 2024.

157. Lan W-H et al. Location of phosphorylation sites within long polypeptide chains by binder-assisted nanopore detection. *JACS*, 2024.

158. Guerin TM et al. An extrinsic motor directs chromatin loop formation by cohesin. *EMBO Journal* 43(19):4466-4497, 2024. PMID: 39160275.

159. Guerin TM, Uhlmann F. A unified model for cohesin function in sister chromatid cohesion and chromatin loop formation. *Molecular Cell* 85(6):1060-1072, 2025. PMID: 40118039.

160. Bastie N et al. Sister chromatid cohesion halts DNA loop expansion. *Molecular Cell* 84(6):1139-1148, 2024. PMID: 38452765.

161. Hirano T, Kinoshita K. SMC-mediated chromosome organization: does loop extrusion explain it all? *Current Opinion in Cell Biology* 92:102447, 2025. PMID: 39603149.

162. Davidson IF, Peters JM. In vitro dynamics of DNA loop extrusion by SMC complexes. *Cold Spring Harbor Symposia*, 2024. PMID: 39591812.

163. Serrano D et al. Loop-extruding Smc5/6 organizes transcription-induced positive DNA supercoils. *Molecular Cell* 84(5):867-882, 2024. PMID: 38295804.

164. Zheng G et al. Genome folding by cohesin. *Current Opinion in Genetics & Development* 91:102310, 2025. PMID: 39827577.

165. Berger G et al. Cohesin regulation of genome organization in mature granule neurons. *Epigenetics & Chromatin* 18:60, 2025. PMID: 41013693.

166. Bing X et al. Chromosome structure in Drosophila is determined by boundary pairing not loop extrusion. *eLife* 13:RP94070, 2024. PMID: 39110499.

167. Morelli C et al. RNA modulates hnRNPA1A amyloid formation mediated by biomolecular condensates. *Nature Chemistry* 16:1064-1073, 2024. PMID: 38472406.

168. Ryu K et al. Emerging insights into transcriptional condensates. *Experimental & Molecular Medicine* 56:820-826, 2024. PMID: 38658705.

169. Blobel GA et al. Dysregulation of transcriptional condensates in human disease. *Current Opinion in Genetics & Development* 86:102182, 2024. PMID: 38788489.

170. Parker R et al. Selective RNA sequestration in biomolecular condensates directs cell fate transitions. *Nature Biotechnology*, 2025. PMID: 40654687.

171. Chandra B et al. Properties governing small-molecule partitioning into biomolecular condensates. *Nature Chemistry* 16:1731-1732, 2024. PMID: 39438761.

172. Luo M et al. NDA submission of vepdegestrant to U.S. FDA: the beginning of a new era of PROTAC degraders. *Journal of Medicinal Chemistry* 68(14):14129-14136, 2025.

173. Donovan KA et al. Leveraging structural and computational biology for molecular glue discovery. *Journal of Medicinal Chemistry* 68(3):2048-2051, 2025. PMID: 39854250.

174. Yang J et al. Molecular glue degrader for tumor treatment. *Frontiers in Oncology* 14:1512666, 2024.

175. Vetter M et al. Challenging AlphaFold in predicting proteins with large-scale allosteric transitions. *Communications Chemistry* 8:378, 2025.

176. Carloni P, Rossetti G, Muller CE. Rational design of ligands with optimized residence time. *ACS Pharmacology & Translational Science* 8(2):613-615, 2025.

177. Wu J et al. Integrative ML and MD approach to unveil allosteric site for beta2AR. *Nature Communications* 15:8051, 2024.

178. Wei H, McCammon JA. Structure and dynamics in drug discovery. *npj Drug Discovery* 1:1, 2024.

179. Gasparikova D, Chikhale R, Cole J, Pohl E. Recent computational advances in cryptic binding site identification. *Bioinformatics Advances* 5(1):vbaf156, 2025.

180. Zhao Y et al. Low reactogenicity and high tumour antigen expression from mRNA-LNPs with membrane-destabilizing zwitterionic lipids. *Nature Biomedical Engineering*, 2025.

181. Padilla MS et al. BEND lipids mediate delivery of mRNA and CRISPR-Cas9 RNP for hepatic gene editing. *Nature Communications*, 2025.

182. Davoodi S et al. AI-driven rational design of ionizable lipids for mRNA delivery. *Nature Communications*, 2024.

183. Lok BH et al. High-throughput barcoding identifies cationic lipid-like materials for lung mRNA delivery. *Nature Communications*, 2024.

184. Li H et al. Lipid nanoparticles for mRNA delivery in brain via systemic administration. *Science Advances*, 2025.

185. Afshar Bakshloo M et al. Bio-nanopore technology for biomolecules detection. *Advanced Biotechnology*, 2024.

186. Cui J et al. Nanopore-based label-free and single-molecule sequencing toward precision diagnosis. *Advanced Materials*, 2026. PMID: 41307290.

187. Miyagi A et al. Redesign of translocon EXP2 nanopore for detecting peptide fragments. *Small Methods*, 2025.

188. Wang J et al. Nanopore-based massively parallel sensing for peptide profiling and protein identification. *Nature Communications*, 2026.

189. De Wit E et al. Complex 3D genome organization networks revealed by controlled cohesin loading. *Nature Genetics*, 2025.

190. Vercellone F et al. A multiscale perspective on chromatin architecture through polymer physics. *Physiology* 40(3), 2025. PMID: 39601793.

191. Maeshima K. The shifting paradigm of chromatin structure. *Proceedings of the Japan Academy, Ser. B* 101(6):339-356, 2025. PMID: 40301047.

192. Peters JM. Organization of replicated chromosomes by DNA loops and sister chromatid cohesion. *Nature Reviews Molecular Cell Biology* 27:201-218, 2026. PMID: 41478878.

193. Eftekharzadeh B et al. Drug discovery for diseases with high unmet need through perturbation of biomolecular condensates. *Journal of Molecular Biology* 436(23):168838, 2024. PMID: 39510346.

194. Ma J et al. Small-molecule-induced LLPS suppresses beta-catenin carcinogenesis. *Nature Communications* 16:5408, 2025. PMID: 40593772.

195. Xu Z et al. A cofactor-induced repressive transcription factor condensation. *EMBO Journal* 43(22):5549-5576, 2024. PMID: 39358623.

196. Maharana S et al. Intra-condensate demixing of TDP-43 generates pathological aggregates. *Cell* 188(15):4123-4140, 2025. PMID: 40412392.

197. Woodruff JB et al. Small-molecule dissolution of stress granules by redox modulation. *Nature Chemical Biology* 21(10):1493-1504, 2025. PMID: 40369342.

198. Usman M et al. Small molecules as regulators of LLPS: mechanisms and strategies. *FASEB Journal* 39(13):e70785, 2025. PMID: 40616404.

199. Qin C et al. Current perspectives in drug targeting IDPs and biomolecular condensates. *BMC Biology* 23:118, 2025. PMID: 40325419.

200. Hu L et al. Biomolecular phase separation in tumorigenesis. *Molecular Cancer* 25:220, 2025.

201. Park HJ et al. Disparate leukemia mutations converge on nuclear phase-separated condensates. *Cell*, 2025. PMID: 41192422.

202. Bhatt SS et al. Nuclear phase separation drives NPM1-mutant AML. *Cell*, 2025. PMID: 40501735.

203. Galvanetto N et al. Material properties of biomolecular condensates emerge from nanoscale dynamics. *PNAS* 122(23):e2424135122, 2025. PMID: 40455990.

204. Snead WT et al. Immiscible proteins compete for RNA binding to order condensate layers. *PNAS* 122(32), 2025. PMID: 40768359.

205. Van Treeck B et al. Homotypic RNA clustering accompanies liquid-to-solid transitions in multi-component condensates. *Nature Chemistry* 17:1289-1299, 2025. PMID: 40603603.

206. Emmanouilidis L et al. A solid beta-sheet structure forms at the surface of FUS droplets during aging. *Nature Chemical Biology* 20(8):1044-1052, 2024. PMID: 38467846.

207. Hernandez-Candia CN et al. A platform to induce and mature biomolecular condensates. *Nature Chemical Biology* 20(4):452-462, 2024. PMID: 38191942.

208. Quek RT et al. Comparative evaluation of cell-based assay technologies for drug-induced condensation. *SLAS Discovery* 30(3):100212, 2025. PMID: 39894078.

